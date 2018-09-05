---
title: NuGet-CLI-Befehl "Pack"
description: Referenz für die nuget.exe-Pack-Befehl
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: db236b0eaac34ca9f6f67fd15ca3ad6884f6a18d
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549095"
---
# <a name="pack-command-nuget-cli"></a><span data-ttu-id="675c8-103">Der Befehl „pack“ (NuGet-CLI)</span><span class="sxs-lookup"><span data-stu-id="675c8-103">pack command (NuGet CLI)</span></span>

<span data-ttu-id="675c8-104">**Gilt für:** paketerstellung &bullet; **unterstützte Versionen:** 2.7 und höher</span><span class="sxs-lookup"><span data-stu-id="675c8-104">**Applies to:** package creation &bullet; **Supported versions:** 2.7+</span></span>

<span data-ttu-id="675c8-105">Erstellt ein NuGet-Paket, das auf der Grundlage der angegebenen `.nuspec` oder einer Projektdatei.</span><span class="sxs-lookup"><span data-stu-id="675c8-105">Creates a NuGet package based on the specified `.nuspec` or project file.</span></span> <span data-ttu-id="675c8-106">Die `dotnet pack` Befehl (finden Sie unter [Dotnet-Befehle](dotnet-Commands.md)) und `msbuild /t:pack` (finden Sie unter [MSBuild-Ziele](../reference/msbuild-targets.md)) als alternativen verwendet werden kann.</span><span class="sxs-lookup"><span data-stu-id="675c8-106">The `dotnet pack` command (see [dotnet Commands](dotnet-Commands.md)) and `msbuild /t:pack` (see [MSBuild targets](../reference/msbuild-targets.md)) may be used as alternates.</span></span>

> [!Important]
> <span data-ttu-id="675c8-107">Unter Mono wird das Erstellen eines Pakets aus einer Projektdatei nicht unterstützt.</span><span class="sxs-lookup"><span data-stu-id="675c8-107">Under Mono, creating a package from a project file is not supported.</span></span> <span data-ttu-id="675c8-108">Müssen Sie auch anpassen, nicht lokale Pfade in der `.nuspec` Datei auf Unix-Format-Pfade, wie Windows-Pfadnamen selbst nuget.exe konvertiert und deswegen nicht.</span><span class="sxs-lookup"><span data-stu-id="675c8-108">You also need to adjust non-local paths in the `.nuspec` file to Unix-style paths, as nuget.exe doesn't convert Windows pathnames itself.</span></span>

## <a name="usage"></a><span data-ttu-id="675c8-109">Verwendung</span><span class="sxs-lookup"><span data-stu-id="675c8-109">Usage</span></span>

```cli
nuget pack <nuspecPath | projectPath> [options] [-Properties ...]
```

<span data-ttu-id="675c8-110">wobei `<nuspecPath>` und `<projectPath>` angeben der `.nuspec` oder Projektdatei bzw.</span><span class="sxs-lookup"><span data-stu-id="675c8-110">where `<nuspecPath>` and `<projectPath>` specify the `.nuspec` or project file, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="675c8-111">Optionen</span><span class="sxs-lookup"><span data-stu-id="675c8-111">Options</span></span>

