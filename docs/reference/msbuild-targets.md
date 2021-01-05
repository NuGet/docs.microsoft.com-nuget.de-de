---
title: NuGet pack and restore as MSBuild targets (NuGet-Befehle „pack“ und „restore“ MSBuild-Ziele)
description: Die NuGet-Befehle „pack“ und „restore“ können direkt als MSBuild-Ziele mit NuGet 4.0 und höher arbeiten.
author: nkolev92
ms.author: nikolev
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: 66df4e0e4739300608fd5f9e44eea5bcd00079c8
ms.sourcegitcommit: 53b06e27bcfef03500a69548ba2db069b55837f1
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/19/2020
ms.locfileid: "97699886"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a>NuGet pack and restore as MSBuild targets (NuGet-Befehle „pack“ und „restore“ MSBuild-Ziele)

*NuGet 4.0 und höher*

Beim [packagereferenzierungsformat](../consume-packages/package-references-in-project-files.md) kann nuget 4.0 + alle Manifestressourcen direkt in einer Projektdatei speichern, anstatt eine separate Datei zu verwenden `.nuspec` .

Mit MSBuild 15.1 und höher stellt NuGet auch einen MSBuild-Angehörigen der ersten Klasse mit den Zielen `pack` und `restore` dar, wie im Folgenden beschrieben. Durch diese Ziele können Sie mit NuGet wie mit jeder anderen MSBuild-Task oder jedem anderen MSBuild-Ziel arbeiten. Anweisungen zum Erstellen eines nuget-Pakets mithilfe von MSBuild finden Sie unter [Erstellen eines nuget-Pakets mithilfe von MSBuild](../create-packages/creating-a-package-msbuild.md). (Bei NuGet 3.x und früher verwenden Sie die Befehle [pack](../reference/cli-reference/cli-ref-pack.md) und [restore](../reference/cli-reference/cli-ref-restore.md) stattdessen über die NuGet-CLI.)

## <a name="target-build-order"></a>Buildreihenfolge für Ziele

Da es sich bei `pack` und `restore` um MSBuild-Ziele handelt, können sie zur Verbesserung Ihres Workflows darauf zugreifen. Angenommen Sie möchten Ihr Paket nach dem Packen in eine Netzwerkfreigabe kopieren. Fügen Sie hierzu Folgendes in Ihrer Projektdatei hinzu:

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

Gleichermaßen können Sie eine MSBuild-Task schreiben, Ihr eigenes Ziel schreiben und NuGet-Eigenschaften in der MSBuild-Task verwenden.

> [!NOTE]
> `$(OutputPath)` ist relativ und erwartet, dass Sie den Befehl aus dem Projektstamm ausführen.

## <a name="pack-target"></a>Pack-Ziel

Für .NET Standard Projekte, die das packagereferenzierungsformat verwenden, `msbuild -t:pack` zeichnet mithilfe von Eingaben aus der Projektdatei, die beim Erstellen eines nuget-Pakets verwendet werden sollen.

In der folgenden Tabelle werden die MSBuild-Eigenschaften beschrieben, die im ersten `<PropertyGroup>`-Knoten zu einer Projektdatei hinzugefügt werden können. Sie können diese Änderungen problemlos in Visual Studio 2017 und höheren Versionen vornehmen, indem Sie mit der rechten Maustaste auf das Projekt klicken und **{Project_name} bearbeiten** im Kontextmenü auswählen. Zur einfacheren Handhabung wird die Tabelle nach der entsprechenden Eigenschaft in einer [ `.nuspec` Datei](../reference/nuspec.md)organisiert.

Beachten Sie, dass die Eigenschaften `Owners` und `Summary` aus einer `.nuspec`-Datei in MSBuild nicht unterstützt werden.

