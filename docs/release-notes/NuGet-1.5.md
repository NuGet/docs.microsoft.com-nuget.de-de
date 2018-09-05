---
title: Anmerkungen zu NuGet-Version 1.5
description: Anmerkungen zu NuGet 1.5, einschließlich der bekannten Probleme, Fehlerkorrekturen, hinzugefügter Features und DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: c2b549f65e675e5fde9ae1dfea3f44f7d691a86b
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548724"
---
# <a name="nuget-15-release-notes"></a><span data-ttu-id="e388e-103">Anmerkungen zu NuGet-Version 1.5</span><span class="sxs-lookup"><span data-stu-id="e388e-103">NuGet 1.5 Release Notes</span></span>

<span data-ttu-id="e388e-104">[Anmerkungen zu NuGet 1.4](../release-notes/nuget-1.4.md) | [Anmerkungen zu NuGet 1.6](../release-notes/nuget-1.6.md)</span><span class="sxs-lookup"><span data-stu-id="e388e-104">[NuGet 1.4 Release Notes](../release-notes/nuget-1.4.md) | [NuGet 1.6 Release Notes](../release-notes/nuget-1.6.md)</span></span>

<span data-ttu-id="e388e-105">NuGet 1.5 wurde am 30. August 2011 veröffentlicht.</span><span class="sxs-lookup"><span data-stu-id="e388e-105">NuGet 1.5 was released on August 30, 2011.</span></span>

## <a name="features"></a><span data-ttu-id="e388e-106">Features</span><span class="sxs-lookup"><span data-stu-id="e388e-106">Features</span></span>

### <a name="project-templates-with-preinstalled-nuget-packages"></a><span data-ttu-id="e388e-107">Projektvorlagen vorinstallierte NuGet-Pakete</span><span class="sxs-lookup"><span data-stu-id="e388e-107">Project Templates with Preinstalled NuGet Packages</span></span>
<span data-ttu-id="e388e-108">Wenn Sie eine neue ASP.NET MVC 3-Projektvorlage erstellen, werden die jQuery-Skriptbibliotheken, die im Projekt enthaltenen tatsächlich dort platziert, durch die Installation von NuGet-Pakete.</span><span class="sxs-lookup"><span data-stu-id="e388e-108">When creating a new ASP.NET MVC 3 project template, the jQuery script libraries included in the project are actually placed there by installing NuGet packages.</span></span>

<span data-ttu-id="e388e-109">Die ASP.NET MVC 3-Projektvorlage enthält einen Satz von NuGet-Pakete, die installiert werden, wenn die Projektvorlage aus aufgerufen wird.</span><span class="sxs-lookup"><span data-stu-id="e388e-109">The ASP.NET MVC 3 project template includes a set of NuGet packages that get installed when the project template is invoked.</span></span> <span data-ttu-id="e388e-110">Diese Fähigkeit zum Einschließen von NuGet-Pakete mit einer Projektvorlage ist jetzt ein Feature von NuGet, _alle_ Projektvorlage kann jetzt nutzen.</span><span class="sxs-lookup"><span data-stu-id="e388e-110">This ability to include NuGet packages with a project template is now a feature of NuGet that _any_ project template can now take advantage of.</span></span>

