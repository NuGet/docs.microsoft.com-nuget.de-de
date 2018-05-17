---
title: NuGet-CLI-Update-Befehl
description: Referenz für den nuget.exe Update-Befehl
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: e6964d92436ce1bac9e6af85f6dae75fcf40378d
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="update-command-nuget-cli"></a>Der Befehl „commnad“ (NuGet CLI)

**Gilt für:** Verpacken Sie Verbrauch &bullet; **unterstützte Versionen:** alle

Aktualisiert alle Pakete in einem Projekt (mit `packages.config`) auf die neueste Version. Es wird empfohlen, führen Sie ["restore"](cli-ref-restore.md) vor dem Ausführen der `update`. (Verwenden Sie zum Aktualisieren eines einzelnen Pakets [ `nuget install` ](cli-ref-install.md) ohne Angabe eine Versionsnummer, die in der Groß-/Kleinschreibung NuGet die neueste Version installiert.)

Hinweis: `update` funktioniert nicht mit der CLI unter Mono (Mac OS x oder Linux) oder ausgeführt, wenn das PackageReference-Format verwendet.

Die `update` Befehl aktualisiert auch Assemblyverweise in der Projektdatei, vorausgesetzt die verweist bereits vorhanden. Wenn Sie ein aktualisiertes Paket eine hinzugefügte Assembly hat, wird ein neuer Verweis *nicht* hinzugefügt. Ferner müssen neue paketabhängigkeiten nicht ihre Assemblyverweise hinzugefügt. Um diese Vorgänge im Rahmen des ein Update einzuschließen, das Paket in Visual Studio mit der Paket-Manager-UI oder der Paket-Manager-Konsole zu aktualisieren.

Mit diesem Befehl kann auch zum Aktualisieren von nuget.exe selbst verwendet werden mithilfe der *-Self-Service* Flag.

## <a name="usage"></a>Verwendung

```cli
nuget update <configPath> [options]
```

auf dem `<configPath>` identifiziert, entweder eine `packages.config` oder die Projektmappendatei, die das Projekt Abhängigkeiten aufgeführt.

## <a name="options"></a>Optionen

| Option | Beschreibung |
| --- | --- |
| ConfigFile | Die NuGet-Konfigurationsdatei angewendet werden soll. Wenn nicht angegeben, `%AppData%\NuGet\NuGet.Config` (Windows) oder `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) verwendet wird.|
| FileConflictAction | Gibt die Aktion an, wenn Sie gefragt werden, überschreiben oder vorhandene Dateien, die vom Projekt referenzierte ignoriert werden. Werte sind *überschreiben, ignorieren möchten, keine*. |
| ForceEnglishOutput | *(3.5 +)*  Erzwingt nuget.exe über eine invariante Kultur Englisch-basierte ausgeführt werden. |
| Hilfe | Zeigt die Hilfe Informationen für den Befehl. |
| Id | Gibt eine Liste der Paket-IDs zu aktualisieren. |
| MSBuildPath | *(4.0 und höher)*  Gibt den Pfad des MSBuild für die Verwendung mit dem Befehl, Vorrang vor `-MSBuildVersion`. |
| MSBuildVersion | *(3.2 +)*  Gibt die Version von MSBuild mit diesem Befehl verwendet werden soll. Unterstützte Werte sind 4, 12, 14, 15. Standardmäßig werden die MSBuild-Datei in Ihrem Pfad abgerufen wird, wird standardmäßig andernfalls die neueste installierte Version von MSBuild. |
| NonInteractive | Unterdrückt aufforderungen für Benutzereingaben oder Bestätigungen an. |
| Vorabversion | Ermöglicht es, auf Vorabversionen aktualisiert. Dieses Flag ist nicht erforderlich, beim Aktualisieren von Vorabversionen von Paketen, die bereits installiert sind. |
| RepositoryPath | Gibt den lokalen Ordner, in dem Pakete installiert sind. |
| Safe | Gibt an, dass nur mit der höchsten Version in die gleiche Haupt- und Nebenversionsnummern Version verfügbaren updates wie das installierte Paket installiert werden soll. |
| Self-Service | Wird nuget.exe auf die neueste Version aktualisiert. Alle anderen Argumente werden ignoriert. |
| Quelle | Gibt die Liste der Paketquellen (wie URLs), um nach Updates verwenden. Wenn nicht angegeben, wird der Befehl verwendet die Quellen in Konfigurationsdateien bereitgestellt, finden Sie unter [NuGet Konfigurieren von Verhalten](../consume-packages/configuring-nuget-behavior.md). |
| Ausführlichkeit | Gibt die Anzahl der Details in der Ausgabe angezeigt: *normalen*, *stillen*, *ausführliche*. |
| Version | Bei Verwendung mit einem Paket-ID gibt die Version des Pakets aktualisieren. |

Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)

## <a name="examples"></a>Beispiele

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
