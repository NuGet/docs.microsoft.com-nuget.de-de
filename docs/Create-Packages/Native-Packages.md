---
title: Erstellen von nativen NuGet-Paketen | Microsoft-Dokumentation
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 1/9/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 7a70d748-efe2-4f8f-a3fd-67ddb0f6214e
description: "Informationen über das Erstellen von nativen NuGet-Paketen, die C++-Code statt verwaltetem Code enthalten und in C++-Projekten verwendet werden können."
keywords: "Native NuGet-Pakete, C++-Pakete für NuGet, native Codepakete, C++-Zielprojekte"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: fa5baaa6ecbad0f5f6dd85d657679ffbbbc8a47a
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/14/2017
---
# <a name="creating-native-packages"></a>Erstellen von nativen Paketen

Ein natives Paket enthält nativen C++-Code anstelle von verwaltetem Code, sodass es innerhalb von C++-Projekten verwendet werden kann. (Lesen Sie hierzu den Absatz zum Thema [Native C++-Pakete](../consume-packages/finding-and-choosing-packages.md#native-cpp-packages) im Abschnitt zum Thema „Verwenden“.)

Ein Paket muss das Framework `native` als Ziel haben, damit Sie dieses in einem C++-Projekt verwenden können. Derzeit sind diesem Framework keine Versionsnummern zugeordnet, da NuGet alle C++-Projekte gleich behandelt.

> [!Note]
> Schließen Sie im Abschnitt `<tags>` Ihrer `.nuspec`-Datei unbedingt *native* ein, damit andere Entwickler das Paket finden können, indem sie nach diesem Tag suchen.

Native NuGet-Pakete mit dem Ziel `native` stellen dann in den Ordnern `\build`, `\content` und `\tools` Dateien bereit; `\lib` wird in diesem Fall nicht verwendet, da NuGet keine direkten Verweise auf C++-Projekte hinzufügen kann. Ein Paket kann im Ordner `\build` auch Zieldateien und Eigenschaftendateien enthalten, die NuGet automatisch in die Projekte importiert, die das Paket verwenden. Diese Dateien müssen den gleichen Namen wie die Paket-IDs mit den Erweiterungen `.targets` und/oder `.props` aufweisen. Beispielsweise enthält das Paket [cpprestsdk](https://nuget.org/packages/cpprestsdk/) im Ordner `\build` eine Datei des Typs `cpprestsdk.targets`.

Der Ordner `\build` kann für alle NuGet-Pakete und nicht nur für native Pakete verwendet werden. Der Ordner `\build` berücksichtigt Zielframeworks ebenso wie die Ordner `\content`, `\lib` und `\tools`. Dies bedeutet, dass Sie einen Ordner namens `\build\net40` und einen namens `\build\net45` erstellen können und NuGet die entsprechenden Eigenschaftendateien und Zieldateien dann in das Projekt importiert. (PowerShell-Skripts sind zum Importieren von MSBuild-Zielen nicht erforderlich.)
