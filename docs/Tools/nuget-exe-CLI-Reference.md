---
title: NuGet-Befehlszeilenschnittstelle (CLI)-Referenz | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/23/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Befehlszeilenreferenz Index für die nuget.exe CLI"
keywords: NuGet.exe Verweisindex, nuget.exe-Befehlszeilenschnittstelle, nuget.exe CLI, NuGet-Befehls
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 8b1ee17702f5a54a77dc2cd663e13729a9b4a39f
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-cli-reference"></a>NuGet-CLI-Referenz

Die NuGet-Befehlszeilenschnittstelle (CLI), `nuget.exe`, enthält das Ausmaß des NuGet-Funktionen zu installieren, erstellen, veröffentlichen und Pakete zu verwalten, ohne Änderungen an der Projektdateien.

Um einen Befehl zu verwenden, öffnen Sie ein Eingabeaufforderungsfenster oder bash-Shell aus, und führen Sie `nuget` gefolgt von dem Befehl und die entsprechenden Optionen wie z. B. `nuget help pack` (zum Anzeigen von Hilfe zum Befehl "Pack").

In dieser Dokumentation gibt die neueste Version des NuGet-CLI wieder. Führen Sie genaue Angaben für eine bestimmte Version, die Sie verwenden `nuget help` für den gewünschten Befehl.

## <a name="installing-nugetexe"></a>Installing nuget.exe

[!INCLUDE[install-cli](../includes/install-cli.md)]

> [!Tip]
> Um die CLI NuGet in Visual Studio in der Paket-Manager-Konsole verfügbar zu machen, finden Sie unter [mithilfe der CLI nuget.exe in der Konsole](package-manager-console.md#using-the-nugetexe-cli-in-the-console).

## <a name="availability"></a>Verfügbarkeit

Finden Sie unter [Verfügbarkeit von Features](../install-nuget-client-tools.md#feature-availability) genaue Angaben.

- Alle Befehle sind unter Windows verfügbar.
- Alle Befehle funktionieren mit nuget.exe auf Mono ausgeführt werden, außer für angegeben `pack`, `restore`, und `update`.
- Die `pack`, `restore`, `delete`, `locals`, und `push` Befehle stehen auch für Mac und Linux über die CLI-Dotnet.

## <a name="commands-and-applicability"></a>Befehle und Anwendbarkeit

Verfügbaren Befehle und Anwendbarkeit auf die Erstellung des Pakets, Paket Verbrauch und/oder veröffentlichen ein Paket auf einem Host:

| Häufig verwendete Befehle | Anwendbaren Serverrollen | NuGet-Version | Beschreibung |
| --- | --- | --- | --- |
| [pack](cli-ref-pack.md) | Erstellung | 2.7+ | Erstellt ein NuGet-Paket aus einer `.nuspec` oder der Projektdatei. Bei Ausführung auf Mono wird das Erstellen eines Pakets aus einer Projektdatei nicht unterstützt. |
| [push](cli-ref-push.md) | Veröffentlichen | Alle | Ein Paket veröffentlicht eine Paketquelle. |
| [config](cli-ref-config.md) | Alle | Alle | Ruft ab, oder legt ihn fest NuGet Konfigurationswerte. |
| [help oder ?](cli-ref-help.md) | Alle | Alle | Zeigt die Informationen oder Hilfe für einen Befehl Hilfe. |
| [locals](cli-ref-locals.md) | Verbrauch | 3.3+ | Löscht listet Pakete in verschiedenen Caches oder der Ordner "globale Pakete" oder die Ordner identifiziert. |
| [restore](cli-ref-restore.md) | Verbrauch | 2.7+ | Stellt alle Pakete verweist auf das Paketformat-Verweis verwendet. Bei Ausführung auf Mono wird das Wiederherstellen von Paketen, die mit dem PackageReference-Format nicht unterstützt. |
| [setapikey](cli-ref-setapikey.md) | Veröffentlichen, wählen Sie Verbrauch | Alle | Speichert einen API-Schlüssel für eine bestimmte Paketquelle an, wenn diese Paketquelle einen Schlüssel für den Zugriff erforderlich ist. |
| [spec](cli-ref-spec.md) | Erstellung | Alle | Generiert eine `.nuspec` Datei Token verwenden, wenn die Datei aus einem Visual Studio-Projekt generiert wird. |

| Sekundäre Befehle | Anwendbaren Serverrollen | NuGet-Version | Beschreibung |
| --- | --- | --- | --- |
| [add](cli-ref-add.md) | Veröffentlichen | 3.3+ | Eine nicht-HTTP-Paketquelle hierarchischen Anordnung dargestellt mithilfe hinzugefügt ein Pakets. Verwenden Sie für HTTP-Quellen *Push*. |
| [delete](cli-ref-delete.md) | Veröffentlichen | Alle | Entfernt, oder ein Paket aus einer Paketquelle unlists. |
| [init](cli-ref-init.md) | Erstellung | 3.3+ | Eine hierarchische Layout mit Paketquelle hinzugefügt Pakete aus einem Ordner. |
| [install](cli-ref-install.md) | Verbrauch | Alle | Installiert ein Paket in das aktuelle Projekt jedoch keine Projekte ändern oder Dateien zu verweisen. |
| [list](cli-ref-list.md) | Ressourcenverbrauch, vielleicht veröffentlichen | Alle | Zeigt Pakete von einer bestimmten Quelle an. |
| [mirror](cli-ref-mirror.md) | Veröffentlichen | Veraltetes Feature in 3.2 + | Spiegelt ein Paket und seine Abhängigkeiten von einer Quelle in ein Zielrepository. |
| [sources](cli-ref-sources.md) | Verbrauch, veröffentlichen | Alle | Verwaltet die Paketquellen in Konfigurationsdateien. |
| [update](cli-ref-update.md) | Verbrauch | Alle | Wird ein Projekt Pakete auf die neueste Version aktualisiert. Auf Mono Kompatibilitätsmodus unterstützt nicht. |

Stellen Sie verschiedene Befehle verwenden verschiedener [Umgebungsvariablen](cli-ref-environment-variables.md).

NuGet-CLI-Befehlen durch den entsprechenden Rollen:

| Rolle | Befehle |
| --- | --- |
| Verbrauch | `config`, `help`, `install`, `list`, `locals`, `restore`, `setapikey`, `sources`, `update` |
| Erstellung | `config`, `help`, `init`, `pack`, `spec` |
| Veröffentlichen | `add`, `config`, `delete`, `help`, `list`, `push`, `setapikey`, `sources` |

Entwickler dürfte nur nutzen von Paketen, müssen z. B. nur diese Teilmenge von NuGet-Befehle verstehen.

> [!Note]
> Befehl Optionsnamen Groß-/Kleinschreibung unterschieden. Optionen, die als veraltet markiert werden sind nicht wie in dieser Referenz enthalten `NoPrompt` (Fassung `NonInteractive`) und `Verbose` (Fassung `Verbosity`).
