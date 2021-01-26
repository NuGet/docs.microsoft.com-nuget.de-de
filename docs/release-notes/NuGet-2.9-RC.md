---
title: Anmerkungen zu dieser Version von nuget 2,9-RC
description: Anmerkungen zu dieser Version von nuget 2,9 RC, einschließlich bekannter Probleme, Fehlerbehebungen, hinzugefügter Features und dcrs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: b9d32f09fae7e12f81cf92b5b6e6b36c71d55f26
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780321"
---
# <a name="nuget-29-rc-release-notes"></a><span data-ttu-id="1efc1-103">Anmerkungen zu dieser Version von nuget 2,9-RC</span><span class="sxs-lookup"><span data-stu-id="1efc1-103">NuGet 2.9-RC Release Notes</span></span>

<span data-ttu-id="1efc1-104">[Nuget 2.8.7 Anmerkungen](../release-notes/nuget-2.8.7.md)  |  zu dieser Version [Anmerkungen zu dieser Version von nuget 3,0 Preview](../release-notes/nuget-3.0-preview.md)</span><span class="sxs-lookup"><span data-stu-id="1efc1-104">[NuGet 2.8.7 Release Notes](../release-notes/nuget-2.8.7.md) | [NuGet 3.0 Preview Release Notes](../release-notes/nuget-3.0-preview.md)</span></span>

<span data-ttu-id="1efc1-105">Nuget 2,9 wurde am 10. September 2015 als Update für 2.8.7 VSIX für Visual Studio 2012 und 2013 veröffentlicht.</span><span class="sxs-lookup"><span data-stu-id="1efc1-105">NuGet 2.9 was released September 10, 2015 as an update to the 2.8.7 VSIX for Visual Studio 2012 and 2013.</span></span>

### <a name="updates-in-this-release"></a><span data-ttu-id="1efc1-106">Updates in dieser Version</span><span class="sxs-lookup"><span data-stu-id="1efc1-106">Updates in this release</span></span>

* <span data-ttu-id="1efc1-107">Die Verarbeitung von Paketen wird übersprungen, wenn das enthaltene `.nuspec` Dokument falsch formatiert ist [PR8](https://github.com/NuGet/NuGet2/pull/8)</span><span class="sxs-lookup"><span data-stu-id="1efc1-107">Now skipping processing packages if their contained `.nuspec` document is malformed - [PR8](https://github.com/NuGet/NuGet2/pull/8)</span></span>
* <span data-ttu-id="1efc1-108">Korrigierte multipartwebrequest-Behandlung von \r\n für UNIX/Linux-Szenarien: [776](https://github.com/NuGet/Home/issues/776)</span><span class="sxs-lookup"><span data-stu-id="1efc1-108">Corrected multipartwebrequest handling of \r\n for Unix/Linux scenarios - [776](https://github.com/NuGet/Home/issues/776)</span></span>
* <span data-ttu-id="1efc1-109">Korrigierte Integration in Buildereignisse in Visual Studio 2013 Community Edition- [1180](https://github.com/NuGet/Home/issues/1180)</span><span class="sxs-lookup"><span data-stu-id="1efc1-109">Corrected integration with build events in Visual Studio 2013 Community edition - [1180](https://github.com/NuGet/Home/issues/1180)</span></span>


<span data-ttu-id="1efc1-110">Die komplette Liste der Fixes in dieser Version finden Sie auf GitHub im 2.8.8- [Meilenstein](https://github.com/NuGet/Home/issues?q=milestone%3A2.8.8+is%3Aclosed) .</span><span class="sxs-lookup"><span data-stu-id="1efc1-110">The complete list of fixes in this release can be found on GitHub in the [2.8.8 milestone](https://github.com/NuGet/Home/issues?q=milestone%3A2.8.8+is%3Aclosed)</span></span>
