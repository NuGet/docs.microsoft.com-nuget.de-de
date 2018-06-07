---
title: NuGet-CLI Setapikey-Befehl
description: Referenz für den nuget.exe Setapikey-Befehl
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 66fc62074b4e7c39ff2ed6b515eee9f821530536
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817683"
---
# <a name="setapikey-command-nuget-cli"></a><span data-ttu-id="45bdd-103">Setapikey-Befehl (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="45bdd-103">setapikey command (NuGet CLI)</span></span>

<span data-ttu-id="45bdd-104">**Gilt für:** Paket Verbrauchs, Veröffentlichung &bullet; **unterstützte Versionen:** alle</span><span class="sxs-lookup"><span data-stu-id="45bdd-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="45bdd-105">Speichert einen API-Schlüssel für einen bestimmten Server-URL in `NuGet.Config` , damit sie nicht benötigt, für nachfolgende Befehle eingegeben werden.</span><span class="sxs-lookup"><span data-stu-id="45bdd-105">Saves an API key for a given server URL into `NuGet.Config` so that it doesn't need to be entered for subsequent commands.</span></span>

## <a name="usage"></a><span data-ttu-id="45bdd-106">Verwendung</span><span class="sxs-lookup"><span data-stu-id="45bdd-106">Usage</span></span>

```cli
nuget setapikey <key> -Source <url> [options]
```

<span data-ttu-id="45bdd-107">wobei `<source>` identifiziert den Server und `<key>` ist der Schlüssel oder das Kennwort zu speichern.</span><span class="sxs-lookup"><span data-stu-id="45bdd-107">where `<source>` identifies the server and `<key>` is the key or password to save.</span></span> <span data-ttu-id="45bdd-108">Wenn `<source>` wird weggelassen, nuget.org wird angenommen.</span><span class="sxs-lookup"><span data-stu-id="45bdd-108">If `<source>` is omitted, nuget.org is assumed.</span></span>

## <a name="options"></a><span data-ttu-id="45bdd-109">Optionen</span><span class="sxs-lookup"><span data-stu-id="45bdd-109">Options</span></span>

| <span data-ttu-id="45bdd-110">Option</span><span class="sxs-lookup"><span data-stu-id="45bdd-110">Option</span></span> | <span data-ttu-id="45bdd-111">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="45bdd-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="45bdd-112">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="45bdd-112">ConfigFile</span></span> | <span data-ttu-id="45bdd-113">Die NuGet-Konfigurationsdatei angewendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="45bdd-113">The NuGet configuration file to apply.</span></span> <span data-ttu-id="45bdd-114">Wenn nicht angegeben, `%AppData%\NuGet\NuGet.Config` (Windows) oder `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="45bdd-114">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="45bdd-115">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="45bdd-115">ForceEnglishOutput</span></span> | <span data-ttu-id="45bdd-116">*(3.5 +)*  Erzwingt nuget.exe über eine invariante Kultur Englisch-basierte ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="45bdd-116">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="45bdd-117">Hilfe</span><span class="sxs-lookup"><span data-stu-id="45bdd-117">Help</span></span> | <span data-ttu-id="45bdd-118">Zeigt die Hilfe Informationen für den Befehl.</span><span class="sxs-lookup"><span data-stu-id="45bdd-118">Displays help information for the command.</span></span> |
| <span data-ttu-id="45bdd-119">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="45bdd-119">NonInteractive</span></span> | <span data-ttu-id="45bdd-120">Unterdrückt aufforderungen für Benutzereingaben oder Bestätigungen an.</span><span class="sxs-lookup"><span data-stu-id="45bdd-120">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="45bdd-121">Ausführlichkeit</span><span class="sxs-lookup"><span data-stu-id="45bdd-121">Verbosity</span></span> | <span data-ttu-id="45bdd-122">Gibt die Anzahl der Details in der Ausgabe angezeigt: *normalen*, *stillen*, *ausführliche*.</span><span class="sxs-lookup"><span data-stu-id="45bdd-122">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="45bdd-123">Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="45bdd-123">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="45bdd-124">Beispiele</span><span class="sxs-lookup"><span data-stu-id="45bdd-124">Examples</span></span>

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
