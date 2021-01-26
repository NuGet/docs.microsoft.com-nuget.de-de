---
title: Anmerkungen zu dieser Version von nuget 3,1
description: Anmerkungen zu dieser Version von nuget 3,1 einschließlich bekannter Probleme, Fehlerbehebungen, hinzugefügter Features und dcrs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: e1dc31e2543610b1da395f77fd2424bd85d985ef
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776538"
---
# <a name="nuget-31-release-notes"></a>Anmerkungen zu dieser Version von nuget 3,1

Anmerkungen zu dieser [Version von nuget 3,0](../release-notes/nuget-3.0.0.md)  |  [Anmerkungen zu nuget 3.1.1](../release-notes/nuget-3.1.1.md)

Nuget 3,1 wurde am 27. Juli 2015 als gebündelte Erweiterung zum universelle Windows-Plattform SDK für Visual Studio 2015 veröffentlicht. Wir haben diese Version mit dem Windows Platform SDK geliefert, damit die Windows-Entwicklungsumgebung die plattformübergreifende nuget-Arbeit nutzen kann, die zuvor gestartet wurde. Diese nuget-Erweiterungs Version ist nur für Visual Studio 2015 verfügbar.

Wir empfehlen Entwicklern, die Zugriff auf das Visual Studio Gallery-Update haben, auf die neueste Version, die verfügbar ist, da wir immer Updates mit Fehlerbehebungen und neuen Features veröffentlichen.

## <a name="nuget-visual-studio-extension"></a>Nuget Visual Studio-Erweiterung

Probleme und Features in dieser Version sind auf GitHub mit dem [Meilenstein "3,1 RTM UWP transitiv Support"](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aclosed+milestone%3A%223.1+RTM+UWP+transitive+support%22+)  gekennzeichnet. Wir haben 67-Probleme in der 3,1-Version geschlossen.

### <a name="new-features"></a>Neue Funktionen

* `project.json` Unterstützung für Windows UWP-und ASP.net 5-Unterstützung
* Transitive Paketinstallation

Beschreibungen und Definitionen dieser Features finden Sie an anderer Stelle in der Dokumentation.

### <a name="deprecated"></a>Als veraltet markiert

Die folgenden Features sind für Visual Studio 2015 nicht mehr verfügbar:

* Pakete auf Projektmappenebene können nicht mehr installiert werden.

Die folgenden Features sind für Visual Studio 2015 und Projekte, die die Spezifikation verwenden, nicht mehr verfügbar. `project.json`

* `install.ps1``uninstall.ps1`diese Skripts werden während der Installation, Wiederherstellung, Aktualisierung und Deinstallation von Paketen ignoriert.
* Konfigurations Transformationen werden ignoriert.
* Inhalt wird übernommen, aber nicht in ein Projekt kopiert.
    * Das Team arbeitet daran, dieses Feature erneut zu implementieren, und befolgt die Diskussion und den Fortschritt unter: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627)


### <a name="known-issues"></a>Bekannte Probleme

Diese Version enthält eine Reihe bekannter Probleme.

* Durch die Installation der Version 3,1 mit dem Windows 10 SDK wird eine beliebige Version der zuvor installierten nuget-Erweiterung herabgestuft.

## <a name="nuget-command-line"></a>Nuget-Befehlszeile

Die ausführbare nuget-Befehlszeilen Datei wurde aktualisiert und an einen neuen verteilbaren Speicherort verschoben, damit historische Versionen von nuget.exe weiterhin verfügbar gemacht werden können.  Sie können die 3,1 Beta Version von nuget.exe für Windows herunterladen unter: [http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe](http://dist.nuget.org/win-x86-commandline/v3.1.0-beta/nuget.exe)

Der neue verteilbare Speicherort befindet sich auf dem dist.nuget.org-Host mit einer Ordnerstruktur, die dieser Vorlage folgt:

```
{platform supported}/{version}/nuget.exe
```

### <a name="new-features"></a>Neue Funktionen

* nuget.exe können Pakete in Projekten, die eine Datei verwenden, wiederherstellen und installieren `project.json` .
* nuget.exe können eine Verbindung mit dem nuget V3-Protokoll herstellen und es nutzen unter: [https://api.nuget.org/v3/index.json](https://api.nuget.org/v3/index.json)

## <a name="known-issues"></a>Bekannte Probleme ##

1.    Das Paket kann nicht für eine Datei ausgeführt werden `project.json` : [928](https://github.com/NuGet/Home/issues/928)
2.    Wird in Mono- [1059](https://github.com/NuGet/Home/issues/1059) nicht unterstützt.
3.    Ist nicht lokalisiert- [1058](https://github.com/NuGet/Home/issues/1058),   [1057](https://github.com/NuGet/Home/issues/1057)
4.    Ist nicht signiert, genau wie das vorhandene http://nuget.org/nuget.exe  -  [1073](https://github.com/NuGet/Home/issues/1073)
