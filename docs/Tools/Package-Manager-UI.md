---
title: "Benutzeroberflächenreferenz für NuGet-Paket-Manager | Microsoft Docs"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/08/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
f1_keywords:
- vs.toolsoptionspages.nuget_package_manager
- vs.toolsoptionspages.nuget_package_manager.general
- vs.toolsoptionspages.nuget_package_manager.package_sources
- vs.nuget.packagemanager.ui
description: "Anweisungen für die Verwendung der NuGet-Paket-Manager-UI in Visual Studio für die Arbeit mit NuGet-Pakete."
keywords: "NuGet UI, NuGet-Paket-Manager NuGet in Visual Studio, Verwalten von NuGet-Pakete, die NuGet-Benutzeroberfläche, die Paket-Manager in Visual Studio-Benutzeroberfläche"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 35bb856ccff43c77af7eac67da4614d83dcdc533
ms.sourcegitcommit: 8f26d10bdf256f72962010348083ff261dae81b9
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/08/2018
---
# <a name="nuget-package-manager-ui"></a><span data-ttu-id="c7b16-104">NuGet-Paket-Manager-Benutzeroberfläche</span><span class="sxs-lookup"><span data-stu-id="c7b16-104">NuGet Package Manager UI</span></span>

<span data-ttu-id="c7b16-105">Die NuGet-Paket-Manager-UI in Visual Studio unter Windows können Sie problemlos installieren, deinstallieren und Aktualisieren von NuGet-Pakete in Projekten und Projektmappen.</span><span class="sxs-lookup"><span data-stu-id="c7b16-105">The NuGet Package Manager UI in Visual Studio on Windows allows you to easily install, uninstall, and update NuGet packages in projects and solutions.</span></span> <span data-ttu-id="c7b16-106">Die Erfahrung in Visual Studio für Mac, finden Sie unter [einschließlich eines NuGet-Paket im Projekt](/visualstudio/mac/nuget-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="c7b16-106">For the experience in Visual Studio for Mac, see [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span> <span data-ttu-id="c7b16-107">Die Paket-Manager-UI kann nicht mit Visual Studio-Code enthalten ist.</span><span class="sxs-lookup"><span data-stu-id="c7b16-107">The Package Manager UI is not included with Visual Studio Code.</span></span>

<span data-ttu-id="c7b16-108">In diesem Thema:</span><span class="sxs-lookup"><span data-stu-id="c7b16-108">In this topic:</span></span>

- [<span data-ttu-id="c7b16-109">Suchen und installieren ein Paket (Registerkarte "Durchsuchen")</span><span class="sxs-lookup"><span data-stu-id="c7b16-109">Finding and installing a package (Browse tab)</span></span>](#finding-and-installing-a-package)
- [<span data-ttu-id="c7b16-110">Deinstallieren ein Paket (Registerkarte "installiert")</span><span class="sxs-lookup"><span data-stu-id="c7b16-110">Uninstalling a package (Installed tab)</span></span>](#uninstalling-a-package)
- <span data-ttu-id="c7b16-111">[Aktualisieren eines Pakets (Registerkarten installiert und Updates)](#updating-a-package) (enthält die ["Implizit auf die verwiesen wird durch ein SDK" oder "AutoReferenced" Nachricht](#implicit_reference))</span><span class="sxs-lookup"><span data-stu-id="c7b16-111">[Updating a package (Installed and Updates tabs)](#updating-a-package) (includes the ["Implicitly referenced by an SDK" or "AutoReferenced" message](#implicit_reference))</span></span>
- <span data-ttu-id="c7b16-112">[Verwalten von Paketen für die Projektmappe](#managing-packages-for-the-solution) (Arbeiten mit mehreren Projekten gleichzeitig).</span><span class="sxs-lookup"><span data-stu-id="c7b16-112">[Managing packages for the solution](#managing-packages-for-the-solution) (working with multiple projects at the same time).</span></span>
- [<span data-ttu-id="c7b16-113">Paketquellen</span><span class="sxs-lookup"><span data-stu-id="c7b16-113">Package sources</span></span>](#package-sources)
- [<span data-ttu-id="c7b16-114">Paket-Manager-Optionen steuern</span><span class="sxs-lookup"><span data-stu-id="c7b16-114">Package manager Options control</span></span>](#package-manager-options-control)

> [!Note]
> <span data-ttu-id="c7b16-115">Wenn Sie das NuGet-Paket-Manager in Visual Studio 2015 nicht vorhanden sind, überprüfen Sie **Tools > Erweiterungen und Updates...**  , suchen Sie nach der *NuGet Package Manager* Erweiterung.</span><span class="sxs-lookup"><span data-stu-id="c7b16-115">If you're missing the NuGet Package Manager in Visual Studio 2015, check **Tools > Extensions and Updates...** and search for the *NuGet Package Manager* extension.</span></span> <span data-ttu-id="c7b16-116">Wenn Sie nicht das Installationsprogramm für Erweiterungen in Visual Studio verwenden möchten, laden Sie die Erweiterung direkt aus [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="c7b16-116">If you're unable to use the extensions installer in Visual Studio, download the extension directly from [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span></span>
>
> <span data-ttu-id="c7b16-117">In Visual Studio 2017 werden NuGet und NuGet-Paket-Manager automatisch mit installiert. NET-bezogenen Arbeitslasten.</span><span class="sxs-lookup"><span data-stu-id="c7b16-117">In Visual Studio 2017, NuGet and the NuGet Package Manager are automatically installed with any .NET-related workloads.</span></span> <span data-ttu-id="c7b16-118">Dazu einzeln Installieren der **Einzelkomponenten > Code Extras > NuGet-Paket-Manager** -Option in Visual Studio 2017 Installationsprogramm.</span><span class="sxs-lookup"><span data-stu-id="c7b16-118">Install it individually by selecting the **Individual components > Code tools > NuGet package manager** option in the Visual Studio 2017 installer.</span></span>

## <a name="finding-and-installing-a-package"></a><span data-ttu-id="c7b16-119">Suchen und Installieren eines Pakets</span><span class="sxs-lookup"><span data-stu-id="c7b16-119">Finding and installing a package</span></span>

1. <span data-ttu-id="c7b16-120">In **Projektmappen-Explorer**, mit der rechten Maustaste entweder **Verweise** oder ein Projekt, und wählen **NuGet-Pakete verwalten...** .</span><span class="sxs-lookup"><span data-stu-id="c7b16-120">In **Solution Explorer**, right-click either **References**  or a project and select **Manage NuGet Packages...**.</span></span>

    ![Menüoption für NuGet-Pakete verwalten](media/ManagePackagesUICommand.png)

1. <span data-ttu-id="c7b16-122">Die **Durchsuchen** Registerkarte zeigt die Pakete nach verwendungshäufigkeit von der aktuell ausgewählten Quelle (finden Sie unter [Paket Quellen](#package-sources)).</span><span class="sxs-lookup"><span data-stu-id="c7b16-122">The **Browse** tab displays packages by popularity from the currently selected source (see [package sources](#package-sources)).</span></span> <span data-ttu-id="c7b16-123">Suchen Sie nach einem bestimmten Paket mithilfe des Suchfelds auf der linken oberen Ecke.</span><span class="sxs-lookup"><span data-stu-id="c7b16-123">Search for a specific package using the search box on the upper left.</span></span> <span data-ttu-id="c7b16-124">Wählen Sie ein Paket aus der Liste, um dessen Informationen anzuzeigen, wodurch die können auch die **installieren** zusammen mit einem Versionsauswahl Dropdown-Schaltfläche.</span><span class="sxs-lookup"><span data-stu-id="c7b16-124">Select a package from the list to display its information, which also enables the **Install** button along with a version-selection drop-down.</span></span>

    ![Verwalten von NuGet-Pakete Dialogfeld Durchsuchen Registerkarte](media/Search.png)

1. <span data-ttu-id="c7b16-126">Wählen Sie die gewünschte Version aus der Dropdownliste aus, und wählen Sie **installieren**.</span><span class="sxs-lookup"><span data-stu-id="c7b16-126">Select the desired version from the drop-down and select **Install**.</span></span> <span data-ttu-id="c7b16-127">Visual Studio installiert das Paket und seine Abhängigkeiten im Projekt.</span><span class="sxs-lookup"><span data-stu-id="c7b16-127">Visual Studio installs the package and its dependencies into the project.</span></span> <span data-ttu-id="c7b16-128">Möglicherweise werden Sie aufgefordert, Lizenzbedingungen zu akzeptieren.</span><span class="sxs-lookup"><span data-stu-id="c7b16-128">You may be asked to accept license terms.</span></span> <span data-ttu-id="c7b16-129">Nach Abschluss der Installation zusätzliche Pakete angezeigt werden, auf die **installiert** Registerkarte. Pakete werden ebenfalls aufgeführt, der **Verweise** Knoten des Projektmappen-Explorer, der angibt, dass Sie im Projekt die darauf verweisen können `using` Anweisungen.</span><span class="sxs-lookup"><span data-stu-id="c7b16-129">When installation is complete, the added packages appear on the **Installed** tab. Packages are also listed in the **References** node of Solution Explorer, indicating that you can refer to them in the project with `using` statements.</span></span>

    ![Verweise im Projektmappen-Explorer](media/References.png)

> [!Tip]
    > <span data-ttu-id="c7b16-131">Vorabversionen in die Suche einbeziehen und Vorabversionen Dropdown-in der Version verfügbar machen möchten, wählen Sie die **Vorabversion einschließen** Option.</span><span class="sxs-lookup"><span data-stu-id="c7b16-131">To include prerelease versions in the search, and to make prerelease versions available in the version drop-down, select the **Include prerelease** option.</span></span>

## <a name="uninstalling-a-package"></a><span data-ttu-id="c7b16-132">Deinstallieren eines Pakets</span><span class="sxs-lookup"><span data-stu-id="c7b16-132">Uninstalling a package</span></span>

1. <span data-ttu-id="c7b16-133">In **Projektmappen-Explorer**, mit der rechten Maustaste entweder **Verweise** oder das gewünschte Projekt, und die Select **NuGet-Pakete verwalten...** .</span><span class="sxs-lookup"><span data-stu-id="c7b16-133">In **Solution Explorer**, right-click either **References** or the desired project, and select **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="c7b16-134">Wählen Sie die **installiert** Registerkarte.</span><span class="sxs-lookup"><span data-stu-id="c7b16-134">Select the **Installed** tab.</span></span>
1. <span data-ttu-id="c7b16-135">Wählen Sie das Paket deinstallieren (mithilfe der Suche zum Filtern der Liste aus, falls erforderlich), und wählen **Deinstallieren**.</span><span class="sxs-lookup"><span data-stu-id="c7b16-135">Select the package to uninstall (using search to filter the list if necessary) and select **Uninstall**.</span></span>

    ![Deinstallieren eines Pakets](media/UninstallPackage.png)

1. <span data-ttu-id="c7b16-137">Beachten Sie, dass die **Include Vorabversion** und **Paketquelle** Steuerelemente haben keine Auswirkungen, wenn Sie Pakete zu deinstallieren.</span><span class="sxs-lookup"><span data-stu-id="c7b16-137">Note that the **Include prerelease** and **Package source** controls have no effect when uninstalling packages.</span></span>

## <a name="updating-a-package"></a><span data-ttu-id="c7b16-138">Aktualisieren eines Pakets</span><span class="sxs-lookup"><span data-stu-id="c7b16-138">Updating a package</span></span>

1. <span data-ttu-id="c7b16-139">In **Projektmappen-Explorer**, mit der rechten Maustaste entweder **Verweise** oder das gewünschte Projekt, und die Select **NuGet-Pakete verwalten...** . (Websiteprojekte, mit der Maustaste die **"bin"** Ordner.)</span><span class="sxs-lookup"><span data-stu-id="c7b16-139">In **Solution Explorer**, right-click either **References** or the desired project, and select **Manage NuGet Packages...**. (In web site projects, right-click the **Bin** folder.)</span></span>
1. <span data-ttu-id="c7b16-140">Wählen Sie die **Updates** Registerkarte ", um Pakete anzuzeigen, die aus der ausgewählten Paketquellen verfügbaren Updates verfügen.</span><span class="sxs-lookup"><span data-stu-id="c7b16-140">Select the **Updates** tab to see packages that have available updates from the selected package sources.</span></span> <span data-ttu-id="c7b16-141">Wählen Sie **Vorabversion einschließen** Vorabversionen von Paketen in der Updateliste eingeschlossen werden sollen.</span><span class="sxs-lookup"><span data-stu-id="c7b16-141">Select **Include prerelease** to include prerelease packages in the update list.</span></span>
1. <span data-ttu-id="c7b16-142">Wählen Sie das Paket zu aktualisieren, wählen die gewünschte Version aus der Dropdownliste auf der rechten Seite, und wählen Sie **aktualisieren**.</span><span class="sxs-lookup"><span data-stu-id="c7b16-142">Select the package to update, select the desired version from the drop-down on the right, and select **Update**.</span></span>

    ![Aktualisieren eines Pakets](media/UpdatePackages.png)

1. <a name="implicit_reference"></a><span data-ttu-id="c7b16-144">Für einige Pakete die **Update** Schaltfläche ist deaktiviert, und eine Meldung angezeigt, die besagt, dass "implizit ein SDK verweist" (oder "AutoReferenced").</span><span class="sxs-lookup"><span data-stu-id="c7b16-144">For some packages, the **Update** button is disabled and a message appears saying that it's "Implicitly referenced by an SDK" (or "AutoReferenced").</span></span> <span data-ttu-id="c7b16-145">Die Meldung gibt an, dass das Paket, z. B. Microsoft.NETCore.App oder Microsoft.NETStandard.Library, Teil eines größeren Framework oder SDK ist und nicht unabhängig voneinander aktualisiert werden sollten.</span><span class="sxs-lookup"><span data-stu-id="c7b16-145">The message indicates that the package, such as Microsoft.NETCore.App or Microsoft.NETStandard.Library, is part of a larger framework or SDK and should not be updated independently.</span></span> <span data-ttu-id="c7b16-146">(Solche Pakete sind intern mit markierten `<IsImplicitlyDefined>True</IsImplicitlyDefined>`.) Um das Paket zu aktualisieren, aktualisieren Sie das SDK zu dem er gehört.</span><span class="sxs-lookup"><span data-stu-id="c7b16-146">(Such packages are internally marked with `<IsImplicitlyDefined>True</IsImplicitlyDefined>`.) To update the package, update the SDK to which it belongs.</span></span>

    ![Beispielpaket als implizit gekennzeichnet sein, Verweise oder AutoReferenced](media/PackageManagerUIAutoReferenced.png)

1. <span data-ttu-id="c7b16-148">Um mehrere Pakete auf die neuesten Version zu aktualisieren, wählen sie in der Liste aus und wählen Sie die **aktualisieren** Schaltfläche über der Liste.</span><span class="sxs-lookup"><span data-stu-id="c7b16-148">To update multiple packages to their newest versions, select  them in the list and select the **Update** button above the list.</span></span>
1. <span data-ttu-id="c7b16-149">Sie können auch ein einzelnes Paket aus Aktualisieren der **installiert** Registerkarte. In diesem Fall enthalten die Details für das Paket einen Selektor Version (unterliegen die **Include Vorabversion** Option) und ein **Update** Schaltfläche.</span><span class="sxs-lookup"><span data-stu-id="c7b16-149">You can also update an individual package from the **Installed** tab. In this case, the details for the package include a version selector (subject to the **Include prerelease** option) and an **Update** button.</span></span>

## <a name="managing-packages-for-the-solution"></a><span data-ttu-id="c7b16-150">Verwalten von Paketen für die Projektmappe</span><span class="sxs-lookup"><span data-stu-id="c7b16-150">Managing packages for the solution</span></span>

<span data-ttu-id="c7b16-151">Verwalten von Paketen für eine Projektmappe ist eine bequeme Möglichkeit gleichzeitig mit mehreren Projekten arbeiten.</span><span class="sxs-lookup"><span data-stu-id="c7b16-151">Managing packages for a solution is a convenient means to work with multiple projects simultaneously.</span></span>

1. <span data-ttu-id="c7b16-152">Wählen Sie die **Extras > NuGet-Paket-Manager > NuGet-Pakete für Projektmappe verwalten...**  Menü-Befehls oder mit der rechten Maustaste in der Projektmappe, und wählen Sie **NuGet-Pakete verwalten...** :</span><span class="sxs-lookup"><span data-stu-id="c7b16-152">Select the **Tools > NuGet Package Manager > Manage NuGet Packages for Solution...** menu command, or right-click the solution and select **Manage NuGet Packages...**:</span></span>

    ![Verwalten von NuGet-Pakete für die Projektmappe](media/ManagePackagesSolutionUICommand.png)

1. <span data-ttu-id="c7b16-154">Wenn Sie Pakete für die Projektmappe zu verwalten, kann die Benutzeroberfläche Sie die Projekte auswählen, die von den Vorgängen betroffen sind:</span><span class="sxs-lookup"><span data-stu-id="c7b16-154">When managing packages for the solution, the UI lets you select the projects that are affected by the operations:</span></span>

    ![Projekt-Selektor beim Verwalten von Paketen für die Projektmappe](media/SolutionPackagesUI.png)

### <a name="consolidate-tab"></a><span data-ttu-id="c7b16-156">Registerkarte "Konsolidieren</span><span class="sxs-lookup"><span data-stu-id="c7b16-156">Consolidate tab</span></span>

<span data-ttu-id="c7b16-157">Entwickler halten es in der Regel nicht üblich, verschiedene Versionen desselben NuGet-Pakets über verschiedene Projekte in der gleichen Projektmappe verwenden.</span><span class="sxs-lookup"><span data-stu-id="c7b16-157">Developers typically consider it bad practice to use different versions of the same NuGet package across different projects in the same solution.</span></span> <span data-ttu-id="c7b16-158">Wenn Sie zum Verwalten von Paketen für eine Projektmappe auswählen, die Paket-Manager-UI bietet eine **konsolidieren** Registerkarte auf dem können Sie problemlos nachvollziehen, in denen Pakete mit unterschiedlichen Versionsnummern von verschiedenen Projekten in der Projektmappe verwendet werden:</span><span class="sxs-lookup"><span data-stu-id="c7b16-158">When you choose to manage packages for a solution, the Package Manager UI provides a **Consolidate** tab on which you can easily see where packages with distinct version numbers are used by different projects in the solution:</span></span>

![Paket-Manager-Benutzeroberfläche konsolidieren Registerkarte](media/ConsolidateTab.png)

<span data-ttu-id="c7b16-160">In diesem Beispiel wird das Projekt "ClassLibrary1" EntityFramework 6.2.0 fest, verwendet, wohingegen ConsoleApp1 EntityFramework 6.1.0 verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="c7b16-160">In this example, the ClassLibrary1 project is using EntityFramework 6.2.0, whereas ConsoleApp1 is using EntityFramework 6.1.0.</span></span> <span data-ttu-id="c7b16-161">Führen Sie folgende Schritte aus, um Paketversionen zu konsolidieren:</span><span class="sxs-lookup"><span data-stu-id="c7b16-161">To consolidate package versions, do the following:</span></span>

- <span data-ttu-id="c7b16-162">Wählen Sie die Projekte in der Projektliste aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="c7b16-162">Select the projects to update in the project list.</span></span>
- <span data-ttu-id="c7b16-163">Wählen Sie die Version, verwenden Sie diese Projekte in der **Version** Kontrolle, z. B. EntityFramework 6.2.0 fest.</span><span class="sxs-lookup"><span data-stu-id="c7b16-163">Select the version to use in all those projects in the **Version** control, such as EntityFramework 6.2.0.</span></span>
- <span data-ttu-id="c7b16-164">Wählen Sie die **installieren** Schaltfläche.</span><span class="sxs-lookup"><span data-stu-id="c7b16-164">Select the **Install** button.</span></span>

<span data-ttu-id="c7b16-165">Die Paket-Manager installiert die Version des ausgewählten Pakets in allen ausgewählten Projekte nach dem das Paket nicht mehr angezeigt wird auf die **konsolidieren** Registerkarte.</span><span class="sxs-lookup"><span data-stu-id="c7b16-165">The Package Manager installs the selected package version into all selected projects, after which the package no longer appears on the **Consolidate** tab.</span></span>

## <a name="package-sources"></a><span data-ttu-id="c7b16-166">Paketquellen</span><span class="sxs-lookup"><span data-stu-id="c7b16-166">Package sources</span></span>

<span data-ttu-id="c7b16-167">Wählen Sie eine aus dem Quell-Selektor Schritte aus, um die Quelle zu ändern, aus dem Visual Studio ruft Pakete ab:</span><span class="sxs-lookup"><span data-stu-id="c7b16-167">To change the source from which Visual Studio obtains packages, select one from the source selector:</span></span>

![Paket-Quelle-Selektor in der Paket-Manager-Benutzeroberfläche](media/PackageSourceDropDown.png)

<span data-ttu-id="c7b16-169">So verwalten Sie die Paketquellen überein:</span><span class="sxs-lookup"><span data-stu-id="c7b16-169">To manage package sources:</span></span>

1. <span data-ttu-id="c7b16-170">Wählen Sie die **Einstellungen** Symbol in der Paket-Manager-UI unten beschriebenen, oder verwenden Sie die **Tools > Optionen** Befehl und einen Bildlauf zu **NuGet Package Manager**:</span><span class="sxs-lookup"><span data-stu-id="c7b16-170">Select the **Settings** icon in the Package Manager UI outlined below or use the **Tools > Options** command and scroll to **NuGet Package Manager**:</span></span>

    ![Symbol "Einstellungen" Paket-Manager-Benutzeroberfläche](media/PackageSourceSettings.png)

1. <span data-ttu-id="c7b16-172">Wählen Sie die **Paketquellen** Knoten:</span><span class="sxs-lookup"><span data-stu-id="c7b16-172">Select the **Package Sources** node:</span></span>

    ![Quellen Paketoptionen](media/options.png)

1. <span data-ttu-id="c7b16-174">Wählen Sie zum Hinzufügen einer Quelle  **+** , bearbeiten Sie den Namen, geben Sie die URL oder Pfad in der **Quelle** Steuerelement, und wählen Sie **Update**.</span><span class="sxs-lookup"><span data-stu-id="c7b16-174">To add a source, select **+**, edit the name, enter the URL or path in the **Source** control, and select  **Update**.</span></span> <span data-ttu-id="c7b16-175">Die Quelle wird jetzt in der Dropdownliste angezeigt.</span><span class="sxs-lookup"><span data-stu-id="c7b16-175">The source now appears in the selector drop-down.</span></span>
1. <span data-ttu-id="c7b16-176">Um eine Paketquelle zu ändern, wählen Sie ihn, nehmen Sie Änderungen vor, in der **Namen** und **Quelle** ein, und wählen Sie **Update**.</span><span class="sxs-lookup"><span data-stu-id="c7b16-176">To change a package source, select it, make edits in the **Name** and **Source** boxes, and select **Update**.</span></span>
1. <span data-ttu-id="c7b16-177">Um eine Paketquelle zu deaktivieren, deaktivieren Sie das Kontrollkästchen links neben dem Namen in der Liste aus.</span><span class="sxs-lookup"><span data-stu-id="c7b16-177">To disable a package source, clear the box to the left of the name in the list.</span></span>
1. <span data-ttu-id="c7b16-178">Um eine Paketquelle zu entfernen, wählen Sie ihn, und wählen Sie dann die **X** Schaltfläche.</span><span class="sxs-lookup"><span data-stu-id="c7b16-178">To remove a package source, select it and then select the **X** button.</span></span>
1. <span data-ttu-id="c7b16-179">Verwenden Sie die nach-oben und nach-unten Sie-Pfeile, um die Prioritätsreihenfolge der Paketquellen überein ändern.</span><span class="sxs-lookup"><span data-stu-id="c7b16-179">Use the up and down arrow buttons to change the priority order of the package sources.</span></span> <span data-ttu-id="c7b16-180">Visual Studio sucht diese Quellen in der Reihenfolge ihrer Priorität beim Wiederherstellen von Paketen für ein Projekt.</span><span class="sxs-lookup"><span data-stu-id="c7b16-180">Visual Studio searches these sources in the priority order when restoring packages for a project.</span></span> <span data-ttu-id="c7b16-181">Weitere Informationen finden Sie unter [paketwiederherstellung](../consume-packages/package-restore.md).</span><span class="sxs-lookup"><span data-stu-id="c7b16-181">For more information, see [Package restore](../consume-packages/package-restore.md).</span></span>

> [!Tip]
> <span data-ttu-id="c7b16-182">Wenn Sie eine Paketquelle erneut angezeigt wird, nach dem Löschen, kann es in einer Computerebene oder Benutzerebene aufgeführt `NuGet.Config` Dateien.</span><span class="sxs-lookup"><span data-stu-id="c7b16-182">If a package source reappears after deleting it, it may be listed in a computer-level or user-level `NuGet.Config` files.</span></span> <span data-ttu-id="c7b16-183">Finden Sie unter [NuGet Konfigurieren von Verhalten](../consume-packages/configuring-nuget-behavior.md) für den Speicherort dieser Dateien, entfernen Sie Sie dann die Quelle, indem Sie die Dateien manuell zu bearbeiten oder die [Nuget Datenquellen Befehl](../tools/nuget-exe-CLI-reference.md).</span><span class="sxs-lookup"><span data-stu-id="c7b16-183">See [Configuring NuGet behavior](../consume-packages/configuring-nuget-behavior.md) for the location of these files, then remove the source by editing the files manually or using the [nuget sources command](../tools/nuget-exe-CLI-reference.md).</span></span>

## <a name="package-manager-options-control"></a><span data-ttu-id="c7b16-184">Paket-Manager-Optionen steuern</span><span class="sxs-lookup"><span data-stu-id="c7b16-184">Package manager Options control</span></span>

<span data-ttu-id="c7b16-185">Wenn ein Paket ausgewählt ist, zeigt der Paket-Manager-UI ein kleines erweiterbare **Optionen** Steuerelement unterhalb der Version-Selektor (hier gezeigten sowohl reduziert und erweitert).</span><span class="sxs-lookup"><span data-stu-id="c7b16-185">When a package is selected, the Package Manager UI displays a small, expandable **Options** control below the version selector (shown here both collapsed and expanded).</span></span> <span data-ttu-id="c7b16-186">Beachten Sie, die für einige Projekt nur Typen der **Vorschaufenster anzeigen** angegeben wird.</span><span class="sxs-lookup"><span data-stu-id="c7b16-186">Note that for some project types, only the **Show preview window** option is provided.</span></span>

![Optionen des Paket-manager](media/PackageManagerUIOptions.png)

<span data-ttu-id="c7b16-188">Den folgenden Abschnitten werden diese Optionen.</span><span class="sxs-lookup"><span data-stu-id="c7b16-188">The following sections explain these options.</span></span>

### <a name="show-preview-window"></a><span data-ttu-id="c7b16-189">Vorschaufenster anzeigen</span><span class="sxs-lookup"><span data-stu-id="c7b16-189">Show preview window</span></span>

<span data-ttu-id="c7b16-190">Bei Auswahl dieser Option zeigt ein modales Fenster die die Abhängigkeiten eines ausgewählten Pakets vor der Installation des Pakets:</span><span class="sxs-lookup"><span data-stu-id="c7b16-190">When selected, a modal window displays which the dependencies of a chosen package before the package is installed:</span></span>

![Beispiel-Vorschaudialogfeld](media/InstallPreviewDialog.png)

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="install-options"></a>

### <a name="install-and-update-options"></a><span data-ttu-id="c7b16-192">Installations- und Aktualisierungsoptionen</span><span class="sxs-lookup"><span data-stu-id="c7b16-192">Install and Update Options</span></span>

<span data-ttu-id="c7b16-193">(Nicht verfügbar für alle Projekttypen.)</span><span class="sxs-lookup"><span data-stu-id="c7b16-193">(Not available for all project types.)</span></span>

<span data-ttu-id="c7b16-194">**Das abhängigkeitsverhalten** konfiguriert wie NuGet entscheidet sich, welche Versionen der abhängigen Pakete zu installieren:</span><span class="sxs-lookup"><span data-stu-id="c7b16-194">**Dependency behavior** configures how NuGet decides which versions of dependent packages to install:</span></span>

- <span data-ttu-id="c7b16-195">*Ignorieren Sie Abhängigkeiten* überspringt, installieren alle Abhängigkeiten, die zu installierende Paket in der Regel unterbricht.</span><span class="sxs-lookup"><span data-stu-id="c7b16-195">*Ignore dependencies* skips installing any dependencies, which typically breaks the package being installed.</span></span>
- <span data-ttu-id="c7b16-196">*Niedrigste* [Standard] installiert die Abhängigkeit mit der minimalen Versionsnummer, die die Anforderungen des ausgewählten Pakets primären erfüllt.</span><span class="sxs-lookup"><span data-stu-id="c7b16-196">*Lowest* [Default] installs the dependency with the minimal version number that meets the requirements of the primary chosen package.</span></span>
- <span data-ttu-id="c7b16-197">*Höchste Patch* die Version mit der gleichen Haupt-und Nebenversionsnummern Zahlen, aber die höchste Anzahl der Patch installiert.</span><span class="sxs-lookup"><span data-stu-id="c7b16-197">*Highest Patch* installs the version with the same major and minor version numbers, but the highest patch number.</span></span> <span data-ttu-id="c7b16-198">Z. B. wenn Version 1.2.2 angegeben wird die höchste Version, die mit 1.2 beginnt installiert werden</span><span class="sxs-lookup"><span data-stu-id="c7b16-198">For example, if version 1.2.2 is specified then the highest version that starts with 1.2 will be installed</span></span>
- <span data-ttu-id="c7b16-199">*Höchste Nebenversion* die Version mit der gleichen Hauptversionsnummer nur den höchsten Nebenversionsnummer und die Anzahl der Patch installiert.</span><span class="sxs-lookup"><span data-stu-id="c7b16-199">*Highest Minor* installs the version with the same major version number but the highest minor number and patch number.</span></span> <span data-ttu-id="c7b16-200">Wenn Version 1.2.2 angegeben ist, wird die höchste Version, die mit 1 beginnt installiert werden</span><span class="sxs-lookup"><span data-stu-id="c7b16-200">If version 1.2.2 is specified, then the highest version that starts with 1 will be installed</span></span>
- <span data-ttu-id="c7b16-201">*Höchste* installiert die höchste verfügbare Version des Pakets.</span><span class="sxs-lookup"><span data-stu-id="c7b16-201">*Highest* installs the highest available version of the package.</span></span>

<span data-ttu-id="c7b16-202">**Datei Konflikt Aktion** gibt an, wie NuGet Pakete behandeln soll, die bereits im Projekt oder lokalen Computer vorhanden sind:</span><span class="sxs-lookup"><span data-stu-id="c7b16-202">**File conflict action** specifies how NuGet should handle packages that already exist in the project or local machine:</span></span>

- <span data-ttu-id="c7b16-203">*Prompt* weist NuGet zu Fragen, ob beibehalten oder überschreiben vorhandene Pakete.</span><span class="sxs-lookup"><span data-stu-id="c7b16-203">*Prompt* instructs NuGet to ask whether to keep or overwrite existing packages.</span></span>
- <span data-ttu-id="c7b16-204">*Ignorieren Sie alle* weist NuGet zum Überschreiben aller vorhandenen Pakete überspringen.</span><span class="sxs-lookup"><span data-stu-id="c7b16-204">*Ignore All* instructs NuGet to skip overwriting any existing packages.</span></span>
- <span data-ttu-id="c7b16-205">*Überschreiben Sie alle* weist NuGet, um vorhandene Pakete zu überschreiben.</span><span class="sxs-lookup"><span data-stu-id="c7b16-205">*Overwrite All* instructs NuGet to overwrite any existing packages.</span></span>

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="uninstall-options"></a>

### <a name="uninstall-options"></a><span data-ttu-id="c7b16-206">Deinstallationsoptionen</span><span class="sxs-lookup"><span data-stu-id="c7b16-206">Uninstall Options</span></span>

<span data-ttu-id="c7b16-207">(Nicht verfügbar für alle Projekttypen.)</span><span class="sxs-lookup"><span data-stu-id="c7b16-207">(Not available for all project types.)</span></span>

<span data-ttu-id="c7b16-208">**Entfernen Sie Abhängigkeiten**: Bei Auswahl dieser Option entfernt alle abhängigen Pakete auf, wenn diese nicht an anderer Stelle im Projekt verwiesen wird.</span><span class="sxs-lookup"><span data-stu-id="c7b16-208">**Remove dependencies**: when selected, removes any dependent packages if they're not referenced elsewhere in the project.</span></span>

<span data-ttu-id="c7b16-209">**Deinstallation erzwingen, auch wenn Abhängigkeiten vorhanden sind, darauf**: Bei Auswahl dieser Option wird ein Paket deinstalliert, selbst wenn darauf noch im Projekt verwiesen wird.</span><span class="sxs-lookup"><span data-stu-id="c7b16-209">**Force uninstall even if there are dependencies on it**: when selected, uninstalls a package even if it's still being referenced in the project.</span></span> <span data-ttu-id="c7b16-210">Dies wird normalerweise verwendet, in Kombination mit **Abhängigkeiten entfernen** So entfernen Sie ein Paket und alle von Ihnen gewünschten Abhängigkeiten, die es installiert.</span><span class="sxs-lookup"><span data-stu-id="c7b16-210">This is typically used in combination with **Remove dependencies** to remove a package and whatever dependencies it installed.</span></span> <span data-ttu-id="c7b16-211">Mit dieser Option kann jedoch zu fehlerhaften Verweise im Projekt führen.</span><span class="sxs-lookup"><span data-stu-id="c7b16-211">Using this option may, however, lead to broken references in the project.</span></span> <span data-ttu-id="c7b16-212">In solchen Fällen müssen Sie möglicherweise auf [installieren Sie die anderen Pakete](../consume-packages/reinstalling-and-updating-packages.md).</span><span class="sxs-lookup"><span data-stu-id="c7b16-212">In such cases, you may need to [reinstall those other packages](../consume-packages/reinstalling-and-updating-packages.md).</span></span>
