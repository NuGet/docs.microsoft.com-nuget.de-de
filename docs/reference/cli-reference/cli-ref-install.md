---
title: Befehl "nuget CLI-Installation"
description: Referenz für den Installations Befehl "nuget. exe"
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: f39bcc67c5f659f05ef02f2579bcf07b4481bb27
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327787"
---
# <a name="install-command-nuget-cli"></a>Der Befehl „install“ (NuGet CLI)

**Gilt für:** &bullet; **unterstützte Versionen** von Paket Verbrauch: alle

Lädt ein Paket herunter und installiert es in ein Projekt, wobei die angegebenen Paketquellen standardmäßig auf den aktuellen Ordner zugreifen.

> [!Tip]
> Wenn Sie ein Paket direkt außerhalb des Kontexts eines Projekts herunterladen möchten, besuchen Sie die Seite des Pakets auf [nuget.org](https://www.nuget.org) , und wählen Sie den **Download** Link aus.

Wenn keine Quellen angegeben sind, werden die in der globalen Konfigurationsdatei `%appdata%\NuGet\NuGet.Config` (Windows) oder `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) aufgeführten Quellen verwendet. Weitere Informationen finden [Sie unter Allgemeine nuget-Konfigurationen](../../consume-packages/configuring-nuget-behavior.md) .

Wenn keine bestimmten Pakete angegeben werden, `install` werden alle Pakete installiert, die in der `packages.config` Datei des Projekts aufgelistet sind. [`restore`](cli-ref-restore.md)Dies ist vergleichbar mit.

Mit `install` dem Befehl wird eine Projektdatei oder `packages.config`nicht geändert. auf diese `restore` Weise ähnelt Sie in der Weise, dass nur Pakete auf dem Datenträger hinzugefügt werden, die Abhängigkeiten eines Projekts jedoch nicht geändert werden.

Fügen Sie zum Hinzufügen einer Abhängigkeit entweder über die Benutzeroberfläche oder die Konsole des Paket-Managers in Visual Studio `packages.config` ein Paket hinzu, `install` oder `restore`ändern Sie, und führen Sie dann entweder oder aus.

## <a name="usage"></a>Verwendung

```cli
nuget install <packageID | configFilePath> [options]
```

Dabei benennt das zu installierenden Paket (mit der aktuellen Version) `<configFilePath>` oder identifiziert `packages.config` die Datei, in der die zu installierenden Pakete aufgelistet sind. `<packageID>` Sie können mit der `-Version` Option eine bestimmte Version angeben.

## <a name="options"></a>Optionen

| Option | Beschreibung |
| --- | --- |
| ConfigFile | Die anzuwendende nuget-Konfigurationsdatei. Wenn nichts angegeben ist `%AppData%\NuGet\NuGet.Config` , wird (Windows `~/.nuget/NuGet/NuGet.Config` ) oder (Mac/Linux) verwendet.|
| Dependencyversion | *(4.4* und höher) Die Version der zu verwendenden Abhängigkeits Pakete. Dies kann eine der folgenden sein:<br/><ul><li>*Niedrigste* (Standard): die niedrigste Version</li><li>*Highestpatch*: die Version mit dem niedrigsten, niedrigsten, niedrigsten, größten Patch</li><li>*Highestminor*: die Version mit dem niedrigsten Haupt-, höchst-und Höchstwert</li><li>*Höchste*Version: die höchste Version</li></ul> |
| DisableParallelProcessing | Deaktiviert das parallele Installieren mehrerer Pakete. |
| ExcludeVersion | Installiert das Paket in einem Ordner mit dem Namen, der nur den Paketnamen und nicht die Versionsnummer hat. |
| FallbackSource | *(3.2 +)* Eine Liste von Paketquellen, die als Fallbacks verwendet werden sollen, falls das Paket nicht in der primären oder der Standard Quelle gefunden wurde. |
| ForceEnglishOutput | *(3.5* und höher) Erzwingt, dass "nuget. exe" mit einer invarianten, englischen Kultur ausgeführt wird. |
| Framework | *(4.4* und höher) Ziel Framework, das zum Auswählen von Abhängigkeiten verwendet wird. Der Standardwert ist "Any", wenn kein Wert angegeben ist. |
| Help | Zeigt Hilfe Informationen für den Befehl an. |
| NoCache | Verhindert, dass nuget zwischengespeicherte Pakete verwendet. Weitere Informationen finden Sie [unter Verwalten der globalen Pakete und Cache Ordner](../../consume-packages/managing-the-global-packages-and-cache-folders.md). |
| NonInteractive | Unterdrückt Eingabe Aufforderungen für Benutzereingaben oder Bestätigungen. |
| OutputDirectory | Gibt den Ordner an, in dem Pakete installiert werden. Wenn kein Ordner angegeben wird, wird der aktuelle Ordner verwendet. |
| PackageSaveMode | Gibt die Dateitypen an, die nach der Paketinstallation gespeichert werden `nuspec`sollen `nupkg`: einer `nuspec;nupkg`von, oder. |
| Vorab | Ermöglicht die Installation von vorab Versionen. Dieses Flag ist beim Wiederherstellen von Paketen mit `packages.config`nicht erforderlich. |
| RequireConsent | Überprüft, ob das Wiederherstellen von Paketen aktiviert ist, bevor die Pakete heruntergeladen und installiert werden. Weitere Informationen finden Sie unter [Paket Wiederherstellung](../../consume-packages/package-restore.md). |
| Projektmappenverzeichnis | Gibt den Stamm Ordner der Projekt Mappe an, für die Pakete wieder hergestellt werden sollen. |
| Source | Gibt die Liste der zu verwendenden Paketquellen (als URLs) an. Wenn der Befehl nicht angegeben wird, verwendet der Befehl die in den Konfigurationsdateien bereitgestellten Quellen, siehe [Allgemeine nuget-Konfigurationen](../../consume-packages/configuring-nuget-behavior.md). |
| Verbosity | Gibt den Umfang der in der Ausgabe angezeigten Details an: *Normal*, *quiet*, *ausführlich*. |
| Version | Gibt die Version des zu installierenden Pakets an. |

Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)

## <a name="examples"></a>Beispiele

```cli
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
