---
title: Anmerkungen zu NuGet-Version 2.0
description: Anmerkungen zu NuGet 2.0, einschließlich der bekannten Probleme, Fehlerkorrekturen, hinzugefügter Features und DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: f32eea9260ce7e307ff56b7f3e6b48c6d98e6c90
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43547574"
---
# <a name="nuget-20-release-notes"></a>Anmerkungen zu NuGet-Version 2.0

[Anmerkungen zu NuGet 1.8](../release-notes/nuget-1.8.md) | [Anmerkungen zu NuGet 2.1](../release-notes/nuget-2.1.md)

NuGet 2.0 wurde am 19. Juni 2012 veröffentlicht.

## <a name="known-installation-issue"></a>Problem für bekannte Installationsprobleme
Wenn Sie Visual Studio 2010 SP1 ausführen, können Sie ein Installationsfehler auftreten, beim Versuch, NuGet aktualisieren, wenn Sie eine ältere Version installiert haben.

Die problemumgehung besteht darin, einfach NuGet zuerst deinstallieren und installieren Sie es aus dem Katalog der VS-Erweiterung.  Finden Sie unter [ http://support.microsoft.com/kb/2581019 ](http://support.microsoft.com/kb/2581019) Informationen oder [gehen Sie direkt auf den VS-Hotfix](http://bit.ly/vsixcertfix).

Hinweis: Wenn Visual Studio ist es nicht zulässig, die die Erweiterung deinstallieren (die Schaltfläche "Deinstallieren" deaktiviert ist), müssen Sie wahrscheinlich zum Neustart von Visual Studio mithilfe von "Ausführen als Administrator."

## <a name="package-restore-consent-is-now-active"></a>Paket wiederherstellen Zustimmung ist jetzt aktiv

Gemäß diesem [Beitrag im Paket wiederherstellen Zustimmung](http://blog.nuget.org/20120518/package-restore-and-consent.html), NuGet 2.0 jetzt erfordert, dass die Genehmigung zum Aktivieren der paketwiederherstellung online zu gehen und Herunterladen von Paketen erteilt werden. Stellen Sie sicher, dass Sie die Zustimmung über das Konfigurationsdialogfeld des Paket-Manager oder die Umgebungsvariable EnableNuGetPackageRestore angegeben haben.

## <a name="group-dependencies-by-target-frameworks"></a>Abhängigkeiten von Zielframeworks

Ab Version 2.0, auf der Grundlage Paket variieren können Abhängigkeiten des frameworkprofils des Zielprojekts. Dies erfolgt mithilfe eines aktualisierten `.nuspec` Schema. Die `<dependencies>` Element kann jetzt enthalten eine Reihe von `<group>` Elemente. Jede Gruppe enthält 0 (null) oder mehr `<dependency>` Elemente und ein `targetFramework` Attribut. Alle Abhängigkeiten in einer Gruppe werden zusammen installiert, wenn das Zielframework mit das Zielframeworkprofil im Projekt kompatibel ist. Zum Beispiel:

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

Beachten Sie, die eine Gruppe enthalten, können **0 (null)** Abhängigkeiten. Im obigen Beispiel wenn das Paket ist in einem Projekt, Silverlight 3.0 oder höher installiert, werden keine Abhängigkeiten installiert. Wenn das Paket ist in einem Projekt, .NET 4.0 oder höher ausgeführt werden, werden zwei Abhängigkeiten, jQuery und WebActivator, installiert werden.  Wenn das Paket in einem Projekt, die auf eine frühe Version dieser 2 Frameworks oder ein anderes Framework abzielt installiert wird, wird die RouteMagic 1.1.0 installiert werden. Es gibt keine Vererbung zwischen Gruppen ein. Wenn das Zielframework des Projekts entspricht der `targetFramework` Attributs einer Gruppe, die nur die Abhängigkeiten in dieser Gruppe installiert werden.

Ein Paket kann paketabhängigkeiten in einem der zwei Formate angeben: das alte Format von einer flachen Liste von `<dependency>` Elemente oder Gruppen. Wenn die `<group>` Format wird verwendet, das Paket kann nicht in Versionen vor Version 2.0 von NuGet installiert werden.

Beachten Sie, dass das Kombinieren von den beiden Formaten nicht zulässig ist. Der folgende Codeausschnitt ist z. B. **ungültige** und werden von NuGet abgelehnt.

```xml
<dependencies>
    <dependency id="jQuery" />
    <dependency id="WebActivator" />

    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>
</dependencies>
```

## <a name="grouping-content-files-and-powershell-scripts-by-target-framework"></a>Gruppieren von Inhaltsdateien und PowerShell-Skripts nach Zielframework

Neben der Assemblyverweise können Inhaltsdateien und PowerShell-Skripts auch nach Zielframework gruppiert werden. Die gleiche Ordnerstruktur finden Sie in der `lib` Ordner zum Angeben von Zielframeworks kann jetzt auf die gleiche Weise zu angewendet werden die `content` und `tools` Ordner. Zum Beispiel:

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

**Beachten Sie**: Da `init.ps1` auf Projektmappenebene ausgeführt wird und ist nicht in einem einzelnen Projekt abhängig, es muss platziert werden direkt unter der `tools` Ordner. Wenn in einem Framework-spezifischen Ordner platzieren, wird es ignoriert.

Ein neues Feature in NuGet 2.0 ist außerdem ein frameworkordner möglich *leere*, in diesem Fall NuGet wird nicht Assemblyverweise hinzufügen, Inhaltsdateien, oder führen Sie PowerShell-Skripts für die bestimmte Framework-Version. Im obigen Beispiel ist der Ordner `content\net40` ist leer.

## <a name="improved-tab-completion-performance"></a>Verbesserte Registerkarte-Abschluss-Leistung
Das Feature in der NuGet-Paket-Manager-Konsole wurde aktualisiert, um die Leistung erheblich verbessern. Es fallen weniger Verzögerung, die die Tab-Taste gedrückt wird, bis die Vorschlags-Dropdownliste angezeigt wird.

## <a name="bug-fixes"></a>Fehlerkorrekturen
NuGet 2.0 enthält zahlreiche Programmfehlerbehebungen mit Schwerpunkt auf das Paket wiederherstellen Zustimmung und Leistung.
Eine vollständige Liste der Arbeit Elemente eine feste in NuGet 2.0 Bitte Ansicht der [NuGet Issue Tracker für diese Version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).
