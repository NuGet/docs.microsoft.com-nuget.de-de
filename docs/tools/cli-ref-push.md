---
title: NuGet-CLI-Push-Befehl
description: Referenz für den nuget.exe Push-Befehl
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 05cafa981ecf42829d1b3d8b8988ed51449d9d86
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817190"
---
# <a name="push-command-nuget-cli"></a><span data-ttu-id="1956c-103">Push-Befehl (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="1956c-103">push command (NuGet CLI)</span></span>

<span data-ttu-id="1956c-104">**Gilt für:** Verpacken Sie die Publishing &bullet; **unterstützte Versionen:** alle; erforderlich für nuget.org 4.1.0+</span><span class="sxs-lookup"><span data-stu-id="1956c-104">**Applies to:** package publishing &bullet; **Supported versions:** all; 4.1.0+ required for nuget.org</span></span>

> [!Important]
> <span data-ttu-id="1956c-105">Pakete zum nuget.org betätigen verwenden Sie nuget.exe v4.1.0 und höher, die die erforderlichen implementiert [NuGet-Protokolle](../api/nuget-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="1956c-105">To push packages to nuget.org you must use nuget.exe v4.1.0+, which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

<span data-ttu-id="1956c-106">Es wird ein Paket an eine Paketquelle und veröffentlicht sie.</span><span class="sxs-lookup"><span data-stu-id="1956c-106">Pushes a package to a package source and publishes it.</span></span>

<span data-ttu-id="1956c-107">NuGet Standardkonfiguration erhalten, indem Sie das Laden `%AppData%\NuGet\NuGet.Config` (Windows) oder `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), laden Sie dann alle `Nuget.Config` oder `.nuget\Nuget.Config` Dateien ausgehend vom Stamm des Laufwerks und endet im aktuellen Verzeichnis (finden Sie unter [konfigurieren NuGet-Verhalten](../consume-packages/configuring-nuget-behavior.md))</span><span class="sxs-lookup"><span data-stu-id="1956c-107">NuGet's default configuration is obtained by loading `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), then loading any `Nuget.Config` or `.nuget\Nuget.Config` files starting from root of drive and ending in current directory (see [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md))</span></span>

## <a name="usage"></a><span data-ttu-id="1956c-108">Verwendung</span><span class="sxs-lookup"><span data-stu-id="1956c-108">Usage</span></span>

```cli
nuget push <packagePath> [options]
```

<span data-ttu-id="1956c-109">wobei `<packagePath>` identifiziert das Paket mithilfe von Push an den Server übertragen.</span><span class="sxs-lookup"><span data-stu-id="1956c-109">where `<packagePath>` identifies the package to push to the server.</span></span>

## <a name="options"></a><span data-ttu-id="1956c-110">Optionen</span><span class="sxs-lookup"><span data-stu-id="1956c-110">Options</span></span>

