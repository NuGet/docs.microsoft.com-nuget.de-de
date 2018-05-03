---
title: NuGet-CLI "lokal"-Befehl
description: Referenz für den nuget.exe "lokal"-Befehl
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: ac07dc306bc23c2fedd33c5627e8d34a6098387c
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="locals-command-nuget-cli"></a><span data-ttu-id="ec94f-103">"lokal"-Befehl (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="ec94f-103">locals command (NuGet CLI)</span></span>

<span data-ttu-id="ec94f-104">**Gilt für:** Verpacken Sie Verbrauch &bullet; **unterstützte Versionen:** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="ec94f-104">**Applies to:** package consumption &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="ec94f-105">Löscht oder lokale NuGet-Ressourcen wie z. B. Listet die *http-Cache*, *globalen Pakete* Ordner und den temporären Ordner.</span><span class="sxs-lookup"><span data-stu-id="ec94f-105">Clears or lists local NuGet resources such as the *http-cache*, *global-packages* folder, and the temp folder.</span></span> <span data-ttu-id="ec94f-106">Die `locals` -Befehl kann außerdem verwendet werden, um eine Liste der beiden Speicherorte anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="ec94f-106">The `locals` command can also be used to display a list of those locations.</span></span> <span data-ttu-id="ec94f-107">Weitere Informationen finden Sie unter [Verwaltung der globalen Pakete und der Cacheordner](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="ec94f-107">For more information, see [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

## <a name="usage"></a><span data-ttu-id="ec94f-108">Verwendung</span><span class="sxs-lookup"><span data-stu-id="ec94f-108">Usage</span></span>

```cli
nuget locals <folder> [options]
```

<span data-ttu-id="ec94f-109">wobei `<folder>` ist einer der `all`, `http-cache`, `packages-cache` *(3.5 und früher)*, `global-packages`, und `temp` *(3.4 +)*.</span><span class="sxs-lookup"><span data-stu-id="ec94f-109">where `<folder>` is one of `all`, `http-cache`, `packages-cache` *(3.5 and earlier)*, `global-packages`, and `temp` *(3.4+)*.</span></span>

## <a name="options"></a><span data-ttu-id="ec94f-110">Optionen</span><span class="sxs-lookup"><span data-stu-id="ec94f-110">Options</span></span>

| <span data-ttu-id="ec94f-111">Option</span><span class="sxs-lookup"><span data-stu-id="ec94f-111">Option</span></span> | <span data-ttu-id="ec94f-112">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="ec94f-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ec94f-113">Clear</span><span class="sxs-lookup"><span data-stu-id="ec94f-113">Clear</span></span> | <span data-ttu-id="ec94f-114">Löscht den angegebenen Ordner.</span><span class="sxs-lookup"><span data-stu-id="ec94f-114">Clears the specified folder.</span></span> |
| <span data-ttu-id="ec94f-115">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="ec94f-115">ConfigFile</span></span> | <span data-ttu-id="ec94f-116">Die NuGet-Konfigurationsdatei angewendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="ec94f-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="ec94f-117">Wenn nicht angegeben, `%AppData%\NuGet\NuGet.Config` (Windows) oder `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="ec94f-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="ec94f-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="ec94f-118">ForceEnglishOutput</span></span> | <span data-ttu-id="ec94f-119">*(3.5 +)*  Erzwingt nuget.exe über eine invariante Kultur Englisch-basierte ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="ec94f-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="ec94f-120">Hilfe</span><span class="sxs-lookup"><span data-stu-id="ec94f-120">Help</span></span> | <span data-ttu-id="ec94f-121">Zeigt die Hilfe Informationen für den Befehl.</span><span class="sxs-lookup"><span data-stu-id="ec94f-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="ec94f-122">Liste</span><span class="sxs-lookup"><span data-stu-id="ec94f-122">List</span></span> | <span data-ttu-id="ec94f-123">Listet den Speicherort des angegebenen Ordners oder der Speicherorte von allen Ordnern bei Verwendung mit *alle*.</span><span class="sxs-lookup"><span data-stu-id="ec94f-123">Lists the location of the specified folder, or the locations of all folders when used with *all*.</span></span> |
| <span data-ttu-id="ec94f-124">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="ec94f-124">NonInteractive</span></span> | <span data-ttu-id="ec94f-125">Unterdrückt aufforderungen für Benutzereingaben oder Bestätigungen an.</span><span class="sxs-lookup"><span data-stu-id="ec94f-125">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="ec94f-126">Ausführlichkeit</span><span class="sxs-lookup"><span data-stu-id="ec94f-126">Verbosity</span></span> | <span data-ttu-id="ec94f-127">Gibt die Anzahl der Details in der Ausgabe angezeigt: *normalen*, *stillen*, *ausführliche*.</span><span class="sxs-lookup"><span data-stu-id="ec94f-127">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="ec94f-128">Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="ec94f-128">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="ec94f-129">Beispiele</span><span class="sxs-lookup"><span data-stu-id="ec94f-129">Examples</span></span>

```cli
nuget locals all -list
nuget locals http-cache -clear
```

<span data-ttu-id="ec94f-130">Weitere Beispiele finden Sie unter [Verwaltung der globalen Pakete und der Cacheordner](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="ec94f-130">For additional examples, see [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>