| Attribut/NuSpec-Wert | MSBuild-Eigenschaft | Standard | Notizen |
|--------|--------|--------|--------|
| Id | PackageId | AssemblyName | $(AssemblyName) aus MSBuild |
| Version | PackageVersion | Version | Diese Eigenschaft ist mit „semver“ kompatibel, z.B. „1.0.0“, „1.0.0-beta“ oder „1.0.0-beta-00345“ |
| VersionPrefix | PackageVersionPrefix | empty | Durch das Festlegen von PackageVersion wird PackageVersionPrefix überschrieben |
| VersionSuffix | PackageVersionSuffix | empty | $(VersionSuffix) aus MSBuild. Durch das Festlegen von PackageVersion wird PackageVersionSuffix überschrieben |
| Authors | Authors | Name des aktuellen Benutzers | |
| Besitzer | – | In NuSpec nicht vorhanden | |
| Titel | Titel | Die PackageId| |
| BESCHREIBUNG | BESCHREIBUNG | „Paketbeschreibung“ | |
| Copyright | Copyright | empty | |
| RequireLicenseAcceptance | PackageRequireLicenseAcceptance | false | |
| license | PackageLicenseExpression | empty | Entspricht `<license type="expression">` |
| license | PackageLicenseFile | empty | Entspricht `<license type="file">` Sie müssen die referenzierte Lizenzdatei explizit verpacken. |
| LicenseUrl | PackageLicenseUrl | empty | `PackageLicenseUrl` ist veraltet, verwenden Sie die packagelicenseexpression-oder packagelicensefile-Eigenschaft. |
| ProjectUrl | PackageProjectUrl | empty | |
| Symbol | PackageIcon | empty | Sie müssen explizit die Symbolbild Datei, auf die verwiesen wird, verpacken.|
| IconUrl | PackageIconUrl | empty | Um das beste kompatible zu erzielen, `PackageIconUrl` sollte zusätzlich zu angegeben werden `PackageIcon` . Längerfristig `PackageIconUrl` wird als veraltet markiert. |
| Tags | PackageTags | empty | Ziele werden durch Semikolons (;) getrennt. |
| ReleaseNotes | PackageReleaseNotes | empty | |
| Repository/URL | RepositoryUrl | empty | Die Repository-URL, die zum Klonen oder Abrufen von Quellcode verwendet wird. Beispiel *https://github.com/NuGet/NuGet.Client.git* |
| Repository/Typ | RepositoryType | empty | Der Repository-Typ. Beispiele: *git*, *TFS*. |
| Repository/Verzweigung | RepositoryBranch | empty | Optionale Informationen zum Repository-Branch. *RepositoryUrl* muss auch angegeben werden, damit diese Eigenschaft eingeschlossen wird. Beispiel: *Master* (nuget 4.7.0 +) |
| Repository/Commit | RepositoryCommit | empty | Optionaler Repositorycommit oder ein Changeset, um anzugeben, für welches Quellpaket die Erstellung erfolgt ist. *RepositoryUrl* muss auch angegeben werden, damit diese Eigenschaft eingeschlossen wird. Beispiel: *0e4d1b598f 350 b3dc675018d539114d1328189ef* (nuget 4.7.0 +) |
| PackageType | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| Zusammenfassung | Nicht unterstützt | | |

### <a name="pack-target-inputs"></a>Eingaben für das Ziel „pack“

- IsPackable
- Suppressdependenciesder Verpackung
- PackageVersion
- PackageId
- Authors
- BESCHREIBUNG
- Copyright
- PackageRequireLicenseAcceptance
- DevelopmentDependency
- PackageLicenseExpression
- PackageLicenseFile
- PackageLicenseUrl
- PackageProjectUrl
- PackageIconUrl
- PackageReleaseNotes
- PackageTags
- PackageOutputPath
- IncludeSymbols
- IncludeSource
- PackageTypes
- IsTool
- RepositoryUrl
- RepositoryType
- RepositoryBranch
- RepositoryCommit
- NoPackageAnalysis
- MinClientVersion
- IncludeBuildOutput
- IncludeContentInPack
- BuildOutputTargetFolder
- ContentTargetFolders
- NuspecFile
- NuspecBasePath
- NuspecProperties

## <a name="pack-scenarios"></a>Pack-Szenarios

### <a name="suppress-dependencies"></a>Abhängigkeiten unterdrücken

Um Paketabhängigkeiten aus dem generierten nuget-Paket zu unterdrücken, legen `SuppressDependenciesWhenPacking` Sie auf fest `true` . Dadurch können alle Abhängigkeiten von der generierten nupkg-Datei übersprungen werden.

### <a name="packageiconurl"></a>PackageIconUrl

