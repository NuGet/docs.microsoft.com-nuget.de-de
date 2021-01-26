---
title: Befehl "nuget CLI-Spiegel"
description: Verweis auf den Befehl nuget.exe Spiegelung
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 6ecd5c11383f78fdaeb01090366a8ffe294b4f8b
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779175"
---
# <a name="mirror-command-nuget-cli"></a><span data-ttu-id="a5553-103">Spiegel Befehl (nuget-CLI)</span><span class="sxs-lookup"><span data-stu-id="a5553-103">mirror command (NuGet CLI)</span></span>

<span data-ttu-id="a5553-104">**Gilt für:** &bullet; **unterstützte Versionen** der Paket Veröffentlichung: veraltet in 3.2 +</span><span class="sxs-lookup"><span data-stu-id="a5553-104">**Applies to:** package publishing &bullet; **Supported versions:** deprecated in 3.2+</span></span>

<span data-ttu-id="a5553-105">Spiegelt ein Paket und seine Abhängigkeiten aus den angegebenen quelldepots in das Zielrepository ein.</span><span class="sxs-lookup"><span data-stu-id="a5553-105">Mirrors a package and its dependencies from the specified source repositories to the target repository.</span></span>

> [!NOTE]
> <span data-ttu-id="a5553-106">NuGet.ServerExtensions.dll und NuGet-Signed.exe, die diesen Befehl zuvor in nuget 2. x unterstützten (durch Umbenennen von NuGet-Signed.exe in nuget.exe), sind nicht mehr zum Herunterladen verfügbar.</span><span class="sxs-lookup"><span data-stu-id="a5553-106">NuGet.ServerExtensions.dll and NuGet-Signed.exe that previously supported this command in NuGet 2.x (by renaming NuGet-Signed.exe to nuget.exe) are no longer available for download.</span></span> <span data-ttu-id="a5553-107">Wenn Sie einen ähnlichen Befehl wie diesen verwenden möchten, versuchen Sie es mit [nugetmirror](https://www.nuget.org/packages/NuGetMirror/).</span><span class="sxs-lookup"><span data-stu-id="a5553-107">To use a command similar to this, try [NuGetMirror](https://www.nuget.org/packages/NuGetMirror/).</span></span>

## <a name="usage"></a><span data-ttu-id="a5553-108">Verwendung</span><span class="sxs-lookup"><span data-stu-id="a5553-108">Usage</span></span>

```cli
nuget mirror <packageID | configFilePath> <listUrlTarget> <publishUrlTarget> [options]
```

<span data-ttu-id="a5553-109">`<packageID>`gibt an, wo das zu spiegelnde Paket ist, oder `<configFilePath>` identifiziert die Datei, die `packages.config` die zu spiegelnden Pakete auflistet.</span><span class="sxs-lookup"><span data-stu-id="a5553-109">where `<packageID>` is the package to mirror, or `<configFilePath>` identifies the `packages.config` file that lists the packages to mirror.</span></span>

<span data-ttu-id="a5553-110">Der `<listUrlTarget>` gibt das Quellrepository an und `<publishUrlTarget>` gibt das Zielrepository an.</span><span class="sxs-lookup"><span data-stu-id="a5553-110">The `<listUrlTarget>` specifies the source repository, and `<publishUrlTarget>` specifies the target repository.</span></span>

<span data-ttu-id="a5553-111">Wenn das Zielrepository auf dem ausgeführt wird, auf dem `https://machine/repo` [nuget. Server](../../hosting-packages/nuget-server.md)ausgeführt wird, werden die Listen-und pushurls `https://machine/repo/nuget` `https://machine/repo/api/v2/package` bzw.</span><span class="sxs-lookup"><span data-stu-id="a5553-111">If your target repository is on `https://machine/repo` that's running [NuGet.Server](../../hosting-packages/nuget-server.md), the list and push urls will be `https://machine/repo/nuget` and `https://machine/repo/api/v2/package`, respectively.</span></span>

## <a name="options"></a><span data-ttu-id="a5553-112">Optionen</span><span class="sxs-lookup"><span data-stu-id="a5553-112">Options</span></span>

- **`-ApiKey`**

  <span data-ttu-id="a5553-113">Der API-Schlüssel für das Zielrepository.</span><span class="sxs-lookup"><span data-stu-id="a5553-113">The API key for the target repository.</span></span> <span data-ttu-id="a5553-114">Wenn Sie nicht vorhanden ist, wird die in der Konfigurationsdatei angegebene verwendet ( `%AppData%\NuGet\NuGet.Config` (Windows) oder `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span><span class="sxs-lookup"><span data-stu-id="a5553-114">If not present,  the one specified in the config file is used (`%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux)).</span></span>

