---
title: NuGet cross-Platform-Plug-Ins
description: NuGet cross Platform-Plug-Ins für NuGet.exe "," dotnet.exe "," msbuild.exe "und" Visual Studio
author: nkolev92
ms.author: nikolev
ms.date: 07/01/2018
ms.topic: conceptual
ms.openlocfilehash: fdefc5b6189051fd83b2de644080284c09dd85f4
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548205"
---
# <a name="nuget-cross-platform-plugins"></a><span data-ttu-id="dc503-103">NuGet cross-Platform-Plug-Ins</span><span class="sxs-lookup"><span data-stu-id="dc503-103">NuGet cross platform plugins</span></span>

<span data-ttu-id="dc503-104">In NuGet 4.8 und höher wurde Unterstützung für cross-Platform-Plug-Ins hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="dc503-104">In NuGet 4.8+ support for cross platform plugins has been added.</span></span>
<span data-ttu-id="dc503-105">Dies wurde mit erreicht, indem Sie erstellen ein neues-Plug-in-Erweiterbarkeitsmodell, die einem strikter Regeln des Vorgangs entsprechen.</span><span class="sxs-lookup"><span data-stu-id="dc503-105">This was achieved with by building a new plugin extensibility model, that has to conform to a strict set of rules of operation.</span></span>
<span data-ttu-id="dc503-106">Die Plug-Ins sind eigenständige ausführbare Dateien und (in der .NET Core-Welt Runnables), die die NuGet-Clients in einem separaten Prozess zu starten.</span><span class="sxs-lookup"><span data-stu-id="dc503-106">The plugins are self-contained executables (runnables in the .NET Core world), that the NuGet Clients launch in a separate process.</span></span>
<span data-ttu-id="dc503-107">Dies ist ein "true" Schreibvorgang einmal auszuführen weltweit-Plug-in.</span><span class="sxs-lookup"><span data-stu-id="dc503-107">This is a true write once, run everywhere plugin.</span></span> <span data-ttu-id="dc503-108">Es funktioniert mit allen NuGet-Clienttools.</span><span class="sxs-lookup"><span data-stu-id="dc503-108">It will work with all NuGet client tools.</span></span>
<span data-ttu-id="dc503-109">Die Plug-Ins kann entweder mit .NET Framework ("NuGet.exe", "MSBuild.exe" und "Visual Studio") oder .NET Core (dotnet.exe) sein.</span><span class="sxs-lookup"><span data-stu-id="dc503-109">The plugins can be either .NET Framework (NuGet.exe, MSBuild.exe and Visual Studio), or .NET Core (dotnet.exe).</span></span>
<span data-ttu-id="dc503-110">Es wird ein mit versionsverwaltung durch das Kommunikationsprotokoll zwischen dem NuGet-Client und das Plug-in definiert.</span><span class="sxs-lookup"><span data-stu-id="dc503-110">A versioned communication protocol between the NuGet Client and the plugin is defined.</span></span> <span data-ttu-id="dc503-111">Während des Handshakes beim Start aushandeln 2 Prozesse die Protokollversion an.</span><span class="sxs-lookup"><span data-stu-id="dc503-111">During the startup handshake, the 2 processes negotiate the protocol version.</span></span>

<span data-ttu-id="dc503-112">Um alle NuGet Client Tools-Szenarien abzudecken, würde eine ein .NET Framework und eine .NET Core-Plug-in benötigen.</span><span class="sxs-lookup"><span data-stu-id="dc503-112">In order to cover all NuGet client tools scenarios, one would need both a .NET Framework and a .NET Core plugin.</span></span>
<span data-ttu-id="dc503-113">Die im folgenden wird beschrieben, die Client/Framework-Kombinationen der Plug-Ins.</span><span class="sxs-lookup"><span data-stu-id="dc503-113">The below describes the client/framework combinations of the plugins.</span></span>

| <span data-ttu-id="dc503-114">Client-Tool</span><span class="sxs-lookup"><span data-stu-id="dc503-114">Client tool</span></span>  | <span data-ttu-id="dc503-115">Framework</span><span class="sxs-lookup"><span data-stu-id="dc503-115">Framework</span></span> |
| ------------ | --------- |
| <span data-ttu-id="dc503-116">Visual Studio</span><span class="sxs-lookup"><span data-stu-id="dc503-116">Visual Studio</span></span> | <span data-ttu-id="dc503-117">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="dc503-117">.NET Framework</span></span> |
| <span data-ttu-id="dc503-118">dotnet.exe</span><span class="sxs-lookup"><span data-stu-id="dc503-118">dotnet.exe</span></span> | <span data-ttu-id="dc503-119">.NET Core</span><span class="sxs-lookup"><span data-stu-id="dc503-119">.NET Core</span></span> |
| <span data-ttu-id="dc503-120">NuGet.exe</span><span class="sxs-lookup"><span data-stu-id="dc503-120">NuGet.exe</span></span> | <span data-ttu-id="dc503-121">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="dc503-121">.NET Framework</span></span> |
| <span data-ttu-id="dc503-122">MSBuild.exe</span><span class="sxs-lookup"><span data-stu-id="dc503-122">MSBuild.exe</span></span> | <span data-ttu-id="dc503-123">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="dc503-123">.NET Framework</span></span> |
| <span data-ttu-id="dc503-124">NuGet.exe auf Mono</span><span class="sxs-lookup"><span data-stu-id="dc503-124">NuGet.exe on Mono</span></span> | <span data-ttu-id="dc503-125">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="dc503-125">.NET Framework</span></span> |

## <a name="how-does-it-work"></a><span data-ttu-id="dc503-126">Wie funktioniert es</span><span class="sxs-lookup"><span data-stu-id="dc503-126">How does it work</span></span>

<span data-ttu-id="dc503-127">Der allgemeine Workflow kann wie folgt beschrieben werden:</span><span class="sxs-lookup"><span data-stu-id="dc503-127">The high level workflow can be described as follows:</span></span>

1. <span data-ttu-id="dc503-128">NuGet erkennt verfügbaren Plug-Ins.</span><span class="sxs-lookup"><span data-stu-id="dc503-128">NuGet discovers available plugins.</span></span>
1. <span data-ttu-id="dc503-129">Gegebenenfalls wird NuGet die Plug-Ins in der Reihenfolge ihrer Priorität und startet Sie einzeln durchlaufen werden.</span><span class="sxs-lookup"><span data-stu-id="dc503-129">When applicable, NuGet will iterate over the plugins in priority order and starts them one by one.</span></span>
1. <span data-ttu-id="dc503-130">NuGet wird das erste Plug-in verwenden, das die Anforderung bedienen kann.</span><span class="sxs-lookup"><span data-stu-id="dc503-130">NuGet will use the first plugin that can service the request.</span></span>
1. <span data-ttu-id="dc503-131">Die Plug-Ins wird heruntergefahren wenn sie nicht mehr benötigt werden.</span><span class="sxs-lookup"><span data-stu-id="dc503-131">The plugins will be shut down when they are no longer needed.</span></span>

