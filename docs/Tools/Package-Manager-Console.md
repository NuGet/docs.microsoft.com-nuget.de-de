---
title: NuGet-Paket-Manager-Konsole Handbuch | Microsoft Docs
author: kraigb
hms.author: kraigb
manager: ghogen
ms.date: 01/23/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
f1_keywords: vs.nuget.packagemanager.console
description: "Anweisungen für die Verwendung der NuGet-Paket-Manager-Konsole in Visual Studio zum Arbeiten mit Paketen."
keywords: NuGet-Paket-Manager-Konsole, NuGet Powershell NuGet-Pakete verwalten
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: b89c51812cee0f64c6f5c39cd9d86bc4a0be068e
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="package-manager-console"></a><span data-ttu-id="c41dd-104">Paket-Manager-Konsole</span><span class="sxs-lookup"><span data-stu-id="c41dd-104">Package Manager Console</span></span>

<span data-ttu-id="c41dd-105">Die NuGet-Paket-Manager-Konsole wird in Visual Studio unter Windows 2012 und höher integriert.</span><span class="sxs-lookup"><span data-stu-id="c41dd-105">The NuGet Package Manager Console is built into Visual Studio on Windows version 2012 and later.</span></span> <span data-ttu-id="c41dd-106">(Es ist nicht in Visual Studio für Mac oder Visual Studio-Code enthalten.)</span><span class="sxs-lookup"><span data-stu-id="c41dd-106">(It is not included with Visual Studio for Mac or Visual Studio Code.)</span></span>

