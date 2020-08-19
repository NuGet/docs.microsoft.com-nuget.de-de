---
title: NuGet-Client SDK
description: Die API wird weiterentwickelt und noch nicht dokumentiert, aber Beispiele sind im Blog von Dave Glick verfügbar.
author: karann-msft
ms.author: karann
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: 39a4de4071eec70c88a2add158f2a3a734f7d7b7
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622927"
---
# <a name="nuget-client-sdk"></a>NuGet-Client SDK

Das *nuget-Client-SDK* bezieht sich auf eine Gruppe von nuget-Paketen:

* [`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) -Wird für die Interaktion mit http-und dateibasierten nuget-Feeds verwendet
* [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) : Wird für die Interaktion mit nuget-Paketen verwendet. `NuGet.Protocol` hängt von diesem Paket ab

Sie finden den Quellcode für diese Pakete im GitHub [-Repository nuget/nuget. Client](https://github.com/NuGet/NuGet.Client) .

> [!Note]
> Dokumentation zum nuget-Server Protokoll finden Sie in der [nuget-Server-API](~/api/overview.md).

## <a name="getting-started"></a>Erste Schritte

### <a name="install-the-packages"></a>Installieren der Pakete

```ps1
dotnet add package NuGet.Protocol  # interact with HTTP and folder-based NuGet package feeds, includes NuGet.Packaging

dotnet add package NuGet.Packaging # interact with .nupkg and .nuspec files from a stream
```

## <a name="examples"></a>Beispiele

Diese Beispiele finden Sie im [nuget. Protocol. Samples](https://github.com/NuGet/Samples/tree/master/NuGetProtocolSamples) -Projekt auf GitHub.

### <a name="list-package-versions"></a>Auflisten von Paketversionen

Alle Versionen von Newtonsoft.Jsmithilfe der [nuget v3-Paket Inhalts-API](../api/package-base-address-resource.md#enumerate-package-versions)suchen:

[!code-csharp[ListPackageVersions](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ListPackageVersions)]

### <a name="download-a-package"></a>Herunterladen eines Pakets

Laden Sie Newtonsoft.Jsauf v 12.0.1 mit der [nuget v3-Paket Inhalts-API](../api/package-base-address-resource.md)herunter:

[!code-csharp[DownloadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DownloadPackage)]

### <a name="get-package-metadata"></a>Paket Metadaten erhalten

Holen Sie sich die Metadaten für das Paket "Newtonsoft.Json" mit der [nuget V3-Paketmetadaten-API](../api/registration-base-url-resource.md):

[!code-csharp[GetPackageMetadata](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=GetPackageMetadata)]

### <a name="search-packages"></a>Suchen von Paketen

Suchen Sie mit der [nuget V3-Such-API](../api/search-query-service-resource.md)nach "JSON"-Paketen:

[!code-csharp[SearchPackages](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=SearchPackages)]

### <a name="create-a-package"></a>Erstellen eines Pakets

Erstellen Sie ein Paket, legen Sie Metadaten fest, und fügen Sie mithilfe von Abhängigkeiten hinzu [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) .

> [!IMPORTANT]
> Es wird dringend empfohlen, dass nuget-Pakete mit den offiziellen nuget-Tools erstellt werden, **ohne** diese Low-Level-API zu verwenden. Es gibt eine Vielzahl von Merkmalen, die für ein wohl geformtes Paket wichtig sind, und die neueste Version der Tools hilft bei der Integration dieser bewährten Methoden.
> 
> Weitere Informationen zum Erstellen von nuget-Paketen finden Sie in der Übersicht über den [Workflow zur Paket Erstellung](../create-packages/overview-and-workflow.md) und in der Dokumentation für offizielle Paket Tools (z. b. [über die dotnet-CLI](../create-packages/creating-a-package-dotnet-cli.md)).

[!code-csharp[CreatePackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=CreatePackage)]

### <a name="read-a-package"></a>Lesen eines Pakets

Lesen eines Pakets aus einem Datei Datenstrom mithilfe von [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) .

[!code-csharp[ReadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ReadPackage)]

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
