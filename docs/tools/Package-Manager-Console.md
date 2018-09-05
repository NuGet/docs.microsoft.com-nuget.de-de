---
title: Leitfaden für die NuGet-Paket-Manager-Konsole
description: Anweisungen zum Verwenden der NuGet-Paket-Manager-Konsole in Visual Studio zum Arbeiten mit Paketen.
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: conceptual
f1_keywords:
- vs.nuget.packagemanager.console
ms.openlocfilehash: 88979c67ea7f073f2ea5a02c445186642f77f210
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546877"
---
# <a name="package-manager-console"></a><span data-ttu-id="df0a1-103">Paket-Manager-Konsole</span><span class="sxs-lookup"><span data-stu-id="df0a1-103">Package Manager Console</span></span>

<span data-ttu-id="df0a1-104">Der NuGet-Paket-Manager-Konsole ist in Visual Studio unter Windows 2012 und höher integriert.</span><span class="sxs-lookup"><span data-stu-id="df0a1-104">The NuGet Package Manager Console is built into Visual Studio on Windows version 2012 and later.</span></span> <span data-ttu-id="df0a1-105">(Es ist nicht in Visual Studio für Mac oder Visual Studio Code enthalten.)</span><span class="sxs-lookup"><span data-stu-id="df0a1-105">(It is not included with Visual Studio for Mac or Visual Studio Code.)</span></span>

