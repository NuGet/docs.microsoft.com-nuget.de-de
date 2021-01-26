---
title: Befehl "nuget CLI-Installation"
description: Referenz für den nuget.exe Installations Befehl
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 34b79bfa7a0dddf5da6b5c465293caec49129f6c
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779266"
---
# <a name="install-command-nuget-cli"></a>Installations Befehl (nuget-CLI)

**Gilt für:** &bullet; **unterstützte Versionen** von Paket Verbrauch: alle

Lädt ein Paket herunter und installiert es in ein Projekt, wobei die angegebenen Paketquellen standardmäßig auf den aktuellen Ordner zugreifen.

> [!Tip]
> Wenn Sie ein Paket direkt außerhalb des Kontexts eines Projekts herunterladen möchten, besuchen Sie die Seite des Pakets auf [nuget.org](https://www.nuget.org) , und wählen Sie den **Download** Link aus.

Wenn keine Quellen angegeben sind, werden die in der globalen Konfigurationsdatei `%appdata%\NuGet\NuGet.Config` (Windows) oder `~/.nuget/NuGet/NuGet.Config` (Mac/Linux) aufgeführten Quellen verwendet. Weitere Informationen finden [Sie unter Allgemeine nuget-Konfigurationen](../../consume-packages/configuring-nuget-behavior.md) .

Wenn keine bestimmten Pakete angegeben werden, werden `install` alle Pakete installiert, die in der Datei des Projekts aufgelistet sind `packages.config` . Dies ist vergleichbar mit [`restore`](cli-ref-restore.md) .

Mit dem `install` Befehl wird eine Projektdatei oder nicht geändert `packages.config` . auf diese Weise ähnelt Sie in der Weise `restore` , dass nur Pakete auf dem Datenträger hinzugefügt werden, die Abhängigkeiten eines Projekts jedoch nicht geändert werden.

Fügen Sie zum Hinzufügen einer Abhängigkeit entweder über die Benutzeroberfläche oder die Konsole des Paket-Managers in Visual Studio ein Paket hinzu, oder ändern Sie, `packages.config` und führen Sie dann entweder `install` oder aus `restore` .

## <a name="usage"></a>Verwendung

```cli
nuget install <packageID | configFilePath> [options]
```

`<packageID>`dabei benennt das zu installierenden Paket (mit der aktuellen Version) oder `<configFilePath>` identifiziert die Datei, in der `packages.config` die zu installierenden Pakete aufgelistet sind. Sie können mit der Option eine bestimmte Version angeben `-Version` .

## <a name="options"></a>Optionen

- **`-ConfigFile`**

  Die anzuwendende nuget-Konfigurationsdatei. Wenn nichts angegeben ist, `%AppData%\NuGet\NuGet.Config` wird (Windows) `~/.nuget/NuGet/NuGet.Config` oder `~/.config/NuGet/NuGet.Config` (Mac/Linux) verwendet.

- **`-DependencyVersion`**

  *(4.4* und höher) Die Version der zu verwendenden Abhängigkeits Pakete. Dies kann eine der folgenden sein:<br/><ul><li>*Niedrigste* (Standard): die niedrigste Version</li><li>*Highestpatch*: die Version mit dem niedrigsten, niedrigsten, niedrigsten, größten Patch</li><li>*Highestminor*: die Version mit dem niedrigsten Haupt-, höchst-und Höchstwert</li><li>*Höchste* Version: die höchste Version</li><li>*Ignore*: Es werden keine Abhängigkeits Pakete verwendet.</li></ul>

- **`-DirectDownload`**

  Direkt herunterladen, ohne Caches mit Metadaten oder Binärdateien aufzufüllen.

- **`-DisableParallelProcessing`**

  Deaktiviert das parallele Installieren mehrerer Pakete.

- **`-x|-ExcludeVersion`**

  Installiert das Paket in einem Ordner mit dem Namen, der nur den Paketnamen und nicht die Versionsnummer hat.

- **`-FallbackSource`**

  *(3.2 +)* Eine Liste von Paketquellen, die als Fallbacks verwendet werden sollen, falls das Paket nicht in der primären oder der Standard Quelle gefunden wurde.

- **`-ForceEnglishOutput`**

  *(3.5* und höher) Erzwingt das Ausführen von nuget.exe mit einer invarianten, englischen Kultur.

- **`-Framework`**

  *(4.4* und höher) Ziel Framework, das zum Auswählen von Abhängigkeiten verwendet wird. Der Standardwert ist "Any", wenn kein Wert angegeben ist.

- **`-?|-help`**

  Zeigt Hilfe Informationen für den Befehl an.

- **`-NoCache`**

  Verhindert, dass nuget zwischengespeicherte Pakete verwendet. Weitere Informationen finden Sie [unter Verwalten der globalen Pakete und Cache Ordner](../../consume-packages/managing-the-global-packages-and-cache-folders.md).

- **`-NonInteractive`**

  Unterdrückt Eingabe Aufforderungen für Benutzereingaben oder Bestätigungen.

- **`-OutputDirectory`**

  Gibt den Ordner an, in dem Pakete installiert werden. Wenn kein Ordner angegeben wird, wird der aktuelle Ordner verwendet.

- **`-PackageSaveMode`**

  Gibt die Dateitypen an, die nach der Paketinstallation gespeichert werden sollen: einer von `nuspec` , `nupkg` oder `nuspec;nupkg` .

- **`-PreRelease`**

  Ermöglicht die Installation von Paketen mit Vorabversionen Dieses Flag ist beim Wiederherstellen von Paketen mit nicht erforderlich `packages.config` .

- **`-RequireConsent`**

  Überprüft, ob das Wiederherstellen von Paketen aktiviert ist, bevor die Pakete heruntergeladen und installiert werden. Weitere Informationen finden Sie unter [Paket Wiederherstellung](../../consume-packages/package-restore.md).

- **`-SolutionDirectory`**

  Gibt den Stamm Ordner der Projekt Mappe an, für die Pakete wieder hergestellt werden sollen.

- **`-Source`**

   Gibt die Liste der zu verwendenden Paketquellen (als URLs) an. Wenn der Befehl nicht angegeben wird, verwendet der Befehl die in den Konfigurationsdateien bereitgestellten Quellen, siehe [Allgemeine nuget-Konfigurationen](../../consume-packages/configuring-nuget-behavior.md).

- **`-Verbosity [normal|quiet|detailed]`**

  Gibt den Umfang der in der Ausgabe angezeigten Details an: `normal` (Standard), `quiet` oder `detailed` .

- **`-Version`**

  Gibt die Version des zu installierenden Pakets an.

Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)

## <a name="examples"></a>Beispiele

```cli
nuget install elmah

nuget install packages.config

nuget install ninject -OutputDirectory c:\proj
```
