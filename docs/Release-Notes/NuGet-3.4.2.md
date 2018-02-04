---
title: Anmerkungen zur Version des NuGet-3.4.2 | Microsoft Docs
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Versionshinweise für NuGet 3.4.2 einschließlich bekannte Probleme, Fehlerbehebungen, Funktionen und Archivierung von dcrs Design."
keywords: "NuGet-3.4.2 Anmerkungen zu dieser Version, aufgrund von Fehlerbehebungen, bekannte Probleme, zusätzliche Funktionen, Archivierung von dcrs Design"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 892a965e67762af2ae42c2d6ee75d2838104d1c2
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-342-release-notes"></a>Anmerkungen zur Version von NuGet 3.4.2

[Anmerkungen zur Version des NuGet-3.4.1](../release-notes/nuget-3.4.1.md) | [NuGet 3.4.3-Versionshinweise](../release-notes/nuget-3.4.3.md)

NuGet 3.4.2 am 8. April 2016, um mehrere Probleme zu beheben, die in den 3.4 und 3.4.1 identifiziert wurden veröffentlicht wurde freigegeben.

## <a name="nugetexe-342-rc-is-now-available"></a>NuGet.exe 3.4.2 RC ist jetzt verfügbar

Sie können dem Release Candidate von nuget.exe 3.4.2 herunterladen [hier](https://dist.nuget.org/index.html).

## <a name="updates-and-improvements"></a>Updates und Verbesserungen

* Wir haben die Leistung von Updates in einem bestimmten Szenario erheblich verbessert, in dem Updates für die Pakete mit umfassenden Abhängigkeitsdiagramme sehr lange dauerte und nicht reagiert Visual Studio.
* NuGet Restore ohne Netzwerkdatenverkehr ist 2.5 x – 3 X schneller innerhalb von Visual Studio.
* Zusätzlich zu dieser Änderung haben wir das Problem behoben, in denen wurden wir im Netzwerk Erreichens zweimal beim Abrufen des Updates in der Visual Studio-Benutzeroberfläche zu zählen. Dies war teilweise für einige Erfahrung im 3.4/3.4.1 Timeout Probleme Kunden verantwortlich.
* Unterstützung für No_proxy-Einstellung

## <a name="fixes"></a>Fehlerbehebungen

* Ein Problem behoben, bei denen war nuget.org Quelle nach dem Update auf 3.4.1 im NuGet-Einstellungen oder der Konfiguration fehlt.
* Ein Problem behoben, in denen eine Änderung Schreibweise FindPackagesById in 3.4.1 Artifactory unterbrochen.
* Beheben Sie ein Problem mit FIPS, die NuGet-Wiederherstellung mit nuget.exe Fehler verursacht hat.
* Korrektur eines Absturzes, wenn Sie Quellen mit Symbol "ungültig" URL zu durchsuchen.
* Behobene Probleme mit dem Zusammenführen von Versionen und Einträge aus "Alle Quellen".

## <a name="known-issues-in-342-windows-x86-commandline-rc"></a>Bekannte Probleme in 3.4.2 Windows X86 Commandline (RC)

Diese Probleme werden die Anfang der nächsten Woche bevor wir RTM erreicht behoben werden.

*  Ausgeführte NuGet-Wiederherstellung zu einem Lösungsvorschlag schlägt fehl, wenn die Projektmappendatei, die in einer niedrigeren Ordnerhierarchie als die Projektdateien platziert wird.
*  NuGet-Delete-Befehl wird für ein Paket mit dem Feed V2 ausgeführt werden. Verwenden Sie stattdessen V3-Feeds.


Die vollständige Liste der Korrekturen und Verbesserungen in dieser Version, sehen Sie sich die Liste der Probleme [hier](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+milestone%3A3.4.2++is%3Aclosed+).