---
title: Anmerkungen zu dieser Version von nuget 2,0
description: Anmerkungen zu dieser Version von nuget 2,0 einschließlich bekannter Probleme, Fehlerbehebungen, hinzugefügter Features und dcrs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 01fdbfafcaea009cf119dfa880b2b16539c9b088
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/25/2019
ms.locfileid: "75383066"
---
# <a name="nuget-20-release-notes"></a>Anmerkungen zu dieser Version von nuget 2,0

Anmerkungen zu [nuget 1,8](../release-notes/nuget-1.8.md) | Anmerkungen zur [nuget](../release-notes/nuget-2.1.md) -Version 2,1

Nuget 2,0 wurde am 19. Juni 2012 veröffentlicht.

## <a name="known-installation-issue"></a>Bekanntes Installationsproblem
Wenn Sie Visual Studio 2010 SP1 ausführen, tritt möglicherweise ein Installationsfehler auf, wenn Sie versuchen, ein Upgrade für nuget auszuführen, wenn Sie eine ältere Version installiert haben.

Die Problem Umgehung besteht darin, dass Sie nuget einfach deinstallieren und anschließend aus dem vs-Erweiterungs Katalog installieren.  Weitere Informationen finden Sie unter <https://support.microsoft.com/kb/2581019>, oder wechseln [Sie direkt zum vs-Hotfix](http://bit.ly/vsixcertfix).

Hinweis: Wenn Visual Studio die Deinstallation der Erweiterung nicht zulässt (die Schaltfläche "deinstallieren" ist deaktiviert), müssen Sie Visual Studio wahrscheinlich mit "als Administrator ausführen" neu starten.

## <a name="package-restore-consent-is-now-active"></a>Die Zustimmung zur Paket Wiederherstellung ist nun aktiv.

Wie in diesem [Beitrag zur Zustimmung zur Paket Wiederherstellung](http://blog.nuget.org/20120518/package-restore-and-consent.html)beschrieben, erfordert nuget 2,0 nun, dass die Zustimmung erteilt wird, damit die Paket Wiederherstellung online geschaltet und Pakete heruntergeladen werden kann. Stellen Sie sicher, dass Sie die Zustimmung entweder über das Dialogfeld Paket-Manager-Konfiguration oder die Umgebungsvariable enablenugetpackagerestore angegeben haben.

## <a name="group-dependencies-by-target-frameworks"></a>Gruppieren von Abhängigkeiten nach Ziel Frameworks

Ab Version 2,0 können Paketabhängigkeiten basierend auf dem frameworkprofil des Ziel Projekts variieren. Dies wird mit einem aktualisierten `.nuspec` Schema erreicht. Das `<dependencies>`-Element kann jetzt einen Satz von `<group>` Elementen enthalten. Jede Gruppe enthält 0 (null) oder mehr `<dependency>` Elemente und ein `targetFramework` Attribut. Alle Abhängigkeiten innerhalb einer Gruppe werden miteinander installiert, wenn das Ziel Framework mit dem Ziel Projekt Framework-Profil kompatibel ist. Beispiel:

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

Beachten Sie, dass eine Gruppe **keine** Abhängigkeiten enthalten kann. Wenn das Paket in dem obigen Beispiel in einem Projekt installiert wird, das Silverlight 3,0 oder höher als Ziel verwendet, werden keine Abhängigkeiten installiert. Wenn das Paket in einem Projekt installiert wird, das auf .NET 4,0 oder höher ausgerichtet ist, werden zwei Abhängigkeiten, jQuery und webactivator, installiert.  Wenn das Paket in einem Projekt installiert wird, das eine frühe Version dieser 2 Frameworks oder eines beliebigen anderen Frameworks als Ziel hat, wird routemagic 1.1.0 installiert. Es gibt keine Vererbung zwischen Gruppen. Wenn das Ziel Framework eines Projekts mit dem `targetFramework`-Attribut einer Gruppe übereinstimmt, werden nur die Abhängigkeiten innerhalb dieser Gruppe installiert.

Ein Paket kann Paketabhängigkeiten in einem von zwei Formaten angeben: das alte Format einer flachen Liste mit `<dependency>` Elementen oder Gruppen. Wenn das `<group>`-Format verwendet wird, kann das Paket nicht in Versionen von nuget vor 2,0 installiert werden.

Beachten Sie, dass das Mischen der beiden Formate nicht zulässig ist. Der folgende Code Ausschnitt ist beispielsweise **ungültig** und wird von nuget abgelehnt.

```xml
<dependencies>
    <dependency id="jQuery" />
    <dependency id="WebActivator" />

    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>
</dependencies>
```

## <a name="grouping-content-files-and-powershell-scripts-by-target-framework"></a>Gruppieren von Inhalts Dateien und PowerShell-Skripts nach Ziel Framework

Zusätzlich zu Assemblyverweisen können Inhalts Dateien und PowerShell-Skripts auch nach Ziel Framework gruppiert werden. Die gleiche Ordnerstruktur, die im `lib` Ordner zum Angeben des Ziel-Frameworks gefunden wurde, kann jetzt auf die gleiche Weise auf die Ordner `content` und `tools` angewendet werden. Beispiel:

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

**Hinweis**: da `init.ps1` auf Projektmappenebene ausgeführt wird und nicht von einem einzelnen Projekt abhängt, muss Sie direkt unter dem Ordner `tools` platziert werden. Wenn Sie in einem frameworkspezifischen Ordner platziert wird, wird Sie ignoriert.

Außerdem ist ein neues Feature in nuget 2,0, dass ein frameworkordner *leer*sein kann. in diesem Fall werden von nuget keine Assemblyverweise hinzugefügt, Inhalts Dateien hinzugefügt oder PowerShell-Skripts für die jeweilige Frameworkversion ausgeführt. Im obigen Beispiel ist der Ordner `content\net40` leer.

## <a name="improved-tab-completion-performance"></a>Verbesserte Tab-Vervollständigungs Leistung
Die Funktion zum Vervollständigen der Registerkarte in der nuget-Paket-Manager-Konsole wurde aktualisiert, um die Leistung deutlich zu verbessern Der Zeitpunkt, zu dem die Tab-Taste gedrückt wird, wird so lange weniger verzögert, bis die Dropdown Liste für Vorschläge angezeigt wird.

## <a name="bug-fixes"></a>Fehlerkorrekturen
Nuget 2,0 umfasst viele Fehlerbehebungen mit dem Schwerpunkt auf Zustimmung und Leistung der Paket Wiederherstellung.
Eine vollständige Liste der Arbeitselemente, die in nuget 2,0 behoben wurden, finden Sie in der [nuget-Problemverfolgung für diese Version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.0&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).
