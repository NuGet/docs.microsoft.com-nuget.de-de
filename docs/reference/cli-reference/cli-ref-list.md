---
title: Befehl "nuget CLI List"
description: Referenz für den Befehl "nuget.exe List"
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: d8e5c8574b44375e651f3ff1a4868681b3ce6d66
ms.sourcegitcommit: 53b06e27bcfef03500a69548ba2db069b55837f1
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/19/2020
ms.locfileid: "97699853"
---
# <a name="list-command-nuget-cli"></a>List-Befehl (nuget-CLI)

**Gilt für:** Paket Verbrauch, &bullet; **unterstützte Versionen** werden veröffentlicht: alle

Zeigt eine Liste von Paketen aus einer angegebenen Quelle an. Wenn keine Quellen angegeben werden, werden alle Quellen verwendet, die in der globalen Konfigurationsdatei `%AppData%\NuGet\NuGet.Config` (Windows) oder definiert sind `~/.nuget/NuGet/NuGet.Config` . Wenn `NuGet.Config` keine Quellen angibt, `list` verwendet den Standard-Feed (nuget.org).

## <a name="usage"></a>Verbrauch

```cli
nuget list [search terms] [options]
```

Gibt an, wo die optionalen Suchbegriffe die angezeigte Liste filtern. [Suchbegriffe](../../consume-packages/finding-and-choosing-packages.md#search-syntax) werden auf die Namen von Paketen, Tags und Paketbeschreibungen angewendet, genauso wie Sie Sie auf nuget.org verwenden. 

## <a name="options"></a>Optionen

- **`-AllVersions`**

  Listet alle Versionen eines Pakets auf. Standardmäßig wird nur die neueste Paketversion angezeigt.

- **`-ConfigFile`**

  Die anzuwendende nuget-Konfigurationsdatei. Wenn nichts angegeben ist, `%AppData%\NuGet\NuGet.Config` wird (Windows) `~/.nuget/NuGet/NuGet.Config` oder `~/.config/NuGet/NuGet.Config` (Mac/Linux) verwendet.

- **`-ForceEnglishOutput`**

  *(3.5* und höher) Erzwingt das Ausführen von nuget.exe mit einer invarianten, englischen Kultur.

- **`-?|-help`**

  Zeigt Hilfe Informationen für den Befehl an.

- **`-IncludeDelisted`**

  *(3.2 +)* Nicht aufgelistete Pakete anzeigen.

- **`-NonInteractive`**

  Unterdrückt Eingabe Aufforderungen für Benutzereingaben oder Bestätigungen.

- **`-PreRelease`**

  Schließt vorab Pakete in die Liste ein.

- **`-Source`**

  Die zu durchsuchende Paketquelle. Sie können mehrere Quellen angeben, indem Sie die Option mehrmals verwenden `-Source` .

- **`-Verbosity [normal|quiet|detailed]`**

  Gibt den Umfang der in der Ausgabe angezeigten Details an: `normal` (Standard), `quiet` oder `detailed` .

Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)

## <a name="examples"></a>Beispiele

Auflisten aller Pakete aus konfigurierten Feeds:
```
nuget list
```
Auflisten von Azure-bezogenen Paketen mit detaillierter Ausführlichkeit:
```
nuget list Azure -Verbosity detailed
```
Auflisten aller Versionen von Azure-bezogenen Paketen aus konfigurierten Feeds:
```
nuget list Azure -AllVersions
```
Listet alle Versionen von JSON-bezogenen Paketen aus der angegebenen Quelle bzw. dem Feed auf:
```
nuget list JSON -AllVersions -Source "https://nuget.org/api/v2"
```
Auflisten von JSON-bezogenen Paketen aus mehreren Quellen/Feeds:
```
nuget list JSON -Source "https://nuget.org/api/v2" -Source "https://other-feed-url-goes-here"
```
