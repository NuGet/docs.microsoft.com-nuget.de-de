---
title: NuGet CLI delete-Befehl | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Referenz für den Löschbefehl nuget.exe"
keywords: "NuGet Verweis löschen, löschen Sie die Paket-Befehl"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 3890e33ab0fc425e1c2ee39631ade57ea9b92bc9
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="delete-command-nuget-cli"></a><span data-ttu-id="86515-104">Delete-Befehl (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="86515-104">delete command (NuGet CLI)</span></span>

<span data-ttu-id="86515-105">**Gilt für:** Verpacken Sie die Publishing &bullet; **unterstützte Versionen:** alle</span><span class="sxs-lookup"><span data-stu-id="86515-105">**Applies to:** package publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="86515-106">Löscht oder unlists ein Pakets aus der Paketquelle.</span><span class="sxs-lookup"><span data-stu-id="86515-106">Deletes or unlists a package from a package source.</span></span> <span data-ttu-id="86515-107">Für nuget.org, den Löschbefehl [unlists das Paket](../policies/Deleting-Packages.md).</span><span class="sxs-lookup"><span data-stu-id="86515-107">For nuget.org, the delete command [unlists the package](../policies/Deleting-Packages.md).</span></span>

## <a name="usage"></a><span data-ttu-id="86515-108">Verwendung</span><span class="sxs-lookup"><span data-stu-id="86515-108">Usage</span></span>

```cli
nuget delete <packageID> <packageVersion> [options]
```

<span data-ttu-id="86515-109">wobei `<packageID>` und `<packageVersion>` das genaue Paket zu löschen oder die Benutzerauswahl zu identifizieren.</span><span class="sxs-lookup"><span data-stu-id="86515-109">where `<packageID>` and `<packageVersion>` identify the exact package to delete or unlist.</span></span> <span data-ttu-id="86515-110">Das genaue Verhalten hängt von der Quelle ab.</span><span class="sxs-lookup"><span data-stu-id="86515-110">The exact behavior depends on the source.</span></span> <span data-ttu-id="86515-111">Für lokale Ordner ist z. B. das Paket gelöscht. für nuget.org ist das Paket nicht aufgeführte.</span><span class="sxs-lookup"><span data-stu-id="86515-111">For local folders, for instance, the package is deleted; for nuget.org the package is unlisted.</span></span>

## <a name="options"></a><span data-ttu-id="86515-112">Optionen</span><span class="sxs-lookup"><span data-stu-id="86515-112">Options</span></span>

| <span data-ttu-id="86515-113">Option</span><span class="sxs-lookup"><span data-stu-id="86515-113">Option</span></span> | <span data-ttu-id="86515-114">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="86515-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="86515-115">ApiKey</span><span class="sxs-lookup"><span data-stu-id="86515-115">ApiKey</span></span> | <span data-ttu-id="86515-116">Die API-Schlüssel für das Zielrepository.</span><span class="sxs-lookup"><span data-stu-id="86515-116">The API key for the target repository.</span></span> <span data-ttu-id="86515-117">Wenn Sie nicht vorhanden ist, der im angegebenen *%AppData%\NuGet\NuGet.Config* verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="86515-117">If not present, the one specified in *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="86515-118">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="86515-118">ConfigFile</span></span> | <span data-ttu-id="86515-119">Die NuGet-Konfigurationsdatei angewendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="86515-119">The NuGet configuration file to apply.</span></span> <span data-ttu-id="86515-120">Wenn nicht angegeben, *%AppData%\NuGet\NuGet.Config* verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="86515-120">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="86515-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="86515-121">ForceEnglishOutput</span></span> | <span data-ttu-id="86515-122">*(3.5 +)*  Erzwingt nuget.exe über eine invariante Kultur Englisch-basierte ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="86515-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="86515-123">Hilfe</span><span class="sxs-lookup"><span data-stu-id="86515-123">Help</span></span> | <span data-ttu-id="86515-124">Zeigt die Hilfe Informationen für den Befehl.</span><span class="sxs-lookup"><span data-stu-id="86515-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="86515-125">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="86515-125">NonInteractive</span></span> | <span data-ttu-id="86515-126">Unterdrückt aufforderungen für Benutzereingaben oder Bestätigungen an.</span><span class="sxs-lookup"><span data-stu-id="86515-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="86515-127">Quelle</span><span class="sxs-lookup"><span data-stu-id="86515-127">Source</span></span> | <span data-ttu-id="86515-128">Gibt die Server-URL an.</span><span class="sxs-lookup"><span data-stu-id="86515-128">Specifies the server URL.</span></span> <span data-ttu-id="86515-129">Die URL für nuget.org lautet `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="86515-129">The URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="86515-130">Private-Feeds als Ersatz für den Hostnamen, z. B. *%hostname%/api/v3*.</span><span class="sxs-lookup"><span data-stu-id="86515-130">For private feeds, substitute the host name, for example, *%hostname%/api/v3*.</span></span> |
| <span data-ttu-id="86515-131">Ausführlichkeit</span><span class="sxs-lookup"><span data-stu-id="86515-131">Verbosity</span></span> | <span data-ttu-id="86515-132">Gibt die Anzahl der Details in der Ausgabe angezeigt: *normalen*, *stillen*, *ausführliche*.</span><span class="sxs-lookup"><span data-stu-id="86515-132">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="86515-133">Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="86515-133">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="86515-134">Beispiele</span><span class="sxs-lookup"><span data-stu-id="86515-134">Examples</span></span>

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
