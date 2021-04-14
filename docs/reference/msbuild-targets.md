---
title: NuGet Packen und Wiederherstellen als MSBuild Ziele
description: NuGet Pack und Wiederherstellung können direkt als Ziele MSBuild mit NuGet 4.0 und mehr funktionieren.
author: nkolev92
ms.author: nikolev
ms.date: 03/23/2018
ms.topic: conceptual
no-loc:
- NuGet
- MSBuild
- .nuspec
- nuspec
ms.openlocfilehash: 47411641db47884f79f2bc9a4aa00035fc79993b
ms.sourcegitcommit: c8bf16420f235fc3e42c08cd0d56359e91d490e5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/14/2021
ms.locfileid: "107387373"
---
# <a name="nuget-pack-and-restore-as-msbuild-targets"></a>NuGet Packen und Wiederherstellen als MSBuild Ziele

*NuGet 4.0+*

Mit dem [PackageReference-Format](../consume-packages/package-references-in-project-files.md) kann 4.0 und höher alle Manifestmetadaten direkt in einer Projektdatei speichern, anstatt eine NuGet separate Datei zu `.nuspec` verwenden.

Ab 15.1 ist auch ein erstklassiger Bürger mit den Zielen und , wie MSBuild NuGet unten MSBuild `pack` `restore` beschrieben. Mit diesen Zielen können Sie wie bei jeder anderen Aufgabe NuGet oder jedem anderen MSBuild Ziel arbeiten. Anweisungen zum Erstellen eines NuGet Pakets mit MSBuild finden Sie unter Erstellen eines [ NuGet Pakets mit MSBuild ](../create-packages/creating-a-package-msbuild.md). (Für NuGet 3.x und früher verwenden Sie stattdessen die Befehle [pack](../reference/cli-reference/cli-ref-pack.md) und [restore](../reference/cli-reference/cli-ref-restore.md) über die NuGet CLI.)

## <a name="target-build-order"></a>Buildreihenfolge für Ziele

Da `pack` und `restore` Ziele  MSBuild sind, können Sie darauf zugreifen, um Ihren Workflow zu verbessern. Angenommen, Sie möchten Ihr Paket auf eine Netzwerkfreigabe kopieren, nachdem Sie es gepackt haben. Fügen Sie hierzu Folgendes in Ihrer Projektdatei hinzu:

```xml
<Target Name="CopyPackage" AfterTargets="Pack">
  <Copy
    SourceFiles="$(OutputPath)..\$(PackageId).$(PackageVersion).nupkg"
    DestinationFolder="\\myshare\packageshare\"
    />
</Target>
```

Auf ähnliche Weise können Sie eine MSBuild Aufgabe schreiben, Ihr eigenes Ziel schreiben und NuGet Eigenschaften in der Aufgabe MSBuild nutzen.

> [!NOTE]
> `$(OutputPath)` ist relativ und erwartet, dass Sie den Befehl über das Projektstammverzeichnis ausführen.

## <a name="pack-target"></a>Pack-Ziel

Für .NET-Projekte, die das -Format verwenden, zeichnet mit Eingaben aus der Projektdatei, die beim `PackageReference` `msbuild -t:pack` Erstellen eines Pakets verwendet werden NuGet sollen.

In der folgenden Tabelle werden die Eigenschaften beschrieben, die einer Projektdatei innerhalb des ersten MSBuild Knotens hinzugefügt werden `<PropertyGroup>` können. Sie können diese Änderungen problemlos in Visual Studio 2017 und höheren Versionen vornehmen, indem Sie mit der rechten Maustaste auf das Projekt klicken und **{Project_name} bearbeiten** im Kontextmenü auswählen. Der Einfachheit halber wird die Tabelle nach der entsprechenden Eigenschaft in einer Datei [ `.nuspec` organisiert.](../reference/nuspec.md)

> [!NOTE]
> `Owners` - `Summary` und `.nuspec` -Eigenschaften aus werden mit nicht MSBuild unterstützt.

