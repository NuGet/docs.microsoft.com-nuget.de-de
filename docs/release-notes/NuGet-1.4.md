---
title: Anmerkungen zu dieser Version von nuget 1,4
description: Anmerkungen zu dieser Version von nuget 1,4 einschließlich bekannter Probleme, Fehlerbehebungen, hinzugefügter Features und dcrs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 4b31c02b9251d6d45d952fdf8b111493495d57ba
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/02/2020
ms.locfileid: "78230706"
---
# <a name="nuget-14-release-notes"></a><span data-ttu-id="95d9a-103">Anmerkungen zu dieser Version von nuget 1,4</span><span class="sxs-lookup"><span data-stu-id="95d9a-103">NuGet 1.4 Release Notes</span></span>

<span data-ttu-id="95d9a-104">Anmerkungen zu [nuget 1,3](../release-notes/nuget-1.3.md) | Anmerkungen zur [nuget](../release-notes/nuget-1.5.md) -Version 1,5</span><span class="sxs-lookup"><span data-stu-id="95d9a-104">[NuGet 1.3 Release Notes](../release-notes/nuget-1.3.md) | [NuGet 1.5 Release Notes](../release-notes/nuget-1.5.md)</span></span>

<span data-ttu-id="95d9a-105">Nuget 1,4 wurde am 17. Juni 2011 veröffentlicht.</span><span class="sxs-lookup"><span data-stu-id="95d9a-105">NuGet 1.4 was released on June 17, 2011.</span></span>

## <a name="features"></a><span data-ttu-id="95d9a-106">Features</span><span class="sxs-lookup"><span data-stu-id="95d9a-106">Features</span></span>

### <a name="update-package-improvements"></a><span data-ttu-id="95d9a-107">Update-Paket Verbesserungen</span><span class="sxs-lookup"><span data-stu-id="95d9a-107">Update-Package improvements</span></span>
<span data-ttu-id="95d9a-108">Mit nuget 1,4 werden viele Verbesserungen am Befehl "Update-Package" eingeführt, was die Beibehaltung von Paketen in derselben Version in mehreren Projekten in einer Projekt Mappe vereinfacht.</span><span class="sxs-lookup"><span data-stu-id="95d9a-108">NuGet 1.4 introduces a lot of improvements to the Update-Package command making it easier to keep packages at the same version across multiple projects in a solution.</span></span> <span data-ttu-id="95d9a-109">Wenn beispielsweise ein Paket auf die neueste Version aktualisiert wird, ist es sehr üblich, dass alle Projekte, die dieses Paket installiert haben, auf dieselbe Verifizierung aktualisiert werden.</span><span class="sxs-lookup"><span data-stu-id="95d9a-109">For example, when upgrading a package to the latest version, it's very common to want all projects with that package installed to be updated to the same verision.</span></span>

<span data-ttu-id="95d9a-110">Der `Update-Package`-Befehl erleichtert nun Folgendes:</span><span class="sxs-lookup"><span data-stu-id="95d9a-110">The `Update-Package` command now makes it easier to:</span></span>

#### <a name="update-all-packages-in-a-single-project"></a><span data-ttu-id="95d9a-111">Alle Pakete in einem einzelnen Projekt aktualisieren</span><span class="sxs-lookup"><span data-stu-id="95d9a-111">Update all packages in a single project</span></span>

    Update-Package -Project MvcApplication1

#### <a name="update-a-package-in-all-projects"></a><span data-ttu-id="95d9a-112">Aktualisieren eines Pakets in allen Projekten</span><span class="sxs-lookup"><span data-stu-id="95d9a-112">Update a package in all projects</span></span>

    Update-Package PackageId

#### <a name="update-all-packages-in-all-projects"></a><span data-ttu-id="95d9a-113">Alle Pakete in allen Projekten aktualisieren</span><span class="sxs-lookup"><span data-stu-id="95d9a-113">Update all packages in all projects</span></span>

    Update-Package

