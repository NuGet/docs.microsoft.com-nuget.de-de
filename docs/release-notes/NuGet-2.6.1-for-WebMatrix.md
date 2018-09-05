---
title: NuGet 2.6.1 für WebMatrix-Versionshinweise
description: Anmerkungen zu NuGet 2.6.1 für WebMatrix, einschließlich der bekannten Probleme, Fehlerkorrekturen, hinzugefügter Features und DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 10d80a921cbc34b537f91644da97efc44530fa75
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550316"
---
# <a name="nuget-261-for-webmatrix-release-notes"></a><span data-ttu-id="048a2-103">NuGet 2.6.1 für WebMatrix-Versionshinweise</span><span class="sxs-lookup"><span data-stu-id="048a2-103">NuGet 2.6.1 for WebMatrix Release Notes</span></span>

<span data-ttu-id="048a2-104">[Anmerkungen zu NuGet 2.6](../release-notes/nuget-2.6.md) | [Anmerkungen zu NuGet 2.7](../release-notes/nuget-2.7.md)</span><span class="sxs-lookup"><span data-stu-id="048a2-104">[NuGet 2.6 Release Notes](../release-notes/nuget-2.6.md) | [NuGet 2.7 Release Notes](../release-notes/nuget-2.7.md)</span></span>

