---
title: Referenz zur nuget-Befehlszeilenschnittstelle (CLI)
description: Referenzindex der Befehlszeile für die nuget.exe CLI
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: reference
ms.openlocfilehash: e9343f1fdddcf839322849925372587e685aef4a
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/19/2020
ms.locfileid: "88623148"
---
# <a name="nuget-cli-reference"></a>Verweis auf NuGet-CLI

Die nuget-Befehlszeilenschnittstelle (CLI) `nuget.exe` bietet das gesamte Maß an nuget-Funktionen, um Pakete zu installieren, zu erstellen, zu veröffentlichen und zu verwalten, ohne dass Änderungen an den Projektdateien vorgenommen werden.

Um einen beliebigen Befehl zu verwenden, öffnen Sie ein Befehlsfenster oder eine bash-Shell, und führen Sie dann `nuget` aus, gefolgt vom Befehl und den entsprechenden Optionen, z `nuget help pack` . b. (zum Anzeigen der Hilfe zum Befehl Pack).

Diese Dokumentation spiegelt die neueste Version der nuget-CLI wider. Führen Sie für den gewünschten Befehl aus, um genaue Informationen zu einer beliebigen Version zu erhalten, die Sie verwenden `nuget help` .

Informationen zur Verwendung grundlegender Befehle der `nuget.exe`-CLI finden Sie unter [Installieren und Verwenden von Paketen mit der nuget.exe-CLI](../consume-packages/install-use-packages-nuget-cli.md).

## <a name="installing-nugetexe"></a>Installieren von nuget.exe

[!INCLUDE [install-cli](../includes/install-cli.md)]

