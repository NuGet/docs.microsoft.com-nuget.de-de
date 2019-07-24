---
title: Verwalten von NuGet-Paketen mit der nuget.exe-CLI
description: Anweisungen zum Verwenden der nuget.exe-CLI zum Arbeiten mit NuGet-Paketen.
author: mikejo5000
ms.author: mikejo
ms.date: 06/03/2019
ms.topic: conceptual
ms.openlocfilehash: a7177b956930835693921163e634321548c22462
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842367"
---
# <a name="manage-packages-using-the-nugetexe-cli"></a>Verwalten von Paketen mit der nuget.exe-CLI

Mit dem CLI-Tool können Sie auf einfache Weise NuGet-Pakete in Projekten und Projektmappen aktualisieren und wiederherstellen. Dieses Tool bietet alle Funktionen von NuGet unter Windows und stellt darüber hinaus die meisten Features für Mac und Linux unter Mono bereit.

Die nuget.exe-CLI ist für .NET Framework-Projekte und Projekte im Nicht-SDK-Format vorgesehen (z. B. Projekte im Nicht-SDK-Format, die auf .NET-Standardbibliotheken ausgerichtet sind). Wenn Sie ein Nicht-SDK-Projekt verwenden, das zu `PackageReference` migriert wurde, verwenden Sie stattdessen die dotnet-CLI. Die NuGet-CLI erfordert eine Datei [packages.config](../reference/packages-config.md) für Paketverweise.

> [!NOTE]
> In den meisten Szenarien wird empfohlen, [Nicht-SDK-Projekte mit Verwendung von `packages.config` zu PackageReference zu migrieren](../reference/migrate-packages-config-to-package-reference.md). Anschließend können Sie anstelle der `nuget.exe`-CLI die dotnet-CLI verwenden. Für C++- und ASP.NET-Projekte ist momentan keine Migration verfügbar.

Dieser Artikel zeigt die grundlegende Verwendung einiger der gängigsten nuget.exe-CLI-Befehle. Bei den meisten dieser Befehle sucht das CLI-Tool nach einer Projektdatei im aktuellen Verzeichnis, sofern keine Projektdatei im Befehl angegeben ist. Eine vollständige Liste der verfügbaren Befehle und Argumente finden Sie in der [Referenz zur nuget.exe-CLI](../tools/nuget-exe-cli-reference.md).

## <a name="prerequisites"></a>Erforderliche Komponenten

- Installieren Sie die `nuget.exe`-CLI, indem Sie sie von [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe) herunterladen, die `.exe`-Datei in einen geeigneten Ordner speichern und den Ordner der Umgebungsvariable PATH hinzufügen.

## <a name="install-a-package"></a>Installieren eines Pakets

Mit dem Befehl [install](../tools/cli-ref-install.md) wird ein Projekt heruntergeladen und in einem Projekt installiert. Die Installation erfolgt standardmäßig im aktuellen Ordner, unter Verwendung der angegebenen Paketquellen. Installieren Sie neue Pakete im Ordner *packages* in Ihrem Projektstammverzeichnis.

> [!IMPORTANT]
> Der `install`-Befehl nimmt keine Änderungen an einer Projektdatei oder *packages.config* vor. Damit ähnelt er `restore` darin, dass Pakete nur zum Datenträger hinzugefügt, aber die Abhängigkeiten eines Projekts nicht geändert werden. Um eine Abhängigkeit hinzuzufügen, fügen Sie ein Paket entweder über den Paket-Manager oder die Konsole in Visual Studio hinzu. Als dritte Möglichkeit können Sie *packages.config* ändern und anschließend `install` oder `restore` ausführen.

1. Öffnen Sie eine Befehlszeile, und wechseln Sie zu dem Verzeichnis, das Ihre Projektdatei enthält.

