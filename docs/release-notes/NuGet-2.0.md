---
title: Anmerkungen zu dieser Version von nuget 2,0
description: Anmerkungen zu dieser Version von nuget 2,0 einschließlich bekannter Probleme, Fehlerbehebungen, hinzugefügter Features und dcrs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: b6874cbf0404f18ab7007bec1e0f66089c790d08
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776984"
---
# <a name="nuget-20-release-notes"></a><span data-ttu-id="6cec2-103">Anmerkungen zu dieser Version von nuget 2,0</span><span class="sxs-lookup"><span data-stu-id="6cec2-103">NuGet 2.0 Release Notes</span></span>

<span data-ttu-id="6cec2-104">Anmerkungen zu dieser [Version von nuget 1,8](../release-notes/nuget-1.8.md)  |  [Anmerkungen zu dieser Version von nuget 2,1](../release-notes/nuget-2.1.md)</span><span class="sxs-lookup"><span data-stu-id="6cec2-104">[NuGet 1.8 Release Notes](../release-notes/nuget-1.8.md) | [NuGet 2.1 Release Notes](../release-notes/nuget-2.1.md)</span></span>

<span data-ttu-id="6cec2-105">Nuget 2,0 wurde am 19. Juni 2012 veröffentlicht.</span><span class="sxs-lookup"><span data-stu-id="6cec2-105">NuGet 2.0 was released on June 19, 2012.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="6cec2-106">Bekanntes Installationsproblem</span><span class="sxs-lookup"><span data-stu-id="6cec2-106">Known Installation Issue</span></span>
<span data-ttu-id="6cec2-107">Wenn Sie Visual Studio 2010 SP1 ausführen, tritt möglicherweise ein Installationsfehler auf, wenn Sie versuchen, ein Upgrade für nuget auszuführen, wenn Sie eine ältere Version installiert haben.</span><span class="sxs-lookup"><span data-stu-id="6cec2-107">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="6cec2-108">Die Problem Umgehung besteht darin, dass Sie nuget einfach deinstallieren und anschließend aus dem vs-Erweiterungs Katalog installieren.</span><span class="sxs-lookup"><span data-stu-id="6cec2-108">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="6cec2-109"><https://support.microsoft.com/kb/2581019>Weitere Informationen finden Sie unter, oder wechseln [Sie direkt zum vs-Hotfix](http://bit.ly/vsixcertfix).</span><span class="sxs-lookup"><span data-stu-id="6cec2-109">See <https://support.microsoft.com/kb/2581019> for more information, or [go directly to the VS hotfix](http://bit.ly/vsixcertfix).</span></span>

<span data-ttu-id="6cec2-110">Hinweis: Wenn Visual Studio die Deinstallation der Erweiterung nicht zulässt (die Schaltfläche "deinstallieren" ist deaktiviert), müssen Sie Visual Studio wahrscheinlich mit "als Administrator ausführen" neu starten.</span><span class="sxs-lookup"><span data-stu-id="6cec2-110">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="package-restore-consent-is-now-active"></a><span data-ttu-id="6cec2-111">Die Zustimmung zur Paket Wiederherstellung ist nun aktiv.</span><span class="sxs-lookup"><span data-stu-id="6cec2-111">Package restore consent is now active</span></span>

