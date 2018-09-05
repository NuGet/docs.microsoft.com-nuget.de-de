---
title: Anmerkungen zu Version 2.9-RC von NuGet
description: Anmerkungen zu NuGet 2.9 RC, einschließlich der bekannten Probleme, Fehlerkorrekturen, hinzugefügter Features und DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 17c1c3a0c91928602aa47b5ba599faeac0424a4a
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548323"
---
# <a name="nuget-29-rc-release-notes"></a><span data-ttu-id="fbe96-103">Anmerkungen zu Version 2.9-RC von NuGet</span><span class="sxs-lookup"><span data-stu-id="fbe96-103">NuGet 2.9-RC Release Notes</span></span>

<span data-ttu-id="fbe96-104">[Anmerkungen zu NuGet 2.8.7](../release-notes/nuget-2.8.7.md) | [NuGet 3.0 Anmerkungen zur Vorschauversion](../release-notes/nuget-3.0-preview.md)</span><span class="sxs-lookup"><span data-stu-id="fbe96-104">[NuGet 2.8.7 Release Notes](../release-notes/nuget-2.8.7.md) | [NuGet 3.0 Preview Release Notes](../release-notes/nuget-3.0-preview.md)</span></span>

<span data-ttu-id="fbe96-105">NuGet 2.9 wurde am 10. September 2015 veröffentlicht, als Update für die 2.8.7 VSIX für Visual Studio 2012 und 2013.</span><span class="sxs-lookup"><span data-stu-id="fbe96-105">NuGet 2.9 was released September 10, 2015 as an update to the 2.8.7 VSIX for Visual Studio 2012 and 2013.</span></span>

### <a name="updates-in-this-release"></a><span data-ttu-id="fbe96-106">Updates in dieser Version</span><span class="sxs-lookup"><span data-stu-id="fbe96-106">Updates in this release</span></span>

* <span data-ttu-id="fbe96-107">Nachdem die Verarbeitung von Paketen wird übersprungen, wenn die enthaltenen `.nuspec` Dokument ist falsch formatiert: [PR8](https://github.com/NuGet/NuGet2/pull/8)</span><span class="sxs-lookup"><span data-stu-id="fbe96-107">Now skipping processing packages if their contained `.nuspec` document is malformed - [PR8](https://github.com/NuGet/NuGet2/pull/8)</span></span>
* <span data-ttu-id="fbe96-108">Korrigiert Multipartwebrequest Behandlung \r\n für Unix/Linux-Szenarien – [776](https://github.com/NuGet/Home/issues/776)</span><span class="sxs-lookup"><span data-stu-id="fbe96-108">Corrected multipartwebrequest handling of \r\n for Unix/Linux scenarios - [776](https://github.com/NuGet/Home/issues/776)</span></span>
* <span data-ttu-id="fbe96-109">Integration mit Buildereignisse in Visual Studio 2013 Community Edition - korrigiert [1180](https://github.com/NuGet/Home/issues/1180)</span><span class="sxs-lookup"><span data-stu-id="fbe96-109">Corrected integration with build events in Visual Studio 2013 Community edition - [1180](https://github.com/NuGet/Home/issues/1180)</span></span>


<span data-ttu-id="fbe96-110">Die vollständige Liste der Fixes in dieser Version finden Sie auf GitHub in der [2.8.8 Meilenstein](https://github.com/NuGet/Home/issues?q=milestone%3A2.8.8+is%3Aclosed)</span><span class="sxs-lookup"><span data-stu-id="fbe96-110">The complete list of fixes in this release can be found on GitHub in the [2.8.8 milestone](https://github.com/NuGet/Home/issues?q=milestone%3A2.8.8+is%3Aclosed)</span></span>
