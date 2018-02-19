---
title: "Möglichkeiten zum Installieren von NuGet-Paketen | Microsoft-Dokumentation"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 02/12/2018
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "Beschreibt den Prozess der Installation von NuGet-Pakete in ein Projekt, inklusive, was auf dem Datenträger und mit anwendbaren Projektdateien passiert."
keywords: NuGet installieren, NuGet-Paketverbrauch, Installieren von NuGet-Paketen, NuGet-Paketverweise
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 3bae03e148a366388c10d08e83c89dac6ff56d06
ms.sourcegitcommit: 33436d122873249dbb20616556cd8c6783f38909
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/12/2018
---
# <a name="different-ways-to-install-a-nuget-package"></a>Verschiedene Möglichkeiten zum Installieren von NuGet-Paketen

NuGet-Pakete werden mithilfe einer der folgenden Methoden heruntergeladen und installiert (siehe [Install NuGet client tools (Installieren von NuGet-Clienttools)](../install-nuget-client-tools.md), falls Sie diese noch nicht installiert haben):

| Methode | description |
| --- | --- |
| dotnet.exe-CLI<br/>`dotnet install <package_name>` | (Alle Plattformen) Das anhand von \<package_name\> identifizierte Paket wird heruntergeladen, dessen Inhalt wird im aktuellen Verzeichnis in einen Ordner entpackt und ein Verweis zur Projektdatei wird hinzugefügt. Lädt auch Abhängigkeiten herunter und installiert sie.<ul><li>[Installieren und Verwenden eines Pakets (dotnet-CLI)](../quickstart/install-and-use-a-package-using-the-dotnet-cli.md)</li><li>[dotnet-Befehle](../tools/dotnet-commands.md)</li></ul> |
| Benutzeroberfläche des Paket-Managers (Visual Studio) | (Windows und Mac) Bietet eine Benutzeroberfläche, über die Sie die Liste der Pakete durchsuchen, Pakete auswählen und diese Pakete und ihre Abhängigkeiten in ein Projekt installieren können. Fügt der Projektdatei Verweise auf installierte Pakete zu.<ul><li>[Installieren und Verwenden eines Pakets (Visual Studio)](../quickstart/install-and-use-a-package-in-visual-studio.md)</li><li>[Referenz zur Benutzeroberfläche des Paket-Managers (Windows)](../tools/package-manager-ui.md)</li><li>[Einschließen eines NuGet-Pakets in Ihr Projekt (Mac)](/visualstudio/mac/nuget-walkthrough)</li></ul> |
| Paket-Manager-Konsole (Visual Studio)<br/>`Install-Package <package_name>` | (Nur Windows) Lädt das Paket herunter, das durch \<package_name\> identifiziert wurde, und installiert es in ein angegebenes Projekt in der Projektmappe und fügt dann einen Verweis zur Projektdatei hinzu. Lädt auch Abhängigkeiten herunter und installiert sie.<ul><li>[Installieren und Verwenden eines Pakets (Visual Studio)](../quickstart/install-and-use-a-package-in-visual-studio.md)</li><li>[Leitfaden für die Paket-Manager-Konsole](../tools/package-manager-console.md)</li></ul> |
| nuget.exe-CLI<br/>`nuget install <package_name>` | (Alle Plattformen) Das anhand von \<package_name\> identifizierte Paket wird heruntergeladen, dessen Inhalt wird im aktuellen Verzeichnis in einen Ordner entpackt. Kann auch alle Pakete herunterladen, die in einer `packages.config`-Datei aufgelistet sind. Lädt außerdem Abhängigkeiten herunter und installiert sie, nimmt aber keine Änderungen an Projektdateien vor.<ul><li>[install-Befehl](../tools/cli-ref-install.md)</li></ul> |

## <a name="general-install-process"></a>Allgemeiner Installationsvorgang

Im Allgemeinen befolgt NuGet folgende Schritte, wenn ein Paket installiert werden soll:

1. Erhalten des Pakets:
    - Es überprüft, ob das angeforderte Paket bereits in einem Cache vorhanden ist (siehe [Verwalten des NuGet-Caches](managing-the-nuget-cache.md)).
    - Wenn sich das Paket nicht im Cache befindet, versucht NuGet das Paket aus Quellen herunterzuladen, die in den [Konfigurationsdateien](Configuring-NuGet-Behavior.md) aufgelistet sind.
      - Bei Projekten, die das `packages.config`-Referenzformat verwenden, geht NuGet nach der Reihenfolge der Quellen in der Konfiguration vor.
      - Bei Projekten, die das PackageReference-Format verwenden, prüft NuGet zuerst lokale Quellordner, dann Quellen in Netzwerkfreigaben und schließlich HTTP-Quellen (Internet).
      - Im Allgemeinen spielt die Reihenfolge, in der NuGet Quellen überprüft, keine besondere Rolle, weil jedes Paket mit einem bestimmten Bezeichner und einer bestimmten Versionsnummer unabhängig von der Quelle, in der es sich befindet, genau identisch ist.
    - Wenn das Paket erfolgreich aus einer der Quellen abgerufen wurde, fügt NuGet es dem Cache zu. Andernfalls schlägt die Installation fehl.

1. Erweitern des Pakets in das Projekt:
    - Erweitern beschreibt das Entpacken der Paket-Inhalte in einen entsprechenden Unterordner. Eine Kopie der `.nupkg`-Datei selbst wird ebenfalls im Unterordner platziert.
    - Wenn das Paket in ein Projekt in Visual Studio oder .NET Core installiert wird, werden nur Dateien erweitert, die relevant für das Zielframework des Projekts sind. Wenn es mithilfe der Befehlszeile „nuget.exe“ installiert wurde, werden alle Assemblys erweitert.

1. Wenn ein Paket in Visual Studio oder in der dotnet-CLI installiert wird, fügt NuGet einen Verweis zu der entsprechenden Projektdatei hinzu (oder `packages.config` in manchen Projekttypen in Visual Studio).

## <a name="related-topics"></a>Verwandte Themen

- [Übersicht über den Paketverbrauch und dessen Workflows](../consume-packages/overview-and-workflow.md)
- [Suchen und Auswählen von Paketen](../consume-packages/finding-and-choosing-packages.md)
- [Konfigurieren des NuGet-Verhaltens](../consume-packages/configuring-nuget-behavior.md)
- [Verwalten des NuGet-Caches](managing-the-nuget-cache.md)