<span data-ttu-id="048a2-105">Das NuGet-Team hat eine aktualisierte NuGet-Paket-Manager-Erweiterung für WebMatrix 26 März 2014 veröffentlicht.</span><span class="sxs-lookup"><span data-stu-id="048a2-105">The NuGet team released an updated NuGet Package Manager extension for WebMatrix on March 26, 2014.</span></span>  <span data-ttu-id="048a2-106">Dieses Update installiert werden kann, aus der [WebMatrix-Erweiterungskatalog](https://blogs.iis.net/webmatrix/retiring-the-webmatrix-extensions-gallery) verwenden die folgenden Schritte aus:</span><span class="sxs-lookup"><span data-stu-id="048a2-106">This update can be installed from the [WebMatrix Extension Gallery](https://blogs.iis.net/webmatrix/retiring-the-webmatrix-extensions-gallery) using the following steps:</span></span>

1. <span data-ttu-id="048a2-107">Öffnen Sie WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="048a2-107">Open WebMatrix 3</span></span>
1. <span data-ttu-id="048a2-108">Klicken Sie auf das Symbol "Erweiterungen" im Menüband "Start"</span><span class="sxs-lookup"><span data-stu-id="048a2-108">Click the Extensions icon in the Home ribbon</span></span>
1. <span data-ttu-id="048a2-109">Wählen Sie die Registerkarte "Updates"</span><span class="sxs-lookup"><span data-stu-id="048a2-109">Select the Updates tab</span></span>
1. <span data-ttu-id="048a2-110">Klicken Sie auf, um NuGet-Paket-Manager auf 2.6.1 zu aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="048a2-110">Click to update NuGet Package Manager to 2.6.1</span></span>
1. <span data-ttu-id="048a2-111">Schließen Sie und starten Sie WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="048a2-111">Close and restart WebMatrix 3</span></span>

## <a name="notable-changes"></a><span data-ttu-id="048a2-112">Wichtige Änderungen</span><span class="sxs-lookup"><span data-stu-id="048a2-112">Notable Changes</span></span>

<span data-ttu-id="048a2-113">Diese Erweiterung Update behandelt zwei der größten Probleme Benutzer haben verwendeten NuGet-Pakete in WebMatrix konfrontiert.</span><span class="sxs-lookup"><span data-stu-id="048a2-113">This extension update addresses two of the biggest issues users have faced consuming NuGet packages within WebMatrix.</span></span>  <span data-ttu-id="048a2-114">Die erste war ein NuGet-Schemafehler Version und das zweite ein Fehler auf 0 (null)-Byte-DLLs in führenden der `bin` Ordner.</span><span class="sxs-lookup"><span data-stu-id="048a2-114">The first was a NuGet schema version error and the second was a bug leading to zero-byte DLLs in the `bin` folder.</span></span>

### <a name="nuget-schema-version-error"></a><span data-ttu-id="048a2-115">Fehler beim Version des NuGet-Schemas</span><span class="sxs-lookup"><span data-stu-id="048a2-115">NuGet Schema Version Error</span></span>

<span data-ttu-id="048a2-116">Da WebMatrix 3 veröffentlicht wurde, wurden neue Features in NuGet, die eine neue Schemaversion für die NuGet-Pakete erfordern eingeführt.</span><span class="sxs-lookup"><span data-stu-id="048a2-116">Since WebMatrix 3 was released, new features have been introduced into NuGet that require a new schema version for the NuGet packages.</span></span>  <span data-ttu-id="048a2-117">Beim Versuch, Ihr NuGet-Pakete in Ihre Website zu verwalten, können diese neue Pakete zu Fehlern führen, die Sie in WebMatrix zu sehen.</span><span class="sxs-lookup"><span data-stu-id="048a2-117">When trying to manage your NuGet packages in your web site, these new packages can lead to errors that you see in WebMatrix.</span></span>

![Es ist ein Fehler aufgetreten.](./media/NuGet-2.8/webmatrix-schema-version.png)

<span data-ttu-id="048a2-121">Dieses neueste Release bietet Kompatibilität mit den neuesten NuGet-Pakete, die verhindert, dass dieser Fehler auftritt.</span><span class="sxs-lookup"><span data-stu-id="048a2-121">This latest release provides compatibility with the newest NuGet packages, preventing this error from occurring.</span></span> <span data-ttu-id="048a2-122">Neue Versionen der Pakete einschließlich Microsoft.AspNet.WebPages können jetzt in WebMatrix installiert werden.</span><span class="sxs-lookup"><span data-stu-id="048a2-122">New versions of packages including Microsoft.AspNet.WebPages can now be installed in WebMatrix.</span></span>  <span data-ttu-id="048a2-123">Einige dieser Pakete wurden mithilfe von NuGet-Features wie [XDT Konfigurationstransformationen](../release-notes/nuget-2.6.md#xdt), dies war nicht in WebMatrix unterstützt, bis jetzt.</span><span class="sxs-lookup"><span data-stu-id="048a2-123">Some of these packages were using NuGet features such as [XDT config transforms](../release-notes/nuget-2.6.md#xdt), which wasn't supported in WebMatrix until now.</span></span>

### <a name="zero-byte-dlls-in-bin-folder"></a><span data-ttu-id="048a2-124">0-Byte-DLLs im Ordner "bin" "</span><span class="sxs-lookup"><span data-stu-id="048a2-124">Zero-Byte DLLs in bin Folder</span></span>

<span data-ttu-id="048a2-125">Einige Benutzer haben gemeldet, dass nach dem Installieren von NuGet Pakete Sie in WebMatrix, die DLLs enthalten, die kopiert werden, in den Papierkorb, die die DLLs zeigen die `bin` Ordner Dateien mit 0 Byte.</span><span class="sxs-lookup"><span data-stu-id="048a2-125">Some users have reported that after installing NuGet packages in WebMatrix that include DLLs that get copied to bin, that the DLLs show up in the `bin` folder as 0-byte files.</span></span>  <span data-ttu-id="048a2-126">Dies unterbricht die Anwendung zur Laufzeit.</span><span class="sxs-lookup"><span data-stu-id="048a2-126">This breaks the application at runtime.</span></span>

<span data-ttu-id="048a2-127">[Dieses Problem](https://nuget.codeplex.com/workitem/4060) hat sich geändert.</span><span class="sxs-lookup"><span data-stu-id="048a2-127">[This issue](https://nuget.codeplex.com/workitem/4060) has now been fixed.</span></span>

## <a name="other-recent-improvements"></a><span data-ttu-id="048a2-128">Weitere Verbesserungen</span><span class="sxs-lookup"><span data-stu-id="048a2-128">Other Recent Improvements</span></span>

<span data-ttu-id="048a2-129">Als NuGet-Paket-Manager 2.8 für Visual Studio veröffentlicht wurde, veröffentlicht haben wir auch NuGet Package Manager 2.5.0 für WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="048a2-129">When NuGet Package Manager 2.8 was released for Visual Studio, we also released NuGet Package Manager 2.5.0 for WebMatrix.</span></span>  <span data-ttu-id="048a2-130">Während dies im erwähnt wurde die [NuGet 2.8 Release Notes](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates), wir jedoch nicht erwähnt die spezifischen neue Funktionen, die Updates eingeführt wurden.</span><span class="sxs-lookup"><span data-stu-id="048a2-130">While this was mentioned in the [NuGet 2.8 Release Notes](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates), we didn't mention the specific new features that update introduced.</span></span>

### <a name="update-all"></a><span data-ttu-id="048a2-131">Alle aktualisieren</span><span class="sxs-lookup"><span data-stu-id="048a2-131">Update All</span></span>

<span data-ttu-id="048a2-132">Sie können alle Pakete von der Website in einem Schritt jetzt aktualisieren!</span><span class="sxs-lookup"><span data-stu-id="048a2-132">You can now update all of your web site's packages in one step!</span></span>  <span data-ttu-id="048a2-133">Wenn Sie die NuGet-Erweiterung in WebMatrix öffnen, sehen Sie die Liste aller Pakete auf den Katalog, die installiert und diejenigen mit verfügbaren Updates.</span><span class="sxs-lookup"><span data-stu-id="048a2-133">When you open the NuGet extension in WebMatrix, you see the list of all packages on the gallery, those installed, and the ones with updates available.</span></span>  <span data-ttu-id="048a2-134">Früher jedes Paket einzeln aktualisiert werden müsste, aber jetzt befindet sich eine nützliche "Alle aktualisieren"-Schaltfläche, die auf der Registerkarte "Updates" wird angezeigt.</span><span class="sxs-lookup"><span data-stu-id="048a2-134">Previously, every package would have to be updated individually but now there is a useful "Update All" button that shows up on the Updates tab.</span></span>

![Klicken Sie auf "Alle aktualisieren", um alle Pakete mit verfügbaren Updates zu aktualisieren.](./media/NuGet-2.8/webmatrix-update-all.png)

### <a name="overwrite-existing-files"></a><span data-ttu-id="048a2-136">Vorhandene Dateien überschreiben</span><span class="sxs-lookup"><span data-stu-id="048a2-136">Overwrite Existing Files</span></span>

<span data-ttu-id="048a2-137">Beim Installieren von Paketen, die Dateien enthalten, die auf der Website bereits vorhanden sind, hat NuGet immer nur diese Dateien (vorhandenen Dateien allein verlassen) ignoriert.</span><span class="sxs-lookup"><span data-stu-id="048a2-137">When installing packages that contain files that already exist in your web site, NuGet has always just silently ignored those files (leaving your existing files alone).</span></span>  <span data-ttu-id="048a2-138">Dies kann auf den Eindruck führen, dass ein Paket installiert wurde oder wenn in der Tat es war nicht korrekt aktualisiert.</span><span class="sxs-lookup"><span data-stu-id="048a2-138">This could lead to the impression that a package was installed or updated correctly when in fact it wasn't.</span></span>  <span data-ttu-id="048a2-139">NuGet fordert nun Dateien überschrieben werden sollen.</span><span class="sxs-lookup"><span data-stu-id="048a2-139">NuGet will now prompt for files to be overwritten.</span></span>

![Lösung von Konflikten](./media/NuGet-2.8/webmatrix-overwrite-file.png)
