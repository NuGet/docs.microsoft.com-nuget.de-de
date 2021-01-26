---
title: Anmerkungen zu dieser Version von nuget 2.2.1
description: Anmerkungen zu dieser Version von nuget 2.2.1 einschließlich bekannter Probleme, Fehlerbehebungen, hinzugefügter Features und dcrs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: b6058fd596e32d38042aa75027640a5e5baca472
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776810"
---
# <a name="nuget-221-release-notes"></a>Anmerkungen zu dieser Version von nuget 2.2.1

Anmerkungen zu dieser [Version von nuget 2,2](../release-notes/nuget-2.2.md)  |  [Anmerkungen zu dieser Version von nuget 2,5](../release-notes/nuget-2.5.md)

Nuget 2.2.1 wurde am 15. Februar 2013 veröffentlicht.  Die Versionsnummer der vs-Erweiterung ist 2.2.40116.9051.

## <a name="localization-refresh"></a>Lokalisierungs Aktualisierung
Wenn nuget als Teil von Visual Studio 2012 ausgeliefert wurde, war es vollständig in Englisch und 13 anderen Sprachen lokalisiert.  Seitdem haben nuget 2,1 und 2,2 ausgeliefert, aber die Lokalisierung wurde nicht aktualisiert.  Die nuget 2.2.1-Version aktualisiert unsere Lokalisierung.

Die nuget-Benutzeroberfläche und die PowerShell-Konsole sind in den folgenden Sprachen lokalisiert:

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

## <a name="visual-studio-templates-support-multiple-preinstalled-package-repositories"></a>Visual Studio-Vorlagen unterstützen mehrere vorinstallierte paketrepositorys
Wenn Sie Visual Studio-Vorlagen erstellen, können Sie nuget verwenden, um Pakete als Teil der Vorlage [vorzuinstallieren](../visual-studio-extensibility/visual-studio-templates.md) .  Bisher hatte dieses Feature eine Einschränkung, dass alle Pakete aus derselben Quelle stammen mussten.  Mit nuget 2.2.1 können Pakete jedoch aus mehreren Depots (innerhalb der Vorlage, einer VSIX oder einem Ordner auf dem Datenträger, der in der Registrierung definiert ist) installiert werden.

Das Hauptszenario für dieses Feature sind benutzerdefinierte ASP.net-Projektvorlagen.  Die integrierten ASP.net-Vorlagen verwenden vorinstallierte Pakete und ziehen Pakete vom lokalen Datenträger.  Sie können jetzt eine benutzerdefinierte ASP.net-Projektvorlage erstellen, die die vorhandenen Pakete verwendet, die von ASP.NET installiert werden, aber zusätzliche nuget-Pakete zu Ihrer Vorlage hinzufügen.

## <a name="bug-fixes"></a>Fehlerkorrekturen
Nuget 2.2.1 umfasst einige gezielte Fehlerbehebungen. Eine Liste der Arbeitselemente, die in nuget 2.2.1 behoben wurden, finden Sie in der [nuget-Problemverfolgung für diese Version](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=Closed&type=All&priority=All&release=NuGet%202.2.1&assignedTo=All&component=All&sortField=LastUpdatedDate&sortDirection=Descending&page=0).


## <a name="known-issues"></a>Bekannte Probleme

Wenn Sie ASP.net-Projektvorlagen erweitern, müssen alle vorinstallierten paketrepositorys den gleichen Wert für das `isPreunzipped` Attribut verwenden.
