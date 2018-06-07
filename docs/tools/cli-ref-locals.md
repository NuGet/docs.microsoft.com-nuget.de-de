---
title: NuGet-CLI "lokal"-Befehl
description: Referenz für den nuget.exe "lokal"-Befehl
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: 90e8c85e7a3e0e9520933e2ddd6dd84447475f2b
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818200"
---
# <a name="locals-command-nuget-cli"></a><span data-ttu-id="f37c2-103">Der Befehl „locals“ (NuGet-CLI)</span><span class="sxs-lookup"><span data-stu-id="f37c2-103">locals command (NuGet CLI)</span></span>

<span data-ttu-id="f37c2-104">**Gilt für:** Verpacken Sie Verbrauch &bullet; **unterstützte Versionen:** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="f37c2-104">**Applies to:** package consumption &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="f37c2-105">Löscht oder lokale NuGet-Ressourcen wie z. B. Listet die *http-Cache*, *globalen Pakete* Ordner und den temporären Ordner.</span><span class="sxs-lookup"><span data-stu-id="f37c2-105">Clears or lists local NuGet resources such as the *http-cache*, *global-packages* folder, and the temp folder.</span></span> <span data-ttu-id="f37c2-106">Die `locals` -Befehl kann außerdem verwendet werden, um eine Liste der beiden Speicherorte anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="f37c2-106">The `locals` command can also be used to display a list of those locations.</span></span> <span data-ttu-id="f37c2-107">Weitere Informationen finden Sie unter [Verwaltung der globalen Pakete und der Cacheordner](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="f37c2-107">For more information, see [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

## <a name="usage"></a><span data-ttu-id="f37c2-108">Verwendung</span><span class="sxs-lookup"><span data-stu-id="f37c2-108">Usage</span></span>

```cli
nuget locals <folder> [options]
```

<span data-ttu-id="f37c2-109">wobei `<folder>` ist einer der `all`, `http-cache`, `packages-cache` *(3.5 und früher)*, `global-packages`, und `temp` *(3.4 +)*.</span><span class="sxs-lookup"><span data-stu-id="f37c2-109">where `<folder>` is one of `all`, `http-cache`, `packages-cache` *(3.5 and earlier)*, `global-packages`, and `temp` *(3.4+)*.</span></span>

## <a name="options"></a><span data-ttu-id="f37c2-110">Optionen</span><span class="sxs-lookup"><span data-stu-id="f37c2-110">Options</span></span>

| <span data-ttu-id="f37c2-111">Option</span><span class="sxs-lookup"><span data-stu-id="f37c2-111">Option</span></span> | <span data-ttu-id="f37c2-112">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="f37c2-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="f37c2-113">Clear</span><span class="sxs-lookup"><span data-stu-id="f37c2-113">Clear</span></span> | <span data-ttu-id="f37c2-114">Löscht den angegebenen Ordner.</span><span class="sxs-lookup"><span data-stu-id="f37c2-114">Clears the specified folder.</span></span> |
| <span data-ttu-id="f37c2-115">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="f37c2-115">ConfigFile</span></span> | <span data-ttu-id="f37c2-116">Die NuGet-Konfigurationsdatei angewendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="f37c2-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="f37c2-117">Wenn nicht angegeben, `%AppData%\NuGet\NuGet.Config` (Windows) oder `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="f37c2-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="f37c2-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="f37c2-118">ForceEnglishOutput</span></span> | <span data-ttu-id="f37c2-119">*(3.5 +)*  Erzwingt nuget.exe über eine invariante Kultur Englisch-basierte ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="f37c2-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="f37c2-120">Hilfe</span><span class="sxs-lookup"><span data-stu-id="f37c2-120">Help</span></span> | <span data-ttu-id="f37c2-121">Zeigt die Hilfe Informationen für den Befehl.</span><span class="sxs-lookup"><span data-stu-id="f37c2-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="f37c2-122">Liste</span><span class="sxs-lookup"><span data-stu-id="f37c2-122">List</span></span> | <span data-ttu-id="f37c2-123">Listet den Speicherort des angegebenen Ordners oder der Speicherorte von allen Ordnern bei Verwendung mit *alle*.</span><span class="sxs-lookup"><span data-stu-id="f37c2-123">Lists the location of the specified folder, or the locations of all folders when used with *all*.</span></span> |
| <span data-ttu-id="f37c2-124">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="f37c2-124">NonInteractive</span></span> | <span data-ttu-id="f37c2-125">Unterdrückt aufforderungen für Benutzereingaben oder Bestätigungen an.</span><span class="sxs-lookup"><span data-stu-id="f37c2-125">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="f37c2-126">Ausführlichkeit</span><span class="sxs-lookup"><span data-stu-id="f37c2-126">Verbosity</span></span> | <span data-ttu-id="f37c2-127">Gibt die Anzahl der Details in der Ausgabe angezeigt: *normalen*, *stillen*, *ausführliche*.</span><span class="sxs-lookup"><span data-stu-id="f37c2-127">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="f37c2-128">Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="f37c2-128">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="f37c2-129">Beispiele</span><span class="sxs-lookup"><span data-stu-id="f37c2-129">Examples</span></span>

```cli
nuget locals all -list
nuget locals http-cache -clear
```

<span data-ttu-id="f37c2-130">Weitere Beispiele finden Sie unter [Verwaltung der globalen Pakete und der Cacheordner](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="f37c2-130">For additional examples, see [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>
