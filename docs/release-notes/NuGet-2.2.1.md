---
title: Anmerkungen zu NuGet 2.2.1
description: Anmerkungen zu dieser Version für die Einbindung von NuGet 2.2.1 bekannte Probleme, Fehlerkorrekturen, hinzugefügter Features und DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: abbd3a9d9c51132477ceb236fed22cb63ccda209
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550697"
---
# <a name="nuget-221-release-notes"></a>Anmerkungen zu NuGet 2.2.1

[Anmerkungen zu NuGet 2.2](../release-notes/nuget-2.2.md) | [Anmerkungen zu NuGet 2.5](../release-notes/nuget-2.5.md)

NuGet 2.2.1 wurde am 15. Februar 2013 veröffentlicht.  Die Versionsnummer des VS-Erweiterung ist 2.2.40116.9051.

## <a name="localization-refresh"></a>Lokalisierung aktualisieren
Wenn NuGet als Teil von Visual Studio 2012 zur Verfügung gestellt, wurde es vollständig in Englisch + 13 andere Sprachen lokalisiert.  Seit damals NuGet 2.1 und 2.2 wurden ausgeliefert, aber die Lokalisierung hatte nicht aktualisiert wurde.  Die Version von NuGet 2.2.1 aktualisiert Ihre Lokalisierung.

Die NuGet-Benutzeroberfläche und PowerShell-Konsole werden in den folgenden Sprachen lokalisiert:

1. Chinesisch (vereinfacht)
1. Chinesisch (traditionell)
1. Tschechisch
1. Englisch
1. Französisch
1. Deutsch
1. Italienisch
1. Japanisch
1. Koreanisch
1. Polnisch
1. Portugiesisch (Brasilien)
1. Russisch
1. Spanisch
1. Türkisch

## <a name="visual-studio-templates-support-multiple-preinstalled-package-repositories"></a>Visual Studio-Vorlagen unterstützen mehrere vorinstallierten Package-Repositorys
Wenn Sie Visual Studio-Vorlagen erstellt werden, können Sie NuGet, um [Vorinstallieren Pakete](../visual-studio-extensibility/visual-studio-templates.md) als Teil der Vorlage.  Bis jetzt dieses Feature wurde eine Einschränkung, dass alle Pakete benötigt aus derselben Quelle stammen.  Mit NuGet 2.2.1 können Sie jedoch Pakete, die von mehreren Repositorys (innerhalb der Vorlage, einer VSIX-Datei oder einen Ordner auf dem Datenträger, die in der Registrierung definiert) installiert haben.

Das Hauptszenario für dieses Feature ist die benutzerdefinierte Projektvorlagen für ASP.NET.  Die integrierten Vorlagen von ASP.NET verwenden die vorinstallierten Pakete, die Pakete vom lokalen Datenträger abgerufen.  Sie können jetzt erstellen eine benutzerdefinierte ASP.NET-Projektvorlage, die die vorhandenen Pakete installiert, die von ASP.NET verwendet aber zusätzliche NuGet-Pakete in der Vorlage hinzufügen.

## <a name="bug-fixes"></a>Fehlerkorrekturen
NuGet 2.2.1 enthält einige gezielte Fehlerbehebungen. Eine Liste der Arbeit Elemente eine feste NuGet 2.2.1, bitte Ansicht der [NuGet Issue Tracker für diese Version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).


## <a name="known-issues"></a>Bekannte Probleme

Wenn Sie ASP.NET-Projektvorlagen erweitern, müssen alle vorinstallierten paketrepositorys verwenden den gleichen Wert für die `isPreunzipped` Attribut.
