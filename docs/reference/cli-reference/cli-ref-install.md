---
title: Befehl "nuget CLI-Installation"
description: Referenz für den Installations Befehl "nuget. exe"
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 6c49b2406462eae6ce45c65dfd8b3a9eb1077e73
ms.sourcegitcommit: 415c70d7014545c1f65271a2debf8c3c1c5eb688
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/06/2020
ms.locfileid: "77036941"
---
# <a name="install-command-nuget-cli"></a>Der Befehl „install“ (NuGet CLI)

**Gilt für:** Paket Verbrauch &bullet; **unterstützten Versionen:** alle

Lädt ein Paket herunter und installiert es in ein Projekt, wobei die angegebenen Paketquellen standardmäßig auf den aktuellen Ordner zugreifen.

> [!Tip]
> Wenn Sie ein Paket direkt außerhalb des Kontexts eines Projekts herunterladen möchten, besuchen Sie die Seite des Pakets auf [nuget.org](https://www.nuget.org) , und wählen Sie den **Download** Link aus.

Wenn keine Quellen angegeben sind, werden die in der globalen Konfigurationsdatei `%appdata%\NuGet\NuGet.Config` (Windows) oder `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) aufgeführten Quellen verwendet. Weitere Informationen finden [Sie unter Allgemeine nuget-Konfigurationen](../../consume-packages/configuring-nuget-behavior.md) .

Wenn keine bestimmten Pakete angegeben werden, installiert `install` alle Pakete, die in der `packages.config`-Datei des Projekts aufgeführt sind, sodass Sie [`restore`](cli-ref-restore.md)ähnelt.

Mit dem Befehl "`install`" wird eine Projektdatei oder `packages.config`nicht geändert. auf diese Weise ähnelt Sie `restore` darin, dass nur Pakete auf dem Datenträger hinzugefügt werden, die Abhängigkeiten eines Projekts jedoch nicht geändert werden.

Fügen Sie zum Hinzufügen einer Abhängigkeit entweder über die Benutzeroberfläche oder die Konsole des Paket-Managers in Visual Studio ein Paket hinzu, oder ändern Sie `packages.config`, und führen Sie dann entweder `install` oder `restore`aus.

## <a name="usage"></a>Verwendung

```cli
nuget install <packageID | configFilePath> [options]
```

Dabei benennt `<packageID>` das zu installierenden Paket (mit der aktuellen Version), oder `<configFilePath>` die `packages.config` Datei, in der die zu installierenden Pakete aufgelistet sind. Sie können mit der Option `-Version` eine bestimmte Version angeben.

## <a name="options"></a>Tastatur

| Option | BESCHREIBUNG |
| --- | --- |
| ConfigFile | Die anzuwendende nuget-Konfigurationsdatei. Wenn nicht angegeben, wird `%AppData%\NuGet\NuGet.Config` (Windows) oder `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) verwendet.|
| Dependencyversion | *(4.4* und höher) Die Version der zu verwendenden Abhängigkeits Pakete. Dies kann eine der folgenden sein:<br/><ul><li>*Niedrigste* (Standard): die niedrigste Version</li><li>*Highestpatch*: die Version mit dem niedrigsten, niedrigsten, niedrigsten, größten Patch</li><li>*Highestminor*: die Version mit dem niedrigsten Haupt-, höchst-und Höchstwert</li><li>*Höchste*Version: die höchste Version</li><li>*Ignore*: Es werden keine Abhängigkeits Pakete verwendet.</li></ul> |
| DisableParallelProcessing | Deaktiviert das parallele Installieren mehrerer Pakete. |
| ExcludeVersion | Installiert das Paket in einem Ordner mit dem Namen, der nur den Paketnamen und nicht die Versionsnummer hat. |
| FallbackSource | *(3.2 +)* Eine Liste von Paketquellen, die als Fallbacks verwendet werden sollen, falls das Paket nicht in der primären oder der Standard Quelle gefunden wurde. |
| ForceEnglishOutput | *(3.5* und höher) Erzwingt, dass "nuget. exe" mit einer invarianten, englischen Kultur ausgeführt wird. |
| Framework | *(4.4* und höher) Ziel Framework, das zum Auswählen von Abhängigkeiten verwendet wird. Der Standardwert ist "Any", wenn kein Wert angegeben ist. |
| Hilfe | Zeigt Hilfe Informationen für den Befehl an. |
| NoCache | Verhindert, dass nuget zwischengespeicherte Pakete verwendet. Weitere Informationen finden Sie [unter Verwalten der globalen Pakete und Cache Ordner](../../consume-packages/managing-the-global-packages-and-cache-folders.md). |
| NonInteractive | Unterdrückt Eingabe Aufforderungen für Benutzereingaben oder Bestätigungen. |
| OutputDirectory | Gibt den Ordner an, in dem Pakete installiert werden. Wenn kein Ordner angegeben wird, wird der aktuelle Ordner verwendet. |
| PackageSaveMode | Gibt die Dateitypen an, die nach der Paketinstallation gespeichert werden sollen: eine der `nuspec`, `nupkg`oder `nuspec;nupkg`. |
| PreRelease | Ermöglicht die Installation von vorab Versionen. Dieses Flag ist beim Wiederherstellen von Paketen mit `packages.config`nicht erforderlich. |
| RequireConsent | Überprüft, ob das Wiederherstellen von Paketen aktiviert ist, bevor die Pakete heruntergeladen und installiert werden. Weitere Informationen finden Sie unter [Paket Wiederherstellung](../../consume-packages/package-restore.md). |
| Projektmappenverzeichnis | Gibt den Stamm Ordner der Projekt Mappe an, für die Pakete wieder hergestellt werden sollen. |
| `Source` | Gibt die Liste der zu verwendenden Paketquellen (als URLs) an. Wenn der Befehl nicht angegeben wird, verwendet der Befehl die in den Konfigurationsdateien bereitgestellten Quellen, siehe [Allgemeine nuget-Konfigurationen](../../consume-packages/configuring-nuget-behavior.md). |
| Ausführlichkeit | Gibt den Umfang der in der Ausgabe angezeigten Details an: *Normal*, *quiet*, *ausführlich*. |
| Version | Gibt die Version des zu installierenden Pakets an. |

Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)

## <a name="examples"></a>Beispiele

```cli
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
