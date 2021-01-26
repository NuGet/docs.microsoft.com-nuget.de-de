---
title: Befehl "nuget CLI-Befehl" | tapikey
description: Referenz für den Befehl "nuget.exe".
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 3e0c2f84e336e0a642b1b5e815e74a1fb0878467
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780023"
---
# <a name="setapikey-command-nuget-cli"></a><span data-ttu-id="5ff2f-103">Befehl "stapikey" (nuget-CLI)</span><span class="sxs-lookup"><span data-stu-id="5ff2f-103">setapikey command (NuGet CLI)</span></span>

<span data-ttu-id="5ff2f-104">**Gilt für:** Paket Verbrauch, &bullet; **unterstützte Versionen** werden veröffentlicht: alle</span><span class="sxs-lookup"><span data-stu-id="5ff2f-104">**Applies to:** package consumption, publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="5ff2f-105">Speichert einen API-Schlüssel für eine angegebene Server-URL in `NuGet.Config` , sodass er nicht für nachfolgende Befehle eingegeben werden muss.</span><span class="sxs-lookup"><span data-stu-id="5ff2f-105">Saves an API key for a given server URL into `NuGet.Config` so that it doesn't need to be entered for subsequent commands.</span></span>

## <a name="usage"></a><span data-ttu-id="5ff2f-106">Verwendung</span><span class="sxs-lookup"><span data-stu-id="5ff2f-106">Usage</span></span>

```cli
nuget setapikey <key> -Source <url> [options]
```

<span data-ttu-id="5ff2f-107">dabei `<source>` identifiziert den Server und `<key>` den Schlüssel, der gespeichert werden soll.</span><span class="sxs-lookup"><span data-stu-id="5ff2f-107">where `<source>` identifies the server and `<key>` is the key to save.</span></span> <span data-ttu-id="5ff2f-108">Wenn `<source>` weggelassen wird, wird nuget.org angenommen.</span><span class="sxs-lookup"><span data-stu-id="5ff2f-108">If `<source>` is omitted, nuget.org is assumed.</span></span> 

> [!NOTE]
> <span data-ttu-id="5ff2f-109">Der API-Schlüssel wird nicht für die Authentifizierung bei dem privaten Feed verwendet.</span><span class="sxs-lookup"><span data-stu-id="5ff2f-109">API key is not used for authenticating with the private feed.</span></span> <span data-ttu-id="5ff2f-110">Informationen zum Verwalten von Anmeldeinformationen für die Authentifizierung bei der Quelle finden Sie unter dem [`nuget sources`-Befehl](../cli-reference/cli-ref-sources.md).</span><span class="sxs-lookup"><span data-stu-id="5ff2f-110">Refer to [`nuget sources` command](../cli-reference/cli-ref-sources.md) to manage credentials for authenticating with the source.</span></span>
> <span data-ttu-id="5ff2f-111">API-Schlüssel können von den einzelnen NuGet-Servern abgerufen werden.</span><span class="sxs-lookup"><span data-stu-id="5ff2f-111">API keys can be obtained from the individual NuGet servers.</span></span> <span data-ttu-id="5ff2f-112">Informationen zum Erstellen und Verwalten von apikeys für nuget.org finden Sie unter "Abruf [-an-API-Schlüssel](../../nuget-org/scoped-api-keys.md#acquire-an-api-key) ".</span><span class="sxs-lookup"><span data-stu-id="5ff2f-112">To create and manage APIKeys for nuget.org refer to [acquire-an-api-key](../../nuget-org/scoped-api-keys.md#acquire-an-api-key)</span></span>

## <a name="options"></a><span data-ttu-id="5ff2f-113">Optionen</span><span class="sxs-lookup"><span data-stu-id="5ff2f-113">Options</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="5ff2f-114">Die anzuwendende nuget-Konfigurationsdatei.</span><span class="sxs-lookup"><span data-stu-id="5ff2f-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="5ff2f-115">Wenn nichts angegeben ist, `%AppData%\NuGet\NuGet.Config` wird (Windows) `~/.nuget/NuGet/NuGet.Config` oder `~/.config/NuGet/NuGet.Config` (Mac/Linux) verwendet.</span><span class="sxs-lookup"><span data-stu-id="5ff2f-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="5ff2f-116">*(3.5* und höher) Erzwingt das Ausführen von nuget.exe mit einer invarianten, englischen Kultur.</span><span class="sxs-lookup"><span data-stu-id="5ff2f-116">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="5ff2f-117">Zeigt Hilfe Informationen für den Befehl an.</span><span class="sxs-lookup"><span data-stu-id="5ff2f-117">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="5ff2f-118">Unterdrückt Eingabe Aufforderungen für Benutzereingaben oder Bestätigungen.</span><span class="sxs-lookup"><span data-stu-id="5ff2f-118">Suppresses prompts for user input or confirmations.</span></span>

- **`-src|-Source`**

  <span data-ttu-id="5ff2f-119">Server-URL, bei der der API-Schlüssel gültig ist.</span><span class="sxs-lookup"><span data-stu-id="5ff2f-119">Server URL where the API key is valid.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="5ff2f-120">Gibt den Umfang der in der Ausgabe angezeigten Details an: `normal` (Standard), `quiet` oder `detailed` .</span><span class="sxs-lookup"><span data-stu-id="5ff2f-120">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="5ff2f-121">Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="5ff2f-121">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="5ff2f-122">Beispiele</span><span class="sxs-lookup"><span data-stu-id="5ff2f-122">Examples</span></span>

```cli
nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget setapikey 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -source https://example.com/nugetfeed
```
