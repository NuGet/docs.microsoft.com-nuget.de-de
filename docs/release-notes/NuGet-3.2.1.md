---
title: Anmerkungen zu NuGet 3.2.1
description: Anmerkungen zu dieser Version für die Einbindung von NuGet-Version 3.2.1 bekannte Probleme, Fehlerkorrekturen, hinzugefügter Features und DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: e5ddbb8aa52ef85c823404364a3aca79fd16f3b1
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548189"
---
# <a name="nuget-321-release-notes"></a>Anmerkungen zu NuGet 3.2.1

[Anmerkungen zu NuGet 3.2](../release-notes/nuget-3.2.md) | [Anmerkungen zu NuGet 3.3](../release-notes/nuget-3.3.md)

NuGet 3.2.1 für die Befehlszeile am 12. Oktober 2015 kann durch eine Reihe von Optimierungen und Korrekturen für die 3.2-Version wurde veröffentlicht und steht über ["dist.NuGet.org"](http://dist.nuget.org/index.html).

## <a name="improvements"></a>Verbesserungen

* NuGet verwendet nun die Konfigurationsdatei mit dem ursprünglichen Groß-/Kleinschreibung der `NuGet.Config`.  Dies ist wichtig für die Groß-/Kleinschreibung Betriebssysteme [1427](https://github.com/NuGet/Home/issues/1427)
* NuGet-Wiederherstellung ignoriert nun Dnx-Projekte (`*.xproj`), die verarbeitet werden sollen, mit `dnu` [1227](https://github.com/NuGet/Home/issues/1227)
* Optimierung der netzwerknutzung, bei der Arbeit mit `index.json` und Packen Sie die Registrierungsdaten [1426](https://github.com/NuGet/Home/issues/1426)
* Verbesserte Ressourcendownload mit v2-Diensten unter Umständen stabiler sind die Verarbeitung [1448](https://github.com/NuGet/Home/issues/1448)

## <a name="fixes"></a>Fehlerbehebungen

* NuGet ordnungsgemäß zur Aktualisierung der `.csproj` / `.vcxproj` Verweise [1483](https://github.com/NuGet/Home/issues/1483)
* Jetzt verhindern, dass einen lokale .nuget-Ordner erstellt werden, wenn eine SpecialFolders.UserProfile nicht gefunden werden kann [1531](https://github.com/NuGet/Home/issues/1531)
* Verbesserte Behandlung von Paketen im lokalen Cache, die während des Herunterladens beschädigt sind [1405](https://github.com/NuGet/Home/issues/1405) [1157](https://github.com/NuGet/Home/issues/1157)

Eine vollständige Liste der Probleme, die für die Befehlszeile und Visual Studio-Erweiterung Sie im NuGet GitHub finden [3.2.1 Meilenstein](https://github.com/NuGet/Home/issues?q=milestone%3A3.2.1+is%3Aclosed)

## <a name="known-issues"></a>Bekannte Probleme

Wir fahren fort, um Probleme in der Liste unserer GitHub-Probleme nachzuverfolgen, die finden Sie unter: [http://github.com/nuget/home/issues](http://github.com/nuget/home/issues)