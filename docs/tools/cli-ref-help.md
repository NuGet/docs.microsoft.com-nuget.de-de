---
title: NuGet-CLI-Befehl "Hilfe"
description: Referenz für den Befehl "nuget.exe Help"
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: d7112209a0a2a267343c3458ebacaf6b744786a9
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818255"
---
# <a name="help-or--command-nuget-cli"></a><span data-ttu-id="b429f-103">help or ?</span><span class="sxs-lookup"><span data-stu-id="b429f-103">help or ?</span></span> <span data-ttu-id="b429f-104">Der Befehl (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="b429f-104">command (NuGet CLI)</span></span>

<span data-ttu-id="b429f-105">**Gilt für:** alle &bullet; **unterstützten Versionen**: alle</span><span class="sxs-lookup"><span data-stu-id="b429f-105">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="b429f-106">Zeigt allgemeine Hilfe-Informationen und Hilfe-Informationen zu bestimmten Befehlen.</span><span class="sxs-lookup"><span data-stu-id="b429f-106">Displays general help information and help information about specific commands.</span></span>

## <a name="usage"></a><span data-ttu-id="b429f-107">Verwendung</span><span class="sxs-lookup"><span data-stu-id="b429f-107">Usage</span></span>

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

<span data-ttu-id="b429f-108">[Befehl] identifiziert, in einen bestimmten Befehl für die Hilfe angezeigt werden sollen.</span><span class="sxs-lookup"><span data-stu-id="b429f-108">where [command] identifies a specific command for which to display help.</span></span>

> [!Warning]
> <span data-ttu-id="b429f-109">Einige Befehle werden an laufen *Hilfe* ersten, als mit `nuget help install`, da ein Paket mit dem Namen "help" auf nuget.org vorhanden ist. Wenn Sie den Befehl geben `nuget install help`, erhalten keine Hilfe zum Befehl "Install", aber das Paket mit dem Namen Hilfe wird stattdessen installieren.</span><span class="sxs-lookup"><span data-stu-id="b429f-109">With some commands, be mindful to specify *help* first, as with `nuget help install`, because there is a package named "help" on nuget.org. If you give the command `nuget install help`, you won't get help on the install command but will instead install the package named help.</span></span>

## <a name="options"></a><span data-ttu-id="b429f-110">Optionen</span><span class="sxs-lookup"><span data-stu-id="b429f-110">Options</span></span>

| <span data-ttu-id="b429f-111">Option</span><span class="sxs-lookup"><span data-stu-id="b429f-111">Option</span></span> | <span data-ttu-id="b429f-112">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="b429f-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="b429f-113">Alle</span><span class="sxs-lookup"><span data-stu-id="b429f-113">All</span></span> | <span data-ttu-id="b429f-114">Drucken von ausführlichen Hilfeinformationen für alle verfügbaren Befehle; ignoriert, wenn Sie ein bestimmten Befehl angegeben wird.</span><span class="sxs-lookup"><span data-stu-id="b429f-114">Print detailed help for all available commands; ignored if a specific command is given.</span></span> |
| <span data-ttu-id="b429f-115">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="b429f-115">ConfigFile</span></span> | <span data-ttu-id="b429f-116">Die NuGet-Konfigurationsdatei angewendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="b429f-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="b429f-117">Wenn nicht angegeben, `%AppData%\NuGet\NuGet.Config` (Windows) oder `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="b429f-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="b429f-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="b429f-118">ForceEnglishOutput</span></span> | <span data-ttu-id="b429f-119">*(3.5 +)*  Erzwingt nuget.exe über eine invariante Kultur Englisch-basierte ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="b429f-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="b429f-120">Hilfe</span><span class="sxs-lookup"><span data-stu-id="b429f-120">Help</span></span> | <span data-ttu-id="b429f-121">Zeigt die Hilfe Informationen für den Befehl "Help" selbst.</span><span class="sxs-lookup"><span data-stu-id="b429f-121">Displays help information for the help command itself.</span></span> |
| <span data-ttu-id="b429f-122">Markdown</span><span class="sxs-lookup"><span data-stu-id="b429f-122">Markdown</span></span> | <span data-ttu-id="b429f-123">Drucken von ausführlichen Hilfeinformationen in Markdown-Format bei Verwendung mit `-All`.</span><span class="sxs-lookup"><span data-stu-id="b429f-123">Print detailed help in markdown format when used with `-All`.</span></span> <span data-ttu-id="b429f-124">Andernfalls ignoriert.</span><span class="sxs-lookup"><span data-stu-id="b429f-124">Ignored otherwise.</span></span> |
| <span data-ttu-id="b429f-125">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="b429f-125">NonInteractive</span></span> | <span data-ttu-id="b429f-126">Unterdrückt aufforderungen für Benutzereingaben oder Bestätigungen an.</span><span class="sxs-lookup"><span data-stu-id="b429f-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="b429f-127">Ausführlichkeit</span><span class="sxs-lookup"><span data-stu-id="b429f-127">Verbosity</span></span> | <span data-ttu-id="b429f-128">Gibt die Anzahl der Details in der Ausgabe angezeigt: *normalen*, *stillen*, *ausführliche*.</span><span class="sxs-lookup"><span data-stu-id="b429f-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="b429f-129">Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="b429f-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="b429f-130">Beispiele</span><span class="sxs-lookup"><span data-stu-id="b429f-130">Examples</span></span>

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
