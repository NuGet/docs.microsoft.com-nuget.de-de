---
title: NuGet cross-Platform-Plug-Ins
description: NuGet cross Platform-Plug-Ins für NuGet.exe "," dotnet.exe "," msbuild.exe "und" Visual Studio
author: nkolev92
ms.author: nikolev
ms.date: 07/01/2018
ms.topic: conceptual
ms.openlocfilehash: fdefc5b6189051fd83b2de644080284c09dd85f4
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548205"
---
# <a name="nuget-cross-platform-plugins"></a>NuGet cross-Platform-Plug-Ins

In NuGet 4.8 und höher wurde Unterstützung für cross-Platform-Plug-Ins hinzugefügt.
Dies wurde mit erreicht, indem Sie erstellen ein neues-Plug-in-Erweiterbarkeitsmodell, die einem strikter Regeln des Vorgangs entsprechen.
Die Plug-Ins sind eigenständige ausführbare Dateien und (in der .NET Core-Welt Runnables), die die NuGet-Clients in einem separaten Prozess zu starten.
Dies ist ein "true" Schreibvorgang einmal auszuführen weltweit-Plug-in. Es funktioniert mit allen NuGet-Clienttools.
Die Plug-Ins kann entweder mit .NET Framework ("NuGet.exe", "MSBuild.exe" und "Visual Studio") oder .NET Core (dotnet.exe) sein.
Es wird ein mit versionsverwaltung durch das Kommunikationsprotokoll zwischen dem NuGet-Client und das Plug-in definiert. Während des Handshakes beim Start aushandeln 2 Prozesse die Protokollversion an.

Um alle NuGet Client Tools-Szenarien abzudecken, würde eine ein .NET Framework und eine .NET Core-Plug-in benötigen.
Die im folgenden wird beschrieben, die Client/Framework-Kombinationen der Plug-Ins.

| Client-Tool  | Framework |
| ------------ | --------- |
| Visual Studio | .NET Framework |
| dotnet.exe | .NET Core |
| NuGet.exe | .NET Framework |
| MSBuild.exe | .NET Framework |
| NuGet.exe auf Mono | .NET Framework |

## <a name="how-does-it-work"></a>Wie funktioniert es

Der allgemeine Workflow kann wie folgt beschrieben werden:

1. NuGet erkennt verfügbaren Plug-Ins.
1. Gegebenenfalls wird NuGet die Plug-Ins in der Reihenfolge ihrer Priorität und startet Sie einzeln durchlaufen werden.
1. NuGet wird das erste Plug-in verwenden, das die Anforderung bedienen kann.
1. Die Plug-Ins wird heruntergefahren wenn sie nicht mehr benötigt werden.

## <a name="general-plugin-requirements"></a>Allgemeine-Plug-in-Anforderungen

Die aktuelle Protokollversion ist *2.0.0*.
In dieser Version sind wie folgt:

