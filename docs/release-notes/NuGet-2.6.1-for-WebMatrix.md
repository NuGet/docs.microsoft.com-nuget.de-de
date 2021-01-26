---
title: Anmerkungen zu dieser Version von nuget 2.6.1 für webmatrix
description: Anmerkungen zu dieser Version von nuget 2.6.1 für webmatrix einschließlich bekannter Probleme, Fehlerbehebungen, hinzugefügter Features und dcrs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: de568829efd5060f3b02c3129ccfee2b27782821
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780424"
---
# <a name="nuget-261-for-webmatrix-release-notes"></a><span data-ttu-id="9a9dc-103">Anmerkungen zu dieser Version von nuget 2.6.1 für webmatrix</span><span class="sxs-lookup"><span data-stu-id="9a9dc-103">NuGet 2.6.1 for WebMatrix Release Notes</span></span>

<span data-ttu-id="9a9dc-104">Anmerkungen zu dieser [Version von nuget 2,6](../release-notes/nuget-2.6.md)  |  [Anmerkungen zu dieser Version von nuget 2,7](../release-notes/nuget-2.7.md)</span><span class="sxs-lookup"><span data-stu-id="9a9dc-104">[NuGet 2.6 Release Notes](../release-notes/nuget-2.6.md) | [NuGet 2.7 Release Notes](../release-notes/nuget-2.7.md)</span></span>

