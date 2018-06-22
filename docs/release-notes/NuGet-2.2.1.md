---
title: Anmerkungen zur Version von NuGet 2.2.1
description: Versionshinweise für NuGet 2.2.1 einschließlich bekannte Probleme, Fehlerbehebungen, Funktionen und Archivierung von dcrs Design.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: fddeb4e8c9fb2d85ba1876360862461e8ef025af
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
ms.locfileid: "31819292"
---
# <a name="nuget-221-release-notes"></a>Anmerkungen zur Version von NuGet 2.2.1

[NuGet-2.2-Versionshinweise](../release-notes/nuget-2.2.md) | [NuGet 2.5-Versionshinweise](../release-notes/nuget-2.5.md)

NuGet 2.2.1 wurde am 15. Februar 2013 veröffentlicht.  Die Versionsnummer des VS-Erweiterung ist 2.2.40116.9051.

## <a name="localization-refresh"></a>Lokalisierung aktualisieren
Bei der NuGet als Teil von Visual Studio 2012 zur Verfügung gestellt, wurde es vollständig in Englisch + 13 andere Sprachen lokalisiert.  Inzwischen NuGet 2.1 und 2.2 geliefert wurden, aber die Lokalisierung wurde nicht aktualisiert.  Die Version des NuGet-2.2.1 aktualisiert unsere Lokalisierung.

NuGet Benutzeroberfläche und PowerShell-Konsole werden in den folgenden Sprachen lokalisiert:

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

## <a name="visual-studio-templates-support-multiple-preinstalled-package-repositories"></a>Visual Studio-Vorlagen unterstützen mehrere vorinstallierten Paket-Repositorys
Wenn Sie Visual Studio-Vorlagen erzeugen, können Sie NuGet [Vorinstallieren Pakete](../visual-studio-extensibility/visual-studio-templates.md) als Teil der Vorlage.  Bis jetzt wurde dieses Feature eine Einschränkung, dass alle Pakete benötigt, die von der gleichen Quelle stammen.  Mit NuGet 2.2.1 können Sie jedoch Pakete, die aus mehreren Repositorys (innerhalb der Vorlage, einer VSIX oder einen Ordner auf dem Datenträger, die in der Registrierung definiert) installiert haben.

Das Hauptszenario für dieses Feature ist benutzerdefinierte Projektvorlagen für ASP.NET.  Die integrierte Vorlagen für ASP.NET verwenden vorinstallierten Pakete, die Pakete vom lokalen Datenträger abrufen.  Sie können jetzt erstellen eine benutzerdefinierte ASP.NET-Projektvorlage, die die vorhandenen Pakete installiert, die von ASP.NET verwendet jedoch zusätzliche NuGet-Pakete in der Vorlage hinzufügen.

## <a name="bug-fixes"></a>Fehlerkorrekturen
NuGet 2.2.1 enthält einige targeted Fehlerbehebungen. Eine Liste der Arbeit Artikel feste in NuGet 2.2.1, bitte Ansicht der [NuGet Issue Tracker für diese Version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).


## <a name="known-issues"></a>Bekannte Probleme

Wenn Sie ASP.NET Projektvorlagen erweitern, müssen alle vorinstallierten Paket Repositorys verwenden den gleichen Wert für die `isPreunzipped` Attribut.
