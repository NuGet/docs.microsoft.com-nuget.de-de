---
title: NuGet-CLI-Befehl "Update"
description: Referenz für die nuget.exe-Update-Befehl
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: a242d02a54fd86899cbe274ab63538b53307c1bb
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/28/2019
ms.locfileid: "67425920"
---
# <a name="update-command-nuget-cli"></a><span data-ttu-id="b4119-103">Der Befehl „commnad“ (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="b4119-103">update command (NuGet CLI)</span></span>

<span data-ttu-id="b4119-104">**Gilt für:** Paket Verbrauch &bullet; **unterstützte Versionen:** alle</span><span class="sxs-lookup"><span data-stu-id="b4119-104">**Applies to:** package consumption &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="b4119-105">Alle Pakete in einem Projekt aktualisiert (mit `packages.config`) auf ihren aktuellen verfügbaren Versionen.</span><span class="sxs-lookup"><span data-stu-id="b4119-105">Updates all packages in a project (using `packages.config`) to their latest available versions.</span></span> <span data-ttu-id="b4119-106">Es wird empfohlen, führen Sie ['Wiederherstellen'](cli-ref-restore.md) vor dem Ausführen der `update`.</span><span class="sxs-lookup"><span data-stu-id="b4119-106">It is recommended to run ['restore'](cli-ref-restore.md) before running the `update`.</span></span> <span data-ttu-id="b4119-107">(Verwenden Sie zum Aktualisieren eines einzelnen Pakets [ `nuget install` ](cli-ref-install.md) ohne Angabe einer Versionsnummer, die in der Groß-/Kleinschreibung von NuGet die neueste Version installiert.)</span><span class="sxs-lookup"><span data-stu-id="b4119-107">(To update an individual package, use [`nuget install`](cli-ref-install.md) without specifying a version number, in which case NuGet installs the latest version.)</span></span>

<span data-ttu-id="b4119-108">Hinweis: `update` funktioniert nicht mit der Befehlszeilenschnittstelle, die unter Mono (Mac OS x oder Linux) oder wenn das PackageReference-Format verwenden.</span><span class="sxs-lookup"><span data-stu-id="b4119-108">Note: `update` does not work with the CLI running under Mono (Mac OSX or Linux) or when using the PackageReference format.</span></span>

<span data-ttu-id="b4119-109">Die `update` Befehl aktualisiert auch die Verweise der Assembly in der Projektdatei, vorausgesetzt die verweist bereits vorhanden.</span><span class="sxs-lookup"><span data-stu-id="b4119-109">The `update` command also updates assembly references in the project file, provided those references already exist.</span></span> <span data-ttu-id="b4119-110">Wenn ein aktualisiertes Paket eine hinzugefügte Assembly hat, ist ein neuer Verweis *nicht* hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="b4119-110">If an updated package has an added assembly, a new reference is *not* added.</span></span> <span data-ttu-id="b4119-111">Ferner müssen neue paketabhängigkeiten nicht ihre Assemblyverweise hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="b4119-111">New package dependencies also don't have their assembly references added.</span></span> <span data-ttu-id="b4119-112">Aktualisieren Sie das Paket in Visual Studio mithilfe der Paket-Manager-UI oder der Paket-Manager-Konsole, um diese Vorgänge im Rahmen eines Updates einzuschließen.</span><span class="sxs-lookup"><span data-stu-id="b4119-112">To include these operations as part of an update, update the package in Visual Studio using the Package Manager UI or the Package Manager Console.</span></span>

<span data-ttu-id="b4119-113">Mit diesem Befehl kann auch verwendet werden, um nuget.exe selbst aktualisieren mit der *-Self-Service* Flag.</span><span class="sxs-lookup"><span data-stu-id="b4119-113">This command can also be used to update nuget.exe itself using the *-self* flag.</span></span>

## <a name="usage"></a><span data-ttu-id="b4119-114">Verwendung</span><span class="sxs-lookup"><span data-stu-id="b4119-114">Usage</span></span>

```cli
nuget update <configPath> [options]
```

