---
title: NuGet-Paket-Manager-Konsole Handbuch | Microsoft Docs
author: kraigb
hms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 2b92b119-6861-406c-82af-9d739af230e4
f1_keywords: vs.nuget.packagemanager.console
description: "Anweisungen für die Verwendung der NuGet-Paket-Manager-Konsole in Visual Studio zum Arbeiten mit Paketen."
keywords: NuGet-Paket-Manager-Konsole, NuGet Powershell NuGet-Pakete verwalten
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: b8f1df23d1a43412868c14e508ee5221d48dcc7c
ms.sourcegitcommit: bdcd2046b1b187d8b59716b9571142c02181c8fb
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/10/2018
---
# <a name="package-manager-console"></a><span data-ttu-id="fea67-104">Paket-Manager-Konsole</span><span class="sxs-lookup"><span data-stu-id="fea67-104">Package Manager Console</span></span>

<span data-ttu-id="fea67-105">Die NuGet-Paket-Manager-Konsole wird in Visual Studio unter Windows 2012 und höher integriert.</span><span class="sxs-lookup"><span data-stu-id="fea67-105">The NuGet Package Manager Console is built into Visual Studio on Windows version 2012 and later.</span></span> <span data-ttu-id="fea67-106">(Es ist nicht in Visual Studio für Mac oder Visual Studio-Code enthalten.)</span><span class="sxs-lookup"><span data-stu-id="fea67-106">(It is not included with Visual Studio for Mac or Visual Studio Code.)</span></span>

<span data-ttu-id="fea67-107">Die Konsole können Sie verwenden [NuGet PowerShell-Befehle](../tools/powershell-reference.md) finden, installieren, deinstallieren und Aktualisieren von NuGet-Pakete.</span><span class="sxs-lookup"><span data-stu-id="fea67-107">The console lets you use [NuGet PowerShell commands](../tools/powershell-reference.md) to find, install, uninstall, and update NuGet packages.</span></span> <span data-ttu-id="fea67-108">Mithilfe der Konsole ist erforderlich, in Fällen, in dem das Paket-Manager-UI keine Möglichkeit zum Ausführen eines Vorgangs eingeben.</span><span class="sxs-lookup"><span data-stu-id="fea67-108">Using the console is necessary in cases where the Package Manager UI does not provide a way to perform an operation.</span></span>

<span data-ttu-id="fea67-109">Suchen und Installieren eines Pakets erfolgt z. B. mit drei einfachen Schritten:</span><span class="sxs-lookup"><span data-stu-id="fea67-109">For example, finding and installing a package is done with three easy steps:</span></span>

1. <span data-ttu-id="fea67-110">Öffnen Sie das Projekt/die Projektmappe in Visual Studio, und öffnen Sie die Konsole unter Verwendung der **Extras > NuGet-Paket-Manager > Package Manager Console** Befehl.</span><span class="sxs-lookup"><span data-stu-id="fea67-110">Open the project/solution in Visual Studio, and open the console using the **Tools > NuGet Package Manager > Package Manager Console** command.</span></span>

1. <span data-ttu-id="fea67-111">Suchen Sie das Paket, das Sie installieren möchten.</span><span class="sxs-lookup"><span data-stu-id="fea67-111">Find the package you want to install.</span></span> <span data-ttu-id="fea67-112">Fahren Sie mit Schritt 3 fort, wenn Sie dies bereits kennen.</span><span class="sxs-lookup"><span data-stu-id="fea67-112">If you already know this, skip to step 3.</span></span>

    ```ps
    # Find packages containing the keyword "elmah"
    Find-Package elmah
    ```

1. <span data-ttu-id="fea67-113">Führen Sie den Befehl installieren:</span><span class="sxs-lookup"><span data-stu-id="fea67-113">Run the install command:</span></span>

    ```ps
    # Install the Elmah package to the project named MyProject.
    Install-Package Elmah -ProjectName MyProject
    ```

<span data-ttu-id="fea67-114">In diesem Thema:</span><span class="sxs-lookup"><span data-stu-id="fea67-114">In this topic:</span></span>

