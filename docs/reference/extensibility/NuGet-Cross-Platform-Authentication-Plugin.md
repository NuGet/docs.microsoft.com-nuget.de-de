---
title: Plattformübergreifendes Authentifizierungs-Plug-In für NuGet
description: Nuget-Plug-in für die plattformübergreifende Authentifizierung für nuget. exe, dotnet. exe, MSBuild. exe und Visual Studio
author: nkolev92
ms.author: nikolev
ms.date: 07/01/2018
ms.topic: conceptual
ms.openlocfilehash: a716737343ea826d28da6de46c32ca73aef590bd
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/18/2019
ms.locfileid: "68317280"
---
# <a name="nuget-cross-platform-authentication-plugin"></a>Plattformübergreifendes Authentifizierungs-Plug-In für NuGet

Ab Version 4.8 können alle nuget-Clients ("nuget. exe", "Visual Studio", "dotnet. exe" und "MSBuild. exe") ein Authentifizierungs-Plug-in verwenden, das auf dem [nuget-plattformübergreifenden](NuGet-Cross-Platform-Plugins.md) Plug-in-Modell

## <a name="authentication-in-dotnetexe"></a>Authentifizierung in "dotnet. exe"

Visual Studio und "nuget. exe" sind standardmäßig interaktiv. "Nuget. exe" enthält einen Switch, um ihn als [nicht interaktiv](../nuget-exe-CLI-Reference.md)zu gestalten.
Zusätzlich werden die Plug-ins "nuget. exe" und "Visual Studio" den Benutzer zur Eingabe auffordern.
In "dotnet. exe" gibt es keine Eingabeaufforderung, und der Standardwert ist "nicht interaktiv".

Der Authentifizierungsmechanismus in "dotnet. exe" ist der Geräte Fluss. Wenn der Vorgang zum Wiederherstellen oder Hinzufügen eines Pakets interaktiv ausgeführt wird, werden der Vorgang blockiert, und es wird beschrieben, wie die Authentifizierungen durchgeführt werden.
Wenn der Benutzer die Authentifizierung abschließt, wird der Vorgang fortgesetzt.

Um den Vorgang interaktiv durchführen zu können, `--interactive`sollte eine bestanden werden.
Zurzeit unterstützen `dotnet restore` nur `dotnet add package` die expliziten Befehle und einen interaktiven Switch.
Es gibt keinen interaktiven Switch für `dotnet build` und `dotnet publish`.

## <a name="authentication-in-msbuild"></a>Authentifizierung in MSBuild

Ähnlich wie bei "dotnet. exe" ist "MSBuild. exe" standardmäßig nicht interaktiv. der Authentifizierungsmechanismus "MSBuild. exe" ist der Geräte Fluss.
Um die Wiederherstellung anzuhalten und auf die Authentifizierung zu warten, wenden Sie `msbuild -t:restore -p:NuGetInteractive="true"`Restore with an.

## <a name="creating-a-cross-platform-authentication-plugin"></a>Erstellen eines plattformübergreifenden Authentifizierungs-Plug-ins

Eine Beispiel Implementierung finden Sie im [Microsoft Credential Provider-Plug](https://github.com/Microsoft/artifacts-credprovider)-in.

Es ist sehr wichtig, dass die Plug-ins den Sicherheitsanforderungen entsprechen, die von den nuget-Client Tools festgelegt werden.
Die mindestens erforderliche Version für ein Plug-in als Authentifizierungs-Plug-in ist *2.0.0*.
Nuget führt den Handshake mit dem Plug-in durch und fragt die unterstützten Vorgangs Ansprüche ab.
Weitere Informationen zu den spezifischen Nachrichten finden Sie in den nuget- [Protokollmeldungen](NuGet-Cross-Platform-Plugins.md#protocol-messages-index) zum plattformübergreifenden Plug-in.

Nuget legt die Protokollebene fest und stellt ggf. Proxy Informationen für das Plug-in bereit.
Die Protokollierung in der nuget-Konsole ist nur akzeptabel, wenn nuget die Protokollebene auf das Plug-in festgelegt hat.

- .NET Framework Plug-in-Authentifizierungs Verhalten

In .NET Framework können die Plug-ins einen Benutzer in Form eines Dialog Felds zur Eingabe auffordern.

- .Net Core-Plug-in-Authentifizierung

In .net Core kann ein Dialogfeld nicht angezeigt werden. Die Plug-ins sollten zum Authentifizieren den Geräte Fluss verwenden.
Das Plug-in kann Protokollmeldungen mit Anweisungen an den Benutzer an nuget senden.
Beachten Sie, dass die Protokollierung verfügbar ist, nachdem die Protokollebene auf das Plug-in festgelegt wurde.
Nuget übernimmt keine interaktive Eingabe von der Befehlszeile aus.

Wenn der Client das Plug-in mit den Anmelde Informationen für die Authentifizierung Get aufruft, müssen die Plug-ins dem Interaktivität-Switch entsprechen und den Dialog Schalter berücksichtigen. 

In der folgenden Tabelle wird das Verhalten des Plug-Ins für alle Kombinationen zusammengefasst.

| Isnoninteractive | Canshowdialog | Plugin-Verhalten |
| ---------------- | ------------- | --------------- |
| true | true | Der Schalter isnoninteractive hat Vorrang vor dem Dialogfeld Switch. Das Plug-in ist nicht berechtigt, ein Dialogfeld zu öffnen. Diese Kombination gilt nur für .NET Framework-Plug-ins. |
| true | false | Der Schalter isnoninteractive hat Vorrang vor dem Dialogfeld Switch. Das Plug-in darf nicht blockiert werden. Diese Kombination ist nur für .net Core-Plug-ins gültig. |
| false | true | Das Plug-in sollte ein Dialogfeld anzeigen. Diese Kombination gilt nur für .NET Framework-Plug-ins. |
| false | false | Das Plug-in sollte/kann ein Dialogfeld nicht anzeigen. Das Plug-in sollte mithilfe des Geräte Flusses authentifiziert werden, indem eine Anweisungs Nachricht über die Protokollierung protokolliert wird. Diese Kombination ist nur für .net Core-Plug-ins gültig. |

Weitere Informationen finden Sie in den folgenden Spezifikationen, bevor Sie ein Plug-in schreiben.

- [Plug-in für nuget-Paket](https://github.com/NuGet/Home/wiki/NuGet-Package-Download-Plugin)
- [Nuget-Plug-in für die nuget-Authentifizierung](https://github.com/NuGet/Home/wiki/NuGet-cross-plat-authentication-plugin)
