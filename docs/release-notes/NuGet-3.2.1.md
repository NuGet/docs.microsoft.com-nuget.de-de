---
title: Anmerkungen zu dieser Version von nuget 3.2.1
description: Anmerkungen zu dieser Version von nuget 3.2.1 einschließlich bekannter Probleme, Fehlerbehebungen, hinzugefügter Features und dcrs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: cbbef3517122ceda91cb4b4463fe8be43d204db4
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776523"
---
# <a name="nuget-321-release-notes"></a>Anmerkungen zu dieser Version von nuget 3.2.1

Anmerkungen zu dieser [Version von nuget 3,2](../release-notes/nuget-3.2.md)  |  [Anmerkungen zu dieser Version von nuget 3,3](../release-notes/nuget-3.3.md)

Nuget 3.2.1 für die Befehlszeile wurde am 12. Oktober 2015 mit einigen Optimierungen und Korrekturen für die 3,2-Version veröffentlicht und ist über [Dist.nuget.org](http://dist.nuget.org/index.html)verfügbar.

## <a name="improvements"></a>Verbesserungen

* Nuget verwendet nun die Konfigurationsdatei mit der ursprünglichen Schreibweise von `NuGet.Config` .  Dies ist bei Betriebs [1427](https://github.com/NuGet/Home/issues/1427) Systemen mit Unterscheidung nach Groß-/Kleinschreibung wichtig
* Die nuget-Wiederherstellung ignoriert nun DNX-Projekte ( `*.xproj` ), die mit `dnu` [1227](https://github.com/NuGet/Home/issues/1227) verarbeitet werden sollen.
* Optimierte Netzwerk Auslastung bei der Arbeit mit `index.json` und Paket Registrierungsdaten [1426](https://github.com/NuGet/Home/issues/1426)
* Verbesserte Behandlung von Ressourcen Downloads, um mit den V2-Diensten [1448](https://github.com/NuGet/Home/issues/1448) robuster zu sein

## <a name="fixes"></a>Fehlerbehebungen

* Aktualisieren von nuget-Updates ordnungsgemäß, `.csproj` / `.vcxproj` Verweise [1483](https://github.com/NuGet/Home/issues/1483)
* Nun wird verhindert, dass ein lokaler nuget-Ordner erstellt wird, wenn "SpecialFolders. USERPROFILE" nicht gefunden werden kann [1531](https://github.com/NuGet/Home/issues/1531)
* Verbesserte Behandlung von Paketen im lokalen Cache, die während Download [1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157) beschädigt sind

Eine umfassende Liste der Probleme, die für die Befehlszeile und die Visual Studio-Erweiterung behoben wurden, finden Sie im nuget GitHub [3.2.1-Meilenstein](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed) .

## <a name="known-issues"></a>Bekannte Probleme

Wir verfolgen weiterhin Probleme in unserer GitHub-Liste mit Problemen, die unter folgenden Themen zu finden sind: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)