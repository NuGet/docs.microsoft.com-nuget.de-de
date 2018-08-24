---
title: Befehl "Spec" NuGet-CLI
description: Referenz für die nuget.exe-Befehl "Spec"
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: cd1dc66676898e2be1c64698886a5ba29a07f88f
ms.sourcegitcommit: 8d5121af528e68789485405e24e2100fda2868d6
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/23/2018
ms.locfileid: "42794150"
---
# <a name="spec-command-nuget-cli"></a>Befehl "Spec" (NuGet-CLI)

**Gilt für:** paketerstellung &bullet; **unterstützte Versionen:** alle

Generiert eine `.nuspec` -Datei für ein neues Paket. Wenn im gleichen Ordner wie eine Projektdatei (`.csproj`, `.vbproj`, `.fsproj`), `spec` erstellt einen mit Token versehene `.nuspec` Datei. Weitere Informationen finden Sie unter [Erstellen eines Pakets](../create-packages/creating-a-package.md).

## <a name="usage"></a>Verwendung

```cli
nuget spec [<packageID>] [options]
```

wo `<packageID>` ist ein optionales paketbezeichner im Speichern der `.nuspec` Datei.

## <a name="options"></a>Optionen

| Option | Beschreibung |
| --- | --- |
| AssemblyPath | Gibt den Pfad zu der Assembly, die für Metadaten verwendet. |
| Force | Überschreibt vorhandene `.nuspec` Datei. |
| ForceEnglishOutput | *(3.5 und höher)*  Erzwingt nuget.exe über eine invariante Kultur auf Englisch basierenden ausgeführt werden. |
| Hilfe | Zeigt die Informationen für den Befehl Hilfe. |
| NonInteractive | Unterdrückt aufforderungen für Benutzereingaben oder Bestätigungen an. |
| Ausführlichkeit | Gibt an, die Anzahl der Details in der Ausgabe angezeigt: *normalen*, *quiet*, *ausführliche*. |

Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)

## <a name="examples"></a>Beispiele

```cli
nuget spec

nuget spec MyPackage

nuget spec -AssemblyPath MyAssembly.dll
```