<span data-ttu-id="6cec2-112">Wie in diesem [Beitrag zur Zustimmung zur Paket Wiederherstellung](http://blog.nuget.org/20120518/package-restore-and-consent.html)beschrieben, erfordert nuget 2,0 nun, dass die Zustimmung erteilt wird, damit die Paket Wiederherstellung online geschaltet und Pakete heruntergeladen werden kann.</span><span class="sxs-lookup"><span data-stu-id="6cec2-112">As described in this [post on package restore consent](http://blog.nuget.org/20120518/package-restore-and-consent.html), NuGet 2.0 will now require that consent be given to enable package restore to go online and download packages.</span></span> <span data-ttu-id="6cec2-113">Stellen Sie sicher, dass Sie die Zustimmung entweder über das Dialogfeld Paket-Manager-Konfiguration oder die Umgebungsvariable enablenugetpackagerestore angegeben haben.</span><span class="sxs-lookup"><span data-stu-id="6cec2-113">Please ensure that you have provided consent via either the package manager configuration dialog or the EnableNuGetPackageRestore environment variable.</span></span>

## <a name="group-dependencies-by-target-frameworks"></a><span data-ttu-id="6cec2-114">Gruppieren von Abhängigkeiten nach Ziel Frameworks</span><span class="sxs-lookup"><span data-stu-id="6cec2-114">Group dependencies by target frameworks</span></span>

<span data-ttu-id="6cec2-115">Ab Version 2,0 können Paketabhängigkeiten basierend auf dem frameworkprofil des Ziel Projekts variieren.</span><span class="sxs-lookup"><span data-stu-id="6cec2-115">Starting with version 2.0, package dependencies can vary based on the framework profile of the target project.</span></span> <span data-ttu-id="6cec2-116">Dies wird mit einem aktualisierten `.nuspec` Schema erreicht.</span><span class="sxs-lookup"><span data-stu-id="6cec2-116">This is accomplished using an updated `.nuspec` schema.</span></span> <span data-ttu-id="6cec2-117">Das- `<dependencies>` Element kann nun eine Reihe von- `<group>` Elementen enthalten.</span><span class="sxs-lookup"><span data-stu-id="6cec2-117">The `<dependencies>` element can now contain a set of `<group>` elements.</span></span> <span data-ttu-id="6cec2-118">Jede Gruppe enthält 0 (null) oder mehr `<dependency>` Elemente und ein- `targetFramework` Attribut.</span><span class="sxs-lookup"><span data-stu-id="6cec2-118">Each group contains zero or more `<dependency>` elements and a `targetFramework` attribute.</span></span> <span data-ttu-id="6cec2-119">Alle Abhängigkeiten innerhalb einer Gruppe werden miteinander installiert, wenn das Ziel Framework mit dem Ziel Projekt Framework-Profil kompatibel ist.</span><span class="sxs-lookup"><span data-stu-id="6cec2-119">All dependencies inside a group are installed together if the target framework is compatible with the target project framework profile.</span></span> <span data-ttu-id="6cec2-120">Zum Beispiel:</span><span class="sxs-lookup"><span data-stu-id="6cec2-120">For example:</span></span>

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

<span data-ttu-id="6cec2-121">Beachten Sie, dass eine Gruppe **keine** Abhängigkeiten enthalten kann.</span><span class="sxs-lookup"><span data-stu-id="6cec2-121">Note that a group can contain **zero** dependencies.</span></span> <span data-ttu-id="6cec2-122">Wenn das Paket in dem obigen Beispiel in einem Projekt installiert wird, das Silverlight 3,0 oder höher als Ziel verwendet, werden keine Abhängigkeiten installiert.</span><span class="sxs-lookup"><span data-stu-id="6cec2-122">In the example above, if the package is installed into a project that targets Silverlight 3.0 or later, no dependencies will be installed.</span></span> <span data-ttu-id="6cec2-123">Wenn das Paket in einem Projekt installiert wird, das auf .NET 4,0 oder höher ausgerichtet ist, werden zwei Abhängigkeiten, jQuery und webactivator, installiert.</span><span class="sxs-lookup"><span data-stu-id="6cec2-123">If the package is installed into a project that targets .NET 4.0 or later, two dependencies, jQuery and WebActivator, will be installed.</span></span>  <span data-ttu-id="6cec2-124">Wenn das Paket in einem Projekt installiert wird, das eine frühe Version dieser 2 Frameworks oder eines beliebigen anderen Frameworks als Ziel hat, wird routemagic 1.1.0 installiert.</span><span class="sxs-lookup"><span data-stu-id="6cec2-124">If the package is installed into a project that targets an early version of these 2 frameworks, or any other framework, RouteMagic 1.1.0 will be installed.</span></span> <span data-ttu-id="6cec2-125">Es gibt keine Vererbung zwischen Gruppen.</span><span class="sxs-lookup"><span data-stu-id="6cec2-125">There is no inheritance between groups.</span></span> <span data-ttu-id="6cec2-126">Wenn das Ziel Framework eines Projekts mit dem `targetFramework` Attribut einer Gruppe übereinstimmt, werden nur die Abhängigkeiten innerhalb dieser Gruppe installiert.</span><span class="sxs-lookup"><span data-stu-id="6cec2-126">If a project's target framework matches the `targetFramework` attribute of a group, only the dependencies within that group will be installed.</span></span>

<span data-ttu-id="6cec2-127">Ein Paket kann Paketabhängigkeiten in einem von zwei Formaten angeben: das alte Format einer flachen Liste von `<dependency>` Elementen oder Gruppen.</span><span class="sxs-lookup"><span data-stu-id="6cec2-127">A package can specify package dependencies in either of two formats: the old format of a flat list of `<dependency>` elements, or groups.</span></span> <span data-ttu-id="6cec2-128">Wenn das- `<group>` Format verwendet wird, kann das Paket nicht in Versionen von nuget vor 2,0 installiert werden.</span><span class="sxs-lookup"><span data-stu-id="6cec2-128">If the `<group>` format is used, the package cannot be installed into versions of NuGet earlier than 2.0.</span></span>

<span data-ttu-id="6cec2-129">Beachten Sie, dass das Mischen der beiden Formate nicht zulässig ist.</span><span class="sxs-lookup"><span data-stu-id="6cec2-129">Note that mixing the two formats is not allowed.</span></span> <span data-ttu-id="6cec2-130">Der folgende Code Ausschnitt ist beispielsweise **ungültig** und wird von nuget abgelehnt.</span><span class="sxs-lookup"><span data-stu-id="6cec2-130">For example, the following snippet is **invalid** and will be rejected by NuGet.</span></span>

```xml
<dependencies>
    <dependency id="jQuery" />
    <dependency id="WebActivator" />

    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>
</dependencies>
```

## <a name="grouping-content-files-and-powershell-scripts-by-target-framework"></a><span data-ttu-id="6cec2-131">Gruppieren von Inhalts Dateien und PowerShell-Skripts nach Ziel Framework</span><span class="sxs-lookup"><span data-stu-id="6cec2-131">Grouping content files and PowerShell scripts by target framework</span></span>

<span data-ttu-id="6cec2-132">Zusätzlich zu Assemblyverweisen können Inhalts Dateien und PowerShell-Skripts auch nach Ziel Framework gruppiert werden.</span><span class="sxs-lookup"><span data-stu-id="6cec2-132">In addition to assembly references, content files and PowerShell scripts can also be grouped by target framework.</span></span> <span data-ttu-id="6cec2-133">Die gleiche Ordnerstruktur, die im `lib` Ordner zum Angeben des Ziel-Frameworks gefunden wurde, kann jetzt auf die gleiche Weise wie die `content` -und-Ordner angewendet werden `tools` .</span><span class="sxs-lookup"><span data-stu-id="6cec2-133">The same folder structure found in the `lib` folder for specifying target framework can  now be applied in the same way to the `content` and `tools` folders.</span></span> <span data-ttu-id="6cec2-134">Zum Beispiel:</span><span class="sxs-lookup"><span data-stu-id="6cec2-134">For example:</span></span>

```
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
```

<span data-ttu-id="6cec2-135">**Hinweis**: da `init.ps1` auf Projektmappenebene ausgeführt wird und nicht von einem einzelnen Projekt abhängig ist, muss es direkt in den Ordner eingefügt werden `tools` .</span><span class="sxs-lookup"><span data-stu-id="6cec2-135">**Note**: Because `init.ps1` is executed at the solution level and is not dependent on any individual project, it must be placed directly under the `tools` folder.</span></span> <span data-ttu-id="6cec2-136">Wenn Sie in einem frameworkspezifischen Ordner platziert wird, wird Sie ignoriert.</span><span class="sxs-lookup"><span data-stu-id="6cec2-136">If placed within a framework-specific folder, it will be ignored.</span></span>

<span data-ttu-id="6cec2-137">Außerdem ist ein neues Feature in nuget 2,0, dass ein frameworkordner *leer* sein kann. in diesem Fall werden von nuget keine Assemblyverweise hinzugefügt, Inhalts Dateien hinzugefügt oder PowerShell-Skripts für die jeweilige Frameworkversion ausgeführt.</span><span class="sxs-lookup"><span data-stu-id="6cec2-137">Also, a new feature in NuGet 2.0 is that a framework folder can be *empty*, in which case, NuGet will not add assembly references, add content files or run  PowerShell scripts for the particular framework version.</span></span> <span data-ttu-id="6cec2-138">Im obigen Beispiel ist der Ordner `content\net40` leer.</span><span class="sxs-lookup"><span data-stu-id="6cec2-138">In the example above, the folder `content\net40` is empty.</span></span>

## <a name="improved-tab-completion-performance"></a><span data-ttu-id="6cec2-139">Verbesserte Tab-Vervollständigungs Leistung</span><span class="sxs-lookup"><span data-stu-id="6cec2-139">Improved tab completion performance</span></span>
<span data-ttu-id="6cec2-140">Die Funktion zum Vervollständigen der Registerkarte in der nuget-Paket-Manager-Konsole wurde aktualisiert, um die Leistung deutlich zu verbessern</span><span class="sxs-lookup"><span data-stu-id="6cec2-140">The tab completion feature in the NuGet Package Manager Console has been updated to significantly improve performance.</span></span> <span data-ttu-id="6cec2-141">Der Zeitpunkt, zu dem die Tab-Taste gedrückt wird, wird so lange weniger verzögert, bis die Dropdown Liste für Vorschläge angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="6cec2-141">There will be much less delay from the time the tab key is pressed until the suggestion dropdown appears.</span></span>

## <a name="bug-fixes"></a><span data-ttu-id="6cec2-142">Fehlerkorrekturen</span><span class="sxs-lookup"><span data-stu-id="6cec2-142">Bug Fixes</span></span>
<span data-ttu-id="6cec2-143">Nuget 2,0 umfasst viele Fehlerbehebungen mit dem Schwerpunkt auf Zustimmung und Leistung der Paket Wiederherstellung.</span><span class="sxs-lookup"><span data-stu-id="6cec2-143">NuGet 2.0 includes many bug fixes with an emphasis on package restore consent and performance.</span></span>
<span data-ttu-id="6cec2-144">Eine vollständige Liste der Arbeitselemente, die in nuget 2,0 behoben wurden, finden Sie in der [nuget-Problemverfolgung für diese Version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="6cec2-144">For a full list of work items fixed in NuGet 2.0, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
