---
title: NuGet-Version 3.0-Hinweise
description: Versionshinweise für NuGet 3.0.0 einschließlich bekannte Probleme, Fehlerbehebungen, Funktionen und Archivierung von dcrs Design.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 26236c2db0e1a6be9c660905db567d9ebbbbe377
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-30-release-notes"></a><span data-ttu-id="684ba-103">NuGet-Version 3.0-Hinweise</span><span class="sxs-lookup"><span data-stu-id="684ba-103">NuGet 3.0 Release Notes</span></span>

<span data-ttu-id="684ba-104">[Anmerkungen zur Version von NuGet 3.0 RC2](../release-notes/nuget-3.0-RC2.md) | [NuGet 3.1-Versionshinweise](../release-notes/nuget-3.1.md)</span><span class="sxs-lookup"><span data-stu-id="684ba-104">[NuGet 3.0 RC2 Release Notes](../release-notes/nuget-3.0-RC2.md) | [NuGet 3.1 Release Notes](../release-notes/nuget-3.1.md)</span></span>

<span data-ttu-id="684ba-105">NuGet-3.0 wurde auf dem 20. Juli 2015 als Erweiterung des Pakets in Visual Studio 2015 veröffentlicht.</span><span class="sxs-lookup"><span data-stu-id="684ba-105">NuGet 3.0 was released on July 20, 2015 as a bundle extension to Visual Studio 2015.</span></span> <span data-ttu-id="684ba-106">Wir abgelegt, damit die vollständige aktualisierte NuGet-3.0-Erfahrung für neue Visual Studio-Benutzer verfügbar wäre dieser Version von Visual Studio zu übermitteln.</span><span class="sxs-lookup"><span data-stu-id="684ba-106">We pushed to deliver this release with Visual Studio so that the complete updated NuGet 3.0 experience would be available for new Visual Studio users.</span></span> <span data-ttu-id="684ba-107">Diese Version des NuGet-Erweiterung ist nur für Visual Studio 2015 verfügbar.</span><span class="sxs-lookup"><span data-stu-id="684ba-107">This NuGet extension version is only available for Visual Studio 2015.</span></span>

<span data-ttu-id="684ba-108">Es wird empfohlen, die Entwickler mit Zugriff auf die Visual Studio Gallery-Update auf die neueste Version, die verfügbar ist, wie wir ein Update kurz nach der Veröffentlichung von Visual Studio 2015 veröffentlichen, die Unterstützung für die Entwicklung von Windows 10 enthält.</span><span class="sxs-lookup"><span data-stu-id="684ba-108">We recommend those developers that have access to the Visual Studio gallery update to the latest version that is available, as we are publishing an update shortly after the release of Visual Studio 2015 that contains support for Windows 10 development.</span></span>

