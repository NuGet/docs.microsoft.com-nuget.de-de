---
title: Festlegung von Zielversionen für NuGet-Pakete
description: Beschreibung der verschiedenen Methoden für die Ausrichtung mehrerer .NET Framework-Versionen aus einem einzelnen NuGet-Paket.
author: JonDouglas
ms.author: jodou
ms.date: 07/15/2019
ms.topic: conceptual
ms.openlocfilehash: e919b11670589900d9e588db33fd68b8df592ac2
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774561"
---
# <a name="support-multiple-net-versions"></a>Unterstützung für mehrere .NET-Versionen

Viele Bibliotheken sind auf eine bestimmte Version von .NET Framework ausgerichtet. So müssen Sie möglicherweise über eine für die UWP spezifische Version Ihrer Bibliothek sowie über eine weitere Version verfügen, die die Features in .NET Framework 4.6 nutzt. Dafür unterstützt NuGet das Platzieren mehrerer Versionen derselben Bibliothek in einem einzelnen Paket.

Dieser Artikel beschreibt das Layout eines NuGet-Pakets, unabhängig davon, wie das Paket oder die Assemblys aufgebaut sind (d. h. das Layout ist das gleiche, unabhängig davon, ob mehrere *.csproj*-Dateien im Nicht-SDK-Stil und eine benutzerdefinierte *.nuspec*-Datei oder eine einzelne *.csproj*-Datei im SDK-Stil mit mehreren Zielen verwendet werden). Für ein Projekt im SDK-Stil weiß NuGet-[pack targets](../reference/msbuild-targets.md), wie das Paket gestaltet sein muss, und automatisiert das Einfügen der Assemblys in die richtigen lib-Ordner und das Erstellen von Abhängigkeitsgruppen für jedes Zielframework (TFM). Ausführliche Anweisungen finden Sie unter [Unterstützung mehrerer .NET Framework-Versionen in der Projektdatei](multiple-target-frameworks-project-file.md).

