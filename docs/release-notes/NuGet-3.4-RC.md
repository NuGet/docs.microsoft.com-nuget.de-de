---
title: Anmerkungen zu NuGet 3.4-RC
description: Anmerkungen zu NuGet 3.4 RC, einschließlich der bekannten Probleme, Fehlerkorrekturen, hinzugefügter Features und DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 795bdcfaa2e22447856b60d05807aeb0992cdfa0
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546753"
---
# <a name="nuget-34-rc-release-notes"></a>Anmerkungen zu NuGet 3.4-RC

[Anmerkungen zu NuGet 3.3](../release-notes/nuget-3.3.md) | [Anmerkungen zu NuGet 3.4](../release-notes/nuget-3.4.md)

NuGet 3.4-RC am 3. März 2016 zusammen mit Visual Studio 2015 Update 2 RC veröffentlicht wurde, und mit wenigen Grundsätze in Köpfen erstellt wurde:

* Plattformübergreifende Unterstützung
* Leistungsverbesserungen
* Kleinere Verbesserungen der Benutzeroberfläche

Die folgenden Funktionen stehen diese RC-Version, mit mehr für die 3.4 endgültige Version geplant wurde.

## <a name="new-features"></a>Neue Funktionen

* NuGet-Clients unterstützen jetzt Gzip-inhaltscodierung von Repositorys
* Unterstützung für PDBs aus Paketen in Xproj-Projekten
* Unterstützung für IOS- und Android-Buildvorgänge im ContentFiles-element
* Unterstützung für die Framework-Moniker "Netstandard" und "netstandardapp"

## <a name="new-user-interface-features"></a>Neue Features der Benutzeroberfläche

* Signifikante leistungsverbesserungen besonders auf den Registerkarten installiert, Updates und konsolidieren
* Installiert und Updates Registerkarten sind jetzt alphabetisch sortiert
* Schaltfläche "Aktualisieren", die eine Suche aktualisiert werden kann. hinzugefügt

## <a name="updates-and-improvements"></a>Updates und Verbesserungen

* Pakete, die auf die verwiesen wird `project.json` Gleitkommazahl deren Version wird nicht für jeden Build aktualisiert. Stattdessen werden sie aktualisiert nur, wenn Sie gezwungen, wiederherzustellen, bereinigen, neu erstellen oder ändern Sie `project.json`.
* NuGet.org-Repository-Quellen werden in einer Projektkonfiguration nicht mehr gezwungen, bei der Verwendung der Benutzeroberfläche für der NuGet-Konfigurations.
* NuGet nicht mehr stellt Pakete in freigegebene Projekten wieder her und schreibt eine Sperrdatei.
* Wir Netzwerkfehler wurde verbessert, und wiederholen Sie die Behandlung von nicht erreichbar ist oder langsam, reagieren.
* Tastatur und Maus Verhaltensweisen werden in der Visual Studio-Paket-Manager-UI verbessert.
* Wir unterstützen jetzt die neueste Version `project.json` -Schema in DNX.

## <a name="known-issues"></a>Bekannte Probleme

Wir fahren fort, um Probleme in der Liste unserer GitHub-Probleme nachzuverfolgen, die finden Sie unter: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)