---
title: Anmerkungen zu NuGet 3.1
description: Anmerkungen zu NuGet 3.1, einschließlich der bekannten Probleme, Fehlerkorrekturen, hinzugefügter Features und DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 779567d94a5a9a1b3eacddaa4c882201a446cb4b
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545346"
---
# <a name="nuget-31-release-notes"></a>Anmerkungen zu NuGet 3.1

[Anmerkungen zu NuGet 3.0](../release-notes/nuget-3.0.0.md) | [Anmerkungen zu NuGet 3.1.1](../release-notes/nuget-3.1.1.md)

NuGet 3.1 wurde als gebündelte Universal Windows Platform SDK-Erweiterung für Visual Studio 2015 27 Juli 2015 veröffentlicht. Wir übermittelt diese Version mit dem Windows-Plattform-SDK, damit die Windows-Entwicklungsumgebung NuGet plattformübergreifende Arbeit nutzen kann, die zuvor gestartet worden. Diese Version des NuGet-Erweiterung ist nur für Visual Studio 2015 verfügbar.

Es wird empfohlen, die Entwickler, die Zugriff auf Visual Studio-Update-Katalog auf die neueste Version verfügen, die verfügbar ist, da wir immer Veröffentlichen von Updates mit Fehlerbehebungen und neuen Features sind.

## <a name="nuget-visual-studio-extension"></a>NuGet Visual Studio-Erweiterung

Probleme und Funktionen in dieser Version sind auf GitHub markiert die ["transitive 3.1 RTM UWP-Unterstützung" Meilenstein](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+) insgesamt schließen wir 67 Probleme in der Version 3.1.

### <a name="new-features"></a>Neue Funktionen

* `project.json` Unterstützung für Windows UWP und ASP.NET 5-Unterstützung
* Transitiver Paketverweise-installation

Beschreibungs- und Definitionseigenschaften dieser Features an anderer Stelle in der Dokumentation zu finden.

### <a name="deprecated"></a>Als veraltet markiert

Die folgenden Funktionen sind nicht mehr für Visual Studio 2015 zur Verfügung:

* Level-Lösungspakete können nicht mehr installiert werden

Die folgenden Funktionen sind nicht mehr verfügbar ist, für Visual Studio 2015 und Projekte, mit denen die `project.json` Spezifikation

* `install.ps1` und `uninstall.ps1` -diese Skripts werden während der Installation des Pakets ignoriert werden, wiederherstellen, aktualisieren und deinstallieren
* Konfiguration von Transformationen werden ignoriert
* Inhalt wird ausgeführt, aber nicht in einem Projekt kopiert werden.
    * Das Team arbeitet daran, dieses Feature erneut zu implementieren, führen die Diskussion und Fortschritt: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)


### <a name="known-issues"></a>Bekannte Probleme

Es gab eine Reihe bekannter Probleme, die mit dieser Version bereitgestellt.

* Installation von der Version 3.1, mit dem Windows 10 SDK wird jede Version von NuGet-Erweiterung herabgestuft, die zuvor installiert wurde

## <a name="nuget-command-line"></a>NuGet-Befehlszeile

Die NuGet-Befehlszeile ausführbare Datei wurde aktualisiert und an einen neuen verteilbarer Speicherort verschoben werden, sodass historische nuget.exe-Versionen weiterhin zur Verfügung gestellt werden können.  Sie können die 3.1 Betaversion von nuget.exe für Windows auf herunterladen: [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)

Der neue Speicherort des verteilbare befindet sich auf dem Host "dist.NuGet.org" mit einer Ordnerstruktur, die diese Vorlage folgt:

     {platform supported}/{version}/nuget.exe

### <a name="new-features"></a>Neue Funktionen

* NuGet.exe wiederherstellen können, und installieren Sie Pakete in Projekten, mit denen eine `project.json` Datei.
* NuGet.exe können Herstellen einer Verbindung mit und nutzen die NuGet-v3-Protokolls an: [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)

## <a name="known-issues"></a>Bekannte Probleme ##

1.    Kann nicht ausgeführt werden Pack für ein `project.json` -Datei – [928](https://github.com/NuGet/Home/issues/928)
2.    Wird nicht unterstützt, auf das Mono - [1059](https://github.com/NuGet/Home/issues/1059)
3.    Ist nicht lokalisiert - [1058](https://github.com/NuGet/Home/issues/1058), [1057](https://github.com/NuGet/Home/issues/1057)
4.    Ist nicht signiert, wie die vorhandene http://nuget.org/nuget.exe  -  [1073](https://github.com/NuGet/Home/issues/1073)
