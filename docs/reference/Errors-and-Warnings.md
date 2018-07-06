---
title: NuGet-Fehler und Warnungen-Referenz
description: Vollständige Referenz für Warnungen und Fehler, die aus NuGet während der verschiedenen NuGet-Vorgänge ausgegeben.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 25c8a22fc0bce2372c54cf29b904a8d9fbbe9ace
ms.sourcegitcommit: 8e3546ab630a24cde8725610b6a68f8eb87afa47
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/05/2018
ms.locfileid: "37843429"
---
# <a name="errors-and-warnings"></a>Fehler und Warnungen

In NuGet 4.3.0 Fehler und Warnungen sind nummeriert, wie in diesem Thema beschrieben und enthalten ausführliche Informationen zum Beheben der Probleme im Zusammenhang mit beitragen.

Die Fehler und Warnungen, die hier aufgeführten stehen nur mit [PackageReference-basierte](../consume-packages/package-references-in-project-files.md) Projekte und NuGet 4.3.0. NuGet berücksichtigt auch MSBuild-Eigenschaften, um Warnungen unterdrücken oder diese zu Fehlern heraufstufen. Weitere Informationen finden Sie unter [wie: Unterdrücken von Compilerwarnungen](/visualstudio/ide/how-to-suppress-compiler-warnings) in Visual Studio-Dokumentation.

**Fehler**

| Gruppieren | Fehlernummern |
| --- | --- |
| Ungültige Eingabefehler | [NU1001](./errors-and-warnings/NU1001.md), [NU1002](./errors-and-warnings/NU1002.md), [NU1003](./errors-and-warnings/NU1003.md) |
| Fehler aufgrund fehlender Paket- und | [NU1100](./errors-and-warnings/NU1100.md), [NU1101](./errors-and-warnings/NU1101.md), [NU1102](./errors-and-warnings/NU1102.md), [NU1103](./errors-and-warnings/NU1103.md), [NU1104](./errors-and-warnings/NU1104.md), [NU1105](./errors-and-warnings/NU1105.md), [NU1106](./errors-and-warnings/NU1106.md), [NU1107](./errors-and-warnings/NU1107.md) (previously NU1607), [NU1108](./errors-and-warnings/NU1108.md) (previously NU1606) |
| Kompatibilitätsfehler | [NU1201](./errors-and-warnings/NU1201.md), [NU1202](./errors-and-warnings/NU1202.md), [NU1203](./errors-and-warnings/NU1203.md), [NU1401](./errors-and-warnings/NU1401.md) |
| Interner Fehler von NuGet | [NU1000](./errors-and-warnings/NU1000.md) |
| Signierte Pakete-Fehler (Erstellung und Überprüfung) | [NU3000](./errors-and-warnings/NU3000.md), [NU3001](./errors-and-warnings/NU3001.md), [NU3004](./errors-and-warnings/NU3004.md), [NU3008](./errors-and-warnings/NU3008.md) |

**Warnungen**

| Gruppieren | Warnungsnummern |
| --- | --- |
| Ungültige Eingabe-Warnungen | [NU1501](./errors-and-warnings/NU1501.md), [NU1502](./errors-and-warnings/NU1502.md), [NU1503](./errors-and-warnings/NU1503.md) |
| Unerwarteter Paket Version Warnungen | [NU1601](./errors-and-warnings/NU1601.md), [NU1602](./errors-and-warnings/NU1602.md), [NU1603](./errors-and-warnings/NU1603.md), [NU1604](./errors-and-warnings/NU1604.md), [NU1605](./errors-and-warnings/NU1605.md) |
| Warnungen der Resolver-Konflikt | [NU1608](./errors-and-warnings/NU1608.md) |
| Paket-fallback-Warnungen | [NU1701](./errors-and-warnings/NU1701.md) |
| Feed-Warnungen | [NU1801](./errors-and-warnings/NU1801.md) |
| Interne NuGet-Warnungen | [NU1500](./errors-and-warnings/NU1500.md) |
| Signierte Pakete Warnungen (Erstellung und Überprüfung) | [NU3002](./errors-and-warnings/NU3002.md), [NU3018](./errors-and-warnings/NU3018.md), [NU3028](./errors-and-warnings/NU3028.md) |