| <span data-ttu-id="1956c-111">Option</span><span class="sxs-lookup"><span data-stu-id="1956c-111">Option</span></span> | <span data-ttu-id="1956c-112">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="1956c-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1956c-113">"apikey"</span><span class="sxs-lookup"><span data-stu-id="1956c-113">ApiKey</span></span> | <span data-ttu-id="1956c-114">Die API-Schlüssel für das Zielrepository.</span><span class="sxs-lookup"><span data-stu-id="1956c-114">The API key for the target repository.</span></span> <span data-ttu-id="1956c-115">Wenn Sie nicht vorhanden ist, wird in der Datei "App.config" angegebenen verwendet.</span><span class="sxs-lookup"><span data-stu-id="1956c-115">If not present,  the one specified in the config file is used.</span></span> |
| <span data-ttu-id="1956c-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="1956c-116">ConfigFile</span></span> | <span data-ttu-id="1956c-117">Die NuGet-Konfigurationsdatei angewendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="1956c-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="1956c-118">Wenn nicht angegeben, `%AppData%\NuGet\NuGet.Config` (Windows) oder `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="1956c-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="1956c-119">DisableBuffering</span><span class="sxs-lookup"><span data-stu-id="1956c-119">DisableBuffering</span></span> | <span data-ttu-id="1956c-120">Deaktiviert die Pufferung, wenn an einem HTTP-/HTTPS-Server per Push übertragen, um Arbeitsspeicher Verwendungen zu verringern.</span><span class="sxs-lookup"><span data-stu-id="1956c-120">Disables buffering when pushing to an HTTP(s) server to decrease memory usages.</span></span> <span data-ttu-id="1956c-121">Vorsicht: Wenn diese Option verwendet wird, integrierte Windows-Authentifizierung funktionieren möglicherweise nicht.</span><span class="sxs-lookup"><span data-stu-id="1956c-121">Caution: when this option is used, integrated Windows authentication might not work.</span></span> |
| <span data-ttu-id="1956c-122">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="1956c-122">ForceEnglishOutput</span></span> | <span data-ttu-id="1956c-123">*(3.5 +)*  Erzwingt nuget.exe über eine invariante Kultur Englisch-basierte ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="1956c-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="1956c-124">Hilfe</span><span class="sxs-lookup"><span data-stu-id="1956c-124">Help</span></span> | <span data-ttu-id="1956c-125">Zeigt die Hilfe Informationen für den Befehl.</span><span class="sxs-lookup"><span data-stu-id="1956c-125">Displays help information for the command.</span></span> |
| <span data-ttu-id="1956c-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="1956c-126">NonInteractive</span></span> | <span data-ttu-id="1956c-127">Unterdrückt aufforderungen für Benutzereingaben oder Bestätigungen an.</span><span class="sxs-lookup"><span data-stu-id="1956c-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="1956c-128">NoSymbols</span><span class="sxs-lookup"><span data-stu-id="1956c-128">NoSymbols</span></span> | <span data-ttu-id="1956c-129">*(3.5 +)*  Ist ein Symbolpaket vorhanden, er wird nicht abgelegt werden an einen anderen Symbolserver.</span><span class="sxs-lookup"><span data-stu-id="1956c-129">*(3.5+)* If a symbols package exists, it will not be pushed to a symbol server.</span></span> |
| <span data-ttu-id="1956c-130">Quelle</span><span class="sxs-lookup"><span data-stu-id="1956c-130">Source</span></span> | <span data-ttu-id="1956c-131">Gibt die Server-URL an.</span><span class="sxs-lookup"><span data-stu-id="1956c-131">Specifies the server URL.</span></span> <span data-ttu-id="1956c-132">NuGet gibt einen UNC- oder lokalen Ordner Quelle und einfach die Datei statt Programmstapel abzulegen HTTP mit kopiert.</span><span class="sxs-lookup"><span data-stu-id="1956c-132">NuGet identifies a UNC or local folder source and simply copies the file there instead of pushing it using HTTP.</span></span>  <span data-ttu-id="1956c-133">Darüber hinaus starting mit NuGet 3.4.2 ist dies ein erforderlicher Parameter, wenn der `NuGet.Config` Datei gibt eine *DefaultPushSource* Wert (finden Sie unter [NuGet Konfigurieren von Verhalten](../consume-packages/configuring-nuget-behavior.md)).</span><span class="sxs-lookup"><span data-stu-id="1956c-133">Also, starting with NuGet 3.4.2, this is a mandatory parameter unless the `NuGet.Config` file specifies a *DefaultPushSource* value (see [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md)).</span></span> |
| <span data-ttu-id="1956c-134">SymbolSource</span><span class="sxs-lookup"><span data-stu-id="1956c-134">SymbolSource</span></span> | <span data-ttu-id="1956c-135">*(3.5 +)*  Gibt die Symbol-URL, bei dem nuget.smbsrc.net wird verwendet, wenn an nuget.org per Push übertragen</span><span class="sxs-lookup"><span data-stu-id="1956c-135">*(3.5+)* Specifies the symbol server URL; nuget.smbsrc.net is used when pushing to nuget.org</span></span> |
| <span data-ttu-id="1956c-136">SymbolApiKey</span><span class="sxs-lookup"><span data-stu-id="1956c-136">SymbolApiKey</span></span> | <span data-ttu-id="1956c-137">*(3.5 +)*  Gibt den API-Schlüssel an, für die URL im angegebenen `-SymbolSource`.</span><span class="sxs-lookup"><span data-stu-id="1956c-137">*(3.5+)* Specifies the API key for the URL specified in `-SymbolSource`.</span></span> |
| <span data-ttu-id="1956c-138">Timeout</span><span class="sxs-lookup"><span data-stu-id="1956c-138">Timeout</span></span> | <span data-ttu-id="1956c-139">Gibt das Timeout in Sekunden für die auf einem Server übertragen.</span><span class="sxs-lookup"><span data-stu-id="1956c-139">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="1956c-140">Der Standardwert ist 300 Sekunden (5 Minuten).</span><span class="sxs-lookup"><span data-stu-id="1956c-140">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="1956c-141">Ausführlichkeit</span><span class="sxs-lookup"><span data-stu-id="1956c-141">Verbosity</span></span> | <span data-ttu-id="1956c-142">Gibt die Anzahl der Details in der Ausgabe angezeigt: *normalen*, *stillen*, *ausführliche*.</span><span class="sxs-lookup"><span data-stu-id="1956c-142">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="1956c-143">Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="1956c-143">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="1956c-144">Beispiele</span><span class="sxs-lookup"><span data-stu-id="1956c-144">Examples</span></span>

```cli
nuget push foo.nupkg

nuget push foo.symbols.nupkg

nuget push foo.nupkg -Timeout 360

nuget push *.nupkg

nuget.exe push -source \\mycompany\repo\ mypackage.1.0.0.nupkg

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -Source https://api.nuget.org/v3/index.json

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -s https://customsource/
```
