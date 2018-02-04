---
title: Anmerkungen zur Version des NuGet-3.4.3 | Microsoft Docs
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Versionshinweise für NuGet 3.4.3 einschließlich bekannte Probleme, Fehlerbehebungen, Funktionen und Archivierung von dcrs Design."
keywords: "NuGet-3.4.3 Anmerkungen zu dieser Version, aufgrund von Fehlerbehebungen, bekannte Probleme, zusätzliche Funktionen, Archivierung von dcrs Design"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 68aab607659d15f96aefeab7bb90afc787710824
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/02/2018
---
# <a name="nuget-343-release-notes"></a>Anmerkungen zur Version von NuGet 3.4.3

[Anmerkungen zur Version des NuGet-3.4.2](../release-notes/nuget-3.4.2.md) | [NuGet 3.4.4-Versionshinweise](../release-notes/nuget-3.4.4.md)

NuGet 3.4.3 wurde freigegeben, 22 April 2016 verschiedene Probleme, die in den Versionen 3.4 und nachfolgende identifiziert wurden.

Sie können sowohl VSIX-als auch nuget.exe herunterladen [hier](https://dist.nuget.org/index.html).

## <a name="updates-and-improvements"></a>Updates und Verbesserungen

* Verbesserter Zuverlässigkeit für Visual Studio. Wir haben einige Probleme im NuGet behoben, die in Visual Studio abstürzen verursacht hat.

## <a name="fixes"></a>Fehlerbehebungen

* Einige Probleme der Autorisierung behoben mit Nuget, private kennwortgeschützt Feeds.
* Es wurde ein Problem, um nicht auf PCL aus wiederherstellen `project.json` mit Laufzeiten angegeben.
* Einige Kunden ausgeführt wurden in sind zwischenzeitliche Fehler die, wenn Sie Pakete installieren. Dies wurde jetzt in dieser Version behoben.
* Es wurde ein Problem, die in C + Wiederherstellung Fehler verursacht hat c++ / CLI-Projekten mit `project.json`.
* Einige Pakete (z. B. ModernHttpClient), in denen nicht ordnungsgemäß entzippt Wenn Sie Nuget in Mono verwenden. Dies wurde jetzt in dieser Version behoben.

Die vollständige Liste der Korrekturen und Verbesserungen in dieser Version, sehen Sie sich die Liste der Probleme [hier](https://github.com/NuGet/Home/issues?q=is%3Aissue+milestone%3A3.4.3+is%3Aclosed).