---
title: Cross Platform-Plug-ins
description: Nuget-plattformübergreifende Plug-Ins für nuget. exe, dotnet. exe, MSBuild. exe und Visual Studio
author: nkolev92
ms.author: nikolev
ms.date: 07/01/2018
ms.topic: conceptual
ms.openlocfilehash: 74b80b1791dcb403c90bb3032c009717c11ffe57
ms.sourcegitcommit: 5a741f025e816b684ffe44a81ef7d3fbd2800039
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/09/2019
ms.locfileid: "70815302"
---
# <a name="nuget-cross-platform-plugins"></a><span data-ttu-id="98b74-103">Cross Platform-Plug-ins</span><span class="sxs-lookup"><span data-stu-id="98b74-103">NuGet cross platform plugins</span></span>

<span data-ttu-id="98b74-104">In nuget 4.8 und höher wurde die Unterstützung für plattformübergreifende Plug-Ins hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="98b74-104">In NuGet 4.8+ support for cross platform plugins has been added.</span></span>
<span data-ttu-id="98b74-105">Dies wurde durch das Entwickeln eines neuen Plug-in-Erweiterbarkeits Modells erreicht, das einem strengen Satz von Vorgangs Regeln entspricht.</span><span class="sxs-lookup"><span data-stu-id="98b74-105">This was achieved with by building a new plugin extensibility model, that has to conform to a strict set of rules of operation.</span></span>
<span data-ttu-id="98b74-106">Die Plug-ins sind eigenständige ausführbare Dateien (Runnables in der .net Core-Welt), die von den nuget-Clients in einem separaten Prozess gestartet werden.</span><span class="sxs-lookup"><span data-stu-id="98b74-106">The plugins are self-contained executables (runnables in the .NET Core world), that the NuGet Clients launch in a separate process.</span></span>
<span data-ttu-id="98b74-107">Dies ist ein echter Schreibvorgang, wenn Sie das Plug-in überall ausführen.</span><span class="sxs-lookup"><span data-stu-id="98b74-107">This is a true write once, run everywhere plugin.</span></span> <span data-ttu-id="98b74-108">Es funktioniert mit allen nuget-Client Tools.</span><span class="sxs-lookup"><span data-stu-id="98b74-108">It will work with all NuGet client tools.</span></span>
<span data-ttu-id="98b74-109">Die Plug-Ins können entweder .NET Framework (nuget. exe, MSBuild. exe und Visual Studio) oder .net Core (dotnet. exe) sein.</span><span class="sxs-lookup"><span data-stu-id="98b74-109">The plugins can be either .NET Framework (NuGet.exe, MSBuild.exe and Visual Studio), or .NET Core (dotnet.exe).</span></span>
<span data-ttu-id="98b74-110">Ein Kommunikationsprotokoll mit Versions Angabe zwischen dem nuget-Client und dem-Plug-in ist definiert.</span><span class="sxs-lookup"><span data-stu-id="98b74-110">A versioned communication protocol between the NuGet Client and the plugin is defined.</span></span> <span data-ttu-id="98b74-111">Während des Start Handshakes aushandeln die beiden Prozesse die Protokollversion.</span><span class="sxs-lookup"><span data-stu-id="98b74-111">During the startup handshake, the 2 processes negotiate the protocol version.</span></span>

<span data-ttu-id="98b74-112">Um alle Szenarien für nuget-Client Tools abzudecken, benötigen Sie eine .NET Framework und ein .net Core-Plug-in.</span><span class="sxs-lookup"><span data-stu-id="98b74-112">In order to cover all NuGet client tools scenarios, one would need both a .NET Framework and a .NET Core plugin.</span></span>
<span data-ttu-id="98b74-113">Im folgenden werden die Client/Framework-Kombinationen der Plug-Ins beschrieben.</span><span class="sxs-lookup"><span data-stu-id="98b74-113">The below describes the client/framework combinations of the plugins.</span></span>

| <span data-ttu-id="98b74-114">Client-Tool</span><span class="sxs-lookup"><span data-stu-id="98b74-114">Client tool</span></span>  | <span data-ttu-id="98b74-115">Framework</span><span class="sxs-lookup"><span data-stu-id="98b74-115">Framework</span></span> |
| ------------ | --------- |
| <span data-ttu-id="98b74-116">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="98b74-116">Visual Studio</span></span> | <span data-ttu-id="98b74-117">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="98b74-117">.NET Framework</span></span> |
| <span data-ttu-id="98b74-118">dotnet.exe</span><span class="sxs-lookup"><span data-stu-id="98b74-118">dotnet.exe</span></span> | <span data-ttu-id="98b74-119">.NET Core</span><span class="sxs-lookup"><span data-stu-id="98b74-119">.NET Core</span></span> |
| <span data-ttu-id="98b74-120">"Nuget. exe"</span><span class="sxs-lookup"><span data-stu-id="98b74-120">NuGet.exe</span></span> | <span data-ttu-id="98b74-121">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="98b74-121">.NET Framework</span></span> |
| <span data-ttu-id="98b74-122">MSBuild. exe</span><span class="sxs-lookup"><span data-stu-id="98b74-122">MSBuild.exe</span></span> | <span data-ttu-id="98b74-123">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="98b74-123">.NET Framework</span></span> |
| <span data-ttu-id="98b74-124">"Nuget. exe" unter Mono</span><span class="sxs-lookup"><span data-stu-id="98b74-124">NuGet.exe on Mono</span></span> | <span data-ttu-id="98b74-125">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="98b74-125">.NET Framework</span></span> |

## <a name="how-does-it-work"></a><span data-ttu-id="98b74-126">Funktionsweise</span><span class="sxs-lookup"><span data-stu-id="98b74-126">How does it work</span></span>

<span data-ttu-id="98b74-127">Der allgemeine Workflow kann wie folgt beschrieben werden:</span><span class="sxs-lookup"><span data-stu-id="98b74-127">The high level workflow can be described as follows:</span></span>

1. <span data-ttu-id="98b74-128">Nuget erkennt verfügbare Plug-ins.</span><span class="sxs-lookup"><span data-stu-id="98b74-128">NuGet discovers available plugins.</span></span>
1. <span data-ttu-id="98b74-129">Wenn zutreffend, durchläuft nuget die Plug-ins in der Reihenfolge der Priorität und startet Sie nacheinander.</span><span class="sxs-lookup"><span data-stu-id="98b74-129">When applicable, NuGet will iterate over the plugins in priority order and starts them one by one.</span></span>
1. <span data-ttu-id="98b74-130">Nuget verwendet das erste Plug-in, das die Anforderung bedienen kann.</span><span class="sxs-lookup"><span data-stu-id="98b74-130">NuGet will use the first plugin that can service the request.</span></span>
1. <span data-ttu-id="98b74-131">Die Plug-ins werden heruntergefahren, wenn Sie nicht mehr benötigt werden.</span><span class="sxs-lookup"><span data-stu-id="98b74-131">The plugins will be shut down when they are no longer needed.</span></span>

