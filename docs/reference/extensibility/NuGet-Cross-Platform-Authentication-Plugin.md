---
title: NuGet cross Platform-Authentifizierung-Plug-in
description: NuGet cross Platform-Authentifizierung-Plug-Ins für NuGet.exe "," dotnet.exe "," msbuild.exe "und" Visual Studio
author: nkolev92
ms.author: nikolev
ms.date: 07/01/2018
ms.topic: conceptual
ms.openlocfilehash: b76fab1028ec9a4172d2390083fbf9adb4290a6c
ms.sourcegitcommit: 0c5a49ec6e0254a4e7a9d8bca7daeefb853c433a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/28/2018
ms.locfileid: "52453506"
---
# <a name="nuget-cross-platform-authentication-plugin"></a>NuGet cross Platform-Authentifizierung-Plug-in

In Version 4.8 und höher, alle NuGet-Clients (NuGet.exe, Visual Studio "," dotnet.exe "und" MSBuild.exe) können eine Authentifizierung-Plug-in, baut auf den [NuGet cross-Platform-Plug-Ins](NuGet-Cross-Platform-Plugins.md) Modell.

## <a name="authentication-in-dotnetexe"></a>Authentifizierung in dotnet.exe

Visual Studio und NuGet.exe sind standardmäßig interaktive. NuGet.exe enthält einen Schalter zum vereinfachen [nicht interaktiven](../../tools/nuget-exe-CLI-Reference.md).
Außerdem wird der Benutzer für die Eingabe von die NuGet.exe- und Visual Studio-Plug-Ins aufgefordert.
In dotnet.exe besteht keine Eingabeaufforderung, und der Standardwert ist nicht interaktiv.

Der Authentifizierungsmechanismus in dotnet.exe ist Gerät Flow. Bei der Wiederherstellung oder fügen Sie interaktiv, Paket-Vorgang ausgeführt wird, die blockiert und die Anweisungen für den Benutzer an, wie auf vollständige erfolgreiche Authentifizierung in der Befehlszeile erfolgt, hinzu.
Wenn der Benutzer die Authentifizierung abgeschlossen ist, wird der Vorgang fortgesetzt.

Um den Vorgang interaktiv gestalten, sollten eine übergeben `--interactive`.
Derzeit nur den expliziten `dotnet restore` und `dotnet add package` Befehle eine interaktive Switches unterstützt.
Auf nicht interaktive gewechselt ist `dotnet build` und `dotnet publish`.

## <a name="authentication-in-msbuild"></a>Authentifizierung in MSBuild

Ähnlich wie dotnet.exe MSBuild.exe ist, wird standardmäßig nicht interaktiv der MSBuild.exe-Authentifizierungsmechanismus Gerät Flow ist.
Um die Wiederherstellung zum Anhalten und warten Sie, für die Authentifizierung zu ermöglichen, rufen Sie die Wiederherstellung mit `msbuild -t:restore -p:NuGetInteractive="true"`.

## <a name="creating-a-cross-platform-authentication-plugin"></a>Erstellen eine plattformübergreifende Authentifizierung-Plug-in

Eine beispielimplementierung finden Sie im [Microsoft Credential Provider-Plug-Ins](https://github.com/Microsoft/artifacts-credprovider).

Es ist sehr wichtig, dass die Plug-Ins die Nutzungsweise der NuGet-Clienttools sicherheitsanforderungen entspricht.
Die mindestens erforderliche Version für ein Plug-in eine Authentifizierung-Plug-Ins werden *2.0.0*.
NuGet führt den Handshake mit den-Plug-Ins und die Abfrage für die Ansprüche unterstützt.
Finden Sie in der NuGet cross-Platform-Plug-Ins [Protokoll Nachrichten](NuGet-Cross-Platform-Plugins.md#protocol-messages-index) um mehr über die Nachrichten.

NuGet wird die Protokollebene und Bereitstellen von Proxyinformationen des Plug-Ins, falls zutreffend.
Anmelden des NuGet-Pakets ist Konsole nachdem NuGet die Protokollebene auf das Plug-in festgelegt hat nur akzeptabel.

- Verhalten der .NET Framework-Plug-in-Authentifizierung

In .NET Framework sind die Plug-Ins zulässig, einen Benutzer zur Eingabe auf, im Formular eines Dialogfelds aufgefordert.

- .NET Core-Plug-in-Benutzerauthentifizierung

In .NET Core kann ein Dialogfeld angezeigt werden. Die Plug-Ins sollte Gerät Flow verwenden, um authentifizieren zu können.
Das Plug-in kann Meldungen in NuGet mit Anweisungen für den Benutzer senden.
Beachten Sie, dass die Protokollierung verfügbar ist, nachdem die Protokollebene des Plug-Ins festgelegt wurde.
NuGet dauert keine interaktive Eingabe von der Befehlszeile aus.

Wenn der Client das Plug-in mit einer Authentifizierungsanmeldeinformationen erhalten aufruft, müssen die Plug-Ins entsprechen, mit dem Switch Interaktivität und berücksichtigen des Dialogfeld-Schalters. 

Die folgende Tabelle fasst zusammen, wie das Plug-In für alle Kombinationen Verhalten soll.

| IsNonInteractive | CanShowDialog | -Plug-in-Verhalten |
| ---------------- | ------------- | --------------- |
| true | true | Der Schalter IsNonInteractive hat Vorrang vor der Dialogfeld-Schalter. Das Plug-in ist nicht zulässig, um ein Dialogfeld angezeigt. Diese Kombination ist nur gültig für .NET Framework-Plug-Ins |
| true | False | Der Schalter IsNonInteractive hat Vorrang vor der Dialogfeld-Schalter. Das Plug-in ist nicht zulässig, um zu blockieren. Diese Kombination ist nur gültig für .NET Core-Plug-Ins |
| False | true | Das Plug-in sollte es sich um ein Dialogfeld angezeigt. Diese Kombination ist nur gültig für .NET Framework-Plug-Ins |
| False | False | Das Plug-in kann/sollte kein Dialogfeld angezeigt. Das Plug-in sollten Geräte Flow authentifizieren, indem Sie die Protokollierung von einer Anweisung Nachricht über die Protokollierung verwenden. Diese Kombination ist nur gültig für .NET Core-Plug-Ins |

Finden Sie in der folgenden Spezifikationen, vor dem Schreiben eines Plug-Ins.

- [NuGet-Paket herunterladen-Plug-in](https://github.com/NuGet/Home/wiki/NuGet-Package-Download-Plugin)
- [NuGet cross-Plat-Authentifizierung-Plug-in](https://github.com/NuGet/Home/wiki/NuGet-cross-plat-authentication-plugin)
