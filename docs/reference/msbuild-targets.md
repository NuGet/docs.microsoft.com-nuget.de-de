---
title: NuGet pack and restore as MSBuild targets (NuGet-Befehle „pack“ und „restore“ MSBuild-Ziele)
description: Die NuGet-Befehle „pack“ und „restore“ können direkt als MSBuild-Ziele mit NuGet 4.0 und höher arbeiten.
author: nkolev92
ms.author: nikolev
ms.date: 03/23/2018
ms.topic: conceptual
ms.openlocfilehash: 0c32978baf6146f10c262ba7af94f61fee22272d
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777716"
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

Für .net-Projekte, die das- `PackageReference` Format verwenden, `msbuild -t:pack` zeichnet mithilfe von Eingaben aus der Projektdatei, die beim Erstellen eines nuget-Pakets verwendet werden sollen.

In der folgenden Tabelle werden die MSBuild-Eigenschaften beschrieben, die einer Projektdatei innerhalb des ersten Knotens hinzugefügt werden können `<PropertyGroup>` . Sie können diese Änderungen problemlos in Visual Studio 2017 und höheren Versionen vornehmen, indem Sie mit der rechten Maustaste auf das Projekt klicken und **{Project_name} bearbeiten** im Kontextmenü auswählen. Zur einfacheren Handhabung wird die Tabelle nach der entsprechenden Eigenschaft in einer [ `.nuspec` Datei](../reference/nuspec.md)organisiert.

Beachten Sie, dass die Eigenschaften `Owners` und `Summary` aus einer `.nuspec`-Datei in MSBuild nicht unterstützt werden.

