---
title: Cross Platform-Plug-ins
description: Nuget-plattformübergreifende Plug-Ins für nuget. exe, dotnet. exe, MSBuild. exe und Visual Studio
author: nkolev92
ms.author: nikolev
ms.date: 07/01/2018
ms.topic: conceptual
ms.openlocfilehash: 00410214500c7f5256be243dd6fca0907ba9b0c4
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/16/2020
ms.locfileid: "79428384"
---
# <a name="nuget-cross-platform-plugins"></a><span data-ttu-id="a81fd-103">Cross Platform-Plug-ins</span><span class="sxs-lookup"><span data-stu-id="a81fd-103">NuGet cross platform plugins</span></span>

<span data-ttu-id="a81fd-104">In nuget 4.8 und höher wurde die Unterstützung für plattformübergreifende Plug-Ins hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="a81fd-104">In NuGet 4.8+ support for cross platform plugins has been added.</span></span>
<span data-ttu-id="a81fd-105">Dies wurde durch das Entwickeln eines neuen Plug-in-Erweiterbarkeits Modells erreicht, das einem strengen Satz von Vorgangs Regeln entspricht.</span><span class="sxs-lookup"><span data-stu-id="a81fd-105">This was achieved with by building a new plugin extensibility model, that has to conform to a strict set of rules of operation.</span></span>
<span data-ttu-id="a81fd-106">Die Plug-ins sind eigenständige ausführbare Dateien (Runnables in der .net Core-Welt), die von den nuget-Clients in einem separaten Prozess gestartet werden.</span><span class="sxs-lookup"><span data-stu-id="a81fd-106">The plugins are self-contained executables (runnables in the .NET Core world), that the NuGet Clients launch in a separate process.</span></span>
<span data-ttu-id="a81fd-107">Dies ist ein echter Schreibvorgang, wenn Sie das Plug-in überall ausführen.</span><span class="sxs-lookup"><span data-stu-id="a81fd-107">This is a true write once, run everywhere plugin.</span></span> <span data-ttu-id="a81fd-108">Es funktioniert mit allen nuget-Client Tools.</span><span class="sxs-lookup"><span data-stu-id="a81fd-108">It will work with all NuGet client tools.</span></span>
<span data-ttu-id="a81fd-109">Die Plug-Ins können entweder .NET Framework (nuget. exe, MSBuild. exe und Visual Studio) oder .net Core (dotnet. exe) sein.</span><span class="sxs-lookup"><span data-stu-id="a81fd-109">The plugins can be either .NET Framework (NuGet.exe, MSBuild.exe and Visual Studio), or .NET Core (dotnet.exe).</span></span>
<span data-ttu-id="a81fd-110">Ein Kommunikationsprotokoll mit Versions Angabe zwischen dem nuget-Client und dem-Plug-in ist definiert.</span><span class="sxs-lookup"><span data-stu-id="a81fd-110">A versioned communication protocol between the NuGet Client and the plugin is defined.</span></span> <span data-ttu-id="a81fd-111">Während des Start Handshakes aushandeln die beiden Prozesse die Protokollversion.</span><span class="sxs-lookup"><span data-stu-id="a81fd-111">During the startup handshake, the 2 processes negotiate the protocol version.</span></span>

<span data-ttu-id="a81fd-112">Um alle Szenarien für nuget-Client Tools abzudecken, benötigen Sie eine .NET Framework und ein .net Core-Plug-in.</span><span class="sxs-lookup"><span data-stu-id="a81fd-112">In order to cover all NuGet client tools scenarios, one would need both a .NET Framework and a .NET Core plugin.</span></span>
<span data-ttu-id="a81fd-113">Im folgenden werden die Client/Framework-Kombinationen der Plug-Ins beschrieben.</span><span class="sxs-lookup"><span data-stu-id="a81fd-113">The below describes the client/framework combinations of the plugins.</span></span>

| <span data-ttu-id="a81fd-114">Clienttool</span><span class="sxs-lookup"><span data-stu-id="a81fd-114">Client tool</span></span>  | <span data-ttu-id="a81fd-115">Framework</span><span class="sxs-lookup"><span data-stu-id="a81fd-115">Framework</span></span> |
| ------------ | --------- |
| <span data-ttu-id="a81fd-116">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="a81fd-116">Visual Studio</span></span> | <span data-ttu-id="a81fd-117">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="a81fd-117">.NET Framework</span></span> |
| <span data-ttu-id="a81fd-118">dotnet.exe</span><span class="sxs-lookup"><span data-stu-id="a81fd-118">dotnet.exe</span></span> | <span data-ttu-id="a81fd-119">.NET Core</span><span class="sxs-lookup"><span data-stu-id="a81fd-119">.NET Core</span></span> |
| <span data-ttu-id="a81fd-120">"Nuget. exe"</span><span class="sxs-lookup"><span data-stu-id="a81fd-120">NuGet.exe</span></span> | <span data-ttu-id="a81fd-121">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="a81fd-121">.NET Framework</span></span> |
| <span data-ttu-id="a81fd-122">MSBuild. exe</span><span class="sxs-lookup"><span data-stu-id="a81fd-122">MSBuild.exe</span></span> | <span data-ttu-id="a81fd-123">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="a81fd-123">.NET Framework</span></span> |
| <span data-ttu-id="a81fd-124">"Nuget. exe" unter Mono</span><span class="sxs-lookup"><span data-stu-id="a81fd-124">NuGet.exe on Mono</span></span> | <span data-ttu-id="a81fd-125">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="a81fd-125">.NET Framework</span></span> |

## <a name="how-does-it-work"></a><span data-ttu-id="a81fd-126">Funktionsweise</span><span class="sxs-lookup"><span data-stu-id="a81fd-126">How does it work</span></span>

<span data-ttu-id="a81fd-127">Der allgemeine Workflow kann wie folgt beschrieben werden:</span><span class="sxs-lookup"><span data-stu-id="a81fd-127">The high level workflow can be described as follows:</span></span>

1. <span data-ttu-id="a81fd-128">Nuget erkennt verfügbare Plug-ins.</span><span class="sxs-lookup"><span data-stu-id="a81fd-128">NuGet discovers available plugins.</span></span>
1. <span data-ttu-id="a81fd-129">Wenn zutreffend, durchläuft nuget die Plug-ins in der Reihenfolge der Priorität und startet Sie nacheinander.</span><span class="sxs-lookup"><span data-stu-id="a81fd-129">When applicable, NuGet will iterate over the plugins in priority order and starts them one by one.</span></span>
1. <span data-ttu-id="a81fd-130">Nuget verwendet das erste Plug-in, das die Anforderung bedienen kann.</span><span class="sxs-lookup"><span data-stu-id="a81fd-130">NuGet will use the first plugin that can service the request.</span></span>
1. <span data-ttu-id="a81fd-131">Die Plug-ins werden heruntergefahren, wenn Sie nicht mehr benötigt werden.</span><span class="sxs-lookup"><span data-stu-id="a81fd-131">The plugins will be shut down when they are no longer needed.</span></span>

## <a name="general-plugin-requirements"></a><span data-ttu-id="a81fd-132">Allgemeine Plug-ins</span><span class="sxs-lookup"><span data-stu-id="a81fd-132">General plugin requirements</span></span>

