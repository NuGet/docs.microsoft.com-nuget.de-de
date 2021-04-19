---
title: Problembehandlung bei installierten Paketen
description: So finden Sie heraus, welche Paketquelle für einzelne Pakete verwendet wurde.
author: JonDouglas
ms.author: jodou
ms.date: 03/26/2021
ms.topic: conceptual
ms.openlocfilehash: 22fb51ebb996c66e10b860f0158676fd2d9da295
ms.sourcegitcommit: c8bf16420f235fc3e42c08cd0d56359e91d490e5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/14/2021
ms.locfileid: "107387530"
---
# <a name="troubleshooting-installed-packages"></a>Problembehandlung bei installierten Paketen

Manchmal möchten Sie möglicherweise überprüfen, aus welcher Quelle ein bestimmtes Paket installiert wurde. Hier einige Möglichkeiten der Überprüfung.

> [!Note]
> Einige Paketquellen unterstützen ein Konzept, das als Upstreamquellen bezeichnet wird. Beispielsweise [Azure Artifacts-Upstreamquellen](/azure/devops/artifacts/concepts/upstream-sources). NuGet-Clients wissen nicht, ob ein Paket aus einer Upstreamquelle stammt. Daher listet jede Protokollierung der Paketquelle die konfigurierte Quelle und nicht die Upstreamquelle auf.

## <a name="nupkgmetadata-file-in-global-packages-folder"></a>Datei `.nupkg.metadata` im Ordner für globale Pakete

Wenn ein Paket in den Ordner *global-packages* extrahiert wird, wird eine `.nupkg.metadata`-Datei geschrieben. Ab NuGet 5.9.0 fügt NuGet die Paketquelle hinzu. Im Folgenden erfahren Sie, wie Sie NuGet-Versionen Visual Studio-oder .NET SDK-Versionen zuordnen. Beispiel:

```json
{
  "version": 2,
  "contentHash": "bw3R9q8cVNhWXNpnvWb0OGP4HadS4zvClq+T1zf7AF+tLY1haZ2AvbHidQekf4PDv1T40c6brZeT/V0IBq7cEQ==",
  "source": "https://api.nuget.org/v3/index.json"
}
```

> [!Note]
> Wenn Ihr Ordner *global-packages* Pakete enthält, die extrahiert wurden, bevor Sie ein Upgrade auf eine neuere Version von Tools mit NuGet 5.9.0 durchgeführt haben, ist die Datei `.nupkg.metadata` Version 1 und enthält die Paketquelle nicht. Sie können Ihren [Ordner *global-packages* löschen](../consume-packages/managing-the-global-packages-and-cache-folders.md#clearing-local-folders), um sicherzustellen, dass alle Pakete die Paketquelle enthalten.

> [!Tip]
> NuGet schreibt die Datei `.nupkg.metadata` nur in den Ordner *global-packages.* Projekte, die `packages.config` verwenden, verwenden einen Lösungspaketordner, der keine Datei `.nupkg.metadata` erstellt.

## <a name="installed-package-log-message"></a>Protokollmeldung zu installierten Paketen

Ab NuGet 5.9.0 gibt NuGet die Paketquelle in der Wiederherstellungsmeldung aus, die darüber informiert, dass ein Paket installiert wurde. Beispiel:

```text
Installed Moq 4.16.1 from https://api.nuget.org/v3/index.json with content hash bw3R9q8cVNhWXNpnvWb0OGP4HadS4zvClq+T1zf7AF+tLY1haZ2AvbHidQekf4PDv1T40c6brZeT/V0IBq7cEQ==.
```

> [!Tip]
> Diese Meldung wird bei normaler/informationaler Ausführlichkeit ausgegeben. Visual Studio und die `dotnet` CLI sind standardmäßig auf minimale Ausführlichkeit festgelegt, sodass diese Meldung standardmäßig nicht sichtbar ist. `msbuild` und die `nuget` CLI-Tools sind standardmäßig auf normale Ausführlichkeit festgelegt, sodass diese Meldung standardmäßig sichtbar ist.

## <a name="http-log-message"></a>HTTP-Protokollmeldung

Wenn ein Paket nicht lokal verfügbar ist (im Ordner *global-packages*, einem Fallbackordner oder einer lokalen Dateiquelle), lädt NuGet es aus einer beliebigen konfigurierten Paketquelle über HTTP herunter. HTTP-Anforderungen und -Antworten werden mit der normalen Ausführlichkeitsstufe protokolliert, und Sie sollten nur eine einzige Anforderung und Antwort pro Paketversion sehen. Beispiel:

```text
info :   GET https://api.nuget.org/v3-flatcontainer/moq/index.json
info :   OK https://api.nuget.org/v3-flatcontainer/moq/index.json 56ms
info :   GET https://api.nuget.org/v3-flatcontainer/moq/4.16.1/moq.4.16.1.nupkg
info :   OK https://api.nuget.org/v3-flatcontainer/moq/4.16.1/moq.4.16.1.nupkg 3ms
```

Wenn die Dateien vor Kurzem heruntergeladen wurden, können sie ggf. aus dem *http-cache* von NuGet abgerufen werden.

```text
CACHE https://api.nuget.org/v3-flatcontainer/moq/index.json
CACHE https://api.nuget.org/v3-flatcontainer/moq/4.16.1/moq.4.16.1.nupkg
```

Das URL-Format kann für verschiedene NuGet-HTTP-Serverimplementierungen und abhängig davon unterschiedlich sein, ob das HTTP-Protokoll NuGet V2 oder V3 implementiert wird.

Wenn für Ihre Datei `nuget.config` mehrere HTTP-Quellen definiert sind, werden mehrere Anforderungen für jede `index.json`-Datei jedes Pakets angezeigt, eine für jede Quelle. Es wird jedoch nur ein einzelner `nupkg`-Download für jede Version des Pakets vorhanden sein.

## <a name="package-signature-log-message"></a>Paketsignatur-Protokollmeldung

Wenn das heruntergeladene Paket signiert ist, überprüft NuGet die Signatur und protokolliert die folgende Meldung mit detaillierter Ausführlichkeit:

```text
PackageSignatureVerificationLog: PackageIdentity: Moq.4.16.1 Source: https://api.nuget.org/v3/index.json PackageSignatureValidity: True
```

Diese Meldung wird unabhängig davon ausgegeben, ob das Paket aus einer HTTP-Paketquelle heruntergeladen oder aus einer lokalen Paketquelle kopiert wurde. Sie wird nicht ausgegeben, wenn das Paket bereits im Ordner *global-packages* oder in einem Fallbackordner verfügbar ist.

> [!Important]
> Aufgrund der [Aufhebung der Vertrauensstellung von VeriSign CA](https://github.com/dotnet/announcements/issues/180) hat NuGet die Überprüfung signierter Pakete auf bestimmten Plattformen in bestimmten Versionen von NuGet und im .NET SDK deaktiviert. Daher können dieselben Pakete `PackageSignatureVerificationLog`-Protokolle aufweisen, oder diese Protokolle können fehlen, je nachdem, auf welcher Plattform Sie die Wiederherstellung ausführen und welche Version von .NET oder NuGet Sie verwenden.

## <a name="nuget-version-map"></a>NuGet-Versionszuordnung

Die folgenden Versionen von NuGet weisen wichtige Änderungen in Bezug auf die Paketquellprotokollierung auf:

|NuGet-Version|Visual Studio-Version|Version des .NET SDK|
|---|---|---|
|NuGet 5.9.0|Visual Studio 2019 16.9.0|.NET 5 SDK 5.0.200|
