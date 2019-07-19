---
title: Befehl "nuget CLI-Update"
description: Referenz für den Befehl "nuget. exe Update"
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: b5da09c3dd6ffa0ce1b7b44731ed67ddd0336c58
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327507"
---
# <a name="update-command-nuget-cli"></a><span data-ttu-id="cef7f-103">Der Befehl „commnad“ (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="cef7f-103">update command (NuGet CLI)</span></span>

<span data-ttu-id="cef7f-104">**Gilt für:** &bullet; **unterstützte Versionen** von Paket Verbrauch: alle</span><span class="sxs-lookup"><span data-stu-id="cef7f-104">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="cef7f-105">Alle Pakete in einem Projekt werden (unter Verwendung von `packages.config`) auf die neuesten verfügbaren Versionen aktualisiert.</span><span class="sxs-lookup"><span data-stu-id="cef7f-105">Updates all packages in a project (using `packages.config`) to their latest available versions.</span></span> <span data-ttu-id="cef7f-106">Es wird empfohlen, ["Restore"](cli-ref-restore.md) auszuführen, bevor Sie `update`ausführen.</span><span class="sxs-lookup"><span data-stu-id="cef7f-106">It is recommended to run ['restore'](cli-ref-restore.md) before running the `update`.</span></span> <span data-ttu-id="cef7f-107">(Um ein einzelnes Paket zu aktualisieren, [`nuget install`](cli-ref-install.md) verwenden Sie, ohne eine Versionsnummer anzugeben. in diesem Fall installiert nuget die neueste Version.)</span><span class="sxs-lookup"><span data-stu-id="cef7f-107">(To update an individual package, use [`nuget install`](cli-ref-install.md) without specifying a version number, in which case NuGet installs the latest version.)</span></span>

<span data-ttu-id="cef7f-108">Hinweis: `update` funktioniert nicht mit der CLI, die unter Mono (Mac OSX oder Linux) ausgeführt wird, oder wenn das packagereferenzierungsformat verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="cef7f-108">Note: `update` does not work with the CLI running under Mono (Mac OSX or Linux) or when using the PackageReference format.</span></span>

<span data-ttu-id="cef7f-109">Der `update` Befehl aktualisiert außerdem Assemblyverweise in der Projektdatei, sofern diese Verweise bereits vorhanden sind.</span><span class="sxs-lookup"><span data-stu-id="cef7f-109">The `update` command also updates assembly references in the project file, provided those references already exist.</span></span> <span data-ttu-id="cef7f-110">Wenn ein aktualisiertes Paket über eine hinzugefügte Assembly verfügt, wird *kein* neuer Verweis hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="cef7f-110">If an updated package has an added assembly, a new reference is *not* added.</span></span> <span data-ttu-id="cef7f-111">Neuen Paketabhängigkeiten werden auch keine Assemblyverweise hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="cef7f-111">New package dependencies also don't have their assembly references added.</span></span> <span data-ttu-id="cef7f-112">Aktualisieren Sie das Paket in Visual Studio mithilfe der Benutzeroberfläche des Paket-Managers oder der Paket-Manager-Konsole, um diese Vorgänge als Teil eines Updates einzuschließen.</span><span class="sxs-lookup"><span data-stu-id="cef7f-112">To include these operations as part of an update, update the package in Visual Studio using the Package Manager UI or the Package Manager Console.</span></span>

<span data-ttu-id="cef7f-113">Dieser Befehl kann auch verwendet werden, um nuget. exe selbst mit dem *-Self-* Flag zu aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="cef7f-113">This command can also be used to update nuget.exe itself using the *-self* flag.</span></span>

## <a name="usage"></a><span data-ttu-id="cef7f-114">Verwendung</span><span class="sxs-lookup"><span data-stu-id="cef7f-114">Usage</span></span>

```cli
nuget update <configPath> [options]
```

<span data-ttu-id="cef7f-115">Dabei identifiziert entweder eine `packages.config` oder eine Projektmappendatei, die die Abhängigkeiten des Projekts auflistet. `<configPath>`</span><span class="sxs-lookup"><span data-stu-id="cef7f-115">where `<configPath>` identifies either a `packages.config` or solution file that lists the project's dependencies.</span></span>

