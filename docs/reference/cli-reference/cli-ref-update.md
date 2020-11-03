---
title: Befehl "nuget CLI-Update"
description: Referenz für den nuget.exe Update-Befehl
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 106c4027f03d8e8c1d19545b3ca9b6cd5263830e
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/03/2020
ms.locfileid: "93236788"
---
# <a name="update-command-nuget-cli"></a><span data-ttu-id="044cb-103">Befehl Aktualisieren (nuget-CLI)</span><span class="sxs-lookup"><span data-stu-id="044cb-103">update command (NuGet CLI)</span></span>

<span data-ttu-id="044cb-104">**Gilt für:** &bullet; **unterstützte Versionen** von Paket Verbrauch: alle</span><span class="sxs-lookup"><span data-stu-id="044cb-104">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="044cb-105">Alle Pakete in einem Projekt werden (unter Verwendung von `packages.config`) auf die neuesten verfügbaren Versionen aktualisiert.</span><span class="sxs-lookup"><span data-stu-id="044cb-105">Updates all packages in a project (using `packages.config`) to their latest available versions.</span></span> <span data-ttu-id="044cb-106">Es wird empfohlen, ["Restore"](cli-ref-restore.md) auszuführen, bevor Sie Ausführen `update` .</span><span class="sxs-lookup"><span data-stu-id="044cb-106">It is recommended to run ['restore'](cli-ref-restore.md) before running the `update`.</span></span> <span data-ttu-id="044cb-107">(Um ein einzelnes Paket zu aktualisieren, verwenden Sie, [`nuget install`](cli-ref-install.md) ohne eine Versionsnummer anzugeben. in diesem Fall installiert nuget die neueste Version.)</span><span class="sxs-lookup"><span data-stu-id="044cb-107">(To update an individual package, use [`nuget install`](cli-ref-install.md) without specifying a version number, in which case NuGet installs the latest version.)</span></span>

<span data-ttu-id="044cb-108">Hinweis: `update` funktioniert nicht mit der CLI, die unter Mono (Mac OSX oder Linux) ausgeführt wird, oder wenn das packagereferenzierungsformat verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="044cb-108">Note: `update` does not work with the CLI running under Mono (Mac OSX or Linux) or when using the PackageReference format.</span></span>

<span data-ttu-id="044cb-109">Der `update` Befehl aktualisiert außerdem Assemblyverweise in der Projektdatei, sofern diese Verweise bereits vorhanden sind.</span><span class="sxs-lookup"><span data-stu-id="044cb-109">The `update` command also updates assembly references in the project file, provided those references already exist.</span></span> <span data-ttu-id="044cb-110">Wenn ein aktualisiertes Paket über eine hinzugefügte Assembly verfügt, wird *kein* neuer Verweis hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="044cb-110">If an updated package has an added assembly, a new reference is *not* added.</span></span> <span data-ttu-id="044cb-111">Neuen Paketabhängigkeiten werden auch keine Assemblyverweise hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="044cb-111">New package dependencies also don't have their assembly references added.</span></span> <span data-ttu-id="044cb-112">Aktualisieren Sie das Paket in Visual Studio mithilfe der Benutzeroberfläche des Paket-Managers oder der Paket-Manager-Konsole, um diese Vorgänge als Teil eines Updates einzuschließen.</span><span class="sxs-lookup"><span data-stu-id="044cb-112">To include these operations as part of an update, update the package in Visual Studio using the Package Manager UI or the Package Manager Console.</span></span>

<span data-ttu-id="044cb-113">Dieser Befehl kann auch verwendet werden, um nuget.exe mit dem *-Self-* Flag zu aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="044cb-113">This command can also be used to update nuget.exe itself using the *-self* flag.</span></span>

## <a name="usage"></a><span data-ttu-id="044cb-114">Verbrauch</span><span class="sxs-lookup"><span data-stu-id="044cb-114">Usage</span></span>

```cli
nuget update <configPath> [options]
```

<span data-ttu-id="044cb-115">dabei `<configPath>` identifiziert entweder eine `packages.config` oder eine Projektmappendatei, die die Abhängigkeiten des Projekts auflistet.</span><span class="sxs-lookup"><span data-stu-id="044cb-115">where `<configPath>` identifies either a `packages.config` or solution file that lists the project's dependencies.</span></span>

