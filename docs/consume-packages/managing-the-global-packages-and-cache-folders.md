---
title: 'Gewusst wie: Verwalten der globalen Pakete, des Caches und temporärer Ordner in NuGet'
description: So verwalten Sie den globalen Paketinstallationsordner, den Paketcache und die auf einem Computer vorhandenen temporären Ordner, die bei der Installation, Wiederherstellung und Aktualisierung von Paketen verwendet werden.
author: karann-msft
ms.author: karann
ms.date: 03/19/2018
ms.topic: conceptual
ms.openlocfilehash: e2672aa0bf57242526364639f0df74f9d1adb934
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237321"
---
# <a name="managing-the-global-packages-cache-and-temp-folders"></a>Verwalten von globalen Pakete-, Cache- und temporären Ordnern

Wann immer Sie ein Paket installieren, aktualisieren oder wiederherstellen, verwaltet NuGet Pakete und Paketinformationen in mehreren Ordnern außerhalb Ihrer Projektstruktur:

| name | Beschreibung und Speicherort (pro Benutzer)|
| --- | --- |
| global&#8209;packages | Im Ordner *global-packages* installiert NuGet alle heruntergeladenen Pakete. Jedes Paket wird vollständig in einen Unterordner erweitert, der mit dem Paketbezeichner und der Versionsnummer übereinstimmt. Projekte, die das [PackageReference](package-references-in-project-files.md)-Format verwenden, verwenden immer Pakete direkt aus diesem Ordner. Bei Verwendung der [packages.config](../reference/packages-config.md) werden Pakete in den Ordner *global-packages* installiert und dann in den Ordner `packages` des Projekts kopiert.<br/><ul><li>Windows: `%userprofile%\.nuget\packages`</li><li>Mac/Linux: `~/.nuget/packages`</li><li>Überschreiben mit der Umgebungsvariable NUGET_PACKAGES, den [Konfigurationseinstellungen](../reference/nuget-config-file.md#config-section) `globalPackagesFolder` oder `repositoryPath` (bei Verwendung von PackageReference bzw. `packages.config`) oder der MSBuild-Eigenschaft `RestorePackagesPath` (nur MSBuild). Die Umgebungsvariable hat Vorrang vor der Konfigurationseinstellung.</li></ul> |
| http&#8209;cache | Der Visual Studio-Paket-Manager (NuGet 3.x und höher) und das `dotnet`-Tool speichern Kopien heruntergeladener Pakete in diesem Cache (gespeichert als `.dat`-Dateien), die in Unterordnern für jede Paketquelle organisiert sind. Pakete werden nicht aufgelöst, und der Cache hat eine Ablaufzeit von 30 Minuten.<br/><ul><li>Windows: `%localappdata%\NuGet\v3-cache`</li><li>Mac/Linux: `~/.local/share/NuGet/v3-cache`</li><li>Überschreiben mit der Umgebungsvariable NUGET_HTTP_CACHE_PATH.</li></ul> |
| temp | Ein Ordner, in dem NuGet während der verschiedenen Vorgänge temporäre Dateien speichert.<br/><li>Windows: `%temp%\NuGetScratch`</li><li>Mac/Linux: `/tmp/NuGetScratch`</li></ul> |
| plugins-cache **4.8 und höher** | Ein Ordner, in den NuGet die Ergebnisse aus der Vorgangsanspruchsanforderung speichert.<br/><ul><li>Windows: `%localappdata%\NuGet\plugins-cache`</li><li>Mac/Linux: `~/.local/share/NuGet/plugins-cache`</li><li>Überschreiben mit der Umgebungsvariable NUGET_PLUGINS_CACHE_PATH.</li></ul> |

> [!Note]
> NuGet 3.5 und Vorgängerversionen verwenden *packages-cache* anstelle von *http-cache* , der sich unter `%localappdata%\NuGet\Cache` befindet.

Durch die Verwendung des Cacheordners und des Ordners *global-packages* vermeidet NuGet im Allgemeinen das Herunterladen von Paketen, die bereits auf dem Computer vorhanden sind. Dadurch wird die Leistung von Installations-, Update- und Wiederherstellungsvorgängen verbessert. Bei der Verwendung von PackageReference wird durch den Ordner *global-packages* ebenfalls vermieden, dass heruntergeladene Pakete in Projektordnern aufbewahrt werden, wo sie versehentlich zur Quellcodeverwaltung hinzugefügt werden. Auf diese Weise belegt NuGet noch weniger Computerspeicher.

Wenn Sie aufgefordert werden, ein Paket abzurufen, sucht NuGet zuerst im Ordner *global-packages*. Wenn die genaue Version des Pakets nicht vorhanden ist, prüft NuGet alle Nicht-HTTP-Paketquellen. Wenn das Paket immer noch nicht gefunden wird, sucht NuGet nach dem Paket im *http-cache* , es sei denn, Sie geben `--no-cache` mit `dotnet.exe`-Befehlen oder `-NoCache` mit `nuget.exe`-Befehlen an. Wenn sich das Paket nicht im Cache befindet oder der Cache nicht verwendet wird, ruft NuGet das Paket über HTTP ab.

