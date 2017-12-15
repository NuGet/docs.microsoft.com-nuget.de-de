---
title: NuGet-CLI-Spec-Befehl | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/24/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: 85611449-87e6-489b-8c6c-fe1d7be76c13
description: "Referenz für den nuget.exe Spec-Befehl"
keywords: "NuGet – technische Referenz, Spec-Befehl"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c32b23e66c8eb4db1c8fa6dc615589219c00239f
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/14/2017
---
# <a name="spec-command-nuget-cli"></a>gemäß der Spezifikation Befehl (NuGet CLI)

**Gilt für:** Erstellen von Paketen &bullet; **unterstützte Versionen:** alle

Generiert eine `.nuspec` -Datei für ein neues Paket. Beim Ausführen im gleichen Ordner wie eine Projektdatei (`.csproj`, `.vbproj`, `.fsproj`), `spec` erstellt ein Token dargestellten `.nuspec` Datei. Weitere Informationen finden Sie unter [Erstellen eines Pakets](../create-packages/creating-a-package.md).

## <a name="usage"></a>Verwendung

```
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
| Nicht interaktive | Unterdrückt aufforderungen für Benutzereingaben oder Bestätigungen an. |
| Ausführlichkeit | Gibt die Anzahl der Details in der Ausgabe angezeigt: *normalen*, *stillen*, *detaillierte (2.5 und höher)*. |

Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)

## <a name="examples"></a>Beispiele

```
nuget spec

nuget spec MyPackage

nuget spec -a MyAssembly.dll
```
