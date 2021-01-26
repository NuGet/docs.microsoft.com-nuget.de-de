---
title: Befehl "nuget CLI-Suche"
description: Referenz für den nuget.exe Search-Befehl
author: JonDouglas
ms.author: jodou
ms.date: 08/17/2020
ms.topic: reference
ms.openlocfilehash: 6f4adcdf3981e5ec0e5e88337a8c3bcdd9158ca3
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98779158"
---
# <a name="search-command-nuget-cli"></a>Suchbefehl (nuget-CLI)

**Gilt für:** &bullet; **unterstützte Versionen** von Paketen: 5.8 und höher

Durchsucht eine angegebene Quelle mithilfe der angegebenen Abfrage Zeichenfolge. Wenn keine Quellen angegeben werden, werden alle in% APPDATA% \NuGet\NuGet.config definierten Quellen verwendet.

## <a name="usage"></a>Verwendung

```cli
nuget search [search terms] [options]
```

Wenn die Suchbegriffe auf die Namen von Paketen, Tags und Paketbeschreibungen angewendet werden, so wie Sie Sie in nuget.org verwenden.

## <a name="options"></a>Optionen

| Name | BESCHREIBUNG | Verwendung |
| ---  |     ---     |  :-:  |
| Vorab | Vorab Versionen von Paketen sind nicht standardmäßig enthalten, können jedoch mithilfe dieses Arguments eingefügt werden. | -Vorabversion |
| `Source` | Bestimmte Paketquellen, die durchsucht werden sollen, anstatt die Standard Quellen in __nuget.config__ zu Abfragen | -Quelle `<Source URL>`|
| Take | Die Anzahl der zurück zugebende Ergebnisse. Der Standardwert lautet 20. | -Take `<positive integer>` |
| Ausführlichkeit | Die Detailebene, die in der Ausgabe angezeigt werden soll. Der Standardwert ist " _Normal_". (Siehe Hinweis unten)  | -Ausführlichkeit `<quiet|normal|detailed>` |
| Hilfe | Zeigt Hilfe Informationen für den Befehl an | -Hilfe |

Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)

> [!NOTE] 
> Ausführlichkeits Grade:
> * _quiet_ -Paket-ID, Version
> * _Normal_ -Paket-ID, Version, Downloads, Vorschau der Beschreibung
> * _ausführlich_ : Paket-ID, Version, Downloads, vollständige Beschreibung, andere Informationen, wie z. b. die Abfrage-URL

## <a name="examples"></a>Beispiele

Suchen Sie nach *Protokollierungs* bezogenen Paketen aus Standard Quellen:
```
nuget search logging
```
Suchen Sie nach *Protokollierungs* bezogenen Paketen mit ausführlicher Ausführlichkeit:
```
nuget search logging -Verbosity detailed
```
Suchen Sie nach *Protokollierungs* bezogenen Paketen, und zeigen Sie nur die ersten 5 Ergebnisse an:
```
nuget search logging -Take 5
```
Suchen Sie nach *JSON*-bezogenen Paketen, einschließlich vorab Versionen, aus der angegebenen Quelle bzw. dem Feed:
```
nuget search JSON -PreRelease -Source "https://api.nuget.org/v3/index.json"
```
Suchen Sie nach *JSON*-bezogenen Paketen aus mehreren Quellen/Feeds:
```
nuget search JSON -Source "https://api.nuget.org/v3/index.json" -Source "https://other-feed-url-goes-here"
```
