---
title: Anmelde Informationsanbieter für "nuget. exe"
description: nuget. exe-Anmelde Informationsanbieter authentifizieren sich mit einem-Feed und werden als ausführbare Befehlszeilen Dateien implementiert, die bestimmten Konventionen folgen.
author: karann-msft
ms.author: karann
ms.date: 12/12/2017
ms.topic: conceptual
ms.openlocfilehash: 41e3e63138351bafd5e3a56080268faef10d85a3
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/16/2020
ms.locfileid: "79428300"
---
# <a name="authenticating-feeds-with-nugetexe-credential-providers"></a>Authentifizieren von Feeds mit nuget. exe-Anmelde Informationsanbietern

In Version `3.3` Unterstützung für `nuget.exe` bestimmten Anmelde Informationsanbietern hinzugefügt. Seitdem wurde in Version `4.8` [Unterstützung für](NuGet-Cross-Platform-Authentication-Plugin.md) Anmelde Informationsanbieter hinzugefügt, die über alle Befehlszeilen Szenarios hinweg funktionieren (`nuget.exe`, `dotnet.exe`, `msbuild.exe`).

Weitere Informationen zu allen Authentifizierungs Ansätzen für `nuget.exe` finden Sie unter verwenden [von Paketen aus authentifizierten Feeds](../../consume-packages/consuming-packages-authenticated-feeds.md#nugetexe) .

## <a name="nugetexe-credential-provider-discovery"></a>Ermittlung des Anmelde Informationsanbieters für nuget. exe

nuget. exe-Anmelde Informationsanbieter können auf drei Arten verwendet werden:

- **Global**: um einen Anmelde Informationsanbieter für alle Instanzen von verfügbar zu machen `nuget.exe` unter dem Profil des aktuellen Benutzers ausgeführt werden, fügen Sie ihn zu `%LocalAppData%\NuGet\CredentialProviders`hinzu. Möglicherweise müssen Sie den `CredentialProviders` Ordner erstellen. Anmelde Informationsanbieter können im Stammverzeichnis des `CredentialProviders` Ordners oder innerhalb eines unter Ordners installiert werden. Wenn ein Anmelde Informationsanbieter über mehrere Dateien/Assemblys verfügt, können Sie Unterordner verwenden, um die Anbieter zu organisieren.

- **Aus einer Umgebungsvariablen**: Anmelde Informationsanbieter können `nuget.exe` an einem beliebigen Speicherort gespeichert und zugänglich gemacht werden, indem die `%NUGET_CREDENTIALPROVIDERS_PATH%` Umgebungsvariable auf den Speicherort des Anbieters festgelegt wird. Bei dieser Variablen kann es sich um eine durch Semikolons getrennte Liste (z. b. `path1;path2`) handeln, wenn mehrere Standorte vorhanden sind.

- **Neben nuget. exe**können auch nuget. exe-Anmelde Informationsanbieter in demselben Ordner wie `nuget.exe`platziert werden.

Beim Laden von Anmelde Informationsanbietern durchsucht `nuget.exe` die oben aufgeführten Speicherorte für jede Datei mit dem Namen `credentialprovider*.exe`in der richtigen Reihenfolge. diese Dateien werden dann in der Reihenfolge geladen, in der Sie gefunden wurden. Wenn sich mehrere Anmelde Informationsanbieter im selben Ordner befinden, werden Sie in alphabetischer Reihenfolge geladen.

## <a name="creating-a-nugetexe-credential-provider"></a>Erstellen eines nuget. exe-Anmelde Informationsanbieters

Ein Anmelde Informationsanbieter ist eine ausführbare Befehlszeilen Datei mit dem Namen im Formular `CredentialProvider*.exe`, die Eingaben sammelt, die Anmelde Informationen nach Bedarf abruft und dann den entsprechenden Beendigungs Statuscode und die Standardausgabe zurückgibt.

Ein Anbieter muss folgende Aktionen ausführen:

- Bestimmen Sie, ob die Anmelde Informationen für den Ziel-URI vor dem Initiieren der Anmelde Informationen bereitgestellt werden können. Wenn dies nicht der Fall ist, sollte der Statuscode 1 ohne Anmelde Informationen zurückgegeben werden.
- `Nuget.Config` nicht ändern (z. b. das Festlegen von Anmelde Informationen).
- Verwalten Sie die http-Proxykonfiguration eigenständig, da nuget keine Proxy Informationen für das Plug-in bereitstellt.
- Geben Sie Anmelde Informationen oder Fehlerdetails an `nuget.exe` zurück, indem Sie mithilfe der UTF-8-Codierung ein JSON-Antwortobjekt (siehe unten) in stdout schreiben.
- Geben Sie optional eine zusätzliche Ablauf Verfolgungs Protokollierung an stderr aus. Es sollten keine geheimen Schlüssel in stderr geschrieben werden, da auf den ausführlichkeits Stufen "Normal" oder "ausführlich" solche Ablauf Verfolgungen von nuget in der Konsole angezeigt werden.
- Unerwartete Parameter sollten ignoriert werden und sorgen für die Vorwärtskompatibilität mit zukünftigen Versionen von nuget.

### <a name="input-parameters"></a>Eingabeparameter

| Parameter/Switch |BESCHREIBUNG|
|----------------|-----------|
| URI {Value} | Der Paketquellen-URI, der Anmelde Informationen erfordert.|
| NonInteractive | Falls vorhanden, gibt der Anbieter keine interaktiven Eingabe Aufforderungen aus. |
| Isretry | Gibt ggf. an, dass dieser Versuch eine Wiederholung eines zuvor fehlgeschlagenen Versuchs ist. Anbieter verwenden dieses Flag in der Regel, um sicherzustellen, dass alle vorhandenen Caches umgangen werden und nach Möglichkeit neue Anmelde Informationen angefordert werden.|
| Ausführlichkeit {Value} | Falls vorhanden, einer der folgenden Werte: "Normal", "quiet" oder "ausführlich". Wenn kein Wert angegeben wird, wird standardmäßig "Normal" verwendet. Anbieter sollten dies als Anzeichen für die Ebene der optionalen Protokollierung verwenden, die an den Standardfehlerstream ausgegeben werden soll. |

### <a name="exit-codes"></a>Exitcodes

| Code |Ergebnis | BESCHREIBUNG |
|----------------|-----------|-----------|
| 0 | Erfolg | Die Anmelde Informationen wurden erfolgreich abgerufen und in "stdout" geschrieben.|
| 1 | ProviderNotApplicable | Der aktuelle Anbieter stellt keine Anmelde Informationen für den angegebenen URI bereit.|
| 2 | Fehler | Der Anbieter ist der richtige Anbieter für den angegebenen URI, kann aber keine Anmelde Informationen bereitstellen. In diesem Fall wird die Authentifizierung von "nuget. exe" nicht erneut versucht, und es tritt ein Fehler auf. Ein typisches Beispiel ist, wenn ein Benutzer einen interaktiven Anmelde Namen abbricht. |

### <a name="standard-output"></a>Standardausgabe

| Eigenschaft |Notizen|
|----------------|-----------|
| Username | Benutzername für authentifizierte Anforderungen.|
| Kennwort | Kennwort für authentifizierte Anforderungen.|
| `Message` | Optionale Details zur Antwort, die nur verwendet werden, um zusätzliche Details in Fehler Fällen anzuzeigen. |

Beispiel: stdout:

    { "Username" : "freddy@example.com",
      "Password" : "bwm3bcx6txhprzmxhl2x63mdsul6grctazoomtdb6kfbof7m3a3z",
      "Message"  : "" }

## <a name="troubleshooting-a-credential-provider"></a>Problembehandlung bei einem Anmelde Informationsanbieter

Derzeit bietet nuget keine direkte Unterstützung für das Debuggen von benutzerdefinierten Anmelde Informationsanbietern. [Problem 4598](https://github.com/NuGet/Home/issues/4598) ist die Nachverfolgung dieser Arbeit.

Sie können auch die folgenden Aktionen ausführen:

- Führen Sie "nuget. exe" mit dem `-verbosity`-Schalter aus, um die ausführliche Ausgabe zu
- Fügen Sie `stdout` an geeigneten Stellen Debugmeldungen hinzu.
- Stellen Sie sicher, dass Sie nuget. exe 3,3 oder höher verwenden.
- Fügen Sie den Debugger beim Start mit diesem Code Ausschnitt an:

    ```cs
    while (!Debugger.IsAttached)
    {
        System.Threading.Thread.Sleep(100);
    }
    Debugger.Break();
    ```
