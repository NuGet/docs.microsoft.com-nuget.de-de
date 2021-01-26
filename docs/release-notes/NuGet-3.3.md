---
title: Anmerkungen zu dieser Version von nuget 3,3
description: Anmerkungen zu dieser Version von nuget 3,3 einschließlich bekannter Probleme, Fehlerbehebungen, hinzugefügter Features und dcrs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: cd3f8c9c4586c608d41e7b8bfc413acfc6aff497
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776505"
---
# <a name="nuget-33-release-notes"></a>Anmerkungen zu dieser Version von nuget 3,3

Anmerkungen zu dieser [Version von nuget 3.2.1](../release-notes/nuget-3.2.1.md)  |  [Anmerkungen zu dieser Version von nuget 3,4-RC](../release-notes/nuget-3.4-RC.md)

Nuget 3,3 wurde am 30. November 2015 mit einer erheblichen Anzahl von Benutzeroberflächen Updates und Befehlszeilen Features sowie eine Sammlung nützlicher Korrekturen für die nuget-Clients veröffentlicht.

## <a name="new-features"></a>Neue Funktionen

* Es wurden Anmelde Informationsanbieter eingeführt, mit denen nuget-Befehlszeilen Clients nahtlos mit einem authentifizierten Feed arbeiten können. [Anweisungen zum Installieren des Visual Studio Team Services ](../reference/extensibility/nuget-exe-credential-providers.md) Anmelde Informationsanbieters und zum Konfigurieren der zu verwendenden nuget-Clients finden Sie unter nuget-Dokumentation.

## <a name="new-user-interface-features"></a>Neue Benutzeroberflächen Features

* Getrennte Registerkarten zum Durchsuchen, installieren und aktualisieren
* Verfügbarer Hinweis "Updates" gibt die Anzahl der Pakete mit verfügbaren Updates an
* Paket Ausweise in der Paketliste, um anzugeben, ob das Paket installiert ist oder ein Update verfügbar ist
* Download Anzahl und Autor zur Paketliste hinzugefügt
* Höchste verfügbare Versionsnummer und aktuell installierte Versionsnummer in der Paketliste
* Aktions Schaltflächen für die schnelle Installation, Aktualisierung und Deinstallation in der Paketliste
* Klarere Aktions Schaltflächen im Paket Detailbereich
* Paket Aktualisierungsdatum im Paket Detailbereich
* Bereich "konsolidieren" in der Lösungs Ansicht
* Sortier bares Raster von Projekten und installierten Versionsnummern in der projektmappenansicht

## <a name="new-command-line-features"></a>Neue Befehlszeilen Funktionen

In dieser Version haben wir die `add` Befehle und eingeführt `init` , um Ordner basierte Depots zu initialisieren, wie in der [nuget.exe Referenz](../reference/nuget-exe-cli-reference.md)beschrieben. Mit dieser Ordnerstruktur erstellte und erhaltene Depots [bieten bedeutende Leistungsvorteile](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) , die in unserem Blog beschrieben werden.

## <a name="contentfiles"></a>ContentFiles

Der Inhalt wird nun in `project.json` verwalteten Projekten durch die neue `contentFiles` Ordner-und `.nuspec` `contentFiles` Element Notation unterstützt.  Dieser Inhalt kann vom Paket Ersteller für Interaktionen mit Projekt Systemen direkt angegeben werden.  Weitere Informationen zum Konfigurieren von contentfiles in einem Dokument finden Sie `.nuspec` in der [nuspec-Referenz](../reference/nuspec.md).

## <a name="nuget-locals-cache-management"></a>Lokale nuget-Cache Verwaltung

Die nuget-Befehlszeile wurde aktualisiert und enthält Informationen zum Verwalten der lokalen Caches auf einer Arbeitsstation.  Weitere Informationen zum Befehl "Locals" finden Sie in der [nuget-Befehlszeilen Referenz](../reference/cli-reference/cli-ref-locals.md).

## <a name="fixed-issues"></a>Behobene Probleme

**Relevante Probleme**

* [1543](https://github.com/NuGet/Home/issues/1543) in der nuget-Befehlszeilen Wiederherstellung wiederhergestellte Unterstützung für die Wiederherstellung von Paketen mit einer Projektmappendatei

Eine umfassende Liste der Probleme, die in Version 3,3 behoben wurden, finden Sie auf GitHub unter dem [3,3-Meilenstein](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).

Die Liste der Probleme, die in der 3,3-Befehlszeilen Freigabe behoben wurden, wird in der [3,3 Command-Line-Meilenstein](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline)aufgezeichnet.

## <a name="known-issues"></a>Bekannte Probleme

Wir verfolgen weiterhin Probleme in unserer GitHub-Liste mit Problemen, die unter folgenden Themen zu finden sind: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)