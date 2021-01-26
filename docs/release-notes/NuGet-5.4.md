---
title: Anmerkungen zu dieser Version von nuget 5,4
description: Anmerkungen zu dieser Version von nuget 5,4, einschließlich neuer Features, Fehlerbehebungen und dcrs.
author: JonDouglas
ms.author: jodou
ms.date: 09/06/2019
ms.topic: conceptual
ms.openlocfilehash: dd4c10672db3a65b68f18636105ee55ab09da7ef
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776189"
---
# <a name="nuget-54-release-notes"></a><span data-ttu-id="dab66-103">Anmerkungen zu dieser Version von nuget 5,4</span><span class="sxs-lookup"><span data-stu-id="dab66-103">NuGet 5.4 Release Notes</span></span>

<span data-ttu-id="dab66-104">Möglichkeiten der NuGet-Verteilung:</span><span class="sxs-lookup"><span data-stu-id="dab66-104">NuGet distribution vehicles:</span></span>

| <span data-ttu-id="dab66-105">NuGet-Version</span><span class="sxs-lookup"><span data-stu-id="dab66-105">NuGet version</span></span> | <span data-ttu-id="dab66-106">Verfügbar in der Visual Studio-Version</span><span class="sxs-lookup"><span data-stu-id="dab66-106">Available in Visual Studio version</span></span>| <span data-ttu-id="dab66-107">Verfügbar in .NET SDK(s)</span><span class="sxs-lookup"><span data-stu-id="dab66-107">Available in .NET SDK(s)</span></span>|
|:---|:---|:---|
| [<span data-ttu-id="dab66-108">**5.4.0**</span><span class="sxs-lookup"><span data-stu-id="dab66-108">**5.4.0**</span></span>](https://nuget.org/downloads) | [<span data-ttu-id="dab66-109">Visual Studio 2019, Version 16,4</span><span class="sxs-lookup"><span data-stu-id="dab66-109">Visual Studio 2019 version 16.4</span></span>](https://visualstudio.microsoft.com/downloads/) | <span data-ttu-id="dab66-110">[3.1.100](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span><span class="sxs-lookup"><span data-stu-id="dab66-110">[3.1.100](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup></span></span> |

<span data-ttu-id="dab66-111"><sup>1</sup> Installiert mit Visual Studio 2019 mit .net Core-Arbeitsauslastung</span><span class="sxs-lookup"><span data-stu-id="dab66-111"><sup>1</sup>Installed with Visual Studio 2019 with .NET Core workload</span></span>

## <a name="summary-whats-new-in-54"></a><span data-ttu-id="dab66-112">Zusammenfassung: Neues in 5,4</span><span class="sxs-lookup"><span data-stu-id="dab66-112">Summary: What's New in 5.4</span></span>

* <span data-ttu-id="dab66-113">Schnellere Ladezeit für Projektmappen: der Aufwand für die Ausführung von nuget-Code beim ersten Laden der Projekt Mappe wurde über partielle ngen reduziert, um JIT-Kosten [#6007](https://github.com/NuGet/Home/issues/6007)</span><span class="sxs-lookup"><span data-stu-id="dab66-113">Faster solution load time - Overhead running NuGet code during first solution load has been reduced via partial-ngen to reduce JIT cost - [#6007](https://github.com/NuGet/Home/issues/6007)</span></span>

* <span data-ttu-id="dab66-114">Neue Hilfsfunktion: Wenn Sie eine Liste von Paket-IDs und-Versionen erhalten, erhalten Sie die wahrscheinlichsten Pakete auf oberster Ebene.</span><span class="sxs-lookup"><span data-stu-id="dab66-114">New helper function - given a list of package ids and versions, get the likely top level packages.</span></span><span data-ttu-id="dab66-115"> - [#8316](https://github.com/NuGet/Home/issues/8316)</span><span class="sxs-lookup"><span data-stu-id="dab66-115"> - [#8316](https://github.com/NuGet/Home/issues/8316)</span></span>

* <span data-ttu-id="dab66-116">Neue [`nuget/setup-nuget`](https://github.com/marketplace/actions/setup-nuget-exe-for-use-with-actions) Aktion zum Installieren und Konfigurieren von NuGet.exe auf [GitHub-Aktionen](https://github.com/features/actions).</span><span class="sxs-lookup"><span data-stu-id="dab66-116">New [`nuget/setup-nuget`](https://github.com/marketplace/actions/setup-nuget-exe-for-use-with-actions) action for installing and configuring NuGet.exe on [GitHub Actions](https://github.com/features/actions).</span></span><span data-ttu-id="dab66-117"> - [#8818](https://github.com/NuGet/Home/issues/8818)</span><span class="sxs-lookup"><span data-stu-id="dab66-117"> - [#8818](https://github.com/NuGet/Home/issues/8818)</span></span>

### <a name="issues-fixed-in-this-release"></a><span data-ttu-id="dab66-118">In diesem Release behobene Probleme</span><span class="sxs-lookup"><span data-stu-id="dab66-118">Issues fixed in this release</span></span>

<span data-ttu-id="dab66-119">**Fehler**</span><span class="sxs-lookup"><span data-stu-id="dab66-119">**Bugs**</span></span>

* <span data-ttu-id="dab66-120">Plug-in: Zeit Genauigkeit der Protokollierung auf Linux/Mac- [#8747](https://github.com/NuGet/Home/issues/8747)</span><span class="sxs-lookup"><span data-stu-id="dab66-120">Plugin: Logging time accuracy is off on linux/Mac - [#8747](https://github.com/NuGet/Home/issues/8747)</span></span>

* <span data-ttu-id="dab66-121">Das Verwerfen eines Plug-ins kann manchmal den gesamten Vorgang auslösen und einen Fehler verursachen.</span><span class="sxs-lookup"><span data-stu-id="dab66-121">Disposing of a plugin can sometimes throw and fail the whole operation.</span></span><span data-ttu-id="dab66-122"> - [#8732](https://github.com/NuGet/Home/issues/8732)</span><span class="sxs-lookup"><span data-stu-id="dab66-122"> - [#8732](https://github.com/NuGet/Home/issues/8732)</span></span>

* <span data-ttu-id="dab66-123">Anzeigen von Versions Duplikaten in der Liste der zulässigen und blockierten Versionen in PMUI- [#8679](https://github.com/NuGet/Home/issues/8679)</span><span class="sxs-lookup"><span data-stu-id="dab66-123">Stop displaying version duplicates in allowed and blocked versions list in PMUI - [#8679](https://github.com/NuGet/Home/issues/8679)</span></span>

* <span data-ttu-id="dab66-124">Die Sperrdatei wurde nicht ordnungsgemäß generiert. die frameworkreihen Folge sollte die Wiederherstellung mit lockedmode- [#8645](https://github.com/NuGet/Home/issues/8645) nicht beeinträchtigen.</span><span class="sxs-lookup"><span data-stu-id="dab66-124">Lock File not properly generated - framework ordering should not impact the restore with lockedmode - [#8645](https://github.com/NuGet/Home/issues/8645)</span></span>

* <span data-ttu-id="dab66-125">Fehler bei der lockfile-Überprüfung für Projekte mit <RuntimeIdentifiers> Set in SDK 3.0.100- [#8639](https://github.com/NuGet/Home/issues/8639)</span><span class="sxs-lookup"><span data-stu-id="dab66-125">LockFile validation fails for projects with <RuntimeIdentifiers> set in SDK 3.0.100 - [#8639](https://github.com/NuGet/Home/issues/8639)</span></span>

* <span data-ttu-id="dab66-126">Bei der Signatur Überprüfung werden Signaturen mit Zeitstempeln ordnungsgemäß abgelehnt, die zwei Werte unter derselben OID aufweisen [#8629](https://github.com/NuGet/Home/issues/8629)</span><span class="sxs-lookup"><span data-stu-id="dab66-126">Signing Validation will now properly reject signatures with timestamps which have 2 values under the same OID - [#8629](https://github.com/NuGet/Home/issues/8629)</span></span>

* <span data-ttu-id="dab66-127">Aktualisieren der Lizenz Liste- [#8544](https://github.com/NuGet/Home/issues/8544)</span><span class="sxs-lookup"><span data-stu-id="dab66-127">Update the license list - [#8544](https://github.com/NuGet/Home/issues/8544)</span></span>

<span data-ttu-id="dab66-128">**DCRs**</span><span class="sxs-lookup"><span data-stu-id="dab66-128">**DCRs**</span></span>

* <span data-ttu-id="dab66-129">Onboarding von Diagnose Dateien in ifeedbackdiagnosticfileprovider- [#8535](https://github.com/NuGet/Home/issues/8535)</span><span class="sxs-lookup"><span data-stu-id="dab66-129">Onboarding diagnostic files to IFeedbackDiagnosticFileProvider - [#8535](https://github.com/NuGet/Home/issues/8535)</span></span>

<span data-ttu-id="dab66-130">**[Liste aller Probleme, die in dieser Version behoben wurden: 5,4](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.4")**</span><span class="sxs-lookup"><span data-stu-id="dab66-130">**[List of all issues fixed in this release - 5.4](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.4")**</span></span>
