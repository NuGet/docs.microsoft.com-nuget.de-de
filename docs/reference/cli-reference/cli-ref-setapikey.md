---
title: Befehl "nuget CLI-Befehl" | tapikey
description: Referenz für den Befehl "nuget. exe" "".
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: e06cfb5b355dfae8104090db7babdecdf9e9fec1
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231226"
---
# <a name="setapikey-command-nuget-cli"></a><span data-ttu-id="3ceb5-103">Befehl "stapikey" (nuget-CLI)</span><span class="sxs-lookup"><span data-stu-id="3ceb5-103">setapikey command (NuGet CLI)</span></span>

<span data-ttu-id="3ceb5-104">**Gilt für:** Paket Verbrauch, Veröffentlichung &bullet; **unterstützten Versionen:** alle</span><span class="sxs-lookup"><span data-stu-id="3ceb5-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="3ceb5-105">Speichert einen API-Schlüssel für eine angegebene Server-URL in `NuGet.Config`, sodass er nicht für nachfolgende Befehle eingegeben werden muss.</span><span class="sxs-lookup"><span data-stu-id="3ceb5-105">Saves an API key for a given server URL into `NuGet.Config` so that it doesn't need to be entered for subsequent commands.</span></span>

## <a name="usage"></a><span data-ttu-id="3ceb5-106">Verwendung</span><span class="sxs-lookup"><span data-stu-id="3ceb5-106">Usage</span></span>

```cli
nuget setapikey <key> -Source <url> [options]
```

<span data-ttu-id="3ceb5-107">Wenn `<source>` den Server identifiziert und `<key>` der Schlüssel ist, der gespeichert werden soll.</span><span class="sxs-lookup"><span data-stu-id="3ceb5-107">where `<source>` identifies the server and `<key>` is the key to save.</span></span> <span data-ttu-id="3ceb5-108">Wenn `<source>` weggelassen wird, wird nuget.org angenommen.</span><span class="sxs-lookup"><span data-stu-id="3ceb5-108">If `<source>` is omitted, nuget.org is assumed.</span></span> 

> [!NOTE]
> <span data-ttu-id="3ceb5-109">Der API-Schlüssel wird nicht für die Authentifizierung mit dem privaten Feed verwendet.</span><span class="sxs-lookup"><span data-stu-id="3ceb5-109">API key is not used for authenticating with the private feed.</span></span> <span data-ttu-id="3ceb5-110">Informationen zum Verwalten von Anmelde Informationen für die Authentifizierung bei der Quelle finden Sie unter [`nuget sources`-Befehl](../cli-reference/cli-ref-sources.md) .</span><span class="sxs-lookup"><span data-stu-id="3ceb5-110">Refer to [`nuget sources` command](../cli-reference/cli-ref-sources.md) to manage credentials for authenticating with the source.</span></span>
> <span data-ttu-id="3ceb5-111">API-Schlüssel können von den einzelnen nuget-Servern abgerufen werden.</span><span class="sxs-lookup"><span data-stu-id="3ceb5-111">API keys can be obtained from the individual NuGet servers.</span></span> <span data-ttu-id="3ceb5-112">Informationen zum Erstellen und Verwalten von apikeys für nuget.org finden Sie unter [Publish-API-Key](../../quickstart/includes/publish-api-key.md) .</span><span class="sxs-lookup"><span data-stu-id="3ceb5-112">To create and manage APIKeys for nuget.org refer to [publish-api-key](../../quickstart/includes/publish-api-key.md)</span></span>

## <a name="options"></a><span data-ttu-id="3ceb5-113">Tastatur</span><span class="sxs-lookup"><span data-stu-id="3ceb5-113">Options</span></span>

| <span data-ttu-id="3ceb5-114">Option</span><span class="sxs-lookup"><span data-stu-id="3ceb5-114">Option</span></span> | <span data-ttu-id="3ceb5-115">BESCHREIBUNG</span><span class="sxs-lookup"><span data-stu-id="3ceb5-115">Description</span></span> |
| --- | --- |
| <span data-ttu-id="3ceb5-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="3ceb5-116">ConfigFile</span></span> | <span data-ttu-id="3ceb5-117">Die anzuwendende nuget-Konfigurationsdatei.</span><span class="sxs-lookup"><span data-stu-id="3ceb5-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="3ceb5-118">Wenn nicht angegeben, wird `%AppData%\NuGet\NuGet.Config` (Windows) oder `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) verwendet.</span><span class="sxs-lookup"><span data-stu-id="3ceb5-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="3ceb5-119">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="3ceb5-119">ForceEnglishOutput</span></span> | <span data-ttu-id="3ceb5-120">*(3.5* und höher) Erzwingt, dass "nuget. exe" mit einer invarianten, englischen Kultur ausgeführt wird.</span><span class="sxs-lookup"><span data-stu-id="3ceb5-120">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="3ceb5-121">Hilfe</span><span class="sxs-lookup"><span data-stu-id="3ceb5-121">Help</span></span> | <span data-ttu-id="3ceb5-122">Zeigt Hilfe Informationen für den Befehl an.</span><span class="sxs-lookup"><span data-stu-id="3ceb5-122">Displays help information for the command.</span></span> |
| <span data-ttu-id="3ceb5-123">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="3ceb5-123">NonInteractive</span></span> | <span data-ttu-id="3ceb5-124">Unterdrückt Eingabe Aufforderungen für Benutzereingaben oder Bestätigungen.</span><span class="sxs-lookup"><span data-stu-id="3ceb5-124">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="3ceb5-125">Ausführlichkeit</span><span class="sxs-lookup"><span data-stu-id="3ceb5-125">Verbosity</span></span> | <span data-ttu-id="3ceb5-126">Gibt den Umfang der in der Ausgabe angezeigten Details an: *Normal*, *quiet*, *ausführlich*.</span><span class="sxs-lookup"><span data-stu-id="3ceb5-126">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="3ceb5-127">Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="3ceb5-127">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="3ceb5-128">Beispiele</span><span class="sxs-lookup"><span data-stu-id="3ceb5-128">Examples</span></span>

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
