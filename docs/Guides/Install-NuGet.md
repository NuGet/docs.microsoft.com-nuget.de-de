---
title: Installieren von NuGet-Clienttools | Microsoft-Dokumentation
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/02/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 683b8b34-a6f4-4d56-b9cd-2483bfbad1ad
description: "Anleitung zum Installieren von Clienttools, der Befehlszeilenschnittstelle (Command-Line Interface, CLI) und des Paket-Managers für Visual Studio."
keywords: "CLI von nuget.exe, NuGet-Clienttools, NuGet-Paket-Manager, NuGet-Paket-Manager-Konsole, NuGet für Visual Studio, NuGet-Beta-Kanal"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: b1abb30458c9ebfb0ffb28be254efd9709a9627f
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/14/2017
---
# <a name="installing-nuget-client-tools"></a><span data-ttu-id="b8b74-104">Installieren von NuGet-Clienttools</span><span class="sxs-lookup"><span data-stu-id="b8b74-104">Installing NuGet client tools</span></span>

> [!Tip]
> <span data-ttu-id="b8b74-105">**Sie möchten ein Paket installieren? Unter [Schnellstart - Verwenden eines Pakets](../Quickstart/Use-a-Package.md) finden Sie weitere Informationen.**</span><span class="sxs-lookup"><span data-stu-id="b8b74-105">**Looking to install a package? See [Quickstart - Use a package](../Quickstart/Use-a-Package.md).**</span></span>

<span data-ttu-id="b8b74-106">Es gibt zwei primäre Tools, die Sie beim Erstellen, Veröffentlichen und Verwenden von NuGet-Paketen unterstützen:</span><span class="sxs-lookup"><span data-stu-id="b8b74-106">There are two primary tools available to help you build, publish and consume NuGet packages:</span></span>

