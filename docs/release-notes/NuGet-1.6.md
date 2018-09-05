---
title: Anmerkungen zu NuGet-Version 1.6
description: Anmerkungen zu NuGet-1.6, einschließlich der bekannten Probleme, Fehlerkorrekturen, hinzugefügter Features und DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 351303ca3ae27a37c19e59d84dfc9b4629fe0ca5
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43549011"
---
 # <a name="nuget-16-release-notes"></a><span data-ttu-id="e0fa4-103">Anmerkungen zu NuGet-Version 1.6</span><span class="sxs-lookup"><span data-stu-id="e0fa4-103">NuGet 1.6 Release Notes</span></span>

<span data-ttu-id="e0fa4-104">[Anmerkungen zu NuGet 1.5](../release-notes/nuget-1.5.md) | [Anmerkungen zu NuGet 1.7](../release-notes/nuget-1.7.md)</span><span class="sxs-lookup"><span data-stu-id="e0fa4-104">[NuGet 1.5 Release Notes](../release-notes/nuget-1.5.md) | [NuGet 1.7 Release Notes](../release-notes/nuget-1.7.md)</span></span>

<span data-ttu-id="e0fa4-105">NuGet-1.6 wurde am 13 Dezember 2011 veröffentlicht.</span><span class="sxs-lookup"><span data-stu-id="e0fa4-105">NuGet 1.6 was released on December 13, 2011.</span></span>

## <a name="known-installation-issue"></a><span data-ttu-id="e0fa4-106">Problem für bekannte Installationsprobleme</span><span class="sxs-lookup"><span data-stu-id="e0fa4-106">Known Installation Issue</span></span>
<span data-ttu-id="e0fa4-107">Wenn Sie Visual Studio 2010 SP1 ausführen, können Sie ein Installationsfehler auftreten, beim Versuch, NuGet aktualisieren, wenn Sie eine ältere Version installiert haben.</span><span class="sxs-lookup"><span data-stu-id="e0fa4-107">If you are running VS 2010 SP1, you might run into an installation error when attempting to upgrade NuGet if you have an older version installed.</span></span>

<span data-ttu-id="e0fa4-108">Die problemumgehung besteht darin, einfach NuGet zuerst deinstallieren und installieren Sie es aus dem Katalog der VS-Erweiterung.</span><span class="sxs-lookup"><span data-stu-id="e0fa4-108">The workaround is to simply uninstall NuGet and then install it from the VS Extension Gallery.</span></span>  <span data-ttu-id="e0fa4-109">Weitere Informationen finden Sie unter [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019).</span><span class="sxs-lookup"><span data-stu-id="e0fa4-109">See [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) for more information.</span></span>

<span data-ttu-id="e0fa4-110">Hinweis: Wenn Visual Studio ist es nicht zulässig, die die Erweiterung deinstallieren (die Schaltfläche "Deinstallieren" deaktiviert ist), müssen Sie wahrscheinlich zum Neustart von Visual Studio mithilfe von "Ausführen als Administrator."</span><span class="sxs-lookup"><span data-stu-id="e0fa4-110">Note: If Visual Studio won't allow you to uninstall the extension (the Uninstall button is disabled), then you likely need to restart Visual Studio using "Run as Administrator."</span></span>

## <a name="features"></a><span data-ttu-id="e0fa4-111">Features</span><span class="sxs-lookup"><span data-stu-id="e0fa4-111">Features</span></span>

### <a name="support-for-semantic-versioning-and-prerelease-packages"></a><span data-ttu-id="e0fa4-112">Unterstützung für semantische Versionierung und Vorabversionen von Paketen</span><span class="sxs-lookup"><span data-stu-id="e0fa4-112">Support for Semantic Versioning and Prerelease Packages</span></span>
<span data-ttu-id="e0fa4-113">NuGet-1.6 führt die Unterstützung für semantische Versionskontrolle (SemVer).</span><span class="sxs-lookup"><span data-stu-id="e0fa4-113">NuGet 1.6 introduces support for Semantic Versioning (SemVer).</span></span> <span data-ttu-id="e0fa4-114">Lesen Sie weitere Informationen dazu, wie sie SemVer verwendet die [Versionsverwaltung Dokumentation](../create-packages/prerelease-packages.md).</span><span class="sxs-lookup"><span data-stu-id="e0fa4-114">For more details on how it uses SemVer, read the [Versioning documentation](../create-packages/prerelease-packages.md).</span></span>

### <a name="using-nuget-without-checking-in-packages-package-restore"></a><span data-ttu-id="e0fa4-115">Verwenden von NuGet ohne das Einchecken von Paketen (Paketwiederherstellung)</span><span class="sxs-lookup"><span data-stu-id="e0fa4-115">Using NuGet Without Checking In Packages (Package Restore)</span></span>
<span data-ttu-id="e0fa4-116">NuGet-1.6 verfügt jetzt über erstklassige Unterstützung für den Workflow, in welche, den, den NuGet Pakete werden in die quellcodeverwaltung nicht hinzugefügt, jedoch stattdessen werden wiederhergestellt zum Zeitpunkt der Erstellung bei fehlen.</span><span class="sxs-lookup"><span data-stu-id="e0fa4-116">NuGet 1.6 now has first class support for the workflow in which NuGet packages are not added to source control, but instead are restored at build time if missing.</span></span> <span data-ttu-id="e0fa4-117">Weitere Informationen finden Sie in der [mithilfe von NuGet ohne das Übernehmen von Paketen in der quellcodeverwaltung](../consume-packages/packages-and-source-control.md) Thema.</span><span class="sxs-lookup"><span data-stu-id="e0fa4-117">For more details, read the [Using NuGet without committing packages to source control](../consume-packages/packages-and-source-control.md) topic.</span></span>

