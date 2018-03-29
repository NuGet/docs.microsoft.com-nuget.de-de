---
title: NuGet-CLI "lokal"-Befehl | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/19/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Referenz für den nuget.exe "lokal"-Befehl
keywords: NuGet "lokal" Verweis "lokal"-Befehl
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 0122c79e55b12838bd123cf91bfcbc5dbbd2a65c
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="locals-command-nuget-cli"></a><span data-ttu-id="653c7-104">"lokal"-Befehl (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="653c7-104">locals command (NuGet CLI)</span></span>

<span data-ttu-id="653c7-105">**Gilt für:** Verpacken Sie Verbrauch &bullet; **unterstützte Versionen:** 3.3 +</span><span class="sxs-lookup"><span data-stu-id="653c7-105">**Applies to:** package consumption &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="653c7-106">Löscht oder lokale NuGet-Ressourcen wie z. B. Listet die *http-Cache*, *globalen Pakete* Ordner und den temporären Ordner.</span><span class="sxs-lookup"><span data-stu-id="653c7-106">Clears or lists local NuGet resources such as the *http-cache*, *global-packages* folder, and the temp folder.</span></span> <span data-ttu-id="653c7-107">Die `locals` -Befehl kann außerdem verwendet werden, um eine Liste der beiden Speicherorte anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="653c7-107">The `locals` command can also be used to display a list of those locations.</span></span> <span data-ttu-id="653c7-108">Weitere Informationen finden Sie unter [Verwaltung der globalen Pakete und der Cacheordner](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="653c7-108">For more information, see [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

## <a name="usage"></a><span data-ttu-id="653c7-109">Verwendung</span><span class="sxs-lookup"><span data-stu-id="653c7-109">Usage</span></span>

```cli
nuget locals <folder> [options]
```

<span data-ttu-id="653c7-110">wobei `<folder>` ist einer der `all`, `http-cache`, `packages-cache` *(3.5 und früher)*, `global-packages`, und `temp` *(3.4 +)*.</span><span class="sxs-lookup"><span data-stu-id="653c7-110">where `<folder>` is one of `all`, `http-cache`, `packages-cache` *(3.5 and earlier)*, `global-packages`, and `temp` *(3.4+)*.</span></span>

## <a name="options"></a><span data-ttu-id="653c7-111">Optionen</span><span class="sxs-lookup"><span data-stu-id="653c7-111">Options</span></span>

| <span data-ttu-id="653c7-112">Option</span><span class="sxs-lookup"><span data-stu-id="653c7-112">Option</span></span> | <span data-ttu-id="653c7-113">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="653c7-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="653c7-114">Clear</span><span class="sxs-lookup"><span data-stu-id="653c7-114">Clear</span></span> | <span data-ttu-id="653c7-115">Löscht den angegebenen Ordner.</span><span class="sxs-lookup"><span data-stu-id="653c7-115">Clears the specified folder.</span></span> |
| <span data-ttu-id="653c7-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="653c7-116">ConfigFile</span></span> | <span data-ttu-id="653c7-117">Die NuGet-Konfigurationsdatei angewendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="653c7-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="653c7-118">Wenn nicht angegeben, `%AppData%\NuGet\NuGet.Config` (Windows) oder `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="653c7-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="653c7-119">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="653c7-119">ForceEnglishOutput</span></span> | <span data-ttu-id="653c7-120">*(3.5 +)*  Erzwingt nuget.exe über eine invariante Kultur Englisch-basierte ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="653c7-120">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="653c7-121">Hilfe</span><span class="sxs-lookup"><span data-stu-id="653c7-121">Help</span></span> | <span data-ttu-id="653c7-122">Zeigt die Hilfe Informationen für den Befehl.</span><span class="sxs-lookup"><span data-stu-id="653c7-122">Displays help information for the command.</span></span> |
| <span data-ttu-id="653c7-123">Liste</span><span class="sxs-lookup"><span data-stu-id="653c7-123">List</span></span> | <span data-ttu-id="653c7-124">Listet den Speicherort des angegebenen Ordners oder der Speicherorte von allen Ordnern bei Verwendung mit *alle*.</span><span class="sxs-lookup"><span data-stu-id="653c7-124">Lists the location of the specified folder, or the locations of all folders when used with *all*.</span></span> |
| <span data-ttu-id="653c7-125">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="653c7-125">NonInteractive</span></span> | <span data-ttu-id="653c7-126">Unterdrückt aufforderungen für Benutzereingaben oder Bestätigungen an.</span><span class="sxs-lookup"><span data-stu-id="653c7-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="653c7-127">Ausführlichkeit</span><span class="sxs-lookup"><span data-stu-id="653c7-127">Verbosity</span></span> | <span data-ttu-id="653c7-128">Gibt die Anzahl der Details in der Ausgabe angezeigt: *normalen*, *stillen*, *ausführliche*.</span><span class="sxs-lookup"><span data-stu-id="653c7-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="653c7-129">Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="653c7-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="653c7-130">Beispiele</span><span class="sxs-lookup"><span data-stu-id="653c7-130">Examples</span></span>

```cli
nuget locals all -list
nuget locals http-cache -clear
```

<span data-ttu-id="653c7-131">Weitere Beispiele finden Sie unter [Verwaltung der globalen Pakete und der Cacheordner](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="653c7-131">For additional examples, see [Managing the global packages and cache folders](../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>
