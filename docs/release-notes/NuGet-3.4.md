---
title: Anmerkungen zu NuGet 3.4
description: Anmerkungen zu NuGet 3.4, einschließlich der bekannten Probleme, Fehlerkorrekturen, hinzugefügter Features und DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 77c0117fc40031a327e8dcb0aac5cd4045239e97
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551190"
---
# <a name="nuget-34-release-notes"></a>Anmerkungen zu NuGet 3.4

[Anmerkungen zu NuGet 3.4-RC](../release-notes/nuget-3.4-RC.md) | [Anmerkungen zu NuGet 3.4.1](../release-notes/nuget-3.4.1.md)

NuGet 3.4 wurde am 30. März 2016 als Teil der Visual Studio 2015 Update 2 und Visual Studio 15 Preview-Version veröffentlicht und mit wenigen Grundsätze in Köpfen erstellt wurde:

* Plattformübergreifende Unterstützung
* Leistungsverbesserungen
* Kleinere Verbesserungen der Benutzeroberfläche

Die folgenden Features wurden waren zuvor hinzugefügt haben, in die RC-Version und aktualisiert oder der Version 3.4 abgeschlossen:

## <a name="new-features"></a>Neue Funktionen

* NuGet-Clients unterstützen jetzt Gzip-inhaltscodierung von Repositorys
* Unterstützung für PDBs aus Paketen in Xproj-Projekten
* Unterstützung für IOS- und Android-Buildvorgänge im ContentFiles-element
* Unterstützung für die Framework-Moniker "Netstandard" und "netstandardapp"

## <a name="new-user-interface-features"></a>Neue Features der Benutzeroberfläche

* Signifikante leistungsverbesserungen besonders auf den Registerkarten installiert, Updates und konsolidieren
* Aggregieren "Alle Paketquellen"-Quelle ist verfügbar, mit der richtigen Suche Ergebnis zusammenführen
* Installiert und Updates Registerkarten sind jetzt alphabetisch sortiert
* Schaltfläche "Aktualisieren", die eine Suche aktualisiert werden kann. hinzugefügt
* Neueste Build-Optionen am oberen Rand der Liste der Versionen

## <a name="updates-and-improvements"></a>Updates und Verbesserungen

* Pakete, die auf die verwiesen wird `project.json` Gleitkommazahl deren Version wird nicht für jeden Build aktualisiert. Stattdessen werden sie aktualisiert nur, wenn Sie gezwungen, wiederherzustellen, bereinigen, neu erstellen oder ändern Sie `project.json`.
* NuGet.org-Repository-Quellen werden in einer Projektkonfiguration nicht mehr gezwungen, bei der Verwendung der Benutzeroberfläche für der NuGet-Konfigurations.
* NuGet nicht mehr stellt Pakete in freigegebene Projekten wieder her und schreibt eine Sperrdatei.
* Wir Netzwerkfehler wurde verbessert, und wiederholen Sie die Behandlung von nicht erreichbar ist oder langsam, reagieren.
* Tastatur und Maus Verhaltensweisen werden in der Visual Studio-Paket-Manager-UI verbessert.
* Wir unterstützen jetzt die neueste Version `project.json` -Schema in DNX.

## <a name="breaking-changes"></a>Die Lauffähigkeit der Anwendung beeinträchtigende Änderungen

* Paket-Versionsnummern werden jetzt in das Format normalisiert *wichtigen*. *kleinere*. *Patch*-*Vorabversion* aller Haupt-, neben- und patch werden als Zahlen behandelt, und legen Sie alle führenden Nullen auf.  Die vorabversionsinformationen wird als Zeichenfolge behandelt, und keine Änderungen angewendet werden. Diese Zahlen werden in Abfragen verwendet, indem Sie die NuGet-Clients und die Suche, die von der nuget.org-Dienst bereitgestellt wird.  Weitere Informationen finden Sie in der NuGet-Dokumentation unter [Vorabversion Versionen](../create-packages/prerelease-packages.md).

## <a name="known-issues"></a>Bekannte Probleme

* **Problem:** Windows 10-v1511-Benutzern möglicherweise auftreten, Probleme oder sogar eine Visual Studio-Absturzes mithilfe von Powershell in Visual Studio in den folgenden Szenarien:
    * Installieren / Deinstallieren von Paketen, die Install. ps1 / uninstall.ps1-Skripts
    * Laden von Projekten, die ein Skript init.ps1 (z. B. EntityFramework)
    * Veröffentlichen von Webinhalten

* **Problemumgehung:** stellen Sie sicher, dass Ihre Windows 10-Installation die neuesten Patches angewendet, Expecially der Januar 2016 (KB 3124263) oder ein neueres Update ist.  Weitere Informationen finden Sie auf [GitHub-Problem #1638](http://github.com/nuget/home/issues/1638)

* **Problem:** NuGet v2-Protokollumleitungen sind defekt
Benutzerdefinierte NuGet-Repositorys, die Anforderungen an einen alternativen Host umleiten, beachten die Umleitungsanforderung nicht.
* **Problemumgehung:** um dieses Problem zu umgehen, konfigurieren Sie den paketrepository-URI in den Einstellungen, die auf den Standort des umgeleiteten Servers verweist.
Weitere Informationen finden Sie unter [Pull Request auf GitHub #387](https://github.com/NuGet/NuGet.Client/pull/387).

Wir fahren fort, um Probleme in der Liste unserer GitHub-Probleme nachzuverfolgen, die finden Sie unter: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)