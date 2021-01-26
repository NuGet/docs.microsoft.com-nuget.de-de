---
title: Nuget 3.4.2 Anmerkungen zu dieser Version
description: Anmerkungen zu dieser Version von nuget 3.4.2 einschließlich bekannter Probleme, Fehlerbehebungen, hinzugefügter Features und dcrs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 6e6aa174582d059faa5bef9469cd83b19da51cf3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780250"
---
# <a name="nuget-342-release-notes"></a>Nuget 3.4.2 Anmerkungen zu dieser Version

Anmerkungen zu nuget- [Version 3.4.1](../release-notes/nuget-3.4.1.md)  |  [Nuget 3.4.3 Anmerkungen](../release-notes/nuget-3.4.3.md) zu dieser Version

Nuget 3.4.2 wurde am 8. April 2016 veröffentlicht, um verschiedene Probleme zu beheben, die in der Version 3,4 und 3.4.1 identifiziert wurden.

## <a name="nugetexe-342-rc-is-now-available"></a>nuget.exe 3.4.2 RC ist jetzt verfügbar.

Sie können den Release Candidate nuget.exe 3.4.2 [hier](https://dist.nuget.org/index.html)herunterladen.

## <a name="updates-and-improvements"></a>Updates und Verbesserungen

* Wir haben die Leistung von Updates in einem bestimmten Szenario erheblich verbessert, bei dem Updates von Paketen mit Deep-Abhängigkeits Diagrammen sehr lange gedauert haben und Visual Studio nicht reagiert haben.
* die nuget-Wiederherstellung ohne Netzwerk Datenverkehr erfolgt in Visual Studio 2,5 x – 3X schneller.
* Zusätzlich zu dieser Änderung haben wir ein Problem behoben, bei dem das Netzwerk zweimal beim Abrufen der Update Anzahl in der vs-Benutzeroberfläche aufgetreten ist. Dies war teilweise verantwortlich für einige Timeout Probleme, die Kunden in 3.4/3.4.1 hatten.
* Unterstützung für no_proxy Einstellung hinzugefügt

## <a name="fixes"></a>Fehlerbehebungen

* Es wurde ein Problem behoben, bei dem nuget.org source in den nuget-Einstellungen oder-Konfigurationen nach dem Aktualisieren auf 3.4.1 fehlt.
* Es wurde ein Problem behoben, bei dem eine Änderung der Groß-/Kleinschreibung von "findpackagesbyid" in 3.4.1 in
* Es wurde ein Problem mit dem Fehler behoben, das eine nuget-Wiederherstellung mit nuget.exe verursacht hat.
* Beim Durchsuchen von Quellen mit ungültiger Symbol-URL wurde ein Absturz korrigiert.
* Behobene Probleme beim Zusammenführen von Versionen und Einträgen aus "alle Quellen".

## <a name="known-issues-in-342-windows-x86-commandline-rc"></a>Bekannte Probleme in 3.4.2 Windows x86 commandline (RC)

Diese Probleme werden frühzeitig in der nächsten Woche behoben, bevor RTM getroffen wird.

*  Das Ausführen der nuget-Wiederherstellung für eine Lösung schlägt fehl, wenn die Projektmappendatei in einer niedrigeren Ordnerhierarchie platziert wird als die Projektdateien.
*  Das Ausführen des Befehls "nuget löschen" für ein Paket mit dem V2-Feed schlägt fehl. Verwenden Sie stattdessen den V3-Feed.


Eine umfassende Liste der Fehlerbehebungen und Verbesserungen in dieser Version finden Sie in der Liste [der Probleme.](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+)