#### <a name="perform-a-safe-update-on-all-packages"></a><span data-ttu-id="95d9a-114">Ausführen eines "sicheren" Updates für alle Pakete</span><span class="sxs-lookup"><span data-stu-id="95d9a-114">Perform a "safe" update on all packages</span></span>
<span data-ttu-id="95d9a-115">Das `-Safe`-Flag schränkt Upgrades auf Versionen mit der gleichen Haupt-und neben Versions Komponente ein.</span><span class="sxs-lookup"><span data-stu-id="95d9a-115">The `-Safe` flag constrains upgrades to only versions with the same Major and Minor version component.</span></span> <span data-ttu-id="95d9a-116">Wenn z. b. Version 1.0.0 eines Pakets installiert ist und die Versionen 1.0.1, 1.0.2 und 1,1 im Feed verfügbar sind, wird das Paket mit dem `-Safe`-Flag auf 1.0.2 aktualisiert.</span><span class="sxs-lookup"><span data-stu-id="95d9a-116">For example, if version 1.0.0 of a package is installed, and versions 1.0.1, 1.0.2, and 1.1 are available in the feed, the `-Safe` flag updates the package to 1.0.2.</span></span> <span data-ttu-id="95d9a-117">Wenn Sie ohne das `-Safe`-Flag aktualisieren, wird das Paket auf die neueste Version 1,1 aktualisiert.</span><span class="sxs-lookup"><span data-stu-id="95d9a-117">Upgrading without the `-Safe` flag would upgrade the package to the latest version, 1.1.</span></span>

    Update-Package -Safe

### <a name="managing-packages-at-the-solution-level"></a><span data-ttu-id="95d9a-118">Verwalten von Paketen auf Projektmappenebene</span><span class="sxs-lookup"><span data-stu-id="95d9a-118">Managing Packages at the Solution Level</span></span>
<span data-ttu-id="95d9a-119">Vor dem nuget 1,4 war das Installieren eines Pakets in mehreren Projekten mit dem Dialogfeld mühsam.</span><span class="sxs-lookup"><span data-stu-id="95d9a-119">Prior to NuGet 1.4, installing a package into multiple projects was cumbersome using the dialog.</span></span> <span data-ttu-id="95d9a-120">Es war erforderlich, dass das Dialogfeld einmal pro Projekt gestartet wird.</span><span class="sxs-lookup"><span data-stu-id="95d9a-120">It required launching the dialog once per project.</span></span>

<span data-ttu-id="95d9a-121">Nuget 1,4 bietet Unterstützung für das Installieren/Deinstallieren/Aktualisieren von Paketen in mehreren Projekten gleichzeitig.</span><span class="sxs-lookup"><span data-stu-id="95d9a-121">NuGet 1.4 adds support for installing/uninstalling/updating packages in multiple projects at the same time.</span></span> <span data-ttu-id="95d9a-122">Starten Sie einfach mit der rechten Maustaste auf die Projekt Mappe, und wählen Sie die Menüoption **nuget-Pakete verwalten** aus.</span><span class="sxs-lookup"><span data-stu-id="95d9a-122">Simply launch the by right clicking the Solution and selecting the **Manage NuGet Packages** menu option.</span></span>

![Dialogfeld "nuget-Pakete verwalten" auf Lösungsebene](./media/manage-nuget-packages-solution-dialog.png)

<span data-ttu-id="95d9a-124">Beachten Sie, dass in der Titelleiste des Dialog Felds der Name der Projekt Mappe und nicht der Name eines Projekts angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="95d9a-124">Notice that in the title bar of the dialog, the name of the solution is displayed, not the name of a project.</span></span>
<span data-ttu-id="95d9a-125">Paket Vorgänge bieten nun eine Liste von Kontrollkästchen mit der Liste der Projekte, auf die der Vorgang angewendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="95d9a-125">Package operations now provide a list of checkboxes with the list of projects the operation should apply to.</span></span>

![Projektauswahl für nuget-Pakete verwalten](./media/manage-nuget-packages-project-selection.png)

