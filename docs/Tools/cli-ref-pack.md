---
title: NuGet-CLI-Pack-Befehl | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/08/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 55e9e4d2-8039-4e9b-bdd9-c8b3eb0e894b
description: "Referenz für den nuget.exe-Pack-Befehl"
keywords: NuGet-Pack-Verweis, Pack-Befehl
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 353d5d839d85c04bc315c3a0e9cfe274a361bd15
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/14/2017
---
# <a name="pack-command-nuget-cli"></a><span data-ttu-id="8a5ff-104">Pack-Befehl (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="8a5ff-104">pack command (NuGet CLI)</span></span>

<span data-ttu-id="8a5ff-105">**Gilt für:** Erstellen von Paketen &bullet; **unterstützte Versionen:** 2.7 +</span><span class="sxs-lookup"><span data-stu-id="8a5ff-105">**Applies to:** package creation &bullet; **Supported versions:** 2.7+</span></span>

<span data-ttu-id="8a5ff-106">Erstellt ein NuGet-Paket auf der Grundlage der angegebenen `.nuspec` oder der Projektdatei.</span><span class="sxs-lookup"><span data-stu-id="8a5ff-106">Creates a NuGet package based on the specified `.nuspec` or project file.</span></span> <span data-ttu-id="8a5ff-107">Die `dotnet pack` Befehl (finden Sie unter [Dotnet Befehle](dotnet-Commands.md)) und `msbuild /t:pack` (finden Sie unter [MSBuild-Ziele](../schema/msbuild-targets.md)) als alternativen verwendet werden kann.</span><span class="sxs-lookup"><span data-stu-id="8a5ff-107">The `dotnet pack` command (see [dotnet Commands](dotnet-Commands.md)) and `msbuild /t:pack` (see [MSBuild targets](../schema/msbuild-targets.md)) may be used as alternates.</span></span>

> [!Important]
> <span data-ttu-id="8a5ff-108">Unter Mono wird das Erstellen eines Pakets aus einer Projektdatei nicht unterstützt.</span><span class="sxs-lookup"><span data-stu-id="8a5ff-108">Under Mono, creating a package from a project file is not supported.</span></span> <span data-ttu-id="8a5ff-109">Müssen Sie auch nicht lokale Pfade in Anpassen der `.nuspec` Datei auf Unix-Format Pfade, wie Windows-Pfadnamen selbst nuget.exe konvertiert und deswegen nicht.</span><span class="sxs-lookup"><span data-stu-id="8a5ff-109">You also need to adjust non-local paths in the `.nuspec` file to Unix-style paths, as nuget.exe doesn't convert Windows pathnames itself.</span></span>

## <a name="usage"></a><span data-ttu-id="8a5ff-110">Verwendung</span><span class="sxs-lookup"><span data-stu-id="8a5ff-110">Usage</span></span>

```
nuget pack <nuspecPath | projectPath> [options]
```

<span data-ttu-id="8a5ff-111">wobei `<nuspecPath>` und `<projectPath>` angeben der `.nuspec` oder Projektdatei bzw.</span><span class="sxs-lookup"><span data-stu-id="8a5ff-111">where `<nuspecPath>` and `<projectPath>` specify the `.nuspec` or project file, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="8a5ff-112">Optionen</span><span class="sxs-lookup"><span data-stu-id="8a5ff-112">Options</span></span>

