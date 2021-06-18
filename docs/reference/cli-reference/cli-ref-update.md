---
title: Befehl zum Aktualisieren der NuGet-BEFEHLSZEILEnschnittstelle
description: Referenz für den befehl nuget.exe update
author: JonDouglas
ms.author: jodou
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 5f244e4cf15ca7afa0e6318a8c20d464ff75bd8e
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323647"
---
# <a name="update-command-nuget-cli"></a><span data-ttu-id="55cb9-103">Befehl "update" (NuGet-CLI)</span><span class="sxs-lookup"><span data-stu-id="55cb9-103">update command (NuGet CLI)</span></span>

<span data-ttu-id="55cb9-104">**Gilt für:** Paketnutzung &bullet; **Unterstützte Versionen:** alle</span><span class="sxs-lookup"><span data-stu-id="55cb9-104">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="55cb9-105">Alle Pakete in einem Projekt werden (unter Verwendung von `packages.config`) auf die neuesten verfügbaren Versionen aktualisiert.</span><span class="sxs-lookup"><span data-stu-id="55cb9-105">Updates all packages in a project (using `packages.config`) to their latest available versions.</span></span> <span data-ttu-id="55cb9-106">Es wird empfohlen, ["restore"](cli-ref-restore.md) auszuführen, bevor Sie `update` ausführen.</span><span class="sxs-lookup"><span data-stu-id="55cb9-106">It is recommended to run ['restore'](cli-ref-restore.md) before running the `update`.</span></span> <span data-ttu-id="55cb9-107">(Um ein einzelnes Paket zu aktualisieren, verwenden Sie [`nuget install`](cli-ref-install.md) , ohne eine Versionsnummer anzugeben. In diesem Fall installiert NuGet die neueste Version.)</span><span class="sxs-lookup"><span data-stu-id="55cb9-107">(To update an individual package, use [`nuget install`](cli-ref-install.md) without specifying a version number, in which case NuGet installs the latest version.)</span></span>

<span data-ttu-id="55cb9-108">Hinweis: funktioniert nicht mit der CLI unter `update` Mono (Mac OSX oder Linux) oder bei Verwendung des PackageReference-Formats.</span><span class="sxs-lookup"><span data-stu-id="55cb9-108">Note: `update` does not work with the CLI running under Mono (Mac OSX or Linux) or when using the PackageReference format.</span></span>

<span data-ttu-id="55cb9-109">Der `update` Befehl aktualisiert auch Assemblyverweise in der Projektdatei, sofern diese Verweise bereits vorhanden sind.</span><span class="sxs-lookup"><span data-stu-id="55cb9-109">The `update` command also updates assembly references in the project file, provided those references already exist.</span></span> <span data-ttu-id="55cb9-110">Wenn ein aktualisiertes Paket über eine hinzugefügte Assembly verfügt, wird *kein* neuer Verweis hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="55cb9-110">If an updated package has an added assembly, a new reference is *not* added.</span></span> <span data-ttu-id="55cb9-111">Neuen Paketabhängigkeiten werden auch keine Assemblyverweise hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="55cb9-111">New package dependencies also don't have their assembly references added.</span></span> <span data-ttu-id="55cb9-112">Um diese Vorgänge als Teil eines Updates einzubeziehen, aktualisieren Sie das Paket in Visual Studio mithilfe der Paket-Manager-Benutzeroberfläche oder der Paket-Manager-Konsole.</span><span class="sxs-lookup"><span data-stu-id="55cb9-112">To include these operations as part of an update, update the package in Visual Studio using the Package Manager UI or the Package Manager Console.</span></span>

<span data-ttu-id="55cb9-113">Dieser Befehl kann auch verwendet werden, um nuget.exe selbst mithilfe des Flags *-self* zu aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="55cb9-113">This command can also be used to update nuget.exe itself using the *-self* flag.</span></span>

## <a name="usage"></a><span data-ttu-id="55cb9-114">Verwendung</span><span class="sxs-lookup"><span data-stu-id="55cb9-114">Usage</span></span>

```cli
nuget update <configPath> [options]
```

<span data-ttu-id="55cb9-115">, wobei `<configPath>` entweder eine `packages.config` Projektmappendatei oder eine Projektmappendatei identifiziert, die die Abhängigkeiten des Projekts auflistet.</span><span class="sxs-lookup"><span data-stu-id="55cb9-115">where `<configPath>` identifies either a `packages.config` or solution file that lists the project's dependencies.</span></span>