<span data-ttu-id="95d9a-127">Weitere Informationen finden Sie im Thema zum [Verwalten von Paketen für die Lösung](../consume-packages/install-use-packages-visual-studio.md#manage-packages-for-the-solution).</span><span class="sxs-lookup"><span data-stu-id="95d9a-127">For more details, see the topic on [Managing Packages for the Solution](../consume-packages/install-use-packages-visual-studio.md#manage-packages-for-the-solution).</span></span>

### <a name="constraining-upgrades-to-allowed-versions"></a><span data-ttu-id="95d9a-128">Einschränken von Upgrades auf zulässige Versionen</span><span class="sxs-lookup"><span data-stu-id="95d9a-128">Constraining Upgrades To Allowed Versions</span></span>
<span data-ttu-id="95d9a-129">Wenn Sie den `Update-Package` Befehl in einem Paket ausführen (oder das Paket mithilfe des Dialog Felds aktualisieren), wird es standardmäßig auf die neueste Version im Feed aktualisiert.</span><span class="sxs-lookup"><span data-stu-id="95d9a-129">By default, when running the `Update-Package` command on a package (or updating the package using dialog), it will be updated to the latest version in the feed.</span></span> <span data-ttu-id="95d9a-130">Mit der neuen Unterstützung für das Aktualisieren aller Pakete kann es Fälle geben, in denen Sie ein Paket für einen bestimmten Versions Bereich sperren möchten.</span><span class="sxs-lookup"><span data-stu-id="95d9a-130">With the new support for updating all packages, there may be cases in which you want to lock a package to a specific version range.</span></span> <span data-ttu-id="95d9a-131">Beispielsweise können Sie im Voraus wissen, dass Ihre Anwendung nur mit Version 2. \* eines Pakets funktioniert, aber nicht mit 3,0 und höher.</span><span class="sxs-lookup"><span data-stu-id="95d9a-131">For example, you may know in advance that your application will only work with version 2.\* of a package, but not 3.0 and above.</span></span> <span data-ttu-id="95d9a-132">Um zu verhindern, dass das Paket versehentlich auf 3 aktualisiert wird, fügt nuget 1,4 Unterstützung für das Einschränken des Bereichs von Versionen hinzu, auf die Pakete aktualisiert werden können, indem Sie die `packages.config` Datei mithilfe des neuen `allowedVersions` Attributs bearbeiten.</span><span class="sxs-lookup"><span data-stu-id="95d9a-132">In order to prevent accidentally updating the package to 3, NuGet 1.4 adds support for constraining the range of versions that packages can be upgraded to by hand editing the `packages.config` file using the new `allowedVersions` attribute.</span></span>

<span data-ttu-id="95d9a-133">Das folgende Beispiel zeigt beispielsweise, wie das `SomePackage` Paket den Versions Bereich 2,0-3,0 (exklusiv) gesperrt wird.</span><span class="sxs-lookup"><span data-stu-id="95d9a-133">For example, the following example shows how to lock the `SomePackage` package the version range 2.0 - 3.0 (exclusive).</span></span>
<span data-ttu-id="95d9a-134">Das `allowedVersions`-Attribut akzeptiert Werte unter Verwendung des [Versions Bereichs Formats](../concepts/package-versioning.md#version-ranges).</span><span class="sxs-lookup"><span data-stu-id="95d9a-134">The `allowedVersions` attribute accepts values using the [version range format](../concepts/package-versioning.md#version-ranges).</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="SomePackage" version="2.1.0" allowedVersions="[2.0, 3.0)" />
</packages>
```

<span data-ttu-id="95d9a-135">Beachten Sie, dass in 1,4 das Sperren eines Pakets in einen bestimmten Versions Bereich Hand bearbeitetet werden muss.</span><span class="sxs-lookup"><span data-stu-id="95d9a-135">Note that in 1.4, locking a package to a specific version range must be hand-edited.</span></span> <span data-ttu-id="95d9a-136">In nuget 1,5 planen wir die Unterstützung für das Platzieren dieses Bereichs über den `Install-Package`-Befehl.</span><span class="sxs-lookup"><span data-stu-id="95d9a-136">In NuGet 1.5 we plan to add support for placing this range via the `Install-Package` command.</span></span>

### <a name="package-visualizer"></a><span data-ttu-id="95d9a-137">Paket Schnellansicht</span><span class="sxs-lookup"><span data-stu-id="95d9a-137">Package Visualizer</span></span>
<span data-ttu-id="95d9a-138">Mithilfe der neuen Paket Schnellansicht, die über die Menüoption **Tools** -> **Library Package Manager** -> **Package Visualizer** gestartet wurde, können Sie alle Projekte und ihre Paketabhängigkeiten innerhalb einer Projekt Mappe problemlos visualisieren.</span><span class="sxs-lookup"><span data-stu-id="95d9a-138">The new package visualizer, launched via the **Tools** -> **Library Package Manager** -> **Package Visualizer** menu option, enables you to easily visualize all the projects and their package dependencies within a solution.</span></span>

<span data-ttu-id="95d9a-139">_**Wichtiger Hinweis:** Diese Funktion nutzt die DGML-Unterstützung in Visual Studio. Das Erstellen der Visualisierung wird nur in Visual Studio Ultimate unterstützt. Das Anzeigen eines dgml-Diagramms wird nur in Visual Studio Premium oder höher unterstützt._</span><span class="sxs-lookup"><span data-stu-id="95d9a-139">_**Important Note:** This feature takes advantage of the DGML support in Visual Studio. Creating the visualization is only supported in Visual Studio Ultimate. Viewing a DGML diagram is only supported in Visual Studio Premium or Higher._</span></span>

![Paket Schnellansicht](./media/package-visualizer.png)

### <a name="automatic-update-check-for-the-nuget-dialog"></a><span data-ttu-id="95d9a-141">Automatische Update Überprüfung für das nuget-Dialog Feld</span><span class="sxs-lookup"><span data-stu-id="95d9a-141">Automatic Update Check for the NuGet Dialog</span></span>
<span data-ttu-id="95d9a-142">In einigen Versionen von nuget werden neue Funktionen eingeführt, die über die `.nuspec` Datei ausgedrückt werden, die von älteren Versionen des nuget-Dialog Felds nicht verstanden werden.</span><span class="sxs-lookup"><span data-stu-id="95d9a-142">Some versions of NuGet introduce new features expressed via the `.nuspec` file which are not understood by older versions of the NuGet dialog.</span></span>
<span data-ttu-id="95d9a-143">Ein Beispiel hierfür ist die Einführung in nuget 1,4 zum [angeben](../release-notes/nuget-1.2.md#framework-assembly-refs)von Frameworkassemblys.</span><span class="sxs-lookup"><span data-stu-id="95d9a-143">One example is the introduction in NuGet 1.4 for [specifying framework assemblies](../release-notes/nuget-1.2.md#framework-assembly-refs).</span></span>
<span data-ttu-id="95d9a-144">Daher ist es wichtig, dass Sie die neueste Version von nuget verwenden, um sicherzustellen, dass Sie Pakete verwenden können, die die neuesten Features nutzen.</span><span class="sxs-lookup"><span data-stu-id="95d9a-144">Because of this, it's important to use the latest version of NuGet to ensure you can use packages taking advantage of the latest features.</span></span>
<span data-ttu-id="95d9a-145">Um nuget-Aktualisierungen besser sichtbar zu machen, enthält das nuget-Dialogfeld Logik zum hervorheben, wenn eine neuere Version verfügbar ist.</span><span class="sxs-lookup"><span data-stu-id="95d9a-145">To make updates to NuGet more visible, the NuGet dialog contains logic to highlight when a newer version is available.</span></span>

<span data-ttu-id="95d9a-146">_**Hinweis**: die Überprüfung wird nur vorgenommen, wenn die Registerkarte **Online** in der aktuellen Sitzung ausgewählt wurde._</span><span class="sxs-lookup"><span data-stu-id="95d9a-146">_**Note**: The check is only made if the **Online** tab has been selected in the current session._</span></span>

![Dialogfeld "nuget-Pakete verwalten" mit neuer verfügbarer Version](./media/manage-nuget-packages-update-notification.png)

<span data-ttu-id="95d9a-148">Wenn Sie die automatische Suche nach Updates deaktivieren möchten, wechseln Sie zum Dialogfeld nuget-Einstellungen, und deaktivieren Sie **automatisch nach Updates suchen**.</span><span class="sxs-lookup"><span data-stu-id="95d9a-148">To turn off the automatic check for updates, go to the NuGet settings dialog and uncheck **Automatically check for updates**.</span></span>

![Nuget-Einstellungen](./media/nuget-settings.png)

<span data-ttu-id="95d9a-150">Diese Funktion wurde in nuget 1,3 tatsächlich hinzugefügt, wäre aber natürlich nicht sichtbar, bis ein Update auf 1,3, z. b. nuget 1,4, verfügbar gemacht wurde.</span><span class="sxs-lookup"><span data-stu-id="95d9a-150">This feature was actually added in NuGet 1.3, but would not be visible, of course, until an update to 1.3, such as NuGet 1.4, was made available.</span></span>

### <a name="package-manager-dialog-improvements"></a><span data-ttu-id="95d9a-151">Verbesserungen im Paket-Manager</span><span class="sxs-lookup"><span data-stu-id="95d9a-151">Package Manager Dialog Improvements</span></span>
* <span data-ttu-id="95d9a-152">**Verbesserte Menü Namen**: die Menü Optionen zum Starten des Dialog Felds wurden aus Gründen der Übersichtlichkeit umbenannt.</span><span class="sxs-lookup"><span data-stu-id="95d9a-152">**Menu names improved**: Menu options to launch the dialog have been renamed for clarity.</span></span> <span data-ttu-id="95d9a-153">Die Menüoption ist jetzt **nuget-Pakete verwalten**.</span><span class="sxs-lookup"><span data-stu-id="95d9a-153">The menu option is now **Manage NuGet Packages**.</span></span>
* <span data-ttu-id="95d9a-154">**Detailbereich zeigt das aktuelle Aktualisierungsdatum**an: im Dialogfeld "nuget" wird das Datum des letzten Updates im Detailbereich für ein Paket angezeigt, wenn die Registerkarte " **Online** " oder " **Updates** " ausgewählt ist.</span><span class="sxs-lookup"><span data-stu-id="95d9a-154">**Details pane shows latest update date**: The NuGet dialog displays the date of the latest update in the details pane for a package when the **Online** or **Updates** tab is selected.</span></span>
* <span data-ttu-id="95d9a-155">**Liste der angezeigten Tags**: das nuget-Dialogfeld zeigt Tags an.</span><span class="sxs-lookup"><span data-stu-id="95d9a-155">**List of tags displayed**: The Nuget dialog displays tags.</span></span>

### <a name="powershell-improvements"></a><span data-ttu-id="95d9a-156">PowerShell-Optimierungen</span><span class="sxs-lookup"><span data-stu-id="95d9a-156">Powershell Improvements</span></span>
* <span data-ttu-id="95d9a-157">**Signierte PowerShell-Skripts**: nuget umfasst signierte PowerShell-Skripts, die die Verwendung in restriktiveren Umgebungen</span><span class="sxs-lookup"><span data-stu-id="95d9a-157">**Signed PowerShell scripts**: NuGet includes signed Powershell scripts enabling usage in more restrictive environments.</span></span>
* <span data-ttu-id="95d9a-158">**Unterstützung**der Eingabeaufforderung: die Paket-Manager-Konsole unterstützt nun die Eingabeaufforderung über die Befehle `$host.ui.Prompt` und `$host.ui.PromptForChoice`</span><span class="sxs-lookup"><span data-stu-id="95d9a-158">**Prompting Support**: The Package Manager Console now supports prompting via the `$host.ui.Prompt` and `$host.ui.PromptForChoice` commands.</span></span>
* <span data-ttu-id="95d9a-159">**Paketquellen Namen**: die Angabe des Namens einer Paketquelle wird unterstützt, wenn eine Paketquelle mit dem `-Source`-Flag angegeben wird.</span><span class="sxs-lookup"><span data-stu-id="95d9a-159">**Package Source Names**: Supplying the name of a package source is supported when specifying a package source using the `-Source` flag.</span></span>

### <a name="nugetexe-command-line-improvements"></a><span data-ttu-id="95d9a-160">Verbesserungen der Befehlszeile "nuget. exe"</span><span class="sxs-lookup"><span data-stu-id="95d9a-160">nuget.exe Command line improvements</span></span>
* <span data-ttu-id="95d9a-161">**Benutzerdefinierte nuget-Befehle**: "nuget. exe" kann über benutzerdefinierte Befehle mithilfe von MEF erweitert werden.</span><span class="sxs-lookup"><span data-stu-id="95d9a-161">**NuGet Custom Commands**: nuget.exe is extensible via custom commands using MEF.</span></span>
* <span data-ttu-id="95d9a-162">**Einfacherer Workflow zum Erstellen von Symbol Paketen**: das `-Symbols`-Flag kann auf eine normale, auf der Konvention basierende Ordnerstruktur angewendet werden, indem ein Symbol Paket erstellt wird, indem nur die Quell-und `.pdb` Dateien in den Ordner eingeschlossen werden.</span><span class="sxs-lookup"><span data-stu-id="95d9a-162">**Simpler the workflow for creating symbol packages**: The `-Symbols` flag can be applied to a normal convention based folder structure creating a symbols package by only including the source and `.pdb` files within the folder.</span></span>
* <span data-ttu-id="95d9a-163">**Angeben mehrerer Quellen**: der `NuGet install`-Befehl unterstützt die Angabe mehrerer Quellen mithilfe von Semikolons als Trennzeichen oder durch mehrmals Angabe von `-Source`.</span><span class="sxs-lookup"><span data-stu-id="95d9a-163">**Specifying Multiple Sources**: The `NuGet install` command supports specifying multiple sources using semi-colons as a delimiter or by specifying `-Source` multiple times.</span></span>
* <span data-ttu-id="95d9a-164">**Unterstützung der Proxy Authentifizierung**: nuget 1,4 fügt Unterstützung für die Eingabeaufforderung für Benutzer Anmelde Informationen hinzu, wenn nuget hinter einem Proxy verwendet wird</span><span class="sxs-lookup"><span data-stu-id="95d9a-164">**Proxy Authentication Support**: NuGet 1.4 adds support for prompting for user credentials when using NuGet behind a proxy that requires authentication.</span></span>
* <span data-ttu-id="95d9a-165">fehlerhafte Änderung von " **nuget. exe**": das `-Self`-Flag ist jetzt erforderlich, damit "nuget. exe" sich selbst aktualisiert.</span><span class="sxs-lookup"><span data-stu-id="95d9a-165">**nuget.exe Update Breaking Change**: The `-Self` flag is now required for nuget.exe to update itself.</span></span> <span data-ttu-id="95d9a-166">`nuget.exe Update` nimmt nun einen Pfad zur `packages.config` Datei an und versucht, Pakete zu aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="95d9a-166">`nuget.exe Update` now takes in a path to the `packages.config` file and will attempt to update packages.</span></span> <span data-ttu-id="95d9a-167">Beachten Sie, dass dieses Update so eingeschränkt ist, dass es nicht: \* \* aktualisieren, hinzufügen und Entfernen von Inhalten in der Projektdatei.</span><span class="sxs-lookup"><span data-stu-id="95d9a-167">Note that this update is limited in that it will not: \*\* Update, add, remove content in the project file.</span></span>
<span data-ttu-id="95d9a-168">\* \* Führen Sie PowerShell-Skripts innerhalb des Pakets aus.</span><span class="sxs-lookup"><span data-stu-id="95d9a-168">\*\* Run Powershell scripts within the package.</span></span>

### <a name="nuget-server-support-for-pushing-packages-using-nugetexe"></a><span data-ttu-id="95d9a-169">Unterstützung für nuget-Server zum Übertragen von Paketen mithilfe von nuget. exe</span><span class="sxs-lookup"><span data-stu-id="95d9a-169">NuGet Server Support for Pushing Packages using nuget.exe</span></span>
<span data-ttu-id="95d9a-170">Nuget bietet eine einfache Möglichkeit, ein einfaches [webbasiertes nuget-Repository](../hosting-packages/nuget-server.md) über das `NuGet.Server` nuget-Paket zu hosten.</span><span class="sxs-lookup"><span data-stu-id="95d9a-170">NuGet includes a simple way to host a [lightweight web based NuGet repository](../hosting-packages/nuget-server.md) via the `NuGet.Server` NuGet package.</span></span> <span data-ttu-id="95d9a-171">Mit nuget 1,4 unterstützt der Lightweight-Server das pushen und Löschen von Paketen mithilfe von "nuget. exe".</span><span class="sxs-lookup"><span data-stu-id="95d9a-171">With NuGet 1.4, the lightweight server supports pushing and deleting packages using nuget.exe.</span></span>
<span data-ttu-id="95d9a-172">Die neueste Version von `NuGet.Server` fügt eine neue `appSetting`namens `apiKey`hinzu.</span><span class="sxs-lookup"><span data-stu-id="95d9a-172">The latest version of `NuGet.Server` adds a new `appSetting`, named `apiKey`.</span></span> <span data-ttu-id="95d9a-173">Wenn der Schlüssel weggelassen oder leer gelassen wird, ist das Übertragen von Paketen in den Feed deaktiviert.</span><span class="sxs-lookup"><span data-stu-id="95d9a-173">When the key is omitted or left blank, pushing packages to the feed is disabled.</span></span> <span data-ttu-id="95d9a-174">Wenn Sie den APIKey auf einen Wert festlegen (im Idealfall ein sicheres Kennwort), können Pakete mithilfe von "nuget. exe" per Push</span><span class="sxs-lookup"><span data-stu-id="95d9a-174">Setting the apiKey to a value (ideally a strong password) enables pushing packages using nuget.exe.</span></span>

```xml
<appSettings>
    <!-- Set the value here to allow people to push/delete packages from the server.
            NOTE: This is a shared key (password) for all users. -->
    <add key="apiKey" value="" />
</appSettings>
```

### <a name="support-for-windows-phone-tools-mango-edition"></a><span data-ttu-id="95d9a-175">Unterstützung für die Windows Phone Tools-Mango-Edition</span><span class="sxs-lookup"><span data-stu-id="95d9a-175">Support for Windows Phone Tools Mango Edition</span></span>
<span data-ttu-id="95d9a-176">Nuget wird jetzt in der Release Candidate-Version von Windows Phone Tools für MANGO unterstützt.</span><span class="sxs-lookup"><span data-stu-id="95d9a-176">NuGet is now supported in the release candidate version of Windows Phone Tools for Mango.</span></span>
<span data-ttu-id="95d9a-177">Derzeit verfügt Windows Phone Tools nicht über Unterstützung für den Visual Studio-Erweiterungs-Manager. um nuget für Windows Phone Tools zu installieren, müssen Sie die VSIX möglicherweise manuell herunterladen und ausführen.</span><span class="sxs-lookup"><span data-stu-id="95d9a-177">Currently, Windows Phone Tools does not have support for the Visual Studio Extension manager so to install NuGet for Windows Phone Tools, you may need to download and run the VSIX manually.</span></span>

<span data-ttu-id="95d9a-178">Führen Sie den folgenden Befehl aus, um nuget für Windows Phone Tools zu deinstallieren.</span><span class="sxs-lookup"><span data-stu-id="95d9a-178">To uninstall NuGet for Windows Phone Tools, run the following command.</span></span>

     vsixinstaller.exe /uninstall:NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5

## <a name="bug-fixes"></a><span data-ttu-id="95d9a-179">Fehlerbehebungen</span><span class="sxs-lookup"><span data-stu-id="95d9a-179">Bug Fixes</span></span>
<span data-ttu-id="95d9a-180">Für nuget 1,4 wurden insgesamt 88 Arbeitselemente korrigiert.</span><span class="sxs-lookup"><span data-stu-id="95d9a-180">NuGet 1.4 had a total of 88 work items fixed.</span></span> <span data-ttu-id="95d9a-181">71 von diesen wurden als Fehler gekennzeichnet.</span><span class="sxs-lookup"><span data-stu-id="95d9a-181">71 of those were marked as bugs.</span></span>

<span data-ttu-id="95d9a-182">Eine vollständige Liste der Arbeitselemente, die in nuget 1,4 behoben wurden, finden Sie in der [nuget-Problemverfolgung für diese Version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="95d9a-182">For a full list of work items fixed in NuGet 1.4, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.4&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="95d9a-183">Fehlerbehebungen beachten Sie Folgendes:</span><span class="sxs-lookup"><span data-stu-id="95d9a-183">Bug fixes worth noting:</span></span>

* <span data-ttu-id="95d9a-184">[Problem 603](http://nuget.codeplex.com/workitem/603): Paketabhängigkeiten in verschiedenen Depots werden ordnungsgemäß aufgelöst, wenn eine bestimmte Paketquelle angegeben wird.</span><span class="sxs-lookup"><span data-stu-id="95d9a-184">[Issue 603](http://nuget.codeplex.com/workitem/603): Package dependencies across different repositories resolves correctly when specifying a specific package source.</span></span>
* <span data-ttu-id="95d9a-185">[Problem 1036](http://nuget.codeplex.com/workitem/1036): das Hinzufügen von `NuGet Pack SomeProject.csproj` zum Postbuildereignis bewirkt nicht mehr eine Endlosschleife.</span><span class="sxs-lookup"><span data-stu-id="95d9a-185">[Issue 1036](http://nuget.codeplex.com/workitem/1036): Adding `NuGet Pack SomeProject.csproj` to post-build event no longer causes an infinite loop.</span></span>
* <span data-ttu-id="95d9a-186">[Problem 961](http://nuget.codeplex.com/workitem/961): `-Source`-Flag unterstützt relative Pfade.</span><span class="sxs-lookup"><span data-stu-id="95d9a-186">[Issue 961](http://nuget.codeplex.com/workitem/961): `-Source` flag supports relative paths.</span></span>

## <a name="nuget-14-update"></a><span data-ttu-id="95d9a-187">Nuget 1,4-Update</span><span class="sxs-lookup"><span data-stu-id="95d9a-187">NuGet 1.4 Update</span></span>
<span data-ttu-id="95d9a-188">Kurz nach der Veröffentlichung von nuget 1,4 haben wir einige Probleme festgestellt, die für die Behebung wichtig waren.</span><span class="sxs-lookup"><span data-stu-id="95d9a-188">Shortly after the release of NuGet 1.4, we found a couple of issues that were important to fix.</span></span>
<span data-ttu-id="95d9a-189">Die spezifische Versionsnummer dieses Updates auf 1,4 lautet 1.4.20615.9020.</span><span class="sxs-lookup"><span data-stu-id="95d9a-189">The specific version number of this update to 1.4 is 1.4.20615.9020.</span></span>

### <a name="bug-fixes"></a><span data-ttu-id="95d9a-190">Fehlerbehebungen</span><span class="sxs-lookup"><span data-stu-id="95d9a-190">Bug Fixes</span></span>
* <span data-ttu-id="95d9a-191">[Problem 1220](http://nuget.codeplex.com/workitem/1220): "Update-Package" wird `install.ps1`/`uninstall.ps1` nicht in allen Projekten ausgeführt, wenn mehrere Projekte vorhanden sind.</span><span class="sxs-lookup"><span data-stu-id="95d9a-191">[Issue 1220](http://nuget.codeplex.com/workitem/1220): Update-Package doesnt execute `install.ps1`/`uninstall.ps1` in all projects when there is more than one project</span></span>
* <span data-ttu-id="95d9a-192">[Problem 1156](http://nuget.codeplex.com/workitem/1156): der Paket-Manager ist auf W2K3/XP hängen (Wenn PowerShell 2 nicht installiert ist).</span><span class="sxs-lookup"><span data-stu-id="95d9a-192">[Issue 1156](http://nuget.codeplex.com/workitem/1156): Package Manager Consol stuck on W2K3/XP (when Powershell 2 is not installed)</span></span>