| <span data-ttu-id="675c8-112">Option</span><span class="sxs-lookup"><span data-stu-id="675c8-112">Option</span></span> | <span data-ttu-id="675c8-113">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="675c8-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="675c8-114">BasePath</span><span class="sxs-lookup"><span data-stu-id="675c8-114">BasePath</span></span> | <span data-ttu-id="675c8-115">Legt den Basispfad der Dateien in definiert die `.nuspec` Datei.</span><span class="sxs-lookup"><span data-stu-id="675c8-115">Sets the base path of the files defined in the `.nuspec` file.</span></span> |
| <span data-ttu-id="675c8-116">Build</span><span class="sxs-lookup"><span data-stu-id="675c8-116">Build</span></span> | <span data-ttu-id="675c8-117">Gibt an, dass das Projekt erstellt werden soll, bevor Sie das Paket zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="675c8-117">Specifies that the project should be built before building the package.</span></span> |
| <span data-ttu-id="675c8-118">Ausschließen</span><span class="sxs-lookup"><span data-stu-id="675c8-118">Exclude</span></span> | <span data-ttu-id="675c8-119">Gibt einen oder mehrere Platzhaltermuster ausschließen, wenn ein Paket erstellen.</span><span class="sxs-lookup"><span data-stu-id="675c8-119">Specifies one or more wildcard patterns to exclude when creating a package.</span></span> <span data-ttu-id="675c8-120">Um mehr als ein Muster anzugeben, wiederholen Sie den - Flag ausschließen.</span><span class="sxs-lookup"><span data-stu-id="675c8-120">To specify more than one pattern, repeat the -Exclude flag.</span></span> <span data-ttu-id="675c8-121">Siehe Beispiel unten.</span><span class="sxs-lookup"><span data-stu-id="675c8-121">See example below.</span></span> |
| <span data-ttu-id="675c8-122">ExcludeEmptyDirectories</span><span class="sxs-lookup"><span data-stu-id="675c8-122">ExcludeEmptyDirectories</span></span> | <span data-ttu-id="675c8-123">Verhindert den Einschluss leere Verzeichnisse bei der Erstellung des Pakets.</span><span class="sxs-lookup"><span data-stu-id="675c8-123">Prevents inclusion of empty directories when building the package.</span></span> |
| <span data-ttu-id="675c8-124">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="675c8-124">ForceEnglishOutput</span></span> | <span data-ttu-id="675c8-125">*(3.5 und höher)*  Erzwingt nuget.exe über eine invariante Kultur auf Englisch basierenden ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="675c8-125">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="675c8-126">Hilfe</span><span class="sxs-lookup"><span data-stu-id="675c8-126">Help</span></span> | <span data-ttu-id="675c8-127">Zeigt die Informationen für den Befehl Hilfe.</span><span class="sxs-lookup"><span data-stu-id="675c8-127">Displays help information for the command.</span></span> |
| <span data-ttu-id="675c8-128">IncludeReferencedProjects</span><span class="sxs-lookup"><span data-stu-id="675c8-128">IncludeReferencedProjects</span></span> | <span data-ttu-id="675c8-129">Gibt an, dass das erstellte Paket referenzierte Projekte entweder als Abhängigkeiten oder als Teil des Pakets enthalten soll.</span><span class="sxs-lookup"><span data-stu-id="675c8-129">Indicates that the built package should include referenced projects either as dependencies or as part of the package.</span></span> <span data-ttu-id="675c8-130">Wenn ein Referenziertes Projekt ein entsprechendes hat `.nuspec` -Datei mit dem gleichen Namen wie das Projekt, und klicken Sie dann das referenzierte Projekt als Abhängigkeit hinzugefügt wird.</span><span class="sxs-lookup"><span data-stu-id="675c8-130">If a referenced project has a corresponding `.nuspec` file that has the same name as the project, then that referenced project is added as a dependency.</span></span> <span data-ttu-id="675c8-131">Andernfalls wird das referenzierte Projekt als Teil des Pakets hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="675c8-131">Otherwise, the referenced project is added as part of the package.</span></span> |
| <span data-ttu-id="675c8-132">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="675c8-132">MinClientVersion</span></span> | <span data-ttu-id="675c8-133">Legen Sie die *MinClientVersion* -Attribut für das erstellte Paket.</span><span class="sxs-lookup"><span data-stu-id="675c8-133">Set the *minClientVersion* attribute for the created package.</span></span> <span data-ttu-id="675c8-134">Dieser Wert überschreibt den Wert des vorhandenen *MinClientVersion* -Attribut (sofern vorhanden) in der `.nuspec` Datei.</span><span class="sxs-lookup"><span data-stu-id="675c8-134">This value will override the value of the existing *minClientVersion* attribute (if any) in the `.nuspec` file.</span></span> |
| <span data-ttu-id="675c8-135">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="675c8-135">MSBuildPath</span></span> | <span data-ttu-id="675c8-136">*(4.0 und höher)*  Gibt den Pfad des MSBuild für die Verwendung mit dem Befehl vor `-MSBuildVersion`.</span><span class="sxs-lookup"><span data-stu-id="675c8-136">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="675c8-137">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="675c8-137">MSBuildVersion</span></span> | <span data-ttu-id="675c8-138">*(3.2 und höher)*  Gibt die Version von MSBuild mit dem folgenden Befehl verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="675c8-138">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="675c8-139">Unterstützte Werte sind 4, 12, 14, 15.</span><span class="sxs-lookup"><span data-stu-id="675c8-139">Supported values are 4, 12, 14, 15.</span></span> <span data-ttu-id="675c8-140">Standardmäßig die MSBuild in Ihrem Pfad ausgewählt wird, wird standardmäßig andernfalls die neueste installierte Version von MSBuild.</span><span class="sxs-lookup"><span data-stu-id="675c8-140">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="675c8-141">NoDefaultExcludes</span><span class="sxs-lookup"><span data-stu-id="675c8-141">NoDefaultExcludes</span></span> | <span data-ttu-id="675c8-142">Verhindert die Standard-Ausschlussliste von NuGet-Paket-Dateien, Dateien und Ordnern, wie z. B. mit einem Punkt, ab `.svn` und `.gitignore`.</span><span class="sxs-lookup"><span data-stu-id="675c8-142">Prevents default exclusion of NuGet package files and files and folders starting with a dot, such as `.svn` and `.gitignore`.</span></span> |
| <span data-ttu-id="675c8-143">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="675c8-143">NoPackageAnalysis</span></span> | <span data-ttu-id="675c8-144">Gibt an, dass der Packvorgang keine Paketanalyse nach dem Erstellen des Pakets ausführen sollte.</span><span class="sxs-lookup"><span data-stu-id="675c8-144">Specifies that pack should not run package analysis after building the package.</span></span> |
| <span data-ttu-id="675c8-145">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="675c8-145">OutputDirectory</span></span> | <span data-ttu-id="675c8-146">Gibt den Ordner, in dem das erstellte Paket gespeichert ist.</span><span class="sxs-lookup"><span data-stu-id="675c8-146">Specifies the folder in which the created package is stored.</span></span> <span data-ttu-id="675c8-147">Wenn kein Ordner angegeben wird, wird der aktuelle Ordner verwendet.</span><span class="sxs-lookup"><span data-stu-id="675c8-147">If no folder is specified, the current folder is used.</span></span> |
| <span data-ttu-id="675c8-148">Eigenschaften</span><span class="sxs-lookup"><span data-stu-id="675c8-148">Properties</span></span> | <span data-ttu-id="675c8-149">Zuletzt in der Befehlszeile sollten nach der anderen Optionen angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="675c8-149">Should appear last on the command line after other options.</span></span> <span data-ttu-id="675c8-150">Gibt eine Liste der Eigenschaften, die Werte in der Projektdatei überschrieben werden; finden Sie unter [gemeinsame MSBuild-Projekteigenschaften](/visualstudio/msbuild/common-msbuild-project-properties) für Eigenschaftsnamen.</span><span class="sxs-lookup"><span data-stu-id="675c8-150">Specifies a list of properties that override values in the project file; see [Common MSBuild Project Properties](/visualstudio/msbuild/common-msbuild-project-properties) for property names.</span></span> <span data-ttu-id="675c8-151">Hier das Eigenschaften-Argument ist eine Liste von Token = Wert-Paaren, durch Semikolons getrennt, in denen jedes Vorkommen von `$token$` in die `.nuspec` Datei mit dem angegebenen Wert ersetzt werden.</span><span class="sxs-lookup"><span data-stu-id="675c8-151">The Properties argument here is a list of token=value pairs, separated by semicolons, where each occurrence of `$token$` in the `.nuspec` file will be replaced with the given value.</span></span> <span data-ttu-id="675c8-152">Werte können Zeichenfolgen in Anführungszeichen sein.</span><span class="sxs-lookup"><span data-stu-id="675c8-152">Values can be strings in quotation marks.</span></span> <span data-ttu-id="675c8-153">Beachten Sie, dass für die Eigenschaft "Konfiguration" die Standardeinstellung ist "Debug".</span><span class="sxs-lookup"><span data-stu-id="675c8-153">Note that for the "Configuration" property, the default is "Debug".</span></span> <span data-ttu-id="675c8-154">Verwenden Sie zum Ändern zu einer versionskonfiguration `-Properties Configuration=Release`.</span><span class="sxs-lookup"><span data-stu-id="675c8-154">To change to a Release configuration, use `-Properties Configuration=Release`.</span></span> |
| <span data-ttu-id="675c8-155">Suffix</span><span class="sxs-lookup"><span data-stu-id="675c8-155">Suffix</span></span> | <span data-ttu-id="675c8-156">*(3.4.4+)*  Fügt ein Suffix, die intern generierte Versionsnummer, die in der Regel zum Anfügen von Build oder andere Vorabversion-IDs verwendet.</span><span class="sxs-lookup"><span data-stu-id="675c8-156">*(3.4.4+)* Appends a suffix to the internally generated version number, typically used for appending build or other pre-release identifiers.</span></span> <span data-ttu-id="675c8-157">Verwenden Sie beispielsweise `-suffix nightly` erstellt ein Paket mit einer Version Anzahl Like `1.2.3-nightly`.</span><span class="sxs-lookup"><span data-stu-id="675c8-157">For example, using `-suffix nightly` will create a package with a version number like `1.2.3-nightly`.</span></span> <span data-ttu-id="675c8-158">Suffixe müssen mit einem Buchstaben, vermeiden Sie Warnungen, Fehler und mögliche Inkompatibilitäten mit verschiedenen Versionen von NuGet und den NuGet-Paket-Manager starten.</span><span class="sxs-lookup"><span data-stu-id="675c8-158">Suffixes must start with a letter to avoid warnings, errors, and potential incompatibilities with different versions of NuGet and the NuGet Package Manager.</span></span> |
| <span data-ttu-id="675c8-159">Symbole</span><span class="sxs-lookup"><span data-stu-id="675c8-159">Symbols</span></span> | <span data-ttu-id="675c8-160">Gibt an, dass das Paket Quellen und Symbole enthält.</span><span class="sxs-lookup"><span data-stu-id="675c8-160">Specifies that the package contains sources and symbols.</span></span> <span data-ttu-id="675c8-161">Bei Verwendung mit einem `.nuspec` Datei dies eine normale NuGet-Paket-Datei erstellt und das entsprechende Symbolpaket.</span><span class="sxs-lookup"><span data-stu-id="675c8-161">When used with a `.nuspec` file, this creates a regular NuGet package file and the corresponding symbols package.</span></span> |
| <span data-ttu-id="675c8-162">Tool</span><span class="sxs-lookup"><span data-stu-id="675c8-162">Tool</span></span> | <span data-ttu-id="675c8-163">Gibt an, dass die Ausgabedateien des Projekts soll, in platziert werden der `tool` Ordner.</span><span class="sxs-lookup"><span data-stu-id="675c8-163">Specifies that the output files of the project should be placed in the `tool` folder.</span></span> |
| <span data-ttu-id="675c8-164">Ausführlichkeit</span><span class="sxs-lookup"><span data-stu-id="675c8-164">Verbosity</span></span> | <span data-ttu-id="675c8-165">Gibt an, die Anzahl der Details in der Ausgabe angezeigt: *normalen*, *quiet*, *ausführliche*.</span><span class="sxs-lookup"><span data-stu-id="675c8-165">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |
| <span data-ttu-id="675c8-166">Version</span><span class="sxs-lookup"><span data-stu-id="675c8-166">Version</span></span> | <span data-ttu-id="675c8-167">Überschreibt die Version aus der `.nuspec` Datei.</span><span class="sxs-lookup"><span data-stu-id="675c8-167">Overrides the version number from the `.nuspec` file.</span></span> |

