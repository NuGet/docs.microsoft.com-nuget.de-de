---
title: NuGet-CLI-Befehl "Hilfe"
description: Referenz für den Befehl "nuget.exe Help"
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: dbfc803e24c824d30e128d6e86cfa3c43660668f
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="help-or--command-nuget-cli"></a><span data-ttu-id="7c690-103">Hilfe oder?</span><span class="sxs-lookup"><span data-stu-id="7c690-103">help or ?</span></span> <span data-ttu-id="7c690-104">Der Befehl (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="7c690-104">command (NuGet CLI)</span></span>

<span data-ttu-id="7c690-105">**Gilt für:** alle &bullet; **unterstützten Versionen**: alle</span><span class="sxs-lookup"><span data-stu-id="7c690-105">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="7c690-106">Zeigt allgemeine Hilfe-Informationen und Hilfe-Informationen zu bestimmten Befehlen.</span><span class="sxs-lookup"><span data-stu-id="7c690-106">Displays general help information and help information about specific commands.</span></span>

## <a name="usage"></a><span data-ttu-id="7c690-107">Verwendung</span><span class="sxs-lookup"><span data-stu-id="7c690-107">Usage</span></span>

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

<span data-ttu-id="7c690-108">[Befehl] identifiziert, in einen bestimmten Befehl für die Hilfe angezeigt werden sollen.</span><span class="sxs-lookup"><span data-stu-id="7c690-108">where [command] identifies a specific command for which to display help.</span></span>

> [!Warning]
> <span data-ttu-id="7c690-109">Einige Befehle werden an laufen *Hilfe* ersten, als mit `nuget help install`, da ein Paket mit dem Namen "help" auf nuget.org vorhanden ist. Wenn Sie den Befehl geben `nuget install help`, erhalten keine Hilfe zum Befehl "Install", aber das Paket mit dem Namen Hilfe wird stattdessen installieren.</span><span class="sxs-lookup"><span data-stu-id="7c690-109">With some commands, be mindful to specify *help* first, as with `nuget help install`, because there is a package named "help" on nuget.org. If you give the command `nuget install help`, you won't get help on the install command but will instead install the package named help.</span></span>

## <a name="options"></a><span data-ttu-id="7c690-110">Optionen</span><span class="sxs-lookup"><span data-stu-id="7c690-110">Options</span></span>

| <span data-ttu-id="7c690-111">Option</span><span class="sxs-lookup"><span data-stu-id="7c690-111">Option</span></span> | <span data-ttu-id="7c690-112">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="7c690-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="7c690-113">Alle</span><span class="sxs-lookup"><span data-stu-id="7c690-113">All</span></span> | <span data-ttu-id="7c690-114">Drucken von ausführlichen Hilfeinformationen für alle verfügbaren Befehle; ignoriert, wenn Sie ein bestimmten Befehl angegeben wird.</span><span class="sxs-lookup"><span data-stu-id="7c690-114">Print detailed help for all available commands; ignored if a specific command is given.</span></span> |
| <span data-ttu-id="7c690-115">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="7c690-115">ConfigFile</span></span> | <span data-ttu-id="7c690-116">Die NuGet-Konfigurationsdatei angewendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="7c690-116">The NuGet configuration file to apply.</span></span> <span data-ttu-id="7c690-117">Wenn nicht angegeben, `%AppData%\NuGet\NuGet.Config` (Windows) oder `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="7c690-117">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="7c690-118">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="7c690-118">ForceEnglishOutput</span></span> | <span data-ttu-id="7c690-119">*(3.5 +)*  Erzwingt nuget.exe über eine invariante Kultur Englisch-basierte ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="7c690-119">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="7c690-120">Hilfe</span><span class="sxs-lookup"><span data-stu-id="7c690-120">Help</span></span> | <span data-ttu-id="7c690-121">Zeigt die Hilfe Informationen für den Befehl "Help" selbst.</span><span class="sxs-lookup"><span data-stu-id="7c690-121">Displays help information for the help command itself.</span></span> |
| <span data-ttu-id="7c690-122">Markdown</span><span class="sxs-lookup"><span data-stu-id="7c690-122">Markdown</span></span> | <span data-ttu-id="7c690-123">Drucken von ausführlichen Hilfeinformationen in Markdown-Format bei Verwendung mit `-All`.</span><span class="sxs-lookup"><span data-stu-id="7c690-123">Print detailed help in markdown format when used with `-All`.</span></span> <span data-ttu-id="7c690-124">Andernfalls ignoriert.</span><span class="sxs-lookup"><span data-stu-id="7c690-124">Ignored otherwise.</span></span> |
| <span data-ttu-id="7c690-125">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="7c690-125">NonInteractive</span></span> | <span data-ttu-id="7c690-126">Unterdrückt aufforderungen für Benutzereingaben oder Bestätigungen an.</span><span class="sxs-lookup"><span data-stu-id="7c690-126">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="7c690-127">Ausführlichkeit</span><span class="sxs-lookup"><span data-stu-id="7c690-127">Verbosity</span></span> | <span data-ttu-id="7c690-128">Gibt die Anzahl der Details in der Ausgabe angezeigt: *normalen*, *stillen*, *ausführliche*.</span><span class="sxs-lookup"><span data-stu-id="7c690-128">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="7c690-129">Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="7c690-129">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="7c690-130">Beispiele</span><span class="sxs-lookup"><span data-stu-id="7c690-130">Examples</span></span>

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
