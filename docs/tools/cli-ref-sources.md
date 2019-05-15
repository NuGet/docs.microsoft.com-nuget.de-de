---
title: NuGet-CLI-Befehl Quellen
description: Referenz für die nuget.exe Datenquellen-Befehl
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 94134b87f83e057d5d11a2722d9067fb76cc8e21
ms.sourcegitcommit: 4ea46498aee386b4f592b5ebba4af7f9092ac607
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/14/2019
ms.locfileid: "65610623"
---
# <a name="sources-command-nuget-cli"></a>Der Befehl „sources“ (NuGet-CLI)

**Gilt für:** -paketverbrauch, Veröffentlichung &bullet; **unterstützte Versionen:** alle

Verwaltet die Liste der Datenquellen, die sich in der Benutzerkonfigurationsdatei für den Bereich oder einer bestimmten Konfigurationsdatei befinden. Die Benutzerkonfigurationsdatei für den Bereich befindet sich unter `%appdata%\NuGet\NuGet.Config` (Windows) und `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).

Beachten Sie, dass die Quell-URL für nuget.org `https://api.nuget.org/v3/index.json` ist.

## <a name="usage"></a>Verwendung

```cli
nuget sources <operation> -Name <name> -Source <source>
```

in denen `<operation>` ist einer der *auflisten, hinzufügen, entfernen und Aktivierung, Deaktivierung* oder *Update*, `<name>` ist der Name der Quelle, und `<source>` ist die Quelle der URL. Sie können für nur eine Quelle zu einem Zeitpunkt aufzurufen.

## <a name="options"></a>Optionen

| Option | Beschreibung |
| --- | --- |
| ConfigFile | Die NuGet-Konfigurationsdatei angewendet werden soll. Wenn nicht angegeben, `%AppData%\NuGet\NuGet.Config` (Windows) oder `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) verwendet wird.|
| ForceEnglishOutput | *(3.5 und höher)*  Erzwingt nuget.exe über eine invariante Kultur auf Englisch basierenden ausgeführt werden. |
| Format | Gilt für die `list` Aktion und kann `Detailed` (Standard) oder `Short`. |
| Help | Zeigt die Informationen für den Befehl Hilfe. |
| NonInteractive | Unterdrückt aufforderungen für Benutzereingaben oder Bestätigungen an. |
| Kennwort | Gibt das Kennwort für die Authentifizierung mit der Quelle. |
| StorePasswordInClearText | Gibt an, um das Kennwort in unverschlüsselter Text anstelle des Standardverhaltens speichern verschlüsselten Form speichern. |
| UserName | Gibt den Benutzernamen für die Authentifizierung mit der Quelle an. |
| Verbosity | Gibt an, die Anzahl der Details in der Ausgabe angezeigt: *normalen*, *quiet*, *ausführliche*. |

> [!Note]
> Stellen Sie sicher, dass die Quellen das Kennwort unter dem gleichen Benutzerkontext hinzufügen, wie die nuget.exe später verwendet wird, auf die Paketquelle. Das Kennwort in der Config-Datei verschlüsselt gespeichert und kann nur in demselben Benutzerkontext entschlüsselt werden, da er verschlüsselt wurde. Zum Beispiel wenn Sie einen Buildserver verwenden zum Wiederherstellen von NuGet-Pakete, die das Kennwort verschlüsselt sein muss mit dem gleichen Windows-Benutzer, unter dem der Build-Server-Task ausgeführt wird.

Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)

## <a name="examples"></a>Beispiele

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget sources Enable -Name "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
