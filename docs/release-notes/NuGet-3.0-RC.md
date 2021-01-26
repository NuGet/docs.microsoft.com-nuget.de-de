---
title: Anmerkungen zu dieser Version von nuget 3,0 RC
description: Anmerkungen zu dieser Version von nuget 3,0 RC, einschließlich bekannter Probleme, Fehlerbehebungen, hinzugefügter Features und dcrs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 19bc51a278425295811db253ca3f4ba4366ccf49
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776579"
---
# <a name="nuget-30-rc-release-notes"></a>Anmerkungen zu dieser Version von nuget 3,0 RC

Anmerkungen zu dieser [Version von nuget 3,0 Beta](../release-notes/nuget-3.0-beta.md)  |  [Anmerkungen zu dieser Version von nuget 3,0 rc2](../release-notes/nuget-3.0-RC2.md)

Nuget 3,0 RC wurde am 29. April 2015 mit der Version von Visual Studio 2015 RC veröffentlicht. Diese Version enthält eine Reihe wichtiger Programmfehler Behebungen, Leistungsverbesserungen und Updates, um die neuen Frameworks zu unterstützen.  Er ist nur für Visual Studio 2015 verfügbar.

### <a name="continued-focus-on-performance"></a>Fortsetzen des Fokus auf die Leistung

Die Stabilität und Leistung von nuget-Abfragen ist weiterhin ein heißes Thema, auf das wir uns konzentrieren.  Mit dieser Version sollten Sie sehr schnelle Suchvorgänge in der nuget-Benutzeroberfläche und-Website sehen.  Wir überwachen den Dienst und die Verwendung des Dienstanbieter, damit wir diese Vorgänge weiterhin optimieren können.

## <a name="significant-issues-resolved"></a>Wichtige Probleme gelöst

Um die nuget-Clients zu stabilisieren, haben wir viele Probleme im Rahmen dieser Version gelöst.  Im folgenden finden Sie eine kurze Liste einiger wichtiger Probleme, die behoben wurden:

* Im Rahmen der Umbenennung des K-Frameworks für ASP.net 5 wurden FrameworkMoniker aktualisiert, um den [Link](https://github.com/NuGet/Home/issues/215) DNX und dnxcore zu behandeln.
* Hilfe Dokumentation von Links im Visual Studio-UI- [Link](https://github.com/NuGet/Home/issues/232) hinzugefügt
* Bessere Behandlung komplexer Verweise in `.nuspec` mit durch Trennzeichen getrennten frameworkverweis- [Links](https://github.com/NuGet/Home/issues/276)
* Unterstützung für den [Link](https://github.com/NuGet/Home/issues/253) "japanische Kulturen" korrigiert
* Aktualisierter Client, damit ASP.net 5 Projekte den [Link](https://github.com/NuGet/Home/issues/219) "neue V3-Endpunkte" verwenden können
* Das Thema wurde aktualisiert, um den Paket Ordner [](https://github.com/NuGet/Home/issues/56) mit der Quell Code Verwaltung besser
* Unterstützung für den [Link](https://github.com/NuGet/Home/issues/17) "Satelliten Pakete" korrigiert
* Unterstützung für frameworkspezifische [Inhalts Dateien korrigiert](https://github.com/NuGet/Home/issues/18)

## <a name="github-presence-overhaul"></a>GitHub-Anwesenheits Überprüfung

Wir haben einige Änderungen an den [Quell Code Depots auf GitHub](http://github.com/nuget/home)vorgenommen.  Wenn Sie Probleme mit dem nuget-Visual Studio-Client, den PowerShell-Befehlen oder der ausführbaren Befehlszeilen Datei haben, können Sie diese Probleme protokollieren und ihren Fortschritt in unserer [GitHub-Home-Repository-Liste "Probleme](http://github.com/nuget/home/issues)" überwachen.  Wir verfolgen Probleme für den Katalog in unserem [GitHub nugetgallery-Repository](http://github.com/nuget/NuGetGallery/issues).


## <a name="stay-tuned"></a>Bleiben Sie dran

Im [Blog](http://blog.nuget.org) erhalten Sie weitere Informationen zum Fortschritt und Ankündigungen für nuget 3,0!