- Haben Sie einen gültigen und vertrauenswürdigen Authenticode-Signatur Assemblys, die auf Windows und Mono ausgeführt werden. Es ist keine besondere Vertrauensstellung erforderlich für Assemblys, die noch unter Linux und Mac ausgeführt. [Relevante Problem](https://github.com/NuGet/Home/issues/6702)
- Unterstützung von zustandslosen starten im aktuellen Sicherheitskontext der NuGet-Clienttools. NuGet-Clienttools führt beispielsweise keine Erhöhung der Rechte oder zusätzliche Initialisierung außerhalb des-Plug-in-Protokolls, die weiter unten beschrieben.
- Sofern nicht ausdrücklich angegeben, wird nicht interaktiv sein.
- Das ausgehandelte-Plug-Ins Protokoll, Version entsprechen.
- Für alle Anforderungen innerhalb eines angemessenen Zeitraums zu reagieren.
- Berücksichtigen Sie abbruchanforderungen für jeden Vorgang in Bearbeitung.

Die technische Spezifikation wird in der folgenden Spezifikationen ausführlicher beschrieben:

- [NuGet-Paket herunterladen-Plug-in](https://github.com/NuGet/Home/wiki/NuGet-Package-Download-Plugin)
- [NuGet cross-Plat-Authentifizierung-Plug-in](https://github.com/NuGet/Home/wiki/NuGet-cross-plat-authentication-plugin)

## <a name="client---plugin-interaction"></a>Client --Plug-in-Interaktion

NuGet-Clienttools und die Plug-Ins kommunizieren mit JSON-Code über standard-Streams (Stdin, Stdout, Stderr). Alle Daten müssen UTF-8 codiert sein.
Die Plug-Ins werden gestartet, mit dem Argument "--Plug-in". Für den Fall, dass ein Benutzer direkt ein ausführbare Datei ohne dieses Argument-Plug-in startet, kann das Plug-in eine informative Meldung, anstatt abzuwarten, bis eine Protokoll-Handshakes geben.
Das Protokoll-Handshakes-Timeout beträgt 5 Sekunden. Das Plug-in sollte die Einrichtung in als, kleiner als eine Menge wie möglich abgeschlossen werden.
NuGet-Clienttools werden unterstützten ein Plug-in-Vorgänge durch die Übergabe dienstindex für ein NuGet-Quelle abgefragt werden. Ein Plug-in kann den dienstindex verwenden, um auf das Vorhandensein der unterstützten Diensttypen überprüfen zu können.

Die Kommunikation zwischen den NuGet-Clienttools und das Plug-in ist bidirektional. Jede Anforderung hat ein Timeout von fünf Sekunden. Wenn Vorgänge sollten länger dauern sollte eine Statusmeldung, um zu verhindern, dass die Anforderung ein Timeout eingetreten der entsprechende Prozess gesendet. Nach einer Minute Inaktivität ein Plug-in als inaktiv betrachtet und wird heruntergefahren.

## <a name="plugin-installation-and-discovery"></a>Plug-in-Installation und Ermittlung

Die Plug-Ins werden über eine Verzeichnisstruktur konventionsbasierten ermittelt.
CI/CD-Szenarien und erfahrene Benutzer können eine Umgebungsvariable, das Verhalten.

- `NUGET_PLUGIN_PATHS` : definiert die Plug-Ins, die für diesen Prozess für NuGet, Priorität, die reserviert verwendet werden. Wenn diese Umgebungsvariable festgelegt ist, wird die Ermittlung des konventionsbasierten überschrieben.
-  Benutzer-Speicherort, den Speicherort der NuGet-Startseite in `%UserProfile%/.nuget/plugins`. Dieser Speicherort kann nicht überschrieben werden. Ein Stammverzeichnis für die verschiedenen wird für .NET Core und .NET Framework-Plug-Ins verwendet werden.

| Framework | Stammverzeichnis für die Ermittlung  |
| ------- | ------------------------ |
| .NET Core |  `%UserProfile%/.nuget/plugins/netcore` |
| .NET Framework | `%UserProfile%/.nuget/plugins/netfx` |

Jede-Plug-in sollte in einem eigenen Ordner installiert werden.
Der Einstiegspunkt-Plug-in werden der Name des installierten-Ordner, mit der DLL-Erweiterungen für .NET Core und ".exe"-Erweiterung für .NET Framework.

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
> Es gibt derzeit keine User Storys für die Installation des Plug-Ins. Es ist so einfach wie die erforderlichen Dateien in den zuvor festgelegten Speicherort verschieben.

## <a name="supported-operations"></a>Unterstützte Vorgänge

Zwei Vorgänge werden in das neue Plug-in-Protokoll unterstützt.

| Vorgangsname | Mindestprotokollversion | Mindestversion für NuGet-client |
| -------------- | ----------------------- | --------------------- |
| Paket herunterladen | 1.0.0 | 4.3.0 |
| [Authentifizierung](NuGet-Cross-Platform-Authentication-Plugin.md) | 2.0.0 | 4.8.0 |

## <a name="running-plugins-under-the-correct-runtime"></a>Ausführen unter die richtige Runtime-Plug-Ins

Für die NuGet in dotnet.exe-Szenarien müssen-Plug-Ins unter dieser bestimmten Laufzeit von der dotnet.exe ausgeführt werden.
Es ist der Anbieter-Plug-Ins und Consumer, um sicherzustellen, dass eine kompatible dotnet.exe/plugin-Kombination verwendet wird.
Ein mögliches Problem kann auftreten, mit dem Benutzerstandort Plug-Ins bei z. B., eine dotnet.exe unter der 2.0-Runtime versucht, eine-Plug-Ins für die 2.1-Runtime geschrieben wurden.

## <a name="capabilities-caching"></a>Funktionen, die Zwischenspeicherung

Die sicherheitsüberprüfung und -Instanziierung der Plug-Ins ist teuer. Der Downloadvorgang geschieht viel häufiger auf als den Authentifizierungsvorgang, jedoch ist der durchschnittliche Benutzer von NuGet nur wahrscheinlich eine Authentifizierung-Plug-in.
Um die benutzerfreundlichkeit zu verbessern, speichert NuGet die Vorgang-Ansprüche für die angegebene Anforderung. Dieser Cache wird pro-Plug-in, mit dem-Plug-in-Schlüssel wird der Pfad-Plug-in, und das Ablaufdatum für diesen Cache Funktionen beträgt 30 Tage. 

Der Cache befindet sich im `%LocalAppData%/NuGet/plugins-cache` und werden zusammen mit der Umgebungsvariable `NUGET_PLUGINS_CACHE_PATH`. Um dies zu löschen [Cache](../../consume-packages/managing-the-global-packages-and-cache-folders.md), möglich, die lokal auszuführen-Befehl mit der `plugins-cache` Option.
Die `all` "lokal"-Option wird auch den Cache-Plug-Ins gelöscht. 

## <a name="protocol-messages-index"></a>Index der Protokoll-Nachrichten

Protokollversion *1.0.0* Nachrichten:

1.  Schließen
    * Anfordern der Richtung: NuGet ->-Plug-in
    * Die Anforderung wird keine Nutzlast enthalten.
    * Es wird keine Antwort erwartet.  Die richtige Antwort ist für den Prozess-Plug-in, um sofort zu beenden.

2.  Kopieren von Dateien im Paket
    * Anfordern der Richtung: NuGet ->-Plug-in
    * Die Anforderung enthält Folgendes:
        * der Paket-ID und version
        * Speicherort für die Paketquelle repository
        * Zielverzeichnispfad
        * ein aufzählbares Objekt von Dateien im Paket in den Zielverzeichnispfad kopiert werden sollen
    * Eine Antwort enthält Folgendes:
        * Antwortcode, der angibt, des Ergebnis des Vorgangs
        * ein aufzählbares Objekt von vollständigen Pfade für die kopierten Dateien in das Zielverzeichnis, wenn der Vorgang erfolgreich war

3.  Kopieren Sie die Paketdatei (NUPKG-Datei)
    * Anfordern der Richtung: NuGet ->-Plug-in
    * Die Anforderung enthält Folgendes:
        * der Paket-ID und version
        * Speicherort für die Paketquelle repository
        * der Zieldateipfad
    * Eine Antwort enthält Folgendes:
        * Antwortcode, der angibt, des Ergebnis des Vorgangs

4.  Abrufen von Anmeldeinformationen
    * Anfordern der Richtung: NuGet-Plug-in ->
    * Die Anforderung enthält Folgendes:
        * Speicherort für die Paketquelle repository
        * die HTTP-Statuscode, der vom Paket Quell-Repository mit aktuellen Anmeldeinformationen abgerufen
    * Eine Antwort enthält Folgendes:
        * Antwortcode, der angibt, des Ergebnis des Vorgangs
        * ein Benutzername, sofern verfügbar
        * ein Kennwort, falls verfügbar

5.  Abrufen von Dateien im Paket
    * Anfordern der Richtung: NuGet ->-Plug-in
    * Die Anforderung enthält Folgendes:
        * der Paket-ID und version
        * Speicherort für die Paketquelle repository
    * Eine Antwort enthält Folgendes:
        * Antwortcode, der angibt, des Ergebnis des Vorgangs
        * ein aufzählbares Objekt von Dateipfaden in das Paket aus, wenn der Vorgang erfolgreich war

6.  Abrufen von Vorgang Ansprüche 
    * Anfordern der Richtung: NuGet ->-Plug-in
    * Die Anforderung enthält Folgendes:
        * der Dienst index.json für eine Paketquelle
        * Speicherort für die Paketquelle repository
    * Eine Antwort enthält Folgendes:
        * Antwortcode, der angibt, des Ergebnis des Vorgangs
        * ein aufzählbares Objekt von unterstützten Vorgänge (z. B.: Paketdownload), wenn der Vorgang erfolgreich war.  Wenn Sie ein Plug-in die Paketquelle nicht unterstützt, muss die-Plug-in einen leeren Satz von unterstützten Vorgänge zurückgeben.

> [!Note]
> Diese Nachricht wurde in Version aktualisiert *2.0.0*. Es ist auf dem Client um Abwärtskompatibilität zu gewährleisten.

7.  Abrufen der pakethash
    * Anfordern der Richtung: NuGet ->-Plug-in
    * Die Anforderung enthält Folgendes:
        * der Paket-ID und version
        * Speicherort für die Paketquelle repository
        * Der Hashalgorithmus
    * Eine Antwort enthält Folgendes:
        * Antwortcode, der angibt, des Ergebnis des Vorgangs
        * der Dateihash ein Paket unter Verwendung des angeforderten Hashalgorithmus, wenn der Vorgang erfolgreich war

8.  Abrufen von Paketversionen
    * Anfordern der Richtung: NuGet ->-Plug-in
    * Die Anforderung enthält Folgendes:
        * die Paket-ID
        * Speicherort für die Paketquelle repository
    * Eine Antwort enthält Folgendes:
        * Antwortcode, der angibt, des Ergebnis des Vorgangs
        * ein aufzählbares Objekt von Paketversionen, wenn der Vorgang erfolgreich war

9.  Dienstindex abrufen
    * Anfordern der Richtung: NuGet-Plug-in ->
    * Die Anforderung enthält Folgendes:
        * Speicherort für die Paketquelle repository
    * Eine Antwort enthält Folgendes:
        * Antwortcode, der angibt, des Ergebnis des Vorgangs
        * der dienstindex, wenn der Vorgang erfolgreich war

10.  Handshake
     * Anfordern der Richtung: NuGet <> –-Plug-in
     * Die Anforderung enthält Folgendes:
         * die aktuelle Version des-Plug-in-Protokoll
         * die unterstützte Mindestversion-Plug-in-Protokoll
     * Eine Antwort enthält Folgendes:
         * Antwortcode, der angibt, des Ergebnis des Vorgangs
         * Das ausgehandelte Protokoll-Version, wenn der Vorgang erfolgreich war.  Ein Fehler führen die Beendigung des Plug-Ins.

11.  Initialisieren
     * Anfordern der Richtung: NuGet ->-Plug-in
     * Die Anforderung enthält Folgendes:
         * die Version des NuGet-Client-Tools
         * die NuGet Client Tools effektive Sprache.  Dies berücksichtigt die ForceEnglishOutput-Einstellung, wenn verwendet.
         * das standardmäßige Anforderung-Timeout, die der Protokoll-Standardwert hat Vorrang vor.
     * Eine Antwort enthält Folgendes:
         * eine Antwortcode, der angibt, des Ergebnis des Vorgangs.  Ein Fehler führen die Beendigung des Plug-Ins.

12.  Protokoll
     * Anfordern der Richtung: NuGet-Plug-in ->
     * Die Anforderung enthält Folgendes:
         * die Protokollebene für die Anforderung
         * einer zu protokollierenden Meldung
     * Eine Antwort enthält Folgendes:
         * eine Antwortcode, der angibt, des Ergebnis des Vorgangs.

13.  Überwachen von NuGet-Prozessende
     * Anfordern der Richtung: NuGet ->-Plug-in
     * Die Anforderung enthält Folgendes:
         * die NuGet-Prozess-ID
     * Eine Antwort enthält Folgendes:
         * eine Antwortcode, der angibt, des Ergebnis des Vorgangs.

14.  Vorabrufen von Paket
     * Anfordern der Richtung: NuGet ->-Plug-in
     * Die Anforderung enthält Folgendes:
         * der Paket-ID und version
         * Speicherort für die Paketquelle repository
     * Eine Antwort enthält Folgendes:
         * Antwortcode, der angibt, des Ergebnis des Vorgangs

15.  Festlegen von Anmeldeinformationen
     * Anfordern der Richtung: NuGet ->-Plug-in
     * Die Anforderung enthält Folgendes:
         * Speicherort für die Paketquelle repository
         * der letzte bekannte Quelle paketbenutzernamen, falls verfügbar
         * das letzte bekannte Quelle Paketkennwort, falls verfügbar
         * der letzte bekannte Proxybenutzername, falls verfügbar
         * das letzte bekannte Proxykennwort, falls verfügbar
     * Eine Antwort enthält Folgendes:
         * Antwortcode, der angibt, des Ergebnis des Vorgangs

16.  Set-Protokollebene
     * Anfordern der Richtung: NuGet ->-Plug-in
     * Die Anforderung enthält Folgendes:
         * Die Standardprotokollebene
     * Eine Antwort enthält Folgendes:
         * Antwortcode, der angibt, des Ergebnis des Vorgangs

Protokollversion *2.0.0* Nachrichten

17. Abrufen von Vorgang Ansprüche

* Anfordern der Richtung: NuGet ->-Plug-in
    * Die Anforderung enthält Folgendes:
        * der Dienst index.json für eine Paketquelle
        * Speicherort für die Paketquelle repository
    * Eine Antwort enthält Folgendes:
        * Antwortcode, der angibt, des Ergebnis des Vorgangs
        * ein aufzählbares Element für unterstützten Vorgänge, wenn der Vorgang erfolgreich war.  Wenn Sie ein Plug-in die Paketquelle nicht unterstützt, muss die-Plug-in einen leeren Satz von unterstützten Vorgänge zurückgeben.

    Wenn die Dienst Index und die Paket-Quelle auf null festgelegt sind, kann das Plug-in mit der Authentifizierung beantworten.

18. Abrufen von Authentifizierungsanmeldeinformationen für

* Anfordern der Richtung: NuGet ->-Plug-in
* Die Anforderung enthält Folgendes:
    * URI
    * isRetry
    * NonInteractive
    * CanShowDialog
* Eine Antwort enthält.
    * Benutzername
    * Kennwort
    * Meldung
    * Liste der Typen der Authentifizierung
    * MessageResponseCode