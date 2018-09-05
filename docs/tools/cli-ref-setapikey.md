---
title: NuGet-CLI-Befehl "Setapikey"
description: Referenz für die nuget.exe-Befehl "Setapikey"
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: b00e8b1f7a6fda9c1a0c079069fa8ee08a45b419
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549219"
---
# <a name="setapikey-command-nuget-cli"></a><span data-ttu-id="26004-103">Befehl "Setapikey" (NuGet-CLI)</span><span class="sxs-lookup"><span data-stu-id="26004-103">setapikey command (NuGet CLI)</span></span>

<span data-ttu-id="26004-104">**Gilt für:** -paketverbrauch, Veröffentlichung &bullet; **unterstützte Versionen:** alle</span><span class="sxs-lookup"><span data-stu-id="26004-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="26004-105">Speichert einen API-Schlüssel für einen bestimmten Server-URL in `NuGet.Config` so, dass er nicht für nachfolgende Befehle eingegeben werden.</span><span class="sxs-lookup"><span data-stu-id="26004-105">Saves an API key for a given server URL into `NuGet.Config` so that it doesn't need to be entered for subsequent commands.</span></span>

## <a name="usage"></a><span data-ttu-id="26004-106">Verwendung</span><span class="sxs-lookup"><span data-stu-id="26004-106">Usage</span></span>

```cli
nuget setapikey <key> -Source <url> [options]
```

<span data-ttu-id="26004-107">wo `<source>` identifiziert den Server und `<key>` ist der Schlüssel oder das Kennwort zu speichern.</span><span class="sxs-lookup"><span data-stu-id="26004-107">where `<source>` identifies the server and `<key>` is the key or password to save.</span></span> <span data-ttu-id="26004-108">Wenn `<source>` wird ausgelassen, wird "NuGet.org" begonnen.</span><span class="sxs-lookup"><span data-stu-id="26004-108">If `<source>` is omitted, nuget.org is assumed.</span></span>

## <a name="options"></a><span data-ttu-id="26004-109">Optionen</span><span class="sxs-lookup"><span data-stu-id="26004-109">Options</span></span>

| <span data-ttu-id="26004-110">Option</span><span class="sxs-lookup"><span data-stu-id="26004-110">Option</span></span> | <span data-ttu-id="26004-111">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="26004-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="26004-112">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="26004-112">ConfigFile</span></span> | <span data-ttu-id="26004-113">Die NuGet-Konfigurationsdatei angewendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="26004-113">The NuGet configuration file to apply.</span></span> <span data-ttu-id="26004-114">Wenn nicht angegeben, `%AppData%\NuGet\NuGet.Config` (Windows) oder `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="26004-114">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="26004-115">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="26004-115">ForceEnglishOutput</span></span> | <span data-ttu-id="26004-116">*(3.5 und höher)*  Erzwingt nuget.exe über eine invariante Kultur auf Englisch basierenden ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="26004-116">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="26004-117">Hilfe</span><span class="sxs-lookup"><span data-stu-id="26004-117">Help</span></span> | <span data-ttu-id="26004-118">Zeigt die Informationen für den Befehl Hilfe.</span><span class="sxs-lookup"><span data-stu-id="26004-118">Displays help information for the command.</span></span> |
| <span data-ttu-id="26004-119">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="26004-119">NonInteractive</span></span> | <span data-ttu-id="26004-120">Unterdrückt aufforderungen für Benutzereingaben oder Bestätigungen an.</span><span class="sxs-lookup"><span data-stu-id="26004-120">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="26004-121">Ausführlichkeit</span><span class="sxs-lookup"><span data-stu-id="26004-121">Verbosity</span></span> | <span data-ttu-id="26004-122">Gibt an, die Anzahl der Details in der Ausgabe angezeigt: *normalen*, *quiet*, *ausführliche*.</span><span class="sxs-lookup"><span data-stu-id="26004-122">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="26004-123">Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="26004-123">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="26004-124">Beispiele</span><span class="sxs-lookup"><span data-stu-id="26004-124">Examples</span></span>

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