| Attribut/NuSpec-Wert | MSBuild-Eigenschaft | Standard | Hinweise |
|--------|--------|--------|--------|
| Id | PackageId | AssemblyName | $(AssemblyName) aus MSBuild |
| Version | PackageVersion | Version | Diese Eigenschaft ist mit „semver“ kompatibel, z.B. „1.0.0“, „1.0.0-beta“ oder „1.0.0-beta-00345“ |
| VersionPrefix | PackageVersionPrefix | empty | Durch das Festlegen von PackageVersion wird PackageVersionPrefix überschrieben |
| VersionSuffix | PackageVersionSuffix | empty | $(VersionSuffix) aus MSBuild. Durch das Festlegen von PackageVersion wird PackageVersionSuffix überschrieben |
| Authors | Authors | Name des aktuellen Benutzers | Eine durch Semikolons getrennte Liste der Paketautoren, die mit Profilnamen unter nuget.org übereinstimmen. Diese werden im NuGet-Katalog unter nuget.org angezeigt und werden verwendet, um Querverweise auf Pakete von den gleichen Autoren zu geben. |
| Besitzer | – | In NuSpec nicht vorhanden | |
| Titel | Titel | Die PackageId| Ein benutzerfreundlicher Titel des Pakets, der in der Regel in der Benutzeroberfläche wie auf nuget.org angezeigt wird und der Paket-Manager in Visual Studio. |
| BESCHREIBUNG | BESCHREIBUNG | „Paketbeschreibung“ | Eine lange Beschreibung für die Assembly. Wenn `PackageDescription` nicht angegeben ist, wird diese Eigenschaft auch als Beschreibung des Pakets verwendet. |
| Copyright | Copyright | empty | Copyright-Informationen für das Paket. |
| RequireLicenseAcceptance | PackageRequireLicenseAcceptance | false | Ein Boolescher Wert, der angibt, ob der Client den Verbraucher dazu auffordern muss, die Paketlizenz vor der Installation des Pakets zu akzeptieren. |
| license | PackageLicenseExpression | empty | Entspricht `<license type="expression">` Weitere Informationen finden Sie unter [Verpacken eines Lizenz Ausdrucks oder einer Lizenzdatei](#packing-a-license-expression-or-a-license-file). |
| license | PackageLicenseFile | empty | Der Pfad zu einer Lizenzdatei innerhalb des Pakets, wenn Sie eine benutzerdefinierte Lizenz oder eine Lizenz verwenden, der kein spdx-Bezeichner zugewiesen wurde. Sie müssen die referenzierte Lizenzdatei explizit verpacken. Entspricht `<license type="file">` Weitere Informationen finden Sie unter [Verpacken eines Lizenz Ausdrucks oder einer Lizenzdatei](#packing-a-license-expression-or-a-license-file). |
| LicenseUrl | PackageLicenseUrl | empty | `PackageLicenseUrl` ist veraltet. Verwenden Sie stattdessen `PackageLicenseExpression` oder `PackageLicenseFile`. |
| ProjectUrl | PackageProjectUrl | empty | |
| Symbol | PackageIcon | empty | Ein Pfad zu einem Bild im Paket, das als Paketsymbol verwendet werden soll. Sie müssen explizit die Symbolbild Datei, auf die verwiesen wird, verpacken. Weitere Informationen finden Sie unter [Packen einer Symbolbild Datei](#packing-an-icon-image-file) und von [ `icon` Metadaten](/nuget/reference/nuspec#icon). |
| IconUrl | PackageIconUrl | empty | `PackageIconUrl` wird als veraltet markiert `PackageIcon` . Allerdings sollten Sie für die bestmögliche downlevelfunktion zusätzlich `PackageIconUrl` zu angeben `PackageIcon` . |
| Tags | PackageTags | empty | Eine durch Semikolons getrennte Liste von Tags, die das Paket festlegt. |
| ReleaseNotes | PackageReleaseNotes | empty | Anmerkungen zu diesem Paket. |
| Repository/URL | RepositoryUrl | empty | Die Repository-URL, die zum Klonen oder Abrufen von Quellcode verwendet wird. Beispiel: *https://github.com/NuGet/NuGet.Client.git* . |
| Repository/Typ | RepositoryType | empty | Der Repository-Typ. Beispiele: `git` (Standard), `tfs` . |
| Repository/Verzweigung | RepositoryBranch | empty | Optionale Informationen zum Repository-Branch. `RepositoryUrl` muss ebenfalls angegeben werden, damit diese Eigenschaft einbezogen wird. Beispiel: *Master* (nuget 4.7.0 +). |
| Repository/Commit | RepositoryCommit | empty | Optionaler Repositorycommit oder ein Changeset, um anzugeben, für welches Quellpaket die Erstellung erfolgt ist. `RepositoryUrl` muss ebenfalls angegeben werden, damit diese Eigenschaft einbezogen wird. Beispiel: *0e4d1b598f 350 b3dc675018d539114d1328189ef* (nuget 4.7.0 +). |
| PackageType | `<PackageType>DotNetCliTool, 1.0.0.0;Dependency, 2.0.0.0</PackageType>` | | |
| Zusammenfassung | Nicht unterstützt | | |

### <a name="pack-target-inputs"></a>Eingaben für das Ziel „pack“

| Eigenschaft | BESCHREIBUNG |
| - | - |
| IsPackable | Ein Boolescher Wert, der angibt, ob das Projekt verpackt werden kann. Der Standardwert ist `true`. |
| Suppressdependenciesder Verpackung | Legen Sie auf fest, `true` um Paketabhängigkeiten aus dem generierten nuget-Paket zu unterdrücken. |
| PackageVersion | Gibt die Version an, die das resultierende Paket haben wird. Akzeptiert alle Arten von NuGet-Versionszeichenfolgen. Standardmäßig beträgt der Wert `$(Version)` der Eigenschaft `Version` im Projekt. |
| PackageId | Gibt den Namen für das resultierende Paket an. Wenn nicht angegeben, verwendet der `pack`-Vorgang standardmäßig `AssemblyName` oder den Verzeichnisnamen als Paketnamen. |
| PackageDescription | Eine ausführliche Beschreibung des Pakets für die Anzeige der Benutzeroberfläche. |
| Authors | Eine durch Semikolons getrennte Liste der Paketautoren, die mit Profilnamen unter nuget.org übereinstimmen. Diese werden im NuGet-Katalog unter nuget.org angezeigt und werden verwendet, um Querverweise auf Pakete von den gleichen Autoren zu geben. |
| Beschreibung | Eine lange Beschreibung für die Assembly. Wenn `PackageDescription` nicht angegeben ist, wird diese Eigenschaft auch als Beschreibung des Pakets verwendet. |
| Copyright | Copyright-Informationen für das Paket. |
| PackageRequireLicenseAcceptance | Ein Boolescher Wert, der angibt, ob der Client den Verbraucher dazu auffordern muss, die Paketlizenz vor der Installation des Pakets zu akzeptieren. Der Standardwert ist `false`. |
| DevelopmentDependency | Ein boolescher Wert, der angibt, ob das Paket mit einer Abhängigkeit markiert werden soll, die nur für die Entwicklung gilt, wodurch vermieden wird, dass das Paket als Abhängigkeit in andere Pakete eingefügt wird. Mit `PackageReference` (nuget 4.8 und höher) bedeutet dieses Flag auch, dass Kompilierzeit Ressourcen von der Kompilierung ausgeschlossen werden. Weitere Informationen finden Sie unter [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference) (DevelopmentDependency-Unterstützung für PackageReference). |
| PackageLicenseExpression | Ein [spdx-Lizenz Bezeichner](https://spdx.org/licenses/) oder-Ausdruck, z `Apache-2.0` . b.. Weitere Informationen finden Sie unter [packen eines Lizenz Ausdrucks oder einer Lizenzdatei](#packing-a-license-expression-or-a-license-file). |
| PackageLicenseFile | Der Pfad zu einer Lizenzdatei innerhalb des Pakets, wenn Sie eine benutzerdefinierte Lizenz oder eine Lizenz verwenden, der kein spdx-Bezeichner zugewiesen wurde. |
| PackageLicenseUrl | `PackageLicenseUrl` ist veraltet. Verwenden Sie stattdessen `PackageLicenseExpression` oder `PackageLicenseFile`. |
| PackageProjectUrl | |
| PackageIcon | Gibt den Paket Symbol Pfad relativ zum Stamm des Pakets an. Weitere Informationen finden Sie unter [Packen einer Symbolbild Datei](#packing-an-icon-image-file). |
| PackageReleaseNotes| Anmerkungen zu diesem Paket. |
| PackageTags | Eine durch Semikolons getrennte Liste von Tags, die das Paket festlegt. |
| PackageOutputPath | Bestimmt den Ausgabepfad, in dem das gepackte Paket abgelegt wird. Der Standardwert ist `$(OutputPath)`. |
| IncludeSymbols | Dieser Boolesche Wert gibt an, ob das Paket ein zusätzliches Symbolpaket erstellen soll, wenn das Projekt verpackt wird. Das Format des Symbolpakets wird durch die Eigenschaft `SymbolPackageFormat` gesteuert. Weitere Informationen finden Sie unter [includesymbols](#includesymbols). |
| IncludeSource | Dieser Boolesche Wert gibt an, ob der Packprozess ein Quellpaket erstellen sollte. Das Quellpaket enthält den Quellcode der Bibliothek sowie die PDB-Dateien. Quelldateien werden im `src/ProjectName`-Verzeichnis in der resultierenden Paketdatei gespeichert. Weitere Informationen finden Sie unter [includesource](#includesource). |
| PackageTypes
| IsTool | Gibt an, ob alle Ausgabedateien in den *Tools*-Ordner anstelle des *Lib*-Ordners kopiert werden. Weitere Informationen finden Sie unter [ihocker](#istool). |
| RepositoryUrl | Die Repository-URL, die zum Klonen oder Abrufen von Quellcode verwendet wird. Beispiel: *https://github.com/NuGet/NuGet.Client.git* . |
| RepositoryType | Der Repository-Typ. Beispiele: `git` (Standard), `tfs` . |
| RepositoryBranch | Optionale Informationen zum Repository-Branch. `RepositoryUrl` muss ebenfalls angegeben werden, damit diese Eigenschaft einbezogen wird. Beispiel: *Master* (nuget 4.7.0 +). |
| RepositoryCommit | Optionaler Repositorycommit oder ein Changeset, um anzugeben, für welches Quellpaket die Erstellung erfolgt ist. `RepositoryUrl` muss ebenfalls angegeben werden, damit diese Eigenschaft einbezogen wird. Beispiel: *0e4d1b598f 350 b3dc675018d539114d1328189ef* (nuget 4.7.0 +). |
| SymbolPackageFormat | Gibt das Format des Symbolpakets an. Wenn "Symbols. nupkg" angezeigt wird, wird ein Legacy Symbols-Paket mit der Erweiterung " *. Symbols. nupkg* " erstellt, die pdsb, DLLs und andere Ausgabedateien enthält. Wenn "schnupkg" angezeigt wird, wird ein snupkg-Symbol Paket erstellt, das die portablen pdsb enthält. Der Standardwert ist "Symbols. nupkg". |
| NoPackageAnalysis | Gibt an, dass `pack` nach der Erstellung des Pakets keine Paket Analyse ausführen soll. |
| MinClientVersion | Gibt die minimale Version des NuGet-Clients an, der dieses Paket installieren kann. Dies wird von nuget.exe und dem Paket-Manager von Visual Studio erzwungen. |
| IncludeBuildOutput | Dieser Boolesche Wert gibt an, ob die Buildausgabeassemblys in die *NUPKG*-Datei gepackt werden sollen oder nicht. |
| IncludeContentInPack | Dieser boolesche Wert gibt an, ob Elemente, die einen Typ haben, `Content` automatisch in das resultierende Paket eingefügt werden. Der Standardwert ist `true`. |
| BuildOutputTargetFolder | Gibt den Ordner an, in dem die Ausgabeassemblys abgelegt werden. Die Ausgabeassemblys (und andere Ausgabedateien) werden in ihre jeweiligen Frameworkordner kopiert. Weitere Informationen finden Sie unter [Ausgabeassemblys](#output-assemblies). |
| ContentTargetFolders | Gibt den Standard Speicherort an, an dem alle Inhalts Dateien weitergeleitet werden sollen, wenn `PackagePath` für Sie nicht angegeben ist. Der Standardwert ist „content;contentFiles“. Weitere Informationen finden Sie unter [Inhalt in ein Paket einschließen](#including-content-in-a-package). |
| NuspecFile | Relativer oder absoluter Pfad zur *.nuspec*-Datei, die für die Komprimierung verwendet wird. Wenn dieser Wert angegeben wird, wird er **ausschließlich** zum Verpacken von Informationen verwendet, und alle Informationen in den Projekten werden nicht verwendet. Weitere Informationen finden Sie unter [Verpacken mithilfe einer nuspec](#packing-using-a-nuspec)-Datei. |
| NuspecBasePath | Der Basispfad für die *.nuspec*-Datei. Weitere Informationen finden Sie unter [Verpacken mithilfe einer nuspec](#packing-using-a-nuspec)-Datei. |
| NuspecProperties | Durch Semikolons getrennte Liste der Schlüssel = Wertpaare. Weitere Informationen finden Sie unter [Verpacken mithilfe einer nuspec](#packing-using-a-nuspec)-Datei. |

## <a name="pack-scenarios"></a>Pack-Szenarios

### <a name="suppress-dependencies"></a>Abhängigkeiten unterdrücken

Um Paketabhängigkeiten aus dem generierten nuget-Paket zu unterdrücken, legen `SuppressDependenciesWhenPacking` Sie auf fest `true` . Dadurch können alle Abhängigkeiten von der generierten nupkg-Datei übersprungen werden.

### <a name="packageiconurl"></a>PackageIconUrl

`PackageIconUrl` wird zugunsten der-Eigenschaft als veraltet markiert [`PackageIcon`](#packageicon) . Ab nuget 5,3 und Visual Studio 2019 Version 16,3 wird `pack` die [NU5048](./errors-and-warnings/nu5048.md) -Warnung ausgelöst, wenn die Paket Metadaten nur angeben `PackageIconUrl` .

### <a name="packageicon"></a>PackageIcon

> [!Tip]
> Um die Abwärtskompatibilität mit Clients und Quellen aufrechtzuerhalten, die noch nicht unterstützt `PackageIcon` werden, geben Sie sowohl `PackageIcon` als auch an `PackageIconUrl` . Visual Studio unterstützt Pakete, die `PackageIcon` aus einer Ordner basierten Quelle stammen.

#### <a name="packing-an-icon-image-file"></a>Packen einer Symbolbild Datei

Beim Packen einer Symbolbild Datei verwenden `PackageIcon` Sie die-Eigenschaft, um den Symbol Datei Pfad relativ zum Stamm des Pakets anzugeben. Stellen Sie außerdem sicher, dass die Datei im Paket enthalten ist. Die Größe der Bild Datei ist auf 1 MB beschränkt. Unterstützte Dateiformate sind JPEG und PNG. Wir empfehlen eine Bildauflösung von 128 x 128.

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

Wenn Sie einen Lizenz Ausdruck verwenden, verwenden Sie die- `PackageLicenseExpression` Eigenschaft. Ein Beispiel finden Sie unter [Beispiel für einen Lizenz Ausdruck](https://github.com/NuGet/Samples/tree/master/PackageLicenseExpressionExample).

```xml
<PropertyGroup>
    <PackageLicenseExpression>MIT</PackageLicenseExpression>
</PropertyGroup>
```

Weitere Informationen zu Lizenz Ausdrücken und Lizenzen, die von NuGet.org akzeptiert werden, finden Sie unter [Lizenz Metadaten](nuspec.md#license).

Verwenden Sie beim Verpacken einer Lizenzdatei `PackageLicenseFile` die-Eigenschaft, um den Paketpfad relativ zum Stamm des Pakets anzugeben. Stellen Sie außerdem sicher, dass die Datei im Paket enthalten ist. Zum Beispiel:

```xml
<PropertyGroup>
    <PackageLicenseFile>LICENSE.txt</PackageLicenseFile>
</PropertyGroup>

<ItemGroup>
    <None Include="licenses\LICENSE.txt" Pack="true" PackagePath=""/>
</ItemGroup>
```

Ein Beispiel finden Sie unter [Beispiel für eine Lizenzdatei](https://github.com/NuGet/Samples/tree/master/PackageLicenseFileExample).

> [!NOTE]
> Nur eine von `PackageLicenseExpression` , `PackageLicenseFile` und `PackageLicenseUrl` kann gleichzeitig angegeben werden.

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
| Restoreueinstaticgraphevaluation | Ein Opt-in-Switch zur Verwendung statischer Graph-MSBuild-Auswertung anstelle der Standard Auswertung. Die statische Graph-Auswertung ist ein experimentelles Feature, das für große Repositorys und Lösungen erheblich schneller ist. |

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

### <a name="restoring-with-msbuild-static-graph-evaluation"></a>Wiederherstellen mit der MSBuild static Graph-Auswertung

> [!NOTE]
> Mit MSBuild 16,6 und höher hat nuget ein experimentelles Feature hinzugefügt, um die statische Graph-Auswertung von der Befehlszeile aus zu verwenden, die die Wiederherstellungszeit für große Depots erheblich verbessert.

```cli
msbuild -t:restore -p:RestoreUseStaticGraphEvaluation=true
```

Alternativ können Sie Sie aktivieren, indem Sie die-Eigenschaft in "Directory. Build.-Eigenschaften" festlegen.

```xml
<Project>
  <PropertyGroup>
    <RestoreUseStaticGraphEvaluation>true</RestoreUseStaticGraphEvaluation>
  </PropertyGroup>
</Project>
```

> [!NOTE]
> Ab Visual Studio 2019. x und nuget 5. x gilt dieses Feature als experimentell und als Opt-in. Unter [nuget/Home # 9803](https://github.com/NuGet/Home/issues/9803) finden Sie ausführliche Informationen dazu, wann dieses Feature standardmäßig aktiviert wird.

Bei der statischen Graph-Wiederherstellung wird der MSBuild-Teil der Wiederherstellung, das Lesen und Auswerten des Projekts, aber nicht der Wiederherstellungs Algorithmus geändert. Der Wiederherstellungs Algorithmus ist in allen nuget-Tools (NuGet.exe, MSBuild.exe, dotnet.exe und Visual Studio) identisch.

In sehr wenigen Szenarios kann sich die statische Graph-Wiederherstellung anders als die aktuelle Wiederherstellung Verhalten, und bestimmte deklarierte packagereferences oder ProjectReferences fehlen möglicherweise.

Um Ihre Meinung als einmalige Überprüfung beim Migrieren zur statischen Graph-Wiederherstellung zu vereinfachen, sollten Sie Folgendes ausführen:

```cli
msbuild.exe -t:restore -p:RestoreUseStaticGraphEvaluation
msbuild.exe -t:restore
```

Nuget sollte *keine* Änderungen melden. Wenn eine Abweichung angezeigt wird, melden Sie ein Problem bei [nuget/Home](https://github.com/nuget/home/issues/new).

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