<span data-ttu-id="df0a1-106">Die Konsole können Sie verwenden [NuGet-PowerShell-Befehle](../tools/powershell-reference.md) finden, installieren, deinstallieren und Aktualisieren von NuGet-Pakete.</span><span class="sxs-lookup"><span data-stu-id="df0a1-106">The console lets you use [NuGet PowerShell commands](../tools/powershell-reference.md) to find, install, uninstall, and update NuGet packages.</span></span> <span data-ttu-id="df0a1-107">Mithilfe der Konsole ist erforderlich, in Fällen, in denen die Paket-Manager-UI keine Möglichkeit zum Ausführen eines Vorgangs bereitstellt.</span><span class="sxs-lookup"><span data-stu-id="df0a1-107">Using the console is necessary in cases where the Package Manager UI does not provide a way to perform an operation.</span></span> <span data-ttu-id="df0a1-108">Verwendung von `nuget.exe` Befehle in der Konsole finden Sie unter [mithilfe der nuget.exe-CLI in der Konsole](#using-the-nugetexe-cli-in-the-console).</span><span class="sxs-lookup"><span data-stu-id="df0a1-108">To use `nuget.exe` commands in the console, see [Using the nuget.exe CLI in the console](#using-the-nugetexe-cli-in-the-console).</span></span>

<span data-ttu-id="df0a1-109">Suchen und Installieren eines Pakets erfolgt z. B. mit drei einfachen Schritten:</span><span class="sxs-lookup"><span data-stu-id="df0a1-109">For example, finding and installing a package is done with three easy steps:</span></span>

1. <span data-ttu-id="df0a1-110">Öffnen Sie das Projekt/Projektmappe in Visual Studio, und öffnen Sie die Konsole mit der **Tools > NuGet-Paket-Manager > Paket-Manager-Konsole** Befehl.</span><span class="sxs-lookup"><span data-stu-id="df0a1-110">Open the project/solution in Visual Studio, and open the console using the **Tools > NuGet Package Manager > Package Manager Console** command.</span></span>

1. <span data-ttu-id="df0a1-111">Suchen Sie das Paket, die, das Sie installieren möchten.</span><span class="sxs-lookup"><span data-stu-id="df0a1-111">Find the package you want to install.</span></span> <span data-ttu-id="df0a1-112">Wenn Sie dies zum bereits kennen, fahren Sie mit Schritt 3 fort.</span><span class="sxs-lookup"><span data-stu-id="df0a1-112">If you already know this, skip to step 3.</span></span>

    ```ps
    # Find packages containing the keyword "elmah"
    Find-Package elmah
    ```

1. <span data-ttu-id="df0a1-113">Führen Sie den Befehl "Install":</span><span class="sxs-lookup"><span data-stu-id="df0a1-113">Run the install command:</span></span>

    ```ps
    # Install the Elmah package to the project named MyProject.
    Install-Package Elmah -ProjectName MyProject
    ```

> [!Important]
> <span data-ttu-id="df0a1-114">Alle Vorgänge, die in der Konsole verfügbaren erreichen Sie auch mit der [NuGet-CLI](../tools/nuget-exe-cli-reference.md).</span><span class="sxs-lookup"><span data-stu-id="df0a1-114">All operations that are available in the console can also be done with the [NuGet CLI](../tools/nuget-exe-cli-reference.md).</span></span> <span data-ttu-id="df0a1-115">Allerdings Konsolenbefehle im Kontext von Visual Studio und einer gespeicherten Projekt/Projektmappe arbeiten und häufig mehr als die entsprechende CLI-Befehle ausführen.</span><span class="sxs-lookup"><span data-stu-id="df0a1-115">However, console commands operate within the context of Visual Studio and a saved project/solution and often accomplish more than their equivalent CLI commands.</span></span> <span data-ttu-id="df0a1-116">Installieren eines Pakets über die Konsole fügt z. B. einen Verweis auf das Projekt während der CLI-Befehl nicht der Fall ist.</span><span class="sxs-lookup"><span data-stu-id="df0a1-116">For example, installing a package through the console adds a reference to the project whereas the CLI command does not.</span></span> <span data-ttu-id="df0a1-117">Aus diesem Grund bevorzugen die Entwickler in Visual Studio in der Regel mithilfe der Konsole auf die CLI.</span><span class="sxs-lookup"><span data-stu-id="df0a1-117">For this reason, developers working in Visual Studio typically prefer using the console to the CLI.</span></span>

> [!Tip]
> <span data-ttu-id="df0a1-118">Viele konsolenvorgänge hängen davon ab, eine Lösung mit einem bekannten Pfadnamen in Visual Studio geöffnet.</span><span class="sxs-lookup"><span data-stu-id="df0a1-118">Many console operations depend on having a solution opened in Visual Studio with a known path name.</span></span> <span data-ttu-id="df0a1-119">Wenn Sie eine nicht gespeicherte oder keine Lösung verfügen, können die Fehler, "Projektmappe nicht geöffnet oder nicht gespeichert.</span><span class="sxs-lookup"><span data-stu-id="df0a1-119">If you have an unsaved solution, or no solution, you can see the error, "Solution is not opened or not saved.</span></span> <span data-ttu-id="df0a1-120">Stellen Sie sicher, dass Sie eine Projektmappe geöffnet und gespeichert haben."</span><span class="sxs-lookup"><span data-stu-id="df0a1-120">Please ensure you have an open and saved solution."</span></span> <span data-ttu-id="df0a1-121">Dies bedeutet, dass es sich bei die Konsole nicht den Projektmappenordner bestimmen kann.</span><span class="sxs-lookup"><span data-stu-id="df0a1-121">This indicates that the console cannot determine the solution folder.</span></span> <span data-ttu-id="df0a1-122">Speichern eine nicht gespeicherte Projektmappe, oder erstellen und eine Projektmappe gespeichert, falls noch nicht öffnen, sollte den Fehler zu beheben.</span><span class="sxs-lookup"><span data-stu-id="df0a1-122">Saving an unsaved solution, or creating and saving a solution if you don't have one open, should correct the error.</span></span>

## <a name="opening-the-console-and-console-controls"></a><span data-ttu-id="df0a1-123">Öffnen die Konsole und die Konsole-Steuerelemente</span><span class="sxs-lookup"><span data-stu-id="df0a1-123">Opening the console and console controls</span></span>

1. <span data-ttu-id="df0a1-124">Öffnen Sie die Konsole in Visual Studio mithilfe der **Tools > NuGet-Paket-Manager > Paket-Manager-Konsole** Befehl.</span><span class="sxs-lookup"><span data-stu-id="df0a1-124">Open the console in Visual Studio using the **Tools > NuGet Package Manager > Package Manager Console** command.</span></span> <span data-ttu-id="df0a1-125">Die Konsole ist ein Visual Studio-Fenster, das angeordnet und positioniert beliebig werden kann (siehe [Anpassen von Fensterlayouts in Visual Studio](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).</span><span class="sxs-lookup"><span data-stu-id="df0a1-125">The console is a Visual Studio window that can be arranged and positioned however you like (see [Customize window layouts in Visual Studio](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).</span></span>

1. <span data-ttu-id="df0a1-126">Standardmäßig werden Konsolenbefehle für eine bestimmte Quelle und das Projekt als Satz in das Steuerelement am oberen Rand des Fensters:</span><span class="sxs-lookup"><span data-stu-id="df0a1-126">By default, console commands operate against a specific package source and project as set in the control at the top of the window:</span></span>

    ![Paket-Manager-Konsole steuert für Quelle und das Projekt](media/PackageManagerConsoleControls1.png)

1. <span data-ttu-id="df0a1-128">Auswählen einer anderen Quelle und/oder ändert diese Standardwerte für nachfolgende Befehle.</span><span class="sxs-lookup"><span data-stu-id="df0a1-128">Selecting a different package source and/or project changes those defaults for subsequent commands.</span></span> <span data-ttu-id="df0a1-129">Auf einem diese Einstellungen ohne Ändern der Standardwerte, die meisten Befehle unterstützen `-Source` und `-ProjectName` Optionen.</span><span class="sxs-lookup"><span data-stu-id="df0a1-129">To overrride these settings without changing the defaults, most commands support `-Source` and `-ProjectName` options.</span></span>

1. <span data-ttu-id="df0a1-130">Wählen Sie das Zahnradsymbol, um Paketquellen zu verwalten.</span><span class="sxs-lookup"><span data-stu-id="df0a1-130">To manage package sources, select the gear icon.</span></span> <span data-ttu-id="df0a1-131">Dies ist eine Verknüpfung zu den **Tools > Optionen > NuGet-Paket-Manager > Paketquellen** wie beschrieben in das Dialogfeld die [-Paket-Manager-UI](package-manager-ui.md#package-sources) Seite.</span><span class="sxs-lookup"><span data-stu-id="df0a1-131">This is a shortcut to the **Tools > Options > NuGet Package Manager > Package Sources** dialog box as described on the [Package Manager UI](package-manager-ui.md#package-sources) page.</span></span> <span data-ttu-id="df0a1-132">Darüber hinaus löscht das Steuerelement rechts neben die Projektauswahl der Konsole Inhalt:</span><span class="sxs-lookup"><span data-stu-id="df0a1-132">Also, the control to the right of the project selector clears the console's contents:</span></span>

    ![Einstellungen für die Paket-Manager-Konsole und Steuerelemente löschen](media/PackageManagerConsoleControls2.png)

1. <span data-ttu-id="df0a1-134">Die Schaltfläche ganz rechts Hardwareinterrupts benötigt hat einen lang andauernden-Befehl.</span><span class="sxs-lookup"><span data-stu-id="df0a1-134">The rightmost button interrupts a long-running command.</span></span> <span data-ttu-id="df0a1-135">Z. B. Ausführung `Get-Package -ListAvailable -PageSize 500` Listet die Top-500-Pakete auf dem Quellcomputer (z. B. "NuGet.org"), dies kann einige Minuten dauern.</span><span class="sxs-lookup"><span data-stu-id="df0a1-135">For example, running `Get-Package -ListAvailable -PageSize 500` lists the top 500 packages on the default source (such as nuget.org), which could take several minutes to run.</span></span>

    ![Paket-Manager-Konsole beenden-Steuerelement](media/PackageManagerConsoleControls3.png)

## <a name="installing-a-package"></a><span data-ttu-id="df0a1-137">Installieren eines Pakets</span><span class="sxs-lookup"><span data-stu-id="df0a1-137">Installing a package</span></span>

```ps
# Add the Elmah package to the default project as specified in the console's project selector
Install-Package Elmah

# Add the Elmah package to a project named UtilitiesLib that is not the default
Install-Package Elmah -ProjectName UtilitiesLib
```

<span data-ttu-id="df0a1-138">Finden Sie unter [Install-Package](../tools/ps-ref-install-package.md).</span><span class="sxs-lookup"><span data-stu-id="df0a1-138">See [Install-Package](../tools/ps-ref-install-package.md).</span></span>

<span data-ttu-id="df0a1-139">Installieren eines Pakets in der Konsole führt die gleichen Schritte aus, wie im [was geschieht, wenn die Installation eines Pakets](../consume-packages/ways-to-install-a-package.md#what-happens-when-a-package-is-installed), mit den folgenden Ergänzungen:</span><span class="sxs-lookup"><span data-stu-id="df0a1-139">Installing a package in the console performs the same steps as described on [What happens when a package is installed](../consume-packages/ways-to-install-a-package.md#what-happens-when-a-package-is-installed), with the following additions:</span></span>

- <span data-ttu-id="df0a1-140">Die Konsole zeigt jeweils geltenden Lizenzbedingungen genannten in einem Fenster mit implizite Vereinbarung.</span><span class="sxs-lookup"><span data-stu-id="df0a1-140">The Console displays applicable license terms in its window with implied agreement.</span></span> <span data-ttu-id="df0a1-141">Wenn Sie den Lizenzbedingungen nicht einverstanden sind, sollten Sie das Paket sofort deinstallieren.</span><span class="sxs-lookup"><span data-stu-id="df0a1-141">If you do not agree to the terms, you should uninstall the package immediately.</span></span>
- <span data-ttu-id="df0a1-142">Außerdem ein Verweis auf das Paket wird in der Projektdatei hinzugefügt und wird im **Projektmappen-Explorer** unter der **Verweise** Knoten müssen Sie zum Speichern des Projekts, um die Änderungen in der Projektdatei direkt anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="df0a1-142">Also a reference to the package is added to the project file and appears in **Solution Explorer** under the **References** node, you need to save the project to see the changes in the project file directly.</span></span>

## <a name="uninstalling-a-package"></a><span data-ttu-id="df0a1-143">Wenn ein Paket deinstalliert</span><span class="sxs-lookup"><span data-stu-id="df0a1-143">Uninstalling a package</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```

<span data-ttu-id="df0a1-144">Finden Sie unter [Uninstall-Package](../tools/ps-ref-uninstall-package.md).</span><span class="sxs-lookup"><span data-stu-id="df0a1-144">See [Uninstall-Package](../tools/ps-ref-uninstall-package.md).</span></span> <span data-ttu-id="df0a1-145">Verwendung [Get-Package](../tools/ps-ref-get-package.md) , finden alle Pakete, die derzeit im Standardprojekt installiert, wenn Sie einen Bezeichner zu suchen müssen.</span><span class="sxs-lookup"><span data-stu-id="df0a1-145">Use [Get-Package](../tools/ps-ref-get-package.md) to see all packages currently installed in the default project if you need to find an identifier.</span></span>

<span data-ttu-id="df0a1-146">Wenn ein Paket deinstalliert führt folgende Aktionen aus:</span><span class="sxs-lookup"><span data-stu-id="df0a1-146">Uninstalling a package performs the following actions:</span></span>

- <span data-ttu-id="df0a1-147">Entfernt Verweise auf das Paket aus dem Projekt (und dem Managementobjektformat verwendet wird).</span><span class="sxs-lookup"><span data-stu-id="df0a1-147">Removes references to the package from the project (and whatever management format is in use).</span></span> <span data-ttu-id="df0a1-148">Verweise nicht mehr angezeigt werden, **Projektmappen-Explorer**.</span><span class="sxs-lookup"><span data-stu-id="df0a1-148">References no longer appear in **Solution Explorer**.</span></span> <span data-ttu-id="df0a1-149">(Zum Neuerstellen des Projekts, um daraus überprüfen müssen möglicherweise die **Bin** Ordner.)</span><span class="sxs-lookup"><span data-stu-id="df0a1-149">(You might need to rebuild the project to see it removed from the **Bin** folder.)</span></span>
- <span data-ttu-id="df0a1-150">Kehrt alle Änderungen an `app.config` oder `web.config` Wenn das Paket installiert wurde.</span><span class="sxs-lookup"><span data-stu-id="df0a1-150">Reverses any changes made to `app.config` or `web.config` when the package was installed.</span></span>
- <span data-ttu-id="df0a1-151">Entfernt zuvor installierte Abhängigkeiten, wenn keine verbleibenden Pakete diese Abhängigkeiten verwenden.</span><span class="sxs-lookup"><span data-stu-id="df0a1-151">Removes previously-installed dependencies if no remaining packages use those dependencies.</span></span>

## <a name="updating-a-package"></a><span data-ttu-id="df0a1-152">Aktualisieren eines Pakets</span><span class="sxs-lookup"><span data-stu-id="df0a1-152">Updating a package</span></span>

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

<span data-ttu-id="df0a1-153">Finden Sie unter [Get-Package](../tools/ps-ref-get-package.md) und [Update-Package](../tools/ps-ref-update-package.md)</span><span class="sxs-lookup"><span data-stu-id="df0a1-153">See [Get-Package](../tools/ps-ref-get-package.md) and [Update-Package](../tools/ps-ref-update-package.md)</span></span>

## <a name="finding-a-package"></a><span data-ttu-id="df0a1-154">Suchen ein Paket</span><span class="sxs-lookup"><span data-stu-id="df0a1-154">Finding a package</span></span>

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

<span data-ttu-id="df0a1-155">Finden Sie unter [Find-Package](../tools/ps-ref-find-package.md).</span><span class="sxs-lookup"><span data-stu-id="df0a1-155">See [Find-Package](../tools/ps-ref-find-package.md).</span></span> <span data-ttu-id="df0a1-156">Verwenden Sie in Visual Studio 2013 und früher [Get-Package](../tools/ps-ref-get-package.md) stattdessen.</span><span class="sxs-lookup"><span data-stu-id="df0a1-156">In Visual Studio 2013 and earlier, use [Get-Package](../tools/ps-ref-get-package.md) instead.</span></span>

## <a name="availability-of-the-console"></a><span data-ttu-id="df0a1-157">Verfügbarkeit der Konsole</span><span class="sxs-lookup"><span data-stu-id="df0a1-157">Availability of the console</span></span>

<span data-ttu-id="df0a1-158">In Visual Studio 2017 werden NuGet und den NuGet-Paket-Manager automatisch installiert, wenn Sie eine auswählen. NET-bezogenen Workloads; Sie können auch installieren sie einzeln Überprüfen der **einzelne Komponenten > Codetools > NuGet-Paket-Manager** -Option in der Visual Studio 2017-Installer.</span><span class="sxs-lookup"><span data-stu-id="df0a1-158">In Visual Studio 2017, NuGet and the NuGet Package Manager are automatically installed when you select any .NET-related workloads; you can also install it individually by checking the **Individual components > Code tools > NuGet package manager** option in the Visual Studio 2017 installer.</span></span>

<span data-ttu-id="df0a1-159">Überprüfen Sie auch, wenn Sie den NuGet-Paket-Manager in Visual Studio 2015 und früheren Versionen nicht vorhanden sind, **Tools > Erweiterungen und Updates...**  und suchen Sie nach der NuGet-Paket-Manager-Erweiterung.</span><span class="sxs-lookup"><span data-stu-id="df0a1-159">Also, if you're missing the NuGet Package Manager in Visual Studio 2015 and earlier, check **Tools > Extensions and Updates...** and search for the NuGet Package Manager extension.</span></span> <span data-ttu-id="df0a1-160">Wenn Sie nicht das Installationsprogramm für Erweiterungen in Visual Studio verwenden können, können Sie die Erweiterung direkt aus [ https://dist.nuget.org/index.html ](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="df0a1-160">If you're unable to use the extensions installer in Visual Studio, you can download the extension directly from [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span></span>

<span data-ttu-id="df0a1-161">Der Paket-Manager-Konsole ist zurzeit nicht verfügbar in Visual Studio für Mac.</span><span class="sxs-lookup"><span data-stu-id="df0a1-161">The Package Manager Console is not presently available with Visual Studio for Mac.</span></span> <span data-ttu-id="df0a1-162">Die entsprechenden Befehle, allerdings stehen über die [NuGet-CLI](nuget-exe-CLI-reference.md).</span><span class="sxs-lookup"><span data-stu-id="df0a1-162">The equivalent commands, however, are available through the [NuGet CLI](nuget-exe-CLI-reference.md).</span></span> <span data-ttu-id="df0a1-163">Visual Studio für Mac besitzt eine Benutzeroberfläche zum Verwalten von NuGet-Paketen.</span><span class="sxs-lookup"><span data-stu-id="df0a1-163">Visual Studio for Mac does have a UI for managing NuGet packages.</span></span> <span data-ttu-id="df0a1-164">Finden Sie unter [einschließen eines NuGet-Paket in Ihrem Projekt](/visualstudio/mac/nuget-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="df0a1-164">See [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span>

<span data-ttu-id="df0a1-165">Der Paket-Manager-Konsole ist nicht in Visual Studio Code enthalten.</span><span class="sxs-lookup"><span data-stu-id="df0a1-165">The Package Manager Console is not included with Visual Studio Code.</span></span>

## <a name="extending-the-package-manager-console"></a><span data-ttu-id="df0a1-166">Erweitern Sie die Paket-Manager-Konsole</span><span class="sxs-lookup"><span data-stu-id="df0a1-166">Extending the Package Manager Console</span></span>

<span data-ttu-id="df0a1-167">Einige Pakete installiert, neue Befehle für die Konsole.</span><span class="sxs-lookup"><span data-stu-id="df0a1-167">Some packages install new commands for the console.</span></span> <span data-ttu-id="df0a1-168">Z. B. `MvcScaffolding` erstellt Befehle wie `Scaffold` unten dargestellt, die ASP.NET MVC-Controller und Ansichten generiert:</span><span class="sxs-lookup"><span data-stu-id="df0a1-168">For example, `MvcScaffolding` creates commands like `Scaffold` shown below, which generates ASP.NET MVC controllers and views:</span></span>

![Installieren und Verwenden von MvcScaffold](media/PackageManagerConsoleInstall.png)

## <a name="setting-up-a-nuget-powershell-profile"></a><span data-ttu-id="df0a1-170">Ein NuGet-PowerShell-Profil einrichten</span><span class="sxs-lookup"><span data-stu-id="df0a1-170">Setting up a NuGet PowerShell profile</span></span>

<span data-ttu-id="df0a1-171">Ein PowerShell-Profil können Sie die häufig verwendete Befehle zur Verfügung stellen, wo Sie PowerShell verwenden.</span><span class="sxs-lookup"><span data-stu-id="df0a1-171">A PowerShell profile lets you make commonly-used commands available wherever you use PowerShell.</span></span> <span data-ttu-id="df0a1-172">NuGet unterstützt ein NuGet-spezifischen Profil, in der Regel am folgenden Speicherort gefunden:</span><span class="sxs-lookup"><span data-stu-id="df0a1-172">NuGet supports a NuGet-specific profile typically found at the following location:</span></span>

    %UserProfile%\Documents\WindowsPowerShell\NuGet_profile.ps1

<span data-ttu-id="df0a1-173">Um das Profil zu suchen, geben `$profile` in der Konsole:</span><span class="sxs-lookup"><span data-stu-id="df0a1-173">To find the profile, type `$profile` in the console:</span></span>

```ps
$profile
C:\Users\<user>\Documents\WindowsPowerShell\NuGet_profile.ps1
```

<span data-ttu-id="df0a1-174">Weitere Informationen finden Sie unter [Windows PowerShell-Profile](https://technet.microsoft.com/library/bb613488.aspx).</span><span class="sxs-lookup"><span data-stu-id="df0a1-174">For more details, refer to [Windows PowerShell Profiles](https://technet.microsoft.com/library/bb613488.aspx).</span></span>

## <a name="using-the-nugetexe-cli-in-the-console"></a><span data-ttu-id="df0a1-175">Verwenden die nuget.exe-CLI in der Konsole</span><span class="sxs-lookup"><span data-stu-id="df0a1-175">Using the nuget.exe CLI in the console</span></span>

<span data-ttu-id="df0a1-176">Vornehmen der [ `nuget.exe` CLI](nuget-exe-cli-reference.md) zur Verfügung, in der Paket-Manager-Konsole installieren die [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) Paket über die Konsole:</span><span class="sxs-lookup"><span data-stu-id="df0a1-176">To make the [`nuget.exe` CLI](nuget-exe-cli-reference.md) available in the Package Manager Console, install the [NuGet.CommandLine](http://www.nuget.org/packages/NuGet.CommandLine/) package from the console:</span></span>

```ps
# Other versions are available, see http://www.nuget.org/packages/NuGet.CommandLine/
Install-Package NuGet.CommandLine -Version 4.4.1
```
