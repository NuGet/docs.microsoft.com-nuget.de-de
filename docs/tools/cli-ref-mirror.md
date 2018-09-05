---
title: NuGet-CLI-Spiegel-Befehl
description: Referenz für die nuget.exe-Spiegel-Befehl
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: d3a322e16c4ba212a856e9bf4d2eaab2872c31b6
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550205"
---
# <a name="mirror-command-nuget-cli"></a><span data-ttu-id="01dd2-103">Der Befehl „mirror“ (NuGet-CLI)</span><span class="sxs-lookup"><span data-stu-id="01dd2-103">mirror command (NuGet CLI)</span></span>

<span data-ttu-id="01dd2-104">**Gilt für:** Paket veröffentlichen &bullet; **unterstützte Versionen:** in 3.2 und höher als veraltet markiert</span><span class="sxs-lookup"><span data-stu-id="01dd2-104">**Applies to:** package publishing &bullet; **Supported versions:** deprecated in 3.2+</span></span>

<span data-ttu-id="01dd2-105">Spiegelt ein Paket und dessen Abhängigkeiten aus den Repositorys für die angegebene Quelle zum Ziel-Repository.</span><span class="sxs-lookup"><span data-stu-id="01dd2-105">Mirrors a package and its dependencies from the specified source repositories to the target repository.</span></span>