## <a name="general-plugin-requirements"></a><span data-ttu-id="98b74-132">Allgemeine Plug-ins</span><span class="sxs-lookup"><span data-stu-id="98b74-132">General plugin requirements</span></span>

<span data-ttu-id="98b74-133">Die aktuelle Protokollversion ist *2.0.0*.</span><span class="sxs-lookup"><span data-stu-id="98b74-133">The current protocol version is *2.0.0*.</span></span>
<span data-ttu-id="98b74-134">Unter dieser Version gelten die folgenden Anforderungen:</span><span class="sxs-lookup"><span data-stu-id="98b74-134">Under this version, the requirements are as follows:</span></span>

- <span data-ttu-id="98b74-135">Sie verfügen über eine gültige vertrauenswürdige Authenticode-Signatur-Assemblys, die unter Windows und Mono ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="98b74-135">Have a valid, trusted Authenticode signature assemblies that will run on Windows and Mono.</span></span> <span data-ttu-id="98b74-136">Für Assemblys, die unter Linux und Mac ausgeführt werden, ist keine besondere Vertrauensstellung erforderlich.</span><span class="sxs-lookup"><span data-stu-id="98b74-136">There is no special trust requirement for assemblies run on Linux and Mac yet.</span></span> [<span data-ttu-id="98b74-137">Relevantes Problem</span><span class="sxs-lookup"><span data-stu-id="98b74-137">Relevant issue</span></span>](https://github.com/NuGet/Home/issues/6702)
- <span data-ttu-id="98b74-138">Unterstützung des Zustands losen Starts im aktuellen Sicherheitskontext der nuget-Client Tools.</span><span class="sxs-lookup"><span data-stu-id="98b74-138">Support stateless launching under the current security context of NuGet client tools.</span></span> <span data-ttu-id="98b74-139">Beispielsweise führen nuget-Client Tools keine Rechte Erweiterung oder zusätzliche Initialisierung außerhalb des später beschriebenen Plug-in-Protokolls aus.</span><span class="sxs-lookup"><span data-stu-id="98b74-139">For example, NuGet client tools will not perform elevation or additional initialization outside of the plugin protocol described later.</span></span>
- <span data-ttu-id="98b74-140">Wenn Sie nicht explizit angegeben sind, sind Sie nicht interaktiv.</span><span class="sxs-lookup"><span data-stu-id="98b74-140">Be non interactive, unless explicitly specified.</span></span>
- <span data-ttu-id="98b74-141">Einhaltung der ausgehandelten Plug-in-Protokollversion.</span><span class="sxs-lookup"><span data-stu-id="98b74-141">Adhere to the negotiated plugin protocol version.</span></span>
- <span data-ttu-id="98b74-142">Reagieren Sie innerhalb eines angemessenen Zeitraums auf alle Anforderungen.</span><span class="sxs-lookup"><span data-stu-id="98b74-142">Respond to all requests within a reasonable time period.</span></span>
- <span data-ttu-id="98b74-143">Beachten Sie Abbruch Anforderungen für alle laufenden Vorgänge.</span><span class="sxs-lookup"><span data-stu-id="98b74-143">Honor cancellation requests for any in-progress operation.</span></span>

<span data-ttu-id="98b74-144">Die technische Spezifikation wird in den folgenden Spezifikationen ausführlicher beschrieben:</span><span class="sxs-lookup"><span data-stu-id="98b74-144">The technical specification is described in more detail in the following specs:</span></span>

- [<span data-ttu-id="98b74-145">Plug-in für nuget-Paket</span><span class="sxs-lookup"><span data-stu-id="98b74-145">NuGet Package Download Plugin</span></span>](https://github.com/NuGet/Home/wiki/NuGet-Package-Download-Plugin)
- [<span data-ttu-id="98b74-146">Nuget-Plug-in für die nuget-Authentifizierung</span><span class="sxs-lookup"><span data-stu-id="98b74-146">NuGet cross plat authentication plugin</span></span>](https://github.com/NuGet/Home/wiki/NuGet-cross-plat-authentication-plugin)

## <a name="client---plugin-interaction"></a><span data-ttu-id="98b74-147">Client-Plug-in-Interaktion</span><span class="sxs-lookup"><span data-stu-id="98b74-147">Client - Plugin interaction</span></span>

<span data-ttu-id="98b74-148">Die nuget-Client Tools und-Plug-ins kommunizieren mit JSON über Standardstreams (stdin, stdout, stderr).</span><span class="sxs-lookup"><span data-stu-id="98b74-148">NuGet client tools and the plugins communicate with JSON over standard streams (stdin, stdout, stderr).</span></span> <span data-ttu-id="98b74-149">Alle Daten müssen UTF-8-codiert sein.</span><span class="sxs-lookup"><span data-stu-id="98b74-149">All data must be UTF-8 encoded.</span></span>
<span data-ttu-id="98b74-150">Die Plug-ins werden mit dem Argument "-Plugin" gestartet.</span><span class="sxs-lookup"><span data-stu-id="98b74-150">The plugins are launched with the argument "-Plugin".</span></span> <span data-ttu-id="98b74-151">Wenn ein Benutzer eine ausführbare Plug-in-Datei ohne dieses Argument direkt aufruft, kann das Plug-in eine informative Nachricht senden, anstatt auf einen Protokoll Hand Shake zu warten.</span><span class="sxs-lookup"><span data-stu-id="98b74-151">In case a user directly launches a plugin executable without this argument, the plugin can give an informative message instead of waiting for a protocol handshake.</span></span>
<span data-ttu-id="98b74-152">Der Protokoll Hand Shake Timeout beträgt 5 Sekunden.</span><span class="sxs-lookup"><span data-stu-id="98b74-152">The protocol handshake timeout is 5 seconds.</span></span> <span data-ttu-id="98b74-153">Das Plug-in sollte das Setup so kurz wie möglich ausführen.</span><span class="sxs-lookup"><span data-stu-id="98b74-153">The plugin should complete the setup in as short of an amount as possible.</span></span>
<span data-ttu-id="98b74-154">Die nuget-Client Tools werden die unterstützten Vorgänge eines Plug-ins Abfragen, indem der Dienst Index für eine nuget-Quelle übergeben wird.</span><span class="sxs-lookup"><span data-stu-id="98b74-154">NuGet client tools will query a plugin’s supported operations by passing in the service index for a NuGet source.</span></span> <span data-ttu-id="98b74-155">Ein Plug-in kann den Dienst Index verwenden, um zu überprüfen, ob die unterstützten Dienst Typen vorhanden sind.</span><span class="sxs-lookup"><span data-stu-id="98b74-155">A plugin may use the service index to check for the presence of supported service types.</span></span>

<span data-ttu-id="98b74-156">Die Kommunikation zwischen den nuget-Client Tools und dem Plug-in ist bidirektional.</span><span class="sxs-lookup"><span data-stu-id="98b74-156">The communication between the NuGet client tools and the plugin is bidirectional.</span></span> <span data-ttu-id="98b74-157">Jede Anforderung hat ein Timeout von 5 Sekunden.</span><span class="sxs-lookup"><span data-stu-id="98b74-157">Each request has a timeout of 5 seconds.</span></span> <span data-ttu-id="98b74-158">Wenn der Vorgang länger dauern soll, sollte der jeweilige Prozess eine Statusmeldung senden, um eine Zeitüberschreitung der Anforderung zu verhindern. Nach 1 Minuten Inaktivität wird ein Plug-in als Leerlauf betrachtet und heruntergefahren.</span><span class="sxs-lookup"><span data-stu-id="98b74-158">If operations are supposed to take longer the respective process should send out a progress message to prevent the request from timing out. After 1 minute of inactivity a plugin is considered idle and is shut down.</span></span>

## <a name="plugin-installation-and-discovery"></a><span data-ttu-id="98b74-159">Installation und Ermittlung von Plug-ins</span><span class="sxs-lookup"><span data-stu-id="98b74-159">Plugin installation and discovery</span></span>

<span data-ttu-id="98b74-160">Die Plug-ins werden über eine auf Konventionen basierende Verzeichnisstruktur ermittelt.</span><span class="sxs-lookup"><span data-stu-id="98b74-160">The plugins will be discovered via a convention based directory structure.</span></span>
<span data-ttu-id="98b74-161">CI/CD-Szenarien und Poweruser können Umgebungsvariablen verwenden, um das Verhalten zu überschreiben.</span><span class="sxs-lookup"><span data-stu-id="98b74-161">CI/CD scenarios and power users can use environment variables to override the behavior.</span></span> <span data-ttu-id="98b74-162">Beachten Sie `NUGET_NETFX_PLUGIN_PATHS` , `NUGET_NETCORE_PLUGIN_PATHS` dass und nur mit einer Version von 5.3 und höher für die nuget-Tools und höher verfügbar sind.</span><span class="sxs-lookup"><span data-stu-id="98b74-162">Note that `NUGET_NETFX_PLUGIN_PATHS` and `NUGET_NETCORE_PLUGIN_PATHS` are only available with 5.3+ version of the NuGet tooling and later.</span></span>

- <span data-ttu-id="98b74-163">`NUGET_NETFX_PLUGIN_PATHS`: definiert die Plug-ins, die von den .NET Framework basierten Tools (nuget. exe/MSBuild. exe/Visual Studio) verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="98b74-163">`NUGET_NETFX_PLUGIN_PATHS` - defines the plugins that will be used by the .NET Framework based tooling (NuGet.exe/MSBuild.exe/Visual Studio).</span></span> <span data-ttu-id="98b74-164">Hat Vorrang `NUGET_PLUGIN_PATHS`vor.</span><span class="sxs-lookup"><span data-stu-id="98b74-164">Takes precedence over `NUGET_PLUGIN_PATHS`.</span></span> <span data-ttu-id="98b74-165">(Nur nuget-Version 5.3 +)</span><span class="sxs-lookup"><span data-stu-id="98b74-165">(NuGet version 5.3+ only)</span></span>
- <span data-ttu-id="98b74-166">`NUGET_NETCORE_PLUGIN_PATHS`: definiert die Plug-ins, die von den .net Core-basierten Tools (dotnet. exe) verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="98b74-166">`NUGET_NETCORE_PLUGIN_PATHS` - defines the plugins that will be used by the .NET Core based tooling (dotnet.exe).</span></span> <span data-ttu-id="98b74-167">Hat Vorrang `NUGET_PLUGIN_PATHS`vor.</span><span class="sxs-lookup"><span data-stu-id="98b74-167">Takes precedence over `NUGET_PLUGIN_PATHS`.</span></span> <span data-ttu-id="98b74-168">(Nur nuget-Version 5.3 +)</span><span class="sxs-lookup"><span data-stu-id="98b74-168">(NuGet version 5.3+ only)</span></span>
- <span data-ttu-id="98b74-169">`NUGET_PLUGIN_PATHS`: definiert die Plug-ins, die für den nuget-Prozess verwendet werden, für die die Priorität reserviert ist.</span><span class="sxs-lookup"><span data-stu-id="98b74-169">`NUGET_PLUGIN_PATHS` - defines the plugins that will be used for that NuGet process, priority reserved.</span></span> <span data-ttu-id="98b74-170">Wenn diese Umgebungsvariable festgelegt ist, wird die auf der Konvention basierende Ermittlung überschrieben.</span><span class="sxs-lookup"><span data-stu-id="98b74-170">If this environment variable is set, it overrides the convention based discovery.</span></span> <span data-ttu-id="98b74-171">Wird ignoriert, wenn eine der Framework-spezifischen Variablen angegeben wird.</span><span class="sxs-lookup"><span data-stu-id="98b74-171">Ignored if either of the framework specific variables is specified.</span></span>
-  <span data-ttu-id="98b74-172">Benutzer-Location: der nuget-Start Speicherort in `%UserProfile%/.nuget/plugins`.</span><span class="sxs-lookup"><span data-stu-id="98b74-172">User-location, the NuGet Home location in `%UserProfile%/.nuget/plugins`.</span></span> <span data-ttu-id="98b74-173">Dieser Speicherort kann nicht überschrieben werden.</span><span class="sxs-lookup"><span data-stu-id="98b74-173">This location cannot be overriden.</span></span> <span data-ttu-id="98b74-174">Für .net Core-und .NET Framework-Plug-ins wird ein anderes Stammverzeichnis verwendet.</span><span class="sxs-lookup"><span data-stu-id="98b74-174">A different root directory will be used for .NET Core and .NET Framework plugins.</span></span>

| <span data-ttu-id="98b74-175">Framework</span><span class="sxs-lookup"><span data-stu-id="98b74-175">Framework</span></span> | <span data-ttu-id="98b74-176">Speicherort der Stamm Ermittlung</span><span class="sxs-lookup"><span data-stu-id="98b74-176">Root discovery location</span></span>  |
| ------- | ------------------------ |
| <span data-ttu-id="98b74-177">.NET Core</span><span class="sxs-lookup"><span data-stu-id="98b74-177">.NET Core</span></span> |  `%UserProfile%/.nuget/plugins/netcore` |
| <span data-ttu-id="98b74-178">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="98b74-178">.NET Framework</span></span> | `%UserProfile%/.nuget/plugins/netfx` |

<span data-ttu-id="98b74-179">Jedes Plug-in sollte in einem eigenen Ordner installiert werden.</span><span class="sxs-lookup"><span data-stu-id="98b74-179">Each plugin should be installed in its own folder.</span></span>
<span data-ttu-id="98b74-180">Der Plug-in-Einstiegspunkt ist der Name des installierten Ordners mit den dll-Erweiterungen für .net Core und der Erweiterung ". exe" für .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="98b74-180">The plugin entry point will be the name of the installed folder, with the .dll extensions for .NET Core, and .exe extension for .NET Framework.</span></span>

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
> <span data-ttu-id="98b74-181">Zurzeit gibt es keine User Story für die Installation der Plug-ins.</span><span class="sxs-lookup"><span data-stu-id="98b74-181">There is currently no user story for the installation of the plugins.</span></span> <span data-ttu-id="98b74-182">Es ist ganz einfach, die erforderlichen Dateien an den vordefinierten Speicherort zu verschieben.</span><span class="sxs-lookup"><span data-stu-id="98b74-182">It's as simple as moving the required files into the predetermined location.</span></span>

## <a name="supported-operations"></a><span data-ttu-id="98b74-183">Unterstützte Vorgänge</span><span class="sxs-lookup"><span data-stu-id="98b74-183">Supported operations</span></span>

<span data-ttu-id="98b74-184">Unter dem neuen Plug-in-Protokoll werden zwei Vorgänge unterstützt.</span><span class="sxs-lookup"><span data-stu-id="98b74-184">Two operations are supported under the new plugin protocol.</span></span>

| <span data-ttu-id="98b74-185">Vorgangs Name</span><span class="sxs-lookup"><span data-stu-id="98b74-185">Operation name</span></span> | <span data-ttu-id="98b74-186">Minimale Protokollversion</span><span class="sxs-lookup"><span data-stu-id="98b74-186">Minimum protocol version</span></span> | <span data-ttu-id="98b74-187">Minimale nuget-Client Version</span><span class="sxs-lookup"><span data-stu-id="98b74-187">Minimum NuGet client version</span></span> |
| -------------- | ----------------------- | --------------------- |
| <span data-ttu-id="98b74-188">Paket herunterladen</span><span class="sxs-lookup"><span data-stu-id="98b74-188">Download Package</span></span> | <span data-ttu-id="98b74-189">1.0.0</span><span class="sxs-lookup"><span data-stu-id="98b74-189">1.0.0</span></span> | <span data-ttu-id="98b74-190">4.3.0</span><span class="sxs-lookup"><span data-stu-id="98b74-190">4.3.0</span></span> |
| [<span data-ttu-id="98b74-191">Authentifizierung</span><span class="sxs-lookup"><span data-stu-id="98b74-191">Authentication</span></span>](NuGet-Cross-Platform-Authentication-Plugin.md) | <span data-ttu-id="98b74-192">2.0.0</span><span class="sxs-lookup"><span data-stu-id="98b74-192">2.0.0</span></span> | <span data-ttu-id="98b74-193">4.8.0</span><span class="sxs-lookup"><span data-stu-id="98b74-193">4.8.0</span></span> |

## <a name="running-plugins-under-the-correct-runtime"></a><span data-ttu-id="98b74-194">Ausführen von Plug-ins unter der richtigen Laufzeit</span><span class="sxs-lookup"><span data-stu-id="98b74-194">Running plugins under the correct runtime</span></span>

<span data-ttu-id="98b74-195">Für nuget-Szenarien in dotnet. exe müssen Plug-ins unter dieser bestimmten Laufzeit von "dotnet. exe" ausgeführt werden können.</span><span class="sxs-lookup"><span data-stu-id="98b74-195">For the NuGet in dotnet.exe scenarios, plugins need to be able to execute under that specific runtime of the dotnet.exe.</span></span>
<span data-ttu-id="98b74-196">Er ist auf dem Plug-in-Anbieter und dem Consumer, um sicherzustellen, dass eine kompatible Kombination aus "dotnet. exe/Plugin" verwendet wird</span><span class="sxs-lookup"><span data-stu-id="98b74-196">It's on the plugin provider and the consumer to make sure a compatible dotnet.exe/plugin combination is used.</span></span>
<span data-ttu-id="98b74-197">Ein potenzielles Problem könnte bei den Benutzer-/Speicherort-Plug-ins auftreten, wenn beispielsweise eine dotnet. exe-Datei unter der 2,0-Laufzeit versucht, ein für die 2,1-Laufzeit geschriebenes Plug-in</span><span class="sxs-lookup"><span data-stu-id="98b74-197">A potential issue could arise with the user-location plugins when for example, a dotnet.exe under the 2.0 runtime tries to use a plugin written for the 2.1 runtime.</span></span>

## <a name="capabilities-caching"></a><span data-ttu-id="98b74-198">Zwischenspeichern von Funktionen</span><span class="sxs-lookup"><span data-stu-id="98b74-198">Capabilities caching</span></span>

<span data-ttu-id="98b74-199">Die Sicherheitsüberprüfung und-Instanziierung der Plug-ins ist aufwendig.</span><span class="sxs-lookup"><span data-stu-id="98b74-199">The security verification and instantiation of the plugins is costly.</span></span> <span data-ttu-id="98b74-200">Der Downloadvorgang erfolgt häufiger als der Authentifizierungs Vorgang, aber der durchschnittliche nuget-Benutzer hat wahrscheinlich nur ein Authentifizierungs-Plug-in.</span><span class="sxs-lookup"><span data-stu-id="98b74-200">The download operation happens way more frequently than the authentication operation, however the average NuGet user is only likely to have an authentication plugin.</span></span>
<span data-ttu-id="98b74-201">Um die Leistung zu verbessern, speichert nuget die Vorgangs Ansprüche für die angegebene Anforderung zwischen.</span><span class="sxs-lookup"><span data-stu-id="98b74-201">To improve the experience, NuGet will cache the operation claims for the given request.</span></span> <span data-ttu-id="98b74-202">Dieser Cache ist pro Plug-in, wobei der Plug-in-Pfad der Plug-in-Pfad ist, und der Ablauf für diesen Funktions Cache beträgt 30 Tage.</span><span class="sxs-lookup"><span data-stu-id="98b74-202">This cache is per plugin with the plugin key being the plugin path, and the expiration for this capabilities cache is 30 days.</span></span> 

<span data-ttu-id="98b74-203">Der Cache befindet sich in `%LocalAppData%/NuGet/plugins-cache` und ist mit der Umgebungsvariablen `NUGET_PLUGINS_CACHE_PATH`überschrieben.</span><span class="sxs-lookup"><span data-stu-id="98b74-203">The cache is located in `%LocalAppData%/NuGet/plugins-cache` and be overriden with the environment variable `NUGET_PLUGINS_CACHE_PATH`.</span></span> <span data-ttu-id="98b74-204">Zum Löschen dieses [Caches](../../consume-packages/managing-the-global-packages-and-cache-folders.md)können Sie den Befehl "Locals" mit der `plugins-cache` Option ausführen.</span><span class="sxs-lookup"><span data-stu-id="98b74-204">To clear this [cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md), one can run the locals command with the `plugins-cache` option.</span></span>
<span data-ttu-id="98b74-205">Die `all` Option "Locals" löscht nun auch den Plug-in-Cache.</span><span class="sxs-lookup"><span data-stu-id="98b74-205">The `all` locals option will now also delete the plugins cache.</span></span> 

## <a name="protocol-messages-index"></a><span data-ttu-id="98b74-206">Protokollnachrichten Index</span><span class="sxs-lookup"><span data-stu-id="98b74-206">Protocol messages index</span></span>

<span data-ttu-id="98b74-207">Protokoll Version *1.0.0* :</span><span class="sxs-lookup"><span data-stu-id="98b74-207">Protocol Version *1.0.0* messages:</span></span>

1.  <span data-ttu-id="98b74-208">Schließen</span><span class="sxs-lookup"><span data-stu-id="98b74-208">Close</span></span>
    * <span data-ttu-id="98b74-209">Anforderungs Richtung:  Nuget->-Plug-in</span><span class="sxs-lookup"><span data-stu-id="98b74-209">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="98b74-210">Die Anforderung enthält keine Nutzlast.</span><span class="sxs-lookup"><span data-stu-id="98b74-210">The request will contain no payload</span></span>
    * <span data-ttu-id="98b74-211">Es wird keine Antwort erwartet.</span><span class="sxs-lookup"><span data-stu-id="98b74-211">No response is expected.</span></span>  <span data-ttu-id="98b74-212">Die richtige Antwort besteht darin, dass der Plug-in-Prozess umgehend beendet wird.</span><span class="sxs-lookup"><span data-stu-id="98b74-212">The proper response is for the plugin process to promptly exit.</span></span>

2.  <span data-ttu-id="98b74-213">Dateien in Paket kopieren</span><span class="sxs-lookup"><span data-stu-id="98b74-213">Copy files in package</span></span>
    * <span data-ttu-id="98b74-214">Anforderungs Richtung:  Nuget->-Plug-in</span><span class="sxs-lookup"><span data-stu-id="98b74-214">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="98b74-215">Die Anforderung enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="98b74-215">The request will contain:</span></span>
        * <span data-ttu-id="98b74-216">die Paket-ID und die Version</span><span class="sxs-lookup"><span data-stu-id="98b74-216">the package ID and version</span></span>
        * <span data-ttu-id="98b74-217">Speicherort des Paket Quell Repository</span><span class="sxs-lookup"><span data-stu-id="98b74-217">the package source repository location</span></span>
        * <span data-ttu-id="98b74-218">Zielverzeichnis Pfad</span><span class="sxs-lookup"><span data-stu-id="98b74-218">destination directory path</span></span>
        * <span data-ttu-id="98b74-219">ein Aufzähl bares Element von Dateien im Paket, das in den Zielverzeichnis Pfad kopiert werden soll.</span><span class="sxs-lookup"><span data-stu-id="98b74-219">an enumerable of files in the package to be copied to the destination directory path</span></span>
    * <span data-ttu-id="98b74-220">Eine Antwort enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="98b74-220">A response will contain:</span></span>
        * <span data-ttu-id="98b74-221">ein Antwort Code, der das Ergebnis des Vorgangs angibt.</span><span class="sxs-lookup"><span data-stu-id="98b74-221">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="98b74-222">ein Aufzähl barer vollständiger Pfad für kopierte Dateien im Zielverzeichnis, wenn der Vorgang erfolgreich war.</span><span class="sxs-lookup"><span data-stu-id="98b74-222">an enumerable of full paths for copied files in the destination directory if the operation was successful</span></span>

3.  <span data-ttu-id="98b74-223">Paketdatei kopieren (nupkg-Datei)</span><span class="sxs-lookup"><span data-stu-id="98b74-223">Copy package file (.nupkg)</span></span>
    * <span data-ttu-id="98b74-224">Anforderungs Richtung:  Nuget->-Plug-in</span><span class="sxs-lookup"><span data-stu-id="98b74-224">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="98b74-225">Die Anforderung enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="98b74-225">The request will contain:</span></span>
        * <span data-ttu-id="98b74-226">die Paket-ID und die Version</span><span class="sxs-lookup"><span data-stu-id="98b74-226">the package ID and version</span></span>
        * <span data-ttu-id="98b74-227">Speicherort des Paket Quell Repository</span><span class="sxs-lookup"><span data-stu-id="98b74-227">the package source repository location</span></span>
        * <span data-ttu-id="98b74-228">der Ziel Datei Pfad.</span><span class="sxs-lookup"><span data-stu-id="98b74-228">the destination file path</span></span>
    * <span data-ttu-id="98b74-229">Eine Antwort enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="98b74-229">A response will contain:</span></span>
        * <span data-ttu-id="98b74-230">ein Antwort Code, der das Ergebnis des Vorgangs angibt.</span><span class="sxs-lookup"><span data-stu-id="98b74-230">a response code indicating the outcome of the operation</span></span>

4.  <span data-ttu-id="98b74-231">Anmelde Informationen erhalten</span><span class="sxs-lookup"><span data-stu-id="98b74-231">Get credentials</span></span>
    * <span data-ttu-id="98b74-232">Anforderungs Richtung: Plug-in > nuget</span><span class="sxs-lookup"><span data-stu-id="98b74-232">Request direction:  plugin -> NuGet</span></span>
    * <span data-ttu-id="98b74-233">Die Anforderung enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="98b74-233">The request will contain:</span></span>
        * <span data-ttu-id="98b74-234">Speicherort des Paket Quell Repository</span><span class="sxs-lookup"><span data-stu-id="98b74-234">the package source repository location</span></span>
        * <span data-ttu-id="98b74-235">der HTTP-Statuscode, der über die aktuellen Anmelde Informationen aus dem Paket Quellrepository abgerufen wurde</span><span class="sxs-lookup"><span data-stu-id="98b74-235">the HTTP status code obtained from the package source repository using current credentials</span></span>
    * <span data-ttu-id="98b74-236">Eine Antwort enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="98b74-236">A response will contain:</span></span>
        * <span data-ttu-id="98b74-237">ein Antwort Code, der das Ergebnis des Vorgangs angibt.</span><span class="sxs-lookup"><span data-stu-id="98b74-237">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="98b74-238">ein Benutzername, falls verfügbar</span><span class="sxs-lookup"><span data-stu-id="98b74-238">a username, if available</span></span>
        * <span data-ttu-id="98b74-239">ein Kennwort, falls verfügbar</span><span class="sxs-lookup"><span data-stu-id="98b74-239">a password, if available</span></span>

5.  <span data-ttu-id="98b74-240">Dateien im Paket erhalten</span><span class="sxs-lookup"><span data-stu-id="98b74-240">Get files in package</span></span>
    * <span data-ttu-id="98b74-241">Anforderungs Richtung:  Nuget->-Plug-in</span><span class="sxs-lookup"><span data-stu-id="98b74-241">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="98b74-242">Die Anforderung enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="98b74-242">The request will contain:</span></span>
        * <span data-ttu-id="98b74-243">die Paket-ID und die Version</span><span class="sxs-lookup"><span data-stu-id="98b74-243">the package ID and version</span></span>
        * <span data-ttu-id="98b74-244">Speicherort des Paket Quell Repository</span><span class="sxs-lookup"><span data-stu-id="98b74-244">the package source repository location</span></span>
    * <span data-ttu-id="98b74-245">Eine Antwort enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="98b74-245">A response will contain:</span></span>
        * <span data-ttu-id="98b74-246">ein Antwort Code, der das Ergebnis des Vorgangs angibt.</span><span class="sxs-lookup"><span data-stu-id="98b74-246">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="98b74-247">ein Aufzähl bares Element von Dateipfaden im Paket, wenn der Vorgang erfolgreich war.</span><span class="sxs-lookup"><span data-stu-id="98b74-247">an enumerable of file paths in the package if the operation was successful</span></span>

6.  <span data-ttu-id="98b74-248">Vorgangs Ansprüche abrufen</span><span class="sxs-lookup"><span data-stu-id="98b74-248">Get operation claims</span></span> 
    * <span data-ttu-id="98b74-249">Anforderungs Richtung:  Nuget->-Plug-in</span><span class="sxs-lookup"><span data-stu-id="98b74-249">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="98b74-250">Die Anforderung enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="98b74-250">The request will contain:</span></span>
        * <span data-ttu-id="98b74-251">der Dienst Index. JSON für eine Paketquelle</span><span class="sxs-lookup"><span data-stu-id="98b74-251">the service index.json for a package source</span></span>
        * <span data-ttu-id="98b74-252">Speicherort des Paket Quell Repository</span><span class="sxs-lookup"><span data-stu-id="98b74-252">the package source repository location</span></span>
    * <span data-ttu-id="98b74-253">Eine Antwort enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="98b74-253">A response will contain:</span></span>
        * <span data-ttu-id="98b74-254">ein Antwort Code, der das Ergebnis des Vorgangs angibt.</span><span class="sxs-lookup"><span data-stu-id="98b74-254">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="98b74-255">ein Aufzähl bares Element unterstützter Vorgänge (z. b. Paket Download), wenn der Vorgang erfolgreich war.</span><span class="sxs-lookup"><span data-stu-id="98b74-255">an enumerable of supported operations (e.g.:  package download) if the operation was successful.</span></span>  <span data-ttu-id="98b74-256">Wenn ein Plug-in die Paketquelle nicht unterstützt, muss das Plug-in eine leere Gruppe unterstützter Vorgänge zurückgeben.</span><span class="sxs-lookup"><span data-stu-id="98b74-256">If a plugin does not support the package source, the plugin must return an empty set of supported operations.</span></span>

> [!Note]
> <span data-ttu-id="98b74-257">Diese Meldung wurde in Version *2.0.0*aktualisiert.</span><span class="sxs-lookup"><span data-stu-id="98b74-257">This message has been updated in version *2.0.0*.</span></span> <span data-ttu-id="98b74-258">Sie befindet sich auf dem Client, um die Abwärtskompatibilität aufrechtzuerhalten.</span><span class="sxs-lookup"><span data-stu-id="98b74-258">It is on the client to preserve backward compatibility.</span></span>

7.  <span data-ttu-id="98b74-259">Pakethash erhalten</span><span class="sxs-lookup"><span data-stu-id="98b74-259">Get package hash</span></span>
    * <span data-ttu-id="98b74-260">Anforderungs Richtung:  Nuget->-Plug-in</span><span class="sxs-lookup"><span data-stu-id="98b74-260">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="98b74-261">Die Anforderung enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="98b74-261">The request will contain:</span></span>
        * <span data-ttu-id="98b74-262">die Paket-ID und die Version</span><span class="sxs-lookup"><span data-stu-id="98b74-262">the package ID and version</span></span>
        * <span data-ttu-id="98b74-263">Speicherort des Paket Quell Repository</span><span class="sxs-lookup"><span data-stu-id="98b74-263">the package source repository location</span></span>
        * <span data-ttu-id="98b74-264">der Hash Algorithmus</span><span class="sxs-lookup"><span data-stu-id="98b74-264">the hash algorithm</span></span>
    * <span data-ttu-id="98b74-265">Eine Antwort enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="98b74-265">A response will contain:</span></span>
        * <span data-ttu-id="98b74-266">ein Antwort Code, der das Ergebnis des Vorgangs angibt.</span><span class="sxs-lookup"><span data-stu-id="98b74-266">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="98b74-267">ein paketdateihash, der den angeforderten Hash Algorithmus verwendet, wenn der Vorgang erfolgreich war.</span><span class="sxs-lookup"><span data-stu-id="98b74-267">a package file hash using the requested hash algorithm if the operation was successful</span></span>

8.  <span data-ttu-id="98b74-268">Paketversionen erhalten</span><span class="sxs-lookup"><span data-stu-id="98b74-268">Get package versions</span></span>
    * <span data-ttu-id="98b74-269">Anforderungs Richtung:  Nuget->-Plug-in</span><span class="sxs-lookup"><span data-stu-id="98b74-269">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="98b74-270">Die Anforderung enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="98b74-270">The request will contain:</span></span>
        * <span data-ttu-id="98b74-271">die Paket-ID</span><span class="sxs-lookup"><span data-stu-id="98b74-271">the package ID</span></span>
        * <span data-ttu-id="98b74-272">Speicherort des Paket Quell Repository</span><span class="sxs-lookup"><span data-stu-id="98b74-272">the package source repository location</span></span>
    * <span data-ttu-id="98b74-273">Eine Antwort enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="98b74-273">A response will contain:</span></span>
        * <span data-ttu-id="98b74-274">ein Antwort Code, der das Ergebnis des Vorgangs angibt.</span><span class="sxs-lookup"><span data-stu-id="98b74-274">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="98b74-275">ein Aufzähl bares Element von Paketversionen, wenn der Vorgang erfolgreich war.</span><span class="sxs-lookup"><span data-stu-id="98b74-275">an enumerable of package versions if the operation was successful</span></span>

9.  <span data-ttu-id="98b74-276">Dienst Index erhalten</span><span class="sxs-lookup"><span data-stu-id="98b74-276">Get service index</span></span>
    * <span data-ttu-id="98b74-277">Anforderungs Richtung: Plug-in > nuget</span><span class="sxs-lookup"><span data-stu-id="98b74-277">Request direction:  plugin -> NuGet</span></span>
    * <span data-ttu-id="98b74-278">Die Anforderung enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="98b74-278">The request will contain:</span></span>
        * <span data-ttu-id="98b74-279">Speicherort des Paket Quell Repository</span><span class="sxs-lookup"><span data-stu-id="98b74-279">the package source repository location</span></span>
    * <span data-ttu-id="98b74-280">Eine Antwort enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="98b74-280">A response will contain:</span></span>
        * <span data-ttu-id="98b74-281">ein Antwort Code, der das Ergebnis des Vorgangs angibt.</span><span class="sxs-lookup"><span data-stu-id="98b74-281">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="98b74-282">der Dienst Index, wenn der Vorgang erfolgreich war.</span><span class="sxs-lookup"><span data-stu-id="98b74-282">the service index if the operation was successful</span></span>

10.  <span data-ttu-id="98b74-283">Shakes</span><span class="sxs-lookup"><span data-stu-id="98b74-283">Handshake</span></span>
     * <span data-ttu-id="98b74-284">Anforderungs Richtung:  Nuget-<->-Plug-in</span><span class="sxs-lookup"><span data-stu-id="98b74-284">Request direction:  NuGet <-> plugin</span></span>
     * <span data-ttu-id="98b74-285">Die Anforderung enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="98b74-285">The request will contain:</span></span>
         * <span data-ttu-id="98b74-286">die aktuelle Plug-in-Protokollversion</span><span class="sxs-lookup"><span data-stu-id="98b74-286">the current plugin protocol version</span></span>
         * <span data-ttu-id="98b74-287">die minimal unterstützte Plug-in-Protokollversion</span><span class="sxs-lookup"><span data-stu-id="98b74-287">the minimum supported plugin protocol version</span></span>
     * <span data-ttu-id="98b74-288">Eine Antwort enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="98b74-288">A response will contain:</span></span>
         * <span data-ttu-id="98b74-289">ein Antwort Code, der das Ergebnis des Vorgangs angibt.</span><span class="sxs-lookup"><span data-stu-id="98b74-289">a response code indicating the outcome of the operation</span></span>
         * <span data-ttu-id="98b74-290">die ausgehandelte Protokollversion, wenn der Vorgang erfolgreich war.</span><span class="sxs-lookup"><span data-stu-id="98b74-290">the negotiated protocol version if the operation was successful.</span></span>  <span data-ttu-id="98b74-291">Ein Fehler führt zu einer Beendigung des Plug-ins.</span><span class="sxs-lookup"><span data-stu-id="98b74-291">A failure will result in termination of the plugin.</span></span>

11.  <span data-ttu-id="98b74-292">Initialize</span><span class="sxs-lookup"><span data-stu-id="98b74-292">Initialize</span></span>
     * <span data-ttu-id="98b74-293">Anforderungs Richtung:  Nuget->-Plug-in</span><span class="sxs-lookup"><span data-stu-id="98b74-293">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="98b74-294">Die Anforderung enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="98b74-294">The request will contain:</span></span>
         * <span data-ttu-id="98b74-295">die Version des nuget-Client Tools</span><span class="sxs-lookup"><span data-stu-id="98b74-295">the NuGet client tool version</span></span>
         * <span data-ttu-id="98b74-296">die effektive Sprache des nuget-Client Tools.</span><span class="sxs-lookup"><span data-stu-id="98b74-296">the NuGet client tool effective language.</span></span>  <span data-ttu-id="98b74-297">Dabei wird ggf. die Einstellung "forceengloutput" berücksichtigt.</span><span class="sxs-lookup"><span data-stu-id="98b74-297">This takes into consideration the ForceEnglishOutput setting, if used.</span></span>
         * <span data-ttu-id="98b74-298">der standardmäßige Anforderungs Timeout, der den Standardwert des Protokolls ersetzt.</span><span class="sxs-lookup"><span data-stu-id="98b74-298">the default request timeout, which supersedes the protocol default.</span></span>
     * <span data-ttu-id="98b74-299">Eine Antwort enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="98b74-299">A response will contain:</span></span>
         * <span data-ttu-id="98b74-300">ein Antwort Code, der das Ergebnis des Vorgangs angibt.</span><span class="sxs-lookup"><span data-stu-id="98b74-300">a response code indicating the outcome of the operation.</span></span>  <span data-ttu-id="98b74-301">Ein Fehler führt zu einer Beendigung des Plug-ins.</span><span class="sxs-lookup"><span data-stu-id="98b74-301">A failure will result in termination of the plugin.</span></span>

12.  <span data-ttu-id="98b74-302">Protokoll</span><span class="sxs-lookup"><span data-stu-id="98b74-302">Log</span></span>
     * <span data-ttu-id="98b74-303">Anforderungs Richtung: Plug-in > nuget</span><span class="sxs-lookup"><span data-stu-id="98b74-303">Request direction:  plugin -> NuGet</span></span>
     * <span data-ttu-id="98b74-304">Die Anforderung enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="98b74-304">The request will contain:</span></span>
         * <span data-ttu-id="98b74-305">die Protokollebene für die Anforderung.</span><span class="sxs-lookup"><span data-stu-id="98b74-305">the log level for the request</span></span>
         * <span data-ttu-id="98b74-306">eine Meldung, die protokolliert werden soll</span><span class="sxs-lookup"><span data-stu-id="98b74-306">a message to log</span></span>
     * <span data-ttu-id="98b74-307">Eine Antwort enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="98b74-307">A response will contain:</span></span>
         * <span data-ttu-id="98b74-308">ein Antwort Code, der das Ergebnis des Vorgangs angibt.</span><span class="sxs-lookup"><span data-stu-id="98b74-308">a response code indicating the outcome of the operation.</span></span>

13.  <span data-ttu-id="98b74-309">Überwachen von nuget-Prozess beenden</span><span class="sxs-lookup"><span data-stu-id="98b74-309">Monitor NuGet process exit</span></span>
     * <span data-ttu-id="98b74-310">Anforderungs Richtung:  Nuget->-Plug-in</span><span class="sxs-lookup"><span data-stu-id="98b74-310">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="98b74-311">Die Anforderung enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="98b74-311">The request will contain:</span></span>
         * <span data-ttu-id="98b74-312">die nuget-Prozess-ID</span><span class="sxs-lookup"><span data-stu-id="98b74-312">the NuGet process ID</span></span>
     * <span data-ttu-id="98b74-313">Eine Antwort enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="98b74-313">A response will contain:</span></span>
         * <span data-ttu-id="98b74-314">ein Antwort Code, der das Ergebnis des Vorgangs angibt.</span><span class="sxs-lookup"><span data-stu-id="98b74-314">a response code indicating the outcome of the operation.</span></span>

14.  <span data-ttu-id="98b74-315">Paket vorab abrufen</span><span class="sxs-lookup"><span data-stu-id="98b74-315">Prefetch package</span></span>
     * <span data-ttu-id="98b74-316">Anforderungs Richtung:  Nuget->-Plug-in</span><span class="sxs-lookup"><span data-stu-id="98b74-316">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="98b74-317">Die Anforderung enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="98b74-317">The request will contain:</span></span>
         * <span data-ttu-id="98b74-318">die Paket-ID und die Version</span><span class="sxs-lookup"><span data-stu-id="98b74-318">the package ID and version</span></span>
         * <span data-ttu-id="98b74-319">Speicherort des Paket Quell Repository</span><span class="sxs-lookup"><span data-stu-id="98b74-319">the package source repository location</span></span>
     * <span data-ttu-id="98b74-320">Eine Antwort enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="98b74-320">A response will contain:</span></span>
         * <span data-ttu-id="98b74-321">ein Antwort Code, der das Ergebnis des Vorgangs angibt.</span><span class="sxs-lookup"><span data-stu-id="98b74-321">a response code indicating the outcome of the operation</span></span>

15.  <span data-ttu-id="98b74-322">Anmelde Informationen festlegen</span><span class="sxs-lookup"><span data-stu-id="98b74-322">Set credentials</span></span>
     * <span data-ttu-id="98b74-323">Anforderungs Richtung:  Nuget->-Plug-in</span><span class="sxs-lookup"><span data-stu-id="98b74-323">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="98b74-324">Die Anforderung enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="98b74-324">The request will contain:</span></span>
         * <span data-ttu-id="98b74-325">Speicherort des Paket Quell Repository</span><span class="sxs-lookup"><span data-stu-id="98b74-325">the package source repository location</span></span>
         * <span data-ttu-id="98b74-326">der letzte bekannte Paket Quell Benutzername, falls verfügbar</span><span class="sxs-lookup"><span data-stu-id="98b74-326">the last known package source username, if available</span></span>
         * <span data-ttu-id="98b74-327">das letzte bekannte Paket Quell Kennwort, falls verfügbar</span><span class="sxs-lookup"><span data-stu-id="98b74-327">the last known package source password, if available</span></span>
         * <span data-ttu-id="98b74-328">der letzte bekannte Proxy Benutzername, falls verfügbar</span><span class="sxs-lookup"><span data-stu-id="98b74-328">the last known proxy username, if available</span></span>
         * <span data-ttu-id="98b74-329">Letztes bekanntes Proxy Kennwort, falls verfügbar</span><span class="sxs-lookup"><span data-stu-id="98b74-329">the last known proxy password, if available</span></span>
     * <span data-ttu-id="98b74-330">Eine Antwort enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="98b74-330">A response will contain:</span></span>
         * <span data-ttu-id="98b74-331">ein Antwort Code, der das Ergebnis des Vorgangs angibt.</span><span class="sxs-lookup"><span data-stu-id="98b74-331">a response code indicating the outcome of the operation</span></span>

16.  <span data-ttu-id="98b74-332">Festlegen der Protokollebene</span><span class="sxs-lookup"><span data-stu-id="98b74-332">Set log level</span></span>
     * <span data-ttu-id="98b74-333">Anforderungs Richtung:  Nuget->-Plug-in</span><span class="sxs-lookup"><span data-stu-id="98b74-333">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="98b74-334">Die Anforderung enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="98b74-334">The request will contain:</span></span>
         * <span data-ttu-id="98b74-335">die Standardprotokoll Ebene</span><span class="sxs-lookup"><span data-stu-id="98b74-335">the default log level</span></span>
     * <span data-ttu-id="98b74-336">Eine Antwort enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="98b74-336">A response will contain:</span></span>
         * <span data-ttu-id="98b74-337">ein Antwort Code, der das Ergebnis des Vorgangs angibt.</span><span class="sxs-lookup"><span data-stu-id="98b74-337">a response code indicating the outcome of the operation</span></span>

<span data-ttu-id="98b74-338">Protokoll Version *2.0.0* -Nachrichten</span><span class="sxs-lookup"><span data-stu-id="98b74-338">Protocol Version *2.0.0* messages</span></span>

17. <span data-ttu-id="98b74-339">Vorgangs Ansprüche abrufen</span><span class="sxs-lookup"><span data-stu-id="98b74-339">Get Operation Claims</span></span>

* <span data-ttu-id="98b74-340">Anforderungs Richtung:  Nuget->-Plug-in</span><span class="sxs-lookup"><span data-stu-id="98b74-340">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="98b74-341">Die Anforderung enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="98b74-341">The request will contain:</span></span>
        * <span data-ttu-id="98b74-342">der Dienst Index. JSON für eine Paketquelle</span><span class="sxs-lookup"><span data-stu-id="98b74-342">the service index.json for a package source</span></span>
        * <span data-ttu-id="98b74-343">Speicherort des Paket Quell Repository</span><span class="sxs-lookup"><span data-stu-id="98b74-343">the package source repository location</span></span>
    * <span data-ttu-id="98b74-344">Eine Antwort enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="98b74-344">A response will contain:</span></span>
        * <span data-ttu-id="98b74-345">ein Antwort Code, der das Ergebnis des Vorgangs angibt.</span><span class="sxs-lookup"><span data-stu-id="98b74-345">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="98b74-346">eine Aufzähl Bare der unterstützten Vorgänge, wenn der Vorgang erfolgreich war.</span><span class="sxs-lookup"><span data-stu-id="98b74-346">an enumerable of supported operations if the operation was successful.</span></span>  <span data-ttu-id="98b74-347">Wenn ein Plug-in die Paketquelle nicht unterstützt, muss das Plug-in eine leere Gruppe unterstützter Vorgänge zurückgeben.</span><span class="sxs-lookup"><span data-stu-id="98b74-347">If a plugin does not support the package source, the plugin must return an empty set of supported operations.</span></span>

    <span data-ttu-id="98b74-348">Wenn der Dienst Index und die Paketquelle NULL sind, kann das Plug-in mit der Authentifizierung Antworten.</span><span class="sxs-lookup"><span data-stu-id="98b74-348">If the service index and package source are null, then the plugin can answer with authentication.</span></span>

18. <span data-ttu-id="98b74-349">Authentifizierungs Anmelde Informationen erhalten</span><span class="sxs-lookup"><span data-stu-id="98b74-349">Get Authentication Credentials</span></span>

* <span data-ttu-id="98b74-350">Anforderungs Richtung: Nuget->-Plug-in</span><span class="sxs-lookup"><span data-stu-id="98b74-350">Request direction: NuGet -> plugin</span></span>
* <span data-ttu-id="98b74-351">Die Anforderung enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="98b74-351">The request will contain:</span></span>
    * <span data-ttu-id="98b74-352">URI</span><span class="sxs-lookup"><span data-stu-id="98b74-352">Uri</span></span>
    * <span data-ttu-id="98b74-353">isretry</span><span class="sxs-lookup"><span data-stu-id="98b74-353">isRetry</span></span>
    * <span data-ttu-id="98b74-354">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="98b74-354">NonInteractive</span></span>
    * <span data-ttu-id="98b74-355">Canshowdialog</span><span class="sxs-lookup"><span data-stu-id="98b74-355">CanShowDialog</span></span>
* <span data-ttu-id="98b74-356">Eine Antwort enthält</span><span class="sxs-lookup"><span data-stu-id="98b74-356">A response will contain</span></span>
    * <span data-ttu-id="98b74-357">Benutzername</span><span class="sxs-lookup"><span data-stu-id="98b74-357">Username</span></span>
    * <span data-ttu-id="98b74-358">Kennwort</span><span class="sxs-lookup"><span data-stu-id="98b74-358">Password</span></span>
    * <span data-ttu-id="98b74-359">Meldung</span><span class="sxs-lookup"><span data-stu-id="98b74-359">Message</span></span>
    * <span data-ttu-id="98b74-360">Liste der Authentifizierungs Typen</span><span class="sxs-lookup"><span data-stu-id="98b74-360">List of Auth Types</span></span>
    * <span data-ttu-id="98b74-361">Messageresponsecode</span><span class="sxs-lookup"><span data-stu-id="98b74-361">MessageResponseCode</span></span>
