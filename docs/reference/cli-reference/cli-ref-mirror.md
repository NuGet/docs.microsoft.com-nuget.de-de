---
title: Befehl "nuget CLI-Spiegel"
description: Referenz für den Befehl "nuget. exe"
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 076d7a480e2f07149e4ec7ac58c7ab37040e7a8f
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327667"
---
# <a name="mirror-command-nuget-cli"></a><span data-ttu-id="cf7d5-103">Der Befehl „mirror“ (NuGet-CLI)</span><span class="sxs-lookup"><span data-stu-id="cf7d5-103">mirror command (NuGet CLI)</span></span>

<span data-ttu-id="cf7d5-104">**Gilt für:** &bullet; **unterstützte Versionen** der Paket Veröffentlichung: veraltet in 3.2 +</span><span class="sxs-lookup"><span data-stu-id="cf7d5-104">**Applies to:** package publishing &bullet; **Supported versions:** deprecated in 3.2+</span></span>

<span data-ttu-id="cf7d5-105">Spiegelt ein Paket und seine Abhängigkeiten aus den angegebenen quelldepots in das Zielrepository ein.</span><span class="sxs-lookup"><span data-stu-id="cf7d5-105">Mirrors a package and its dependencies from the specified source repositories to the target repository.</span></span>

> [!NOTE]
> <span data-ttu-id="cf7d5-106">Wenn Sie diesen Befehl für nuget-Versionen vor 3,2 aktivieren möchten [https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases), klicken Sie auf, wählen Sie die neueste `Nuget-Signed.exe` stabile Version aus, und laden `Nuget-Signed.exe` Sie `nuget.exe` Sie auf Ihren lokalen Datenträger herunter `NuGet.ServerExtensions.dll` .</span><span class="sxs-lookup"><span data-stu-id="cf7d5-106">To enable this command for NuGet versions before 3.2, go to [https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases), select the newest stable release, download `NuGet.ServerExtensions.dll` and `Nuget-Signed.exe` to your local disk and rename `Nuget-Signed.exe` to `nuget.exe`.</span></span>

## <a name="usage"></a><span data-ttu-id="cf7d5-107">Verwendung</span><span class="sxs-lookup"><span data-stu-id="cf7d5-107">Usage</span></span>

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

<span data-ttu-id="cf7d5-108">gibt `<packageID>` an, wo das zu spiegelnde `<configFilePath>` Paket ist `packages.config` , oder identifiziert die Datei, die die zu spiegelnden Pakete auflistet.</span><span class="sxs-lookup"><span data-stu-id="cf7d5-108">where `<packageID>` is the package to mirror, or `<configFilePath>` identifies the `packages.config` file that lists the packages to mirror.</span></span>

<span data-ttu-id="cf7d5-109">Der `<listUrlTarget>` gibt das Quellrepository an und `<publishUrlTarget>` gibt das Zielrepository an.</span><span class="sxs-lookup"><span data-stu-id="cf7d5-109">The `<listUrlTarget>` specifies the source repository, and `<publishUrlTarget>` specifies the target repository.</span></span>

<span data-ttu-id="cf7d5-110">Wenn Ihr Zielrepository auf ist `https://machine/repo` , die ausgeführt wird [NuGet.Server in](../../hosting-packages/nuget-server.md), Liste und Push-URLs `https://machine/repo/nuget` und `https://machine/repo/api/v2/package`bzw.</span><span class="sxs-lookup"><span data-stu-id="cf7d5-110">If your target repository is on `https://machine/repo` that's running [NuGet.Server](../../hosting-packages/nuget-server.md), the list and push urls will be `https://machine/repo/nuget` and `https://machine/repo/api/v2/package`, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="cf7d5-111">Optionen</span><span class="sxs-lookup"><span data-stu-id="cf7d5-111">Options</span></span>

