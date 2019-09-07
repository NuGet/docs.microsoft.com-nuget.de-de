---
title: Anmerkungen zu dieser Version von nuget 5,3
description: Anmerkungen zu dieser Version von nuget 5,3, einschließlich neuer Features, Fehlerbehebungen und dcrs.
author: karann-msft
ms.author: karann
ms.date: 09/06/2019
ms.topic: conceptual
ms.openlocfilehash: f16bfe5481009f7924a61f03233d288d25ac618f
ms.sourcegitcommit: f4bfdbf62302c95f1f39e81ccf998f8bbc6d56b0
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/06/2019
ms.locfileid: "70774086"
---
# <a name="nuget-53-release-notes"></a>Anmerkungen zu dieser Version von nuget 5,3

Möglichkeiten der NuGet-Verteilung:

| NuGet-Version | Verfügbar in der Visual Studio-Version| Verfügbar in .NET SDK(s)|
|:---|:---|:---|
| [**5.3.0-preview3**](https://nuget.org/downloads) | [Visual Studio 2019, Version 16,3, Vorschau 3](https://visualstudio.microsoft.com/vs/preview/) | [3.0.100-preview9](https://dotnet.microsoft.com/download/dotnet-core/3.0) <sup>1</sup> |

<sup>1</sup> Installiert mit Visual Studio 2019 mit .net Core-Arbeitsauslastung

## <a name="summary-whats-new-in-53-preview-3"></a>Zusammenfassung: Neuerungen in 5,3 Preview 3

* [Das Paket Symbol kann in das Paket eingebettet werden](../reference/msbuild-targets.md#packing-an-icon-image-file), anstatt eine externe URL zu benötigen. - [#352](https://github.com/NuGet/Home/issues/352)

* Verbesserte Sicherheit mit SHA-Nachverfolgung und-Erzwingung für Packages. config- [#7281](https://github.com/NuGet/Home/issues/7281)

### <a name="issues-fixed-in-this-release"></a>In diesem Release behobene Probleme

**Fehler**

* VS: Assemblys sind vollständig ngen-ED, nicht teilweise ngen- [#8513](https://github.com/NuGet/Home/issues/8513)

* Reduzieren der Speicherauslastung (kündigen von Ereignissen)- [#8471](https://github.com/NuGet/Home/issues/8471)

* Die Meldung "Error_UnableToFindProjectInfo" ist nicht korrekt- [#8441](https://github.com/NuGet/Home/issues/8441)

* NU1403 Verbesserungen-alle Pakete überprüfen, die erwarteten/tatsächlichen SHA-Werte einschließen- [#8424](https://github.com/NuGet/Home/issues/8424)

* Mehrfache Enumeration in "nugetpackagemanager. previewupdatepackagesasync- [#8401](https://github.com/NuGet/Home/issues/8401)

* "Öffentliche > interne" Änderung in "pluginprocess- [#8390](https://github.com/NuGet/Home/issues/8390) " Zurücksetzen

* Ivspackagesourceprovider. getSources (...) weist ein falsch definiertes Ausnahme Verhalten auf [#8383](https://github.com/NuGet/Home/issues/8383)

* Erstellen Sie den PluginManager-Konstruktor erneut öffentlich- [#8379](https://github.com/NuGet/Home/issues/8379)

* Metriken zur Nachverfolgung der Aktualisierungsrate der PM-Benutzeroberfläche- [#8369](https://github.com/NuGet/Home/issues/8369)

* Verringern Sie die Anzahl der Aktualisierungen der Benutzeroberfläche bei der Installation über die Benutzeroberfläche des Paket-Managers- [#8358](https://github.com/NuGet/Home/issues/8358)

* Telemetrie: DateTime-Werte verwenden kulturspezifische Formate- [#8351](https://github.com/NuGet/Home/issues/8351)

* Reduzieren Sie die Aktualisierung der Benutzeroberfläche auf der Registerkarte "Durchsuchen" der Paket-#6570 Manager [#8339](https://github.com/NuGet/Home/issues/8339) -

* [Test Fehler] "Die Konfigurationsdatei kann nicht analysiert werden." wird zweimal aufgefordert [#8320](https://github.com/NuGet/Home/issues/8320)

* NU5037-Fehler mit guter doc-Seite aufrufen, die Kunden Korrekturen erläutert (die erforderliche nuspec-Datei fehlt im Paket)- [#8291](https://github.com/NuGet/Home/issues/8291)

* Bei der Wiederherstellung im gesperrten Modus tritt ein Fehler auf, wenn runtimeidentifier des Projekts geändert wird- [#8260](https://github.com/NuGet/Home/issues/8260)

* Aktivieren der Einstellungen in vs Lazy- [#8156](https://github.com/NuGet/Home/issues/8156)

* Die Regression in "nuget-Quellen hinzufügen" bewirkt, dass das Zeichen ":", Hexadezimalwert 0x3a, nicht in einen Namen eingeschlossen werden kann. Fehler- [#7948](https://github.com/NuGet/Home/issues/7948)

* Anmelde Informationsanbieter für nuget-Plug-in: Ausblenden des Prozess Fensters- [#7511](https://github.com/NuGet/Home/issues/7511)

* "Packageblothresolver erzwingen" ist ein absoluter Pfad [#7349](https://github.com/NuGet/Home/issues/7349)

* Reduzieren der Aktualisierung der Benutzeroberfläche auf der Registerkarte "installieren und aktualisieren" der Benutzeroberfläche des Paket [#6570](https://github.com/NuGet/Home/issues/6570) -Managers

**DCR:**

* Aktualisieren von xamarin Frameworks für die Zuordnung zu netstandard 2,1- [#8368](https://github.com/NuGet/Home/issues/8368)

* Kopieren des Inhalts des Paket-Managers "Vorschaufenster" für Installation/Update- [#8324](https://github.com/NuGet/Home/issues/8324) aktivieren

* Wiederherstellung für proj-Dateien aktivieren- [#8212](https://github.com/NuGet/Home/issues/8212)

* Stellen `NUGET_NETFX_PLUGIN_PATHS` Sie `NUGET_NETCORE_PLUGIN_PATHS` und zur Unterstützung der Konfiguration von beiden zur gleichen Zeit bereit [#8151](https://github.com/NuGet/Home/issues/8151)

* Aktivieren mehrerer Versionen für einen packagedownload über das Version-Attribut- [#8074](https://github.com/NuGet/Home/issues/8074)

* Add-SolutionDirectory und-packagedirectory-Optionen zu nuget. exe Pack- [#7163](https://github.com/NuGet/Home/issues/7163)

* Aktivieren Sie das nuget-Paket als deterministisch [#6229](https://github.com/NuGet/Home/issues/6229)

**[Liste aller in dieser Version behobene Probleme-5,3 Preview 3](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.3")**
