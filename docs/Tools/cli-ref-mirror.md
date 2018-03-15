---
title: NuGet-CLI-Spiegel-Befehl | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Referenz für den nuget.exe Mirror-Befehl"
keywords: NuGet-Spiegel-Verweis, Mirror-Befehl
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 0c1969cc04b2e2cead5e9dadf9739fdabdf65f6c
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/15/2018
---
# <a name="mirror-command-nuget-cli"></a><span data-ttu-id="7be44-104">Mirror-Befehl (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="7be44-104">mirror command (NuGet CLI)</span></span>

<span data-ttu-id="7be44-105">**Gilt für:** Verpacken Sie die Publishing &bullet; **unterstützte Versionen:** in 3.2 + veraltet</span><span class="sxs-lookup"><span data-stu-id="7be44-105">**Applies to:** package publishing &bullet; **Supported versions:** deprecated in 3.2+</span></span>

<span data-ttu-id="7be44-106">Spiegelt ein Paket und seine Abhängigkeiten aus dem angegebenen quellrepositorys im Ziel-Repository.</span><span class="sxs-lookup"><span data-stu-id="7be44-106">Mirrors a package and its dependencies from the specified source repositories to the target repository.</span></span>

> [!NOTE]
> <span data-ttu-id="7be44-107">Um diesen Befehl für NuGet-Versionen vor 3.2 zu aktivieren, wechseln Sie zu [ https://nuget.codeplex.com/releases ](https://nuget.codeplex.com/releases), wählen Sie die neueste stabile Version, zum Downloadpfad `NuGet.ServerExtensions.dll` und `Nuget-Signed.exe` auf Ihre lokale Festplatte und Rename `Nuget-Signed.exe` auf `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="7be44-107">To enable this command for NuGet versions before 3.2, go to [https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases), select the newest stable release, download `NuGet.ServerExtensions.dll` and `Nuget-Signed.exe` to your local disk and rename `Nuget-Signed.exe` to `nuget.exe`.</span></span>

## <a name="usage"></a><span data-ttu-id="7be44-108">Verwendung</span><span class="sxs-lookup"><span data-stu-id="7be44-108">Usage</span></span>

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

<span data-ttu-id="7be44-109">auf dem `<packageID>` ist das Paket zum Spiegeln von, oder `<configFilePath>` identifiziert die `packages.config` Datei, die Pakete zum Spiegeln von aufgeführt.</span><span class="sxs-lookup"><span data-stu-id="7be44-109">where `<packageID>` is the package to mirror, or `<configFilePath>` identifies the `packages.config` file that lists the packages to mirror.</span></span>

<span data-ttu-id="7be44-110">Die `<listUrlTarget>` gibt an, das Quellrepository und `<publishUrlTarget>` gibt an, die Ziel-Repository.</span><span class="sxs-lookup"><span data-stu-id="7be44-110">The `<listUrlTarget>` specifies the source repository, and `<publishUrlTarget>` specifies the target repository.</span></span>

<span data-ttu-id="7be44-111">Wenn Ihr Zielrepository auf ist `https://machine/repo` , die ausgeführt wird [NuGet.Server in](../hosting-packages/nuget-server.md), Liste und Push-URLs `https://machine/repo/nuget` und `https://machine/repo/api/v2/package`bzw.</span><span class="sxs-lookup"><span data-stu-id="7be44-111">If your target repository is on `https://machine/repo` that's running [NuGet.Server](../hosting-packages/nuget-server.md), the list and push urls will be `https://machine/repo/nuget` and `https://machine/repo/api/v2/package`, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="7be44-112">Optionen</span><span class="sxs-lookup"><span data-stu-id="7be44-112">Options</span></span>

| <span data-ttu-id="7be44-113">Option</span><span class="sxs-lookup"><span data-stu-id="7be44-113">Option</span></span> | <span data-ttu-id="7be44-114">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="7be44-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7be44-115">ApiKey</span><span class="sxs-lookup"><span data-stu-id="7be44-115">ApiKey</span></span> | <span data-ttu-id="7be44-116">Die API-Schlüssel für das Zielrepository.</span><span class="sxs-lookup"><span data-stu-id="7be44-116">The API key for the target repository.</span></span> <span data-ttu-id="7be44-117">Wenn Sie nicht vorhanden ist, in der Datei "App.config" angegebenen verwendet wird (`%AppData%\NuGet\NuGet.Config` (Windows) oder `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span><span class="sxs-lookup"><span data-stu-id="7be44-117">If not present,  the one specified in the config file is used (`%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span></span> |
| <span data-ttu-id="7be44-118">Hilfe</span><span class="sxs-lookup"><span data-stu-id="7be44-118">Help</span></span> | <span data-ttu-id="7be44-119">Zeigt die Hilfe Informationen für den Befehl.</span><span class="sxs-lookup"><span data-stu-id="7be44-119">Displays help information for the command.</span></span> |
| <span data-ttu-id="7be44-120">NoCache</span><span class="sxs-lookup"><span data-stu-id="7be44-120">NoCache</span></span> | <span data-ttu-id="7be44-121">Verhindert, dass NuGet Pakete aus lokalen Caches.</span><span class="sxs-lookup"><span data-stu-id="7be44-121">Prevents NuGet from using packages from local machine caches.</span></span> |
| <span data-ttu-id="7be44-122">NOOP</span><span class="sxs-lookup"><span data-stu-id="7be44-122">Noop</span></span> | <span data-ttu-id="7be44-123">Protokolliert, was erfolgt, führt jedoch die Aktionen; geht davon aus Erfolg für Push-Vorgänge.</span><span class="sxs-lookup"><span data-stu-id="7be44-123">Logs what would be done but does not perform the actions; assumes success for push operations.</span></span> |
| <span data-ttu-id="7be44-124">PreRelease</span><span class="sxs-lookup"><span data-stu-id="7be44-124">PreRelease</span></span> | <span data-ttu-id="7be44-125">Schließt Vorabversionen von Paketen, in dem Spiegelungsvorgang.</span><span class="sxs-lookup"><span data-stu-id="7be44-125">Includes prerelease packages in the mirroring operation.</span></span> |
| <span data-ttu-id="7be44-126">Quelle</span><span class="sxs-lookup"><span data-stu-id="7be44-126">Source</span></span> | <span data-ttu-id="7be44-127">Eine Liste der Paketquellen zu spiegeln.</span><span class="sxs-lookup"><span data-stu-id="7be44-127">A list of package sources to mirror.</span></span> <span data-ttu-id="7be44-128">Wenn keine Datenquellen angegeben sind, definiert die der Datei "App.config" (siehe "apikey" oben) verwendet werden, direktionales nuget.org keine Parameter angegeben.</span><span class="sxs-lookup"><span data-stu-id="7be44-128">If no sources are specified, the ones defined in the config file (see ApiKey above) are used, defaulting to nuget.org if none are specified.</span></span> |
| <span data-ttu-id="7be44-129">Timeout</span><span class="sxs-lookup"><span data-stu-id="7be44-129">Timeout</span></span> | <span data-ttu-id="7be44-130">Gibt das Timeout in Sekunden für die auf einem Server übertragen.</span><span class="sxs-lookup"><span data-stu-id="7be44-130">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="7be44-131">Der Standardwert ist 300 Sekunden (5 Minuten).</span><span class="sxs-lookup"><span data-stu-id="7be44-131">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="7be44-132">Version</span><span class="sxs-lookup"><span data-stu-id="7be44-132">Version</span></span> | <span data-ttu-id="7be44-133">Die Version des zu installierenden Pakets an.</span><span class="sxs-lookup"><span data-stu-id="7be44-133">The version of the package to install.</span></span> <span data-ttu-id="7be44-134">Wenn nicht angegeben, wird die neueste Version gespiegelt.</span><span class="sxs-lookup"><span data-stu-id="7be44-134">If not specified, the latest version is mirrored.</span></span> |

<span data-ttu-id="7be44-135">Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="7be44-135">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="7be44-136">Beispiele</span><span class="sxs-lookup"><span data-stu-id="7be44-136">Examples</span></span>

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
