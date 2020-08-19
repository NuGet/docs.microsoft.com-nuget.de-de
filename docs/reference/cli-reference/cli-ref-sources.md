---
title: Befehl "nuget CLI-Quellen"
description: Referenz für den Befehl "nuget.exe Quellen"
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 73c9cea8200a1ab1937d25a9a611ae7f2a943dba
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622589"
---
# <a name="sources-command-nuget-cli"></a>Quellen Befehl (nuget-CLI)

**Gilt für:** Paket Verbrauch, &bullet; **unterstützte Versionen** werden veröffentlicht: alle

Verwaltet die Liste der Quellen, die sich in der Benutzer Bereichs Konfigurationsdatei oder einer angegebenen Konfigurationsdatei befinden. Die Benutzer Bereichs Konfigurationsdatei befindet sich unter `%appdata%\NuGet\NuGet.Config` (Windows) und `~/.nuget/NuGet/NuGet.Config` (Mac/Linux).

Beachten Sie, dass die Quell-URL für nuget.org `https://api.nuget.org/v3/index.json` ist.

## <a name="usage"></a>Verwendung

```cli
nuget sources <operation> -Name <name> -Source <source>
```

Dabei ist "List", "Add", "Remove", "enable", " `<operation>` *Deaktivieren* " oder " *Update*", `<name>` der Name der Quelle und `<source>` die URL der Quelle. Sie können jeweils nur auf einer Quelle arbeiten.

## <a name="options"></a>Optionen

- **`-ConfigFile`**

  Die anzuwendende nuget-Konfigurationsdatei. Wenn nichts angegeben ist, `%AppData%\NuGet\NuGet.Config` wird (Windows) `~/.nuget/NuGet/NuGet.Config` oder `~/.config/NuGet/NuGet.Config` (Mac/Linux) verwendet.

- **`-ForceEnglishOutput`**

  *(3.5* und höher) Erzwingt das Ausführen von nuget.exe mit einer invarianten, englischen Kultur.

- **`-Format`**

  Gilt für die `list` Aktion und kann `Detailed` (die Standardeinstellung) oder sein `Short` .

- **`-?|-help`**

  Zeigt Hilfe Informationen für den Befehl an.

- **`-Name`**

  Name der Quelle.

- **`-NonInteractive`**

  Unterdrückt Eingabe Aufforderungen für Benutzereingaben oder Bestätigungen.

- **`-Password`**

  Gibt das Kennwort für die Authentifizierung mit der Quelle an.

- **`-src|-Source`**

  Pfad zur Paketquelle (n).

- **`-StorePasswordInClearText`**

  Gibt an, dass das Kennwort in unverschlüsseltem Text gespeichert wird, anstatt das Standardverhalten beim Speichern eines verschlüsselten Formulars.

- **`-UserName`**

  Gibt den Benutzernamen für die Authentifizierung mit der Quelle an.

- **`-ValidAuthenticationTypes`**

  Durch Trennzeichen getrennte Liste mit gültigen Authentifizierungstypen für diese Quelle. Standardmäßig sind alle Authentifizierungs Typen gültig. Beispiel: `basic,negotiate`.

- **`-Verbosity [normal|quiet|detailed]`**

  Gibt den Umfang der in der Ausgabe angezeigten Details an: `normal` (Standard), `quiet` oder `detailed` .

> [!Note]
> Stellen Sie sicher, dass Sie das Kennwort der Quellen im gleichen Benutzer Kontext hinzufügen, wie das nuget.exe später für den Zugriff auf die Paketquelle verwendet wird. Das Kennwort wird verschlüsselt in der Konfigurationsdatei gespeichert und kann nur im gleichen Benutzer Kontext entschlüsselt werden, in dem es verschlüsselt wurde. Wenn Sie z. b. einen Buildserver zum Wiederherstellen von nuget-Paketen verwenden, muss das Kennwort mit demselben Windows-Benutzer verschlüsselt werden, unter dem der buildservertask ausgeführt wird.

Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)

## <a name="examples"></a>Beispiele

```cli
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget sources Enable -Name "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
