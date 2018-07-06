---
title: Möglichkeiten zum Installieren von NuGet-Paketen
description: Beschreibt den Prozess der Installation von NuGet-Pakete in ein Projekt, inklusive, was auf dem Datenträger und mit anwendbaren Projektdateien passiert.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 02/12/2018
ms.topic: overview
ms.openlocfilehash: 0f59c3b7f1e32ae34889921c13d15074ef5c1260
ms.sourcegitcommit: 8e3546ab630a24cde8725610b6a68f8eb87afa47
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/05/2018
ms.locfileid: "37843380"
---
# <a name="different-ways-to-install-a-nuget-package"></a>Verschiedene Möglichkeiten zum Installieren von NuGet-Paketen

NuGet-Pakete werden mithilfe einer der Methoden in den folgenden Tabellen heruntergeladen und installiert (siehe [Install NuGet client tools (Installieren von NuGet-Clienttools)](../install-nuget-client-tools.md), falls Sie diese noch nicht installiert haben). Das Paket wird möglicherweise aus dem Cache abgerufen und nicht heruntergeladen.

| Methode | description |
| --- | --- |
| dotnet.exe-CLI<br/>`dotnet add package <package_name>` | (Alle Plattformen) Das anhand von \<package_name\> identifizierte Paket wird abgerufen, dessen Inhalt wird im aktuellen Verzeichnis in einen Ordner entpackt, und ein Verweis zur Projektdatei wird hinzugefügt. Ruft auch Abhängigkeiten ab und installiert sie.<ul><li>[Installieren und Verwenden eines Pakets (dotnet-CLI)](../quickstart/install-and-use-a-package-using-the-dotnet-cli.md)</li><li>[Befehl „dotnet add package“](/dotnet/core/tools/dotnet-add-package)</li></ul> |
| Benutzeroberfläche des Paket-Managers (Visual Studio) | (Windows und Mac) Bietet eine Benutzeroberfläche, über die Sie die Liste der Pakete durchsuchen, Pakete auswählen und diese Pakete und ihre Abhängigkeiten in ein Projekt aus einer angegebenen Paketquelle installieren können. Fügt der Projektdatei Verweise auf installierte Pakete zu.<ul><li>[Installieren und Verwenden eines Pakets (Visual Studio)](../quickstart/install-and-use-a-package-in-visual-studio.md)</li><li>[Referenz zur Benutzeroberfläche des Paket-Managers (Windows)](../tools/package-manager-ui.md)</li><li>[Einschließen eines NuGet-Pakets in Ihr Projekt (Mac)](/visualstudio/mac/nuget-walkthrough)</li></ul> |
| Paket-Manager-Konsole (Visual Studio)<br/>`Install-Package <package_name>` | (Nur Windows) Ruft das Paket ab, das durch \<package_name\> identifiziert wurde, und installiert es aus einer ausgewählten Quelle in ein angegebenes Projekt in der Projektmappe und fügt dann einen Verweis zur Projektdatei hinzu. Ruft auch Abhängigkeiten ab und installiert sie.<ul><li>[Installieren und Verwenden eines Pakets (Visual Studio)](../quickstart/install-and-use-a-package-in-visual-studio.md)</li><li>[Leitfaden für die Paket-Manager-Konsole](../tools/package-manager-console.md)</li></ul> |
| nuget.exe-CLI<br/>`nuget install <package_name>` | (Alle Plattformen) Das anhand von \<package_name\> identifizierte Paket wird abgerufen, dessen Inhalt wird im aktuellen Verzeichnis in einen Ordner entpackt. Kann auch alle Pakete abrufen, die in einer `packages.config`-Datei aufgelistet sind. Ruft außerdem Abhängigkeiten ab und installiert sie, nimmt aber keine Änderungen an Projektdateien oder `packages.config` vor.<ul><li>[install-Befehl](../tools/cli-ref-install.md)</li></ul> |

## <a name="what-happens-when-a-package-is-installed"></a>Nach der Paketinstallation

Die verschiedenen NuGet-Tools erstellen typischerweise einen Verweis auf ein Paket in der Projektdatei oder `packages.config` und führen dann eine Paketwiederherstellung durch, die das Paket effektiv installiert. `nuget install` ist die Ausnahme, bei der das Paket nur in einen `packages`-Ordner erweitert wird, andere Dateien jedoch unverändert bleiben.

Im Allgemeinen läuft der Prozess wie folgt ab:

1. (Alle Tools außer `nuget.exe`) Speichern Sie den Paketbezeichner und die Paketversion in der Projektdatei oder `packages.config`.

