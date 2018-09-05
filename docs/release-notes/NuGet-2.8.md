---
title: Anmerkungen zu NuGet 2.8
description: Anmerkungen zu NuGet 2.8, einschließlich der bekannten Probleme, Fehlerkorrekturen, hinzugefügter Features und DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 98b8b7334738306e6d40ba7c455409a87c4bb822
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547458"
---
# <a name="nuget-28-release-notes"></a>Anmerkungen zu NuGet 2.8

[Anmerkungen zu NuGet 2.7.2](../release-notes/nuget-2.7.2.md) | [Anmerkungen zu NuGet 2.8.1](../release-notes/nuget-2.8.1.md)

NuGet 2.8 wurde am 29. Januar 2014 veröffentlicht.

## <a name="acknowledgements"></a>Bestätigungen

1. [Falco Pritchard](https://www.codeplex.com/site/users/view/leppie) ([@leppie](https://twitter.com/leppie))
    - [#3466](https://nuget.codeplex.com/workitem/3466) : beim Packen von Paketen, überprüfen die Id der abhängigkeitspakete vorhanden sind.
2. [Maarten Balliauw](https://www.codeplex.com/site/users/view/maartenba) ([@maartenballiauw](https://twitter.com/maartenballiauw))
    - [#2379](https://nuget.codeplex.com/workitem/2379) -entfernen Sie das $metadata-Suffix ein, wenn Persistening Anmeldeinformationen feed.
3. [Filip De Vos](https://www.codeplex.com/site/users/view/FilipDeVos) ([@foxtricks](https://twitter.com/foxtricks))
    - [#3538](http://nuget.codeplex.com/workitem/3538) - Unterstützung, die Projektdatei für die nuget.exe-Update-Befehl angeben.
4. [Juan Gonzalez](https://www.codeplex.com/site/users/view/jjgonzalez)
    - [#3536](http://nuget.codeplex.com/workitem/3536) -Ersetzungstoken, die nicht mit - IncludeReferencedProjects übergeben.
5. [David Poole](https://www.codeplex.com/site/users/view/Sarkie) ([@Sarkie_Dave](https://twitter.com/Sarkie_Dave))
    - [#3677](http://nuget.codeplex.com/workitem/3677) -beheben nuget.push OutOfMemoryException-Fehler auslösen, wenn großes Paket übertragen.
6. [Wouter Ouwens](https://www.codeplex.com/site/users/view/Despotes)
    - [#3666](http://nuget.codeplex.com/workitem/3666) – Wenn auf ein Projekt einer anderen CLI/C++-Projekt, falsche Zielpfad beheben.
7. [ADAM Ralph](http://www.codeplex.com/site/users/view/adamralph) ([@adamralph](https://twitter.com/adamralph))
    - [#3639](https://nuget.codeplex.com/workitem/3639) -Pakete als entwicklungsabhängigkeiten standardmäßig installiert werden
8. [David Fowler](https://www.codeplex.com/site/users/view/dfowler) ([@davidfowl](https://twitter.com/davidfowl))
    - [#3717](https://nuget.codeplex.com/workitem/3717) -implizite Upgrades auf die neueste Patchversion entfernen
9. [Gregory Vandenbrouck](https://www.codeplex.com/site/users/view/vdbg)
    - Verschiedene Programmfehler behobene und Verbesserungen für die "NuGet.Server" und der nuget.exe-Spiegel-Befehl.
    - Diese Arbeit erfolgte in Monaten mit Gregory arbeiten mit uns auf das richtige Timing, in der Master für 2.8 zu integrieren.

## <a name="patch-resolution-for-dependencies"></a>Patch-Auflösung für Abhängigkeiten

Beim Auflösen von paketabhängigkeiten hat NuGet in der Vergangenheit implementiert, eine Strategie für die niedrigste Haupt- und Nebenversionsnummern Paketversion, die Abhängigkeiten für das Paket erfüllt, auswählen. Im Gegensatz zu den Haupt- und Nebenversionsnummern-Version jedoch wurde die Patchversion immer auf die höchste Version behoben. Obwohl das Verhalten arglose war, erstellt es einen Mangel an Determinismus zum Installieren von Paketen mit Abhängigkeiten. Betrachten Sie das folgende Beispiel:

    PackageA@1.0.0 -[ >=1.0.0 ]-> PackageB@1.0.0

    Developer1 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.0

    PackageB@1.0.1 is published

    Developer2 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.1

In diesem Beispiel, obwohl Developer1 und Developer2 installiert PackageA@1.0.0, jeweils am Ende mit einer anderen Version von PackageB. NuGet 2.8 ändert dieses Standardverhalten, dass das Verhalten des Dependency-Auflösung für Patchversionen mit dem Verhalten für Haupt-und Nebenversionen konsistent ist. Im obigen Beispiel, klicken Sie dann PackageB@1.0.0 würde durch die Installation von installiert werden PackageA@1.0.0, unabhängig von der neueren Patchversion.

## <a name="-dependencyversion-switch"></a>-Optionen "dependencyversion" wechseln

Wenn NuGet 2.8 ändert die _Standard_ Verhalten zum Auflösen von Abhängigkeiten, werden außerdem eine genauere Steuerung der Abhängigkeit Lösungsprozess über den Switch - Optionen "dependencyversion" in der Konsole des Paket-Manager hinzugefügt. Der Schalter aktiviert Auflösen von Abhängigkeiten, um die niedrigste mögliche Version (Standardverhalten), die höchste mögliche Version oder die höchste Nebenversion oder Patch-Version.  Diese Option funktioniert nur für Install-Package, in der Powershell-Befehl.

![Optionen "dependencyversion" wechseln](./media/NuGet-2.8/dependencyversion.png)

## <a name="dependencyversion-attribute"></a>Optionen "dependencyversion"-Attribut

Zusätzlich zu den aufgeführten, NuGet gewährt auch die Möglichkeit, legen Sie ein neues Attribut in der Datei "NuGet.config" - Optionen "dependencyversion"-Switch definieren was der Standardwert ist, wenn der Switch - Optionen "dependencyversion" bei einem Aufruf von nicht angegeben ist Install-Package. Dieser Wert wird auch durch das Dialogfeld "NuGet-Paket-Manager" für beliebige Vorgänge der Install-Package berücksichtigt werden. Um diesen Wert festzulegen, fügen Sie das Attribut unter zu Ihrer Datei "NuGet.config" hinzu:

    <config>
        <add key="dependencyversion" value="Highest" />
    </config>

## <a name="preview-nuget-operations-with--whatif"></a>Vorschau-NuGet-Vorgängen mit - whatif

Einige NuGet-Pakete können die Tiefe von Abhängigkeitsdiagrammen haben, und daher es hilfreich sein, während einer Installation, deinstallieren oder aktualisieren, lesen zunächst, was passiert, kann. NuGet 2.8 fügt den PowerShell - Whatif standardswitch das Install-Package-Paket deinstallieren und Update-Package-Befehle zum Aktivieren die Visualisierung des gesamten Abschluss von Paketen, die auf die der Befehl angewendet werden soll. Z. B. Ausführung `install-package Microsoft.AspNet.WebApi -whatif` in eine leere ASP.NET Web Application liefert folgendes Ergebnis.

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

## <a name="downgrade-package"></a>Ein Downgrade-Paket

Es ist nicht ungewöhnlich, mit eine Vorabversion von einem Paket zu installieren, um neue Funktionen zu untersuchen und dann entscheiden, ob ein Rollback auf die letzte stabile Version. Vor NuGet 2.8 war dies ein mehrstufiger Prozess deinstalliert werden, die Vorabversion Paket und seine Abhängigkeiten, und anschließend die frühere Version installieren. Mit NuGet 2.8 führt allerdings-Paket für das Update jetzt die gesamte paketabschluss (z.B. der Paket Abhängigkeit-Struktur) auf die vorherige Version Rollback.

## <a name="development-dependencies"></a>Entwicklungsabhängigkeiten

Viele verschiedene Arten von Funktionen können als NuGet-Pakete – einschließlich Tools, die verwendet werden, für die Optimierung des Entwicklungsprozesses übermittelt werden. Diese Komponenten, während sie zunächst ein neues Paket entwickeln werden, können nicht berücksichtigen Sie eine Abhängigkeit für das neue Paket bei einem späteren Zeitpunkt der Veröffentlichung. NuGet 2.8 kann ein Paket zur Identifizierung in den `.nuspec` -Datei als ein DevelopmentDependency. Bei der Installation diese Metadaten werden auch hinzugefügt werden die `packages.config` -Datei des Projekts, in dem das Paket installiert wurde. Wenn, `packages.config` Datei wird später für NuGet-Abhängigkeiten während analysiert `nuget.exe pack`, schließt er diese Abhängigkeiten als entwicklungsabhängigkeiten gekennzeichnet.

## <a name="individual-packagesconfig-files-for-different-platforms"></a>Einzelne Datei "Packages.config"-Dateien für verschiedene Plattformen

Wenn Sie Anwendungen für mehrere Zielplattformen zu entwickeln, ist es üblich, verschiedene Projektdateien für jede von der jeweiligen Buildumgebungen verfügen. Es ist auch üblich, die verschiedene NuGet-Paketen in verschiedenen Projektdateien verwenden, wie Pakete verschiedene Ebenen der Unterstützung für verschiedene Plattformen haben. NuGet 2.8 bietet verbesserte Unterstützung für dieses Szenario durch das Erstellen von anderen `packages.config` -Dateien für andere plattformspezifische Projektdateien.

![Mehrere Dateien der Datei "Package.config"](./media/NuGet-2.8/multiple-packageconfigs.png)

## <a name="fallback-to-local-cache"></a>Fallback auf den lokalen Cache

Obwohl die NuGet-Pakete, z. B. in der Regel aus einem Remotekatalog genutzt werden [der NuGet Gallery](http://www.nuget.org/) mithilfe einer Netzwerkverbindungs viele Szenarios, in dem der Client ist nicht verbunden, werden. Ohne eine Netzwerkverbindung konnte der NuGet-Client nicht für die erfolgreiche Installation von Paketen – selbst wenn diese Pakete bereits auf dem Clientcomputer im lokalen NuGet-Cache enthalten waren. NuGet 2.8 hinzugefügt der Paket-Manager-Konsole automatisch nach fallback Cacheservern. Beispielsweise zeigt beim Trennen des Netzwerkadapters, und installieren jQuery, die Konsole Folgendes:

    PM> Install-Package jquery
    The source at nuget.org [https://www.nuget.org/api/v2/] is unreachable. Falling back to NuGet Local Cache at C:\Users\me\AppData\Local\NuGet\Cache
    Installing 'jQuery 2.0.3'.
    Successfully installed 'jQuery 2.0.3'.
    Adding 'jQuery 2.0.3' to WebApplication18.
    Successfully added 'jQuery 2.0.3' to WebApplication18.

Die Cache-fallback-Funktion erfordert keine bestimmten Befehlsargumente. Darüber hinaus Cache fallback funktioniert derzeit nur in der Konsole des Paket-Manager: das Verhalten funktioniert derzeit nicht im Dialogfeld "Paket-Manager".

## <a name="webmatrix-nuget-client-updates"></a>WebMatrix-NuGet-Client aktualisiert.

Zusammen mit NuGet 2.8, die NuGet-Erweiterung für WebMatrix wurde ebenfalls aktualisiert, um viele der wichtigsten Features, die im Lieferumfang enthalten [NuGet 2.5](../release-notes/nuget-2.5.md). Mit den neuen Funktionen gehören die wie "Update-All", "Minimum-NuGet-Version" und für Inhaltsdateien überschreiben können.

So aktualisieren Sie die NuGet-Paket-Manager-Erweiterung in WebMatrix 3:

1. Öffnen Sie WebMatrix 3
1. Klicken Sie auf das Symbol "Erweiterungen" im Menüband
1. Wählen Sie die Registerkarte "Updates"
1. Klicken Sie auf, um NuGet-Paket-Manager auf 2.5.0 zu aktualisieren.
1. Schließen Sie und starten Sie WebMatrix 3

Dies ist das NuGet-Team erste Version der NuGet-Paket-Manager-Erweiterung für WebMatrix.  Der Code wurde vor kurzem von Microsoft in der Open Source-NuGet-Projekt bereitgestellt. Zuvor wurde die NuGet-Integration in WebMatrix erstellt, und konnte Out-of-Band-aus WebMatrix nicht aktualisiert werden.  Wir haben jetzt die Möglichkeit, weitere zusammen mit den anderen NuGet Clienttools zu aktualisieren.

## <a name="bug-fixes"></a>Fehlerkorrekturen

Eine der wichtigen Fehlerbehebungen vorgenommen wurde leistungsverbesserungen in der Update-Package-Befehl zu installieren.

Zusätzlich zu diesen Features und die oben genannten Leistung Fehlerbehebung enthält diese Version von NuGet auch viele andere Fehlerkorrekturen. Gab es 181 insgesamt in den Release behobenen Problemen. Eine vollständige Liste der Arbeit Elemente eine feste in NuGet 2.8, bitte Ansicht der [NuGet Issue Tracker für diese Version](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.8&status=all).
