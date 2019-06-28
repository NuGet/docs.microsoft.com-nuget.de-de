---
title: NuGet-CLI-Befehl "löschen"
description: Referenz für die nuget.exe-Delete-Befehl
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3ea2dc3e87d0a626704fe5623d39eaf5bd3f3446
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426109"
---
# <a name="delete-command-nuget-cli"></a><span data-ttu-id="a2e13-103">Delete-Befehl (NuGet-CLI)</span><span class="sxs-lookup"><span data-stu-id="a2e13-103">delete command (NuGet CLI)</span></span>

<span data-ttu-id="a2e13-104">**Gilt für:** Paket veröffentlichen &bullet; **unterstützte Versionen:** alle</span><span class="sxs-lookup"><span data-stu-id="a2e13-104">**Applies to:** package publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="a2e13-105">Löscht oder hebt dessen Auflistung auf ein Paket aus der Paketquelle.</span><span class="sxs-lookup"><span data-stu-id="a2e13-105">Deletes or unlists a package from a package source.</span></span> <span data-ttu-id="a2e13-106">Für "nuget.org" der Delete-Befehl [hebt dessen Auflistung auf das Paket](../nuget-org/policies/deleting-packages.md).</span><span class="sxs-lookup"><span data-stu-id="a2e13-106">For nuget.org, the delete command [unlists the package](../nuget-org/policies/deleting-packages.md).</span></span>

## <a name="usage"></a><span data-ttu-id="a2e13-107">Verwendung</span><span class="sxs-lookup"><span data-stu-id="a2e13-107">Usage</span></span>

```cli
nuget delete <packageID> <packageVersion> [options]
```

<span data-ttu-id="a2e13-108">wo `<packageID>` und `<packageVersion>` identifizieren Sie das genaue Paket löschen oder aus der Liste entfernen.</span><span class="sxs-lookup"><span data-stu-id="a2e13-108">where `<packageID>` and `<packageVersion>` identify the exact package to delete or unlist.</span></span> <span data-ttu-id="a2e13-109">Das genaue Verhalten hängt von der Quelle ab.</span><span class="sxs-lookup"><span data-stu-id="a2e13-109">The exact behavior depends on the source.</span></span> <span data-ttu-id="a2e13-110">Für lokale Ordner ist wird z. B. das Paket gelöscht. für "NuGet.org" für das Paket nicht aufgelistet ist.</span><span class="sxs-lookup"><span data-stu-id="a2e13-110">For local folders, for instance, the package is deleted; for nuget.org the package is unlisted.</span></span>

## <a name="options"></a><span data-ttu-id="a2e13-111">Optionen</span><span class="sxs-lookup"><span data-stu-id="a2e13-111">Options</span></span>

| <span data-ttu-id="a2e13-112">Option</span><span class="sxs-lookup"><span data-stu-id="a2e13-112">Option</span></span> | <span data-ttu-id="a2e13-113">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="a2e13-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="a2e13-114">ApiKey</span><span class="sxs-lookup"><span data-stu-id="a2e13-114">ApiKey</span></span> | <span data-ttu-id="a2e13-115">Die API-Schlüssel für die Ziel-Repository.</span><span class="sxs-lookup"><span data-stu-id="a2e13-115">The API key for the target repository.</span></span> <span data-ttu-id="a2e13-116">Wenn nicht vorhanden ist, wird angegeben, in der Konfigurationsdatei verwendet.</span><span class="sxs-lookup"><span data-stu-id="a2e13-116">If not present, the one specified in the config file is used.</span></span> |
| <span data-ttu-id="a2e13-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="a2e13-117">ConfigFile</span></span> | <span data-ttu-id="a2e13-118">Die NuGet-Konfigurationsdatei angewendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="a2e13-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="a2e13-119">Wenn nicht angegeben, `%AppData%\NuGet\NuGet.Config` (Windows) oder `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="a2e13-119">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="a2e13-120">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="a2e13-120">ForceEnglishOutput</span></span> | <span data-ttu-id="a2e13-121">*(3.5 und höher)*  Erzwingt nuget.exe über eine invariante Kultur auf Englisch basierenden ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="a2e13-121">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="a2e13-122">Help</span><span class="sxs-lookup"><span data-stu-id="a2e13-122">Help</span></span> | <span data-ttu-id="a2e13-123">Zeigt die Informationen für den Befehl Hilfe.</span><span class="sxs-lookup"><span data-stu-id="a2e13-123">Displays help information for the command.</span></span> |
| <span data-ttu-id="a2e13-124">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="a2e13-124">NonInteractive</span></span> | <span data-ttu-id="a2e13-125">Unterdrückt aufforderungen für Benutzereingaben oder Bestätigungen an.</span><span class="sxs-lookup"><span data-stu-id="a2e13-125">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="a2e13-126">Source</span><span class="sxs-lookup"><span data-stu-id="a2e13-126">Source</span></span> | <span data-ttu-id="a2e13-127">Gibt die Server-URL an.</span><span class="sxs-lookup"><span data-stu-id="a2e13-127">Specifies the server URL.</span></span> <span data-ttu-id="a2e13-128">Die URL für nuget.org `https://api.nuget.org/v3/index.json`.</span><span class="sxs-lookup"><span data-stu-id="a2e13-128">The URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="a2e13-129">Ersetzen Sie für private Feeds den Hostnamen ein, z. B. *%hostname%/api/v3*.</span><span class="sxs-lookup"><span data-stu-id="a2e13-129">For private feeds, substitute the host name, for example, *%hostname%/api/v3*.</span></span> |
| <span data-ttu-id="a2e13-130">Verbosity</span><span class="sxs-lookup"><span data-stu-id="a2e13-130">Verbosity</span></span> | <span data-ttu-id="a2e13-131">Gibt an, die Anzahl der Details in der Ausgabe angezeigt: *normalen*, *quiet*, *ausführliche*.</span><span class="sxs-lookup"><span data-stu-id="a2e13-131">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="a2e13-132">Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="a2e13-132">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="a2e13-133">Beispiele</span><span class="sxs-lookup"><span data-stu-id="a2e13-133">Examples</span></span>

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
