---
title: NuGet-CLI-Spec-Befehl
description: Referenz für den nuget.exe Spec-Befehl
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: 17d3c5fc083f52fd9ab4a854ad358995bc55293b
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/06/2018
ms.locfileid: "34817085"
---
# <a name="spec-command-nuget-cli"></a>gemäß der Spezifikation Befehl (NuGet CLI)

**Gilt für:** Erstellen von Paketen &bullet; **unterstützte Versionen:** alle

Generiert eine `.nuspec` -Datei für ein neues Paket. Beim Ausführen im gleichen Ordner wie eine Projektdatei (`.csproj`, `.vbproj`, `.fsproj`), `spec` erstellt ein Token dargestellten `.nuspec` Datei. Weitere Informationen finden Sie unter [Erstellen eines Pakets](../create-packages/creating-a-package.md).

## <a name="usage"></a>Verwendung

```cli
nuget spec [<packageID>] [options]
```

wobei `<packageID>` ist ein optionales paketbezeichner zum Speichern in der `.nuspec` Datei.

## <a name="options"></a>Optionen

| Option | Beschreibung |
| --- | --- |
| AssemblyPath | Gibt den Pfad zur Assembly, die für Metadaten verwendet. |
| Force | Überschreibt alle vorhandenen `.nuspec` Datei. |
| ForceEnglishOutput | *(3.5 +)*  Erzwingt nuget.exe über eine invariante Kultur Englisch-basierte ausgeführt werden. |
| Hilfe | Zeigt die Hilfe Informationen für den Befehl. |
| NonInteractive | Unterdrückt aufforderungen für Benutzereingaben oder Bestätigungen an. |
| Ausführlichkeit | Gibt die Anzahl der Details in der Ausgabe angezeigt: *normalen*, *stillen*, *ausführliche*. |

Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)

## <a name="examples"></a>Beispiele

```cli
nuget spec

nuget spec MyPackage

nuget spec -a MyAssembly.dll
```
