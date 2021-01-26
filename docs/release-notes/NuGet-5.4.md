---
title: Anmerkungen zu dieser Version von nuget 5,4
description: Anmerkungen zu dieser Version von nuget 5,4, einschließlich neuer Features, Fehlerbehebungen und dcrs.
author: JonDouglas
ms.author: jodou
ms.date: 09/06/2019
ms.topic: conceptual
ms.openlocfilehash: dd4c10672db3a65b68f18636105ee55ab09da7ef
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98776189"
---
# <a name="nuget-54-release-notes"></a>Anmerkungen zu dieser Version von nuget 5,4

Möglichkeiten der NuGet-Verteilung:

| NuGet-Version | Verfügbar in der Visual Studio-Version| Verfügbar in .NET SDK(s)|
|:---|:---|:---|
| [**5.4.0**](https://nuget.org/downloads) | [Visual Studio 2019, Version 16,4](https://visualstudio.microsoft.com/downloads/) | [3.1.100](https://dotnet.microsoft.com/download/dotnet-core/3.1)<sup>1</sup> |

<sup>1</sup> Installiert mit Visual Studio 2019 mit .net Core-Arbeitsauslastung

## <a name="summary-whats-new-in-54"></a>Zusammenfassung: Neues in 5,4

* Schnellere Ladezeit für Projektmappen: der Aufwand für die Ausführung von nuget-Code beim ersten Laden der Projekt Mappe wurde über partielle ngen reduziert, um JIT-Kosten [#6007](https://github.com/NuGet/Home/issues/6007)

* Neue Hilfsfunktion: Wenn Sie eine Liste von Paket-IDs und-Versionen erhalten, erhalten Sie die wahrscheinlichsten Pakete auf oberster Ebene. - [#8316](https://github.com/NuGet/Home/issues/8316)

* Neue [`nuget/setup-nuget`](https://github.com/marketplace/actions/setup-nuget-exe-for-use-with-actions) Aktion zum Installieren und Konfigurieren von NuGet.exe auf [GitHub-Aktionen](https://github.com/features/actions). - [#8818](https://github.com/NuGet/Home/issues/8818)

### <a name="issues-fixed-in-this-release"></a>In diesem Release behobene Probleme

**Fehler**

* Plug-in: Zeit Genauigkeit der Protokollierung auf Linux/Mac- [#8747](https://github.com/NuGet/Home/issues/8747)

* Das Verwerfen eines Plug-ins kann manchmal den gesamten Vorgang auslösen und einen Fehler verursachen. - [#8732](https://github.com/NuGet/Home/issues/8732)

* Anzeigen von Versions Duplikaten in der Liste der zulässigen und blockierten Versionen in PMUI- [#8679](https://github.com/NuGet/Home/issues/8679)

* Die Sperrdatei wurde nicht ordnungsgemäß generiert. die frameworkreihen Folge sollte die Wiederherstellung mit lockedmode- [#8645](https://github.com/NuGet/Home/issues/8645) nicht beeinträchtigen.

* Fehler bei der lockfile-Überprüfung für Projekte mit <RuntimeIdentifiers> Set in SDK 3.0.100- [#8639](https://github.com/NuGet/Home/issues/8639)

* Bei der Signatur Überprüfung werden Signaturen mit Zeitstempeln ordnungsgemäß abgelehnt, die zwei Werte unter derselben OID aufweisen [#8629](https://github.com/NuGet/Home/issues/8629)

* Aktualisieren der Lizenz Liste- [#8544](https://github.com/NuGet/Home/issues/8544)

**DCRs**

* Onboarding von Diagnose Dateien in ifeedbackdiagnosticfileprovider- [#8535](https://github.com/NuGet/Home/issues/8535)

**[Liste aller Probleme, die in dieser Version behoben wurden: 5,4](https://github.com/nuget/home/issues?q=is%3Aissue+is%3Aclosed+milestone%3A%225.4")**
