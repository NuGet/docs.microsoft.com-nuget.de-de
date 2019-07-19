---
title: Befehl "nuget CLI-Spezifikation"
description: Referenz für den Befehl "nuget. exe"
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: reference
ms.openlocfilehash: be6e4fdfe127d5582ecf9983a753a41e6760afe2
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327567"
---
# <a name="spec-command-nuget-cli"></a>spec-Befehl (nuget-CLI)

**Gilt für: von** der &bullet; Paket Erstellung **unterstützte Versionen:** alle

Generiert eine `.nuspec` Datei für ein neues Paket. Wenn Sie im selben Ordner wie eine Projektdatei (`.csproj`, `.vbproj`, `.fsproj`) ausgeführt wird `spec` , erstellt eine `.nuspec` Tokendatei. Weitere Informationen finden Sie unter [Erstellen eines Pakets](../../create-packages/creating-a-package.md).

## <a name="usage"></a>Verwendung

```cli
nuget spec [<packageID>] [options]
```

Dabei ist ein optionaler Paket Bezeichner, der `.nuspec` in der Datei gespeichert werden soll. `<packageID>`

## <a name="options"></a>Optionen

| Option | Beschreibung |
| --- | --- |
| AssemblyPath | Gibt den Pfad zu der Assembly an, die für Metadaten verwendet werden soll. |
| Geltende | Überschreibt eine vorhandene `.nuspec` Datei. |
| ForceEnglishOutput | *(3.5* und höher) Erzwingt, dass "nuget. exe" mit einer invarianten, englischen Kultur ausgeführt wird. |
| Help | Zeigt Hilfe Informationen für den Befehl an. |
| NonInteractive | Unterdrückt Eingabe Aufforderungen für Benutzereingaben oder Bestätigungen. |
| Verbosity | Gibt den Umfang der in der Ausgabe angezeigten Details an: *Normal*, *quiet*, *ausführlich*. |

Siehe auch [Umgebungsvariablen](cli-ref-environment-variables.md)

## <a name="examples"></a>Beispiele

```cli
nuget spec

nuget spec MyPackage

nuget spec -AssemblyPath MyAssembly.dll
```