<span data-ttu-id="c41dd-107">Die Konsole können Sie verwenden [NuGet PowerShell-Befehle](../tools/powershell-reference.md) finden, installieren, deinstallieren und Aktualisieren von NuGet-Pakete.</span><span class="sxs-lookup"><span data-stu-id="c41dd-107">The console lets you use [NuGet PowerShell commands](../tools/powershell-reference.md) to find, install, uninstall, and update NuGet packages.</span></span> <span data-ttu-id="c41dd-108">Mithilfe der Konsole ist erforderlich, in Fällen, in dem das Paket-Manager-UI keine Möglichkeit zum Ausführen eines Vorgangs eingeben.</span><span class="sxs-lookup"><span data-stu-id="c41dd-108">Using the console is necessary in cases where the Package Manager UI does not provide a way to perform an operation.</span></span> <span data-ttu-id="c41dd-109">Mit `nuget.exe` Befehle in der Konsole finden Sie unter [mithilfe der CLI nuget.exe in der Konsole](#using-the-nugetexe-cli-in-the-console).</span><span class="sxs-lookup"><span data-stu-id="c41dd-109">To use `nuget.exe` commands in the console, see [Using the nuget.exe CLI in the console](#using-the-nugetexe-cli-in-the-console).</span></span>

<span data-ttu-id="c41dd-110">Suchen und Installieren eines Pakets erfolgt z. B. mit drei einfachen Schritten:</span><span class="sxs-lookup"><span data-stu-id="c41dd-110">For example, finding and installing a package is done with three easy steps:</span></span>

1. <span data-ttu-id="c41dd-111">Öffnen Sie das Projekt/die Projektmappe in Visual Studio, und öffnen Sie die Konsole unter Verwendung der **Extras > NuGet-Paket-Manager > Package Manager Console** Befehl.</span><span class="sxs-lookup"><span data-stu-id="c41dd-111">Open the project/solution in Visual Studio, and open the console using the **Tools > NuGet Package Manager > Package Manager Console** command.</span></span>

1. <span data-ttu-id="c41dd-112">Suchen Sie das Paket, das Sie installieren möchten.</span><span class="sxs-lookup"><span data-stu-id="c41dd-112">Find the package you want to install.</span></span> <span data-ttu-id="c41dd-113">Fahren Sie mit Schritt 3 fort, wenn Sie dies bereits kennen.</span><span class="sxs-lookup"><span data-stu-id="c41dd-113">If you already know this, skip to step 3.</span></span>

    ```ps
    # Find packages containing the keyword "elmah"
    Find-Package elmah
    ```

1. <span data-ttu-id="c41dd-114">Führen Sie den Befehl installieren:</span><span class="sxs-lookup"><span data-stu-id="c41dd-114">Run the install command:</span></span>

    ```ps
    # Install the Elmah package to the project named MyProject.
    Install-Package Elmah -ProjectName MyProject
    ```

> [!Important]
> <span data-ttu-id="c41dd-115">Alle Vorgänge, die in der Konsole verfügbaren können auch dazu die [NuGet CLI](../tools/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="c41dd-115">All operations that are available in the console can also be done with the [NuGet CLI](../tools/nuget-exe-cli-reference.md).</span></span> <span data-ttu-id="c41dd-116">Allerdings Konsolenbefehle innerhalb des Kontexts des Visual Studio und eine gespeicherte Projektmappe ausgeführt werden und häufig mehr als die entsprechenden CLI-Befehlen zu erreichen.</span><span class="sxs-lookup"><span data-stu-id="c41dd-116">However, console commands operate within the context of Visual Studio and a saved project/solution and often accomplish more than their equivalent CLI commands.</span></span> <span data-ttu-id="c41dd-117">Beispielsweise fügt die Installation eines Pakets über die Konsole einen Verweis auf das Projekt, während der CLI-Befehl nicht der Fall ist.</span><span class="sxs-lookup"><span data-stu-id="c41dd-117">For example, installing a package through the console adds a reference to the project whereas the CLI command does not.</span></span> <span data-ttu-id="c41dd-118">Aus diesem Grund bevorzugen Entwickler in Visual Studio in der Regel mithilfe der CLI-Konsole.</span><span class="sxs-lookup"><span data-stu-id="c41dd-118">For this reason, developers working in Visual Studio typically prefer using the console to the CLI.</span></span>

> [!Tip]
> <span data-ttu-id="c41dd-119">Viele Konsole Vorgänge hängen davon ab, müssen eine Projektmappe mit einem bekannten Pfadnamen in Visual Studio geöffnet.</span><span class="sxs-lookup"><span data-stu-id="c41dd-119">Many console operations depend on having a solution opened in Visual Studio with a known path name.</span></span> <span data-ttu-id="c41dd-120">Wenn Sie eine nicht gespeicherte oder keine Lösung haben, sehen Sie den Fehler, "Projektmappe ist nicht geöffnet oder nicht gespeichert.</span><span class="sxs-lookup"><span data-stu-id="c41dd-120">If you have an unsaved solution, or no solution, you can see the error, "Solution is not opened or not saved.</span></span> <span data-ttu-id="c41dd-121">Stellen Sie sicher, dass Sie über eine geöffnete und gespeicherte Projektmappe verfügen."</span><span class="sxs-lookup"><span data-stu-id="c41dd-121">Please ensure you have an open and saved solution."</span></span> <span data-ttu-id="c41dd-122">Dies gibt an, dass die Konsole Projektmappenordner bestimmen kann.</span><span class="sxs-lookup"><span data-stu-id="c41dd-122">This indicates that the console cannot determine the solution folder.</span></span> <span data-ttu-id="c41dd-123">Eine nicht gespeicherte Projektmappe speichern oder zu erstellen und speichern eine Projektmappe aus, falls Sie noch keins besitzen öffnen, sollte den Fehler zu beheben.</span><span class="sxs-lookup"><span data-stu-id="c41dd-123">Saving an unsaved solution, or creating and saving a solution if you don't have one open, should correct the error.</span></span>

## <a name="opening-the-console-and-console-controls"></a><span data-ttu-id="c41dd-124">Öffnen der Konsole und die Konsole-Steuerelemente</span><span class="sxs-lookup"><span data-stu-id="c41dd-124">Opening the console and console controls</span></span>

1. <span data-ttu-id="c41dd-125">Öffnen Sie die Konsole in Visual Studio mithilfe der **Extras > NuGet-Paket-Manager > Package Manager Console** Befehl.</span><span class="sxs-lookup"><span data-stu-id="c41dd-125">Open the console in Visual Studio using the **Tools > NuGet Package Manager > Package Manager Console** command.</span></span> <span data-ttu-id="c41dd-126">Die Konsole ist ein Visual Studio-Fenster, das angeordnet und jedoch beliebig positioniert werden kann (siehe [Anpassen der Fensterlayouts in Visual Studio](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).</span><span class="sxs-lookup"><span data-stu-id="c41dd-126">The console is a Visual Studio window that can be arranged and positioned however you like (see [Customize window layouts in Visual Studio](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).</span></span>

1. <span data-ttu-id="c41dd-127">Standardmäßig ausgeführt werden Konsolenbefehle an einen bestimmten Paketquelle und das Projekt als Gruppe im Steuerelement am oberen Rand des Fensters:</span><span class="sxs-lookup"><span data-stu-id="c41dd-127">By default, console commands operate against a specific package source and project as set in the control at the top of the window:</span></span>

    ![Paket-Manager-Konsole-Steuerelemente für die Paketquelle und Projekt](media/PackageManagerConsoleControls1.png)

1. <span data-ttu-id="c41dd-129">Bei der Auswahl einer anderen Paketquelle und/oder Projekt geändert Diese Standardwerte für nachfolgende Befehle.</span><span class="sxs-lookup"><span data-stu-id="c41dd-129">Selecting a different package source and/or project changes those defaults for subsequent commands.</span></span> <span data-ttu-id="c41dd-130">Um einem diese Einstellungen ohne Ändern der Standardwerte, die meisten Befehle unterstützt `-Source` und `-ProjectName` Optionen.</span><span class="sxs-lookup"><span data-stu-id="c41dd-130">To overrride these settings without changing the defaults, most commands support `-Source` and `-ProjectName` options.</span></span>

1. <span data-ttu-id="c41dd-131">Wählen Sie das Zahnradsymbol zum Verwalten von Paketquellen überein.</span><span class="sxs-lookup"><span data-stu-id="c41dd-131">To manage package sources, select the gear icon.</span></span> <span data-ttu-id="c41dd-132">Dies ist eine Verknüpfung zu den **Tools > Optionen > NuGet-Paket-Manager > Paketquellen** wie beschrieben auf das Dialogfeld die [Paket-Manager-UI](Package-Manager-UI.md#package-sources) Seite.</span><span class="sxs-lookup"><span data-stu-id="c41dd-132">This is a shortcut to the **Tools > Options > NuGet Package Manager > Package Sources** dialog box as described on the [Package Manager UI](Package-Manager-UI.md#package-sources) page.</span></span> <span data-ttu-id="c41dd-133">Das Steuerelement rechts neben dem Projekt Selektor löscht, der Konsole Inhalt:</span><span class="sxs-lookup"><span data-stu-id="c41dd-133">Also, the control to the right of the project selector clears the console's contents:</span></span>

    ![Einstellungen für die Paket-Manager-Konsole und Steuerelemente löschen](media/PackageManagerConsoleControls2.png)

1. <span data-ttu-id="c41dd-135">Die Schaltfläche ganz rechts unterbricht einen lang ausgeführte Befehl.</span><span class="sxs-lookup"><span data-stu-id="c41dd-135">The rightmost button interrupts a long-running command.</span></span> <span data-ttu-id="c41dd-136">Z. B. Ausführung `Get-Package -ListAvailable -PageSize 500` Listet die Top-500-Pakete in der Quelle (z. B. nuget.org), die einige Zeit in Anspruch nehmen kann.</span><span class="sxs-lookup"><span data-stu-id="c41dd-136">For example, running `Get-Package -ListAvailable -PageSize 500` lists the top 500 packages on the default source (such as nuget.org), which could take several minutes to run.</span></span>

    ![Paket-Manager-Konsole beenden-Steuerelement](media/PackageManagerConsoleControls3.png)

## <a name="installing-a-package"></a><span data-ttu-id="c41dd-138">Installieren eines Pakets</span><span class="sxs-lookup"><span data-stu-id="c41dd-138">Installing a package</span></span>

```ps
# Add the Elmah package to the default project as specified in the console's project selector
Install-Package Elmah

# Add the Elmah package to a project named UtilitiesLib that is not the default
Install-Package Elmah -ProjectName UtilitiesLib
```

<span data-ttu-id="c41dd-139">Finden Sie unter [Install-Package](../tools/ps-ref-install-package.md).</span><span class="sxs-lookup"><span data-stu-id="c41dd-139">See [Install-Package](../tools/ps-ref-install-package.md).</span></span>

<span data-ttu-id="c41dd-140">Installieren eines Pakets werden die folgenden Aktionen ausgeführt:</span><span class="sxs-lookup"><span data-stu-id="c41dd-140">Installing a package performs the following actions:</span></span>

- <span data-ttu-id="c41dd-141">Zeigt geltenden Lizenzbedingungen in das Konsolenfenster mit impliziten Vereinbarung an.</span><span class="sxs-lookup"><span data-stu-id="c41dd-141">Displays applicable license terms in the console window with implied agreement.</span></span> <span data-ttu-id="c41dd-142">Wenn Sie nicht den Bedingungen zustimmen, sollten Sie das Paket sofort deinstallieren.</span><span class="sxs-lookup"><span data-stu-id="c41dd-142">If you do not agree to the terms, you should uninstall the package immediately.</span></span>
- <span data-ttu-id="c41dd-143">Fügt einen Verweis auf das Projekt in dem Verweis-Format verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="c41dd-143">Adds a reference to the project in whatever reference format is in use.</span></span> <span data-ttu-id="c41dd-144">Verweise werden anschließend im Projektmappen-Explorer und die entsprechenden Verweis Formatdatei angezeigt.</span><span class="sxs-lookup"><span data-stu-id="c41dd-144">References subsequently appear in Solution Explorer and the applicable reference format file.</span></span> <span data-ttu-id="c41dd-145">Beachten Sie jedoch, dass mit PackageReference, Sie zum Speichern des Projekts, um die Änderungen in der Projektdatei direkt anzuzeigen müssen.</span><span class="sxs-lookup"><span data-stu-id="c41dd-145">Note, however, that with PackageReference, you need to save the project to see the changes in the project file directly.</span></span>
- <span data-ttu-id="c41dd-146">Speichert das Paket an:</span><span class="sxs-lookup"><span data-stu-id="c41dd-146">Caches the package:</span></span>
  - <span data-ttu-id="c41dd-147">PackageReference: Paket in zwischengespeichert `%USERPROFILE%\.nuget\packages` und die Sperre Datei, d. h. `project.assets.json` wird aktualisiert.</span><span class="sxs-lookup"><span data-stu-id="c41dd-147">PackageReference:  package is cached at `%USERPROFILE%\.nuget\packages` and the lock file i.e. `project.assets.json` is updated.</span></span>
  - <span data-ttu-id="c41dd-148">`packages.config`: erstellt eine `packages` Ordner am Stamm-Lösung und kopiert das Paket in einen Unterordner darin enthaltenen Dateien.</span><span class="sxs-lookup"><span data-stu-id="c41dd-148">`packages.config`: creates a `packages` folder at the solution root and copies the package files into a subfolder within it.</span></span> <span data-ttu-id="c41dd-149">Die `package.config` Datei aktualisiert wird.</span><span class="sxs-lookup"><span data-stu-id="c41dd-149">The `package.config` file is updated.</span></span>
- <span data-ttu-id="c41dd-150">Updates `app.config` und/oder `web.config` Wenn vom Paket verwendete [Source "und" Config-Datei Transformationen](../create-packages/source-and-config-file-transformations.md).</span><span class="sxs-lookup"><span data-stu-id="c41dd-150">Updates `app.config` and/or `web.config` if the package uses [source and config file transformations](../create-packages/source-and-config-file-transformations.md).</span></span>
- <span data-ttu-id="c41dd-151">Alle Abhängigkeiten installiert, sofern nicht bereits im Projekt vorhanden.</span><span class="sxs-lookup"><span data-stu-id="c41dd-151">Installs any dependencies if not already present in the project.</span></span> <span data-ttu-id="c41dd-152">Dies kann die Paketversionen im Prozess aktualisieren, wie in beschrieben [Abhängigkeit Auflösung](../consume-packages/dependency-resolution.md).</span><span class="sxs-lookup"><span data-stu-id="c41dd-152">This might update package versions in the process, as described in [Dependency Resolution](../consume-packages/dependency-resolution.md).</span></span>
- <span data-ttu-id="c41dd-153">Infodatei für das Paket, falls verfügbar, in einem Visual Studio-Fenster angezeigt.</span><span class="sxs-lookup"><span data-stu-id="c41dd-153">Displays the package's readme file, if available, in a Visual Studio window.</span></span>

> [!Tip]
> <span data-ttu-id="c41dd-154">Einer der Hauptvorteile der Installation von Paketen mit dem `Install-Package` Befehl in der Konsole ist, einen Verweis auf das Projekt addiert wird, als ob Sie die Paket-Manager-UI verwendet.</span><span class="sxs-lookup"><span data-stu-id="c41dd-154">One of the primary advantages of installing packages with the `Install-Package` command in the console is that adds a reference to the project just as if you used the Package Manager UI.</span></span> <span data-ttu-id="c41dd-155">Im Gegensatz dazu die `nuget install` CLI-Befehl nur das Paket wird heruntergeladen und nicht automatisch einen Verweis hinzu.</span><span class="sxs-lookup"><span data-stu-id="c41dd-155">In contrast, the `nuget install` CLI command only downloads the package and does not automatically add a reference.</span></span>

## <a name="uninstalling-a-package"></a><span data-ttu-id="c41dd-156">Deinstallieren eines Pakets</span><span class="sxs-lookup"><span data-stu-id="c41dd-156">Uninstalling a package</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```

<span data-ttu-id="c41dd-157">Finden Sie unter [Uninstall-Package](../tools/ps-ref-uninstall-package.md).</span><span class="sxs-lookup"><span data-stu-id="c41dd-157">See [Uninstall-Package](../tools/ps-ref-uninstall-package.md).</span></span> <span data-ttu-id="c41dd-158">Verwendung [Get-Package](../tools/ps-ref-get-package.md) sehen alle Pakete, die derzeit im Standardprojekt installiert, wenn Sie einen Bezeichner zu suchen müssen.</span><span class="sxs-lookup"><span data-stu-id="c41dd-158">Use [Get-Package](../tools/ps-ref-get-package.md) to see all packages currently installed in the default project if you need to find an identifier.</span></span>

<span data-ttu-id="c41dd-159">Deinstallieren ein Paket führt die folgenden Aktionen aus:</span><span class="sxs-lookup"><span data-stu-id="c41dd-159">Uninstalling a package performs the following actions:</span></span>

- <span data-ttu-id="c41dd-160">Entfernt Verweise auf das Paket aus dem Projekt (und dem Verweis-Format verwendet wird).</span><span class="sxs-lookup"><span data-stu-id="c41dd-160">Removes references to the package from the project (and whatever reference format is in use).</span></span> <span data-ttu-id="c41dd-161">Verweise werden nicht mehr im Projektmappen-Explorer angezeigt.</span><span class="sxs-lookup"><span data-stu-id="c41dd-161">References no longer appear in Solution Explorer.</span></span> <span data-ttu-id="c41dd-162">(Zum Neuerstellen des Projekts, um es daraus sehen müssen möglicherweise die **"bin"** Ordner.)</span><span class="sxs-lookup"><span data-stu-id="c41dd-162">(You might need to rebuild the project to see it removed from the **Bin** folder.)</span></span>
- <span data-ttu-id="c41dd-163">Kehrt alle Änderungen an `app.config` oder `web.config` wann das Paket wurde installiert.</span><span class="sxs-lookup"><span data-stu-id="c41dd-163">Reverses any changes made to `app.config` or `web.config` when the package was installed.</span></span>
- <span data-ttu-id="c41dd-164">Entfernt einen zuvor installierten Abhängigkeiten, wenn keine verbleibenden Pakete solcher Abhängigkeiten verwenden.</span><span class="sxs-lookup"><span data-stu-id="c41dd-164">Removes previously-installed dependencies if no remaining packages use those dependencies.</span></span>

> [!Tip]
> <span data-ttu-id="c41dd-165">Wie `Install-Package`, `Uninstall-Package` Befehl hat den Vorteil der Verwaltung von Verweise im Projekt, im Gegensatz zu den `nuget uninstall` CLI-Befehl.</span><span class="sxs-lookup"><span data-stu-id="c41dd-165">Like `Install-Package`, the `Uninstall-Package` command has the benefit of managing references in the project, unlike the `nuget uninstall` CLI command.</span></span>

## <a name="updating-a-package"></a><span data-ttu-id="c41dd-166">Aktualisieren eines Pakets</span><span class="sxs-lookup"><span data-stu-id="c41dd-166">Updating a package</span></span>

```ps
# Checks if there are newer versions available for any installed packages
Get-Package -updates

# Updates a specific package using its identifier, in this case jQuery
Update-Package jQuery

# Update all packages in the project named MyProject (as it appears in Solution Explorer)
Update-Package -ProjectName MyProject

# Update all packages in the solution
Update-Package
```

<span data-ttu-id="c41dd-167">Finden Sie unter [Get-Package](../tools/ps-ref-get-package.md) und [Update-Paket](../tools/ps-ref-update-package.md)</span><span class="sxs-lookup"><span data-stu-id="c41dd-167">See [Get-Package](../tools/ps-ref-get-package.md) and [Update-Package](../tools/ps-ref-update-package.md)</span></span>

## <a name="finding-a-package"></a><span data-ttu-id="c41dd-168">Suchen ein Paket</span><span class="sxs-lookup"><span data-stu-id="c41dd-168">Finding a package</span></span>

```ps
# Find packages containing keywords
Find-Package elmah
Find-Package logging

# List packages whose ID begins with Elmah
Find-Package Elmah -StartWith

# By default, Get-Package returns a list of 20 packages; use -First to show more
Find-Package logging -First 100

# List all versions of the package with the ID of "jquery"
Find-Package jquery -AllVersions -ExactMatch
```

<span data-ttu-id="c41dd-169">Finden Sie unter [Find-Package](../tools/ps-ref-find-package.md).</span><span class="sxs-lookup"><span data-stu-id="c41dd-169">See [Find-Package](../tools/ps-ref-find-package.md).</span></span> <span data-ttu-id="c41dd-170">Verwenden Sie in Visual Studio 2013 und früheren [Get-Package](../tools/ps-ref-get-package.md) stattdessen.</span><span class="sxs-lookup"><span data-stu-id="c41dd-170">In Visual Studio 2013 and earlier, use [Get-Package](../tools/ps-ref-get-package.md) instead.</span></span>

## <a name="availability-of-the-console"></a><span data-ttu-id="c41dd-171">Verfügbarkeit der Konsole</span><span class="sxs-lookup"><span data-stu-id="c41dd-171">Availability of the console</span></span>

<span data-ttu-id="c41dd-172">In Visual Studio 2017 werden NuGet und NuGet-Paket-Manager automatisch installiert, wenn Sie auswählen. NET-bezogenen Arbeitslasten; Sie können auch installieren sie einzeln durch Überprüfen der **Einzelkomponenten > Tools Code > NuGet-Paket-Manager** -Option in der 2017 von Visual Studio-Installer.</span><span class="sxs-lookup"><span data-stu-id="c41dd-172">In Visual Studio 2017, NuGet and the NuGet Package Manager are automatically installed when you select any .NET-related workloads; you can also install it individually by checking the **Individual components > Code tools > NuGet package manager** option in the Visual Studio 2017 installer.</span></span>

<span data-ttu-id="c41dd-173">Überprüfen Sie auch, wenn Sie den NuGet-Paket-Manager in Visual Studio 2015 und früheren Versionen nicht vorhanden sind, **Tools > Erweiterungen und Updates...**  und suchen Sie nach der Erweiterung von NuGet-Paket-Manager.</span><span class="sxs-lookup"><span data-stu-id="c41dd-173">Also, if you're missing the NuGet Package Manager in Visual Studio 2015 and earlier, check **Tools > Extensions and Updates...** and search for the NuGet Package Manager extension.</span></span> <span data-ttu-id="c41dd-174">Wenn Sie nicht das Installationsprogramm für Erweiterungen in Visual Studio verwenden möchten, können Sie die Erweiterung direkt von herunterladen [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="c41dd-174">If you're unable to use the extensions installer in Visual Studio, you can download the extension directly from [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span></span>

<span data-ttu-id="c41dd-175">Der Paket-Manager-Konsole ist zurzeit nicht verfügbar in Visual Studio für Mac.</span><span class="sxs-lookup"><span data-stu-id="c41dd-175">The Package Manager Console is not presently available with Visual Studio for Mac.</span></span> <span data-ttu-id="c41dd-176">Allerdings stehen die entsprechenden Befehle zur Verfügung, über die [NuGet CLI](nuget-exe-CLI-reference.md).</span><span class="sxs-lookup"><span data-stu-id="c41dd-176">The equivalent commands, however, are available through the [NuGet CLI](nuget-exe-CLI-reference.md).</span></span> <span data-ttu-id="c41dd-177">Visual Studio für Mac besitzt eine Benutzeroberfläche zum Verwalten von NuGet-Paketen.</span><span class="sxs-lookup"><span data-stu-id="c41dd-177">Visual Studio for Mac does have a UI for managing NuGet packages.</span></span> <span data-ttu-id="c41dd-178">Finden Sie unter [einschließlich eines NuGet-Paket im Projekt](/visualstudio/mac/nuget-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="c41dd-178">See [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span>

<span data-ttu-id="c41dd-179">Der Paket-Manager-Konsole ist nicht mit Visual Studio-Code enthalten.</span><span class="sxs-lookup"><span data-stu-id="c41dd-179">The Package Manager Console is not included with Visual Studio Code.</span></span>

## <a name="extending-the-package-manager-console"></a><span data-ttu-id="c41dd-180">Erweitern Sie die Paket-Manager-Konsole</span><span class="sxs-lookup"><span data-stu-id="c41dd-180">Extending the Package Manager Console</span></span>

<span data-ttu-id="c41dd-181">Einige Pakete installieren Sie neue Befehle für die Konsole.</span><span class="sxs-lookup"><span data-stu-id="c41dd-181">Some packages install new commands for the console.</span></span> <span data-ttu-id="c41dd-182">Beispielsweise `MvcScaffolding` erstellt Befehle wie `Scaffold` unten, wodurch die ASP.NET MVC-Controller und Ansichten generiert:</span><span class="sxs-lookup"><span data-stu-id="c41dd-182">For example, `MvcScaffolding` creates commands like `Scaffold` shown below, which generates ASP.NET MVC controllers and views:</span></span>

![Installieren und Verwenden von MvcScaffold](media/PackageManagerConsoleInstall.png)

## <a name="setting-up-a-nuget-powershell-profile"></a><span data-ttu-id="c41dd-184">Einrichten eines NuGet-PowerShell-Profils</span><span class="sxs-lookup"><span data-stu-id="c41dd-184">Setting up a NuGet PowerShell profile</span></span>

<span data-ttu-id="c41dd-185">Ein PowerShell-Profil können Sie häufig verwendete Befehle zur Verfügung stellen, wo Sie PowerShell verwenden.</span><span class="sxs-lookup"><span data-stu-id="c41dd-185">A PowerShell profile lets you make commonly-used commands available wherever you use PowerShell.</span></span> <span data-ttu-id="c41dd-186">NuGet unterstützt ein NuGet-spezifischen Profil, in der Regel am folgenden Speicherort gefunden:</span><span class="sxs-lookup"><span data-stu-id="c41dd-186">NuGet supports a NuGet-specific profile typically found at the following location:</span></span>

    %UserProfile%\Documents\WindowsPowerShell\NuGet_profile.ps1

<span data-ttu-id="c41dd-187">Um das Profil zu suchen, geben Sie `$profile` in der Konsole:</span><span class="sxs-lookup"><span data-stu-id="c41dd-187">To find the profile, type `$profile` in the console:</span></span>

```ps
$profile
C:\Users\<user>\Documents\WindowsPowerShell\NuGet_profile.ps1
```

<span data-ttu-id="c41dd-188">Weitere Informationen finden Sie unter [Windows PowerShell-Profile](https://technet.microsoft.com/library/bb613488.aspx).</span><span class="sxs-lookup"><span data-stu-id="c41dd-188">For more details, refer to [Windows PowerShell Profiles](https://technet.microsoft.com/library/bb613488.aspx).</span></span>

## <a name="using-the-nugetexe-cli-in-the-console"></a><span data-ttu-id="c41dd-189">Mithilfe der CLI nuget.exe in der Konsole</span><span class="sxs-lookup"><span data-stu-id="c41dd-189">Using the nuget.exe CLI in the console</span></span>

<span data-ttu-id="c41dd-190">Vornehmen der [ `nuget.exe` CLI](nuget-exe-CLI-Reference.md) zur Verfügung, in der Paket-Manager-Konsole installieren der [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) eines Pakets aus der Konsole:</span><span class="sxs-lookup"><span data-stu-id="c41dd-190">To make the [`nuget.exe` CLI](nuget-exe-CLI-Reference.md) available in the Package Manager Console, install the [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) package from the console:</span></span>

```ps
# Other versions are available, see http://www.nuget.org/packages/NuGet.CommandLine/
Install-Package NuGet.CommandLine -Version 4.4.1
```