## <a name="options"></a><span data-ttu-id="55cb9-116">Optionen</span><span class="sxs-lookup"><span data-stu-id="55cb9-116">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="55cb9-117">Die zu übernehmende NuGet-Konfigurationsdatei.</span><span class="sxs-lookup"><span data-stu-id="55cb9-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="55cb9-118">Wenn keine Angabe erfolgt, `%AppData%\NuGet\NuGet.Config` wird (Windows) `~/.nuget/NuGet/NuGet.Config` oder oder `~/.config/NuGet/NuGet.Config` (Mac/Linux) verwendet.</span><span class="sxs-lookup"><span data-stu-id="55cb9-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>
  
- **`-DependencyVersion [Lowest, HighestPatch, HighestMinor, Highest, Ignore]`**

  <span data-ttu-id="55cb9-119">Gibt die Version der zu verwendenden Abhängigkeitspakete an, die eines der folgenden sein kann:</span><span class="sxs-lookup"><span data-stu-id="55cb9-119">Specifies the version of the dependency packages to use, which can be one of the following:</span></span><br/><ul><li><span data-ttu-id="55cb9-120">*Niedrigste* (Standardeinstellung): die niedrigste Version</span><span class="sxs-lookup"><span data-stu-id="55cb9-120">*Lowest* (default): the lowest version</span></span></li><li><span data-ttu-id="55cb9-121">*HighestPatch:* Die Version mit der niedrigsten Hauptversion, der niedrigsten Nebenversion und dem höchsten Patch</span><span class="sxs-lookup"><span data-stu-id="55cb9-121">*HighestPatch*: the version with the lowest major, lowest minor, highest patch</span></span></li><li><span data-ttu-id="55cb9-122">*HighestMinor:* Die Version mit der niedrigsten Hauptversion, der höchsten Nebenversion und dem höchsten Patch</span><span class="sxs-lookup"><span data-stu-id="55cb9-122">*HighestMinor*: the version with the lowest major, highest minor, highest patch</span></span></li><li><span data-ttu-id="55cb9-123">*Höchste*: die höchste Version</span><span class="sxs-lookup"><span data-stu-id="55cb9-123">*Highest*: the highest version</span></span></li><li><span data-ttu-id="55cb9-124">*Ignorieren:* Es werden keine Abhängigkeitspakete verwendet.</span><span class="sxs-lookup"><span data-stu-id="55cb9-124">*Ignore*: No dependency packages will be used</span></span></li></ul>

- **`-FileConflictAction [PromptUser, Overwrite, Ignore]`**

  <span data-ttu-id="55cb9-125">Gibt die Standardaktion an, wenn eine Datei aus einem Paket bereits im Zielprojekt vorhanden ist.</span><span class="sxs-lookup"><span data-stu-id="55cb9-125">Specifies the default action when a file from a package already exists in the target project.</span></span> <span data-ttu-id="55cb9-126">Legen Sie auf `Overwrite` fest, um Dateien immer zu überschreiben.</span><span class="sxs-lookup"><span data-stu-id="55cb9-126">Set to `Overwrite` to always overwrite files.</span></span> <span data-ttu-id="55cb9-127">Legen Sie auf `Ignore` fest, um Dateien zu überspringen.</span><span class="sxs-lookup"><span data-stu-id="55cb9-127">Set to `Ignore` to skip files.</span></span>

  <span data-ttu-id="55cb9-128">Die `PromptUser` Standardaktion fordert für jede in Konflikt stehende Datei auf, es sei `OverwriteAll` denn, oder `IgnoreAll` wird angegeben, was für alle verbleibenden Dateien gilt.</span><span class="sxs-lookup"><span data-stu-id="55cb9-128">The `PromptUser` action, the default, will prompt for each conflicting file unless `OverwriteAll` or `IgnoreAll` is provided, which will apply to all remaining files.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="55cb9-129">*(3.5+)* Erzwingt die Ausführung nuget.exe mithilfe einer invarianten, englischsprachigen Kultur.</span><span class="sxs-lookup"><span data-stu-id="55cb9-129">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="55cb9-130">Zeigt Hilfeinformationen für den Befehl an.</span><span class="sxs-lookup"><span data-stu-id="55cb9-130">Displays help information for the command.</span></span>

- **`-Id`**

  <span data-ttu-id="55cb9-131">Gibt eine Liste der zu aktualisierenden Paket-IDs an.</span><span class="sxs-lookup"><span data-stu-id="55cb9-131">Specifies a list of package IDs to update.</span></span>

- **`-MSBuildPath`**

  <span data-ttu-id="55cb9-132">*(4.0+)* Gibt den Pfad von MSBuild an, der mit dem Befehl verwendet werden soll, und hat Vorrang vor `-MSBuildVersion` .</span><span class="sxs-lookup"><span data-stu-id="55cb9-132">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span>

