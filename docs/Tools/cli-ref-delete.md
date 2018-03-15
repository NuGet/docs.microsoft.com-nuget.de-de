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
ms.openlocfilehash: b5d53b83cdccaa8e284b844786b0ec27e7afb63a
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/15/2018
---
# <a name="delete-command-nuget-cli"></a><span data-ttu-id="d78b6-104">Delete-Befehl (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="d78b6-104">delete command (NuGet CLI)</span></span>

<span data-ttu-id="d78b6-105">**Gilt für:** Verpacken Sie die Publishing &bullet; **unterstützte Versionen:** alle</span><span class="sxs-lookup"><span data-stu-id="d78b6-105">**Applies to:** package publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="d78b6-106">Löscht oder unlists ein Pakets aus der Paketquelle.</span><span class="sxs-lookup"><span data-stu-id="d78b6-106">Deletes or unlists a package from a package source.</span></span> <span data-ttu-id="d78b6-107">Für nuget.org, den Löschbefehl [unlists das Paket](../policies/deleting-packages.md).</span><span class="sxs-lookup"><span data-stu-id="d78b6-107">For nuget.org, the delete command [unlists the package](../policies/deleting-packages.md).</span></span>

## <a name="usage"></a><span data-ttu-id="d78b6-108">Verwendung</span><span class="sxs-lookup"><span data-stu-id="d78b6-108">Usage</span></span>

```cli
nuget delete <packageID> <packageVersion> [options]
```

<span data-ttu-id="d78b6-109">wobei `<packageID>` und `<packageVersion>` das genaue Paket zu löschen oder die Benutzerauswahl zu identifizieren.</span><span class="sxs-lookup"><span data-stu-id="d78b6-109">where `<packageID>` and `<packageVersion>` identify the exact package to delete or unlist.</span></span> <span data-ttu-id="d78b6-110">Das genaue Verhalten hängt von der Quelle ab.</span><span class="sxs-lookup"><span data-stu-id="d78b6-110">The exact behavior depends on the source.</span></span> <span data-ttu-id="d78b6-111">Für lokale Ordner ist z. B. das Paket gelöscht. für nuget.org ist das Paket nicht aufgeführte.</span><span class="sxs-lookup"><span data-stu-id="d78b6-111">For local folders, for instance, the package is deleted; for nuget.org the package is unlisted.</span></span>

## <a name="options"></a><span data-ttu-id="d78b6-112">Optionen</span><span class="sxs-lookup"><span data-stu-id="d78b6-112">Options</span></span>

| <span data-ttu-id="d78b6-113">Option</span><span class="sxs-lookup"><span data-stu-id="d78b6-113">Option</span></span> | <span data-ttu-id="d78b6-114">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="d78b6-114">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d78b6-115">ApiKey</span><span class="sxs-lookup"><span data-stu-id="d78b6-115">ApiKey</span></span> | <span data-ttu-id="d78b6-116">Die API-Schlüssel für das Zielrepository.</span><span class="sxs-lookup"><span data-stu-id="d78b6-116">The API key for the target repository.</span></span> <span data-ttu-id="d78b6-117">Wenn Sie nicht vorhanden ist, wird in der Datei "App.config" angegebenen verwendet.</span><span class="sxs-lookup"><span data-stu-id="d78b6-117">If not present, the one specified in the config file is used.</span></span> |
| <span data-ttu-id="d78b6-118">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="d78b6-118">ConfigFile</span></span> | <span data-ttu-id="d78b6-119">Die NuGet-Konfigurationsdatei angewendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="d78b6-119">The NuGet configuration file to apply.</span></span> <span data-ttu-id="d78b6-120">Wenn nicht angegeben, `%AppData%\NuGet\NuGet.Config` (Windows) oder `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="d78b6-120">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="d78b6-121">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="d78b6-121">ForceEnglishOutput</span></span> | <span data-ttu-id="d78b6-122">*(3.5 +)*  Erzwingt nuget.exe über eine invariante Kultur Englisch-basierte ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="d78b6-122">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="d78b6-123">Hilfe</span><span class="sxs-lookup"><span data-stu-id="d78b6-123">Help</span></span> | <span data-ttu-id="d78b6-124">Zeigt die Hilfe Informationen für den Befehl.</span><span class="sxs-lookup"><span data-stu-id="d78b6-124">Displays help information for the command.</span></span> |
| <span data-ttu-id="d78b6-125">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="d78b6-125">NonInteractive</span></span> | <span data-ttu-id="d78b6-126">Unterdrückt aufforderungen für Benutzereingaben oder Bestätigungen an.</span><span class="sxs-lookup"><span data-stu-id="d78b6-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="d78b6-127">Quelle</span><span class="sxs-lookup"><span data-stu-id="d78b6-127">Source</span></span> | <span data-ttu-id="d78b6-128">Gibt die Server-URL an.</span><span class="sxs-lookup"><span data-stu-id="d78b6-128">Specifies the server URL.</span></span> <span data-ttu-id="d78b6-129">Die URL für nuget.org lautet `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="d78b6-129">The URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="d78b6-130">Private-Feeds als Ersatz für den Hostnamen, z. B. *%hostname%/api/v3*.</span><span class="sxs-lookup"><span data-stu-id="d78b6-130">For private feeds, substitute the host name, for example, *%hostname%/api/v3*.</span></span> |
| <span data-ttu-id="d78b6-131">Ausführlichkeit</span><span class="sxs-lookup"><span data-stu-id="d78b6-131">Verbosity</span></span> | <span data-ttu-id="d78b6-132">Gibt die Anzahl der Details in der Ausgabe angezeigt: *normalen*, *stillen*, *ausführliche*.</span><span class="sxs-lookup"><span data-stu-id="d78b6-132">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="d78b6-133">Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="d78b6-133">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="d78b6-134">Beispiele</span><span class="sxs-lookup"><span data-stu-id="d78b6-134">Examples</span></span>

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
