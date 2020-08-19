---
title: Befehl "nuget-CLI"
description: Verweis auf den nuget.exe Help-Befehl
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 12776b7c16aeef223a0b682ee2468edec8ea3295
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623109"
---
# <a name="help-or--command-nuget-cli"></a><span data-ttu-id="c3d3f-103">help or ?</span><span class="sxs-lookup"><span data-stu-id="c3d3f-103">help or ?</span></span> <span data-ttu-id="c3d3f-104">Befehl (nuget-CLI)</span><span class="sxs-lookup"><span data-stu-id="c3d3f-104">command (NuGet CLI)</span></span>

<span data-ttu-id="c3d3f-105">**Gilt für:** alle &bullet; **unterstützten Versionen**: alle</span><span class="sxs-lookup"><span data-stu-id="c3d3f-105">**Applies to:** all &bullet; **Supported versions**: all</span></span>

<span data-ttu-id="c3d3f-106">Zeigt allgemeine Hilfe Informationen und Hilfe Informationen zu bestimmten Befehlen an.</span><span class="sxs-lookup"><span data-stu-id="c3d3f-106">Displays general help information and help information about specific commands.</span></span>

## <a name="usage"></a><span data-ttu-id="c3d3f-107">Verwendung</span><span class="sxs-lookup"><span data-stu-id="c3d3f-107">Usage</span></span>

```cli
nuget help [command] [options]
nuget ? [command] [options]
```

<span data-ttu-id="c3d3f-108">WHERE [Command] identifiziert einen bestimmten Befehl, für den Hilfe angezeigt werden soll.</span><span class="sxs-lookup"><span data-stu-id="c3d3f-108">where [command] identifies a specific command for which to display help.</span></span>

> [!Warning]
> <span data-ttu-id="c3d3f-109">Beachten Sie bei einigen Befehlen, dass Sie zuerst die *Hilfe* angeben, wie bei `nuget help install` , da ein Paket mit dem Namen "Help" auf nuget.org vorhanden ist. Wenn Sie den Befehl verwenden `nuget install help` , erhalten Sie keine Hilfe zum Installations Befehl, sondern installieren das Paket mit dem Namen "Help".</span><span class="sxs-lookup"><span data-stu-id="c3d3f-109">With some commands, be mindful to specify *help* first, as with `nuget help install`, because there is a package named "help" on nuget.org. If you give the command `nuget install help`, you won't get help on the install command but will instead install the package named help.</span></span>

## <a name="options"></a><span data-ttu-id="c3d3f-110">Optionen</span><span class="sxs-lookup"><span data-stu-id="c3d3f-110">Options</span></span>

- **`-All`**

  <span data-ttu-id="c3d3f-111">Ausführliche Hilfe für alle verfügbaren Befehle drucken wird ignoriert, wenn ein bestimmter Befehl angegeben wird.</span><span class="sxs-lookup"><span data-stu-id="c3d3f-111">Print detailed help for all available commands; ignored if a specific command is given.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="c3d3f-112">Die anzuwendende nuget-Konfigurationsdatei.</span><span class="sxs-lookup"><span data-stu-id="c3d3f-112">The NuGet configuration file to apply.</span></span> <span data-ttu-id="c3d3f-113">Wenn nichts angegeben ist, `%AppData%\NuGet\NuGet.Config` wird (Windows) `~/.nuget/NuGet/NuGet.Config` oder `~/.config/NuGet/NuGet.Config` (Mac/Linux) verwendet.</span><span class="sxs-lookup"><span data-stu-id="c3d3f-113">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="c3d3f-114">*(3.5* und höher) Erzwingt das Ausführen von nuget.exe mit einer invarianten, englischen Kultur.</span><span class="sxs-lookup"><span data-stu-id="c3d3f-114">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="c3d3f-115">Zeigt Hilfe Informationen für den Befehl an.</span><span class="sxs-lookup"><span data-stu-id="c3d3f-115">Displays help information for the command.</span></span>

- **`-Markdown`**

  <span data-ttu-id="c3d3f-116">Drucken Sie ausführliche Hilfe im Markdown-Format, wenn Sie mit verwendet werden `-All` .</span><span class="sxs-lookup"><span data-stu-id="c3d3f-116">Print detailed help in markdown format when used with `-All`.</span></span> <span data-ttu-id="c3d3f-117">Andernfalls ignoriert.</span><span class="sxs-lookup"><span data-stu-id="c3d3f-117">Ignored otherwise.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="c3d3f-118">Unterdrückt Eingabe Aufforderungen für Benutzereingaben oder Bestätigungen.</span><span class="sxs-lookup"><span data-stu-id="c3d3f-118">Suppresses prompts for user input or confirmations.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="c3d3f-119">Gibt den Umfang der in der Ausgabe angezeigten Details an: `normal` (Standard), `quiet` oder `detailed` .</span><span class="sxs-lookup"><span data-stu-id="c3d3f-119">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="c3d3f-120">Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="c3d3f-120">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="c3d3f-121">Beispiele</span><span class="sxs-lookup"><span data-stu-id="c3d3f-121">Examples</span></span>

```cli
nuget help
nuget help push
nuget ?
nuget push -?
nuget help -All -Markdown
```
