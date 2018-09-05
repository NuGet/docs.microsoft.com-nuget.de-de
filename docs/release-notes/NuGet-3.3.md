---
title: Anmerkungen zu NuGet 3.3
description: Anmerkungen zu NuGet 3.3, einschließlich der bekannten Probleme, Fehlerkorrekturen, hinzugefügter Features und DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 5fb840ab6a1329611e9cf417724bcdcd75efe2df
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43546646"
---
# <a name="nuget-33-release-notes"></a>Anmerkungen zu NuGet 3.3

[Anmerkungen zu NuGet 3.2.1](../release-notes/nuget-3.2.1.md) | [NuGet 3.4-RC-Versionsanmerkungen](../release-notes/nuget-3.4-RC.md)

NuGet 3.3 wurde am 30. November 2015 mit einer großen Anzahl von Benutzerschnittstellen-Updates und -Befehlszeilenfunktionen sowie eine Sammlung von nützlich Fehlerbehebungen für die NuGet-Clients veröffentlicht.

## <a name="new-features"></a>Neue Funktionen

* Anmeldeinformationsanbieter wurden eingeführt, mit denen Befehlszeilen NuGet-Clients, um die nahtlose Zusammenarbeit mit einem authentifizierten-Feed zu können. [Anweisungen zum Installieren von Visual Studio Team Services-Anmeldeinformationen Anbieter ](../api/nuget-exe-credential-providers.md) und Konfigurieren des NuGet-Pakets Clients seiner Verwendung finden Sie auf NuGet-Dokumentation.

## <a name="new-user-interface-features"></a>Neue Features der Benutzeroberfläche

* Separate Registerkarten für das Durchsuchen, installiert und Updates verfügbar
* Verfügbare Updates-Badge, der angibt, der Anzahl der Pakete mit verfügbaren updates
* Paketbadges in der Paketliste angeben, ob das Paket installiert ist, oder ein Update verfügbar ist
* Herunterladen Sie Anzahl und der Autor hinzugefügt, um die Liste der Pakete
* Anzahl der höchste verfügbare Version und die Anzahl der aktuell installierten Version in der Paketliste
* Aktionsschaltflächen können schnell installieren, aktualisieren und deinstallieren Sie auf die Liste der Pakete
* Klarer Aktionsschaltflächen im Bereich der Paket-Details
* Paket Aktualisierungsdatum im Bereich der Paket-Details
* Bereich, in der Projektmappenansicht konsolidieren
* Sortierbar Raster von Projekten und der installierten Versionsnummern in der Projektmappenansicht

## <a name="new-command-line-features"></a>Neue Befehlszeile Features

In dieser Version eingeführten wir die `add` und `init` Befehle aus, um die Ordner-basierten Repositorys zu initialisieren, wie beschrieben in der [Referenz zur nuget.exe](../tools/nuget-exe-cli-reference.md). Repositorys, die erstellt und verwaltet, die mit diesem Ordner-Struktur wird [bieten Sie beachtliche Leistungsvorteile](http://blog.nuget.org/20150922/Accelerate-Package-Source.html) wie beschrieben in unserem Blog.

## <a name="contentfiles"></a>ContentFiles

Inhalt wird nun unterstützt `project.json` zu verwalteten Projekten, die über die neue `contentFiles` Ordner und `.nuspec` `contentFiles` Element-Notation.  Dieser Inhalt kann direkt vom Paketersteller für Interaktionen mit Projektsystemen angegeben werden.  Weitere Informationen zum Konfigurieren von "contentfiles" in einem `.nuspec` Dokument finden Sie in der [NuSpec-Referenz](../reference/nuspec.md).

## <a name="nuget-locals-cache-management"></a>NuGet "lokal" Cache-Verwaltung

Das NuGet-Befehlszeile wurde aktualisiert, um Informationen zum Verwalten des lokalen Caches auf einer Arbeitsstation gehören.  Weitere Informationen zu den Befehl "Locals" steht in der [NuGet-Befehlszeilenreferenz](../tools/cli-ref-locals.md).

## <a name="fixed-issues"></a>Behobene Probleme

**Relevante Probleme**

* NuGet-Befehlszeile wiederhergestellten Unterstützung für die Wiederherstellung mit einer Projektmappe unter Mono - Pakete [1543](https://github.com/NuGet/Home/issues/1543)

Die vollständige Liste der in der Version 3.3 behandelten Probleme finden Sie auf GitHub unter den [3.3 Meilenstein](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.3.0+is%3Aclosed).

Die Liste der in der Befehlszeile 3.3-Version behobene Probleme in aufgezeichnet werden die [3.3 Befehlszeilen Meilenstein](https://github.com/NuGet/Home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A3.3.0-commandline).

## <a name="known-issues"></a>Bekannte Probleme

Wir fahren fort, um Probleme in der Liste unserer GitHub-Probleme nachzuverfolgen, die finden Sie unter: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)