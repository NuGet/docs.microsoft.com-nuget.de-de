---
title: NuGet 2.6.1 WebMatrix Versionshinweise | Microsoft Docs
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 119ea65b-b38b-4a8c-a4ed-6ea06f1aad09
description: "Versionshinweise für NuGet 2.6.1 für WebMatrix, einschließlich der bekannten Probleme, Fehlerbehebungen, Funktionen und Archivierung von dcrs Design."
keywords: "NuGet 2.6.1 für WebMatrix-Versionshinweise, Fehlerbehebungen, bekannten Problemen, die zusätzliche Funktionen, Archivierung von dcrs Design"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 9c37ddc998378b8aaa477dd5df814bab6f0b3c58
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-261-for-webmatrix-release-notes"></a><span data-ttu-id="aa238-104">NuGet 2.6.1 WebMatrix-Versionshinweise</span><span class="sxs-lookup"><span data-stu-id="aa238-104">NuGet 2.6.1 for WebMatrix Release Notes</span></span>

<span data-ttu-id="aa238-105">[Anmerkungen zur Version des NuGet-2.6](../release-notes/nuget-2.6.md) | [NuGet 2.7-Versionshinweise](../release-notes/nuget-2.7.md)</span><span class="sxs-lookup"><span data-stu-id="aa238-105">[NuGet 2.6 Release Notes](../release-notes/nuget-2.6.md) | [NuGet 2.7 Release Notes](../release-notes/nuget-2.7.md)</span></span>

