---
title: Befehl "nuget CLI-Spiegel"
description: Referenz für den Befehl "nuget. exe"
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 81866172bfbf55c42ee96c213c0117f1f986235c
ms.sourcegitcommit: 9803981c90a1ed954dc11ed71731264c0e75ea0a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/12/2019
ms.locfileid: "68959714"
---
# <a name="mirror-command-nuget-cli"></a><span data-ttu-id="d97fd-103">Der Befehl „mirror“ (NuGet-CLI)</span><span class="sxs-lookup"><span data-stu-id="d97fd-103">mirror command (NuGet CLI)</span></span>

<span data-ttu-id="d97fd-104">**Gilt für:** &bullet; **unterstützte Versionen** der Paket Veröffentlichung: veraltet in 3.2 +</span><span class="sxs-lookup"><span data-stu-id="d97fd-104">**Applies to:** package publishing &bullet; **Supported versions:** deprecated in 3.2+</span></span>

<span data-ttu-id="d97fd-105">Spiegelt ein Paket und seine Abhängigkeiten aus den angegebenen quelldepots in das Zielrepository ein.</span><span class="sxs-lookup"><span data-stu-id="d97fd-105">Mirrors a package and its dependencies from the specified source repositories to the target repository.</span></span>

> [!NOTE]
> <span data-ttu-id="d97fd-106">"Nuget. Server Extensions. dll" und "NuGet-Signed. exe", die zuvor diesen Befehl in nuget 2. x unterstützten (durch Umbenennen von "NuGet-Signed. exe" in "nuget. exe"), sind nicht mehr zum Download verfügbar.</span><span class="sxs-lookup"><span data-stu-id="d97fd-106">NuGet.ServerExtensions.dll and NuGet-Signed.exe that previously supported this command in NuGet 2.x (by renaming NuGet-Signed.exe to nuget.exe) are no longer available for download.</span></span> <span data-ttu-id="d97fd-107">Wenn Sie einen ähnlichen Befehl wie diesen verwenden möchten, versuchen Sie es mit [nugetmirror](https://www.nuget.org/packages/NuGetMirror/).</span><span class="sxs-lookup"><span data-stu-id="d97fd-107">To use a command similar to this, try [NuGetMirror](https://www.nuget.org/packages/NuGetMirror/).</span></span>

## <a name="usage"></a><span data-ttu-id="d97fd-108">Verwendung</span><span class="sxs-lookup"><span data-stu-id="d97fd-108">Usage</span></span>

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

<span data-ttu-id="d97fd-109">gibt `<packageID>` an, wo das zu spiegelnde `<configFilePath>` Paket ist `packages.config` , oder identifiziert die Datei, die die zu spiegelnden Pakete auflistet.</span><span class="sxs-lookup"><span data-stu-id="d97fd-109">where `<packageID>` is the package to mirror, or `<configFilePath>` identifies the `packages.config` file that lists the packages to mirror.</span></span>

<span data-ttu-id="d97fd-110">Der `<listUrlTarget>` gibt das Quellrepository an und `<publishUrlTarget>` gibt das Zielrepository an.</span><span class="sxs-lookup"><span data-stu-id="d97fd-110">The `<listUrlTarget>` specifies the source repository, and `<publishUrlTarget>` specifies the target repository.</span></span>

<span data-ttu-id="d97fd-111">Wenn Ihr Zielrepository auf ist `https://machine/repo` , die ausgeführt wird [NuGet.Server in](../../hosting-packages/nuget-server.md), Liste und Push-URLs `https://machine/repo/nuget` und `https://machine/repo/api/v2/package`bzw.</span><span class="sxs-lookup"><span data-stu-id="d97fd-111">If your target repository is on `https://machine/repo` that's running [NuGet.Server](../../hosting-packages/nuget-server.md), the list and push urls will be `https://machine/repo/nuget` and `https://machine/repo/api/v2/package`, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="d97fd-112">Optionen</span><span class="sxs-lookup"><span data-stu-id="d97fd-112">Options</span></span>

| <span data-ttu-id="d97fd-113">Option</span><span class="sxs-lookup"><span data-stu-id="d97fd-113">Option</span></span> | <span data-ttu-id="d97fd-114">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="d97fd-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d97fd-115">ApiKey</span><span class="sxs-lookup"><span data-stu-id="d97fd-115">ApiKey</span></span> | <span data-ttu-id="d97fd-116">Der API-Schlüssel für das Zielrepository.</span><span class="sxs-lookup"><span data-stu-id="d97fd-116">The API key for the target repository.</span></span> <span data-ttu-id="d97fd-117">Wenn Sie nicht vorhanden ist, wird die in der Konfigurationsdatei angegebene verwendet`%AppData%\NuGet\NuGet.Config` ((Windows) `~/.nuget/NuGet/NuGet.Config` oder (Mac/Linux)).</span><span class="sxs-lookup"><span data-stu-id="d97fd-117">If not present,  the one specified in the config file is used (`%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span></span> |
| <span data-ttu-id="d97fd-118">Help</span><span class="sxs-lookup"><span data-stu-id="d97fd-118">Help</span></span> | <span data-ttu-id="d97fd-119">Zeigt Hilfe Informationen für den Befehl an.</span><span class="sxs-lookup"><span data-stu-id="d97fd-119">Displays help information for the command.</span></span> |
| <span data-ttu-id="d97fd-120">NoCache</span><span class="sxs-lookup"><span data-stu-id="d97fd-120">NoCache</span></span> | <span data-ttu-id="d97fd-121">Verhindert, dass nuget zwischengespeicherte Pakete verwendet.</span><span class="sxs-lookup"><span data-stu-id="d97fd-121">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="d97fd-122">Weitere Informationen finden Sie [unter Verwalten der globalen Pakete und Cache Ordner](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="d97fd-122">See [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="d97fd-123">NOOP</span><span class="sxs-lookup"><span data-stu-id="d97fd-123">Noop</span></span> | <span data-ttu-id="d97fd-124">Protokolliert, was geschehen würde, führt die Aktionen jedoch nicht aus. nimmt die erfolgreiche Ausführung von pushvorgängen an.</span><span class="sxs-lookup"><span data-stu-id="d97fd-124">Logs what would be done but does not perform the actions; assumes success for push operations.</span></span> |
| <span data-ttu-id="d97fd-125">Vorab</span><span class="sxs-lookup"><span data-stu-id="d97fd-125">PreRelease</span></span> | <span data-ttu-id="d97fd-126">Schließt vorab Pakete in den Spiegelungs Vorgang ein.</span><span class="sxs-lookup"><span data-stu-id="d97fd-126">Includes prerelease packages in the mirroring operation.</span></span> |
| <span data-ttu-id="d97fd-127">Source</span><span class="sxs-lookup"><span data-stu-id="d97fd-127">Source</span></span> | <span data-ttu-id="d97fd-128">Eine Liste der zu spiegelnden Paketquellen.</span><span class="sxs-lookup"><span data-stu-id="d97fd-128">A list of package sources to mirror.</span></span> <span data-ttu-id="d97fd-129">Wenn keine Quellen angegeben sind, werden die in der Konfigurationsdatei definierten (siehe APIKey oben) verwendet, wobei "nuget.org" verwendet wird, wenn keine Daten angegeben sind.</span><span class="sxs-lookup"><span data-stu-id="d97fd-129">If no sources are specified, the ones defined in the config file (see ApiKey above) are used, defaulting to nuget.org if none are specified.</span></span> |
| <span data-ttu-id="d97fd-130">Timeout</span><span class="sxs-lookup"><span data-stu-id="d97fd-130">Timeout</span></span> | <span data-ttu-id="d97fd-131">Gibt den Timeout Wert (in Sekunden) für das Push an einen Server an.</span><span class="sxs-lookup"><span data-stu-id="d97fd-131">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="d97fd-132">Der Standardwert ist 300 Sekunden (5 Minuten).</span><span class="sxs-lookup"><span data-stu-id="d97fd-132">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="d97fd-133">Version</span><span class="sxs-lookup"><span data-stu-id="d97fd-133">Version</span></span> | <span data-ttu-id="d97fd-134">Die Version des zu installierenden Pakets.</span><span class="sxs-lookup"><span data-stu-id="d97fd-134">The version of the package to install.</span></span> <span data-ttu-id="d97fd-135">Wenn nicht angegeben, wird die aktuelle Version gespiegelt.</span><span class="sxs-lookup"><span data-stu-id="d97fd-135">If not specified, the latest version is mirrored.</span></span> |

<span data-ttu-id="d97fd-136">Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="d97fd-136">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="d97fd-137">Beispiele</span><span class="sxs-lookup"><span data-stu-id="d97fd-137">Examples</span></span>

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
