---
title: Nuget 3.4.3 Anmerkungen zu dieser Version
description: Anmerkungen zu dieser Version von nuget 3.4.3 einschließlich bekannter Probleme, Fehlerbehebungen, hinzugefügter Features und dcrs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: f0d9740aaf0a82b9e4023b5e4990c8f4adbea63c
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776471"
---
# <a name="nuget-343-release-notes"></a>Nuget 3.4.3 Anmerkungen zu dieser Version

[Nuget 3.4.2 Anmerkungen](../release-notes/nuget-3.4.2.md)  |  zu dieser Version [Nuget 3.4.4 Anmerkungen](../release-notes/nuget-3.4.4.md) zu dieser Version

Nuget 3.4.3 wurde am 22. April 2016 veröffentlicht, um verschiedene Probleme zu beheben, die in den 3,4 und nachfolgenden Releases identifiziert wurden.

Sie können die vsix-Datei und die-nuget.exe [hier](https://dist.nuget.org/index.html)herunterladen.

## <a name="updates-and-improvements"></a>Updates und Verbesserungen

* Verbesserte Visual Studio-Zuverlässigkeit. Wir haben einige Probleme in nuget behoben, die Abstürze in Visual Studio verursacht haben.

## <a name="fixes"></a>Fehlerbehebungen

* Einige Autorisierungs Probleme wurden durch Kenn Wort geschützte private nuget-Feeds behoben.
* Es wurde ein Problem behoben, das die Verwendung von PCL aus `project.json` mit angegebenen Laufzeiten nicht wiederherstellen konnte.
* Einige Kunden haben bei der Installation von Paketen zeitweilig auftretende Fehler fest. Dies wurde nun in dieser Version behoben.
* Es wurde ein Problem behoben, das Wiederherstellungs Fehler in C++/CLI-Projekten mit verursacht hat `project.json` .
* Einige Pakete (z. b. modernhttpclient), in denen Sie nicht ordnungsgemäß entpackt werden, wenn Sie nuget in Mono verwenden. Dies wurde nun in dieser Version behoben.

Eine umfassende Liste der Fehlerbehebungen und Verbesserungen in dieser Version finden Sie in der Liste [der Probleme.](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed)