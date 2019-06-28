---
title: Installieren und Verwalten von NuGet-Pakete in Visual Studio
description: Anweisungen zum Verwenden der NuGet-Paket-Manager-UI in Visual Studio für die Arbeit mit NuGet-Pakete.
author: karann-msft
ms.author: karann
ms.date: 12/08/2017
ms.topic: conceptual
f1_keywords:
- vs.toolsoptionspages.nuget_package_manager
- vs.toolsoptionspages.nuget_package_manager.general
- vs.toolsoptionspages.nuget_package_manager.package_sources
- vs.nuget.packagemanager.ui
ms.openlocfilehash: 97e5de3f07199cd3c6a645749c8f2f1603ca630e
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426240"
---
# <a name="install-and-manage-packages-in-visual-studio"></a><span data-ttu-id="b606d-103">Installieren und Verwalten von Paketen in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="b606d-103">Install and manage packages in Visual Studio</span></span>

<span data-ttu-id="b606d-104">Die NuGet-Paket-Manager-UI in Visual Studio unter Windows können Sie ganz einfach zu installieren, deinstallieren und Aktualisieren von NuGet-Paketen in Projekte und Projektmappen.</span><span class="sxs-lookup"><span data-stu-id="b606d-104">The NuGet Package Manager UI in Visual Studio on Windows allows you to easily install, uninstall, and update NuGet packages in projects and solutions.</span></span> <span data-ttu-id="b606d-105">Die Umgebung in Visual Studio für Mac, finden Sie unter [einschließen eines NuGet-Paket in Ihrem Projekt](/visualstudio/mac/nuget-walkthrough).</span><span class="sxs-lookup"><span data-stu-id="b606d-105">For the experience in Visual Studio for Mac, see [Including a NuGet package in your project](/visualstudio/mac/nuget-walkthrough).</span></span> <span data-ttu-id="b606d-106">Die Paket-Manager-UI kann nicht mit Visual Studio Code enthalten ist.</span><span class="sxs-lookup"><span data-stu-id="b606d-106">The Package Manager UI is not included with Visual Studio Code.</span></span>

