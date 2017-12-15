---
title: Anmerkungen zur Version des NuGet-3.1 | Microsoft Docs
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 0fc4d89a-ccca-4d63-85bf-461cd9ced882
description: "Versionshinweise für NuGet 3.1 einschließlich bekannte Probleme, Fehlerbehebungen, Funktionen und Archivierung von dcrs Design."
keywords: "NuGet-3.1 Anmerkungen zu dieser Version, aufgrund von Fehlerbehebungen, bekannte Probleme, zusätzliche Funktionen, Archivierung von dcrs Design"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: eef2b2c1af99671c7ae3874c2c12130f104e88eb
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-31-release-notes"></a>NuGet-Version 3.1 Hinweise

[Anmerkungen zur Version des NuGet-3.0](../release-notes/nuget-3.0.0.md) | [NuGet 3.1.1-Versionshinweise](../release-notes/nuget-3.1.1.md)

NuGet-3.1 wurde 27 Juli 2015 als gebündelte Universal Windows Platform SDK-Erweiterung für Visual Studio 2015 veröffentlicht. Diese Version mit der Windows-Plattform-SDK von uns bereitgestellten, damit der Windows-entwicklungserfahrung NuGet plattformübergreifende Arbeit nutzen konnte, die zuvor gestartete. Diese Version des NuGet-Erweiterung ist nur für Visual Studio 2015 verfügbar.

Es wird empfohlen, die Entwickler, die Zugriff auf die Visual Studio Gallery-Update auf die neueste Version verfügen, die verfügbar ist, ist es immer Veröffentlichen von Updates mit Fehlerkorrekturen und neue Funktionen sind.

## <a name="nuget-visual-studio-extension"></a>NuGet Visual Studio-Erweiterung

Probleme und Funktionen in dieser Version sind auf GitHub markiert die ["3.1 transitiv RTM uwp-Support" Meilenstein](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+) insgesamt wir 67 Probleme in der Version 3.1 geschlossen.

### <a name="new-features"></a>Neue Funktionen

* `project.json`Unterstützung für Windows-UWP und ASP.NET 5 Unterstützung
* Transitiv Paketinstallation

Beschreibung "und" Definition dieser Funktionen können an anderer Stelle in der Dokumentation gefunden werden.

### <a name="deprecated"></a>Als veraltet markiert

Die folgenden Funktionen sind nicht mehr für Visual Studio 2015 verfügbar:

* Level-Lösungspakete können nicht mehr installiert werden

Die folgenden Funktionen sind nicht mehr verfügbar, für die Visual Studio 2015 und Projekte, mit denen die `project.json` Spezifikation

* `install.ps1`und `uninstall.ps1` -diese Skripts während der Paketinstallation ignoriert werden, stellen Sie wieder her, aktualisieren und deinstallieren
* Konfiguration Transformationen werden ignoriert
* Inhalt wird ausgeführt, aber nicht in ein Projekt kopiert werden.
    * Das Team arbeitet daran, diese Funktion erneut implementieren, führen die Diskussion und aktueller Fortschritt: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)


### <a name="known-issues"></a>Bekannte Probleme

Es wurden einige bekannte Probleme in dieser Version übermittelt.

* Installation der mit dem Windows 10-SDK-Version 3.1 downgrade wird Version des NuGet-Erweiterung, die zuvor installiert wurde

## <a name="nuget-command-line"></a>NuGet-Befehlszeile

Ausführbare Befehlszeilendatei "NuGet" wurde aktualisiert und an einem neuen verteilbarer Speicherort verschoben werden, sodass frühere Versionen des nuget.exe fortgesetzt werden können, zur Verfügung gestellt werden.  Sie können die 3.1 Beta-Version von nuget.exe für Windows herunterladen: [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)

Die neue Position des verteilbare befindet sich auf dem Host dist.nuget.org mit eine Ordnerstruktur, die mit dieser Vorlage folgt:

     {platform supported}/{version}/nuget.exe

### <a name="new-features"></a>Neue Funktionen

* NuGet.exe können wiederherstellen und Installieren von Paketen in-Projekte, mit denen eine `project.json` Datei.
* NuGet.exe können Herstellen einer Verbindung mit und nutzen Sie das NuGet-v3-Protokolls an: [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)

## <a name="known-issues"></a>Bekannte Probleme ##

1.    Kann nicht ausgeführt werden Pack für ein `project.json` Datei - [928](https://github.com/NuGet/Home/issues/928)
2.    Wird nicht unterstützt, auf das Mono - [1059](https://github.com/NuGet/Home/issues/1059)
3.    Ist nicht lokalisiert - [1058](https://github.com/NuGet/Home/issues/1058), [1057](https://github.com/NuGet/Home/issues/1057)
4.    Ist nicht signiert, wie die vorhandene http://nuget.org/nuget.exe - [1073](https://github.com/NuGet/Home/issues/1073)
