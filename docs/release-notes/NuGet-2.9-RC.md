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
# <a name="nuget-29-rc-release-notes"></a>Anmerkungen zu Version 2.9-RC von NuGet

[Anmerkungen zu NuGet 2.8.7](../release-notes/nuget-2.8.7.md) | [NuGet 3.0 Anmerkungen zur Vorschauversion](../release-notes/nuget-3.0-preview.md)

NuGet 2.9 wurde am 10. September 2015 veröffentlicht, als Update für die 2.8.7 VSIX für Visual Studio 2012 und 2013.

### <a name="updates-in-this-release"></a>Updates in dieser Version

* Nachdem die Verarbeitung von Paketen wird übersprungen, wenn die enthaltenen `.nuspec` Dokument ist falsch formatiert: [PR8](https://github.com/NuGet/NuGet2/pull/8)
* Korrigiert Multipartwebrequest Behandlung \r\n für Unix/Linux-Szenarien – [776](https://github.com/NuGet/Home/issues/776)
* Integration mit Buildereignisse in Visual Studio 2013 Community Edition - korrigiert [1180](https://github.com/NuGet/Home/issues/1180)


Die vollständige Liste der Fixes in dieser Version finden Sie auf GitHub in der [2.8.8 Meilenstein](https://github.com/NuGet/Home/issues?q=milestone%3A2.8.8+is%3Aclosed)
