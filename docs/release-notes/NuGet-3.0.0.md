---
title: Anmerkungen zu NuGet-Version 3.0
description: Anmerkungen zu dieser Version für die Einbindung von NuGet 3.0.0 bekannte Probleme, Fehlerkorrekturen, hinzugefügter Features und DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 1ade2b5b5ff7d57d756829c1c1853b5573c17d6d
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551862"
---
# <a name="nuget-30-release-notes"></a><span data-ttu-id="bab9c-103">Anmerkungen zu NuGet-Version 3.0</span><span class="sxs-lookup"><span data-stu-id="bab9c-103">NuGet 3.0 Release Notes</span></span>

<span data-ttu-id="bab9c-104">[Anmerkungen zu NuGet 3.0 RC2](../release-notes/nuget-3.0-RC2.md) | [NuGet 3.1: Anmerkungen zu dieser Version](../release-notes/nuget-3.1.md)</span><span class="sxs-lookup"><span data-stu-id="bab9c-104">[NuGet 3.0 RC2 Release Notes](../release-notes/nuget-3.0-RC2.md) | [NuGet 3.1 Release Notes](../release-notes/nuget-3.1.md)</span></span>

<span data-ttu-id="bab9c-105">NuGet 3.0 wurde am 20. Juli 2015 als Erweiterung des Pakets in Visual Studio 2015 veröffentlicht.</span><span class="sxs-lookup"><span data-stu-id="bab9c-105">NuGet 3.0 was released on July 20, 2015 as a bundle extension to Visual Studio 2015.</span></span> <span data-ttu-id="bab9c-106">Wir mithilfe von Push übertragen dieser Version mit Visual Studio bereitstellen, damit die vollständige aktualisierte NuGet 3.0-Benutzeroberfläche für neue Benutzer von Visual Studio verfügbar ist.</span><span class="sxs-lookup"><span data-stu-id="bab9c-106">We pushed to deliver this release with Visual Studio so that the complete updated NuGet 3.0 experience would be available for new Visual Studio users.</span></span> <span data-ttu-id="bab9c-107">Diese Version des NuGet-Erweiterung ist nur für Visual Studio 2015 verfügbar.</span><span class="sxs-lookup"><span data-stu-id="bab9c-107">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="bab9c-108">Es wird empfohlen, die Entwickler, die Zugriff auf Visual Studio-Update-Katalog auf die neueste Version, die verfügbar ist verfügen, da wir ein Update kurz nach der Veröffentlichung von Visual Studio 2015 veröffentlichen, die Unterstützung für Windows 10-Entwicklung enthält.</span><span class="sxs-lookup"><span data-stu-id="bab9c-108">We recommend those developers that have access to the Visual Studio gallery update to the latest version that is available, as we are publishing an update shortly after the release of Visual Studio 2015 that contains support for Windows 10 development.</span></span>

<span data-ttu-id="bab9c-109">Insgesamt, die wir geschlossen 240 Probleme in der Version 3.0, und Sie können überprüfen, die [vollständige Liste der Probleme auf GitHub](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed).</span><span class="sxs-lookup"><span data-stu-id="bab9c-109">In total, we closed 240 issues in the 3.0 release, and you can review the [complete list of issues on GitHub](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed).</span></span>

## <a name="known-issues"></a><span data-ttu-id="bab9c-110">Bekannte Probleme</span><span class="sxs-lookup"><span data-stu-id="bab9c-110">Known Issues</span></span>

<span data-ttu-id="bab9c-111">Es gab eine Reihe bekannter Probleme, die mit dieser Version bereitgestellt, und alle diese Elemente sind in unserer geplanten 3.1-Version an mit der Veröffentlichung von Windows 10 ab dem 29. Juli festgelegt.</span><span class="sxs-lookup"><span data-stu-id="bab9c-111">There were a number of known issues delivered with this release, and all of these items are fixed in our scheduled 3.1 release to coincide with the release of Windows 10 on July 29th.</span></span>  <span data-ttu-id="bab9c-112">Sie können zum Aktualisieren Ihrer Visual Studio-Erweiterungs über den Katalog am oder nach diesem Datum dieser bekannten Probleme zu beheben.</span><span class="sxs-lookup"><span data-stu-id="bab9c-112">You are able to update your Visual Studio extension from the gallery on or after that date to fix these known issues.</span></span>

*  <span data-ttu-id="bab9c-113">Übersetzung wird nicht für die Bezeichnung "Nicht mehr anzeigen", auf das Fenster "Vorschau" und die Bezeichnung "Autoren" in das Fenster der Paket-Beschreibung bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="bab9c-113">Translation is not provided for the "Do not show this again" label on the preview window and the "Authors" label in the package description window.</span></span>
*  <span data-ttu-id="bab9c-114">Wenn Sie an einem Projekt arbeiten, mit der TFS--Steuerelement Source kann nicht NuGet der Paket-Manager-Benutzeroberfläche vorhanden, wenn die Datei "NuGet.config" als schreibgeschützt markiert ist.</span><span class="sxs-lookup"><span data-stu-id="bab9c-114">When you working on a project by using TFS source control, NuGet cannot present the package manager user interface if the Nuget.Config file is marked as read-only.</span></span>
   * <span data-ttu-id="bab9c-115">**Problemumgehung** sehen Sie sich die Datei von TFS.</span><span class="sxs-lookup"><span data-stu-id="bab9c-115">**Workaround** Check out the file from TFS.</span></span>