Sie müssen das Paket manuell gestalten, wie in diesem Artikel beschrieben, wenn Sie die unter [Erstellen eines Pakets](../create-packages/creating-a-package.md#from-a-convention-based-working-directory) beschriebene konventionsbasierte Arbeitsverzeichnismethode verwenden. Für ein Projekt im SDK-Stil wird die automatisierte Methode empfohlen. Sie können das Paket aber auch manuell gestalten, wie in diesem Artikel beschrieben.

## <a name="framework-version-folder-structure"></a>Ordnerstruktur der Frameworkversion

Beim Erstellen eines Pakets, das nur eine Version einer Bibliothek enthält oder mehrere Frameworks ansteuert, müssen Sie unter `lib` immer Unterordner erstellen und dabei verschiedene Frameworknamen unter Beachtung der Groß-/Kleinschreibung mit der folgenden Konvention verwenden:

```
lib\{framework name}[{version}]
```

Eine vollständige Liste der unterstützten Namen finden Sie in der Referenz zu [Zielframeworks](../reference/target-frameworks.md#supported-frameworks).

Sie sollten niemals über eine Version der Bibliothek verfügen, die für ein Framework nicht spezifisch ist und direkt im Stammordner `lib` angeordnet ist. (Diese Funktion wurde nur mit `packages.config` unterstützt.) Dadurch kann eine mit einem beliebigen Zielframework kompatible Bibliothek überall installiert werden. Dies würde vermutlich zu unerwarteten Laufzeitfehlern führen. Das Hinzufügen von Assemblys im Stammordner (z.B. `lib\abc.dll`) oder in Unterordnern (z.B. `lib\abc\abc.dll`) wurde als veraltete gekennzeichnet und wird bei Verwendung des PackagesReference-Formats ignoriert.

Die folgende Ordnerstruktur unterstützt beispielsweise vier frameworkspezifische Versionen einer Assembly:

```
\lib
    \net46
        \MyAssembly.dll
    \net461
        \MyAssembly.dll
    \uap
        \MyAssembly.dll
    \netcore
        \MyAssembly.dll
```

Verwenden Sie den rekursiven Platzhalter `**` im Abschnitt `<files>` Ihrer `.nuspec`-Datei, damit alle diese Dateien bei der Erstellung des Pakets problemlos eingeschlossen werden können:

```xml
<files>
    <file src="lib\**" target="lib/{framework name}[{version}]" />
</files>
```

### <a name="architecture-specific-folders"></a>Architekturspezifische Ordner

Wenn Sie über architekturspezifische Assemblys verfügen, d.h. separate Assemblys, die ARM, x86 und x64 ansteuern, müssen Sie diese in einem Ordner mit dem Namen `runtimes` in dem Unterordner `{platform}-{architecture}\lib\{framework}` oder `{platform}-{architecture}\native` anordnen. Beispielsweise würden in der folgenden Ordnerstruktur native und verwaltete DLLs untergebracht, die Windows 10 und das Framework `uap10.0` ansteuern:

```
\runtimes
    \win10-arm
        \native
        \lib\uap10.0
    \win10-x86
        \native
        \lib\uap10.0
    \win10-x64
        \native
        \lib\uap10.0
```

Diese Assemblys sind nur zur Laufzeit verfügbar. Wenn Sie also auch die entsprechende Assembly für die Kompilierzeit bereitstellen möchten, speichern Sie die `AnyCPU`-Assembly im Ordner `/ref/{tfm}`. 

Beachten Sie Folgendes: NuGet wählt diese Ressourcen für die Kompilier- oder Laufzeit immer aus einem einzigen Ordner aus. Wenn also beim Hinzufügen von Assemblys für die Kompilierzeit kompatible Ressourcen aus `/ref` verfügbar sind, wird `/lib` ignoriert. Ebenso gilt: Wenn kompatible Ressourcen aus `/runtimes` verfügbar sind, wird `/lib` für die Laufzeit ebenfalls ignoriert.

Unter [Create UWP Packages (Erstellen von UWP-Paketen)](../guides/create-uwp-packages.md) finden Sie ein Beispiel für den Verweis auf diese Dateien im `.nuspec`-Manifest.

Weitere Informationen finden Sie auch unter [Packing a Windows store app component with NuGet](/archive/blogs/mim/packaging-a-windows-store-apps-component-with-nuget-part-2) (Packen einer Windows Store-App-Komponente mit NuGet).

## <a name="matching-assembly-versions-and-the-target-framework-in-a-project"></a>Abgleichen von Assemblyversionen und dem Zielframework in einem Projekt

Wenn NuGet ein Paket mit mehreren Assemblyversionen installiert, versucht es, die Frameworknamen der Assembly mit dem Zielframework des Projekts abzugleichen.

Wenn keine Übereinstimmung gefunden wird, kopiert NuGet, sofern verfügbar, die Assembly für die höchste Version, die kleiner oder gleich dem Zielframework des Projekts ist. Wenn keine kompatible Assembly gefunden wird, gibt NuGet eine entsprechende Fehlermeldung zurück.

Betrachten Sie beispielsweise die folgende Ordnerstruktur in einem Paket:

```
\lib
    \net45
        \MyAssembly.dll
    \net461
        \MyAssembly.dll
```

Bei der Installation dieses Pakets in einem Projekt für .NET Framework 4.6 installiert NuGet die Assembly in dem Ordner `net45`, da dies die höchste verfügbare Version ist, die kleiner oder gleich 4.6 ist.

Wenn das Projekt .NET Framework 4.6.1 ansteuert, installiert NuGet die Assembly wiederum im Ordner `net461`.

Wenn das Projekt .NET Framework 4.0 und frühere Versionen ansteuert, löst NuGet eine entsprechende Fehlermeldung aus, nach der die kompatible Assembly nicht gefunden werden kann.

## <a name="grouping-assemblies-by-framework-version"></a>Gruppieren von Assemblys nach Frameworkversion

NuGet kopiert Assemblys nur aus einem Bibliotheksordner im Paket. Angenommen beispielsweise, ein Paket weist die folgende Ordnerstruktur auf:

```
\lib
    \net40
        \MyAssembly.dll (v1.0)
        \MyAssembly.Core.dll (v1.0)
    \net45
        \MyAssembly.dll (v2.0)
```

Wenn das Paket in einem Projekt für .NET Framework 4.5 installiert wird, ist `MyAssembly.dll` (v2.0) die einzige installierte Assembly. `MyAssembly.Core.dll` (v1.0) wurde nicht installiert, da sie im Ordner `net45` nicht aufgeführt wird. Diese Verhaltensweise von NuGet ist darauf zurückzuführen, dass `MyAssembly.Core.dll` möglicherweise in Version 2.0 von `MyAssembly.dll` zusammengeführt wurde.

Wenn Sie möchten, dass `MyAssembly.Core.dll` für .NET Framework 4.5 installiert werden soll, fügen Sie eine Kopie in den Ordner `net45` ein.

## <a name="grouping-assemblies-by-framework-profile"></a>Gruppieren von Assemblys nach Frameworkprofil

NuGet unterstützt auch das Ansteuern eines bestimmten Frameworkprofils durch Anhängen eines Bindestrichs und des Profilnamens an das Ende des Ordners.

lib\{framework name}-{profile}

Die unterstützten Profile lauten wie folgt:

- `client`: Clientprofil
- `full`: Vollständiges Profil
- `wp`: Windows Phone
- `cf`: Compact Framework

## <a name="declaring-dependencies-advanced"></a>Deklarieren von Abhängigkeiten (Erweitert)

Beim Packen einer Projektdatei versucht NuGet, die Abhängigkeiten aus dem Projekt automatisch zu generieren. Die Informationen in diesem Abschnitt zur Verwendung einer *NUSPEC*-Datei zum Deklarieren von Abhängigkeiten sind in der Regel nur für erweiterte Szenarien erforderlich.

*(Version 2.0 und höher)*: Sie können Paketabhängigkeiten in der *NUSPEC*-Datei deklarieren, die dem Zielframework des Zielprojekts entspricht, indem Sie `<group>`-Elemente innerhalb des `<dependencies>`-Elements verwenden. Weitere Informationen finden Sie unter [dependencies-Element](../reference/nuspec.md#dependencies-element).

Jede Gruppe verfügt über ein Attribut mit dem Namen `targetFramework` und enthält entweder kein `<dependency>`-Element oder mindestens eins. Diese Abhängigkeiten werden zusammen installiert, wenn das Zielframework kompatibel mit dem Frameworkprofil des Projekts ist. Die genauen Frameworkbezeichner finden Sie unter [Zielframeworks](../reference/target-frameworks.md).

Es wird empfohlen, eine Gruppe pro Zielframeworkmoniker (TFM) für Dateien in den Ordnern *lib/* und *ref/* zu verwenden.

Im folgenden Beispiel werden verschiedene Variationen des `<group>`-Elements dargestellt:

```xml
<dependencies>

    <group targetFramework="net472">
        <dependency id="jQuery" version="1.10.2" />
        <dependency id="WebActivatorEx" version="2.2.0" />
    </group>

    <group targetFramework="net20">
    </group>

</dependencies>
```

## <a name="determining-which-nuget-target-to-use"></a>Bestimmen des zu verwendenden NuGet-Ziels

Beim Packen von Bibliotheken, die die portable Klassenbibliothek als Ziel verwenden, kann die Bestimmung des in Ihren Ordnernamen und in der `.nuspec`-Datei zu verwendenden NuGet-Ziels schwierig sein, insbesondere dann, wenn sich die Ansteuerung nur auf ein Subset der portablen Klassenbibliothek bezieht. Die folgenden externen Ressourcen helfen Ihnen dabei:

- [Framework-Profile in .NET](https://blog.stephencleary.com/2012/05/framework-profiles-in-net.html) (stephenclearly.com)
- [Portable Klassenbibliotheksprofile](https://embed.plnkr.co/03ck2dCtnJogBKHJ9EjY/preview) (plnkr.co): Tabelle, in der portable Klassenbibliotheksprofile und die entsprechenden NuGet-Ziele aufgezählt werden
- [Tool für portable Klassenbibliotheksprofile](https://github.com/StephenCleary/PortableLibraryProfiles) (github.com): Befehlszeilentool zum Bestimmen der auf Ihrem System verfügbaren portablen Klassenbibliotheksprofile

## <a name="content-files-and-powershell-scripts"></a>Inhaltsdateien und PowerShell-Skripts

> [!Warning]
> Änderbare Inhaltsdateien und die Skriptausführung sind nur im Format `packages.config` verfügbar. In allen anderen Formaten sind sie veraltet und sollten nicht für neue Pakete verwendet werden.

Bei `packages.config` können Inhaltsdateien und PowerShell-Skripts mit der gleichen Ordnerkonvention in den Ordnern `content` und `tools` nach Zielframework gruppiert werden. Beispiel:

```
\content
    \net46
        \MyContent.txt
    \net461
        \MyContent461.txt
    \uap
        \MyUWPContent.html
    \netcore
\tools
    init.ps1
    \net46
        install.ps1
        uninstall.ps1
    \uap
        install.ps1
        uninstall.ps1
```

Wenn ein Frameworkordner leer bleibt, fügt NuGet keine Assemblyverweise oder Inhaltsdateien hinzu oder führt die PowerShell-Skripts für dieses Framework aus.

> [!Note]
> Da `init.ps1` auf der Projektmappenebene und nicht abhängig von dem Projekt ausgeführt wird, muss das Skript direkt unter dem Ordner `tools` angeordnet werden. Es wird ignoriert, wenn es unter einem Frameworkordner angeordnet wird.