---
title: NuGet.exe-Anmeldeinformationsanbieter
description: NuGet.exe-Anmeldeinformationsanbieter mit einem Feed zu authentifizieren, und werden als ausführbare Befehlszeilendateien, die bestimmte Konventionen implementiert.
author: karann-msft
ms.author: karann
ms.date: 12/12/2017
ms.topic: conceptual
ms.openlocfilehash: 97a44c6d561f426fa50fa068a9bbf793f77a3111
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550188"
---
# <a name="authenticating-feeds-with-nugetexe-credential-providers"></a>Authentifizieren von Feeds mit nuget.exe-Anmeldeinformationsanbieter

*NuGet 3.3+*

Wenn `nuget.exe` benötigt Anmeldeinformationen für die Authentifizierung mit einen Feed, gesucht, der diese auf folgende Weise:

1. Sucht NuGet zuerst zur Eingabe von Anmeldeinformationen in `Nuget.Config` Dateien.
1. Klicken Sie dann mithilfe von NuGet-Plug-in-Anmeldeinformationsanbieter, gemäß der unten angegebenen Reihenfolge. (Beispiel ist die [Visual Studio Team Services-Anmeldeinformationsanbieter](https://www.visualstudio.com/docs/package/get-started/nuget/auth#vsts-credential-provider).)
1. NuGet fordert dann den Benutzer zur Eingabe von Anmeldeinformationen in der Befehlszeile.

Beachten Sie, die nur in den hier beschriebenen Anmeldeinformationsanbieter zu arbeiten `nuget.exe` und nicht in "Dotnet Restore" oder Visual Studio. Der Anmeldeinformationsanbieter mit Visual Studio, finden Sie unter [nuget.exe-Anmeldeinformationsanbieter für Visual Studio](nuget-credential-providers-for-visual-studio.md)

NuGet.exe-Anmeldeinformationsanbieter können auf 3 Arten verwendet werden:

- **Global**: einen Anbieter für Anmeldeinformationen für alle Instanzen zur Verfügung stellen `nuget.exe` Profil des aktuellen Benutzers ausgeführt, hinzufügen zu `%LocalAppData%\NuGet\CredentialProviders`. Sie müssen zum Erstellen der `CredentialProviders` Ordner. Anmeldeinformationsanbieter können installiert werden, am Stamm der `CredentialProviders` Ordner oder in einem Unterordner. Wenn ein Anmeldeinformationsanbieter mehrere Dateien/Assemblys verfügt, können Unterordner Sie um die Anbieter, organisiert zu bleiben.

- **Von einer Umgebungsvariablen**: Anmeldeinformationsanbieter gespeichert und verfügbar gemacht werden können, `nuget.exe` durch Festlegen der `%NUGET_CREDENTIALPROVIDERS_PATH%` -Umgebungsvariable auf den Speicherort eines Anbieters. Diese Variable kann eine durch Semikolons getrennte Liste sein (z. B. `path1;path2`) Wenn Sie über mehrere Standorte verfügen.

- **Zusammen mit nuget.exe**: nuget.exe-Anmeldeinformationsanbieter platziert werden können, im gleichen Ordner wie `nuget.exe`.

Beim Laden der Anmeldeinformationsanbieter, `nuget.exe` durchsucht die obigen Speicherorten nacheinander für jede Datei, die mit dem Namen `credentialprovider*.exe`, lädt dann die Dateien in der Reihenfolge, die diese finden. Wenn mehrere Anmeldeinformationsanbieter im selben Ordner vorhanden ist, sind in alphabetischer Reihenfolge geladen.

## <a name="creating-a-nugetexe-credential-provider"></a>Erstellen einen nuget.exe-Anmeldeinformationsanbieter

Ein Anmeldeinformationsanbieter ist eine ausführbare Befehlszeilendatei Namens in das Formular `CredentialProvider*.exe`, die Eingaben erfasst, erhält Sie die Anmeldeinformationen nach Bedarf und gibt dann den entsprechenden Exit-Statuscode und die Standardausgabe zurück.

Ein Anbieter muss die folgenden Schritte ausführen:

- Bestimmen Sie, ob sie Anmeldeinformationen für den Ziel-URI angeben kann, vor dem Abrufen von Anmeldeinformationen zu initiieren. Wenn dies nicht der Fall ist, sollte der Statuscode 1 ohne Anmeldeinformationen zurückgegeben.
- Ändern Sie nicht `Nuget.Config` (z. B. das Festlegen von Anmeldeinformationen vorhanden).
- Handle HTTP-Proxykonfiguration auf ihren eigenen als NuGet bietet keine Informationen zum Proxy des Plug-Ins.
- Zurückgeben von Anmeldeinformationen oder Fehlerdetails an `nuget.exe` durch Schreiben ein JSON-Antwort-Objekt (siehe unten) in "stdout" mit UTF-8-Codierung.
- Geben Sie optional zusätzliche ablaufverfolgungsprotokollierung an Stderr. Keine Geheimnisse sollte jemals an Stderr, geschrieben werden, da am Ausführlichkeitsgrade "normal" oder "detailliert" ablaufverfolgungen von NuGet in die Konsole ausgegeben werden.
- Unerwarteter Parameter sollte ignoriert werden Aufwärtskompatibilität mit zukünftigen Versionen von NuGet bereitgestellt werden.

### <a name="input-parameters"></a>Eingabeparameter

| Parameter oder einen |Beschreibung|
|----------------|-----------|
| URI {Value} | Die Paket-URI erfordert Anmeldeinformationen für die Datenquelle.|
| NonInteractive | Falls vorhanden, Anbieter keine interaktive eingabeaufforderungen ausgegeben. |
| isRetry | Falls vorhanden, gibt Sie an, dass dieser Versuch einen Wiederholungsversuch für einen zuvor fehlgeschlagenen Versuch ist. Anbieter verwenden Sie dieses Flag in der Regel um sicherzustellen, dass sie einen vorhandenen Cache umgehen und möglichst neuer Anmeldeinformationen aufgefordert.|
| Ausführlichkeit {Value} | Falls vorhanden, einen der folgenden Werte: "normal", "quiet" oder "detaillierte". Wenn kein Wert angegeben wird, wird standardmäßig auf "Normal". Anbieter sollten dies als Hinweis auf die Ebene der optionalen Protokollierung verwenden, um in den Standardfehlerstream auszugeben. |

### <a name="exit-codes"></a>Exitcodes

| Code |Ergebnis | Beschreibung |
|----------------|-----------|-----------|
| 0 | Erfolgreich | Anmeldeinformationen wurden erfolgreich abgerufen und an "stdout" geschrieben wurden.|
| 1 | ProviderNotApplicable | Der aktuelle Anbieter bietet keine Anmeldeinformationen für den angegebenen URI.|
| 2 | Fehler | Der Anbieter ist der richtige-Anbieter für den angegebenen URI, aber es kann keine Anmeldeinformationen bereitstellen. In diesem Fall wird nuget.exe Authentifizierung wird nicht erneut ausführen und schlägt fehl. Ein typisches Beispiel ist, wenn ein Benutzer eine interaktive Anmeldung abbricht. |

### <a name="standard-output"></a>Standardausgabe

| Eigenschaft |Hinweise|
|----------------|-----------|
| Benutzername | Benutzername für authentifizierte Anforderungen.|
| Kennwort | Das Kennwort für authentifizierte Anforderungen.|
| Meldung | Optionale Details der Antwort nur verwendet, um weitere Details angezeigt, bei Ausfällen. |

Beispiel für "stdout":

    { "Username" : "freddy@example.com",
      "Password" : "bwm3bcx6txhprzmxhl2x63mdsul6grctazoomtdb6kfbof7m3a3z",
      "Message"  : "" }

## <a name="troubleshooting-a-credential-provider"></a>Problembehandlung bei einem Anmeldeinformationsanbieter

Derzeit enthalten keine NuGet-Pakete viele direkte Unterstützung für das Debuggen von benutzerdefinierten Anmeldeinformationsanbieter; [ausgeben 4598](https://github.com/NuGet/Home/issues/4598) ist diese Arbeit nachverfolgen.

Sie können auch die folgenden Schritte ausführen:

- Führen Sie nuget.exe mit der `-verbosity` wechseln, um ausführliche Ausgabe zu überprüfen.
- Hinzufügen von Debugmeldungen an `stdout` an geeigneten Stellen.
- Achten Sie darauf, dass Sie nuget.exe 3.3 oder höher verwenden.
- Fügen Sie der Debugger beim Start durch diesen Codeausschnitt:

    ```cs
    while (!Debugger.IsAttached)
    {
        System.Threading.Thread.Sleep(100);
    }
    Debugger.Break();
    ```

Weitere Hilfe [senden Sie eine Supportanfrage ein nuget.org](https://www.nuget.org/policies/Contact).
