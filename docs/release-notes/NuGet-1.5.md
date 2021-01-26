---
title: Anmerkungen zu dieser Version von nuget 1,5
description: Anmerkungen zu dieser Version von nuget 1,5 einschließlich bekannter Probleme, Fehlerbehebungen, hinzugefügter Features und dcrs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: c9946f3d8cf545ec14f842c40105743c231b4b72
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777088"
---
# <a name="nuget-15-release-notes"></a><span data-ttu-id="fe767-103">Anmerkungen zu dieser Version von nuget 1,5</span><span class="sxs-lookup"><span data-stu-id="fe767-103">NuGet 1.5 Release Notes</span></span>

<span data-ttu-id="fe767-104">Anmerkungen zu dieser [Version von nuget 1,4](../release-notes/nuget-1.4.md)  |  [Anmerkungen zu dieser Version von nuget 1,6](../release-notes/nuget-1.6.md)</span><span class="sxs-lookup"><span data-stu-id="fe767-104">[NuGet 1.4 Release Notes](../release-notes/nuget-1.4.md) | [NuGet 1.6 Release Notes](../release-notes/nuget-1.6.md)</span></span>

<span data-ttu-id="fe767-105">Nuget 1,5 wurde am 30. August 2011 veröffentlicht.</span><span class="sxs-lookup"><span data-stu-id="fe767-105">NuGet 1.5 was released on August 30, 2011.</span></span>

## <a name="features"></a><span data-ttu-id="fe767-106">Features</span><span class="sxs-lookup"><span data-stu-id="fe767-106">Features</span></span>

### <a name="project-templates-with-preinstalled-nuget-packages"></a><span data-ttu-id="fe767-107">Projektvorlagen mit vorinstallierten nuget-Paketen</span><span class="sxs-lookup"><span data-stu-id="fe767-107">Project Templates with Preinstalled NuGet Packages</span></span>
<span data-ttu-id="fe767-108">Beim Erstellen einer neuen ASP.NET MVC 3-Projektvorlage werden die im Projekt enthaltenen jQuery-Skript Bibliotheken tatsächlich durch die Installation von nuget-Paketen platziert.</span><span class="sxs-lookup"><span data-stu-id="fe767-108">When creating a new ASP.NET MVC 3 project template, the jQuery script libraries included in the project are actually placed there by installing NuGet packages.</span></span>

<span data-ttu-id="fe767-109">Die ASP.NET MVC 3-Projektvorlage enthält einen Satz von nuget-Paketen, die installiert werden, wenn die Projektvorlage aufgerufen wird.</span><span class="sxs-lookup"><span data-stu-id="fe767-109">The ASP.NET MVC 3 project template includes a set of NuGet packages that get installed when the project template is invoked.</span></span> <span data-ttu-id="fe767-110">Diese Möglichkeit, nuget-Pakete mit einer Projektvorlage aufzunehmen, ist jetzt eine Funktion von nuget, die _alle_ Projektvorlagen jetzt nutzen können.</span><span class="sxs-lookup"><span data-stu-id="fe767-110">This ability to include NuGet packages with a project template is now a feature of NuGet that _any_ project template can now take advantage of.</span></span>

