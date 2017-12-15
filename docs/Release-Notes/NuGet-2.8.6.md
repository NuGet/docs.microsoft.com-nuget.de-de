---
title: Anmerkungen zur Version des NuGet-2.8.6 | Microsoft Docs
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 920c551c-18a7-40f4-a32b-ce84de6ea766
description: "Versionshinweise für NuGet 2.8.6 einschließlich bekannte Probleme, Fehlerbehebungen, Funktionen und Archivierung von dcrs Design."
keywords: "NuGet-2.8.6 versionsanmerkungen aufgrund von Fehlerbehebungen, bekannte Probleme, zusätzliche Funktionen, Archivierung von dcrs Design"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: f33c1edd3ef703a8cd97b7bdd97c37e12426aafa
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/14/2017
---
# <a name="nuget-286-release-notes"></a>Anmerkungen zur Version von NuGet 2.8.6

[Anmerkungen zur Version des NuGet-2.8.5](../release-notes/nuget-2.8.5.md) | [NuGet 2.8.7-Versionshinweise](../release-notes/nuget-2.8.7.md)

NuGet 2.8.6 freigegeben wurde dem 20. Juli 2015 als ein kleineres Update, um unsere 2.8.5 VSIX mit einigen ausgerichtet, Korrekturen und Verbesserungen für Pakete, die übermittelt werden, möglicherweise mit Unterstützung für Windows 10-UWP-Entwicklungsmodell zu unterstützen.

Diese Version des NuGet-Paket-Manager-Erweiterung bietet nur Unterstützung für Visual Studio 2013.

In dieser Version musste das Dialogfeld "NuGet-Paket-Manager" Unterstützung für:

* Zur Unterstützung von Windows 10-Anwendungsentwicklung UAP Zielframeworkmoniker, eingeführt.
* NuGet-Version 3-protokollendpunkte
* Unterstützung für ["NuGet.config"](../consume-packages/configuring-nuget-behavior.md) ProtocolVersion Attribut Repository Quellen. Standardwert ist "2"
* Fallback auf remote-Repository, wenn eine erforderliches Paket-Version nicht verfügbar, im lokalen Cache ist