## <a name="options"></a><span data-ttu-id="044cb-116">Optionen</span><span class="sxs-lookup"><span data-stu-id="044cb-116">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="044cb-117">Die anzuwendende nuget-Konfigurationsdatei.</span><span class="sxs-lookup"><span data-stu-id="044cb-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="044cb-118">Wenn nichts angegeben ist, `%AppData%\NuGet\NuGet.Config` wird (Windows) `~/.nuget/NuGet/NuGet.Config` oder `~/.config/NuGet/NuGet.Config` (Mac/Linux) verwendet.</span><span class="sxs-lookup"><span data-stu-id="044cb-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>
  
- **`-DependencyVersion [Lowest, HighestPatch, HighestMinor, Highest, Ignore]`**

  <span data-ttu-id="044cb-119">Gibt die Version der zu verwendenden Abhängigkeits Pakete an. dabei kann es sich um einen der folgenden handeln:</span><span class="sxs-lookup"><span data-stu-id="044cb-119">Specifies the version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="044cb-120">*Niedrigste* (Standard): die niedrigste Version</span><span class="sxs-lookup"><span data-stu-id="044cb-120">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="044cb-121">*Highestpatch* : die Version mit dem niedrigsten, niedrigsten, niedrigsten, größten Patch</span><span class="sxs-lookup"><span data-stu-id="044cb-121">*HighestPatch* : the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="044cb-122">*Highestminor* : die Version mit dem niedrigsten Haupt-, höchst-und Höchstwert</span><span class="sxs-lookup"><span data-stu-id="044cb-122">*HighestMinor* : the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="044cb-123">*Höchste* Version: die höchste Version</span><span class="sxs-lookup"><span data-stu-id="044cb-123">*Highest* : the highest version</span></span></li><li><span data-ttu-id="044cb-124">*Ignore* : Es werden keine Abhängigkeits Pakete verwendet.</span><span class="sxs-lookup"><span data-stu-id="044cb-124">*Ignore* : No dependency packages will be used</span></span></li></ul>

- **`-FileConflictAction [PromptUser, Overwrite, Ignore]`**

  <span data-ttu-id="044cb-125">Gibt die Standardaktion an, wenn eine Datei aus einem Paket im Ziel Projekt bereits vorhanden ist.</span><span class="sxs-lookup"><span data-stu-id="044cb-125">Specifies the default action when a file from a package already exists in the target project.</span></span> <span data-ttu-id="044cb-126">Legen Sie auf fest, `Overwrite` um Dateien immer zu überschreiben.</span><span class="sxs-lookup"><span data-stu-id="044cb-126">Set to `Overwrite` to always overwrite files.</span></span> <span data-ttu-id="044cb-127">Auf festlegen, `Ignore` um Dateien zu überspringen.</span><span class="sxs-lookup"><span data-stu-id="044cb-127">Set to `Ignore` to skip files.</span></span>

  <span data-ttu-id="044cb-128">Durch die `PromptUser` Aktion (Standardeinstellung) wird eine Eingabeaufforderung für jede in Konflikt stehende Datei angezeigt, sofern nicht `OverwriteAll` oder angegeben wird `IgnoreAll` , was für alle verbleibenden Dateien gilt.</span><span class="sxs-lookup"><span data-stu-id="044cb-128">The `PromptUser` action, the default, will prompt for each conflicting file unless `OverwriteAll` or `IgnoreAll` is provided, which will apply to all remaining files.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="044cb-129">*(3.5* und höher) Erzwingt das Ausführen von nuget.exe mit einer invarianten, englischen Kultur.</span><span class="sxs-lookup"><span data-stu-id="044cb-129">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="044cb-130">Zeigt Hilfe Informationen für den Befehl an.</span><span class="sxs-lookup"><span data-stu-id="044cb-130">Displays help information for the command.</span></span>

- **`-Id`**

  <span data-ttu-id="044cb-131">Gibt eine Liste der zu aktualisierenden Paket-IDs an.</span><span class="sxs-lookup"><span data-stu-id="044cb-131">Specifies a list of package IDs to update.</span></span>

