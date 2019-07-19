---
title: Befehl "nuget CLI-Befehl" | tapikey
description: Referenz für den Befehl "nuget. exe" "".
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: b00e8b1f7a6fda9c1a0c079069fa8ee08a45b419
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327607"
---
# <a name="setapikey-command-nuget-cli"></a><span data-ttu-id="2dfef-103">Befehl "stapikey" (nuget-CLI)</span><span class="sxs-lookup"><span data-stu-id="2dfef-103">setapikey command (NuGet CLI)</span></span>

<span data-ttu-id="2dfef-104">**Gilt für:** Paket Verbrauch, &bullet; **unterstützte Versionen** werden veröffentlicht: alle</span><span class="sxs-lookup"><span data-stu-id="2dfef-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="2dfef-105">Speichert einen API-Schlüssel für eine angegebene Server- `NuGet.Config` URL in, sodass er nicht für nachfolgende Befehle eingegeben werden muss.</span><span class="sxs-lookup"><span data-stu-id="2dfef-105">Saves an API key for a given server URL into `NuGet.Config` so that it doesn't need to be entered for subsequent commands.</span></span>

## <a name="usage"></a><span data-ttu-id="2dfef-106">Verwendung</span><span class="sxs-lookup"><span data-stu-id="2dfef-106">Usage</span></span>

```cli
nuget setapikey <key> -Source <url> [options]
```

<span data-ttu-id="2dfef-107">Dabei identifiziert den Server und `<key>` den Schlüssel oder das Kennwort, das gespeichert werden soll. `<source>`</span><span class="sxs-lookup"><span data-stu-id="2dfef-107">where `<source>` identifies the server and `<key>` is the key or password to save.</span></span> <span data-ttu-id="2dfef-108">Wenn `<source>` weggelassen wird, wird nuget.org angenommen.</span><span class="sxs-lookup"><span data-stu-id="2dfef-108">If `<source>` is omitted, nuget.org is assumed.</span></span>

## <a name="options"></a><span data-ttu-id="2dfef-109">Optionen</span><span class="sxs-lookup"><span data-stu-id="2dfef-109">Options</span></span>

| <span data-ttu-id="2dfef-110">Option</span><span class="sxs-lookup"><span data-stu-id="2dfef-110">Option</span></span> | <span data-ttu-id="2dfef-111">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="2dfef-111">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2dfef-112">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="2dfef-112">ConfigFile</span></span> | <span data-ttu-id="2dfef-113">Die anzuwendende nuget-Konfigurationsdatei.</span><span class="sxs-lookup"><span data-stu-id="2dfef-113">The NuGet configuration file to apply.</span></span> <span data-ttu-id="2dfef-114">Wenn nichts angegeben ist `%AppData%\NuGet\NuGet.Config` , wird (Windows `~/.nuget/NuGet/NuGet.Config` ) oder (Mac/Linux) verwendet.</span><span class="sxs-lookup"><span data-stu-id="2dfef-114">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="2dfef-115">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="2dfef-115">ForceEnglishOutput</span></span> | <span data-ttu-id="2dfef-116">*(3.5* und höher) Erzwingt, dass "nuget. exe" mit einer invarianten, englischen Kultur ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="2dfef-116">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="2dfef-117">Help</span><span class="sxs-lookup"><span data-stu-id="2dfef-117">Help</span></span> | <span data-ttu-id="2dfef-118">Zeigt Hilfe Informationen für den Befehl an.</span><span class="sxs-lookup"><span data-stu-id="2dfef-118">Displays help information for the command.</span></span> |
| <span data-ttu-id="2dfef-119">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="2dfef-119">NonInteractive</span></span> | <span data-ttu-id="2dfef-120">Unterdrückt Eingabe Aufforderungen für Benutzereingaben oder Bestätigungen.</span><span class="sxs-lookup"><span data-stu-id="2dfef-120">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="2dfef-121">Verbosity</span><span class="sxs-lookup"><span data-stu-id="2dfef-121">Verbosity</span></span> | <span data-ttu-id="2dfef-122">Gibt den Umfang der in der Ausgabe angezeigten Details an: *Normal*, *quiet*, *ausführlich*.</span><span class="sxs-lookup"><span data-stu-id="2dfef-122">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="2dfef-123">Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="2dfef-123">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="2dfef-124">Beispiele</span><span class="sxs-lookup"><span data-stu-id="2dfef-124">Examples</span></span>

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
