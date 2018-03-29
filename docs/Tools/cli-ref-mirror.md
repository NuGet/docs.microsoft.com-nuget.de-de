---
title: NuGet-CLI-Spiegel-Befehl | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Referenz für den nuget.exe Mirror-Befehl
keywords: NuGet-Spiegel-Verweis, Mirror-Befehl
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 512bd72d568cda81eb7c6a1555c36ead66b5c438
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="mirror-command-nuget-cli"></a><span data-ttu-id="565ca-104">Mirror-Befehl (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="565ca-104">mirror command (NuGet CLI)</span></span>

<span data-ttu-id="565ca-105">**Gilt für:** Verpacken Sie die Publishing &bullet; **unterstützte Versionen:** in 3.2 + veraltet</span><span class="sxs-lookup"><span data-stu-id="565ca-105">**Applies to:** package publishing &bullet; **Supported versions:** deprecated in 3.2+</span></span>

<span data-ttu-id="565ca-106">Spiegelt ein Paket und seine Abhängigkeiten aus dem angegebenen quellrepositorys im Ziel-Repository.</span><span class="sxs-lookup"><span data-stu-id="565ca-106">Mirrors a package and its dependencies from the specified source repositories to the target repository.</span></span>

> [!NOTE]
> <span data-ttu-id="565ca-107">Um diesen Befehl für NuGet-Versionen vor 3.2 zu aktivieren, wechseln Sie zu [ https://nuget.codeplex.com/releases ](https://nuget.codeplex.com/releases), wählen Sie die neueste stabile Version, zum Downloadpfad `NuGet.ServerExtensions.dll` und `Nuget-Signed.exe` auf Ihre lokale Festplatte und Rename `Nuget-Signed.exe` auf `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="565ca-107">To enable this command for NuGet versions before 3.2, go to [https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases), select the newest stable release, download `NuGet.ServerExtensions.dll` and `Nuget-Signed.exe` to your local disk and rename `Nuget-Signed.exe` to `nuget.exe`.</span></span>

## <a name="usage"></a><span data-ttu-id="565ca-108">Verwendung</span><span class="sxs-lookup"><span data-stu-id="565ca-108">Usage</span></span>

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

<span data-ttu-id="565ca-109">auf dem `<packageID>` ist das Paket zum Spiegeln von, oder `<configFilePath>` identifiziert die `packages.config` Datei, die Pakete zum Spiegeln von aufgeführt.</span><span class="sxs-lookup"><span data-stu-id="565ca-109">where `<packageID>` is the package to mirror, or `<configFilePath>` identifies the `packages.config` file that lists the packages to mirror.</span></span>

<span data-ttu-id="565ca-110">Die `<listUrlTarget>` gibt an, das Quellrepository und `<publishUrlTarget>` gibt an, die Ziel-Repository.</span><span class="sxs-lookup"><span data-stu-id="565ca-110">The `<listUrlTarget>` specifies the source repository, and `<publishUrlTarget>` specifies the target repository.</span></span>

<span data-ttu-id="565ca-111">Wenn Ihr Zielrepository auf ist `https://machine/repo` , die ausgeführt wird [NuGet.Server in](../hosting-packages/nuget-server.md), Liste und Push-URLs `https://machine/repo/nuget` und `https://machine/repo/api/v2/package`bzw.</span><span class="sxs-lookup"><span data-stu-id="565ca-111">If your target repository is on `https://machine/repo` that's running [NuGet.Server](../hosting-packages/nuget-server.md), the list and push urls will be `https://machine/repo/nuget` and `https://machine/repo/api/v2/package`, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="565ca-112">Optionen</span><span class="sxs-lookup"><span data-stu-id="565ca-112">Options</span></span>

| <span data-ttu-id="565ca-113">Option</span><span class="sxs-lookup"><span data-stu-id="565ca-113">Option</span></span> | <span data-ttu-id="565ca-114">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="565ca-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="565ca-115">ApiKey</span><span class="sxs-lookup"><span data-stu-id="565ca-115">ApiKey</span></span> | <span data-ttu-id="565ca-116">Die API-Schlüssel für das Zielrepository.</span><span class="sxs-lookup"><span data-stu-id="565ca-116">The API key for the target repository.</span></span> <span data-ttu-id="565ca-117">Wenn Sie nicht vorhanden ist, in der Datei "App.config" angegebenen verwendet wird (`%AppData%\NuGet\NuGet.Config` (Windows) oder `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span><span class="sxs-lookup"><span data-stu-id="565ca-117">If not present,  the one specified in the config file is used (`%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span></span> |
| <span data-ttu-id="565ca-118">Hilfe</span><span class="sxs-lookup"><span data-stu-id="565ca-118">Help</span></span> | <span data-ttu-id="565ca-119">Zeigt die Hilfe Informationen für den Befehl.</span><span class="sxs-lookup"><span data-stu-id="565ca-119">Displays help information for the command.</span></span> |
| <span data-ttu-id="565ca-120">NoCache</span><span class="sxs-lookup"><span data-stu-id="565ca-120">NoCache</span></span> | <span data-ttu-id="565ca-121">Verhindert, dass NuGet zwischengespeicherten Pakete verwenden.</span><span class="sxs-lookup"><span data-stu-id="565ca-121">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="565ca-122">Finden Sie unter [Verwaltung der globalen Pakete und der Cacheordner](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="565ca-122">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="565ca-123">NOOP</span><span class="sxs-lookup"><span data-stu-id="565ca-123">Noop</span></span> | <span data-ttu-id="565ca-124">Protokolliert, was erfolgt, führt jedoch die Aktionen; geht davon aus Erfolg für Push-Vorgänge.</span><span class="sxs-lookup"><span data-stu-id="565ca-124">Logs what would be done but does not perform the actions; assumes success for push operations.</span></span> |
| <span data-ttu-id="565ca-125">PreRelease</span><span class="sxs-lookup"><span data-stu-id="565ca-125">PreRelease</span></span> | <span data-ttu-id="565ca-126">Schließt Vorabversionen von Paketen, in dem Spiegelungsvorgang.</span><span class="sxs-lookup"><span data-stu-id="565ca-126">Includes prerelease packages in the mirroring operation.</span></span> |
| <span data-ttu-id="565ca-127">Quelle</span><span class="sxs-lookup"><span data-stu-id="565ca-127">Source</span></span> | <span data-ttu-id="565ca-128">Eine Liste der Paketquellen zu spiegeln.</span><span class="sxs-lookup"><span data-stu-id="565ca-128">A list of package sources to mirror.</span></span> <span data-ttu-id="565ca-129">Wenn keine Datenquellen angegeben sind, definiert die der Datei "App.config" (siehe "apikey" oben) verwendet werden, direktionales nuget.org keine Parameter angegeben.</span><span class="sxs-lookup"><span data-stu-id="565ca-129">If no sources are specified, the ones defined in the config file (see ApiKey above) are used, defaulting to nuget.org if none are specified.</span></span> |
| <span data-ttu-id="565ca-130">Timeout</span><span class="sxs-lookup"><span data-stu-id="565ca-130">Timeout</span></span> | <span data-ttu-id="565ca-131">Gibt das Timeout in Sekunden für die auf einem Server übertragen.</span><span class="sxs-lookup"><span data-stu-id="565ca-131">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="565ca-132">Der Standardwert ist 300 Sekunden (5 Minuten).</span><span class="sxs-lookup"><span data-stu-id="565ca-132">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="565ca-133">Version</span><span class="sxs-lookup"><span data-stu-id="565ca-133">Version</span></span> | <span data-ttu-id="565ca-134">Die Version des zu installierenden Pakets an.</span><span class="sxs-lookup"><span data-stu-id="565ca-134">The version of the package to install.</span></span> <span data-ttu-id="565ca-135">Wenn nicht angegeben, wird die neueste Version gespiegelt.</span><span class="sxs-lookup"><span data-stu-id="565ca-135">If not specified, the latest version is mirrored.</span></span> |

<span data-ttu-id="565ca-136">Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="565ca-136">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="565ca-137">Beispiele</span><span class="sxs-lookup"><span data-stu-id="565ca-137">Examples</span></span>

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