<span data-ttu-id="9a9dc-105">Das nuget-Team hat am 26. März 2014 eine aktualisierte nuget-Paket-Manager-Erweiterung für webmatrix veröffentlicht.</span><span class="sxs-lookup"><span data-stu-id="9a9dc-105">The NuGet team released an updated NuGet Package Manager extension for WebMatrix on March 26, 2014.</span></span>  <span data-ttu-id="9a9dc-106">Dieses Update kann mithilfe der folgenden Schritte aus dem [webmatrix-Erweiterungs](https://blogs.iis.net/webmatrix/retiring-the-webmatrix-extensions-gallery) Katalog installiert werden:</span><span class="sxs-lookup"><span data-stu-id="9a9dc-106">This update can be installed from the [WebMatrix Extension Gallery](https://blogs.iis.net/webmatrix/retiring-the-webmatrix-extensions-gallery) using the following steps:</span></span>

1. <span data-ttu-id="9a9dc-107">Webmatrix 3 Öffnen</span><span class="sxs-lookup"><span data-stu-id="9a9dc-107">Open WebMatrix 3</span></span>
1. <span data-ttu-id="9a9dc-108">Klicken Sie im Menüband Start auf das Symbol Erweiterungen.</span><span class="sxs-lookup"><span data-stu-id="9a9dc-108">Click the Extensions icon in the Home ribbon</span></span>
1. <span data-ttu-id="9a9dc-109">Registerkarte "Updates" auswählen</span><span class="sxs-lookup"><span data-stu-id="9a9dc-109">Select the Updates tab</span></span>
1. <span data-ttu-id="9a9dc-110">Klicken Sie, um den nuget-Paket-Manager zu 2.6.1</span><span class="sxs-lookup"><span data-stu-id="9a9dc-110">Click to update NuGet Package Manager to 2.6.1</span></span>
1. <span data-ttu-id="9a9dc-111">Schließen und Neustarten von webmatrix 3</span><span class="sxs-lookup"><span data-stu-id="9a9dc-111">Close and restart WebMatrix 3</span></span>

## <a name="notable-changes"></a><span data-ttu-id="9a9dc-112">Wichtige Änderungen</span><span class="sxs-lookup"><span data-stu-id="9a9dc-112">Notable Changes</span></span>

<span data-ttu-id="9a9dc-113">Dieses Erweiterungs Update bezieht sich auf zwei der größten Probleme, die Benutzern bei der Nutzung von nuget-Paketen in webmatrix ausgesetzt waren.</span><span class="sxs-lookup"><span data-stu-id="9a9dc-113">This extension update addresses two of the biggest issues users have faced consuming NuGet packages within WebMatrix.</span></span>  <span data-ttu-id="9a9dc-114">Der erste war ein Fehler in der nuget-Schema Version, und der zweite war ein Fehler, der zu 0-Byte-DLLs im `bin` Ordner führte.</span><span class="sxs-lookup"><span data-stu-id="9a9dc-114">The first was a NuGet schema version error and the second was a bug leading to zero-byte DLLs in the `bin` folder.</span></span>

### <a name="nuget-schema-version-error"></a><span data-ttu-id="9a9dc-115">Fehler bei der nuget-Schema Version</span><span class="sxs-lookup"><span data-stu-id="9a9dc-115">NuGet Schema Version Error</span></span>

<span data-ttu-id="9a9dc-116">Seit der Veröffentlichung von webmatrix 3 wurden neue Features in nuget eingeführt, die eine neue Schema Version für die nuget-Pakete erfordern.</span><span class="sxs-lookup"><span data-stu-id="9a9dc-116">Since WebMatrix 3 was released, new features have been introduced into NuGet that require a new schema version for the NuGet packages.</span></span>  <span data-ttu-id="9a9dc-117">Wenn Sie versuchen, ihre nuget-Pakete auf Ihrer Website zu verwalten, können diese neuen Pakete zu Fehlern führen, die in webmatrix angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="9a9dc-117">When trying to manage your NuGet packages in your web site, these new packages can lead to errors that you see in WebMatrix.</span></span>

![Ein Fehler ist aufgetreten.](./media/NuGet-2.8/webmatrix-schema-version.png)

<span data-ttu-id="9a9dc-121">Diese neueste Version bietet Kompatibilität mit den neuesten nuget-Paketen, wodurch dieser Fehler nicht mehr auftritt.</span><span class="sxs-lookup"><span data-stu-id="9a9dc-121">This latest release provides compatibility with the newest NuGet packages, preventing this error from occurring.</span></span> <span data-ttu-id="9a9dc-122">Neue Versionen von Paketen einschließlich Microsoft. Aspnet. Webseiten können jetzt in webmatrix installiert werden.</span><span class="sxs-lookup"><span data-stu-id="9a9dc-122">New versions of packages including Microsoft.AspNet.WebPages can now be installed in WebMatrix.</span></span>  <span data-ttu-id="9a9dc-123">Einige dieser Pakete verwendeten nuget-Features, wie z. b. [xdt-Konfigurations Transformationen](../release-notes/nuget-2.6.md#xdt), die bisher in webmatrix nicht unterstützt wurden.</span><span class="sxs-lookup"><span data-stu-id="9a9dc-123">Some of these packages were using NuGet features such as [XDT config transforms](../release-notes/nuget-2.6.md#xdt), which wasn't supported in WebMatrix until now.</span></span>

### <a name="zero-byte-dlls-in-bin-folder"></a><span data-ttu-id="9a9dc-124">Zero-Byte DLLs im Ordner "bin"</span><span class="sxs-lookup"><span data-stu-id="9a9dc-124">Zero-Byte DLLs in bin Folder</span></span>

<span data-ttu-id="9a9dc-125">Einige Benutzer haben gemeldet, dass die DLLs nach der Installation von nuget-Paketen in webmatrix, die DLLs enthalten, die in bin kopiert werden, `bin` als 0-Byte-Dateien im Ordner angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="9a9dc-125">Some users have reported that after installing NuGet packages in WebMatrix that include DLLs that get copied to bin, that the DLLs show up in the `bin` folder as 0-byte files.</span></span>  <span data-ttu-id="9a9dc-126">Dadurch wird die Anwendung zur Laufzeit unterbrochen.</span><span class="sxs-lookup"><span data-stu-id="9a9dc-126">This breaks the application at runtime.</span></span>

<span data-ttu-id="9a9dc-127">[Dieses Problem](https://nuget.codeplex.com/workitem/4060) wurde jetzt behoben.</span><span class="sxs-lookup"><span data-stu-id="9a9dc-127">[This issue](https://nuget.codeplex.com/workitem/4060) has now been fixed.</span></span>

## <a name="other-recent-improvements"></a><span data-ttu-id="9a9dc-128">Weitere aktuelle Verbesserungen</span><span class="sxs-lookup"><span data-stu-id="9a9dc-128">Other Recent Improvements</span></span>

<span data-ttu-id="9a9dc-129">Als der nuget-Paket-Manager 2,8 für Visual Studio freigegeben wurde, haben wir auch den nuget-Paket-Manager 2.5.0 für webmatrix veröffentlicht.</span><span class="sxs-lookup"><span data-stu-id="9a9dc-129">When NuGet Package Manager 2.8 was released for Visual Studio, we also released NuGet Package Manager 2.5.0 for WebMatrix.</span></span>  <span data-ttu-id="9a9dc-130">Obwohl dies in den Anmerkungen zu dieser [Version von nuget 2,8](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates)erwähnt wurde, haben wir die neuen Features, die von Update eingeführt wurden, nicht erwähnt.</span><span class="sxs-lookup"><span data-stu-id="9a9dc-130">While this was mentioned in the [NuGet 2.8 Release Notes](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates), we didn't mention the specific new features that update introduced.</span></span>

### <a name="update-all"></a><span data-ttu-id="9a9dc-131">Alle aktualisieren</span><span class="sxs-lookup"><span data-stu-id="9a9dc-131">Update All</span></span>

<span data-ttu-id="9a9dc-132">Sie können jetzt alle Pakete Ihrer Website in einem Schritt aktualisieren!</span><span class="sxs-lookup"><span data-stu-id="9a9dc-132">You can now update all of your web site's packages in one step!</span></span>  <span data-ttu-id="9a9dc-133">Wenn Sie die nuget-Erweiterung in webmatrix öffnen, sehen Sie die Liste aller Pakete im Katalog, die installiert und die Updates, die verfügbar sind.</span><span class="sxs-lookup"><span data-stu-id="9a9dc-133">When you open the NuGet extension in WebMatrix, you see the list of all packages on the gallery, those installed, and the ones with updates available.</span></span>  <span data-ttu-id="9a9dc-134">Zuvor musste jedes Paket einzeln aktualisiert werden, aber jetzt gibt es eine nützliche Schaltfläche "Alle aktualisieren", die auf der Registerkarte "Updates" angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="9a9dc-134">Previously, every package would have to be updated individually but now there is a useful "Update All" button that shows up on the Updates tab.</span></span>

![Klicken Sie auf alle aktualisieren, um alle Pakete mit verfügbaren Updates zu aktualisieren](./media/NuGet-2.8/webmatrix-update-all.png)

### <a name="overwrite-existing-files"></a><span data-ttu-id="9a9dc-136">Vorhandene Dateien überschreiben</span><span class="sxs-lookup"><span data-stu-id="9a9dc-136">Overwrite Existing Files</span></span>

<span data-ttu-id="9a9dc-137">Wenn Sie Pakete installieren, die bereits auf der Website vorhandene Dateien enthalten, ignoriert nuget diese Dateien immer im Hintergrund (wobei die vorhandenen Dateien unverändert geblieben sind).</span><span class="sxs-lookup"><span data-stu-id="9a9dc-137">When installing packages that contain files that already exist in your web site, NuGet has always just silently ignored those files (leaving your existing files alone).</span></span>  <span data-ttu-id="9a9dc-138">Dies könnte dazu führen, dass ein Paket ordnungsgemäß installiert oder aktualisiert wurde, wenn dies nicht der Fall war.</span><span class="sxs-lookup"><span data-stu-id="9a9dc-138">This could lead to the impression that a package was installed or updated correctly when in fact it wasn't.</span></span>  <span data-ttu-id="9a9dc-139">Nuget wird jetzt aufgefordert, Dateien zu überschreiben.</span><span class="sxs-lookup"><span data-stu-id="9a9dc-139">NuGet will now prompt for files to be overwritten.</span></span>

![Auflösung von Dateikonflikten](./media/NuGet-2.8/webmatrix-overwrite-file.png)