## <a name="general-plugin-requirements"></a><span data-ttu-id="dc503-132">Allgemeine-Plug-in-Anforderungen</span><span class="sxs-lookup"><span data-stu-id="dc503-132">General plugin requirements</span></span>

<span data-ttu-id="dc503-133">Die aktuelle Protokollversion ist *2.0.0*.</span><span class="sxs-lookup"><span data-stu-id="dc503-133">The current protocol version is *2.0.0*.</span></span>
<span data-ttu-id="dc503-134">In dieser Version sind wie folgt:</span><span class="sxs-lookup"><span data-stu-id="dc503-134">Under this version, the requirements are as follows:</span></span>

- <span data-ttu-id="dc503-135">Haben Sie einen gültigen und vertrauenswürdigen Authenticode-Signatur Assemblys, die auf Windows und Mono ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="dc503-135">Have a valid, trusted Authenticode signature assemblies that will run on Windows and Mono.</span></span> <span data-ttu-id="dc503-136">Es ist keine besondere Vertrauensstellung erforderlich für Assemblys, die noch unter Linux und Mac ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="dc503-136">There is no special trust requirement for assemblies run on Linux and Mac yet.</span></span> [<span data-ttu-id="dc503-137">Relevante Problem</span><span class="sxs-lookup"><span data-stu-id="dc503-137">Relevant issue</span></span>](https://github.com/NuGet/Home/issues/6702)
- <span data-ttu-id="dc503-138">Unterstützung von zustandslosen starten im aktuellen Sicherheitskontext der NuGet-Clienttools.</span><span class="sxs-lookup"><span data-stu-id="dc503-138">Support stateless launching under the current security context of NuGet client tools.</span></span> <span data-ttu-id="dc503-139">NuGet-Clienttools führt beispielsweise keine Erhöhung der Rechte oder zusätzliche Initialisierung außerhalb des-Plug-in-Protokolls, die weiter unten beschrieben.</span><span class="sxs-lookup"><span data-stu-id="dc503-139">For example, NuGet client tools will not perform elevation or additional initialization outside of the plugin protocol described later.</span></span>
- <span data-ttu-id="dc503-140">Sofern nicht ausdrücklich angegeben, wird nicht interaktiv sein.</span><span class="sxs-lookup"><span data-stu-id="dc503-140">Be non interactive, unless explicitly specified.</span></span>
- <span data-ttu-id="dc503-141">Das ausgehandelte-Plug-Ins Protokoll, Version entsprechen.</span><span class="sxs-lookup"><span data-stu-id="dc503-141">Adhere to the negotiated plugin protocol version.</span></span>
- <span data-ttu-id="dc503-142">Für alle Anforderungen innerhalb eines angemessenen Zeitraums zu reagieren.</span><span class="sxs-lookup"><span data-stu-id="dc503-142">Respond to all requests within a reasonable time period.</span></span>
- <span data-ttu-id="dc503-143">Berücksichtigen Sie abbruchanforderungen für jeden Vorgang in Bearbeitung.</span><span class="sxs-lookup"><span data-stu-id="dc503-143">Honor cancellation requests for any in-progress operation.</span></span>

<span data-ttu-id="dc503-144">Die technische Spezifikation wird in der folgenden Spezifikationen ausführlicher beschrieben:</span><span class="sxs-lookup"><span data-stu-id="dc503-144">The technical specification is described in more detail in the following specs:</span></span>

- [<span data-ttu-id="dc503-145">NuGet-Paket herunterladen-Plug-in</span><span class="sxs-lookup"><span data-stu-id="dc503-145">NuGet Package Download Plugin</span></span>](https://github.com/NuGet/Home/wiki/NuGet-Package-Download-Plugin)
- [<span data-ttu-id="dc503-146">NuGet cross-Plat-Authentifizierung-Plug-in</span><span class="sxs-lookup"><span data-stu-id="dc503-146">NuGet cross plat authentication plugin</span></span>](https://github.com/NuGet/Home/wiki/NuGet-cross-plat-authentication-plugin)

## <a name="client---plugin-interaction"></a><span data-ttu-id="dc503-147">Client --Plug-in-Interaktion</span><span class="sxs-lookup"><span data-stu-id="dc503-147">Client - Plugin interaction</span></span>

<span data-ttu-id="dc503-148">NuGet-Clienttools und die Plug-Ins kommunizieren mit JSON-Code über standard-Streams (Stdin, Stdout, Stderr).</span><span class="sxs-lookup"><span data-stu-id="dc503-148">NuGet client tools and the plugins communicate with JSON over standard streams (stdin, stdout, stderr).</span></span> <span data-ttu-id="dc503-149">Alle Daten müssen UTF-8 codiert sein.</span><span class="sxs-lookup"><span data-stu-id="dc503-149">All data must be UTF-8 encoded.</span></span>
<span data-ttu-id="dc503-150">Die Plug-Ins werden gestartet, mit dem Argument "--Plug-in".</span><span class="sxs-lookup"><span data-stu-id="dc503-150">The plugins are launched with the argument "-Plugin".</span></span> <span data-ttu-id="dc503-151">Für den Fall, dass ein Benutzer direkt ein ausführbare Datei ohne dieses Argument-Plug-in startet, kann das Plug-in eine informative Meldung, anstatt abzuwarten, bis eine Protokoll-Handshakes geben.</span><span class="sxs-lookup"><span data-stu-id="dc503-151">In case a user directly launches a plugin executable without this argument, the plugin can give an informative message instead of waiting for a protocol handshake.</span></span>
<span data-ttu-id="dc503-152">Das Protokoll-Handshakes-Timeout beträgt 5 Sekunden.</span><span class="sxs-lookup"><span data-stu-id="dc503-152">The protocol handshake timeout is 5 seconds.</span></span> <span data-ttu-id="dc503-153">Das Plug-in sollte die Einrichtung in als, kleiner als eine Menge wie möglich abgeschlossen werden.</span><span class="sxs-lookup"><span data-stu-id="dc503-153">The plugin should complete the setup in as short of an amount as possible.</span></span>
<span data-ttu-id="dc503-154">NuGet-Clienttools werden unterstützten ein Plug-in-Vorgänge durch die Übergabe dienstindex für ein NuGet-Quelle abgefragt werden.</span><span class="sxs-lookup"><span data-stu-id="dc503-154">NuGet client tools will query a plugin’s supported operations by passing in the service index for a NuGet source.</span></span> <span data-ttu-id="dc503-155">Ein Plug-in kann den dienstindex verwenden, um auf das Vorhandensein der unterstützten Diensttypen überprüfen zu können.</span><span class="sxs-lookup"><span data-stu-id="dc503-155">A plugin may use the service index to check for the presence of supported service types.</span></span>

<span data-ttu-id="dc503-156">Die Kommunikation zwischen den NuGet-Clienttools und das Plug-in ist bidirektional.</span><span class="sxs-lookup"><span data-stu-id="dc503-156">The communication between the NuGet client tools and the plugin is bidirectional.</span></span> <span data-ttu-id="dc503-157">Jede Anforderung hat ein Timeout von fünf Sekunden.</span><span class="sxs-lookup"><span data-stu-id="dc503-157">Each request has a timeout of 5 seconds.</span></span> <span data-ttu-id="dc503-158">Wenn Vorgänge sollten länger dauern sollte eine Statusmeldung, um zu verhindern, dass die Anforderung ein Timeout eingetreten der entsprechende Prozess gesendet. Nach einer Minute Inaktivität ein Plug-in als inaktiv betrachtet und wird heruntergefahren.</span><span class="sxs-lookup"><span data-stu-id="dc503-158">If operations are supposed to take longer the respective process should send out a progress message to prevent the request from timing out. After 1 minute of inactivity a plugin is considered idle and is shut down.</span></span>

## <a name="plugin-installation-and-discovery"></a><span data-ttu-id="dc503-159">Plug-in-Installation und Ermittlung</span><span class="sxs-lookup"><span data-stu-id="dc503-159">Plugin installation and discovery</span></span>

<span data-ttu-id="dc503-160">Die Plug-Ins werden über eine Verzeichnisstruktur konventionsbasierten ermittelt.</span><span class="sxs-lookup"><span data-stu-id="dc503-160">The plugins will be discovered via a convention based directory structure.</span></span>
<span data-ttu-id="dc503-161">CI/CD-Szenarien und erfahrene Benutzer können eine Umgebungsvariable, das Verhalten.</span><span class="sxs-lookup"><span data-stu-id="dc503-161">CI/CD scenarios and power users can use an environment variable to override the behavior.</span></span>

- <span data-ttu-id="dc503-162">`NUGET_PLUGIN_PATHS` : definiert die Plug-Ins, die für diesen Prozess für NuGet, Priorität, die reserviert verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="dc503-162">`NUGET_PLUGIN_PATHS` - defines the plugins that will be used for that NuGet process, priority reserved.</span></span> <span data-ttu-id="dc503-163">Wenn diese Umgebungsvariable festgelegt ist, wird die Ermittlung des konventionsbasierten überschrieben.</span><span class="sxs-lookup"><span data-stu-id="dc503-163">If this environment variable is set, it overrides the convention based discovery.</span></span>
-  <span data-ttu-id="dc503-164">Benutzer-Speicherort, den Speicherort der NuGet-Startseite in `%UserProfile%/.nuget/plugins`.</span><span class="sxs-lookup"><span data-stu-id="dc503-164">User-location, the NuGet Home location in `%UserProfile%/.nuget/plugins`.</span></span> <span data-ttu-id="dc503-165">Dieser Speicherort kann nicht überschrieben werden.</span><span class="sxs-lookup"><span data-stu-id="dc503-165">This location cannot be overriden.</span></span> <span data-ttu-id="dc503-166">Ein Stammverzeichnis für die verschiedenen wird für .NET Core und .NET Framework-Plug-Ins verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="dc503-166">A different root directory will be used for .NET Core and .NET Framework plugins.</span></span>

| <span data-ttu-id="dc503-167">Framework</span><span class="sxs-lookup"><span data-stu-id="dc503-167">Framework</span></span> | <span data-ttu-id="dc503-168">Stammverzeichnis für die Ermittlung</span><span class="sxs-lookup"><span data-stu-id="dc503-168">Root discovery location</span></span>  |
| ------- | ------------------------ |
| <span data-ttu-id="dc503-169">.NET Core</span><span class="sxs-lookup"><span data-stu-id="dc503-169">.NET Core</span></span> |  `%UserProfile%/.nuget/plugins/netcore` |
| <span data-ttu-id="dc503-170">.NET Framework</span><span class="sxs-lookup"><span data-stu-id="dc503-170">.NET Framework</span></span> | `%UserProfile%/.nuget/plugins/netfx` |

<span data-ttu-id="dc503-171">Jede-Plug-in sollte in einem eigenen Ordner installiert werden.</span><span class="sxs-lookup"><span data-stu-id="dc503-171">Each plugin should be installed in its own folder.</span></span>
<span data-ttu-id="dc503-172">Der Einstiegspunkt-Plug-in werden der Name des installierten-Ordner, mit der DLL-Erweiterungen für .NET Core und ".exe"-Erweiterung für .NET Framework.</span><span class="sxs-lookup"><span data-stu-id="dc503-172">The plugin entry point will be the name of the installed folder, with the .dll extensions for .NET Core, and .exe extension for .NET Framework.</span></span>

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
> <span data-ttu-id="dc503-173">Es gibt derzeit keine User Storys für die Installation des Plug-Ins.</span><span class="sxs-lookup"><span data-stu-id="dc503-173">There is currently no user story for the installation of the plugins.</span></span> <span data-ttu-id="dc503-174">Es ist so einfach wie die erforderlichen Dateien in den zuvor festgelegten Speicherort verschieben.</span><span class="sxs-lookup"><span data-stu-id="dc503-174">It's as simple as moving the required files into the predetermined location.</span></span>

## <a name="supported-operations"></a><span data-ttu-id="dc503-175">Unterstützte Vorgänge</span><span class="sxs-lookup"><span data-stu-id="dc503-175">Supported operations</span></span>

<span data-ttu-id="dc503-176">Zwei Vorgänge werden in das neue Plug-in-Protokoll unterstützt.</span><span class="sxs-lookup"><span data-stu-id="dc503-176">Two operations are supported under the new plugin protocol.</span></span>

| <span data-ttu-id="dc503-177">Vorgangsname</span><span class="sxs-lookup"><span data-stu-id="dc503-177">Operation name</span></span> | <span data-ttu-id="dc503-178">Mindestprotokollversion</span><span class="sxs-lookup"><span data-stu-id="dc503-178">Minimum protocol version</span></span> | <span data-ttu-id="dc503-179">Mindestversion für NuGet-client</span><span class="sxs-lookup"><span data-stu-id="dc503-179">Minimum NuGet client version</span></span> |
| -------------- | ----------------------- | --------------------- |
| <span data-ttu-id="dc503-180">Paket herunterladen</span><span class="sxs-lookup"><span data-stu-id="dc503-180">Download Package</span></span> | <span data-ttu-id="dc503-181">1.0.0</span><span class="sxs-lookup"><span data-stu-id="dc503-181">1.0.0</span></span> | <span data-ttu-id="dc503-182">4.3.0</span><span class="sxs-lookup"><span data-stu-id="dc503-182">4.3.0</span></span> |
| [<span data-ttu-id="dc503-183">Authentifizierung</span><span class="sxs-lookup"><span data-stu-id="dc503-183">Authentication</span></span>](NuGet-Cross-Platform-Authentication-Plugin.md) | <span data-ttu-id="dc503-184">2.0.0</span><span class="sxs-lookup"><span data-stu-id="dc503-184">2.0.0</span></span> | <span data-ttu-id="dc503-185">4.8.0</span><span class="sxs-lookup"><span data-stu-id="dc503-185">4.8.0</span></span> |

## <a name="running-plugins-under-the-correct-runtime"></a><span data-ttu-id="dc503-186">Ausführen unter die richtige Runtime-Plug-Ins</span><span class="sxs-lookup"><span data-stu-id="dc503-186">Running plugins under the correct runtime</span></span>

<span data-ttu-id="dc503-187">Für die NuGet in dotnet.exe-Szenarien müssen-Plug-Ins unter dieser bestimmten Laufzeit von der dotnet.exe ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="dc503-187">For the NuGet in dotnet.exe scenarios, plugins need to be able to execute under that specific runtime of the dotnet.exe.</span></span>
<span data-ttu-id="dc503-188">Es ist der Anbieter-Plug-Ins und Consumer, um sicherzustellen, dass eine kompatible dotnet.exe/plugin-Kombination verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="dc503-188">It's on the plugin provider and the consumer to make sure a compatible dotnet.exe/plugin combination is used.</span></span>
<span data-ttu-id="dc503-189">Ein mögliches Problem kann auftreten, mit dem Benutzerstandort Plug-Ins bei z. B., eine dotnet.exe unter der 2.0-Runtime versucht, eine-Plug-Ins für die 2.1-Runtime geschrieben wurden.</span><span class="sxs-lookup"><span data-stu-id="dc503-189">A potential issue could arise with the user-location plugins when for example, a dotnet.exe under the 2.0 runtime tries to use a plugin written for the 2.1 runtime.</span></span>

## <a name="capabilities-caching"></a><span data-ttu-id="dc503-190">Funktionen, die Zwischenspeicherung</span><span class="sxs-lookup"><span data-stu-id="dc503-190">Capabilities caching</span></span>

<span data-ttu-id="dc503-191">Die sicherheitsüberprüfung und -Instanziierung der Plug-Ins ist teuer.</span><span class="sxs-lookup"><span data-stu-id="dc503-191">The security verification and instantiation of the plugins is costly.</span></span> <span data-ttu-id="dc503-192">Der Downloadvorgang geschieht viel häufiger auf als den Authentifizierungsvorgang, jedoch ist der durchschnittliche Benutzer von NuGet nur wahrscheinlich eine Authentifizierung-Plug-in.</span><span class="sxs-lookup"><span data-stu-id="dc503-192">The download operation happens way more frequently than the authentication operation, however the average NuGet user is only likely to have an authentication plugin.</span></span>
<span data-ttu-id="dc503-193">Um die benutzerfreundlichkeit zu verbessern, speichert NuGet die Vorgang-Ansprüche für die angegebene Anforderung.</span><span class="sxs-lookup"><span data-stu-id="dc503-193">To improve the experience, NuGet will cache the operation claims for the given request.</span></span> <span data-ttu-id="dc503-194">Dieser Cache wird pro-Plug-in, mit dem-Plug-in-Schlüssel wird der Pfad-Plug-in, und das Ablaufdatum für diesen Cache Funktionen beträgt 30 Tage.</span><span class="sxs-lookup"><span data-stu-id="dc503-194">This cache is per plugin with the plugin key being the plugin path, and the expiration for this capabilities cache is 30 days.</span></span> 

<span data-ttu-id="dc503-195">Der Cache befindet sich im `%LocalAppData%/NuGet/plugins-cache` und werden zusammen mit der Umgebungsvariable `NUGET_PLUGINS_CACHE_PATH`.</span><span class="sxs-lookup"><span data-stu-id="dc503-195">The cache is located in `%LocalAppData%/NuGet/plugins-cache` and be overriden with the environment variable `NUGET_PLUGINS_CACHE_PATH`.</span></span> <span data-ttu-id="dc503-196">Um dies zu löschen [Cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md), möglich, die lokal auszuführen-Befehl mit der `plugins-cache` Option.</span><span class="sxs-lookup"><span data-stu-id="dc503-196">To clear this [cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md), one can run the locals command with the `plugins-cache` option.</span></span>
<span data-ttu-id="dc503-197">Die `all` "lokal"-Option wird auch den Cache-Plug-Ins gelöscht.</span><span class="sxs-lookup"><span data-stu-id="dc503-197">The `all` locals option will now also delete the plugins cache.</span></span> 

## <a name="protocol-messages-index"></a><span data-ttu-id="dc503-198">Index der Protokoll-Nachrichten</span><span class="sxs-lookup"><span data-stu-id="dc503-198">Protocol messages index</span></span>

<span data-ttu-id="dc503-199">Protokollversion *1.0.0* Nachrichten:</span><span class="sxs-lookup"><span data-stu-id="dc503-199">Protocol Version *1.0.0* messages:</span></span>

1.  <span data-ttu-id="dc503-200">Schließen</span><span class="sxs-lookup"><span data-stu-id="dc503-200">Close</span></span>
    * <span data-ttu-id="dc503-201">Anfordern der Richtung: NuGet ->-Plug-in</span><span class="sxs-lookup"><span data-stu-id="dc503-201">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="dc503-202">Die Anforderung wird keine Nutzlast enthalten.</span><span class="sxs-lookup"><span data-stu-id="dc503-202">The request will contain no payload</span></span>
    * <span data-ttu-id="dc503-203">Es wird keine Antwort erwartet.</span><span class="sxs-lookup"><span data-stu-id="dc503-203">No response is expected.</span></span>  <span data-ttu-id="dc503-204">Die richtige Antwort ist für den Prozess-Plug-in, um sofort zu beenden.</span><span class="sxs-lookup"><span data-stu-id="dc503-204">The proper response is for the plugin process to promptly exit.</span></span>

2.  <span data-ttu-id="dc503-205">Kopieren von Dateien im Paket</span><span class="sxs-lookup"><span data-stu-id="dc503-205">Copy files in package</span></span>
    * <span data-ttu-id="dc503-206">Anfordern der Richtung: NuGet ->-Plug-in</span><span class="sxs-lookup"><span data-stu-id="dc503-206">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="dc503-207">Die Anforderung enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="dc503-207">The request will contain:</span></span>
        * <span data-ttu-id="dc503-208">der Paket-ID und version</span><span class="sxs-lookup"><span data-stu-id="dc503-208">the package ID and version</span></span>
        * <span data-ttu-id="dc503-209">Speicherort für die Paketquelle repository</span><span class="sxs-lookup"><span data-stu-id="dc503-209">the package source repository location</span></span>
        * <span data-ttu-id="dc503-210">Zielverzeichnispfad</span><span class="sxs-lookup"><span data-stu-id="dc503-210">destination directory path</span></span>
        * <span data-ttu-id="dc503-211">ein aufzählbares Objekt von Dateien im Paket in den Zielverzeichnispfad kopiert werden sollen</span><span class="sxs-lookup"><span data-stu-id="dc503-211">an enumerable of files in the package to be copied to the destination directory path</span></span>
    * <span data-ttu-id="dc503-212">Eine Antwort enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="dc503-212">A response will contain:</span></span>
        * <span data-ttu-id="dc503-213">Antwortcode, der angibt, des Ergebnis des Vorgangs</span><span class="sxs-lookup"><span data-stu-id="dc503-213">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="dc503-214">ein aufzählbares Objekt von vollständigen Pfade für die kopierten Dateien in das Zielverzeichnis, wenn der Vorgang erfolgreich war</span><span class="sxs-lookup"><span data-stu-id="dc503-214">an enumerable of full paths for copied files in the destination directory if the operation was successful</span></span>

3.  <span data-ttu-id="dc503-215">Kopieren Sie die Paketdatei (NUPKG-Datei)</span><span class="sxs-lookup"><span data-stu-id="dc503-215">Copy package file (.nupkg)</span></span>
    * <span data-ttu-id="dc503-216">Anfordern der Richtung: NuGet ->-Plug-in</span><span class="sxs-lookup"><span data-stu-id="dc503-216">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="dc503-217">Die Anforderung enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="dc503-217">The request will contain:</span></span>
        * <span data-ttu-id="dc503-218">der Paket-ID und version</span><span class="sxs-lookup"><span data-stu-id="dc503-218">the package ID and version</span></span>
        * <span data-ttu-id="dc503-219">Speicherort für die Paketquelle repository</span><span class="sxs-lookup"><span data-stu-id="dc503-219">the package source repository location</span></span>
        * <span data-ttu-id="dc503-220">der Zieldateipfad</span><span class="sxs-lookup"><span data-stu-id="dc503-220">the destination file path</span></span>
    * <span data-ttu-id="dc503-221">Eine Antwort enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="dc503-221">A response will contain:</span></span>
        * <span data-ttu-id="dc503-222">Antwortcode, der angibt, des Ergebnis des Vorgangs</span><span class="sxs-lookup"><span data-stu-id="dc503-222">a response code indicating the outcome of the operation</span></span>

4.  <span data-ttu-id="dc503-223">Abrufen von Anmeldeinformationen</span><span class="sxs-lookup"><span data-stu-id="dc503-223">Get credentials</span></span>
    * <span data-ttu-id="dc503-224">Anfordern der Richtung: NuGet-Plug-in -></span><span class="sxs-lookup"><span data-stu-id="dc503-224">Request direction:  plugin -> NuGet</span></span>
    * <span data-ttu-id="dc503-225">Die Anforderung enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="dc503-225">The request will contain:</span></span>
        * <span data-ttu-id="dc503-226">Speicherort für die Paketquelle repository</span><span class="sxs-lookup"><span data-stu-id="dc503-226">the package source repository location</span></span>
        * <span data-ttu-id="dc503-227">die HTTP-Statuscode, der vom Paket Quell-Repository mit aktuellen Anmeldeinformationen abgerufen</span><span class="sxs-lookup"><span data-stu-id="dc503-227">the HTTP status code obtained from the package source repository using current credentials</span></span>
    * <span data-ttu-id="dc503-228">Eine Antwort enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="dc503-228">A response will contain:</span></span>
        * <span data-ttu-id="dc503-229">Antwortcode, der angibt, des Ergebnis des Vorgangs</span><span class="sxs-lookup"><span data-stu-id="dc503-229">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="dc503-230">ein Benutzername, sofern verfügbar</span><span class="sxs-lookup"><span data-stu-id="dc503-230">a username, if available</span></span>
        * <span data-ttu-id="dc503-231">ein Kennwort, falls verfügbar</span><span class="sxs-lookup"><span data-stu-id="dc503-231">a password, if available</span></span>

5.  <span data-ttu-id="dc503-232">Abrufen von Dateien im Paket</span><span class="sxs-lookup"><span data-stu-id="dc503-232">Get files in package</span></span>
    * <span data-ttu-id="dc503-233">Anfordern der Richtung: NuGet ->-Plug-in</span><span class="sxs-lookup"><span data-stu-id="dc503-233">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="dc503-234">Die Anforderung enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="dc503-234">The request will contain:</span></span>
        * <span data-ttu-id="dc503-235">der Paket-ID und version</span><span class="sxs-lookup"><span data-stu-id="dc503-235">the package ID and version</span></span>
        * <span data-ttu-id="dc503-236">Speicherort für die Paketquelle repository</span><span class="sxs-lookup"><span data-stu-id="dc503-236">the package source repository location</span></span>
    * <span data-ttu-id="dc503-237">Eine Antwort enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="dc503-237">A response will contain:</span></span>
        * <span data-ttu-id="dc503-238">Antwortcode, der angibt, des Ergebnis des Vorgangs</span><span class="sxs-lookup"><span data-stu-id="dc503-238">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="dc503-239">ein aufzählbares Objekt von Dateipfaden in das Paket aus, wenn der Vorgang erfolgreich war</span><span class="sxs-lookup"><span data-stu-id="dc503-239">an enumerable of file paths in the package if the operation was successful</span></span>

6.  <span data-ttu-id="dc503-240">Abrufen von Vorgang Ansprüche</span><span class="sxs-lookup"><span data-stu-id="dc503-240">Get operation claims</span></span> 
    * <span data-ttu-id="dc503-241">Anfordern der Richtung: NuGet ->-Plug-in</span><span class="sxs-lookup"><span data-stu-id="dc503-241">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="dc503-242">Die Anforderung enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="dc503-242">The request will contain:</span></span>
        * <span data-ttu-id="dc503-243">der Dienst index.json für eine Paketquelle</span><span class="sxs-lookup"><span data-stu-id="dc503-243">the service index.json for a package source</span></span>
        * <span data-ttu-id="dc503-244">Speicherort für die Paketquelle repository</span><span class="sxs-lookup"><span data-stu-id="dc503-244">the package source repository location</span></span>
    * <span data-ttu-id="dc503-245">Eine Antwort enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="dc503-245">A response will contain:</span></span>
        * <span data-ttu-id="dc503-246">Antwortcode, der angibt, des Ergebnis des Vorgangs</span><span class="sxs-lookup"><span data-stu-id="dc503-246">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="dc503-247">ein aufzählbares Objekt von unterstützten Vorgänge (z. B.: Paketdownload), wenn der Vorgang erfolgreich war.</span><span class="sxs-lookup"><span data-stu-id="dc503-247">an enumerable of supported operations (e.g.:  package download) if the operation was successful.</span></span>  <span data-ttu-id="dc503-248">Wenn Sie ein Plug-in die Paketquelle nicht unterstützt, muss die-Plug-in einen leeren Satz von unterstützten Vorgänge zurückgeben.</span><span class="sxs-lookup"><span data-stu-id="dc503-248">If a plugin does not support the package source, the plugin must return an empty set of supported operations.</span></span>

> [!Note]
> <span data-ttu-id="dc503-249">Diese Nachricht wurde in Version aktualisiert *2.0.0*.</span><span class="sxs-lookup"><span data-stu-id="dc503-249">This message has been updated in version *2.0.0*.</span></span> <span data-ttu-id="dc503-250">Es ist auf dem Client um Abwärtskompatibilität zu gewährleisten.</span><span class="sxs-lookup"><span data-stu-id="dc503-250">It is on the client to preserve backward compatibility.</span></span>

7.  <span data-ttu-id="dc503-251">Abrufen der pakethash</span><span class="sxs-lookup"><span data-stu-id="dc503-251">Get package hash</span></span>
    * <span data-ttu-id="dc503-252">Anfordern der Richtung: NuGet ->-Plug-in</span><span class="sxs-lookup"><span data-stu-id="dc503-252">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="dc503-253">Die Anforderung enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="dc503-253">The request will contain:</span></span>
        * <span data-ttu-id="dc503-254">der Paket-ID und version</span><span class="sxs-lookup"><span data-stu-id="dc503-254">the package ID and version</span></span>
        * <span data-ttu-id="dc503-255">Speicherort für die Paketquelle repository</span><span class="sxs-lookup"><span data-stu-id="dc503-255">the package source repository location</span></span>
        * <span data-ttu-id="dc503-256">Der Hashalgorithmus</span><span class="sxs-lookup"><span data-stu-id="dc503-256">the hash algorithm</span></span>
    * <span data-ttu-id="dc503-257">Eine Antwort enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="dc503-257">A response will contain:</span></span>
        * <span data-ttu-id="dc503-258">Antwortcode, der angibt, des Ergebnis des Vorgangs</span><span class="sxs-lookup"><span data-stu-id="dc503-258">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="dc503-259">der Dateihash ein Paket unter Verwendung des angeforderten Hashalgorithmus, wenn der Vorgang erfolgreich war</span><span class="sxs-lookup"><span data-stu-id="dc503-259">a package file hash using the requested hash algorithm if the operation was successful</span></span>

8.  <span data-ttu-id="dc503-260">Abrufen von Paketversionen</span><span class="sxs-lookup"><span data-stu-id="dc503-260">Get package versions</span></span>
    * <span data-ttu-id="dc503-261">Anfordern der Richtung: NuGet ->-Plug-in</span><span class="sxs-lookup"><span data-stu-id="dc503-261">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="dc503-262">Die Anforderung enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="dc503-262">The request will contain:</span></span>
        * <span data-ttu-id="dc503-263">die Paket-ID</span><span class="sxs-lookup"><span data-stu-id="dc503-263">the package ID</span></span>
        * <span data-ttu-id="dc503-264">Speicherort für die Paketquelle repository</span><span class="sxs-lookup"><span data-stu-id="dc503-264">the package source repository location</span></span>
    * <span data-ttu-id="dc503-265">Eine Antwort enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="dc503-265">A response will contain:</span></span>
        * <span data-ttu-id="dc503-266">Antwortcode, der angibt, des Ergebnis des Vorgangs</span><span class="sxs-lookup"><span data-stu-id="dc503-266">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="dc503-267">ein aufzählbares Objekt von Paketversionen, wenn der Vorgang erfolgreich war</span><span class="sxs-lookup"><span data-stu-id="dc503-267">an enumerable of package versions if the operation was successful</span></span>

9.  <span data-ttu-id="dc503-268">Dienstindex abrufen</span><span class="sxs-lookup"><span data-stu-id="dc503-268">Get service index</span></span>
    * <span data-ttu-id="dc503-269">Anfordern der Richtung: NuGet-Plug-in -></span><span class="sxs-lookup"><span data-stu-id="dc503-269">Request direction:  plugin -> NuGet</span></span>
    * <span data-ttu-id="dc503-270">Die Anforderung enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="dc503-270">The request will contain:</span></span>
        * <span data-ttu-id="dc503-271">Speicherort für die Paketquelle repository</span><span class="sxs-lookup"><span data-stu-id="dc503-271">the package source repository location</span></span>
    * <span data-ttu-id="dc503-272">Eine Antwort enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="dc503-272">A response will contain:</span></span>
        * <span data-ttu-id="dc503-273">Antwortcode, der angibt, des Ergebnis des Vorgangs</span><span class="sxs-lookup"><span data-stu-id="dc503-273">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="dc503-274">der dienstindex, wenn der Vorgang erfolgreich war</span><span class="sxs-lookup"><span data-stu-id="dc503-274">the service index if the operation was successful</span></span>

10.  <span data-ttu-id="dc503-275">Handshake</span><span class="sxs-lookup"><span data-stu-id="dc503-275">Handshake</span></span>
     * <span data-ttu-id="dc503-276">Anfordern der Richtung: NuGet <> –-Plug-in</span><span class="sxs-lookup"><span data-stu-id="dc503-276">Request direction:  NuGet <-> plugin</span></span>
     * <span data-ttu-id="dc503-277">Die Anforderung enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="dc503-277">The request will contain:</span></span>
         * <span data-ttu-id="dc503-278">die aktuelle Version des-Plug-in-Protokoll</span><span class="sxs-lookup"><span data-stu-id="dc503-278">the current plugin protocol version</span></span>
         * <span data-ttu-id="dc503-279">die unterstützte Mindestversion-Plug-in-Protokoll</span><span class="sxs-lookup"><span data-stu-id="dc503-279">the minimum supported plugin protocol version</span></span>
     * <span data-ttu-id="dc503-280">Eine Antwort enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="dc503-280">A response will contain:</span></span>
         * <span data-ttu-id="dc503-281">Antwortcode, der angibt, des Ergebnis des Vorgangs</span><span class="sxs-lookup"><span data-stu-id="dc503-281">a response code indicating the outcome of the operation</span></span>
         * <span data-ttu-id="dc503-282">Das ausgehandelte Protokoll-Version, wenn der Vorgang erfolgreich war.</span><span class="sxs-lookup"><span data-stu-id="dc503-282">the negotiated protocol version if the operation was successful.</span></span>  <span data-ttu-id="dc503-283">Ein Fehler führen die Beendigung des Plug-Ins.</span><span class="sxs-lookup"><span data-stu-id="dc503-283">A failure will result in termination of the plugin.</span></span>

11.  <span data-ttu-id="dc503-284">Initialisieren</span><span class="sxs-lookup"><span data-stu-id="dc503-284">Initialize</span></span>
     * <span data-ttu-id="dc503-285">Anfordern der Richtung: NuGet ->-Plug-in</span><span class="sxs-lookup"><span data-stu-id="dc503-285">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="dc503-286">Die Anforderung enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="dc503-286">The request will contain:</span></span>
         * <span data-ttu-id="dc503-287">die Version des NuGet-Client-Tools</span><span class="sxs-lookup"><span data-stu-id="dc503-287">the NuGet client tool version</span></span>
         * <span data-ttu-id="dc503-288">die NuGet Client Tools effektive Sprache.</span><span class="sxs-lookup"><span data-stu-id="dc503-288">the NuGet client tool effective language.</span></span>  <span data-ttu-id="dc503-289">Dies berücksichtigt die ForceEnglishOutput-Einstellung, wenn verwendet.</span><span class="sxs-lookup"><span data-stu-id="dc503-289">This takes into consideration the ForceEnglishOutput setting, if used.</span></span>
         * <span data-ttu-id="dc503-290">das standardmäßige Anforderung-Timeout, die der Protokoll-Standardwert hat Vorrang vor.</span><span class="sxs-lookup"><span data-stu-id="dc503-290">the default request timeout, which supersedes the protocol default.</span></span>
     * <span data-ttu-id="dc503-291">Eine Antwort enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="dc503-291">A response will contain:</span></span>
         * <span data-ttu-id="dc503-292">eine Antwortcode, der angibt, des Ergebnis des Vorgangs.</span><span class="sxs-lookup"><span data-stu-id="dc503-292">a response code indicating the outcome of the operation.</span></span>  <span data-ttu-id="dc503-293">Ein Fehler führen die Beendigung des Plug-Ins.</span><span class="sxs-lookup"><span data-stu-id="dc503-293">A failure will result in termination of the plugin.</span></span>

12.  <span data-ttu-id="dc503-294">Protokoll</span><span class="sxs-lookup"><span data-stu-id="dc503-294">Log</span></span>
     * <span data-ttu-id="dc503-295">Anfordern der Richtung: NuGet-Plug-in -></span><span class="sxs-lookup"><span data-stu-id="dc503-295">Request direction:  plugin -> NuGet</span></span>
     * <span data-ttu-id="dc503-296">Die Anforderung enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="dc503-296">The request will contain:</span></span>
         * <span data-ttu-id="dc503-297">die Protokollebene für die Anforderung</span><span class="sxs-lookup"><span data-stu-id="dc503-297">the log level for the request</span></span>
         * <span data-ttu-id="dc503-298">einer zu protokollierenden Meldung</span><span class="sxs-lookup"><span data-stu-id="dc503-298">a message to log</span></span>
     * <span data-ttu-id="dc503-299">Eine Antwort enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="dc503-299">A response will contain:</span></span>
         * <span data-ttu-id="dc503-300">eine Antwortcode, der angibt, des Ergebnis des Vorgangs.</span><span class="sxs-lookup"><span data-stu-id="dc503-300">a response code indicating the outcome of the operation.</span></span>

13.  <span data-ttu-id="dc503-301">Überwachen von NuGet-Prozessende</span><span class="sxs-lookup"><span data-stu-id="dc503-301">Monitor NuGet process exit</span></span>
     * <span data-ttu-id="dc503-302">Anfordern der Richtung: NuGet ->-Plug-in</span><span class="sxs-lookup"><span data-stu-id="dc503-302">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="dc503-303">Die Anforderung enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="dc503-303">The request will contain:</span></span>
         * <span data-ttu-id="dc503-304">die NuGet-Prozess-ID</span><span class="sxs-lookup"><span data-stu-id="dc503-304">the NuGet process ID</span></span>
     * <span data-ttu-id="dc503-305">Eine Antwort enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="dc503-305">A response will contain:</span></span>
         * <span data-ttu-id="dc503-306">eine Antwortcode, der angibt, des Ergebnis des Vorgangs.</span><span class="sxs-lookup"><span data-stu-id="dc503-306">a response code indicating the outcome of the operation.</span></span>

14.  <span data-ttu-id="dc503-307">Vorabrufen von Paket</span><span class="sxs-lookup"><span data-stu-id="dc503-307">Prefetch package</span></span>
     * <span data-ttu-id="dc503-308">Anfordern der Richtung: NuGet ->-Plug-in</span><span class="sxs-lookup"><span data-stu-id="dc503-308">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="dc503-309">Die Anforderung enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="dc503-309">The request will contain:</span></span>
         * <span data-ttu-id="dc503-310">der Paket-ID und version</span><span class="sxs-lookup"><span data-stu-id="dc503-310">the package ID and version</span></span>
         * <span data-ttu-id="dc503-311">Speicherort für die Paketquelle repository</span><span class="sxs-lookup"><span data-stu-id="dc503-311">the package source repository location</span></span>
     * <span data-ttu-id="dc503-312">Eine Antwort enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="dc503-312">A response will contain:</span></span>
         * <span data-ttu-id="dc503-313">Antwortcode, der angibt, des Ergebnis des Vorgangs</span><span class="sxs-lookup"><span data-stu-id="dc503-313">a response code indicating the outcome of the operation</span></span>

15.  <span data-ttu-id="dc503-314">Festlegen von Anmeldeinformationen</span><span class="sxs-lookup"><span data-stu-id="dc503-314">Set credentials</span></span>
     * <span data-ttu-id="dc503-315">Anfordern der Richtung: NuGet ->-Plug-in</span><span class="sxs-lookup"><span data-stu-id="dc503-315">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="dc503-316">Die Anforderung enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="dc503-316">The request will contain:</span></span>
         * <span data-ttu-id="dc503-317">Speicherort für die Paketquelle repository</span><span class="sxs-lookup"><span data-stu-id="dc503-317">the package source repository location</span></span>
         * <span data-ttu-id="dc503-318">der letzte bekannte Quelle paketbenutzernamen, falls verfügbar</span><span class="sxs-lookup"><span data-stu-id="dc503-318">the last known package source username, if available</span></span>
         * <span data-ttu-id="dc503-319">das letzte bekannte Quelle Paketkennwort, falls verfügbar</span><span class="sxs-lookup"><span data-stu-id="dc503-319">the last known package source password, if available</span></span>
         * <span data-ttu-id="dc503-320">der letzte bekannte Proxybenutzername, falls verfügbar</span><span class="sxs-lookup"><span data-stu-id="dc503-320">the last known proxy username, if available</span></span>
         * <span data-ttu-id="dc503-321">das letzte bekannte Proxykennwort, falls verfügbar</span><span class="sxs-lookup"><span data-stu-id="dc503-321">the last known proxy password, if available</span></span>
     * <span data-ttu-id="dc503-322">Eine Antwort enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="dc503-322">A response will contain:</span></span>
         * <span data-ttu-id="dc503-323">Antwortcode, der angibt, des Ergebnis des Vorgangs</span><span class="sxs-lookup"><span data-stu-id="dc503-323">a response code indicating the outcome of the operation</span></span>

16.  <span data-ttu-id="dc503-324">Set-Protokollebene</span><span class="sxs-lookup"><span data-stu-id="dc503-324">Set log level</span></span>
     * <span data-ttu-id="dc503-325">Anfordern der Richtung: NuGet ->-Plug-in</span><span class="sxs-lookup"><span data-stu-id="dc503-325">Request direction:  NuGet -> plugin</span></span>
     * <span data-ttu-id="dc503-326">Die Anforderung enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="dc503-326">The request will contain:</span></span>
         * <span data-ttu-id="dc503-327">Die Standardprotokollebene</span><span class="sxs-lookup"><span data-stu-id="dc503-327">the default log level</span></span>
     * <span data-ttu-id="dc503-328">Eine Antwort enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="dc503-328">A response will contain:</span></span>
         * <span data-ttu-id="dc503-329">Antwortcode, der angibt, des Ergebnis des Vorgangs</span><span class="sxs-lookup"><span data-stu-id="dc503-329">a response code indicating the outcome of the operation</span></span>

<span data-ttu-id="dc503-330">Protokollversion *2.0.0* Nachrichten</span><span class="sxs-lookup"><span data-stu-id="dc503-330">Protocol Version *2.0.0* messages</span></span>

17. <span data-ttu-id="dc503-331">Abrufen von Vorgang Ansprüche</span><span class="sxs-lookup"><span data-stu-id="dc503-331">Get Operation Claims</span></span>

* <span data-ttu-id="dc503-332">Anfordern der Richtung: NuGet ->-Plug-in</span><span class="sxs-lookup"><span data-stu-id="dc503-332">Request direction:  NuGet -> plugin</span></span>
    * <span data-ttu-id="dc503-333">Die Anforderung enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="dc503-333">The request will contain:</span></span>
        * <span data-ttu-id="dc503-334">der Dienst index.json für eine Paketquelle</span><span class="sxs-lookup"><span data-stu-id="dc503-334">the service index.json for a package source</span></span>
        * <span data-ttu-id="dc503-335">Speicherort für die Paketquelle repository</span><span class="sxs-lookup"><span data-stu-id="dc503-335">the package source repository location</span></span>
    * <span data-ttu-id="dc503-336">Eine Antwort enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="dc503-336">A response will contain:</span></span>
        * <span data-ttu-id="dc503-337">Antwortcode, der angibt, des Ergebnis des Vorgangs</span><span class="sxs-lookup"><span data-stu-id="dc503-337">a response code indicating the outcome of the operation</span></span>
        * <span data-ttu-id="dc503-338">ein aufzählbares Element für unterstützten Vorgänge, wenn der Vorgang erfolgreich war.</span><span class="sxs-lookup"><span data-stu-id="dc503-338">an enumerable of supported operations if the operation was successful.</span></span>  <span data-ttu-id="dc503-339">Wenn Sie ein Plug-in die Paketquelle nicht unterstützt, muss die-Plug-in einen leeren Satz von unterstützten Vorgänge zurückgeben.</span><span class="sxs-lookup"><span data-stu-id="dc503-339">If a plugin does not support the package source, the plugin must return an empty set of supported operations.</span></span>

    <span data-ttu-id="dc503-340">Wenn die Dienst Index und die Paket-Quelle auf null festgelegt sind, kann das Plug-in mit der Authentifizierung beantworten.</span><span class="sxs-lookup"><span data-stu-id="dc503-340">If the service index and package source are null, then the plugin can answer with authentication.</span></span>

18. <span data-ttu-id="dc503-341">Abrufen von Authentifizierungsanmeldeinformationen für</span><span class="sxs-lookup"><span data-stu-id="dc503-341">Get Authentication Credentials</span></span>

* <span data-ttu-id="dc503-342">Anfordern der Richtung: NuGet ->-Plug-in</span><span class="sxs-lookup"><span data-stu-id="dc503-342">Request direction: NuGet -> plugin</span></span>
* <span data-ttu-id="dc503-343">Die Anforderung enthält Folgendes:</span><span class="sxs-lookup"><span data-stu-id="dc503-343">The request will contain:</span></span>
    * <span data-ttu-id="dc503-344">URI</span><span class="sxs-lookup"><span data-stu-id="dc503-344">Uri</span></span>
    * <span data-ttu-id="dc503-345">isRetry</span><span class="sxs-lookup"><span data-stu-id="dc503-345">isRetry</span></span>
    * <span data-ttu-id="dc503-346">NonInteractive</span><span class="sxs-lookup"><span data-stu-id="dc503-346">NonInteractive</span></span>
    * <span data-ttu-id="dc503-347">CanShowDialog</span><span class="sxs-lookup"><span data-stu-id="dc503-347">CanShowDialog</span></span>
* <span data-ttu-id="dc503-348">Eine Antwort enthält.</span><span class="sxs-lookup"><span data-stu-id="dc503-348">A response will contain</span></span>
    * <span data-ttu-id="dc503-349">Benutzername</span><span class="sxs-lookup"><span data-stu-id="dc503-349">Username</span></span>
    * <span data-ttu-id="dc503-350">Kennwort</span><span class="sxs-lookup"><span data-stu-id="dc503-350">Password</span></span>
    * <span data-ttu-id="dc503-351">Meldung</span><span class="sxs-lookup"><span data-stu-id="dc503-351">Message</span></span>
    * <span data-ttu-id="dc503-352">Liste der Typen der Authentifizierung</span><span class="sxs-lookup"><span data-stu-id="dc503-352">List of Auth Types</span></span>
    * <span data-ttu-id="dc503-353">MessageResponseCode</span><span class="sxs-lookup"><span data-stu-id="dc503-353">MessageResponseCode</span></span>