Weitere Informationen finden Sie unter [Was geschieht bei der Paketinstallation?](../concepts/package-installation-process.md).

## <a name="viewing-folder-locations"></a>Anzeigen der Speicherorte von Ordnern

Speicherorte lassen sich auch über den Befehl [nuget locals](../reference/cli-reference/cli-ref-locals.md) anzeigen:

```cli
# Display locals for all folders: global-packages, http cache, temp and plugins cache
nuget locals all -list
```

Typische Ausgabe (Windows; „user1“ ist der aktuelle Benutzername):

```output
http-cache: C:\Users\user1\AppData\Local\NuGet\v3-cache
global-packages: C:\Users\user1\.nuget\packages\
temp: C:\Users\user1\AppData\Local\Temp\NuGetScratch
plugins-cache: C:\Users\user1\AppData\Local\NuGet\plugins-cache
```

(`package-cache` wird in NuGet 2.x verwendet und mit NuGet 3.5 und Vorgängerversionen angezeigt.)

Mit dem Befehl [dotnet nuget locals](/dotnet/core/tools/dotnet-nuget-locals) können Sie auch die Speicherorte von Ordnern anzeigen:

```dotnetcli
dotnet nuget locals all --list
```

Typische Ausgabe (Mac/Linux; „user1“ ist der aktuelle Benutzername):

```output
info : http-cache: /home/user1/.local/share/NuGet/v3-cache
info : global-packages: /home/user1/.nuget/packages/
info : temp: /tmp/NuGetScratch
info : plugins-cache: /home/user1/.local/share/NuGet/plugins-cache
```

Verwenden Sie `http-cache`, `global-packages`, `temp` oder `plugins-cache` anstelle von `all`, um den Speicherort eines einzelnen Ordners anzuzeigen.

## <a name="clearing-local-folders"></a>Löschen von lokalen Ordnern

Wenn beim Installieren von Paketen Probleme auftreten bzw. Sie sicherstellen wollen, dass die Pakete aus einem Remotekatalog installiert werden, verwenden Sie die Option `locals --clear` (dotnet.exe) oder `locals -clear` (nuget.exe). Geben Sie dabei den zu löschenden Ordner an, oder `all`, um alle Ordner zu löschen:

```cli
# Clear the 3.x+ cache (use either command)
dotnet nuget locals http-cache --clear
nuget locals http-cache -clear

# Clear the 2.x cache (NuGet CLI 3.5 and earlier only)
nuget locals packages-cache -clear

# Clear the global packages folder (use either command)
dotnet nuget locals global-packages --clear
nuget locals global-packages -clear

# Clear the temporary cache (use either command)
dotnet nuget locals temp --clear
nuget locals temp -clear

# Clear the plugins cache (use either command)
dotnet nuget locals plugins-cache --clear
nuget locals plugins-cache -clear

# Clear all caches (use either command)
dotnet nuget locals all --clear
nuget locals all -clear
```

Alle Pakete, die von Projekten verwendet werden, die derzeit in Visual Studio geöffnet sind, werden nicht aus dem Ordner *global-packages* gelöscht.

Ab Visual Studio 2017 verwenden Sie den Menübefehl **Extras > NuGet-Paket-Manager > Paket-Manager-Einstellungen** , und wählen Sie dann **Alle NuGet-Caches leeren**. Die Verwaltung des Caches ist derzeit nicht über die Paket-Manager-Konsole möglich. Verwenden Sie in Visual Studio 2015 stattdessen die CLI-Befehle.

![NuGet-Optionsbefehl zum Bereinigen des Caches](media/options-clear-caches.png)

## <a name="troubleshooting-errors"></a>Problembehandlung bei Fehlern

Folgende Fehler können beim Verwenden von `nuget locals` oder `dotnet nuget locals` auftreten:

- *Fehler: Der Prozess kann nicht auf die Datei <package> zugreifen, da sie von einem anderen Prozess verwendet wird.* oder *Fehler beim Löschen der lokalen Ressourcen: Mindestens eine Datei konnte nicht gelöscht werden.*

    Mindestens eine Datei im Ordner wird von einem anderen Prozess verwendet; beispielsweise ist ein Visual Studio-Projekt geöffnet, das sich auf Pakete im Ordner *global-packages* bezieht. Schließen Sie diese Prozesse, und wiederholen Sie den Vorgang.

- *Fehler: Der Zugriff auf den Pfad <path> wird verweigert.* oder *Das Verzeichnis ist nicht leer.*

    Sie haben keine Berechtigung zum Löschen von Dateien in dem Cache. Ändern Sie die Zugriffsberechtigungen für den Ordner, wenn möglich, und wiederholen Sie den Vorgang. Wenden Sie sich anderenfalls an Ihren Systemadministrator.

- *Fehler: Der angegebene Pfad und/oder Dateiname sind zu lang. Der vollqualifizierte Dateiname muss weniger als 260 Zeichen umfassen, und der Verzeichnisname muss kürzer als 248 Zeichen sein.*

    Kürzen Sie die Ordnernamen, und wiederholen Sie den Vorgang.