> [!NOTE]
> <span data-ttu-id="b606d-107">Wenn Sie das NuGet-Paket-Manager in Visual Studio 2015 nicht vorhanden sind, überprüfen Sie **Tools > Erweiterungen und Updates...**  und suchen Sie nach der *NuGet Package Manager* Erweiterung.</span><span class="sxs-lookup"><span data-stu-id="b606d-107">If you're missing the NuGet Package Manager in Visual Studio 2015, check **Tools > Extensions and Updates...** and search for the *NuGet Package Manager* extension.</span></span> <span data-ttu-id="b606d-108">Wenn Sie nicht das Installationsprogramm für Erweiterungen in Visual Studio verwenden können, laden Sie die Erweiterung direkt aus [ https://dist.nuget.org/index.html ](https://dist.nuget.org/index.html).</span><span class="sxs-lookup"><span data-stu-id="b606d-108">If you're unable to use the extensions installer in Visual Studio, download the extension directly from [https://dist.nuget.org/index.html](https://dist.nuget.org/index.html).</span></span>
>
> <span data-ttu-id="b606d-109">In Visual Studio 2017 beginnen, werden NuGet und den NuGet-Paket-Manager automatisch mit allen installiert. NET-bezogenen Workloads.</span><span class="sxs-lookup"><span data-stu-id="b606d-109">Starting in Visual Studio 2017, NuGet and the NuGet Package Manager are automatically installed with any .NET-related workloads.</span></span> <span data-ttu-id="b606d-110">Installieren Sie sie einzeln durch Auswählen der **einzelne Komponenten > Codetools > NuGet-Paket-Manager** -Option in Visual Studio-Installer.</span><span class="sxs-lookup"><span data-stu-id="b606d-110">Install it individually by selecting the **Individual components > Code tools > NuGet package manager** option in the Visual Studio installer.</span></span>

## <a name="finding-and-installing-a-package"></a><span data-ttu-id="b606d-111">Suchen und Installieren eines Pakets</span><span class="sxs-lookup"><span data-stu-id="b606d-111">Finding and installing a package</span></span>

1. <span data-ttu-id="b606d-112">In **Projektmappen-Explorer**, mit der rechten Maustaste entweder **Verweise** oder ein Projekt, und wählen **NuGet-Pakete verwalten...** .</span><span class="sxs-lookup"><span data-stu-id="b606d-112">In **Solution Explorer**, right-click either **References**  or a project and select **Manage NuGet Packages...**.</span></span>

    ![Option für das NuGet-Pakete verwalten](media/ManagePackagesUICommand.png)

1. <span data-ttu-id="b606d-114">Die **Durchsuchen** Registerkarte zeigt die Pakete nach Beliebtheit, aus der ausgewählten Quelle (finden Sie unter [Paketquellen](#package-sources)).</span><span class="sxs-lookup"><span data-stu-id="b606d-114">The **Browse** tab displays packages by popularity from the currently selected source (see [package sources](#package-sources)).</span></span> <span data-ttu-id="b606d-115">Suchen Sie nach einem bestimmten Paket mithilfe des Suchfelds oben links.</span><span class="sxs-lookup"><span data-stu-id="b606d-115">Search for a specific package using the search box on the upper left.</span></span> <span data-ttu-id="b606d-116">Wählen Sie ein Paket aus der Liste, um die Informationen anzeigen, werden dadurch auch die **installieren** Schaltfläche zusammen mit einem Dropdown-Auswahl-Version.</span><span class="sxs-lookup"><span data-stu-id="b606d-116">Select a package from the list to display its information, which also enables the **Install** button along with a version-selection drop-down.</span></span>

    ![Verwalten Sie die Registerkarte Durchsuchen zu NuGet-Pakete-Dialogfeld](media/Search.png)

1. <span data-ttu-id="b606d-118">Wählen Sie die gewünschte Version aus der Dropdownliste aus, und wählen Sie **installieren**.</span><span class="sxs-lookup"><span data-stu-id="b606d-118">Select the desired version from the drop-down and select **Install**.</span></span> <span data-ttu-id="b606d-119">Visual Studio installiert das Paket und seine Abhängigkeiten in das Projekt an.</span><span class="sxs-lookup"><span data-stu-id="b606d-119">Visual Studio installs the package and its dependencies into the project.</span></span> <span data-ttu-id="b606d-120">Möglicherweise werden Sie aufgefordert, Lizenzbedingungen zu akzeptieren.</span><span class="sxs-lookup"><span data-stu-id="b606d-120">You may be asked to accept license terms.</span></span> <span data-ttu-id="b606d-121">Wenn die Installation abgeschlossen ist, die zusätzliche Pakete angezeigt werden, auf die **installiert** Registerkarte. Pakete werden ebenfalls aufgeführt, der **Verweise** -Knoten des Projektmappen-Explorer, der angibt, dass Sie auf sie verweisen können, die im Projekt mit `using` Anweisungen.</span><span class="sxs-lookup"><span data-stu-id="b606d-121">When installation is complete, the added packages appear on the **Installed** tab. Packages are also listed in the **References** node of Solution Explorer, indicating that you can refer to them in the project with `using` statements.</span></span>

    ![Verweise im Projektmappen-Explorer](media/References.png)

> [!Tip]
> <span data-ttu-id="b606d-123">Wählen Sie zum Einschließen von Vorabversionen in die Suche und Vorabversionen in der Version Dropdownliste zur Verfügung, die **Vorabversion einbeziehen** Option.</span><span class="sxs-lookup"><span data-stu-id="b606d-123">To include prerelease versions in the search, and to make prerelease versions available in the version drop-down, select the **Include prerelease** option.</span></span>

## <a name="uninstalling-a-package"></a><span data-ttu-id="b606d-124">Wenn ein Paket deinstalliert</span><span class="sxs-lookup"><span data-stu-id="b606d-124">Uninstalling a package</span></span>

1. <span data-ttu-id="b606d-125">In **Projektmappen-Explorer**, mit der rechten Maustaste entweder **Verweise** oder das gewünschte Projekt, und die Sie **NuGet-Pakete verwalten...** .</span><span class="sxs-lookup"><span data-stu-id="b606d-125">In **Solution Explorer**, right-click either **References** or the desired project, and select **Manage NuGet Packages...**.</span></span>
1. <span data-ttu-id="b606d-126">Wählen Sie die **installiert** Registerkarte.</span><span class="sxs-lookup"><span data-stu-id="b606d-126">Select the **Installed** tab.</span></span>
1. <span data-ttu-id="b606d-127">Wählen Sie das Paket deinstallieren (mit der Suche zum Filtern der Liste aus, falls erforderlich), und wählen **Deinstallieren**.</span><span class="sxs-lookup"><span data-stu-id="b606d-127">Select the package to uninstall (using search to filter the list if necessary) and select **Uninstall**.</span></span>

    ![Wenn ein Paket deinstalliert](media/UninstallPackage.png)

1. <span data-ttu-id="b606d-129">Beachten Sie, dass die **Vorabversion einbeziehen** und **Paketquelle** Steuerelemente haben keine Auswirkungen, wenn Pakete zu deinstallieren.</span><span class="sxs-lookup"><span data-stu-id="b606d-129">Note that the **Include prerelease** and **Package source** controls have no effect when uninstalling packages.</span></span>

## <a name="updating-a-package"></a><span data-ttu-id="b606d-130">Aktualisieren eines Pakets</span><span class="sxs-lookup"><span data-stu-id="b606d-130">Updating a package</span></span>

1. <span data-ttu-id="b606d-131">In **Projektmappen-Explorer**, mit der rechten Maustaste entweder **Verweise** oder das gewünschte Projekt, und die Sie **NuGet-Pakete verwalten...** . (Klicken Sie im Website-Projekten mit der Maustaste der **Bin** Ordner.)</span><span class="sxs-lookup"><span data-stu-id="b606d-131">In **Solution Explorer**, right-click either **References** or the desired project, and select **Manage NuGet Packages...**. (In web site projects, right-click the **Bin** folder.)</span></span>
1. <span data-ttu-id="b606d-132">Wählen Sie die **Updates** Registerkarte, um Pakete anzuzeigen, die aus den Quellen für die ausgewählte Paket verfügbaren Updates verfügen.</span><span class="sxs-lookup"><span data-stu-id="b606d-132">Select the **Updates** tab to see packages that have available updates from the selected package sources.</span></span> <span data-ttu-id="b606d-133">Wählen Sie **Vorabversion einbeziehen** Vorabversionen von Paketen in der Update-Liste aufgenommen.</span><span class="sxs-lookup"><span data-stu-id="b606d-133">Select **Include prerelease** to include prerelease packages in the update list.</span></span>
1. <span data-ttu-id="b606d-134">Wählen Sie das Paket zu aktualisieren, wählen Sie die gewünschte Version aus der Dropdownliste auf der rechten Seite, und wählen Sie **aktualisieren**.</span><span class="sxs-lookup"><span data-stu-id="b606d-134">Select the package to update, select the desired version from the drop-down on the right, and select **Update**.</span></span>

    ![Aktualisieren eines Pakets](media/UpdatePackages.png)

1. <a name="implicit_reference"></a><span data-ttu-id="b606d-136">Für einige Pakete aufgeführt die **Update** -Schaltfläche deaktiviert ist und eine Meldung angezeigt wird, besagt, dass "implizit ein SDK verweist" (oder "AutoReferenced").</span><span class="sxs-lookup"><span data-stu-id="b606d-136">For some packages, the **Update** button is disabled and a message appears saying that it's "Implicitly referenced by an SDK" (or "AutoReferenced").</span></span> <span data-ttu-id="b606d-137">Diese Meldung gibt an, dass das Paket Teil einer größeren Framework oder das SDK ist und nicht unabhängig voneinander aktualisiert werden sollten.</span><span class="sxs-lookup"><span data-stu-id="b606d-137">This message indicates that the package is part of a larger framework or SDK and should not be updated independently.</span></span> <span data-ttu-id="b606d-138">(Diese Pakete mit intern markiert sind `<IsImplicitlyDefined>True</IsImplicitlyDefined>`.) Z. B. `Microsoft.NETCore.App` ist Teil des .NET Core SDK und die Paketversion ist nicht identisch mit der Version der Runtime-Framework, die von der Anwendung verwendet.</span><span class="sxs-lookup"><span data-stu-id="b606d-138">(Such packages are internally marked with `<IsImplicitlyDefined>True</IsImplicitlyDefined>`.) For example, `Microsoft.NETCore.App` is part of the .NET Core SDK, and the package version is not the same as the version of the runtime framework used by the application.</span></span> <span data-ttu-id="b606d-139">Sie müssen [die .NET Core-Installation zu aktualisieren](https://aka.ms/dotnet-download) um neue Versionen der ASP.NET Core und .NET Core-Runtime zu erhalten.</span><span class="sxs-lookup"><span data-stu-id="b606d-139">You need to [update your .NET Core installation](https://aka.ms/dotnet-download) to get new versions of the ASP.NET Core and .NET Core runtime.</span></span> <span data-ttu-id="b606d-140">[Finden Sie unter diesem Dokument Weitere Informationen zu .NET Core-metapakete und versionsverwaltung](/dotnet/core/packages).</span><span class="sxs-lookup"><span data-stu-id="b606d-140">[See this document for more details on .NET Core metapackages and versioning](/dotnet/core/packages).</span></span> <span data-ttu-id="b606d-141">Dies gilt für die folgenden häufig verwendeten Pakete:</span><span class="sxs-lookup"><span data-stu-id="b606d-141">This applies to the following commonly used packages:</span></span>
    * <span data-ttu-id="b606d-142">Microsoft.AspNetCore.All</span><span class="sxs-lookup"><span data-stu-id="b606d-142">Microsoft.AspNetCore.All</span></span>
    * <span data-ttu-id="b606d-143">Microsoft.AspNetCore.App</span><span class="sxs-lookup"><span data-stu-id="b606d-143">Microsoft.AspNetCore.App</span></span>
    * <span data-ttu-id="b606d-144">Microsoft.NETCore.App</span><span class="sxs-lookup"><span data-stu-id="b606d-144">Microsoft.NETCore.App</span></span>
    * <span data-ttu-id="b606d-145">NETStandard.Library</span><span class="sxs-lookup"><span data-stu-id="b606d-145">NETStandard.Library</span></span>

    ![Beispielpaket markiert als implizit verweisen oder AutoReferenced](media/PackageManagerUIAutoReferenced.png)

1. <span data-ttu-id="b606d-147">Um mehrere Pakete auf die neuesten Version zu aktualisieren, wählen Sie sie in der Liste aus und wählen Sie die **aktualisieren** oberhalb der Liste auf die Schaltfläche.</span><span class="sxs-lookup"><span data-stu-id="b606d-147">To update multiple packages to their newest versions, select  them in the list and select the **Update** button above the list.</span></span>
1. <span data-ttu-id="b606d-148">Sie können auch ein einzelnes Paket vom Aktualisieren der **installiert** Registerkarte. In diesem Fall enthalten die Details für das Paket die Auswahl einer Version (unterliegt den **Vorabversion einbeziehen** Option) und ein **Update** Schaltfläche.</span><span class="sxs-lookup"><span data-stu-id="b606d-148">You can also update an individual package from the **Installed** tab. In this case, the details for the package include a version selector (subject to the **Include prerelease** option) and an **Update** button.</span></span>

## <a name="managing-packages-for-the-solution"></a><span data-ttu-id="b606d-149">Verwalten von Paketen für die Lösung</span><span class="sxs-lookup"><span data-stu-id="b606d-149">Managing packages for the solution</span></span>

<span data-ttu-id="b606d-150">Verwalten von Paketen für eine Lösung ist eine komfortable mit mehreren Projekten gleichzeitig arbeiten.</span><span class="sxs-lookup"><span data-stu-id="b606d-150">Managing packages for a solution is a convenient means to work with multiple projects simultaneously.</span></span>

1. <span data-ttu-id="b606d-151">Wählen Sie die **Tools > NuGet-Paket-Manager > NuGet-Pakete für Projektmappe verwalten...**  Menü Befehl oder mit der rechten Maustaste in der Projektmappe, und wählen Sie **NuGet-Pakete verwalten...** :</span><span class="sxs-lookup"><span data-stu-id="b606d-151">Select the **Tools > NuGet Package Manager > Manage NuGet Packages for Solution...** menu command, or right-click the solution and select **Manage NuGet Packages...**:</span></span>

    ![Verwalten von NuGet-Pakete für die Lösung](media/ManagePackagesSolutionUICommand.png)

1. <span data-ttu-id="b606d-153">Wenn Sie Pakete für die Projektmappe zu verwalten, kann die Benutzeroberfläche Sie die Projekte auswählen, die von den Vorgängen betroffen sind:</span><span class="sxs-lookup"><span data-stu-id="b606d-153">When managing packages for the solution, the UI lets you select the projects that are affected by the operations:</span></span>

    ![Projektauswahl, wenn Sie Pakete für die Projektmappe verwalten](media/SolutionPackagesUI.png)

### <a name="consolidate-tab"></a><span data-ttu-id="b606d-155">Konsolidieren Sie die Registerkarte "</span><span class="sxs-lookup"><span data-stu-id="b606d-155">Consolidate tab</span></span>

<span data-ttu-id="b606d-156">Entwickler halten es in der Regel nicht üblich ist, verschiedene Versionen des gleichen NuGet-Pakets für andere Projekte in der gleichen Projektmappe verwenden.</span><span class="sxs-lookup"><span data-stu-id="b606d-156">Developers typically consider it bad practice to use different versions of the same NuGet package across different projects in the same solution.</span></span> <span data-ttu-id="b606d-157">Wenn Sie zum Verwalten von Paketen für eine Lösung auswählen, enthält die Paket-Manager-UI ein **konsolidieren** Registerkarte, die auf dem Sie können leicht erkennen, in dem Pakete mit unterschiedlichen Versionsnummern von verschiedenen Projekten in der Projektmappe verwendet werden:</span><span class="sxs-lookup"><span data-stu-id="b606d-157">When you choose to manage packages for a solution, the Package Manager UI provides a **Consolidate** tab on which you can easily see where packages with distinct version numbers are used by different projects in the solution:</span></span>

![Paket-Manager-Benutzeroberfläche konsolidieren Registerkarte](media/ConsolidateTab.png)

<span data-ttu-id="b606d-159">In diesem Beispiel verwendet das Projekt ClassLibrary1 EntityFramework 6.2.0 fest, während ConsoleApp1 EntityFramework 6.1.0 verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="b606d-159">In this example, the ClassLibrary1 project is using EntityFramework 6.2.0, whereas ConsoleApp1 is using EntityFramework 6.1.0.</span></span> <span data-ttu-id="b606d-160">Um Paketversionen konsolidieren möchten, führen Sie folgende Schritte aus:</span><span class="sxs-lookup"><span data-stu-id="b606d-160">To consolidate package versions, do the following:</span></span>

- <span data-ttu-id="b606d-161">Wählen Sie die Projekte, die in der Projektliste aktualisiert.</span><span class="sxs-lookup"><span data-stu-id="b606d-161">Select the projects to update in the project list.</span></span>
- <span data-ttu-id="b606d-162">Wählen Sie die Version für die Verwendung in allen diesen Projekten in der **Version** Kontrolle, z. B. EntityFramework 6.2.0 fest.</span><span class="sxs-lookup"><span data-stu-id="b606d-162">Select the version to use in all those projects in the **Version** control, such as EntityFramework 6.2.0.</span></span>
- <span data-ttu-id="b606d-163">Wählen Sie die **installieren** Schaltfläche.</span><span class="sxs-lookup"><span data-stu-id="b606d-163">Select the **Install** button.</span></span>

<span data-ttu-id="b606d-164">Der Paket-Manager installiert die Version des ausgewählten Pakets in allen ausgewählten Projekte, die nach dem das Paket nicht mehr angezeigt wird auf die **konsolidieren** Registerkarte.</span><span class="sxs-lookup"><span data-stu-id="b606d-164">The Package Manager installs the selected package version into all selected projects, after which the package no longer appears on the **Consolidate** tab.</span></span>

## <a name="package-sources"></a><span data-ttu-id="b606d-165">Paketquellen</span><span class="sxs-lookup"><span data-stu-id="b606d-165">Package sources</span></span>

<span data-ttu-id="b606d-166">Wählen Sie zum Ändern der Quelle, aus dem Visual Studio ruft Pakete ab, aus der Source-Selektor:</span><span class="sxs-lookup"><span data-stu-id="b606d-166">To change the source from which Visual Studio obtains packages, select one from the source selector:</span></span>

![Paket-Source-Selektor in der Benutzeroberfläche des Paket-Managers](media/PackageSourceDropDown.png)

<span data-ttu-id="b606d-168">So verwalten Sie Paketquellen</span><span class="sxs-lookup"><span data-stu-id="b606d-168">To manage package sources:</span></span>

1. <span data-ttu-id="b606d-169">Wählen Sie die **Einstellungen** Symbol in der Paket-Manager-UI unten beschriebenen, oder verwenden Sie die **Tools > Optionen** -Befehl aus, und scrollen Sie zum **NuGet Package Manager**:</span><span class="sxs-lookup"><span data-stu-id="b606d-169">Select the **Settings** icon in the Package Manager UI outlined below or use the **Tools > Options** command and scroll to **NuGet Package Manager**:</span></span>

    ![Symbol "Einstellungen" Paket-Manager-Benutzeroberfläche](media/PackageSourceSettings.png)

1. <span data-ttu-id="b606d-171">Wählen Sie die **Paketquellen** Knoten:</span><span class="sxs-lookup"><span data-stu-id="b606d-171">Select the **Package Sources** node:</span></span>

    ![Quellen Paketoptionen](media/options.png)

1. <span data-ttu-id="b606d-173">Wählen Sie zum Hinzufügen einer Quelle **+** , bearbeiten Sie den Namen, geben Sie die URL oder Pfad in der **Quelle** steuern, und wählen Sie **Update**.</span><span class="sxs-lookup"><span data-stu-id="b606d-173">To add a source, select **+**, edit the name, enter the URL or path in the **Source** control, and select  **Update**.</span></span> <span data-ttu-id="b606d-174">Die Quelle wird jetzt in der Auswahl-Dropdownliste angezeigt.</span><span class="sxs-lookup"><span data-stu-id="b606d-174">The source now appears in the selector drop-down.</span></span>
1. <span data-ttu-id="b606d-175">Um eine Paketquelle zu ändern, wählen Sie ihn aus, nehmen Sie Änderungen vor, in der **Namen** und **Quelle** angezeigt, und wählen Sie **Update**.</span><span class="sxs-lookup"><span data-stu-id="b606d-175">To change a package source, select it, make edits in the **Name** and **Source** boxes, and select **Update**.</span></span>
1. <span data-ttu-id="b606d-176">Um eine Paketquelle zu deaktivieren, deaktivieren Sie das Kontrollkästchen links neben dem Namen in der Liste aus.</span><span class="sxs-lookup"><span data-stu-id="b606d-176">To disable a package source, clear the box to the left of the name in the list.</span></span>
1. <span data-ttu-id="b606d-177">Um eine Paketquelle zu entfernen, wählen Sie ihn, und wählen Sie dann die **X** Schaltfläche.</span><span class="sxs-lookup"><span data-stu-id="b606d-177">To remove a package source, select it and then select the **X** button.</span></span>
1. <span data-ttu-id="b606d-178">Verwenden die nach-oben und Pfeil nach unten Schaltflächen ändert nicht die Reihenfolge der Priorität die Paketquellen.</span><span class="sxs-lookup"><span data-stu-id="b606d-178">Using the up and down arrow buttons does not change the priority order of the package sources.</span></span> <span data-ttu-id="b606d-179">Visual Studio ignoriert die Reihenfolgen der Paketquellen, verwendet dabei das Paket aus einer beliebigen Quelle als Erstes auf Anforderungen reagieren.</span><span class="sxs-lookup"><span data-stu-id="b606d-179">Visual Studio ignores the order of package sources, using the package from whichever source is first to respond to requests.</span></span> <span data-ttu-id="b606d-180">Weitere Informationen finden Sie unter [paketwiederherstellung](../consume-packages/package-restore.md).</span><span class="sxs-lookup"><span data-stu-id="b606d-180">For more information, see [Package restore](../consume-packages/package-restore.md).</span></span>

> [!Tip]
> <span data-ttu-id="b606d-181">Wenn Sie eine Paketquelle erneut angezeigt wird, nach dem Löschen, kann es in einer Computerebene oder Benutzerebene aufgeführt `NuGet.Config` Dateien.</span><span class="sxs-lookup"><span data-stu-id="b606d-181">If a package source reappears after deleting it, it may be listed in a computer-level or user-level `NuGet.Config` files.</span></span> <span data-ttu-id="b606d-182">Finden Sie unter [häufig auftretenden NuGet Konfigurationen](../consume-packages/configuring-nuget-behavior.md) für den Speicherort dieser Dateien, entfernen Sie Sie dann die Quelle durch die Dateien manuell bearbeiten, oder Verwenden der [Nuget Quellen Befehl](../tools/nuget-exe-CLI-reference.md).</span><span class="sxs-lookup"><span data-stu-id="b606d-182">See [Common NuGet configurations](../consume-packages/configuring-nuget-behavior.md) for the location of these files, then remove the source by editing the files manually or using the [nuget sources command](../tools/nuget-exe-CLI-reference.md).</span></span>

## <a name="package-manager-options-control"></a><span data-ttu-id="b606d-183">Steuerelement "Optionen" Paket-manager</span><span class="sxs-lookup"><span data-stu-id="b606d-183">Package manager Options control</span></span>

<span data-ttu-id="b606d-184">Wenn ein Paket ausgewählt ist, zeigt der Paket-Manager-UI ein kleines, erweiterbare **Optionen** Steuerelement unterhalb der Auswahl-Version (Siehe hier beide reduziert und erweitert).</span><span class="sxs-lookup"><span data-stu-id="b606d-184">When a package is selected, the Package Manager UI displays a small, expandable **Options** control below the version selector (shown here both collapsed and expanded).</span></span> <span data-ttu-id="b606d-185">Hinweis: damit das einem Projekt nur Typen der **Vorschaufenster anzeigen** angegeben wird.</span><span class="sxs-lookup"><span data-stu-id="b606d-185">Note that for some project types, only the **Show preview window** option is provided.</span></span>

![Optionen der Paket-manager](media/PackageManagerUIOptions.png)

<span data-ttu-id="b606d-187">Den folgenden Abschnitten werden diese Optionen.</span><span class="sxs-lookup"><span data-stu-id="b606d-187">The following sections explain these options.</span></span>

### <a name="show-preview-window"></a><span data-ttu-id="b606d-188">Vorschaufenster anzeigen</span><span class="sxs-lookup"><span data-stu-id="b606d-188">Show preview window</span></span>

<span data-ttu-id="b606d-189">Bei Auswahl dieser Option zeigt ein modales Fenster die die Abhängigkeiten eines ausgewählten Pakets vor der Installation des Pakets:</span><span class="sxs-lookup"><span data-stu-id="b606d-189">When selected, a modal window displays which the dependencies of a chosen package before the package is installed:</span></span>

![Beispiel-Dialogfelds "Datenvorschau"](media/InstallPreviewDialog.png)

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="install-options"></a>

### <a name="install-and-update-options"></a><span data-ttu-id="b606d-191">Installation und Update-Optionen</span><span class="sxs-lookup"><span data-stu-id="b606d-191">Install and Update Options</span></span>

<span data-ttu-id="b606d-192">(Nicht verfügbar für alle Projekttypen.)</span><span class="sxs-lookup"><span data-stu-id="b606d-192">(Not available for all project types.)</span></span>

<span data-ttu-id="b606d-193">**Abhängigkeit Verhalten** konfiguriert, wie NuGet entscheidet, welche Versionen der abhängigen Pakete zu installieren:</span><span class="sxs-lookup"><span data-stu-id="b606d-193">**Dependency behavior** configures how NuGet decides which versions of dependent packages to install:</span></span>

- <span data-ttu-id="b606d-194">*Ignorieren Sie Abhängigkeiten* überspringt die Installation von Abhängigkeiten, die in der Regel das Paket installiert wird.</span><span class="sxs-lookup"><span data-stu-id="b606d-194">*Ignore dependencies* skips installing any dependencies, which typically breaks the package being installed.</span></span>
- <span data-ttu-id="b606d-195">*Niedrigste* [Standard] installiert die Abhängigkeit durch die minimale Versionsnummer, die die Anforderungen des ausgewählten primärpakets erfüllt.</span><span class="sxs-lookup"><span data-stu-id="b606d-195">*Lowest* [Default] installs the dependency with the minimal version number that meets the requirements of the primary chosen package.</span></span>
- <span data-ttu-id="b606d-196">*Höchste Patch* wird die Version mit der gleichen Haupt-und Nebenversionsnummern Zahlen, aber die höchste Anzahl der Patch installiert.</span><span class="sxs-lookup"><span data-stu-id="b606d-196">*Highest Patch* installs the version with the same major and minor version numbers, but the highest patch number.</span></span> <span data-ttu-id="b606d-197">Z. B. wenn Version 1.2.2 angegeben wird die höchste Version, die mit 1.2 beginnt installiert werden</span><span class="sxs-lookup"><span data-stu-id="b606d-197">For example, if version 1.2.2 is specified then the highest version that starts with 1.2 will be installed</span></span>
- <span data-ttu-id="b606d-198">*Höchste Minor* installiert die Version mit der gleichen Hauptversionsnummer, aber der höchsten Nebenversionsnummer und Patch-Anzahl.</span><span class="sxs-lookup"><span data-stu-id="b606d-198">*Highest Minor* installs the version with the same major version number but the highest minor number and patch number.</span></span> <span data-ttu-id="b606d-199">Wenn Version 1.2.2 angegeben ist, wird die höchste Version, die mit 1 beginnt installiert werden</span><span class="sxs-lookup"><span data-stu-id="b606d-199">If version 1.2.2 is specified, then the highest version that starts with 1 will be installed</span></span>
- <span data-ttu-id="b606d-200">*Höchste* installiert die höchste verfügbare Version des Pakets.</span><span class="sxs-lookup"><span data-stu-id="b606d-200">*Highest* installs the highest available version of the package.</span></span>

<span data-ttu-id="b606d-201">**Datei konfliktlösung Aktion** gibt an, wie NuGet Pakete behandeln soll, die bereits im Projekt oder in lokalen Computer vorhanden sind:</span><span class="sxs-lookup"><span data-stu-id="b606d-201">**File conflict action** specifies how NuGet should handle packages that already exist in the project or local machine:</span></span>

- <span data-ttu-id="b606d-202">*Eingabeaufforderung* NuGet die Anweisung, die Fragen, ob vorhandene Pakete überschreiben oder beibehalten.</span><span class="sxs-lookup"><span data-stu-id="b606d-202">*Prompt* instructs NuGet to ask whether to keep or overwrite existing packages.</span></span>
- <span data-ttu-id="b606d-203">*Alle ignorieren* NuGet die Anweisung, überschreiben vorhandene Pakete zu überspringen.</span><span class="sxs-lookup"><span data-stu-id="b606d-203">*Ignore All* instructs NuGet to skip overwriting any existing packages.</span></span>
- <span data-ttu-id="b606d-204">*Alle überschreiben* NuGet die Anweisung, überschreiben vorhandene Pakete.</span><span class="sxs-lookup"><span data-stu-id="b606d-204">*Overwrite All* instructs NuGet to overwrite any existing packages.</span></span>

<!-- This is here because the link in the UI needs this anchor. See https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Clients/PackageManagement.UI/Xamls/OptionsControl.xaml -->
<a name="uninstall-options"></a>

### <a name="uninstall-options"></a><span data-ttu-id="b606d-205">Deinstallieren von Optionen</span><span class="sxs-lookup"><span data-stu-id="b606d-205">Uninstall Options</span></span>

<span data-ttu-id="b606d-206">(Nicht verfügbar für alle Projekttypen.)</span><span class="sxs-lookup"><span data-stu-id="b606d-206">(Not available for all project types.)</span></span>

<span data-ttu-id="b606d-207">**Entfernen Sie Abhängigkeiten**: Bei Auswahl dieser Option alle erforderlichen abhängigen Pakete entfernt, wenn diese nicht an anderer Stelle im Projekt verwiesen wird.</span><span class="sxs-lookup"><span data-stu-id="b606d-207">**Remove dependencies**: when selected, removes any dependent packages if they're not referenced elsewhere in the project.</span></span>

<span data-ttu-id="b606d-208">**Deinstallation erzwingen, auch wenn Abhängigkeiten vorhanden sind, darauf**: Bei Auswahl dieser Option wird ein Paket deinstalliert, auch wenn es weiterhin im Projekt verwiesen wird.</span><span class="sxs-lookup"><span data-stu-id="b606d-208">**Force uninstall even if there are dependencies on it**: when selected, uninstalls a package even if it's still being referenced in the project.</span></span> <span data-ttu-id="b606d-209">Dies wird normalerweise verwendet, in Kombination mit **Abhängigkeiten entfernen** So entfernen Sie ein Paket und alle Abhängigkeiten, die sie installiert.</span><span class="sxs-lookup"><span data-stu-id="b606d-209">This is typically used in combination with **Remove dependencies** to remove a package and whatever dependencies it installed.</span></span> <span data-ttu-id="b606d-210">Mit dieser Option kann jedoch zu fehlerhaften Verweisen im Projekt führen.</span><span class="sxs-lookup"><span data-stu-id="b606d-210">Using this option may, however, lead to broken references in the project.</span></span> <span data-ttu-id="b606d-211">In solchen Fällen müssen Sie möglicherweise auf [Installieren dieser anderen Pakete](../consume-packages/reinstalling-and-updating-packages.md).</span><span class="sxs-lookup"><span data-stu-id="b606d-211">In such cases, you may need to [reinstall those other packages](../consume-packages/reinstalling-and-updating-packages.md).</span></span>
