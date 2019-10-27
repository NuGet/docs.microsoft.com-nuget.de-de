---
title: Anmerkungen zu dieser Version von nuget 5,3
description: Anmerkungen zu dieser Version von nuget 5,3, einschließlich neuer Features, Fehlerbehebungen und dcrs.
author: karann-msft
ms.author: karann
ms.date: 09/06/2019
ms.topic: conceptual
ms.openlocfilehash: 994a0da3728e05a09b5537d150f2203477922efc
ms.sourcegitcommit: 904cbee57770af04efcae0b3709301685475bf64
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/26/2019
ms.locfileid: "72962290"
---
# <a name="nuget-53-release-notes"></a>Anmerkungen zu dieser Version von nuget 5,3

Möglichkeiten der NuGet-Verteilung:

| NuGet-Version | Verfügbar in der Visual Studio-Version| Verfügbar in .NET SDK(s)|
|:---|:---|:---|
| [**5.3.0**](https://nuget.org/downloads) | [Visual Studio 2019, Version 16,3](https://visualstudio.microsoft.com/downloads/) | [3.0.100](https://dotnet.microsoft.com/download/dotnet-core/3.0)<sup>1</sup> |
| [**5.3.1**](https://nuget.org/downloads) | [Visual Studio 2019 Version 16.3.6](https://visualstudio.microsoft.com/downloads/) | [Zukünftige Version: 3.0.101](https://dotnet.microsoft.com/download/dotnet-core/3.0) |

<sup>1</sup> Installiert mit Visual Studio 2019 mit .net Core-Arbeitsauslastung

## <a name="summary-whats-new-in-53"></a>Zusammenfassung: Neues in 5,3

* [Das Paket Symbol kann in das Paket eingebettet werden](../reference/msbuild-targets.md#packing-an-icon-image-file), anstatt eine externe URL zu benötigen. - [#352](https://github.com/NuGet/Home/issues/352)

* Verbesserte Sicherheit mit SHA-Nachverfolgung und-Erzwingung für Packages. config- [#7281](https://github.com/NuGet/Home/issues/7281)

* Aktivieren von veralteten/Legacy-nuget-Paketen [#2867](https://github.com/NuGet/Home/issues/2867) | [Blog Beitrag](https://devblogs.microsoft.com/nuget/deprecating-packages-on-nuget-org/) | [docs](https://docs.microsoft.com/en-us/nuget/nuget-org/deprecate-packages)

### <a name="issues-fixed-in-this-release"></a>In diesem Release behobene Probleme

**Fehler**

* Nuget-Pakete, die mit 3.0.100-preview9 SDK erstellt wurden, können von 2,2 SDK-Benutzern nicht verwendet werden... abhängig von Ihrer Zeitzone [#8603](https://github.com/NuGet/Home/issues/8603)

* Anführungszeichen "ungültige Zeichen im Pfad" in `nuget restore` [#8168](https://github.com/NuGet/Home/issues/8168)

* VS: Assemblys sind vollständig ngen-ED, nicht teilweise ngen- [#8513](https://github.com/NuGet/Home/issues/8513)

* Reduzieren der Speicherauslastung (kündigen von Ereignissen)- [#8471](https://github.com/NuGet/Home/issues/8471)

* Die Meldung "Error_UnableToFindProjectInfo" ist nicht korrekt- [#8441](https://github.com/NuGet/Home/issues/8441)

* NU1403 Verbesserungen-alle Pakete überprüfen, die erwarteten/tatsächlichen SHA-Werte einschließen- [#8424](https://github.com/NuGet/Home/issues/8424)

* Mehrfache Enumeration in `NuGetPackageManager.PreviewUpdatePackagesAsync` - [#8401](https://github.com/NuGet/Home/issues/8401)

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

* Regression in `Nuget sources add` bewirkt, dass das Zeichen "The": ", der Hexadezimalwert 0x3a, nicht in einen Namen eingeschlossen werden kann [#7948](https://github.com/NuGet/Home/issues/7948)

* Anmelde Informationsanbieter für nuget-Plug-in: Ausblenden des Prozess Fensters- [#7511](https://github.com/NuGet/Home/issues/7511)

* "Packageblothresolver erzwingen" ist ein absoluter Pfad [#7349](https://github.com/NuGet/Home/issues/7349)

* Reduzieren der Aktualisierung der Benutzeroberfläche auf der Registerkarte "installieren und aktualisieren" der Benutzeroberfläche des Paket [#6570](https://github.com/NuGet/Home/issues/6570) -Managers

**DCR:**

* Aktualisieren von xamarin Frameworks für die Zuordnung zu netstandard 2,1- [#8368](https://github.com/NuGet/Home/issues/8368)

* Kopieren des Inhalts des Paket-Managers "Vorschaufenster" für Installation/Update- [#8324](https://github.com/NuGet/Home/issues/8324) aktivieren

* Wiederherstellung für proj-Dateien aktivieren- [#8212](https://github.com/NuGet/Home/issues/8212)

* Führen Sie `NUGET_NETFX_PLUGIN_PATHS` und `NUGET_NETCORE_PLUGIN_PATHS` ein, um die Konfiguration von beiden zur gleichen Zeit zu unterstützen [#8151](https://github.com/NuGet/Home/issues/8151)

* Aktivieren mehrerer Versionen für einen packagedownload über das Version-Attribut- [#8074](https://github.com/NuGet/Home/issues/8074)

* Add-SolutionDirectory und-packagedirectory-Optionen zu nuget. exe Pack- [#7163](https://github.com/NuGet/Home/issues/7163)

**[Liste aller Probleme, die in dieser Version behoben wurden: 5,3](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.3")**

## <a name="summary-whats-new-in-531"></a>Zusammenfassung: Neues in 5.3.1

* Plug-in: eine Aufgabe wurde abgebrochen. die Kündigung lässt keine Auswirkung auf die Plug [#8648](https://github.com/NuGet/Home/issues/8648) -in-Instanziierung

* Restore-Tasks können nicht auf sichere Weise zweimal in einem Prozess ausgeführt werden (wenn Anmelde Informationsanbieter verwendet werden)- [#8688](https://github.com/NuGet/Home/issues/8688)
