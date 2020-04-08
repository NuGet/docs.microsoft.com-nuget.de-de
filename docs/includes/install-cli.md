---
ms.openlocfilehash: 5197447531288a8b071354dbeb3a3ae02f7cce09
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/07/2020
ms.locfileid: "73610531"
---
#### <a name="windows"></a>Windows

> [!Note]
> Für die Ausführung von NuGet.exe 5.0 und höher ist .NET Framework 4.7.2 erforderlich.

1. Besuchen Sie [nuget.org/downloads](https://nuget.org/downloads), und wählen Sie NuGet 3.3 oder höher aus (2.8.6 ist nicht kompatibel mit Mono). Die neueste Version wird immer empfohlen, und 4.1.0+ ist erforderlich, um Pakete in „nuget.org“ zu veröffentlichen.
1. Jeder Download ist direkt die Datei `nuget.exe`. Weisen Sie Ihren Browser an, die Datei in einem Ordner Ihrer Wahl zu speichern. Die Datei ist *kein* Installationsprogramm; es wird nichts angezeigt, wenn Sie es direkt über den Browser ausführen.
1. Fügen Sie den Ordner, in dem Sie `nuget.exe` platziert haben, Ihrer Umgebungsvariablen PATH hinzu, um das CLI-Tool von überall aus verwenden zu können.

#### <a name="macoslinux"></a>macOS/Linux

Das Verhalten kann je nach Betriebssystemdistribution leicht variieren.

1. Installieren Sie [Mono 4.4.2 oder höher](https://www.mono-project.com/docs/getting-started/install/).

1. Führen Sie an einer Shelleingabeaufforderung folgenden Befehl aus:

    ```bash
    # Download the latest stable `nuget.exe` to `/usr/local/bin`
    sudo curl -o /usr/local/bin/nuget.exe https://dist.nuget.org/win-x86-commandline/latest/nuget.exe
    ```

1. Erstellen Sie einen Alias, indem Sie das folgende Skript der entsprechenden Datei für Ihr Betriebssystem hinzufügen (in der Regel `~/.bash_aliases` oder `~/.bash_profile`):

    ```bash
    # Create as alias for nuget
    alias nuget="mono /usr/local/bin/nuget.exe"
    ```

1. Laden Sie die Shell neu.  Testen Sie die Installation, indem Sie `nuget` ohne Parameter eingeben. Die NuGet-CLI-Hilfe sollte angezeigt werden.