<span data-ttu-id="a81fd-133">Die aktuelle Protokollversion ist *2.0.0*.</span><span class="sxs-lookup"><span data-stu-id="a81fd-133">The current protocol version is *2.0.0*.</span></span>
<span data-ttu-id="a81fd-134">Unter dieser Version gelten die folgenden Anforderungen:</span><span class="sxs-lookup"><span data-stu-id="a81fd-134">Under this version, the requirements are as follows:</span></span>

- <span data-ttu-id="a81fd-135">Sie verfügen über eine gültige vertrauenswürdige Authenticode-Signatur-Assemblys, die unter Windows und Mono ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="a81fd-135">Have a valid, trusted Authenticode signature assemblies that will run on Windows and Mono.</span></span> <span data-ttu-id="a81fd-136">Für Assemblys, die unter Linux und Mac ausgeführt werden, ist keine besondere Vertrauensstellung erforderlich.</span><span class="sxs-lookup"><span data-stu-id="a81fd-136">There is no special trust requirement for assemblies run on Linux and Mac yet.</span></span> [<span data-ttu-id="a81fd-137">Relevantes Problem</span><span class="sxs-lookup"><span data-stu-id="a81fd-137">Relevant issue</span></span>](https://github.com/NuGet/Home/issues/6702)
- <span data-ttu-id="a81fd-138">Unterstützung des Zustands losen Starts im aktuellen Sicherheitskontext der nuget-Client Tools.</span><span class="sxs-lookup"><span data-stu-id="a81fd-138">Support stateless launching under the current security context of NuGet client tools.</span></span> <span data-ttu-id="a81fd-139">Beispielsweise führen nuget-Client Tools keine Rechte Erweiterung oder zusätzliche Initialisierung außerhalb des später beschriebenen Plug-in-Protokolls aus.</span><span class="sxs-lookup"><span data-stu-id="a81fd-139">For example, NuGet client tools will not perform elevation or additional initialization outside of the plugin protocol described later.</span></span>
- <span data-ttu-id="a81fd-140">Wenn Sie nicht explizit angegeben sind, sind Sie nicht interaktiv.</span><span class="sxs-lookup"><span data-stu-id="a81fd-140">Be non interactive, unless explicitly specified.</span></span>
- <span data-ttu-id="a81fd-141">Einhaltung der ausgehandelten Plug-in-Protokollversion.</span><span class="sxs-lookup"><span data-stu-id="a81fd-141">Adhere to the negotiated plugin protocol version.</span></span>
- <span data-ttu-id="a81fd-142">Reagieren Sie innerhalb eines angemessenen Zeitraums auf alle Anforderungen.</span><span class="sxs-lookup"><span data-stu-id="a81fd-142">Respond to all requests within a reasonable time period.</span></span>
- <span data-ttu-id="a81fd-143">Beachten Sie Abbruch Anforderungen für alle laufenden Vorgänge.</span><span class="sxs-lookup"><span data-stu-id="a81fd-143">Honor cancellation requests for any in-progress operation.</span></span>

<span data-ttu-id="a81fd-144">Die technische Spezifikation wird in den folgenden Spezifikationen ausführlicher beschrieben:</span><span class="sxs-lookup"><span data-stu-id="a81fd-144">The technical specification is described in more detail in the following specs:</span></span>

- [<span data-ttu-id="a81fd-145">Plug-in für nuget-Paket</span><span class="sxs-lookup"><span data-stu-id="a81fd-145">NuGet Package Download Plugin</span></span>](https://github.com/NuGet/Home/wiki/NuGet-Package-Download-Plugin)
- [<span data-ttu-id="a81fd-146">Nuget-Plug-in für die nuget-Authentifizierung</span><span class="sxs-lookup"><span data-stu-id="a81fd-146">NuGet cross plat authentication plugin</span></span>](https://github.com/NuGet/Home/wiki/NuGet-cross-plat-authentication-plugin)

## <a name="client---plugin-interaction"></a><span data-ttu-id="a81fd-147">Client-Plug-in-Interaktion</span><span class="sxs-lookup"><span data-stu-id="a81fd-147">Client - Plugin interaction</span></span>

<span data-ttu-id="a81fd-148">Die nuget-Client Tools und-Plug-ins kommunizieren mit JSON über Standardstreams (stdin, stdout, stderr).</span><span class="sxs-lookup"><span data-stu-id="a81fd-148">NuGet client tools and the plugins communicate with JSON over standard streams (stdin, stdout, stderr).</span></span> <span data-ttu-id="a81fd-149">Alle Daten müssen UTF-8-codiert sein.</span><span class="sxs-lookup"><span data-stu-id="a81fd-149">All data must be UTF-8 encoded.</span></span>
<span data-ttu-id="a81fd-150">Die Plug-ins werden mit dem Argument "-Plugin" gestartet.</span><span class="sxs-lookup"><span data-stu-id="a81fd-150">The plugins are launched with the argument "-Plugin".</span></span> <span data-ttu-id="a81fd-151">Wenn ein Benutzer eine ausführbare Plug-in-Datei ohne dieses Argument direkt aufruft, kann das Plug-in eine informative Nachricht senden, anstatt auf einen Protokoll Hand Shake zu warten.</span><span class="sxs-lookup"><span data-stu-id="a81fd-151">In case a user directly launches a plugin executable without this argument, the plugin can give an informative message instead of waiting for a protocol handshake.</span></span>
<span data-ttu-id="a81fd-152">Der Protokoll Hand Shake Timeout beträgt 5 Sekunden.</span><span class="sxs-lookup"><span data-stu-id="a81fd-152">The protocol handshake timeout is 5 seconds.</span></span> <span data-ttu-id="a81fd-153">Das Plug-in sollte das Setup so kurz wie möglich ausführen.</span><span class="sxs-lookup"><span data-stu-id="a81fd-153">The plugin should complete the setup in as short of an amount as possible.</span></span>
<span data-ttu-id="a81fd-154">Die nuget-Client Tools werden die unterstützten Vorgänge eines Plug-ins Abfragen, indem der Dienst Index für eine nuget-Quelle übergeben wird.</span><span class="sxs-lookup"><span data-stu-id="a81fd-154">NuGet client tools will query a plugin’s supported operations by passing in the service index for a NuGet source.</span></span> <span data-ttu-id="a81fd-155">Ein Plug-in kann den Dienst Index verwenden, um zu überprüfen, ob die unterstützten Dienst Typen vorhanden sind.</span><span class="sxs-lookup"><span data-stu-id="a81fd-155">A plugin may use the service index to check for the presence of supported service types.</span></span>

<span data-ttu-id="a81fd-156">Die Kommunikation zwischen den nuget-Client Tools und dem Plug-in ist bidirektional.</span><span class="sxs-lookup"><span data-stu-id="a81fd-156">The communication between the NuGet client tools and the plugin is bidirectional.</span></span> <span data-ttu-id="a81fd-157">Jede Anforderung hat ein Timeout von 5 Sekunden.</span><span class="sxs-lookup"><span data-stu-id="a81fd-157">Each request has a timeout of 5 seconds.</span></span> <span data-ttu-id="a81fd-158">Wenn der Vorgang länger dauern soll, sollte der jeweilige Prozess eine Statusmeldung senden, um eine Zeitüberschreitung der Anforderung zu verhindern. Nach 1 Minuten Inaktivität wird ein Plug-in als Leerlauf betrachtet und heruntergefahren.</span><span class="sxs-lookup"><span data-stu-id="a81fd-158">If operations are supposed to take longer the respective process should send out a progress message to prevent the request from timing out. After 1 minute of inactivity a plugin is considered idle and is shut down.</span></span>

## <a name="plugin-installation-and-discovery"></a><span data-ttu-id="a81fd-159">Installation und Ermittlung von Plug-ins</span><span class="sxs-lookup"><span data-stu-id="a81fd-159">Plugin installation and discovery</span></span>

<span data-ttu-id="a81fd-160">Die Plug-ins werden über eine auf Konventionen basierende Verzeichnisstruktur ermittelt.</span><span class="sxs-lookup"><span data-stu-id="a81fd-160">The plugins will be discovered via a convention based directory structure.</span></span>
<span data-ttu-id="a81fd-161">CI/CD-Szenarien und Poweruser können Umgebungsvariablen verwenden, um das Verhalten zu überschreiben.</span><span class="sxs-lookup"><span data-stu-id="a81fd-161">CI/CD scenarios and power users can use environment variables to override the behavior.</span></span> <span data-ttu-id="a81fd-162">Wenn Sie Umgebungsvariablen verwenden, sind nur absolute Pfade zulässig.</span><span class="sxs-lookup"><span data-stu-id="a81fd-162">When using environment variables, only absolute paths are allowed.</span></span> <span data-ttu-id="a81fd-163">Beachten Sie, dass `NUGET_NETFX_PLUGIN_PATHS` und `NUGET_NETCORE_PLUGIN_PATHS` nur mit einer Version von 5.3 und höher für die nuget-Tools und höher verfügbar sind.</span><span class="sxs-lookup"><span data-stu-id="a81fd-163">Note that `NUGET_NETFX_PLUGIN_PATHS` and `NUGET_NETCORE_PLUGIN_PATHS` are only available with 5.3+ version of the NuGet tooling and later.</span></span>

- <span data-ttu-id="a81fd-164">`NUGET_NETFX_PLUGIN_PATHS`: definiert die Plug-ins, die von den .NET Framework basierten Tools (nuget. exe/MSBuild. exe/Visual Studio) verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="a81fd-164">`NUGET_NETFX_PLUGIN_PATHS` - defines the plugins that will be used by the .NET Framework based tooling (NuGet.exe/MSBuild.exe/Visual Studio).</span></span> <span data-ttu-id="a81fd-165">Hat Vorrang vor `NUGET_PLUGIN_PATHS`.</span><span class="sxs-lookup"><span data-stu-id="a81fd-165">Takes precedence over `NUGET_PLUGIN_PATHS`.</span></span> <span data-ttu-id="a81fd-166">(Nur nuget-Version 5.3 +)</span><span class="sxs-lookup"><span data-stu-id="a81fd-166">(NuGet version 5.3+ only)</span></span>
- <span data-ttu-id="a81fd-167">`NUGET_NETCORE_PLUGIN_PATHS`: definiert die Plug-ins, die von den .net Core-basierten Tools (dotnet. exe) verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="a81fd-167">`NUGET_NETCORE_PLUGIN_PATHS` - defines the plugins that will be used by the .NET Core based tooling (dotnet.exe).</span></span> <span data-ttu-id="a81fd-168">Hat Vorrang vor `NUGET_PLUGIN_PATHS`.</span><span class="sxs-lookup"><span data-stu-id="a81fd-168">Takes precedence over `NUGET_PLUGIN_PATHS`.</span></span> <span data-ttu-id="a81fd-169">(Nur nuget-Version 5.3 +)</span><span class="sxs-lookup"><span data-stu-id="a81fd-169">(NuGet version 5.3+ only)</span></span>
- <span data-ttu-id="a81fd-170">`NUGET_PLUGIN_PATHS`: definiert die Plug-ins, die für den nuget-Prozess verwendet werden. die Priorität wird beibehalten.</span><span class="sxs-lookup"><span data-stu-id="a81fd-170">`NUGET_PLUGIN_PATHS` - defines the plugins that will be used for that NuGet process, priority preserved.</span></span> <span data-ttu-id="a81fd-171">Wenn diese Umgebungsvariable festgelegt ist, wird die auf der Konvention basierende Ermittlung überschrieben.</span><span class="sxs-lookup"><span data-stu-id="a81fd-171">If this environment variable is set, it overrides the convention based discovery.</span></span> <span data-ttu-id="a81fd-172">Wird ignoriert, wenn eine der Framework-spezifischen Variablen angegeben wird.</span><span class="sxs-lookup"><span data-stu-id="a81fd-172">Ignored if either of the framework specific variables is specified.</span></span>
-  <span data-ttu-id="a81fd-173">Benutzer-Location: der nuget-Start Speicherort in `%UserProfile%/.nuget/plugins`.</span><span class="sxs-lookup"><span data-stu-id="a81fd-173">User-location, the NuGet Home location in `%UserProfile%/.nuget/plugins`.</span></span> <span data-ttu-id="a81fd-174">Dieser Speicherort kann nicht überschrieben werden.</span><span class="sxs-lookup"><span data-stu-id="a81fd-174">This location cannot be overriden.</span></span> <span data-ttu-id="a81fd-175">Für .net Core-und .NET Framework-Plug-ins wird ein anderes Stammverzeichnis verwendet.</span><span class="sxs-lookup"><span data-stu-id="a81fd-175">A different root directory will be used for .NET Core and .NET Framework plugins.</span></span>

| <span data-ttu-id="a81fd-176">Framework</span><span class="sxs-lookup"><span data-stu-id="a81fd-176">Framework</span></span> | <span data-ttu-id="a81fd-177">Speicherort der Stamm Ermittlung</span><span class="sxs-lookup"><span data-stu-id="a81fd-177">Root discovery location</span></span>  |
| ------- | ------------------------ |
| <span data-ttu-id="a81fd-178">.NET Core</span><span class="sxs-lookup"><span data-stu-id="a81fd-178">.NET Core</span></span> |  `%UserProfile%/.nuget/plugins/netcore` |
| <span data-ttu-id="a81fd-179">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="a81fd-179">.NET Framework</span></span> | `%UserProfile%/.nuget/plugins/netfx` |

<span data-ttu-id="a81fd-180">Jedes Plug-in sollte in einem eigenen Ordner installiert werden.</span><span class="sxs-lookup"><span data-stu-id="a81fd-180">Each plugin should be installed in its own folder.</span></span>
<span data-ttu-id="a81fd-181">Der Plug-in-Einstiegspunkt ist der Name des installierten Ordners mit den dll-Erweiterungen für .net Core und der Erweiterung ". exe" für .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="a81fd-181">The plugin entry point will be the name of the installed folder, with the .dll extensions for .NET Core, and .exe extension for .NET Framework.</span></span>

```
.nuget
    plugins
        netfx
            myPlugin
                myPlugin.exe
                nuget.protocol.dll
                ...
        netcore
            myPlugin
                myPlugin.dll
                nuget.protocol.dll
                ...
```

> [!Note]
> <span data-ttu-id="a81fd-182">Zurzeit gibt es keine User Story für die Installation der Plug-ins.</span><span class="sxs-lookup"><span data-stu-id="a81fd-182">There is currently no user story for the installation of the plugins.</span></span> <span data-ttu-id="a81fd-183">Es ist ganz einfach, die erforderlichen Dateien an den vordefinierten Speicherort zu verschieben.</span><span class="sxs-lookup"><span data-stu-id="a81fd-183">It's as simple as moving the required files into the predetermined location.</span></span>

## <a name="supported-operations"></a><span data-ttu-id="a81fd-184">Unterstützte Vorgänge</span><span class="sxs-lookup"><span data-stu-id="a81fd-184">Supported operations</span></span>

<span data-ttu-id="a81fd-185">Unter dem neuen Plug-in-Protokoll werden zwei Vorgänge unterstützt.</span><span class="sxs-lookup"><span data-stu-id="a81fd-185">Two operations are supported under the new plugin protocol.</span></span>

| <span data-ttu-id="a81fd-186">Vorgangsname</span><span class="sxs-lookup"><span data-stu-id="a81fd-186">Operation name</span></span> | <span data-ttu-id="a81fd-187">Minimale Protokollversion</span><span class="sxs-lookup"><span data-stu-id="a81fd-187">Minimum protocol version</span></span> | <span data-ttu-id="a81fd-188">Minimale nuget-Client Version</span><span class="sxs-lookup"><span data-stu-id="a81fd-188">Minimum NuGet client version</span></span> |
| -------------- | ----------------------- | --------------------- |
| <span data-ttu-id="a81fd-189">Paket herunterladen</span><span class="sxs-lookup"><span data-stu-id="a81fd-189">Download Package</span></span> | <span data-ttu-id="a81fd-190">1.0.0</span><span class="sxs-lookup"><span data-stu-id="a81fd-190">1.0.0</span></span> | <span data-ttu-id="a81fd-191">4.3.0</span><span class="sxs-lookup"><span data-stu-id="a81fd-191">4.3.0</span></span> |
| [<span data-ttu-id="a81fd-192">Authentifizierung</span><span class="sxs-lookup"><span data-stu-id="a81fd-192">Authentication</span></span>](NuGet-Cross-Platform-Authentication-Plugin.md) | <span data-ttu-id="a81fd-193">2.0.0</span><span class="sxs-lookup"><span data-stu-id="a81fd-193">2.0.0</span></span> | <span data-ttu-id="a81fd-194">4.8.0</span><span class="sxs-lookup"><span data-stu-id="a81fd-194">4.8.0</span></span> |

## <a name="running-plugins-under-the-correct-runtime"></a><span data-ttu-id="a81fd-195">Ausführen von Plug-ins unter der richtigen Laufzeit</span><span class="sxs-lookup"><span data-stu-id="a81fd-195">Running plugins under the correct runtime</span></span>

<span data-ttu-id="a81fd-196">Für nuget-Szenarien in dotnet. exe müssen Plug-ins unter dieser bestimmten Laufzeit von "dotnet. exe" ausgeführt werden können.</span><span class="sxs-lookup"><span data-stu-id="a81fd-196">For the NuGet in dotnet.exe scenarios, plugins need to be able to execute under that specific runtime of the dotnet.exe.</span></span>
<span data-ttu-id="a81fd-197">Er ist auf dem Plug-in-Anbieter und dem Consumer, um sicherzustellen, dass eine kompatible Kombination aus "dotnet. exe/Plugin" verwendet wird</span><span class="sxs-lookup"><span data-stu-id="a81fd-197">It's on the plugin provider and the consumer to make sure a compatible dotnet.exe/plugin combination is used.</span></span>
<span data-ttu-id="a81fd-198">Ein potenzielles Problem könnte bei den Benutzer-/Speicherort-Plug-ins auftreten, wenn beispielsweise eine dotnet. exe-Datei unter der 2,0-Laufzeit versucht, ein für die 2,1-Laufzeit geschriebenes Plug-in</span><span class="sxs-lookup"><span data-stu-id="a81fd-198">A potential issue could arise with the user-location plugins when for example, a dotnet.exe under the 2.0 runtime tries to use a plugin written for the 2.1 runtime.</span></span>

## <a name="capabilities-caching"></a><span data-ttu-id="a81fd-199">Zwischenspeichern von Funktionen</span><span class="sxs-lookup"><span data-stu-id="a81fd-199">Capabilities caching</span></span>

<span data-ttu-id="a81fd-200">Die Sicherheitsüberprüfung und-Instanziierung der Plug-ins ist aufwendig.</span><span class="sxs-lookup"><span data-stu-id="a81fd-200">The security verification and instantiation of the plugins is costly.</span></span> <span data-ttu-id="a81fd-201">Der Downloadvorgang erfolgt häufiger als der Authentifizierungs Vorgang, aber der durchschnittliche nuget-Benutzer hat wahrscheinlich nur ein Authentifizierungs-Plug-in.</span><span class="sxs-lookup"><span data-stu-id="a81fd-201">The download operation happens way more frequently than the authentication operation, however the average NuGet user is only likely to have an authentication plugin.</span></span>
<span data-ttu-id="a81fd-202">Um die Leistung zu verbessern, speichert nuget die Vorgangs Ansprüche für die angegebene Anforderung zwischen.</span><span class="sxs-lookup"><span data-stu-id="a81fd-202">To improve the experience, NuGet will cache the operation claims for the given request.</span></span> <span data-ttu-id="a81fd-203">Dieser Cache ist pro Plug-in, wobei der Plug-in-Pfad der Plug-in-Pfad ist, und der Ablauf für diesen Funktions Cache beträgt 30 Tage.</span><span class="sxs-lookup"><span data-stu-id="a81fd-203">This cache is per plugin with the plugin key being the plugin path, and the expiration for this capabilities cache is 30 days.</span></span> 

<span data-ttu-id="a81fd-204">Der Cache befindet sich in `%LocalAppData%/NuGet/plugins-cache` und kann mit der Umgebungsvariablen `NUGET_PLUGINS_CACHE_PATH`überschrieben werden.</span><span class="sxs-lookup"><span data-stu-id="a81fd-204">The cache is located in `%LocalAppData%/NuGet/plugins-cache` and be overriden with the environment variable `NUGET_PLUGINS_CACHE_PATH`.</span></span> <span data-ttu-id="a81fd-205">Zum Löschen dieses [Caches](../../consume-packages/managing-the-global-packages-and-cache-folders.md)können Sie den Befehl "Locals" mit der Option "`plugins-cache`" ausführen.</span><span class="sxs-lookup"><span data-stu-id="a81fd-205">To clear this [cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md), one can run the locals command with the `plugins-cache` option.</span></span>
<span data-ttu-id="a81fd-206">Mit der Option "`all` Locals" wird nun auch der Plug-in-Cache gelöscht.</span><span class="sxs-lookup"><span data-stu-id="a81fd-206">The `all` locals option will now also delete the plugins cache.</span></span> 

## <a name="protocol-messages-index"></a><span data-ttu-id="a81fd-207">Protokollnachrichten Index</span><span class="sxs-lookup"><span data-stu-id="a81fd-207">Protocol messages index</span></span>

<span data-ttu-id="a81fd-208">Protokoll Version *1.0.0* :</span><span class="sxs-lookup"><span data-stu-id="a81fd-208">Protocol Version *1.0.0* messages:</span></span>

1.  <span data-ttu-id="a81fd-209">Close (Schließen)</span><span class="sxs-lookup"><span data-stu-id="a81fd-209">Close</span></span>
    * <span data-ttu-id="a81fd-210">Anforderungs Richtung: nuget->-Plug-in</span><span class="sxs-lookup"><span data-stu-id="a81fd-210">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="a81fd-211">Die Anforderung enthält keine Nutzlast.</span><span class="sxs-lookup"><span data-stu-id="a81fd-211">The request will contain no payload</span></span>
    * <span data-ttu-id="a81fd-212">Es wird keine Antwort erwartet.</span><span class="sxs-lookup"><span data-stu-id="a81fd-212">No response is expected.</span></span>  <span data-ttu-id="a81fd-213">Die richtige Antwort besteht darin, dass der Plug-in-Prozess umgehend beendet wird.</span><span class="sxs-lookup"><span data-stu-id="a81fd-213">The proper response is for the plugin process to promptly exit.</span></span>

2.  <span data-ttu-id="a81fd-214">Dateien in Paket kopieren</span><span class="sxs-lookup"><span data-stu-id="a81fd-214">Copy files in package</span></span>
    * <span data-ttu-id="a81fd-215">Anforderungs Richtung: nuget->-Plug-in</span><span class="sxs-lookup"><span data-stu-id="a81fd-215">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="a81fd-216">Die Anforderung enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="a81fd-216">The request will contain:</span></span>
        * <span data-ttu-id="a81fd-217">die Paket-ID und die Version</span><span class="sxs-lookup"><span data-stu-id="a81fd-217">the package ID and version</span></span>
        * <span data-ttu-id="a81fd-218">Speicherort des Paket Quell Repository</span><span class="sxs-lookup"><span data-stu-id="a81fd-218">the package source repository location</span></span>
        * <span data-ttu-id="a81fd-219">Zielverzeichnis Pfad</span><span class="sxs-lookup"><span data-stu-id="a81fd-219">destination directory path</span></span>
        * <span data-ttu-id="a81fd-220">ein Aufzähl bares Element von Dateien im Paket, das in den Zielverzeichnis Pfad kopiert werden soll.</span><span class="sxs-lookup"><span data-stu-id="a81fd-220">an enumerable of files in the package to be copied to the destination directory path</span></span>
    * <span data-ttu-id="a81fd-221">Eine Antwort enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="a81fd-221">A response will contain:</span></span>
        * <span data-ttu-id="a81fd-222">ein Antwort Code, der das Ergebnis des Vorgangs angibt.</span><span class="sxs-lookup"><span data-stu-id="a81fd-222">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="a81fd-223">ein Aufzähl barer vollständiger Pfad für kopierte Dateien im Zielverzeichnis, wenn der Vorgang erfolgreich war.</span><span class="sxs-lookup"><span data-stu-id="a81fd-223">an enumerable of full paths for copied files in the destination directory if the operation was successful</span></span>

3.  <span data-ttu-id="a81fd-224">Paketdatei kopieren (nupkg-Datei)</span><span class="sxs-lookup"><span data-stu-id="a81fd-224">Copy package file (.nupkg)</span></span>
    * <span data-ttu-id="a81fd-225">Anforderungs Richtung: nuget->-Plug-in</span><span class="sxs-lookup"><span data-stu-id="a81fd-225">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="a81fd-226">Die Anforderung enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="a81fd-226">The request will contain:</span></span>
        * <span data-ttu-id="a81fd-227">die Paket-ID und die Version</span><span class="sxs-lookup"><span data-stu-id="a81fd-227">the package ID and version</span></span>
        * <span data-ttu-id="a81fd-228">Speicherort des Paket Quell Repository</span><span class="sxs-lookup"><span data-stu-id="a81fd-228">the package source repository location</span></span>
        * <span data-ttu-id="a81fd-229">der Ziel Datei Pfad.</span><span class="sxs-lookup"><span data-stu-id="a81fd-229">the destination file path</span></span>
    * <span data-ttu-id="a81fd-230">Eine Antwort enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="a81fd-230">A response will contain:</span></span>
        * <span data-ttu-id="a81fd-231">ein Antwort Code, der das Ergebnis des Vorgangs angibt.</span><span class="sxs-lookup"><span data-stu-id="a81fd-231">a response code indicating the outcome of the operation</span></span>

4.  <span data-ttu-id="a81fd-232">Abrufen von Anmeldeinformationen</span><span class="sxs-lookup"><span data-stu-id="a81fd-232">Get credentials</span></span>
    * <span data-ttu-id="a81fd-233">Anforderungs Richtung: Plug-in > nuget</span><span class="sxs-lookup"><span data-stu-id="a81fd-233">Request direction:  plugin -> NuGet</span></span>
    * <span data-ttu-id="a81fd-234">Die Anforderung enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="a81fd-234">The request will contain:</span></span>
        * <span data-ttu-id="a81fd-235">Speicherort des Paket Quell Repository</span><span class="sxs-lookup"><span data-stu-id="a81fd-235">the package source repository location</span></span>
        * <span data-ttu-id="a81fd-236">der HTTP-Statuscode, der über die aktuellen Anmelde Informationen aus dem Paket Quellrepository abgerufen wurde</span><span class="sxs-lookup"><span data-stu-id="a81fd-236">the HTTP status code obtained from the package source repository using current credentials</span></span>
    * <span data-ttu-id="a81fd-237">Eine Antwort enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="a81fd-237">A response will contain:</span></span>
        * <span data-ttu-id="a81fd-238">ein Antwort Code, der das Ergebnis des Vorgangs angibt.</span><span class="sxs-lookup"><span data-stu-id="a81fd-238">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="a81fd-239">ein Benutzername, falls verfügbar</span><span class="sxs-lookup"><span data-stu-id="a81fd-239">a username, if available</span></span>
        * <span data-ttu-id="a81fd-240">ein Kennwort, falls verfügbar</span><span class="sxs-lookup"><span data-stu-id="a81fd-240">a password, if available</span></span>

5.  <span data-ttu-id="a81fd-241">Dateien im Paket erhalten</span><span class="sxs-lookup"><span data-stu-id="a81fd-241">Get files in package</span></span>
    * <span data-ttu-id="a81fd-242">Anforderungs Richtung: nuget->-Plug-in</span><span class="sxs-lookup"><span data-stu-id="a81fd-242">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="a81fd-243">Die Anforderung enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="a81fd-243">The request will contain:</span></span>
        * <span data-ttu-id="a81fd-244">die Paket-ID und die Version</span><span class="sxs-lookup"><span data-stu-id="a81fd-244">the package ID and version</span></span>
        * <span data-ttu-id="a81fd-245">Speicherort des Paket Quell Repository</span><span class="sxs-lookup"><span data-stu-id="a81fd-245">the package source repository location</span></span>
    * <span data-ttu-id="a81fd-246">Eine Antwort enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="a81fd-246">A response will contain:</span></span>
        * <span data-ttu-id="a81fd-247">ein Antwort Code, der das Ergebnis des Vorgangs angibt.</span><span class="sxs-lookup"><span data-stu-id="a81fd-247">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="a81fd-248">ein Aufzähl bares Element von Dateipfaden im Paket, wenn der Vorgang erfolgreich war.</span><span class="sxs-lookup"><span data-stu-id="a81fd-248">an enumerable of file paths in the package if the operation was successful</span></span>

6.  <span data-ttu-id="a81fd-249">Vorgangs Ansprüche abrufen</span><span class="sxs-lookup"><span data-stu-id="a81fd-249">Get operation claims</span></span> 
    * <span data-ttu-id="a81fd-250">Anforderungs Richtung: nuget->-Plug-in</span><span class="sxs-lookup"><span data-stu-id="a81fd-250">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="a81fd-251">Die Anforderung enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="a81fd-251">The request will contain:</span></span>
        * <span data-ttu-id="a81fd-252">der Dienst Index. JSON für eine Paketquelle</span><span class="sxs-lookup"><span data-stu-id="a81fd-252">the service index.json for a package source</span></span>
        * <span data-ttu-id="a81fd-253">Speicherort des Paket Quell Repository</span><span class="sxs-lookup"><span data-stu-id="a81fd-253">the package source repository location</span></span>
    * <span data-ttu-id="a81fd-254">Eine Antwort enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="a81fd-254">A response will contain:</span></span>
        * <span data-ttu-id="a81fd-255">ein Antwort Code, der das Ergebnis des Vorgangs angibt.</span><span class="sxs-lookup"><span data-stu-id="a81fd-255">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="a81fd-256">ein Aufzähl bares Element unterstützter Vorgänge (z. b. Paket Download), wenn der Vorgang erfolgreich war.</span><span class="sxs-lookup"><span data-stu-id="a81fd-256">an enumerable of supported operations (e.g.:  package download) if the operation was successful.</span></span>  <span data-ttu-id="a81fd-257">Wenn ein Plug-in die Paketquelle nicht unterstützt, muss das Plug-in eine leere Gruppe unterstützter Vorgänge zurückgeben.</span><span class="sxs-lookup"><span data-stu-id="a81fd-257">If a plugin does not support the package source, the plugin must return an empty set of supported operations.</span></span>

> [!Note]
> <span data-ttu-id="a81fd-258">Diese Meldung wurde in Version *2.0.0*aktualisiert.</span><span class="sxs-lookup"><span data-stu-id="a81fd-258">This message has been updated in version *2.0.0*.</span></span> <span data-ttu-id="a81fd-259">Sie befindet sich auf dem Client, um die Abwärtskompatibilität aufrechtzuerhalten.</span><span class="sxs-lookup"><span data-stu-id="a81fd-259">It is on the client to preserve backward compatibility.</span></span>

7.  <span data-ttu-id="a81fd-260">Pakethash erhalten</span><span class="sxs-lookup"><span data-stu-id="a81fd-260">Get package hash</span></span>
    * <span data-ttu-id="a81fd-261">Anforderungs Richtung: nuget->-Plug-in</span><span class="sxs-lookup"><span data-stu-id="a81fd-261">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="a81fd-262">Die Anforderung enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="a81fd-262">The request will contain:</span></span>
        * <span data-ttu-id="a81fd-263">die Paket-ID und die Version</span><span class="sxs-lookup"><span data-stu-id="a81fd-263">the package ID and version</span></span>
        * <span data-ttu-id="a81fd-264">Speicherort des Paket Quell Repository</span><span class="sxs-lookup"><span data-stu-id="a81fd-264">the package source repository location</span></span>
        * <span data-ttu-id="a81fd-265">der Hash Algorithmus</span><span class="sxs-lookup"><span data-stu-id="a81fd-265">the hash algorithm</span></span>
    * <span data-ttu-id="a81fd-266">Eine Antwort enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="a81fd-266">A response will contain:</span></span>
        * <span data-ttu-id="a81fd-267">ein Antwort Code, der das Ergebnis des Vorgangs angibt.</span><span class="sxs-lookup"><span data-stu-id="a81fd-267">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="a81fd-268">ein paketdateihash, der den angeforderten Hash Algorithmus verwendet, wenn der Vorgang erfolgreich war.</span><span class="sxs-lookup"><span data-stu-id="a81fd-268">a package file hash using the requested hash algorithm if the operation was successful</span></span>

8.  <span data-ttu-id="a81fd-269">Abrufen von Paketversionen</span><span class="sxs-lookup"><span data-stu-id="a81fd-269">Get package versions</span></span>
    * <span data-ttu-id="a81fd-270">Anforderungs Richtung: nuget->-Plug-in</span><span class="sxs-lookup"><span data-stu-id="a81fd-270">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="a81fd-271">Die Anforderung enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="a81fd-271">The request will contain:</span></span>
        * <span data-ttu-id="a81fd-272">die Paket-ID</span><span class="sxs-lookup"><span data-stu-id="a81fd-272">the package ID</span></span>
        * <span data-ttu-id="a81fd-273">Speicherort des Paket Quell Repository</span><span class="sxs-lookup"><span data-stu-id="a81fd-273">the package source repository location</span></span>
    * <span data-ttu-id="a81fd-274">Eine Antwort enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="a81fd-274">A response will contain:</span></span>
        * <span data-ttu-id="a81fd-275">ein Antwort Code, der das Ergebnis des Vorgangs angibt.</span><span class="sxs-lookup"><span data-stu-id="a81fd-275">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="a81fd-276">ein Aufzähl bares Element von Paketversionen, wenn der Vorgang erfolgreich war.</span><span class="sxs-lookup"><span data-stu-id="a81fd-276">an enumerable of package versions if the operation was successful</span></span>

9.  <span data-ttu-id="a81fd-277">Dienst Index erhalten</span><span class="sxs-lookup"><span data-stu-id="a81fd-277">Get service index</span></span>
    * <span data-ttu-id="a81fd-278">Anforderungs Richtung: Plug-in > nuget</span><span class="sxs-lookup"><span data-stu-id="a81fd-278">Request direction:  plugin -> NuGet</span></span>
    * <span data-ttu-id="a81fd-279">Die Anforderung enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="a81fd-279">The request will contain:</span></span>
        * <span data-ttu-id="a81fd-280">Speicherort des Paket Quell Repository</span><span class="sxs-lookup"><span data-stu-id="a81fd-280">the package source repository location</span></span>
    * <span data-ttu-id="a81fd-281">Eine Antwort enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="a81fd-281">A response will contain:</span></span>
        * <span data-ttu-id="a81fd-282">ein Antwort Code, der das Ergebnis des Vorgangs angibt.</span><span class="sxs-lookup"><span data-stu-id="a81fd-282">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="a81fd-283">der Dienst Index, wenn der Vorgang erfolgreich war.</span><span class="sxs-lookup"><span data-stu-id="a81fd-283">the service index if the operation was successful</span></span>

10.  <span data-ttu-id="a81fd-284">Shakes</span><span class="sxs-lookup"><span data-stu-id="a81fd-284">Handshake</span></span>
     * <span data-ttu-id="a81fd-285">Anforderungs Richtung: nuget-<->-Plug-in</span><span class="sxs-lookup"><span data-stu-id="a81fd-285">Request direction:  NuGet <-> plugin</span></span>
     * <span data-ttu-id="a81fd-286">Die Anforderung enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="a81fd-286">The request will contain:</span></span>
         * <span data-ttu-id="a81fd-287">die aktuelle Plug-in-Protokollversion</span><span class="sxs-lookup"><span data-stu-id="a81fd-287">the current plugin protocol version</span></span>
         * <span data-ttu-id="a81fd-288">die minimal unterstützte Plug-in-Protokollversion</span><span class="sxs-lookup"><span data-stu-id="a81fd-288">the minimum supported plugin protocol version</span></span>
     * <span data-ttu-id="a81fd-289">Eine Antwort enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="a81fd-289">A response will contain:</span></span>
         * <span data-ttu-id="a81fd-290">ein Antwort Code, der das Ergebnis des Vorgangs angibt.</span><span class="sxs-lookup"><span data-stu-id="a81fd-290">a response code indicating the outcome of the operation</span></span>
         * <span data-ttu-id="a81fd-291">die ausgehandelte Protokollversion, wenn der Vorgang erfolgreich war.</span><span class="sxs-lookup"><span data-stu-id="a81fd-291">the negotiated protocol version if the operation was successful.</span></span>  <span data-ttu-id="a81fd-292">Ein Fehler führt zu einer Beendigung des Plug-ins.</span><span class="sxs-lookup"><span data-stu-id="a81fd-292">A failure will result in termination of the plugin.</span></span>

11.  <span data-ttu-id="a81fd-293">Initialisieren</span><span class="sxs-lookup"><span data-stu-id="a81fd-293">Initialize</span></span>
     * <span data-ttu-id="a81fd-294">Anforderungs Richtung: nuget->-Plug-in</span><span class="sxs-lookup"><span data-stu-id="a81fd-294">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="a81fd-295">Die Anforderung enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="a81fd-295">The request will contain:</span></span>
         * <span data-ttu-id="a81fd-296">die Version des nuget-Client Tools</span><span class="sxs-lookup"><span data-stu-id="a81fd-296">the NuGet client tool version</span></span>
         * <span data-ttu-id="a81fd-297">die effektive Sprache des nuget-Client Tools.</span><span class="sxs-lookup"><span data-stu-id="a81fd-297">the NuGet client tool effective language.</span></span>  <span data-ttu-id="a81fd-298">Dabei wird ggf. die Einstellung "forceengloutput" berücksichtigt.</span><span class="sxs-lookup"><span data-stu-id="a81fd-298">This takes into consideration the ForceEnglishOutput setting, if used.</span></span>
         * <span data-ttu-id="a81fd-299">der standardmäßige Anforderungs Timeout, der den Standardwert des Protokolls ersetzt.</span><span class="sxs-lookup"><span data-stu-id="a81fd-299">the default request timeout, which supersedes the protocol default.</span></span>
     * <span data-ttu-id="a81fd-300">Eine Antwort enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="a81fd-300">A response will contain:</span></span>
         * <span data-ttu-id="a81fd-301">ein Antwort Code, der das Ergebnis des Vorgangs angibt.</span><span class="sxs-lookup"><span data-stu-id="a81fd-301">a response code indicating the outcome of the operation.</span></span>  <span data-ttu-id="a81fd-302">Ein Fehler führt zu einer Beendigung des Plug-ins.</span><span class="sxs-lookup"><span data-stu-id="a81fd-302">A failure will result in termination of the plugin.</span></span>

12.  <span data-ttu-id="a81fd-303">Log</span><span class="sxs-lookup"><span data-stu-id="a81fd-303">Log</span></span>
     * <span data-ttu-id="a81fd-304">Anforderungs Richtung: Plug-in > nuget</span><span class="sxs-lookup"><span data-stu-id="a81fd-304">Request direction:  plugin -> NuGet</span></span>
     * <span data-ttu-id="a81fd-305">Die Anforderung enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="a81fd-305">The request will contain:</span></span>
         * <span data-ttu-id="a81fd-306">die Protokollebene für die Anforderung.</span><span class="sxs-lookup"><span data-stu-id="a81fd-306">the log level for the request</span></span>
         * <span data-ttu-id="a81fd-307">eine Meldung, die protokolliert werden soll</span><span class="sxs-lookup"><span data-stu-id="a81fd-307">a message to log</span></span>
     * <span data-ttu-id="a81fd-308">Eine Antwort enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="a81fd-308">A response will contain:</span></span>
         * <span data-ttu-id="a81fd-309">ein Antwort Code, der das Ergebnis des Vorgangs angibt.</span><span class="sxs-lookup"><span data-stu-id="a81fd-309">a response code indicating the outcome of the operation.</span></span>

13.  <span data-ttu-id="a81fd-310">Überwachen von nuget-Prozess beenden</span><span class="sxs-lookup"><span data-stu-id="a81fd-310">Monitor NuGet process exit</span></span>
     * <span data-ttu-id="a81fd-311">Anforderungs Richtung: nuget->-Plug-in</span><span class="sxs-lookup"><span data-stu-id="a81fd-311">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="a81fd-312">Die Anforderung enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="a81fd-312">The request will contain:</span></span>
         * <span data-ttu-id="a81fd-313">die nuget-Prozess-ID</span><span class="sxs-lookup"><span data-stu-id="a81fd-313">the NuGet process ID</span></span>
     * <span data-ttu-id="a81fd-314">Eine Antwort enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="a81fd-314">A response will contain:</span></span>
         * <span data-ttu-id="a81fd-315">ein Antwort Code, der das Ergebnis des Vorgangs angibt.</span><span class="sxs-lookup"><span data-stu-id="a81fd-315">a response code indicating the outcome of the operation.</span></span>

14.  <span data-ttu-id="a81fd-316">Paket vorab abrufen</span><span class="sxs-lookup"><span data-stu-id="a81fd-316">Prefetch package</span></span>
     * <span data-ttu-id="a81fd-317">Anforderungs Richtung: nuget->-Plug-in</span><span class="sxs-lookup"><span data-stu-id="a81fd-317">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="a81fd-318">Die Anforderung enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="a81fd-318">The request will contain:</span></span>
         * <span data-ttu-id="a81fd-319">die Paket-ID und die Version</span><span class="sxs-lookup"><span data-stu-id="a81fd-319">the package ID and version</span></span>
         * <span data-ttu-id="a81fd-320">Speicherort des Paket Quell Repository</span><span class="sxs-lookup"><span data-stu-id="a81fd-320">the package source repository location</span></span>
     * <span data-ttu-id="a81fd-321">Eine Antwort enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="a81fd-321">A response will contain:</span></span>
         * <span data-ttu-id="a81fd-322">ein Antwort Code, der das Ergebnis des Vorgangs angibt.</span><span class="sxs-lookup"><span data-stu-id="a81fd-322">a response code indicating the outcome of the operation</span></span>

15.  <span data-ttu-id="a81fd-323">Festlegen von Anmeldeinformationen</span><span class="sxs-lookup"><span data-stu-id="a81fd-323">Set credentials</span></span>
     * <span data-ttu-id="a81fd-324">Anforderungs Richtung: nuget->-Plug-in</span><span class="sxs-lookup"><span data-stu-id="a81fd-324">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="a81fd-325">Die Anforderung enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="a81fd-325">The request will contain:</span></span>
         * <span data-ttu-id="a81fd-326">Speicherort des Paket Quell Repository</span><span class="sxs-lookup"><span data-stu-id="a81fd-326">the package source repository location</span></span>
         * <span data-ttu-id="a81fd-327">der letzte bekannte Paket Quell Benutzername, falls verfügbar</span><span class="sxs-lookup"><span data-stu-id="a81fd-327">the last known package source username, if available</span></span>
         * <span data-ttu-id="a81fd-328">das letzte bekannte Paket Quell Kennwort, falls verfügbar</span><span class="sxs-lookup"><span data-stu-id="a81fd-328">the last known package source password, if available</span></span>
         * <span data-ttu-id="a81fd-329">der letzte bekannte Proxy Benutzername, falls verfügbar</span><span class="sxs-lookup"><span data-stu-id="a81fd-329">the last known proxy username, if available</span></span>
         * <span data-ttu-id="a81fd-330">Letztes bekanntes Proxy Kennwort, falls verfügbar</span><span class="sxs-lookup"><span data-stu-id="a81fd-330">the last known proxy password, if available</span></span>
     * <span data-ttu-id="a81fd-331">Eine Antwort enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="a81fd-331">A response will contain:</span></span>
         * <span data-ttu-id="a81fd-332">ein Antwort Code, der das Ergebnis des Vorgangs angibt.</span><span class="sxs-lookup"><span data-stu-id="a81fd-332">a response code indicating the outcome of the operation</span></span>

16.  <span data-ttu-id="a81fd-333">Festlegen der Protokollebene</span><span class="sxs-lookup"><span data-stu-id="a81fd-333">Set log level</span></span>
     * <span data-ttu-id="a81fd-334">Anforderungs Richtung: nuget->-Plug-in</span><span class="sxs-lookup"><span data-stu-id="a81fd-334">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="a81fd-335">Die Anforderung enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="a81fd-335">The request will contain:</span></span>
         * <span data-ttu-id="a81fd-336">die Standardprotokoll Ebene</span><span class="sxs-lookup"><span data-stu-id="a81fd-336">the default log level</span></span>
     * <span data-ttu-id="a81fd-337">Eine Antwort enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="a81fd-337">A response will contain:</span></span>
         * <span data-ttu-id="a81fd-338">ein Antwort Code, der das Ergebnis des Vorgangs angibt.</span><span class="sxs-lookup"><span data-stu-id="a81fd-338">a response code indicating the outcome of the operation</span></span>

<span data-ttu-id="a81fd-339">Protokoll Version *2.0.0* -Nachrichten</span><span class="sxs-lookup"><span data-stu-id="a81fd-339">Protocol Version *2.0.0* messages</span></span>

17. <span data-ttu-id="a81fd-340">Vorgangs Ansprüche abrufen</span><span class="sxs-lookup"><span data-stu-id="a81fd-340">Get Operation Claims</span></span>

* <span data-ttu-id="a81fd-341">Anforderungs Richtung: nuget->-Plug-in</span><span class="sxs-lookup"><span data-stu-id="a81fd-341">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="a81fd-342">Die Anforderung enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="a81fd-342">The request will contain:</span></span>
        * <span data-ttu-id="a81fd-343">der Dienst Index. JSON für eine Paketquelle</span><span class="sxs-lookup"><span data-stu-id="a81fd-343">the service index.json for a package source</span></span>
        * <span data-ttu-id="a81fd-344">Speicherort des Paket Quell Repository</span><span class="sxs-lookup"><span data-stu-id="a81fd-344">the package source repository location</span></span>
    * <span data-ttu-id="a81fd-345">Eine Antwort enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="a81fd-345">A response will contain:</span></span>
        * <span data-ttu-id="a81fd-346">ein Antwort Code, der das Ergebnis des Vorgangs angibt.</span><span class="sxs-lookup"><span data-stu-id="a81fd-346">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="a81fd-347">eine Aufzähl Bare der unterstützten Vorgänge, wenn der Vorgang erfolgreich war.</span><span class="sxs-lookup"><span data-stu-id="a81fd-347">an enumerable of supported operations if the operation was successful.</span></span>  <span data-ttu-id="a81fd-348">Wenn ein Plug-in die Paketquelle nicht unterstützt, muss das Plug-in eine leere Gruppe unterstützter Vorgänge zurückgeben.</span><span class="sxs-lookup"><span data-stu-id="a81fd-348">If a plugin does not support the package source, the plugin must return an empty set of supported operations.</span></span>

    <span data-ttu-id="a81fd-349">Wenn der Dienst Index und die Paketquelle NULL sind, kann das Plug-in mit der Authentifizierung Antworten.</span><span class="sxs-lookup"><span data-stu-id="a81fd-349">If the service index and package source are null, then the plugin can answer with authentication.</span></span>

18. <span data-ttu-id="a81fd-350">Authentifizierungs Anmelde Informationen erhalten</span><span class="sxs-lookup"><span data-stu-id="a81fd-350">Get Authentication Credentials</span></span>

* <span data-ttu-id="a81fd-351">Anforderungs Richtung: nuget->-Plug-in</span><span class="sxs-lookup"><span data-stu-id="a81fd-351">Request direction: NuGet -> plugin</span></span>
* <span data-ttu-id="a81fd-352">Die Anforderung enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="a81fd-352">The request will contain:</span></span>
    * <span data-ttu-id="a81fd-353">Uri</span><span class="sxs-lookup"><span data-stu-id="a81fd-353">Uri</span></span>
    * <span data-ttu-id="a81fd-354">Isretry</span><span class="sxs-lookup"><span data-stu-id="a81fd-354">isRetry</span></span>
    * <span data-ttu-id="a81fd-355">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="a81fd-355">NonInteractive</span></span>
    * <span data-ttu-id="a81fd-356">Canshowdialog</span><span class="sxs-lookup"><span data-stu-id="a81fd-356">CanShowDialog</span></span>
* <span data-ttu-id="a81fd-357">Eine Antwort enthält</span><span class="sxs-lookup"><span data-stu-id="a81fd-357">A response will contain</span></span>
    * <span data-ttu-id="a81fd-358">Username</span><span class="sxs-lookup"><span data-stu-id="a81fd-358">Username</span></span>
    * <span data-ttu-id="a81fd-359">Kennwort</span><span class="sxs-lookup"><span data-stu-id="a81fd-359">Password</span></span>
    * <span data-ttu-id="a81fd-360">`Message`</span><span class="sxs-lookup"><span data-stu-id="a81fd-360">Message</span></span>
    * <span data-ttu-id="a81fd-361">Liste der Authentifizierungs Typen</span><span class="sxs-lookup"><span data-stu-id="a81fd-361">List of Auth Types</span></span>
    * <span data-ttu-id="a81fd-362">Messageresponsecode</span><span class="sxs-lookup"><span data-stu-id="a81fd-362">MessageResponseCode</span></span>
