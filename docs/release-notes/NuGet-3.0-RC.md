---
title: Anmerkungen dieser Version von NuGet 3.0 RC
description: Anmerkungen zu NuGet 3.0 RC, einschließlich der bekannten Probleme, Fehlerkorrekturen, hinzugefügter Features und DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 0575cb1598f259a1cf1597f67123b644d67c31b5
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43551718"
---
# <a name="nuget-30-rc-release-notes"></a>Anmerkungen dieser Version von NuGet 3.0 RC

[Anmerkungen zu NuGet 3.0 Beta](../release-notes/nuget-3.0-beta.md) | [NuGet 3.0 RC2 – Versionshinweise](../release-notes/nuget-3.0-RC2.md)

NuGet 3.0 RC wurde mit dem Visual Studio 2015 RC-Release vom 29. April 2015 veröffentlicht. Diese Version enthält eine Reihe von wichtiger Programmfehlerbehebungen, leistungsverbesserungen und Upgrades zur Unterstützung der neuen Frameworks.  Es ist nur für Visual Studio 2015 verfügbar.

### <a name="continued-focus-on-performance"></a>Mittelpunkt und Leistung

Stabilität und Leistung von Abfragen von NuGet weiterhin ein wichtiges Thema, dem auf konzentrieren wir uns sind.  In dieser Version sollten Sie beginnen, um sehr schnelle Suchvorgänge in der NuGet UI und die Website anzuzeigen.  Wird überwacht der Dienst und wie Sie den Dienst verwenden, damit wir optimieren diese Vorgänge fortgesetzt werden kann.

## <a name="significant-issues-resolved"></a>Wichtige Probleme gelöst wurden

Um die NuGet-Clients zu stabilisieren, behoben wir viele Probleme, als Teil dieses Release.  Hier ist nur eine kurze Liste einiger wichtiger Probleme behoben:

* Im Rahmen der Umbenennung von K-Framework für ASP.NET 5, frameworkMoniker aktualisiert, um das Verarbeiten von Dnx und Dnxcore [Link](https://github.com/NuGet/Home/issues/215)
* In der Hilfe zu über Links im Visual Studio-Benutzeroberfläche hinzugefügt [Link](https://github.com/NuGet/Home/issues/232)
* Bessere Behandlung von komplexen Verweise in `.nuspec` mit durch Trennzeichen getrennte frameworkverweise [Link](https://github.com/NuGet/Home/issues/276)
* Unterstützung für japanische Kulturen festen [Link](https://github.com/NuGet/Home/issues/253)
* Aktualisierten Client, um neue v3-Endpunkte verwenden, die ASP.NET 5-Projekte ermöglichen [Link](https://github.com/NuGet/Home/issues/219)
* Ordner "Pakete" aktualisiert und eine bessere Handle in die quellcodeverwaltung [Link](https://github.com/NuGet/Home/issues/56)
* Unterstützung für satellitenpakete festen [Link](https://github.com/NuGet/Home/issues/17)
* Unterstützung für Inhaltsdateien frameworkspezifische korrigiert [Link](https://github.com/NuGet/Home/issues/18)

## <a name="github-presence-overhaul"></a>Überarbeitung der GitHub-Präsenz

Wir haben einige Änderungen an unseren [source auf GitHub-Repositorys](http://github.com/nuget/home).  Wenn Sie Probleme mit NuGet Visual Studio-Client, der Powershell-Befehle oder der Befehlszeile haben ausführbare können Sie diese Probleme zu melden und ihren Fortschritt überwachen unsere [Startseite des GitHub-Repository-Problemliste](http://github.com/nuget/home/issues).  Verfolgen wir Probleme für den Katalog in unserer [Repository von GitHub NuGetGallery](http://github.com/nuget/NuGetGallery/issues).


## <a name="stay-tuned"></a>Bleiben Sie dran

Bitte achten Sie auf [unseren Blog](http://blog.nuget.org) für die weitere Bearbeitung sowie Ankündigungen von NuGet 3.0!