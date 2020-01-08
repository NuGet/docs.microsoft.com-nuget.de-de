---
title: Befehl "nuget CLI-Befehl" | tapikey
description: Referenz für den Befehl "nuget. exe" "".
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 0e2119953e6d07cd3571f156fa0b2665de49f963
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/25/2019
ms.locfileid: "75383968"
---
# <a name="setapikey-command-nuget-cli"></a><span data-ttu-id="ec70e-103">Befehl "stapikey" (nuget-CLI)</span><span class="sxs-lookup"><span data-stu-id="ec70e-103">setapikey command (NuGet CLI)</span></span>

<span data-ttu-id="ec70e-104">**Gilt für:** Paket Verbrauch, Veröffentlichung &bullet; **unterstützten Versionen:** alle</span><span class="sxs-lookup"><span data-stu-id="ec70e-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="ec70e-105">Speichert einen API-Schlüssel für eine angegebene Server-URL in `NuGet.Config`, sodass er nicht für nachfolgende Befehle eingegeben werden muss.</span><span class="sxs-lookup"><span data-stu-id="ec70e-105">Saves an API key for a given server URL into `NuGet.Config` so that it doesn't need to be entered for subsequent commands.</span></span>

## <a name="usage"></a><span data-ttu-id="ec70e-106">Verwendungs-</span><span class="sxs-lookup"><span data-stu-id="ec70e-106">Usage</span></span>

```cli
nuget setapikey <key> -Source <url> [options]
```

<span data-ttu-id="ec70e-107">Dabei identifiziert `<source>` den Server, und `<key>` ist der Schlüssel oder das Kennwort, das gespeichert werden soll.</span><span class="sxs-lookup"><span data-stu-id="ec70e-107">where `<source>` identifies the server and `<key>` is the key or password to save.</span></span> <span data-ttu-id="ec70e-108">Wenn `<source>` weggelassen wird, wird nuget.org angenommen.</span><span class="sxs-lookup"><span data-stu-id="ec70e-108">If `<source>` is omitted, nuget.org is assumed.</span></span>

> [!NOTE]
> <span data-ttu-id="ec70e-109">Der API-Schlüssel wird nicht für die Authentifizierung mit dem privaten Feed verwendet.</span><span class="sxs-lookup"><span data-stu-id="ec70e-109">API key is not used for authenticating with the private feed.</span></span> <span data-ttu-id="ec70e-110">Informationen zum Verwalten von Anmelde Informationen für die Authentifizierung bei der Quelle finden Sie unter [`nuget sources`-Befehl](../cli-reference/cli-ref-sources.md) .</span><span class="sxs-lookup"><span data-stu-id="ec70e-110">Refer to [`nuget sources` command](../cli-reference/cli-ref-sources.md) to manage credentials for authenticating with the source.</span></span>

## <a name="options"></a><span data-ttu-id="ec70e-111">Options</span><span class="sxs-lookup"><span data-stu-id="ec70e-111">Options</span></span>

| <span data-ttu-id="ec70e-112">-Option</span><span class="sxs-lookup"><span data-stu-id="ec70e-112">Option</span></span> | <span data-ttu-id="ec70e-113">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="ec70e-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ec70e-114">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="ec70e-114">ConfigFile</span></span> | <span data-ttu-id="ec70e-115">Die anzuwendende nuget-Konfigurationsdatei.</span><span class="sxs-lookup"><span data-stu-id="ec70e-115">The NuGet configuration file to apply.</span></span> <span data-ttu-id="ec70e-116">Wenn nicht angegeben, wird `%AppData%\NuGet\NuGet.Config` (Windows) oder `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) verwendet.</span><span class="sxs-lookup"><span data-stu-id="ec70e-116">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="ec70e-117">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="ec70e-117">ForceEnglishOutput</span></span> | <span data-ttu-id="ec70e-118">*(3.5* und höher) Erzwingt, dass "nuget. exe" mit einer invarianten, englischen Kultur ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="ec70e-118">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="ec70e-119">Hilfe</span><span class="sxs-lookup"><span data-stu-id="ec70e-119">Help</span></span> | <span data-ttu-id="ec70e-120">Zeigt Hilfe Informationen für den Befehl an.</span><span class="sxs-lookup"><span data-stu-id="ec70e-120">Displays help information for the command.</span></span> |
| <span data-ttu-id="ec70e-121">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="ec70e-121">NonInteractive</span></span> | <span data-ttu-id="ec70e-122">Unterdrückt Eingabe Aufforderungen für Benutzereingaben oder Bestätigungen.</span><span class="sxs-lookup"><span data-stu-id="ec70e-122">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="ec70e-123">Ausführlichkeit</span><span class="sxs-lookup"><span data-stu-id="ec70e-123">Verbosity</span></span> | <span data-ttu-id="ec70e-124">Gibt den Umfang der in der Ausgabe angezeigten Details an: *Normal*, *quiet*, *ausführlich*.</span><span class="sxs-lookup"><span data-stu-id="ec70e-124">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="ec70e-125">Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="ec70e-125">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="ec70e-126">Beispiele</span><span class="sxs-lookup"><span data-stu-id="ec70e-126">Examples</span></span>

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