| <span data-ttu-id="8a5ff-113">Option</span><span class="sxs-lookup"><span data-stu-id="8a5ff-113">Option</span></span> | <span data-ttu-id="8a5ff-114">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="8a5ff-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8a5ff-115">BasePath</span><span class="sxs-lookup"><span data-stu-id="8a5ff-115">BasePath</span></span> | <span data-ttu-id="8a5ff-116">Legt den Basispfad der Dateien im definiert die `.nuspec` Datei.</span><span class="sxs-lookup"><span data-stu-id="8a5ff-116">Sets the base path of the files defined in the `.nuspec` file.</span></span> |
| <span data-ttu-id="8a5ff-117">Build</span><span class="sxs-lookup"><span data-stu-id="8a5ff-117">Build</span></span> | <span data-ttu-id="8a5ff-118">Gibt an, dass das Projekt erstellt werden soll, bevor Sie das Paket erstellen.</span><span class="sxs-lookup"><span data-stu-id="8a5ff-118">Specifies that the project should be built before building the package.</span></span> |
| <span data-ttu-id="8a5ff-119">Ausschließen</span><span class="sxs-lookup"><span data-stu-id="8a5ff-119">Exclude</span></span> | <span data-ttu-id="8a5ff-120">Gibt einen oder mehrere Platzhaltermustern auszuschließende beim Erstellen eines Pakets an.</span><span class="sxs-lookup"><span data-stu-id="8a5ff-120">Specifies one or more wildcard patterns to exclude when creating a package.</span></span> |
| <span data-ttu-id="8a5ff-121">ExcludeEmptyDirectories</span><span class="sxs-lookup"><span data-stu-id="8a5ff-121">ExcludeEmptyDirectories</span></span> | <span data-ttu-id="8a5ff-122">Verhindert den Einschluss leere Verzeichnisse beim Erstellen des Pakets.</span><span class="sxs-lookup"><span data-stu-id="8a5ff-122">Prevents inclusion of empty directories when building the package.</span></span> |
| <span data-ttu-id="8a5ff-123">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="8a5ff-123">ForceEnglishOutput</span></span> | <span data-ttu-id="8a5ff-124">*(3.5 +)*  Erzwingt nuget.exe über eine invariante Kultur Englisch-basierte ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="8a5ff-124">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="8a5ff-125">Hilfe</span><span class="sxs-lookup"><span data-stu-id="8a5ff-125">Help</span></span> | <span data-ttu-id="8a5ff-126">Zeigt die Hilfe Informationen für den Befehl.</span><span class="sxs-lookup"><span data-stu-id="8a5ff-126">Displays help information for the command.</span></span> |
| <span data-ttu-id="8a5ff-127">IncludeReferencedProjects</span><span class="sxs-lookup"><span data-stu-id="8a5ff-127">IncludeReferencedProjects</span></span> | <span data-ttu-id="8a5ff-128">Gibt an, dass das erstellte Paket referenzierte Projekten als Abhängigkeiten oder auch als Teil des Pakets werden sollen.</span><span class="sxs-lookup"><span data-stu-id="8a5ff-128">Indicates that the built package should include referenced projects either as dependencies or as part of the package.</span></span> <span data-ttu-id="8a5ff-129">Wenn ein Referenziertes Projekt eine entsprechende wurde `.nuspec` Datei mit den gleichen Namen wie das Projekt, und klicken Sie dann dieses Projekt verwiesen wird, als Abhängigkeit hinzugefügt wird.</span><span class="sxs-lookup"><span data-stu-id="8a5ff-129">If a referenced project has a corresponding `.nuspec` file that has the same name as the project, then that referenced project is added as a dependency.</span></span> <span data-ttu-id="8a5ff-130">Andernfalls wird das Projekt als Teil des Pakets hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="8a5ff-130">Otherwise, the referenced project is added as part of the package.</span></span> |
| <span data-ttu-id="8a5ff-131">MinClientVersion</span><span class="sxs-lookup"><span data-stu-id="8a5ff-131">MinClientVersion</span></span> | <span data-ttu-id="8a5ff-132">Legen Sie die *"minclientversion"* Attribut für das erstellte Paket.</span><span class="sxs-lookup"><span data-stu-id="8a5ff-132">Set the *minClientVersion* attribute for the created package.</span></span> <span data-ttu-id="8a5ff-133">Dieser Wert überschreibt den Wert des vorhandenen *"minclientversion"* Attribut (sofern vorhanden) in der `.nuspec` Datei.</span><span class="sxs-lookup"><span data-stu-id="8a5ff-133">This value will override the value of the existing *minClientVersion* attribute (if any) in the `.nuspec` file.</span></span> |
| <span data-ttu-id="8a5ff-134">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="8a5ff-134">MSBuildPath</span></span> | <span data-ttu-id="8a5ff-135">*(4.0 und höher)*  Gibt den Pfad des MSBuild für die Verwendung mit dem Befehl, Vorrang vor `-MSBuildVersion`.</span><span class="sxs-lookup"><span data-stu-id="8a5ff-135">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="8a5ff-136">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="8a5ff-136">MSBuildVersion</span></span> | <span data-ttu-id="8a5ff-137">*(3.2 +)*  Gibt die Version von MSBuild mit diesem Befehl verwendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="8a5ff-137">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="8a5ff-138">Unterstützte Werte sind 4, 12, 14, 15.</span><span class="sxs-lookup"><span data-stu-id="8a5ff-138">Supported values are 4, 12, 14, 15.</span></span> <span data-ttu-id="8a5ff-139">Standardmäßig werden die MSBuild-Datei in Ihrem Pfad abgerufen wird, wird standardmäßig andernfalls die neueste installierte Version von MSBuild.</span><span class="sxs-lookup"><span data-stu-id="8a5ff-139">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="8a5ff-140">NoDefaultExcludes</span><span class="sxs-lookup"><span data-stu-id="8a5ff-140">NoDefaultExcludes</span></span> | <span data-ttu-id="8a5ff-141">Verhindert die Standard-Ausschlussliste NuGet-Paket-Dateien, Dateien und Ordnern, die mit einem Punkt beginnt wie `.svn` und `.gitignore`.</span><span class="sxs-lookup"><span data-stu-id="8a5ff-141">Prevents default exclusion of NuGet package files and files and folders starting with a dot, such as `.svn` and `.gitignore`.</span></span> |
| <span data-ttu-id="8a5ff-142">NoPackageAnalysis</span><span class="sxs-lookup"><span data-stu-id="8a5ff-142">NoPackageAnalysis</span></span> | <span data-ttu-id="8a5ff-143">Gibt an, dass der Packvorgang keine Paketanalyse nach dem Erstellen des Pakets ausführen sollte.</span><span class="sxs-lookup"><span data-stu-id="8a5ff-143">Specifies that pack should not run package analysis after building the package.</span></span> |
| <span data-ttu-id="8a5ff-144">OutputDirectory</span><span class="sxs-lookup"><span data-stu-id="8a5ff-144">OutputDirectory</span></span> | <span data-ttu-id="8a5ff-145">Gibt den Ordner, in dem das erstellte Paket gespeichert ist.</span><span class="sxs-lookup"><span data-stu-id="8a5ff-145">Specifies the folder in which the created package is stored.</span></span> <span data-ttu-id="8a5ff-146">Wenn kein Ordner angegeben wird, wird der aktuelle Ordner verwendet.</span><span class="sxs-lookup"><span data-stu-id="8a5ff-146">If no folder is specified, the current folder is used.</span></span> |
| <span data-ttu-id="8a5ff-147">Eigenschaften</span><span class="sxs-lookup"><span data-stu-id="8a5ff-147">Properties</span></span> | <span data-ttu-id="8a5ff-148">Gibt eine Liste mit Eigenschaften, die Werte in der Projektdatei zu überschreiben. finden Sie unter [gemeinsame MSBuild-Projekteigenschaften](https://docs.microsoft.com/visualstudio/msbuild/common-msbuild-project-properties) für Eigenschaftennamen.</span><span class="sxs-lookup"><span data-stu-id="8a5ff-148">Specifies a list of properties that override values in the project file; see [Common MSBuild Project Properties](https://docs.microsoft.com/visualstudio/msbuild/common-msbuild-project-properties) for property names.</span></span> <span data-ttu-id="8a5ff-149">Eigenschaftenargument hier ist eine Liste mit Token = Wert-Paaren, die durch Semikolons getrennt, in dem jedes Vorkommen von `$token$` in die `.nuspec` Datei mit dem angegebenen Wert ersetzt werden.</span><span class="sxs-lookup"><span data-stu-id="8a5ff-149">The Properties argument here is a list of token=value pairs, separated by semicolons, where each occurrence of `$token$` in the `.nuspec` file will be replaced with the given value.</span></span> <span data-ttu-id="8a5ff-150">Werte können Zeichenfolgen in Anführungszeichen eingeschlossen sein.</span><span class="sxs-lookup"><span data-stu-id="8a5ff-150">Values can be strings in quotation marks.</span></span> <span data-ttu-id="8a5ff-151">Beachten Sie, dass für die Eigenschaft "Konfiguration" die Standardeinstellung ist "Debug".</span><span class="sxs-lookup"><span data-stu-id="8a5ff-151">Note that for the "Configuration" property, the default is "Debug".</span></span> <span data-ttu-id="8a5ff-152">Um in einer Release-Konfiguration ändern, verwenden Sie `-Properties Configuration=Release`.</span><span class="sxs-lookup"><span data-stu-id="8a5ff-152">To change to a Release configuration, use `-Properties Configuration=Release`.</span></span> |
| <span data-ttu-id="8a5ff-153">Suffix</span><span class="sxs-lookup"><span data-stu-id="8a5ff-153">Suffix</span></span> | <span data-ttu-id="8a5ff-154">*(3.4.4+)*  Fügt ein Suffix, die intern generierten Versionsnummer, die in der Regel zum Anfügen von Build oder andere Vorabversion Bezeichner verwendet.</span><span class="sxs-lookup"><span data-stu-id="8a5ff-154">*(3.4.4+)* Appends a suffix to the internally generated version number, typically used for appending build or other pre-release identifiers.</span></span> <span data-ttu-id="8a5ff-155">Beispiel für die Verwendung `-suffix nightly` erstellen Sie ein Paket wird mit Version Number Like `1.2.3-nightly`.</span><span class="sxs-lookup"><span data-stu-id="8a5ff-155">For example, using `-suffix nightly` will create a package with a version number like `1.2.3-nightly`.</span></span> <span data-ttu-id="8a5ff-156">Suffixe müssen mit einem Buchstaben zur Vermeidung von Warnungen, Fehler und mögliche Inkompatibilitäten mit verschiedenen Versionen von NuGet und NuGet-Paket-Manager starten.</span><span class="sxs-lookup"><span data-stu-id="8a5ff-156">Suffixes must start with a letter to avoid warnings, errors, and potential incompatibilities with different versions of NuGet and the NuGet Package Manager.</span></span> |
| <span data-ttu-id="8a5ff-157">Symbole</span><span class="sxs-lookup"><span data-stu-id="8a5ff-157">Symbols</span></span> | <span data-ttu-id="8a5ff-158">Gibt an, dass das Paket Quellen und Symbole enthält.</span><span class="sxs-lookup"><span data-stu-id="8a5ff-158">Specifies that the package contains sources and symbols.</span></span> <span data-ttu-id="8a5ff-159">Bei Verwendung mit einem `.nuspec` Datei dies eine normale NuGet-Paket-Datei erstellt und das entsprechende Paket Symbole.</span><span class="sxs-lookup"><span data-stu-id="8a5ff-159">When used with a `.nuspec` file, this creates a regular NuGet package file and the corresponding symbols package.</span></span> |
| <span data-ttu-id="8a5ff-160">Tool</span><span class="sxs-lookup"><span data-stu-id="8a5ff-160">Tool</span></span> | <span data-ttu-id="8a5ff-161">Gibt an, dass die Ausgabedateien des Projekts soll, in platziert werden der `tool` Ordner.</span><span class="sxs-lookup"><span data-stu-id="8a5ff-161">Specifies that the output files of the project should be placed in the `tool` folder.</span></span> |
| <span data-ttu-id="8a5ff-162">Ausführlichkeit</span><span class="sxs-lookup"><span data-stu-id="8a5ff-162">Verbosity</span></span> | <span data-ttu-id="8a5ff-163">Gibt die Anzahl der Details in der Ausgabe angezeigt: *normalen*, *stillen*, *detaillierte (2.5 und höher)*.</span><span class="sxs-lookup"><span data-stu-id="8a5ff-163">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |
| <span data-ttu-id="8a5ff-164">Version</span><span class="sxs-lookup"><span data-stu-id="8a5ff-164">Version</span></span> | <span data-ttu-id="8a5ff-165">Überschreibt die Versionsnummer auf der `.nuspec` Datei.</span><span class="sxs-lookup"><span data-stu-id="8a5ff-165">Overrides the version number from the `.nuspec` file.</span></span> |

<span data-ttu-id="8a5ff-166">Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="8a5ff-166">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="excluding-development-dependencies"></a><span data-ttu-id="8a5ff-167">Ausschließen von Entwicklung Abhängigkeiten</span><span class="sxs-lookup"><span data-stu-id="8a5ff-167">Excluding development dependencies</span></span>

<span data-ttu-id="8a5ff-168">Einige NuGet-Pakete eignen sich als Entwicklung Abhängigkeiten, können Sie eigene Bibliothek erstellen, aber nicht notwendigerweise als tatsächliche paketabhängigkeiten benötigt werden.</span><span class="sxs-lookup"><span data-stu-id="8a5ff-168">Some NuGet packages are useful as development dependencies, which help you author your own library, but aren't necessarily needed as actual package dependencies.</span></span>

<span data-ttu-id="8a5ff-169">Die `pack` Befehl ignoriert `package` Einträge in `packages.config` , auf denen die `developmentDependency` -Attributsatz zur `true`.</span><span class="sxs-lookup"><span data-stu-id="8a5ff-169">The `pack` command will ignore `package` entries in `packages.config` that have the `developmentDependency` attribute set to `true`.</span></span> <span data-ttu-id="8a5ff-170">Diese Einträge werden nicht als eine Abhängigkeiten in der erstellten Paket eingefügt werden.</span><span class="sxs-lookup"><span data-stu-id="8a5ff-170">These entries will not be include as a dependencies in the created package.</span></span>

<span data-ttu-id="8a5ff-171">Angenommen, Sie haben die folgenden `packages.config` -Datei in das Quellprojekt:</span><span class="sxs-lookup"><span data-stu-id="8a5ff-171">For example, consider the following `packages.config` file in the source project:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="jQuery" version="1.5.2" />
    <package id="netfx-Guard" version="1.3.3.2" developmentDependency="true" />
    <package id="microsoft-web-helpers" version="1.15" />
</packages>
```

<span data-ttu-id="8a5ff-172">Für dieses Projekt das Paket erstellt hat, indem `nuget pack` hat eine Abhängigkeit auf `jQuery` und `microsoft-web-helpers` , aber nicht `netfx-Guard`.</span><span class="sxs-lookup"><span data-stu-id="8a5ff-172">For this project, the package created by `nuget pack` will have a dependency on `jQuery` and `microsoft-web-helpers` but not `netfx-Guard`.</span></span>

## <a name="examples"></a><span data-ttu-id="8a5ff-173">Beispiele</span><span class="sxs-lookup"><span data-stu-id="8a5ff-173">Examples</span></span>

```
nuget pack

nuget pack foo.nuspec

nuget pack foo.csproj

nuget pack foo.csproj -Properties Configuration=Release

nuget pack foo.csproj -Build -Symbols -Properties owners=janedoe,xiaop;version="1.0.5"

# create a package from project foo.csproj, using MSBuild version 12 to build the project
nuget pack foo.csproj -Build -Symbols -Properties owners=janedoe,xiaop;version="1.0.5" -MSBuildVersion 12

nuget pack foo.nuspec -Version 2.1.0

nuget pack foo.nuspec -Version 1.0.0 -MinClientVersion 2.5
```
