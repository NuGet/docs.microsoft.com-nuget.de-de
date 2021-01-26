---
title: Befehl "nuget CLI Pack"
description: Referenz für den nuget.exe Pack-Befehl
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: e2906d53119cb8c922df7d177cd686836ac50a5a
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780039"
---
# <a name="pack-command-nuget-cli"></a><span data-ttu-id="915e0-103">Pack-Befehl (nuget-CLI)</span><span class="sxs-lookup"><span data-stu-id="915e0-103">pack command (NuGet CLI)</span></span>

<span data-ttu-id="915e0-104">**Gilt für: von** der Paket Erstellung &bullet; **unterstützte Versionen:** 2.7 +</span><span class="sxs-lookup"><span data-stu-id="915e0-104">**Applies to:** package creation &bullet; **Supported versions:** 2.7+</span></span>

<span data-ttu-id="915e0-105">Erstellt ein nuget-Paket auf der Grundlage der angegebenen [. nuspec](../nuspec.md) -oder Projektdatei.</span><span class="sxs-lookup"><span data-stu-id="915e0-105">Creates a NuGet package based on the specified [.nuspec](../nuspec.md) or project file.</span></span> <span data-ttu-id="915e0-106">Der `dotnet pack` -Befehl (siehe [dotnet-Befehle](../dotnet-Commands.md)) und `msbuild -t:pack` (siehe [MSBuild-Ziele](../msbuild-targets.md)) können als Alternativen verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="915e0-106">The `dotnet pack` command (see [dotnet Commands](../dotnet-Commands.md)) and `msbuild -t:pack` (see [MSBuild targets](../msbuild-targets.md)) may be used as alternates.</span></span>

> [!Important]
> <span data-ttu-id="915e0-107">Verwenden Sie [`dotnet pack`](../dotnet-Commands.md) oder [`msbuild -t:pack`](../msbuild-targets.md) für [packagereferenzierungsbasierte](../../consume-packages/package-references-in-project-files.md) Projekte.</span><span class="sxs-lookup"><span data-stu-id="915e0-107">Use [`dotnet pack`](../dotnet-Commands.md) or [`msbuild -t:pack`](../msbuild-targets.md) for [PackageReference](../../consume-packages/package-references-in-project-files.md) based projects.</span></span>
> <span data-ttu-id="915e0-108">Unter Mono wird das Erstellen eines Pakets aus einer Projektdatei nicht unterstützt.</span><span class="sxs-lookup"><span data-stu-id="915e0-108">Under Mono, creating a package from a project file is not supported.</span></span> <span data-ttu-id="915e0-109">Außerdem müssen Sie nicht lokale Pfade in der `.nuspec` Datei an Pfade im Unix-Stil anpassen, da nuget.exe keine Windows-Pfadnamen selbst konvertiert.</span><span class="sxs-lookup"><span data-stu-id="915e0-109">You also need to adjust non-local paths in the `.nuspec` file to Unix-style paths, as nuget.exe doesn't convert Windows pathnames itself.</span></span>

## <a name="usage"></a><span data-ttu-id="915e0-110">Verwendung</span><span class="sxs-lookup"><span data-stu-id="915e0-110">Usage</span></span>

```cli
nuget pack <nuspecPath | projectPath> [options] [-Properties ...]
```

<span data-ttu-id="915e0-111">dabei `<nuspecPath>` `<projectPath>` Geben Sie die-oder- `.nuspec` Projektdatei an.</span><span class="sxs-lookup"><span data-stu-id="915e0-111">where `<nuspecPath>` and `<projectPath>` specify the `.nuspec` or project file, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="915e0-112">Optionen</span><span class="sxs-lookup"><span data-stu-id="915e0-112">Options</span></span>
- **`-BasePath`**

   <span data-ttu-id="915e0-113">Legt den Basispfad der in der [nuspec](../nuspec.md) -Datei definierten Dateien fest.</span><span class="sxs-lookup"><span data-stu-id="915e0-113">Sets the base path of the files defined in the [.nuspec](../nuspec.md) file.</span></span>