- **`-MSBuildPath`**

  <span data-ttu-id="044cb-132">*(4.0* und höher) Gibt den Pfad von MSBuild an, der mit dem Befehl verwendet werden soll, und hat Vorrang vor `-MSBuildVersion` .</span><span class="sxs-lookup"><span data-stu-id="044cb-132">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span>

- **`-MSBuildVersion`**

  <span data-ttu-id="044cb-133">*(3.2 +)* Gibt die Version von MSBuild an, die mit diesem Befehl verwendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="044cb-133">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="044cb-134">Unterstützte Werte sind 4, 12, 14, 15,1, 15,3, 15,4, 15,5, 15,6, 15,7, 15,8, 15,9.</span><span class="sxs-lookup"><span data-stu-id="044cb-134">Supported values are 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9.</span></span> <span data-ttu-id="044cb-135">Standardmäßig wird der MSBuild in Ihrem Pfad ausgewählt; andernfalls wird standardmäßig die höchste installierte Version von MSBuild verwendet.</span><span class="sxs-lookup"><span data-stu-id="044cb-135">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="044cb-136">Unterdrückt Eingabe Aufforderungen für Benutzereingaben oder Bestätigungen.</span><span class="sxs-lookup"><span data-stu-id="044cb-136">Suppresses prompts for user input or confirmations.</span></span>

- **`-PreRelease`**

  <span data-ttu-id="044cb-137">Ermöglicht das Aktualisieren von vorab Versionen.</span><span class="sxs-lookup"><span data-stu-id="044cb-137">Allows updating to prerelease versions.</span></span> <span data-ttu-id="044cb-138">Dieses Flag ist beim Aktualisieren bereits installierter vorab Pakete nicht erforderlich.</span><span class="sxs-lookup"><span data-stu-id="044cb-138">This flag is not required when updating prerelease packages that are already installed.</span></span>

- **`-RepositoryPath`**

  <span data-ttu-id="044cb-139">Gibt den lokalen Ordner an, in dem Pakete installiert werden.</span><span class="sxs-lookup"><span data-stu-id="044cb-139">Specifies the local folder where packages are installed.</span></span>

- **`-Safe`**

  <span data-ttu-id="044cb-140">Gibt an, dass nur Updates mit der höchsten Version, die innerhalb derselben Haupt-und neben Version wie das installierte Paket verfügbar ist, installiert werden.</span><span class="sxs-lookup"><span data-stu-id="044cb-140">Specifies that only updates with the highest version available within the same major and minor version as the installed package will be installed.</span></span>

- **`-Self`**

  <span data-ttu-id="044cb-141">Aktualisiert nuget.exe auf die neueste Version. alle anderen Argumente werden ignoriert.</span><span class="sxs-lookup"><span data-stu-id="044cb-141">Updates nuget.exe to the latest version; all other arguments are ignored.</span></span>

- **`-Source`**

  <span data-ttu-id="044cb-142">Gibt die Liste der Paketquellen (als URLs) an, die für die Updates verwendet werden sollen.</span><span class="sxs-lookup"><span data-stu-id="044cb-142">Specifies the list of package sources (as URLs) to use for the updates.</span></span> <span data-ttu-id="044cb-143">Wenn der Befehl nicht angegeben wird, verwendet der Befehl die in den Konfigurationsdateien bereitgestellten Quellen, siehe [Allgemeine nuget-Konfigurationen](../../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="044cb-143">If omitted, the command uses the sources provided in configuration files, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="044cb-144">Gibt den Umfang der in der Ausgabe angezeigten Details an: `normal` (Standard), `quiet` oder `detailed` .</span><span class="sxs-lookup"><span data-stu-id="044cb-144">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

- **`-Version`**

  <span data-ttu-id="044cb-145">Gibt bei Verwendung mit einer Paket-ID die Version des zu aktualisierenden Pakets an.</span><span class="sxs-lookup"><span data-stu-id="044cb-145">When used with one package ID, specifies the version of the package to update.</span></span>

<span data-ttu-id="044cb-146">Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="044cb-146">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="044cb-147">Beispiele</span><span class="sxs-lookup"><span data-stu-id="044cb-147">Examples</span></span>

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