<span data-ttu-id="e388e-111">Weitere Informationen zu diesem Feature finden Sie in diesem [Blogbeitrag vom Entwickler des Features](http://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx).</span><span class="sxs-lookup"><span data-stu-id="e388e-111">For more details about this feature, read this [blog post by the developer of the feature](http://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx).</span></span>

### <a name="explicit-assembly-references"></a><span data-ttu-id="e388e-112">Explizite Assemblyverweise</span><span class="sxs-lookup"><span data-stu-id="e388e-112">Explicit Assembly References</span></span>

<span data-ttu-id="e388e-113">Einen neuen `<references />` Element, das verwendet wird, explizit angeben, welche Assemblys in der das Paket verwiesen werden soll.</span><span class="sxs-lookup"><span data-stu-id="e388e-113">Added a new `<references />` element used to explicitly specify which assemblies within the the package should be referenced.</span></span>

<span data-ttu-id="e388e-114">Angenommen, Sie Folgendes hinzufügen:</span><span class="sxs-lookup"><span data-stu-id="e388e-114">For example, if you add the following:</span></span>

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

<span data-ttu-id="e388e-115">Nur die `xunit.dll` und `xunit.extensions.dll` in den entsprechenden verwiesen [Frameworkprofil/Unterordner](../reference/nuspec.md#explicit-assembly-references) von der `lib` Ordner, auch wenn es andere Assemblys im Ordner.</span><span class="sxs-lookup"><span data-stu-id="e388e-115">Then only the `xunit.dll` and `xunit.extensions.dll` will be referenced from the appropriate [framework/profile subfolder](../reference/nuspec.md#explicit-assembly-references) of the `lib` folder even if there are other assemblies in the folder.</span></span>

<span data-ttu-id="e388e-116">Wenn dieses Element ist nicht angegeben, wird das übliche Verhalten, die bezieht auf jede Assembly in den `lib` Ordner.</span><span class="sxs-lookup"><span data-stu-id="e388e-116">If this element is omitted, then the usual behavior applies, which is to reference every assembly in the `lib` folder.</span></span>

<span data-ttu-id="e388e-117">__Was wird für dieses Feature verwendet?__</span><span class="sxs-lookup"><span data-stu-id="e388e-117">__What is this feature used for?__</span></span>

<span data-ttu-id="e388e-118">Dieses Feature unterstützt nur die Assemblys zur Entwurfszeit.</span><span class="sxs-lookup"><span data-stu-id="e388e-118">This feature supports design-time only assemblies.</span></span> <span data-ttu-id="e388e-119">Beispielsweise müssen bei der Verwendung von Codeverträgen die Vertragsassemblys neben den runtimeassemblys sein, die sie erweitern, damit Visual Studio sie finden jedoch die Vertragsassemblys sollte nicht tatsächlich vom Projekt verwiesen werden, und in nicht kopiert werden sollen die `bin` Ordner.</span><span class="sxs-lookup"><span data-stu-id="e388e-119">For example, when using Code Contracts, the contract assemblies need to be next to the runtime assemblies that they augment so that Visual Studio can find them, but the contract assemblies should not actually be referenced by the project and should not be copied into the `bin` folder.</span></span>

<span data-ttu-id="e388e-120">Ebenso kann das Feature für Komponententestframeworks wie XUnit die benötigen die Tools-Assemblys werden neben den runtimeassemblys befinden, aber von der Projekt-verweisen ausgeschlossen, verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="e388e-120">Likewise, the feature can be used to for unit test frameworks such as XUnit which need its tools assemblies to be located next to the runtime assemblies, but excluded from project references.</span></span>

### <a name="added-ability-to-exclude-files-in-the-nuspec"></a><span data-ttu-id="e388e-121">Neue Möglichkeit zum Ausschließen von Dateien in der NuSpec</span><span class="sxs-lookup"><span data-stu-id="e388e-121">Added ability to exclude files in the .nuspec</span></span>
<span data-ttu-id="e388e-122">Die `<file>` Element innerhalb einer `.nuspec` Datei kann verwendet werden, um eine bestimmte Datei oder einen Satz von Dateien, die mit einem Platzhalter enthalten.</span><span class="sxs-lookup"><span data-stu-id="e388e-122">The `<file>` element within a `.nuspec` file can be used to include a specific file or a set of files using a wildcard.</span></span> <span data-ttu-id="e388e-123">Wenn Sie einen Platzhalter zu verwenden, besteht keine Möglichkeit, eine bestimmte Teilmenge der in Ihr enthaltenen Dateien ausschließen.</span><span class="sxs-lookup"><span data-stu-id="e388e-123">When using a wildcard, there's no way to exclude a specific subset of the included files.</span></span> <span data-ttu-id="e388e-124">Nehmen wir beispielsweise an, dass Sie möchten, dass alle Textdateien in einem Ordner mit Ausnahme einer bestimmten.</span><span class="sxs-lookup"><span data-stu-id="e388e-124">For example, suppose you want all text files within a folder except a specific one.</span></span>

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt" />
</files>
```

<span data-ttu-id="e388e-125">Verwenden Sie Semikolons, um mehrere Dateien anzugeben.</span><span class="sxs-lookup"><span data-stu-id="e388e-125">Use semicolons to specify multiple files.</span></span>

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt;log.txt" />
</files>
```

<span data-ttu-id="e388e-126">Oder verwenden Sie einen Platzhalter, um einen Satz von Dateien, z. B. alle Sicherungsdateien ausschließen</span><span class="sxs-lookup"><span data-stu-id="e388e-126">Or use a wild card to exclude a set of files such as all backup files</span></span>

```xml
<files>
    <file src="tools\*.*" target="tools" exclude="*.bak" />
</files>
```

### <a name="removing-packages-using-the-dialog-prompts-to-remove-dependencies"></a><span data-ttu-id="e388e-127">Entfernen von Paketen mithilfe des Dialogfelds aufgefordert, Abhängigkeiten zu entfernen</span><span class="sxs-lookup"><span data-stu-id="e388e-127">Removing packages using the dialog prompts to remove dependencies</span></span>
<span data-ttu-id="e388e-128">Bei der Deinstallation eines Pakets mit Abhängigkeiten von NuGet aufgefordert werden, sodass das Entfernen eines Pakets Abhängigkeiten zusammen mit dem Paket.</span><span class="sxs-lookup"><span data-stu-id="e388e-128">When uninstalling a package with dependencies, NuGet prompts, allowing the removal of a package's dependencies along with the package.</span></span>

![Entfernen die abhängigen Pakete](./media/remove-dependent-packages.png)


### <a name="get-package-command-improvement"></a><span data-ttu-id="e388e-130">`Get-Package` Befehl zur Verbesserung der</span><span class="sxs-lookup"><span data-stu-id="e388e-130">`Get-Package` command improvement</span></span>
<span data-ttu-id="e388e-131">Die `Get-Package` Befehl unterstützt jetzt eine `-ProjectName` Parameter.</span><span class="sxs-lookup"><span data-stu-id="e388e-131">The `Get-Package` command now supports a `-ProjectName` parameter.</span></span> <span data-ttu-id="e388e-132">Also den Befehl</span><span class="sxs-lookup"><span data-stu-id="e388e-132">So the command</span></span>

    Get-Package –ProjectName A

<span data-ttu-id="e388e-133">Listet alle Pakete im Projekt a installiert</span><span class="sxs-lookup"><span data-stu-id="e388e-133">will list all packages installed in project A.</span></span>

### <a name="support-for-proxies-that-require-authentication"></a><span data-ttu-id="e388e-134">Unterstützung von Proxys, für die Authentifizierung erforderlich</span><span class="sxs-lookup"><span data-stu-id="e388e-134">Support for Proxies that require authentication</span></span>
<span data-ttu-id="e388e-135">Wenn Sie NuGet hinter einem Proxy verwenden zu können, die eine Authentifizierung erforderlich ist, fordert NuGet nun Proxyanmeldeinformationen.</span><span class="sxs-lookup"><span data-stu-id="e388e-135">When using NuGet behind a proxy that requires authentication, NuGet will now prompt for proxy credentials.</span></span> <span data-ttu-id="e388e-136">Eingeben von Anmeldeinformationen können NuGet, um die Verbindung mit des remote-Repositorys.</span><span class="sxs-lookup"><span data-stu-id="e388e-136">Entering credentials allows NuGet to connect to the remote repository.</span></span>

### <a name="support-for-repositories-that-require-authentication"></a><span data-ttu-id="e388e-137">Unterstützung für Repositorys, die Authentifizierung erforderlich ist</span><span class="sxs-lookup"><span data-stu-id="e388e-137">Support for Repositories that require authentication</span></span>
<span data-ttu-id="e388e-138">NuGet unterstützt jetzt die Verbindung mit [private Repositorys](../hosting-packages/local-feeds.md) , Basic oder NTLM-Authentifizierung erfordern.</span><span class="sxs-lookup"><span data-stu-id="e388e-138">NuGet now supports connecting to [private repositories](../hosting-packages/local-feeds.md) that require basic or NTLM authentication.</span></span>

<span data-ttu-id="e388e-139">Unterstützung für Digest-Authentifizierung wird in einer zukünftigen Version hinzugefügt werden.</span><span class="sxs-lookup"><span data-stu-id="e388e-139">Support for Digest authentication will be added in a future release.</span></span>

### <a name="performance-improvements-to-the-nugetorg-repository"></a><span data-ttu-id="e388e-140">Leistungsverbesserungen für das nuget.org-repository</span><span class="sxs-lookup"><span data-stu-id="e388e-140">Performance improvements to the nuget.org repository</span></span>
<span data-ttu-id="e388e-141">Wir haben mehrere leistungsverbesserungen auf der NuGet-Katalog zum Paket, auflisten und Durchsuchen schneller werden vorgenommen.</span><span class="sxs-lookup"><span data-stu-id="e388e-141">We've made several performance improvements to the nuget.org gallery to make package listing and searching faster.</span></span>

### <a name="solution-dialog-project-filtering"></a><span data-ttu-id="e388e-142">Dialogfeld Projekt lösungsfilterung</span><span class="sxs-lookup"><span data-stu-id="e388e-142">Solution dialog project filtering</span></span>
<span data-ttu-id="e388e-143">Auf Projektmappenebene im Dialogfeld bei für welche Projekte zu installieren erläutert, nur Projekte, die mit dem ausgewählten Paket kompatibel sind.</span><span class="sxs-lookup"><span data-stu-id="e388e-143">In the Solution-level dialog, when prompting for what projects to install, we only show projects that are compatible with the selected package.</span></span>

### <a name="package-release-notes"></a><span data-ttu-id="e388e-144">Anmerkungen zur Version des Pakets</span><span class="sxs-lookup"><span data-stu-id="e388e-144">Package Release Notes</span></span>
<span data-ttu-id="e388e-145">NuGet-Pakete umfassen jetzt Unterstützung für Anmerkungen zu dieser Version.</span><span class="sxs-lookup"><span data-stu-id="e388e-145">NuGet packages now include support for release notes.</span></span> <span data-ttu-id="e388e-146">Die Anmerkungen zu dieser Version nur Sie beim Anzeigen von _Updates_ für ein Paket, sodass es nicht sinnvoll So fügen sie dem ersten Release hinzu.</span><span class="sxs-lookup"><span data-stu-id="e388e-146">The release notes only show up when viewing _Updates_ for a package, so it doesn't make sense to add them to your first release.</span></span>

![Anmerkungen zu dieser Version in der Registerkarte "Updates"](./media/manage-nuget-packages-release-notes.png)

<span data-ttu-id="e388e-148">Um die Anmerkungen zu dieser Version eines Pakets hinzugefügt haben, verwenden Sie die neue `<releaseNotes />` Metadata-Element in der NuSpec-Datei.</span><span class="sxs-lookup"><span data-stu-id="e388e-148">To add release notes to a package, use the new `<releaseNotes />` metadata element in your NuSpec file.</span></span>

### <a name="nuspec-ltfiles-gt-improvement"></a><span data-ttu-id="e388e-149">NuSpec & Ltfiles /&gt; zur Verbesserung der</span><span class="sxs-lookup"><span data-stu-id="e388e-149">.nuspec &ltfiles /&gt; improvement</span></span>
<span data-ttu-id="e388e-150">Die `.nuspec` -Datei können nun leere `<files />` -Element, das weist nuget.exe nicht auf eine beliebige Datei im Paket enthalten.</span><span class="sxs-lookup"><span data-stu-id="e388e-150">The `.nuspec` file now allows empty `<files />` element, which tells nuget.exe not to include any file in the package.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="e388e-151">Fehlerkorrekturen</span><span class="sxs-lookup"><span data-stu-id="e388e-151">Bug Fixes</span></span>
<span data-ttu-id="e388e-152">NuGet 1.5 mussten insgesamt 107 Arbeitsaufgaben behoben.</span><span class="sxs-lookup"><span data-stu-id="e388e-152">NuGet 1.5 had a total of 107 work items fixed.</span></span> <span data-ttu-id="e388e-153">103 davon waren als Fehler gekennzeichnet.</span><span class="sxs-lookup"><span data-stu-id="e388e-153">103 of those were marked as bugs.</span></span>

<span data-ttu-id="e388e-154">Eine vollständige Liste der Arbeit Elemente eine feste in NuGet 1.5, bitte Ansicht der [NuGet Issue Tracker für diese Version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="e388e-154">For a full list of work items fixed in NuGet 1.5, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="e388e-155">Fehlerbehebungen zu beachten:</span><span class="sxs-lookup"><span data-stu-id="e388e-155">Bug fixes worth noting:</span></span>

* <span data-ttu-id="e388e-156">[Problem 1273](http://nuget.codeplex.com/workitem/1273): vorgenommen `packages.config` Weitere Versionskontrolle benutzerfreundliche durch Pakete alphabetisch zu sortieren und Entfernen von zusätzlichen Leerzeichen.</span><span class="sxs-lookup"><span data-stu-id="e388e-156">[Issue 1273](http://nuget.codeplex.com/workitem/1273): Made `packages.config` more version control friendly by sorting packages alphabetically and removing extra whitespace.</span></span>
* <span data-ttu-id="e388e-157">[Problem 844](http://nuget.codeplex.com/workitem/844): Versionsnummern werden jetzt normalisiert, damit `Install-Package 1.0` funktioniert für ein Paket mit der Version `1.0.0`.</span><span class="sxs-lookup"><span data-stu-id="e388e-157">[Issue 844](http://nuget.codeplex.com/workitem/844): Version numbers are now normalized so that `Install-Package 1.0` works on a package with the version `1.0.0`.</span></span>
* <span data-ttu-id="e388e-158">[Problem 1060](http://nuget.codeplex.com/workitem/1060): beim Erstellen eines Pakets mithilfe von nuget.exe, die `-Version` flag Außerkraftsetzungen der `<version />` Element.</span><span class="sxs-lookup"><span data-stu-id="e388e-158">[Issue 1060](http://nuget.codeplex.com/workitem/1060): When creating a package using nuget.exe, the `-Version` flag overrides the `<version />` element.</span></span>