> [!NOTE]
> <span data-ttu-id="01dd2-106">Um diesen Befehl für NuGet-Versionen vor 3.2 zu aktivieren, wechseln Sie zu [ https://nuget.codeplex.com/releases ](https://nuget.codeplex.com/releases), wählen Sie das neueste stabile Release, zum Downloadpfad `NuGet.ServerExtensions.dll` und `Nuget-Signed.exe` auf Ihrem lokalen Datenträger und benennen Sie `Nuget-Signed.exe` zu `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="01dd2-106">To enable this command for NuGet versions before 3.2, go to [https://nuget.codeplex.com/releases](https://nuget.codeplex.com/releases), select the newest stable release, download `NuGet.ServerExtensions.dll` and `Nuget-Signed.exe` to your local disk and rename `Nuget-Signed.exe` to `nuget.exe`.</span></span>

## <a name="usage"></a><span data-ttu-id="01dd2-107">Verwendung</span><span class="sxs-lookup"><span data-stu-id="01dd2-107">Usage</span></span>

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

<span data-ttu-id="01dd2-108">in denen `<packageID>` ist das Paket zu spiegeln, oder `<configFilePath>` identifiziert die `packages.config` Datei, die die Pakete, spiegeln auflistet.</span><span class="sxs-lookup"><span data-stu-id="01dd2-108">where `<packageID>` is the package to mirror, or `<configFilePath>` identifies the `packages.config` file that lists the packages to mirror.</span></span>

<span data-ttu-id="01dd2-109">Die `<listUrlTarget>` gibt an, das Quell-Repository und `<publishUrlTarget>` gibt an, die Ziel-Repository.</span><span class="sxs-lookup"><span data-stu-id="01dd2-109">The `<listUrlTarget>` specifies the source repository, and `<publishUrlTarget>` specifies the target repository.</span></span>

<span data-ttu-id="01dd2-110">Wenn Ihr Zielrepository auf ist `https://machine/repo` , die ausgeführt wird [NuGet.Server in](../hosting-packages/nuget-server.md), Liste und Push-URLs `https://machine/repo/nuget` und `https://machine/repo/api/v2/package`bzw.</span><span class="sxs-lookup"><span data-stu-id="01dd2-110">If your target repository is on `https://machine/repo` that's running [NuGet.Server](../hosting-packages/nuget-server.md), the list and push urls will be `https://machine/repo/nuget` and `https://machine/repo/api/v2/package`, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="01dd2-111">Optionen</span><span class="sxs-lookup"><span data-stu-id="01dd2-111">Options</span></span>

| <span data-ttu-id="01dd2-112">Option</span><span class="sxs-lookup"><span data-stu-id="01dd2-112">Option</span></span> | <span data-ttu-id="01dd2-113">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="01dd2-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="01dd2-114">"Apikey"</span><span class="sxs-lookup"><span data-stu-id="01dd2-114">ApiKey</span></span> | <span data-ttu-id="01dd2-115">Die API-Schlüssel für die Ziel-Repository.</span><span class="sxs-lookup"><span data-stu-id="01dd2-115">The API key for the target repository.</span></span> <span data-ttu-id="01dd2-116">Wenn nicht vorhanden ist, angegeben in der Konfigurationsdatei verwendet wird (`%AppData%\NuGet\NuGet.Config` (Windows) oder `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span><span class="sxs-lookup"><span data-stu-id="01dd2-116">If not present,  the one specified in the config file is used (`%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span></span> |
| <span data-ttu-id="01dd2-117">Hilfe</span><span class="sxs-lookup"><span data-stu-id="01dd2-117">Help</span></span> | <span data-ttu-id="01dd2-118">Zeigt die Informationen für den Befehl Hilfe.</span><span class="sxs-lookup"><span data-stu-id="01dd2-118">Displays help information for the command.</span></span> |
| <span data-ttu-id="01dd2-119">NoCache</span><span class="sxs-lookup"><span data-stu-id="01dd2-119">NoCache</span></span> | <span data-ttu-id="01dd2-120">Verhindert, dass NuGet zwischengespeicherte Pakete verwenden.</span><span class="sxs-lookup"><span data-stu-id="01dd2-120">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="01dd2-121">Finden Sie unter [Verwalten der globalen Paketordner und Cacheordner](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="01dd2-121">See [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span> |
| <span data-ttu-id="01dd2-122">NOOP</span><span class="sxs-lookup"><span data-stu-id="01dd2-122">Noop</span></span> | <span data-ttu-id="01dd2-123">Protokolliert, was geschehen, jedoch nicht die Aktionen ausgeführt wird; geht davon aus Erfolg für Push-Vorgänge.</span><span class="sxs-lookup"><span data-stu-id="01dd2-123">Logs what would be done but does not perform the actions; assumes success for push operations.</span></span> |
| <span data-ttu-id="01dd2-124">Vorabversion</span><span class="sxs-lookup"><span data-stu-id="01dd2-124">PreRelease</span></span> | <span data-ttu-id="01dd2-125">Schließt Vorabversionen von Paketen in der datenbankspiegelungs-Vorgang an.</span><span class="sxs-lookup"><span data-stu-id="01dd2-125">Includes prerelease packages in the mirroring operation.</span></span> |
| <span data-ttu-id="01dd2-126">Quelle</span><span class="sxs-lookup"><span data-stu-id="01dd2-126">Source</span></span> | <span data-ttu-id="01dd2-127">Eine Liste der Paketquellen zu spiegeln.</span><span class="sxs-lookup"><span data-stu-id="01dd2-127">A list of package sources to mirror.</span></span> <span data-ttu-id="01dd2-128">Wenn keine Quellen angegeben werden, die definiert, die Config-Datei (siehe "apikey" oben) verwendet werden, standardmäßig auf nuget.org, wenn keine angegeben werden.</span><span class="sxs-lookup"><span data-stu-id="01dd2-128">If no sources are specified, the ones defined in the config file (see ApiKey above) are used, defaulting to nuget.org if none are specified.</span></span> |
| <span data-ttu-id="01dd2-129">Timeout</span><span class="sxs-lookup"><span data-stu-id="01dd2-129">Timeout</span></span> | <span data-ttu-id="01dd2-130">Gibt das Timeout in Sekunden für die Übertragung auf einen Server an.</span><span class="sxs-lookup"><span data-stu-id="01dd2-130">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="01dd2-131">Der Standardwert ist 300 Sekunden (5 Minuten).</span><span class="sxs-lookup"><span data-stu-id="01dd2-131">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="01dd2-132">Version</span><span class="sxs-lookup"><span data-stu-id="01dd2-132">Version</span></span> | <span data-ttu-id="01dd2-133">Die Version des zu installierenden Pakets an.</span><span class="sxs-lookup"><span data-stu-id="01dd2-133">The version of the package to install.</span></span> <span data-ttu-id="01dd2-134">Wenn nicht angegeben, wird die neueste Version gespiegelt.</span><span class="sxs-lookup"><span data-stu-id="01dd2-134">If not specified, the latest version is mirrored.</span></span> |

<span data-ttu-id="01dd2-135">Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="01dd2-135">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="01dd2-136">Beispiele</span><span class="sxs-lookup"><span data-stu-id="01dd2-136">Examples</span></span>

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