- **`-Help`**

  <span data-ttu-id="a5553-115">Zeigt Hilfe Informationen für den Befehl an.</span><span class="sxs-lookup"><span data-stu-id="a5553-115">Displays help information for the command.</span></span>

- **`-NoCache`**

  <span data-ttu-id="a5553-116">Verhindert, dass nuget zwischengespeicherte Pakete verwendet.</span><span class="sxs-lookup"><span data-stu-id="a5553-116">Prevents NuGet from using cached packages.</span></span> <span data-ttu-id="a5553-117">Weitere Informationen finden Sie [unter Verwalten der globalen Pakete und Cache Ordner](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="a5553-117">See [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

- **`-Noop`**

  <span data-ttu-id="a5553-118">Protokolliert, was geschehen würde, führt die Aktionen jedoch nicht aus. nimmt die erfolgreiche Ausführung von pushvorgängen an.</span><span class="sxs-lookup"><span data-stu-id="a5553-118">Logs what would be done but does not perform the actions; assumes success for push operations.</span></span>

- **`-PreRelease`**

  <span data-ttu-id="a5553-119">Schließt vorab Pakete in den Spiegelungs Vorgang ein.</span><span class="sxs-lookup"><span data-stu-id="a5553-119">Includes prerelease packages in the mirroring operation.</span></span>

- **`-Source`**

  <span data-ttu-id="a5553-120">Eine Liste der zu spiegelnden Paketquellen.</span><span class="sxs-lookup"><span data-stu-id="a5553-120">A list of package sources to mirror.</span></span> <span data-ttu-id="a5553-121">Wenn keine Quellen angegeben sind, werden die in der Konfigurationsdatei definierten (siehe APIKey oben) verwendet, wobei "nuget.org" verwendet wird, wenn keine Daten angegeben sind.</span><span class="sxs-lookup"><span data-stu-id="a5553-121">If no sources are specified, the ones defined in the config file (see ApiKey above) are used, defaulting to nuget.org if none are specified.</span></span>

- **`-Timeout`**

  <span data-ttu-id="a5553-122">Gibt den Timeout Wert (in Sekunden) für das Push an einen Server an.</span><span class="sxs-lookup"><span data-stu-id="a5553-122">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="a5553-123">Der Standardwert beträgt 300 Sekunden (5 Minuten).</span><span class="sxs-lookup"><span data-stu-id="a5553-123">The default is 300 seconds (5 minutes).</span></span>

- **`-Version`**

  <span data-ttu-id="a5553-124">Die Version des zu installierenden Pakets.</span><span class="sxs-lookup"><span data-stu-id="a5553-124">The version of the package to install.</span></span> <span data-ttu-id="a5553-125">Wenn nicht angegeben, wird die aktuelle Version gespiegelt.</span><span class="sxs-lookup"><span data-stu-id="a5553-125">If not specified, the latest version is mirrored.</span></span>

<span data-ttu-id="a5553-126">Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="a5553-126">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="a5553-127">Beispiele</span><span class="sxs-lookup"><span data-stu-id="a5553-127">Examples</span></span>

```cli
nuget mirror packages.config  https://MyRepo/nuget https://MyRepo/api/v2/package -source https://nuget.org/api/v2 -apikey myApiKey -nocache

nuget mirror Microsoft.AspNet.Mvc https://MyRepo/nuget https://MyRepo/api/v2/package -version 4.0.20505.0

nuget mirror Microsoft.Net.Http https://MyRepo/nuget https://MyRepo/api/v2/package -prerelease
```
