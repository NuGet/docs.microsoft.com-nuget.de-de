---
title: Anmerkungen zu NuGet-Version 2.0
description: Anmerkungen zu NuGet 2.0, einschließlich der bekannten Probleme, Fehlerkorrekturen, hinzugefügter Features und DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: f32eea9260ce7e307ff56b7f3e6b48c6d98e6c90
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547574"
---
# <a name="nuget-20-release-notes"></a><span data-ttu-id="cc84f-103">Anmerkungen zu NuGet-Version 2.0</span><span class="sxs-lookup"><span data-stu-id="cc84f-103">NuGet 2.0 Release Notes</span></span>

<span data-ttu-id="cc84f-104">[Anmerkungen zu NuGet 1.8](../release-notes/nuget-1.8.md) | [Anmerkungen zu NuGet 2.1](../release-notes/nuget-2.1.md)</span><span class="sxs-lookup"><span data-stu-id="cc84f-104">[NuGet 1.8 Release Notes](../release-notes/nuget-1.8.md) | [NuGet 2.1 Release Notes](../release-notes/nuget-2.1.md)</span></span>

<span data-ttu-id="cc84f-105">NuGet 2.0 wurde am 19. Juni 2012 veröffentlicht.</span><span class="sxs-lookup"><span data-stu-id="cc84f-105">NuGet 2.0 was released on June 19, 2012.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="cc84f-106">Problem für bekannte Installationsprobleme</span><span class="sxs-lookup"><span data-stu-id="cc84f-106">Known Installation Issue</span></span>
<span data-ttu-id="cc84f-107">Wenn Sie Visual Studio 2010 SP1 ausführen, können Sie ein Installationsfehler auftreten, beim Versuch, NuGet aktualisieren, wenn Sie eine ältere Version installiert haben.</span><span class="sxs-lookup"><span data-stu-id="cc84f-107">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="cc84f-108">Die problemumgehung besteht darin, einfach NuGet zuerst deinstallieren und installieren Sie es aus dem Katalog der VS-Erweiterung.</span><span class="sxs-lookup"><span data-stu-id="cc84f-108">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="cc84f-109">Finden Sie unter [ http://support.microsoft.com/kb/2581019 ](http://support.microsoft.com/kb/2581019) Informationen oder [gehen Sie direkt auf den VS-Hotfix](http://bit.ly/vsixcertfix).</span><span class="sxs-lookup"><span data-stu-id="cc84f-109">See [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) for more information, or [go directly to the VS hotfix](http://bit.ly/vsixcertfix).</span></span>

<span data-ttu-id="cc84f-110">Hinweis: Wenn Visual Studio ist es nicht zulässig, die die Erweiterung deinstallieren (die Schaltfläche "Deinstallieren" deaktiviert ist), müssen Sie wahrscheinlich zum Neustart von Visual Studio mithilfe von "Ausführen als Administrator."</span><span class="sxs-lookup"><span data-stu-id="cc84f-110">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="package-restore-consent-is-now-active"></a><span data-ttu-id="cc84f-111">Paket wiederherstellen Zustimmung ist jetzt aktiv</span><span class="sxs-lookup"><span data-stu-id="cc84f-111">Package restore consent is now active</span></span>

<span data-ttu-id="cc84f-112">Gemäß diesem [Beitrag im Paket wiederherstellen Zustimmung](http://blog.nuget.org/20120518/package-restore-and-consent.html), NuGet 2.0 jetzt erfordert, dass die Genehmigung zum Aktivieren der paketwiederherstellung online zu gehen und Herunterladen von Paketen erteilt werden.</span><span class="sxs-lookup"><span data-stu-id="cc84f-112">As described in this [post on package restore consent](http://blog.nuget.org/20120518/package-restore-and-consent.html), NuGet 2.0 will now require that consent be given to enable package restore to go online and download packages.</span></span> <span data-ttu-id="cc84f-113">Stellen Sie sicher, dass Sie die Zustimmung über das Konfigurationsdialogfeld des Paket-Manager oder die Umgebungsvariable EnableNuGetPackageRestore angegeben haben.</span><span class="sxs-lookup"><span data-stu-id="cc84f-113">Please ensure that you have provided consent via either the package manager configuration dialog or the EnableNuGetPackageRestore environment variable.</span></span>

## <a name="group-dependencies-by-target-frameworks"></a><span data-ttu-id="cc84f-114">Abhängigkeiten von Zielframeworks</span><span class="sxs-lookup"><span data-stu-id="cc84f-114">Group dependencies by target frameworks</span></span>

<span data-ttu-id="cc84f-115">Ab Version 2.0, auf der Grundlage Paket variieren können Abhängigkeiten des frameworkprofils des Zielprojekts.</span><span class="sxs-lookup"><span data-stu-id="cc84f-115">Starting with version 2.0, package dependencies can vary based on the framework profile of the target project.</span></span> <span data-ttu-id="cc84f-116">Dies erfolgt mithilfe eines aktualisierten `.nuspec` Schema.</span><span class="sxs-lookup"><span data-stu-id="cc84f-116">This is accomplished using an updated `.nuspec` schema.</span></span> <span data-ttu-id="cc84f-117">Die `<dependencies>` Element kann jetzt enthalten eine Reihe von `<group>` Elemente.</span><span class="sxs-lookup"><span data-stu-id="cc84f-117">The `<dependencies>` element can now contain a set of `<group>` elements.</span></span> <span data-ttu-id="cc84f-118">Jede Gruppe enthält 0 (null) oder mehr `<dependency>` Elemente und ein `targetFramework` Attribut.</span><span class="sxs-lookup"><span data-stu-id="cc84f-118">Each group contains zero or more `<dependency>` elements and a `targetFramework` attribute.</span></span> <span data-ttu-id="cc84f-119">Alle Abhängigkeiten in einer Gruppe werden zusammen installiert, wenn das Zielframework mit das Zielframeworkprofil im Projekt kompatibel ist.</span><span class="sxs-lookup"><span data-stu-id="cc84f-119">All dependencies inside a group are installed together if the target framework is compatible with the target project framework profile.</span></span> <span data-ttu-id="cc84f-120">Zum Beispiel:</span><span class="sxs-lookup"><span data-stu-id="cc84f-120">For example:</span></span>

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

<span data-ttu-id="cc84f-121">Beachten Sie, die eine Gruppe enthalten, können **0 (null)** Abhängigkeiten.</span><span class="sxs-lookup"><span data-stu-id="cc84f-121">Note that a group can contain **zero** dependencies.</span></span> <span data-ttu-id="cc84f-122">Im obigen Beispiel wenn das Paket ist in einem Projekt, Silverlight 3.0 oder höher installiert, werden keine Abhängigkeiten installiert.</span><span class="sxs-lookup"><span data-stu-id="cc84f-122">In the example above, if the package is installed into a project that targets Silverlight 3.0 or later, no dependencies will be installed.</span></span> <span data-ttu-id="cc84f-123">Wenn das Paket ist in einem Projekt, .NET 4.0 oder höher ausgeführt werden, werden zwei Abhängigkeiten, jQuery und WebActivator, installiert werden.</span><span class="sxs-lookup"><span data-stu-id="cc84f-123">If the package is installed into a project that targets .NET 4.0 or later, two dependencies, jQuery and WebActivator, will be installed.</span></span>  <span data-ttu-id="cc84f-124">Wenn das Paket in einem Projekt, die auf eine frühe Version dieser 2 Frameworks oder ein anderes Framework abzielt installiert wird, wird die RouteMagic 1.1.0 installiert werden.</span><span class="sxs-lookup"><span data-stu-id="cc84f-124">If the package is installed into a project that targets an early version of these 2 frameworks, or any other framework, RouteMagic 1.1.0 will be installed.</span></span> <span data-ttu-id="cc84f-125">Es gibt keine Vererbung zwischen Gruppen ein.</span><span class="sxs-lookup"><span data-stu-id="cc84f-125">There is no inheritance between groups.</span></span> <span data-ttu-id="cc84f-126">Wenn das Zielframework des Projekts entspricht der `targetFramework` Attributs einer Gruppe, die nur die Abhängigkeiten in dieser Gruppe installiert werden.</span><span class="sxs-lookup"><span data-stu-id="cc84f-126">If a project's target framework matches the `targetFramework` attribute of a group, only the dependencies within that group will be installed.</span></span>

<span data-ttu-id="cc84f-127">Ein Paket kann paketabhängigkeiten in einem der zwei Formate angeben: das alte Format von einer flachen Liste von `<dependency>` Elemente oder Gruppen.</span><span class="sxs-lookup"><span data-stu-id="cc84f-127">A package can specify package dependencies in either of two formats: the old format of a flat list of `<dependency>` elements, or groups.</span></span> <span data-ttu-id="cc84f-128">Wenn die `<group>` Format wird verwendet, das Paket kann nicht in Versionen vor Version 2.0 von NuGet installiert werden.</span><span class="sxs-lookup"><span data-stu-id="cc84f-128">If the `<group>` format is used, the package cannot be installed into versions of NuGet earlier than 2.0.</span></span>

<span data-ttu-id="cc84f-129">Beachten Sie, dass das Kombinieren von den beiden Formaten nicht zulässig ist.</span><span class="sxs-lookup"><span data-stu-id="cc84f-129">Note that mixing the two formats is not allowed.</span></span> <span data-ttu-id="cc84f-130">Der folgende Codeausschnitt ist z. B. **ungültige** und werden von NuGet abgelehnt.</span><span class="sxs-lookup"><span data-stu-id="cc84f-130">For example, the following snippet is **invalid** and will be rejected by NuGet.</span></span>

```xml
<dependencies>
    <dependency id="jQuery" />
    <dependency id="WebActivator" />

    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>
</dependencies>
```

## <a name="grouping-content-files-and-powershell-scripts-by-target-framework"></a><span data-ttu-id="cc84f-131">Gruppieren von Inhaltsdateien und PowerShell-Skripts nach Zielframework</span><span class="sxs-lookup"><span data-stu-id="cc84f-131">Grouping content files and PowerShell scripts by target framework</span></span>

<span data-ttu-id="cc84f-132">Neben der Assemblyverweise können Inhaltsdateien und PowerShell-Skripts auch nach Zielframework gruppiert werden.</span><span class="sxs-lookup"><span data-stu-id="cc84f-132">In addition to assembly references, content files and PowerShell scripts can also be grouped by target framework.</span></span> <span data-ttu-id="cc84f-133">Die gleiche Ordnerstruktur finden Sie in der `lib` Ordner zum Angeben von Zielframeworks kann jetzt auf die gleiche Weise zu angewendet werden die `content` und `tools` Ordner.</span><span class="sxs-lookup"><span data-stu-id="cc84f-133">The same folder structure found in the `lib` folder for specifying target framework can  now be applied in the same way to the `content` and `tools` folders.</span></span> <span data-ttu-id="cc84f-134">Zum Beispiel:</span><span class="sxs-lookup"><span data-stu-id="cc84f-134">For example:</span></span>

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

<span data-ttu-id="cc84f-135">**Beachten Sie**: Da `init.ps1` auf Projektmappenebene ausgeführt wird und ist nicht in einem einzelnen Projekt abhängig, es muss platziert werden direkt unter der `tools` Ordner.</span><span class="sxs-lookup"><span data-stu-id="cc84f-135">**Note**: Because `init.ps1` is executed at the solution level and is not dependent on any individual project, it must be placed directly under the `tools` folder.</span></span> <span data-ttu-id="cc84f-136">Wenn in einem Framework-spezifischen Ordner platzieren, wird es ignoriert.</span><span class="sxs-lookup"><span data-stu-id="cc84f-136">If placed within a framework-specific folder, it will be ignored.</span></span>

<span data-ttu-id="cc84f-137">Ein neues Feature in NuGet 2.0 ist außerdem ein frameworkordner möglich *leere*, in diesem Fall NuGet wird nicht Assemblyverweise hinzufügen, Inhaltsdateien, oder führen Sie PowerShell-Skripts für die bestimmte Framework-Version.</span><span class="sxs-lookup"><span data-stu-id="cc84f-137">Also, a new feature in NuGet 2.0 is that a framework folder can be *empty*, in which case, NuGet will not add assembly references, add content files or run  PowerShell scripts for the particular framework version.</span></span> <span data-ttu-id="cc84f-138">Im obigen Beispiel ist der Ordner `content\net40` ist leer.</span><span class="sxs-lookup"><span data-stu-id="cc84f-138">In the example above, the folder `content\net40` is empty.</span></span>

## <a name="improved-tab-completion-performance"></a><span data-ttu-id="cc84f-139">Verbesserte Registerkarte-Abschluss-Leistung</span><span class="sxs-lookup"><span data-stu-id="cc84f-139">Improved tab completion performance</span></span>
<span data-ttu-id="cc84f-140">Das Feature in der NuGet-Paket-Manager-Konsole wurde aktualisiert, um die Leistung erheblich verbessern.</span><span class="sxs-lookup"><span data-stu-id="cc84f-140">The tab completion feature in the NuGet Package Manager Console has been updated to significantly improve performance.</span></span> <span data-ttu-id="cc84f-141">Es fallen weniger Verzögerung, die die Tab-Taste gedrückt wird, bis die Vorschlags-Dropdownliste angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="cc84f-141">There will be much less delay from the time the tab key is pressed until the suggestion dropdown appears.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="cc84f-142">Fehlerkorrekturen</span><span class="sxs-lookup"><span data-stu-id="cc84f-142">Bug Fixes</span></span>
<span data-ttu-id="cc84f-143">NuGet 2.0 enthält zahlreiche Programmfehlerbehebungen mit Schwerpunkt auf das Paket wiederherstellen Zustimmung und Leistung.</span><span class="sxs-lookup"><span data-stu-id="cc84f-143">NuGet 2.0 includes many bug fixes with an emphasis on package restore consent and performance.</span></span>
<span data-ttu-id="cc84f-144">Eine vollständige Liste der Arbeit Elemente eine feste in NuGet 2.0 Bitte Ansicht der [NuGet Issue Tracker für diese Version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="cc84f-144">For a full list of work items fixed in NuGet 2.0, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