> [!Tip]
> Informationen dazu, wie Sie die nuget-CLI in der Paket-Manager-Konsole in Visual Studio verfügbar machen, finden [Sie unter Verwenden der nuget.exe CLI in der Konsole](../consume-packages/install-use-packages-powershell.md#use-the-nugetexe-cli-in-the-console).

## <a name="availability"></a>Verfügbarkeit

Genaue Informationen finden Sie unter [Verfügbarkeit von Features](../install-nuget-client-tools.md#feature-availability) .

- Alle Befehle sind unter Windows verfügbar.
- Alle Befehle funktionieren mit nuget.exe, die unter Mono ausgeführt werden, außer wenn für `pack` , und angegeben ist `restore` `update` .
- Die `pack` `restore` Befehle,, `delete` , `locals` und `push` sind auch unter Mac und Linux über die dotnet-CLI verfügbar.

## <a name="commands-and-applicability"></a>Befehle und Anwendbarkeit

Verfügbare Befehle und Anwendbarkeit bei der Paket Erstellung, dem Paket Verbrauch und/oder dem Veröffentlichen eines Pakets auf einem Host:

| Allgemeine Befehle | Anwendbare Rollen | NuGet-Version | BESCHREIBUNG |
| --- | --- | --- | --- |
| [pack](cli-reference/cli-ref-pack.md) | Erstellung | 2.7 und höher | Erstellt ein nuget-Paket aus einer- `.nuspec` oder-Projektdatei. Wenn Sie unter Mono ausführen, wird das Erstellen eines Pakets aus einer Projektdatei nicht unterstützt. |
| [push](cli-reference/cli-ref-push.md) | Veröffentlichung | All | Veröffentlicht ein Paket in einer Paketquelle. |
| [config](cli-reference/cli-ref-config.md) | All | All | Ruft nuget-Konfigurationswerte ab oder legt Sie fest. |
| [help or ?](cli-reference/cli-ref-help.md) | All | All | Zeigt Hilfe Informationen oder Hilfe zu einem Befehl an. |
| [locals](cli-reference/cli-ref-locals.md) | Nutzung | 3.3 und höher | Listet die Speicherorte der Ordner " *Global-Packages*", " *http-Cache*" und " *Temp* " auf und löscht den Inhalt dieser Ordner. |
| [restore](cli-reference/cli-ref-restore.md) | Nutzung | 2.7 und höher | Stellt alle Pakete wieder her, auf die im verwendeten Paket Verwaltungs Format verwiesen wird. Bei der Ausführung unter Mono wird das Wiederherstellen von Paketen mit dem packagereferenzierungsformat nicht unterstützt. |
| [setapikey](cli-reference/cli-ref-setapikey.md) | Veröffentlichen, Verbrauch | All | Speichert einen API-Schlüssel für eine bestimmte Paketquelle, wenn diese Paketquelle einen Schlüssel für den Zugriff benötigt. |
| [spec](cli-reference/cli-ref-spec.md) | Erstellung | All | Generiert eine `.nuspec` Datei mithilfe von Token, wenn die Datei aus einem Visual Studio-Projekt generiert wird. |

| Sekundäre Befehle | Anwendbare Rollen | NuGet-Version | BESCHREIBUNG |
| --- | --- | --- | --- |
| [add](cli-reference/cli-ref-add.md) | Veröffentlichung | 3.3 und höher | Fügt mithilfe des hierarchischen Layouts ein Paket zu einer nicht-http-Paketquelle hinzu. Verwenden Sie für http-Quellen *Push*. |
| [delete](cli-reference/cli-ref-delete.md) | Veröffentlichung | All | Entfernt oder hebt die Auflistung eines Pakets aus einer Paketquelle auf. |
| [init](cli-reference/cli-ref-init.md) | Erstellung | 3.3 und höher | Fügt mithilfe des hierarchischen Layouts Pakete aus einem Ordner einer Paketquelle hinzu. |
| [install](cli-reference/cli-ref-install.md) | Nutzung | All | Installiert ein Paket im aktuellen Projekt, ändert jedoch keine Projekte oder Verweis Dateien. |
| [list](cli-reference/cli-ref-list.md) | Verbrauch, vielleicht veröffentlichen | All | Zeigt Pakete aus einer angegebenen Quelle an. |
| [mirror](cli-reference/cli-ref-mirror.md) | Veröffentlichung | Veraltet in 3.2 + | Spiegelt ein Paket und seine Abhängigkeiten von einer Quelle in ein Zielrepository ein. |
| [search](cli-reference/cli-ref-search.md) | Nutzung | 5.8 + | Durchsucht eine angegebene Quelle mithilfe der angegebenen Abfrage Zeichenfolge. |
| [sources](cli-reference/cli-ref-sources.md) | Verbrauch, Veröffentlichung | All | Verwaltet Paketquellen in Konfigurationsdateien. |
| [update](cli-reference/cli-ref-update.md) | Nutzung | All | Aktualisiert die Pakete eines Projekts auf die neuesten verfügbaren Versionen. Wird nicht unterstützt, wenn Sie unter Mono ausgeführt wird. |

Verschiedene Befehle verwenden verschiedene [Umgebungsvariablen](cli-reference/cli-ref-environment-variables.md).

Nuget-CLI-Befehle nach anwendbaren Rollen:

| Role | Befehle |
| --- | --- |
| Nutzung | `config`, `help`, `install`, `list`, `locals`, `restore`, `search`, `setapikey`, `sources`, `update` |
| Erstellung | `config`, `help`, `init`, `pack`, `spec` |
| Veröffentlichung | `add`, `config`, `delete`, `help`, `list`, `push`, `setapikey`, `sources` |

Entwickler, die sich nur mit der Verwendung von Paketen beschäftigen, benötigen beispielsweise nur diese Teilmenge von nuget-Befehlen.

> [!Note]
> Bei Befehls Optionsnamen wird die Groß-/Kleinschreibung beachtet Veraltete Optionen sind in diesem Verweis nicht enthalten, z `NoPrompt` . b. (ersetzt durch `NonInteractive` ) und `Verbose` (ersetzt durch `Verbosity` ).