## <a name="options"></a><span data-ttu-id="cef7f-116">Optionen</span><span class="sxs-lookup"><span data-stu-id="cef7f-116">Options</span></span>

| <span data-ttu-id="cef7f-117">Option</span><span class="sxs-lookup"><span data-stu-id="cef7f-117">Option</span></span> | <span data-ttu-id="cef7f-118">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="cef7f-118">Description</span></span> |
| --- | --- |
| <span data-ttu-id="cef7f-119">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="cef7f-119">ConfigFile</span></span> | <span data-ttu-id="cef7f-120">Die anzuwendende nuget-Konfigurationsdatei.</span><span class="sxs-lookup"><span data-stu-id="cef7f-120">The NuGet configuration file to apply.</span></span> <span data-ttu-id="cef7f-121">Wenn nichts angegeben ist `%AppData%\NuGet\NuGet.Config` , wird (Windows `~/.nuget/NuGet/NuGet.Config` ) oder (Mac/Linux) verwendet.</span><span class="sxs-lookup"><span data-stu-id="cef7f-121">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="cef7f-122">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="cef7f-122">FileConflictAction</span></span> | <span data-ttu-id="cef7f-123">Gibt die Aktion an, die ausgeführt werden soll, wenn die vom Projekt referenzierten Dateien überschrieben oder ignoriert werden sollen.</span><span class="sxs-lookup"><span data-stu-id="cef7f-123">Specifies the action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="cef7f-124">Werte sind über *schreiben, ignorieren, keine*.</span><span class="sxs-lookup"><span data-stu-id="cef7f-124">Values are *overwrite, ignore, none*.</span></span> |
| <span data-ttu-id="cef7f-125">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="cef7f-125">ForceEnglishOutput</span></span> | <span data-ttu-id="cef7f-126">*(3.5* und höher) Erzwingt, dass "nuget. exe" mit einer invarianten, englischen Kultur ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="cef7f-126">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="cef7f-127">Help</span><span class="sxs-lookup"><span data-stu-id="cef7f-127">Help</span></span> | <span data-ttu-id="cef7f-128">Zeigt Hilfe Informationen für den Befehl an.</span><span class="sxs-lookup"><span data-stu-id="cef7f-128">Displays help information for the command.</span></span> |
| <span data-ttu-id="cef7f-129">Id</span><span class="sxs-lookup"><span data-stu-id="cef7f-129">Id</span></span> | <span data-ttu-id="cef7f-130">Gibt eine Liste der zu aktualisierenden Paket-IDs an.</span><span class="sxs-lookup"><span data-stu-id="cef7f-130">Specifies a list of package IDs to update.</span></span> |
| <span data-ttu-id="cef7f-131">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="cef7f-131">MSBuildPath</span></span> | <span data-ttu-id="cef7f-132">*(4.0* und höher) Gibt den Pfad von MSBuild an, der mit dem Befehl verwendet werden soll `-MSBuildVersion`, und hat Vorrang vor.</span><span class="sxs-lookup"><span data-stu-id="cef7f-132">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="cef7f-133">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="cef7f-133">MSBuildVersion</span></span> | <span data-ttu-id="cef7f-134">*(3.2 +)* Gibt die Version von MSBuild an, die mit diesem Befehl verwendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="cef7f-134">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="cef7f-135">Unterstützte Werte sind 4, 12, 14, 15,1, 15,3, 15,4, 15,5, 15,6, 15,7, 15,8, 15,9.</span><span class="sxs-lookup"><span data-stu-id="cef7f-135">Supported values are 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9.</span></span> <span data-ttu-id="cef7f-136">Standardmäßig wird der MSBuild in Ihrem Pfad ausgewählt; andernfalls wird standardmäßig die höchste installierte Version von MSBuild verwendet.</span><span class="sxs-lookup"><span data-stu-id="cef7f-136">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="cef7f-137">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="cef7f-137">NonInteractive</span></span> | <span data-ttu-id="cef7f-138">Unterdrückt Eingabe Aufforderungen für Benutzereingaben oder Bestätigungen.</span><span class="sxs-lookup"><span data-stu-id="cef7f-138">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="cef7f-139">Vorab</span><span class="sxs-lookup"><span data-stu-id="cef7f-139">PreRelease</span></span> | <span data-ttu-id="cef7f-140">Ermöglicht das Aktualisieren von vorab Versionen.</span><span class="sxs-lookup"><span data-stu-id="cef7f-140">Allows updating to prerelease versions.</span></span> <span data-ttu-id="cef7f-141">Dieses Flag ist beim Aktualisieren bereits installierter vorab Pakete nicht erforderlich.</span><span class="sxs-lookup"><span data-stu-id="cef7f-141">This flag is not required when updating prerelease packages that are already installed.</span></span> |
| <span data-ttu-id="cef7f-142">RepositoryPath</span><span class="sxs-lookup"><span data-stu-id="cef7f-142">RepositoryPath</span></span> | <span data-ttu-id="cef7f-143">Gibt den lokalen Ordner an, in dem Pakete installiert werden.</span><span class="sxs-lookup"><span data-stu-id="cef7f-143">Specifies the local folder where packages are installed.</span></span> |
| <span data-ttu-id="cef7f-144">Sauberem</span><span class="sxs-lookup"><span data-stu-id="cef7f-144">Safe</span></span> | <span data-ttu-id="cef7f-145">Gibt an, dass nur Updates mit der höchsten Version, die innerhalb derselben Haupt-und neben Version wie das installierte Paket verfügbar ist, installiert werden.</span><span class="sxs-lookup"><span data-stu-id="cef7f-145">Specifies that only updates with the highest version available within the same major and minor version as the installed package will be installed.</span></span> |
| <span data-ttu-id="cef7f-146">Selbstbedienungs</span><span class="sxs-lookup"><span data-stu-id="cef7f-146">Self</span></span> | <span data-ttu-id="cef7f-147">Aktualisiert "nuget. exe" auf die neueste Version. alle anderen Argumente werden ignoriert.</span><span class="sxs-lookup"><span data-stu-id="cef7f-147">Updates nuget.exe to the latest version; all other arguments are ignored.</span></span> |
| <span data-ttu-id="cef7f-148">Source</span><span class="sxs-lookup"><span data-stu-id="cef7f-148">Source</span></span> | <span data-ttu-id="cef7f-149">Gibt die Liste der Paketquellen (als URLs) an, die für die Updates verwendet werden sollen.</span><span class="sxs-lookup"><span data-stu-id="cef7f-149">Specifies the list of package sources (as URLs) to use for the updates.</span></span> <span data-ttu-id="cef7f-150">Wenn der Befehl nicht angegeben wird, verwendet der Befehl die in den Konfigurationsdateien bereitgestellten Quellen, siehe [Allgemeine nuget-Konfigurationen](../../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="cef7f-150">If omitted, the command uses the sources provided in configuration files, see [Common NuGet configurations](../../consume-packages/configuring-nuget-behavior.md).</span></span> |
| <span data-ttu-id="cef7f-151">Verbosity</span><span class="sxs-lookup"><span data-stu-id="cef7f-151">Verbosity</span></span> | <span data-ttu-id="cef7f-152">Gibt den Umfang der in der Ausgabe angezeigten Details an: *Normal*, *quiet*, *ausführlich*.</span><span class="sxs-lookup"><span data-stu-id="cef7f-152">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |
| <span data-ttu-id="cef7f-153">Version</span><span class="sxs-lookup"><span data-stu-id="cef7f-153">Version</span></span> | <span data-ttu-id="cef7f-154">Gibt bei Verwendung mit einer Paket-ID die Version des zu aktualisierenden Pakets an.</span><span class="sxs-lookup"><span data-stu-id="cef7f-154">When used with one package ID, specifies the version of the package to update.</span></span> |

<span data-ttu-id="cef7f-155">Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="cef7f-155">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="cef7f-156">Beispiele</span><span class="sxs-lookup"><span data-stu-id="cef7f-156">Examples</span></span>

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
