---
title: NuGet-CLI "lokal"-Befehl | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Referenz für den nuget.exe \"lokal\"-Befehl"
keywords: NuGet "lokal" Verweis "lokal"-Befehl
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: b2f62a9ab5699bfb486eee146ab7046f5240aa50
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="locals-command-nuget-cli"></a><span data-ttu-id="5d834-104">"lokal"-Befehl (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="5d834-104">locals command (NuGet CLI)</span></span>

<span data-ttu-id="5d834-105">**Gilt für:** Verpacken Sie Verbrauch &bullet; **unterstützte Versionen:** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="5d834-105">**Applies to:** package consumption &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="5d834-106">Löscht oder lokale NuGet-Ressourcen wie z. B. http-Anforderung Cache Pakete Cache und den Ordner computerweite globalen Pakete aufgelistet.</span><span class="sxs-lookup"><span data-stu-id="5d834-106">Clears or lists local NuGet resources such as the http-request cache, packages cache, and the machine-wide global packages folder.</span></span> <span data-ttu-id="5d834-107">Die `locals` -Befehl kann außerdem verwendet werden, um eine Liste der beiden Speicherorte anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="5d834-107">The `locals` command can also be used to display a list of those locations.</span></span> <span data-ttu-id="5d834-108">Weitere Informationen finden Sie unter [Verwalten von NuGet-Cache](../consume-packages/managing-the-nuget-cache.md).</span><span class="sxs-lookup"><span data-stu-id="5d834-108">For more information, see [Managing the NuGet Cache](../consume-packages/managing-the-nuget-cache.md).</span></span>

## <a name="usage"></a><span data-ttu-id="5d834-109">Verwendung</span><span class="sxs-lookup"><span data-stu-id="5d834-109">Usage</span></span>

```cli
nuget locals <cache> [options]
```

<span data-ttu-id="5d834-110">wobei `<cache>` ist einer der `all`, `http-cache`, `packages-cache`, `global-packages`, und `temp` *(3.4 +)*.</span><span class="sxs-lookup"><span data-stu-id="5d834-110">where `<cache>` is one of `all`, `http-cache`, `packages-cache`, `global-packages`, and `temp` *(3.4+)*.</span></span>

## <a name="options"></a><span data-ttu-id="5d834-111">Optionen</span><span class="sxs-lookup"><span data-stu-id="5d834-111">Options</span></span>

| <span data-ttu-id="5d834-112">Option</span><span class="sxs-lookup"><span data-stu-id="5d834-112">Option</span></span> | <span data-ttu-id="5d834-113">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="5d834-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="5d834-114">Clear</span><span class="sxs-lookup"><span data-stu-id="5d834-114">Clear</span></span> | <span data-ttu-id="5d834-115">Löscht den angegebenen Cache.</span><span class="sxs-lookup"><span data-stu-id="5d834-115">Clears the specified cache.</span></span> |
| <span data-ttu-id="5d834-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="5d834-116">ConfigFile</span></span> | <span data-ttu-id="5d834-117">Die NuGet-Konfigurationsdatei angewendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="5d834-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="5d834-118">Wenn nicht angegeben, *%AppData%\NuGet\NuGet.Config* verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="5d834-118">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="5d834-119">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="5d834-119">ForceEnglishOutput</span></span> | <span data-ttu-id="5d834-120">*(3.5 +)*  Erzwingt nuget.exe über eine invariante Kultur Englisch-basierte ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="5d834-120">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="5d834-121">Hilfe</span><span class="sxs-lookup"><span data-stu-id="5d834-121">Help</span></span> | <span data-ttu-id="5d834-122">Zeigt die Hilfe Informationen für den Befehl.</span><span class="sxs-lookup"><span data-stu-id="5d834-122">Displays help information for the command.</span></span> |
| <span data-ttu-id="5d834-123">Liste</span><span class="sxs-lookup"><span data-stu-id="5d834-123">List</span></span> | <span data-ttu-id="5d834-124">Listet den Speicherort des angegebenen Cache oder die Speicherorte der alle Caches, die bei Verwendung mit *alle*.</span><span class="sxs-lookup"><span data-stu-id="5d834-124">Lists the location of the specified cache, or the locations of all caches when used with *all*.</span></span> |
| <span data-ttu-id="5d834-125">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="5d834-125">NonInteractive</span></span> | <span data-ttu-id="5d834-126">Unterdrückt aufforderungen für Benutzereingaben oder Bestätigungen an.</span><span class="sxs-lookup"><span data-stu-id="5d834-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="5d834-127">Ausführlichkeit</span><span class="sxs-lookup"><span data-stu-id="5d834-127">Verbosity</span></span> | <span data-ttu-id="5d834-128">Gibt die Anzahl der Details in der Ausgabe angezeigt: *normalen*, *stillen*, *ausführliche*.</span><span class="sxs-lookup"><span data-stu-id="5d834-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="5d834-129">Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="5d834-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="5d834-130">Beispiele</span><span class="sxs-lookup"><span data-stu-id="5d834-130">Examples</span></span>

```cli
nuget locals all -list
nuget locals http-cache -clear
```
