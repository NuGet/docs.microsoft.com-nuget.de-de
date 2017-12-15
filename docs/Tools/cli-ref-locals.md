---
title: NuGet-CLI "lokal"-Befehl | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 7f672c7c-74c9-4296-bc27-4d47882b541c
description: "Referenz für den nuget.exe \"lokal\"-Befehl"
keywords: NuGet "lokal" Verweis "lokal"-Befehl
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 8cc06eedc20507e2bdd210e40c471ff551b89563
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/14/2017
---
## <a name="locals-command-nuget-cli"></a><span data-ttu-id="fe378-104">"lokal"-Befehl (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="fe378-104">locals command (NuGet CLI)</span></span>

<span data-ttu-id="fe378-105">**Gilt für:** Verpacken Sie Verbrauch &bullet; **unterstützte Versionen:** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="fe378-105">**Applies to:** package consumption &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="fe378-106">Löscht oder lokale NuGet-Ressourcen wie z. B. http-Anforderung Cache Pakete Cache und den Ordner computerweite globalen Pakete aufgelistet.</span><span class="sxs-lookup"><span data-stu-id="fe378-106">Clears or lists local NuGet resources such as the http-request cache, packages cache, and the machine-wide global packages folder.</span></span> <span data-ttu-id="fe378-107">Die `locals` -Befehl kann außerdem verwendet werden, um eine Liste der beiden Speicherorte anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="fe378-107">The `locals` command can also be used to display a list of those locations.</span></span> <span data-ttu-id="fe378-108">Weitere Informationen finden Sie unter [Verwalten von NuGet-Cache](../consume-packages/managing-the-nuget-cache.md).</span><span class="sxs-lookup"><span data-stu-id="fe378-108">For more information, see [Managing the NuGet Cache](../consume-packages/managing-the-nuget-cache.md).</span></span>

## <a name="usage"></a><span data-ttu-id="fe378-109">Verwendung</span><span class="sxs-lookup"><span data-stu-id="fe378-109">Usage</span></span>

```
nuget locals <cache> [options]
```

<span data-ttu-id="fe378-110">wobei `<cache>` ist einer der `all`, `http-cache`, `packages-cache`, `global-packages`, und `temp` *(3.4 +)*.</span><span class="sxs-lookup"><span data-stu-id="fe378-110">where `<cache>` is one of `all`, `http-cache`, `packages-cache`, `global-packages`, and `temp` *(3.4+)*.</span></span>

## <a name="options"></a><span data-ttu-id="fe378-111">Optionen</span><span class="sxs-lookup"><span data-stu-id="fe378-111">Options</span></span>

| <span data-ttu-id="fe378-112">Option</span><span class="sxs-lookup"><span data-stu-id="fe378-112">Option</span></span> | <span data-ttu-id="fe378-113">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="fe378-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="fe378-114">Clear</span><span class="sxs-lookup"><span data-stu-id="fe378-114">Clear</span></span> | <span data-ttu-id="fe378-115">Löscht den angegebenen Cache.</span><span class="sxs-lookup"><span data-stu-id="fe378-115">Clears the specified cache.</span></span> |
| <span data-ttu-id="fe378-116">"ConfigFile" hinzu</span><span class="sxs-lookup"><span data-stu-id="fe378-116">ConfigFile</span></span> | <span data-ttu-id="fe378-117">Die NuGet-Konfigurationsdatei angewendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="fe378-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="fe378-118">Wenn nicht angegeben, *%AppData%\NuGet\NuGet.Config* verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="fe378-118">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="fe378-119">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="fe378-119">ForceEnglishOutput</span></span> | <span data-ttu-id="fe378-120">*(3.5 +)*  Erzwingt nuget.exe über eine invariante Kultur Englisch-basierte ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="fe378-120">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="fe378-121">Hilfe</span><span class="sxs-lookup"><span data-stu-id="fe378-121">Help</span></span> | <span data-ttu-id="fe378-122">Zeigt die Hilfe Informationen für den Befehl.</span><span class="sxs-lookup"><span data-stu-id="fe378-122">Displays help information for the command.</span></span> |
| <span data-ttu-id="fe378-123">Liste</span><span class="sxs-lookup"><span data-stu-id="fe378-123">List</span></span> | <span data-ttu-id="fe378-124">Listet den Speicherort des angegebenen Cache oder die Speicherorte der alle Caches, die bei Verwendung mit *alle*.</span><span class="sxs-lookup"><span data-stu-id="fe378-124">Lists the location of the specified cache, or the locations of all caches when used with *all*.</span></span> |
| <span data-ttu-id="fe378-125">Nicht interaktive</span><span class="sxs-lookup"><span data-stu-id="fe378-125">NonInteractive</span></span> | <span data-ttu-id="fe378-126">Unterdrückt aufforderungen für Benutzereingaben oder Bestätigungen an.</span><span class="sxs-lookup"><span data-stu-id="fe378-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="fe378-127">Ausführlichkeit</span><span class="sxs-lookup"><span data-stu-id="fe378-127">Verbosity</span></span> | <span data-ttu-id="fe378-128">Gibt die Anzahl der Details in der Ausgabe angezeigt: *normalen*, *stillen*, *ausführliche*.</span><span class="sxs-lookup"><span data-stu-id="fe378-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="fe378-129">Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="fe378-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="fe378-130">Beispiele</span><span class="sxs-lookup"><span data-stu-id="fe378-130">Examples</span></span>

```
nuget locals all -list
nuget locals http-cache -clear
```
