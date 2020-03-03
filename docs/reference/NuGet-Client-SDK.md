---
title: Nuget-Client-SDK
description: Die API wird weiterentwickelt und noch nicht dokumentiert, aber Beispiele sind im Blog von Dave Glick verfügbar.
author: karann-msft
ms.author: karann
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: a5c542379318f24ee35ccf25651d0e8de91253ba
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231239"
---
# <a name="nuget-client-sdk"></a>Nuget-Client-SDK

Das *nuget-Client-SDK* bezieht sich auf eine Gruppe von nuget-Paketen:

* [`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) : für die Interaktion mit http-und dateibasierten nuget-Feeds verwendet
* [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) , die für die Interaktion mit nuget-Paketen verwendet wird. `NuGet.Protocol` hängt von diesem Paket ab.

Sie finden den Quellcode für diese Pakete im GitHub [-Repository nuget/nuget. Client](https://github.com/NuGet/NuGet.Client) .

> [!Note]
> Dokumentation zum nuget-Server Protokoll finden Sie in der [nuget-Server-API](~/api/overview.md).

## <a name="getting-started"></a>Erste Schritte

### <a name="install-the-package"></a>Installieren des Pakets

```ps1
dotnet add package NuGet.Protocol
```

## <a name="examples"></a>Beispiele

Diese Beispiele finden Sie im [nuget. Protocol. Samples](https://github.com/NuGet/Samples/tree/master/NuGetProtocolSamples) -Projekt auf GitHub.

### <a name="list-package-versions"></a>Auflisten von Paketversionen

Suchen Sie alle Versionen von "newtonsoft. JSON" mithilfe der [nuget v3-Paket Inhalts-API](../api/package-base-address-resource.md#enumerate-package-versions):

[!code-csharp[ListPackageVersions](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ListPackageVersions)]

### <a name="download-a-package"></a>Herunterladen eines Pakets

Laden Sie Newton Soft. JSON v 12.0.1 mit der [nuget v3-Paket Inhalts-API](../api/package-base-address-resource.md)herunter:

[!code-csharp[DownloadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DownloadPackage)]

### <a name="get-package-metadata"></a>Paket Metadaten erhalten

Holen Sie sich die Metadaten für das Paket "newtonsoft. JSON" mit der [nuget V3-Paketmetadaten-API](../api/registration-base-url-resource.md):

[!code-csharp[GetPackageMetadata](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=GetPackageMetadata)]

### <a name="search-packages"></a>Suchen von Paketen

Suchen Sie mit der [nuget V3-Such-API](../api/search-query-service-resource.md)nach "JSON"-Paketen:

[!code-csharp[SearchPackages](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=SearchPackages)]

## <a name="third-party-documentation"></a>Dokumentation von Drittanbietern

Beispiele und Dokumentationen für einige der APIs finden Sie in der folgenden Blog Reihe von Dave Glick, veröffentlicht 2016:

- [Erkunden der nuget V3-Bibliotheken, Teil 1: Einführung und Konzepte](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [Erkunden der nuget V3-Bibliotheken, Teil 2: Suchen nach Paketen](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [Erkunden der nuget V3-Bibliotheken, Teil 3: Installieren von Paketen](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> Diese Blogbeiträge wurden kurz nach der Veröffentlichung der **3.4.3** -Version der nuget-Client-SDK-Pakete geschrieben.
> Neuere Versionen der Pakete sind möglicherweise nicht mit den Informationen in den Blogbeiträgen kompatibel.

Martin björkström hat einen nachfolgenden Blogbeitrag zur Blog Reihe von Dave Glick durchgeführt, in dem er eine andere Vorgehensweise zum Installieren von nuget-Paketen mit dem nuget-Client-SDK einführt:

- [Neubesuchen der nuget V3-Bibliotheken](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
