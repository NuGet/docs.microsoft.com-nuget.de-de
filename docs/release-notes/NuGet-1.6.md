---
title: Anmerkungen zu dieser Version von nuget 1,6
description: Anmerkungen zu dieser Version von nuget 1,6 einschließlich bekannter Probleme, Fehlerbehebungen, hinzugefügter Features und dcrs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 08b1cb3736e645d6efcc33f920f521c9c0fc7507
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777014"
---
 # <a name="nuget-16-release-notes"></a><span data-ttu-id="f2602-103">Anmerkungen zu dieser Version von nuget 1,6</span><span class="sxs-lookup"><span data-stu-id="f2602-103">NuGet 1.6 Release Notes</span></span>

<span data-ttu-id="f2602-104">Anmerkungen zu dieser [Version von nuget 1,5](../release-notes/nuget-1.5.md)  |  [Anmerkungen zu dieser Version von nuget 1,7](../release-notes/nuget-1.7.md)</span><span class="sxs-lookup"><span data-stu-id="f2602-104">[NuGet 1.5 Release Notes](../release-notes/nuget-1.5.md) | [NuGet 1.7 Release Notes](../release-notes/nuget-1.7.md)</span></span>

<span data-ttu-id="f2602-105">Nuget 1,6 wurde am 13. Dezember 2011 veröffentlicht.</span><span class="sxs-lookup"><span data-stu-id="f2602-105">NuGet 1.6 was released on December 13, 2011.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="f2602-106">Bekanntes Installationsproblem</span><span class="sxs-lookup"><span data-stu-id="f2602-106">Known Installation Issue</span></span>
<span data-ttu-id="f2602-107">Wenn Sie Visual Studio 2010 SP1 ausführen, tritt möglicherweise ein Installationsfehler auf, wenn Sie versuchen, ein Upgrade für nuget auszuführen, wenn Sie eine ältere Version installiert haben.</span><span class="sxs-lookup"><span data-stu-id="f2602-107">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="f2602-108">Die Problem Umgehung besteht darin, dass Sie nuget einfach deinstallieren und anschließend aus dem vs-Erweiterungs Katalog installieren.</span><span class="sxs-lookup"><span data-stu-id="f2602-108">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="f2602-109">Weitere Informationen finden Sie unter <https://support.microsoft.com/kb/2581019>.</span><span class="sxs-lookup"><span data-stu-id="f2602-109">See <https://support.microsoft.com/kb/2581019> for more information.</span></span>

<span data-ttu-id="f2602-110">Hinweis: Wenn Visual Studio die Deinstallation der Erweiterung nicht zulässt (die Schaltfläche "deinstallieren" ist deaktiviert), müssen Sie Visual Studio wahrscheinlich mit "als Administrator ausführen" neu starten.</span><span class="sxs-lookup"><span data-stu-id="f2602-110">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="features"></a><span data-ttu-id="f2602-111">Features</span><span class="sxs-lookup"><span data-stu-id="f2602-111">Features</span></span>

### <a name="support-for-semantic-versioning-and-prerelease-packages"></a><span data-ttu-id="f2602-112">Unterstützung für semantische Versionierung und vorab Versionen von Paketen</span><span class="sxs-lookup"><span data-stu-id="f2602-112">Support for Semantic Versioning and Prerelease Packages</span></span>
<span data-ttu-id="f2602-113">Mit nuget 1,6 wird die Unterstützung für die semantische Versionierung (semver) eingeführt.</span><span class="sxs-lookup"><span data-stu-id="f2602-113">NuGet 1.6 introduces support for Semantic Versioning (SemVer).</span></span> <span data-ttu-id="f2602-114">Weitere Informationen zur Verwendung von semver finden Sie in der [Dokumentation zur Versions](../create-packages/prerelease-packages.md)Verwaltung.</span><span class="sxs-lookup"><span data-stu-id="f2602-114">For more details on how it uses SemVer, read the [Versioning documentation](../create-packages/prerelease-packages.md).</span></span>

### <a name="using-nuget-without-checking-in-packages-package-restore"></a><span data-ttu-id="f2602-115">Verwenden von nuget ohne Einchecken von Paketen (Paket Wiederherstellung)</span><span class="sxs-lookup"><span data-stu-id="f2602-115">Using NuGet Without Checking In Packages (Package Restore)</span></span>
<span data-ttu-id="f2602-116">Nuget 1,6 bietet jetzt erstklassige Unterstützung für den Workflow, in dem nuget-Pakete nicht zur Quell Code Verwaltung hinzugefügt werden, sondern zur Buildzeit wieder hergestellt werden, wenn Sie nicht vorhanden sind.</span><span class="sxs-lookup"><span data-stu-id="f2602-116">NuGet 1.6 now has first class support for the workflow in which NuGet packages are not added to source control, but instead are restored at build time if missing.</span></span> <span data-ttu-id="f2602-117">Weitere Informationen finden Sie im Thema [Verwenden von nuget ohne Commit für Pakete in die Quell](../consume-packages/packages-and-source-control.md) Code Verwaltung.</span><span class="sxs-lookup"><span data-stu-id="f2602-117">For more details, read the [Using NuGet without committing packages to source control](../consume-packages/packages-and-source-control.md) topic.</span></span>

