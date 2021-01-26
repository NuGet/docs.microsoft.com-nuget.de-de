---
title: Nuget 2.8.6 Anmerkungen zu dieser Version
description: Anmerkungen zu dieser Version von nuget 2.8.6 einschließlich bekannter Probleme, Fehlerbehebungen, hinzugefügter Features und dcrs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: ea291bdf7a5b6cc3ac3bde526030e517db4632d7
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776701"
---
# <a name="nuget-286-release-notes"></a>Nuget 2.8.6 Anmerkungen zu dieser Version

[Nuget 2.8.5 Anmerkungen](../release-notes/nuget-2.8.5.md)  |  zu dieser Version [Nuget 2.8.7 Anmerkungen](../release-notes/nuget-2.8.7.md) zu dieser Version

Nuget 2.8.6 wurde am 20. Juli 2015 als ein kleineres Update für unsere 2.8.5 VSIX veröffentlicht, mit einigen gezielten Korrekturen und Verbesserungen für die Unterstützung von Paketen, die Unterstützung für das Windows 10 UWP-Entwicklungsmodell bereitgestellt werden können.

Diese Version der nuget-Paket-Manager-Erweiterung bietet nur Unterstützung für Visual Studio 2013.

In dieser Version wurde dem Dialogfeld "nuget-Paket-Manager" Unterstützung für hinzugefügt:

* In wurde der UAP-zielframeworkmoniker zur Unterstützung der Windows 10-Anwendungsentwicklung eingeführt.
* Nuget-Protokoll, Version 3, Endpunkte
* Unterstützung für [Nuget.Config](../consume-packages/configuring-nuget-behavior.md) ProtocolVersion-Attribut in Repository-Quellen. Der Standardwert ist "2".
* Fallback auf Remoterepository, wenn eine erforderliche Paketversion im lokalen Cache nicht verfügbar ist