<span data-ttu-id="b4119-115">in denen `<configPath>` identifiziert entweder eine `packages.config` oder Projektmappendatei, die die Abhängigkeiten des Projekts aufgeführt.</span><span class="sxs-lookup"><span data-stu-id="b4119-115">where `<configPath>` identifies either a `packages.config` or solution file that lists the project's dependencies.</span></span>

## <a name="options"></a><span data-ttu-id="b4119-116">Optionen</span><span class="sxs-lookup"><span data-stu-id="b4119-116">Options</span></span>

| <span data-ttu-id="b4119-117">Option</span><span class="sxs-lookup"><span data-stu-id="b4119-117">Option</span></span> | <span data-ttu-id="b4119-118">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="b4119-118">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b4119-119">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="b4119-119">ConfigFile</span></span> | <span data-ttu-id="b4119-120">Die NuGet-Konfigurationsdatei angewendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="b4119-120">The NuGet configuration file to apply.</span></span> <span data-ttu-id="b4119-121">Wenn nicht angegeben, `%AppData%\NuGet\NuGet.Config` (Windows) oder `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="b4119-121">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="b4119-122">FileConflictAction</span><span class="sxs-lookup"><span data-stu-id="b4119-122">FileConflictAction</span></span> | <span data-ttu-id="b4119-123">Gibt die Aktion an, wenn Sie gefragt werden, überschrieben werden soll, oder ignorieren die vorhandene Dateien, die vom Projekt verwiesen wird.</span><span class="sxs-lookup"><span data-stu-id="b4119-123">Specifies the action to take when asked to overwrite or ignore existing files referenced by the project.</span></span> <span data-ttu-id="b4119-124">Werte sind *überschrieben werden soll, zu ignorieren, keine*.</span><span class="sxs-lookup"><span data-stu-id="b4119-124">Values are *overwrite, ignore, none*.</span></span> |
| <span data-ttu-id="b4119-125">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="b4119-125">ForceEnglishOutput</span></span> | <span data-ttu-id="b4119-126">*(3.5 und höher)*  Erzwingt nuget.exe über eine invariante Kultur auf Englisch basierenden ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="b4119-126">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="b4119-127">Help</span><span class="sxs-lookup"><span data-stu-id="b4119-127">Help</span></span> | <span data-ttu-id="b4119-128">Zeigt die Informationen für den Befehl Hilfe.</span><span class="sxs-lookup"><span data-stu-id="b4119-128">Displays help information for the command.</span></span> |
| <span data-ttu-id="b4119-129">Id</span><span class="sxs-lookup"><span data-stu-id="b4119-129">Id</span></span> | <span data-ttu-id="b4119-130">Gibt eine Liste der Paket-IDs zu aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="b4119-130">Specifies a list of package IDs to update.</span></span> |
| <span data-ttu-id="b4119-131">MSBuildPath</span><span class="sxs-lookup"><span data-stu-id="b4119-131">MSBuildPath</span></span> | <span data-ttu-id="b4119-132">*(4.0 und höher)*  Gibt den Pfad des MSBuild für die Verwendung mit dem Befehl vor `-MSBuildVersion`.</span><span class="sxs-lookup"><span data-stu-id="b4119-132">*(4.0+)* Specifies the path of MSBuild to use with the command, taking precedence over `-MSBuildVersion`.</span></span> |
| <span data-ttu-id="b4119-133">MSBuildVersion</span><span class="sxs-lookup"><span data-stu-id="b4119-133">MSBuildVersion</span></span> | <span data-ttu-id="b4119-134">*(3.2 und höher)*  Gibt die Version von MSBuild mit dem folgenden Befehl verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="b4119-134">*(3.2+)* Specifies the version of MSBuild to be used with this command.</span></span> <span data-ttu-id="b4119-135">Unterstützte Werte sind 4, 12, 14, 15.1, 15.3, Version 15.4, Version 15.5, 15.6, 15.7, 15.8, 15.9.</span><span class="sxs-lookup"><span data-stu-id="b4119-135">Supported values are 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9.</span></span> <span data-ttu-id="b4119-136">Standardmäßig die MSBuild in Ihrem Pfad ausgewählt wird, wird standardmäßig andernfalls die neueste installierte Version von MSBuild.</span><span class="sxs-lookup"><span data-stu-id="b4119-136">By default the MSBuild in your path is picked, otherwise it defaults to the highest installed version of MSBuild.</span></span> |
| <span data-ttu-id="b4119-137">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="b4119-137">NonInteractive</span></span> | <span data-ttu-id="b4119-138">Unterdrückt aufforderungen für Benutzereingaben oder Bestätigungen an.</span><span class="sxs-lookup"><span data-stu-id="b4119-138">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="b4119-139">PreRelease</span><span class="sxs-lookup"><span data-stu-id="b4119-139">PreRelease</span></span> | <span data-ttu-id="b4119-140">Ermöglicht das Aktualisieren auf Vorabversionen.</span><span class="sxs-lookup"><span data-stu-id="b4119-140">Allows updating to prerelease versions.</span></span> <span data-ttu-id="b4119-141">Dieses Flag ist nicht erforderlich, beim Aktualisieren von Vorabversionen von Paketen, die bereits installiert sind.</span><span class="sxs-lookup"><span data-stu-id="b4119-141">This flag is not required when updating prerelease packages that are already installed.</span></span> |
| <span data-ttu-id="b4119-142">RepositoryPath</span><span class="sxs-lookup"><span data-stu-id="b4119-142">RepositoryPath</span></span> | <span data-ttu-id="b4119-143">Gibt den lokalen Ordner, in dem Pakete installiert sind.</span><span class="sxs-lookup"><span data-stu-id="b4119-143">Specifies the local folder where packages are installed.</span></span> |
| <span data-ttu-id="b4119-144">Safe</span><span class="sxs-lookup"><span data-stu-id="b4119-144">Safe</span></span> | <span data-ttu-id="b4119-145">Gibt an, dass nur mit der höchsten Version innerhalb der gleichen Haupt- und Nebenversionsnummern Version verfügbaren updates wie das installierte Paket installiert wird.</span><span class="sxs-lookup"><span data-stu-id="b4119-145">Specifies that only updates with the highest version available within the same major and minor version as the installed package will be installed.</span></span> |
| <span data-ttu-id="b4119-146">Self-Service</span><span class="sxs-lookup"><span data-stu-id="b4119-146">Self</span></span> | <span data-ttu-id="b4119-147">Nuget.exe auf die neueste Version aktualisiert wird; Alle anderen Argumente werden ignoriert.</span><span class="sxs-lookup"><span data-stu-id="b4119-147">Updates nuget.exe to the latest version; all other arguments are ignored.</span></span> |
| <span data-ttu-id="b4119-148">Source</span><span class="sxs-lookup"><span data-stu-id="b4119-148">Source</span></span> | <span data-ttu-id="b4119-149">Gibt die Liste der Paketquellen (wie URLs), um nach Updates verwenden.</span><span class="sxs-lookup"><span data-stu-id="b4119-149">Specifies the list of package sources (as URLs) to use for the updates.</span></span> <span data-ttu-id="b4119-150">Wenn nicht angegeben, wird der Befehl verwendet die Quellen in Konfigurationsdateien, finden Sie unter [häufig auftretenden NuGet Konfigurationen](../consume-packages/configuring-nuget-behavior.md).</span><span class="sxs-lookup"><span data-stu-id="b4119-150">If omitted, the command uses the sources provided in configuration files, see [Common NuGet configurations](../consume-packages/configuring-nuget-behavior.md).</span></span> |
| <span data-ttu-id="b4119-151">Verbosity</span><span class="sxs-lookup"><span data-stu-id="b4119-151">Verbosity</span></span> | <span data-ttu-id="b4119-152">Gibt an, die Anzahl der Details in der Ausgabe angezeigt: *normalen*, *quiet*, *ausführliche*.</span><span class="sxs-lookup"><span data-stu-id="b4119-152">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |
| <span data-ttu-id="b4119-153">Version</span><span class="sxs-lookup"><span data-stu-id="b4119-153">Version</span></span> | <span data-ttu-id="b4119-154">Bei Verwendung mit einem Paket-ID gibt die Version des Pakets aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="b4119-154">When used with one package ID, specifies the version of the package to update.</span></span> |

<span data-ttu-id="b4119-155">Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="b4119-155">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="b4119-156">Beispiele</span><span class="sxs-lookup"><span data-stu-id="b4119-156">Examples</span></span>

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
