---
title: Anmerkungen zu dieser Version von nuget 2,8
description: Anmerkungen zu dieser Version von nuget 2,8 einschließlich bekannter Probleme, Fehlerbehebungen, hinzugefügter Features und dcrs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 98b8b7334738306e6d40ba7c455409a87c4bb822
ms.sourcegitcommit: b138bc1d49fbf13b63d975c581a53be4283b7ebf
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/03/2020
ms.locfileid: "93237020"
---
# <a name="nuget-28-release-notes"></a>Anmerkungen zu dieser Version von nuget 2,8

[Nuget 2.7.2 Anmerkungen](../release-notes/nuget-2.7.2.md)  |  zu dieser Version [Anmerkungen zu dieser Version von nuget 2.8.1](../release-notes/nuget-2.8.1.md)

Nuget 2,8 wurde am 29. Januar 2014 veröffentlicht.

## <a name="acknowledgements"></a>Danksagung

1. [Llewellyn Pritchard](https://www.codeplex.com/site/users/view/leppie) ( [@leppie](https://twitter.com/leppie) )
    - [#3466](https://nuget.codeplex.com/workitem/3466) : beim Packen von Paketen wird die ID der Abhängigkeits Pakete überprüft.
2. [Maarten balliauw](https://www.codeplex.com/site/users/view/maartenba) ( [@maartenballiauw](https://twitter.com/maartenballiauw) )
    - Entfernen Sie das $Metadata Suffix [#2379](https://nuget.codeplex.com/workitem/2379) , wenn Sie Feed-Anmelde Informationen persistat.
3. [Filip de Vos](https://www.codeplex.com/site/users/view/FilipDeVos) ( [@foxtricks](https://twitter.com/foxtricks) )
    - [#3538](http://nuget.codeplex.com/workitem/3538) -Unterstützung für die Angabe der Projektdatei für den nuget.exe Update-Befehl.
4. [Juan Gonzalez](https://www.codeplex.com/site/users/view/jjgonzalez)
    - [#3536](http://nuget.codeplex.com/workitem/3536) Ersatz Token, die nicht mit-includereferencedprojects übergebenen werden.
5. [David Poole](https://www.codeplex.com/site/users/view/Sarkie) ( [@Sarkie_Dave](https://twitter.com/Sarkie_Dave) )
    - [#3677](http://nuget.codeplex.com/workitem/3677) -Korrektur nuget. Push löst OutOfMemoryException aus, wenn das große Paket per Push übertragen wird.
6. [Wouter-Ouwens](https://www.codeplex.com/site/users/view/Despotes)
    - [#3666](http://nuget.codeplex.com/workitem/3666) Korrektur eines falschen Zielpfads, wenn das Projekt auf ein anderes CLI/C++-Projekt verweist.
7. [Adam Ralph](http://www.codeplex.com/site/users/view/adamralph) ( [@adamralph](https://twitter.com/adamralph) )
    - [#3639](https://nuget.codeplex.com/workitem/3639) zulassen, dass Pakete standardmäßig als Entwicklungs Abhängigkeiten installiert werden
8. [David Fowler](https://www.codeplex.com/site/users/view/dfowler) ( [@davidfowl](https://twitter.com/davidfowl) )
    - [#3717](https://nuget.codeplex.com/workitem/3717) entfernen impliziter Upgrades auf die neueste Patchversion
9. [Gregory vandumbrouck](https://www.codeplex.com/site/users/view/vdbg)
    - Verschiedene Fehlerbehebungen und Verbesserungen für "nuget. Server", den Befehl "nuget.exe Spiegelung" und andere.
    - Diese Arbeit wurde über mehrere Monate durchgeführt, und Gregory arbeitete mit uns am richtigen Zeitpunkt für die Integration in Master für 2,8.

## <a name="patch-resolution-for-dependencies"></a>Patchauflösung für Abhängigkeiten

Beim Auflösen von Paketabhängigkeiten hat nuget in der Vergangenheit eine Strategie zum Auswählen der niedrigsten Haupt-und neben Paketversion implementiert, die die Abhängigkeiten des Pakets erfüllt. Anders als bei der Haupt-und neben Version wurde die Patchversion jedoch immer auf die höchste Version aufgelöst. Obwohl das Verhalten wohl gemeint war, wurde für die Installation von Paketen mit Abhängigkeiten ein fehlender Determinismus geschaffen. Betrachten Sie das folgenden Beispiel:

    PackageA@1.0.0 -[ >=1.0.0 ]-> PackageB@1.0.0

    Developer1 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.0

    PackageB@1.0.1 is published

    Developer2 installs PackageA@1.0.0: installed PackageA@1.0.0 and PackageB@1.0.1

In diesem Beispiel hat die Installation von Developer1 und Developer2 PackageA@1.0.0 jeweils eine andere Version von packageb. Mit nuget 2,8 wird dieses Standardverhalten geändert, sodass das Verhalten der Abhängigkeitsauflösung für Patchversionen mit dem Verhalten für die Haupt-und neben Versionen konsistent ist. Im obigen Beispiel PackageB@1.0.0 wird dann als Ergebnis der Installation von installiert PackageA@1.0.0 , unabhängig von der neueren Patchversion.

## <a name="-dependencyversion-switch"></a>-Dependencyversion-Schalter

Obwohl nuget 2,8 das _Standard_ Verhalten für das Auflösen von Abhängigkeiten ändert, bietet es auch eine präzisere Kontrolle über den Prozess der Abhängigkeitsauflösung über den Schalter-dependencyversion in der Paket-Manager-Konsole. Der-Switch ermöglicht das Auflösen von Abhängigkeiten zur niedrigsten möglichen Version (Standardverhalten), der höchstmöglichen Version oder der höchsten neben Version bzw. der höchsten Version des Patches.  Dieser Switch funktioniert nur für install-Package im PowerShell-Befehl.

![Dependencyversion-Schalter](./media/NuGet-2.8/dependencyversion.png)

## <a name="dependencyversion-attribute"></a>Dependencyversion-Attribut

Zusätzlich zum oben beschriebenen Schalter "-dependencyversion" hat nuget auch die Möglichkeit, ein neues Attribut in der Nuget.Config Datei festzulegen, die den Standardwert definiert, wenn der Schalter "-dependencyversion" bei einem Aufruf von "Install-Package" nicht angegeben ist. Dieser Wert wird auch vom Dialog Feld nuget-Paket-Manager für alle Installationspaket Vorgänge beachtet. Um diesen Wert festzulegen, fügen Sie das unten angegebene-Attribut ihrer Nuget.Config-Datei hinzu:

    <config>
        <add key="dependencyversion" value="Highest" />
    </config>

## <a name="preview-nuget-operations-with--whatif"></a>Vorschau von nuget-Vorgängen mit-WhatIf

Einige nuget-Pakete können über Deep-Abhängigkeits Diagramme verfügen. Daher kann es bei einem Installations-, Deinstallations-oder Update Vorgang hilfreich sein, um zuerst zu sehen, was passiert. Nuget 2,8 fügt den standardmäßigen PowerShell-WhatIf-Switch zu den Befehlen install-Package, uninstall-Package und Update-Package hinzu, um die Visualisierung des gesamten Abschlusses von Paketen zu ermöglichen, auf die der Befehl angewendet wird. Beispielsweise `install-package Microsoft.AspNet.WebApi -whatif` ergibt die Ausführung in einer leeren ASP.NET-Webanwendung Folgendes:

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

## <a name="downgrade-package"></a>Paket herabstufen

Es ist nicht ungewöhnlich, eine Vorabversion eines Pakets zu installieren, um neue Funktionen zu untersuchen und dann ein Rollback auf die letzte stabile Version auszuführen. Vor nuget 2,8 war dies ein mehrstufiger Prozess der Deinstallieren des vorab Pakets und seiner Abhängigkeiten und der anschließenden Installation der früheren Version. Mit nuget 2,8 führt das Update-Package nun jedoch ein Rollback für den gesamten Paket Abschluss (z. b. die Abhängigkeitsstruktur des Pakets) zur vorherigen Version aus.

## <a name="development-dependencies"></a>Entwicklungs Abhängigkeiten

Viele verschiedene Arten von Funktionen können als nuget-Pakete übermittelt werden, einschließlich Tools, die zur Optimierung des Entwicklungsprozesses verwendet werden. Diese Komponenten, während Sie für die Entwicklung eines neuen Pakets wichtig sein können, sollten beim späteren veröffentlichen nicht als Abhängigkeit des neuen Pakets angesehen werden. Mit nuget 2,8 kann ein Paket sich in der `.nuspec` Datei als developmentdependenz identifizieren. Bei der Installation werden diese Metadaten auch der `packages.config` Datei des Projekts hinzugefügt, in dem das Paket installiert wurde. Wenn diese `packages.config` Datei später für nuget-Abhängigkeiten analysiert wird `nuget.exe pack` , werden diese Abhängigkeiten ausgeschlossen, die als Entwicklungs Abhängigkeiten gekennzeichnet sind.

## <a name="individual-packagesconfig-files-for-different-platforms"></a>Einzelne packages.config Dateien für verschiedene Plattformen

Beim Entwickeln von Anwendungen für mehrere Zielplattformen ist es üblich, dass für jede der jeweiligen Buildumgebungen verschiedene Projektdateien vorhanden sind. Es ist auch üblich, dass unterschiedliche nuget-Pakete in verschiedenen Projektdateien verwendet werden, da Pakete unterschiedliche Ebenen der Unterstützung für verschiedene Plattformen aufweisen. Nuget 2,8 bietet eine verbesserte Unterstützung für dieses Szenario, indem verschiedene `packages.config` Dateien für verschiedene plattformspezifische Projektdateien erstellt werden.

![Mehrere package.config Dateien](./media/NuGet-2.8/multiple-packageconfigs.png)

## <a name="fallback-to-local-cache"></a>Fallback zum lokalen Cache

Obwohl nuget-Pakete in der Regel aus einem Remote Katalog wie [dem nuget](http://www.nuget.org/) -Katalog über eine Netzwerkverbindung genutzt werden, gibt es viele Szenarios, in denen der Client nicht verbunden ist. Ohne eine Netzwerkverbindung konnte der nuget-Client Pakete nicht erfolgreich installieren, auch wenn sich diese Pakete bereits auf dem Client Computer im lokalen nuget-Cache befanden. Nuget 2,8 fügt der Paket-Manager-Konsole einen automatischen Fall Back für den Cache hinzu. Wenn Sie z. b. die Verbindung zwischen dem Netzwerkadapter und der jQuery-Installation trennen, wird in der-Konsole Folgendes angezeigt:

    PM> Install-Package jquery
    The source at nuget.org [https://www.nuget.org/api/v2/] is unreachable. Falling back to NuGet Local Cache at C:\Users\me\AppData\Local\NuGet\Cache
    Installing 'jQuery 2.0.3'.
    Successfully installed 'jQuery 2.0.3'.
    Adding 'jQuery 2.0.3' to WebApplication18.
    Successfully added 'jQuery 2.0.3' to WebApplication18.

Das Cache Fall Back Feature erfordert keine bestimmten Befehlsargumente. Außerdem funktioniert der Cache Fall Back zurzeit nur in der Paket-Manager-Konsole. das Verhalten funktioniert derzeit nicht im Dialogfeld Paket-Manager.

## <a name="webmatrix-nuget-client-updates"></a>Webmatrix-nuget-Client Updates

Zusammen mit nuget 2,8 wurde auch die nuget-Erweiterung für webmatrix aktualisiert und enthält viele wichtige Features, die mit [nuget 2,5](../release-notes/nuget-2.5.md)geliefert wurden. Zu den neuen Funktionen zählen z. b. "Update all", "Minimum nuget Version" und das Überschreiben von Inhalts Dateien.

So aktualisieren Sie die nuget-Paket-Manager-Erweiterung in webmatrix 3:

1. Webmatrix 3 Öffnen
1. Klicken Sie im Menüband auf das Symbol Erweiterungen.
1. Registerkarte "Updates" auswählen
1. Klicken Sie, um den nuget-Paket-Manager zu 2.5.0
1. Schließen und Neustarten von webmatrix 3

Dies ist die erste Version der nuget-Paket-Manager-Erweiterung für webmatrix.  Der Code wurde vor kurzem von Microsoft im Open-Source-nuget-Projekt bereitgestellt. Zuvor wurde die nuget-Integration in webmatrix integriert und konnte nicht von webmatrix out of Band aktualisiert werden.  Wir haben nun die Möglichkeit, Sie neben den restlichen Client Tools von nuget zu aktualisieren.

## <a name="bug-fixes"></a>Fehlerkorrekturen

Eine der wichtigsten Fehlerbehebungen war die Leistungsverbesserung im Befehl Update-Package-REINSTALL.

Zusätzlich zu diesen Features und der erwähnten Leistungs Korrektur enthält diese Version von nuget auch viele andere Fehlerbehebungen. In der Version wurden 181 Gesamtprobleme behoben. Eine vollständige Liste der Arbeitselemente, die in nuget 2,8 korrigiert wurden, finden Sie in der [nuget-Problemverfolgung für diese Version](https://nuget.codeplex.com/workitem/list/advanced?release=NuGet%202.8&status=all).
