---
title: NuGet-CLI-Push-Befehl
description: Referenz für die nuget.exe-Push-Befehl
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: bce04864224a66019a52cdfff8355f68dc424204
ms.sourcegitcommit: 69b5eb1494a1745a4b1a7f320a91255d5d8356a9
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/21/2019
ms.locfileid: "65975002"
---
# <a name="push-command-nuget-cli"></a><span data-ttu-id="2a246-103">Push-Befehl (NuGet-CLI)</span><span class="sxs-lookup"><span data-stu-id="2a246-103">push command (NuGet CLI)</span></span>

<span data-ttu-id="2a246-104">**Gilt für:** Paket veröffentlichen &bullet; **unterstützte Versionen:** alle; erforderlich für nuget.org 4.1.0 oder höher</span><span class="sxs-lookup"><span data-stu-id="2a246-104">**Applies to:** package publishing &bullet; **Supported versions:** all; 4.1.0+ required for nuget.org</span></span>

> [!Important]
> <span data-ttu-id="2a246-105">Um Pakete per Push an nuget.org übertragen müssen, verwenden Sie nuget.exe Verze 4.1.0 +, die die erforderlichen implementiert [NuGet-Protokolle](../api/nuget-protocols.md).</span><span class="sxs-lookup"><span data-stu-id="2a246-105">To push packages to nuget.org you must use nuget.exe v4.1.0+, which implements the required [NuGet protocols](../api/nuget-protocols.md).</span></span>

<span data-ttu-id="2a246-106">Überträgt ein Paket auf eine Paketquelle und veröffentlicht es.</span><span class="sxs-lookup"><span data-stu-id="2a246-106">Pushes a package to a package source and publishes it.</span></span>

<span data-ttu-id="2a246-107">NuGet Standardkonfiguration wird abgerufen, indem `%AppData%\NuGet\NuGet.Config` (Windows) oder `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), laden Sie dann alle `Nuget.Config` oder `.nuget\Nuget.Config` Dateien, beginnend mit Stamm des Laufwerks und endend im aktuellen Verzeichnis (finden Sie unter [konfigurieren NuGet-Verhaltens](../consume-packages/configuring-nuget-behavior.md))</span><span class="sxs-lookup"><span data-stu-id="2a246-107">NuGet's default configuration is obtained by loading `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), then loading any `Nuget.Config` or `.nuget\Nuget.Config` files starting from root of drive and ending in current directory (see [Configuring NuGet Behavior](../consume-packages/configuring-nuget-behavior.md))</span></span>

## <a name="usage"></a><span data-ttu-id="2a246-108">Verwendung</span><span class="sxs-lookup"><span data-stu-id="2a246-108">Usage</span></span>

```cli
nuget push <packagePath> [options]
```

<span data-ttu-id="2a246-109">wo `<packagePath>` identifiziert das Paket an den Server mithilfe von Push übertragen.</span><span class="sxs-lookup"><span data-stu-id="2a246-109">where `<packagePath>` identifies the package to push to the server.</span></span>

## <a name="options"></a><span data-ttu-id="2a246-110">Optionen</span><span class="sxs-lookup"><span data-stu-id="2a246-110">Options</span></span>

