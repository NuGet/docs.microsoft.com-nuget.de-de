---
title: NuGet-CLI-Befehl Quellen | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 997ce736-91ba-4cd2-88c9-b4b168e3130a
description: "Referenz für die nuget.exe Datenquellen-Befehl"
keywords: NuGet Verweis Datenquellen, Datenquellen-Befehl
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 2eca8557840c467a60f5f708efe242cd83609164
ms.sourcegitcommit: bdcd2046b1b187d8b59716b9571142c02181c8fb
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/10/2018
---
# <a name="sources-command-nuget-cli"></a>Quellen-Befehl (NuGet CLI)

**Gilt für:** Paket Verbrauchs, Veröffentlichung &bullet; **unterstützte Versionen:** alle

Verwaltet die Liste der Datenquellen, die im Verzeichnis `%AppData%\NuGet\NuGet.Config` oder die angegebene Konfigurationsdatei.

Beachten Sie, dass der Quell-URL für nuget.org `https://api.nuget.org/v3/index.json`.

## <a name="usage"></a>Verwendung

```
nuget sources <operation> -Name <name> -Source <source>
```

auf dem `<operation>` ist einer der *auflisten, hinzufügen, entfernen, aktivieren, deaktivieren,* oder *Update*, `<name>` ist der Name der Quelle, und `<source>` ist die Quell-URL.

## <a name="options"></a>Optionen

| Option | Beschreibung |
| --- | --- |
| "ConfigFile" hinzu | *(2,5 +)*  Das NuGet-Konfigurationsdatei angewendet. Wenn nicht angegeben, *%AppData%\NuGet\NuGet.Config* verwendet wird. |
| ForceEnglishOutput | *(3.5 +)*  Erzwingt nuget.exe über eine invariante Kultur Englisch-basierte ausgeführt werden. |
| Format | Gilt für die `list` Aktion und kann `Detailed` (Standard) oder `Short`. |
| Hilfe | Zeigt die Hilfe Informationen für den Befehl. |
| Nicht interaktive | Unterdrückt aufforderungen für Benutzereingaben oder Bestätigungen an. |
| Kennwort | Gibt das Kennwort für die Authentifizierung mit der Quelle. |
| StorePasswordInClearText | Gibt an, um das Kennwort in unverschlüsselter Text statt das Standardverhalten des Speicherns von verschlüsselter Form speichern. |
| UserName | Gibt den Benutzernamen für die Authentifizierung mit der Quelle an. |
| Ausführlichkeit | Gibt die Anzahl der Details in der Ausgabe angezeigt: *normalen*, *stillen*, *detaillierte (2.5 und höher)*. |

> [!Note]
> Stellen Sie sicher, dass die Quellen Kennwort unter demselben Benutzerkontext hinzugefügt, wie die nuget.exe später verwendet wird, auf die Paketquelle zugreifen. Das Kennwort in der Config-Datei verschlüsselt gespeichert und kann nur in demselben Benutzerkontext entschlüsselt werden, da er verschlüsselt wurde. Z. B. Wenn Sie einen Build-Server verwenden wiederherzustellenden NuGet-Pakete, die das Kennwort verschlüsselt werden muss mit dem gleichen Windows-Benutzer unter dem der Build-Server-Aufgabe ausgeführt wird.

Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)

## <a name="examples"></a>Beispiele

```
nuget sources Add -Name "MyServer" -Source \\myserver\packages

nuget sources Disable -Name "MyServer"

nuget source Enable -Source "nuget.org"

nuget sources add -name foo.bar -source C:\NuGet\local -username foo -password bar -StorePasswordInClearText -configfile %AppData%\NuGet\my.config
```