<span data-ttu-id="684ba-109">Insgesamt, die wir geschlossen 240 Probleme in der Version 3.0, und Sie können überprüfen, die [vollständige Liste der Probleme auf GitHub](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed).</span><span class="sxs-lookup"><span data-stu-id="684ba-109">In total, we closed 240 issues in the 3.0 release, and you can review the [complete list of issues on GitHub](https://github.com/NuGet/Home/issues?q=milestone%3A3.0.0-RTM+is%3Aclosed).</span></span>

## <a name="known-issues"></a><span data-ttu-id="684ba-110">Bekannte Probleme</span><span class="sxs-lookup"><span data-stu-id="684ba-110">Known Issues</span></span>

<span data-ttu-id="684ba-111">Gab es eine Reihe bekannter Probleme, die im Lieferumfang dieser Version und alle diese Elemente sind in unserer geplanten 3.1-Version mit der Version von Windows 10 nach einer auf dem 29. Juli fest.</span><span class="sxs-lookup"><span data-stu-id="684ba-111">There were a number of known issues delivered with this release, and all of these items are fixed in our scheduled 3.1 release to coincide with the release of Windows 10 on July 29th.</span></span>  <span data-ttu-id="684ba-112">Sie können beim Aktualisieren Ihrer Visual Studio-Erweiterungs aus dem Katalog am oder nach diesem Datum dieser bekannten Probleme zu beheben.</span><span class="sxs-lookup"><span data-stu-id="684ba-112">You are able to update your Visual Studio extension from the gallery on or after that date to fix these known issues.</span></span>

*  <span data-ttu-id="684ba-113">Übersetzung ist nicht für die Bezeichnung "Nicht erneut anzeigen", auf das Vorschaufenster und die Bezeichnung "Autoren" im Fenster Beschreibung Paket bereitgestellt.</span><span class="sxs-lookup"><span data-stu-id="684ba-113">Translation is not provided for the "Do not show this again" label on the preview window and the "Authors" label in the package description window.</span></span>
*  <span data-ttu-id="684ba-114">Wenn Sie die Arbeiten an einem Projekt mithilfe von TFS Datenquellen, kann nicht NuGet der Paket-Manager-Benutzeroberfläche vorhanden, wenn die Datei "Nuget.Config" als schreibgeschützt gekennzeichnet ist.</span><span class="sxs-lookup"><span data-stu-id="684ba-114">When you working on a project by using TFS source control, NuGet cannot present the package manager user interface if the Nuget.Config file is marked as read-only.</span></span>
   * <span data-ttu-id="684ba-115">**Problemumgehung** sehen Sie sich die Datei von TFS.</span><span class="sxs-lookup"><span data-stu-id="684ba-115">**Workaround** Check out the file from TFS.</span></span>
*  <span data-ttu-id="684ba-116">Text in der gelbe "Restart-weißen Balken im NuGet Powershell-Fenster ist nicht sichtbar, wenn Sie die Visual Studio Design" dunkel "verwenden.</span><span class="sxs-lookup"><span data-stu-id="684ba-116">Text in the yellow "restart bar" in the NuGet Powershell window is not visible when you use the Visual Studio dark theme.</span></span>
   * <span data-ttu-id="684ba-117">**Problemumgehung** das helle Design von Visual Studio verwenden.</span><span class="sxs-lookup"><span data-stu-id="684ba-117">**Workaround** Use the Visual Studio light theme.</span></span>


## <a name="summary-of-top-issues-resolved"></a><span data-ttu-id="684ba-118">Zusammenfassung der wichtigsten Probleme behoben</span><span class="sxs-lookup"><span data-stu-id="684ba-118">Summary of top issues resolved</span></span>

* [<span data-ttu-id="684ba-119">Häufige Netzwerk Update Ruft auf, wenn die Paket-Manager-Fenster wird aktualisiert</span><span class="sxs-lookup"><span data-stu-id="684ba-119">Frequent network update calls when package manager window refreshes</span></span>](https://github.com/NuGet/Home/issues/515)
* [<span data-ttu-id="684ba-120">Führen Sie einen Bildlauf verzögert, wenn Ansicht ändern im Paket-Manager installiert werden.</span><span class="sxs-lookup"><span data-stu-id="684ba-120">Delayed scroll when changing to installed view in package manager</span></span>](https://github.com/NuGet/Home/issues/519)
* [<span data-ttu-id="684ba-121">Netzwerkaufrufe sollte in einem Hintergrundthread ausgeführt werden</span><span class="sxs-lookup"><span data-stu-id="684ba-121">Network calls should be run on a background thread</span></span>](https://github.com/NuGet/Home/issues/516)
* [<span data-ttu-id="684ba-122">Kontrollkästchen "Fenster" Preview "nicht anzeigen" hinzugefügt</span><span class="sxs-lookup"><span data-stu-id="684ba-122">Added 'Do not show preview window' checkbox</span></span>](https://github.com/NuGet/Home/issues/566)
* [<span data-ttu-id="684ba-123">Hinzugefügte Prozess Einschränkung zur prozessorauslastung zu reduzieren.</span><span class="sxs-lookup"><span data-stu-id="684ba-123">Added process throttling to reduce processor usage</span></span>](https://github.com/NuGet/Home/issues/356)
* <span data-ttu-id="684ba-124">Verbesserte Behandlung Portable Klassenbibliothek-Referenz</span><span class="sxs-lookup"><span data-stu-id="684ba-124">Improved portable-class-library reference handling</span></span>
    * [https://github.com/NuGet/Home/issues/562](https://github.com/NuGet/Home/issues/562)
    * [https://github.com/NuGet/Home/issues/454](https://github.com/NuGet/Home/issues/454)
    * [https://github.com/NuGet/Home/issues/440](https://github.com/NuGet/Home/issues/440)
* [<span data-ttu-id="684ba-125">AutoVervollständigen-Dienst entsprechend seiner Groß-/Kleinschreibung unterschieden</span><span class="sxs-lookup"><span data-stu-id="684ba-125">Autocomplete service was case sensitive</span></span>](https://github.com/NuGet/Home/issues/198)
* [<span data-ttu-id="684ba-126">Aktualisiert werden, um die Anmeldeinformationen für Standardauthentifizierung Rückmeldung</span><span class="sxs-lookup"><span data-stu-id="684ba-126">Update to reintroduce basic auth credentials</span></span>](https://github.com/NuGet/Home/issues/456)
* [<span data-ttu-id="684ba-127">Verbesserte fehlerprotokollierung</span><span class="sxs-lookup"><span data-stu-id="684ba-127">Improved error logging</span></span>](https://github.com/NuGet/Home/issues/407)
* [<span data-ttu-id="684ba-128">Verbesserte Powershell Fehlermeldungen beim Aufrufen von Update-Paket</span><span class="sxs-lookup"><span data-stu-id="684ba-128">Improved powershell error messages when calling Update-Package</span></span>](https://github.com/NuGet/Home/issues/5)
* [<span data-ttu-id="684ba-129">Korrigiert den Link "Weitere Informationen zu den Optionen", um zu verhindern, aber bei Windows 10</span><span class="sxs-lookup"><span data-stu-id="684ba-129">Fixed the 'Learn about Options' link to prevent crashing on Windows 10</span></span>](https://github.com/NuGet/Home/issues/822)
* [<span data-ttu-id="684ba-130">Denken Sie daran Vorabversion Checkbox-Einstellung</span><span class="sxs-lookup"><span data-stu-id="684ba-130">Remember pre-release checkbox setting</span></span>](https://github.com/NuGet/Home/issues/732)
* [<span data-ttu-id="684ba-131">Verbesserte Gather-Leistung durch Zwischenspeichern der Ergebnisse übergreifend über Projekte in einer Projektmappe</span><span class="sxs-lookup"><span data-stu-id="684ba-131">Improved gather performance by caching results across projects in a solution</span></span>](https://github.com/NuGet/Home/issues/721)
* [<span data-ttu-id="684ba-132">Gleichzeitig können mehrere Pakete erfasst werden</span><span class="sxs-lookup"><span data-stu-id="684ba-132">Multiple Packages can be gathered in parallel</span></span>](https://github.com/NuGet/Home/issues/713)
* [<span data-ttu-id="684ba-133">Install-Package entfernt-Befehl zu erzwingen</span><span class="sxs-lookup"><span data-stu-id="684ba-133">Removed install-package -force command</span></span>](https://github.com/NuGet/Home/issues/697)

<span data-ttu-id="684ba-134">Bitte achten Sie auf [unserem Blog](http://blog.nuget.org) weitere Bearbeitung und Ankündigungen wie wir bieten Unterstützung für die Entwicklung von Windows 10 bereiten.</span><span class="sxs-lookup"><span data-stu-id="684ba-134">Please keep an eye on [our blog](http://blog.nuget.org) for more progress and announcements as we get ready to deliver support for Windows 10 development.</span></span>