2. Verwenden Sie den folgenden Befehl, um ein NuGet-Paket im Ordner *packages* zu installieren.

    ```cli
    nuget install <packageID> -OutputDirectory packages
    ```

    Um das `Newtonsoft.json`-Paket im Ordner *packages* zu installieren, verwenden Sie den folgenden Befehl:

    ```cli
    nuget install Newtonsoft.Json -OutputDirectory packages
    ```

Alternativ können Sie den folgenden Befehl verwenden, um ein NuGet-Paket unter Verwendung einer vorhandenen `packages.config`-Datei im Ordner *packages* zu installieren. Hierdurch wird das Paket nicht zu Ihren Projektabhängigkeiten hinzugefügt, sondern lokal installiert.

```cli
nuget install packages.config -OutputDirectory packages
```

## <a name="install-a-specific-version-of-a-package"></a>Installieren einer bestimmten Paketversion

Wenn bei Verwendung des Befehls [install](../tools/cli-ref-install.md) keine Version angegeben wird, installiert NuGet die neueste Version des Pakets. Sie können auch eine bestimmte Version eines Pakets installieren:

```cli
nuget install <packageID | configFilePath> -Version <version>
```

Verwenden Sie beispielsweise diesen Befehl, um Version 12.0.1 des `Newtonsoft.json`-Pakets hinzuzufügen:

```cli
nuget install Newtonsoft.Json -Version 12.0.1
```

Weitere Informationen zu Einschränkungen und Verhalten von `install` finden Sie unter [Installieren eines Pakets](#install-a-package).

## <a name="remove-a-package"></a>Entfernen eines Pakets

Um ein Paket oder mehrere Pakete zu entfernen, löschen Sie die betreffenden Pakete aus dem Ordner *packages*.

Wenn Sie Pakete erneut installieren möchten, verwenden Sie den Befehl `restore` oder `install`.

## <a name="list-packages"></a>Auflisten von Paketen

Sie können über den Befehl [list](../tools/cli-ref-list.md) eine Liste der Pakete einer angegebenen Quelle anzeigen. Verwenden Sie die Option `-Source`, um die Suche einzuschränken.

```cli
nuget list -Source <source>
```

Listen Sie beispielsweise die Pakete im Ordner *packages* auf.

```cli
nuget list -Source C:\Users\username\source\repos\MyProject\packages
```

Wenn Sie einen Suchbegriff verwenden, umfasst die Suche die Namen von Paketen, Tags und Paketbeschreibungen.

```cli
nuget list <search term>
```

## <a name="update-an-individual-package"></a>Aktualisieren eines einzelnen Pakets

NuGet installiert die neueste Version eines Pakets, wenn bei Verwendung des `install`-Befehls keine Version angegeben wird.

## <a name="update-all-packages"></a>Aktualisieren aller Pakete

Verwenden Sie den Befehl [update](../tools/cli-ref-update.md), um alle Pakete zu aktualisieren. Alle Pakete in einem Projekt werden (unter Verwendung von `packages.config`) auf die neuesten verfügbaren Versionen aktualisiert. Es wird empfohlen, `restore` vor `update` auszuführen.

```cli
nuget update
```

## <a name="restore-packages"></a>Pakete wiederherstellen

Verwenden Sie zum Wiederherstellen den Befehl [restore](../tools/cli-ref-restore.md). Mit diesem Befehl werden alle Pakete heruntergeladen und installiert, die im Ordner *packages* fehlen.

`restore` fügt Pakete nur zum Datenträger hinzu, die Abhängigkeiten eines Projekts werden nicht geändert. Um Projektabhängigkeiten wiederherzustellen, ändern Sie `packages.config`, und verwenden Sie anschließend den Befehl `restore`.

Öffnen Sie wie bei anderen `dotnet`-CLI-Befehlen zunächst eine Befehlszeile, und wechseln Sie zu dem Verzeichnis, das die Projektdatei enthält.

Wiederherstellen eines Pakets mit `restore`:

```cli
nuget restore MySolution.sln
```