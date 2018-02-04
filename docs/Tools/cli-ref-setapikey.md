---
title: NuGet-CLI Setapikey-Befehl | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Referenz für den nuget.exe Setapikey-Befehl"
keywords: NuGet-Verweis Setapikey Setapikey-Befehl
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: ca6caddbf1404bcaa1ca068c9556f7cf0c651947
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/02/2018
---
# <a name="setapikey-command-nuget-cli"></a><span data-ttu-id="0c587-104">Setapikey-Befehl (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="0c587-104">setapikey command (NuGet CLI)</span></span>

<span data-ttu-id="0c587-105">**Gilt für:** Paket Verbrauchs, Veröffentlichung &bullet; **unterstützte Versionen:** alle</span><span class="sxs-lookup"><span data-stu-id="0c587-105">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="0c587-106">Speichert einen API-Schlüssel für einen bestimmten Server-URL in `NuGet.Config` , damit sie nicht benötigt, für nachfolgende Befehle eingegeben werden.</span><span class="sxs-lookup"><span data-stu-id="0c587-106">Saves an API key for a given server URL into `NuGet.Config` so that it doesn't need to be entered for subsequent commands.</span></span>

## <a name="usage"></a><span data-ttu-id="0c587-107">Verwendung</span><span class="sxs-lookup"><span data-stu-id="0c587-107">Usage</span></span>

```cli
nuget setapikey <key> -Source <url> [options]
```

<span data-ttu-id="0c587-108">wobei `<source>` identifiziert den Server und `<key>` ist der Schlüssel oder das Kennwort zu speichern.</span><span class="sxs-lookup"><span data-stu-id="0c587-108">where `<source>` identifies the server and `<key>` is the key or password to save.</span></span> <span data-ttu-id="0c587-109">Wenn `<source>` wird weggelassen, nuget.org wird angenommen.</span><span class="sxs-lookup"><span data-stu-id="0c587-109">If `<source>` is omitted, nuget.org is assumed.</span></span>

## <a name="options"></a><span data-ttu-id="0c587-110">Optionen</span><span class="sxs-lookup"><span data-stu-id="0c587-110">Options</span></span>

| <span data-ttu-id="0c587-111">Option</span><span class="sxs-lookup"><span data-stu-id="0c587-111">Option</span></span> | <span data-ttu-id="0c587-112">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="0c587-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="0c587-113">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="0c587-113">ConfigFile</span></span> | <span data-ttu-id="0c587-114">Die NuGet-Konfigurationsdatei zu ändern.</span><span class="sxs-lookup"><span data-stu-id="0c587-114">The NuGet configuration file to modify.</span></span> <span data-ttu-id="0c587-115">Wenn nicht angegeben, *%AppData%\NuGet\NuGet.Config* verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="0c587-115">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="0c587-116">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="0c587-116">ForceEnglishOutput</span></span> | <span data-ttu-id="0c587-117">*(3.5 +)*  Erzwingt nuget.exe über eine invariante Kultur Englisch-basierte ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="0c587-117">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="0c587-118">Hilfe</span><span class="sxs-lookup"><span data-stu-id="0c587-118">Help</span></span> | <span data-ttu-id="0c587-119">Zeigt die Hilfe Informationen für den Befehl.</span><span class="sxs-lookup"><span data-stu-id="0c587-119">Displays help information for the command.</span></span> |
| <span data-ttu-id="0c587-120">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="0c587-120">NonInteractive</span></span> | <span data-ttu-id="0c587-121">Unterdrückt aufforderungen für Benutzereingaben oder Bestätigungen an.</span><span class="sxs-lookup"><span data-stu-id="0c587-121">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="0c587-122">Ausführlichkeit</span><span class="sxs-lookup"><span data-stu-id="0c587-122">Verbosity</span></span> | <span data-ttu-id="0c587-123">Gibt die Anzahl der Details in der Ausgabe angezeigt: *normalen*, *stillen*, *ausführliche*.</span><span class="sxs-lookup"><span data-stu-id="0c587-123">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="0c587-124">Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="0c587-124">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="0c587-125">Beispiele</span><span class="sxs-lookup"><span data-stu-id="0c587-125">Examples</span></span>

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
