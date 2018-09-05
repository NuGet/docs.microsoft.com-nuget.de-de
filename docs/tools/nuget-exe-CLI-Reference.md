---
title: Referenz für NuGet-Befehlszeilenschnittstelle (CLI)
description: Befehlszeilenreferenz-Index für die nuget.exe-CLI
author: karann-msft
ms.author: karann
ms.date: 01/23/2018
ms.topic: reference
ms.openlocfilehash: 2743dde63487124c706f2b1521ef2c6c3b28339d
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548077"
---
# <a name="nuget-cli-reference"></a>NuGet-CLI-Referenz

Die NuGet Command Line Interface (CLI), `nuget.exe`, enthält das Ausmaß des NuGet-Funktionen zu installieren, erstellen, veröffentlichen und -Pakete verwalten, ohne dass Änderungen an Projektdateien.

Um einen beliebigen Befehl verwenden, öffnen Sie ein Befehlsfenster oder bash-Shell, und führen Sie `nuget` wie z. B. gefolgt von den Befehl und die entsprechenden Optionen `nuget help pack` (zum Anzeigen der Hilfe zum Befehl "Pack").

In dieser Dokumentation gibt die neueste Version des NuGet-CLI. Führen Sie für Informationen für jede Version, die Sie verwenden, `nuget help` für den gewünschten Befehl.

## <a name="installing-nugetexe"></a>Installieren von nuget.exe

[!INCLUDE [install-cli](../includes/install-cli.md)]

> [!Tip]
> Um die NuGet-CLI in Visual Studio in der Paket-Manager-Konsole verfügbar zu machen, finden Sie unter [mithilfe der nuget.exe-CLI in der Konsole](package-manager-console.md#using-the-nugetexe-cli-in-the-console).

## <a name="availability"></a>Verfügbarkeit

Finden Sie unter [Verfügbarkeit von Features](../install-nuget-client-tools.md#feature-availability) genaue Angaben.

- Alle Befehle sind in Windows verfügbar.
- Alle Befehle funktionieren bei nuget.exe unter Mono ausgeführt wird, wenn nicht anders für angegeben `pack`, `restore`, und `update`.
- Die `pack`, `restore`, `delete`, `locals`, und `push` Befehle stehen auch unter Mac und Linux über die Dotnet-CLI.

## <a name="commands-and-applicability"></a>Befehle und Anwendbarkeit

Verfügbare Befehle und Anwendbarkeit für die Erstellung des Pakets, paketverbrauch und/oder Veröffentlichen eines Pakets auf einem Host:

| Häufig verwendete Befehle | Anwendbaren Serverrollen | NuGet-Version | Beschreibung |
| --- | --- | --- | --- |
| [pack](cli-ref-pack.md) | Erstellen | 2.7+ | Erstellt ein NuGet-Paket aus einer `.nuspec` oder einer Projektdatei. Wenn unter Mono ausgeführt wird, wird das Erstellen eines Pakets aus einer Projektdatei nicht unterstützt. |
| [push](cli-ref-push.md) | Veröffentlichen | Alle | Ein Paket veröffentlicht in eine Paketquelle. |
| [config](cli-ref-config.md) | Alle | Alle | Übernimmt oder bestimmt die NuGet-Konfigurationswerte. |
| [help or ?](cli-ref-help.md) | Alle | Alle | Zeigt die Informationen oder Hilfe für einen Befehl Hilfe. |
| [locals](cli-ref-locals.md) | Verbrauch | 3.3+ | Listet die Speicherorte der *global-Packages*, *http-Cache*, und *Temp* Ordner und löscht den Inhalt der Ordner. |
| [restore](cli-ref-restore.md) | Verbrauch | 2.7+ | Stellt alle Pakete, die auf die verwiesen wird durch das Format für die paketverwaltung verwendet. Wenn unter Mono ausgeführt wird, wird das Wiederherstellen von Paketen, die das PackageReference-Format mit nicht unterstützt. |
| [setapikey](cli-ref-setapikey.md) | Veröffentlichung, Nutzung | Alle | Speichert einen API-Schlüssel für einen angegebenen Paketquelle aus, wenn diese Paketquelle für den Zugriff auf ein Schlüssel erforderlich ist. |
| [spec](cli-ref-spec.md) | Erstellen | Alle | Generiert eine `.nuspec` Datei, Token verwenden, wenn die Datei aus einem Visual Studio-Projekt generiert wird. |

| Sekundäre Befehle | Anwendbaren Serverrollen | NuGet-Version | Beschreibung |
| --- | --- | --- | --- |
| [add](cli-ref-add.md) | Veröffentlichen | 3.3+ | Fügt ein Paket mit einer nicht-HTTP-Paket-Datenquelle, die mithilfe von hierarchischen Anordnung an. Verwenden Sie für HTTP-Quellen *Push*. |
| [delete](cli-ref-delete.md) | Veröffentlichen | Alle | Entfernt oder hebt dessen Auflistung auf ein Paket aus der Paketquelle. |
| [init](cli-ref-init.md) | Erstellen | 3.3+ | Mithilfe hierarchischen Anordnung Paketquelle hinzugefügt Pakete aus einem Ordner. |
| [install](cli-ref-install.md) | Verbrauch | Alle | Installiert ein Paket in das aktuelle Projekt jedoch keine Projekte zu ändern oder Dateien zu verweisen. |
| [list](cli-ref-list.md) | Nutzung, z. B. veröffentlichen | Alle | Werden Pakete aus einer angegebenen Quelle angezeigt. |
| [mirror](cli-ref-mirror.md) | Veröffentlichen | Veraltet in 3.2 und höher | Spiegelt ein Paket und seine Abhängigkeiten von einer Quelle in ein Zielrepository. |
| [sources](cli-ref-sources.md) | Nutzung, die Veröffentlichung | Alle | Verwaltet die Paketquellen in Konfigurationsdateien. |
| [update](cli-ref-update.md) | Verbrauch | Alle | Die aktuellen verfügbaren Versionen aktualisiert eines Projekts Pakete. Wenn unter Mono unterstützt nicht. |

Stellen Sie andere Befehle verwenden verschiedener [Umgebungsvariablen](cli-ref-environment-variables.md).

NuGet-CLI-Befehle nach anwendbaren Serverrollen:

| Rolle | Befehle |
| --- | --- |
| Verbrauch | `config`, `help`, `install`, `list`, `locals`, `restore`, `setapikey`, `sources`, `update` |
| Erstellen | `config`, `help`, `init`, `pack`, `spec` |
| Veröffentlichen | `add`, `config`, `delete`, `help`, `list`, `push`, `setapikey`, `sources` |

Entwickler, die nur mit der Nutzen von Paketen, befassen müssen z. B. nur diese Teilmenge von NuGet-Befehle verstehen.

> [!Note]
> Befehl Optionsnamen Groß-und Kleinschreibung. Optionen, die veraltet sind nicht befinden sich in dieser Referenz, z. B. `NoPrompt` (ersetzt durch `NonInteractive`) und `Verbose` (ersetzt durch `Verbosity`).