1. <span data-ttu-id="b8b74-107">Die [**NuGet-CLI**](#nuget-cli) ist das Befehlszeilenprogramm für Windows, über die alle Funktionen von NuGet bereitgestellt werden; sie kann auch unter Mac OSX und Linux mit Mono oder über die .NET Core-CLI (`dotnet`) ausgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="b8b74-107">The [**NuGet CLI**](#nuget-cli) is the command-line utility for Windows that provides all NuGet capabilities; it can also be run on Mac OSX and Linux using Mono, or through the .NET Core CLI (`dotnet`).</span></span>
1. <span data-ttu-id="b8b74-108">Bei dem [**NuGet-Paket-Manager in Visual Studio**](#nuget-package-manager-in-visual-studio) (nur Windows) handelt es sich um ein GUI-Tool für die Verwaltung von Paketen. Es enthält eine PowerShell-Konsole, über die Sie bestimmte NuGet-Befehle direkt in Visual Studio verwenden können.</span><span class="sxs-lookup"><span data-stu-id="b8b74-108">The [**NuGet Package Manager in Visual Studio**](#nuget-package-manager-in-visual-studio) (Windows only) is a GUI tool for managing packages and includes a PowerShell console through which you can use certain NuGet commands directly within Visual Studio.</span></span> <span data-ttu-id="b8b74-109">Die Benutzeroberfläche des Paket-Managers und die Paket-Manager-Konsole sind beide in Visual Studio 2012 und höher (unter Windows) enthalten und können manuell für frühere Versionen installiert werden.</span><span class="sxs-lookup"><span data-stu-id="b8b74-109">The Package Manager UI and Console are both included with Visual Studio (on Windows) 2012 and later and can be installed manually for earlier versions.</span></span>

    <span data-ttu-id="b8b74-110">Bei Visual Studio für Mac sind NuGet-Funktionen direkt integriert.</span><span class="sxs-lookup"><span data-stu-id="b8b74-110">With Visual Studio for Mac, NuGet capabilities are built in directly.</span></span> <span data-ttu-id="b8b74-111">Eine exemplarische Vorgehensweise finde Sie unter [Einschließen eines NuGet-Pakets in Ihr Projekt](https://docs.microsoft.com/visualstudio/mac/nuget-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="b8b74-111">See [Including a NuGet package in your project](https://docs.microsoft.com/visualstudio/mac/nuget-walkthrough) for a walkthrough.</span></span>

    <span data-ttu-id="b8b74-112">Visual Studio Code verfügt derzeit über keine integrierte NuGet-Unterstützung.</span><span class="sxs-lookup"><span data-stu-id="b8b74-112">Visual Studio Code at present does not have any built-in NuGet support.</span></span> <span data-ttu-id="b8b74-113">Verwenden Sie die NuGet-CLI oder die [Dotnet-CLI](../Tools/dotnet-Commands.md).</span><span class="sxs-lookup"><span data-stu-id="b8b74-113">Use the NuGet CLI or the [dotnet CLI](../Tools/dotnet-Commands.md).</span></span>

<span data-ttu-id="b8b74-114">Die NuGet-CLI und der Paket-Manager unterstützen folgende Vorgänge:</span><span class="sxs-lookup"><span data-stu-id="b8b74-114">The NuGet CLI and Package Manager both support the following operations:</span></span>

- <span data-ttu-id="b8b74-115">Suchen von Paketen</span><span class="sxs-lookup"><span data-stu-id="b8b74-115">Search packages</span></span>
- <span data-ttu-id="b8b74-116">Installieren von Paketen</span><span class="sxs-lookup"><span data-stu-id="b8b74-116">Install packages</span></span>
- <span data-ttu-id="b8b74-117">Aktualisieren von Paketen</span><span class="sxs-lookup"><span data-stu-id="b8b74-117">Update packages</span></span>
- <span data-ttu-id="b8b74-118">Deinstallieren von Paketen</span><span class="sxs-lookup"><span data-stu-id="b8b74-118">Uninstall packages</span></span>
- <span data-ttu-id="b8b74-119">Wiederherstellen von Paketen (UI nur im Paket-Manager)</span><span class="sxs-lookup"><span data-stu-id="b8b74-119">Restore packages (UI only in the Package Manager)</span></span>
- <span data-ttu-id="b8b74-120">Verwalten von NuGet-Quellen</span><span class="sxs-lookup"><span data-stu-id="b8b74-120">Manage NuGet sources</span></span>

<span data-ttu-id="b8b74-121">Die folgenden Funktionen werden nur in der NuGet-CLI unterstützt:</span><span class="sxs-lookup"><span data-stu-id="b8b74-121">The following capabilities are supported only in the NuGet CLI:</span></span>

- <span data-ttu-id="b8b74-122">Verwalten von Paketen (nuget.org oder privater Feed)</span><span class="sxs-lookup"><span data-stu-id="b8b74-122">Manage packages (nuget.org or private feed)</span></span>
- <span data-ttu-id="b8b74-123">Erstellen von Paketen</span><span class="sxs-lookup"><span data-stu-id="b8b74-123">Create packages</span></span> 
- <span data-ttu-id="b8b74-124">Veröffentlichen von Paketen</span><span class="sxs-lookup"><span data-stu-id="b8b74-124">Publish packages</span></span>
- <span data-ttu-id="b8b74-125">Verwalten von „Nuget.Config“</span><span class="sxs-lookup"><span data-stu-id="b8b74-125">Manage Nuget.Config</span></span>
- <span data-ttu-id="b8b74-126">Verwalten des NuGet-Cache</span><span class="sxs-lookup"><span data-stu-id="b8b74-126">Manage the NuGet cache</span></span>
- <span data-ttu-id="b8b74-127">Replizieren eines Pakets</span><span class="sxs-lookup"><span data-stu-id="b8b74-127">Replicating a package</span></span>

> [!Note]
> <span data-ttu-id="b8b74-128">Ein weiteres gutes Tool ist der [NuGet-Paket-Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer), ein eigenständiges Open Source-Tool, mit dem NuGet-Pakete visuell angezeigt, erstellt und bearbeitet werden können.</span><span class="sxs-lookup"><span data-stu-id="b8b74-128">Another good tool is the [NuGet Package Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer), an open-source, stand-alone tool to visually explore, create, and edit NuGet packages.</span></span> <span data-ttu-id="b8b74-129">Dieses Tool ist beispielsweise sehr hilfreich, wenn experimentelle Änderungen an einer Paketstruktur vorgenommen werden, ohne das Paket jedes Mal neu erstellen zu müssen.</span><span class="sxs-lookup"><span data-stu-id="b8b74-129">It's very helpful, for example, to make experimental changes to a package structure without having to rebuild the package each time.</span></span>
> <span data-ttu-id="b8b74-130">Die für die Entwicklung von .NET Core-Apps verwendete plattformübergreifende Toolkette der [.NET Core-CLI](https://docs.microsoft.com/dotnet/articles/core/tools/index#installation) unterstützt mehrere NuGet-Befehle, wie z.B. „delete“, „locals“, „push“, „pack“ und „restore“.</span><span class="sxs-lookup"><span data-stu-id="b8b74-130">The cross-platform [.NET Core CLI](https://docs.microsoft.com/dotnet/articles/core/tools/index#installation) toolchain, used for developing .NET Core applications, supports several NuGet commands, such as delete, locals, push, pack, and restore.</span></span> 

## <a name="nuget-cli"></a><span data-ttu-id="b8b74-131">NuGet-CLI</span><span class="sxs-lookup"><span data-stu-id="b8b74-131">NuGet CLI</span></span>

<span data-ttu-id="b8b74-132">Die NuGet-Befehlszeilenschnittstelle ermöglicht den Zugriff auf alle NuGet-Funktionen und kann unter Windows, Mac OSX und Linux ausgeführt werden, wie in den folgenden Abschnitten beschrieben.</span><span class="sxs-lookup"><span data-stu-id="b8b74-132">The NuGet command-line interface provides access to all NuGet capabilities, and can be run on Windows, Mac OSX, and Linux as described in the following sections.</span></span>

### <a name="windows"></a><span data-ttu-id="b8b74-133">Windows</span><span class="sxs-lookup"><span data-stu-id="b8b74-133">Windows</span></span>

<span data-ttu-id="b8b74-134">**Direkter Download:**</span><span class="sxs-lookup"><span data-stu-id="b8b74-134">**Direct download:**</span></span>

[!INCLUDE[install-cli](../includes/install-cli.md)]

> [!Note]
> <span data-ttu-id="b8b74-135">In NuGet 1.4 oder höher können Sie `nuget update -self` für das Update Ihrer vorhandenen nuget.exe auf die neueste Version verwenden.</span><span class="sxs-lookup"><span data-stu-id="b8b74-135">With NuGet 1.4+, you can use `nuget update -self` to update your existing nuget.exe to the latest version.</span></span>

<span data-ttu-id="b8b74-136">**Weitere Methoden:**</span><span class="sxs-lookup"><span data-stu-id="b8b74-136">**Other methods:**</span></span>

- <span data-ttu-id="b8b74-137">**Chocolatey**: Installieren Sie das Chocolatey-Paket [NuGet.CommandLine](http://chocolatey.org/packages/NuGet.CommandLine) mithilfe des [Chocolatey](http://chocolatey.org)-Clients.</span><span class="sxs-lookup"><span data-stu-id="b8b74-137">**Chocolatey**: Install the [NuGet.CommandLine](http://chocolatey.org/packages/NuGet.CommandLine) Chocolatey package using the [Chocolatey](http://chocolatey.org) client.</span></span> 

    ```ps
    choco install nuget.commandline
    ```

- <span data-ttu-id="b8b74-138">**Visual Studio**: Installieren Sie das Paket [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) über die Paket-Manager-Konsole in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="b8b74-138">**Visual Studio**: Install the [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) package from the Package Manager Console in Visual Studio.</span></span>

    > [!Note]
    > <span data-ttu-id="b8b74-139">**Für Benutzer von NuGet 2.x**: Aufgrund von wichtigen Änderungen in NuGet 3.2 wird auf [https://nuget.org/nuget.exe](https://nuget.org/nuget.exe) auf das neueste stabile Release von NuGet-2.x verwiesen, damit eine potenzielle Unterbrechung von Continuous Integration-Systemen verhindert werden kann.</span><span class="sxs-lookup"><span data-stu-id="b8b74-139">**For NuGet 2.x users**: Because of breaking changes introduced in NuGet 3.2, [https://nuget.org/nuget.exe](https://nuget.org/nuget.exe) points to the latest stable NuGet 2.x release to prevent continuous integration systems from potentially breaking.</span></span>

<a name="compatibility-with-mono"></a>

## <a name="mac-osx-and-linux"></a><span data-ttu-id="b8b74-140">Mac OSX und Linux</span><span class="sxs-lookup"><span data-stu-id="b8b74-140">Mac OSX and Linux</span></span>

<span data-ttu-id="b8b74-141">Unter Mac OSX und Linux gibt es zwei Möglichkeiten für die Ausführung der NuGet-CLI:</span><span class="sxs-lookup"><span data-stu-id="b8b74-141">On Mac OSX and Linux, there are two ways to run the NuGet CLI:</span></span>

- <span data-ttu-id="b8b74-142">Installieren Sie das [.NET Core SDK](https://www.microsoft.com/net/download/core), darunter die NuGet-Hauptfunktionen.</span><span class="sxs-lookup"><span data-stu-id="b8b74-142">Install the [.NET Core SDK](https://www.microsoft.com/net/download/core), which includes the core NuGet capabilities.</span></span> <span data-ttu-id="b8b74-143">Downloads werden auch unter [github.com/dotnet/cli](https://github.com/dotnet/cli) aufgeführt.</span><span class="sxs-lookup"><span data-stu-id="b8b74-143">Downloads are also listed on [github.com/dotnet/cli](https://github.com/dotnet/cli).</span></span> <span data-ttu-id="b8b74-144">Wenn Sie umfassendere Funktionen benötigen, verwenden Sie die zweite, nachfolgende Option für die Verwendung von `nuget.exe` mit Mono.</span><span class="sxs-lookup"><span data-stu-id="b8b74-144">If you need fuller capabilities, then use the second option below to use `nuget.exe` with Mono.</span></span>

- <span data-ttu-id="b8b74-145">Installieren Sie [Mono](http://www.mono-project.com/docs/getting-started/install/), und verwenden Sie anschließend die ausführbare Befehlszeilendatei von `nuget.exe` für Windows (Version 3.2 und höher) von [nuget.org/downloads](https://nuget.org/downloads).</span><span class="sxs-lookup"><span data-stu-id="b8b74-145">Install [Mono](http://www.mono-project.com/docs/getting-started/install/) and then use the `nuget.exe` command-line executable for Windows (version 3.2 and later) from [nuget.org/downloads](https://nuget.org/downloads).</span></span> <span data-ttu-id="b8b74-146">Die Ausführung von NuGet in Mono unterliegt folgenden Einschränkungen:</span><span class="sxs-lookup"><span data-stu-id="b8b74-146">Running NuGet on Mono is subject to the following limitations:</span></span>

    - <span data-ttu-id="b8b74-147">Auf ihre Funktionsfähigkeit getestete Befehle:</span><span class="sxs-lookup"><span data-stu-id="b8b74-147">Commands tested to work:</span></span>
        - <span data-ttu-id="b8b74-148">config</span><span class="sxs-lookup"><span data-stu-id="b8b74-148">config</span></span>
        - <span data-ttu-id="b8b74-149">Löschen</span><span class="sxs-lookup"><span data-stu-id="b8b74-149">delete</span></span>
        - <span data-ttu-id="b8b74-150">help</span><span class="sxs-lookup"><span data-stu-id="b8b74-150">help</span></span>
        - <span data-ttu-id="b8b74-151">install</span><span class="sxs-lookup"><span data-stu-id="b8b74-151">install</span></span>
        - <span data-ttu-id="b8b74-152">Liste</span><span class="sxs-lookup"><span data-stu-id="b8b74-152">list</span></span>
        - <span data-ttu-id="b8b74-153">push</span><span class="sxs-lookup"><span data-stu-id="b8b74-153">push</span></span>
        - <span data-ttu-id="b8b74-154">setApiKey</span><span class="sxs-lookup"><span data-stu-id="b8b74-154">setApiKey</span></span>
        - <span data-ttu-id="b8b74-155">sources</span><span class="sxs-lookup"><span data-stu-id="b8b74-155">sources</span></span>
        - <span data-ttu-id="b8b74-156">spec</span><span class="sxs-lookup"><span data-stu-id="b8b74-156">spec</span></span>

    - <span data-ttu-id="b8b74-157">Teilweise funktionierende Befehle:</span><span class="sxs-lookup"><span data-stu-id="b8b74-157">Partially-working commands:</span></span>
        - <span data-ttu-id="b8b74-158">pack: Funktioniert bei `.nuspec`-Dateien, jedoch nicht bei Projektdateien.</span><span class="sxs-lookup"><span data-stu-id="b8b74-158">pack: works with `.nuspec` files but not with project files.</span></span>
        - <span data-ttu-id="b8b74-159">restore: Funktioniert bei `packages.config`- und `project.json`-Dateien, jedoch nicht bei Projektmappendateien (`.sln`).</span><span class="sxs-lookup"><span data-stu-id="b8b74-159">restore: works with `packages.config` and `project.json` files but not with solution (`.sln`) files.</span></span>

    - <span data-ttu-id="b8b74-160">Nicht funktionierende Befehle:</span><span class="sxs-lookup"><span data-stu-id="b8b74-160">Commands that do not work:</span></span>
        - <span data-ttu-id="b8b74-161">aktualisieren</span><span class="sxs-lookup"><span data-stu-id="b8b74-161">update</span></span>

### <a name="related-topics"></a><span data-ttu-id="b8b74-162">Verwandte Themen</span><span class="sxs-lookup"><span data-stu-id="b8b74-162">Related topics</span></span>

- [<span data-ttu-id="b8b74-163">Verweis auf NuGet-CLI</span><span class="sxs-lookup"><span data-stu-id="b8b74-163">NuGet CLI reference</span></span>](../tools/nuget-exe-cli-reference.md)
- [<span data-ttu-id="b8b74-164">Erstellen eines Pakets</span><span class="sxs-lookup"><span data-stu-id="b8b74-164">Creating a package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="b8b74-165">Veröffentlichen eines Pakets</span><span class="sxs-lookup"><span data-stu-id="b8b74-165">Publishing a Package</span></span>](../create-packages/publish-a-package.md)

## <a name="nuget-package-manager-in-visual-studio"></a><span data-ttu-id="b8b74-166">NuGet-Paket-Manager in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b8b74-166">NuGet Package Manager in Visual Studio</span></span>

<span data-ttu-id="b8b74-167">Der NuGet-Paket-Manager ist in jeder Edition von Visual Studio unter Windows ab Version 2012 enthalten.</span><span class="sxs-lookup"><span data-stu-id="b8b74-167">The NuGet Package Manager is included in every edition of Visual Studio on Windows, 2012 and later.</span></span> <span data-ttu-id="b8b74-168">Er umfasst die Benutzeroberfläche des Paket-Managers ([Referenz](../tools/package-manager-ui.md)) sowie die Paket-Manager-Konsole, über die Sie auf Tools zugreifen können, die im Lieferumfang bestimmter Pakete enthalten sind ([Referenz](../tools/package-manager-console.md)).</span><span class="sxs-lookup"><span data-stu-id="b8b74-168">It includes the Package Manager UI ([reference](../tools/package-manager-ui.md)), and the Package Manager Console through which you can access tools that come with certain packages ([reference](../tools/package-manager-console.md)).</span></span>

<span data-ttu-id="b8b74-169">Der Installer von Visual Studio 2017 umfasst den NuGet-Paket-Manager mit allen Workloads, die .NET verwenden.</span><span class="sxs-lookup"><span data-stu-id="b8b74-169">The Visual Studio 2017 installer includes the NuGet Package Manager with any workload that employs .NET.</span></span> <span data-ttu-id="b8b74-170">Führen Sie den Installer von Visual Studio 2017 aus, und überprüfen Sie die Option unter **Einzelne Komponenten > Codetools > NuGet-Paket-Manager**, um eine separate Installation auszuführen oder um zu überprüfen, ob der Paket-Manager installiert wurde.</span><span class="sxs-lookup"><span data-stu-id="b8b74-170">To install separately, or to verify that the Package Manager is installed, run the Visual Studio 2017 installer and check the option under **Individual Components > Code tools > NuGet package manager**.</span></span>

> [!Note]
> <span data-ttu-id="b8b74-171">Für die Konsole ist [PowerShell 2.0](http://support.microsoft.com/kb/968929) erforderlich, das unter Windows 7 oder höher und Windows Server 2008 R2 oder höher bereits installiert ist.</span><span class="sxs-lookup"><span data-stu-id="b8b74-171">The console requires [PowerShell 2.0](http://support.microsoft.com/kb/968929), which will already be installed on Windows 7 or higher and Windows Server 2008 R2 or higher.</span></span>
>
> <span data-ttu-id="b8b74-172">Befehle der Paket-Manager-Konsole funktionieren auch nur in Visual Studio unter Windows.</span><span class="sxs-lookup"><span data-stu-id="b8b74-172">Package Manager Console commands also work only within Visual Studio on Windows.</span></span> <span data-ttu-id="b8b74-173">Verwenden Sie die NuGet-CLI außerhalb dieser Umgebung, einschließlich mit Visual Studio für Mac und Visual Studio Code.</span><span class="sxs-lookup"><span data-stu-id="b8b74-173">Use the NuGet CLI outside of that environment, including with Visual Studio for Mac and Visual Studio Code.</span></span>

### <a name="package-manager-installation-for-visual-studio-2010-and-earlier"></a><span data-ttu-id="b8b74-174">Installation des Paket-Managers für Visual Studio 2010 oder ältere Versionen</span><span class="sxs-lookup"><span data-stu-id="b8b74-174">Package Manager installation for Visual Studio 2010 and earlier</span></span>

<span data-ttu-id="b8b74-175">*Diese Schritte sind für Visual Studio 2012 und höher nicht erforderlich, da der Paket-Manager dort bereits enthalten ist.*</span><span class="sxs-lookup"><span data-stu-id="b8b74-175">*These steps are not necessary for Visual Studio 2012 and later, which already include the Package Manager.*</span></span>

1. <span data-ttu-id="b8b74-176">Klicken Sie in Visual Studio 2010 und älteren Versionen auf **Tools > Erweiterungen und Updates**.</span><span class="sxs-lookup"><span data-stu-id="b8b74-176">In Visual Studio 2010 and earlier, click **Tools > Extension and Updates**.</span></span>
1. <span data-ttu-id="b8b74-177">Navigieren Sie zu **Online**, suchen Sie nach „NuGet-Paket-Manager für Visual Studio“, und klicken Sie auf **Herunterladen**.</span><span class="sxs-lookup"><span data-stu-id="b8b74-177">Navigate to **Online**, then search for "NuGet Package Manager for Visual Studio" and click **Download**.</span></span>
1. <span data-ttu-id="b8b74-178">Klicken Sie im Dialogfeld „Installer“ auf **Installieren**.</span><span class="sxs-lookup"><span data-stu-id="b8b74-178">In the Installer dialog box, click **Install**.</span></span>
1. <span data-ttu-id="b8b74-179">Starten Sie Visual Studio nach Abschluss der Installation erneut.</span><span class="sxs-lookup"><span data-stu-id="b8b74-179">When installation is complete, restart Visual Studio.</span></span>

> [!Tip]
> <span data-ttu-id="b8b74-180">Wenn Sie das Dialogfeld **Erweiterungen und Updates** in Visual Studio nicht verwenden können (da es z.B. von einem Proxy blockiert wird), können Sie Erweiterungen für Visual Studio 2013 und 2015 direkt unter [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html) herunterladen.</span><span class="sxs-lookup"><span data-stu-id="b8b74-180">If you're unable to use the **Extensions and Updates** dialog in Visual Studio (for example, its blocked by a proxy), you can download extensions for Visual Studio 2013 and 2015 directly at [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span></span>

### <a name="updating-the-package-manager"></a><span data-ttu-id="b8b74-181">Aktualisieren des Paket-Managers</span><span class="sxs-lookup"><span data-stu-id="b8b74-181">Updating the Package Manager</span></span>

<span data-ttu-id="b8b74-182">In Visual Studio 2015 Update 2 und höher wird der Paket-Manager automatisch auf das neueste stabile Release aktualisiert.</span><span class="sxs-lookup"><span data-stu-id="b8b74-182">For Visual Studio 2015 Update 2 and later, the Package Manager is automatically updated to the latest stable release.</span></span>

<span data-ttu-id="b8b74-183">Wählen Sie bei Visual Studio 2015 Update 1 und früher den Befehl **Tools > Erweiterungen und Updates** aus, und klicken Sie auf die Registerkarte **Updates**, um zu überprüfen, ob eine neue Version des Paket-Managers verfügbar ist.</span><span class="sxs-lookup"><span data-stu-id="b8b74-183">For Visual Studio 2015 Update 1 and earlier, select the **Tools > Extensions and Updates** command and click on the **Updates** tab to see if a new version of the Package Manager is available.</span></span>  

### <a name="nuget-previews"></a><span data-ttu-id="b8b74-184">NuGet-Vorschauen</span><span class="sxs-lookup"><span data-stu-id="b8b74-184">NuGet previews</span></span>

<span data-ttu-id="b8b74-185">Wenn Sie eine Vorschau der geplanten NuGet-Funktionen sehen möchten, installieren Sie die [Visual Studio 2017 Preview](https://www.visualstudio.com/vs/preview/), die parallel mit stabilen Releases von Visual Studio arbeitet.</span><span class="sxs-lookup"><span data-stu-id="b8b74-185">If you'd like to preview upcoming NuGet features, install the [Visual Studio 2017 Preview](https://www.visualstudio.com/vs/preview/), which works side-by-side with stable releases of Visual Studio.</span></span>

<span data-ttu-id="b8b74-186">Beachten Sie, dass der vorherige NuGet-Beta-Kanal (`https://dotnet.myget.org/F/nuget-beta/vsix/`) für Visual Studio 2015 nicht mehr verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="b8b74-186">Note that the previous NuGet Beta Channel (`https://dotnet.myget.org/F/nuget-beta/vsix/`) for Visual Studio 2015 is no longer used.</span></span>

<span data-ttu-id="b8b74-187">Wenn Sie Probleme mit einem Release von NuGet melden oder Ideen teilen möchten, können Sie sich im [GitHub-Repository von NuGet](https://github.com/Nuget/Home) beteiligen.</span><span class="sxs-lookup"><span data-stu-id="b8b74-187">To report problems with any release of NuGet or to share ideas, open an issue on the [NuGet GitHub repository](https://github.com/Nuget/Home).</span></span>

### <a name="related-topics"></a><span data-ttu-id="b8b74-188">Verwandte Themen</span><span class="sxs-lookup"><span data-stu-id="b8b74-188">Related topics</span></span>

- [<span data-ttu-id="b8b74-189">Benutzeroberflächenverweis des Paket-Managers</span><span class="sxs-lookup"><span data-stu-id="b8b74-189">Package Manager UI reference</span></span>](../tools/package-manager-ui.md)
- [<span data-ttu-id="b8b74-190">Verweis der Paket-Manager-Konsole</span><span class="sxs-lookup"><span data-stu-id="b8b74-190">Package Manager Console reference</span></span>](../tools/package-manager-console.md)
- [<span data-ttu-id="b8b74-191">PowerShell-Verweis des Paket-Managers</span><span class="sxs-lookup"><span data-stu-id="b8b74-191">Package Manager Console PowerShell reference</span></span>](../tools/powershell-reference.md)