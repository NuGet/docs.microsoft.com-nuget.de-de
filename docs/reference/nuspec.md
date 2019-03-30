---
title: NUSPEC-Dateireferenz für NuGet
description: Die NUSPEC-Datei enthält Paketmetadaten, die bei der Erstellung eines Pakets verwendet werden, um für die Paketconsumer Informationen bereitzustellen.
author: karann-msft
ms.author: karann
ms.date: 08/29/2017
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 21678cc36fd9bf1ed49143bee3f35208640fc8a7
ms.sourcegitcommit: 2af17c8bb452a538977794bf559cdd78d58f2790
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/29/2019
ms.locfileid: "58637648"
---
# <a name="nuspec-reference"></a>NUSPEC-Referenz

Bei einer `.nuspec`-Datei handelt es sich um eine XML-Manifestdatei, die Paketmetadaten enthält. Diese Manifestdatei wird sowohl für die Erstellung des Pakets als auch zur Bereitstellung von Informationen für die Consumer verwendet. Manifestdateien sind in allen Paketen enthalten.

In diesem Thema:

- [Allgemeine Form und Schema](#general-form-and-schema)
- [Ersetzungstokens](#replacement-tokens) (bei der Verwendung in einem Visual Studio-Projekt)
- [Abhängigkeiten](#dependencies)
- [Explizite Assemblyverweise](#explicit-assembly-references)
- [Verweise auf Frameworkassemblys](#framework-assembly-references)
- [Einschließen von Assemblydateien](#including-assembly-files)
- [Einschließen von Inhaltsdateien](#including-content-files)
- [NUSPEC-Beispieldateien](#example-nuspec-files)

## <a name="general-form-and-schema"></a>Allgemeine Form und Schema

Die aktuelle `nuspec.xsd`-Schemadatei finden Sie im [NuGet-GitHub-Repository](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).

Für dieses Schema gilt die im Folgenden dargestellte allgemeine Form für die `.nuspec`-Datei:

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <!-- Required elements-->
        <id></id>
        <version></version>
        <description></description>
        <authors></authors>

        <!-- Optional elements -->
        <!-- ... -->
    </metadata>
    <!-- Optional 'files' node -->
</package>
```

Um eine übersichtliche Darstellung des Schemas anzuzeigen, öffnen Sie die Schemadatei im Entwurfsmodus in Visual Studio und klicken dann auf den Link **XML-Schema-Explorer**. Alternativ können Sie die Datei auch als Code öffnen, mit der rechten Maustaste in den Editor klicken und **Show XML Schema Explorer** (XML-Schema-Explorer anzeigen) auswählen. In beiden Fällen wird eine Ansicht zurückgegeben, die der in der folgenden Abbildung gezeigten ähnlich ist (bei erweiterter Darstellung):

![Visual Studio-Schema-Explorer mit geöffneter „nuspec.xsd“-Datei](media/SchemaExplorer.png)

### <a name="required-metadata-elements"></a>Erforderliche Metadatenelemente

Obwohl es sich bei den folgenden Elementen um die Mindestanforderungen für ein Paket handelt, sollten Sie in Erwägung ziehen, die [optionalen Metadatenelemente](#optional-metadata-elements) hinzuzufügen, damit Entwicklern die Arbeit mit Ihren Paketen erleichtert wird. 

Die folgenden Elemente müssen in einem `<metadata>`-Element vorhanden sein.

#### <a name="id"></a>id 
Paketbezeichner, der auf nuget.org oder im für das Paket verwendeten Katalog eindeutig sein muss. Die Groß-/Kleinschreibung wird nicht berücksichtigt. IDs dürfen keine Leerzeichen oder in URLs unzulässige Zeichen enthalten. Im Wesentlichen müssen sie den Regeln für .NET-Namespaces entsprechen. Informationen finden Sie unter [Auswählen eines eindeutigen Paketbezeichners und Festlegen der Versionsnummer](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number).
#### <a name="version"></a>version
Die Version des Pakets. Das Format lautet *Hauptversion.Nebenversion.Patch*. Versionsnummern enthalten möglicherweise, wie unter [Version Ranges and Wildcards (Versionsbereiche und Platzhalter)](../reference/package-versioning.md#pre-release-versions) beschrieben, ein Suffix der Vorabversion. 
#### <a name="description"></a>description
Eine ausführliche Beschreibung des Pakets zur Anzeige auf der Benutzeroberfläche. 
#### <a name="authors"></a>authors
Eine durch Kommas getrennte Liste der Paketautoren entsprechend den Profilnamen unter nuget.org. Diese werden im NuGet-Katalog auf nuget.org angezeigt und verwendet, um auf Pakete derselben Autoren zu verweisen. 

### <a name="optional-metadata-elements"></a>Optionale Metadatenelemente

#### <a name="title"></a>title
Ein benutzerfreundlicher Titel des Pakets, der gewöhnlich auf Benutzeroberflächen wie auf nuget.org oder im Paket-Manager in Visual Studio angezeigt wird. Sofern nicht angegeben, wird die Paket-ID verwendet. 
#### <a name="owners"></a>owners
Eine durch Kommas getrennte Liste der Paketersteller mit den auf nuget.org verwendeten Profilnamen. Dabei handelt es sich häufig um dieselbe Liste wie in `authors`. Sie wird beim Hochladen der Pakete auf nuget.org ignoriert. Informationen hierzu finden Sie unter [Verwalten von Paketbesitzern auf nuget.org](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg). 
#### <a name="projecturl"></a>projectUrl
URL der Homepage des Pakets, wird häufig auf Benutzeroberflächen und auf nuget.org angezeigt. 
#### <a name="licenseurl"></a>licenseUrl
> [!Important]
> "licenseUrl" ist veraltet. Verwenden Sie stattdessen die Lizenz.

URL der Paketlizenz, wird häufig auf Benutzeroberflächen und auf nuget.org angezeigt.
#### <a name="license"></a>Lizenz
Ein SPDX-Lizenzausdruck oder Pfad zu einer Lizenzdatei innerhalb des Pakets, der oft sowohl in der Benutzeroberfläche als auch auf nuget.org angezeigt wird. Wenn Sie das Paket unter einer gemeinsamen Lizenz z. B. BSD-2-Klausel oder MIT lizenzieren, verwenden Sie den zugehörigen SPDX-Lizenz-Bezeichner.<br>Beispiel: `<license type="expression">MIT</license>`

Hier ist die vollständige Liste der [SPDX Lizenzbezeichner](https://spdx.org/licenses/). NuGet.org akzeptiert nur von OSI oder FSF genehmigte Lizenzen, wenn der Ausdruck „license type“ verwendet wird.

Wenn Ihr Paket in mehrere allgemeine-Lizenzen lizenziert ist, können Sie angeben, eine zusammengesetzte Lizenz mithilfe der [SPDX Expression Syntaxversion 2.0](https://spdx.org/spdx-specification-21-web-version#h.jxpfx0ykyb60).<br>Beispiel: `<license type="expression">BSD-2-Clause OR MIT</license>`

Wenn Sie eine Lizenz, die einen Bezeichner SPDX zugewiesen wurde, oder es eine benutzerdefinierte-Lizenz ist, können Sie eine Datei verpacken (nur `.txt` oder `.md`) mit dem Text der Lizenz. Zum Beispiel:
```xml
<package>
  <metadata>
    ...
    <license type="file">LICENSE.txt</license>
    ...
  </metadata>
  <files>
    ...
    <file src="licenses\LICENSE.txt" target="" />
    ...
  </files>
</package>
```

Für die MSBuild-Entsprechung, sehen Sie sich [Packen eines Ausdrucks für die Lizenz oder eine Lizenzdatei](msbuild-targets.md#packing-a-license-expression-or-a-license-file).

Die genaue Syntax für Ausdrücke für die NuGet-Lizenz wird im folgenden beschrieben in [ABNF](https://tools.ietf.org/html/rfc5234).
```cli
license-id            = <short form license identifier from https://spdx.org/spdx-specification-21-web-version#h.luq9dgcle9mo>

license-exception-id  = <short form license exception identifier from https://spdx.org/spdx-specification-21-web-version#h.ruv3yl8g6czd>

simple-expression = license-id / license-id”+”

compound-expression =  1*1(simple-expression /
                simple-expression "WITH" license-exception-id /
                compound-expression "AND" compound-expression /
                compound-expression "OR" compound-expression ) /                
                "(" compound-expression ")" )

license-expression =  1*1(simple-expression / compound-expression / UNLICENSED)
```

#### <a name="iconurl"></a>iconUrl
URL eines 64 × 64 Pixel großen Bilds mit transparentem Hintergrund, das als Symbol für das Paket auf der Benutzeroberfläche verwendet wird. Stellen Sie sicher, dass dieses Element die *direkte Bild-URL* und nicht die URL einer Webseite enthält, auf der das Bild zu finden ist. Wenn Sie beispielsweise ein Bild auf GitHub verwenden möchten, geben Sie die URL der Rohdatendatei an (z. B. <em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>). 

#### <a name="requirelicenseacceptance"></a>requireLicenseAcceptance
Ein boolescher Wert, der angibt, ob der Client den Consumer dazu auffordern muss, die Paketlizenz vor der Installation des Pakets zu akzeptieren.
#### <a name="developmentdependency"></a>developmentDependency
*(ab Version 2.8)* Boolescher Wert, der angibt, ob das Paket mit einer Abhängigkeit markiert werden soll, die nur für die Entwicklung gilt. Hierdurch wird vermieden, dass das Paket als Abhängigkeit in andere Pakete eingeschlossen wird. Mit "packagereference" (NuGet 4.8) bedeutet dieses Flag auch, dass es während der Kompilierung von Ressourcen aus der Kompilierung ausgeschlossen werden. Finden Sie unter [DevelopmentDependency-Unterstützung für PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)
#### <a name="summary"></a>summary
Kurzbeschreibung des Pakets zur Anzeige auf der Benutzeroberfläche. Wenn diese nicht angegeben ist, wird eine gekürzte Version von `description` verwendet.
#### <a name="releasenotes"></a>releaseNotes
*(ab Version 1.5)* Beschreibung der in diesem Release des Pakets enthaltenen Änderungen, die häufig auf Benutzeroberflächen wie der Registerkarte **Updates** des Visual Studio-Paket-Managers anstelle von Paketbeschreibungen verwendet wird.
#### <a name="copyright"></a>copyright
*(ab Version 1.5)* Urheberrechtliche Hinweise zum Paket.
#### <a name="language"></a>language
Gebietsschema-ID des Pakets. Informationen hierzu finden Sie unter [Erstellen lokalisierter NuGet-Pakete](../create-packages/creating-localized-packages.md).
#### <a name="tags"></a>tags
Eine durch Leerzeichen getrennte Liste mit Tags und Schlüsselwörtern, die das Paket beschreiben und das Auffinden von Paketen mithilfe von Suchvorgängen und Filtern erleichtern. 
#### <a name="serviceable"></a>serviceable 
*(ab Version 3.3)* Nur zur internen Verwendung von NuGet.
#### <a name="repository"></a>repository
Repositorymetadaten. Sie umfassen vier optionale Attribute: *type* und *url* *(ab Version 4.0)* sowie *branch* und *commit* *(ab Version 4.6)*. Mit diesen Attributen können Sie die NUPKG-Datei dem Repository zuordnen, mit dem es erstellt wurde. Dabei lässt sich eine Detailtiefe bis hinab zum einzelnen Branch oder Commit erzielen, durch den das Paket erstellt wurde. Hierbei sollte es sich um eine öffentlich zugängliche URL handeln, die direkt von einer Versionskontrollsoftware aufgerufen werden kann. Dagegen sollte es keine HTML-Seite sein, da diese für den Computer vorgesehen ist. Zur Verknüpfung mit der Projektseite verwenden Sie stattdessen das Feld `projectUrl`.

#### <a name="minclientversion"></a>minClientVersion
Gibt die mindestens erforderliche Version des NuGet-Clients an, der dieses Paket installieren kann. Dies wird von nuget.exe und dem Paket-Manager von Visual Studio erzwungen. Das Attribut wird verwendet, wenn das Paket von bestimmten Funktionen der `.nuspec`-Datei abhängig ist, die in einer bestimmten Version des NuGet-Clients hinzugefügt wurden. Beispielsweise sollte ein Paket, das das `developmentDependency`-Attribut verwendet, „2.8“ für `minClientVersion` angeben. Genauso sollte ein Paket, das das `contentFiles`-Element verwendet (vgl. nächster Abschnitt), `minClientVersion` auf „3.3“ festlegen. Beachten Sie außerdem, dass NuGet-Clients vor Version 2.5 dieses Flag nicht erkennen und daher die Installation des Pakets unabhängig vom Inhalt von `minClientVersion` *immer* verweigern.

#### <a name="collection-elements"></a>Sammlungselemente

#### <a name="packagetypes"></a>packageTypes
*(ab Version 3.5)* Eine Sammlung mit null oder mehr `<packageType>`-Elementen, die den Pakettyp angibt, sofern es sich nicht um ein gewöhnliches Abhängigkeitspaket handelt. Jedes packageType-Element verfügt über die Attribute *name* und *version*. Informationen hierzu finden Sie unter [Festlegen eines Pakettyps](../create-packages/creating-a-package.md#setting-a-package-type).
#### <a name="dependencies"></a>dependencies
Eine Sammlung mit null oder mehr `<dependency>`-Elementen, die die Abhängigkeiten für das Paket angibt. Jede Abhängigkeit verfügt über die Attribute *id*, *version*, *include* und *exclude* (ab Version 3.x). Informationen hierzu finden Sie im Abschnitt [Abhängigkeiten](#dependencies-element) weiter unten.
#### <a name="frameworkassemblies"></a>frameworkAssemblies
*(ab Version 1.2)* Eine Sammlung mit null oder mehr `<frameworkAssembly>`-Elementen, die die für das Paket erforderlichen Verweise auf .NET Framework-Assemblys benennt. Hierdurch wird sichergestellt, dass Verweise auf Projekte hinzugefügt werden, die das Paket verarbeiten. Jedes frameworkAssembly-Element verfügt über die Attribute *assemblyName* und *targetFramework*. Informationen hierzu finden Sie unter [Verweise auf Frameworkassemblys](#specifying-framework-assembly-references-gac). |
#### <a name="references"></a>references
*(ab Version 1.5)* Eine Sammlung mit null oder mehr `<reference>`-Elementen, die Assemblys im `lib`-Ordner des Pakets benennt, die als Projektverweise hinzugefügt werden. Jeder Verweis verfügt über ein *file*-Attribut. `<references>` kann außerdem ein `<group>`-Element mit einem *targetFramework*-Attribut enthalten, das seinerseits `<reference>`-Elemente enthält. Wenn das Element nicht angegeben ist, werden alle Verweise in `lib` eingeschlossen. Informationen hierzu finden Sie unter [Explizite Assemblyverweise](#specifying-explicit-assembly-references).
#### <a name="contentfiles"></a>contentFiles
*(ab Version 3.3)* Eine Sammlung von `<files>`-Elementen, die Inhaltsdateien angeben, die in das verarbeitende Projekt eingeschlossen werden sollen. Diese Dateien werden zusammen mit Attributen angegeben, die beschreiben, wie sie im Projektsystem verwendet werden sollen. Informationen hierzu finden Sie weiter unten unter [Einschließen von Assemblydateien](#specifying-files-to-include-in-the-package).
#### <a name="files"></a>files 
Die `<package>` -Knoten enthält möglicherweise eine `<files>` Knoten einen gleichgeordneten Knoten zu `<metadata>`, und ein `<contentFiles>` untergeordnetes Element unter `<metadata>`, um anzugeben, welche Dateien Assembly- und Inhaltsdateien im Paket enthalten. Ausführliche Informationen hierzu finden Sie weiter unten in den Abschnitten [Einschließen von Assemblydateien](#including-assembly-files) und [Einschließen von Inhaltsdateien](#including-content-files).

## <a name="replacement-tokens"></a>Ersetzungstoken

Bei der Erstellung eines Pakets ersetzt der [`nuget pack`-Befehl](../tools/cli-ref-pack.md) durch $ getrennte Token im `<metadata>`-Knoten der `.nuspec`-Datei durch Werte, die entweder einer Projektdatei oder der `-properties`-Option des `pack`-Befehls entstammen.

Geben Sie in der Befehlszeile die Tokenwerte mit `nuget pack -properties <name>=<value>;<name>=<value>` an. Beispielsweise können Sie ein Token wie `$owners$` und `$desc$` in der `.nuspec`-Datei verwenden und die Werte zur Packzeit wie im Folgenden dargestellt bereitstellen:

```ps
nuget pack MyProject.csproj -properties
    owners=janedoe,harikm,kimo,xiaop;desc="Awesome app logger utility"
```

Geben Sie die in der untenstehenden Tabelle beschriebenen Token an, um Werte aus einem Projekt zu verwenden (AssemblyInfo verweist auf Dateien wie `AssemblyInfo.cs` oder `AssemblyInfo.vb` in `Properties`).

Führen Sie anstelle von `.nuspec` nur `nuget pack` in der Projektdatei aus, um diese Token zu verwenden. Beispielsweise werden bei der Verwendung des folgenden Befehls die Token `$id$` und `$version$` in einer `.nuspec`-Datei durch die Werte `AssemblyName` und `AssemblyVersion` des Projekts ersetzt:

```ps
nuget pack MyProject.csproj
```

In der Regel erstellen Sie die `.nuspec`-Datei in einem Projekt zuerst mithilfe von `nuget spec MyProject.csproj`, wodurch automatisch einige dieser Standardtoken eingeschlossen werden. Wenn in einem Projekt allerdings keine Werte für erforderliche `.nuspec`-Elemente enthalten sind, tritt bei `nuget pack` ein Fehler auf. Stellen Sie außerdem bei der Änderung von Projektwerten sicher, dass Sie diese neu erstellen, bevor Sie das Paket erstellen. Dies können Sie ganz einfach über die Option `build` des Packbefehls tun.

Mit Ausnahme von `$configuration$` werden Werte im Projekt gegenüber Werten bevorzugt, die demselben Token in der Befehlszeile zugeordnet sind.

| Token | Wertquelle | Wert
| --- | --- | ---
| **$id$** | Projektdatei | "AssemblyName" (Titel) aus der Projektdatei |
| **$version$** | AssemblyInfo | „AssemblyInformationalVersion“, falls vorhanden, andernfalls „AssemblyVersion“ |
| **$author$** | AssemblyInfo | AssemblyCompany |
| **$title$** | AssemblyInfo | AssemblyTitle |
| **$description$** | AssemblyInfo | AssemblyDescription |
| **$copyright$** | AssemblyInfo | AssemblyCopyright |
| **$configuration$** | Assembly-DLL | Konfiguration, die zur Erstellung der Assembly verwendet wird und standardmäßig auf „Debug“ festgelegt ist. Achten Sie darauf, dass Sie stets `-properties Configuration=Release` in der Befehlszeile verwenden, um mithilfe einer Releasekonfiguration ein Paket zu erstellen. |

Token können auch zum Auflösen von Pfaden verwendet werden, wenn Sie [Assemblydateien](#including-assembly-files) und [Inhaltsdateien](#including-content-files) hinzufügen. Die Namen der Token und der MSBuild-Eigenschaften sind identisch, wodurch Sie abhängig von der aktuellen Buildkonfiguration Dateien auswählen können, die eingeschlossen werden sollen. Wenn Sie beispielsweise die folgenden Token in der `.nuspec`-Datei verwenden

```xml
<files>
    <file src="bin\$configuration$\$id$.pdb" target="lib\net40" />
</files>
```

und eine Assembly mit der `Release`-Konfiguration in MSBuild erstellen, deren `AssemblyName` den Wert `LoggingLibrary` hat, sehen die dadurch entstandenen Zeilen in der `.nuspec`-Datei in den Paketen wie folgt aus:

```xml
<files>
    <file src="bin\Release\LoggingLibrary.pdb" target="lib\net40" />
</files>
```

## <a name="dependencies-element"></a>Abhängigkeitselement

Das `<dependencies>`-Element in `<metadata>` enthält eine beliebige Anzahl von `<dependency>`-Elementen, die andere Pakete angeben, von denen das Paket der obersten Ebene abhängig ist. Im Folgenden werden die Attribute für jede `<dependency>` dargestellt:

| Attribut | Beschreibung |
| --- | --- |
| `id` | (Erforderlich) Paket-ID der Abhängigkeit, z.B. „EntityFramework“ und „NUnit“. Dies ist der Name des Pakets, der auf nuget.org auf einer Paketseite angezeigt wird. |
| `version` | (Erforderlich) Bereich an Versionen, die als Abhängigkeiten akzeptiert werden. Die genaue Syntax finden Sie unter [Version Ranges and Wildcards (Versionsbereiche und Platzhalter)](../reference/package-versioning.md#version-ranges-and-wildcards). |
| include | Eine kommagetrennte Liste mit include- und exclude-Tags (siehe nachfolgende Tabelle), die die Abhängigkeit angibt, die in das endgültige Paket eingeschlossen werden soll. Der Standardwert ist `all`. |
| exclude | Eine kommagetrennte Liste mit include- und exclude-Tags (siehe nachfolgende Tabelle), die die Abhängigkeit angibt, die aus dem endgültigen Paket ausgeschlossen werden soll. Der Standardwert ist `build,analyzers`. Er kann überschrieben werden. Allerdings werden implizit auch `content/ ContentFiles` aus dem endgültigen Paket ausgeschlossen, was sich nicht überschreiben lässt. `exclude`-Tags haben Vorrang vor `include`-Tags. Beispielsweise hat `include="runtime, compile" exclude="compile"` die gleiche Wirkung wie `include="runtime"`. |

| Include-/Exclude-Tag | Betroffene Ordner auf dem Ziel |
| --- | --- |
| contentFiles | Content |
| runtime | Runtime, Resources und FrameworkAssemblies |
| compile | lib |
| Build | Build (MSBuild-Eigenschaften und -Ziele) |
| native | native |
| none | Keine Ordner |
| all | Alle Ordner |

Beispielsweise verweisen die folgenden Zeilen auf Abhängigkeiten von `PackageA` Version 1.1.0 und höher und `PackageB` Version 1.x.

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" />
    <dependency id="PackageB" version="[1,2)" />
</dependencies>
```

In den folgenden Zeilen wird zwar auf Abhängigkeiten von denselben Paketen verwiesen, allerdings wird auch angegeben, dass die Ordner `contentFiles` und `build` aus `PackageA` sowie alle anderen Ordner bis auf `native` und `compile` aus `PackageB` eingeschlossen werden sollen.

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" include="contentFiles, build" />
    <dependency id="PackageB" version="[1,2)" exclude="native, compile" />
</dependencies>
```

Hinweis: Beim Erstellen einer `.nuspec` aus einem Projekt mit `nuget spec`, Abhängigkeiten, die in diesem Projekt vorhanden sind, sind automatisch im resultierenden enthalten `.nuspec` Datei.

### <a name="dependency-groups"></a>Abhängigkeitsgruppen

*Version 2.0 und höher*

Als Alternative zu einer einzelnen flachen Liste können Abhängigkeiten auf der Grundlage des Frameworkprofils des Zielprojekts mithilfe von `<group>`-Elementen in `<dependencies>` angegeben werden.

Jede Gruppe verfügt über ein Attribut mit dem Namen `targetFramework` und enthält null oder mehr `<dependency>`-Elemente. Diese Abhängigkeiten werden gemeinsam installiert, wenn das Zielframework kompatibel mit dem Frameworkprofil des Projekts ist.

Das `<group>`-Element ohne ein `targetFramework`-Attribut wird als Standard- oder Fallbackliste der Abhängigkeiten verwendet. Die genauen Frameworkbezeichner finden Sie unter [Zielframeworks](../reference/target-frameworks.md).

> [!Important]
> Das Gruppenformat kann nicht mit einer flachen Liste vermischt werden.

Im folgenden Beispiel werden verschiedene Variationen des `<group>`-Elements dargestellt:

```xml
<dependencies>
    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>

    <group targetFramework="net40">
        <dependency id="jQuery" />
        <dependency id="WebActivator" />
    </group>

    <group targetFramework="sl30">
    </group>
</dependencies>
```

<a name="specifying-explicit-assembly-references"></a>

## <a name="explicit-assembly-references"></a>Explizite Assemblyverweise

Das `<references>`-Element gibt ausdrücklich die Assemblyverweise an, auf die das Zielprojekt bei der Verwendung des Pakets verweisen soll. Wenn dieses Element vorhanden ist, fügt NuGet nur Verweise auf die aufgelisteten Assemblys hinzu. Es werden keine Verweise auf andere Assemblys im `lib`-Ordner des Pakets hinzugefügt.

Beispielsweise gibt das folgende `<references>`-Element NuGet die Anweisung, Verweise auch dann nur auf `xunit.dll` und `xunit.extensions.dll` hinzuzufügen, wenn zusätzliche Assemblys im Paket enthalten sind:

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

In der Regel werden Verweise nur für Assemblys zur Entwurfszeit verwendet. Beispielsweise müssen sich Vertragsassemblys bei der Verwendung von [Codeverträgen](/dotnet/framework/debug-trace-profile/code-contracts) neben den Runtimeassemblys befinden, die sie erweitern, damit Visual Studio sie finden kann. Allerdings muss das Projekt auf die Vertragsassemblys verweisen, und sie dürfen auch nicht in den `bin`-Ordner des Projekts kopiert werden.

Genauso können explizite Verweise für Komponententestframeworks wie XUnit verwendet werden, in denen sich zwar die Toolassemblys neben den Runtimeassemblys befinden, jedoch nicht als Projektverweise eingeschlossen werden müssen.

### <a name="reference-groups"></a>Verweisgruppen

Als Alternative zu einer einzelnen flachen Liste können mithilfe von `<group>`-Elementen in `<references>` Verweise auf der Grundlage des Frameworkprofils des Zielprojekts angegeben werden.

Jede Gruppe verfügt über ein Attribut namens `targetFramework` und enthält null oder mehr `<reference>`-Elemente. Diese Verweise werden einem Projekt hinzugefügt, wenn das Zielframework mit dem Frameworkprofil des Projekts kompatibel ist.

Das `<group>`-Element ohne `targetFramework`-Attribut wird als Standard- oder Fallbackliste für Verweise verwendet. Die genauen Frameworkbezeichner finden Sie unter [Zielframeworks](../reference/target-frameworks.md).

> [!Important]
> Das Gruppenformat kann nicht mit einer flachen Liste vermischt werden.

Im folgenden Beispiel werden verschiedene Variationen des `<group>`-Elements dargestellt:

```xml
<references>
    <group>
        <reference file="a.dll" />
    </group>

    <group targetFramework="net45">
        <reference file="b45.dll" />
    </group>

    <group targetFramework="netcore45">
        <reference file="bcore45.dll" />
    </group>
</references>
```

<a name="specifying-framework-assembly-references-gac"></a>

## <a name="framework-assembly-references"></a>Verweise auf Frameworkassemblys

Frameworkassemblys gehören zum .NET Framework und sollten für jeden vorhandenen Computer bereits im globalen Assemblycache vorhanden sein. Durch Angabe dieser Assemblys im `<frameworkAssemblies>`-Element können Pakete sicherstellen, dass erforderliche Verweise einem Projekt hinzugefügt werden, falls das Projekt noch nicht über solche Verweise verfügt. Derartige Assemblys sind natürlich nicht von Anfang an in Paketen enthalten.

Das `<frameworkAssemblies>`-Element enthält null oder mehr `<frameworkAssembly>`-Elemente, die jeweils die folgenden Attribute angeben:

| Attribut | Beschreibung |
| --- | --- |
| **assemblyName** | (Erforderlich) Vollqualifizierter Assemblyname. |
| **targetFramework** | (Optional) Gibt das Zielframework an, auf das sich dieser Verweis bezieht. Das Fehlen des Attributs weist darauf hin, dass der Verweis für alle Frameworks gilt. Die genauen Frameworkbezeichner finden Sie unter [Zielframeworks](../reference/target-frameworks.md). |

Das folgende Beispiel zeigt einen Verweis auf `System.Net` für alle Zielframeworks sowie einen weiteren Verweis auf `System.ServiceModel`, der ausschließlich für .NET Framework 4.0 gilt:

```xml
<frameworkAssemblies>
    <frameworkAssembly assemblyName="System.Net"  />

    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
</frameworkAssemblies>
```

<a name="specifying-files-to-include-in-the-package"></a>

## <a name="including-assembly-files"></a>Einschließen von Assemblydateien

Wenn Sie die unter [Erstellen von NuGet-Paketen](../create-packages/creating-a-package.md) beschriebenen Konventionen beachten, müssen Sie nicht explizit eine Liste mit Dateien in der `.nuspec`-Datei angeben. Der `nuget pack`-Befehl ruft die benötigten Dateien automatisch ab.

> [!Important]
> Wenn ein Paket in einem Projekt installiert wird, fügt NuGet der DLL des Pakets automatisch Assemblyverweise hinzu. Verweise namens `.resources.dll` werden dabei allerdings *nicht* hinzugefügt, da angenommen wird, dass es sich dabei um lokalisierte Satellitenassemblys handelt. Vermeiden Sie aus diesem Grund die Verwendung von `.resources.dll` für Dateien, die darüber hinaus wichtigen Paketcode enthalten.

Wenn Sie diese automatischen Abläufe umgehen und explizit steuern möchten, welche Dateien in einem Paket enthalten sein sollen, legen Sie ein `<files>`-Element als untergeordnetes Element von `<package>` (und gleichgeordnetes Element von `<metadata>`) fest, das jede Datei mit einem separaten `<file>`-Element benennt. Zum Beispiel:

```xml
<files>
    <file src="bin\Debug\*.dll" target="lib" />
    <file src="bin\Debug\*.pdb" target="lib" />
    <file src="tools\**\*.*" exclude="**\*.log" />
</files>
```

Das `<files>`-Element wird außerdem bei NuGet 2.x und früher sowie bei Projekten, die `packages.config` verwenden, zum Einschließen unveränderlicher Inhaltsdateien während der Paketinstallation benutzt. Seit NuGet 3.3 und bei Projekten, die PackageReference verwenden, wird stattdessen das `<contentFiles>`-Element verwendet. Weitere Informationen finden Sie unter [Einschließen von Inhaltsdateien](#including-content-files).

### <a name="file-element-attributes"></a>Dateielementattribute

Jedes `<file>`-Element gibt die folgenden Attribute an:

| Attribut | Beschreibung |
| --- | --- |
| **src** | Speicherort der einzuschließenden Dateien. Hierbei werden die vom `exclude`-Attribut angegebenen Ausschlüsse berücksichtigt. Der Pfad ist relativ zur `.nuspec`-Datei, sofern kein absoluter Pfad angegeben ist. Das Platzhalterzeichen `*` ist zulässig, und das doppelte Platzhalterzeichen `**` impliziert eine rekursive Ordnersuche. |
| **target** | Relativer Pfad zu dem Ordner im Paket, in dem die Quelldateien abgelegt sind. Dieser muss mit `lib`, `content`, `build` oder `tools` beginnen. Informationen hierzu finden Sie unter [Erstellen der NUSPEC-Datei > Aus einem konventionsbasierten Arbeitsverzeichnis](../create-packages/creating-a-package.md#from-a-convention-based-working-directory). |
| **exclude** | Eine mit Semikolons getrennte Datei oder ein Muster für Dateien, die aus dem `src`-Speicherort ausgeschlossen werden. Das Platzhalterzeichen `*` ist zulässig, und das doppelte Platzhalterzeichen `**` impliziert eine rekursive Ordnersuche. |

### <a name="examples"></a>Beispiele

**Einzelne Assembly**

    Source file:
        library.dll

    .nuspec entry:
        <file src="library.dll" target="lib" />

    Packaged result:
        lib\library.dll

**Einzelne Assembly, die für ein Zielframework spezifisch ist**

    Source file:
        library.dll

    .nuspec entry:
        <file src="assemblies\net40\library.dll" target="lib\net40" />

    Packaged result:
        lib\net40\library.dll

**Mehrere DLLs mit Verwendung eines Platzhalterzeichens**

    Source files:
        bin\release\libraryA.dll
        bin\release\libraryB.dll

    .nuspec entry:
        <file src="bin\release\*.dll" target="lib" />

    Packaged result:
        lib\libraryA.dll
        lib\libraryB.dll

**DLLs für verschiedene Frameworks**

    Source files:
        lib\net40\library.dll
        lib\net20\library.dll

    .nuspec entry (using ** recursive search):
        <file src="lib\**" target="lib" />

    Packaged result:
        lib\net40\library.dll
        lib\net20\library.dll

**Ausschließen von Dateien**

    Source files:
        \tools\fileA.bak
        \tools\fileB.bak
        \tools\fileA.log
        \tools\build\fileB.log

    .nuspec entries:
        <file src="tools\*.*" target="tools" exclude="tools\*.bak" />
        <file src="tools\**\*.*" target="tools" exclude="**\*.log" />

    Package result:
        (no files)

## <a name="including-content-files"></a>Einschließen von Inhaltsdateien

Bei Inhaltsdateien handelt es sich um unveränderliche Dateien, die ein Paket in ein Projekt einschließen muss. Da sie unveränderlich sind, sollten sie auch nicht von dem verarbeitenden Projekt geändert werden. Zu den Inhaltsdateien gehören z.B.:

- Bilder, die als Ressourcen eingebettet werden
- bereits kompilierte Quelldateien
- Skripts, die in die Buildausgabe des Projekts eingeschlossen werden müssen
- Konfigurationsdateien für das Paket, die zwar in das Projekt eingeschlossen werden müssen, an denen jedoch keine projektspezifischen Änderungen vorgenommen werden müssen

Inhaltsdateien werden mithilfe eines `<files>`-Elements in ein Paket eingeschlossen. Dieses Element gibt den `content`-Ordner im `target`-Attribut an. Allerdings werden diese Dateien ignoriert, wenn das Paket per PackageReference in einem Projekt installiert wird, das stattdessen das `<contentFiles>`-Element verwendet.

Im Idealfall geben Pakete die Inhaltsdateien in beiden Elementen an, um ein Höchstmaß an Kompatibilität mit den verarbeitenden Projekten zu erreichen.

### <a name="using-the-files-element-for-content-files"></a>Verwenden des Dateielements für Inhaltsdateien

Verwenden Sie für Inhaltsdateien einfach dasselbe Format wie für Assemblydateien. Geben Sie dabei allerdings  wie in den folgenden Beispielen dargestellt `content` als Basisordner im `target`-Attribut an.

**Grundlegende Inhaltsdateien**

    Source files:
        css\mobile\style1.css
        css\mobile\style2.css

    .nuspec entry:
        <file src="css\mobile\*.css" target="content\css\mobile" />

    Packaged result:
        content\css\mobile\style1.css
        content\css\mobile\style2.css

**Inhaltsdateien mit Verzeichnisstruktur**

    Source files:
        css\mobile\style.css
        css\mobile\wp7\style.css
        css\browser\style.css

    .nuspec entry:
        <file src="css\**\*.css" target="content\css" />

    Packaged result:
        content\css\mobile\style.css
        content\css\mobile\wp7\style.css
        content\css\browser\style.css

**Inhaltsdatei für ein bestimmtes Zielframework**

    Source file:
        css\cool\style.css

    .nuspec entry
        <file src="css\cool\style.css" target="Content" />

    Packaged result:
        content\style.css

**Inhaltsdatei, die in einen Ordner mit einem Punkt im Namen kopiert wird**

In diesem Fall erkennt NuGet, dass die Erweiterung in `target` nicht mit der Erweiterung in `src` übereinstimmt, und behandelt diesen Namensbestandteil in `target` als Ordner:

    Source file:
        images\picture.png

    .nuspec entry:
        <file src="images\picture.png" target="Content\images\package.icons" />

    Packaged result:
        content\images\package.icons\picture.png

**Inhaltsdateien ohne Erweiterungen**

Verwenden Sie die Platzhalterzeichen `*` oder `**`, um Dateien ohne Erweiterungen einzuschließen:

    Source file:
        flags\installed

    .nuspec entry:
        <file src="flags\**" target="flags" />

    Packaged result:
        flags\installed

**Inhaltsdateien mit langen Pfaden und langen Zielen**

In diesem Fall nimmt NuGet an, dass das Ziel ein Dateiname und kein Ordner ist, da die Dateierweiterungen von Quelle und Ziel übereinstimmen:

    Source file:
        css\cool\style.css

    .nuspec entry:
        <file src="css\cool\style.css" target="Content\css\cool" />
        or:
        <file src="css\cool\style.css" target="Content\css\cool\style.css" />

    Packaged result:
        content\css\cool\style.css

**Umbenennen einer Inhaltsdatei im Paket**

    Source file:
        ie\css\style.css

    .nuspec entry:
        <file src="ie\css\style.css" target="Content\css\ie.css" />

    Packaged result:
        content\css\ie.css

**Ausschließen von Dateien**

    Source file:
        docs\*.txt (multiple files)

    .nuspec entry:
        <file src="docs\*.txt" target="content\docs" exclude="docs\admin.txt" />
        or
        <file src="*.txt" target="content\docs" exclude="admin.txt;log.txt" />

    Packaged result:
        All .txt files from docs except admin.txt (first example)
        All .txt files from docs except admin.txt and log.txt (second example)

<a name="using-contentfiles-element-for-content-files"></a>

### <a name="using-the-contentfiles-element-for-content-files"></a>Verwenden des contentFiles-Elements für Inhaltsdateien

*NuGet 4.0 und höher mit PackageReference*

Standardmäßig legen Pakete Inhalte in einem `contentFiles`-Ordner (siehe unten) ab, in den `nuget pack` alle Dateien mithilfe von Standardattributen eingeschlossen hat. In diesem Fall ist es gar nicht notwendig, einen `contentFiles`-Knoten in `.nuspec` einzuschließen.

Um zu steuern, welche Dateien eingeschlossen werden, gibt das `<contentFiles>`-Element eine Sammlung mit `<files>`-Elementen an, die die einzuschließenden Dateien präzise angeben.

Die Angabe der Dateien erfolgt mithilfe mehrerer Attribute, die beschreiben, wie sie im Projektsystem verwendet werden sollen:

| Attribut | Beschreibung |
| --- | --- |
| **include** | (Erforderlich) Speicherort der Dateien, die eingeschlossen werden sollen. Hierbei werden die vom `exclude`-Attribut angegebenen Ausschlüsse berücksichtigt. Der Pfad ist relativ zur `.nuspec`-Datei, sofern kein absoluter Pfad angegeben ist. Das Platzhalterzeichen `*` ist zulässig, und das doppelte Platzhalterzeichen `**` impliziert eine rekursive Ordnersuche. |
| **exclude** | Eine mit Semikolons getrennte Datei oder ein Muster für Dateien, die aus dem `src`-Speicherort ausgeschlossen werden. Das Platzhalterzeichen `*` ist zulässig, und das doppelte Platzhalterzeichen `**` impliziert eine rekursive Ordnersuche. |
| **buildAction** | Die Buildaktion, die dem Inhaltselement für MSBuild zugewiesen werden soll, z.B. `Content`, `None`, `Embedded Resource` oder `Compile`. Die Standardeinstellung ist `Compile`. |
| **copyToOutput** | Boolescher Wert, mit dem angegeben wird, ob Inhaltselemente in den Buildausgabeordner (oder den Veröffentlichungsausgabeordner) kopiert werden sollen. Der Standardwert ist FALSE. |
| **flatten** | Boolescher Wert, der angibt, ob Inhaltselemente in einen Ordner in der Buildausgabe kopiert werden sollen (TRUE) oder die Ordnerstruktur in den Paketen beibehalten werden soll (FALSE). Dieses Flag funktioniert nur, wenn das copyToOutput-Flag auf TRUE festgelegt ist. Der Standardwert ist FALSE. |

Beim Installieren eines Pakets wendet NuGet die untergeordneten Elemente von `<contentFiles>` von oben nach unten an. Wenn mehrere Einträge derselben Datei entsprechen, werden sie alle angewendet. Der oberste Eintrag hat im Falle eines Attributkonflikts Vorrang vor den untergeordneten Einträgen.

#### <a name="package-folder-structure"></a>Paketordnerstruktur

Das Paketprojekt sollte Inhalte anhand des folgenden Musters strukturieren:

    /contentFiles/{codeLanguage}/{TxM}/{any?}

- `codeLanguages` kann `cs`, `vb`, `fs`, `any` oder das klein geschriebene Äquivalent einer `$(ProjectLanguage)` sein.
- `TxM` ist ein für das Zielframework zulässiger Moniker, den NuGet unterstützt (Informationen hierzu finden Sie unter [Zielframeworks](../reference/target-frameworks.md)).
- Ans Ende dieser Syntax kann eine beliebige Ordnerstruktur angehängt werden.

Zum Beispiel:

    Language- and framework-agnostic:
        /contentFiles/any/any/config.xml

    net45 content for all languages
        /contentFiles/any/net45/config.xml

    C#-specific content for net45 and up
        /contentFiles/cs/net45/sample.cs

Für leere Ordner kann `.` eingefügt werden, wenn diese keine Inhalte mehr für bestimmte Sprachen und TxM bereitstellen sollen. Zum Beispiel:

    /contentFiles/vb/any/code.vb
    /contentFiles/cs/any/.

#### <a name="example-contentfiles-section"></a>contentFiles-Beispielabschnitt

```xml
<contentFiles>
    <!-- Embed image resources -->
    <files include="any/any/images/dnf.png" buildAction="EmbeddedResource" />
    <files include="any/any/images/ui.png" buildAction="EmbeddedResource" />

    <!-- Embed all image resources under contentFiles/cs/ -->
    <files include="cs/**/*.png" buildAction="EmbeddedResource" />

    <!-- Copy config.xml to the root of the output folder -->
    <files include="cs/uap/config/config.xml" buildAction="None" copyToOutput="true" flatten="true" />

    <!-- Copy run.cmd to the output folder and keep the directory structure -->
    <files include="cs/commands/run.cmd" buildAction="None" copyToOutput="true" flatten="false" />

    <!-- Include everything in the scripts folder except exe files -->
    <files include="cs/net45/scripts/*" exclude="**/*.exe"  buildAction="None" copyToOutput="true" />
</contentFiles>
```

## <a name="example-nuspec-files"></a>NUSPEC-Beispieldateien

**Einfache `.nuspec`-Datei, die weder Abhängigkeiten noch Dateien enthält**

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>sample</id>
        <version>1.2.3</version>
        <authors>Kim Abercrombie, Franck Halmaert</authors>
        <description>Sample exists only to show a sample .nuspec file.</description>
        <language>en-US</language>
        <projectUrl>http://xunit.codeplex.com/</projectUrl>
        <license type="expression">MIT</license>
    </metadata>
</package>
```

**`.nuspec`-Datei mit Abhängigkeiten**

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>sample</id>
        <version>1.0.0</version>
        <authors>Microsoft</authors>
        <dependencies>
            <dependency id="another-package" version="3.0.0" />
            <dependency id="yet-another-package" version="1.0.0" />
        </dependencies>
    </metadata>
</package>
```

**`.nuspec`-Datei mit Dateien**

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>routedebugger</id>
        <version>1.0.0</version>
        <authors>Jay Hamlin</authors>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Route Debugger is a little utility I wrote...</description>
    </metadata>
    <files>
        <file src="bin\Debug\*.dll" target="lib" />
    </files>
</package>
```

**`.nuspec`-Datei mit Frameworkassemblys**

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>PackageWithGacReferences</id>
        <version>1.0</version>
        <authors>Author here</authors>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>
            A package that has framework assemblyReferences depending
            on the target framework.
        </description>
        <frameworkAssemblies>
            <frameworkAssembly assemblyName="System.Web" targetFramework="net40" />
            <frameworkAssembly assemblyName="System.Net" targetFramework="net40-client, net40" />
            <frameworkAssembly assemblyName="Microsoft.Devices.Sensors" targetFramework="sl4-wp" />
            <frameworkAssembly assemblyName="System.Json" targetFramework="sl3" />
        </frameworkAssemblies>
    </metadata>
</package>
```

In diesem Beispiel werden die folgenden Elemente für bestimmte Projektziele installiert:

- .NET4: `System.Web` und `System.Net`
- .NET4-Clientprofil: `System.Net`
- Silverlight 3: `System.Json`
- Silverlight 4: `System.Windows.Controls.DomainServices`
- WindowsPhone: `Microsoft.Devices.Sensors`
