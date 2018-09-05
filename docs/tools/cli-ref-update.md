---
title: NuGet-CLI-Befehl "Update"
description: Referenz für die nuget.exe-Update-Befehl
author: karann-msft
ms.author: karann
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: fc34550b3669d83466318645987cfd3078bc3c18
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545099"
---
# <a name="update-command-nuget-cli"></a>Der Befehl „commnad“ (NuGet CLI)

**Gilt für:** Paket Verbrauch &bullet; **unterstützte Versionen:** alle

Alle Pakete in einem Projekt aktualisiert (mit `packages.config`) auf ihren aktuellen verfügbaren Versionen. Es wird empfohlen, führen Sie ['Wiederherstellen'](cli-ref-restore.md) vor dem Ausführen der `update`. (Verwenden Sie zum Aktualisieren eines einzelnen Pakets [ `nuget install` ](cli-ref-install.md) ohne Angabe einer Versionsnummer, die in der Groß-/Kleinschreibung von NuGet die neueste Version installiert.)

Hinweis: `update` funktioniert nicht mit der Befehlszeilenschnittstelle, die unter Mono (Mac OS x oder Linux) oder wenn das PackageReference-Format verwenden.

Die `update` Befehl aktualisiert auch die Verweise der Assembly in der Projektdatei, vorausgesetzt die verweist bereits vorhanden. Wenn ein aktualisiertes Paket eine hinzugefügte Assembly hat, ist ein neuer Verweis *nicht* hinzugefügt. Ferner müssen neue paketabhängigkeiten nicht ihre Assemblyverweise hinzugefügt. Aktualisieren Sie das Paket in Visual Studio mithilfe der Paket-Manager-UI oder der Paket-Manager-Konsole, um diese Vorgänge im Rahmen eines Updates einzuschließen.

Mit diesem Befehl kann auch verwendet werden, um nuget.exe selbst aktualisieren mit der *-Self-Service* Flag.

## <a name="usage"></a>Verwendung

```cli
nuget update <configPath> [options]
```

in denen `<configPath>` identifiziert entweder eine `packages.config` oder Projektmappendatei, die die Abhängigkeiten des Projekts aufgeführt.

## <a name="options"></a>Optionen

| Option | Beschreibung |
| --- | --- |
| ConfigFile | Die NuGet-Konfigurationsdatei angewendet werden soll. Wenn nicht angegeben, `%AppData%\NuGet\NuGet.Config` (Windows) oder `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) verwendet wird.|
| FileConflictAction | Gibt die Aktion an, wenn Sie gefragt werden, überschrieben werden soll, oder ignorieren die vorhandene Dateien, die vom Projekt verwiesen wird. Werte sind *überschrieben werden soll, zu ignorieren, keine*. |
| ForceEnglishOutput | *(3.5 und höher)*  Erzwingt nuget.exe über eine invariante Kultur auf Englisch basierenden ausgeführt werden. |
| Hilfe | Zeigt die Informationen für den Befehl Hilfe. |
| Id | Gibt eine Liste der Paket-IDs zu aktualisieren. |
| MSBuildPath | *(4.0 und höher)*  Gibt den Pfad des MSBuild für die Verwendung mit dem Befehl vor `-MSBuildVersion`. |
| MSBuildVersion | *(3.2 und höher)*  Gibt die Version von MSBuild mit dem folgenden Befehl verwendet werden. Unterstützte Werte sind 4, 12, 14, 15. Standardmäßig die MSBuild in Ihrem Pfad ausgewählt wird, wird standardmäßig andernfalls die neueste installierte Version von MSBuild. |
| NonInteractive | Unterdrückt aufforderungen für Benutzereingaben oder Bestätigungen an. |
| Vorabversion | Ermöglicht das Aktualisieren auf Vorabversionen. Dieses Flag ist nicht erforderlich, beim Aktualisieren von Vorabversionen von Paketen, die bereits installiert sind. |
| RepositoryPath | Gibt den lokalen Ordner, in dem Pakete installiert sind. |
| Safe | Gibt an, dass nur mit der höchsten Version innerhalb der gleichen Haupt- und Nebenversionsnummern Version verfügbaren updates wie das installierte Paket installiert wird. |
| Self-Service | Nuget.exe auf die neueste Version aktualisiert wird; Alle anderen Argumente werden ignoriert. |
| Quelle | Gibt die Liste der Paketquellen (wie URLs), um nach Updates verwenden. Wenn nicht angegeben, wird der Befehl verwendet die Quellen in Konfigurationsdateien, finden Sie unter [Konfigurieren des NuGet-Verhaltens](../consume-packages/configuring-nuget-behavior.md). |
| Ausführlichkeit | Gibt an, die Anzahl der Details in der Ausgabe angezeigt: *normalen*, *quiet*, *ausführliche*. |
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
