---
title: NuGet 2.0-Versionshinweise | Microsoft Docs
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Versionshinweise für NuGet 2.0 bekannte Probleme, Fehlerbehebungen, Funktionen und Archivierung von dcrs Design einschließlich."
keywords: "NuGet 2.0 Anmerkungen zu dieser Version, aufgrund von Fehlerbehebungen, bekannte Probleme, zusätzliche Funktionen, Archivierung von dcrs Design"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: eaa3c8db1cce72ff93671a1df63698748cdfab70
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-20-release-notes"></a>NuGet 2.0-Versionshinweise

[Anmerkungen zur Version des NuGet-1.8](../release-notes/nuget-1.8.md) | [NuGet 2.1-Versionshinweise](../release-notes/nuget-2.1.md)

NuGet 2.0 wurde 19 Juni 2012 veröffentlicht.

## <a name="known-installation-issue"></a>Bekannte Problem
Wenn Sie Visual Studio 2010 SP1 ausführen, kann ein Installationsfehler auftreten beim Upgrade von NuGet ausführen, wenn Sie eine ältere Version installiert haben.

Die problemumgehung besteht darin, einfach NuGet deinstallieren und installieren Sie es aus dem Katalog der VS-Erweiterung.  Finden Sie unter [http://support.microsoft.com/kb/2581019](http://support.microsoft.com/kb/2581019) für Weitere Informationen oder [fahren Sie direkt mit den VS-Hotfix](http://bit.ly/vsixcertfix).

Hinweis: Wenn Visual Studio lässt Sie beim Deinstallieren der Erweiterung (die Schaltfläche "Deinstallieren" deaktiviert ist), müssen Sie wahrscheinlich zum Neustart von Visual Studio, die mit "Als Administrator ausführen".

## <a name="package-restore-consent-is-now-active"></a>Paket Wiederherstellung Zustimmung ist jetzt aktiv

Wie dies unter [Beitrag im Blog Paket Wiederherstellung Zustimmung](http://blog.nuget.org/20120518/package-restore-and-consent.html), NuGet 2.0 erfordert nun, dass die Zustimmung erteilt werden, um paketwiederherstellung online zu gehen und Herunterladen von Paketen zu aktivieren. Stellen Sie sicher, dass Sie die Zustimmung über das Dialogfeld "Konfiguration" die Paket-Manager oder die Umgebungsvariable EnableNuGetPackageRestore eingegeben haben.

## <a name="group-dependencies-by-target-frameworks"></a>Abhängigkeiten von Aufgabengruppen von Zielframeworks

Ab Version 2.0, auf der Grundlage Paket Abhängigkeiten variieren können des Framework-Profils für das Zielprojekt. Dies erfolgt über ein aktualisiertes `.nuspec` Schema. Die `<dependencies>` Element kann jetzt enthalten eine Reihe von `<group>` Elemente. Jede Gruppe enthält 0 (null) oder mehr `<dependency>` Elemente und ein `targetFramework` Attribut. Alle Abhängigkeiten in einer Gruppe werden zusammen installiert, wenn das Zielframework mit dem Profil des Zielframeworks Projekt kompatibel ist. Zum Beispiel:

```xml
<dependencies>
    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>

    <group targetFramework="net40">
        <dependency id="jQuery" />
        <dependency id="WebActivator" />
    </group>

    <group targetFramework="sl30">
    </group>
</dependencies>
```

Beachten Sie, die eine Gruppe enthalten kann **0 (null)** Abhängigkeiten. Im obigen Beispiel ist das Paket installiert werden in ein Projekt, die auf Silverlight 3.0 oder höher, werden keine Abhängigkeiten installiert werden. Wenn das Paket ist in ein Projekt, die auf .NET 4.0 oder höher ausgeführt werden, werden zwei Abhängigkeiten, jQuery und WebActivator, installiert.  Wenn das Paket in einem Projekt, die auf eine frühere Version des diese 2 Frameworks oder andere Frameworks abzielen installiert wird, wird RouteMagic 1.1.0 installiert. Es gibt keine Vererbung zwischen Gruppen ein. Wenn das Zielframework des Projekts entspricht der `targetFramework` Attribut einer Gruppe, die nur die Abhängigkeiten in dieser Gruppe installiert werden soll.

Ein Paket kann in zwei Formaten paketabhängigkeiten angeben: das alte Format von einer flachen Liste von `<dependency>` Elemente oder Gruppen. Wenn die `<group>` Format verwendet wird, das Paket kann nicht in Versionen vor Version 2.0 von NuGet installiert werden.

Beachten Sie, dass das Mischen von den beiden Formaten nicht zulässig ist. Der folgende Codeausschnitt ist z. B. **ungültige** und werden durch NuGet abgelehnt.

```xml
<dependencies>
    <dependency id="jQuery" />
    <dependency id="WebActivator" />

    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>
</dependencies>
```

## <a name="grouping-content-files-and-powershell-scripts-by-target-framework"></a>Gruppieren von Inhaltsdateien und PowerShell-Skripts von Zielframework

Zusätzlich zu den Assemblyverweise können Inhaltsdateien und PowerShell-Skripts auch nach Zielframework gruppiert werden. Die gleiche Ordnerstruktur gefunden wird, der `lib` Ordner für die Angabe von Zielframework kann jetzt angewendet werden, auf die gleiche Weise auf die `content` und `tools` Ordner. Zum Beispiel:

    \content
        \net11
            \MyContent.txt
        \net20
            \MyContent20.txt
        \net40
        \sl40
            \MySilverlightContent.html

    \tools
        \init.ps1
        \net40
            \install.ps1
            \uninstall.ps1
        \sl40
            \install.ps1
            \uninstall.ps1

**Hinweis**: Da `init.ps1` auf Projektmappenebene ausgeführt wird und ist nicht auf einem einzelnen Projekt abhängige, muss sie verschoben werden direkt unter der `tools` Ordner. Wenn in einem frameworkspezifischen Ordner platziert werden, wird es ignoriert.

Darüber hinaus ein neues Feature in NuGet 2.0 hat es, dass einem frameworkordner *leere*, im letzteren Fall NuGet wird keine Assemblyverweise hinzufügen Inhaltsdateien oder Ausführen von PowerShell-Skripts für die bestimmten Framework-Version. In der oben gezeigten Beispiel wird der Ordner `content\net40` ist leer.

## <a name="improved-tab-completion-performance"></a>Verbesserte Registerkarte Abschluss Leistung
Das Feature zum Vervollständigen Registerkarte in der NuGet-Paket-Manager-Konsole wurde aktualisiert, um die Leistung erheblich verbessern. Es werden viel weniger Verzögerung ab dem Zeitpunkt, den die Tab-Taste gedrückt wird, bis die Vorschlag-Dropdownliste angezeigt wird.

## <a name="bug-fixes"></a>Fehlerkorrekturen
NuGet 2.0 enthält zahlreiche Programmfehlerbehebungen mit Schwerpunkt auf das Paket wiederherstellen Benutzeroberfläche zur administratorzustimmung und Leistung.
Eine vollständige Liste der Arbeit Artikel feste in NuGet 2.0 Bitte Ansicht der [NuGet Issue Tracker für diese Version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).
