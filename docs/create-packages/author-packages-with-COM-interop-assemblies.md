---
title: Erstellen von Paketen mit COM-Interop-Assemblys
description: Beschreibt das Erstellen von Paketen, die COM-Interop-Assemblys enthalten
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: de164b136a1636b89f674b8626613094fc53e04c
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/07/2020
ms.locfileid: "75385571"
---
# <a name="create-nuget-packages-that-contain-com-interop-assemblies"></a><span data-ttu-id="be629-103">Erstellen von NuGet-Paketen, die COM-Interop-Assemblys enthalten</span><span class="sxs-lookup"><span data-stu-id="be629-103">Create NuGet packages that contain COM interop assemblies</span></span>

<span data-ttu-id="be629-104">Pakete, die COM-Interop-Assemblys enthalten, müssen eine entsprechende [Zieledatei](creating-a-package.md#include-msbuild-props-and-targets-in-a-package) enthalten, damit die richtigen `EmbedInteropTypes`-Metadaten zu Projekten hinzugefügt werden, die das Format „PackageReference“ verwenden.</span><span class="sxs-lookup"><span data-stu-id="be629-104">Packages that contain COM interop assemblies must include an appropriate [targets file](creating-a-package.md#include-msbuild-props-and-targets-in-a-package) so that the correct `EmbedInteropTypes` metadata is added to projects using the PackageReference format.</span></span> <span data-ttu-id="be629-105">Die `EmbedInteropTypes`-Metadaten sind für alle Assemblys immer FALSE, wenn „PackageReference“ verwendet wird, damit die Zieledatei diese Metadaten explizit hinzufügt.</span><span class="sxs-lookup"><span data-stu-id="be629-105">By default, the `EmbedInteropTypes` metadata is always false for all assemblies when PackageReference is used, so the targets file adds this metadata explicitly.</span></span> <span data-ttu-id="be629-106">Um Konflikte zu vermeiden, sollte der Name des Ziels eindeutig sein. Verwenden Sie am besten eine Kombination aus dem Paketnamen und der Assembly, die eingebettet wird, und ersetzen Sie `{InteropAssemblyName}` im folgenden Beispiel durch diesen Wert.</span><span class="sxs-lookup"><span data-stu-id="be629-106">To avoid conflicts, the target name should be unique; ideally, use a combination of your package name and the assembly being embedded, replacing the `{InteropAssemblyName}` in the example below with that value.</span></span> <span data-ttu-id="be629-107">Ein weiteres Beispiel finden Sie unter [NuGet.Samples.Interop](https://github.com/NuGet/Samples/tree/master/NuGet.Samples.Interop).</span><span class="sxs-lookup"><span data-stu-id="be629-107">(Also see [NuGet.Samples.Interop](https://github.com/NuGet/Samples/tree/master/NuGet.Samples.Interop) for an example.)</span></span>

```xml
<Target Name="Embedding**AssemblyName**From**PackageId**" AfterTargets="ResolveReferences" BeforeTargets="FindReferenceAssembliesForReferences">
  <ItemGroup>
    <ReferencePath Condition=" '%(FileName)' == '{InteropAssemblyName}' AND '%(ReferencePath.NuGetPackageId)' == '$(MSBuildThisFileName)' ">
      <EmbedInteropTypes>true</EmbedInteropTypes>
    </ReferencePath>
  </ItemGroup>
</Target>
```

<span data-ttu-id="be629-108">Hinweis: Wenn Sie das `packages.config`-Verwaltungsformat verwenden, prüfen NuGet und Visual Studio beim Hinzufügen von Verweisen zu den Assemblys aus Paketen auf COM-Interop-Assemblys und legen `EmbedInteropTypes` in der Projektdatei auf TRUE fest.</span><span class="sxs-lookup"><span data-stu-id="be629-108">Note that when using the `packages.config` management format, adding references to the assemblies from the packages causes NuGet and Visual Studio to check for COM interop assemblies and set the `EmbedInteropTypes` to true in the project file.</span></span> <span data-ttu-id="be629-109">In diesem Fall werden die Ziele außer Kraft gesetzt.</span><span class="sxs-lookup"><span data-stu-id="be629-109">In this case, the targets are overridden.</span></span>

<span data-ttu-id="be629-110">Darüber hinaus werden die [Buildressourcen standardmäßig nicht transitiv weitergeben](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span><span class="sxs-lookup"><span data-stu-id="be629-110">Additionally, by default the [build assets do not flow transitively](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).</span></span> <span data-ttu-id="be629-111">Pakete, die dieser Beschreibung nach erstellt werden, funktionieren anders, wenn sie als transitive Abhängigkeit aus einem Projekt in einen Projektverweis gezogen werden.</span><span class="sxs-lookup"><span data-stu-id="be629-111">Packages authored as described here work differently when they are pulled as a transitive dependency from a project to project reference.</span></span> <span data-ttu-id="be629-112">Der Paketbenutzer kann die Weiterleitung zulassen, indem er den Standardwert „PrivateAssets“ so ändert, dass „build“ nicht enthalten ist.</span><span class="sxs-lookup"><span data-stu-id="be629-112">The package consumer can allow them to flow by modifying the PrivateAssets default value to not include build.</span></span>

<a name="creating-the-package"></a>