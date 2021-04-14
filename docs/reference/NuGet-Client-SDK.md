---
title: NuGet-Client SDK
description: Die API wird weiterentwickelt und noch nicht dokumentiert, aber Beispiele finden Sie im Blog von Dave Glick.
author: JonDouglas
ms.author: jodou
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: 6417c971dc13cf9ed05dcec4e4156af94c0ea058
ms.sourcegitcommit: c8bf16420f235fc3e42c08cd0d56359e91d490e5
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/14/2021
ms.locfileid: "107387386"
---
# <a name="nuget-client-sdk"></a>NuGet-Client SDK

Das *NuGet Client SDK* bezieht sich auf eine Gruppe von NuGet-Paketen:

* [`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) – Wird für die Interaktion mit HTTP- und dateibasierten NuGet-Feeds verwendet.
* [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) – Wird für die Interaktion mit NuGet-Paketen verwendet. `NuGet.Protocol` hängt von diesem Paket ab.

Den Quellcode für diese Pakete finden Sie im GitHub-Repository [NuGet/NuGet.Client.](https://github.com/NuGet/NuGet.Client)
Den Quellcode für diese Beispiele finden Sie im Projekt [NuGet.Protocol.Samples](https://github.com/NuGet/Samples/tree/main/NuGetProtocolSamples) auf GitHub.

> [!Note]
> Die Dokumentation zum NuGet-Serverprotokoll finden Sie in der [NuGet-Server-API.](~/api/overview.md)

## <a name="nugetprotocol"></a>NuGet.Protocol

Installieren Sie das `NuGet.Protocol` Paket für die Interaktion mit HTTP- und ordnerbasierten NuGet-Paketfeeds:

```ps1
dotnet add package NuGet.Protocol
```

> [!Tip]
> `Repository.Factory` wird im `NuGet.Protocol.Core.Types` -Namespace definiert, und die `GetCoreV3` -Methode ist eine erweiterungsmethode, die im -Namespace definiert `NuGet.Protocol` ist. Daher müssen Sie `using` -Anweisungen für beide Namespaces hinzufügen.

### <a name="list-package-versions"></a>Auflisten von Paketversionen

Suchen Sie alle Versionen von Newtonsoft.Jsmithilfe der [NuGet V3-Paketinhalts-API:](../api/package-base-address-resource.md#enumerate-package-versions)

[!code-csharp[ListPackageVersions](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ListPackageVersions)]

### <a name="download-a-package"></a>Herunterladen eines Pakets

Laden Sie Newtonsoft.Jsunter v12.0.1 mithilfe der [NuGet V3-Paketinhalts-API](../api/package-base-address-resource.md)herunter:

[!code-csharp[DownloadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DownloadPackage)]

### <a name="get-package-metadata"></a>Abrufen von Paketmetadaten

Abrufen der Metadaten für das Paket "Newtonsoft.Json" mithilfe der [NuGet V3-Paketmetadaten-API:](../api/registration-base-url-resource.md)

[!code-csharp[GetPackageMetadata](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=GetPackageMetadata)]

### <a name="search-packages"></a>Suchen von Paketen

Suchen Sie mithilfe der [NuGet V3-Such-API nach JSON-Paketen:](../api/search-query-service-resource.md)

[!code-csharp[SearchPackages](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=SearchPackages)]

### <a name="push-a-package"></a>Pushen eines Pakets

Pushen eines Pakets mithilfe der [NuGet V3-PUSH- und DELETE-API:](../api/package-publish-resource.md)

[!code-csharp[PushPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=PushPackage)]

### <a name="delete-a-package"></a>Löschen eines Pakets

Löschen Sie ein Paket mithilfe der [NuGet V3-PUSH- und DELETE-API:](../api/package-publish-resource.md)

> [!Note]
> NuGet-Server können eine Paketlöschanforderung als "hard delete", "soft delete" oder "unlist" interpretieren.
> Beispielsweise interpretiert nuget.org die Paketlöschanforderung als "Unlist". Weitere Informationen zu dieser Vorgehensweise finden Sie unter Löschen [von Paketen.](../nuget-org/policies/deleting-packages.md)

[!code-csharp[DeletePackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=DeletePackage)]

### <a name="work-with-authenticated-feeds"></a>Arbeiten mit authentifizierten Feeds

Verwenden [`NuGet.Protocol`](https://www.nuget.org/packages/NuGet.Protocol) Sie , um mit authentifizierten Feeds zu arbeiten.

[!code-csharp[AuthenticatedFeed](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=AuthenticatedFeed)]

## <a name="nugetpackaging"></a>NuGet.Packaging

Installieren Sie das `NuGet.Packaging` Paket für die Interaktion mit - und `.nupkg` `.nuspec` -Dateien aus einem Stream:

```ps1
dotnet add package NuGet.Packaging
```

### <a name="create-a-package"></a>Erstellen eines Pakets

Erstellen Sie mit ein Paket, legen Sie Metadaten fest, und fügen Sie Abhängigkeiten [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) hinzu.

> [!IMPORTANT]
> Es wird dringend empfohlen, NuGet-Pakete mit den  offiziellen NuGet-Tools und nicht mit dieser low-level-API zu erstellen. Es gibt eine Vielzahl von Merkmalen, die für ein wohlgeformte Paket wichtig sind, und die neueste Version der Tools hilft, diese bewährten Methoden zu integrieren.
> 
> Weitere Informationen zum Erstellen von NuGet-Paketen finden Sie in der Übersicht über den Workflow zur Paketerstellung und in der Dokumentation zu offiziellen Pakettools (z. B. mithilfe der [dotnet-CLI).](../create-packages/creating-a-package-dotnet-cli.md) [](../create-packages/overview-and-workflow.md)

[!code-csharp[CreatePackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=CreatePackage)]

### <a name="read-a-package"></a>Lesen eines Pakets

Lesen eines Pakets aus einem Dateistream mithilfe von [`NuGet.Packaging`](https://www.nuget.org/packages/NuGet.Packaging) .

[!code-csharp[ReadPackage](~/../nuget-samples/NuGetProtocolSamples/Program.cs?name=ReadPackage)]

## <a name="third-party-documentation"></a>Dokumentation von Drittanbietern

Beispiele und Dokumentation für einige der APIs finden Sie in der folgenden Blogreihe von Dave Glick, veröffentlicht 2016:

- [Erkunden der NuGet v3-Bibliotheken, Teil 1: Einführung und Konzepte](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [Erkunden der NuGet v3-Bibliotheken, Teil 2: Suchen nach Paketen](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [Erkunden der NuGet v3-Bibliotheken, Teil 3: Installieren von Paketen](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> Diese Blogbeiträge wurden kurz nach der Veröffentlichung der **Version 3.4.3** der NuGet-Client-SDK-Pakete geschrieben.
> Neuere Versionen der Pakete sind möglicherweise nicht mit den Informationen in den Blogbeiträgen kompatibel.

Martin Björkzweig hat einen Folgeblogbeitrag zu Dave Glicks Blogreihe geschrieben, in dem er einen anderen Ansatz zur Verwendung des NuGet-Client-SDK zum Installieren von NuGet-Paketen vorstellt:

- [Erneutes Aufarbeiten der NuGet v3-Bibliotheken](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
