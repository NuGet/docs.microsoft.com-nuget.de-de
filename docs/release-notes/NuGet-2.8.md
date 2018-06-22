---
title: NuGet 2.8-Versionshinweise
description: Versionshinweise für NuGet 2.8 enthalten bekannte Probleme, Fehlerbehebungen, Funktionen und Archivierung von dcrs Design einschließlich.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 9f472f1370bfedaf04ebe889c0da01155b8aec22
ms.sourcegitcommit: a6ca160b1e7e5c58b135af4eba0e9463127a59e8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/28/2018
ms.locfileid: "32044689"
---
# <a name="nuget-28-release-notes"></a>NuGet 2.8-Versionshinweise

[Anmerkungen zur Version des NuGet-2.7.2](../release-notes/nuget-2.7.2.md) | [NuGet 2.8.1-Versionshinweise](../release-notes/nuget-2.8.1.md)

NuGet 2.8 wurde am 29. Januar 2014 veröffentlicht.

## <a name="acknowledgements"></a>Bestätigungen

1. [Llewellyn Pritchard](https://www.codeplex.com/site/users/view/leppie) ([@leppie](https://twitter.com/leppie))
    - [#3466](https://nuget.codeplex.com/workitem/3466) – Wenn Sie Pakete, überprüfen die Id der abhängigkeitspakete zu packen.
2. [Maarten Balliauw](https://www.codeplex.com/site/users/view/maartenba) ([@maartenballiauw](https://twitter.com/maartenballiauw))
    - [#2379](https://nuget.codeplex.com/workitem/2379) -entfernen Sie das $metadata-Suffix ein, wenn Persistening Anmeldeinformationen feed.
3. [Filip De Vos](https://www.codeplex.com/site/users/view/FilipDeVos) ([@foxtricks](https://twitter.com/foxtricks))
    - [#3538](http://nuget.codeplex.com/workitem/3538) - Unterstützung, die Projektdatei für den nuget.exe Update-Befehl angeben.
4. [Juan Gonzalez](https://www.codeplex.com/site/users/view/jjgonzalez)
    - [#3536](http://nuget.codeplex.com/workitem/3536) -Ersatz-Token, die nicht mit - IncludeReferencedProjects übergeben.
5. [David Poole](https://www.codeplex.com/site/users/view/Sarkie) ([@Sarkie_Dave](https://twitter.com/Sarkie_Dave))
    - [#3677](http://nuget.codeplex.com/workitem/3677) -beheben nuget.push OutOfMemoryException auslösen, wenn ein großes Paket per Push übertragen.
6. [Wouter Ouwens](https://www.codeplex.com/site/users/view/Despotes)
    - [#3666](http://nuget.codeplex.com/workitem/3666) -Korrektur falsch Zielpfad bei Projekt ein anderes CLI/C++-Projekt verweist.
7. [ADAM Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))
    - [#3639](https://nuget.codeplex.com/workitem/3639) -Pakete als Entwicklung Abhängigkeiten, die standardmäßig installiert werden
8. [David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))
    - [#3717](https://nuget.codeplex.com/workitem/3717) -implizite Upgrades auf die neueste Patchversion entfernen
9. [Gregory Vandenbrouck](https://www.codeplex.com/site/users/view/vdbg)
    - Mehrere Fehler Korrekturen und Verbesserungen für NuGet.Server in und dem nuget.exe Mirror-Befehl.
    - Dieses Werk wurde über mehrere Monate Gregory arbeiten mit uns auf die richtige zeitliche Steuerung zur Integration in Master für 2.8 abgeschlossen.

## <a name="patch-resolution-for-dependencies"></a>Patch für die Auflösung für Abhängigkeiten

Wenn paketabhängigkeiten behoben haben, verfügt über NuGet in der Vergangenheit implementiert eine Strategie für die niedrigste Haupt- und Nebenversionsnummern Paketversion, die Abhängigkeiten für das Paket erfüllt, auszuwählen. Im Gegensatz zu den Haupt- und Nebenversionsnummern-Version wurde die Patchversion jedoch immer die höchste Version behoben. Obwohl das Verhalten Exploit wurde, erstellt es einen mangelnde Determinismus zum Installieren von Paketen mit Abhängigkeiten. Betrachten Sie das folgende Beispiel:

    PackageA@1.0.0 -[ >=1.0.0 ]-> PackageB@1.0.0

    Developer1 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.0

    PackageB@1.0.1 is published

    Developer2 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.1

In diesem Beispiel, obwohl Developer1 und Developer2 installiert PackageA@1.0.0, sich mit einer anderen Version von PackageB jedes beendet. NuGet 2.8 dieses Standardverhalten so geändert, dass das Verhalten des Abhängigkeit-Auflösung für die Patch-Versionen mit dem Verhalten für Haupt-und Nebenversionen konsistent ist. Im obigen Beispiel, klicken Sie dann PackageB@1.0.0 würde als Ergebnis der Installation installiert werden PackageA@1.0.0, unabhängig von der neueren Patchversion.

## <a name="-dependencyversion-switch"></a>DependencyVersion - Switch

Obwohl NuGet 2.8 ändert die _Standard_ Verhalten zu Abhängigkeiten werden aufgelöst, werden außerdem präzisen Steuern Abhängigkeit Auflösungsvorgang über den Switch - DependencyVersion in der Paket-Manager-Konsole hinzugefügt. Der Switch ermöglicht die niedrigste mögliche Version (Standardverhalten), die höchste mögliche Version oder die höchste Nebenversion oder Patchversion Auflösen von Abhängigkeiten.  Diese Option funktioniert nur bei Installationspakets in der Powershell-Befehl.

![DependencyVersion Switch](./media/NuGet-2.8/dependencyversion.png)

## <a name="dependencyversion-attribute"></a>DependencyVersion-Attribut

Zusätzlich zu den DependencyVersion - Switch ausführliche oben NuGet hat die Möglichkeit ebenfalls zulässig. Legen Sie ein neues Attribut in der Datei "NuGet.config" definieren neuerungen der Standardwert, wenn der DependencyVersion - Schalter nicht in einem Aufruf der angegeben wird Install-Package. Dieser Wert wird auch über das Dialogfeld "NuGet-Paket-Manager" für alle Paketvorgängen installieren eingehalten werden. Um diesen Wert festzulegen, fügen Sie das Attribut unter mit Ihrer Datei "NuGet.config" hinzu:

    <config>
        <add key="dependencyversion" value="Highest" />
    </config>

## <a name="preview-nuget-operations-with--whatif"></a>NuGet-Vorschauvorgänge mit "-WhatIf"

Einige NuGet-Pakete können umfassende Abhängigkeitsdiagramme haben und daher es hilfreich sein, während der Installation, Deinstallation oder Aktualisierungsvorgang zunächst sehen, was passiert. 2.8 NuGet-hinzugefügt Paket installieren, deinstallieren Sie Pakets und Update-Paket-Befehle zum Aktivieren die Visualisierung der gesamte Schließung von Paketen, die auf die der Befehl angewendet werden soll PowerShell "- WhatIf" standardswitch. Z. B. Ausführung `install-package Microsoft.AspNet.WebApi -whatif` in eine leere ASP.NET Web Anwendung Folgendes ergibt.

    PM> install-package Microsoft.AspNet.WebApi -whatif
    Attempting to resolve dependency 'Microsoft.AspNet.WebApi.WebHost (≥ 5.0.0)'.
    Attempting to resolve dependency 'Microsoft.AspNet.WebApi.Core (≥ 5.0.0)'.
    Attempting to resolve dependency 'Microsoft.AspNet.WebApi.Client (≥ 5.0.0)'.
    Attempting to resolve dependency 'Newtonsoft.Json (≥ 4.5.11)'.
    Install Newtonsoft.Json 4.5.11
    Install Microsoft.AspNet.WebApi.Client 5.0.0
    Install Microsoft.AspNet.WebApi.Core 5.0.0
    Install Microsoft.AspNet.WebApi.WebHost 5.0.0
    Install Microsoft.AspNet.WebApi 5.0.0

## <a name="downgrade-package"></a>Downgrade für Paket

Es ist nicht ungewöhnlich, installieren Sie eine Vorabversion von einem Paket, um neue Funktionen zu untersuchen und dann entscheiden, ob ein Rollback auf die letzte stabile Version. Bevor Sie NuGet 2.8 enthalten war dies mehreren Schritten der Vorabversion Paket und seine Abhängigkeiten deinstallieren und installieren Sie dann die frühere Version. Mit NuGet 2.8 enthalten wird jedoch das Updatepaket jetzt das gesamte Paket schließen (z. B. das Paket Abhängigkeitsstruktur) auf die vorherige Version zurückgesetzt.

## <a name="development-dependencies"></a>Entwicklung Abhängigkeiten

Viele verschiedene Arten von Funktionen können als NuGet-Pakete - einschließlich Tools, die verwendet werden, für die Optimierung des Entwicklungsprozesses übermittelt werden. Diese Komponenten sollte können sie bei der Entwicklung eines neuen Pakets instrumentellen sein nicht verwendet werden eine Abhängigkeit für das neue Paket, wenn sie später erneut veröffentlicht wird. NuGet 2.8 kann ein Paket zur Identifizierung in den `.nuspec` -Datei als ein DevelopmentDependency. Bei der Installation, diese Metadaten werden auch hinzugefügt werden die `packages.config` -Datei des Projekts, in dem das Paket installiert wurde. Wenn, `packages.config` Datei wird später für NuGet Abhängigkeiten während analysiert `nuget.exe pack`, schließt er diese Abhängigkeiten als Entwicklung Abhängigkeiten gekennzeichnet.

## <a name="individual-packagesconfig-files-for-different-platforms"></a>Einzelne "Packages.config" Dateien für unterschiedliche Plattformen

Bei der Entwicklung von Anwendungen für mehrere Zielplattformen ist es üblich, andere Projektdateien für jede von der jeweiligen Buildumgebungen zu verwenden. Es ist auch, die verschiedene NuGet-Pakete in andere Projektdateien, nutzen gemeinsam, wie Pakete verschiedene Ebenen der Unterstützung für unterschiedliche Plattformen haben. NuGet 2.8 bietet verbesserte Unterstützung für dieses Szenario durch das Erstellen von verschiedenen `packages.config` Dateien für verschiedene plattformspezifisches Projektdateien.

![Mehrere package.config-Dateien](./media/NuGet-2.8/multiple-packageconfigs.png)

## <a name="fallback-to-local-cache"></a>Fallback auf den lokalen Cache

Obwohl die NuGet-Pakete, z. B. in der Regel von einem remote-Katalog verbraucht werden [der NuGet Gallery](http://www.nuget.org/) mithilfe einer Netzwerkverbindung, es gibt viele Szenarien, in denen der Client ist nicht verbunden. Ohne eine Netzwerkverbindung konnte der NuGet-Client nicht für die erfolgreiche Installation von Paketen – selbst wenn diese Pakete bereits auf dem Clientcomputer in den lokalen NuGet-Cache enthalten waren. NuGet 2.8 enthalten hinzugefügt die Paket-Manager-Konsole fallback automatische Cache. Beispielsweise zeigt beim Trennen des Netzwerkadapters, und Installieren von jQuery, die Konsole Folgendes:

    PM> Install-Package jquery
    The source at nuget.org [https://www.nuget.org/api/v2/] is unreachable. Falling back to NuGet Local Cache at C:\Users\me\AppData\Local\NuGet\Cache
    Installing 'jQuery 2.0.3'.
    Successfully installed 'jQuery 2.0.3'.
    Adding 'jQuery 2.0.3' to WebApplication18.
    Successfully added 'jQuery 2.0.3' to WebApplication18.

Die Cache-fallback-Funktion erfordert keine Befehlsargumente bestimmte. Darüber hinaus fallback Cache funktioniert zurzeit nur in der Paket-Manager-Konsole – das Verhalten funktioniert zurzeit nicht im Dialogfeld "Paket-Manager".

## <a name="webmatrix-nuget-client-updates"></a>WebMatrix-NuGet-Clientupdates

Zusammen mit NuGet 2.8 enthalten, die NuGet-Erweiterung für WebMatrix wurde ebenfalls aktualisiert, um viele der Hauptfunktionen, die im Lieferumfang enthalten [NuGet 2.5](../release-notes/nuget-2.5.md). Neue Funktionen zählen die z. B. "Alle aktualisieren", "Minimum NuGet-Version" und die Möglichkeit für das Überschreiben von Inhaltsdateien.

So aktualisieren Sie die NuGet-Paket-Manager-Erweiterung in WebMatrix 3:

1. Öffnen Sie WebMatrix 3
1. Klicken Sie auf das Symbol "Erweiterungen" im Menüband
1. Wählen Sie die Registerkarte "Softwareupdates"
1. Klicken Sie auf, um NuGet-Paket-Manager auf 2.5.0 zu aktualisieren.
1. Schließen Sie, und starten Sie die WebMatrix-3

Dies ist die erste Version der Erweiterung NuGet-Paket-Manager das NuGet-Team für WebMatrix.  Der Code wurde von Microsoft in der Open Source-NuGet-Projekts vor kurzem beigesteuert. Zuvor wurde die NuGet-Integration in WebMatrix integriert und konnte nicht außerhalb des Bereichs von WebMatrix aktualisiert werden.  Wir haben jetzt die Möglichkeit, weitere zusammen mit den restlichen NuGet Clienttools zu aktualisieren.

## <a name="bug-fixes"></a>Fehlerkorrekturen

Einer der wichtigsten Fehlerbehebungen vorgenommen wurde Leistungssteigerung in der Update-Paket-Befehl zu installieren.

Zusätzlich zu diesen Funktionen und den zuvor erwähnten Leistung Fix enthält diese Version von NuGet auch zahlreiche Programmfehlerbehebungen. Es gab 181 insgesamt Probleme, die in der Version behoben. Eine vollständige Liste der Arbeit Elemente korrigiert in NuGet 2.8 enthalten, bitte Ansicht der [NuGet Issue Tracker für diese Version](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.8&status=all).
