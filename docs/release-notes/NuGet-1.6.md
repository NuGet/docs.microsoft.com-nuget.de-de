---
title: Anmerkungen zu dieser Version von nuget 1,6
description: Anmerkungen zu dieser Version von nuget 1,6 einschließlich bekannter Probleme, Fehlerbehebungen, hinzugefügter Features und dcrs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 08b1cb3736e645d6efcc33f920f521c9c0fc7507
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98777014"
---
 # <a name="nuget-16-release-notes"></a>Anmerkungen zu dieser Version von nuget 1,6

Anmerkungen zu dieser [Version von nuget 1,5](../release-notes/nuget-1.5.md)  |  [Anmerkungen zu dieser Version von nuget 1,7](../release-notes/nuget-1.7.md)

Nuget 1,6 wurde am 13. Dezember 2011 veröffentlicht.

## <a name="known-installation-issue"></a>Bekanntes Installationsproblem
Wenn Sie Visual Studio 2010 SP1 ausführen, tritt möglicherweise ein Installationsfehler auf, wenn Sie versuchen, ein Upgrade für nuget auszuführen, wenn Sie eine ältere Version installiert haben.

Die Problem Umgehung besteht darin, dass Sie nuget einfach deinstallieren und anschließend aus dem vs-Erweiterungs Katalog installieren.  Weitere Informationen finden Sie unter <https://support.microsoft.com/kb/2581019>.

Hinweis: Wenn Visual Studio die Deinstallation der Erweiterung nicht zulässt (die Schaltfläche "deinstallieren" ist deaktiviert), müssen Sie Visual Studio wahrscheinlich mit "als Administrator ausführen" neu starten.

## <a name="features"></a>Features

### <a name="support-for-semantic-versioning-and-prerelease-packages"></a>Unterstützung für semantische Versionierung und vorab Versionen von Paketen
Mit nuget 1,6 wird die Unterstützung für die semantische Versionierung (semver) eingeführt. Weitere Informationen zur Verwendung von semver finden Sie in der [Dokumentation zur Versions](../create-packages/prerelease-packages.md)Verwaltung.

### <a name="using-nuget-without-checking-in-packages-package-restore"></a>Verwenden von nuget ohne Einchecken von Paketen (Paket Wiederherstellung)
Nuget 1,6 bietet jetzt erstklassige Unterstützung für den Workflow, in dem nuget-Pakete nicht zur Quell Code Verwaltung hinzugefügt werden, sondern zur Buildzeit wieder hergestellt werden, wenn Sie nicht vorhanden sind. Weitere Informationen finden Sie im Thema [Verwenden von nuget ohne Commit für Pakete in die Quell](../consume-packages/packages-and-source-control.md) Code Verwaltung.

### <a name="item-templates-that-install-nuget-packages"></a>Element Vorlagen zum Installieren von nuget-Paketen
Wenn Sie auf der Arbeit arbeiten, um das vorinstallierte nuget-Paket in Visual Studio-Projektvorlagen zu unterstützen, fügt nuget 1,6 auch Unterstützung für Visual Studio-Element Vorlagen hinzu Element Vorlagen können zugehörige nuget-Pakete aufweisen, die beim Aufrufen der Vorlage installiert werden.

Weitere Informationen zum Ändern einer Projekt-/Elementvorlage zum Installieren von nuget-Paketen finden Sie im Thema [Pakete in Visual Studio-Vorlagen](../visual-studio-extensibility/visual-studio-templates.md) .

### <a name="support-for-disabling-package-sources"></a>Unterstützung für das Deaktivieren von Paketquellen
Wenn mehrere Paketquellen konfiguriert sind, sucht nuget bei der Installation eines Pakets und dessen Abhängigkeiten jeweils nach Paketen. Eine Paketquelle, die aus irgendeinem Grund herunter ist, kann nuget erheblich verlangsamen.

Vor dem nuget-1,6 konnten Sie die Paketquelle entfernen, aber dann müssen Sie sich die Details merken, wenn Sie Sie wieder hinzufügen möchten.

Mit nuget 1,6 können Sie eine Paketquelle deaktivieren, um Sie zu deaktivieren.

![Deaktivieren eines Pakets](./media/package-source-with-disabled-source.png)

## <a name="bug-fixes"></a>Fehlerkorrekturen
Für nuget 1,6 wurden insgesamt 106 Arbeitselemente korrigiert. 95 von diesen wurden als Fehler klassifiziert, und 10 dieser Features waren.

Eine vollständige Liste der Arbeitselemente, die in nuget 1,6 behoben wurden, finden Sie in der [nuget-Problemverfolgung für diese Version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%201.6&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0).
