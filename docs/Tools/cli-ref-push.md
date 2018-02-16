---
title: NuGet-CLI-Push-Befehl | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Referenz für den nuget.exe Push-Befehl"
keywords: Befehl "Push"-NuGet-Push Verweis
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: df8ef42f650a20b92a281fff3e597ac8d484544e
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/14/2018
---
# <a name="push-command-nuget-cli"></a><span data-ttu-id="db0fc-104">Push-Befehl (NuGet CLI)</span><span class="sxs-lookup"><span data-stu-id="db0fc-104">push command (NuGet CLI)</span></span>

<span data-ttu-id="db0fc-105">**Gilt für:** Verpacken Sie die Publishing &bullet; **unterstützte Versionen:** alle; erforderlich für nuget.org 4.1.0+</span><span class="sxs-lookup"><span data-stu-id="db0fc-105">**Applies to:** package publishing &bullet; **Supported versions:** all; 4.1.0+ required for nuget.org</span></span>

> [!Important]
> <span data-ttu-id="db0fc-106">Pakete zum nuget.org betätigen verwenden Sie nuget.exe v4.1.0 und höher, die die erforderlichen implementiert [NuGet-Protokolle](../api/nuget-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="db0fc-106">To push packages to nuget.org you must use nuget.exe v4.1.0+, which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

<span data-ttu-id="db0fc-107">Es wird ein Paket an eine Paketquelle und veröffentlicht sie.</span><span class="sxs-lookup"><span data-stu-id="db0fc-107">Pushes a package to a package source and publishes it.</span></span>

<span data-ttu-id="db0fc-108">NuGet Standardkonfiguration erhalten, indem Sie das Laden `%AppData%\NuGet\NuGet.Config`, und klicken Sie dann alle laden `Nuget.Config` oder `.nuget\Nuget.Config` Dateien ausgehend vom Stamm des Laufwerks und endet im aktuellen Verzeichnis (finden Sie unter [Konfigurieren von NuGet-Verhalten](../consume-packages/configuring-nuget-behavior.md))</span><span class="sxs-lookup"><span data-stu-id="db0fc-108">NuGet's default configuration is obtained by loading `%AppData%\NuGet\NuGet.Config`, then loading any `Nuget.Config` or `.nuget\Nuget.Config` files starting from root of drive and ending in current directory (see [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md))</span></span>

## <a name="usage"></a><span data-ttu-id="db0fc-109">Verwendung</span><span class="sxs-lookup"><span data-stu-id="db0fc-109">Usage</span></span>

```cli
nuget push <packagePath> [options]
```

<span data-ttu-id="db0fc-110">wobei `<packagePath>` identifiziert das Paket mithilfe von Push an den Server übertragen.</span><span class="sxs-lookup"><span data-stu-id="db0fc-110">where `<packagePath>` identifies the package to push to the server.</span></span>

## <a name="options"></a><span data-ttu-id="db0fc-111">Optionen</span><span class="sxs-lookup"><span data-stu-id="db0fc-111">Options</span></span>

| <span data-ttu-id="db0fc-112">Option</span><span class="sxs-lookup"><span data-stu-id="db0fc-112">Option</span></span> | <span data-ttu-id="db0fc-113">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="db0fc-113">Description</span></span> |
| --- | --- |
| <span data-ttu-id="db0fc-114">ApiKey</span><span class="sxs-lookup"><span data-stu-id="db0fc-114">ApiKey</span></span> | <span data-ttu-id="db0fc-115">Die API-Schlüssel für das Zielrepository.</span><span class="sxs-lookup"><span data-stu-id="db0fc-115">The API key for the target repository.</span></span> <span data-ttu-id="db0fc-116">Wenn Sie nicht vorhanden ist, der im angegebenen *%AppData%\NuGet\NuGet.Config* verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="db0fc-116">If not present,  the one specified in *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="db0fc-117">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="db0fc-117">ConfigFile</span></span> | <span data-ttu-id="db0fc-118">Die NuGet-Konfigurationsdatei angewendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="db0fc-118">The NuGet configuration file to apply.</span></span> <span data-ttu-id="db0fc-119">Wenn nicht angegeben, *%AppData%\NuGet\NuGet.Config* verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="db0fc-119">If not specified, *%AppData%\NuGet\NuGet.Config* is used.</span></span> |
| <span data-ttu-id="db0fc-120">DisableBuffering</span><span class="sxs-lookup"><span data-stu-id="db0fc-120">DisableBuffering</span></span> | <span data-ttu-id="db0fc-121">Deaktiviert die Pufferung, wenn an einem HTTP-/HTTPS-Server per Push übertragen, um Arbeitsspeicher Verwendungen zu verringern.</span><span class="sxs-lookup"><span data-stu-id="db0fc-121">Disables buffering when pushing to an HTTP(s) server to decrease memory usages.</span></span> <span data-ttu-id="db0fc-122">Vorsicht: Wenn diese Option verwendet wird, integrierte Windows-Authentifizierung funktionieren möglicherweise nicht.</span><span class="sxs-lookup"><span data-stu-id="db0fc-122">Caution: when this option is used, integrated Windows authentication might not work.</span></span> |
| <span data-ttu-id="db0fc-123">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="db0fc-123">ForceEnglishOutput</span></span> | <span data-ttu-id="db0fc-124">*(3.5 +)*  Erzwingt nuget.exe über eine invariante Kultur Englisch-basierte ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="db0fc-124">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="db0fc-125">Hilfe</span><span class="sxs-lookup"><span data-stu-id="db0fc-125">Help</span></span> | <span data-ttu-id="db0fc-126">Zeigt die Hilfe Informationen für den Befehl.</span><span class="sxs-lookup"><span data-stu-id="db0fc-126">Displays help information for the command.</span></span> |
| <span data-ttu-id="db0fc-127">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="db0fc-127">NonInteractive</span></span> | <span data-ttu-id="db0fc-128">Unterdrückt aufforderungen für Benutzereingaben oder Bestätigungen an.</span><span class="sxs-lookup"><span data-stu-id="db0fc-128">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="db0fc-129">NoSymbols</span><span class="sxs-lookup"><span data-stu-id="db0fc-129">NoSymbols</span></span> | <span data-ttu-id="db0fc-130">*(3.5 +)*  Ist ein Symbolpaket vorhanden, er wird nicht abgelegt werden an einen anderen Symbolserver.</span><span class="sxs-lookup"><span data-stu-id="db0fc-130">*(3.5+)* If a symbols package exists, it will not be pushed to a symbol server.</span></span> |
| <span data-ttu-id="db0fc-131">Quelle</span><span class="sxs-lookup"><span data-stu-id="db0fc-131">Source</span></span> | <span data-ttu-id="db0fc-132">Gibt die Server-URL an.</span><span class="sxs-lookup"><span data-stu-id="db0fc-132">Specifies the server URL.</span></span> <span data-ttu-id="db0fc-133">NuGet gibt einen UNC- oder lokalen Ordner Quelle und einfach die Datei statt Programmstapel abzulegen HTTP mit kopiert.</span><span class="sxs-lookup"><span data-stu-id="db0fc-133">NuGet identifies a UNC or local folder source and simply copies the file there instead of pushing it using HTTP.</span></span>  <span data-ttu-id="db0fc-134">Darüber hinaus starting mit NuGet 3.4.2 ist dies ein erforderlicher Parameter, wenn der `NuGet.Config` Datei gibt eine *DefaultPushSource* Wert (finden Sie unter [NuGet Konfigurieren von Verhalten](../consume-packages/configuring-nuget-behavior.md)).</span><span class="sxs-lookup"><span data-stu-id="db0fc-134">Also, starting with NuGet 3.4.2, this is a mandatory parameter unless the `NuGet.Config` file specifies a *DefaultPushSource* value (see [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md)).</span></span> |
| <span data-ttu-id="db0fc-135">SymbolSource</span><span class="sxs-lookup"><span data-stu-id="db0fc-135">SymbolSource</span></span> | <span data-ttu-id="db0fc-136">*(3.5 +)*  Gibt die Symbol-URL, bei dem nuget.smbsrc.net wird verwendet, wenn an nuget.org per Push übertragen</span><span class="sxs-lookup"><span data-stu-id="db0fc-136">*(3.5+)* Specifies the symbol server URL; nuget.smbsrc.net is used when pushing to nuget.org</span></span> |
| <span data-ttu-id="db0fc-137">SymbolApiKey</span><span class="sxs-lookup"><span data-stu-id="db0fc-137">SymbolApiKey</span></span> | <span data-ttu-id="db0fc-138">*(3.5 +)*  Gibt den API-Schlüssel an, für die URL im angegebenen `-SymbolSource`.</span><span class="sxs-lookup"><span data-stu-id="db0fc-138">*(3.5+)* Specifies the API key for the URL specified in `-SymbolSource`.</span></span> |
| <span data-ttu-id="db0fc-139">Timeout</span><span class="sxs-lookup"><span data-stu-id="db0fc-139">Timeout</span></span> | <span data-ttu-id="db0fc-140">Gibt das Timeout in Sekunden für die auf einem Server übertragen.</span><span class="sxs-lookup"><span data-stu-id="db0fc-140">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="db0fc-141">Der Standardwert ist 300 Sekunden (5 Minuten).</span><span class="sxs-lookup"><span data-stu-id="db0fc-141">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="db0fc-142">Ausführlichkeit</span><span class="sxs-lookup"><span data-stu-id="db0fc-142">Verbosity</span></span> | <span data-ttu-id="db0fc-143">Gibt die Anzahl der Details in der Ausgabe angezeigt: *normalen*, *stillen*, *ausführliche*.</span><span class="sxs-lookup"><span data-stu-id="db0fc-143">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="db0fc-144">Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="db0fc-144">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="db0fc-145">Beispiele</span><span class="sxs-lookup"><span data-stu-id="db0fc-145">Examples</span></span>

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
