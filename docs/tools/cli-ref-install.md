---
title: NuGet-CLI-Befehl "Install"
description: Referenz für den Befehl "nuget.exe Install"
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: e609b01bc14083ce212f6d4d4c6d3412f0ee316b
ms.sourcegitcommit: 4d139cb54a46616ae48d1768fa108ae3bf450d5b
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/03/2018
ms.locfileid: "39508321"
---
# <a name="install-command-nuget-cli"></a>Der Befehl „install“ (NuGet CLI)

**Gilt für:** Paket Verbrauch &bullet; **unterstützte Versionen:** alle

Heruntergeladen und installiert ein Paket in einem Projekt als dem aktuellen Ordner, der mit der angegebenen Paketquellen.

> [!Tip]
> Um ein Paket im Kontext eines Projekts direkt herunterzuladen, besuchen Sie die Seite des Pakets [nuget.org](https://www.nuget.org) , und wählen Sie die **herunterladen** Link.

Wenn keine Quellen angegeben ist, ist die in die globale XML-Konfigurationsdatei aufgeführt `%appdata%\NuGet\NuGet.Config` (Windows) oder `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) verwendet werden. Finden Sie unter [Konfigurieren des NuGet-Verhaltens](../consume-packages/configuring-nuget-behavior.md) Weitere Details.

Wenn keine bestimmte Pakete angegeben werden, `install` installiert alle Pakete des Projekts aufgeführt `packages.config` Datei ähnelt somit [ `restore` ](cli-ref-restore.md).

Die `install` Befehl ändert sich nicht auf eine Projektdatei oder `packages.config`; auf diese Weise ähnelt `restore` in an, dass er nur Pakete, auf dem Datenträger hinzugefügt, sondern sich nicht auf die Abhängigkeiten eines Projekts ändert.

Um eine Abhängigkeit hinzuzufügen, ein Paket über die Paket-Manager-Benutzeroberfläche oder Konsole in Visual Studio hinzufügen oder ändern Sie `packages.config` und führen Sie dann entweder `install` oder `restore`.

## <a name="usage"></a>Verwendung

```cli
nuget install <packageID | configFilePath> [options]
```

in denen `<packageID>` benennt das Paket zu installieren (verwenden die neueste Version), oder `<configFilePath>` identifiziert die `packages.config` Datei, die die zu installierenden Pakete auflistet. Sie können angeben, dass eine bestimmte Version mit der `-Version` Option.

## <a name="options"></a>Optionen

| Option | Beschreibung |
| --- | --- |
| ConfigFile | Die NuGet-Konfigurationsdatei angewendet werden soll. Wenn nicht angegeben, `%AppData%\NuGet\NuGet.Config` (Windows) oder `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) verwendet wird.|
| Optionen "dependencyversion" | *(4.4 und höher)*  Die Version der abhängigkeitspakete zu verwenden, die in der folgenden Werte sind möglich:<br/><ul><li>*Niedrigste* (Standard): die niedrigste Version</li><li>*HighestPatch*: die Version mit der niedrigsten wichtigen, niedrigste kleinere, höchste Patch</li><li>*HighestMinor*: die Version mit der niedrigsten Hauptversion, die höchste kleinere, höchste-Patch</li><li>*Höchste*: die höchste Version</li></ul> |
| DisableParallelProcessing | Deaktiviert, die mehrere Pakete gleichzeitig installieren. |
| ExcludeVersion | Installiert das Paket in einen Ordner mit dem Namen mit nur den Paketnamen und nicht die Versionsnummer an. |
| FallbackSource | *(3.2 und höher)*  Eine Liste der Paketquellen, die als Fallbacks verwendet werden soll, für den Fall, dass das Paket nicht, auf dem primären gefunden wird oder Standardquelle. |
| ForceEnglishOutput | *(3.5 und höher)*  Erzwingt nuget.exe über eine invariante Kultur auf Englisch basierenden ausgeführt werden. |
| Framework | *(4.4 und höher)*  Zielframework wird verwendet, um Abhängigkeiten. Der Standardwert ist "Any", wenn nicht angegeben. |
| Hilfe | Zeigt die Informationen für den Befehl Hilfe. |
| NoCache | Verhindert, dass NuGet zwischengespeicherte Pakete verwenden. Finden Sie unter [Verwalten der globalen Paketordner und Cacheordner](../consume-packages/managing-the-global-packages-and-cache-folders.md). |
| NonInteractive | Unterdrückt aufforderungen für Benutzereingaben oder Bestätigungen an. |
| OutputDirectory | Gibt den Ordner, in dem Pakete installiert sind. Wenn kein Ordner angegeben wird, wird der aktuelle Ordner verwendet. |
| PackageSaveMode | Gibt die Typen von Dateien, die nach der Paketinstallation speichern: einer der `nuspec`, `nupkg`, oder `nuspec;nupkg`. |
| Vorabversion | Können Vorabversionen von Paketen installiert werden. Dieses Flag ist nicht erforderlich, beim Wiederherstellen von Paketen mit `packages.config`. |
| RequireConsent | Stellt sicher, dass die Wiederherstellung von Paketen aktiviert ist, vor dem Herunterladen und Installieren der Pakete. Weitere Informationen finden Sie unter [Paketwiederherstellung](../consume-packages/package-restore.md). |
| SolutionDirectory | Gibt an, der Stammordner der Projektmappe für das Wiederherstellen von Paketen. |
| Quelle | Gibt die Liste der Paketquellen (wie URLs), um verwenden. Wenn nicht angegeben, wird der Befehl verwendet die Quellen in Konfigurationsdateien, finden Sie unter [Konfigurieren des NuGet-Verhaltens](../consume-packages/configuring-nuget-behavior.md). |
| Ausführlichkeit | Gibt an, die Anzahl der Details in der Ausgabe angezeigt: *normalen*, *quiet*, *ausführliche*. |
| Version | Gibt die Version der zu installierenden Pakets an. |

Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)

## <a name="examples"></a>Beispiele

```cli
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
