---
title: Befehl "nuget CLI Delete"
description: Verweis auf den nuget.exe DELETE-Befehl
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: bec1a778d4986a4cb7ee87e1ef8a98550c96ed57
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622862"
---
# <a name="delete-command-nuget-cli"></a><span data-ttu-id="def78-103">DELETE-Befehl (nuget-CLI)</span><span class="sxs-lookup"><span data-stu-id="def78-103">delete command (NuGet CLI)</span></span>

<span data-ttu-id="def78-104">**Gilt für:** &bullet; **unterstützte Versionen** der Paket Veröffentlichung: alle</span><span class="sxs-lookup"><span data-stu-id="def78-104">**Applies to:** package publishing &bullet; **Supported versions:** all</span></span>

<span data-ttu-id="def78-105">Löscht ein Paket aus einer Paketquelle oder hebt die Auflistung auf.</span><span class="sxs-lookup"><span data-stu-id="def78-105">Deletes or unlists a package from a package source.</span></span> <span data-ttu-id="def78-106">Bei nuget.org wird das Paket durch den DELETE-Befehl [nicht mehr aufgelistet](../../nuget-org/policies/deleting-packages.md).</span><span class="sxs-lookup"><span data-stu-id="def78-106">For nuget.org, the delete command [unlists the package](../../nuget-org/policies/deleting-packages.md).</span></span>

## <a name="usage"></a><span data-ttu-id="def78-107">Verwendung</span><span class="sxs-lookup"><span data-stu-id="def78-107">Usage</span></span>

```cli
nuget delete <packageID> <packageVersion> [options]
```

<span data-ttu-id="def78-108">dabei `<packageID>` `<packageVersion>` identifizieren Sie das genaue Paket, das gelöscht oder die Auflistung der Auflistung entfernt werden soll.</span><span class="sxs-lookup"><span data-stu-id="def78-108">where `<packageID>` and `<packageVersion>` identify the exact package to delete or unlist.</span></span> <span data-ttu-id="def78-109">Das genaue Verhalten hängt von der Quelle ab.</span><span class="sxs-lookup"><span data-stu-id="def78-109">The exact behavior depends on the source.</span></span> <span data-ttu-id="def78-110">Für lokale Ordner wird das Paket beispielsweise gelöscht. für nuget.org wird das Paket nicht aufgelistet.</span><span class="sxs-lookup"><span data-stu-id="def78-110">For local folders, for instance, the package is deleted; for nuget.org the package is unlisted.</span></span>

## <a name="options"></a><span data-ttu-id="def78-111">Optionen</span><span class="sxs-lookup"><span data-stu-id="def78-111">Options</span></span>

- **`-ApiKey`**

  <span data-ttu-id="def78-112">Der API-Schlüssel für das Zielrepository.</span><span class="sxs-lookup"><span data-stu-id="def78-112">The API key for the target repository.</span></span> <span data-ttu-id="def78-113">Wenn kein Wert vorhanden ist, wird der in der Konfigurationsdatei angegebene verwendet.</span><span class="sxs-lookup"><span data-stu-id="def78-113">If not present, the one specified in the config file is used.</span></span>

- **`-ConfigFile`**

  <span data-ttu-id="def78-114">Die anzuwendende nuget-Konfigurationsdatei.</span><span class="sxs-lookup"><span data-stu-id="def78-114">The NuGet configuration file to apply.</span></span> <span data-ttu-id="def78-115">Wenn nichts angegeben ist, `%AppData%\NuGet\NuGet.Config` wird (Windows) `~/.nuget/NuGet/NuGet.Config` oder `~/.config/NuGet/NuGet.Config` (Mac/Linux) verwendet.</span><span class="sxs-lookup"><span data-stu-id="def78-115">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows), or `~/.nuget/NuGet/NuGet.Config` or `~/.config/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>

- **`-ForceEnglishOutput`**

  <span data-ttu-id="def78-116">*(3.5* und höher) Erzwingt das Ausführen von nuget.exe mit einer invarianten, englischen Kultur.</span><span class="sxs-lookup"><span data-stu-id="def78-116">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span>

- **`-?|-help`**

  <span data-ttu-id="def78-117">Zeigt Hilfe Informationen für den Befehl an.</span><span class="sxs-lookup"><span data-stu-id="def78-117">Displays help information for the command.</span></span>

- **`-NonInteractive`**

  <span data-ttu-id="def78-118">Unterdrückt Eingabe Aufforderungen für Benutzereingaben oder Bestätigungen.</span><span class="sxs-lookup"><span data-stu-id="def78-118">Suppresses prompts for user input or confirmations.</span></span>

 - **`-np|-NoPrompt`**

   <span data-ttu-id="def78-119">Beim Löschen nicht auffordern.</span><span class="sxs-lookup"><span data-stu-id="def78-119">Do not prompt when deleting.</span></span>

 - <span data-ttu-id="def78-120">**`-NoServiceEndpoint`** Fügt "API/v2/Packages" nicht an die Quell-URL an.</span><span class="sxs-lookup"><span data-stu-id="def78-120">**`-NoServiceEndpoint`** Does not append "api/v2/packages" to the source URL.</span></span>

- **`-src|-Source`**

  <span data-ttu-id="def78-121">Gibt die Server-URL an.</span><span class="sxs-lookup"><span data-stu-id="def78-121">Specifies the server URL.</span></span> <span data-ttu-id="def78-122">Die URL für nuget.org ist `https://api.nuget.org/v3/index.json` .</span><span class="sxs-lookup"><span data-stu-id="def78-122">The URL for nuget.org is `https://api.nuget.org/v3/index.json`.</span></span> <span data-ttu-id="def78-123">Ersetzen Sie für private Feeds den Hostnamen, z. b. " *% Hostname%/API/v3*".</span><span class="sxs-lookup"><span data-stu-id="def78-123">For private feeds, substitute the host name, for example, *%hostname%/api/v3*.</span></span>

- **`-Verbosity [normal|quiet|detailed]`**

  <span data-ttu-id="def78-124">Gibt den Umfang der in der Ausgabe angezeigten Details an: `normal` (Standard), `quiet` oder `detailed` .</span><span class="sxs-lookup"><span data-stu-id="def78-124">Specifies the amount of detail displayed in the output: `normal` (the default), `quiet`, or `detailed`.</span></span>

<span data-ttu-id="def78-125">Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="def78-125">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="def78-126">Beispiele</span><span class="sxs-lookup"><span data-stu-id="def78-126">Examples</span></span>

```cli
nuget delete MyPackage 1.0

nuget delete MyPackage 1.0 -Source http://package.contoso.com/source -apikey A1B2C3
```
