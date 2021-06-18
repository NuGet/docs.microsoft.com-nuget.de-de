---
title: Befehl zum Aktualisieren der NuGet-BEFEHLSZEILEnschnittstelle
description: Referenz für den befehl nuget.exe update
author: JonDouglas
ms.author: jodou
ms.date: 12/07/2017
ms.topic: reference
ms.openlocfilehash: 5f244e4cf15ca7afa0e6318a8c20d464ff75bd8e
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323647"
---
# <a name="update-command-nuget-cli"></a>Befehl "update" (NuGet-CLI)

**Gilt für:** Paketnutzung &bullet; **Unterstützte Versionen:** alle

Alle Pakete in einem Projekt werden (unter Verwendung von `packages.config`) auf die neuesten verfügbaren Versionen aktualisiert. Es wird empfohlen, ["restore"](cli-ref-restore.md) auszuführen, bevor Sie `update` ausführen. (Um ein einzelnes Paket zu aktualisieren, verwenden Sie [`nuget install`](cli-ref-install.md) , ohne eine Versionsnummer anzugeben. In diesem Fall installiert NuGet die neueste Version.)

Hinweis: funktioniert nicht mit der CLI unter `update` Mono (Mac OSX oder Linux) oder bei Verwendung des PackageReference-Formats.

Der `update` Befehl aktualisiert auch Assemblyverweise in der Projektdatei, sofern diese Verweise bereits vorhanden sind. Wenn ein aktualisiertes Paket über eine hinzugefügte Assembly verfügt, wird *kein* neuer Verweis hinzugefügt. Neuen Paketabhängigkeiten werden auch keine Assemblyverweise hinzugefügt. Um diese Vorgänge als Teil eines Updates einzubeziehen, aktualisieren Sie das Paket in Visual Studio mithilfe der Paket-Manager-Benutzeroberfläche oder der Paket-Manager-Konsole.

Dieser Befehl kann auch verwendet werden, um nuget.exe selbst mithilfe des Flags *-self* zu aktualisieren.

## <a name="usage"></a>Verwendung

```cli
nuget update <configPath> [options]
```

, wobei `<configPath>` entweder eine `packages.config` Projektmappendatei oder eine Projektmappendatei identifiziert, die die Abhängigkeiten des Projekts auflistet.

## <a name="options"></a>Optionen

- **`-ConfigFile`**

  Die zu übernehmende NuGet-Konfigurationsdatei. Wenn keine Angabe erfolgt, `%AppData%\NuGet\NuGet.Config` wird (Windows) `~/.nuget/NuGet/NuGet.Config` oder oder `~/.config/NuGet/NuGet.Config` (Mac/Linux) verwendet.
  
- **`-DependencyVersion [Lowest, HighestPatch, HighestMinor, Highest, Ignore]`**

  Gibt die Version der zu verwendenden Abhängigkeitspakete an, die eines der folgenden sein kann:<br/><ul><li>*Niedrigste* (Standardeinstellung): die niedrigste Version</li><li>*HighestPatch:* Die Version mit der niedrigsten Hauptversion, der niedrigsten Nebenversion und dem höchsten Patch</li><li>*HighestMinor:* Die Version mit der niedrigsten Hauptversion, der höchsten Nebenversion und dem höchsten Patch</li><li>*Höchste*: die höchste Version</li><li>*Ignorieren:* Es werden keine Abhängigkeitspakete verwendet.</li></ul>

- **`-FileConflictAction [PromptUser, Overwrite, Ignore]`**

  Gibt die Standardaktion an, wenn eine Datei aus einem Paket bereits im Zielprojekt vorhanden ist. Legen Sie auf `Overwrite` fest, um Dateien immer zu überschreiben. Legen Sie auf `Ignore` fest, um Dateien zu überspringen.

  Die `PromptUser` Standardaktion fordert für jede in Konflikt stehende Datei auf, es sei `OverwriteAll` denn, oder `IgnoreAll` wird angegeben, was für alle verbleibenden Dateien gilt.

- **`-ForceEnglishOutput`**

  *(3.5+)* Erzwingt die Ausführung nuget.exe mithilfe einer invarianten, englischsprachigen Kultur.

- **`-?|-help`**

  Zeigt Hilfeinformationen für den Befehl an.

- **`-Id`**

  Gibt eine Liste der zu aktualisierenden Paket-IDs an.

- **`-MSBuildPath`**

  *(4.0+)* Gibt den Pfad von MSBuild an, der mit dem Befehl verwendet werden soll, und hat Vorrang vor `-MSBuildVersion` .

- **`-MSBuildVersion`**

  *(3.2+)* Gibt die Version von MSBuild an, die mit diesem Befehl verwendet werden soll. Unterstützte Werte sind 4, 12, 14, 15.1, 15.3, 15.4, 15.5, 15.6, 15.7, 15.8, 15.9. Standardmäßig wird MSBuild in Ihrem Pfad ausgewählt, andernfalls wird standardmäßig die höchste installierte Version von MSBuild verwendet.

- **`-NonInteractive`**

  Unterdrückt Aufforderungen zu Benutzereingaben oder Bestätigungen.

- **`-PreRelease`**

  Ermöglicht das Aktualisieren auf Vorabversionen. Dieses Flag ist nicht erforderlich, wenn Vorabversionspakete aktualisiert werden, die bereits installiert sind.

- **`-RepositoryPath`**

  Gibt den lokalen Ordner an, in dem Pakete installiert werden.

- **`-Safe`**

  Gibt an, dass nur Updates mit der höchsten verfügbaren Version innerhalb der gleichen Haupt- und Nebenversion wie das installierte Paket installiert werden.

- **`-Self`**

  Updates `nuget.exe` auf die neueste Version. `-Source` kann verwendet werden, aber alle anderen Argumente werden ignoriert. Wenn keine Quelle bereitgestellt wird, wird unabhängig von den Einstellungen nach `nuget.org` Updates `NuGet.Config` gesucht.

- **`-Source`**

  Gibt die Liste der Paketquellen (als URLs) an, die für die Updates verwendet werden sollen. Wenn diese Angabe nicht erfolgt, verwendet der Befehl die in Konfigurationsdateien bereitgestellten Quellen. Weitere Informationen finden Sie unter [Allgemeine NuGet-Konfigurationen.](../../consume-packages/configuring-nuget-behavior.md)

- **`-Verbosity [normal|quiet|detailed]`**

  Gibt die Detailmenge an, die in der Ausgabe angezeigt wird: `normal` (Standard), `quiet` oder `detailed` .

- **`-Version`**

  Gibt bei Verwendung mit einer Paket-ID die Version des zu aktualisierenden Pakets an.

Siehe auch [Umgebungsvariablen.](cli-ref-environment-variables.md)

## <a name="examples"></a>Beispiele

```cli
nuget update

# update packages installed in solution.sln, using MSBuild version 14.0 to load the solution and its project(s).
nuget update solution.sln -MSBuildVersion 14

nuget update -safe

nuget update -self
```