<span data-ttu-id="675c8-168">Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="675c8-168">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="excluding-development-dependencies"></a><span data-ttu-id="675c8-169">Ausschließen von entwicklungsabhängigkeiten</span><span class="sxs-lookup"><span data-stu-id="675c8-169">Excluding development dependencies</span></span>

<span data-ttu-id="675c8-170">Einige NuGet-Pakete eignen sich als entwicklungsabhängigkeiten, können Sie Ihre eigene Bibliothek erstellen, aber nicht unbedingt als tatsächliche paketabhängigkeiten benötigt.</span><span class="sxs-lookup"><span data-stu-id="675c8-170">Some NuGet packages are useful as development dependencies, which help you author your own library, but aren't necessarily needed as actual package dependencies.</span></span>

<span data-ttu-id="675c8-171">Die `pack` Befehl ignoriert `package` Einträge im `packages.config` verfügen, die die `developmentDependency` -Attributsatz auf `true`.</span><span class="sxs-lookup"><span data-stu-id="675c8-171">The `pack` command will ignore `package` entries in `packages.config` that have the `developmentDependency` attribute set to `true`.</span></span> <span data-ttu-id="675c8-172">Diese Einträge sind nicht als eine Abhängigkeiten in das erstellte Paket enthalten.</span><span class="sxs-lookup"><span data-stu-id="675c8-172">These entries will not be include as a dependencies in the created package.</span></span>