`PackageIconUrl` wird zugunsten der neuen Eigenschaft als veraltet markiert [`PackageIcon`](#packageicon) .

Ab nuget 5,3 & Visual Studio 2019 Version 16,3 `pack` wird [NU5048](./errors-and-warnings/nu5048.md) Warning ausgegeben, wenn die Paket Metadaten nur angeben `PackageIconUrl` .

### <a name="packageicon"></a>PackageIcon

> [!Tip]
> Sie sollten sowohl `PackageIcon` als auch angeben `PackageIconUrl` , um die Abwärtskompatibilität mit Clients und Quellen zu gewährleisten, die noch nicht unterstützen `PackageIcon` . Visual Studio unterstützt `PackageIcon` Pakete, die in einer zukünftigen Version aus einer Ordner basierten Quelle stammen.

#### <a name="packing-an-icon-image-file"></a>Packen einer Symbolbild Datei

Beim Packen einer Symbolbild Datei müssen Sie die-Eigenschaft verwenden, `PackageIcon` um den Paketpfad relativ zum Stamm des Pakets anzugeben. Außerdem müssen Sie sicherstellen, dass die Datei im Paket enthalten ist. Die Größe der Bild Datei ist auf 1 MB beschränkt. Unterstützte Dateiformate sind JPEG und PNG. Wir empfehlen eine Bildauflösung von 128 x 128.

Zum Beispiel:

```xml
<PropertyGroup>
    ...
    <PackageIcon>icon.png</PackageIcon>
    ...
</PropertyGroup>

<ItemGroup>
    ...
    <None Include="images\icon.png" Pack="true" PackagePath="\"/>
    ...
</ItemGroup>
```

[Paket Symbol Beispiel](https://github.com/NuGet/Samples/tree/master/PackageIconExample).

Die nuspec-Entsprechung finden Sie in der [nuspec-Referenz für das Symbol](nuspec.md#icon).

### <a name="output-assemblies"></a>Ausgabeassemblys

`nuget pack` kopiert Ausgabedateien mit den Erweiterungen `.exe`, `.dll`, `.xml`, `.winmd`, `.json` und `.pri`. Welche Ausgabedateien kopiert werden, hängt davon ab, was MSBuild aus dem Ziel `BuiltOutputProjectGroup` bereitstellt.

Sie können zwei MSBuild-Eigenschaften in Ihrer Projektdatei oder Befehlszeile verwenden, um das Ziel der Ausgabeassemblys zu steuern:

- `IncludeBuildOutput`: Ein boolescher Wert, der bestimmt, ob die Ausgabeassemblys des Builds in das Paket eingeschlossen werden sollten.
- `BuildOutputTargetFolder`: Gibt den Ordner an, in dem die Ausgabeassemblys angeordnet werden sollten. Die Ausgabeassemblys (und andere Ausgabedateien) werden in ihre jeweiligen Frameworkordner kopiert.

### <a name="package-references"></a>Paketverweise

Siehe [Package References in Project Files ](../consume-packages/package-references-in-project-files.md) (Paketverweise in Projektdateien).

### <a name="project-to-project-references"></a>Projekt-zu-Projekt-Verweise

Projekt-zu-Projekt-Verweise gelten standardmäßig als NuGet-Paketverweise, z.B.:

```xml
<ProjectReference Include="..\UwpLibrary2\UwpLibrary2.csproj"/>
```

Sie können auf folgende Metadaten zu Ihrem Projektverweis hinzufügen:

```xml
<IncludeAssets>
<ExcludeAssets>
<PrivateAssets>
```

### <a name="including-content-in-a-package"></a>Einschließlich der Inhalte in einem Paket

Fügen Sie zusätzliche Metadaten zu dem vorhandenen `<Content>`-Element hinzu, um Inhalte einzuschließen. Standardmäßig werden alle Elemente vom Typ „Content“ in das Paket eingeschlossen, sofern Sie diese Elemente nicht mit Einträgen wie den folgenden überschreiben:

 ```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>false</Pack>
</Content>
 ```

Standardmäßig werden alle Elemente zum Stammverzeichnis der Ordner `content` und `contentFiles\any\<target_framework>` innerhalb eines Pakets hinzugefügt, und die relative Ordnerstruktur wird beibehalten, sofern Sie keinen Paketpfad angeben:

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles\</PackagePath>
</Content>
```

Wenn Sie alle Ihre Inhalte in nur einen bestimmten Stammordner kopieren möchten (statt in die Ordner `content` und `contentFiles`), können Sie die MSBuild-Eigenschaft `ContentTargetFolders` verwenden, die standardmäßig auf „content;contentFiles“ festgelegt ist, aber auf beliebige andere Ordnernamen festgelegt werden kann. Beachten Sie Folgendes: Wenn Sie in `ContentTargetFolders` nur „contentFiles“ angeben, werden Dateien unter `contentFiles\any\<target_framework>` oder `contentFiles\<language>\<target_framework>` basierend auf `buildAction` angeordnet.

`PackagePath` kann eine durch Semikolons (;) getrennte Reihe von Zielpfaden sein. Durch die Angabe eines leeren Paketpfads würde die Datei zum Stammverzeichnis des Pakets hinzugefügt. Im Folgenden wird beispielsweise `libuv.txt` zu`content\myfiles`, `content\samples` und dem Stammverzeichnis des Pakets hinzugefügt:

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

Es gibt auch eine MSBuild-Eigenschaft, `$(IncludeContentInPack)`, die standardmäßig auf `true` festgelegt ist. Wenn diese in einem Projekt auf `false` festgelegt wird, werden die Inhalte aus diesem Projekt nicht in das NuGet-Paket eingeschlossen.

Weitere für das Ziel „pack“ spezifische Metadaten, die Sie auf ein beliebiges der oben genannten Elemente festlegen können, enthalten ```<PackageCopyToOutput>``` und ```<PackageFlatten>```, die die Werte ```CopyToOutput``` und ```Flatten``` auf den ```contentFiles```-Eintrag in der ausgegebenen Nuspec-Datei festlegen.

> [!Note]
> Die Metadaten `<Pack>` und `<PackagePath>` können nicht nur auf Inhaltselemente, sondern auch auf Dateien mit den Buildvorgängen „Compile“, „EmbeddedResource“, „ApplicationDefinition“, „Page“, „Resource“, „SplashScreen“, „DesignData“, „DesignDataWithDesignTimeCreateableTypes“, „CodeAnalysisDictionary“, „AndroidAsset“, „AndroidResource“, „BundleResource“ oder „None“ festgelegt werden.
>
> Damit das Ziel „pack“ bei der Verwendung von Globmustern den Dateinamen an Ihren Paketpfad anhängt, muss Ihr Paketpfad mit dem Ordnertrennzeichen enden. Andernfalls wird der Paketpfad als vollständiger Pfad einschließlich des Dateinamens behandelt.

### <a name="includesymbols"></a>IncludeSymbols

Bei Verwendung von `MSBuild -t:pack -p:IncludeSymbols=true` werden die entsprechenden `.pdb`-Dateien zusammen mit anderen Ausgabedateien kopiert (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`). Beachten Sie, dass durch das Festlegen von `IncludeSymbols=true` ein reguläres Paket *und* ein Symbolpaket erstellt werden.

### <a name="includesource"></a>IncludeSource

Dies ist mit `IncludeSymbols` identisch. Der einzige Unterschied besteht darin, dass Quelldateien auch zusammen mit `.pdb`-Dateien kopiert werden. Alle Dateien vom Typ `Compile` werden in `src\<ProjectName>\` kopiert. Dabei wird die Ordnerstruktur im relativen Pfad im resultierenden Paket beibehalten. Gleiches gilt auch für Quelldateien einer beliebigen `ProjectReference`, bei der `TreatAsPackageReference` auf `false` festgelegt ist.

Wenn sich eine Datei vom Typ „Compile“ außerhalb des Projektordners befindet, wird sie nur zu `src\<ProjectName>\` hinzugefügt.

### <a name="packing-a-license-expression-or-a-license-file"></a>Verpacken eines Lizenz Ausdrucks oder einer Lizenzdatei

Wenn Sie einen Lizenz Ausdruck verwenden, sollte die packagelicenseexpression-Eigenschaft verwendet werden. 
[Beispiel für den Lizenz Ausdruck](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

[Erfahren Sie mehr über Lizenz Ausdrücke und Lizenzen, die von NuGet.org akzeptiert werden](nuspec.md#license).

Beim Verpacken einer Lizenzdatei müssen Sie den Paketpfad relativ zum Stamm des Pakets mit der packagelicensefile-Eigenschaft angeben. Außerdem müssen Sie sicherstellen, dass die Datei im Paket enthalten ist. Zum Beispiel:

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```

[Beispiel für eine Lizenzdatei](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).

### <a name="packing-a-file-without-an-extension"></a>Packen einer Datei ohne Erweiterung

In einigen Szenarien, wie z. b. beim Verpacken einer Lizenzdatei, empfiehlt es sich, eine Datei ohne Erweiterung aufzunehmen.
Aus historischen Gründen werden von nuget & MSBuild Pfade ohne Erweiterung als Verzeichnisse behandelt.

```xml
  <PropertyGroup>
    <TargetFrameworks>netstandard2.0</TargetFrameworks>
    <PackageLicenseFile>LICENSE</PackageLicenseFile>
  </PropertyGroup>

  <ItemGroup>
    <None Include="LICENSE" Pack="true" PackagePath=""/>
  </ItemGroup>  
```

[Datei ohne Erweiterungs Beispiel](https://github.com/NuGet/Samples/blob/master/PackageLicenseFileExtensionlessExample/).
### <a name="istool"></a>IsTool

Bei Verwendung von `MSBuild -t:pack -p:IsTool=true` werden alle Ausgabedateien entsprechend den Angaben im Szenario [Ausgabeassemblys](#output-assemblies) in den Ordner `tools` und nicht in den Ordner `lib` kopiert. Beachten Sie, dass sich dies von einem `DotNetCliTool` unterscheidet, das durch Festlegen von `PackageType` in der `.csproj`-Datei angegeben wird.

### <a name="packing-using-a-nuspec"></a>Packen mit einer .nuspec-Datei

Es wird empfohlen, stattdessen [alle Eigenschaften](../reference/msbuild-targets.md#pack-target) , die normalerweise in der-Datei in der `.nuspec` Projektdatei enthalten sind, zu verwenden. Sie können jedoch auch eine-Datei verwenden, `.nuspec` um das Projekt zu verpacken. Für ein Projekt, das nicht im SDK verwendet `PackageReference` wird, müssen Sie importieren, `NuGet.Build.Tasks.Pack.targets` damit der Pack-Task ausgeführt werden kann. Sie müssen das Projekt dennoch wiederherstellen, bevor Sie eine nuspec-Datei packen können. (Ein Projekt im SDK-Stil enthält standardmäßig die Paket Ziele.)

Das Ziel Framework der Projektdatei ist irrelevant und wird beim Packen einer nuspec-Datei nicht verwendet. Die folgenden drei MSBuild-Eigenschaften sind für das Packen mit einer `.nuspec`-Datei relevant:

1. `NuspecFile`: Relativer oder absoluter Pfad zur `.nuspec`-Datei, der für das Packen verwendet wird.
1. `NuspecProperties`: Durch Semikolons (;) getrennte Liste der Schlüssel/Wert-Paare. Aufgrund der Funktionsweise der MSBuild-Befehlszeilenanalyse müssen mehrere Eigenschaften wie folgt angegeben werden: `-p:NuspecProperties="key1=value1;key2=value2"`.  
1. `NuspecBasePath`: Der Basispfad für die `.nuspec`-Datei.

Wenn Sie Ihr Projekt mithilfe der Datei `dotnet.exe` packen, verwenden Sie einen Befehl wie den folgenden:

```dotnetcli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

Wenn Sie Ihr Projekt mithilfe von MSBuild packen, verwenden Sie einen Befehl wie den folgenden:

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

Beachten Sie, dass das Packen einer nuspec-Datei mit dotnet.exe oder MSBuild ebenfalls dazu führt, dass das Projekt standardmäßig erstellt wird. Dies kann vermieden werden, indem ```--no-build``` Sie die-Eigenschaft an dotnet.exe übergeben. Dies entspricht der-Einstellung ```<NoBuild>true</NoBuild> ``` in der Projektdatei und der-Einstellung ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in der Projektdatei.

Ein Beispiel für eine *csproj* -Datei zum Packen einer nuspec-Datei ist:

```xml
<Project Sdk="Microsoft.NET.Sdk">
  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <NoBuild>true</NoBuild>
    <IncludeBuildOutput>false</IncludeBuildOutput>
    <NuspecFile>PATH_TO_NUSPEC_FILE</NuspecFile>
    <NuspecProperties>add nuspec properties here</NuspecProperties>
    <NuspecBasePath>optional to provide</NuspecBasePath>
  </PropertyGroup>
</Project>
```

### <a name="advanced-extension-points-to-create-customized-package"></a>Verbesserte Erweiterungspunkte zum Erstellen benutzerdefinierter Pakete

Das `pack` Ziel bietet zwei Erweiterungs Punkte, die im Inneren, zielframeworkspezifischen Build ausgeführt werden. Die Erweiterungs Punkte unterstützen den Inhalt und die Assemblys für das Ziel Framework in ein Paket:

- `TargetsForTfmSpecificBuildOutput` Ziel: Verwenden Sie für Dateien innerhalb des `lib` Ordners oder eines mit angegebenen Ordners `BuildOutputTargetFolder` .
- `TargetsForTfmSpecificContentInPackage` Ziel: wird für Dateien außerhalb von verwendet `BuildOutputTargetFolder` .

#### <a name="targetsfortfmspecificbuildoutput"></a>Targezfortfmspecificbuildoutput

Schreiben Sie ein benutzerdefiniertes Ziel, und geben Sie es als Wert der- `$(TargetsForTfmSpecificBuildOutput)` Eigenschaft an. Für alle Dateien, die in den `BuildOutputTargetFolder` (standardmäßig lib) wechseln müssen, sollte das Ziel diese Dateien in die ItemGroup schreiben `BuildOutputInPackage` und die folgenden beiden Metadatenwerte festlegen:

- `FinalOutputPath`: Der absolute Pfad der Datei. Wenn keine Angabe erfolgt, wird die Identität verwendet, um den Quellpfad auszuwerten.
- `TargetPath`: (Optional) legen Sie fest, wann die Datei in einen Unterordner in wechseln muss `lib\<TargetFramework>` , z. b. Satellitenassemblys, die sich unter den jeweiligen Kultur Ordnern befinden. Der Standardwert ist der Name der Datei.

Beispiel:

```xml
<PropertyGroup>
  <TargetsForTfmSpecificBuildOutput>$(TargetsForTfmSpecificBuildOutput);GetMyPackageFiles</TargetsForTfmSpecificBuildOutput>
</PropertyGroup>

<Target Name="GetMyPackageFiles">
  <ItemGroup>
    <BuildOutputInPackage Include="$(OutputPath)cs\$(AssemblyName).resources.dll">
        <TargetPath>cs</TargetPath>
    </BuildOutputInPackage>
  </ItemGroup>
</Target>
```

#### <a name="targetsfortfmspecificcontentinpackage"></a>Targetfortfmspecificcontentinpackage

Schreiben Sie ein benutzerdefiniertes Ziel, und geben Sie es als Wert der- `$(TargetsForTfmSpecificContentInPackage)` Eigenschaft an. Für alle Dateien, die in das Paket eingeschlossen werden sollen, sollte das Ziel diese Dateien in die ItemGroup schreiben `TfmSpecificPackageFile` und die folgenden optionalen Metadaten festlegen:

- `PackagePath`: Pfad, in dem die Datei im Paket ausgegeben werden soll. Nuget gibt eine Warnung aus, wenn demselben Paketpfad mehr als eine Datei hinzugefügt wird.
- `BuildAction`: Die Buildaktion, die der Datei zugewiesen werden soll. Dies ist nur erforderlich, wenn sich der Paketpfad im `contentFiles` Ordner befindet. Der Standardwert ist "None".

Beispiel:
```xml
<PropertyGroup>
  <TargetsForTfmSpecificContentInPackage>$(TargetsForTfmSpecificContentInPackage);CustomContentTarget</TargetsForTfmSpecificContentInPackage>
</PropertyGroup>

<Target Name="CustomContentTarget">
  <ItemGroup>
    <TfmSpecificPackageFile Include="abc.txt">
      <PackagePath>mycontent/$(TargetFramework)</PackagePath>
    </TfmSpecificPackageFile>
    <TfmSpecificPackageFile Include="Extensions/ext.txt" Condition="'$(TargetFramework)' == 'net46'">
      <PackagePath>net46content</PackagePath>
    </TfmSpecificPackageFile>  
  </ItemGroup>
</Target>  
```

## <a name="restore-target"></a>Wiederherstellungsziel

Das Ziel `MSBuild -t:restore` (das von `nuget restore` und `dotnet restore` in .NET Core-Projekten verwendet wird), stellt wie folgt Pakete wieder her, auf die in der Projektdatei verwiesen wird:

1. Lesen aller Projekt-zu-Projekt-Verweise
1. Lesen der Projekteigenschaften, um den Zwischenordner und Zielframeworks zu finden
1. MSBuild-Daten an NuGet.Build.Tasks.dll übergeben
1. Ausführen des Befehls „restore“
1. Herunterladen von Paketen
1. Schreiben von Assetdatei, Zielen und Eigenschaften

Das `restore` Ziel funktioniert für Projekte, die das packagereferenzierungsformat verwenden.
`MSBuild 16.5+` bietet auch eine [Opt-in-Unterstützung](#restoring-packagereference-and-packagesconfig-with-msbuild) für das- `packages.config` Format.

> [!NOTE]
> Das `restore` Ziel [sollte nicht](#restoring-and-building-with-one-msbuild-command) in Kombination mit dem Ziel ausgeführt werden `build` .

### <a name="restore-properties"></a>Wiederherstellen von Eigenschaften

Weitere Wiederherstellungseigenschaften können aus MSBuild-Eigenschaften in der Projektdatei stammen. Werte können auch mithilfe des `-p:`-Switch über die Befehlszeile festgelegt werden (siehe nachfolgende Beispiele).

| Eigenschaft | BESCHREIBUNG |
|--------|--------|
| RestoreSources | Eine durch Semikolons (;) getrennte Liste mit Paketquellen. |
| RestorePackagesPath | Ordnerpfad der Pakete für Benutzer. |
| RestoreDisableParallel | Begrenzt Downloads auf jeweils einen Download. |
| RestoreConfigFile | Der Pfad zu einer anzuwendenden `Nuget.Config`-Datei. |
| RestoreNoCache | Wenn true, wird die Verwendung von zwischengespeicherten Paketen vermieden. Weitere Informationen finden Sie [unter Verwalten der globalen Pakete und Cache Ordner](../consume-packages/managing-the-global-packages-and-cache-folders.md). |
| RestoreIgnoreFailedSources | Wenn „TRUE“ festgelegt ist, werden fehlerhafte oder fehlende Paketquellen ignoriert. |
| Restorefallbackfolders | Fall Back Ordner, die auf die gleiche Weise verwendet werden wie der Ordner "Benutzer Pakete". |
| Restoreadditionalprojectsources | Zusätzliche Quellen, die während der Wiederherstellung verwendet werden sollen. |
| Restoreadditionalprojectfallbackfolders | Zusätzliche Fall Back Ordner, die während der Wiederherstellung verwendet werden sollen. |
| Restoreadditionalprojectfallbackfoldersexcludes | Schließt in angegebene Fall Back Ordner aus. `RestoreAdditionalProjectFallbackFolders` |
| RestoreTaskAssemblyFile | Pfad zu `NuGet.Build.Tasks.dll`. |
| RestoreGraphProjectInput | Durch Semikolons (;) getrennte Liste mit wiederherzustellenden Projekten, die absolute Pfade enthalten sollten. |
| Restoreuseskipnonexistenttargets  | Wenn die Projekte über MSBuild gesammelt werden, wird ermittelt, ob Sie mithilfe der `SkipNonexistentTargets` Optimierung gesammelt werden. Wenn nicht festgelegt, wird standardmäßig auf festgelegt `true` . Die Folge ist ein fehlerhafter Verhalten, wenn die Ziele eines Projekts nicht importiert werden können. |
| MSBuildProjectExtensionsPath | Ausgabeordner, standardmäßig auf `BaseIntermediateOutputPath` und den `obj` Ordner. |
| Restoreforce | In packagereferenzierungsbasierten Projekten erzwingt, dass alle Abhängigkeiten gelöst werden, auch wenn die letzte Wiederherstellung erfolgreich war. Die Angabe dieses Flags ähnelt dem Löschen der `project.assets.json` Datei. Dadurch wird der HTTP-Cache nicht umgangen. |
| RestorePackagesWithLockFile | Ermöglicht die Verwendung einer Sperrdatei. |
| RestoreLockedMode | Führen Sie die Wiederherstellung im gesperrten Modus aus. Dies bedeutet, dass bei der Wiederherstellung die Abhängigkeiten nicht neu ausgewertet werden. |
| NuGetLockFilePath | Ein benutzerdefinierter Speicherort für die Sperrdatei. Der Standard Speicherort ist neben dem Projekt und hat den Namen `packages.lock.json` . |
| RestoreForceEvaluate | Erzwingt die Wiederherstellung, um die Abhängigkeiten neu zu berechnen und die Sperrdatei ohne Warnung zu aktualisieren. |
| Restorepackagesconfig | Ein Opt-in-Switch, mit dem Projekte mit packages.config wieder hergestellt werden. Unterstützung `MSBuild -t:restore` nur mit. |

#### <a name="examples"></a>Beispiele

Befehlszeile:

```cli
msbuild -t:restore -p:RestoreConfigFile=<path>
```

Projektdatei:

```xml
<PropertyGroup>
    <RestoreIgnoreFailedSource>true</RestoreIgnoreFailedSource>
</PropertyGroup>
```

### <a name="restore-outputs"></a>Wiederherstellen von Ausgaben

Bei der Wiederherstellung werden die folgenden Dateien im `obj`-Buildordner erstellt:

| Datei | BESCHREIBUNG |
|--------|--------|
| `project.assets.json` | Enthält das Abhängigkeits Diagramm aller Paket Verweise. |
| `{projectName}.projectFileExtension.nuget.g.props` | Verweist auf in Paketen enthaltene MSBuild-Eigenschaften |
| `{projectName}.projectFileExtension.nuget.g.targets` | Verweist auf in Paketen enthaltene MSBuild-Ziele |

### <a name="restoring-and-building-with-one-msbuild-command"></a>Wiederherstellen und erstellen mit einem MSBuild-Befehl

Aufgrund der Tatsache, dass nuget Pakete wiederherstellen kann, von denen MSBuild-Ziele und-Eigenschaften heruntergefahren werden, werden die Wiederherstellungs-und buildauswertungen mit unterschiedlichen globalen Eigenschaften ausgeführt.
Dies bedeutet, dass Folgendes ein unvorhersehbares und häufig falsches Verhalten hat.

```cli
msbuild -t:restore,build
```

 Stattdessen wird die empfohlene Vorgehensweise empfohlen:

```cli
msbuild -t:build -restore
```

Die gleiche Logik gilt für andere Ziele ähnlich wie `build` .

### <a name="restoring-packagereference-and-packagesconfig-with-msbuild"></a>Wiederherstellen von packagereferenzierungen und packages.config mit MSBuild

Mit MSBuild 16.5 + werden packages.config auch für unterstützt `msbuild -t:restore` .

```cli
msbuild -t:restore -p:RestorePackagesConfig=true
```

> [!NOTE]
> `packages.config` Restore ist nur mit verfügbar `MSBuild 16.5+` , nicht mit `dotnet.exe`

### <a name="packagetargetfallback"></a>PackageTargetFallback

Das `PackageTargetFallback`-Element ermöglicht die Angabe eines Satzes von kompatiblen Zielen, die verwendet werden sollen, wenn Pakete wiederhergestellt werden. Dies soll ermöglichen, dass Pakete, in denen ein dotnet [TxM](../reference/target-frameworks.md) verwendet wird, mit kompatiblen Paketen funktionieren, in denen kein dotnet TxM deklariert ist. Wird in Ihrem Projekt das dotnet TxM verwendet, müssen folglich alle Pakete, zu denen es eine Abhängigkeit gibt, ebenfalls ein .NET TxM haben. Dies trifft nur dann nicht zu, wenn Sie das `<PackageTargetFallback>`-Element zu Ihrem Projekt hinzufügen, sodass Nicht-dotnet-Plattformen mit dotnet kompatibel sind.

Wenn im Projekt beispielsweise das `netstandard1.6` TxM verwendet wird, und ein abhängiges Paket nur `lib/net45/a.dll` und `lib/portable-net45+win81/a.dll` enthält, schlägt die Erstellung des Projekts fehl. Wenn es sich bei dem, was Sie importieren möchten, um die letzte DLL handelt, können Sie ein `PackageTargetFallback`-Element wie folgt hinzufügen, um zu sagen, dass die DLL von `portable-net45+win81` kompatibel ist:

```xml
<PackageTargetFallback Condition="'$(TargetFramework)'=='netstandard1.6'">
    portable-net45+win81
</PackageTargetFallback>
```

Lassen Sie das Attribut `Condition` deaktiviert, um einen Fallback für alle Ziele in Ihrem Projekt zu deklarieren. Sie können auch alle vorhandenen `PackageTargetFallback`-Elemente erweitern, indem Sie `$(PackageTargetFallback)` einschließen, wie im Folgenden dargestellt:

```xml
<PackageTargetFallback>
    $(PackageTargetFallback);portable-net45+win81
</PackageTargetFallback >
```

### <a name="replacing-one-library-from-a-restore-graph"></a>Ersetzen einer Bibliothek aus einem Wiederherstellungsdiagramm

Wenn bei einer Wiederherstellung die falsche Assembly eingebunden wurde, kann diese Paketstandardauswahl ausgeschlossen und durch Ihre eigene Wahl ersetzt werden. Schließen Sie zunächst mit einem `PackageReference`-Element der obersten Ebene alle Objekte aus:

```xml
<PackageReference Include="Newtonsoft.Json" Version="9.0.1">
  <ExcludeAssets>All</ExcludeAssets>
</PackageReference>
```

Fügen Sie als Nächstes Ihren eigenen Verweis zur entsprechenden lokalen Kopie der DLL hinzu:

```xml
<Reference Include="Newtonsoft.Json.dll" />
```
