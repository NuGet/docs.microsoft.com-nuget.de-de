---
title: Befehl "nuget CLI Restore"
description: Referenz für den nuget.exe Restore-Befehl
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 108317aba2107948180ab0149c0c5ba5150cf9b8
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622829"
---
# <a name="restore-command-nuget-cli"></a><span data-ttu-id="cb1a1-103">Restore-Befehl (nuget-CLI)</span><span class="sxs-lookup"><span data-stu-id="cb1a1-103">restore command (NuGet CLI)</span></span>

<span data-ttu-id="cb1a1-104">**Gilt für:** &bullet; **unterstützte Versionen** von Paketen: 2.7 und höher</span><span class="sxs-lookup"><span data-stu-id="cb1a1-104">**Applies to:** package consumption &bullet; **Supported versions:** 2.7+</span></span>

<span data-ttu-id="cb1a1-105">Alle Pakete, die im Ordner fehlen, werden heruntergeladen und installiert `packages` .</span><span class="sxs-lookup"><span data-stu-id="cb1a1-105">Downloads and installs any packages missing from the `packages` folder.</span></span> <span data-ttu-id="cb1a1-106">Bei der Verwendung mit nuget 4.0 und höher und dem packagereferenzierungsformat wird `<project>.nuget.props` bei Bedarf im Ordner eine Datei generiert `obj` .</span><span class="sxs-lookup"><span data-stu-id="cb1a1-106">When used with NuGet 4.0+ and the PackageReference format, generates a `<project>.nuget.props` file, if needed, in the `obj` folder.</span></span> <span data-ttu-id="cb1a1-107">(Die Datei kann in der Quell Code Verwaltung ausgelassen werden.)</span><span class="sxs-lookup"><span data-stu-id="cb1a1-107">(The file can be omitted from source control.)</span></span>

<span data-ttu-id="cb1a1-108">Unter Mac OSX und Linux mit der CLI in Mono wird das Wiederherstellen von Paketen mit packagereferenzierung nicht unterstützt.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-108">On Mac OSX and Linux with the CLI on Mono, restoring packages is not supported with PackageReference.</span></span>

## <a name="usage"></a><span data-ttu-id="cb1a1-109">Verwendung</span><span class="sxs-lookup"><span data-stu-id="cb1a1-109">Usage</span></span>

```cli
nuget restore <projectPath> [options]
```

