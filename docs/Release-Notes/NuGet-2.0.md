---
title: NuGet 2.0-Versionshinweise | Microsoft Docs
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Versionshinweise für NuGet 2.0 bekannte Probleme, Fehlerbehebungen, Funktionen und Archivierung von dcrs Design einschließlich."
keywords: "NuGet 2.0 Anmerkungen zu dieser Version, aufgrund von Fehlerbehebungen, bekannte Probleme, zusätzliche Funktionen, Archivierung von dcrs Design"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: eaa3c8db1cce72ff93671a1df63698748cdfab70
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-20-release-notes"></a><span data-ttu-id="2f0f5-104">NuGet 2.0-Versionshinweise</span><span class="sxs-lookup"><span data-stu-id="2f0f5-104">NuGet 2.0 Release Notes</span></span>

<span data-ttu-id="2f0f5-105">[Anmerkungen zur Version des NuGet-1.8](../release-notes/nuget-1.8.md) | [NuGet 2.1-Versionshinweise](../release-notes/nuget-2.1.md)</span><span class="sxs-lookup"><span data-stu-id="2f0f5-105">[NuGet 1.8 Release Notes](../release-notes/nuget-1.8.md) | [NuGet 2.1 Release Notes](../release-notes/nuget-2.1.md)</span></span>

