---
title: Erstellen eines NuGet-Pakets | Microsoft-Dokumentation
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/12/2017
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Eine ausführliche Anleitung zum Entwerfen und Erstellen eines NuGet-Pakets, einschließlich der wichtigsten Entscheidungspunkte wie Dateien und Versionsverwaltung
keywords: Erstellen von NuGet-Paketen, Erstellen eines Pakets, NUSPEC-Manifest, NuGet-Paketkonventionen, Version des NuGet-Pakets
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 7bb7e16a317aff908effe0b6c603ea53c9e8a563
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="creating-nuget-packages"></a>Erstellen von NuGet-Paketen

Unabhängig davon, was Ihr Paket macht oder welchen Code es enthält, können Sie die Funktionalität mit `nuget.exe` in eine Komponente packen, die für andere Entwickler freigegeben und von ihnen verwendet werden kann. Weitere Informationen zum Installieren von `nuget.exe` finden Sie unter [Install NuGet CLI (Installieren der NuGet-CLI)](../install-nuget-client-tools.md#nugetexe-cli). Beachten Sie, dass `nuget.exe` nicht automatisch in Visual Studio enthalten ist.

Technisch gesehen ist ein NuGet-Paket eine ZIP-Datei, die mit der `.nupkg`-Erweiterung umbenannt wurde und deren Inhalt bestimmten Konventionen entspricht. In diesem Thema werden die Schritte zum Erstellen eines Pakets, das diesen Konventionen entspricht, ausführlich beschrieben. Eine fokussierte exemplarische Vorgehensweise finden Sie unter [Quickstart: Create and Publish a Package (Schnellstart: Erstellen und Veröffentlichen eines Pakets)](../quickstart/create-and-publish-a-package.md).

Das Packen beginnt mit dem kompilierten Code (Assemblys), Symbolen und/oder anderen Dateien, die Sie als Paket übermitteln möchten. Weitere Informationen finden Sie unter [Overview and workflow (Übersicht und Workflow)](overview-and-workflow.md). Dieser Vorgang wird unabhängig vom Kompilieren oder jeder anderen Methode zum Erstellen der Dateien ausgeführt, die in das Paket gepackt werden. Sie können die kompilierten Assemblys und Pakete jedoch mithilfe der Informationen in einer Projektdatei kontinuierlich synchronisieren.

> [!Note]
> Dieses Thema gilt nicht für .NET Core-Projekte, in denen Visual Studio 2017 und NuGet 4.0 und höher verwendet wurde. In diesen .NET-Projekten verwendet NuGet die Informationen direkt in der Projektdatei. Weitere Informationen finden Sie unter [Create .NET Standard Packages with Visual Studio 2017 (Erstellen von .NET Standard-Paketen mit Visual Studio 2017)](../guides/create-net-standard-packages-vs2017.md) und [NuGet pack and restore as MSBuild targets (NuGet-Befehle „pack“ und „restore“ als MSBuild-Ziele)](../reference/msbuild-targets.md).

## <a name="deciding-which-assemblies-to-package"></a>Welche Assemblys sollen gepackt werden?

Die meisten allgemeinen Pakete enthalten mindestens eine Assembly, die andere Entwickler in ihren eigenen Projekten verwenden können.

- Es ist empfehlenswert, in jedem NuGet-Paket eine Assembly zu haben, vorausgesetzt, dass jede Assembly für sich nützlich ist. Beispiel: Wenn `Utilities.dll` von `Parser.dll` abhängt und `Parser.dll` für sich allein bereits nützlich ist, dann müssen Sie für jede Datei ein eigenes Paket erstellen. So können Entwickler `Parser.dll` unabhängig von `Utilities.dll` verwenden.

- Wenn Ihre Bibliothek aus mehreren Assemblys besteht, die für sich allein nicht nützlich sind, können diese in einem Paket zusammengefasst werden. Bleiben wir beim vorherigen Beispiel: Wenn `Parser.dll` Code enthält, der nur von `Utilities.dll` verwendet wird, kann `Parser.dll` in dasselbe Paket eingefügt werden.

- Auch `Utilities.dll` und `Utilities.resources.dll` können im selben Paket zusammengefasst werden, wenn erstere DLL von der letzteren abhängt und die letztere nicht für sich allein nützlich ist.

Ressourcen hingegen sind ein besonderer Fall. Wenn ein Paket in einem Projekt installiert wird, fügt NuGet automatisch den DLLs des Pakets Assemblyverweise hinzu. Die Verweise, die mit `.resources.dll` benannt sind, werden dabei allerdings *nicht* hinzugefügt, da angenommen wird, dass es sich dabei um lokalisierte Satellitenassemblys handelt. Weitere Informationen finden Sie unter [Creating localized NuGet packages (Erstellen lokalisierter NuGet-Pakete)](creating-localized-packages.md). Vermeiden Sie aus diesem Grund die Verwendung von `.resources.dll` für Dateien, die darüber hinaus wichtigen Paketcode enthalten.

Wenn Ihre Bibliothek COM-Interop-Assemblys enthält, führen Sie die zusätzlichen Schritte unter [Erstellen von Paketen, die COM-Interop-Assemblys enthalten](#authoring-packages-with-com-interop-assemblies) aus.

## <a name="the-role-and-structure-of-the-nuspec-file"></a>Rolle und Struktur der NUSPEC-Datei

Nachdem Sie entschieden haben, welche Dateien gepackt werden sollen, erstellen Sie ein Paketmanifest in einer `.nuspec`-XML-Datei.

Das Manifest:

1. Beschreibt den Inhalt des Pakets und ist im Paket enthalten.
1. Ist unerlässlich für die Erstellung des Pakets und weist NuGet an, wie das Paket in ein Projekt installiert werden soll. Das Manifest erkennt z.B. andere Paketabhängigkeiten, sodass NuGet bei der Installation des Hauptpakets auch diese installieren kann.
1. Enthält wie unten beschrieben erforderliche und optionale Eigenschaften. Weitere Informationen, einschließlich anderer Eigenschaften, die hier nicht erwähnt werden, finden Sie unter [.nuspec reference (NUSPEC-Referenz)](../reference/nuspec.md).

Erforderliche Eigenschaften:

- Der Paketbezeichner. Dieser muss im Katalog, der das Paket hostet, eindeutig sein.
- Eine bestimmte Versionsnummer in der Schreibweise *Hauptversion.Nebenversion.Patch[-Suffix]*, wobei im *-Suffix* die [Vorabversionen](prerelease-packages.md) angegeben werden
- Der Titel des Pakets, so wie er auf dem Host (z.B. „nuget.org“) angezeigt werden sollte
- Informationen zum Autor und zum Besitzer
- Eine ausführliche Beschreibung des Pakets

Allgemeine optionale Eigenschaften:

- Anmerkungen zu diesem Release
- Copyrightinformationen
- Eine kurze Beschreibung der [Paket-Manager-UI in Visual Studio](../tools/package-manager-ui.md)
- Eine Gebietsschema-ID
- URL der Startseite und der Lizenz
- Eine URL für das Symbol
- Listen der Abhängigkeiten und Verweise
- Tags für die Katalogsuche

Im folgenden Beispiel sehen Sie eine typische, aber fiktive `.nuspec`-Datei mit Kommentaren, die die Eigenschaften beschreiben:

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2013/05/nuspec.xsd">
    <metadata>
    <!-- The identifier that must be unique within the hosting gallery -->
    <id>Contoso.Utility.UsefulStuff</id>

    <!-- The package version number that is used when resolving dependencies -->
    <version>1.8.3-beta</version>

    <!-- Authors contain text that appears directly on the gallery -->
    <authors>Dejana Tesic, Rajeev Dey</authors>

    <!-- Owners are typically nuget.org identities that allow gallery
            users to easily find other packages by the same owners.  -->
    <owners>dejanatc, rjdey</owners>

    <!-- License and project URLs provide links for the gallery -->
    <licenseUrl>http://opensource.org/licenses/MS-PL</licenseUrl>
    <projectUrl>http://github.com/contoso/UsefulStuff</projectUrl>

    <!-- The icon is used in Visual Studio's package manager UI -->
    <iconUrl>http://github.com/contoso/UsefulStuff/nuget_icon.png</iconUrl>

    <!-- If true, this value prompts the user to accept the license when
            installing the package. -->
    <requireLicenseAcceptance>false</requireLicenseAcceptance>

    <!-- Any details about this particular release -->
    <releaseNotes>Bug fixes and performance improvements</releaseNotes>

    <!-- The description can be used in package manager UI. Note that the
            nuget.org gallery uses information you add in the portal. -->
    <description>Core utility functions for web applications</description>

    <!-- Copyright information -->
    <copyright>Copyright ©2016 Contoso Corporation</copyright>

    <!-- Tags appear in the gallery and can be used for tag searches -->
    <tags>web utility http json url parsing</tags>

    <!-- Dependencies are automatically installed when the package is installed -->
    <dependencies>
        <dependency id="Newtonsoft.Json" version="9.0" />
    </dependencies>
    </metadata>

    <!-- A readme.txt to display when the package is installed -->
    <files>
        <file src="readme.txt" target="" />
    </files>
</package>
```

Weitere Informationen zum Deklarieren von Abhängigkeiten und zum Angeben von Versionsnummern finden Sie unter [Package versioning (Paketversionsverwaltung)](../reference/package-versioning.md). Es ist auch möglich, Ressourcen aus Abhängigkeiten mithilfe der Attribute `include` und `exclude` des Elements `dependency` direkt im Paket verfügbar zu machen. Informationen dazu finden Sie unter [.nuspec Reference – Dependencies (NUSPEC-Referenz: Abhängigkeiten)](../reference/nuspec.md#dependencies).

Da das Manifest im Paket enthalten ist, aus dem es erstellt wurde, finden Sie viele weitere Beispiele in den vorhandenen Paketen. Eine gute Quelle ist z.B. der Ordner *global-packages* auf Ihrem Computer, der sich mithilfe des folgenden Befehls öffnen lässt:

```cli
nuget locals -list global-packages
```

Wechseln Sie in einen Ordner unter *package\version*, kopieren die `.nupkg`- in eine `.zip`-Datei, öffnen Sie dann die `.zip`-Datei, und sehen Sie sich die `.nuspec`-Datei darin an.

> [!Note]
> Wenn Sie eine `.nuspec`-Datei aus einem Visual Studio-Projekt erstellen, enthält das Manifest Tokens, die bei der Paketerstellung durch Informationen aus dem Projekt ersetzt werden. Weitere Informationen finden Sie im Abschnitt [Aus einem Visual Studio-Projekt](#from-a-visual-studio-project).

## <a name="creating-the-nuspec-file"></a>Erstellen der NUSPEC-Datei

Das Erstellen eines vollständigen Manifests beginnt in der Regel mit einer einfachen `.nuspec`-Datei, die mithilfe einer der folgenden Methoden generiert wird:

- [einem konventionsbasierten Arbeitsverzeichnis](#from-a-convention-based-working-directory)
- [einer Assembly-DLL](#from-an-assembly-dll)
- [einem Visual Studio-Projekt](#from-a-visual-studio-project)    
- [einer neuen Datei mit Standardwerten](#new-file-with-default-values)

Anschließend bearbeiten Sie die Datei manuell, sodass sie den genauen Inhalt beschreibt, den das letzte Paket enthalten soll.

> [!Important]
> Generierte `.nuspec`-Dateien enthalten Platzhalter. Diese müssen geändert werden, bevor das Paket mit dem Befehl `nuget pack` erstellt wird, da dieser fehlschlägt, wenn die `.nuspec`-Datei Platzhalter enthält.

### <a name="from-a-convention-based-working-directory"></a>Aus einem konventionsbasierten Arbeitsverzeichnis

Da ein NuGet-Paket nur eine mit der `.nupkg`-Erweiterung umbenannte ZIP-Datei ist, ist es oftmals am einfachsten, die gewünschte Ordnerstruktur im Dateisystem und die `.nuspec`-Datei anschließend direkt aus dieser Struktur zu erstellen. Der Befehl `nuget pack` fügt dann automatisch alle Dateien in dieser Ordnerstruktur ein (außer den Ordnern, die mit einem `.` beginnen, sodass private Dateien in der gleichen Struktur bleiben können).

Der Vorteil dieses Ansatzes ist, dass Sie nicht wie weiter unten in diesem Thema erläutert im Manifest angeben müssen, welche Dateien im Paket enthalten sein sollen. Sie können einfach beim Buildprozess die genaue Ordnerstruktur für das Paket erstellen lassen und problemlos weitere Dateien aufnehmen, die andernfalls zu keinem Projekt gehören würden:

- Inhalt und Quellcode, der in das Zielprojekt eingefügt werden soll.
- PowerShell-Skripts (in NuGet 2.x verwendete Pakete können auch Installationsskripts enthalten, die in NuGet 3.x und höher nicht unterstützt werden).
- Transformationen in vorhandene Konfigurations- und Quellcodedateien in einem Projekt.

Die Ordnerkonventionen lauten folgendermaßen:

| Ordner | description | Aktion bei der Paketinstallation |
| --- | --- | --- |
| (Stammverzeichnis) | Speicherort für „readme.txt“ | In Visual Studio wird die Datei „readme.txt“ im Stammverzeichnis des Pakets angezeigt, wenn das Paket installiert wird. |
| lib/{tfm} | Assembly- (`.dll`), Dokumentations- (`.xml`) und Symboldateien (`.pdb`) für den angegebenen Zielframeworkmoniker (Target Framework Moniker, TFM) | Assemblys werden als Verweise hinzugefügt, und `.xml` sowie `.pdb` werden in Projektordner kopiert. Informationen zum Erstellen von für das Zielframework spezifischen Unterordnern finden Sie unter [Supporting multiple .NET framework versions (Unterstützen mehrerer .NET Framework-Versionen)](supporting-multiple-target-frameworks.md). |
| Laufzeiten | Architekturspezifische Assembly- (`.dll`), Symbol- (`.pdb`) und native Ressourcendateien (`.pri`) | Assemblys werden als Verweise hinzugefügt. Andere Dateien werden in Projektordner kopiert. Weitere Informationen finden Sie unter [Supporting multiple .NET framework versions (Unterstützen mehrerer .NET Framework-Versionen)](supporting-multiple-target-frameworks.md). |
| Inhalt | Beliebige Dateien | Inhalte werden in das Projektstammverzeichnis kopiert. Der Ordner **content** (Inhalt) entspricht in etwa dem Stammverzeichnis der Zielanwendung, die das Paket letztendlich nutzt. Damit das Paket dem Ordner */images* der Anwendung ein Image hinzufügt, müssen Sie es im Ordner *content/images* ablegen. |
| Build | MSBuild-Dateien `.targets` und `.props` | Sie werden automatisch in die Projektdatei oder in `project.lock.json` (NuGet 3.x und höher) eingefügt. |
| Tools | PowerShell-Skripts und -Programme, auf die über die Paket-Manager-Konsole zugegriffen werden kann | Der Ordner `tools` wird nur zur Umgebungsvariable `PATH` der Paket-Manager-Konsole hinzugefügt, *niemals* jedoch zu `PATH`, so wie es für MSBuild beim Erstellen des Projekts festgelegt ist. |

Da die Ordnerstruktur beliebig viele Assemblys für beliebig viele Zielframeworks enthalten kann, ist diese Methode für das Erstellen von Paketen erforderlich, die mehrere Frameworks unterstützen. 

Sobald Sie die gewünschte Ordnerstruktur eingerichtet haben, führen Sie den folgenden Befehl in diesem Ordner aus, um die `.nuspec`-Datei zu erstellen:

```cli
nuget spec
```

Die generierte `.nuspec`-Datei enthält wie bereits erwähnt keine expliziten Verweise auf Dateien in der Ordnerstruktur. NuGet schließt bei der Paketerstellung automatisch alle Dateien ein. Die Platzhalterwerte müssen jedoch trotzdem noch in anderen Teilen des Manifests bearbeitet werden.

### <a name="from-an-assembly-dll"></a>Aus einer Assembly-DLL

Das Erstellen eines Pakets aus einer Assembly ist ein einfacher Vorgang. Dabei können Sie eine `.nuspec`-Datei aus den Metadaten in der Assembly mithilfe des folgenden Befehls generieren:

```cli
nuget spec <assembly-name>.dll
```

Bei dieser Schreibweise werden einige Platzhalter im Manifest durch bestimmte Werte aus der Assembly ersetzt. Die Eigenschaft `<id>` wird beispielsweise auf den Assemblynamen festgelegt und `<version>` auf die Version. Andere Manifesteigenschaften haben jedoch keine übereinstimmenden Werte in der Assembly und enthalten somit weiterhin Platzhalter.

### <a name="from-a-visual-studio-project"></a>Aus einem Visual Studio-Projekt

Es empfiehlt sich, eine `.nuspec`-Datei aus einer `.csproj`- oder `.vbproj`-Datei zu erstellen, da auf andere Pakete, die in dieses Projekt installiert wurden, automatisch als Abhängigkeiten verwiesen wird. Verwenden Sie einfach den folgenden Befehl im Ordner der Projektdatei:

```cli
# Use in a folder containing a project file <project-name>.csproj or <project-name>.vbproj
nuget spec
```

Die anschließend erstellte `<project-name>.nuspec`-Datei enthält *Tokens*, die zur Packzeit durch Werte aus dem Projekt ersetzt werden, einschließlich der Verweise auf alle anderen Pakete, die bereits installiert wurden.

Ein Token wird auf beiden Seiten der Projekteigenschaft durch das Symbol `$` begrenzt. Wird der Wert `<id>` auf diese Weise in einem Manifest generiert, wird er in der Regel folgendermaßen angezeigt:

```xml
<id>$id$</id>
```

Dieses Token wird zur Packzeit durch den Wert `AssemblyName` aus der Projektdatei ersetzt. Weitere Informationen zur genauen Zuordnung von Projektwerten und `.nuspec`-Tokens finden Sie im Abschnitt [Replacement tokens (Ersetzungstokens)](../reference/nuspec.md#replacement-tokens) im Artikel „.nuspec reference“ (NUSPEC-Referenz).

Durch Tokens müssen Sie wichtige Werte wie die Versionsnummer in der `.nuspec`-Datei nicht mit dem Projekt zusammen aktualisieren. Sie können die Tokens bei Bedarf jederzeit durch Literalwerte ersetzen. 

Wenn Sie in einem Visual Studio-Projekt arbeiten, haben weitere Packoptionen zur Auswahl. Dies wird weiter unten im Abschnitt [Ausführen von „nuget pack“ zum Generieren der NUPKG-Datei](#running-nuget-pack-to-generate-the-nupkg-file) beschrieben.

#### <a name="solution-level-packages"></a>Pakete auf Projektmappenebene

*Nur NuGet 2.x. Nicht verfügbar in NuGet 3.0 und höher.*

In NuGet 2.x werden Pakete auf Projektmappenebene unterstützt, über die Tools oder zusätzliche Befehle für die Paket-Manager-Konsole installiert werden (der Inhalt des Ordners `tools`), die jedoch weder Verweise noch Inhalt hinzufügen oder Anpassungen für Projekte in der Projektmappe erstellen. Solche Pakete enthalten keine Dateien in den direkten Ordnern `lib`, `content` oder `build`, und keine der dazugehörigen Abhängigkeiten besitzt Dateien in den jeweiligen `lib`-, `content`- oder `build`-Ordnern.

NuGet verfolgt installierte Pakete auf Projektmappenebene in einer `packages.config`-Datei im Ordner `.nuget` nach, statt in der `packages.config`-Datei des Projekts.

### <a name="new-file-with-default-values"></a>Neue Datei mit Standardwerten

Mit dem folgenden Befehl wird ein Standardmanifest mit Platzhaltern erstellt, das gewährleistet, dass Sie mit der richtigen Dateistruktur beginnen:

```cli
nuget spec [<package-name>]
```

Wenn Sie \<package-name\> weglassen, lautet die Ergebnisdatei `Package.nuspec`. Wenn Sie einen Namen wie `Contoso.Utility.UsefulStuff` angeben, lautet die Datei `Contoso.Utility.UsefulStuff.nuspec`.

Die resultierende `.nuspec`-Datei enthält Platzhalter für Werte wie `projectUrl`. Denken Sie daran, die Datei zu bearbeiten, bevor Sie mit ihr die endgültige `.nupkg`-Datei erstellen.

## <a name="choosing-a-unique-package-identifier-and-setting-the-version-number"></a>Auswählen eines eindeutigen Paketbezeichners und Festlegen der Versionsnummer

Der Paketbezeichner (`<id>`-Element) und die Versionsnummer (`<version>`-Element) sind die beiden wichtigsten Werte im Manifest, da sie eindeutig den exakten Code bezeichnen, der im Paket enthalten ist.

**Bewährte Methoden für den Paketbezeichner:**

- **Eindeutigkeit:** Der Bezeichner muss auf „nuget.org“ bzw. in dem Katalog, in dem das Paket gehostet wird, eindeutig sein. Bevor Sie sich für einen Bezeichner entscheiden, vergewissern Sie sich, dass dieser im entsprechenden Katalog nicht bereits verwendet wird. Zur Vermeidung von Konflikten empfiehlt es sich, den Namen Ihres Unternehmens im ersten Teil des Bezeichners zu nutzen, z.B. `Contoso.`.
- **Namespace-ähnliche Namen:** Verwenden Sie Punkte statt Bindestrichen, wie bei der Notation von Namespaces in .NET. Schreiben Sie z.B. `Contoso.Utility.UsefulStuff` statt `Contoso-Utility-UsefulStuff` oder `Contoso_Utility_UsefulStuff`. Benutzer finden es auch hilfreich, wenn der Paketbezeichner den im Code verwendeten Namespaces entspricht.
- **Beispielpakete:** Wenn Sie ein Paket mit Beispielcode erstellen, das veranschaulicht, wie ein anderes Paket verwenden, fügen Sie `.Sample` als Suffix an den Bezeichner an, z.B. `Contoso.Utility.UsefulStuff.Sample`. Das Beispielpaket würde natürlich vom anderen Paket abhängen. Verwenden Sie beim Erstellen eines Beispielpakets wie weiter oben beschrieben das konventionsbasierte Arbeitsverzeichnis. Arrangieren Sie den Beispielcode im Ordner `content` in einem Ordner namens `\Samples\<identifier>`, z.B. `\Samples\Contoso.Utility.UsefulStuff.Sample`.

**Bewährte Methoden für die Paketversion:**

- Legen Sie die Version des Pakets auf die der Bibliothek fest, obwohl dies nicht zwingend erforderlich ist. Dies ist sehr einfach, wenn Sie ein Paket, wie zuvor im Abschnitt [Welche Assemblys sollen gepackt werden?](#deciding-which-assemblies-to-package) beschrieben, auf eine einzelne Assembly beschränken. Bedenken Sie, dass NuGet sich beim Auflösen der Abhängigkeiten nach den Paketversionen richtet, nicht nach den Assemblyversionen.
- Wenn Sie ein nicht standardmäßiges Versionsschema verwenden, müssen Sie die NuGet-Versionsregeln wie unter [Package versioning (Paketversionsverwaltung](../reference/package-versioning.md) beschrieben anwenden.

> Die folgenden kurzen Blogbeiträge enthalten weitere Informationen zur Versionsverwaltung:
>
> - [Part 1: Taking on DLL Hell (Teil 1: DLLs)](http://blog.davidebbo.com/2011/01/nuget-versioning-part-1-taking-on-dll.html)
> - [Part 2: The core algorithm (Teil 2: Der Kernalgorithmus)](http://blog.davidebbo.com/2011/01/nuget-versioning-part-2-core-algorithm.html)
> - [Part 3: Unification via Binding Redirects (Teil 3: Vereinheitlichung über Bindungsumleitungen)](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)

## <a name="setting-a-package-type"></a>Festlegen eines Pakettyps

In NuGet 3.5 und höher können Pakete mit einem bestimmten *Pakettyp* gekennzeichnet werden, um den vorgesehenen Zweck anzugeben. Pakete ohne Typ, einschließlich aller mit früheren Versionen von NuGet erstellten Pakete, haben standardmäßig den Typ `Dependency`.

- Pakete mit Typ `Dependency` fügen Bibliotheken und Anwendungen Build- oder Laufzeitressourcen hinzu und können in jedem Projekttyp installiert werden, wenn sie kompatibel sind.

- Pakete mit Typ `DotnetCliTool` sind Erweiterungen der [.NET-CLI](/dotnet/articles/core/tools/index) und werden über die Befehlszeile aufgerufen. Solche Pakete können nur in .NET Core-Projekten installiert werden und haben keine Auswirkungen auf Wiederherstellungsvorgänge. Weitere Informationen zu diesen projektspezifischen Erweiterungen finden Sie in der Dokumentation zur [.NET Core-Erweiterbarkeit](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility).

- Pakete des benutzerdefinierten Typs verwenden einen willkürlichen Typbezeichner, der den gleichen Formatierungsregeln wie Paketbezeichner unterliegt. Der NuGet-Paket-Manager in Visual Studio erkennt jedoch nur die Typen `Dependency` und `DotnetCliTool`.

Pakettypen werden in der `.nuspec`-Datei festgelegt. Für die Abwärtskompatibilität wird empfohlen, den `Dependency`-Typ *nicht* explizit festzulegen und stattdessen NuGet entscheiden zu lassen, wenn kein Typ angegeben ist.

- `.nuspec`: Geben Sie den Pakettyp innerhalb eines `packageTypes\packageType`-Knotens unter dem `<metadata>`-Element an:

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <package xmlns="http://schemas.microsoft.com/packaging/2012/06/nuspec.xsd">
        <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="DotnetCliTool" />
        </packageTypes>
        </metadata>
    </package>
    ```

## <a name="adding-a-readme-and-other-files"></a>Hinzufügen einer Infodatei und anderer Dateien

Verwenden Sie den `<files>`-Knoten in der `.nuspec`-Datei, die dem `<metadata>`-Tag *folgt*, um Dateien, die in das Paket aufgenommen werden sollen, direkt anzugeben:

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2013/05/nuspec.xsd">
    <metadata>
    <!-- ... -->
    </metadata>
    <files>
    <!-- Add a readme -->
    <file src="readme.txt" target="" />

    <!-- Add files from an arbitrary folder that's not necessarily in the project -->
    <file src="..\..\SomeRoot\**\*.*" target="" />
    </files>
</package>
```

> [!Tip]
> Bei einem konventionsbasierten Arbeitsverzeichnis können Sie die Datei „readme.txt“ im Stammverzeichnis des Pakets und andere Inhalte im Ordner `content` platzieren. Dazu sind keine `<file>`-Elemente im Manifest erforderlich.

Wenn Sie eine Datei namens `readme.txt` im Stammverzeichnis des Pakets einschließen, zeigt Visual Studio unmittelbar nach der direkten Installation des Pakets den Inhalt der Datei als Nur-Text an. Für Pakete, die als Abhängigkeiten installiert wurden, werden keine Infodateien angezeigt. Die Infodatei für das Paket „HtmlAgilityPack“ wird z.B. folgendermaßen angezeigt:

![Anzeige einer Infodatei für ein NuGet-Paket nach der Installation](media/Create_01-ShowReadme.png)

> [!Note]
> Wenn Sie einen leeren `<files>`-Knoten in die `.nuspec`-Datei einschließen, fügt NuGet dem Paket keine weiteren Inhalte außer denen im Ordner `lib` hinzu.

## <a name="including-msbuild-props-and-targets-in-a-package"></a>Einfügen von MSBuild-Eigenschaften und -Zielen in ein Paket

In einigen Fällen (z.B. beim Ausführen eines benutzerdefinierten Tools oder Prozesses während des Buildvorgangs) sollten Sie benutzerdefinierte Buildziele oder -eigenschaften zu Projekten hinzufügen, die Ihr Paket nutzen. Platzieren Sie dazu Dateien mit der Schreibweise `<package_id>.targets` oder `<package_id>.props` (z.B. `Contoso.Utility.UsefulStuff.targets`) im `\build`-Ordner des Projekts.

Dateien im `\build`-Stammverzeichnis gelten als für alle Zielframeworks geeignet. Um frameworkspezifische Dateien bereitzustellen, platzieren Sie zuerst Dateien wie die folgenden in den entsprechenden Unterordnern:

    \build
        \netstandard1.4
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets
        \net462
            \Contoso.Utility.UsefulStuff.props
            \Contoso.Utility.UsefulStuff.targets

Verweisen Sie dann in der `.nuspec`-Datei im `<files>`-Knoten auf diese Dateien:

```xml
<?xml version="1.0"?>
<package >
    <metadata minClientVersion="2.5">
    <!-- ... -->
    </metadata>
    <files>
    <!-- Include everything in \build -->
    <file src="build\**" target="build" />

    <!-- Other files -->
    <!-- ... -->
    </files>
</package>
```

Das Einfügen von MSBuild-Eigenschaften und -Zielen in ein Paket wurde [mit NuGet 2.5 eingeführt](../release-notes/NuGet-2.5.md#automatic-import-of-msbuild-targets-and-props-files). Daher wird empfohlen, dem Element `metadata` das `minClientVersion="2.5"`-Attribut hinzuzufügen, damit die für das Paket erforderliche Mindestversion des NuGet-Clients angegeben wird.

Wenn NuGet ein Paket mit `\build`-Dateien erstellt, werden der Projektdatei MSBuild-`<Import>`-Elemente hinzufügt, die auf die `.targets`- und `.props`-Dateien zeigen. `.props` wird oben in der Projektdatei hinzugefügt und `.targets` ganz unten. Für jedes Zielframework wird ein eigenes bedingtes MSBuild-`<Import>`-Element hinzugefügt.

MSBuild-`.props`- und -`.targets`-Dateien für frameworkübergreifende Ziele können im Ordner `\buildCrossTargeting` abgelegt werden. Bei der Paketinstallation fügt NuGet die entsprechenden `<Import>`-Elemente in die Projektdatei mit der Bedingung ein, dass das Zielframework nicht festgelegt ist (die MSBuild-Eigenschaft `$(TargetFramework)` muss leer sein).

In NuGet 3.x werden Ziele nicht zum Projekt hinzugefügt, sondern über `project.lock.json` zur Verfügung gestellt.

## <a name="authoring-packages-with-com-interop-assemblies"></a>Erstellen von Paketen, die COM-Interop-Assemblys enthalten

Pakete, die COM-Interop-Assemblys enthalten, müssen eine entsprechende [Zieledatei](#including-msbuild-props-and-targets-in-a-package) enthalten, damit die richtigen `EmbedInteropTypes`-Metadaten zu Projekten hinzugefügt werden, die das Format „PackageReference“ verwenden. Die `EmbedInteropTypes`-Metadaten sind für alle Assemblys immer FALSE, wenn „PackageReference“ verwendet wird, damit die Zieledatei diese Metadaten explizit hinzufügt. Um Konflikte zu vermeiden, sollte der Name des Ziels eindeutig sein. Verwenden Sie am besten eine Kombination aus dem Paketnamen und der Assembly, die eingebettet wird, und ersetzen Sie `{InteropAssemblyName}` im folgenden Beispiel durch diesen Wert. Ein weiteres Beispiel finden Sie unter [NuGet.Samples.Interop](https://github.com/NuGet/Samples/tree/master/NuGet.Samples.Interop).

```xml
<Target Name="EmbeddingAssemblyNameFromPackageId" AfterTargets="ResolveReferences" BeforeTargets="FindReferenceAssembliesForReferences">
  <PropertyGroup>
    <_InteropAssemblyFileName>{InteropAssemblyName}</_InteropAssemblyFileName>
  </PropertyGroup>
  <ItemGroup>
    <ReferencePath Condition=" '%(FileName)' == '$(_InteropAssemblyFileName)' AND '%(ReferencePath.NuGetPackageId)' == '$(MSBuildThisFileName)' ">
      <EmbedInteropTypes>true</EmbedInteropTypes>
    </ReferencePath>
  </ItemGroup>
</Target>
```

Hinweis: Wenn Sie das `packages.config`-Verwaltungsformat verwenden, prüfen NuGet und Visual Studio beim Hinzufügen von Verweisen zu den Assemblys aus Paketen auf COM-Interop-Assemblys und legen `EmbedInteropTypes` in der Projektdatei auf TRUE fest. In diesem Fall werden die Ziele überschrieben.

Darüber hinaus werden die [Buildressourcen standardmäßig nicht transitiv weitergeben](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets). Pakete, die dieser Beschreibung nach erstellt werden, funktionieren anders, wenn sie als transitive Abhängigkeit aus einem Projekt in einen Projektverweis gezogen werden. Der Paketbenutzer kann die Weiterleitung zulassen, indem er den Standardwert „PrivateAssets“ so ändert, dass „build“ nicht enthalten ist.

<a name="creating-the-package"></a>

## <a name="running-nuget-pack-to-generate-the-nupkg-file"></a>Ausführen von „nuget pack“ zum Generieren der NUPKG-Datei

Wenn Sie eine Assembly oder das konventionsbasierte Arbeitsverzeichnis verwenden, erstellen Sie ein Paket, indem Sie den Befehl `nuget pack` mit der `.nuspec`-Datei ausführen und dabei `<manifest-name>` durch den bestimmten Dateinamen ersetzen:

```cli
nuget pack <project-name>.nuspec
```

Wenn Sie ein Visual Studio-Projekt verwenden, führen Sie `nuget pack` mit der Projektdatei aus, die automatisch die `.nuspec`-Datei des Projekts lädt und alle Tokens darin durch die Werte in der Projektdatei ersetzt:

```cli
nuget pack <project-name>.csproj
```

> [!Note]
> Die direkte Verwendung der Projektdatei ist für die Tokenersetzung erforderlich, da das Projekt die Quelle der Tokenwerte ist. Die Tokenersetzung wird nicht ausgeführt, wenn Sie `nuget pack` mit einer `.nuspec`-Datei verwenden.

`nuget pack` schließt auf jeden Fall Ordner aus, die mit einem Punkt beginnen, z.B. `.git` oder `.hg`.

NuGet gibt an, ob die `.nuspec`-Datei Fehler enthält, die korrigiert werden müssen, z.B. nicht geänderte Platzhalterwerte im Manifest.

Wenn `nuget pack` erfolgreich ausgeführt wurde, können Sie die erstellte `.nupkg`-Datei wie in [Publishing packages (Veröffentlichen von Paketen)](../create-packages/publish-a-package.md) beschrieben in einem geeigneten Katalog veröffentlichen.

> [!Tip]
> Wenn Sie sich das erstellte Paket genauer ansehen möchten, öffnen Sie es einfach im [Paket-Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer). Dieser stellt den Inhalt des Pakets und das Manifest grafisch dar. Sie können die resultierende `.nupkg`-Datei auch in eine `.zip`-Datei umbenennen und deren Inhalt direkt prüfen.

### <a name="additional-options"></a>Zusätzliche Optionen

Sie können `nuget pack` mit verschiedenen Befehlszeilenparameter verwenden, um z.B. Dateien auszuschließen, die Versionsnummer im Manifest zu überschreiben und den Ausgabeordner zu ändern. Eine vollständige Liste finden Sie in der [Referenz zum Packbefehl](../tools/cli-ref-pack.md).

Folgende Optionen werden beispielsweise häufig in Visual Studio-Projekten verwendet:

- **Referenzierte Projekte:** Wenn das Projekt auf andere verweist, können Sie die referenzierten Projekte mithilfe der Option `-IncludeReferencedProjects` als Teil des Pakets oder als Abhängigkeiten hinzufügen:

    ```cli
    nuget pack MyProject.csproj -IncludeReferencedProjects
    ```

    Diese Einschließung ist rekursiv. Wenn also `MyProject.csproj` auf die Projekte B und C verweist und diese Projekte ihrerseits auf die Projekte D, E und F, dann werden Dateien aus B, C, D, E und F in das Paket aufgenommen.

    Wenn ein referenziertes Projekt selbst eine `.nuspec`-Datei enthält, fügt NuGet dieses Projekt stattdessen als Abhängigkeit hinzu.  Dieses Projekt muss separat gepackt und veröffentlicht werden.

- **Buildkonfiguration:** NuGet verwendet die in der Projektdatei festgelegte Standardbuildkonfiguration, üblicherweise *Debuggen*. Um Dateien aus einer anderen Buildkonfiguration zu packen, z.B. *Release*, verwenden Sie die Option `-properties` mit folgender Konfiguration:

    ```cli
    nuget pack MyProject.csproj -properties Configuration=Release
    ```

- **Symbole:** Um Symbole einzuschließen, mit denen Benutzer den Paketcode im Debugger schrittweise ausführen können, verwenden Sie die Option `-Symbols`:

    ```cli
    nuget pack MyProject.csproj -symbols
    ```

### <a name="testing-package-installation"></a>Testen der Paketinstallation

Vor dem Veröffentlichen eines Pakets testen Sie in der Regel die Installation eines Pakets in einem Projekt. Diese Tests stellen sicher, dass die erforderlichen Dateien an den richtigen Orten im Projekt installiert werden.

Installationen lassen sich manuell in Visual Studio oder mithilfe der normalen [Paketinstallationsschritte](../consume-packages/ways-to-install-a-package.md) über die Befehlszeile testen.

Für automatisierte Tests gehen Sie folgendermaßen vor:

1. Kopieren Sie die `.nupkg`-Datei in einen lokalen Ordner.
1. Fügen Sie den Ordner mithilfe des `nuget sources add -name <name> -source <path>`-Befehls den Paketquellen hinzu. Weitere Informationen finden Sie unter [sources command (NuGet CLI) (sources-Befehl (NuGet-CLI))](../tools/cli-ref-sources.md). Diese lokale Quelle muss auf einem Computer nur einmal festgelegt werden.
1. Installieren Sie das Paket aus dieser Quelle mithilfe von `nuget install <packageID> -source <name>`, wobei `<name>` dem Namen der Quelle entspricht, so wie er an `nuget sources` übergeben wurde. Durch das Angeben der Quelle wird sichergestellt, dass das Paket nur aus dieser Quelle installiert wird.
1. Überprüfen Sie das Dateisystem, um sicherzustellen, dass Dateien richtig installiert wurden.

## <a name="next-steps"></a>Nächste Schritte

Nachdem Sie ein Paket erstellt haben, das eine `.nupkg`-Datei ist, können Sie sie wie unter [Publishing packages (Veröffentlichen von Paketen)](../create-packages/publish-a-package.md) beschrieben im Katalog Ihrer Wahl veröffentlichen.

Sie können auch die Funktionen des Pakets erweitern oder wie in den folgenden Themen beschrieben andere Szenarios unterstützen:

- [Paketversionsverwaltung](../reference/package-versioning.md)
- [Unterstützen mehrerer Zielframeworks](../create-packages/supporting-multiple-target-frameworks.md)
- [Transformationen von Quell- und Konfigurationsdateien](../create-packages/source-and-config-file-transformations.md)
- [Lokalisierung](../create-packages/creating-localized-packages.md)
- [Vorabversionen](../create-packages/prerelease-packages.md)

Außerdem sollten Sie die folgenden zusätzlichen Pakettypen berücksichtigen:

- [Native Pakete](../create-packages/native-packages.md)
- [Symbolpakete](../create-packages/symbol-packages.md)