- **`-Build`**

  <span data-ttu-id="915e0-114">Gibt an, dass das Projekt erstellt werden soll, bevor das Paket erstellt wird.</span><span class="sxs-lookup"><span data-stu-id="915e0-114">Specifies that the project should be built before building the package.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="915e0-115">Die anzuwendende nuget-Konfigurationsdatei.</span><span class="sxs-lookup"><span data-stu-id="915e0-115">The NuGet configuration file to apply.</span></span> <span data-ttu-id="915e0-116">Wenn nichts angegeben ist, `%AppData%\NuGet\NuGet.Config` wird (Windows) `~/.nuget/NuGet/NuGet.Config` oder `~/.config/NuGet/NuGet.Config` (Mac/Linux) verwendet.</span><span class="sxs-lookup"><span data-stu-id="915e0-116">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-Exclude`**

  <span data-ttu-id="915e0-117">Gibt ein oder mehrere Platzhalter Muster an, die beim Erstellen eines Pakets ausgeschlossen werden sollen.</span><span class="sxs-lookup"><span data-stu-id="915e0-117">Specifies one or more wildcard patterns to exclude when creating a package.</span></span> <span data-ttu-id="915e0-118">Wenn Sie mehr als ein Muster angeben möchten, wiederholen Sie das Flag-Exclude.</span><span class="sxs-lookup"><span data-stu-id="915e0-118">To specify more than one pattern, repeat the -Exclude flag.</span></span> <span data-ttu-id="915e0-119">Ein Beispiel sehen Sie unten.</span><span class="sxs-lookup"><span data-stu-id="915e0-119">See example below.</span></span>

- **`-ExcludeEmptyDirectories`**

  <span data-ttu-id="915e0-120">Verhindert die Einbindung leerer Verzeichnisse beim Paket Erstellung.</span><span class="sxs-lookup"><span data-stu-id="915e0-120">Prevents inclusion of empty directories when building the package.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="915e0-121">*(3.5* und höher) Erzwingt das Ausführen von nuget.exe mit einer invarianten, englischen Kultur.</span><span class="sxs-lookup"><span data-stu-id="915e0-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="915e0-122">Zeigt Hilfe Informationen für den Befehl an.</span><span class="sxs-lookup"><span data-stu-id="915e0-122">Displays help information for the command.</span></span>

- **`-IncludeReferencedProjects`**

  <span data-ttu-id="915e0-123">Gibt an, dass das integrierte Paket referenzierte Projekte entweder als Abhängigkeiten oder als Teil des Pakets einschließen soll.</span><span class="sxs-lookup"><span data-stu-id="915e0-123">Indicates that the built package should include referenced projects either as dependencies or as part of the package.</span></span> <span data-ttu-id="915e0-124">Wenn ein referenziertes Projekt über eine entsprechende Datei verfügt, `.nuspec` die den gleichen Namen wie das Projekt hat, wird dieses referenzierte Projekt als Abhängigkeit hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="915e0-124">If a referenced project has a corresponding `.nuspec` file that has the same name as the project, then that referenced project is added as a dependency.</span></span> <span data-ttu-id="915e0-125">Andernfalls wird das Projekt, auf das verwiesen wird, als Teil des Pakets hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="915e0-125">Otherwise, the referenced project is added as part of the package.</span></span>

- **`-InstallPackageToOutputPath`**

  <span data-ttu-id="915e0-126">Geben Sie an, ob der Befehl das Paketausgabe Verzeichnis für die Unterstützung von Freigabe als Feed vorbereiten soll.</span><span class="sxs-lookup"><span data-stu-id="915e0-126">Specify if the command should prepare the package output directory to support share as feed.</span></span>

- **`-MinClientVersion`**

  <span data-ttu-id="915e0-127">Legen Sie das *minclientversion* -Attribut für das erstellte Paket fest.</span><span class="sxs-lookup"><span data-stu-id="915e0-127">Set the *minClientVersion* attribute for the created package.</span></span> <span data-ttu-id="915e0-128">Durch diesen Wert wird der Wert des vorhandenen *minclientversion* -Attributs (sofern vorhanden) in der Datei überschrieben `.nuspec` .</span><span class="sxs-lookup"><span data-stu-id="915e0-128">This value will override the value of the existing *minClientVersion* attribute (if any) in the `.nuspec` file.</span></span>

- **`-MSBuildPath`**

  <span data-ttu-id="915e0-129">*(4.0* und höher) Gibt den Pfad von MSBuild an, der mit dem Befehl verwendet werden soll, und hat Vorrang vor `-MSBuildVersion` .</span><span class="sxs-lookup"><span data-stu-id="915e0-129">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span>

- **`-MSBuildVersion`**

  <span data-ttu-id="915e0-130">*(3.2 +)* Gibt die Version von MSBuild an, die mit diesem Befehl verwendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="915e0-130">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="915e0-131">Unterstützte Werte sind 4, 12, 14, 15,1, 15,3, 15,4, 15,5, 15,6, 15,7, 15,8, 15,9.</span><span class="sxs-lookup"><span data-stu-id="915e0-131">Supported values are 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9.</span></span> <span data-ttu-id="915e0-132">Standardmäßig wird der MSBuild in Ihrem Pfad ausgewählt; andernfalls wird standardmäßig die höchste installierte Version von MSBuild verwendet.</span><span class="sxs-lookup"><span data-stu-id="915e0-132">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span>

- **`-NoDefaultExcludes`**

  <span data-ttu-id="915e0-133">Verhindert, dass nuget-Paketdateien und-Dateien und-Ordner mit einem Punkt beginnen, `.svn` z `.gitignore` . b. und.</span><span class="sxs-lookup"><span data-stu-id="915e0-133">Prevents default exclusion of NuGet package files and files and folders starting with a dot, such as `.svn` and `.gitignore`.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="915e0-134">Unterdrückt Eingabe Aufforderungen für Benutzereingaben oder Bestätigungen.</span><span class="sxs-lookup"><span data-stu-id="915e0-134">Suppresses prompts for user input or confirmations.</span></span>

- **`-NoPackageAnalysis`**

  <span data-ttu-id="915e0-135">Gibt an, dass der Packvorgang keine Paketanalyse nach dem Erstellen des Pakets ausführen sollte.</span><span class="sxs-lookup"><span data-stu-id="915e0-135">Specifies that pack should not run package analysis after building the package.</span></span>

- **`-OutputDirectory`**

  <span data-ttu-id="915e0-136">Gibt den Ordner an, in dem das erstellte Paket gespeichert ist.</span><span class="sxs-lookup"><span data-stu-id="915e0-136">Specifies the folder in which the created package is stored.</span></span> <span data-ttu-id="915e0-137">Wenn kein Ordner angegeben wird, wird der aktuelle Ordner verwendet.</span><span class="sxs-lookup"><span data-stu-id="915e0-137">If no folder is specified, the current folder is used.</span></span>

- **`-OutputFileNamesWithoutVersion`**

  <span data-ttu-id="915e0-138">Geben Sie an, ob der Paketausgabe Name mit dem Befehl ohne die Version vorbereitet werden soll.</span><span class="sxs-lookup"><span data-stu-id="915e0-138">Specify if the command should prepare the package output name without the version.</span></span>

- **`-PackagesDirectory`**

  <span data-ttu-id="915e0-139">Gibt den Ordner "Packages" an.</span><span class="sxs-lookup"><span data-stu-id="915e0-139">Specifies the packages folder.</span></span>

- **`-p|-Properties`**

  <span data-ttu-id="915e0-140">Sollte zuletzt in der Befehlszeile nach anderen Optionen angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="915e0-140">Should appear last on the command line after other options.</span></span> <span data-ttu-id="915e0-141">Gibt eine Liste von Eigenschaften an, die Werte in der Projektdatei überschreiben. Weitere Informationen finden Sie unter [allgemeine MSBuild-Projekteigenschaften für Eigenschaften](/visualstudio/msbuild/common-msbuild-project-properties) Namen.</span><span class="sxs-lookup"><span data-stu-id="915e0-141">Specifies a list of properties that override values in the project file; see [Common MSBuild Project Properties](/visualstudio/msbuild/common-msbuild-project-properties) for property names.</span></span> <span data-ttu-id="915e0-142">Das hier angegebene Properties-Argument ist eine Liste von Token = Wert-Paaren, die durch Semikolons getrennt sind, wobei jedes Vorkommen von `$token$` in der `.nuspec` Datei durch den angegebenen Wert ersetzt wird.</span><span class="sxs-lookup"><span data-stu-id="915e0-142">The Properties argument here is a list of token=value pairs, separated by semicolons, where each occurrence of `$token$` in the `.nuspec` file will be replaced with the given value.</span></span> <span data-ttu-id="915e0-143">Werte können Zeichen folgen in Anführungszeichen sein.</span><span class="sxs-lookup"><span data-stu-id="915e0-143">Values can be strings in quotation marks.</span></span> <span data-ttu-id="915e0-144">Beachten Sie, dass für die Eigenschaft "Configuration" der Standardwert "Debug" lautet.</span><span class="sxs-lookup"><span data-stu-id="915e0-144">Note that for the "Configuration" property, the default is "Debug".</span></span> <span data-ttu-id="915e0-145">Verwenden Sie, um zu einer Releasekonfiguration zu wechseln `-Properties Configuration=Release` .</span><span class="sxs-lookup"><span data-stu-id="915e0-145">To change to a Release configuration, use `-Properties Configuration=Release`.</span></span> <span data-ttu-id="915e0-146">**Im allgemeinen** sollten Eigenschaften identisch sein, die während des entsprechenden Projektbuilds verwendet wurden, um potenziell merkwürdiges Verhalten zu vermeiden.</span><span class="sxs-lookup"><span data-stu-id="915e0-146">**In general**, Properties should be the same that were used during the corresponding project build, in order to avoid potentially strange behavior.</span></span>

- **`-SolutionDirectory`**

  <span data-ttu-id="915e0-147">Gibt das Projektmappenverzeichnis an.</span><span class="sxs-lookup"><span data-stu-id="915e0-147">Specifies the solution directory.</span></span>

- **`-Suffix`**

  <span data-ttu-id="915e0-148">*(3.4.4 +)* Fügt ein Suffix an die intern generierte Versionsnummer an, die in der Regel zum Anhängen von Builds oder anderen vorab-releasebezeichnerids verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="915e0-148">*(3.4.4+)* Appends a suffix to the internally generated version number, typically used for appending build or other pre-release identifiers.</span></span> <span data-ttu-id="915e0-149">Wenn Sie z. b. verwenden, `-suffix nightly` wird ein Paket mit einer Versionsnummer wie erstellt `1.2.3-nightly` .</span><span class="sxs-lookup"><span data-stu-id="915e0-149">For example, using `-suffix nightly` will create a package with a version number like `1.2.3-nightly`.</span></span> <span data-ttu-id="915e0-150">Suffixe müssen mit einem Buchstaben beginnen, um Warnungen, Fehler und mögliche Inkompatibilitäten mit verschiedenen Versionen von nuget und dem nuget-Paket-Manager zu vermeiden.</span><span class="sxs-lookup"><span data-stu-id="915e0-150">Suffixes must start with a letter to avoid warnings, errors, and potential incompatibilities with different versions of NuGet and the NuGet Package Manager.</span></span>

- **`-SymbolPackageFormat`**

  <span data-ttu-id="915e0-151">Beim Erstellen eines Symbols-Pakets ermöglicht die Auswahl zwischen dem `snupkg` -Format und dem- `symbols.nupkg` Format.</span><span class="sxs-lookup"><span data-stu-id="915e0-151">When creating a symbols package, allows to choose between the `snupkg` and `symbols.nupkg` format.</span></span>

- **`-Symbols`**

  <span data-ttu-id="915e0-152">Gibt an, dass das Paketquellen und Symbole enthält.</span><span class="sxs-lookup"><span data-stu-id="915e0-152">Specifies that the package contains sources and symbols.</span></span> <span data-ttu-id="915e0-153">Bei Verwendung mit einer- `.nuspec` Datei werden dadurch eine reguläre nuget-Paketdatei und das entsprechende Symbol Paket erstellt.</span><span class="sxs-lookup"><span data-stu-id="915e0-153">When used with a `.nuspec` file, this creates a regular NuGet package file and the corresponding symbols package.</span></span> <span data-ttu-id="915e0-154">Standardmäßig wird ein [Legacy Symbol Paket](../../create-packages/Symbol-Packages.md)erstellt.</span><span class="sxs-lookup"><span data-stu-id="915e0-154">By default it creates a [legacy symbol package](../../create-packages/Symbol-Packages.md).</span></span> <span data-ttu-id="915e0-155">Das neue empfohlene Format für Symbolpakete ist „.snupkg“.</span><span class="sxs-lookup"><span data-stu-id="915e0-155">The new recommended format for symbol packages is .snupkg.</span></span> <span data-ttu-id="915e0-156">Weitere Informationen finden Sie unter [Erstellen von Symbolpaketen (.snupkg)](../../create-packages/Symbol-Packages-snupkg.md).</span><span class="sxs-lookup"><span data-stu-id="915e0-156">See [Creating symbol packages (.snupkg)](../../create-packages/Symbol-Packages-snupkg.md).</span></span>

- **`-Tool`**

   <span data-ttu-id="915e0-157">Gibt an, dass die Ausgabedateien des Projekts in den Ordner eingefügt werden sollen `tool` .</span><span class="sxs-lookup"><span data-stu-id="915e0-157">Specifies that the output files of the project should be placed in the `tool` folder.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="915e0-158">Gibt den Umfang der in der Ausgabe angezeigten Details an: `normal` (Standard), `quiet` oder `detailed` .</span><span class="sxs-lookup"><span data-stu-id="915e0-158">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

- **`-Version`**

  <span data-ttu-id="915e0-159">Überschreibt die Versionsnummer der `.nuspec` Datei.</span><span class="sxs-lookup"><span data-stu-id="915e0-159">Overrides the version number from the `.nuspec` file.</span></span>

<span data-ttu-id="915e0-160">Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="915e0-160">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="excluding-development-dependencies"></a><span data-ttu-id="915e0-161">Ausschließen von Entwicklungs Abhängigkeiten</span><span class="sxs-lookup"><span data-stu-id="915e0-161">Excluding development dependencies</span></span>

<span data-ttu-id="915e0-162">Einige nuget-Pakete sind nützlich als Entwicklungs Abhängigkeiten, die Sie beim Erstellen Ihrer eigenen Bibliothek unterstützen, aber nicht unbedingt als tatsächliche Paketabhängigkeiten benötigt werden.</span><span class="sxs-lookup"><span data-stu-id="915e0-162">Some NuGet packages are useful as development dependencies, which help you author your own library, but aren't necessarily needed as actual package dependencies.</span></span>

<span data-ttu-id="915e0-163">Der `pack` Befehl ignoriert `package` Einträge in `packages.config` , bei denen das- `developmentDependency` Attribut auf festgelegt ist `true` .</span><span class="sxs-lookup"><span data-stu-id="915e0-163">The `pack` command will ignore `package` entries in `packages.config` that have the `developmentDependency` attribute set to `true`.</span></span> <span data-ttu-id="915e0-164">Diese Einträge werden nicht als Abhängigkeiten in das erstellte Paket einbezogen.</span><span class="sxs-lookup"><span data-stu-id="915e0-164">These entries will not be include as a dependencies in the created package.</span></span>

<span data-ttu-id="915e0-165">Sehen Sie sich beispielsweise die folgende `packages.config` Datei im Quell Projekt an:</span><span class="sxs-lookup"><span data-stu-id="915e0-165">For example, consider the following `packages.config` file in the source project:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="jQuery" version="1.5.2" />
    <package id="netfx-Guard" version="1.3.3.2" developmentDependency="true" />
    <package id="microsoft-web-helpers" version="1.15" />
</packages>
```

