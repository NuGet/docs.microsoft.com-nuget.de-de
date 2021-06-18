---
title: NuGet CLI-Suchbefehl
description: Referenz für den nuget.exe-Suchbefehl
author: JonDouglas
ms.author: jodou
ms.date: 08/17/2020
ms.topic: reference
ms.openlocfilehash: 0b0d0445f21ae49bc4785a6de822f9b56ec5c453
ms.sourcegitcommit: f3d98c23408a4a1c01ea92fc45493fa7bd97c3ee
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/17/2021
ms.locfileid: "112323660"
---
# <a name="search-command-nuget-cli"></a>Search-Befehl (NuGet-CLI)

**Gilt für:** Paketnutzung &bullet; **Unterstützte Versionen:** 5.8 und höher

Durchsucht eine bestimmte Quelle mithilfe der bereitgestellten Abfragezeichenfolge. Wenn keine Quellen angegeben werden, werden alle in %AppData%\NuGet\NuGet.Config definierten Quellen verwendet.

## <a name="usage"></a>Verwendung

```cli
nuget search [search terms] [options]
```

, wobei die Suchbegriffe auf die Namen von Paketen, Tags und Paketbeschreibungen genauso angewendet werden wie bei der Verwendung auf nuget.org.

## <a name="options"></a>Optionen

| Name | BESCHREIBUNG | Verwendung |
| ---  |     ---     |  :-:  |
| Prerelease | Vorabversionspakete sind standardmäßig nicht enthalten, können aber mit diesem Argument eingeschlossen werden. | -PreRelease |
| `Source` | Bestimmte Paketquellen, die gesucht werden sollen, anstatt die Standardquellen in __nuget.config__ | -Source `<Source URL>`|
| Take | Die Anzahl der zurückzugebende Ergebnisse. Der Standardwert lautet 20. | -Take `<positive integer>` |
| Ausführlichkeit | Die Detailebene, die in der Ausgabe angezeigt werden soll. Der Standardwert ist _normal._ (Siehe Hinweis unten)  | -Ausführlichkeit `<quiet|normal|detailed>` |
| Hilfe | Zeigt Hilfeinformationen für den Befehl an. | -Help |

Siehe auch [Umgebungsvariablen.](cli-ref-environment-variables.md)

> [!NOTE] 
> Ausführlichkeitsstufen:
> * _quiet_ – Paket-ID, Version
> * _normal_ – Paket-ID, Version, Downloads, Vorschau der Beschreibung
> * _detailed_ : Paket-ID, Version, Downloads, vollständige Beschreibung, Weitere Informationen wie die Abfrage-URL

## <a name="examples"></a>Beispiele

Suchen Sie nach *Protokollierungspaketen* aus Standardquellen:
```
nuget search logging
```
Suchen Sie nach *Protokollierungspaketen* mit detaillierter Ausführlichkeit:
```
nuget search logging -Verbosity detailed
```
Suchen Sie nach *paketbezogenen Protokollierungspaketen,* und zeigen Sie nur die ersten fünf Ergebnisse an:
```
nuget search logging -Take 5
```
Suchen Sie nach *JSON-bezogenen* Paketen, einschließlich Vorabversionen, aus der angegebenen Quelle/dem angegebenen Feed:
```
nuget search JSON -PreRelease -Source "https://api.nuget.org/v3/index.json"
```
Suchen Sie nach *JSON-bezogenen* Paketen aus mehreren Quellen/Feeds:
```
nuget search JSON -Source "https://api.nuget.org/v3/index.json" -Source "https://other-feed-url-goes-here"
```
