---
title: Installieren und Verwalten von NuGet-Paketen mit der Konsole in Visual Studio
description: Anweisungen zum Verwenden der NuGet-Paket-Manager-Konsole in Visual Studio zum Arbeiten mit Paketen.
author: karann-msft
ms.author: karann
ms.date: 07/08/2019
ms.topic: conceptual
f1_keywords:
- vs.nuget.packagemanager.console
ms.openlocfilehash: 42031f7b5fe4d3c1b4dbe5e1bfbf9197014e0e88
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/07/2020
ms.locfileid: "79428576"
---
# <a name="install-and-manage-packages-with-the-package-manager-console-in-visual-studio-powershell"></a><span data-ttu-id="ad6d6-103">Installieren und Verwalten von Paketen mit der Paket-Manager-Konsole in Visual Studio (PowerShell)</span><span class="sxs-lookup"><span data-stu-id="ad6d6-103">Install and manage packages with the Package Manager Console in Visual Studio (PowerShell)</span></span>

<span data-ttu-id="ad6d6-104">Mit der NuGet-Paket-Manager-Konsole können Sie die [NuGet PowerShell-Befehle](../reference/powershell-reference.md) verwenden, um NuGet-Pakete zu suchen, zu installieren, zu deinstallieren und zu aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="ad6d6-104">The NuGet Package Manager Console lets you use [NuGet PowerShell commands](../reference/powershell-reference.md) to find, install, uninstall, and update NuGet packages.</span></span> <span data-ttu-id="ad6d6-105">Die Verwendung der Konsole ist dann erforderlich, wenn es mit der Benutzeroberfläche des Paket-Managers nicht möglich ist, einen Vorgang durchzuführen.</span><span class="sxs-lookup"><span data-stu-id="ad6d6-105">Using the console is necessary in cases where the Package Manager UI does not provide a way to perform an operation.</span></span> <span data-ttu-id="ad6d6-106">Informationen zur Verwendung von `nuget.exe`-CLI-Befehlen in der Konsole finden Sie unter [Verwenden der nuget.exe-CLI in der Konsole](#use-the-nugetexe-cli-in-the-console).</span><span class="sxs-lookup"><span data-stu-id="ad6d6-106">To use `nuget.exe` CLI commands in the console, see [Using the nuget.exe CLI in the console](#use-the-nugetexe-cli-in-the-console).</span></span>

<span data-ttu-id="ad6d6-107">Die Konsole ist in Visual Studio unter Windows integriert.</span><span class="sxs-lookup"><span data-stu-id="ad6d6-107">The console is built into Visual Studio on Windows.</span></span> <span data-ttu-id="ad6d6-108">Sie ist nicht in Visual Studio für Mac oder Visual Studio Code integriert.</span><span class="sxs-lookup"><span data-stu-id="ad6d6-108">It is not included with Visual Studio for Mac or Visual Studio Code.</span></span>

## <a name="find-and-install-a-package"></a><span data-ttu-id="ad6d6-109">Suchen und Installieren eines Pakets</span><span class="sxs-lookup"><span data-stu-id="ad6d6-109">Find and install a package</span></span>

<span data-ttu-id="ad6d6-110">Beispielsweise erfolgt das Suchen und Installieren eines Pakets in drei einfachen Schritten:</span><span class="sxs-lookup"><span data-stu-id="ad6d6-110">For example, finding and installing a package is done with three easy steps:</span></span>

1. <span data-ttu-id="ad6d6-111">Öffnen Sie das Projekt/die Projektmappe in Visual Studio und anschließend die Konsole mit dem Befehl **Tools > NuGet-Paket-Manager > Paket-Manager-Konsole**.</span><span class="sxs-lookup"><span data-stu-id="ad6d6-111">Open the project/solution in Visual Studio, and open the console using the **Tools > NuGet Package Manager > Package Manager Console** command.</span></span>

1. <span data-ttu-id="ad6d6-112">Suchen Sie das Paket, dass Sie installieren möchten.</span><span class="sxs-lookup"><span data-stu-id="ad6d6-112">Find the package you want to install.</span></span> <span data-ttu-id="ad6d6-113">Wenn Sie dies bereits kennen, fahren Sie mit Schritt 3 fort.</span><span class="sxs-lookup"><span data-stu-id="ad6d6-113">If you already know this, skip to step 3.</span></span>

    ```ps
    # Find packages containing the keyword "elmah"
    Find-Package elmah
    ```

1. <span data-ttu-id="ad6d6-114">Führen Sie den Installationsbefehl aus:</span><span class="sxs-lookup"><span data-stu-id="ad6d6-114">Run the install command:</span></span>

    ```ps
    # Install the Elmah package to the project named MyProject.
    Install-Package Elmah -ProjectName MyProject
    ```

> [!Important]
> <span data-ttu-id="ad6d6-115">Alle Vorgänge, die in der Konsole verfügbar sind, können auch mit der [NuGet-CLI](../reference/nuget-exe-cli-reference.md) durchgeführt werden.</span><span class="sxs-lookup"><span data-stu-id="ad6d6-115">All operations that are available in the console can also be done with the [NuGet CLI](../reference/nuget-exe-cli-reference.md).</span></span> <span data-ttu-id="ad6d6-116">Konsolenbefehle arbeiten jedoch im Kontext von Visual Studio und einem gespeichertem Projekt/einer Projektmappe und erreichen oft mehr als ihre entsprechenden CLI-Befehle.</span><span class="sxs-lookup"><span data-stu-id="ad6d6-116">However, console commands operate within the context of Visual Studio and a saved project/solution and often accomplish more than their equivalent CLI commands.</span></span> <span data-ttu-id="ad6d6-117">Wenn Sie beispielsweise ein Paket über die Konsole installieren, wird ein Verweis auf das Projekt hinzugefügt. Mit einem CLI-Befehl ist dies nicht der Fall.</span><span class="sxs-lookup"><span data-stu-id="ad6d6-117">For example, installing a package through the console adds a reference to the project whereas the CLI command does not.</span></span> <span data-ttu-id="ad6d6-118">Aus diesem Grund ziehen Entwickler, die in Visual Studio arbeiten, es in der Regel vor, die Konsole anstelle der CLI zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="ad6d6-118">For this reason, developers working in Visual Studio typically prefer using the console to the CLI.</span></span>

> [!Tip]
> <span data-ttu-id="ad6d6-119">Viele Konsolenvorgänge hängen davon ab, dass eine Projektmappe in Visual Studio mit einem bekannten Pfadnamen geöffnet wurde.</span><span class="sxs-lookup"><span data-stu-id="ad6d6-119">Many console operations depend on having a solution opened in Visual Studio with a known path name.</span></span> <span data-ttu-id="ad6d6-120">Wenn Sie eine nicht gespeicherte Projektmappe oder keine Projektmappe haben, wird folgender Fehler angezeigt: „Projektmappe wurde nicht geöffnet oder nicht gespeichert.</span><span class="sxs-lookup"><span data-stu-id="ad6d6-120">If you have an unsaved solution, or no solution, you can see the error, "Solution is not opened or not saved.</span></span> <span data-ttu-id="ad6d6-121">Stellen Sie sicher, dass Sie eine geöffnete und gespeicherte Projektmappe haben.“</span><span class="sxs-lookup"><span data-stu-id="ad6d6-121">Please ensure you have an open and saved solution."</span></span> <span data-ttu-id="ad6d6-122">Dadurch wird angegeben, dass die Konsole den Projektmappenordner nicht ermitteln kann.</span><span class="sxs-lookup"><span data-stu-id="ad6d6-122">This indicates that the console cannot determine the solution folder.</span></span> <span data-ttu-id="ad6d6-123">Durch das Speichern einer nicht gespeicherten Projektmappe oder das Erstellen und Speichern einer Projektmappe (wenn Sie keine offene Projektmappe haben), sollte der Fehler behoben werden.</span><span class="sxs-lookup"><span data-stu-id="ad6d6-123">Saving an unsaved solution, or creating and saving a solution if you don't have one open, should correct the error.</span></span>

## <a name="opening-the-console-and-console-controls"></a><span data-ttu-id="ad6d6-124">Öffnen der Konsolen-und der Konsolensteuerelemente</span><span class="sxs-lookup"><span data-stu-id="ad6d6-124">Opening the console and console controls</span></span>

1. <span data-ttu-id="ad6d6-125">Öffnen Sie die Konsole in Visual Studio mit dem Befehl **Tools > NuGet-Paket-Manager > Paket-Manager-Konsole**.</span><span class="sxs-lookup"><span data-stu-id="ad6d6-125">Open the console in Visual Studio using the **Tools > NuGet Package Manager > Package Manager Console** command.</span></span> <span data-ttu-id="ad6d6-126">Die Konsole ist ein Visual Studio-Fenster, das beliebig angeordnet und positioniert werden kann (siehe [Anpassen von Fensterlayouts in Visual Studio](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).</span><span class="sxs-lookup"><span data-stu-id="ad6d6-126">The console is a Visual Studio window that can be arranged and positioned however you like (see [Customize window layouts in Visual Studio](/visualstudio/ide/customizing-window-layouts-in-visual-studio)).</span></span>

1. <span data-ttu-id="ad6d6-127">Standardmäßig werden Konsolenbefehle gegen eine bestimmte Paketquelle und ein bestimmtes Projekt ausgeführt, wie es in dem Steuerelement am oberen Rand des Fensters festgelegt ist:</span><span class="sxs-lookup"><span data-stu-id="ad6d6-127">By default, console commands operate against a specific package source and project as set in the control at the top of the window:</span></span>

    ![Steuerelemente der Paket-Manager-Konsole für Paketquelle und Projekt](media/PackageManagerConsoleControls1.png)

1. <span data-ttu-id="ad6d6-129">Die Auswahl einer anderen Paketquelle und/oder eines anderen Projekts ändert diese Standardwerte für nachfolgende Befehle.</span><span class="sxs-lookup"><span data-stu-id="ad6d6-129">Selecting a different package source and/or project changes those defaults for subsequent commands.</span></span> <span data-ttu-id="ad6d6-130">Um diese Einstellungen zu überschreiben, ohne die Standardeinstellungen zu ändern, unterstützen die meisten Befehle die Optionen `-Source` und `-ProjectName`.</span><span class="sxs-lookup"><span data-stu-id="ad6d6-130">To overrride these settings without changing the defaults, most commands support `-Source` and `-ProjectName` options.</span></span>

1. <span data-ttu-id="ad6d6-131">Wählen Sie zum Verwalten von Paketquellen das Zahnradsymbol aus.</span><span class="sxs-lookup"><span data-stu-id="ad6d6-131">To manage package sources, select the gear icon.</span></span> <span data-ttu-id="ad6d6-132">Dies ist eine Verknüpfung zum Dialogfeld **Tools > Optionen > NuGet-Paket-Manager > Paketquellen**, wie auf der Seite [Benutzeroberfläche von Paket-Manager](install-use-packages-visual-studio.md#package-sources) beschrieben.</span><span class="sxs-lookup"><span data-stu-id="ad6d6-132">This is a shortcut to the **Tools > Options > NuGet Package Manager > Package Sources** dialog box as described on the [Package Manager UI](install-use-packages-visual-studio.md#package-sources) page.</span></span> <span data-ttu-id="ad6d6-133">Außerdem löscht das Steuerelement rechts neben der Projektauswahl den Inhalt der Konsole:</span><span class="sxs-lookup"><span data-stu-id="ad6d6-133">Also, the control to the right of the project selector clears the console's contents:</span></span>

    ![Einstellungen und Steuerelemente zum Löschen in der Paket-Manager-Konsole](media/PackageManagerConsoleControls2.png)

1. <span data-ttu-id="ad6d6-135">Die Schaltfläche ganz rechts unterbricht einen Befehl mit langer Ausführungszeit.</span><span class="sxs-lookup"><span data-stu-id="ad6d6-135">The rightmost button interrupts a long-running command.</span></span> <span data-ttu-id="ad6d6-136">Beispielsweise listet die Ausführung von `Get-Package -ListAvailable -PageSize 500` die 500 besten Pakete in der Standardquelle (z.B. nuget.org) auf, deren Ausführung mehrere Minuten dauern kann.</span><span class="sxs-lookup"><span data-stu-id="ad6d6-136">For example, running `Get-Package -ListAvailable -PageSize 500` lists the top 500 packages on the default source (such as nuget.org), which could take several minutes to run.</span></span>

    ![Steuerelement zum Anhalten von Befehlen in der Paket-Manager-Konsole](media/PackageManagerConsoleControls3.png)

## <a name="install-a-package"></a><span data-ttu-id="ad6d6-138">Installieren eines Pakets</span><span class="sxs-lookup"><span data-stu-id="ad6d6-138">Install a package</span></span>

```ps
# Add the Elmah package to the default project as specified in the console's project selector
Install-Package Elmah

# Add the Elmah package to a project named UtilitiesLib that is not the default
Install-Package Elmah -ProjectName UtilitiesLib
```

<span data-ttu-id="ad6d6-139">Siehe [Install-Package](../reference/ps-reference/ps-ref-install-package.md).</span><span class="sxs-lookup"><span data-stu-id="ad6d6-139">See [Install-Package](../reference/ps-reference/ps-ref-install-package.md).</span></span>

<span data-ttu-id="ad6d6-140">Die Installation eines Pakets in der Konsole führt die gleichen Schritte aus wie unter [Nach der Paketinstallation](../concepts/package-installation-process.md), mit den folgenden Ergänzungen:</span><span class="sxs-lookup"><span data-stu-id="ad6d6-140">Installing a package in the console performs the same steps as described on [What happens when a package is installed](../concepts/package-installation-process.md), with the following additions:</span></span>

- <span data-ttu-id="ad6d6-141">Die Konsole zeigt in ihrem Fenster die geltenden Lizenzbedingungen mit stillschweigender Zustimmung an.</span><span class="sxs-lookup"><span data-stu-id="ad6d6-141">The Console displays applicable license terms in its window with implied agreement.</span></span> <span data-ttu-id="ad6d6-142">Wenn Sie mit den Bedingungen nicht einverstanden sind, müssen Sie das Paket sofort deinstallieren.</span><span class="sxs-lookup"><span data-stu-id="ad6d6-142">If you do not agree to the terms, you should uninstall the package immediately.</span></span>
- <span data-ttu-id="ad6d6-143">Außerdem wird ein Verweis auf das Paket zur Projektdatei hinzugefügt und im **Projektmappen-Explorer** unter dem Knoten **Verweise** angezeigt. Sie müssen das Projekt speichern, um die Änderungen in der Projektdatei direkt anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="ad6d6-143">Also a reference to the package is added to the project file and appears in **Solution Explorer** under the **References** node, you need to save the project to see the changes in the project file directly.</span></span>

## <a name="uninstall-a-package"></a><span data-ttu-id="ad6d6-144">Deinstallieren eines Pakets</span><span class="sxs-lookup"><span data-stu-id="ad6d6-144">Uninstall a package</span></span>

```ps
# Uninstalls the Elmah package from the default project
Uninstall-Package Elmah

# Uninstalls the Elmah package and all its unused dependencies
Uninstall-Package Elmah -RemoveDependencies 

# Uninstalls the Elmah package even if another package depends on it
Uninstall-Package Elmah -Force
```

<span data-ttu-id="ad6d6-145">Siehe [Uninstall-Package](../reference/ps-reference/ps-ref-uninstall-package.md).</span><span class="sxs-lookup"><span data-stu-id="ad6d6-145">See [Uninstall-Package](../reference/ps-reference/ps-ref-uninstall-package.md).</span></span> <span data-ttu-id="ad6d6-146">Verwenden Sie [Get-Package](../reference/ps-reference/ps-ref-get-package.md), um alle Pakete anzuzeigen, die derzeit im Standardprojekt installiert sind, wenn Sie einen Bezeichner finden müssen.</span><span class="sxs-lookup"><span data-stu-id="ad6d6-146">Use [Get-Package](../reference/ps-reference/ps-ref-get-package.md) to see all packages currently installed in the default project if you need to find an identifier.</span></span>

<span data-ttu-id="ad6d6-147">Beim Deinstallieren eines Pakets werden die folgenden Aktionen durchführt:</span><span class="sxs-lookup"><span data-stu-id="ad6d6-147">Uninstalling a package performs the following actions:</span></span>

- <span data-ttu-id="ad6d6-148">Entfernt Verweise auf das Paket aus dem Projekt (und das verwendete Verwaltungsformat).</span><span class="sxs-lookup"><span data-stu-id="ad6d6-148">Removes references to the package from the project (and whatever management format is in use).</span></span> <span data-ttu-id="ad6d6-149">Verweise werden nicht mehr im **Projektmappen-Explorer** angezeigt.</span><span class="sxs-lookup"><span data-stu-id="ad6d6-149">References no longer appear in **Solution Explorer**.</span></span> <span data-ttu-id="ad6d6-150">(Möglicherweise müssen Sie das Projekt neu erstellen, damit es aus dem Ordner **Bin** entfernt wird.)</span><span class="sxs-lookup"><span data-stu-id="ad6d6-150">(You might need to rebuild the project to see it removed from the **Bin** folder.)</span></span>
- <span data-ttu-id="ad6d6-151">Macht alle Änderungen rückgängig, die an `app.config` oder `web.config` vorgenommen wurden, als das Paket installiert wurde.</span><span class="sxs-lookup"><span data-stu-id="ad6d6-151">Reverses any changes made to `app.config` or `web.config` when the package was installed.</span></span>
- <span data-ttu-id="ad6d6-152">Entfernt zuvor installierte Abhängigkeiten, wenn diese Abhängigkeiten von keinem verbleibenden Paket verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="ad6d6-152">Removes previously-installed dependencies if no remaining packages use those dependencies.</span></span>

## <a name="update-a-package"></a><span data-ttu-id="ad6d6-153">Aktualisieren eines Pakets</span><span class="sxs-lookup"><span data-stu-id="ad6d6-153">Update a package</span></span>

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

<span data-ttu-id="ad6d6-154">Siehe [Get-Package](../reference/ps-reference/ps-ref-get-package.md) und [Update-Package](../reference/ps-reference/ps-ref-update-package.md).</span><span class="sxs-lookup"><span data-stu-id="ad6d6-154">See [Get-Package](../reference/ps-reference/ps-ref-get-package.md) and [Update-Package](../reference/ps-reference/ps-ref-update-package.md)</span></span>

## <a name="find-a-package"></a><span data-ttu-id="ad6d6-155">Suchen eines Pakets</span><span class="sxs-lookup"><span data-stu-id="ad6d6-155">Find a package</span></span>

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

<span data-ttu-id="ad6d6-156">Siehe [Find-Package](../reference/ps-reference/ps-ref-find-package.md).</span><span class="sxs-lookup"><span data-stu-id="ad6d6-156">See [Find-Package](../reference/ps-reference/ps-ref-find-package.md).</span></span> <span data-ttu-id="ad6d6-157">Verwenden Sie in Visual Studio 2013 und früheren Versionen stattdessen [Get-Package](../reference/ps-reference/ps-ref-get-package.md).</span><span class="sxs-lookup"><span data-stu-id="ad6d6-157">In Visual Studio 2013 and earlier, use [Get-Package](../reference/ps-reference/ps-ref-get-package.md) instead.</span></span>

## <a name="availability-of-the-console"></a><span data-ttu-id="ad6d6-158">Verfügbarkeit der Konsole</span><span class="sxs-lookup"><span data-stu-id="ad6d6-158">Availability of the console</span></span>

<span data-ttu-id="ad6d6-159">Ab Visual Studio 2017 werden NuGet und der NuGet-Paket-Manager automatisch installiert, wenn Sie .NET-bezogene Workloads auswählen. Sie können sie auch einzeln installieren, indem Sie die Option **Einzelne Komponenten > Codetools > NuGet-Paket-Manager** im Visual Studio-Installationsprogramm aktivieren.</span><span class="sxs-lookup"><span data-stu-id="ad6d6-159">Starting in Visual Studio 2017, NuGet and the NuGet Package Manager are automatically installed when you select any .NET-related workloads; you can also install it individually by checking the **Individual components > Code tools > NuGet package manager** option in the Visual Studio installer.</span></span>

<span data-ttu-id="ad6d6-160">Wenn der NuGet-Paket-Manager in Visual Studio 2015 und früher fehlt, aktivieren Sie **Tools > Erweiterungen und Updates...** , und suchen Sie nach der Erweiterung für den NuGet-Paket-Manager.</span><span class="sxs-lookup"><span data-stu-id="ad6d6-160">Also, if you're missing the NuGet Package Manager in Visual Studio 2015 and earlier, check **Tools > Extensions and Updates...** and search for the NuGet Package Manager extension.</span></span> <span data-ttu-id="ad6d6-161">Wenn Sie das Installationsprogramm für Erweiterungen in Visual Studio nicht verwenden können, können Sie die Erweiterung direkt von [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html) herunterladen.</span><span class="sxs-lookup"><span data-stu-id="ad6d6-161">If you're unable to use the extensions installer in Visual Studio, you can download the extension directly from [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span></span>

<span data-ttu-id="ad6d6-162">Die Paket-Manager-Konsole ist derzeit nicht in Visual Studio für Mac verfügbar.</span><span class="sxs-lookup"><span data-stu-id="ad6d6-162">The Package Manager Console is not presently available with Visual Studio for Mac.</span></span> <span data-ttu-id="ad6d6-163">Die entsprechenden Befehle sind jedoch über die [NuGet-CLI](../reference/nuget-exe-CLI-reference.md) verfügbar.</span><span class="sxs-lookup"><span data-stu-id="ad6d6-163">The equivalent commands, however, are available through the [NuGet CLI](../reference/nuget-exe-CLI-reference.md).</span></span> <span data-ttu-id="ad6d6-164">Visual Studio für Mac verfügt über eine Benutzeroberfläche zum Verwalten von NuGet-Paketen.</span><span class="sxs-lookup"><span data-stu-id="ad6d6-164">Visual Studio for Mac does have a UI for managing NuGet packages.</span></span> <span data-ttu-id="ad6d6-165">Siehe [Einschließen eines NuGet-Pakets in Ihr Projekt](/visualstudio/mac/nuget-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="ad6d6-165">See [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span>

<span data-ttu-id="ad6d6-166">Die Paket-Manager-Konsole ist nicht in Visual Studio Code enthalten.</span><span class="sxs-lookup"><span data-stu-id="ad6d6-166">The Package Manager Console is not included with Visual Studio Code.</span></span>

## <a name="extend-the-package-manager-console"></a><span data-ttu-id="ad6d6-167">Erweitern der Paket-Manager-Konsole</span><span class="sxs-lookup"><span data-stu-id="ad6d6-167">Extend the Package Manager Console</span></span>

<span data-ttu-id="ad6d6-168">Einige Pakete installieren neue Befehle für die Konsole.</span><span class="sxs-lookup"><span data-stu-id="ad6d6-168">Some packages install new commands for the console.</span></span> <span data-ttu-id="ad6d6-169">Beispielsweise erstellt `MvcScaffolding` Befehle wie `Scaffold`, wie unten gezeigt, die ASP.NET MVC-Controller und -Ansichten generieren:</span><span class="sxs-lookup"><span data-stu-id="ad6d6-169">For example, `MvcScaffolding` creates commands like `Scaffold` shown below, which generates ASP.NET MVC controllers and views:</span></span>

![Installieren und Verwenden von MvcScaffold](media/PackageManagerConsoleInstall.png)

## <a name="set-up-a-nuget-powershell-profile"></a><span data-ttu-id="ad6d6-171">Einrichten eines NuGet-PowerShell-Profils</span><span class="sxs-lookup"><span data-stu-id="ad6d6-171">Set up a NuGet PowerShell profile</span></span>

<span data-ttu-id="ad6d6-172">Mit einem PowerShell-Profil können Sie häufig verwendete Befehle überall dort verfügbar machen, wo Sie PowerShell verwenden.</span><span class="sxs-lookup"><span data-stu-id="ad6d6-172">A PowerShell profile lets you make commonly-used commands available wherever you use PowerShell.</span></span> <span data-ttu-id="ad6d6-173">NuGet unterstützt ein NuGet-spezifisches Profil, das in der Regel an folgendem Speicherort zu finden ist:</span><span class="sxs-lookup"><span data-stu-id="ad6d6-173">NuGet supports a NuGet-specific profile typically found at the following location:</span></span>

    %UserProfile%\Documents\WindowsPowerShell\NuGet_profile.ps1

<span data-ttu-id="ad6d6-174">Um das Profil zu suchen, geben Sie `$profile` in der Konsole ein:</span><span class="sxs-lookup"><span data-stu-id="ad6d6-174">To find the profile, type `$profile` in the console:</span></span>

```ps
$profile
C:\Users\<user>\Documents\WindowsPowerShell\NuGet_profile.ps1
```

<span data-ttu-id="ad6d6-175">Weitere Informationen finden Sie unter [Windows PowerShell-Profile.](https://technet.microsoft.com/library/bb613488.aspx)</span><span class="sxs-lookup"><span data-stu-id="ad6d6-175">For more details, refer to [Windows PowerShell Profiles](https://technet.microsoft.com/library/bb613488.aspx).</span></span>

## <a name="use-the-nugetexe-cli-in-the-console"></a><span data-ttu-id="ad6d6-176">Verwenden der nuget.exe-CLI in der-Konsole</span><span class="sxs-lookup"><span data-stu-id="ad6d6-176">Use the nuget.exe CLI in the console</span></span>

<span data-ttu-id="ad6d6-177">Um die [`nuget.exe`-CLI](../reference/nuget-exe-cli-reference.md) in der Paket-Manager-Konsole verfügbar zu machen, installieren Sie das Paket [NuGet.CommandLine](https://www.nuget.org/packages/NuGet.CommandLine/) über die Konsole:</span><span class="sxs-lookup"><span data-stu-id="ad6d6-177">To make the [`nuget.exe` CLI](../reference/nuget-exe-cli-reference.md) available in the Package Manager Console, install the [NuGet.CommandLine](https://www.nuget.org/packages/NuGet.CommandLine/) package from the console:</span></span>

```ps
# Other versions are available, see https://www.nuget.org/packages/NuGet.CommandLine/
Install-Package NuGet.CommandLine -Version 4.4.1
```
