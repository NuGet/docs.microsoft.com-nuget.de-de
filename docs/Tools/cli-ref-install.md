---
title: NuGet CLI Installationsbefehl | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 59ac622f-837c-4545-bc93-a56330e02d71
description: "Referenz für die nuget.exe Installationsbefehl"
keywords: NuGet Verweis installieren, installieren Sie die Paket-Befehl
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 88c123a7f2a3d628713cefcc4b110fb0205093b4
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/14/2017
---
# <a name="install-command-nuget-cli"></a>Installationsbefehl (NuGet CLI)

**Gilt für:** Verpacken Sie Verbrauch &bullet; **unterstützte Versionen:** alle

Heruntergeladen und installiert ein Paket in ein Projekt, dem aktuellen Ordner, die mit der angegebenen Paketquellen auszuführen.

> [!Tip]
> Um ein Paket im Kontext eines Projekts direkt herunterzuladen, besuchen Sie das Paket die Seite [nuget.org](https://www.nuget.org) , und wählen Sie die **herunterladen** Link. 

Wenn keine Datenquellen angegeben sind, ist die in der Datei globale Konfiguration aufgelisteten `%APPDATA%\NuGet\NuGet.Config`, verwendet werden. Finden Sie unter [Konfigurieren von NuGet-Verhalten](../consume-packages/configuring-nuget-behavior.md) für weitere Details.

Wenn keine bestimmte Pakete angegeben werden, `install` installiert alle Pakete in des Projekts aufgeführten `packages.config` Datei, wodurch die ähnelt [ `restore` ](#restore). (Die `install` Befehl funktioniert nicht mit `project.json`.)

Die `install` Befehl ändert sich nicht auf eine Projektdatei oder `packages.config`; auf diese Weise ähnelt `restore` nur Pakete auf den Datenträger fügt jedoch ändert sich nicht auf ein Projekt Abhängigkeiten.

Zum Hinzufügen einer Abhängigkeit ein Projekts durch die Paketmanager-Benutzeroberfläche oder die Konsole in Visual Studio hinzufügen oder ändern `packages.config` und führen Sie einen `install` oder `restore`. Für Projekte mit `project.json`, können Sie diese Datei ändern und anschließend ausführen `restore`.

## <a name="usage"></a>Verwendung

```
nuget install <packageID | configFilePath> [options]
```

auf dem `<packageID>` benennt das Paket zu installieren (verwenden die neueste Version), oder `<configFilePath>` identifiziert die `packages.config` Datei, die Pakete installieren aufgeführt. Sie können angeben, dass eine bestimmte Version mit der `-Version` Option.

## <a name="options"></a>Optionen

| Option | Beschreibung |
| --- | --- |
| "ConfigFile" hinzu | *(2,5 +)*  Das NuGet-Konfigurationsdatei angewendet. Wenn nicht angegeben, *%AppData%\NuGet\NuGet.Config* verwendet wird. |
| DisableParallelProcessing | Deaktiviert die Installation von mehreren Paketen parallel. |
| ExcludeVersion | Installiert das Paket in einen Ordner mit dem Namen mit nur den Paketnamen und nicht die Versionsnummer an. |
| Alternativer | *(3.2 +)*  Eine Liste der Paketquellen überein, die als Zugriffe verwendet werden soll, für den Fall, dass das Paket nicht, in der primären gefunden wird oder Standardquelle. |
| ForceEnglishOutput | *(3.5 +)*  Erzwingt nuget.exe über eine invariante Kultur Englisch-basierte ausgeführt werden. |
| Framework | *(4.4 +)*  Zielframework wird verwendet, um Abhängigkeiten. Der Standardwert ist "Any", wenn nicht angegeben. |
| Hilfe | Zeigt die Hilfe Informationen für den Befehl. |
| NoCache | Verhindert, dass NuGet Pakete aus lokalen Caches. |
| Nicht interaktive | Unterdrückt aufforderungen für Benutzereingaben oder Bestätigungen an. |
| OutputDirectory | Gibt den Ordner, in dem Pakete installiert sind. Wenn kein Ordner angegeben wird, wird der aktuelle Ordner verwendet. |
| PackageSaveMode | Gibt die Typen von Dateien nach der Paketinstallation speichern: einer der `nuspec`, `nupkg`, oder `nuspec;nupkg`. |
| Vorabversion | Mit der Vorabversion Pakete installiert werden. Dieses Flag ist nicht erforderlich, beim Wiederherstellen von Paketen mit `packages.config`. |
| RequireConsent | Überprüft, ob Pakete werden wiederhergestellt aktiviert wird vor dem Herunterladen und Installieren der Pakete. Weitere Informationen finden Sie unter [Paketwiederherstellung](../consume-packages/package-restore.md). |
| SolutionDirectory | Gibt die Stammordner der Lösung für das Wiederherstellen von Paketen. |
| Quelle | Gibt die Liste der Paketquellen (wie URLs) Verwendung an. Wenn nicht angegeben, wird der Befehl verwendet die Quellen in Konfigurationsdateien bereitgestellt, finden Sie unter [NuGet Konfigurieren von Verhalten](../Consume-Packages/Configuring-NuGet-Behavior.md). |
| Ausführlichkeit | Gibt die Anzahl der Details in der Ausgabe angezeigt: *normalen*, *stillen*, *detaillierte (2.5 und höher)*. |
| Version | Gibt die Version des zu installierenden Pakets an. |

Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)

## <a name="examples"></a>Beispiele

```
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
