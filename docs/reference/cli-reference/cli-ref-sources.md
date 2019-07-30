---
title: Befehl "nuget CLI-Quellen"
description: Referenz für den Befehl "nuget. exe Sources"
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 94134b87f83e057d5d11a2722d9067fb76cc8e21
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327597"
---
# <a name="sources-command-nuget-cli"></a>Der Befehl „sources“ (NuGet-CLI)

**Gilt für:** Paket Verbrauch, &bullet; **unterstützte Versionen** werden veröffentlicht: alle

Verwaltet die Liste der Quellen, die sich in der Benutzer Bereichs Konfigurationsdatei oder einer angegebenen Konfigurationsdatei befinden. Die Benutzer Bereichs Konfigurationsdatei befindet sich `%appdata%\NuGet\NuGet.Config` unter (Windows) `~/.nuget/NuGet/NuGet.Config` und (Mac/Linux).

Beachten Sie, dass die Quell-URL für nuget.org `https://api.nuget.org/v3/index.json` ist.

## <a name="usage"></a>Verwendung

```cli
nuget sources <operation> -Name <name> -Source <source>
```

`<name>` `<source>` dabei ist "List", "Add", "Remove", "enable", "deaktivieren" oder "Update", der Name der Quelle und die URL der Quelle. `<operation>` Sie können jeweils nur auf einer Quelle arbeiten.

## <a name="options"></a>Optionen

| Option | Beschreibung |
| --- | --- |
| ConfigFile | Die anzuwendende nuget-Konfigurationsdatei. Wenn nichts angegeben ist `%AppData%\NuGet\NuGet.Config` , wird (Windows `~/.nuget/NuGet/NuGet.Config` ) oder (Mac/Linux) verwendet.|
| ForceEnglishOutput | *(3.5* und höher) Erzwingt, dass "nuget. exe" mit einer invarianten, englischen Kultur ausgeführt wird. |
| Format | Gilt für die `list` Aktion und kann ( `Detailed` die Standardeinstellung) oder `Short`sein. |
| Help | Zeigt Hilfe Informationen für den Befehl an. |
| NonInteractive | Unterdrückt Eingabe Aufforderungen für Benutzereingaben oder Bestätigungen. |
| Kennwort | Gibt das Kennwort für die Authentifizierung mit der Quelle an. |
| StorePasswordInClearText | Gibt an, dass das Kennwort in unverschlüsseltem Text gespeichert wird, anstatt das Standardverhalten beim Speichern eines verschlüsselten Formulars. |
| UserName | Gibt den Benutzernamen für die Authentifizierung mit der Quelle an. |
| Verbosity | Gibt den Umfang der in der Ausgabe angezeigten Details an: *Normal*, *quiet*, *ausführlich*. |

> [!Note]
> Stellen Sie sicher, dass Sie das Kennwort der Quellen im gleichen Benutzer Kontext hinzufügen, wie "nuget. exe" später für den Zugriff auf die Paketquelle verwendet wird. Das Kennwort wird verschlüsselt in der Konfigurationsdatei gespeichert und kann nur im gleichen Benutzer Kontext entschlüsselt werden, in dem es verschlüsselt wurde. Wenn Sie z. b. einen Buildserver zum Wiederherstellen von nuget-Paketen verwenden, muss das Kennwort mit demselben Windows-Benutzer verschlüsselt werden, unter dem der buildservertask ausgeführt wird.

Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)

## <a name="examples"></a>Beispiele

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget sources Enable -Name "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
