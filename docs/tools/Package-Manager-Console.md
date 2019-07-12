---
title: Installieren und Verwalten von NuGet-Pakete, die mit der Konsole in Visual Studio
description: Anweisungen zum Verwenden der NuGet-Paket-Manager-Konsole in Visual Studio zum Arbeiten mit Paketen.
author: karann-msft
ms.author: karann
ms.date: 06/24/2019
ms.topic: conceptual
f1_keywords:
- vs.nuget.packagemanager.console
ms.openlocfilehash: 91ab3859994e5ae738c6637219681ebbfc92d420
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842585"
---
# <a name="install-and-manage-packages-with-the-package-manager-console-in-visual-studio-powershell"></a><span data-ttu-id="f56e5-103">Installieren und Verwalten von Paketen mit der Paket-Manager-Konsole in Visual Studio (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="f56e5-103">Install and manage packages with the Package Manager Console in Visual Studio (PowerShell)</span></span>

<span data-ttu-id="f56e5-104">Der NuGet-Paket-Manager-Konsole können Sie die Verwendung [NuGet-PowerShell-Befehle](../tools/powershell-reference.md) finden, installieren, deinstallieren und Aktualisieren von NuGet-Pakete.</span><span class="sxs-lookup"><span data-stu-id="f56e5-104">The NuGet Package Manager Console lets you use [NuGet PowerShell commands](../tools/powershell-reference.md) to find, install, uninstall, and update NuGet packages.</span></span> <span data-ttu-id="f56e5-105">Mithilfe der Konsole ist erforderlich, in Fällen, in denen die Paket-Manager-UI keine Möglichkeit zum Ausführen eines Vorgangs bereitstellt.</span><span class="sxs-lookup"><span data-stu-id="f56e5-105">Using the console is necessary in cases where the Package Manager UI does not provide a way to perform an operation.</span></span> <span data-ttu-id="f56e5-106">Verwendung von `nuget.exe` CLI-Befehle in der Konsole finden Sie unter [mithilfe der nuget.exe-CLI in der Konsole](#using-the-nugetexe-cli-in-the-console).</span><span class="sxs-lookup"><span data-stu-id="f56e5-106">To use `nuget.exe` CLI commands in the console, see [Using the nuget.exe CLI in the console](#using-the-nugetexe-cli-in-the-console).</span></span>

<span data-ttu-id="f56e5-107">Die Konsole ist in Visual Studio unter Windows integriert.</span><span class="sxs-lookup"><span data-stu-id="f56e5-107">The console is built into Visual Studio on Windows.</span></span> <span data-ttu-id="f56e5-108">Es ist nicht in Visual Studio für Mac oder Visual Studio Code enthalten.</span><span class="sxs-lookup"><span data-stu-id="f56e5-108">It is not included with Visual Studio for Mac or Visual Studio Code.</span></span>

## <a name="find-and-install-a-package"></a><span data-ttu-id="f56e5-109">Suchen und Installieren eines Pakets</span><span class="sxs-lookup"><span data-stu-id="f56e5-109">Find and install a package</span></span>

<span data-ttu-id="f56e5-110">Suchen und Installieren eines Pakets erfolgt z. B. mit drei einfachen Schritten:</span><span class="sxs-lookup"><span data-stu-id="f56e5-110">For example, finding and installing a package is done with three easy steps:</span></span>

1. <span data-ttu-id="f56e5-111">Öffnen Sie das Projekt/Projektmappe in Visual Studio, und öffnen Sie die Konsole mit der **Tools > NuGet-Paket-Manager > Paket-Manager-Konsole** Befehl.</span><span class="sxs-lookup"><span data-stu-id="f56e5-111">Open the project/solution in Visual Studio, and open the console using the **Tools > NuGet Package Manager > Package Manager Console** command.</span></span>

1. <span data-ttu-id="f56e5-112">Suchen Sie das Paket, die, das Sie installieren möchten.</span><span class="sxs-lookup"><span data-stu-id="f56e5-112">Find the package you want to install.</span></span> <span data-ttu-id="f56e5-113">Wenn Sie dies zum bereits kennen, fahren Sie mit Schritt 3 fort.</span><span class="sxs-lookup"><span data-stu-id="f56e5-113">If you already know this, skip to step 3.</span></span>

    ```ps
    # Find packages containing the keyword "elmah"
    Find-Package elmah
    ```

1. <span data-ttu-id="f56e5-114">Führen Sie den Befehl "Install":</span><span class="sxs-lookup"><span data-stu-id="f56e5-114">Run the install command:</span></span>

    ```ps
    # Install the Elmah package to the project named MyProject.
    Install-Package Elmah -ProjectName MyProject
    ```

> [!Important]
> <span data-ttu-id="f56e5-115">Alle Vorgänge, die in der Konsole verfügbaren erreichen Sie auch mit der [NuGet-CLI](../tools/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="f56e5-115">All operations that are available in the console can also be done with the [NuGet CLI](../tools/nuget-exe-cli-reference.md).</span></span> <span data-ttu-id="f56e5-116">Allerdings Konsolenbefehle im Kontext von Visual Studio und einer gespeicherten Projekt/Projektmappe arbeiten und häufig mehr als die entsprechende CLI-Befehle ausführen.</span><span class="sxs-lookup"><span data-stu-id="f56e5-116">However, console commands operate within the context of Visual Studio and a saved project/solution and often accomplish more than their equivalent CLI commands.</span></span> <span data-ttu-id="f56e5-117">Installieren eines Pakets über die Konsole fügt z. B. einen Verweis auf das Projekt während der CLI-Befehl nicht der Fall ist.</span><span class="sxs-lookup"><span data-stu-id="f56e5-117">For example, installing a package through the console adds a reference to the project whereas the CLI command does not.</span></span> <span data-ttu-id="f56e5-118">Aus diesem Grund bevorzugen die Entwickler in Visual Studio in der Regel mithilfe der Konsole auf die CLI.</span><span class="sxs-lookup"><span data-stu-id="f56e5-118">For this reason, developers working in Visual Studio typically prefer using the console to the CLI.</span></span>

> [!Tip]
> <span data-ttu-id="f56e5-119">Viele konsolenvorgänge hängen davon ab, eine Lösung mit einem bekannten Pfadnamen in Visual Studio geöffnet.</span><span class="sxs-lookup"><span data-stu-id="f56e5-119">Many console operations depend on having a solution opened in Visual Studio with a known path name.</span></span> <span data-ttu-id="f56e5-120">Wenn Sie eine nicht gespeicherte oder keine Lösung verfügen, können die Fehler, "Projektmappe nicht geöffnet oder nicht gespeichert.</span><span class="sxs-lookup"><span data-stu-id="f56e5-120">If you have an unsaved solution, or no solution, you can see the error, "Solution is not opened or not saved.</span></span> <span data-ttu-id="f56e5-121">Stellen Sie sicher, dass Sie eine Projektmappe geöffnet und gespeichert haben."</span><span class="sxs-lookup"><span data-stu-id="f56e5-121">Please ensure you have an open and saved solution."</span></span> <span data-ttu-id="f56e5-122">Dies bedeutet, dass es sich bei die Konsole nicht den Projektmappenordner bestimmen kann.</span><span class="sxs-lookup"><span data-stu-id="f56e5-122">This indicates that the console cannot determine the solution folder.</span></span> <span data-ttu-id="f56e5-123">Speichern eine nicht gespeicherte Projektmappe, oder erstellen und eine Projektmappe gespeichert, falls noch nicht öffnen, sollte den Fehler zu beheben.</span><span class="sxs-lookup"><span data-stu-id="f56e5-123">Saving an unsaved solution, or creating and saving a solution if you don't have one open, should correct the error.</span></span>

## <a name="opening-the-console-and-console-controls"></a><span data-ttu-id="f56e5-124">Öffnen die Konsole und die Konsole-Steuerelemente</span><span class="sxs-lookup"><span data-stu-id="f56e5-124">Opening the console and console controls</span></span>

1. <span data-ttu-id="f56e5-125">Öffnen Sie die Konsole in Visual Studio mithilfe der **Tools > NuGet-Paket-Manager > Paket-Manager-Konsole** Befehl.</span><span class="sxs-lookup"><span data-stu-id="f56e5-125">Open the console in Visual Studio using the **Tools > NuGet Package Manager > Package Manager Console** command.</span></span> <span data-ttu-id="f56e5-126">Die Konsole ist ein Visual Studio-Fenster, das angeordnet und positioniert beliebig werden kann (siehe [Anpassen von Fensterlayouts in Visual Studio](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).</span><span class="sxs-lookup"><span data-stu-id="f56e5-126">The console is a Visual Studio window that can be arranged and positioned however you like (see [Customize window layouts in Visual Studio](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).</span></span>

1. <span data-ttu-id="f56e5-127">Standardmäßig werden Konsolenbefehle für eine bestimmte Quelle und das Projekt als Satz in das Steuerelement am oberen Rand des Fensters:</span><span class="sxs-lookup"><span data-stu-id="f56e5-127">By default, console commands operate against a specific package source and project as set in the control at the top of the window:</span></span>

    ![Paket-Manager-Konsole steuert für Quelle und das Projekt](media/PackageManagerConsoleControls1.png)

1. <span data-ttu-id="f56e5-129">Auswählen einer anderen Quelle und/oder ändert diese Standardwerte für nachfolgende Befehle.</span><span class="sxs-lookup"><span data-stu-id="f56e5-129">Selecting a different package source and/or project changes those defaults for subsequent commands.</span></span> <span data-ttu-id="f56e5-130">Auf einem diese Einstellungen ohne Ändern der Standardwerte, die meisten Befehle unterstützen `-Source` und `-ProjectName` Optionen.</span><span class="sxs-lookup"><span data-stu-id="f56e5-130">To overrride these settings without changing the defaults, most commands support `-Source` and `-ProjectName` options.</span></span>

1. <span data-ttu-id="f56e5-131">Wählen Sie das Zahnradsymbol, um Paketquellen zu verwalten.</span><span class="sxs-lookup"><span data-stu-id="f56e5-131">To manage package sources, select the gear icon.</span></span> <span data-ttu-id="f56e5-132">Dies ist eine Verknüpfung zu den **Tools > Optionen > NuGet-Paket-Manager > Paketquellen** wie beschrieben in das Dialogfeld die [-Paket-Manager-UI](package-manager-ui.md#package-sources) Seite.</span><span class="sxs-lookup"><span data-stu-id="f56e5-132">This is a shortcut to the **Tools > Options > NuGet Package Manager > Package Sources** dialog box as described on the [Package Manager UI](package-manager-ui.md#package-sources) page.</span></span> <span data-ttu-id="f56e5-133">Darüber hinaus löscht das Steuerelement rechts neben die Projektauswahl der Konsole Inhalt:</span><span class="sxs-lookup"><span data-stu-id="f56e5-133">Also, the control to the right of the project selector clears the console's contents:</span></span>

    ![Einstellungen für die Paket-Manager-Konsole und Steuerelemente löschen](media/PackageManagerConsoleControls2.png)

1. <span data-ttu-id="f56e5-135">Die Schaltfläche ganz rechts Hardwareinterrupts benötigt hat einen lang andauernden-Befehl.</span><span class="sxs-lookup"><span data-stu-id="f56e5-135">The rightmost button interrupts a long-running command.</span></span> <span data-ttu-id="f56e5-136">Z. B. Ausführung `Get-Package -ListAvailable -PageSize 500` Listet die Top-500-Pakete auf dem Quellcomputer (z. B. "NuGet.org"), dies kann einige Minuten dauern.</span><span class="sxs-lookup"><span data-stu-id="f56e5-136">For example, running `Get-Package -ListAvailable -PageSize 500` lists the top 500 packages on the default source (such as nuget.org), which could take several minutes to run.</span></span>

    ![Paket-Manager-Konsole beenden-Steuerelement](media/PackageManagerConsoleControls3.png)

## <a name="installing-a-package"></a><span data-ttu-id="f56e5-138">Installieren eines Pakets</span><span class="sxs-lookup"><span data-stu-id="f56e5-138">Installing a package</span></span>

```ps
# Add the Elmah package to the default project as specified in the console's project selector
Install-Package Elmah

# Add the Elmah package to a project named UtilitiesLib that is not the default
Install-Package Elmah -ProjectName UtilitiesLib
```

<span data-ttu-id="f56e5-139">Finden Sie unter [Install-Package](../tools/ps-ref-install-package.md).</span><span class="sxs-lookup"><span data-stu-id="f56e5-139">See [Install-Package](../tools/ps-ref-install-package.md).</span></span>

<span data-ttu-id="f56e5-140">Installieren eines Pakets in der Konsole führt die gleichen Schritte aus, wie im [was geschieht, wenn die Installation eines Pakets](../concepts/package-installation-process.md), mit den folgenden Ergänzungen:</span><span class="sxs-lookup"><span data-stu-id="f56e5-140">Installing a package in the console performs the same steps as described on [What happens when a package is installed](../concepts/package-installation-process.md), with the following additions:</span></span>

- <span data-ttu-id="f56e5-141">Die Konsole zeigt jeweils geltenden Lizenzbedingungen genannten in einem Fenster mit implizite Vereinbarung.</span><span class="sxs-lookup"><span data-stu-id="f56e5-141">The Console displays applicable license terms in its window with implied agreement.</span></span> <span data-ttu-id="f56e5-142">Wenn Sie den Lizenzbedingungen nicht einverstanden sind, sollten Sie das Paket sofort deinstallieren.</span><span class="sxs-lookup"><span data-stu-id="f56e5-142">If you do not agree to the terms, you should uninstall the package immediately.</span></span>
- <span data-ttu-id="f56e5-143">Außerdem ein Verweis auf das Paket wird in der Projektdatei hinzugefügt und wird im **Projektmappen-Explorer** unter der **Verweise** Knoten müssen Sie zum Speichern des Projekts, um die Änderungen in der Projektdatei direkt anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="f56e5-143">Also a reference to the package is added to the project file and appears in **Solution Explorer** under the **References** node, you need to save the project to see the changes in the project file directly.</span></span>

## <a name="uninstalling-a-package"></a><span data-ttu-id="f56e5-144">Wenn ein Paket deinstalliert</span><span class="sxs-lookup"><span data-stu-id="f56e5-144">Uninstalling a package</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```

<span data-ttu-id="f56e5-145">Finden Sie unter [Uninstall-Package](../tools/ps-ref-uninstall-package.md).</span><span class="sxs-lookup"><span data-stu-id="f56e5-145">See [Uninstall-Package](../tools/ps-ref-uninstall-package.md).</span></span> <span data-ttu-id="f56e5-146">Verwendung [Get-Package](../tools/ps-ref-get-package.md) , finden alle Pakete, die derzeit im Standardprojekt installiert, wenn Sie einen Bezeichner zu suchen müssen.</span><span class="sxs-lookup"><span data-stu-id="f56e5-146">Use [Get-Package](../tools/ps-ref-get-package.md) to see all packages currently installed in the default project if you need to find an identifier.</span></span>

<span data-ttu-id="f56e5-147">Wenn ein Paket deinstalliert führt folgende Aktionen aus:</span><span class="sxs-lookup"><span data-stu-id="f56e5-147">Uninstalling a package performs the following actions:</span></span>

- <span data-ttu-id="f56e5-148">Entfernt Verweise auf das Paket aus dem Projekt (und dem Managementobjektformat verwendet wird).</span><span class="sxs-lookup"><span data-stu-id="f56e5-148">Removes references to the package from the project (and whatever management format is in use).</span></span> <span data-ttu-id="f56e5-149">Verweise nicht mehr angezeigt werden, **Projektmappen-Explorer**.</span><span class="sxs-lookup"><span data-stu-id="f56e5-149">References no longer appear in **Solution Explorer**.</span></span> <span data-ttu-id="f56e5-150">(Zum Neuerstellen des Projekts, um daraus überprüfen müssen möglicherweise die **Bin** Ordner.)</span><span class="sxs-lookup"><span data-stu-id="f56e5-150">(You might need to rebuild the project to see it removed from the **Bin** folder.)</span></span>
- <span data-ttu-id="f56e5-151">Kehrt alle Änderungen an `app.config` oder `web.config` Wenn das Paket installiert wurde.</span><span class="sxs-lookup"><span data-stu-id="f56e5-151">Reverses any changes made to `app.config` or `web.config` when the package was installed.</span></span>
- <span data-ttu-id="f56e5-152">Entfernt zuvor installierte Abhängigkeiten, wenn keine verbleibenden Pakete diese Abhängigkeiten verwenden.</span><span class="sxs-lookup"><span data-stu-id="f56e5-152">Removes previously-installed dependencies if no remaining packages use those dependencies.</span></span>

## <a name="updating-a-package"></a><span data-ttu-id="f56e5-153">Aktualisieren eines Pakets</span><span class="sxs-lookup"><span data-stu-id="f56e5-153">Updating a package</span></span>

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

<span data-ttu-id="f56e5-154">Finden Sie unter [Get-Package](../tools/ps-ref-get-package.md) und [Update-Package](../tools/ps-ref-update-package.md)</span><span class="sxs-lookup"><span data-stu-id="f56e5-154">See [Get-Package](../tools/ps-ref-get-package.md) and [Update-Package](../tools/ps-ref-update-package.md)</span></span>

## <a name="finding-a-package"></a><span data-ttu-id="f56e5-155">Suchen ein Paket</span><span class="sxs-lookup"><span data-stu-id="f56e5-155">Finding a package</span></span>

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

<span data-ttu-id="f56e5-156">Finden Sie unter [Find-Package](../tools/ps-ref-find-package.md).</span><span class="sxs-lookup"><span data-stu-id="f56e5-156">See [Find-Package](../tools/ps-ref-find-package.md).</span></span> <span data-ttu-id="f56e5-157">Verwenden Sie in Visual Studio 2013 und früher [Get-Package](../tools/ps-ref-get-package.md) stattdessen.</span><span class="sxs-lookup"><span data-stu-id="f56e5-157">In Visual Studio 2013 and earlier, use [Get-Package](../tools/ps-ref-get-package.md) instead.</span></span>

## <a name="availability-of-the-console"></a><span data-ttu-id="f56e5-158">Verfügbarkeit der Konsole</span><span class="sxs-lookup"><span data-stu-id="f56e5-158">Availability of the console</span></span>

<span data-ttu-id="f56e5-159">In Visual Studio 2017 beginnen, werden NuGet und den NuGet-Paket-Manager automatisch installiert, wenn Sie eine auswählen. NET-bezogenen Workloads; Sie können auch installieren sie einzeln überprüfen die **einzelne Komponenten > Codetools > NuGet-Paket-Manager** -Option in Visual Studio-Installer.</span><span class="sxs-lookup"><span data-stu-id="f56e5-159">Starting in Visual Studio 2017, NuGet and the NuGet Package Manager are automatically installed when you select any .NET-related workloads; you can also install it individually by checking the **Individual components > Code tools > NuGet package manager** option in the Visual Studio installer.</span></span>

<span data-ttu-id="f56e5-160">Überprüfen Sie auch, wenn Sie den NuGet-Paket-Manager in Visual Studio 2015 und früheren Versionen nicht vorhanden sind, **Tools > Erweiterungen und Updates...**  und suchen Sie nach der NuGet-Paket-Manager-Erweiterung.</span><span class="sxs-lookup"><span data-stu-id="f56e5-160">Also, if you're missing the NuGet Package Manager in Visual Studio 2015 and earlier, check **Tools > Extensions and Updates...** and search for the NuGet Package Manager extension.</span></span> <span data-ttu-id="f56e5-161">Wenn Sie nicht das Installationsprogramm für Erweiterungen in Visual Studio verwenden können, können Sie die Erweiterung direkt aus [ https://dist.nuget.org/index.html ](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="f56e5-161">If you're unable to use the extensions installer in Visual Studio, you can download the extension directly from [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span></span>

<span data-ttu-id="f56e5-162">Der Paket-Manager-Konsole ist zurzeit nicht verfügbar in Visual Studio für Mac.</span><span class="sxs-lookup"><span data-stu-id="f56e5-162">The Package Manager Console is not presently available with Visual Studio for Mac.</span></span> <span data-ttu-id="f56e5-163">Die entsprechenden Befehle, allerdings stehen über die [NuGet-CLI](nuget-exe-CLI-reference.md).</span><span class="sxs-lookup"><span data-stu-id="f56e5-163">The equivalent commands, however, are available through the [NuGet CLI](nuget-exe-CLI-reference.md).</span></span> <span data-ttu-id="f56e5-164">Visual Studio für Mac besitzt eine Benutzeroberfläche zum Verwalten von NuGet-Paketen.</span><span class="sxs-lookup"><span data-stu-id="f56e5-164">Visual Studio for Mac does have a UI for managing NuGet packages.</span></span> <span data-ttu-id="f56e5-165">Finden Sie unter [einschließen eines NuGet-Paket in Ihrem Projekt](/visualstudio/mac/nuget-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="f56e5-165">See [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span>

<span data-ttu-id="f56e5-166">Der Paket-Manager-Konsole ist nicht in Visual Studio Code enthalten.</span><span class="sxs-lookup"><span data-stu-id="f56e5-166">The Package Manager Console is not included with Visual Studio Code.</span></span>

## <a name="extending-the-package-manager-console"></a><span data-ttu-id="f56e5-167">Erweitern Sie die Paket-Manager-Konsole</span><span class="sxs-lookup"><span data-stu-id="f56e5-167">Extending the Package Manager Console</span></span>

<span data-ttu-id="f56e5-168">Einige Pakete installiert, neue Befehle für die Konsole.</span><span class="sxs-lookup"><span data-stu-id="f56e5-168">Some packages install new commands for the console.</span></span> <span data-ttu-id="f56e5-169">Z. B. `MvcScaffolding` erstellt Befehle wie `Scaffold` unten dargestellt, die ASP.NET MVC-Controller und Ansichten generiert:</span><span class="sxs-lookup"><span data-stu-id="f56e5-169">For example, `MvcScaffolding` creates commands like `Scaffold` shown below, which generates ASP.NET MVC controllers and views:</span></span>

![Installieren und Verwenden von MvcScaffold](media/PackageManagerConsoleInstall.png)

## <a name="setting-up-a-nuget-powershell-profile"></a><span data-ttu-id="f56e5-171">Ein NuGet-PowerShell-Profil einrichten</span><span class="sxs-lookup"><span data-stu-id="f56e5-171">Setting up a NuGet PowerShell profile</span></span>

<span data-ttu-id="f56e5-172">Ein PowerShell-Profil können Sie die häufig verwendete Befehle zur Verfügung stellen, wo Sie PowerShell verwenden.</span><span class="sxs-lookup"><span data-stu-id="f56e5-172">A PowerShell profile lets you make commonly-used commands available wherever you use PowerShell.</span></span> <span data-ttu-id="f56e5-173">NuGet unterstützt ein NuGet-spezifischen Profil, in der Regel am folgenden Speicherort gefunden:</span><span class="sxs-lookup"><span data-stu-id="f56e5-173">NuGet supports a NuGet-specific profile typically found at the following location:</span></span>

    %UserProfile%\Documents\WindowsPowerShell\NuGet_profile.ps1

<span data-ttu-id="f56e5-174">Um das Profil zu suchen, geben `$profile` in der Konsole:</span><span class="sxs-lookup"><span data-stu-id="f56e5-174">To find the profile, type `$profile` in the console:</span></span>

```ps
$profile
C:\Users\<user>\Documents\WindowsPowerShell\NuGet_profile.ps1
```

<span data-ttu-id="f56e5-175">Weitere Informationen finden Sie unter [Windows PowerShell-Profile](https://technet.microsoft.com/library/bb613488.aspx).</span><span class="sxs-lookup"><span data-stu-id="f56e5-175">For more details, refer to [Windows PowerShell Profiles](https://technet.microsoft.com/library/bb613488.aspx).</span></span>

## <a name="using-the-nugetexe-cli-in-the-console"></a><span data-ttu-id="f56e5-176">Verwenden die nuget.exe-CLI in der Konsole</span><span class="sxs-lookup"><span data-stu-id="f56e5-176">Using the nuget.exe CLI in the console</span></span>

<span data-ttu-id="f56e5-177">Vornehmen der [ `nuget.exe` CLI](nuget-exe-cli-reference.md) zur Verfügung, in der Paket-Manager-Konsole installieren die [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) Paket über die Konsole:</span><span class="sxs-lookup"><span data-stu-id="f56e5-177">To make the [`nuget.exe` CLI](nuget-exe-cli-reference.md) available in the Package Manager Console, install the [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) package from the console:</span></span>

```ps
# Other versions are available, see http://www.nuget.org/packages/NuGet.CommandLine/
Install-Package NuGet.CommandLine -Version 4.4.1
```