<span data-ttu-id="2f0f5-106">NuGet 2.0 wurde 19 Juni 2012 veröffentlicht.</span><span class="sxs-lookup"><span data-stu-id="2f0f5-106">NuGet 2.0 was released on June 19, 2012.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="2f0f5-107">Bekannte Problem</span><span class="sxs-lookup"><span data-stu-id="2f0f5-107">Known Installation Issue</span></span>
<span data-ttu-id="2f0f5-108">Wenn Sie Visual Studio 2010 SP1 ausführen, kann ein Installationsfehler auftreten beim Upgrade von NuGet ausführen, wenn Sie eine ältere Version installiert haben.</span><span class="sxs-lookup"><span data-stu-id="2f0f5-108">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="2f0f5-109">Die problemumgehung besteht darin, einfach NuGet deinstallieren und installieren Sie es aus dem Katalog der VS-Erweiterung.</span><span class="sxs-lookup"><span data-stu-id="2f0f5-109">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="2f0f5-110">Finden Sie unter [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) für Weitere Informationen oder [fahren Sie direkt mit den VS-Hotfix](http://bit.ly/vsixcertfix).</span><span class="sxs-lookup"><span data-stu-id="2f0f5-110">See [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) for more information, or [go directly to the VS hotfix](http://bit.ly/vsixcertfix).</span></span>

<span data-ttu-id="2f0f5-111">Hinweis: Wenn Visual Studio lässt Sie beim Deinstallieren der Erweiterung (die Schaltfläche "Deinstallieren" deaktiviert ist), müssen Sie wahrscheinlich zum Neustart von Visual Studio, die mit "Als Administrator ausführen".</span><span class="sxs-lookup"><span data-stu-id="2f0f5-111">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="package-restore-consent-is-now-active"></a><span data-ttu-id="2f0f5-112">Paket Wiederherstellung Zustimmung ist jetzt aktiv</span><span class="sxs-lookup"><span data-stu-id="2f0f5-112">Package restore consent is now active</span></span>

<span data-ttu-id="2f0f5-113">Wie dies unter [Beitrag im Blog Paket Wiederherstellung Zustimmung](http://blog.nuget.org/20120518/package-restore-and-consent.html), NuGet 2.0 erfordert nun, dass die Zustimmung erteilt werden, um paketwiederherstellung online zu gehen und Herunterladen von Paketen zu aktivieren.</span><span class="sxs-lookup"><span data-stu-id="2f0f5-113">As described in this [post on package restore consent](http://blog.nuget.org/20120518/package-restore-and-consent.html), NuGet 2.0 will now require that consent be given to enable package restore to go online and download packages.</span></span> <span data-ttu-id="2f0f5-114">Stellen Sie sicher, dass Sie die Zustimmung über das Dialogfeld "Konfiguration" die Paket-Manager oder die Umgebungsvariable EnableNuGetPackageRestore eingegeben haben.</span><span class="sxs-lookup"><span data-stu-id="2f0f5-114">Please ensure that you have provided consent via either the package manager configuration dialog or the EnableNuGetPackageRestore environment variable.</span></span>

## <a name="group-dependencies-by-target-frameworks"></a><span data-ttu-id="2f0f5-115">Abhängigkeiten von Aufgabengruppen von Zielframeworks</span><span class="sxs-lookup"><span data-stu-id="2f0f5-115">Group dependencies by target frameworks</span></span>

<span data-ttu-id="2f0f5-116">Ab Version 2.0, auf der Grundlage Paket Abhängigkeiten variieren können des Framework-Profils für das Zielprojekt.</span><span class="sxs-lookup"><span data-stu-id="2f0f5-116">Starting with version 2.0, package dependencies can vary based on the framework profile of the target project.</span></span> <span data-ttu-id="2f0f5-117">Dies erfolgt über ein aktualisiertes `.nuspec` Schema.</span><span class="sxs-lookup"><span data-stu-id="2f0f5-117">This is accomplished using an updated `.nuspec` schema.</span></span> <span data-ttu-id="2f0f5-118">Die `<dependencies>` Element kann jetzt enthalten eine Reihe von `<group>` Elemente.</span><span class="sxs-lookup"><span data-stu-id="2f0f5-118">The `<dependencies>` element can now contain a set of `<group>` elements.</span></span> <span data-ttu-id="2f0f5-119">Jede Gruppe enthält 0 (null) oder mehr `<dependency>` Elemente und ein `targetFramework` Attribut.</span><span class="sxs-lookup"><span data-stu-id="2f0f5-119">Each group contains zero or more `<dependency>` elements and a `targetFramework` attribute.</span></span> <span data-ttu-id="2f0f5-120">Alle Abhängigkeiten in einer Gruppe werden zusammen installiert, wenn das Zielframework mit dem Profil des Zielframeworks Projekt kompatibel ist.</span><span class="sxs-lookup"><span data-stu-id="2f0f5-120">All dependencies inside a group are installed together if the target framework is compatible with the target project framework profile.</span></span> <span data-ttu-id="2f0f5-121">Zum Beispiel:</span><span class="sxs-lookup"><span data-stu-id="2f0f5-121">For example:</span></span>

```xml
<dependencies>
    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>

    <group targetFramework="net40">
        <dependency id="jQuery" />
        <dependency id="WebActivator" />
    </group>

    <group targetFramework="sl30">
    </group>
</dependencies>
```

<span data-ttu-id="2f0f5-122">Beachten Sie, die eine Gruppe enthalten kann **0 (null)** Abhängigkeiten.</span><span class="sxs-lookup"><span data-stu-id="2f0f5-122">Note that a group can contain **zero** dependencies.</span></span> <span data-ttu-id="2f0f5-123">Im obigen Beispiel ist das Paket installiert werden in ein Projekt, die auf Silverlight 3.0 oder höher, werden keine Abhängigkeiten installiert werden.</span><span class="sxs-lookup"><span data-stu-id="2f0f5-123">In the example above, if the package is installed into a project that targets Silverlight 3.0 or later, no dependencies will be installed.</span></span> <span data-ttu-id="2f0f5-124">Wenn das Paket ist in ein Projekt, die auf .NET 4.0 oder höher ausgeführt werden, werden zwei Abhängigkeiten, jQuery und WebActivator, installiert.</span><span class="sxs-lookup"><span data-stu-id="2f0f5-124">If the package is installed into a project that targets .NET 4.0 or later, two dependencies, jQuery and WebActivator, will be installed.</span></span>  <span data-ttu-id="2f0f5-125">Wenn das Paket in einem Projekt, die auf eine frühere Version des diese 2 Frameworks oder andere Frameworks abzielen installiert wird, wird RouteMagic 1.1.0 installiert.</span><span class="sxs-lookup"><span data-stu-id="2f0f5-125">If the package is installed into a project that targets an early version of these 2 frameworks, or any other framework, RouteMagic 1.1.0 will be installed.</span></span> <span data-ttu-id="2f0f5-126">Es gibt keine Vererbung zwischen Gruppen ein.</span><span class="sxs-lookup"><span data-stu-id="2f0f5-126">There is no inheritance between groups.</span></span> <span data-ttu-id="2f0f5-127">Wenn das Zielframework des Projekts entspricht der `targetFramework` Attribut einer Gruppe, die nur die Abhängigkeiten in dieser Gruppe installiert werden soll.</span><span class="sxs-lookup"><span data-stu-id="2f0f5-127">If a project's target framework matches the `targetFramework` attribute of a group, only the dependencies within that group will be installed.</span></span>

<span data-ttu-id="2f0f5-128">Ein Paket kann in zwei Formaten paketabhängigkeiten angeben: das alte Format von einer flachen Liste von `<dependency>` Elemente oder Gruppen.</span><span class="sxs-lookup"><span data-stu-id="2f0f5-128">A package can specify package dependencies in either of two formats: the old format of a flat list of `<dependency>` elements, or groups.</span></span> <span data-ttu-id="2f0f5-129">Wenn die `<group>` Format verwendet wird, das Paket kann nicht in Versionen vor Version 2.0 von NuGet installiert werden.</span><span class="sxs-lookup"><span data-stu-id="2f0f5-129">If the `<group>` format is used, the package cannot be installed into versions of NuGet earlier than 2.0.</span></span>

<span data-ttu-id="2f0f5-130">Beachten Sie, dass das Mischen von den beiden Formaten nicht zulässig ist.</span><span class="sxs-lookup"><span data-stu-id="2f0f5-130">Note that mixing the two formats is not allowed.</span></span> <span data-ttu-id="2f0f5-131">Der folgende Codeausschnitt ist z. B. **ungültige** und werden durch NuGet abgelehnt.</span><span class="sxs-lookup"><span data-stu-id="2f0f5-131">For example, the following snippet is **invalid** and will be rejected by NuGet.</span></span>

```xml
<dependencies>
    <dependency id="jQuery" />
    <dependency id="WebActivator" />

    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>
</dependencies>
```

## <a name="grouping-content-files-and-powershell-scripts-by-target-framework"></a><span data-ttu-id="2f0f5-132">Gruppieren von Inhaltsdateien und PowerShell-Skripts von Zielframework</span><span class="sxs-lookup"><span data-stu-id="2f0f5-132">Grouping content files and PowerShell scripts by target framework</span></span>

<span data-ttu-id="2f0f5-133">Zusätzlich zu den Assemblyverweise können Inhaltsdateien und PowerShell-Skripts auch nach Zielframework gruppiert werden.</span><span class="sxs-lookup"><span data-stu-id="2f0f5-133">In addition to assembly references, content files and PowerShell scripts can also be grouped by target framework.</span></span> <span data-ttu-id="2f0f5-134">Die gleiche Ordnerstruktur gefunden wird, der `lib` Ordner für die Angabe von Zielframework kann jetzt angewendet werden, auf die gleiche Weise auf die `content` und `tools` Ordner.</span><span class="sxs-lookup"><span data-stu-id="2f0f5-134">The same folder structure found in the `lib` folder for specifying target framework can  now be applied in the same way to the `content` and `tools` folders.</span></span> <span data-ttu-id="2f0f5-135">Zum Beispiel:</span><span class="sxs-lookup"><span data-stu-id="2f0f5-135">For example:</span></span>

    \content
        \net11
            \MyContent.txt
        \net20
            \MyContent20.txt
        \net40
        \sl40
            \MySilverlightContent.html

    \tools
        \init.ps1
        \net40
            \install.ps1
            \uninstall.ps1
        \sl40
            \install.ps1
            \uninstall.ps1

<span data-ttu-id="2f0f5-136">**Hinweis**: Da `init.ps1` auf Projektmappenebene ausgeführt wird und ist nicht auf einem einzelnen Projekt abhängige, muss sie verschoben werden direkt unter der `tools` Ordner.</span><span class="sxs-lookup"><span data-stu-id="2f0f5-136">**Note**: Because `init.ps1` is executed at the solution level and is not dependent on any individual project, it must be placed directly under the `tools` folder.</span></span> <span data-ttu-id="2f0f5-137">Wenn in einem frameworkspezifischen Ordner platziert werden, wird es ignoriert.</span><span class="sxs-lookup"><span data-stu-id="2f0f5-137">If placed within a framework-specific folder, it will be ignored.</span></span>

<span data-ttu-id="2f0f5-138">Darüber hinaus ein neues Feature in NuGet 2.0 hat es, dass einem frameworkordner *leere*, im letzteren Fall NuGet wird keine Assemblyverweise hinzufügen Inhaltsdateien oder Ausführen von PowerShell-Skripts für die bestimmten Framework-Version.</span><span class="sxs-lookup"><span data-stu-id="2f0f5-138">Also, a new feature in NuGet 2.0 is that a framework folder can be *empty*, in which case, NuGet will not add assembly references, add content files or run  PowerShell scripts for the particular framework version.</span></span> <span data-ttu-id="2f0f5-139">In der oben gezeigten Beispiel wird der Ordner `content\net40` ist leer.</span><span class="sxs-lookup"><span data-stu-id="2f0f5-139">In the example above, the folder `content\net40` is empty.</span></span>

## <a name="improved-tab-completion-performance"></a><span data-ttu-id="2f0f5-140">Verbesserte Registerkarte Abschluss Leistung</span><span class="sxs-lookup"><span data-stu-id="2f0f5-140">Improved tab completion performance</span></span>
<span data-ttu-id="2f0f5-141">Das Feature zum Vervollständigen Registerkarte in der NuGet-Paket-Manager-Konsole wurde aktualisiert, um die Leistung erheblich verbessern.</span><span class="sxs-lookup"><span data-stu-id="2f0f5-141">The tab completion feature in the NuGet Package Manager Console has been updated to significantly improve performance.</span></span> <span data-ttu-id="2f0f5-142">Es werden viel weniger Verzögerung ab dem Zeitpunkt, den die Tab-Taste gedrückt wird, bis die Vorschlag-Dropdownliste angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="2f0f5-142">There will be much less delay from the time the tab key is pressed until the suggestion dropdown appears.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="2f0f5-143">Fehlerkorrekturen</span><span class="sxs-lookup"><span data-stu-id="2f0f5-143">Bug Fixes</span></span>
<span data-ttu-id="2f0f5-144">NuGet 2.0 enthält zahlreiche Programmfehlerbehebungen mit Schwerpunkt auf das Paket wiederherstellen Benutzeroberfläche zur administratorzustimmung und Leistung.</span><span class="sxs-lookup"><span data-stu-id="2f0f5-144">NuGet 2.0 includes many bug fixes with an emphasis on package restore consent and performance.</span></span>
<span data-ttu-id="2f0f5-145">Eine vollständige Liste der Arbeit Artikel feste in NuGet 2.0 Bitte Ansicht der [NuGet Issue Tracker für diese Version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="2f0f5-145">For a full list of work items fixed in NuGet 2.0, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