<span data-ttu-id="cb1a1-110">dabei `<projectPath>` gibt den Speicherort einer Projekt Mappe oder einer `packages.config` Datei an.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-110">where `<projectPath>` specifies the location of a solution or a `packages.config` file.</span></span> <span data-ttu-id="cb1a1-111">Informationen zu den Verhaltens [Details finden Sie unten in](#remarks) den hinweisen.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-111">See [Remarks](#remarks) below for behavioral details.</span></span>

## <a name="options"></a><span data-ttu-id="cb1a1-112">Optionen</span><span class="sxs-lookup"><span data-stu-id="cb1a1-112">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="cb1a1-113">Die anzuwendende nuget-Konfigurationsdatei.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-113">The NuGet configuration file to apply.</span></span> <span data-ttu-id="cb1a1-114">Wenn nichts angegeben ist, `%AppData%\NuGet\NuGet.Config` wird (Windows) `~/.nuget/NuGet/NuGet.Config` oder `~/.config/NuGet/NuGet.Config` (Mac/Linux) verwendet.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-114">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-DirectDownload`**

  <span data-ttu-id="cb1a1-115">*(4.0* und höher) Pakete werden direkt heruntergeladen, ohne dass Caches mit Binärdateien oder Metadaten aufgefüllt werden.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-115">*(4.0+)* Downloads packages directly without populating caches with any binaries or metadata.</span></span>

- **`-DisableParallelProcessing`**

   <span data-ttu-id="cb1a1-116">Deaktiviert die parallele Wiederherstellung mehrerer Pakete.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-116">Disables restoring multiple packages in parallel.</span></span>

- **`-FallbackSource`**

  <span data-ttu-id="cb1a1-117">*(3.2 +)* Eine Liste von Paketquellen, die als Fallbacks verwendet werden sollen, falls das Paket nicht in der primären oder der Standard Quelle gefunden wurde.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-117">*(3.2+)* A list of package sources to use as fallbacks in case the package isn't found in the primary or default source.</span></span> <span data-ttu-id="cb1a1-118">Verwenden Sie zum Trennen von Listeneinträgen ein Semikolon.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-118">Use a semicolon to separate list entries.</span></span>

- **`-Force`**

  <span data-ttu-id="cb1a1-119">In packagereferenzierungsbasierten Projekten erzwingt, dass alle Abhängigkeiten gelöst werden, auch wenn die letzte Wiederherstellung erfolgreich war.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-119">In PackageReference based projects, forces all dependencies to be resolved even if the last restore was successful.</span></span> <span data-ttu-id="cb1a1-120">Die Angabe dieses Flags ähnelt dem Löschen der `project.assets.json` Datei.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-120">Specifying this flag is similar to deleting the `project.assets.json` file.</span></span> <span data-ttu-id="cb1a1-121">Dadurch wird der HTTP-Cache nicht umgangen.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-121">This does not bypass the http-cache.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="cb1a1-122">*(3.5* und höher) Erzwingt das Ausführen von nuget.exe mit einer invarianten, englischen Kultur.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-ForceEvaluate`**

  <span data-ttu-id="cb1a1-123">Erzwingt die Neubewertung aller Abhängigkeiten bei der Wiederherstellung, selbst wenn bereits eine Sperrdatei vorhanden ist.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-123">Forces restore to reevaluate all dependencies even if a lock file already exists.</span></span>

- **`-?|-help`**

  <span data-ttu-id="cb1a1-124">Zeigt Hilfe Informationen für den Befehl an.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-124">Displays help information for the command.</span></span>

- **`-LockFilePath`**

  <span data-ttu-id="cb1a1-125">Ausgabespeicherort, in den die Projektsperrdatei geschrieben wird.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-125">Output location where project lock file is written.</span></span> <span data-ttu-id="cb1a1-126">Die Standardeinstellung ist `PROJECT_ROOT\packages.lock.json`.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-126">By default, this is `PROJECT_ROOT\packages.lock.json`.</span></span>

- **`-LockedMode`**

  <span data-ttu-id="cb1a1-127">Lassen Sie keine Aktualisierung der Projektsperrdatei zu.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-127">Don't allow updating project lock file.</span></span>

- **`-MSBuildPath`**

   <span data-ttu-id="cb1a1-128">*(4.0* und höher) Gibt den Pfad von MSBuild an, der mit dem Befehl verwendet werden soll, und hat Vorrang vor `-MSBuildVersion` .</span><span class="sxs-lookup"><span data-stu-id="cb1a1-128">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span>

- **`-MSBuildVersion`**

  <span data-ttu-id="cb1a1-129">*(3.2 +)* Gibt die Version von MSBuild an, die mit diesem Befehl verwendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-129">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="cb1a1-130">Unterstützte Werte sind 4, 12, 14, 15,1, 15,3, 15,4, 15,5, 15,6, 15,7, 15,8, 15,9.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-130">Supported values are 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9.</span></span> <span data-ttu-id="cb1a1-131">Standardmäßig wird der MSBuild in Ihrem Pfad ausgewählt; andernfalls wird standardmäßig die höchste installierte Version von MSBuild verwendet.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-131">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span>

- **`-NoCache`**

  <span data-ttu-id="cb1a1-132">Verhindert, dass nuget zwischengespeicherte Pakete verwendet.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-132">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="cb1a1-133">Weitere Informationen finden Sie [unter Verwalten der globalen Pakete und Cache Ordner](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="cb1a1-133">See [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="cb1a1-134">Unterdrückt Eingabe Aufforderungen für Benutzereingaben oder Bestätigungen.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-134">Suppresses prompts for user input or confirmations.</span></span>

- **`-OutputDirectory`**

  <span data-ttu-id="cb1a1-135">Gibt den Ordner an, in dem Pakete installiert werden.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-135">Specifies the folder in which packages are installed.</span></span> <span data-ttu-id="cb1a1-136">Wenn kein Ordner angegeben wird, wird der aktuelle Ordner verwendet.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-136">If no folder is specified, the current folder is used.</span></span> <span data-ttu-id="cb1a1-137">Erforderlich, wenn mit einer `packages.config` Datei wieder hergestellt wird, sofern nicht `PackagesDirectory` oder `SolutionDirectory` verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-137">Required when restoring with a `packages.config` file unless `PackagesDirectory` or `SolutionDirectory` is used.</span></span>

- **`-PackageSaveMode`**

  <span data-ttu-id="cb1a1-138">Gibt die Dateitypen an, die nach der Paketinstallation gespeichert werden sollen: einer von `nuspec` , `nupkg` oder `nuspec;nupkg` .</span><span class="sxs-lookup"><span data-stu-id="cb1a1-138">Specifies the types of files to save after package installation: one of `nuspec`, `nupkg`, or `nuspec;nupkg`.</span></span>

- **`-PackagesDirectory`**

  <span data-ttu-id="cb1a1-139">Wie in `OutputDirectory`.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-139">Same as `OutputDirectory`.</span></span> <span data-ttu-id="cb1a1-140">Erforderlich, wenn mit einer `packages.config` Datei wieder hergestellt wird, sofern nicht `OutputDirectory` oder `SolutionDirectory` verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-140">Required when restoring with a `packages.config` file unless `OutputDirectory` or `SolutionDirectory` is used.</span></span>

- **`-Project2ProjectTimeOut`**

  <span data-ttu-id="cb1a1-141">Timeout in Sekunden für das Auflösen von Projekt-zu-Projekt-verweisen.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-141">Timeout in seconds for resolving project-to-project references.</span></span>

- **`-Recursive`**

  <span data-ttu-id="cb1a1-142">*(4.0* und höher) Stellt alle Referenzprojekte für UWP-und .net Core-Projekte wieder her.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-142">*(4.0+)* Restores all references projects for UWP and .NET Core projects.</span></span> <span data-ttu-id="cb1a1-143">Gilt nicht für Projekte, die verwenden `packages.config` .</span><span class="sxs-lookup"><span data-stu-id="cb1a1-143">Does not apply to projects using `packages.config`.</span></span>

- **`-RequireConsent`**

  <span data-ttu-id="cb1a1-144">Überprüft, ob das Wiederherstellen von Paketen aktiviert ist, bevor die Pakete heruntergeladen und installiert werden.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-144">Verifies that restoring packages is enabled before downloading and installing the packages.</span></span> <span data-ttu-id="cb1a1-145">Weitere Informationen finden Sie unter [Paket Wiederherstellung](../../consume-packages/package-restore.md).</span><span class="sxs-lookup"><span data-stu-id="cb1a1-145">For details, see [Package Restore](../../consume-packages/package-restore.md).</span></span>

- **`-SolutionDirectory`**

  <span data-ttu-id="cb1a1-146">Gibt den Projektmappenordner an.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-146">Specifies the solution folder.</span></span> <span data-ttu-id="cb1a1-147">Ungültig beim Wiederherstellen von Paketen für eine Projekt Mappe.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-147">Not valid when restoring packages for a solution.</span></span> <span data-ttu-id="cb1a1-148">Erforderlich, wenn mit einer `packages.config` Datei wieder hergestellt wird, sofern nicht `PackagesDirectory` oder `OutputDirectory` verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-148">Required when restoring with a `packages.config` file unless `PackagesDirectory` or `OutputDirectory` is used.</span></span>

- **`-Source`**

  <span data-ttu-id="cb1a1-149">Gibt die Liste der Paketquellen (als URLs) an, die für die Wiederherstellung verwendet werden sollen.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-149">Specifies the list of package sources (as URLs) to use for the restore.</span></span> <span data-ttu-id="cb1a1-150">Wenn der Befehl weggelassen wird, verwendet der Befehl die in den Konfigurationsdateien bereitgestellten Quellen, siehe [Konfigurieren des nuget-Verhaltens](../../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="cb1a1-150">If omitted, the command uses the sources provided in configuration files, see [Configuring NuGet behavior](../../consume-packages/configuring-nuget-behavior.md).</span></span> <span data-ttu-id="cb1a1-151">Verwenden Sie zum Trennen von Listeneinträgen ein Semikolon.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-151">Use a semicolon to separate list entries.</span></span>

- **`-UseLockFile`**

  <span data-ttu-id="cb1a1-152">Ermöglicht das Generieren und Verwenden einer Projektsperrdatei bei der Wiederherstellung.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-152">Enables project lock file to be generated and used with restore.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="cb1a1-153">Gibt den Umfang der in der Ausgabe angezeigten Details an: `normal` (Standard), `quiet` oder `detailed` .</span><span class="sxs-lookup"><span data-stu-id="cb1a1-153">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="cb1a1-154">Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="cb1a1-154">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="remarks"></a><span data-ttu-id="cb1a1-155">Hinweise</span><span class="sxs-lookup"><span data-stu-id="cb1a1-155">Remarks</span></span>

<span data-ttu-id="cb1a1-156">Der Restore-Befehl führt die folgenden Schritte aus:</span><span class="sxs-lookup"><span data-stu-id="cb1a1-156">The restore command performs the following steps:</span></span>

1. <span data-ttu-id="cb1a1-157">Bestimmen Sie den Betriebsmodus des Restore-Befehls.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-157">Determine the operation mode of the restore command.</span></span>

   | <span data-ttu-id="cb1a1-158">ProjectPath-Dateityp</span><span class="sxs-lookup"><span data-stu-id="cb1a1-158">projectPath file type</span></span> | <span data-ttu-id="cb1a1-159">Verhalten</span><span class="sxs-lookup"><span data-stu-id="cb1a1-159">Behavior</span></span> |
   | --- | --- |
   | <span data-ttu-id="cb1a1-160">Lösung (Ordner)</span><span class="sxs-lookup"><span data-stu-id="cb1a1-160">Solution (folder)</span></span> | <span data-ttu-id="cb1a1-161">Nuget sucht nach einer `.sln` Datei und verwendet diese, wenn Sie gefunden wird, andernfalls wird ein Fehler ausgegeben.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-161">NuGet looks for a `.sln` file and uses that if found; otherwise gives an error.</span></span> <span data-ttu-id="cb1a1-162">`(SolutionDir)\.nuget` wird als Startordner verwendet.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-162">`(SolutionDir)\.nuget` is used as the starting folder.</span></span> |
   | <span data-ttu-id="cb1a1-163">`.sln`-Datei</span><span class="sxs-lookup"><span data-stu-id="cb1a1-163">`.sln` file</span></span> | <span data-ttu-id="cb1a1-164">Von der Lösung identifizierte Pakete wiederherstellen; Gibt einen Fehler aus, wenn `-SolutionDirectory` verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-164">Restore packages identified by the solution; gives an error if `-SolutionDirectory` is used.</span></span> <span data-ttu-id="cb1a1-165">`$(SolutionDir)\.nuget` wird als Startordner verwendet.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-165">`$(SolutionDir)\.nuget` is used as the starting folder.</span></span> |
   | <span data-ttu-id="cb1a1-166">`packages.config` -oder-Projektdatei</span><span class="sxs-lookup"><span data-stu-id="cb1a1-166">`packages.config` or project file</span></span> | <span data-ttu-id="cb1a1-167">Wiederherstellen der in der Datei aufgeführten Pakete, auflösen und Installieren von Abhängigkeiten.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-167">Restore packages listed in the file, resolving and installing dependencies.</span></span> |
   | <span data-ttu-id="cb1a1-168">Anderer Dateityp</span><span class="sxs-lookup"><span data-stu-id="cb1a1-168">Other file type</span></span> | <span data-ttu-id="cb1a1-169">Es wird davon ausgegangen, dass eine Datei `.sln` wie oben angegeben wird. wenn es sich nicht um eine Lösung handelt, gibt nuget einen Fehler aus.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-169">File is assumed to be a `.sln` file as above; if it's not a solution, NuGet gives an error.</span></span> |
   | <span data-ttu-id="cb1a1-170">(ProjectPath nicht angegeben)</span><span class="sxs-lookup"><span data-stu-id="cb1a1-170">(projectPath not specified)</span></span> | <ul><li><span data-ttu-id="cb1a1-171">Nuget sucht im aktuellen Ordner nach Projektmappendateien.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-171">NuGet looks for solution files in the current folder.</span></span> <span data-ttu-id="cb1a1-172">Wenn eine einzelne Datei gefunden wird, wird diese zum Wiederherstellen von Paketen verwendet. Wenn mehrere Lösungen gefunden werden, gibt nuget einen Fehler aus.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-172">If a single file is found, that one is used to restore packages; if multiple solutions are found, NuGet gives an error.</span></span></li><li><span data-ttu-id="cb1a1-173">Wenn keine Projektmappendateien vorhanden sind, sucht nuget nach einem `packages.config` und verwendet dieses zum Wiederherstellen von Paketen.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-173">If there are no solution files, NuGet looks for a `packages.config` and uses that to restore packages.</span></span></li><li><span data-ttu-id="cb1a1-174">Wenn keine Projekt `packages.config` Mappe oder Datei gefunden wird, gibt nuget einen Fehler aus.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-174">If no solution or `packages.config` file is found, NuGet gives an error.</span></span></ul> |

2. <span data-ttu-id="cb1a1-175">Bestimmen Sie den Ordner "Pakete" mit der folgenden Prioritäts Reihenfolge (nuget gibt einen Fehler aus, wenn keiner dieser Ordner gefunden wird):</span><span class="sxs-lookup"><span data-stu-id="cb1a1-175">Determine the packages folder using the following priority order (NuGet gives an error if none of these folders are found):</span></span>

    - <span data-ttu-id="cb1a1-176">Der mit angegebene Ordner `-PackagesDirectory` .</span><span class="sxs-lookup"><span data-stu-id="cb1a1-176">The folder specified with `-PackagesDirectory`.</span></span>
    - <span data-ttu-id="cb1a1-177">Der `repositoryPath` Wert in `Nuget.Config`</span><span class="sxs-lookup"><span data-stu-id="cb1a1-177">The `repositoryPath` value in `Nuget.Config`</span></span>
    - <span data-ttu-id="cb1a1-178">Der mit angegebene Ordner `-SolutionDirectory`</span><span class="sxs-lookup"><span data-stu-id="cb1a1-178">The folder specified with `-SolutionDirectory`</span></span>
    - `$(SolutionDir)\packages`

3. <span data-ttu-id="cb1a1-179">Beim Wiederherstellen von Paketen für eine Lösung führt nuget Folgendes aus:</span><span class="sxs-lookup"><span data-stu-id="cb1a1-179">When restoring packages for a solution, NuGet does the following:</span></span>
    - <span data-ttu-id="cb1a1-180">Lädt die Projektmappendatei.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-180">Loads the solution file.</span></span>
    - <span data-ttu-id="cb1a1-181">Stellt Pakete auf `$(SolutionDir)\.nuget\packages.config` Projektmappenebene wieder her, die in aufgelistet sind `packages` .</span><span class="sxs-lookup"><span data-stu-id="cb1a1-181">Restores solution level packages listed in `$(SolutionDir)\.nuget\packages.config` into the `packages` folder.</span></span>
    - <span data-ttu-id="cb1a1-182">Wiederherstellen der in aufgelisteten Pakete in `$(ProjectDir)\packages.config` den `packages` Ordner.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-182">Restore packages listed in `$(ProjectDir)\packages.config` into the `packages` folder.</span></span> <span data-ttu-id="cb1a1-183">Stellen Sie das Paket für jedes angegebene Paket parallel wieder her, es sei denn, `-DisableParallelProcessing` wird angegeben.</span><span class="sxs-lookup"><span data-stu-id="cb1a1-183">For each package specified, restore the package in parallel unless `-DisableParallelProcessing` is specified.</span></span>

## <a name="examples"></a><span data-ttu-id="cb1a1-184">Beispiele</span><span class="sxs-lookup"><span data-stu-id="cb1a1-184">Examples</span></span>

```cli
# Restore packages for a solution file
nuget restore a.sln

# Restore packages for a solution file, using MSBuild version 14.0 to load the solution and its project(s)
nuget restore a.sln -MSBuildVersion 14

# Restore packages for a project's packages.config file, with the packages folder at the parent
nuget restore proj1\packages.config -PackagesDirectory ..\packages

# Restore packages for the solution in the current folder, specifying package sources
nuget restore -source "https://api.nuget.org/v3/index.json;https://www.myget.org/F/nuget"
```