| <span data-ttu-id="2a246-111">Option</span><span class="sxs-lookup"><span data-stu-id="2a246-111">Option</span></span> | <span data-ttu-id="2a246-112">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="2a246-112">Description</span></span> |
| --- | --- |
| <span data-ttu-id="2a246-113">ApiKey</span><span class="sxs-lookup"><span data-stu-id="2a246-113">ApiKey</span></span> | <span data-ttu-id="2a246-114">Die API-Schlüssel für die Ziel-Repository.</span><span class="sxs-lookup"><span data-stu-id="2a246-114">The API key for the target repository.</span></span> <span data-ttu-id="2a246-115">Wenn nicht vorhanden ist, wird angegeben, in der Konfigurationsdatei verwendet.</span><span class="sxs-lookup"><span data-stu-id="2a246-115">If not present,  the one specified in the config file is used.</span></span> |
| <span data-ttu-id="2a246-116">ConfigFile</span><span class="sxs-lookup"><span data-stu-id="2a246-116">ConfigFile</span></span> | <span data-ttu-id="2a246-117">Die NuGet-Konfigurationsdatei angewendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="2a246-117">The NuGet configuration file to apply.</span></span> <span data-ttu-id="2a246-118">Wenn nicht angegeben, `%AppData%\NuGet\NuGet.Config` (Windows) oder `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="2a246-118">If not specified, `%AppData%\NuGet\NuGet.Config` (Windows) or `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) is used.</span></span>|
| <span data-ttu-id="2a246-119">DisableBuffering</span><span class="sxs-lookup"><span data-stu-id="2a246-119">DisableBuffering</span></span> | <span data-ttu-id="2a246-120">Deaktiviert die Pufferung, wenn auf einem Server HTTP(s) übertragen werden, um Arbeitsspeicher Verwendungen zu verringern.</span><span class="sxs-lookup"><span data-stu-id="2a246-120">Disables buffering when pushing to an HTTP(s) server to decrease memory usages.</span></span> <span data-ttu-id="2a246-121">Vorsicht: Wenn diese Option verwendet wird, integrierte Windows-Authentifizierung funktioniert möglicherweise nicht.</span><span class="sxs-lookup"><span data-stu-id="2a246-121">Caution: when this option is used, integrated Windows authentication might not work.</span></span> |
| <span data-ttu-id="2a246-122">ForceEnglishOutput</span><span class="sxs-lookup"><span data-stu-id="2a246-122">ForceEnglishOutput</span></span> | <span data-ttu-id="2a246-123">*(3.5 und höher)*  Erzwingt nuget.exe über eine invariante Kultur auf Englisch basierenden ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="2a246-123">*(3.5+)* Forces nuget.exe to run using an invariant, English-based culture.</span></span> |
| <span data-ttu-id="2a246-124">Help</span><span class="sxs-lookup"><span data-stu-id="2a246-124">Help</span></span> | <span data-ttu-id="2a246-125">Zeigt die Informationen für den Befehl Hilfe.</span><span class="sxs-lookup"><span data-stu-id="2a246-125">Displays help information for the command.</span></span> |
| <span data-ttu-id="2a246-126">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="2a246-126">NonInteractive</span></span> | <span data-ttu-id="2a246-127">Unterdrückt aufforderungen für Benutzereingaben oder Bestätigungen an.</span><span class="sxs-lookup"><span data-stu-id="2a246-127">Suppresses prompts for user input or confirmations.</span></span> |
| <span data-ttu-id="2a246-128">NoSymbols</span><span class="sxs-lookup"><span data-stu-id="2a246-128">NoSymbols</span></span> | <span data-ttu-id="2a246-129">*(3.5 und höher)*  Ist ein Symbolpaket vorhanden, es wird nicht abgelegt werden auf einem Symbolserver.</span><span class="sxs-lookup"><span data-stu-id="2a246-129">*(3.5+)* If a symbols package exists, it will not be pushed to a symbol server.</span></span> |
| <span data-ttu-id="2a246-130">Source</span><span class="sxs-lookup"><span data-stu-id="2a246-130">Source</span></span> | <span data-ttu-id="2a246-131">Gibt die Server-URL an.</span><span class="sxs-lookup"><span data-stu-id="2a246-131">Specifies the server URL.</span></span> <span data-ttu-id="2a246-132">NuGet identifiziert eine UNC- oder lokaler Ordner Quelle und einfach kopiert die Datei dort mithilfe von Push übertragen sie die Verwendung von HTTP.</span><span class="sxs-lookup"><span data-stu-id="2a246-132">NuGet identifies a UNC or local folder source and simply copies the file there instead of pushing it using HTTP.</span></span>  <span data-ttu-id="2a246-133">Ab NuGet 3.4.2, dies ist auch ein obligatorischer Parameter, wenn die `NuGet.Config` -Datei gibt eine *DefaultPushSource* Wert (finden Sie unter [Konfigurieren des NuGet-Verhaltens](../consume-packages/configuring-nuget-behavior.md)).</span><span class="sxs-lookup"><span data-stu-id="2a246-133">Also, starting with NuGet 3.4.2, this is a mandatory parameter unless the `NuGet.Config` file specifies a *DefaultPushSource* value (see [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md)).</span></span> |
| <span data-ttu-id="2a246-134">SkipDuplicate</span><span class="sxs-lookup"><span data-stu-id="2a246-134">SkipDuplicate</span></span> | <span data-ttu-id="2a246-135">Wenn ein Paket und die Version bereits vorhanden ist, diesen Schritt überspringen und weiterhin mit dem nächsten Paket in den Push, sofern vorhanden.</span><span class="sxs-lookup"><span data-stu-id="2a246-135">If a package and version already exists, skip it and continue with the next package in the push, if any.</span></span> |
| <span data-ttu-id="2a246-136">SymbolSource</span><span class="sxs-lookup"><span data-stu-id="2a246-136">SymbolSource</span></span> | <span data-ttu-id="2a246-137">*(3.5 und höher)*  Gibt an, die Symbolserver-URL; nuget.smbsrc.net wird verwendet, wenn Sie mithilfe von Push an nuget.org übertragen</span><span class="sxs-lookup"><span data-stu-id="2a246-137">*(3.5+)* Specifies the symbol server URL; nuget.smbsrc.net is used when pushing to nuget.org</span></span> |
| <span data-ttu-id="2a246-138">SymbolApiKey</span><span class="sxs-lookup"><span data-stu-id="2a246-138">SymbolApiKey</span></span> | <span data-ttu-id="2a246-139">*(3.5 und höher)*  Gibt den API-Schlüssel an, für die URL in angegeben `-SymbolSource`.</span><span class="sxs-lookup"><span data-stu-id="2a246-139">*(3.5+)* Specifies the API key for the URL specified in `-SymbolSource`.</span></span> |
| <span data-ttu-id="2a246-140">Timeout</span><span class="sxs-lookup"><span data-stu-id="2a246-140">Timeout</span></span> | <span data-ttu-id="2a246-141">Gibt das Timeout in Sekunden für die Übertragung auf einen Server an.</span><span class="sxs-lookup"><span data-stu-id="2a246-141">Specifies the timeout, in seconds, for pushing to a server.</span></span> <span data-ttu-id="2a246-142">Der Standardwert ist 300 Sekunden (5 Minuten).</span><span class="sxs-lookup"><span data-stu-id="2a246-142">The default is 300 seconds (5 minutes).</span></span> |
| <span data-ttu-id="2a246-143">Verbosity</span><span class="sxs-lookup"><span data-stu-id="2a246-143">Verbosity</span></span> | <span data-ttu-id="2a246-144">Gibt an, die Anzahl der Details in der Ausgabe angezeigt: *normalen*, *quiet*, *ausführliche*.</span><span class="sxs-lookup"><span data-stu-id="2a246-144">Specifies the amount of detail displayed in the output: *normal*, *quiet*, *detailed*.</span></span> |

<span data-ttu-id="2a246-145">Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)</span><span class="sxs-lookup"><span data-stu-id="2a246-145">Also see [Environment variables](cli-ref-environment-variables.md)</span></span>

## <a name="examples"></a><span data-ttu-id="2a246-146">Beispiele</span><span class="sxs-lookup"><span data-stu-id="2a246-146">Examples</span></span>

```cli
nuget push foo.nupkg

nuget push foo.symbols.nupkg

nuget push foo.nupkg -Timeout 360

nuget push *.nupkg

nuget.exe push -source \\mycompany\repo\ mypackage.1.0.0.nupkg

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -Source https://api.nuget.org/v3/index.json

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a

nuget push foo.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -src https://customsource/

:: In the example below -SkipDuplicate will skip pushing the package if package "Foo" version "5.0.2" already exists on NuGet.org
nuget push Foo.5.0.2.nupkg 4003d786-cc37-4004-bfdf-c4f3e8ef9b3a -src https://api.nuget.org/v3/index.json -SkipDuplicate
```
