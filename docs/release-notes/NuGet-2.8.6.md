---
title: Anmerkungen zur Version von NuGet 2.8.6
description: Versionshinweise für NuGet 2.8.6 einschließlich bekannte Probleme, Fehlerbehebungen, Funktionen und Archivierung von dcrs Design.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: ee801a0edfe22888d65506cea557fd9c79dcf7bd
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
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