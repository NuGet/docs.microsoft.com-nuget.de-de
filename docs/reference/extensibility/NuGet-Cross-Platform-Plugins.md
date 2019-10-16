---
title: Cross Platform-Plug-ins
description: Nuget-plattformübergreifende Plug-Ins für nuget. exe, dotnet. exe, MSBuild. exe und Visual Studio
author: nkolev92
ms.author: nikolev
ms.date: 07/01/2018
ms.topic: conceptual
ms.openlocfilehash: 00410214500c7f5256be243dd6fca0907ba9b0c4
ms.sourcegitcommit: 363ec6843409b4714c91b75b105619a3a3184b43
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/16/2019
ms.locfileid: "72380502"
---
# <a name="nuget-cross-platform-plugins"></a>Cross Platform-Plug-ins

In nuget 4.8 und höher wurde die Unterstützung für plattformübergreifende Plug-Ins hinzugefügt.
Dies wurde durch das Entwickeln eines neuen Plug-in-Erweiterbarkeits Modells erreicht, das einem strengen Satz von Vorgangs Regeln entspricht.
Die Plug-ins sind eigenständige ausführbare Dateien (Runnables in der .net Core-Welt), die von den nuget-Clients in einem separaten Prozess gestartet werden.
Dies ist ein echter Schreibvorgang, wenn Sie das Plug-in überall ausführen. Es funktioniert mit allen nuget-Client Tools.
Die Plug-Ins können entweder .NET Framework (nuget. exe, MSBuild. exe und Visual Studio) oder .net Core (dotnet. exe) sein.
Ein Kommunikationsprotokoll mit Versions Angabe zwischen dem nuget-Client und dem-Plug-in ist definiert. Während des Start Handshakes aushandeln die beiden Prozesse die Protokollversion.

Um alle Szenarien für nuget-Client Tools abzudecken, benötigen Sie eine .NET Framework und ein .net Core-Plug-in.
Im folgenden werden die Client/Framework-Kombinationen der Plug-Ins beschrieben.

| Client-Tool  | Framework |
| ------------ | --------- |
| Visual Studio | .NET Framework |
| dotnet.exe | .NET Core |
| "Nuget. exe" | .NET Framework |
| MSBuild. exe | .NET Framework |
| "Nuget. exe" unter Mono | .NET Framework |

## <a name="how-does-it-work"></a>Funktionsweise

Der allgemeine Workflow kann wie folgt beschrieben werden:

1. Nuget erkennt verfügbare Plug-ins.
1. Wenn zutreffend, durchläuft nuget die Plug-ins in der Reihenfolge der Priorität und startet Sie nacheinander.
1. Nuget verwendet das erste Plug-in, das die Anforderung bedienen kann.
1. Die Plug-ins werden heruntergefahren, wenn Sie nicht mehr benötigt werden.

## <a name="general-plugin-requirements"></a>Allgemeine Plug-ins

Die aktuelle Protokollversion ist *2.0.0*.
Unter dieser Version gelten die folgenden Anforderungen:

