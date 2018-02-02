---
title: NuGet-CLI-Spec-Befehl | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Referenz für den nuget.exe Spec-Befehl"
keywords: "NuGet – technische Referenz, Spec-Befehl"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: cc7e772e737a0f74929d13e2b126f7796b6d0dc7
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
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
