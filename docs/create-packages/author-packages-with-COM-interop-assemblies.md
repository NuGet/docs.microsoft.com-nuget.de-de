---
title: Erstellen von Paketen mit COM-Interop-Assemblys
description: Beschreibt das Erstellen von Paketen, die COM-Interop-Assemblys enthalten
author: JonDouglas
ms.author: jodou
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: b12672e81a974e113ffbda80560c9d3eede9c69d
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859121"
---
# <a name="create-nuget-packages-that-contain-com-interop-assemblies"></a>Erstellen von NuGet-Paketen, die COM-Interop-Assemblys enthalten

Pakete, die COM-Interop-Assemblys enthalten, müssen eine entsprechende [Zieledatei](creating-a-package.md#include-msbuild-props-and-targets-in-a-package) enthalten, damit die richtigen `EmbedInteropTypes`-Metadaten zu Projekten hinzugefügt werden, die das Format „PackageReference“ verwenden. Die `EmbedInteropTypes`-Metadaten sind für alle Assemblys immer FALSE, wenn „PackageReference“ verwendet wird, damit die Zieledatei diese Metadaten explizit hinzufügt. Um Konflikte zu vermeiden, sollte der Name des Ziels eindeutig sein. Verwenden Sie am besten eine Kombination aus dem Paketnamen und der Assembly, die eingebettet wird, und ersetzen Sie `{InteropAssemblyName}` im folgenden Beispiel durch diesen Wert. Ein weiteres Beispiel finden Sie unter [NuGet.Samples.Interop](https://github.com/NuGet/Samples/tree/main/NuGet.Samples.Interop).

```xml
<Target Name="Embedding**AssemblyName**From**PackageId**" AfterTargets="ResolveReferences" BeforeTargets="FindReferenceAssembliesForReferences">
  <ItemGroup>
    <ReferencePath Condition=" '%(FileName)' == '{InteropAssemblyName}' AND '%(ReferencePath.NuGetPackageId)' == '$(MSBuildThisFileName)' ">
      <EmbedInteropTypes>true</EmbedInteropTypes>
    </ReferencePath>
  </ItemGroup>
</Target>
```

Hinweis: Wenn Sie das `packages.config`-Verwaltungsformat verwenden, prüfen NuGet und Visual Studio beim Hinzufügen von Verweisen zu den Assemblys aus Paketen auf COM-Interop-Assemblys und legen `EmbedInteropTypes` in der Projektdatei auf TRUE fest. In diesem Fall werden die Ziele außer Kraft gesetzt.

Darüber hinaus werden die [Buildressourcen standardmäßig nicht transitiv weitergeben](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets). Pakete, die dieser Beschreibung nach erstellt werden, funktionieren anders, wenn sie als transitive Abhängigkeit aus einem Projekt in einen Projektverweis gezogen werden. Der Paketbenutzer kann die Weiterleitung zulassen, indem er den Standardwert „PrivateAssets“ so ändert, dass „build“ nicht enthalten ist.

<a name="creating-the-package"></a>