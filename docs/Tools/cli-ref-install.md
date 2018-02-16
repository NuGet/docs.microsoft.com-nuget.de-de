---
title: NuGet CLI Installationsbefehl | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Referenz für die nuget.exe Installationsbefehl"
keywords: NuGet Verweis installieren, installieren Sie die Paket-Befehl
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 9e824b08486704371eebefb964f86315d82fc222
ms.sourcegitcommit: b0af28d1c809c7e951b0817d306643fcc162a030
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/14/2018
---
# <a name="install-command-nuget-cli"></a>Installationsbefehl (NuGet CLI)

**Gilt für:** Verpacken Sie Verbrauch &bullet; **unterstützte Versionen:** alle

Heruntergeladen und installiert ein Paket in ein Projekt, dem aktuellen Ordner, die mit der angegebenen Paketquellen auszuführen.

> [!Tip]
> Um ein Paket im Kontext eines Projekts direkt herunterzuladen, besuchen Sie das Paket die Seite [nuget.org](https://www.nuget.org) , und wählen Sie die **herunterladen** Link.

Wenn keine Datenquellen angegeben sind, ist die in der Datei globale Konfiguration aufgelisteten `%APPDATA%\NuGet\NuGet.Config`, verwendet werden. Finden Sie unter [NuGet Konfigurieren von Verhalten](../consume-packages/configuring-nuget-behavior.md) für weitere Details.

Wenn keine bestimmte Pakete angegeben werden, `install` installiert alle Pakete in des Projekts aufgeführten `packages.config` Datei, wodurch die ähnelt [ `restore` ](cli-ref-restore.md).

Die `install` Befehl ändert sich nicht auf eine Projektdatei oder `packages.config`; auf diese Weise ähnelt `restore` nur Pakete auf den Datenträger fügt jedoch ändert sich nicht auf ein Projekt Abhängigkeiten.

Zum Hinzufügen einer Abhängigkeit ein Projekts durch die Paketmanager-Benutzeroberfläche oder die Konsole in Visual Studio hinzufügen oder ändern `packages.config` und führen Sie einen `install` oder `restore`.

## <a name="usage"></a>Verwendung

```cli
nuget install <packageID | configFilePath> [options]
```

auf dem `<packageID>` benennt das Paket zu installieren (verwenden die neueste Version), oder `<configFilePath>` identifiziert die `packages.config` Datei, die Pakete installieren aufgeführt. Sie können angeben, dass eine bestimmte Version mit der `-Version` Option.

## <a name="options"></a>Optionen

| Option | Beschreibung |
| --- | --- |
| ConfigFile | Die NuGet-Konfigurationsdatei angewendet werden soll. Wenn nicht angegeben, *%AppData%\NuGet\NuGet.Config* verwendet wird. |
| DependencyVersion | *(4.4 +)*  Gibt eine bestimmte Version Überschreiben des Standardverhaltens der Abhängigkeit Auflösung an. |
| DisableParallelProcessing | Deaktiviert die Installation von mehreren Paketen parallel. |
| ExcludeVersion | Installiert das Paket in einen Ordner mit dem Namen mit nur den Paketnamen und nicht die Versionsnummer an. |
| FallbackSource | *(3.2 +)*  Eine Liste der Paketquellen überein, die als Zugriffe verwendet werden soll, für den Fall, dass das Paket nicht, in der primären gefunden wird oder Standardquelle. |
| ForceEnglishOutput | *(3.5 +)*  Erzwingt nuget.exe über eine invariante Kultur Englisch-basierte ausgeführt werden. |
| Framework | *(4.4 +)*  Zielframework wird verwendet, um Abhängigkeiten. Der Standardwert ist "Any", wenn nicht angegeben. |
| Hilfe | Zeigt die Hilfe Informationen für den Befehl. |
| NoCache | Verhindert, dass NuGet Pakete aus lokalen Caches. |
| NonInteractive | Unterdrückt aufforderungen für Benutzereingaben oder Bestätigungen an. |
| OutputDirectory | Gibt den Ordner, in dem Pakete installiert sind. Wenn kein Ordner angegeben wird, wird der aktuelle Ordner verwendet. |
| PackageSaveMode | Gibt die Typen von Dateien nach der Paketinstallation speichern: einer der `nuspec`, `nupkg`, oder `nuspec;nupkg`. |
| PreRelease | Mit der Vorabversion Pakete installiert werden. Dieses Flag ist nicht erforderlich, beim Wiederherstellen von Paketen mit `packages.config`. |
| RequireConsent | Überprüft, ob Pakete werden wiederhergestellt aktiviert wird vor dem Herunterladen und Installieren der Pakete. Weitere Informationen finden Sie unter [Paketwiederherstellung](../consume-packages/package-restore.md). |
| SolutionDirectory | Gibt die Stammordner der Lösung für das Wiederherstellen von Paketen. |
| Quelle | Gibt die Liste der Paketquellen (wie URLs) Verwendung an. Wenn nicht angegeben, wird der Befehl verwendet die Quellen in Konfigurationsdateien bereitgestellt, finden Sie unter [NuGet Konfigurieren von Verhalten](../consume-packages/configuring-nuget-behavior.md). |
| Ausführlichkeit | Gibt die Anzahl der Details in der Ausgabe angezeigt: *normalen*, *stillen*, *ausführliche*. |
| Version | Gibt die Version des zu installierenden Pakets an. |

Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)

## <a name="examples"></a>Beispiele

```cli
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