- [<span data-ttu-id="fea67-115">Öffnen der Konsole</span><span class="sxs-lookup"><span data-stu-id="fea67-115">Opening the console</span></span>](#opening-the-console-and-console-controls)
- [<span data-ttu-id="fea67-116">Installieren eines Pakets</span><span class="sxs-lookup"><span data-stu-id="fea67-116">Installing a package</span></span>](#installing-a-package)
- [<span data-ttu-id="fea67-117">Deinstallieren eines Pakets</span><span class="sxs-lookup"><span data-stu-id="fea67-117">Uninstalling a package</span></span>](#uninstalling-a-package)
- [<span data-ttu-id="fea67-118">Suchen ein Paket</span><span class="sxs-lookup"><span data-stu-id="fea67-118">Finding a package</span></span>](#finding-a-package)
- [<span data-ttu-id="fea67-119">Aktualisieren eines Pakets</span><span class="sxs-lookup"><span data-stu-id="fea67-119">Updating a package</span></span>](#updating-a-package)
- [<span data-ttu-id="fea67-120">Verfügbarkeit der Konsole</span><span class="sxs-lookup"><span data-stu-id="fea67-120">Availability of the console</span></span>](#availability-of-the-console)
- [<span data-ttu-id="fea67-121">Erweitern Sie die Paket-Manager-Konsole</span><span class="sxs-lookup"><span data-stu-id="fea67-121">Extending the Package Manager Console</span></span>](#extending-the-package-manager-console)
- [<span data-ttu-id="fea67-122">Einrichten eines NuGet-PowerShell-Profils</span><span class="sxs-lookup"><span data-stu-id="fea67-122">Setting up a NuGet PowerShell profile</span></span>](#setting-up-a-nuget-powershell-profile)

> [!Important]
> <span data-ttu-id="fea67-123">Alle Vorgänge, die in der Konsole verfügbaren können auch dazu die [NuGet CLI](../tools/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="fea67-123">All operations that are available in the console can also be done with the [NuGet CLI](../tools/nuget-exe-cli-reference.md).</span></span> <span data-ttu-id="fea67-124">Allerdings Konsolenbefehle innerhalb des Kontexts des Visual Studio und eine gespeicherte Projektmappe ausgeführt werden und häufig mehr als die entsprechenden CLI-Befehlen zu erreichen.</span><span class="sxs-lookup"><span data-stu-id="fea67-124">However, console commands operate within the context of Visual Studio and a saved project/solution and often accomplish more than their equivalent CLI commands.</span></span> <span data-ttu-id="fea67-125">Beispielsweise fügt die Installation eines Pakets über die Konsole einen Verweis auf das Projekt, während der CLI-Befehl nicht der Fall ist.</span><span class="sxs-lookup"><span data-stu-id="fea67-125">For example, installing a package through the console adds a reference to the project whereas the CLI command does not.</span></span> <span data-ttu-id="fea67-126">Aus diesem Grund bevorzugen Entwickler in Visual Studio in der Regel mithilfe der CLI-Konsole.</span><span class="sxs-lookup"><span data-stu-id="fea67-126">For this reason, developers working in Visual Studio typically prefer using the console to the CLI.</span></span>

> [!Tip]
> <span data-ttu-id="fea67-127">Viele Konsole Vorgänge hängen davon ab, müssen eine Projektmappe mit einem bekannten Pfadnamen in Visual Studio geöffnet.</span><span class="sxs-lookup"><span data-stu-id="fea67-127">Many console operations depend on having a solution opened in Visual Studio with a known path name.</span></span> <span data-ttu-id="fea67-128">Wenn Sie eine nicht gespeicherte oder keine Lösung haben, sehen Sie den Fehler, "Projektmappe ist nicht geöffnet oder nicht gespeichert.</span><span class="sxs-lookup"><span data-stu-id="fea67-128">If you have an unsaved solution, or no solution, you can see the error, "Solution is not opened or not saved.</span></span> <span data-ttu-id="fea67-129">Stellen Sie sicher, dass Sie über eine geöffnete und gespeicherte Projektmappe verfügen."</span><span class="sxs-lookup"><span data-stu-id="fea67-129">Please ensure you have an open and saved solution."</span></span> <span data-ttu-id="fea67-130">Dies gibt an, dass die Konsole Projektmappenordner bestimmen kann.</span><span class="sxs-lookup"><span data-stu-id="fea67-130">This indicates that the console cannot determine the solution folder.</span></span> <span data-ttu-id="fea67-131">Eine nicht gespeicherte Projektmappe speichern oder zu erstellen und speichern eine Projektmappe aus, falls Sie noch keins besitzen öffnen, sollte den Fehler zu beheben.</span><span class="sxs-lookup"><span data-stu-id="fea67-131">Saving an unsaved solution, or creating and saving a solution if you don't have one open, should correct the error.</span></span>

## <a name="opening-the-console-and-console-controls"></a><span data-ttu-id="fea67-132">Öffnen der Konsole und die Konsole-Steuerelemente</span><span class="sxs-lookup"><span data-stu-id="fea67-132">Opening the console and console controls</span></span>

1. <span data-ttu-id="fea67-133">Öffnen Sie die Konsole in Visual Studio mithilfe der **Extras > NuGet-Paket-Manager > Package Manager Console** Befehl.</span><span class="sxs-lookup"><span data-stu-id="fea67-133">Open the console in Visual Studio using the **Tools > NuGet Package Manager > Package Manager Console** command.</span></span> <span data-ttu-id="fea67-134">Die Konsole ist ein Visual Studio-Fenster, das angeordnet und jedoch beliebig positioniert werden kann (siehe [Anpassen der Fensterlayouts in Visual Studio](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).</span><span class="sxs-lookup"><span data-stu-id="fea67-134">The console is a Visual Studio window that can be arranged and positioned however you like (see [Customize window layouts in Visual Studio](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).</span></span>

1. <span data-ttu-id="fea67-135">Standardmäßig ausgeführt werden Konsolenbefehle an einen bestimmten Paketquelle und das Projekt als Gruppe im Steuerelement am oberen Rand des Fensters:</span><span class="sxs-lookup"><span data-stu-id="fea67-135">By default, console commands operate against a specific package source and project as set in the control at the top of the window:</span></span>

    ![Paket-Manager-Konsole-Steuerelemente für die Paketquelle und Projekt](media/PackageManagerConsoleControls1.png)

1. <span data-ttu-id="fea67-137">Bei der Auswahl einer anderen Paketquelle und/oder Projekt geändert Diese Standardwerte für nachfolgende Befehle.</span><span class="sxs-lookup"><span data-stu-id="fea67-137">Selecting a different package source and/or project changes those defaults for subsequent commands.</span></span> <span data-ttu-id="fea67-138">Um einem diese Einstellungen ohne Ändern der Standardwerte, die meisten Befehle unterstützt `-Source` und `-ProjectName` Optionen.</span><span class="sxs-lookup"><span data-stu-id="fea67-138">To overrride these settings without changing the defaults, most commands support `-Source` and `-ProjectName` options.</span></span>

1. <span data-ttu-id="fea67-139">Wählen Sie das Zahnradsymbol zum Verwalten von Paketquellen überein.</span><span class="sxs-lookup"><span data-stu-id="fea67-139">To manage package sources, select the gear icon.</span></span> <span data-ttu-id="fea67-140">Dies ist eine Verknüpfung zu den **Tools > Optionen > NuGet-Paket-Manager > Paketquellen** wie beschrieben auf das Dialogfeld die [Paket-Manager-UI](Package-Manager-UI.md#package-sources) Seite.</span><span class="sxs-lookup"><span data-stu-id="fea67-140">This is a shortcut to the **Tools > Options > NuGet Package Manager > Package Sources** dialog box as described on the [Package Manager UI](Package-Manager-UI.md#package-sources) page.</span></span> <span data-ttu-id="fea67-141">Das Steuerelement rechts neben dem Projekt Selektor löscht, der Konsole Inhalt:</span><span class="sxs-lookup"><span data-stu-id="fea67-141">Also, the control to the right of the project selector clears the console's contents:</span></span>

    ![Einstellungen für die Paket-Manager-Konsole und Steuerelemente löschen](media/PackageManagerConsoleControls2.png)

1. <span data-ttu-id="fea67-143">Die Schaltfläche ganz rechts unterbricht einen lang ausgeführte Befehl.</span><span class="sxs-lookup"><span data-stu-id="fea67-143">The rightmost button interrupts a long-running command.</span></span> <span data-ttu-id="fea67-144">Z. B. Ausführung `Get-Package -ListAvailable -PageSize 500` Listet die Top-500-Pakete in der Quelle (z. B. nuget.org), die einige Zeit in Anspruch nehmen kann.</span><span class="sxs-lookup"><span data-stu-id="fea67-144">For example, running `Get-Package -ListAvailable -PageSize 500` lists the top 500 packages on the default source (such as nuget.org), which could take several minutes to run.</span></span>

    ![Paket-Manager-Konsole beenden-Steuerelement](media/PackageManagerConsoleControls3.png)

## <a name="installing-a-package"></a><span data-ttu-id="fea67-146">Installieren eines Pakets</span><span class="sxs-lookup"><span data-stu-id="fea67-146">Installing a package</span></span>

```ps
# Add the Elmah package to the default project as specified in the console's project selector
Install-Package Elmah

# Add the Elmah package to a project named UtilitiesLib that is not the default
Install-Package Elmah -ProjectName UtilitiesLib
```

<span data-ttu-id="fea67-147">Finden Sie unter [Install-Package](../tools/ps-ref-install-package.md).</span><span class="sxs-lookup"><span data-stu-id="fea67-147">See [Install-Package](../tools/ps-ref-install-package.md).</span></span>

<span data-ttu-id="fea67-148">Installieren eines Pakets werden die folgenden Aktionen ausgeführt:</span><span class="sxs-lookup"><span data-stu-id="fea67-148">Installing a package performs the following actions:</span></span>

- <span data-ttu-id="fea67-149">Zeigt geltenden Lizenzbedingungen in das Konsolenfenster mit impliziten Vereinbarung an.</span><span class="sxs-lookup"><span data-stu-id="fea67-149">Displays applicable license terms in the console window with implied agreement.</span></span> <span data-ttu-id="fea67-150">Wenn Sie nicht den Bedingungen zustimmen, sollten Sie das Paket sofort deinstallieren.</span><span class="sxs-lookup"><span data-stu-id="fea67-150">If you do not agree to the terms, you should uninstall the package immediately.</span></span>
- <span data-ttu-id="fea67-151">Fügt einen Verweis auf das Projekt in dem Verweis-Format verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="fea67-151">Adds a reference to the project in whatever reference format is in use.</span></span> <span data-ttu-id="fea67-152">Verweise werden anschließend im Projektmappen-Explorer und die entsprechenden Verweis Formatdatei angezeigt.</span><span class="sxs-lookup"><span data-stu-id="fea67-152">References subsequently appear in Solution Explorer and the applicable reference format file.</span></span> <span data-ttu-id="fea67-153">Beachten Sie jedoch, dass mit PackageReference, Sie zum Speichern des Projekts, um die Änderungen in der Projektdatei direkt anzuzeigen müssen.</span><span class="sxs-lookup"><span data-stu-id="fea67-153">Note, however, that with PackageReference, you need to save the project to see the changes in the project file directly.</span></span>
- <span data-ttu-id="fea67-154">Speichert das Paket an:</span><span class="sxs-lookup"><span data-stu-id="fea67-154">Caches the package:</span></span>
    - <span data-ttu-id="fea67-155">PackageReference: Paket in zwischengespeichert `%USERPROFILE%\.nuget\packages` und die Sperre Datei, d. h. `project.assets.json` wird aktualisiert.</span><span class="sxs-lookup"><span data-stu-id="fea67-155">PackageReference:  package is cached at `%USERPROFILE%\.nuget\packages` and the lock file i.e. `project.assets.json` is updated.</span></span>
    - <span data-ttu-id="fea67-156">`packages.config`: erstellt eine `packages` Ordner am Stamm-Lösung und kopiert das Paket in einen Unterordner darin enthaltenen Dateien.</span><span class="sxs-lookup"><span data-stu-id="fea67-156">`packages.config`: creates a `packages` folder at the solution root and copies the package files into a subfolder within it.</span></span> <span data-ttu-id="fea67-157">Die `package.config` Datei aktualisiert wird.</span><span class="sxs-lookup"><span data-stu-id="fea67-157">The `package.config` file is updated.</span></span>
- <span data-ttu-id="fea67-158">Updates `app.config` und/oder `web.config` Wenn vom Paket verwendete [Source "und" Config-Datei Transformationen](../create-packages/source-and-config-file-transformations.md).</span><span class="sxs-lookup"><span data-stu-id="fea67-158">Updates `app.config` and/or `web.config` if the package uses [source and config file transformations](../create-packages/source-and-config-file-transformations.md).</span></span>
- <span data-ttu-id="fea67-159">Alle Abhängigkeiten installiert, sofern nicht bereits im Projekt vorhanden.</span><span class="sxs-lookup"><span data-stu-id="fea67-159">Installs any dependencies if not already present in the project.</span></span> <span data-ttu-id="fea67-160">Dies kann die Paketversionen im Prozess aktualisieren, wie in beschrieben [Abhängigkeit Auflösung](../consume-packages/dependency-resolution.md).</span><span class="sxs-lookup"><span data-stu-id="fea67-160">This might update package versions in the process, as described in [Dependency Resolution](../consume-packages/dependency-resolution.md).</span></span>
- <span data-ttu-id="fea67-161">Infodatei für das Paket, falls verfügbar, in einem Visual Studio-Fenster angezeigt.</span><span class="sxs-lookup"><span data-stu-id="fea67-161">Displays the package's readme file, if available, in a Visual Studio window.</span></span>

> [!Tip]
> <span data-ttu-id="fea67-162">Einer der Hauptvorteile der Installation von Paketen mit dem `Install-Package` Befehl in der Konsole ist, einen Verweis auf das Projekt addiert wird, als ob Sie die Paket-Manager-UI verwendet.</span><span class="sxs-lookup"><span data-stu-id="fea67-162">One of the primary advantages of installing packages with the `Install-Package` command in the console is that adds a reference to the project just as if you used the Package Manager UI.</span></span> <span data-ttu-id="fea67-163">Im Gegensatz dazu die `nuget install` CLI-Befehl nur das Paket wird heruntergeladen und nicht automatisch einen Verweis hinzu.</span><span class="sxs-lookup"><span data-stu-id="fea67-163">In contrast, the `nuget install` CLI command only downloads the package and does not automatically add a reference.</span></span>

## <a name="uninstalling-a-package"></a><span data-ttu-id="fea67-164">Deinstallieren eines Pakets</span><span class="sxs-lookup"><span data-stu-id="fea67-164">Uninstalling a package</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```

<span data-ttu-id="fea67-165">Finden Sie unter [Uninstall-Package](../tools/ps-ref-uninstall-package.md).</span><span class="sxs-lookup"><span data-stu-id="fea67-165">See [Uninstall-Package](../tools/ps-ref-uninstall-package.md).</span></span> <span data-ttu-id="fea67-166">Verwendung [Get-Package](../tools/ps-ref-get-package.md) sehen alle Pakete, die derzeit im Standardprojekt installiert, wenn Sie einen Bezeichner zu suchen müssen.</span><span class="sxs-lookup"><span data-stu-id="fea67-166">Use [Get-Package](../tools/ps-ref-get-package.md) to see all packages currently installed in the default project if you need to find an identifier.</span></span>

<span data-ttu-id="fea67-167">Deinstallieren ein Paket führt die folgenden Aktionen aus:</span><span class="sxs-lookup"><span data-stu-id="fea67-167">Uninstalling a package performs the following actions:</span></span>

- <span data-ttu-id="fea67-168">Entfernt Verweise auf das Paket aus dem Projekt (und dem Verweis-Format verwendet wird).</span><span class="sxs-lookup"><span data-stu-id="fea67-168">Removes references to the package from the project (and whatever reference format is in use).</span></span> <span data-ttu-id="fea67-169">Verweise werden nicht mehr im Projektmappen-Explorer angezeigt.</span><span class="sxs-lookup"><span data-stu-id="fea67-169">References no longer appear in Solution Explorer.</span></span> <span data-ttu-id="fea67-170">(Zum Neuerstellen des Projekts, um es daraus sehen müssen möglicherweise die **"bin"** Ordner.)</span><span class="sxs-lookup"><span data-stu-id="fea67-170">(You might need to rebuild the project to see it removed from the **Bin** folder.)</span></span>
- <span data-ttu-id="fea67-171">Kehrt alle Änderungen an `app.config` oder `web.config` wann das Paket wurde installiert.</span><span class="sxs-lookup"><span data-stu-id="fea67-171">Reverses any changes made to `app.config` or `web.config` when the package was installed.</span></span>
- <span data-ttu-id="fea67-172">Entfernt einen zuvor installierten Abhängigkeiten, wenn keine verbleibenden Pakete solcher Abhängigkeiten verwenden.</span><span class="sxs-lookup"><span data-stu-id="fea67-172">Removes previously-installed dependencies if no remaining packages use those dependencies.</span></span>

> [!Tip]
> <span data-ttu-id="fea67-173">Wie `Install-Package`, `Uninstall-Package` Befehl hat den Vorteil der Verwaltung von Verweise im Projekt, im Gegensatz zu den `nuget uninstall` CLI-Befehl.</span><span class="sxs-lookup"><span data-stu-id="fea67-173">Like `Install-Package`, the `Uninstall-Package` command has the benefit of managing references in the project, unlike the `nuget uninstall` CLI command.</span></span>

## <a name="updating-a-package"></a><span data-ttu-id="fea67-174">Aktualisieren eines Pakets</span><span class="sxs-lookup"><span data-stu-id="fea67-174">Updating a package</span></span>

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

<span data-ttu-id="fea67-175">Finden Sie unter [Get-Package](../tools/ps-ref-get-package.md) und [Update-Paket](../tools/ps-ref-update-package.md)</span><span class="sxs-lookup"><span data-stu-id="fea67-175">See [Get-Package](../tools/ps-ref-get-package.md) and [Update-Package](../tools/ps-ref-update-package.md)</span></span>

## <a name="finding-a-package"></a><span data-ttu-id="fea67-176">Suchen ein Paket</span><span class="sxs-lookup"><span data-stu-id="fea67-176">Finding a package</span></span>

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

<span data-ttu-id="fea67-177">Finden Sie unter [Find-Package](../tools/ps-ref-find-package.md).</span><span class="sxs-lookup"><span data-stu-id="fea67-177">See [Find-Package](../tools/ps-ref-find-package.md).</span></span> <span data-ttu-id="fea67-178">Verwenden Sie in Visual Studio 2013 und früheren [Get-Package](../tools/ps-ref-get-package.md) stattdessen.</span><span class="sxs-lookup"><span data-stu-id="fea67-178">In Visual Studio 2013 and earlier, use [Get-Package](../tools/ps-ref-get-package.md) instead.</span></span>

## <a name="availability-of-the-console"></a><span data-ttu-id="fea67-179">Verfügbarkeit der Konsole</span><span class="sxs-lookup"><span data-stu-id="fea67-179">Availability of the console</span></span>

<span data-ttu-id="fea67-180">In Visual Studio 2017 werden NuGet und NuGet-Paket-Manager automatisch installiert, wenn Sie auswählen. NET-bezogenen Arbeitslasten; Sie können auch installieren sie einzeln durch Überprüfen der **Einzelkomponenten > Tools Code > NuGet-Paket-Manager** -Option in der 2017 von Visual Studio-Installer.</span><span class="sxs-lookup"><span data-stu-id="fea67-180">In Visual Studio 2017, NuGet and the NuGet Package Manager are automatically installed when you select any .NET-related workloads; you can also install it individually by checking the **Individual components > Code tools > NuGet package manager** option in the Visual Studio 2017 installer.</span></span>

<span data-ttu-id="fea67-181">Überprüfen Sie auch, wenn Sie den NuGet-Paket-Manager in Visual Studio 2015 und früheren Versionen nicht vorhanden sind, **Tools > Erweiterungen und Updates...**  und suchen Sie nach der Erweiterung von NuGet-Paket-Manager.</span><span class="sxs-lookup"><span data-stu-id="fea67-181">Also, if you're missing the NuGet Package Manager in Visual Studio 2015 and earlier, check **Tools > Extensions and Updates...** and search for the NuGet Package Manager extension.</span></span> <span data-ttu-id="fea67-182">Wenn Sie nicht das Installationsprogramm für Erweiterungen in Visual Studio verwenden möchten, können Sie die Erweiterung direkt von herunterladen [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="fea67-182">If you're unable to use the extensions installer in Visual Studio, you can download the extension directly from [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span></span>

<span data-ttu-id="fea67-183">Der Paket-Manager-Konsole ist zurzeit nicht verfügbar in Visual Studio für Mac.</span><span class="sxs-lookup"><span data-stu-id="fea67-183">The Package Manager Console is not presently available with Visual Studio for Mac.</span></span> <span data-ttu-id="fea67-184">Allerdings stehen die entsprechenden Befehle zur Verfügung, über die [NuGet CLI](nuget-exe-CLI-reference.md).</span><span class="sxs-lookup"><span data-stu-id="fea67-184">The equivalent commands, however, are available through the [NuGet CLI](nuget-exe-CLI-reference.md).</span></span> <span data-ttu-id="fea67-185">Visual Studio für Mac besitzt eine Benutzeroberfläche zum Verwalten von NuGet-Paketen.</span><span class="sxs-lookup"><span data-stu-id="fea67-185">Visual Studio for Mac does have a UI for managing NuGet packages.</span></span> <span data-ttu-id="fea67-186">Finden Sie unter [einschließlich eines NuGet-Paket im Projekt](/visualstudio/mac/nuget-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="fea67-186">See [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span>

<span data-ttu-id="fea67-187">Der Paket-Manager-Konsole ist nicht mit Visual Studio-Code enthalten.</span><span class="sxs-lookup"><span data-stu-id="fea67-187">The Package Manager Console is not included with Visual Studio Code.</span></span>

## <a name="extending-the-package-manager-console"></a><span data-ttu-id="fea67-188">Erweitern Sie die Paket-Manager-Konsole</span><span class="sxs-lookup"><span data-stu-id="fea67-188">Extending the Package Manager Console</span></span>

<span data-ttu-id="fea67-189">Einige Pakete installieren Sie neue Befehle für die Konsole.</span><span class="sxs-lookup"><span data-stu-id="fea67-189">Some packages install new commands for the console.</span></span> <span data-ttu-id="fea67-190">Beispielsweise `MvcScaffolding` erstellt Befehle wie `Scaffold` unten, wodurch die ASP.NET MVC-Controller und Ansichten generiert:</span><span class="sxs-lookup"><span data-stu-id="fea67-190">For example, `MvcScaffolding` creates commands like `Scaffold` shown below, which generates ASP.NET MVC controllers and views:</span></span>

![Installieren und Verwenden von MvcScaffold](media/PackageManagerConsoleInstall.png)

## <a name="setting-up-a-nuget-powershell-profile"></a><span data-ttu-id="fea67-192">Einrichten eines NuGet-PowerShell-Profils</span><span class="sxs-lookup"><span data-stu-id="fea67-192">Setting up a NuGet PowerShell Profile</span></span>

<span data-ttu-id="fea67-193">Ein PowerShell-Profil können Sie häufig verwendete Befehle zur Verfügung stellen, wo Sie PowerShell verwenden.</span><span class="sxs-lookup"><span data-stu-id="fea67-193">A PowerShell profile lets you make commonly-used commands available wherever you use PowerShell.</span></span> <span data-ttu-id="fea67-194">NuGet unterstützt ein NuGet-spezifischen Profil, in der Regel am folgenden Speicherort gefunden:</span><span class="sxs-lookup"><span data-stu-id="fea67-194">NuGet supports a NuGet-specific profile typically found at the following location:</span></span>

```
%UserProfile%\Documents\WindowsPowerShell\NuGet_profile.ps1
```

<span data-ttu-id="fea67-195">Um das Profil zu suchen, geben Sie `$profile` in der Konsole:</span><span class="sxs-lookup"><span data-stu-id="fea67-195">To find the profile, type `$profile` in the console:</span></span>

```ps
$profile
C:\Users\<user>\Documents\WindowsPowerShell\NuGet_profile.ps1
```

<span data-ttu-id="fea67-196">Weitere Informationen finden Sie unter [Windows PowerShell-Profile](https://technet.microsoft.com/library/bb613488.aspx).</span><span class="sxs-lookup"><span data-stu-id="fea67-196">For more details, refer to [Windows PowerShell Profiles](https://technet.microsoft.com/library/bb613488.aspx).</span></span>