<span data-ttu-id="fe767-111">Weitere Informationen zu diesem Feature finden Sie in diesem [Blogbeitrag vom Entwickler des Features](https://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx).</span><span class="sxs-lookup"><span data-stu-id="fe767-111">For more details about this feature, read this [blog post by the developer of the feature](https://blogs.msdn.com/b/marcinon/archive/2011/07/08/project-templates-and-preinstalled-nuget-packages.aspx).</span></span>

### <a name="explicit-assembly-references"></a><span data-ttu-id="fe767-112">Explizite Assemblyverweise</span><span class="sxs-lookup"><span data-stu-id="fe767-112">Explicit Assembly References</span></span>

<span data-ttu-id="fe767-113">Es wurde ein neues Element hinzugefügt `<references />` , mit dem explizit angegeben wird, auf welche Assemblys im Paket verwiesen werden soll.</span><span class="sxs-lookup"><span data-stu-id="fe767-113">Added a new `<references />` element used to explicitly specify which assemblies within the the package should be referenced.</span></span>

<span data-ttu-id="fe767-114">Wenn Sie z. b. Folgendes hinzufügen:</span><span class="sxs-lookup"><span data-stu-id="fe767-114">For example, if you add the following:</span></span>

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

<span data-ttu-id="fe767-115">`xunit.dll`Auf und wird nur `xunit.extensions.dll` aus dem entsprechenden [Framework/Profil-Unterordner](../reference/nuspec.md#explicit-assembly-references) des `lib` Ordners verwiesen, auch wenn im Ordner weitere Assemblys vorhanden sind.</span><span class="sxs-lookup"><span data-stu-id="fe767-115">Then only the `xunit.dll` and `xunit.extensions.dll` will be referenced from the appropriate [framework/profile subfolder](../reference/nuspec.md#explicit-assembly-references) of the `lib` folder even if there are other assemblies in the folder.</span></span>

<span data-ttu-id="fe767-116">Wenn dieses Element weggelassen wird, gilt das übliche Verhalten, das auf jede Assembly im `lib` Ordner verweist.</span><span class="sxs-lookup"><span data-stu-id="fe767-116">If this element is omitted, then the usual behavior applies, which is to reference every assembly in the `lib` folder.</span></span>

<span data-ttu-id="fe767-117">__Wofür wird dieses Feature verwendet?__</span><span class="sxs-lookup"><span data-stu-id="fe767-117">__What is this feature used for?__</span></span>

<span data-ttu-id="fe767-118">Diese Funktion unterstützt nur-Assemblys zur Entwurfszeit.</span><span class="sxs-lookup"><span data-stu-id="fe767-118">This feature supports design-time only assemblies.</span></span> <span data-ttu-id="fe767-119">Wenn Sie z. b. Code Verträge verwenden, müssen sich die Vertragsassemblys neben den ausführungsassemblys befinden, die Sie erweitern, sodass Sie von Visual Studio gefunden werden können, aber die Vertragsassemblys sollten nicht tatsächlich vom Projekt referenziert werden und sollten nicht in den Ordner kopiert werden `bin` .</span><span class="sxs-lookup"><span data-stu-id="fe767-119">For example, when using Code Contracts, the contract assemblies need to be next to the runtime assemblies that they augment so that Visual Studio can find them, but the contract assemblies should not actually be referenced by the project and should not be copied into the `bin` folder.</span></span>

<span data-ttu-id="fe767-120">Ebenso kann die-Funktion für Komponenten Test-Frameworks wie xUnit verwendet werden, deren toolsassemblys sich neben den Laufzeitassemblys befinden, aber von Projekt verweisen ausgeschlossen werden.</span><span class="sxs-lookup"><span data-stu-id="fe767-120">Likewise, the feature can be used to for unit test frameworks such as XUnit which need its tools assemblies to be located next to the runtime assemblies, but excluded from project references.</span></span>

### <a name="added-ability-to-exclude-files-in-the-nuspec"></a><span data-ttu-id="fe767-121">Hinzugefügte Fähigkeit zum Ausschließen von Dateien in der. nuspec-Datei</span><span class="sxs-lookup"><span data-stu-id="fe767-121">Added ability to exclude files in the .nuspec</span></span>
<span data-ttu-id="fe767-122">Das- `<file>` Element in einer- `.nuspec` Datei kann verwendet werden, um eine bestimmte Datei oder einen Satz von Dateien mithilfe eines Platzhalters einzuschließen.</span><span class="sxs-lookup"><span data-stu-id="fe767-122">The `<file>` element within a `.nuspec` file can be used to include a specific file or a set of files using a wildcard.</span></span> <span data-ttu-id="fe767-123">Wenn Sie einen Platzhalter verwenden, besteht keine Möglichkeit, eine bestimmte Teilmenge der enthaltenen Dateien auszuschließen.</span><span class="sxs-lookup"><span data-stu-id="fe767-123">When using a wildcard, there's no way to exclude a specific subset of the included files.</span></span> <span data-ttu-id="fe767-124">Angenommen, Sie möchten alle Textdateien in einem Ordner außer einem bestimmten Ordner.</span><span class="sxs-lookup"><span data-stu-id="fe767-124">For example, suppose you want all text files within a folder except a specific one.</span></span>

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt" />
</files>
```

<span data-ttu-id="fe767-125">Verwenden Sie Semikolons, um mehrere Dateien anzugeben.</span><span class="sxs-lookup"><span data-stu-id="fe767-125">Use semicolons to specify multiple files.</span></span>

```xml
<files>
    <file src="*.txt" target="content\docs" exclude="admin.txt;log.txt" />
</files>
```

<span data-ttu-id="fe767-126">Oder verwenden Sie eine Platzhalter Karte, um eine Gruppe von Dateien auszuschließen, z. b. alle Sicherungsdateien.</span><span class="sxs-lookup"><span data-stu-id="fe767-126">Or use a wild card to exclude a set of files such as all backup files</span></span>

```xml
<files>
    <file src="tools\*.*" target="tools" exclude="*.bak" />
</files>
```

### <a name="removing-packages-using-the-dialog-prompts-to-remove-dependencies"></a><span data-ttu-id="fe767-127">Entfernen von Paketen mithilfe des Dialog Felds zum Entfernen von Abhängigkeiten</span><span class="sxs-lookup"><span data-stu-id="fe767-127">Removing packages using the dialog prompts to remove dependencies</span></span>
<span data-ttu-id="fe767-128">Wenn Sie ein Paket mit Abhängigkeiten deinstallieren, werden Sie von nuget aufgefordert, das Entfernen der Abhängigkeiten eines Pakets zusammen mit dem Paket zu ermöglichen.</span><span class="sxs-lookup"><span data-stu-id="fe767-128">When uninstalling a package with dependencies, NuGet prompts, allowing the removal of a package's dependencies along with the package.</span></span>

![Entfernen von abhängigen Paketen](./media/remove-dependent-packages.png)


### <a name="get-package-command-improvement"></a><span data-ttu-id="fe767-130">`Get-Package` Befehls Verbesserung</span><span class="sxs-lookup"><span data-stu-id="fe767-130">`Get-Package` command improvement</span></span>
<span data-ttu-id="fe767-131">Der- `Get-Package` Befehl unterstützt jetzt einen- `-ProjectName` Parameter.</span><span class="sxs-lookup"><span data-stu-id="fe767-131">The `Get-Package` command now supports a `-ProjectName` parameter.</span></span> <span data-ttu-id="fe767-132">Der Befehl</span><span class="sxs-lookup"><span data-stu-id="fe767-132">So the command</span></span>

```
Get-Package –ProjectName A
```

<span data-ttu-id="fe767-133">Listet alle Pakete auf, die in Project A installiert sind.</span><span class="sxs-lookup"><span data-stu-id="fe767-133">will list all packages installed in project A.</span></span>

### <a name="support-for-proxies-that-require-authentication"></a><span data-ttu-id="fe767-134">Unterstützung für Proxys, die Authentifizierung erfordern</span><span class="sxs-lookup"><span data-stu-id="fe767-134">Support for Proxies that require authentication</span></span>
<span data-ttu-id="fe767-135">Wenn Sie nuget hinter einem Proxy verwenden, der eine Authentifizierung erfordert, fordert nuget nun zur Eingabe von Proxy Anmelde Informationen auf.</span><span class="sxs-lookup"><span data-stu-id="fe767-135">When using NuGet behind a proxy that requires authentication, NuGet will now prompt for proxy credentials.</span></span> <span data-ttu-id="fe767-136">Durch Eingeben von Anmelde Informationen kann nuget eine Verbindung mit dem Remoterepository herstellen</span><span class="sxs-lookup"><span data-stu-id="fe767-136">Entering credentials allows NuGet to connect to the remote repository.</span></span>

### <a name="support-for-repositories-that-require-authentication"></a><span data-ttu-id="fe767-137">Unterstützung für Depots, die eine Authentifizierung erfordern</span><span class="sxs-lookup"><span data-stu-id="fe767-137">Support for Repositories that require authentication</span></span>
<span data-ttu-id="fe767-138">Nuget unterstützt jetzt das Herstellen einer Verbindung mit [privaten Depots](../hosting-packages/local-feeds.md) , die eine Basic-oder NTLM-Authentifizierung erfordern</span><span class="sxs-lookup"><span data-stu-id="fe767-138">NuGet now supports connecting to [private repositories](../hosting-packages/local-feeds.md) that require basic or NTLM authentication.</span></span>

<span data-ttu-id="fe767-139">Die Unterstützung für die Digest-Authentifizierung wird in einer zukünftigen Version hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="fe767-139">Support for Digest authentication will be added in a future release.</span></span>

### <a name="performance-improvements-to-the-nugetorg-repository"></a><span data-ttu-id="fe767-140">Leistungsverbesserungen für das nuget.org-Repository</span><span class="sxs-lookup"><span data-stu-id="fe767-140">Performance improvements to the nuget.org repository</span></span>
<span data-ttu-id="fe767-141">Wir haben eine Reihe von Leistungsverbesserungen an der nuget.org Gallery vorgenommen, um die Paket Auflistung zu beschleunigen und schneller zu suchen.</span><span class="sxs-lookup"><span data-stu-id="fe767-141">We've made several performance improvements to the nuget.org gallery to make package listing and searching faster.</span></span>

### <a name="solution-dialog-project-filtering"></a><span data-ttu-id="fe767-142">Projekt Filterung für Projekt Mappe</span><span class="sxs-lookup"><span data-stu-id="fe767-142">Solution dialog project filtering</span></span>
<span data-ttu-id="fe767-143">Wenn Sie im Dialogfeld auf Projektmappenebene aufgefordert werden, die zu installierenden Projekte anzugeben, werden nur Projekte angezeigt, die mit dem ausgewählten Paket kompatibel sind.</span><span class="sxs-lookup"><span data-stu-id="fe767-143">In the Solution-level dialog, when prompting for what projects to install, we only show projects that are compatible with the selected package.</span></span>

### <a name="package-release-notes"></a><span data-ttu-id="fe767-144">Anmerkungen zu dieser Paketversion</span><span class="sxs-lookup"><span data-stu-id="fe767-144">Package Release Notes</span></span>
<span data-ttu-id="fe767-145">Nuget-Pakete enthalten jetzt Unterstützung für Versions Anmerkungen.</span><span class="sxs-lookup"><span data-stu-id="fe767-145">NuGet packages now include support for release notes.</span></span> <span data-ttu-id="fe767-146">Die Anmerkungen zu dieser Version werden nur angezeigt, wenn Sie _Updates_ für ein Paket anzeigen, daher ist es nicht sinnvoll, Sie Ihrer ersten Version hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="fe767-146">The release notes only show up when viewing _Updates_ for a package, so it doesn't make sense to add them to your first release.</span></span>

![Anmerkungen zur Version auf der Registerkarte "Updates"](./media/manage-nuget-packages-release-notes.png)

<span data-ttu-id="fe767-148">Verwenden Sie zum Hinzufügen von Versions Anmerkungen zu einem Paket das neue `<releaseNotes />` Metadata-Element in der nuspec-Datei.</span><span class="sxs-lookup"><span data-stu-id="fe767-148">To add release notes to a package, use the new `<releaseNotes />` metadata element in your NuSpec file.</span></span>

### <a name="nuspec-ltfiles-gt-improvement"></a><span data-ttu-id="fe767-149">. nuspec &ltfiles/ &gt; Improvement</span><span class="sxs-lookup"><span data-stu-id="fe767-149">.nuspec &ltfiles /&gt; improvement</span></span>
<span data-ttu-id="fe767-150">Die `.nuspec` Datei lässt jetzt ein leeres- `<files />` Element zu, das anweist, nuget.exe keine Datei in das Paket aufzunehmen.</span><span class="sxs-lookup"><span data-stu-id="fe767-150">The `.nuspec` file now allows empty `<files />` element, which tells nuget.exe not to include any file in the package.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="fe767-151">Fehlerkorrekturen</span><span class="sxs-lookup"><span data-stu-id="fe767-151">Bug Fixes</span></span>
<span data-ttu-id="fe767-152">Für nuget 1,5 wurden insgesamt 107 Arbeitselemente korrigiert.</span><span class="sxs-lookup"><span data-stu-id="fe767-152">NuGet 1.5 had a total of 107 work items fixed.</span></span> <span data-ttu-id="fe767-153">103 von diesen wurden als Fehler gekennzeichnet.</span><span class="sxs-lookup"><span data-stu-id="fe767-153">103 of those were marked as bugs.</span></span>

<span data-ttu-id="fe767-154">Eine vollständige Liste der Arbeitselemente, die in nuget 1,5 behoben wurden, finden Sie in der [nuget-Problemverfolgung für diese Version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="fe767-154">For a full list of work items fixed in NuGet 1.5, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.5&assignedTo=All&component=All&sortField=Summary&sortDirection=Descending&page=0).</span></span>

## <a name="bug-fixes-worth-noting"></a><span data-ttu-id="fe767-155">Fehlerbehebungen beachten Sie Folgendes:</span><span class="sxs-lookup"><span data-stu-id="fe767-155">Bug fixes worth noting:</span></span>

* <span data-ttu-id="fe767-156">[Problem 1273](http://nuget.codeplex.com/workitem/1273): Sie haben `packages.config` eine bessere Versionskontrolle erzielt, indem Sie Pakete alphabetisch sortieren und zusätzliche Leerzeichen entfernen.</span><span class="sxs-lookup"><span data-stu-id="fe767-156">[Issue 1273](http://nuget.codeplex.com/workitem/1273): Made `packages.config` more version control friendly by sorting packages alphabetically and removing extra whitespace.</span></span>
* <span data-ttu-id="fe767-157">[Problem 844](http://nuget.codeplex.com/workitem/844): Versionsnummern werden jetzt normalisiert, sodass Sie `Install-Package 1.0` für ein Paket mit der-Version verwendet werden können `1.0.0` .</span><span class="sxs-lookup"><span data-stu-id="fe767-157">[Issue 844](http://nuget.codeplex.com/workitem/844): Version numbers are now normalized so that `Install-Package 1.0` works on a package with the version `1.0.0`.</span></span>
* <span data-ttu-id="fe767-158">[Problem 1060](http://nuget.codeplex.com/workitem/1060): Wenn Sie ein Paket mit nuget.exe erstellen, `-Version` überschreibt das Flag das- `<version />` Element.</span><span class="sxs-lookup"><span data-stu-id="fe767-158">[Issue 1060](http://nuget.codeplex.com/workitem/1060): When creating a package using nuget.exe, the `-Version` flag overrides the `<version />` element.</span></span>
