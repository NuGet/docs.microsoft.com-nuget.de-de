---
title: Befehl "nuget CLI Locals"
description: Referenz für den lokalen Befehl "nuget. exe"
author: karann-msft
ms.author: karann
ms.date: 03/19/2018
ms.topic: reference
ms.openlocfilehash: b02360c38ad66c95bbe3c7d403ef4a959112c91a
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327807"
---
# <a name="locals-command-nuget-cli"></a><span data-ttu-id="dbf80-103">Der Befehl „locals“ (NuGet-CLI)</span><span class="sxs-lookup"><span data-stu-id="dbf80-103">locals command (NuGet CLI)</span></span>

<span data-ttu-id="dbf80-104">**Gilt für:** &bullet; **unterstützte Versionen** : 3.3+</span><span class="sxs-lookup"><span data-stu-id="dbf80-104">**Applies to:** package consumption &bullet; **Supported versions:** 3.3+</span></span>

<span data-ttu-id="dbf80-105">Löscht lokale nuget-Ressourcen wie den Ordner " *http-Cache*", " *Global-Packages* " und den Ordner "Temp" oder listet diese auf.</span><span class="sxs-lookup"><span data-stu-id="dbf80-105">Clears or lists local NuGet resources such as the *http-cache*, *global-packages* folder, and the temp folder.</span></span> <span data-ttu-id="dbf80-106">Der `locals` Befehl kann auch verwendet werden, um eine Liste dieser Speicherorte anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="dbf80-106">The `locals` command can also be used to display a list of those locations.</span></span> <span data-ttu-id="dbf80-107">Weitere Informationen finden Sie unter [Verwalten der globalen Pakete und Cache Ordner](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="dbf80-107">For more information, see [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>

## <a name="usage"></a><span data-ttu-id="dbf80-108">Verwendung</span><span class="sxs-lookup"><span data-stu-id="dbf80-108">Usage</span></span>

```cli
nuget locals <folder> [options]
```

<span data-ttu-id="dbf80-109">`all` `http-cache` `global-packages` `temp` `plugins-cache`   dabei ist eine von,, `packages-cache` (3,5 und früher),, (3.4 +) und (4.8 +). `<folder>`</span><span class="sxs-lookup"><span data-stu-id="dbf80-109">where `<folder>` is one of `all`, `http-cache`, `packages-cache` *(3.5 and earlier)*, `global-packages`, `temp` *(3.4+)*, and `plugins-cache` *(4.8+)*.</span></span>

## <a name="options"></a><span data-ttu-id="dbf80-110">Optionen</span><span class="sxs-lookup"><span data-stu-id="dbf80-110">Options</span></span>

| <span data-ttu-id="dbf80-111">Option</span><span class="sxs-lookup"><span data-stu-id="dbf80-111">Option</span></span> | <span data-ttu-id="dbf80-112">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="dbf80-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="dbf80-113">Clear</span><span class="sxs-lookup"><span data-stu-id="dbf80-113">Clear</span></span> | <span data-ttu-id="dbf80-114">Löscht den angegebenen Ordner.</span><span class="sxs-lookup"><span data-stu-id="dbf80-114">Clears the specified folder.</span></span> |
| <span data-ttu-id="dbf80-115">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="dbf80-115">ConfigFile</span></span> | <span data-ttu-id="dbf80-116">Die anzuwendende nuget-Konfigurationsdatei.</span><span class="sxs-lookup"><span data-stu-id="dbf80-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="dbf80-117">Wenn nichts angegeben ist `%AppData%\NuGet\NuGet.Config` , wird (Windows `~/.nuget/NuGet/NuGet.Config` ) oder (Mac/Linux) verwendet.</span><span class="sxs-lookup"><span data-stu-id="dbf80-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="dbf80-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="dbf80-118">ForceEnglishOutput</span></span> | <span data-ttu-id="dbf80-119">*(3.5* und höher) Erzwingt, dass "nuget. exe" mit einer invarianten, englischen Kultur ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="dbf80-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="dbf80-120">Help</span><span class="sxs-lookup"><span data-stu-id="dbf80-120">Help</span></span> | <span data-ttu-id="dbf80-121">Zeigt Hilfe Informationen für den Befehl an.</span><span class="sxs-lookup"><span data-stu-id="dbf80-121">Displays help information for the command.</span></span> |
| <span data-ttu-id="dbf80-122">Liste</span><span class="sxs-lookup"><span data-stu-id="dbf80-122">List</span></span> | <span data-ttu-id="dbf80-123">Listet den Speicherort des angegebenen Ordners oder die Speicherorte aller Ordner bei Verwendung mit *allen*auf.</span><span class="sxs-lookup"><span data-stu-id="dbf80-123">Lists the location of the specified folder, or the locations of all folders when used with *all*.</span></span> |
| <span data-ttu-id="dbf80-124">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="dbf80-124">NonInteractive</span></span> | <span data-ttu-id="dbf80-125">Unterdrückt Eingabe Aufforderungen für Benutzereingaben oder Bestätigungen.</span><span class="sxs-lookup"><span data-stu-id="dbf80-125">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="dbf80-126">Verbosity</span><span class="sxs-lookup"><span data-stu-id="dbf80-126">Verbosity</span></span> | <span data-ttu-id="dbf80-127">Gibt den Umfang der in der Ausgabe angezeigten Details an: *Normal*, *quiet*, *ausführlich*.</span><span class="sxs-lookup"><span data-stu-id="dbf80-127">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="dbf80-128">Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="dbf80-128">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="dbf80-129">Beispiele</span><span class="sxs-lookup"><span data-stu-id="dbf80-129">Examples</span></span>

```cli
nuget locals all -list
nuget locals http-cache -clear
```

<span data-ttu-id="dbf80-130">Weitere Beispiele finden Sie unter [Verwalten der globalen Pakete und Cache Ordner](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span><span class="sxs-lookup"><span data-stu-id="dbf80-130">For additional examples, see [Managing the global packages and cache folders](../../consume-packages/managing-the-global-packages-and-cache-folders.md).</span></span>