### <a name="item-templates-that-install-nuget-packages"></a><span data-ttu-id="f2602-118">Element Vorlagen zum Installieren von nuget-Paketen</span><span class="sxs-lookup"><span data-stu-id="f2602-118">Item Templates That Install NuGet Packages</span></span>
<span data-ttu-id="f2602-119">Wenn Sie auf der Arbeit arbeiten, um das vorinstallierte nuget-Paket in Visual Studio-Projektvorlagen zu unterstützen, fügt nuget 1,6 auch Unterstützung für Visual Studio-Element Vorlagen hinzu</span><span class="sxs-lookup"><span data-stu-id="f2602-119">Building on the work to support preinstalled NuGet package to Visual Studio project templates, NuGet 1.6 also adds support for Visual Studio item templates.</span></span> <span data-ttu-id="f2602-120">Element Vorlagen können zugehörige nuget-Pakete aufweisen, die beim Aufrufen der Vorlage installiert werden.</span><span class="sxs-lookup"><span data-stu-id="f2602-120">Item templates can have associated NuGet packages that are installed when the template in invoked.</span></span>

<span data-ttu-id="f2602-121">Weitere Informationen zum Ändern einer Projekt-/Elementvorlage zum Installieren von nuget-Paketen finden Sie im Thema [Pakete in Visual Studio-Vorlagen](../visual-studio-extensibility/visual-studio-templates.md) .</span><span class="sxs-lookup"><span data-stu-id="f2602-121">For more details on how to change a project/item template to install NuGet packages, read the [Packages in Visual Studio Templates](../visual-studio-extensibility/visual-studio-templates.md) topic.</span></span>

### <a name="support-for-disabling-package-sources"></a><span data-ttu-id="f2602-122">Unterstützung für das Deaktivieren von Paketquellen</span><span class="sxs-lookup"><span data-stu-id="f2602-122">Support for disabling package sources</span></span>
<span data-ttu-id="f2602-123">Wenn mehrere Paketquellen konfiguriert sind, sucht nuget bei der Installation eines Pakets und dessen Abhängigkeiten jeweils nach Paketen.</span><span class="sxs-lookup"><span data-stu-id="f2602-123">When multiple package sources are configured, NuGet will look in each one for packages during installation of a package and its dependencies.</span></span> <span data-ttu-id="f2602-124">Eine Paketquelle, die aus irgendeinem Grund herunter ist, kann nuget erheblich verlangsamen.</span><span class="sxs-lookup"><span data-stu-id="f2602-124">A package source that is down for some reason can severely slow down NuGet.</span></span>

<span data-ttu-id="f2602-125">Vor dem nuget-1,6 konnten Sie die Paketquelle entfernen, aber dann müssen Sie sich die Details merken, wenn Sie Sie wieder hinzufügen möchten.</span><span class="sxs-lookup"><span data-stu-id="f2602-125">Prior to NuGet 1.6, you could remove the package source, but then you have to remember the details for when you want to add it back in.</span></span>

<span data-ttu-id="f2602-126">Mit nuget 1,6 können Sie eine Paketquelle deaktivieren, um Sie zu deaktivieren.</span><span class="sxs-lookup"><span data-stu-id="f2602-126">NuGet 1.6 allows unchecking a package source to disable it, but keep it around.</span></span>

![Deaktivieren eines Pakets](./media/package-source-with-disabled-source.png)

## <a name="bug-fixes"></a><span data-ttu-id="f2602-128">Fehlerkorrekturen</span><span class="sxs-lookup"><span data-stu-id="f2602-128">Bug Fixes</span></span>
<span data-ttu-id="f2602-129">Für nuget 1,6 wurden insgesamt 106 Arbeitselemente korrigiert.</span><span class="sxs-lookup"><span data-stu-id="f2602-129">NuGet 1.6 had a total of 106 work items fixed.</span></span> <span data-ttu-id="f2602-130">95 von diesen wurden als Fehler klassifiziert, und 10 dieser Features waren.</span><span class="sxs-lookup"><span data-stu-id="f2602-130">95 of those were classified as bugs and 10 of those were features.</span></span>

<span data-ttu-id="f2602-131">Eine vollständige Liste der Arbeitselemente, die in nuget 1,6 behoben wurden, finden Sie in der [nuget-Problemverfolgung für diese Version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="f2602-131">For a full list of work items fixed in NuGet 1.6, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
