---
title: NuGet CLI delete-Befehl | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: c213a07a-711d-47e0-9ee6-1d582e6cdb69
description: "Referenz für den Löschbefehl nuget.exe"
keywords: "NuGet Verweis löschen, löschen Sie die Paket-Befehl"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 92af9dc356f3932347864976496e0ba1216496c9
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/14/2017
---
# <a name="delete-command-nuget-cli"></a><span data-ttu-id="0152c-104">Delete-Befehl (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="0152c-104">delete command (NuGet CLI)</span></span>

<span data-ttu-id="0152c-105">**Gilt für:** Verpacken Sie die Publishing &bullet; **unterstützte Versionen:** alle</span><span class="sxs-lookup"><span data-stu-id="0152c-105">**Applies to:** package publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="0152c-106">Löscht oder unlists ein Pakets aus der Paketquelle.</span><span class="sxs-lookup"><span data-stu-id="0152c-106">Deletes or unlists a package from a package source.</span></span> <span data-ttu-id="0152c-107">Für nuget.org, den Löschbefehl [unlists das Paket](../policies/Deleting-Packages.md).</span><span class="sxs-lookup"><span data-stu-id="0152c-107">For nuget.org, the delete command [unlists the package](../policies/Deleting-Packages.md).</span></span>

## <a name="usage"></a><span data-ttu-id="0152c-108">Verwendung</span><span class="sxs-lookup"><span data-stu-id="0152c-108">Usage</span></span>

```
nuget delete <packageID> <packageVersion> [options]
```

<span data-ttu-id="0152c-109">wobei `<packageID>` und `<packageVersion>` das genaue Paket zu löschen oder die Benutzerauswahl zu identifizieren.</span><span class="sxs-lookup"><span data-stu-id="0152c-109">where `<packageID>` and `<packageVersion>` identify the exact package to delete or unlist.</span></span> <span data-ttu-id="0152c-110">Das genaue Verhalten hängt von der Quelle ab.</span><span class="sxs-lookup"><span data-stu-id="0152c-110">The exact behavior depends on the source.</span></span> <span data-ttu-id="0152c-111">Für lokale Ordner ist z. B. das Paket gelöscht. für nuget.org ist das Paket nicht aufgeführte.</span><span class="sxs-lookup"><span data-stu-id="0152c-111">For local folders, for instance, the package is deleted; for nuget.org the package is unlisted.</span></span>

## <a name="options"></a><span data-ttu-id="0152c-112">Optionen</span><span class="sxs-lookup"><span data-stu-id="0152c-112">Options</span></span>

| <span data-ttu-id="0152c-113">Option</span><span class="sxs-lookup"><span data-stu-id="0152c-113">Option</span></span> | <span data-ttu-id="0152c-114">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="0152c-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="0152c-115">"apikey"</span><span class="sxs-lookup"><span data-stu-id="0152c-115">ApiKey</span></span> | <span data-ttu-id="0152c-116">Die API-Schlüssel für das Zielrepository.</span><span class="sxs-lookup"><span data-stu-id="0152c-116">The API key for the target repository.</span></span> <span data-ttu-id="0152c-117">Wenn Sie nicht vorhanden ist, der im angegebenen *%AppData%\NuGet\NuGet.Config* verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="0152c-117">If not present, the one specified in *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="0152c-118">"ConfigFile" hinzu</span><span class="sxs-lookup"><span data-stu-id="0152c-118">ConfigFile</span></span> | <span data-ttu-id="0152c-119">*(2,5 +)*  Das NuGet-Konfigurationsdatei angewendet.</span><span class="sxs-lookup"><span data-stu-id="0152c-119">*(2.5+)* The NuGet configuration file to apply.</span></span> <span data-ttu-id="0152c-120">Wenn nicht angegeben, *%AppData%\NuGet\NuGet.Config* verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="0152c-120">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="0152c-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="0152c-121">ForceEnglishOutput</span></span> | <span data-ttu-id="0152c-122">*(3.5 +)*  Erzwingt nuget.exe über eine invariante Kultur Englisch-basierte ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="0152c-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="0152c-123">Hilfe</span><span class="sxs-lookup"><span data-stu-id="0152c-123">Help</span></span> | <span data-ttu-id="0152c-124">Zeigt die Hilfe Informationen für den Befehl.</span><span class="sxs-lookup"><span data-stu-id="0152c-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="0152c-125">Nicht interaktive</span><span class="sxs-lookup"><span data-stu-id="0152c-125">NonInteractive</span></span> | <span data-ttu-id="0152c-126">Unterdrückt aufforderungen für Benutzereingaben oder Bestätigungen an.</span><span class="sxs-lookup"><span data-stu-id="0152c-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="0152c-127">Quelle</span><span class="sxs-lookup"><span data-stu-id="0152c-127">Source</span></span> | <span data-ttu-id="0152c-128">Gibt die Server-URL an.</span><span class="sxs-lookup"><span data-stu-id="0152c-128">Specifies the server URL.</span></span> <span data-ttu-id="0152c-129">Die URL für nuget.org lautet `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="0152c-129">The URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="0152c-130">Private-Feeds als Ersatz für den Hostnamen, z. B. *%hostname%/api/v3*.</span><span class="sxs-lookup"><span data-stu-id="0152c-130">For private feeds, substitute the host name, for example, *%hostname%/api/v3*.</span></span> |
| <span data-ttu-id="0152c-131">Ausführlichkeit</span><span class="sxs-lookup"><span data-stu-id="0152c-131">Verbosity</span></span> | <span data-ttu-id="0152c-132">Gibt die Anzahl der Details in der Ausgabe angezeigt: *normalen*, *stillen*, *detaillierte (2.5 und höher)*.</span><span class="sxs-lookup"><span data-stu-id="0152c-132">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed (2.5+)*.</span></span> |

<span data-ttu-id="0152c-133">Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="0152c-133">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="0152c-134">Beispiele</span><span class="sxs-lookup"><span data-stu-id="0152c-134">Examples</span></span>

```
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
