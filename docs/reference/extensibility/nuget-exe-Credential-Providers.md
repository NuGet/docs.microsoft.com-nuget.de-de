---
title: nuget.exe-Anmeldeinformationsanbieter
description: nuget.exe Anmeldeinformationsanbieter authentifizieren sich mit einem Feed und werden als ausführbare Befehlszeilendateien implementiert, die bestimmten Konventionen entsprechen.
author: JonDouglas
ms.author: jodou
ms.date: 12/12/2017
ms.topic: conceptual
ms.openlocfilehash: 4f0a5a2355b34c39a435d24691a3f8ea10ee9c00
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323829"
---
# <a name="authenticating-feeds-with-nugetexe-credential-providers"></a>Authentifizieren von Feeds mit nuget.exe Anmeldeinformationsanbietern

In `3.3` wurde Unterstützung für `nuget.exe` bestimmte Anmeldeinformationsanbieter hinzugefügt. Seitdem wurde in der `4.8` [Versionsunterstützung für Anmeldeinformationsanbieter](NuGet-Cross-Platform-Authentication-Plugin.md) hinzugefügt, die in allen Befehlszeilenszenarien ( `nuget.exe` , , ) `dotnet.exe` `msbuild.exe` funktionieren.

Weitere Informationen zu allen Authentifizierungsansätzen für finden Sie unter [Verwenden von Paketen aus authentifizierten Feeds.](../../consume-packages/consuming-packages-authenticated-feeds.md#nugetexe)`nuget.exe`

## <a name="nugetexe-credential-provider-discovery"></a>Ermittlung nuget.exe Anmeldeinformationsanbieters

nuget.exe-Anmeldeinformationsanbieter können auf drei Arten verwendet werden:

- **Global:** Um einen Anmeldeinformationsanbieter für alle Instanzen von verfügbar zu `nuget.exe` machen, die unter dem Profil des aktuellen Benutzers ausgeführt werden, fügen Sie ihn zu `%LocalAppData%\NuGet\CredentialProviders` hinzu. Möglicherweise müssen Sie den `CredentialProviders` Ordner erstellen. Anmeldeinformationsanbieter können im Stammverzeichnis des `CredentialProviders`  Ordners oder in einem Unterordner installiert werden. Wenn ein Anmeldeinformationsanbieter über mehrere Dateien/Assemblys verfügt, können Sie die Anbieter mithilfe von Unterordnern organisieren.

- **Aus einer Umgebungsvariablen:** Anmeldeinformationsanbieter können überall gespeichert und zugänglich gemacht werden, `nuget.exe` indem die `%NUGET_CREDENTIALPROVIDERS_PATH%` Umgebungsvariable auf den Anbieterspeicherort festgelegt wird. Diese Variable kann eine durch Semikolons getrennte Liste sein (z. B. `path1;path2` ), wenn Sie über mehrere Speicherorte verfügen.

- **Neben nuget.exe:** nuget.exe Anmeldeinformationsanbieter können sich im selben Ordner wie `nuget.exe` befinden.

Beim Laden von Anmeldeinformationsanbietern `nuget.exe` durchsucht die oben genannten Speicherorte nach jeder Datei mit dem Namen `credentialprovider*.exe` und lädt diese Dateien in der Reihenfolge, in der sie gefunden werden. Wenn mehrere Anmeldeinformationsanbieter im selben Ordner vorhanden sind, werden sie in alphabetischer Reihenfolge geladen.

## <a name="creating-a-nugetexe-credential-provider"></a>Erstellen eines nuget.exe-Anmeldeinformationsanbieters

Ein Anmeldeinformationsanbieter ist eine ausführbare Befehlszeilendatei mit dem Namen im Format `CredentialProvider*.exe` , die Eingaben sammelt, anmeldeinformationen nach Bedarf erhält und dann den entsprechenden Exitstatuscode und die Standardausgabe zurückgibt.

Ein Anbieter muss folgende Schritte ausführen:

- Bestimmen Sie, ob anmeldeinformationen für den Ziel-URI angegeben werden können, bevor Sie den Erwerb von Anmeldeinformationen initiieren. Falls nicht, sollte der Statuscode 1 ohne Anmeldeinformationen zurückgegeben werden.
- Ändern Sie nicht `NuGet.Config` (z. B. legen Sie dort Anmeldeinformationen fest).
- Behandeln Sie die HTTP-Proxykonfiguration eigenständig, da NuGet keine Proxyinformationen für das Plug-In bereitstellt.
- Geben Sie Anmeldeinformationen oder Fehlerdetails an zurück, indem Sie `nuget.exe` mithilfe der UTF-8-Codierung ein JSON-Antwortobjekt (siehe unten) in stdout schreiben.
- Geben Sie optional zusätzliche Ablaufverfolgungsprotokollierung an stderr aus. Es sollten niemals Geheimnisse in stderr geschrieben werden, da solche Ablaufverfolgungen auf ausführlichen Ebenen von NuGet an die Konsole wiederholt werden.
- Unerwartete Parameter sollten ignoriert werden, um Vorwärtskompatibilität mit zukünftigen Versionen von NuGet zu gewährleisten.

### <a name="input-parameters"></a>Eingabeparameter

| Parameter/Switch |Beschreibung|
|----------------|-----------|
| URI {value} | Der Paketquell-URI, der Anmeldeinformationen erfordert.|
| NonInteractive | Falls vorhanden, gibt der Anbieter keine interaktiven Eingabeaufforderungen aus. |
| IsRetry | Gibt ggf. an, dass es sich bei diesem Versuch um eine Wiederholung eines zuvor fehlgeschlagenen Versuchs handelt. Anbieter verwenden dieses Flag in der Regel, um sicherzustellen, dass sie vorhandene Caches umgehen und nach Möglichkeit neue Anmeldeinformationen auffordern.|
| Ausführlichkeit {value} | Falls vorhanden, einer der folgenden Werte: "normal", "quiet" oder "detailed". Wenn kein Wert angegeben wird, wird standardmäßig "normal" verwendet. Anbieter sollten dies als Hinweis auf den Grad der optionalen Protokollierung verwenden, die an den Standardfehlerstream ausgegeben werden soll. |

### <a name="exit-codes"></a>Exitcodes

| Code |Ergebnis | BESCHREIBUNG |
|----------------|-----------|-----------|
| 0 | Erfolgreich | Anmeldeinformationen wurden erfolgreich erworben und in stdout geschrieben.|
| 1 | ProviderNotApplicable | Der aktuelle Anbieter stellt keine Anmeldeinformationen für den angegebenen URI bereit.|
| 2 | Fehler | Der Anbieter ist der richtige Anbieter für den angegebenen URI, kann aber keine Anmeldeinformationen angeben. In diesem Fall wird nuget.exe die Authentifizierung nicht wiederholen und schlägt fehl. Ein typisches Beispiel ist, wenn ein Benutzer eine interaktive Anmeldung abbricht. |

### <a name="standard-output"></a>Standardausgabe

| Eigenschaft |Notizen|
|----------------|-----------|
| Username | Benutzername für authentifizierte Anforderungen.|
| Kennwort | Kennwort für authentifizierte Anforderungen.|
| `Message` | Optionale Details zur Antwort, die nur verwendet werden, um zusätzliche Details in Fehlerfällen anzuzeigen. |

Stdout-Beispiel:

```
{ "Username" : "freddy@example.com",
    "Password" : "bwm3bcx6txhprzmxhl2x63mdsul6grctazoomtdb6kfbof7m3a3z",
    "Message"  : "" }
```

## <a name="troubleshooting-a-credential-provider"></a>Problembehandlung bei einem Anmeldeinformationsanbieter

Derzeit bietet NuGet keine direkte Unterstützung für das Debuggen von benutzerdefinierten Anmeldeinformationsanbietern. [Problem 4598](https://github.com/NuGet/Home/issues/4598) verfolgt diese Arbeit.

Sie können auch die folgenden Aktionen ausführen:

- Führen Sie nuget.exe mit dem `-verbosity` Schalter aus, um die detaillierte Ausgabe zu überprüfen.
- Fügen Sie Debugmeldungen an geeigneten Stellen zu `stdout` hinzu.
- Stellen Sie sicher, dass Sie nuget.exe 3.3 oder höher verwenden.
- Fügen Sie den Debugger beim Start mit dem folgenden Codeausschnitt an:

    ```cs
    while (!Debugger.IsAttached)
    {
        System.Threading.Thread.Sleep(100);
    }
    Debugger.Break();
    ```
