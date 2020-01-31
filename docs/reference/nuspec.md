---
title: NUSPEC-Dateireferenz für NuGet
description: Die NUSPEC-Datei enthält Paketmetadaten, die bei der Erstellung eines Pakets verwendet werden, um für die Paketbenutzer Informationen bereitzustellen.
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: ccb9c21041bef6f2bb791667a6e08b36c55b3e1f
ms.sourcegitcommit: e9c1dd0679ddd8ba3ee992d817b405f13da0472a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/29/2020
ms.locfileid: "76813155"
---
# <a name="nuspec-reference"></a>NUSPEC-Referenz

Bei einer `.nuspec`-Datei handelt es sich um eine XML-Manifestdatei, die Paketmetadaten enthält. Diese Manifestdatei wird sowohl für die Erstellung des Pakets als auch zur Bereitstellung von Informationen für die Benutzer verwendet. Manifestdateien sind in allen Paketen enthalten.

In diesem Abschnitt:

- [Allgemeine Form und Schema](#general-form-and-schema)
- [Ersetzungstokens](#replacement-tokens) (bei der Verwendung in einem Visual Studio-Projekt)
- [Abhängigkeiten](#dependencies)
- [Explizite Assemblyverweise](#explicit-assembly-references)
- [Verweise auf Frameworkassemblys](#framework-assembly-references)
- [Einfügen von Assemblydateien](#including-assembly-files)
- [Einfügen von Inhaltsdateien](#including-content-files)
- [NUSPEC-Beispieldateien](#example-nuspec-files)

## <a name="project-type-compatibility"></a>Projekttyp Kompatibilität

- Verwenden Sie `.nuspec` mit `nuget.exe pack` für Projekte ohne SDK-Stil, die `packages.config`verwenden.

- Zum Erstellen von Paketen für [Projekte im SDK-Stil](../resources/check-project-format.md) ist keine Dateierforderlich(inderRegel.netCore-und.NETStandardProjekte,[diedasSDK-Attributverwenden](/dotnet/core/tools/csproj#additions)`.nuspec` ). (Beachten Sie, dass ein `.nuspec` generiert wird, wenn Sie das Paket erstellen.)

   Wenn Sie ein Paket mit `dotnet.exe pack` oder `msbuild pack target`erstellen, empfiehlt es sich, stattdessen [alle Eigenschaften](../reference/msbuild-targets.md#pack-target) , die normalerweise in der `.nuspec`-Datei enthalten sind, in die Projektdatei einzubeziehen. Stattdessen können Sie jedoch auch [eine `.nuspec` Datei verwenden, um Sie mit `dotnet.exe` oder `msbuild pack target`zu verpacken ](../reference/msbuild-targets.md#packing-using-a-nuspec).

- Für Projekte, die von `packages.config` zu [packagereferenzierung](../consume-packages/package-references-in-project-files.md)migriert wurden, ist eine `.nuspec` Datei zum Erstellen des Pakets nicht erforderlich. Verwenden Sie stattdessen [msbuild-t:Pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).

## <a name="general-form-and-schema"></a>Allgemeine Form und Schema

Die aktuelle `nuspec.xsd`-Schemadatei finden Sie im [NuGet GitHub-Repository](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).

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

Für eine übersichtliche Darstellung des Schemas öffnen Sie die Schemadatei im Entwurfsmodus in Visual Studio, und klicken Sie auf den Link **XML-Schema-Explorer**. Alternativ können Sie auch die Datei als Code öffnen, mit der rechten Maustaste in den Editor klicken und **Show XML Schema Explorer** (XML-Schema-Explorer anzeigen) auswählen. In beiden Fällen wird eine Ansicht zurückgegeben, die der in der folgenden Abbildung ähnlich ist, wenn Sie größtenteils erweitert ist:

![Visual Studio-Schema-Explorer mit geöffneter „nuspec.xsd“-Datei](media/SchemaExplorer.png)

### <a name="required-metadata-elements"></a>Erforderliche Metadatenelemente

Obwohl es sich bei den folgenden Elementen um die Mindestanforderungen für ein Paket handelt, sollten Sie in Erwägung ziehen, die [optionalen Metadatenelemente](#optional-metadata-elements) hinzuzufügen, damit Entwicklern die Arbeit mit Ihren Paketen erleichtert wird. 

Diese Elemente müssen in einem `<metadata>`-Element angezeigt werden.

#### <a name="id"></a>ID 
Der Paketbezeichner, der die Groß- und Kleinschreibung nicht berücksichtigt und auf nuget.org oder im für das Paket verwendeten Katalog eindeutig sein muss. IDs dürfen keine Leerzeichen oder für eine URL unzulässige Zeichen enthalten. Sie müssen den Regeln für .NET-Namespaces entsprechen. Informationen finden Sie unter [Choosing a unique package identifier (Auswählen eines eindeutigen Paketbezeichners)](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number).
#### <a name="version"></a>-Version
Die Version des Pakets, die dem Muster *Hauptversion.Nebenversion.Patch* folgt. Versionsnummern enthalten möglicherweise, wie unter [Paketversionsverwaltung](../concepts/package-versioning.md#pre-release-versions) beschrieben, ein Suffix der Vorabversion. 
#### <a name="description"></a>Beschreibung
Eine Beschreibung des Pakets für die Anzeige der Benutzeroberfläche.
#### <a name="authors"></a>authors
Eine durch Trennzeichen getrennte Liste von Paket Autoren, die mit den Profilnamen auf nuget.org übereinstimmen. Diese werden in der nuget-Galerie auf nuget.org angezeigt und werden verwendet, um die Verweise auf Pakete durch dieselben Autoren zu über verweisen. 

### <a name="optional-metadata-elements"></a>Optionale Metadatenelemente

#### <a name="owners"></a>owners
Eine durch Trennzeichen getrennte Liste der Paket Ersteller, die Profilnamen auf nuget.org verwenden. Dies ist oft die gleiche Liste wie in `authors`und wird beim Hochladen des Pakets in nuget.org ignoriert. Weitere Informationen finden Sie [unter Verwalten von Paket Besitzern auf nuget.org](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg). 

#### <a name="projecturl"></a>projectUrl
Eine URL für die Paket-Homepage, häufig auf der Benutzeroberfläche sowie auf nuget.org angezeigt. 

#### <a name="licenseurl"></a>licenseUrl
> [!Important]
> "licenaburl" ist veraltet. Verwenden Sie stattdessen die Lizenz.

Eine URL für die Lizenz des Pakets, die häufig in Benutzeroberflächen wie nuget.org angezeigt wird.

#### <a name="license"></a>Lizenz
Ein spdx-Lizenz Ausdruck oder Pfad zu einer Lizenzdatei innerhalb des Pakets, die häufig in Benutzeroberflächen wie nuget.org angezeigt wird. Wenn Sie das Paket unter einer gemeinsamen Lizenz lizenzieren, wie z. b. mit oder der BSD-2-Klausel, verwenden Sie den zugehörigen [spdx-Lizenz Bezeichner](https://spdx.org/licenses/). Beispiel:

`<license type="expression">MIT</license>`

> [!Note]
> NuGet.org akzeptiert nur Lizenz Ausdrücke, die von der Open Source-Initiative oder der kostenlosen Software Foundation genehmigt werden.

Wenn Ihr Paket unter mehreren gängigen Lizenzen lizenziert ist, können Sie eine zusammengesetzte Lizenz mithilfe der [spdx-Ausdruckssyntax Version 2,0](https://spdx.org/spdx-specification-21-web-version#h.jxpfx0ykyb60)angeben. Beispiel:

`<license type="expression">BSD-2-Clause OR MIT</license>`

Wenn Sie eine benutzerdefinierte Lizenz verwenden, die nicht von Lizenz Ausdrücken unterstützt wird, können Sie eine `.txt` oder eine `.md` Datei mit dem Lizenztext verpacken. Beispiel:

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

Die MSBuild-Entsprechung finden Sie unter [packen eines Lizenz Ausdrucks oder einer Lizenzdatei](msbuild-targets.md#packing-a-license-expression-or-a-license-file).

Die genaue Syntax der nuget-Lizenz Ausdrücke wird unten in [ABNF](https://tools.ietf.org/html/rfc5234)beschrieben.
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

> [!Important]
> IconUrl ist veraltet. Verwenden Sie stattdessen das-Symbol.

Eine URL für ein 128 x 128-Bild mit Transparenz Hintergrund, das als Symbol für das Paket in der Anzeige der Benutzeroberfläche verwendet werden soll. Stellen Sie sicher, dass dieses Element die *direkte Bild-URL* und nicht nur die URL einer Webseite enthält, die das Bild enthält. Wenn Sie beispielsweise ein Bild auf GitHub verwenden möchten, geben Sie die URL der Rohdatendatei an (z. B. <em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>). 
   
#### <a name="icon"></a>angezeigt

Dabei handelt es sich um einen Pfad zu einer Bilddatei innerhalb des Pakets, die häufig in UIs like nuget.org als Paket Symbol angezeigt wird. Die Größe der Bild Datei ist auf 1 MB beschränkt. Unterstützte Dateiformate sind JPEG und PNG. Wir empfehlen eine Bildauflösung von 128 x 128.

Beim Erstellen eines Pakets mithilfe von "nuget. exe" fügen Sie z. b. Folgendes zu "nuspec" hinzu:

```xml
<package>
  <metadata>
    ...
    <icon>images\icon.png</icon>
    ...
  </metadata>
  <files>
    ...
    <file src="..\icon.png" target="images\" />
    ...
  </files>
</package>
```

[Paket Symbol nuspec-Beispiel.](https://github.com/NuGet/Samples/tree/master/PackageIconNuspecExample)

Wenn Sie die MSBuild-Entsprechung benötigen, sehen Sie sich das [Packen einer Symbolbild Datei](msbuild-targets.md#packing-an-icon-image-file)an.

> [!Tip]
> Sie können sowohl `icon` als auch `iconUrl` angeben, um die Abwärtskompatibilität mit Quellen zu gewährleisten, die `icon`nicht unterstützen. Visual Studio unterstützt `icon` für Pakete, die in einer zukünftigen Version aus einer Ordner basierten Quelle stammen.

#### <a name="requirelicenseacceptance"></a>requireLicenseAcceptance
Ein boolescher Wert, der angibt, ob der Client den Benutzer dazu auffordern muss, die Paketlizenz vor der Installation des Pakets zu akzeptieren.

#### <a name="developmentdependency"></a>developmentDependency
*(2.8 und höher)* Ein boolescher Wert, der angibt, ob das Paket mit einer Abhängigkeit markiert werden soll, die nur für die Entwicklung gilt, wodurch vermieden wird, dass das Paket als Abhängigkeit in andere Pakete eingefügt wird. Mit packagereferen(nuget 4.8 und höher) bedeutet dieses Flag auch, dass die Kompilierzeit Ressourcen von der Kompilierung ausgeschlossen werden. Weitere Informationen finden Sie [unter Unterstützung von "developmentdependependenz](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference) "

#### <a name="summary"></a>Zusammenfassung
> [!Important]
> `summary` ist veraltet. Verwenden Sie stattdessen `description` .

Eine kurze Beschreibung des Pakets für die Anzeige der Benutzeroberfläche. Wenn diese nicht angegeben wird, wird eine gekürzte Version von `description` verwendet.

#### <a name="releasenotes"></a>releaseNotes
*(1.5 und höher)* Eine Beschreibung der in diesem Release des Pakets enthaltenen Änderungen, die häufig in Benutzeroberflächen wie der Registerkarte **Updates** des Visual Studio-Paket-Managers anstelle von Paketbeschreibungen verwendet wird.

#### <a name="copyright"></a>Copyright
*(1.5 und höher)* Copyright-Informationen zum Paket.

#### <a name="language"></a>language
Die Gebietsschema-ID des Pakets. Informationen dazu finden Sie unter [Creating localized packages (Erstellen von lokalisierten Paketen)](../create-packages/creating-localized-packages.md).

#### <a name="tags"></a>Tags
Eine durch Leerzeichen getrennte Liste mit Tags und Schlüsselwörtern, die das Paket beschreiben und zum Ermitteln von Paketen über Suchvorgänge und Filter beitragen. 

#### <a name="serviceable"></a>serviceable 
*(3.3 und höher)* Nur für die interne Verwendung von NuGet.

#### <a name="repository"></a>Repository
Repository-Metadaten, bestehend aus vier optionalen Attributen: `type` und `url` *(4.0*und höher) sowie `branch` und `commit` *(4.6*und höher). Diese Attribute ermöglichen es Ihnen, den `.nupkg` dem Repository zuzuordnen, von dem es erstellt wurde, und mit der Möglichkeit, den einzelnen branchnamen und/oder den SHA-1-Hash, der das Paket erstellt hat, so detailliert wie möglich zu machen. Hierbei sollte es sich um eine öffentlich zugängliche URL handeln, die direkt von einer Versionskontrollsoftware aufgerufen werden kann. Dagegen sollte es keine HTML-Seite sein, da diese für den Computer vorgesehen ist. Zur Verknüpfung mit der Projektseite verwenden Sie stattdessen das Feld `projectUrl`.

Beispiel:
```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2016/06/nuspec.xsd">
    <metadata>
        ...
        <repository type="git" url="https://github.com/NuGet/NuGet.Client.git" branch="dev" commit="e1c65e4524cd70ee6e22abe33e6cb6ec73938cb3" />
        ...
    </metadata>
</package>
```

#### <a name="title"></a>Titel
Ein benutzerfreundlicher Titel des Pakets, das in einigen Benutzeroberflächen anzeigen verwendet werden kann. (nuget.org und der Paket-Manager in Visual Studio zeigen keinen Titel an.)

#### <a name="collection-elements"></a>Auflistungselemente

#### <a name="packagetypes"></a>packageTypes
*(3.5 und höher)* Eine Auflistung, die kein `<packageType>`-Element oder mindestens eins enthält und den Pakettyp angibt, wenn es sich nicht um ein gewöhnliches Abhängigkeitspaket handelt. Jeder „packageType“ verfügt über Attribute von *name* und *version*. Informationen dazu finden Sie unter [Setting a package type (Festlegen eines Pakettypen)](../create-packages/set-package-type.md).
#### <a name="dependencies"></a>Abhängigkeiten
Eine Auflistung, die kein `<dependency>`-Element oder mindestens eins enthält und Abhängigkeiten für das Paket angibt. Jede Abhängigkeit verfügt über Attribute von *id*, *version*, *include* und *exclude* (3.x und höher). Informationen dazu finden Sie im Abschnitt [Abhängigkeiten](#dependencies-element).
#### <a name="frameworkassemblies"></a>frameworkAssemblies
*(1.2 und höher)* Eine Auflistung, die kein `<frameworkAssembly>`-Element oder mindestens eins enthält und die für das Paket erforderlichen Verweise auf .NET Framework-Assemblys erkennt und sicherstellt, dass Verweise zu Projekten hinzugefügt werden, die das Paket verarbeiten. Jedes frameworkAssembly-Element verfügt über die Attribute *assemblyName* und *targetFramework*. Informationen dazu finden Sie unter [Specifying framework assembly references GAC (Angeben von GAC-Verweisen auf Frameworkassemblys)](#specifying-framework-assembly-references-gac).
#### <a name="references"></a>Verweise
*(1.5 und höher)* Eine Auflistung, die kein `<reference>`-Element oder mindestens eins enthält, das Assemblys in dem `lib`-Ordner des Pakets benennt, die als Projektverweise hinzugefügt werden. Jeder Verweis verfügt über ein *file*-Attribut. `<references>` kann außerdem ein `<group>`-Element mit einem *targetFramework*-Attribut enthalten, das anschließend `<reference>`-Elemente enthält. Wenn das Element nicht angegeben ist, werden alle Verweise in `lib` eingefügt. Informationen dazu finden Sie unter [Specifying explicit assembly references (Angeben von expliziten Assemblyverweisen)](#specifying-explicit-assembly-references).
#### <a name="contentfiles"></a>contentFiles
*(3.3 und höher)* Eine Auflistung von `<files>`-Elementen, die Inhaltsdateien ermitteln, die in das verarbeitende Projekt eingefügt werden sollen. Diese Dateien werden zusammen mit mehreren Attributen angegeben, die beschreiben, wie sie in dem Projektsystem verwendet werden sollen. Informationen dazu finden Sie unter [Specifying files to include in the package (Angeben von Dateien, die in das Paket eingefügt werden sollen)](#specifying-files-to-include-in-the-package).
#### <a name="files"></a>Dateien 
Der `<package>` Knoten kann einen `<files>` Knoten als gleich geordnetes Element für `<metadata>`und ein untergeordnetes `<contentFiles>` unter `<metadata>`enthalten, um anzugeben, welche Assembly-und Inhalts Dateien in das Paket eingeschlossen werden sollen. Details dazu finden Sie im Folgenden in den Abschnitten [Einfügen von Assemblydateien](#including-assembly-files) und [Einfügen von Inhaltsdateien](#including-content-files).

### <a name="metadata-attributes"></a>Metadatenattribute

#### <a name="minclientversion"></a>minClientVersion
Gibt die minimale Version des NuGet-Clients an, der dieses Paket installieren kann. Dies wird von nuget.exe und dem Paket-Manager von Visual Studio erzwungen. Dieses Attribut wird verwendet, wenn das Paket von bestimmten Funktionen der `.nuspec`-Datei abhängig ist, die in einer bestimmten Version des NuGet-Clients hinzugefügt wurden. Beispielsweise sollte ein Paket, das das `developmentDependency`-Attribut verwendet, „2.8“ für `minClientVersion` angeben. Genauso sollte ein Paket, das das `contentFiles`-Element verwendet (vgl. nächster Abschnitt), `minClientVersion` auf „3.3“ festlegen. Beachten Sie außerdem, dass NuGet-Clients vor Version 2.5 diese Kennzeichnung nicht erkennen und daher die Installation des Pakets, unabhängig vom Inhalt von `minClientVersion`, *immer* verweigern.

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2013/01/nuspec.xsd">
    <metadata minClientVersion="100.0.0.1">
        <id>dasdas</id>
        <version>2.0.0</version>
        <title />
        <authors>dsadas</authors>
        <owners />
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>My package description.</description>
    </metadata>
    <files>
        <file src="content\one.txt" target="content\one.txt" />
    </files>
</package>
```

## <a name="replacement-tokens"></a>Ersetzungstokens

Bei der Erstellung eines Pakets ersetzt der [`nuget pack`-Befehl](../reference/cli-reference/cli-ref-pack.md) durch $ getrennte Tokens im `<metadata>`-Knoten der `.nuspec`-Datei durch Werte, die entweder einer Projektdatei oder dem `-properties`-Schalter des `pack`-Befehls entstammen.

Geben Sie in der Befehlszeile die Tokenwerte mit `nuget pack -properties <name>=<value>;<name>=<value>` an. Beispielsweise können Sie ein Token wie `$owners$` und `$desc$` in der `.nuspec`-Datei verwenden und die Werte zur Packzeit wie im Folgenden dargestellt bereitstellen:

```ps
nuget pack MyProject.csproj -properties
    owners=janedoe,harikm,kimo,xiaop;desc="Awesome app logger utility"
```

Geben Sie die in der untenstehenden Tabelle beschriebenen Tokens an, um Werte aus einem Projekt zu verwenden (AssemblyInfo verweist auf Dateien wie `AssemblyInfo.cs` oder `AssemblyInfo.vb` in `Properties`).

Führen Sie anstelle von `.nuspec` nur `nuget pack` in der Projektdatei aus, um diese Tokens zu verwenden. Beispielsweise werden bei der Verwendung des folgenden Befehls die Tokens `$id$` und `$version$` in einer `.nuspec`-Datei durch die Werte `AssemblyName` und `AssemblyVersion` des Projekts ersetzt:

```ps
nuget pack MyProject.csproj
```

In der Regel erstellen Sie `.nuspec` in einem Projekt zuerst mithilfe von `nuget spec MyProject.csproj`, wodurch automatisch einige dieser Standardtokens eingefügt werden. Wenn in einem Projekt allerdings keine Werte für erforderliche `.nuspec`-Elemente enthalten sind, schlägt `nuget pack` fehl. Stellen Sie außerdem bei der Änderung von Projektwerten sicher, dass Sie diese neu erstellen, bevor Sie das Paket erstellen. Dies können Sie ganz einfach über den `build`-Paketschalter des Befehls tun.

Mit Ausnahme von `$configuration$` werden Werte in dem Projekt gegenüber Werten bevorzugt, die demselben Token in der Befehlszeile zugeordnet sind.

| Token | Wertquelle | {2&gt;Wert&lt;2}
| --- | --- | ---
| **$id$** | Projektdatei | "AssemblyName" (Titel) aus der Projektdatei |
| **$version$** | AssemblyInfo | „AssemblyInformationalVersion“, falls vorhanden, andernfalls „AssemblyVersion“ |
| **$author$** | AssemblyInfo | AssemblyCompany |
| **$title$** | AssemblyInfo | AssemblyTitle |
| **$description$** | AssemblyInfo | AssemblyDescription |
| **$copyright$** | AssemblyInfo | AssemblyCopyright |
| **$configuration$** | Assembly-DLL | Konfiguration, die zur Erstellung der Assembly verwendet wird und standardmäßig auf „Debuggen“ festgelegt ist. Achten Sie darauf, dass Sie stets `-properties Configuration=Release` in der Befehlszeile verwenden, um mithilfe einer Releasekonfiguration ein Paket zu erstellen. |

Tokens können auch zum Auflösen von Pfaden verwendet werden, wenn Sie [Assemblydateien](#including-assembly-files) und [Inhaltsdateien](#including-content-files) hinzufügen. Die Namen der Tokens und der MSBuild-Eigenschaften stimmen miteinander überein, wodurch Sie abhängig von der aktuellen Buildkonfiguration Dateien auswählen können, die eingefügt werden sollen. Wenn Sie beispielsweise die folgenden Tokens in der `.nuspec`-Datei verwenden

```xml
<files>
    <file src="bin\$configuration$\$id$.pdb" target="lib\net40" />
</files>
```

und Sie eine Assembly mit der `Release`-Konfiguration in MSBuild erstellen, deren `AssemblyName``LoggingLibrary` ist, sehen die dadurch entstandenen Zeilen in der `.nuspec`-Datei in den Paketen wie folgt aus:

```xml
<files>
    <file src="bin\Release\LoggingLibrary.pdb" target="lib\net40" />
</files>
```

## <a name="dependencies-element"></a>Abhängigkeitselement

Das `<dependencies>`-Element in `<metadata>` enthält eine beliebige Anzahl von `<dependency>`-Elementen, die andere Pakete finden, von denen die Pakete auf der obersten Ebene abhängig sind. Im Folgenden werden die Attribute für jede `<dependency>` dargestellt:

| Attribute | Beschreibung |
| --- | --- |
| `id` | (Erforderlich) Die Paket-ID der Abhängigkeit, z.B. „EntityFramework“ und „NUnit“, die der Name des Pakets „nuget.org“ ist, wird auf einer Paketseite angezeigt. |
| `version` | (Erforderlich) Der Bereich an Versionen, die als Abhängigkeiten akzeptiert werden. Die genaue Syntax finden Sie unter [Paketversionsverwaltung](../concepts/package-versioning.md#version-ranges-and-wildcards). Platzhalter Versionen (unverankert) werden nicht unterstützt. |
| include | Eine durch Kommas abgetrennte Liste mit Include/Exclude-Tags (s. Tabelle unten), in der auf die Abhängigkeit verwiesen wird, die in das endgültige Paket eingefügt werden soll. Der Standardwert ist `all`sein. |
| ausschließen | Eine durch Kommas abgetrennte Liste mit Include/Exclude-Tags (s. Tabelle unten), in der auf die Abhängigkeit verwiesen wird, die nicht in das endgültige Paket eingefügt werden soll. Der Standardwert ist `build,analyzers`. Er kann überschrieben werden. Allerdings werden implizit auch `content/ ContentFiles` aus dem endgültigen Paket ausgeschlossen, was sich nicht überschreiben lässt. `exclude`-Tags haben Vorrang gegenüber `include`-Tags. `include="runtime, compile" exclude="compile"` entspricht beispielsweise `include="runtime"`. |

| Include/Exclude-Tag | Betroffene Ordner im Ziel |
| --- | --- |
| contentFiles | Inhalt |
| -Laufzeit | Runtime, Ressourcen und Frameworkassemblys |
| Kompilieren | lib |
| Erstellen | Build (MSBuild-Eigenschaften und -Ziele) |
| Systemeigen | Systemeigen |
| Keine | Keine Ordner |
| alle | Alle Ordner |

Beispielsweise verweisen die folgenden Zeilen auf Abhängigkeiten auf `PackageA` Version 1.1.0 und höher und `PackageB` Version 1.x.

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" />
    <dependency id="PackageB" version="[1,2)" />
</dependencies>
```

In den folgenden Zeilen wird zwar auf Abhängigkeiten von denselben Paketen verwiesen, allerdings wird auch angegeben, dass die Ordner `contentFiles` und `build` von `PackageA` sowie alle anderen Ordner bis auf `native` und `compile` von `PackageB` angegeben werden sollen.

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" include="contentFiles, build" />
    <dependency id="PackageB" version="[1,2)" exclude="native, compile" />
</dependencies>
```

> [!Important]
> Beim Erstellen einer `.nuspec` aus einem Projekt mithilfe von `nuget spec`werden Abhängigkeiten, die in diesem Projekt vorhanden sind, nicht automatisch in die resultierende `.nuspec` Datei eingeschlossen. Verwenden Sie stattdessen `nuget pack myproject.csproj`, und holen Sie sich die *nuspec* -Datei aus der generierten *nupkg* -Datei. Diese *. nuspec* -Datei enthält die Abhängigkeiten.

### <a name="dependency-groups"></a>Abhängigkeitsgruppen

*Version 2.0 und höher*

Als Alternative zu einer einzelnen flachen Liste können Abhängigkeiten auf der Grundlage des Frameworkprofils des Zielprojekts angegeben werden, das `<group>`-Elemente in `<dependencies>` verwendet.

Jede Gruppe verfügt über ein Attribut mit dem Namen `targetFramework` und enthält entweder kein `<dependency>`-Element oder mindestens eins. Diese Abhängigkeiten werden zusammen installiert, wenn das Zielframework kompatibel mit dem Frameworkprofil des Projekts ist.

Das `<group>`-Element ohne ein `targetFramework`-Attribut wird als Standard- oder Ausweichliste der Abhängigkeiten verwendet. Die genauen Frameworkbezeichner finden Sie unter [Zielframeworks](../reference/target-frameworks.md).

> [!Important]
> Das Gruppenformat kann nicht mit einer flachen Liste vermischt werden.

Im folgenden Beispiel werden verschiedene Variationen des `<group>`-Elements dargestellt:

```xml
<dependencies>
    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>

    <group targetFramework="net40">
        <dependency id="jQuery" version="1.6.2" />
        <dependency id="WebActivator" version="1.4.4" />
    </group>

    <group targetFramework="sl30">
    </group>
</dependencies>
```

<a name="specifying-explicit-assembly-references"></a>

## <a name="explicit-assembly-references"></a>Explizite Assemblyverweise

Das `<references>`-Element wird von Projekten verwendet, die `packages.config` verwenden, um explizit die Assemblys anzugeben, auf die das Ziel Projekt bei Verwendung des Pakets verweisen soll. In der Regel werden Verweise nur für Assemblys zur Entwurfszeit verwendet. Weitere Informationen finden Sie auf der Seite zum [Auswählen von](../create-packages/select-assemblies-referenced-by-projects.md) Assemblys, auf die von-Projekten verwiesen wird.

Beispielsweise gibt das folgende `<references>`-Element NuGet die Anweisung, Verweise nur zu `xunit.dll` und `xunit.extensions.dll` hinzuzufügen, wenn zusätzliche Assemblys in dem Paket enthalten sind:

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

### <a name="reference-groups"></a>Verweisgruppen

Als Alternative zu einer einzelnen flachen Liste können Verweise auf der Grundlage des Frameworkprofils des Zielprojekts angegeben werden, das `<group>`-Elemente in `<references>` verwendet.

Jede Gruppe verfügt über ein Attribut mit dem Namen `targetFramework` und enthält entweder kein `<reference>`-Element oder mindestens eins. Diese Verweise werden einem Projekt hinzugefügt, wenn das Zielframework mit dem Frameworkprofil des Projekts kompatibel ist.

Das `<group>`-Element ohne ein `targetFramework`-Attribut wird als Standard- oder Ausweichliste der Verweise verwendet. Die genauen Frameworkbezeichner finden Sie unter [Zielframeworks](../reference/target-frameworks.md).

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

Frameworkassemblys gehören zum .NET Framework und sollten für jeden vorhandenen Computer bereits im globalen Assemblycache vorhanden sein. Pakete können sicherstellen, dass die erforderlichen Verweise, falls nötig, dem Projekt hinzugefügt werden, indem es diese Assemblys im `<frameworkAssemblies>`-Element erkennt. Solche Assemblys sind nicht von Anfang an in Paketen enthalten.

Das `<frameworkAssemblies>`-Element enthält entweder kein `<frameworkAssembly>`-Element oder mindestens eins, das die folgenden Attribute angibt:

| Attribute | Beschreibung |
| --- | --- |
| **assemblyName** | (Erforderlich) Der vollqualifizierte Assemblyname. |
| **targetFramework** | (Optional) Gibt das Zielframework an, auf das sich dieser Verweis bezieht. Wenn dieses Attribut nicht vorhanden ist, deutet dies darauf hin, dass sich der Verweis auf alle Frameworks bezieht. Die genauen Frameworkbezeichner finden Sie unter [Zielframeworks](../reference/target-frameworks.md). |

Im folgenden Beispiel werden Verweise auf `System.Net` für alle Zielframeworks und auf `System.ServiceModel` für ausschließlich .NET Framework 4.0 dargestellt:

```xml
<frameworkAssemblies>
    <frameworkAssembly assemblyName="System.Net"  />

    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
</frameworkAssemblies>
```

<a name="specifying-files-to-include-in-the-package"></a>

## <a name="including-assembly-files"></a>Einfügen von Assemblydateien

Wenn Sie die unter [Creating a Package (Erstellen eines Pakets)](../create-packages/creating-a-package.md) beschriebenen Anweisungen ausführen, müssen Sie nicht explizit eine Liste mit Dateien in der `.nuspec`-Datei angeben. Der `nuget pack`-Befehl ruft die benötigten Dateien automatisch ab.

> [!Important]
> Wenn ein Paket in einem Projekt installiert wird, fügt NuGet automatisch der DLL des Pakets Assemblyverweise hinzu. Die Verweise, die mit `.resources.dll` benannt sind werden dabei allerdings *nicht* hinzugefügt, da angenommen wird, dass es sich dabei um lokalisierte Satellitenassemblys handelt. Vermeiden Sie aus diesem Grund die Verwendung von `.resources.dll` für Dateien, die darüber hinaus wichtigen Paketcode enthalten.

Legen Sie ein `<files>`-Element als untergeordnetes Element von `<package>` und als gleichgeordnetes Element von `<metadata>` fest, das jeder Datei ein separates `<file>`-Element zuordnet, um diese automatischen Vorgänge zu umgehen und genau zu kontrollieren, welche Dateien in einem Paket enthalten sind. Beispiel:

```xml
<files>
    <file src="bin\Debug\*.dll" target="lib" />
    <file src="bin\Debug\*.pdb" target="lib" />
    <file src="tools\**\*.*" exclude="**\*.log" />
</files>
```

Das `<files>`-Element wird bei NuGet 2.x und früher sowie bei Projekten, die `packages.config` verwenden, außerdem verwendet, um unveränderliche Inhaltsdateien während der Paketinstallation einzufügen. Bei NuGet 3.3 und höher und Projekten, die PackageReference verwenden, wird stattdessen das `<contentFiles>`-Element verwendet. Weitere Informationen finden Sie unter [Einfügen von Inhaltsdateien](#including-content-files).

### <a name="file-element-attributes"></a>Dateielementattribute

Jedes `<file>`-Element gibt die folgenden Attribute an:

| Attribute | Beschreibung |
| --- | --- |
| **src** | Der Speicherort der Dateien, die eingefügt werden sollen, unterliegt Ausnahmen, die von dem `exclude`-Attribut angegeben werden. Der Pfad ist relativ zur `.nuspec`-Datei, wenn kein absoluter Pfad angegeben ist. Das Platzhalterzeichen `*` ist zulässig, und das zweifache Platzhalterzeichen `**` impliziert eine rekursive Ordnersuche. |
| **target** | Der relative Pfad zu dem Ordner in dem Paket, in dem die Quelldateien platziert sind, der mit `lib`, `content`, `build` oder `tools` beginnt. Informationen dazu finden Sie unter [Creating a .nuspec from a convention-based working directory (Erstellen einer NUSPEC-Datei aus einem auf Konventionen basierenden Arbeitsverzeichnis)](../create-packages/creating-a-package.md#from-a-convention-based-working-directory). |
| **exclude** | Eine durch Semikolons abgetrennte Datei oder Dateimuster, die sich nicht im `src`-Speicherort befinden dürfen. Das Platzhalterzeichen `*` ist zulässig, und das zweifache Platzhalterzeichen `**` impliziert eine rekursive Ordnersuche. |

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

**Mehrere DLLS, die Platzhalterzeichen verwenden**

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

## <a name="including-content-files"></a>Einfügen von Inhaltsdateien

Bei Inhaltsdateien handelt es sich um unveränderliche Dateien, die ein Paket in ein Projekt einfügen muss. Da sie unveränderlich sind, sollen sie auch nicht von dem verarbeitenden Projekt geändert werden. Zu den Inhaltsdateien gehören z.B.:

- Bilder, die als Ressourcen eingebettet werden
- Quelldateien, die bereits kompiliert sind
- Skripts, die in die Buildausgabe des Projekts eingefügt werden müssen
- Konfigurationsdateien für das Paket, die zwar in das Projekt eingefügt werden müssen, an denen jedoch keine projektspezifischen Änderungen vorgenommen werden müssen.

Inhaltsdateien werden in ein Paket eingefügt, das das `<files>`-Element verwendet, das den `content`-Ordner im `target`-Attribut angibt. Allerdings werden diese Dateien ignoriert, wenn das Paket über PackageReference in ein Projekt installiert wird, das stattdessen das `<contentFiles>`-Element verwendet.

Im Idealfall geben Pakete die Inhaltsdateien in beiden Elementen an, um ein höchstmögliches Maß an Kompatibilität mit den verarbeitenden Projekten zu erreichen.

### <a name="using-the-files-element-for-content-files"></a>Verwenden des Dateielements für Inhaltsdateien

Verwenden Sie für Inhaltsdateien einfach dasselbe Format wie für Assemblydateien. Geben Sie dabei allerdings `content` als Basisordner im `target`-Attribut an, wie in den folgenden Beispielen dargestellt wird.

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

**Inhaltsdatei, die für ein Zielframework spezifisch ist**

    Source file:
        css\cool\style.css

    .nuspec entry
        <file src="css\cool\style.css" target="Content" />

    Packaged result:
        content\style.css

**Inhaltsdatei, die in einen Ordner mit einem Punkt im Namen kopiert wird**

In diesem Fall erkennt NuGet, dass die Erweiterung in `target` nicht mit der Erweiterung in `src` übereinstimmt, und behandelt dieses Bestandteil des Namens in `target` als einen Ordner:

    Source file:
        images\picture.png

    .nuspec entry:
        <file src="images\picture.png" target="Content\images\package.icons" />

    Packaged result:
        content\images\package.icons\picture.png

**Inhaltsdateien ohne Erweiterungen**

Verwenden Sie die Platzhalterzeichen `*` oder `**`, um Dateien ohne Erweiterungen einzufügen:

    Source file:
        flags\installed

    .nuspec entry:
        <file src="flags\**" target="flags" />

    Packaged result:
        flags\installed

**Inhaltsdateien mit tiefen Pfaden und tiefen Zielen**

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

Standardmäßig platzieren Pakete Inhalte in einem `contentFiles`-Ordner (s. unten), in den `nuget pack` alle Dateien mithilfe von Standardattributen eingefügt hat. In diesem Fall ist es nicht notwendig, einen `contentFiles`-Knoten in `.nuspec` einzufügen.

Das `<contentFiles>`-Element gibt eine Auflistung von `<files>`-Elementen an, die die eingefügten Dateien erkennen, um zu kontrollieren, welche Dateien eingefügt wurden.

Diese Dateien werden zusammen mit mehreren Attributen angegeben, die beschreiben, wie sie in dem Projektsystem verwendet werden sollen:

| Attribute | Beschreibung |
| --- | --- |
| **include** | (Erforderlich) Der Speicherort der Dateien, die eingefügt werden sollen, unterliegt Ausnahmen, die von dem `exclude`-Attribut angegeben werden. Der Pfad ist relativ zum `contentFiles` Ordner, es sei denn, es wurde ein absoluter Pfad angegeben. Das Platzhalterzeichen `*` ist zulässig, und das zweifache Platzhalterzeichen `**` impliziert eine rekursive Ordnersuche. |
| **exclude** | Eine durch Semikolons abgetrennte Datei oder Dateimuster, die sich nicht im `src`-Speicherort befinden dürfen. Das Platzhalterzeichen `*` ist zulässig, und das zweifache Platzhalterzeichen `**` impliziert eine rekursive Ordnersuche. |
| **buildAction** | Die Buildaktion, die dem Inhalts Element für MSBuild zugewiesen werden soll, z. b. `Content`, `None`, `Embedded Resource`, `Compile`usw. Der Standardwert ist `Compile`. |
| **copyToOutput** | Boolescher Wert, mit dem angegeben wird, ob Inhaltselemente in den Buildausgabeordner (oder den Veröffentlichungsausgabeordner) kopiert werden sollen. Der Standardwert ist false. |
| **flatten** | Ein boolescher Wert, der angibt, ob Inhaltselemente in einen Ordner in der Buildausgabe kopiert werden sollen (TRUE) oder ob die Ordnerstruktur in den Paketen beibehalten werden soll (FALSE). Diese Flag funktioniert nur, wenn das copyToOutput-Flag auf TRUE festgelegt ist. Der Standardwert ist false. |

NuGet wendet die untergeordneten Elemente von `<contentFiles>` bei der Installation eines Pakets von unten nach oben an. Wenn mehrere Einträge in einer Datei vorhanden sind, werden sie alle angewendet. Der höher geordnete Eintrag setzt die untergeordneten Einträge außer Kraft, wenn ein Konflikt für ein Attribut entsteht.

#### <a name="package-folder-structure"></a>Paketordnerstruktur

Das Paketprojekt sollte Inhalte mithilfe des folgenden Musters strukturieren:

    /contentFiles/{codeLanguage}/{TxM}/{any?}

- `codeLanguages` kann `cs`, `vb`, `fs`, `any` oder das klein geschriebene Äquivalent einer `$(ProjectLanguage)` sein.
- `TxM` ist ein für das Zielframework zulässiger Moniker, der NuGet unterstützt (Informationen dazu finden Sie unter [Zielframeworks](../reference/target-frameworks.md)).
- An das Ende der Syntax kann eine beliebige Ordnerstruktur angehängt werden.

Beispiel:

    Language- and framework-agnostic:
        /contentFiles/any/any/config.xml

    net45 content for all languages
        /contentFiles/any/net45/config.xml

    C#-specific content for net45 and up
        /contentFiles/cs/net45/sample.cs

Für leere Ordner kann `.` eingefügt werden, wenn diese keine Inhalte mehr für bestimmte Sprachen und TxM bereitstellen sollen. Z.B.:

    /contentFiles/vb/any/code.vb
    /contentFiles/cs/any/.

#### <a name="example-contentfiles-section"></a>Beispiel: Abschnitt „contentFiles“

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        ...
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
        </metadata>
</package>
```

## <a name="example-nuspec-files"></a>NUSPEC-Beispieldateien

**Eine einfache `.nuspec`-Datei, die weder Abhängigkeiten noch Dateien enthält**

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

**Eine `.nuspec`-Datei mit Abhängigkeiten**

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

**Eine `.nuspec`-Datei mit Dateien**

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

**Eine `.nuspec`-Datei mit Frameworkassemblys**

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
- WindowsPhone: `Microsoft.Devices.Sensors`