<span data-ttu-id="aa238-106">Das NuGet-Team hat eine aktualisierte NuGet-Paket-Manager-Erweiterung für WebMatrix 26 März 2014 veröffentlicht.</span><span class="sxs-lookup"><span data-stu-id="aa238-106">The NuGet team released an updated NuGet Package Manager extension for WebMatrix on March 26, 2014.</span></span>  <span data-ttu-id="aa238-107">Dieses Update installiert werden kann, aus der [WebMatrix Erweiterungskatalog](http://extensions.webmatrix.com/packages/NuGetPackageManager/) mithilfe der folgenden Schritte:</span><span class="sxs-lookup"><span data-stu-id="aa238-107">This update can be installed from the [WebMatrix Extension Gallery](http://extensions.webmatrix.com/packages/NuGetPackageManager/) using the following steps:</span></span>

1. <span data-ttu-id="aa238-108">Öffnen Sie WebMatrix 3</span><span class="sxs-lookup"><span data-stu-id="aa238-108">Open WebMatrix 3</span></span>
2. <span data-ttu-id="aa238-109">Klicken Sie auf das Symbol "Erweiterungen" im Menüband Home</span><span class="sxs-lookup"><span data-stu-id="aa238-109">Click the Extensions icon in the Home ribbon</span></span>
3. <span data-ttu-id="aa238-110">Wählen Sie die Registerkarte "Softwareupdates"</span><span class="sxs-lookup"><span data-stu-id="aa238-110">Select the Updates tab</span></span>
4. <span data-ttu-id="aa238-111">Klicken Sie auf, um NuGet-Paket-Manager auf 2.6.1 zu aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="aa238-111">Click to update NuGet Package Manager to 2.6.1</span></span>
6. <span data-ttu-id="aa238-112">Schließen Sie, und starten Sie die WebMatrix-3</span><span class="sxs-lookup"><span data-stu-id="aa238-112">Close and restart WebMatrix 3</span></span>

## <a name="notable-changes"></a><span data-ttu-id="aa238-113">Wichtige Änderungen</span><span class="sxs-lookup"><span data-stu-id="aa238-113">Notable Changes</span></span>

<span data-ttu-id="aa238-114">Diese Erweiterung behebt zwei der größten Probleme Benutzer haben verbrauchende NuGet-Pakete in WebMatrix Datenwachstums.</span><span class="sxs-lookup"><span data-stu-id="aa238-114">This extension update addresses two of the biggest issues users have faced consuming NuGet packages within WebMatrix.</span></span>  <span data-ttu-id="aa238-115">Das erste ist ein NuGet-Schema-Version-Fehler und die zweite wurde ein Fehler auf 0 Byte-DLLs in führenden der `bin` Ordner.</span><span class="sxs-lookup"><span data-stu-id="aa238-115">The first was a NuGet schema version error and the second was a bug leading to zero-byte DLLs in the `bin` folder.</span></span>

### <a name="nuget-schema-version-error"></a><span data-ttu-id="aa238-116">NuGet-Version Schemafehler</span><span class="sxs-lookup"><span data-stu-id="aa238-116">NuGet Schema Version Error</span></span>

<span data-ttu-id="aa238-117">Seit der Freigabe von WebMatrix 3 wurden neue Funktionen eingeführt in NuGet, die eine neue Version des Datenbankschemas für die NuGet-Pakete erfordern.</span><span class="sxs-lookup"><span data-stu-id="aa238-117">Since WebMatrix 3 was released, new features have been introduced into NuGet that require a new schema version for the NuGet packages.</span></span>  <span data-ttu-id="aa238-118">Beim Versuch, die NuGet-Pakete auf der Website zu verwalten, können diese neue Pakete zu Fehlern führen, die Sie in WebMatrix sehen.</span><span class="sxs-lookup"><span data-stu-id="aa238-118">When trying to manage your NuGet packages in your web site, these new packages can lead to errors that you'll see in WebMatrix.</span></span>

![Es ist ein Fehler aufgetreten.](./media/NuGet-2.8/webmatrix-schema-version.png)

<span data-ttu-id="aa238-122">Diese neueste Version bietet Kompatibilität mit den neuesten NuGet-Pakete verhindern, dass dieser Fehler auftritt.</span><span class="sxs-lookup"><span data-stu-id="aa238-122">This latest release provides compatibility with the newest NuGet packages, preventing this error from occurring.</span></span> <span data-ttu-id="aa238-123">Neue Versionen der Pakete, einschließlich Microsoft.AspNet.WebPages können jetzt in WebMatrix installiert werden.</span><span class="sxs-lookup"><span data-stu-id="aa238-123">New versions of packages including Microsoft.AspNet.WebPages can now be installed in WebMatrix.</span></span>  <span data-ttu-id="aa238-124">Einige dieser Pakete wurden mithilfe von NuGet-Funktionen wie [XDT Config transformiert](../release-notes/nuget-2.6.md#xdt), dies wurde nicht in WebMatrix unterstützt, die bisher.</span><span class="sxs-lookup"><span data-stu-id="aa238-124">Some of these packages were using NuGet features such as [XDT config transforms](../release-notes/nuget-2.6.md#xdt), which wasn't supported in WebMatrix until now.</span></span>

### <a name="zero-byte-dlls-in-bin-folder"></a><span data-ttu-id="aa238-125">0 Byte-DLLs im Ordner "bin" "</span><span class="sxs-lookup"><span data-stu-id="aa238-125">Zero-Byte DLLs in bin Folder</span></span>

<span data-ttu-id="aa238-126">Einige Benutzer haben gemeldet, dass nach dem Installieren von NuGet Pakete einrichten in WebMatrix mit DLLs, die kopiert werden, um zu klassifizieren, die DLLs zum Anzeigen der `bin` Ordner als 0-Byte-Dateien.</span><span class="sxs-lookup"><span data-stu-id="aa238-126">Some users have reported that after installing NuGet packages in WebMatrix that include DLLs that get copied to bin, that the DLLs show up in the `bin` folder as 0-byte files.</span></span>  <span data-ttu-id="aa238-127">Dieser Vorgang ist die Anwendung zur Laufzeit.</span><span class="sxs-lookup"><span data-stu-id="aa238-127">This breaks the application at runtime.</span></span>

<span data-ttu-id="aa238-128">[Dieses Problem](https://nuget.codeplex.com/workitem/4060) wurde jetzt behoben.</span><span class="sxs-lookup"><span data-stu-id="aa238-128">[This issue](https://nuget.codeplex.com/workitem/4060) has now been fixed.</span></span>

## <a name="other-recent-improvements"></a><span data-ttu-id="aa238-129">Weitere Verbesserungen</span><span class="sxs-lookup"><span data-stu-id="aa238-129">Other Recent Improvements</span></span>

<span data-ttu-id="aa238-130">NuGet-Paket-Manager 2.8 für Visual Studio veröffentlicht wurde, veröffentlicht haben wir auch NuGet Package Manager 2.5.0 für WebMatrix.</span><span class="sxs-lookup"><span data-stu-id="aa238-130">When NuGet Package Manager 2.8 was released for Visual Studio, we also released NuGet Package Manager 2.5.0 for WebMatrix.</span></span>  <span data-ttu-id="aa238-131">Während dies, in erwähnt wurde der [NuGet 2.8-Anmerkungen zu dieser Version](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates), haben nicht wir erwähnt, die spezifische neue Funktionen, die Updates eingeführt.</span><span class="sxs-lookup"><span data-stu-id="aa238-131">While this was mentioned in the [NuGet 2.8 Release Notes](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates), we didn't mention the specific new features that update introduced.</span></span>

### <a name="update-all"></a><span data-ttu-id="aa238-132">Alle aktualisieren</span><span class="sxs-lookup"><span data-stu-id="aa238-132">Update All</span></span>

<span data-ttu-id="aa238-133">Sie können alle Ihre Website-Pakete in einem Schritt jetzt aktualisieren!</span><span class="sxs-lookup"><span data-stu-id="aa238-133">You can now update all of your web site's packages in one step!</span></span>  <span data-ttu-id="aa238-134">Wenn Sie das NuGet-Erweiterung in WebMatrix öffnen, sehen Sie die Liste aller Pakete in der Galerie, installiert und die Beziehungen und Updates verfügbar.</span><span class="sxs-lookup"><span data-stu-id="aa238-134">When you open the NuGet extension in WebMatrix, you see the list of all packages on the gallery, those installed, and the ones with updates available.</span></span>  <span data-ttu-id="aa238-135">Zuvor jedes Paket müssten einzeln aktualisiert werden, aber jetzt besteht eine nützliche "Alle aktualisieren"-Schaltfläche, die auf der Registerkarte "Updates" wird angezeigt.</span><span class="sxs-lookup"><span data-stu-id="aa238-135">Previously, every package would have to be updated individually but now there is a useful "Update All" button that shows up on the Updates tab.</span></span>

![Klicken Sie auf "Alle aktualisieren", um alle Pakete mit verfügbaren Updates aktualisieren](./media/NuGet-2.8/webmatrix-update-all.png)

### <a name="overwrite-existing-files"></a><span data-ttu-id="aa238-137">Vorhandene Dateien überschreiben</span><span class="sxs-lookup"><span data-stu-id="aa238-137">Overwrite Existing Files</span></span>

<span data-ttu-id="aa238-138">Installieren von Paketen, die Dateien enthalten, die auf der Website bereits vorhanden sind, verfügt über NuGet immer nur im Hintergrund (vorhandenen Dateien allein verlassen) Dateien ignoriert.</span><span class="sxs-lookup"><span data-stu-id="aa238-138">When installing packages that contain files that already exist in your web site, NuGet has always just silently ignored those files (leaving your existing files alone).</span></span>  <span data-ttu-id="aa238-139">Dies kann auf den Eindruck führen, dass ein Paket installiert wurde oder wenn tatsächlich war nicht ordnungsgemäß aktualisiert.</span><span class="sxs-lookup"><span data-stu-id="aa238-139">This could lead to the impression that a package was installed or updated correctly when in fact it wasn't.</span></span>  <span data-ttu-id="aa238-140">NuGet fordert nun Dateien überschrieben werden sollen.</span><span class="sxs-lookup"><span data-stu-id="aa238-140">NuGet will now prompt for files to be overwritten.</span></span>

![Auflösung des Konflikts zwischen Datei](./media/NuGet-2.8/webmatrix-overwrite-file.png)