- Sie verfügen über eine gültige vertrauenswürdige Authenticode-Signatur-Assemblys, die unter Windows und Mono ausgeführt werden. Für Assemblys, die unter Linux und Mac ausgeführt werden, ist keine besondere Vertrauensstellung erforderlich. [Relevantes Problem](https://github.com/NuGet/Home/issues/6702)
- Unterstützung des Zustands losen Starts im aktuellen Sicherheitskontext der nuget-Client Tools. Beispielsweise führen nuget-Client Tools keine Rechte Erweiterung oder zusätzliche Initialisierung außerhalb des später beschriebenen Plug-in-Protokolls aus.
- Wenn Sie nicht explizit angegeben sind, sind Sie nicht interaktiv.
- Einhaltung der ausgehandelten Plug-in-Protokollversion.
- Reagieren Sie innerhalb eines angemessenen Zeitraums auf alle Anforderungen.
- Beachten Sie Abbruch Anforderungen für alle laufenden Vorgänge.

Die technische Spezifikation wird in den folgenden Spezifikationen ausführlicher beschrieben:

- [Plug-in für nuget-Paket](https://github.com/NuGet/Home/wiki/NuGet-Package-Download-Plugin)
- [Nuget-Plug-in für die nuget-Authentifizierung](https://github.com/NuGet/Home/wiki/NuGet-cross-plat-authentication-plugin)

## <a name="client---plugin-interaction"></a>Client-Plug-in-Interaktion

Die nuget-Client Tools und-Plug-ins kommunizieren mit JSON über Standardstreams (stdin, stdout, stderr). Alle Daten müssen UTF-8-codiert sein.
Die Plug-ins werden mit dem Argument "-Plugin" gestartet. Wenn ein Benutzer eine ausführbare Plug-in-Datei ohne dieses Argument direkt aufruft, kann das Plug-in eine informative Nachricht senden, anstatt auf einen Protokoll Hand Shake zu warten.
Der Protokoll Hand Shake Timeout beträgt 5 Sekunden. Das Plug-in sollte das Setup so kurz wie möglich ausführen.
Die nuget-Client Tools werden die unterstützten Vorgänge eines Plug-ins Abfragen, indem der Dienst Index für eine nuget-Quelle übergeben wird. Ein Plug-in kann den Dienst Index verwenden, um zu überprüfen, ob die unterstützten Dienst Typen vorhanden sind.

Die Kommunikation zwischen den nuget-Client Tools und dem Plug-in ist bidirektional. Jede Anforderung hat ein Timeout von 5 Sekunden. Wenn der Vorgang länger dauern soll, sollte der jeweilige Prozess eine Statusmeldung senden, um eine Zeitüberschreitung der Anforderung zu verhindern. Nach 1 Minuten Inaktivität wird ein Plug-in als Leerlauf betrachtet und heruntergefahren.

## <a name="plugin-installation-and-discovery"></a>Installation und Ermittlung von Plug-ins

Die Plug-ins werden über eine auf Konventionen basierende Verzeichnisstruktur ermittelt.
CI/CD-Szenarien und Poweruser können Umgebungsvariablen verwenden, um das Verhalten zu überschreiben. Wenn Sie Umgebungsvariablen verwenden, sind nur absolute Pfade zulässig. Beachten Sie, dass `NUGET_NETFX_PLUGIN_PATHS` und `NUGET_NETCORE_PLUGIN_PATHS` nur mit einer Version von 5.3 und höher für die nuget-Tools und höher verfügbar sind.

- `NUGET_NETFX_PLUGIN_PATHS`: definiert die Plug-ins, die von den .NET Framework basierten Tools (nuget. exe/MSBuild. exe/Visual Studio) verwendet werden. Hat Vorrang vor `NUGET_PLUGIN_PATHS`. (Nur nuget-Version 5.3 +)
- `NUGET_NETCORE_PLUGIN_PATHS`: definiert die Plug-ins, die von den .net Core-basierten Tools (dotnet. exe) verwendet werden. Hat Vorrang vor `NUGET_PLUGIN_PATHS`. (Nur nuget-Version 5.3 +)
- `NUGET_PLUGIN_PATHS`: definiert die Plug-ins, die für den nuget-Prozess verwendet werden. die Priorität wird beibehalten. Wenn diese Umgebungsvariable festgelegt ist, wird die auf der Konvention basierende Ermittlung überschrieben. Wird ignoriert, wenn eine der Framework-spezifischen Variablen angegeben wird.
-  Benutzer-Location: der nuget-Start Speicherort in `%UserProfile%/.nuget/plugins`. Dieser Speicherort kann nicht überschrieben werden. Für .net Core-und .NET Framework-Plug-ins wird ein anderes Stammverzeichnis verwendet.

| Framework | Speicherort der Stamm Ermittlung  |
| ------- | ------------------------ |
| .NET Core |  `%UserProfile%/.nuget/plugins/netcore` |
| .NET Framework | `%UserProfile%/.nuget/plugins/netfx` |

Jedes Plug-in sollte in einem eigenen Ordner installiert werden.
Der Plug-in-Einstiegspunkt ist der Name des installierten Ordners mit den dll-Erweiterungen für .net Core und der Erweiterung ". exe" für .NET Framework.

```
.nuget
    plugins
        netfx
            myPlugin
                myPlugin.exe
                nuget.protocol.dll
                ...
        netcore
            myPlugin
                myPlugin.dll
                nuget.protocol.dll
                ...
```

> [!Note]
> Zurzeit gibt es keine User Story für die Installation der Plug-ins. Es ist ganz einfach, die erforderlichen Dateien an den vordefinierten Speicherort zu verschieben.

## <a name="supported-operations"></a>Unterstützte Vorgänge

Unter dem neuen Plug-in-Protokoll werden zwei Vorgänge unterstützt.

| Vorgangs Name | Minimale Protokollversion | Minimale nuget-Client Version |
| -------------- | ----------------------- | --------------------- |
| Paket herunterladen | 1.0.0 | 4.3.0 |
| [Authentifizierung](NuGet-Cross-Platform-Authentication-Plugin.md) | 2.0.0 | 4.8.0 |

## <a name="running-plugins-under-the-correct-runtime"></a>Ausführen von Plug-ins unter der richtigen Laufzeit

Für nuget-Szenarien in dotnet. exe müssen Plug-ins unter dieser bestimmten Laufzeit von "dotnet. exe" ausgeführt werden können.
Er ist auf dem Plug-in-Anbieter und dem Consumer, um sicherzustellen, dass eine kompatible Kombination aus "dotnet. exe/Plugin" verwendet wird
Ein potenzielles Problem könnte bei den Benutzer-/Speicherort-Plug-ins auftreten, wenn beispielsweise eine dotnet. exe-Datei unter der 2,0-Laufzeit versucht, ein für die 2,1-Laufzeit geschriebenes Plug-in

## <a name="capabilities-caching"></a>Zwischenspeichern von Funktionen

Die Sicherheitsüberprüfung und-Instanziierung der Plug-ins ist aufwendig. Der Downloadvorgang erfolgt häufiger als der Authentifizierungs Vorgang, aber der durchschnittliche nuget-Benutzer hat wahrscheinlich nur ein Authentifizierungs-Plug-in.
Um die Leistung zu verbessern, speichert nuget die Vorgangs Ansprüche für die angegebene Anforderung zwischen. Dieser Cache ist pro Plug-in, wobei der Plug-in-Pfad der Plug-in-Pfad ist, und der Ablauf für diesen Funktions Cache beträgt 30 Tage. 

Der Cache befindet sich in `%LocalAppData%/NuGet/plugins-cache` und wird mit der Umgebungsvariablen `NUGET_PLUGINS_CACHE_PATH` überschrieben. Um diesen [Cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md)zu löschen, kann der Befehl "Locals" mit der Option "`plugins-cache`" ausgeführt werden.
Mit der Option "`all` lokal" wird nun auch der Plug-in-Cache gelöscht. 

## <a name="protocol-messages-index"></a>Protokollnachrichten Index

Protokoll Version *1.0.0* :

1.  Schließen
    * Anforderungs Richtung: nuget->-Plug-in
    * Die Anforderung enthält keine Nutzlast.
    * Es wird keine Antwort erwartet.  Die richtige Antwort besteht darin, dass der Plug-in-Prozess umgehend beendet wird.

2.  Dateien in Paket kopieren
    * Anforderungs Richtung: nuget->-Plug-in
    * Die Anforderung enthält Folgendes:
        * die Paket-ID und die Version
        * Speicherort des Paket Quell Repository
        * Zielverzeichnis Pfad
        * ein Aufzähl bares Element von Dateien im Paket, das in den Zielverzeichnis Pfad kopiert werden soll.
    * Eine Antwort enthält Folgendes:
        * ein Antwort Code, der das Ergebnis des Vorgangs angibt.
        * ein Aufzähl barer vollständiger Pfad für kopierte Dateien im Zielverzeichnis, wenn der Vorgang erfolgreich war.

3.  Paketdatei kopieren (nupkg-Datei)
    * Anforderungs Richtung: nuget->-Plug-in
    * Die Anforderung enthält Folgendes:
        * die Paket-ID und die Version
        * Speicherort des Paket Quell Repository
        * der Ziel Datei Pfad.
    * Eine Antwort enthält Folgendes:
        * ein Antwort Code, der das Ergebnis des Vorgangs angibt.

4.  Anmelde Informationen erhalten
    * Anforderungs Richtung: Plug-in > nuget
    * Die Anforderung enthält Folgendes:
        * Speicherort des Paket Quell Repository
        * der HTTP-Statuscode, der über die aktuellen Anmelde Informationen aus dem Paket Quellrepository abgerufen wurde
    * Eine Antwort enthält Folgendes:
        * ein Antwort Code, der das Ergebnis des Vorgangs angibt.
        * ein Benutzername, falls verfügbar
        * ein Kennwort, falls verfügbar

5.  Dateien im Paket erhalten
    * Anforderungs Richtung: nuget->-Plug-in
    * Die Anforderung enthält Folgendes:
        * die Paket-ID und die Version
        * Speicherort des Paket Quell Repository
    * Eine Antwort enthält Folgendes:
        * ein Antwort Code, der das Ergebnis des Vorgangs angibt.
        * ein Aufzähl bares Element von Dateipfaden im Paket, wenn der Vorgang erfolgreich war.

6.  Vorgangs Ansprüche abrufen 
    * Anforderungs Richtung: nuget->-Plug-in
    * Die Anforderung enthält Folgendes:
        * der Dienst Index. JSON für eine Paketquelle
        * Speicherort des Paket Quell Repository
    * Eine Antwort enthält Folgendes:
        * ein Antwort Code, der das Ergebnis des Vorgangs angibt.
        * ein Aufzähl bares Element unterstützter Vorgänge (z. b. Paket Download), wenn der Vorgang erfolgreich war.  Wenn ein Plug-in die Paketquelle nicht unterstützt, muss das Plug-in eine leere Gruppe unterstützter Vorgänge zurückgeben.

> [!Note]
> Diese Meldung wurde in Version *2.0.0*aktualisiert. Sie befindet sich auf dem Client, um die Abwärtskompatibilität aufrechtzuerhalten.

7.  Pakethash erhalten
    * Anforderungs Richtung: nuget->-Plug-in
    * Die Anforderung enthält Folgendes:
        * die Paket-ID und die Version
        * Speicherort des Paket Quell Repository
        * der Hash Algorithmus
    * Eine Antwort enthält Folgendes:
        * ein Antwort Code, der das Ergebnis des Vorgangs angibt.
        * ein paketdateihash, der den angeforderten Hash Algorithmus verwendet, wenn der Vorgang erfolgreich war.

8.  Paketversionen erhalten
    * Anforderungs Richtung: nuget->-Plug-in
    * Die Anforderung enthält Folgendes:
        * die Paket-ID
        * Speicherort des Paket Quell Repository
    * Eine Antwort enthält Folgendes:
        * ein Antwort Code, der das Ergebnis des Vorgangs angibt.
        * ein Aufzähl bares Element von Paketversionen, wenn der Vorgang erfolgreich war.

9.  Dienst Index erhalten
    * Anforderungs Richtung: Plug-in > nuget
    * Die Anforderung enthält Folgendes:
        * Speicherort des Paket Quell Repository
    * Eine Antwort enthält Folgendes:
        * ein Antwort Code, der das Ergebnis des Vorgangs angibt.
        * der Dienst Index, wenn der Vorgang erfolgreich war.

10.  Shakes
     * Anforderungs Richtung: nuget-<->-Plug-in
     * Die Anforderung enthält Folgendes:
         * die aktuelle Plug-in-Protokollversion
         * die minimal unterstützte Plug-in-Protokollversion
     * Eine Antwort enthält Folgendes:
         * ein Antwort Code, der das Ergebnis des Vorgangs angibt.
         * die ausgehandelte Protokollversion, wenn der Vorgang erfolgreich war.  Ein Fehler führt zu einer Beendigung des Plug-ins.

11.  Initialize
     * Anforderungs Richtung: nuget->-Plug-in
     * Die Anforderung enthält Folgendes:
         * die Version des nuget-Client Tools
         * die effektive Sprache des nuget-Client Tools.  Dabei wird ggf. die Einstellung "forceengloutput" berücksichtigt.
         * der standardmäßige Anforderungs Timeout, der den Standardwert des Protokolls ersetzt.
     * Eine Antwort enthält Folgendes:
         * ein Antwort Code, der das Ergebnis des Vorgangs angibt.  Ein Fehler führt zu einer Beendigung des Plug-ins.

12.  Protokoll
     * Anforderungs Richtung: Plug-in > nuget
     * Die Anforderung enthält Folgendes:
         * die Protokollebene für die Anforderung.
         * eine Meldung, die protokolliert werden soll
     * Eine Antwort enthält Folgendes:
         * ein Antwort Code, der das Ergebnis des Vorgangs angibt.

13.  Überwachen von nuget-Prozess beenden
     * Anforderungs Richtung: nuget->-Plug-in
     * Die Anforderung enthält Folgendes:
         * die nuget-Prozess-ID
     * Eine Antwort enthält Folgendes:
         * ein Antwort Code, der das Ergebnis des Vorgangs angibt.

14.  Paket vorab abrufen
     * Anforderungs Richtung: nuget->-Plug-in
     * Die Anforderung enthält Folgendes:
         * die Paket-ID und die Version
         * Speicherort des Paket Quell Repository
     * Eine Antwort enthält Folgendes:
         * ein Antwort Code, der das Ergebnis des Vorgangs angibt.

15.  Anmelde Informationen festlegen
     * Anforderungs Richtung: nuget->-Plug-in
     * Die Anforderung enthält Folgendes:
         * Speicherort des Paket Quell Repository
         * der letzte bekannte Paket Quell Benutzername, falls verfügbar
         * das letzte bekannte Paket Quell Kennwort, falls verfügbar
         * der letzte bekannte Proxy Benutzername, falls verfügbar
         * Letztes bekanntes Proxy Kennwort, falls verfügbar
     * Eine Antwort enthält Folgendes:
         * ein Antwort Code, der das Ergebnis des Vorgangs angibt.

16.  Festlegen der Protokollebene
     * Anforderungs Richtung: nuget->-Plug-in
     * Die Anforderung enthält Folgendes:
         * die Standardprotokoll Ebene
     * Eine Antwort enthält Folgendes:
         * ein Antwort Code, der das Ergebnis des Vorgangs angibt.

Protokoll Version *2.0.0* -Nachrichten

17. Vorgangs Ansprüche abrufen

* Anforderungs Richtung: nuget->-Plug-in
    * Die Anforderung enthält Folgendes:
        * der Dienst Index. JSON für eine Paketquelle
        * Speicherort des Paket Quell Repository
    * Eine Antwort enthält Folgendes:
        * ein Antwort Code, der das Ergebnis des Vorgangs angibt.
        * eine Aufzähl Bare der unterstützten Vorgänge, wenn der Vorgang erfolgreich war.  Wenn ein Plug-in die Paketquelle nicht unterstützt, muss das Plug-in eine leere Gruppe unterstützter Vorgänge zurückgeben.

    Wenn der Dienst Index und die Paketquelle NULL sind, kann das Plug-in mit der Authentifizierung Antworten.

18. Authentifizierungs Anmelde Informationen erhalten

* Anforderungs Richtung: nuget->-Plug-in
* Die Anforderung enthält Folgendes:
    * URI
    * isretry
    * Nicht interaktive
    * Canshowdialog
* Eine Antwort enthält
    * Benutzername
    * Kennwort
    * Nachricht
    * Liste der Authentifizierungs Typen
    * Messageresponsecode
