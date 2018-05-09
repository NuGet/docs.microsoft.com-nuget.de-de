---
title: NuGet-CLI-Delete-Befehl
description: Referenz für den Löschbefehl nuget.exe
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 1db00a32d777f1c0247f855bf57a0dcf1c6734ae
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="delete-command-nuget-cli"></a><span data-ttu-id="7ddb0-103">Delete-Befehl (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="7ddb0-103">delete command (NuGet CLI)</span></span>

<span data-ttu-id="7ddb0-104">**Gilt für:** Verpacken Sie die Publishing &bullet; **unterstützte Versionen:** alle</span><span class="sxs-lookup"><span data-stu-id="7ddb0-104">**Applies to:** package publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="7ddb0-105">Löscht oder unlists ein Pakets aus der Paketquelle.</span><span class="sxs-lookup"><span data-stu-id="7ddb0-105">Deletes or unlists a package from a package source.</span></span> <span data-ttu-id="7ddb0-106">Für nuget.org, den Löschbefehl [unlists das Paket](../policies/deleting-packages.md).</span><span class="sxs-lookup"><span data-stu-id="7ddb0-106">For nuget.org, the delete command [unlists the package](../policies/deleting-packages.md).</span></span>

## <a name="usage"></a><span data-ttu-id="7ddb0-107">Verwendung</span><span class="sxs-lookup"><span data-stu-id="7ddb0-107">Usage</span></span>

```cli
nuget delete <packageID> <packageVersion> [options]
```

<span data-ttu-id="7ddb0-108">wobei `<packageID>` und `<packageVersion>` das genaue Paket zu löschen oder die Benutzerauswahl zu identifizieren.</span><span class="sxs-lookup"><span data-stu-id="7ddb0-108">where `<packageID>` and `<packageVersion>` identify the exact package to delete or unlist.</span></span> <span data-ttu-id="7ddb0-109">Das genaue Verhalten hängt von der Quelle ab.</span><span class="sxs-lookup"><span data-stu-id="7ddb0-109">The exact behavior depends on the source.</span></span> <span data-ttu-id="7ddb0-110">Für lokale Ordner ist z. B. das Paket gelöscht. für nuget.org ist das Paket nicht aufgeführte.</span><span class="sxs-lookup"><span data-stu-id="7ddb0-110">For local folders, for instance, the package is deleted; for nuget.org the package is unlisted.</span></span>

## <a name="options"></a><span data-ttu-id="7ddb0-111">Optionen</span><span class="sxs-lookup"><span data-stu-id="7ddb0-111">Options</span></span>

| <span data-ttu-id="7ddb0-112">Option</span><span class="sxs-lookup"><span data-stu-id="7ddb0-112">Option</span></span> | <span data-ttu-id="7ddb0-113">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="7ddb0-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7ddb0-114">"apikey"</span><span class="sxs-lookup"><span data-stu-id="7ddb0-114">ApiKey</span></span> | <span data-ttu-id="7ddb0-115">Die API-Schlüssel für das Zielrepository.</span><span class="sxs-lookup"><span data-stu-id="7ddb0-115">The API key for the target repository.</span></span> <span data-ttu-id="7ddb0-116">Wenn Sie nicht vorhanden ist, wird in der Datei "App.config" angegebenen verwendet.</span><span class="sxs-lookup"><span data-stu-id="7ddb0-116">If not present, the one specified in the config file is used.</span></span> |
| <span data-ttu-id="7ddb0-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="7ddb0-117">ConfigFile</span></span> | <span data-ttu-id="7ddb0-118">Die NuGet-Konfigurationsdatei angewendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="7ddb0-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="7ddb0-119">Wenn nicht angegeben, `%AppData%\NuGet\NuGet.Config` (Windows) oder `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="7ddb0-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="7ddb0-120">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="7ddb0-120">ForceEnglishOutput</span></span> | <span data-ttu-id="7ddb0-121">*(3.5 +)*  Erzwingt nuget.exe über eine invariante Kultur Englisch-basierte ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="7ddb0-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="7ddb0-122">Hilfe</span><span class="sxs-lookup"><span data-stu-id="7ddb0-122">Help</span></span> | <span data-ttu-id="7ddb0-123">Zeigt die Hilfe Informationen für den Befehl.</span><span class="sxs-lookup"><span data-stu-id="7ddb0-123">Displays help information for the command.</span></span> |
| <span data-ttu-id="7ddb0-124">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="7ddb0-124">NonInteractive</span></span> | <span data-ttu-id="7ddb0-125">Unterdrückt aufforderungen für Benutzereingaben oder Bestätigungen an.</span><span class="sxs-lookup"><span data-stu-id="7ddb0-125">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="7ddb0-126">Quelle</span><span class="sxs-lookup"><span data-stu-id="7ddb0-126">Source</span></span> | <span data-ttu-id="7ddb0-127">Gibt die Server-URL an.</span><span class="sxs-lookup"><span data-stu-id="7ddb0-127">Specifies the server URL.</span></span> <span data-ttu-id="7ddb0-128">Die URL für nuget.org lautet `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="7ddb0-128">The URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="7ddb0-129">Private-Feeds als Ersatz für den Hostnamen, z. B. *%hostname%/api/v3*.</span><span class="sxs-lookup"><span data-stu-id="7ddb0-129">For private feeds, substitute the host name, for example, *%hostname%/api/v3*.</span></span> |
| <span data-ttu-id="7ddb0-130">Ausführlichkeit</span><span class="sxs-lookup"><span data-stu-id="7ddb0-130">Verbosity</span></span> | <span data-ttu-id="7ddb0-131">Gibt die Anzahl der Details in der Ausgabe angezeigt: *normalen*, *stillen*, *ausführliche*.</span><span class="sxs-lookup"><span data-stu-id="7ddb0-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="7ddb0-132">Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="7ddb0-132">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="7ddb0-133">Beispiele</span><span class="sxs-lookup"><span data-stu-id="7ddb0-133">Examples</span></span>

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