### <a name="item-templates-that-install-nuget-packages"></a><span data-ttu-id="e0fa4-118">Vorlagen, die NuGet-Pakete installieren</span><span class="sxs-lookup"><span data-stu-id="e0fa4-118">Item Templates That Install NuGet Packages</span></span>
<span data-ttu-id="e0fa4-119">Auf der Arbeit zur Unterstützung von Visual Studio-Projektvorlagen vorinstallierte NuGet-Paket erstellen, fügt NuGet 1.6 auch Unterstützung für Visual Studio-Projektelementvorlagen.</span><span class="sxs-lookup"><span data-stu-id="e0fa4-119">Building on the work to support preinstalled NuGet package to Visual Studio project templates, NuGet 1.6 also adds support for Visual Studio item templates.</span></span> <span data-ttu-id="e0fa4-120">Elementvorlagen können NuGet-Paketen zugeordnet, die installiert werden, wenn die Vorlage in aufgerufen.</span><span class="sxs-lookup"><span data-stu-id="e0fa4-120">Item templates can have associated NuGet packages that are installed when the template in invoked.</span></span>

<span data-ttu-id="e0fa4-121">Weitere Informationen zum Ändern einer Projekt-/Elementvorlage zum Installieren von NuGet-Pakete finden Sie in der [Pakete in Visual Studio-Vorlagen](../visual-studio-extensibility/visual-studio-templates.md) Thema.</span><span class="sxs-lookup"><span data-stu-id="e0fa4-121">For more details on how to change a project/item template to install NuGet packages, read the [Packages in Visual Studio Templates](../visual-studio-extensibility/visual-studio-templates.md) topic.</span></span>

### <a name="support-for-disabling-package-sources"></a><span data-ttu-id="e0fa4-122">Unterstützung zur Deaktivierung von Paketquellen</span><span class="sxs-lookup"><span data-stu-id="e0fa4-122">Support for disabling package sources</span></span>
<span data-ttu-id="e0fa4-123">Wenn mehrerer Paketquellen konfiguriert sind, sucht NuGet jeweils für Pakete während der Installation von einem Paket und seine Abhängigkeiten.</span><span class="sxs-lookup"><span data-stu-id="e0fa4-123">When multiple package sources are configured, NuGet will look in each one for packages during installation of a package and its dependencies.</span></span> <span data-ttu-id="e0fa4-124">Eine Paketquelle, das Sie für aus irgendeinem Grund stark NuGet verlangsamen kann.</span><span class="sxs-lookup"><span data-stu-id="e0fa4-124">A package source that is down for some reason can severely slow down NuGet.</span></span>

<span data-ttu-id="e0fa4-125">Vor dem NuGet-1.6 könnten Sie die Paketquelle entfernen, aber anschließend müssen Sie denken Sie daran, dass die Details für, wenn Sie sie hinzufügen möchten in back.</span><span class="sxs-lookup"><span data-stu-id="e0fa4-125">Prior to NuGet 1.6, you could remove the package source, but then you have to remember the details for when you want to add it back in.</span></span>

<span data-ttu-id="e0fa4-126">NuGet-1.6 ermöglicht es, wenn Sie eine Paketquelle zum Halten Sie es aber deaktivieren, deaktivieren.</span><span class="sxs-lookup"><span data-stu-id="e0fa4-126">NuGet 1.6 allows unchecking a package source to disable it, but keep it around.</span></span>

![Deaktivieren ein Paket](./media/package-source-with-disabled-source.png)

## <a name="bug-fixes"></a><span data-ttu-id="e0fa4-128">Fehlerkorrekturen</span><span class="sxs-lookup"><span data-stu-id="e0fa4-128">Bug Fixes</span></span>
<span data-ttu-id="e0fa4-129">NuGet-1.6 mussten insgesamt 106 Arbeitsaufgaben behoben.</span><span class="sxs-lookup"><span data-stu-id="e0fa4-129">NuGet 1.6 had a total of 106 work items fixed.</span></span> <span data-ttu-id="e0fa4-130">95 davon wurden als Fehler eingestuft, und 10 dieser wurden die Funktionen.</span><span class="sxs-lookup"><span data-stu-id="e0fa4-130">95 of those were classified as bugs and 10 of those were features.</span></span>

<span data-ttu-id="e0fa4-131">Eine vollständige Liste der Arbeit Elemente eine feste in NuGet-1.6, bitte Ansicht der [NuGet Issue Tracker für diese Version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span><span class="sxs-lookup"><span data-stu-id="e0fa4-131">For a full list of work items fixed in NuGet 1.6, please view the [NuGet Issue Tracker for this release](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).</span></span>