2. Erhalten des Pakets:
   - Überprüfen Sie, ob das Paket (mit exaktem Bezeichner und Versionsnummer) bereits im Ordner *global-packages* installiert ist, wie unter [Verwalten der globalen Paketordner und Cacheordner](managing-the-global-packages-and-cache-folders.md) beschrieben.

   - Wenn sich das Paket nicht im Ordner *global-packages* befindet, versuchen Sie, es aus den in den [Konfigurationsdateien](Configuring-NuGet-Behavior.md) aufgelisteten Quellen abzurufen. Bei Onlinequellen versuchen Sie zuerst, das Paket aus dem Cache abzurufen, es sei denn, `-NoCache` wird mit `nuget.exe`-Befehlen oder `--no-cache` mit `dotnet restore` angegeben. (Visual Studio und `dotnet add package` verwenden immer den Cache.) Wenn ein Paket aus dem Cache verwendet wird, erscheint „CACHE“ in der Ausgabe. Die Ablaufzeit des Caches beträgt 30 Minuten.

   - Wenn sich das Paket nicht im Cache befindet, versuchen Sie, es aus den in der Konfiguration aufgeführten Quellen herunterzuladen. Wird ein Paket heruntergeladen, erscheinen „GET“ und „OK“ in der Ausgabe.

   - Wenn das Paket nicht erfolgreich aus einer Quelle bezogen werden kann, tritt bei der Installation an dieser Stelle ein Fehler auf, z.B. [NU1103](../reference/errors-and-warnings/NU1103.md). Beachten Sie, dass Fehler von `nuget.exe`-Befehlen nur die zuletzt geprüfte Quelle anzeigen, aber implizieren, dass das Paket aus keiner Quelle abgerufen werden konnte.

   Beim Beziehen des Pakets gilt möglicherweise die Reihenfolge der Quellen in der NuGet-Konfiguration:

   - Bei Projekten, die das PackageReference-Format verwenden, prüft NuGet zuerst die lokalen Ordner und Netzwerkfreigaben der Quellen und dann erst HTTP-Quellen.

   - Bei Projekten, die das Verwaltungsformat `packages.config` verwenden, übernimmt NuGet die Reihenfolge der Quellen in der Konfiguration. Eine Ausnahme sind Wiederherstellungsvorgänge, bei denen die Reihenfolge der Quellen ignoriert wird und NuGet das Paket verwendet, von dem die Quelle zuerst antwortet.

   - Im Allgemeinen spielt die Reihenfolge, in der NuGet Quellen überprüft, keine besondere Rolle, weil jedes Paket mit einem bestimmten Bezeichner und einer bestimmten Versionsnummer unabhängig von der Quelle, in der es sich befindet, genau identisch ist.

3. (Alle Tools außer `nuget.exe`) Speichern Sie eine Kopie des Pakets und andere Informationen im Ordner *http-cache*, wie unter [Verwalten der globalen Paketordner und Cacheordner](managing-the-global-packages-and-cache-folders.md) beschrieben.

4. Wenn Sie das Paket heruntergeladen haben, installieren Sie es pro Benutzer im Ordner *global-packages*. NuGet erstellt einen Unterordner für jeden Paketbezeichner und erstellt dann Unterordner für jede installierte Version des Pakets.

5. Aktualisieren Sie andere Projektdateien und -ordner:

    - Bei Projekten, die PackageReference verwenden, aktualisieren Sie das in `obj/project.assets.json` gespeicherte Abhängigkeitsdiagramm für das Paket. Paketinhalte selbst werden nicht in einen Projektordner kopiert.
    - Bei Projekten, die `packages.config` verwenden, kopieren Sie die Teile des erweiterten Pakets, die dem Zielframework des Projekts entsprechen, in den `packages`-Ordner des Projekts. (Bei der Verwendung von `nuget install` wird das gesamte erweiterte Paket kopiert, da `nuget.exe` zum Identifizieren des Zielframeworks keine Projektdateien untersucht.)
    - Aktualisieren Sie `app.config` und/oder `web.config`, wenn das Paket [Transformationen von Quell- und Konfigurationsdateien](../create-packages/source-and-config-file-transformations.md) verwendet.

6. Installieren Sie alle untergeordneten Abhängigkeiten, die nicht bereits im Projekt vorhanden sind. Möglicherweise werden bei diesem Prozess Paketversionen im Prozess aktualisiert, wie in [Abhängigkeitsauflösung](../consume-packages/dependency-resolution.md) beschrieben.

7. (Nur Visual Studio) Zeigt die Infodatei des Pakets, falls vorhanden, in einem Visual Studio-Fenster.

## <a name="related-articles"></a>Verwandte Artikel

- [Übersicht über den Paketverbrauch und dessen Workflows](../consume-packages/overview-and-workflow.md)
- [Suchen und Auswählen von Paketen](../consume-packages/finding-and-choosing-packages.md)
- [Verwalten des Cacheordners und des Ordners „global-packages“ von NuGet](managing-the-global-packages-and-cache-folders.md)
- [Konfigurieren des NuGet-Verhaltens](../consume-packages/configuring-nuget-behavior.md)