<span data-ttu-id="675c8-173">Betrachten Sie beispielsweise die folgenden `packages.config` Datei im Source-Projekt:</span><span class="sxs-lookup"><span data-stu-id="675c8-173">For example, consider the following `packages.config` file in the source project:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="jQuery" version="1.5.2" />
    <package id="netfx-Guard" version="1.3.3.2" developmentDependency="true" />
    <package id="microsoft-web-helpers" version="1.15" />
</packages>
```

<span data-ttu-id="675c8-174">Für dieses Projekt das Paket erstellt `nuget pack` hat eine Abhängigkeit auf `jQuery` und `microsoft-web-helpers` , nicht jedoch `netfx-Guard`.</span><span class="sxs-lookup"><span data-stu-id="675c8-174">For this project, the package created by `nuget pack` will have a dependency on `jQuery` and `microsoft-web-helpers` but not `netfx-Guard`.</span></span>

## <a name="examples"></a><span data-ttu-id="675c8-175">Beispiele</span><span class="sxs-lookup"><span data-stu-id="675c8-175">Examples</span></span>

```cli
nuget pack

nuget pack foo.nuspec

nuget pack foo.csproj

nuget pack foo.csproj -Properties Configuration=Release

nuget pack foo.csproj -Build -Symbols -Properties owners=janedoe,xiaop;version="1.0.5"

# Create a package from project foo.csproj, using MSBuild version 12 to build the project
nuget pack foo.csproj -Build -Symbols -MSBuildVersion 12 -Properties owners=janedoe,xiaop;version="1.0.5

nuget pack foo.nuspec -Version 2.1.0

nuget pack foo.nuspec -Version 1.0.0 -MinClientVersion 2.5

nuget pack Package.nuspec -exclude "*.exe" -exclude "*.bat"
```
