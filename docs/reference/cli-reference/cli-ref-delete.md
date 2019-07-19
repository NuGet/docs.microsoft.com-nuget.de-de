---
title: Befehl "nuget CLI Delete"
description: Referenz für den Befehl "nuget. exe Delete"
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 5185bc8b89f645a0a0f4d3241b5fa04e09560ede
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327837"
---
# <a name="delete-command-nuget-cli"></a><span data-ttu-id="6752f-103">DELETE-Befehl (nuget-CLI)</span><span class="sxs-lookup"><span data-stu-id="6752f-103">delete command (NuGet CLI)</span></span>

<span data-ttu-id="6752f-104">**Gilt für:** &bullet; **unterstützte Versionen** der Paket Veröffentlichung: alle</span><span class="sxs-lookup"><span data-stu-id="6752f-104">**Applies to:** package publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="6752f-105">Löscht ein Paket aus einer Paketquelle oder hebt die Auflistung auf.</span><span class="sxs-lookup"><span data-stu-id="6752f-105">Deletes or unlists a package from a package source.</span></span> <span data-ttu-id="6752f-106">Bei nuget.org wird das Paket durch den DELETE-Befehl [nicht mehr aufgelistet](../../nuget-org/policies/deleting-packages.md).</span><span class="sxs-lookup"><span data-stu-id="6752f-106">For nuget.org, the delete command [unlists the package](../../nuget-org/policies/deleting-packages.md).</span></span>

## <a name="usage"></a><span data-ttu-id="6752f-107">Verwendung</span><span class="sxs-lookup"><span data-stu-id="6752f-107">Usage</span></span>

```cli
nuget delete <packageID> <packageVersion> [options]
```

<span data-ttu-id="6752f-108">`<packageID>` dabeiidentifizierenSiedasgenauePaket,dasgelöschtoderdieAuflistungder`<packageVersion>` Auflistung entfernt werden soll.</span><span class="sxs-lookup"><span data-stu-id="6752f-108">where `<packageID>` and `<packageVersion>` identify the exact package to delete or unlist.</span></span> <span data-ttu-id="6752f-109">Das genaue Verhalten hängt von der Quelle ab.</span><span class="sxs-lookup"><span data-stu-id="6752f-109">The exact behavior depends on the source.</span></span> <span data-ttu-id="6752f-110">Für lokale Ordner wird das Paket beispielsweise gelöscht. für nuget.org wird das Paket nicht aufgelistet.</span><span class="sxs-lookup"><span data-stu-id="6752f-110">For local folders, for instance, the package is deleted; for nuget.org the package is unlisted.</span></span>

## <a name="options"></a><span data-ttu-id="6752f-111">Optionen</span><span class="sxs-lookup"><span data-stu-id="6752f-111">Options</span></span>

| <span data-ttu-id="6752f-112">Option</span><span class="sxs-lookup"><span data-stu-id="6752f-112">Option</span></span> | <span data-ttu-id="6752f-113">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="6752f-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="6752f-114">ApiKey</span><span class="sxs-lookup"><span data-stu-id="6752f-114">ApiKey</span></span> | <span data-ttu-id="6752f-115">Der API-Schlüssel für das Zielrepository.</span><span class="sxs-lookup"><span data-stu-id="6752f-115">The API key for the target repository.</span></span> <span data-ttu-id="6752f-116">Wenn kein Wert vorhanden ist, wird der in der Konfigurationsdatei angegebene verwendet.</span><span class="sxs-lookup"><span data-stu-id="6752f-116">If not present, the one specified in the config file is used.</span></span> |
| <span data-ttu-id="6752f-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="6752f-117">ConfigFile</span></span> | <span data-ttu-id="6752f-118">Die anzuwendende nuget-Konfigurationsdatei.</span><span class="sxs-lookup"><span data-stu-id="6752f-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="6752f-119">Wenn nichts angegeben ist `%AppData%\NuGet\NuGet.Config` , wird (Windows `~/.nuget/NuGet/NuGet.Config` ) oder (Mac/Linux) verwendet.</span><span class="sxs-lookup"><span data-stu-id="6752f-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="6752f-120">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="6752f-120">ForceEnglishOutput</span></span> | <span data-ttu-id="6752f-121">*(3.5* und höher) Erzwingt, dass "nuget. exe" mit einer invarianten, englischen Kultur ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="6752f-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="6752f-122">Help</span><span class="sxs-lookup"><span data-stu-id="6752f-122">Help</span></span> | <span data-ttu-id="6752f-123">Zeigt Hilfe Informationen für den Befehl an.</span><span class="sxs-lookup"><span data-stu-id="6752f-123">Displays help information for the command.</span></span> |
| <span data-ttu-id="6752f-124">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="6752f-124">NonInteractive</span></span> | <span data-ttu-id="6752f-125">Unterdrückt Eingabe Aufforderungen für Benutzereingaben oder Bestätigungen.</span><span class="sxs-lookup"><span data-stu-id="6752f-125">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="6752f-126">Source</span><span class="sxs-lookup"><span data-stu-id="6752f-126">Source</span></span> | <span data-ttu-id="6752f-127">Gibt die Server-URL an.</span><span class="sxs-lookup"><span data-stu-id="6752f-127">Specifies the server URL.</span></span> <span data-ttu-id="6752f-128">Die URL für nuget.org ist `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="6752f-128">The URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="6752f-129">Ersetzen Sie für private Feeds den Hostnamen, z. b. " *% Hostname%/API/v3*".</span><span class="sxs-lookup"><span data-stu-id="6752f-129">For private feeds, substitute the host name, for example, *%hostname%/api/v3*.</span></span> |
| <span data-ttu-id="6752f-130">Verbosity</span><span class="sxs-lookup"><span data-stu-id="6752f-130">Verbosity</span></span> | <span data-ttu-id="6752f-131">Gibt den Umfang der in der Ausgabe angezeigten Details an: *Normal*, *quiet*, *ausführlich*.</span><span class="sxs-lookup"><span data-stu-id="6752f-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="6752f-132">Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="6752f-132">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="6752f-133">Beispiele</span><span class="sxs-lookup"><span data-stu-id="6752f-133">Examples</span></span>

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
