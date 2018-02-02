---
title: Anmeldeinformationsanbieter NuGet.exe | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/12/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Anmeldeinformationsanbieter NuGet.exe authentifizieren sich mit einem Feed und werden als ausführbare Befehlszeilendateien, die bestimmte Konventionen implementiert."
keywords: NuGet.exe Anmeldeinformationsanbieter, Anmeldeinformationsanbieter-API authentifizieren sich mit dem Feed, authentifizieren sich mit der Galerie
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 88ce0106ad4e628ba8120f94b7951c7746ab67f3
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="authenticating-feeds-with-nugetexe-credential-providers"></a>Authentifizieren von Feeds mit nuget.exe Anmeldeinformationsanbieter

*NuGet 3.3+*

Wenn `nuget.exe` benötigt Anmeldeinformationen für die Authentifizierung bei einem Feed, sucht es nach ihnen auf folgende Weise:

1. NuGet sucht zuerst nach Anmeldeinformationen in `Nuget.Config` Dateien.
1. NuGet verwendet-Plug-In für anmeldeinformationenanbieter, unterliegen der unten angegebenen Reihenfolge. (Und Beispiel ist die [Visual Studio Team Services-Anmeldeinformationsanbieter](https://www.visualstudio.com/docs/package/get-started/nuget/auth#vsts-credential-provider).)
1. NuGet fordert dann den Benutzer zum Eingeben von Anmeldeinformationen in der Befehlszeile angegeben.

Beachten Sie, die nur in der hier beschriebenen Anmeldeinformationsanbieter funktionieren `nuget.exe` und nicht in "Dotnet wiederherstellen" oder im Visual Studio. Der Anmeldeinformationsanbieter mit Visual Studio, finden Sie unter [nuget.exe Anmeldeinformationsanbieter für Visual Studio](nuget-credential-providers-for-visual-studio.md)

Anmeldeinformationsanbieter NuGet.exe können auf 3 Arten verwendet werden:

- **Global**: einen Anmeldeinformationsanbieter für alle Instanzen von verfügbar machen können `nuget.exe` unter Profil des aktuellen Benutzers ausgeführt werden, fügen Sie diese `%LocalAppData%\NuGet\CredentialProviders`. Möglicherweise müssen Sie erstellen die `CredentialProviders` Ordner. Anmeldeinformationsanbieter können installiert werden, im Stammverzeichnis der `CredentialProviders` Ordner oder in einem Unterordner. Verfügt ein Anmeldeinformationsanbieter mehrere Dateien/Assemblys, können Sie die Unterordner organisiert Anbieter zu verwenden.

- **Von einer Umgebungsvariablen**: Anmeldeinformationsanbieter an einer beliebigen Stelle gespeichert und verfügbar gemacht werden `nuget.exe` durch Festlegen der `%NUGET_CREDENTIALPROVIDERS_PATH%` -Umgebungsvariable für den Speicherort eines Anbieters. Diese Variable kann eine durch Semikolons getrennte Liste (z. B. `path1;path2`) Wenn Sie über mehrere Standorte verfügen.

- **Neben nuget.exe**: nuget.exe Anmeldeinformationsanbieter platziert werden können, im gleichen Ordner wie `nuget.exe`.

Beim Laden der Anmeldeinformationsanbieter, `nuget.exe` sucht die oben genannten Speicherorten nacheinander für jede Datei mit dem Namen `credentialprovider*.exe`, lädt dann die Dateien in der Reihenfolge, die sie aufgeführt sind. Wenn mehrere Anmeldeinformationsanbieter im selben Ordner vorhanden sind, sind in alphabetischer Reihenfolge geladen.

## <a name="creating-a-nugetexe-credential-provider"></a>Einen Anmeldeinformationsanbieter nuget.exe erstellen

Ein Anmeldeinformationsanbieter ist eine ausführbare Befehlszeilendatei Namens in der Form `CredentialProvider*.exe`, sammelt die Eingaben, erhält die Anmeldeinformationen nach Bedarf und gibt dann den entsprechenden Exit-Statuscode und die Standardausgabe zurück.

Ein Anbieter muss folgende Anforderungen erfüllen:

- Bestimmen Sie, ob sie Anmeldeinformationen für den Ziel-URI bereitstellen kann, vor dem Initiieren der Übernahme von Anmeldeinformationen. Wenn dies nicht der Fall ist, sollte der Statuscode 1 ohne Anmeldeinformationen zurückgegeben.
- Ändern Sie nicht `Nuget.Config` (z. B. das Festlegen von Anmeldeinformationen vorhanden).
- Handle HTTP-Proxykonfiguration auf eine eigene, als NuGet-bietet keine Proxyinformationen des Plug-Ins.
- Zurückgeben von Anmeldeinformationen oder die Fehlerdetails, um `nuget.exe` durch Schreiben von JSON-Antwort-Objekt (siehe unten) in "stdout" mit UTF-8-Codierung.
- Optional Geben Sie zusätzliche ablaufverfolgungsprotokollierung an Stderr. Keine geheimen Schlüssel sollten in "stderr", jemals geschrieben werden, da am ausführlichkeitsebenen "normal" oder "detailliert" solchen ablaufverfolgungen von NuGet auf der Konsole ausgegeben werden.
- Unerwarteter Parameter sollten bereitstellen Aufwärtskompatibilität mit zukünftigen Versionen von NuGet ignoriert werden.

### <a name="input-parameters"></a>Eingabeparameter

| Parameter-Switch |Beschreibung|
|----------------|-----------|
| URI {Value} | Die Paket-URI erfordert Anmeldeinformationen für die Datenquelle.|
| NonInteractive | Falls vorhanden, gibt Anbieter keine interaktive eingabeaufforderungen aus. |
| IsRetry | Falls vorhanden, gibt an, dass dieser Versuch eine Wiederholung für einen zuvor fehlgeschlagenen Versuch ist. Anbieter verwenden Sie dieses Flag in der Regel um sicherzustellen, dass sie alle vorhandenen Caches zu umgehen und nach Möglichkeit zum Eingeben neuer Anmeldeinformationen aufgefordert.|
| Ausführlichkeit {Value} | Falls vorhanden, einen der folgenden Werte: "normale", "quiet" oder "detailliert". Wenn kein Wert angegeben wird, wird standardmäßig in "Normal". Anbieter sollten diese ein Hinweis auf die Ebene der optionalen Protokollierung verwenden, um den Standardfehlerstream auszugeben. |

### <a name="exit-codes"></a>Exit-codes

| Code |Ergebnis | Beschreibung |
|----------------|-----------|-----------|
| 0 | Erfolgreich | Die Anmeldeinformationen wurden erfolgreich abgerufen und in "stdout" geschrieben wurden.|
| 1 | ProviderNotApplicable | Der aktuelle Anbieter bietet keine Anmeldeinformationen für den angegebenen URI.|
| 2 | Fehler | Der Anbieter ist der richtige Anbieter für den angegebenen URI, jedoch kann keine Anmeldeinformationen bereitstellen. In diesem Fall nuget.exe unternimmt keine Authentifizierung und schlägt fehl. Ein typisches Beispiel ist, wenn ein Benutzer eine interaktive Anmeldung abgebrochen wird. |

### <a name="standard-output"></a>Standardausgabe

| Eigenschaft |Hinweise|
|----------------|-----------|
| Benutzername | Der Benutzername für authentifizierte Anforderungen.|
| Kennwort | Kennwort für authentifizierte Anforderungen.|
| Meldung | Optionale Details der Antwort, die nur verwendet, um weitere Details in möglichen Schwachstellen angezeigt. |

Beispiel für "stdout":

    { "Username" : "freddy@example.com",
      "Password" : "bwm3bcx6txhprzmxhl2x63mdsul6grctazoomtdb6kfbof7m3a3z",
      "Message"  : "" }

## <a name="troubleshooting-a-credential-provider"></a>Problembehandlung bei einer Anmeldeinformationsanbieter

Zu diesem Zeitpunkt angeben nicht NuGet viel direkte Unterstützung, für das Debuggen von benutzerdefinierten Anmeldeinformationsanbieter; [ausstellen 4598](https://github.com/NuGet/Home/issues/4598) diese Arbeit nachverfolgt.

Sie können auch die folgenden Aktionen ausführen:

- Führen Sie nuget.exe mit der `-verbosity` Switch, ausführliche Ausgabe zu überprüfen.
- Hinzufügen von Debugmeldungen an `stdout` in den entsprechenden Stellen.
- Achten Sie darauf, dass Sie nuget.exe 3.3 oder höher verwenden.
- Fügen Sie die Debugger beim Start durch diesen Codeausschnitt:

    ```cs
    while (!Debugger.IsAttached)
    {
        System.Threading.Thread.Sleep(100);
    }
    Debugger.Break();
    ```

Weitere Hilfe benötigen [senden Sie eine Supportanfrage ein nuget.org](https://www.nuget.org/policies/Contact).
