---
title: NuGet-CLI-Locals-Befehl
description: Referenz für den Befehl "nuget.exe" Locals "
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: 38d8b9366fb2749b77c987c950da3aa9e7f029fc
ms.sourcegitcommit: 8d5121af528e68789485405e24e2100fda2868d6
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/23/2018
ms.locfileid: "42794134"
---
# <a name="locals-command-nuget-cli"></a><span data-ttu-id="1f175-103">Der Befehl „locals“ (NuGet-CLI)</span><span class="sxs-lookup"><span data-stu-id="1f175-103">locals command (NuGet CLI)</span></span>

<span data-ttu-id="1f175-104">**Gilt für:** Paket Verbrauch &bullet; **unterstützte Versionen:** 3.3 und höher</span><span class="sxs-lookup"><span data-stu-id="1f175-104">**Applies to:** package consumption &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="1f175-105">Löscht bzw. listet diese lokale NuGet-Ressourcen wie z. B. die *http-Cache*, *global-Packages* Ordner und den temporären Ordner.</span><span class="sxs-lookup"><span data-stu-id="1f175-105">Clears or lists local NuGet resources such as the *http-cache*, *global-packages* folder, and the temp folder.</span></span> <span data-ttu-id="1f175-106">Die `locals` Befehl kann auch verwendet werden, um eine Liste dieser Orte anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="1f175-106">The `locals` command can also be used to display a list of those locations.</span></span> <span data-ttu-id="1f175-107">Weitere Informationen finden Sie unter [Verwalten der globalen Paketordner und Cacheordner](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="1f175-107">For more information, see [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

## <a name="usage"></a><span data-ttu-id="1f175-108">Verwendung</span><span class="sxs-lookup"><span data-stu-id="1f175-108">Usage</span></span>

```cli
nuget locals <folder> [options]
```

<span data-ttu-id="1f175-109">wo `<folder>` ist einer der `all`, `http-cache`, `packages-cache` *(3.5 und früher)*, `global-packages`, `temp` *(3.4 und höher)*, und `plugins-cache` *(4.8 und höher)*.</span><span class="sxs-lookup"><span data-stu-id="1f175-109">where `<folder>` is one of `all`, `http-cache`, `packages-cache` *(3.5 and earlier)*, `global-packages`, `temp` *(3.4+)*, and `plugins-cache` *(4.8+)*.</span></span>

## <a name="options"></a><span data-ttu-id="1f175-110">Optionen</span><span class="sxs-lookup"><span data-stu-id="1f175-110">Options</span></span>

| <span data-ttu-id="1f175-111">Option</span><span class="sxs-lookup"><span data-stu-id="1f175-111">Option</span></span> | <span data-ttu-id="1f175-112">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="1f175-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1f175-113">Clear</span><span class="sxs-lookup"><span data-stu-id="1f175-113">Clear</span></span> | <span data-ttu-id="1f175-114">Löscht den angegebenen Ordner.</span><span class="sxs-lookup"><span data-stu-id="1f175-114">Clears the specified folder.</span></span> |
| <span data-ttu-id="1f175-115">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="1f175-115">ConfigFile</span></span> | <span data-ttu-id="1f175-116">Die NuGet-Konfigurationsdatei angewendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="1f175-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="1f175-117">Wenn nicht angegeben, `%AppData%\NuGet\NuGet.Config` (Windows) oder `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="1f175-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="1f175-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="1f175-118">ForceEnglishOutput</span></span> | <span data-ttu-id="1f175-119">*(3.5 und höher)*  Erzwingt nuget.exe über eine invariante Kultur auf Englisch basierenden ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="1f175-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="1f175-120">Hilfe</span><span class="sxs-lookup"><span data-stu-id="1f175-120">Help</span></span> | <span data-ttu-id="1f175-121">Zeigt die Informationen für den Befehl Hilfe.</span><span class="sxs-lookup"><span data-stu-id="1f175-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="1f175-122">Liste</span><span class="sxs-lookup"><span data-stu-id="1f175-122">List</span></span> | <span data-ttu-id="1f175-123">Listet den Speicherort des angegebenen Ordners oder auf die Speicherorte aller Ordner bei der Verwendung mit *alle*.</span><span class="sxs-lookup"><span data-stu-id="1f175-123">Lists the location of the specified folder, or the locations of all folders when used with *all*.</span></span> |
| <span data-ttu-id="1f175-124">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="1f175-124">NonInteractive</span></span> | <span data-ttu-id="1f175-125">Unterdrückt aufforderungen für Benutzereingaben oder Bestätigungen an.</span><span class="sxs-lookup"><span data-stu-id="1f175-125">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="1f175-126">Ausführlichkeit</span><span class="sxs-lookup"><span data-stu-id="1f175-126">Verbosity</span></span> | <span data-ttu-id="1f175-127">Gibt an, die Anzahl der Details in der Ausgabe angezeigt: *normalen*, *quiet*, *ausführliche*.</span><span class="sxs-lookup"><span data-stu-id="1f175-127">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="1f175-128">Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="1f175-128">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="1f175-129">Beispiele</span><span class="sxs-lookup"><span data-stu-id="1f175-129">Examples</span></span>

```cli
nuget locals all -list
nuget locals http-cache -clear
```

<span data-ttu-id="1f175-130">Weitere Beispiele finden Sie unter [Verwalten der globalen Paketordner und Cacheordner](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="1f175-130">For additional examples, see [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>