- **`-MSBuildVersion`**

  <span data-ttu-id="55cb9-133">*(3.2+)* Gibt die Version von MSBuild an, die mit diesem Befehl verwendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="55cb9-133">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="55cb9-134">Unterstützte Werte sind 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9.</span><span class="sxs-lookup"><span data-stu-id="55cb9-134">Supported values are 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9.</span></span> <span data-ttu-id="55cb9-135">Standardmäßig wird MSBuild in Ihrem Pfad ausgewählt, andernfalls wird standardmäßig die höchste installierte Version von MSBuild verwendet.</span><span class="sxs-lookup"><span data-stu-id="55cb9-135">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="55cb9-136">Unterdrückt Aufforderungen zu Benutzereingaben oder Bestätigungen.</span><span class="sxs-lookup"><span data-stu-id="55cb9-136">Suppresses prompts for user input or confirmations.</span></span>

- **`-PreRelease`**

  <span data-ttu-id="55cb9-137">Ermöglicht das Aktualisieren auf Vorabversionen.</span><span class="sxs-lookup"><span data-stu-id="55cb9-137">Allows updating to prerelease versions.</span></span> <span data-ttu-id="55cb9-138">Dieses Flag ist nicht erforderlich, wenn Vorabversionspakete aktualisiert werden, die bereits installiert sind.</span><span class="sxs-lookup"><span data-stu-id="55cb9-138">This flag is not required when updating prerelease packages that are already installed.</span></span>

- **`-RepositoryPath`**

  <span data-ttu-id="55cb9-139">Gibt den lokalen Ordner an, in dem Pakete installiert werden.</span><span class="sxs-lookup"><span data-stu-id="55cb9-139">Specifies the local folder where packages are installed.</span></span>

- **`-Safe`**

  <span data-ttu-id="55cb9-140">Gibt an, dass nur Updates mit der höchsten verfügbaren Version innerhalb der gleichen Haupt- und Nebenversion wie das installierte Paket installiert werden.</span><span class="sxs-lookup"><span data-stu-id="55cb9-140">Specifies that only updates with the highest version available within the same major and minor version as the installed package will be installed.</span></span>

- **`-Self`**

  <span data-ttu-id="55cb9-141">Updates `nuget.exe` auf die neueste Version.</span><span class="sxs-lookup"><span data-stu-id="55cb9-141">Updates `nuget.exe` to the latest version.</span></span> <span data-ttu-id="55cb9-142">`-Source` kann verwendet werden, aber alle anderen Argumente werden ignoriert.</span><span class="sxs-lookup"><span data-stu-id="55cb9-142">`-Source` can be used however all other arguments are ignored.</span></span> <span data-ttu-id="55cb9-143">Wenn keine Quelle bereitgestellt wird, wird unabhängig von den Einstellungen nach `nuget.org` Updates `NuGet.Config` gesucht.</span><span class="sxs-lookup"><span data-stu-id="55cb9-143">If no source is provided, checks `nuget.org` for updates regardless of `NuGet.Config` settings.</span></span>

- **`-Source`**

  <span data-ttu-id="55cb9-144">Gibt die Liste der Paketquellen (als URLs) an, die für die Updates verwendet werden sollen.</span><span class="sxs-lookup"><span data-stu-id="55cb9-144">Specifies the list of package sources (as URLs) to use for the updates.</span></span> <span data-ttu-id="55cb9-145">Wenn diese Angabe nicht erfolgt, verwendet der Befehl die in Konfigurationsdateien bereitgestellten Quellen. Weitere Informationen finden Sie unter [Allgemeine NuGet-Konfigurationen.](../../consume-packages/configuring-nuget-behavior.md)</span><span class="sxs-lookup"><span data-stu-id="55cb9-145">If omitted, the command uses the sources provided in configuration files, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="55cb9-146">Gibt die Detailmenge an, die in der Ausgabe angezeigt wird: `normal` (Standard), `quiet` oder `detailed` .</span><span class="sxs-lookup"><span data-stu-id="55cb9-146">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

- **`-Version`**

  <span data-ttu-id="55cb9-147">Gibt bei Verwendung mit einer Paket-ID die Version des zu aktualisierenden Pakets an.</span><span class="sxs-lookup"><span data-stu-id="55cb9-147">When used with one package ID, specifies the version of the package to update.</span></span>

<span data-ttu-id="55cb9-148">Siehe auch [Umgebungsvariablen.](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="55cb9-148">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="55cb9-149">Beispiele</span><span class="sxs-lookup"><span data-stu-id="55cb9-149">Examples</span></span>

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