<span data-ttu-id="915e0-166">Für dieses Projekt hat das von erstellte Paket `nuget pack` eine Abhängigkeit von und, `jQuery` `microsoft-web-helpers` aber nicht `netfx-Guard` .</span><span class="sxs-lookup"><span data-stu-id="915e0-166">For this project, the package created by `nuget pack` will have a dependency on `jQuery` and `microsoft-web-helpers` but not `netfx-Guard`.</span></span>

## <a name="suppressing-pack-warnings"></a><span data-ttu-id="915e0-167">Unterdrücken von Paket Warnungen</span><span class="sxs-lookup"><span data-stu-id="915e0-167">Suppressing pack warnings</span></span>

<span data-ttu-id="915e0-168">Es wird empfohlen, dass Sie alle nuget-Warnungen während der Paket Vorgänge auflösen, in bestimmten Situationen, in denen Sie unterdrückt werden.</span><span class="sxs-lookup"><span data-stu-id="915e0-168">While it is recommended that you resolve all NuGet warnings during your pack operations, in certain situations suppressing them is warranted.</span></span>

<span data-ttu-id="915e0-169">Dies kann auf folgende Weise erreicht werden:</span><span class="sxs-lookup"><span data-stu-id="915e0-169">You can achieve that in the following way:</span></span> 

> <span data-ttu-id="915e0-170">nuget.exe Pack Package. nuspec-Properties nowarn = NU5104</span><span class="sxs-lookup"><span data-stu-id="915e0-170">nuget.exe pack package.nuspec -Properties NoWarn=NU5104</span></span>

## <a name="examples"></a><span data-ttu-id="915e0-171">Beispiele</span><span class="sxs-lookup"><span data-stu-id="915e0-171">Examples</span></span>

```cli
nuget pack

nuget pack foo.nuspec

nuget pack foo.csproj

nuget pack foo.csproj -Properties Configuration=Release

nuget pack foo.csproj -Build -Symbols -Properties owners=janedoe,xiaop;version="1.0.5"

# Create a package from project foo.csproj, using MSBuild version 12 to build the project
nuget pack foo.csproj -Build -Symbols -MSBuildVersion 12 -Properties owners=janedoe,xiaop;version="1.0.5"

# Create a package from project foo.nuspec and the corresponding symbol package using the new recommended format .snupkg
nuget pack foo.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack foo.nuspec -Version 2.1.0

nuget pack foo.nuspec -Version 1.0.0 -MinClientVersion 2.5

nuget pack Package.nuspec -exclude "*.exe" -exclude "*.bat"
```
