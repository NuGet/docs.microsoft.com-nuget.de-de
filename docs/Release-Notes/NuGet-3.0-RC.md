---
title: Anmerkungen dieser Version von NuGet 3.0 RC
description: Versionshinweise für NuGet 3.0 RC einschließlich bekannte Probleme, Fehlerbehebungen, Funktionen und Archivierung von dcrs Design.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 28ac49d9e9071d16d20b24808abb0acaab214ffd
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="nuget-30-rc-release-notes"></a>Anmerkungen dieser Version von NuGet 3.0 RC

[Anmerkungen zur Version von NuGet 3.0 Beta](../release-notes/nuget-3.0-beta.md) | [NuGet 3.0 RC2-Anmerkungen zu dieser Version](../release-notes/nuget-3.0-RC2.md)

NuGet 3.0 RC wurde mit der Version von Visual Studio 2015 RC am 29. April 2015 veröffentlicht. Diese Version enthält eine Reihe von wichtiger Programmfehlerbehebungen, leistungsverbesserungen und Upgrades zur Unterstützung der neuen Frameworks.  Es ist nur für Visual Studio 2015 verfügbar.

### <a name="continued-focus-on-performance"></a>Kontinuierliche den Fokus auf die Leistung

Stabilität und Leistung von NuGet-Abfragen weiterhin ein im laufenden Systembetrieb Thema sein, dem wir auf konzentrieren.  Mit dieser Version sollte gestartet werden, sehr schnelle Suchvorgänge in der Website und NuGet UI finden Sie unter.  Es wird überwacht, den Dienst und wie Sie den Dienst verwenden, sodass wir fortfahren können, um diese Vorgänge zu optimieren.

## <a name="significant-issues-resolved"></a>Erhebliche Probleme gelöst wurden

Um die NuGet-Clients zu stabilisieren aufgelöst wir viele Probleme, die als Teil dieser Version.  Hier wird nur eine kurze Liste der einiger wichtiger Probleme behoben:

* Als Teil der Umbenennung von K-Framework für ASP.NET 5, frameworkMoniker zur Behandlung von Dnx und Dnxcore aktualisiert wurden [Link](https://github.com/NuGet/Home/issues/215)
* Hilfe-Dokumentation über Links in der Visual Studio-Benutzeroberfläche hinzugefügt [Link](https://github.com/NuGet/Home/issues/232)
* Eine bessere Behandlung von komplexen Verweise in `.nuspec` mit durch Trennzeichen getrennte Framework verweisen [Link](https://github.com/NuGet/Home/issues/276)
* Unterstützung für Japanisch Kulturen festen [Link](https://github.com/NuGet/Home/issues/253)
* Aktualisierte Client neue v3-Endpunkte verwenden, die ASP.NET 5-Projekte ermöglichen es [Link](https://github.com/NuGet/Home/issues/219)
* Aktualisierte besser Handle Pakete (Ordner) mit der quellcodeverwaltung [Link](https://github.com/NuGet/Home/issues/56)
* Unterstützung für Satelliten-Paketen behoben [Link](https://github.com/NuGet/Home/issues/17)
* Unterstützung für frameworkspezifische Inhaltsdateien korrigiert [Link](https://github.com/NuGet/Home/issues/18)

## <a name="github-presence-overhaul"></a>GitHub Vorhandensein Überarbeitung

Wir haben einige Änderungen vorgenommen unsere [source in GitHub-Repositorys](http://github.com/nuget/home).  Haben Probleme mit der Visual Studio NuGet-Clients, die Powershell-Befehle oder der Befehlszeile ausführbare Sie können diese Probleme melden und überwachen ihren Fortschritt auf unserer [Home GitHub-Repository Problemliste](http://github.com/nuget/home/issues).  Verfolgen wir Probleme für den Katalog in unserer [GitHub NuGetGallery-Repository](http://github.com/nuget/NuGetGallery/issues).


## <a name="stay-tuned"></a>Bleiben Sie dran

Bitte achten Sie auf [unserem Blog](http://blog.nuget.org) weitere Bearbeitung und Ankündigungen für NuGet 3.0!