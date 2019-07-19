---
title: Befehl "nuget-CLI"
description: Verweis auf den Hilfe Befehl "nuget. exe"
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3c8b07cb02144da3d88e06956d079b216b3f530f
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327797"
---
# <a name="help-or--command-nuget-cli"></a><span data-ttu-id="d00cc-103">help or ?</span><span class="sxs-lookup"><span data-stu-id="d00cc-103">help or ?</span></span> <span data-ttu-id="d00cc-104">Der Befehl (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="d00cc-104">command (NuGet CLI)</span></span>

<span data-ttu-id="d00cc-105">**Gilt für:** alle &bullet; **unterstützten Versionen**: alle</span><span class="sxs-lookup"><span data-stu-id="d00cc-105">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="d00cc-106">Zeigt allgemeine Hilfe Informationen und Hilfe Informationen zu bestimmten Befehlen an.</span><span class="sxs-lookup"><span data-stu-id="d00cc-106">Displays general help information and help information about specific commands.</span></span>

## <a name="usage"></a><span data-ttu-id="d00cc-107">Verwendung</span><span class="sxs-lookup"><span data-stu-id="d00cc-107">Usage</span></span>

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

<span data-ttu-id="d00cc-108">WHERE [Command] identifiziert einen bestimmten Befehl, für den Hilfe angezeigt werden soll.</span><span class="sxs-lookup"><span data-stu-id="d00cc-108">where [command] identifies a specific command for which to display help.</span></span>

> [!Warning]
> <span data-ttu-id="d00cc-109">Beachten Sie bei einigen Befehlen, dass Sie zuerst die *Hilfe* angeben, `nuget help install`wie bei, da ein Paket mit dem Namen "Help" auf nuget.org vorhanden ist. Wenn Sie den Befehl `nuget install help`verwenden, erhalten Sie keine Hilfe zum Installations Befehl, sondern installieren das Paket mit dem Namen "Help".</span><span class="sxs-lookup"><span data-stu-id="d00cc-109">With some commands, be mindful to specify *help* first, as with `nuget help install`, because there is a package named "help" on nuget.org. If you give the command `nuget install help`, you won't get help on the install command but will instead install the package named help.</span></span>

## <a name="options"></a><span data-ttu-id="d00cc-110">Optionen</span><span class="sxs-lookup"><span data-stu-id="d00cc-110">Options</span></span>

| <span data-ttu-id="d00cc-111">Option</span><span class="sxs-lookup"><span data-stu-id="d00cc-111">Option</span></span> | <span data-ttu-id="d00cc-112">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="d00cc-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="d00cc-113">All</span><span class="sxs-lookup"><span data-stu-id="d00cc-113">All</span></span> | <span data-ttu-id="d00cc-114">Ausführliche Hilfe für alle verfügbaren Befehle drucken wird ignoriert, wenn ein bestimmter Befehl angegeben wird.</span><span class="sxs-lookup"><span data-stu-id="d00cc-114">Print detailed help for all available commands; ignored if a specific command is given.</span></span> |
| <span data-ttu-id="d00cc-115">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="d00cc-115">ConfigFile</span></span> | <span data-ttu-id="d00cc-116">Die anzuwendende nuget-Konfigurationsdatei.</span><span class="sxs-lookup"><span data-stu-id="d00cc-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="d00cc-117">Wenn nichts angegeben ist `%AppData%\NuGet\NuGet.Config` , wird (Windows `~/.nuget/NuGet/NuGet.Config` ) oder (Mac/Linux) verwendet.</span><span class="sxs-lookup"><span data-stu-id="d00cc-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="d00cc-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="d00cc-118">ForceEnglishOutput</span></span> | <span data-ttu-id="d00cc-119">*(3.5* und höher) Erzwingt, dass "nuget. exe" mit einer invarianten, englischen Kultur ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="d00cc-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="d00cc-120">Help</span><span class="sxs-lookup"><span data-stu-id="d00cc-120">Help</span></span> | <span data-ttu-id="d00cc-121">Zeigt Hilfe Informationen für den Befehl "Hilfe" an.</span><span class="sxs-lookup"><span data-stu-id="d00cc-121">Displays help information for the help command itself.</span></span> |
| <span data-ttu-id="d00cc-122">Markdown</span><span class="sxs-lookup"><span data-stu-id="d00cc-122">Markdown</span></span> | <span data-ttu-id="d00cc-123">Drucken Sie ausführliche Hilfe im Markdown-Format, `-All`Wenn Sie mit verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="d00cc-123">Print detailed help in markdown format when used with `-All`.</span></span> <span data-ttu-id="d00cc-124">Andernfalls ignoriert.</span><span class="sxs-lookup"><span data-stu-id="d00cc-124">Ignored otherwise.</span></span> |
| <span data-ttu-id="d00cc-125">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="d00cc-125">NonInteractive</span></span> | <span data-ttu-id="d00cc-126">Unterdrückt Eingabe Aufforderungen für Benutzereingaben oder Bestätigungen.</span><span class="sxs-lookup"><span data-stu-id="d00cc-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="d00cc-127">Verbosity</span><span class="sxs-lookup"><span data-stu-id="d00cc-127">Verbosity</span></span> | <span data-ttu-id="d00cc-128">Gibt den Umfang der in der Ausgabe angezeigten Details an: *Normal*, *quiet*, *ausführlich*.</span><span class="sxs-lookup"><span data-stu-id="d00cc-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="d00cc-129">Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="d00cc-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="d00cc-130">Beispiele</span><span class="sxs-lookup"><span data-stu-id="d00cc-130">Examples</span></span>

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