| <span data-ttu-id="cf7d5-112">Option</span><span class="sxs-lookup"><span data-stu-id="cf7d5-112">Option</span></span> | <span data-ttu-id="cf7d5-113">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="cf7d5-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="cf7d5-114">ApiKey</span><span class="sxs-lookup"><span data-stu-id="cf7d5-114">ApiKey</span></span> | <span data-ttu-id="cf7d5-115">Der API-Schlüssel für das Zielrepository.</span><span class="sxs-lookup"><span data-stu-id="cf7d5-115">The API key for the target repository.</span></span> <span data-ttu-id="cf7d5-116">Wenn Sie nicht vorhanden ist, wird die in der Konfigurationsdatei angegebene verwendet`%AppData%\NuGet\NuGet.Config` ((Windows) `~/.nuget/NuGet/NuGet.Config` oder (Mac/Linux)).</span><span class="sxs-lookup"><span data-stu-id="cf7d5-116">If not present,  the one specified in the config file is used (`%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span></span> |
| <span data-ttu-id="cf7d5-117">Help</span><span class="sxs-lookup"><span data-stu-id="cf7d5-117">Help</span></span> | <span data-ttu-id="cf7d5-118">Zeigt Hilfe Informationen für den Befehl an.</span><span class="sxs-lookup"><span data-stu-id="cf7d5-118">Displays help information for the command.</span></span> |
| <span data-ttu-id="cf7d5-119">NoCache</span><span class="sxs-lookup"><span data-stu-id="cf7d5-119">NoCache</span></span> | <span data-ttu-id="cf7d5-120">Verhindert, dass nuget zwischengespeicherte Pakete verwendet.</span><span class="sxs-lookup"><span data-stu-id="cf7d5-120">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="cf7d5-121">Weitere Informationen finden Sie [unter Verwalten der globalen Pakete und Cache Ordner](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="cf7d5-121">See [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="cf7d5-122">NOOP</span><span class="sxs-lookup"><span data-stu-id="cf7d5-122">Noop</span></span> | <span data-ttu-id="cf7d5-123">Protokolliert, was geschehen würde, führt die Aktionen jedoch nicht aus. nimmt die erfolgreiche Ausführung von pushvorgängen an.</span><span class="sxs-lookup"><span data-stu-id="cf7d5-123">Logs what would be done but does not perform the actions; assumes success for push operations.</span></span> |
| <span data-ttu-id="cf7d5-124">Vorab</span><span class="sxs-lookup"><span data-stu-id="cf7d5-124">PreRelease</span></span> | <span data-ttu-id="cf7d5-125">Schließt vorab Pakete in den Spiegelungs Vorgang ein.</span><span class="sxs-lookup"><span data-stu-id="cf7d5-125">Includes prerelease packages in the mirroring operation.</span></span> |
| <span data-ttu-id="cf7d5-126">Source</span><span class="sxs-lookup"><span data-stu-id="cf7d5-126">Source</span></span> | <span data-ttu-id="cf7d5-127">Eine Liste der zu spiegelnden Paketquellen.</span><span class="sxs-lookup"><span data-stu-id="cf7d5-127">A list of package sources to mirror.</span></span> <span data-ttu-id="cf7d5-128">Wenn keine Quellen angegeben sind, werden die in der Konfigurationsdatei definierten (siehe APIKey oben) verwendet, wobei "nuget.org" verwendet wird, wenn keine Daten angegeben sind.</span><span class="sxs-lookup"><span data-stu-id="cf7d5-128">If no sources are specified, the ones defined in the config file (see ApiKey above) are used, defaulting to nuget.org if none are specified.</span></span> |
| <span data-ttu-id="cf7d5-129">Timeout</span><span class="sxs-lookup"><span data-stu-id="cf7d5-129">Timeout</span></span> | <span data-ttu-id="cf7d5-130">Gibt den Timeout Wert (in Sekunden) für das Push an einen Server an.</span><span class="sxs-lookup"><span data-stu-id="cf7d5-130">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="cf7d5-131">Der Standardwert ist 300 Sekunden (5 Minuten).</span><span class="sxs-lookup"><span data-stu-id="cf7d5-131">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="cf7d5-132">Version</span><span class="sxs-lookup"><span data-stu-id="cf7d5-132">Version</span></span> | <span data-ttu-id="cf7d5-133">Die Version des zu installierenden Pakets.</span><span class="sxs-lookup"><span data-stu-id="cf7d5-133">The version of the package to install.</span></span> <span data-ttu-id="cf7d5-134">Wenn nicht angegeben, wird die aktuelle Version gespiegelt.</span><span class="sxs-lookup"><span data-stu-id="cf7d5-134">If not specified, the latest version is mirrored.</span></span> |

<span data-ttu-id="cf7d5-135">Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="cf7d5-135">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="cf7d5-136">Beispiele</span><span class="sxs-lookup"><span data-stu-id="cf7d5-136">Examples</span></span>

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
