---
title: NuGet-CLI-Befehl "Hilfe"
description: Referenz für die nuget.exe-Help-Befehl
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3c8b07cb02144da3d88e06956d079b216b3f530f
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546562"
---
# <a name="help-or--command-nuget-cli"></a><span data-ttu-id="55041-103">help or ?</span><span class="sxs-lookup"><span data-stu-id="55041-103">help or ?</span></span> <span data-ttu-id="55041-104">Der Befehl (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="55041-104">command (NuGet CLI)</span></span>

<span data-ttu-id="55041-105">**Gilt für:** alle &bullet; **unterstützten Versionen**: alle</span><span class="sxs-lookup"><span data-stu-id="55041-105">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="55041-106">Zeigt allgemeine Hilfeinformationen und Informationen zu bestimmten Befehlen helfen.</span><span class="sxs-lookup"><span data-stu-id="55041-106">Displays general help information and help information about specific commands.</span></span>

## <a name="usage"></a><span data-ttu-id="55041-107">Verwendung</span><span class="sxs-lookup"><span data-stu-id="55041-107">Usage</span></span>

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

<span data-ttu-id="55041-108">[Befehl] identifiziert, in einem bestimmten Befehl für die zum Anzeigen der Hilfe.</span><span class="sxs-lookup"><span data-stu-id="55041-108">where [command] identifies a specific command for which to display help.</span></span>

> [!Warning]
> <span data-ttu-id="55041-109">Einige Befehle, achten Sie an *Hilfe* zuerst mit `nuget help install`, da ein Paket mit dem Namen "help", auf nuget.org vorhanden ist. Wenn Sie den Befehl geben `nuget install help`, Sie erhalten Sie keine Hilfe zum Befehl "Install", jedoch wird stattdessen das Help-Paket installieren.</span><span class="sxs-lookup"><span data-stu-id="55041-109">With some commands, be mindful to specify *help* first, as with `nuget help install`, because there is a package named "help" on nuget.org. If you give the command `nuget install help`, you won't get help on the install command but will instead install the package named help.</span></span>

## <a name="options"></a><span data-ttu-id="55041-110">Optionen</span><span class="sxs-lookup"><span data-stu-id="55041-110">Options</span></span>

| <span data-ttu-id="55041-111">Option</span><span class="sxs-lookup"><span data-stu-id="55041-111">Option</span></span> | <span data-ttu-id="55041-112">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="55041-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="55041-113">Alle</span><span class="sxs-lookup"><span data-stu-id="55041-113">All</span></span> | <span data-ttu-id="55041-114">Detaillierte Hilfe für alle verfügbaren Befehle gedruckt wird. ignoriert, wenn Sie ein bestimmten Befehl erhält.</span><span class="sxs-lookup"><span data-stu-id="55041-114">Print detailed help for all available commands; ignored if a specific command is given.</span></span> |
| <span data-ttu-id="55041-115">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="55041-115">ConfigFile</span></span> | <span data-ttu-id="55041-116">Die NuGet-Konfigurationsdatei angewendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="55041-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="55041-117">Wenn nicht angegeben, `%AppData%\NuGet\NuGet.Config` (Windows) oder `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="55041-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="55041-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="55041-118">ForceEnglishOutput</span></span> | <span data-ttu-id="55041-119">*(3.5 und höher)*  Erzwingt nuget.exe über eine invariante Kultur auf Englisch basierenden ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="55041-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="55041-120">Hilfe</span><span class="sxs-lookup"><span data-stu-id="55041-120">Help</span></span> | <span data-ttu-id="55041-121">Zeigt die Hilfe zu den Hilfebefehl selbst.</span><span class="sxs-lookup"><span data-stu-id="55041-121">Displays help information for the help command itself.</span></span> |
| <span data-ttu-id="55041-122">Markdown</span><span class="sxs-lookup"><span data-stu-id="55041-122">Markdown</span></span> | <span data-ttu-id="55041-123">Drucken Sie detaillierte Hilfe im Markdown-Format bei Verwendung mit `-All`.</span><span class="sxs-lookup"><span data-stu-id="55041-123">Print detailed help in markdown format when used with `-All`.</span></span> <span data-ttu-id="55041-124">Andernfalls ignoriert.</span><span class="sxs-lookup"><span data-stu-id="55041-124">Ignored otherwise.</span></span> |
| <span data-ttu-id="55041-125">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="55041-125">NonInteractive</span></span> | <span data-ttu-id="55041-126">Unterdrückt aufforderungen für Benutzereingaben oder Bestätigungen an.</span><span class="sxs-lookup"><span data-stu-id="55041-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="55041-127">Ausführlichkeit</span><span class="sxs-lookup"><span data-stu-id="55041-127">Verbosity</span></span> | <span data-ttu-id="55041-128">Gibt an, die Anzahl der Details in der Ausgabe angezeigt: *normalen*, *quiet*, *ausführliche*.</span><span class="sxs-lookup"><span data-stu-id="55041-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="55041-129">Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="55041-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="55041-130">Beispiele</span><span class="sxs-lookup"><span data-stu-id="55041-130">Examples</span></span>

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