| nuspecAttribut/Wert | MSBuild -Eigenschaft | Standard | Hinweise |
|--------|--------|--------|--------|
| `Id` | `PackageId` | `$(AssemblyName)` | Extraktion von `$(AssemblyName)` aus MSBuild |
| `Version` | `PackageVersion` | Version | Dies ist semverkompatibel, z. B. `1.0.0` `1.0.0-beta` , oder `1.0.0-beta-00345` |
| `VersionPrefix` | `PackageVersionPrefix` | empty | Festlegen `PackageVersion` von Überschreibungen `PackageVersionPrefix` |
| `VersionSuffix` | `PackageVersionSuffix` | empty | `$(VersionSuffix)` von MSBuild . Festlegen von `PackageVersion` Überschreibungen `PackageVersionSuffix` |
| `Authors` | `Authors` | Name des aktuellen Benutzers | Eine durch Semikolons getrennte Liste von Paketautoren, die den Profilnamen auf nuget.org entspricht. Diese werden im Katalog auf nuget.org angezeigt NuGet und werden verwendet, um von denselben Autoren auf Pakete zu verweisen. |
| `Owners` | – | Nicht in vorhanden nuspec | |
| `Title` | `Title` | Der `PackageId` | Ein benutzerfreundlicher Titel des Pakets, der in der Regel in der Benutzeroberfläche wie auf nuget.org angezeigt wird und der Paket-Manager in Visual Studio. |
| `Description` | `Description` | „Paketbeschreibung“ | Eine lange Beschreibung für die Assembly. Wenn `PackageDescription` nicht angegeben ist, wird diese Eigenschaft auch als Beschreibung des Pakets verwendet. |
| `Copyright` | `Copyright` | empty | Copyright-Informationen für das Paket. |
| `RequireLicenseAcceptance` | `PackageRequireLicenseAcceptance` | `false` | Ein Boolescher Wert, der angibt, ob der Client den Verbraucher dazu auffordern muss, die Paketlizenz vor der Installation des Pakets zu akzeptieren. |
| `license` | `PackageLicenseExpression` | empty | Entspricht `<license type="expression">` Weitere Informationen finden Sie unter [Packen eines Lizenzausdrucks oder einer Lizenzdatei.](#packing-a-license-expression-or-a-license-file) |
| `license` | `PackageLicenseFile` | empty | Der Pfad zu einer Lizenzdatei innerhalb des Pakets, wenn Sie eine benutzerdefinierte Lizenz oder eine Lizenz verwenden, der kein PROTOKOLLDATEI-Bezeichner zugewiesen wurde. Sie müssen die referenzierte Lizenzdatei explizit packen. Entspricht `<license type="file">` Weitere Informationen finden Sie unter [Packen eines Lizenzausdrucks oder einer Lizenzdatei.](#packing-a-license-expression-or-a-license-file) |
| `LicenseUrl` | `PackageLicenseUrl` | empty | `PackageLicenseUrl` ist veraltet. Verwenden Sie stattdessen `PackageLicenseExpression` oder `PackageLicenseFile`. |
| `ProjectUrl` | `PackageProjectUrl` | empty | |
| `Icon` | `PackageIcon` | empty | Ein Pfad zu einem Bild im Paket, das als Paketsymbol verwendet werden soll. Sie müssen die Symbolbilddatei, auf die verwiesen wird, explizit packen. Weitere Informationen finden Sie unter [Packen einer Symbolbilddatei](#packing-an-icon-image-file) und [ `icon` Metadaten.](./nuspec.md#icon) |
| `IconUrl` | `PackageIconUrl` | empty | `PackageIconUrl` ist zugunsten von `PackageIcon` veraltet. Für eine optimale Downlevelerfahrung sollten Sie jedoch `PackageIconUrl` zusätzlich zu `PackageIcon` angeben. |
| `Readme` | `PackageReadmeFile` | empty | Sie müssen die referenzierte Readmedatei explizit packen.|
| `Tags` | `PackageTags` | empty | Eine durch Semikolons getrennte Liste von Tags, die das Paket festlegt. |
| `ReleaseNotes` | `PackageReleaseNotes` | empty | Anmerkungen zu diesem Paket. |
| `Repository/Url` | `RepositoryUrl` | empty | Repository-URL zum Klonen oder Abrufen von Quellcode. Beispiel: *https://github.com/ NuGet / NuGet . Client.git*. |
| `Repository/Type` | `RepositoryType` | empty | Repositorytyp. Beispiele: `git` (Standard), `tfs` . |
| `Repository/Branch` | `RepositoryBranch` | empty | Optionale Repositoryverzweigungsinformationen. `RepositoryUrl` muss ebenfalls angegeben werden, damit diese Eigenschaft einbezogen wird. Beispiel: *master* ( NuGet 4.7.0+). |
| `Repository/Commit` | `RepositoryCommit` | empty | Optionaler Repositorycommit oder ein Changeset, um anzugeben, für welches Quellpaket die Erstellung erfolgt ist. `RepositoryUrl` muss ebenfalls angegeben werden, damit diese Eigenschaft einbezogen wird. Beispiel: *0e4d1b598f350b3dc675018d539114d1328189ef* ( NuGet 4.7.0+). |
| `PackageType` | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| `Summary` | Nicht unterstützt | | |

### <a name="pack-target-inputs"></a>Eingaben für das Ziel „pack“

| Eigenschaft | BESCHREIBUNG |
| - | - |
| `IsPackable` | Ein Boolescher Wert, der angibt, ob das Projekt verpackt werden kann. Der Standardwert ist `true`. |
| `SuppressDependenciesWhenPacking` | Legen Sie auf `true` fest, um Paketabhängigkeiten aus dem generierten Paket zu NuGet unterdrücken. |
| `PackageVersion` | Gibt die Version an, die das resultierende Paket haben wird. Akzeptiert alle Formen von NuGet Versionszeichenfolgen. Standardmäßig beträgt der Wert `$(Version)` der Eigenschaft `Version` im Projekt. |
| `PackageId` | Gibt den Namen für das resultierende Paket an. Wenn nicht angegeben, verwendet der `pack`-Vorgang standardmäßig `AssemblyName` oder den Verzeichnisnamen als Paketnamen. |
| `PackageDescription` | Eine ausführliche Beschreibung des Pakets für die Anzeige der Benutzeroberfläche. |
| `Authors` | Eine durch Semikolons getrennte Liste von Paketautoren, die den Profilnamen auf nuget.org entspricht. Diese werden im Katalog auf nuget.org angezeigt NuGet und werden verwendet, um von denselben Autoren auf Pakete zu verweisen. |
| `Description` | Eine lange Beschreibung für die Assembly. Wenn `PackageDescription` nicht angegeben ist, wird diese Eigenschaft auch als Beschreibung des Pakets verwendet. |
| `Copyright` | Copyright-Informationen für das Paket. |
| `PackageRequireLicenseAcceptance` | Ein Boolescher Wert, der angibt, ob der Client den Verbraucher dazu auffordern muss, die Paketlizenz vor der Installation des Pakets zu akzeptieren. Der Standardwert ist `false`. |
| `DevelopmentDependency` | Ein boolescher Wert, der angibt, ob das Paket mit einer Abhängigkeit markiert werden soll, die nur für die Entwicklung gilt, wodurch vermieden wird, dass das Paket als Abhängigkeit in andere Pakete eingefügt wird. Mit `PackageReference` ( NuGet 4.8+) bedeutet dieses Flag auch, dass Objekte zur Kompilierzeit von der Kompilierung ausgeschlossen werden. Weitere Informationen finden Sie unter [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference) (DevelopmentDependency-Unterstützung für PackageReference). |
| `PackageLicenseExpression` | [EinSCHLÜSSELX-Lizenzbezeichner](https://spdx.org/licenses/) oder -ausdruck, z. `Apache-2.0` B. . Weitere Informationen finden Sie unter [Packen eines Lizenzausdrucks oder einer Lizenzdatei.](#packing-a-license-expression-or-a-license-file) |
| `PackageLicenseFile` | Pfad zu einer Lizenzdatei innerhalb des Pakets, wenn Sie eine benutzerdefinierte Lizenz oder eine Lizenz verwenden, der keinSCHLÜSSELX-Bezeichner zugewiesen wurde. |
| `PackageLicenseUrl` | `PackageLicenseUrl` ist veraltet. Verwenden Sie stattdessen `PackageLicenseExpression` oder `PackageLicenseFile`. |
| `PackageProjectUrl` | |
| `PackageIcon` | Gibt den Paketsymbolpfad relativ zum Stamm des Pakets an. Weitere Informationen finden Sie unter [Packen einer Symbolbilddatei.](#packing-an-icon-image-file) |
| `PackageReleaseNotes` | Anmerkungen zu diesem Paket. |
| `PackageReadmeFile` | Readme für das Paket. |
| `PackageTags` | Eine durch Semikolons getrennte Liste von Tags, die das Paket festlegt. |
| `PackageOutputPath` | Bestimmt den Ausgabepfad, in dem das gepackte Paket abgelegt wird. Der Standardwert ist `$(OutputPath)`. |
| `IncludeSymbols` | Dieser Boolesche Wert gibt an, ob das Paket ein zusätzliches Symbolpaket erstellen soll, wenn das Projekt verpackt wird. Das Format des Symbolpakets wird durch die Eigenschaft `SymbolPackageFormat` gesteuert. Weitere Informationen finden Sie unter [IncludeSymbols](#includesymbols). |
| `IncludeSource` | Dieser Boolesche Wert gibt an, ob der Packprozess ein Quellpaket erstellen sollte. Das Quellpaket enthält den Quellcode der Bibliothek sowie die PDB-Dateien. Quelldateien werden im `src/ProjectName`-Verzeichnis in der resultierenden Paketdatei gespeichert. Weitere Informationen finden Sie unter [IncludeSource](#includesource). |
| `PackageType` | |
| `IsTool` | Gibt an, ob alle Ausgabedateien in den *Tools*-Ordner anstelle des *Lib*-Ordners kopiert werden. Weitere Informationen finden Sie unter [IsTool](#istool). |
| `RepositoryUrl` | Repository-URL zum Klonen oder Abrufen von Quellcode. Beispiel: *https://github.com/ NuGet / NuGet . Client.git*. |
| `RepositoryType` | Repositorytyp. Beispiele: `git` (Standard), `tfs` . |
| `RepositoryBranch` | Optionale Repositoryverzweigungsinformationen. `RepositoryUrl` muss ebenfalls angegeben werden, damit diese Eigenschaft einbezogen wird. Beispiel: *master* ( NuGet 4.7.0+). |
| `RepositoryCommit` | Optionaler Repositorycommit oder ein Changeset, um anzugeben, für welches Quellpaket die Erstellung erfolgt ist. `RepositoryUrl` muss ebenfalls angegeben werden, damit diese Eigenschaft einbezogen wird. Beispiel: *0e4d1b598f350b3dc675018d539114d1328189ef* ( NuGet 4.7.0+). |
| `SymbolPackageFormat` | Gibt das Format des Symbolpakets an. Bei "symbols.nupkg" wird ein Legacysymbolpaket mit der Erweiterung *.symbols.nupkg* erstellt, die PDBs, DLLs und andere Ausgabedateien enthält. Bei "snupkg" wird ein SNUPKG-Symbolpaket erstellt, das die portablen PDBs enthält. Der Standardwert ist "symbols.nupkg". |
| `NoPackageAnalysis` | Gibt an, dass `pack` nach dem Erstellen des Pakets keine Paketanalyse ausführen soll. |
| `MinClientVersion` | Gibt die Mindestversion des Clients an, der NuGet dieses Paket installieren kann, die von nuget.exe und dem Visual Studio Paket-Manager erzwungen wird. |
| `IncludeBuildOutput` | Dieser Boolesche Wert gibt an, ob die Buildausgabeassemblys in die *NUPKG*-Datei gepackt werden sollen oder nicht. |
| `IncludeContentInPack` | Dieser boolesche Wert gibt an, ob Elemente mit dem Typ `Content` automatisch im resultierenden Paket enthalten sind. Der Standardwert lautet `true`. |
| `BuildOutputTargetFolder` | Gibt den Ordner an, in dem die Ausgabeassemblys abgelegt werden. Die Ausgabeassemblys (und andere Ausgabedateien) werden in ihre jeweiligen Frameworkordner kopiert. Weitere Informationen finden Sie unter [Ausgabeassemblys.](#output-assemblies) |
| `ContentTargetFolders` | Gibt den Standardspeicherort von an, an dem alle Inhaltsdateien gespeichert werden sollen, wenn `PackagePath` nicht für sie angegeben ist. Der Standardwert ist „content;contentFiles“. Weitere Informationen finden Sie unter [Inhalt in ein Paket einschließen](#including-content-in-a-package). |
| `NuspecFile` | Relativer oder absoluter Pfad zur Datei, die *.nuspec* zum Packen verwendet wird. Wenn angegeben, wird es **ausschließlich** zum Verpacken von Informationen verwendet, und alle Informationen in den Projekten werden nicht verwendet. Weitere Informationen finden Sie unter [Packen mit einem .nuspec ](#packing-using-a-nuspec-file). |
| `NuspecBasePath` | Basispfad für die *.nuspec* Datei. Weitere Informationen finden Sie unter [Packen mit einem .nuspec ](#packing-using-a-nuspec-file). |
| `NuspecProperties` | Durch Semikolons getrennte Liste der Schlüssel = Wertpaare. Weitere Informationen finden Sie unter [Packen mit einem .nuspec ](#packing-using-a-nuspec-file). |

## <a name="pack-scenarios"></a>Pack-Szenarios

### <a name="suppressing-dependencies"></a>Unterdrücken von Abhängigkeiten

Um Paketabhängigkeiten von generierten NuGet Paketen zu unterdrücken, legen Sie `SuppressDependenciesWhenPacking` auf `true` fest, um das Überspringen aller Abhängigkeiten aus der generierten NUPKG-Datei zu ermöglichen.

### `PackageIconUrl`

`PackageIconUrl` ist zugunsten der [`PackageIcon`](#packageicon) -Eigenschaft veraltet. Ab NuGet Version 5.3 und Visual Studio 2019 Version 16.3 `pack` löst die [NU5048-Warnung](./errors-and-warnings/nu5048.md) aus, wenn die Paketmetadaten nur `PackageIconUrl` angeben.

### `PackageIcon`

> [!Tip]
> Um abwärtskompatibilität mit Clients und Quellen zu gewährleisten, die noch nicht `PackageIcon` unterstützen, geben Sie sowohl als auch `PackageIcon` `PackageIconUrl` an. Visual Studio unterstützt `PackageIcon` Pakete, die aus einer ordnerbasierten Quelle stammen.

#### <a name="packing-an-icon-image-file"></a>Packen einer Symbolbilddatei

Verwenden Sie beim Packen einer Symbolbilddatei `PackageIcon` die -Eigenschaft, um den Dateipfad des Symbols relativ zum Stamm des Pakets anzugeben. Stellen Sie außerdem sicher, dass die Datei im Paket enthalten ist. Die Größe der Bilddatei ist auf 1 MB beschränkt. Unterstützte Dateiformate sind JPEG und PNG. Es wird eine Bildauflösung von 128 x 128 empfohlen.

Beispiel:

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

[Paketsymbolbeispiel](https://github.com/NuGet/Samples/tree/main/PackageIconExample).

Sehen Sie sich als nuspec Äquivalent den [ nuspec Verweis auf das Symbol](nuspec.md#icon)an.

### <a name="packagereadmefile"></a>PackageReadmeFile

Beim Packen einer Readme-Datei müssen Sie die `PackageReadmeFile` -Eigenschaft verwenden, um den Paketpfad relativ zum Stamm des Pakets anzugeben. Darüber hinaus müssen Sie sicherstellen, dass die Datei im Paket enthalten ist. Unterstützte Dateiformate umfassen nur Markdown (*.md*).

Beispiel:

```xml
<PropertyGroup>
    ...
    <PackageReadmeFile>readme.md</PackageReadmeFile>
    ...
</PropertyGroup>

<ItemGroup>
    ...
    <None Include="docs\readme.md" Pack="true" PackagePath="\"/>
    ...
</ItemGroup>
```

Sehen Sie sich für die nuspec Entsprechende einen Verweis auf die [ nuspec Readme](nuspec.md#readme)an.

### <a name="output-assemblies"></a>Ausgabeassemblys

`nuget pack` kopiert Ausgabedateien mit den Erweiterungen `.exe`, `.dll`, `.xml`, `.winmd`, `.json` und `.pri`. Welche Ausgabedateien kopiert werden, hängt davon ab, was MSBuild vom `BuiltOutputProjectGroup` Ziel bereitstellt.

Es gibt zwei MSBuild  Eigenschaften, die Sie in Der Projektdatei oder Befehlszeile verwenden können, um zu steuern, wohin Ausgabeassemblys wechseln:

- `IncludeBuildOutput`: Ein boolescher Wert, der bestimmt, ob die Ausgabeassemblys des Builds in das Paket eingeschlossen werden sollten.
- `BuildOutputTargetFolder`: Gibt den Ordner an, in dem die Ausgabeassemblys angeordnet werden sollten. Die Ausgabeassemblys (und andere Ausgabedateien) werden in ihre jeweiligen Frameworkordner kopiert.

### <a name="package-references"></a>Paketverweise

Siehe [Package References in Project Files ](../consume-packages/package-references-in-project-files.md) (Paketverweise in Projektdateien).

### <a name="project-to-project-references"></a>Projekt-zu-Projekt-Verweise

Projekt-zu-Projekt-Verweise werden standardmäßig als NuGet Paketverweise betrachtet. Beispiel:

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

Wenn Sie ihren gesamten Inhalt nur in einen bestimmten Stammordner (anstelle von und beidem) kopieren `content` `contentFiles` möchten, können Sie die MSBuild Eigenschaft `ContentTargetFolders` verwenden, die standardmäßig auf "content;contentFiles" festgelegt ist, aber auf alle anderen Ordnernamen festgelegt werden kann. Beachten Sie Folgendes: Wenn Sie in `ContentTargetFolders` nur „contentFiles“ angeben, werden Dateien unter `contentFiles\any\<target_framework>` oder `contentFiles\<language>\<target_framework>` basierend auf `buildAction` angeordnet.

`PackagePath` kann eine durch Semikolons (;) getrennte Reihe von Zielpfaden sein. Durch die Angabe eines leeren Paketpfads würde die Datei zum Stammverzeichnis des Pakets hinzugefügt. Im Folgenden wird beispielsweise `libuv.txt` zu`content\myfiles`, `content\samples` und dem Stammverzeichnis des Pakets hinzugefügt:

```xml
<Content Include="..\win7-x64\libuv.txt">
  <Pack>true</Pack>
  <PackagePath>content\myfiles;content\sample;;</PackagePath>
</Content>
```

Es gibt auch eine MSBuild `$(IncludeContentInPack)` -Eigenschaft, die standardmäßig auf eingestellt `true` ist. Wenn diese in einem Projekt auf `false` festgelegt wird, werden die Inhalte aus diesem Projekt nicht in das NuGet-Paket eingeschlossen.

Andere packspezifische Metadaten, die Sie für eines der oben genannten Elemente festlegen können, enthalten und die - ```<PackageCopyToOutput>``` ```<PackageFlatten>``` und ```CopyToOutput``` ```Flatten``` -Werte für den Eintrag in der ```contentFiles``` Ausgabe nuspec festlegen.

> [!Note]
> Die Metadaten `<Pack>` und `<PackagePath>` können nicht nur auf Inhaltselemente, sondern auch auf Dateien mit den Buildvorgängen „Compile“, „EmbeddedResource“, „ApplicationDefinition“, „Page“, „Resource“, „SplashScreen“, „DesignData“, „DesignDataWithDesignTimeCreateableTypes“, „CodeAnalysisDictionary“, „AndroidAsset“, „AndroidResource“, „BundleResource“ oder „None“ festgelegt werden.
>
> Damit das Ziel „pack“ bei der Verwendung von Globmustern den Dateinamen an Ihren Paketpfad anhängt, muss Ihr Paketpfad mit dem Ordnertrennzeichen enden. Andernfalls wird der Paketpfad als vollständiger Pfad einschließlich des Dateinamens behandelt.

### <a name="includesymbols"></a>IncludeSymbols

Bei Verwendung von `MSBuild -t:pack -p:IncludeSymbols=true` werden die entsprechenden `.pdb`-Dateien zusammen mit anderen Ausgabedateien kopiert (`.dll`, `.exe`, `.winmd`, `.xml`, `.json`, `.pri`). Beachten Sie, dass durch das Festlegen von `IncludeSymbols=true` ein reguläres Paket *und* ein Symbolpaket erstellt werden.

### <a name="includesource"></a>IncludeSource

Dies ist mit `IncludeSymbols` identisch. Der einzige Unterschied besteht darin, dass Quelldateien auch zusammen mit `.pdb`-Dateien kopiert werden. Alle Dateien vom Typ `Compile` werden in `src\<ProjectName>\` kopiert. Dabei wird die Ordnerstruktur im relativen Pfad im resultierenden Paket beibehalten. Gleiches gilt auch für Quelldateien einer beliebigen `ProjectReference`, bei der `TreatAsPackageReference` auf `false` festgelegt ist.

Wenn sich eine Datei vom Typ „Compile“ außerhalb des Projektordners befindet, wird sie nur zu `src\<ProjectName>\` hinzugefügt.

### <a name="packing-a-license-expression-or-a-license-file"></a>Packen eines Lizenzausdrucks oder einer Lizenzdatei

Wenn Sie einen Lizenzausdruck verwenden, verwenden Sie die `PackageLicenseExpression` -Eigenschaft. Ein Beispiel finden Sie unter [Lizenzausdrucksbeispiel.](https://github.com/NuGet/Samples/tree/main/PackageLicenseExpressionExample)

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

Weitere Informationen zu Lizenzausdrücken und Lizenzen, die von .org akzeptiert NuGet werden, finden Sie unter [Lizenzmetadaten.](nuspec.md#license)

Verwenden Sie beim Packen einer Lizenzdatei `PackageLicenseFile` die -Eigenschaft, um den Paketpfad relativ zum Stamm des Pakets anzugeben. Stellen Sie außerdem sicher, dass die Datei im Paket enthalten ist. Beispiel:

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```

Ein Beispiel finden Sie unter Beispiel für [eine Lizenzdatei.](https://github.com/NuGet/Samples/tree/main/PackageLicenseFileExample)

> [!NOTE]
> Es kann jeweils nur eine von `PackageLicenseExpression` `PackageLicenseFile` , und angegeben `PackageLicenseUrl` werden.

### <a name="packing-a-file-without-an-extension"></a>Packen einer Datei ohne Erweiterung

In einigen Szenarien, z. B. beim Packen einer Lizenzdatei, sollten Sie eine Datei ohne Erweiterung einschließen.
Behandeln Sie Pfade ohne Erweiterung aus historischen Gründen NuGet  &  MSBuild als Verzeichnisse.

```xml
  <PropertyGroup>
    <TargetFrameworks>netstandard2.0</TargetFrameworks>
    <PackageLicenseFile>LICENSE</PackageLicenseFile>
  </PropertyGroup>

  <ItemGroup>
    <None Include="LICENSE" Pack="true" PackagePath=""/>
  </ItemGroup>  
```

[Datei ohne Erweiterungsbeispiel](https://github.com/NuGet/Samples/blob/main/PackageLicenseFileExtensionlessExample/).

### <a name="istool"></a>IsTool

Bei Verwendung von `MSBuild -t:pack -p:IsTool=true` werden alle Ausgabedateien entsprechend den Angaben im Szenario [Ausgabeassemblys](#output-assemblies) in den Ordner `tools` und nicht in den Ordner `lib` kopiert. Beachten Sie, dass sich dies von einem `DotNetCliTool` unterscheidet, das durch Festlegen von `PackageType` in der `.csproj`-Datei angegeben wird.

### <a name="packing-using-a-nuspec-file"></a>Packen mithilfe einer `.nuspec` Datei

Obwohl es empfohlen wird, [alle Eigenschaften, die](../reference/msbuild-targets.md#pack-target) sich normalerweise in der Datei befinden, `.nuspec` stattdessen in die Projektdatei einzufügen, können Sie eine Datei zum `.nuspec` Packen Des Projekts verwenden. Für ein Nicht-SDK-Projekt, das `PackageReference` verwendet, müssen Sie `NuGet.Build.Tasks.Pack.targets` importieren, damit die Paketaufgabe ausgeführt werden kann. Sie müssen das Projekt dennoch wiederherstellen, bevor Sie eine Datei packen nuspec können. (Ein Projekt im SDK-Stil enthält standardmäßig die Paketziele.)

Das Zielframework der Projektdatei ist irrelevant und wird beim Packen eines nicht nuspec verwendet. Die folgenden drei MSBuild Eigenschaften sind für das Packen mit einem `.nuspec` relevant:

1. `NuspecFile`: Relativer oder absoluter Pfad zur `.nuspec`-Datei, der für das Packen verwendet wird.
1. `NuspecProperties`: Durch Semikolons (;) getrennte Liste der Schlüssel/Wert-Paare. Aufgrund der Funktionsweise der MSBuild Befehlszeilenparsierung müssen mehrere Eigenschaften wie folgt angegeben werden: `-p:NuspecProperties="key1=value1;key2=value2"` .  
1. `NuspecBasePath`: Der Basispfad für die `.nuspec`-Datei.

Wenn Sie Ihr Projekt mithilfe der Datei `dotnet.exe` packen, verwenden Sie einen Befehl wie den folgenden:

```dotnetcli
dotnet pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

Wenn Sie Ihr Projekt mithilfe der Datei MSBuild packen, verwenden Sie einen Befehl wie den folgenden:

```cli
msbuild -t:pack <path to .csproj file> -p:NuspecFile=<path to nuspec file> -p:NuspecProperties=<> -p:NuspecBasePath=<Base path> 
```

Beachten Sie, dass das Packen eines nuspec mithilfe von dotnet.exe oder msbuild standardmäßig auch zum Erstellen des Projekts führt. Dies kann vermieden werden, indem die -Eigenschaft an dotnet.exe übergeben ```--no-build``` wird. Dies entspricht der Einstellung ```<NoBuild>true</NoBuild> ``` in der Projektdatei zusammen mit der Einstellung ```<IncludeBuildOutput>false</IncludeBuildOutput> ``` in der Projektdatei.

Ein Beispiel für eine *CSPROJ-Datei* zum Packen einer nuspec Datei ist:

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

Das `pack` Ziel stellt zwei Erweiterungspunkte bereit, die im inneren, zielframeworkspezifischen Build ausgeführt werden. Die Erweiterungspunkte unterstützen das Einschließen von zielframeworkspezifischen Inhalten und Assemblys in ein Paket:

- `TargetsForTfmSpecificBuildOutput` target: Verwenden Sie für Dateien innerhalb des `lib` Ordners oder eines Ordners, der mit angegeben `BuildOutputTargetFolder` wurde.
- `TargetsForTfmSpecificContentInPackage` target: Wird für Dateien außerhalb von `BuildOutputTargetFolder` verwendet.

#### `TargetsForTfmSpecificBuildOutput`

Schreiben Sie ein benutzerdefiniertes Ziel, und geben Sie es als Wert der `$(TargetsForTfmSpecificBuildOutput)` -Eigenschaft an. Für alle Dateien, die in die `BuildOutputTargetFolder` (standardmäßig lib) wechseln müssen, sollte das Ziel diese Dateien in die ItemGroup schreiben `BuildOutputInPackage` und die folgenden beiden Metadatenwerte festlegen:

- `FinalOutputPath`: Der absolute Pfad der Datei; Wenn keine Angabe erfolgt, wird die Identität zum Auswerten des Quellpfads verwendet.
- `TargetPath`: (Optional) Legen Sie fest, wenn die Datei in einem Unterordner in abgelegt werden muss, z. B. `lib\<TargetFramework>` Satellitenassemblys, die sich unter ihren jeweiligen Kulturordnern befinden. Der Standardwert ist der Name der Datei.

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

#### `TargetsForTfmSpecificContentInPackage`

Schreiben Sie ein benutzerdefiniertes Ziel, und geben Sie es als Wert der `$(TargetsForTfmSpecificContentInPackage)` -Eigenschaft an. Damit dateien in das Paket aufgenommen werden, sollte das Ziel diese Dateien in die ItemGroup schreiben `TfmSpecificPackageFile` und die folgenden optionalen Metadaten festlegen:

- `PackagePath`: Pfad, unter dem die Datei im Paket ausgegeben werden soll. NuGet gibt eine Warnung aus, wenn dem gleichen Paketpfad mehrere Dateien hinzugefügt werden.
- `BuildAction`: Die Buildaktion, die der Datei zugewiesen werden soll, ist nur erforderlich, wenn sich der Paketpfad im `contentFiles` Ordner befindet. Der Standardwert ist "None".

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
1. Übergeben von MSBuild Daten an NuGet.Build.Tasks.dll
1. Ausführen des Befehls „restore“
1. Herunterladen von Paketen
1. Schreiben von Assetdatei, Zielen und Eigenschaften

Das `restore` Ziel funktioniert für Projekte mit dem PackageReference-Format.
`MSBuild 16.5+`[unterstützt](#restoring-packagereference-and-packagesconfig-projects-with-msbuild) auch das `packages.config` Format.

> [!NOTE]
> Das `restore` Ziel sollte nicht in Kombination [mit](#restoring-and-building-with-one-msbuild-command) dem Ziel ausgeführt `build` werden.

### <a name="restore-properties"></a>Wiederherstellen von Eigenschaften

Zusätzliche Wiederherstellungseinstellungen können von MSBuild Eigenschaften in der Projektdatei stammen. Werte können auch mithilfe des `-p:`-Switch über die Befehlszeile festgelegt werden (siehe nachfolgende Beispiele).

| Eigenschaft | BESCHREIBUNG |
|--------|--------|
| `RestoreSources` | Eine durch Semikolons (;) getrennte Liste mit Paketquellen. |
| `RestorePackagesPath` | Ordnerpfad der Pakete für Benutzer. |
| `RestoreDisableParallel` | Begrenzt Downloads auf jeweils einen Download. |
| `RestoreConfigFile` | Der Pfad zu einer anzuwendenden `Nuget.Config`-Datei. |
| `RestoreNoCache` | Bei "true" wird die Verwendung zwischengespeicherter Pakete vermieden. Weitere Informationen [finden Sie unter Verwalten der globalen Pakete und Cacheordner.](../consume-packages/managing-the-global-packages-and-cache-folders.md) |
| `RestoreIgnoreFailedSources` | Wenn „TRUE“ festgelegt ist, werden fehlerhafte oder fehlende Paketquellen ignoriert. |
| `RestoreFallbackFolders` | Fallbackordner, die auf die gleiche Weise wie der Benutzerpaketordner verwendet werden. |
| `RestoreAdditionalProjectSources` | Zusätzliche Quellen, die während der Wiederherstellung verwendet werden. |
| `RestoreAdditionalProjectFallbackFolders` | Zusätzliche Fallbackordner, die während der Wiederherstellung verwendet werden sollen. |
| `RestoreAdditionalProjectFallbackFoldersExcludes` | Schließt Fallbackordner aus, die in angegeben sind. `RestoreAdditionalProjectFallbackFolders` |
| `RestoreTaskAssemblyFile` | Pfad zu `NuGet.Build.Tasks.dll`. |
| `RestoreGraphProjectInput` | Durch Semikolons (;) getrennte Liste mit wiederherzustellenden Projekten, die absolute Pfade enthalten sollten. |
| `RestoreUseSkipNonexistentTargets`  | Wenn die Projekte über gesammelt MSBuild werden, bestimmt sie, ob sie mithilfe der Optimierung gesammelt `SkipNonexistentTargets` werden. Wenn nicht festgelegt, wird standardmäßig auf `true` festgelegt. Die Folge ist ein fail-fast-Verhalten, wenn die Ziele eines Projekts nicht importiert werden können. |
| `MSBuildProjectExtensionsPath` | Ausgabeordner, standardmäßig und `BaseIntermediateOutputPath` der `obj` Ordner. |
| `RestoreForce` | In PackageReference-basierten Projekten erzwingt, dass alle Abhängigkeiten aufgelöst werden, auch wenn die letzte Wiederherstellung erfolgreich war. Die Angabe dieses Flags ähnelt dem Löschen der `project.assets.json` Datei. Dadurch wird http-cache nicht umgangen. |
| `RestorePackagesWithLockFile` | Ermöglicht die Verwendung einer Sperrdatei. |
| `RestoreLockedMode` | Führen Sie die Wiederherstellung im gesperrten Modus aus. Dies bedeutet, dass die Abhängigkeiten bei der Wiederherstellung nicht neu ausgewertet werden. |
| `NuGetLockFilePath` | Ein benutzerdefinierter Speicherort für die Sperrdatei. Der Standardspeicherort befindet sich neben dem Projekt und hat den Namen `packages.lock.json` . |
| `RestoreForceEvaluate` | Erzwingt die Wiederherstellung, um die Abhängigkeiten neu zu kompilieren und die Sperrdatei ohne Warnung zu aktualisieren. |
| `RestorePackagesConfig` | Ein opt-in-Switch, mit dem Projekte mit packages.config wiederhergestellt werden. Unterstützung `MSBuild -t:restore` nur mit. |
| `RestoreUseStaticGraphEvaluation` | Ein opt-in-Schalter zur Verwendung der statischen MSBuild Graphauswertung anstelle der Standardauswertung. Die Statische Graphauswertung ist ein experimentelles Feature, das für große Repositorys und Lösungen erheblich schneller ist. |

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
| `project.assets.json` | Enthält das Abhängigkeitsdiagramm aller Paketverweise. |
| `{projectName}.projectFileExtension.nuget.g.props` | Verweise auf MSBuild in Paketen enthaltene Props |
| `{projectName}.projectFileExtension.nuget.g.targets` | Verweise auf MSBuild Ziele in Paketen |

### <a name="restoring-and-building-with-one-msbuild-command"></a>Wiederherstellen und Erstellen mit einem MSBuild Befehl

Aufgrund der Tatsache, dass NuGet Pakete wiederherstellen kann, die Ziele und Eigenschaften herunterfahren, MSBuild werden die Wiederherstellungs- und Buildauswertungen mit unterschiedlichen globalen Eigenschaften ausgeführt.
Dies bedeutet, dass das folgende Verhalten unvorhersehbar und häufig falsch ist.

```cli
msbuild -t:restore,build
```

 Stattdessen wird folgende Vorgehensweise empfohlen:

```cli
msbuild -t:build -restore
```

Dieselbe Logik gilt für andere Ziele ähnlich `build` wie .

### <a name="restoring-packagereference-and-packagesconfig-projects-with-msbuild"></a>Wiederherstellen von PackageReference- und packages.config-Projekten mit MSBuild

Ab MSBuild 16.5 werden packages.config auch für `msbuild -t:restore` unterstützt.

```cli
msbuild -t:restore -p:RestorePackagesConfig=true
```

> [!NOTE]
> `packages.config`Restore ist nur mit und nicht mit verfügbar. `MSBuild 16.5+``dotnet.exe`

### <a name="restoring-with-msbuild-static-graph-evaluation"></a>Wiederherstellen mit MSBuild statischer Graphauswertung

> [!NOTE]
> Mit MSBuild 16.6 und höher NuGet wurde ein experimentelles Feature zur Verwendung der statischen Graphauswertung über die Befehlszeile hinzugefügt, das die Wiederherstellungszeit für große Repositorys erheblich verbessert.

```cli
msbuild -t:restore -p:RestoreUseStaticGraphEvaluation=true
```

Alternativ können Sie sie aktivieren, indem Sie die -Eigenschaft in einer Directory.Build.Props-Datei festlegen.

```xml
<Project>
  <PropertyGroup>
    <RestoreUseStaticGraphEvaluation>true</RestoreUseStaticGraphEvaluation>
  </PropertyGroup>
</Project>
```

> [!NOTE]
> Ab Visual Studio 2019.x und NuGet 5.x gilt dieses Feature als experimentell und aktiviert. Ausführliche Informationen dazu, wann dieses Feature standardmäßig aktiviert wird, finden Sie unter [ NuGet /Home#9803.](https://github.com/NuGet/Home/issues/9803)

Statische Graphwiederherstellung ändert den msbuild-Teil der Wiederherstellung, das Lesen und Auswerten des Projekts, aber nicht den Wiederherstellungsalgorithmus! Der Wiederherstellungsalgorithmus ist für alle Tools NuGet gleich ( NuGet EXE, MSBuild EXE, dotnet.exe und Visual Studio).

In sehr wenigen Szenarien verhält sich die statische Graphwiederherstellung möglicherweise anders als die aktuelle Wiederherstellung, und bestimmte deklarierte PackageReferences oder ProjectReferences fehlen möglicherweise.

Um Ihre Meinung zu erleichtern, sollten Sie bei der Migration zur statischen Graphwiederherstellung eine einmalige Überprüfung in Betracht ziehen:

```cli
msbuild.exe -t:restore -p:RestoreUseStaticGraphEvaluation
msbuild.exe -t:restore
```

NuGet sollte *keine* Änderungen melden. Wenn eine Abweichung vor sich geht, melden Sie ein Problem unter [ NuGet /Home](https://github.com/nuget/home/issues/new).

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