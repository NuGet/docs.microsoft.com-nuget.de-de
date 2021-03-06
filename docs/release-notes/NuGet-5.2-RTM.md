---
title: Anmerkungen zu dieser Version von nuget 5,2 RTM
description: Anmerkungen zu dieser Version von nuget 5,2, einschließlich neuer Features, Fehlerbehebungen und dcrs.
author: JonDouglas
ms.author: jodou
ms.date: 07/23/2019
ms.topic: conceptual
ms.openlocfilehash: 25fa1d09046a583fb987b9f3dd51a0099f4331a7
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776203"
---
# <a name="nuget-52-release-notes"></a>Anmerkungen zu dieser Version von nuget 5,2

Möglichkeiten der NuGet-Verteilung:

| NuGet-Version | Verfügbar in der Visual Studio-Version| Verfügbar in .NET SDK(s)|
|:---|:---|:---|
| [**verweisen**](https://nuget.org/downloads) | [Visual Studio 2019 Version 16.2](https://visualstudio.microsoft.com/downloads/) | [2.1.80 x](https://dotnet.microsoft.com/download/dotnet-core/2.1)<sup>1</sup>, [2.2.40 x](https://dotnet.microsoft.com/download/dotnet-core/2.2)<sup>2</sup> |

<sup>1</sup> Installiert mit Visual Studio 2019 mit .net Core-Arbeitsauslastung 

<sup>2</sup> Verfügbar als optionale Installation mit Visual Studio 2019 mit .net Core-Arbeitsauslastung

## <a name="summary-whats-new-in-52"></a>Zusammenfassung: Neues in 5,2

* Es wurde ein kritischer Fehler behoben, der gelegentlich zu Fehlern beim nuget-Vorgang aufgrund von Pfad Problemen auf Linux-& Mac- [#7341](https://github.com/NuGet/Home/issues/7341)

* Verbesserte Reaktionsfähigkeit der Benutzeroberfläche beim Durchsuchen von Paketen mithilfe der Benutzeroberfläche des nuget-Paket-Managers in Visual Studio besonders bemerkbar für langsame Quellen [#8039](https://github.com/NuGet/Home/issues/8039)

* Fehlerbehebungen für Fehlerbehebungen für Sperrdateien ([#8187](https://github.com/NuGet/Home/issues/8187),[#8160](https://github.com/NuGet/Home/issues/8160),[#8114](https://github.com/NuGet/Home/issues/8114),[#7840](https://github.com/NuGet/Home/issues/7840)) und das Authentifizierungs-Plug-in ([#8300](https://github.com/NuGet/Home/issues/8300),[#8271](https://github.com/NuGet/Home/issues/8271),[#8269](https://github.com/NuGet/Home/issues/8269),[#8210](https://github.com/NuGet/Home/issues/8210),[#8198](https://github.com/NuGet/Home/issues/8198),[#7845](https://github.com/NuGet/Home/issues/7845))

### <a name="issues-fixed-in-this-release"></a>In diesem Release behobene Probleme

**Fehler**

* Perf: Paket-Manager-Konsole: UI Delay Update "Default Project" ComboBox selected value- [#8235](https://github.com/NuGet/Home/issues/8235)

* Perf: Leistungsverbesserungen in der PM-Benutzeroberfläche- [#8039](https://github.com/NuGet/Home/issues/8039)

* Perf: UI-Verzögerung beim Lesen des Standard Projekts in der PMC- [#6824](https://github.com/NuGet/Home/issues/6824)

* Perf: [vsfeedback] Registerkarte "nuget-Update" friert für eine lokale Paketquelle ein [#6470](https://github.com/NuGet/Home/issues/6470)

* Plug-ins: nuget wartet das vollständige Handshake-Timeout, wenn das Plug [#8300](https://github.com/NuGet/Home/issues/8300) -in nicht gestartet oder vorzeitig beendet wird

* Plug-ins: verbessern der Diagnosemöglichkeiten für Plug-in-Starts- [#8271](https://github.com/NuGet/Home/issues/8271)

* Plug-ins: Problem bei der nuget.exe Ermittlung von integrierten Plug-Ins [#8269](https://github.com/NuGet/Home/issues/8269)

* Plug-ins: die Cachedatei wird nie gelesen [#8210](https://github.com/NuGet/Home/issues/8210)

* Plug-ins: "eine Aufgabe wurde abgebrochen." Fehler mit Authentifizierungs-Plug-in während der Wiederherstellung [#8198](https://github.com/NuGet/Home/issues/8198)

* Der Plug-in-Cache kann auf Linux-Plattformen nicht zeitweise erkannt werden [#7845](https://github.com/NuGet/Home/issues/7845)

* Lockfile: bei ATF hat der Wert false NU1004 aufgrund einer ungültigen Überprüfung des Framework-Gleichheits- [#8187](https://github.com/NuGet/Home/issues/8187)

* Lockfile: das Wiederherstellungs Flag "--Locked-Mode" wird nicht berücksichtigt, wenn die Sperrdatei leer oder falsch formatiert ist [#8160](https://github.com/NuGet/Home/issues/8160)

* Lockfile: Projekte mit benutzerdefinierten Assemblynamen in Paketen Sperrdatei nicht in Kleinbuchstaben [#8114](https://github.com/NuGet/Home/issues/8114)

* Lockfile: Projekt Verweis in Kleinbuchstaben in Sperrdatei erstellen- [#7840](https://github.com/NuGet/Home/issues/7840)

* Wiederherstellung: das Installieren eines manipuliert signierten Pakets führt zu mehreren fehlgeschlagenen Installations versuchen (mit wiederholter Ausgabe)- [#8175](https://github.com/NuGet/Home/issues/8175)

* VS: die Benutzeroptionen für die Lösung können nach dem nuget-Update- [#8166](https://github.com/NuGet/Home/issues/8166) nicht deserialisiert werden.

* DotNet-List-Package in einem UnitTest-Projekt gibt einen Fehler zurück [#8154](https://github.com/NuGet/Home/issues/8154)

* Nuget-Paketgruppe für vs-Installer erstellen: beheben einiger VSIX-Setup Probleme- [#8033](https://github.com/NuGet/Home/issues/8033)

* Generatepackageonbuild sollte nobuild nicht festlegen. - [#7801](https://github.com/NuGet/Home/issues/7801)

* Die neue Option "-symbolpackageformat schnupkg" generiert einen Fehler, wenn die nuspec-Datei ein explizites assemblyverweiselement enthält [#7638](https://github.com/NuGet/Home/issues/7638)

* Nuget. targets (498, 5): Fehler: ein Teil des Pfads "/tmp/NuGetScratch- [#7341](https://github.com/NuGet/Home/issues/7341) wurde nicht gefunden.

**DCR:**

* Fügen Sie eine MSBuild-Eigenschaft hinzu, die angibt, dass packagedownload unterstützt wird: [#8106](https://github.com/NuGet/Home/issues/8106)

* Frameworkreferenzierung unterdrückt den Abhängigkeits Fluss über "frameworkreferen. privateassets- [#7988](https://github.com/NuGet/Home/issues/7988)

* Mechanismus zum Bereitstellen von runtime.jsaußerhalb eines Pakets [#7351](https://github.com/NuGet/Home/issues/7351)

**[Liste aller in dieser Version behobene Probleme-5,2 RTM](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.2")**