*  <span data-ttu-id="bab9c-116">Text in Gelb "Neustart Bar" im NuGet-Powershell-Fenster ist nicht sichtbar, wenn Sie das dunkle Design von Visual Studio verwenden.</span><span class="sxs-lookup"><span data-stu-id="bab9c-116">Text in the yellow "restart bar" in the NuGet Powershell window is not visible when you use the Visual Studio dark theme.</span></span>
   * <span data-ttu-id="bab9c-117">**Problemumgehung** das helle Design von Visual Studio verwenden.</span><span class="sxs-lookup"><span data-stu-id="bab9c-117">**Workaround** Use the Visual Studio light theme.</span></span>


## <a name="summary-of-top-issues-resolved"></a><span data-ttu-id="bab9c-118">Zusammenfassung der wichtigsten Probleme behoben</span><span class="sxs-lookup"><span data-stu-id="bab9c-118">Summary of top issues resolved</span></span>

* [<span data-ttu-id="bab9c-119">Häufige Netzwerk Update aufruft, wenn Fenster der Paket-Manager aktualisiert</span><span class="sxs-lookup"><span data-stu-id="bab9c-119">Frequent network update calls when package manager window refreshes</span></span>](https://github.com/NuGet/Home/issues/515)
* [<span data-ttu-id="bab9c-120">Scrollen Sie verzögert, wenn Ansicht ändern, um im Paket-Manager installiert werden.</span><span class="sxs-lookup"><span data-stu-id="bab9c-120">Delayed scroll when changing to installed view in package manager</span></span>](https://github.com/NuGet/Home/issues/519)
* [<span data-ttu-id="bab9c-121">Netzwerkaufrufe sollte in einem Hintergrundthread ausgeführt werden</span><span class="sxs-lookup"><span data-stu-id="bab9c-121">Network calls should be run on a background thread</span></span>](https://github.com/NuGet/Home/issues/516)
* [<span data-ttu-id="bab9c-122">Kontrollkästchen "Fenster" Vorschau "nicht anzeigen" hinzugefügt</span><span class="sxs-lookup"><span data-stu-id="bab9c-122">Added 'Do not show preview window' checkbox</span></span>](https://github.com/NuGet/Home/issues/566)
* [<span data-ttu-id="bab9c-123">Hinzugefügte Prozess Drosselung, um die prozessorauslastung zu reduzieren.</span><span class="sxs-lookup"><span data-stu-id="bab9c-123">Added process throttling to reduce processor usage</span></span>](https://github.com/NuGet/Home/issues/356)
* <span data-ttu-id="bab9c-124">Verbesserte Behandlung der Referenz zur portablen Klassenbibliothek</span><span class="sxs-lookup"><span data-stu-id="bab9c-124">Improved portable-class-library reference handling</span></span>
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [<span data-ttu-id="bab9c-125">AutoVervollständigen-Dienst konnte die Groß-/Kleinschreibung beachten</span><span class="sxs-lookup"><span data-stu-id="bab9c-125">Autocomplete service was case sensitive</span></span>](https://github.com/NuGet/Home/issues/198)
* [<span data-ttu-id="bab9c-126">Aktualisiert werden, um die Anmeldeinformationen für Standardauthentifizierung Rückmeldung</span><span class="sxs-lookup"><span data-stu-id="bab9c-126">Update to reintroduce basic auth credentials</span></span>](https://github.com/NuGet/Home/issues/456)
* [<span data-ttu-id="bab9c-127">Verbessertes Fehlerprotokoll</span><span class="sxs-lookup"><span data-stu-id="bab9c-127">Improved error logging</span></span>](https://github.com/NuGet/Home/issues/407)
* [<span data-ttu-id="bab9c-128">Verbesserte Powershell Fehlermeldungen beim Aufrufen des Update-Package</span><span class="sxs-lookup"><span data-stu-id="bab9c-128">Improved powershell error messages when calling Update-Package</span></span>](https://github.com/NuGet/Home/issues/5)
* [<span data-ttu-id="bab9c-129">Korrigiert den "Erfahren Sie mehr zu den Optionen"-Link, um zu vermeiden, stürzt ab, unter Windows 10</span><span class="sxs-lookup"><span data-stu-id="bab9c-129">Fixed the 'Learn about Options' link to prevent crashing on Windows 10</span></span>](https://github.com/NuGet/Home/issues/822)
* [<span data-ttu-id="bab9c-130">Beachten Sie die Vorabversion Kontrollkästchen-Einstellung</span><span class="sxs-lookup"><span data-stu-id="bab9c-130">Remember pre-release checkbox setting</span></span>](https://github.com/NuGet/Home/issues/732)
* [<span data-ttu-id="bab9c-131">Verbesserte Gather-Leistung durch Zwischenspeichern der Ergebnisse für Projekte in einer Projektmappe</span><span class="sxs-lookup"><span data-stu-id="bab9c-131">Improved gather performance by caching results across projects in a solution</span></span>](https://github.com/NuGet/Home/issues/721)
* [<span data-ttu-id="bab9c-132">Mehrere Pakete können gleichzeitig gesammelt werden</span><span class="sxs-lookup"><span data-stu-id="bab9c-132">Multiple Packages can be gathered in parallel</span></span>](https://github.com/NuGet/Home/issues/713)
* [<span data-ttu-id="bab9c-133">Entfernt die Install-Package-Befehls erzwingen</span><span class="sxs-lookup"><span data-stu-id="bab9c-133">Removed install-package -force command</span></span>](https://github.com/NuGet/Home/issues/697)

<span data-ttu-id="bab9c-134">Bitte achten Sie auf [unseren Blog](http://blog.nuget.org) weitere Bearbeitung und Ankündigungen, da wir für die Unterstützung für Windows 10-Entwicklung vorzubereiten.</span><span class="sxs-lookup"><span data-stu-id="bab9c-134">Please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements as we get ready to deliver support for Windows 10 development.</span></span>