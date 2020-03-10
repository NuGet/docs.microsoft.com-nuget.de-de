---
title: NuGet-Format „PackageReference“ (Paketverweise in Projektdateien)
description: Details zu NuGet-PackageReference in Projektdateien unterstützt durch NuGet 4.0 und höher und VS2017 sowie .NET Core 2.0
author: karann-msft
ms.author: karann
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: a5833df60c5f7905359f421141347b1237f45d86
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/02/2020
ms.locfileid: "78230615"
---
# <a name="package-references-packagereference-in-project-files"></a><span data-ttu-id="8cebd-103">Paketverweise (PackageReference) in Projektdateien</span><span class="sxs-lookup"><span data-stu-id="8cebd-103">Package references (PackageReference) in project files</span></span>

<span data-ttu-id="8cebd-104">Paketverweise über den `PackageReference`-Knoten verwalten NuGet-Abhängigkeiten direkt in den Projektdateien. Es wird keine separate `packages.config`-Datei benötigt.</span><span class="sxs-lookup"><span data-stu-id="8cebd-104">Package references, using the `PackageReference` node, manage NuGet dependencies directly within project files (as opposed to a separate `packages.config` file).</span></span> <span data-ttu-id="8cebd-105">Die Verwendung von PackageReference hat keine Auswirkungen auf andere Aspekte von NuGet. Einstellungen in Dateien vom Typ `NuGet.config` (Paketquellen eingeschlossen) gelten beispielsweise weiterhin wie unter [Gängige NuGet-Konfigurationen](configuring-nuget-behavior.md) beschrieben.</span><span class="sxs-lookup"><span data-stu-id="8cebd-105">Using PackageReference, as it's called, doesn't affect other aspects of NuGet; for example, settings in `NuGet.config` files (including package sources) are still applied as explained in [Common NuGet configurations](configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="8cebd-106">Mit PackageReference können Sie auch MSBuild-Bedingungen für die Auswahl von Paketverweisen pro Zielframework oder anderen Gruppierungen verwenden.</span><span class="sxs-lookup"><span data-stu-id="8cebd-106">With PackageReference, you can also use MSBuild conditions to choose package references per target framework, or other groupings.</span></span> <span data-ttu-id="8cebd-107">Zudem lässt er eine präzise Steuerung der Abhängigkeiten und des Inhaltsflusses zu.</span><span class="sxs-lookup"><span data-stu-id="8cebd-107">It also allows for fine-grained control over dependencies and content flow.</span></span> <span data-ttu-id="8cebd-108">(Informationen dazu finden Sie unter [NuGet pack and restore as MSBuild targets – restore target (Packen und Wiederherstellen von NuGet als MSBuild-Ziele: Paketwiederherstellung)](../reference/msbuild-targets.md).)</span><span class="sxs-lookup"><span data-stu-id="8cebd-108">(See For more details [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).)</span></span>

## <a name="project-type-support"></a><span data-ttu-id="8cebd-109">Unterstützung für Projekttypen</span><span class="sxs-lookup"><span data-stu-id="8cebd-109">Project type support</span></span>

<span data-ttu-id="8cebd-110">Außer für C++ UWP-Projekte wird PackageReference standardmäßig nur in .NET Core-, .NET Standard- und UWP-Projekten für Windows 10 Build 15063 (Creators Update) und höher unterstützt.</span><span class="sxs-lookup"><span data-stu-id="8cebd-110">By default, PackageReference is used for .NET Core projects, .NET Standard projects, and UWP projects targeting Windows 10 Build 15063 (Creators Update) and later, with the exception of C++ UWP projects.</span></span> <span data-ttu-id="8cebd-111">.NET Framework-Projekte unterstützen PackageReference. Standardmäßig wird jedoch `packages.config` verwendet.</span><span class="sxs-lookup"><span data-stu-id="8cebd-111">.NET Framework projects support PackageReference, but currently default to `packages.config`.</span></span> <span data-ttu-id="8cebd-112">Um PackageReference zu verwenden, [migrieren](../consume-packages/migrate-packages-config-to-package-reference.md) Sie die Abhängigkeiten von `packages.config` zu Ihrer Projektdatei. Entfernen Sie anschließend „packages.config“.</span><span class="sxs-lookup"><span data-stu-id="8cebd-112">To use PackageReference, [migrate](../consume-packages/migrate-packages-config-to-package-reference.md) the dependencies from `packages.config` into your project file, then remove packages.config.</span></span>

<span data-ttu-id="8cebd-113">ASP.NET-Apps für das vollständige .NET Framework enthalten nur [eingeschränkte Unterstützung](https://github.com/NuGet/Home/issues/5877) für PackageReference.</span><span class="sxs-lookup"><span data-stu-id="8cebd-113">ASP.NET apps targeting the full .NET Framework include only [limited support](https://github.com/NuGet/Home/issues/5877) for PackageReference.</span></span> <span data-ttu-id="8cebd-114">C++- und JavaScript-Projekttypen werden nicht unterstützt.</span><span class="sxs-lookup"><span data-stu-id="8cebd-114">C++ and JavaScript project types are unsupported.</span></span>

## <a name="adding-a-packagereference"></a><span data-ttu-id="8cebd-115">Hinzufügen einer PackageReference</span><span class="sxs-lookup"><span data-stu-id="8cebd-115">Adding a PackageReference</span></span>

<span data-ttu-id="8cebd-116">Fügen Sie mit der folgenden Syntax eine Abhängigkeit in Ihrer Projektdatei hinzu:</span><span class="sxs-lookup"><span data-stu-id="8cebd-116">Add a dependency in your project file using the following syntax:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a><span data-ttu-id="8cebd-117">Steuern die Abhängigkeitsversion</span><span class="sxs-lookup"><span data-stu-id="8cebd-117">Controlling dependency version</span></span>

<span data-ttu-id="8cebd-118">Die Konvention für die Angabe der Version eines Pakets entspricht der Verwendung von `packages.config`:</span><span class="sxs-lookup"><span data-stu-id="8cebd-118">The convention for specifying the version of a package is the same as when using `packages.config`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="8cebd-119">Im obigen Beispiel steht 3.6.0 für eine beliebige Version >= 3.6.0, wobei die niedrigste Version bevorzugt wird, wie unter [Paketversionsverwaltung](../concepts/package-versioning.md#version-ranges) beschrieben.</span><span class="sxs-lookup"><span data-stu-id="8cebd-119">In the example above, 3.6.0 means any version that is >=3.6.0 with preference for the lowest version, as described on [Package versioning](../concepts/package-versioning.md#version-ranges).</span></span>

## <a name="using-packagereference-for-a-project-with-no-packagereferences"></a><span data-ttu-id="8cebd-120">Verwenden von PackageReference für ein Projekt ohne PackageReferences</span><span class="sxs-lookup"><span data-stu-id="8cebd-120">Using PackageReference for a project with no PackageReferences</span></span>

<span data-ttu-id="8cebd-121">Erweitert: Wenn Sie keine Pakete in einem Projekt installiert haben (keine PackageReferences in der Projektdatei oder der packages.config-Datei), aber das Projekt mit dem Format von PackageReference wiederherstellen möchten, können Sie in der Projektdatei eine RestoreProjectStyle-Projekteigenschaft auf PackageReference festlegen.</span><span class="sxs-lookup"><span data-stu-id="8cebd-121">Advanced: If you have no packages installed in a project (no PackageReferences in project file and no packages.config file), but want the project to be restored as PackageReference style, you can set a Project property RestoreProjectStyle to PackageReference in your project file.</span></span>

```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreProjectStyle>PackageReference</RestoreProjectStyle>
    <!--- ... -->
</PropertyGroup>    
```

<span data-ttu-id="8cebd-122">Dies kann sich als nützlich erweisen, wenn Sie auf Projekte verweisen, die das Format von PackageReference aufweisen (vorhandene Projekte im CSPROJ- oder SDK-Format).</span><span class="sxs-lookup"><span data-stu-id="8cebd-122">This may be useful, if you reference projects which are PackageReference styled (existing csproj or SDK-style projects).</span></span> <span data-ttu-id="8cebd-123">Dadurch kann Ihr Projekt „transitiv“ auf die Pakete verweisen, auf die diese Projekte verweisen.</span><span class="sxs-lookup"><span data-stu-id="8cebd-123">This will enable packages that those projects refer to, to be "transitively" referenced by your project.</span></span>

## <a name="packagereference-and-sources"></a><span data-ttu-id="8cebd-124">PackageReference und Quellen</span><span class="sxs-lookup"><span data-stu-id="8cebd-124">PackageReference and sources</span></span>

<span data-ttu-id="8cebd-125">In PackageReference-Projekten werden transitive Abhängigkeitsversionen zur Wiederherstellungszeit aufgelöst.</span><span class="sxs-lookup"><span data-stu-id="8cebd-125">In PackageReference projects, the transitive dependency versions are resolved at restore time.</span></span> <span data-ttu-id="8cebd-126">Daher müssen in PackageReference-Projekten alle Quellen für alle Wiederherstellungen verfügbar sein.</span><span class="sxs-lookup"><span data-stu-id="8cebd-126">As such, in PackageReference projects all sources need to be available for all restores.</span></span> 

## <a name="floating-versions"></a><span data-ttu-id="8cebd-127">Unverankerte Versionen</span><span class="sxs-lookup"><span data-stu-id="8cebd-127">Floating Versions</span></span>

<span data-ttu-id="8cebd-128">[Unverankerte Versionen](../concepts/dependency-resolution.md#floating-versions) werden mit `PackageReference` unterstützt:</span><span class="sxs-lookup"><span data-stu-id="8cebd-128">[Floating versions](../concepts/dependency-resolution.md#floating-versions) are supported with `PackageReference`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a><span data-ttu-id="8cebd-129">Steuern von Abhängigkeitsobjekten</span><span class="sxs-lookup"><span data-stu-id="8cebd-129">Controlling dependency assets</span></span>

<span data-ttu-id="8cebd-130">Sie verwenden eine Abhängigkeit möglicherweise rein als Entwicklungsumgebung und möchten diese nicht für Projekte verfügbar machen, die Ihr Paket nutzen.</span><span class="sxs-lookup"><span data-stu-id="8cebd-130">You might be using a dependency purely as a development harness and might not want to expose that to projects that will consume your package.</span></span> <span data-ttu-id="8cebd-131">In diesem Szenario können Sie dieses Verhalten über die `PrivateAssets`-Metadaten steuern.</span><span class="sxs-lookup"><span data-stu-id="8cebd-131">In this scenario, you can use the `PrivateAssets` metadata to control this behavior.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="8cebd-132">Mit den folgenden Metadatentags werden Abhängigkeitsobjekte gesteuert:</span><span class="sxs-lookup"><span data-stu-id="8cebd-132">The following metadata tags control dependency assets:</span></span>

| <span data-ttu-id="8cebd-133">Tag</span><span class="sxs-lookup"><span data-stu-id="8cebd-133">Tag</span></span> | <span data-ttu-id="8cebd-134">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="8cebd-134">Description</span></span> | <span data-ttu-id="8cebd-135">Standardwert</span><span class="sxs-lookup"><span data-stu-id="8cebd-135">Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="8cebd-136">IncludeAssets</span><span class="sxs-lookup"><span data-stu-id="8cebd-136">IncludeAssets</span></span> | <span data-ttu-id="8cebd-137">Diese Objekte werden verbraucht</span><span class="sxs-lookup"><span data-stu-id="8cebd-137">These assets will be consumed</span></span> | <span data-ttu-id="8cebd-138">alle</span><span class="sxs-lookup"><span data-stu-id="8cebd-138">all</span></span> |
| <span data-ttu-id="8cebd-139">ExcludeAssets</span><span class="sxs-lookup"><span data-stu-id="8cebd-139">ExcludeAssets</span></span> | <span data-ttu-id="8cebd-140">Diese Objekte werden nicht verbraucht</span><span class="sxs-lookup"><span data-stu-id="8cebd-140">These assets will not be consumed</span></span> | <span data-ttu-id="8cebd-141">Keine</span><span class="sxs-lookup"><span data-stu-id="8cebd-141">none</span></span> |
| <span data-ttu-id="8cebd-142">PrivateAssets</span><span class="sxs-lookup"><span data-stu-id="8cebd-142">PrivateAssets</span></span> | <span data-ttu-id="8cebd-143">Diese Objekte werden verbraucht, aber nicht in das übergeordnete Projekt übertragen</span><span class="sxs-lookup"><span data-stu-id="8cebd-143">These assets will be consumed but won't flow to the parent project</span></span> | <span data-ttu-id="8cebd-144">contentfiles;analyzers;build</span><span class="sxs-lookup"><span data-stu-id="8cebd-144">contentfiles;analyzers;build</span></span> |

<span data-ttu-id="8cebd-145">Folgende Werte sind für diese Tags zulässig, wobei mehrere Werte durch ein Semikolon (;) getrennt sind; eine Ausnahme stellen `all` und `none` dar, die nur alleine dargestellt werden dürfen:</span><span class="sxs-lookup"><span data-stu-id="8cebd-145">Allowable values for these tags are as follows, with multiple values separated by a semicolon except with `all` and `none` which must appear by themselves:</span></span>

| <span data-ttu-id="8cebd-146">Wert</span><span class="sxs-lookup"><span data-stu-id="8cebd-146">Value</span></span> | <span data-ttu-id="8cebd-147">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="8cebd-147">Description</span></span> |
| --- | ---
| <span data-ttu-id="8cebd-148">compile</span><span class="sxs-lookup"><span data-stu-id="8cebd-148">compile</span></span> | <span data-ttu-id="8cebd-149">Inhalt des Ordners `lib` und steuert, ob Ihr Projekt anhand der Assemblys im Ordner kompiliert werden kann</span><span class="sxs-lookup"><span data-stu-id="8cebd-149">Contents of the `lib` folder and controls whether your project can compile against the assemblies within the folder</span></span> |
| <span data-ttu-id="8cebd-150">Laufzeit</span><span class="sxs-lookup"><span data-stu-id="8cebd-150">runtime</span></span> | <span data-ttu-id="8cebd-151">Inhalt der Ordner `lib` und `runtimes` und steuert, ob diese Assemblys in das Buildausgabeverzeichnis kopiert werden</span><span class="sxs-lookup"><span data-stu-id="8cebd-151">Contents of the `lib` and `runtimes` folder and controls whether these assemblies will be copied out to the build output directory</span></span> |
| <span data-ttu-id="8cebd-152">contentFiles</span><span class="sxs-lookup"><span data-stu-id="8cebd-152">contentFiles</span></span> | <span data-ttu-id="8cebd-153">Inhalte des Ordners `contentfiles`</span><span class="sxs-lookup"><span data-stu-id="8cebd-153">Contents of the `contentfiles` folder</span></span> |
| <span data-ttu-id="8cebd-154">build</span><span class="sxs-lookup"><span data-stu-id="8cebd-154">build</span></span> | <span data-ttu-id="8cebd-155">`.props` und `.targets` im Ordner `build`</span><span class="sxs-lookup"><span data-stu-id="8cebd-155">`.props` and `.targets` in the `build` folder</span></span> |
| <span data-ttu-id="8cebd-156">buildMultitargeting</span><span class="sxs-lookup"><span data-stu-id="8cebd-156">buildMultitargeting</span></span> | <span data-ttu-id="8cebd-157">*(4.0)* `.props` und `.targets` im Ordner `buildMultitargeting` für frameworkübergreifende Zielplattformen</span><span class="sxs-lookup"><span data-stu-id="8cebd-157">*(4.0)* `.props` and `.targets` in the `buildMultitargeting` folder, for cross-framework targeting</span></span> |
| <span data-ttu-id="8cebd-158">buildTransitive</span><span class="sxs-lookup"><span data-stu-id="8cebd-158">buildTransitive</span></span> | <span data-ttu-id="8cebd-159">*(5.0 und höher)* `.props` und `.targets` im Ordner `buildTransitive` für Ressourcen, die transitiv in beliebige verarbeitende Projekte eingefügt werden.</span><span class="sxs-lookup"><span data-stu-id="8cebd-159">*(5.0+)* `.props` and `.targets` in the `buildTransitive` folder, for assets that flow transitively to any consuming project.</span></span> <span data-ttu-id="8cebd-160">Weitere Informationen finden Sie auf der Seite [Feature](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior).</span><span class="sxs-lookup"><span data-stu-id="8cebd-160">See the [feature](https://github.com/NuGet/Home/wiki/Allow-package--authors-to-define-build-assets-transitive-behavior) page.</span></span> |
| <span data-ttu-id="8cebd-161">Analysetools</span><span class="sxs-lookup"><span data-stu-id="8cebd-161">analyzers</span></span> | <span data-ttu-id="8cebd-162">.NET-Analystetools</span><span class="sxs-lookup"><span data-stu-id="8cebd-162">.NET analyzers</span></span> |
| <span data-ttu-id="8cebd-163">Systemeigen</span><span class="sxs-lookup"><span data-stu-id="8cebd-163">native</span></span> | <span data-ttu-id="8cebd-164">Inhalte des Ordners `native`</span><span class="sxs-lookup"><span data-stu-id="8cebd-164">Contents of the `native` folder</span></span> |
| <span data-ttu-id="8cebd-165">Keine</span><span class="sxs-lookup"><span data-stu-id="8cebd-165">none</span></span> | <span data-ttu-id="8cebd-166">Keiner der obigen Werte wird verwendet.</span><span class="sxs-lookup"><span data-stu-id="8cebd-166">None of the above are used.</span></span> |
| <span data-ttu-id="8cebd-167">alle</span><span class="sxs-lookup"><span data-stu-id="8cebd-167">all</span></span> | <span data-ttu-id="8cebd-168">Alle oben genannten Werte (mit Ausnahme von `none`)</span><span class="sxs-lookup"><span data-stu-id="8cebd-168">All of the above (except `none`)</span></span> |

<span data-ttu-id="8cebd-169">Im folgenden Beispiel wird im Projekt bis auf die Inhaltsdateien aus dem Paket alles verwendet, und alles bis auf die Inhaltsdateien und Analysetools wird in das übergeordnete Projekt übertragen.</span><span class="sxs-lookup"><span data-stu-id="8cebd-169">In the following example, everything except the content files from the package would be consumed by the project and everything except content files and analyzers would flow to the parent project.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <IncludeAssets>all</IncludeAssets>
        <ExcludeAssets>contentFiles</ExcludeAssets>
        <PrivateAssets>contentFiles;analyzers</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="8cebd-170">Beachten Sie Folgendes: Da `build` nicht in `PrivateAssets` enthalten ist, *werden* Ziele und Eigenschaften an das übergeordnete Projekt übergeben.</span><span class="sxs-lookup"><span data-stu-id="8cebd-170">Note that because `build` is not included with `PrivateAssets`, targets and props *will* flow to the parent project.</span></span> <span data-ttu-id="8cebd-171">Angenommen, der obenstehende Verweis wird in einem Projekt verwendet, in dem ein NuGet-Paket mit dem Namen AppLogger erstellt wird.</span><span class="sxs-lookup"><span data-stu-id="8cebd-171">Consider, for example, that the reference above is used in a project that builds a NuGet package called AppLogger.</span></span> <span data-ttu-id="8cebd-172">AppLogger kann die Ziele und Eigenschaften aus `Contoso.Utility.UsefulStuff` verarbeiten, wie Projekte, die AppLogger verarbeiten.</span><span class="sxs-lookup"><span data-stu-id="8cebd-172">AppLogger can consume the targets and props from `Contoso.Utility.UsefulStuff`, as can projects that consume AppLogger.</span></span>

> [!NOTE]
> <span data-ttu-id="8cebd-173">Wenn `developmentDependency` in einer `.nuspec`-Datei auf `true` festgelegt ist, kennzeichnet dies ein Paket mit einer Abhängigkeit, die nur für die Entwicklung gilt. Dadurch wird vermieden, dass das Paket als Abhängigkeit in andere Pakete eingefügt wird.</span><span class="sxs-lookup"><span data-stu-id="8cebd-173">When `developmentDependency` is set to `true` in a `.nuspec` file, this marks a package as a development-only dependency, which prevents the package from being included as a dependency in other packages.</span></span> <span data-ttu-id="8cebd-174">Bei PackageReference *(NuGet 4.8+)* bedeutet dieses Flag auch, dass Objekte zur Kompilierzeit von der Kompilierung ausgeschlossen werden.</span><span class="sxs-lookup"><span data-stu-id="8cebd-174">With PackageReference *(NuGet 4.8+)*, this flag also means that it will exclude compile-time assets from compilation.</span></span> <span data-ttu-id="8cebd-175">Weitere Informationen finden Sie unter [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference) (DevelopmentDependency-Unterstützung für PackageReference).</span><span class="sxs-lookup"><span data-stu-id="8cebd-175">For more information, see [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference).</span></span>

## <a name="adding-a-packagereference-condition"></a><span data-ttu-id="8cebd-176">Hinzufügen einer PackageReference-Bedingung</span><span class="sxs-lookup"><span data-stu-id="8cebd-176">Adding a PackageReference condition</span></span>

<span data-ttu-id="8cebd-177">Sie können mithilfe einer Bedingung steuern, ob ein Paket eingeschlossen wird. Dabei kann in Bedingungen eine beliebige MSBuild-Variable oder eine in der Ziel- oder Eigenschaftendatei definierte Variable verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="8cebd-177">You can use a condition to control whether a package is included, where conditions can use any MSBuild variable or a variable defined in the targets or props file.</span></span> <span data-ttu-id="8cebd-178">Zum aktuellen Zeitpunkt wird jedoch nur die Variable `TargetFramework` unterstützt.</span><span class="sxs-lookup"><span data-stu-id="8cebd-178">However, at presently, only the `TargetFramework` variable is supported.</span></span>

<span data-ttu-id="8cebd-179">Angenommen, Ihre Zielgruppen lauten `netstandard1.4` und `net452`, die vorhandene Abhängigkeit gilt jedoch nur für `net452`.</span><span class="sxs-lookup"><span data-stu-id="8cebd-179">For example, say you're targeting `netstandard1.4` as well as `net452` but have a dependency that is applicable only for `net452`.</span></span> <span data-ttu-id="8cebd-180">In diesem Fall sollte diese unnötige Abhängigkeit nicht zu einem `netstandard1.4`-Projekt hinzugefügt werden, in dem Ihr Paket verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="8cebd-180">In this case you don't want a `netstandard1.4` project that's consuming your package to add that unnecessary dependency.</span></span> <span data-ttu-id="8cebd-181">Sie geben in der `PackageReference` eine Bedingung an, um dies zu verhindern, die wie folgt lautet:</span><span class="sxs-lookup"><span data-stu-id="8cebd-181">To prevent this, you specify a condition on the `PackageReference` as follows:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="8cebd-182">Ein Paket, das in diesem Projekt erstellt wurde, zeigt an, dass die Datei „Newtonsoft.json“ nur als Abhängigkeit für ein `net452`-Ziel enthalten ist:</span><span class="sxs-lookup"><span data-stu-id="8cebd-182">A package built using this project will show that Newtonsoft.Json is included as a dependency only for a `net452` target:</span></span>

![Das Ergebnis der Anwendung einer Bedingung auf die PackageReference mit VS2017](media/PackageReference-Condition.png)

<span data-ttu-id="8cebd-184">Bedingungen können auch auf der `ItemGroup`-Ebene angewendet werden und gelten dann für alle untergeordneten `PackageReference`-Elemente:</span><span class="sxs-lookup"><span data-stu-id="8cebd-184">Conditions can also be applied at the `ItemGroup` level and will apply to all children `PackageReference` elements:</span></span>

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="generatepathproperty"></a><span data-ttu-id="8cebd-185">GeneratePathProperty</span><span class="sxs-lookup"><span data-stu-id="8cebd-185">GeneratePathProperty</span></span>

<span data-ttu-id="8cebd-186">Dieses Feature ist mit NuGet **5.0** oder höher und mit Visual Studio 2019 **16.0** oder höher verfügbar.</span><span class="sxs-lookup"><span data-stu-id="8cebd-186">This feature is available with NuGet **5.0** or above and with Visual Studio 2019 **16.0** or above.</span></span>

<span data-ttu-id="8cebd-187">Manchmal ist es wünschenswert, von einem MSBuild-Ziel aus auf Dateien in einem Paket zu verweisen.</span><span class="sxs-lookup"><span data-stu-id="8cebd-187">Sometimes it is desirable to reference files in a package from an MSBuild target.</span></span>
<span data-ttu-id="8cebd-188">In `packages.config`-basierten Projekten werden die Pakete in einem Ordner mit Bezug zur Projektdatei installiert.</span><span class="sxs-lookup"><span data-stu-id="8cebd-188">In `packages.config` based projects, the packages are installed in a folder relative to the project file.</span></span> <span data-ttu-id="8cebd-189">Bei PackageReference werden die Pakete hingegen aus dem Ordner *global-packages* [verwendet](../concepts/package-installation-process.md), der von Computer zu Computer variieren kann.</span><span class="sxs-lookup"><span data-stu-id="8cebd-189">However in PackageReference, the packages are [consumed](../concepts/package-installation-process.md) from the *global-packages* folder, which can vary from machine to machine.</span></span>

<span data-ttu-id="8cebd-190">Um diese Lücke zu schließen, wurde in NuGet eine Eigenschaft eingeführt, die auf den Speicherort verweist, von dem aus das Paket verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="8cebd-190">To bridge that gap, NuGet introduced a property that points to the location from which the package will be consumed.</span></span>

<span data-ttu-id="8cebd-191">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="8cebd-191">Example:</span></span>

```xml
  <ItemGroup>
      <PackageReference Include="Some.Package" Version="1.0.0" GeneratePathProperty="true" />
  </ItemGroup>

  <Target Name="TakeAction" AfterTargets="Build">
    <Exec Command="$(PkgSome_Package)\something.exe" />
  </Target>
````

<span data-ttu-id="8cebd-192">Zusätzlich werden von NuGet automatisch Eigenschaften für Pakete generiert, die einen Tools-Ordner enthalten.</span><span class="sxs-lookup"><span data-stu-id="8cebd-192">Additionally NuGet will automatically generate properties for packages containing a tools folder.</span></span>

```xml
  <ItemGroup>
      <PackageReference Include="Package.With.Tools" Version="1.0.0" />
  </ItemGroup>

  <Target Name="TakeAction" AfterTargets="Build">
    <Exec Command="$(PkgPackage_With_Tools)\tools\tool.exe" />
  </Target>
````

<span data-ttu-id="8cebd-193">MSBuild-Eigenschaften und Paketidentitäten haben nicht die gleichen Einschränkungen, sodass die Paketidentität in einen MSBuild-Anzeigenamen geändert werden muss, dem das Wort `Pkg` vorangestellt ist.</span><span class="sxs-lookup"><span data-stu-id="8cebd-193">MSBuild properties and package identities do not have the same restrictions so the package identity needs to be changed to an MSBuild friendly name, prefixed by the word `Pkg`.</span></span>
<span data-ttu-id="8cebd-194">Beachten Sie die generierte [nuget.g.props](../reference/msbuild-targets.md#restore-outputs)-Datei, um den genauen Namen der generierten Eigenschaft zu überprüfen.</span><span class="sxs-lookup"><span data-stu-id="8cebd-194">To verify the exact name of the property generated, look at the generated [nuget.g.props](../reference/msbuild-targets.md#restore-outputs) file.</span></span>

## <a name="nuget-warnings-and-errors"></a><span data-ttu-id="8cebd-195">NuGet-Warnungen und -Fehler</span><span class="sxs-lookup"><span data-stu-id="8cebd-195">NuGet warnings and errors</span></span>

<span data-ttu-id="8cebd-196">*Dieses Feature ist mit NuGet **4.3** oder höher und mit Visual Studio 2017 **15.3** oder höher verfügbar.*</span><span class="sxs-lookup"><span data-stu-id="8cebd-196">*This feature is available with NuGet **4.3** or above and with Visual Studio 2017 **15.3** or above.*</span></span>

<span data-ttu-id="8cebd-197">Für viele Pack- und Wiederherstellungsszenarios werden alle NuGet-Warnungen und -Fehler codiert, und sie beginnen mit `NU****`.</span><span class="sxs-lookup"><span data-stu-id="8cebd-197">For many pack and restore scenarios, all NuGet warnings and errors are coded, and start with `NU****`.</span></span> <span data-ttu-id="8cebd-198">Alle NuGet-Warnungen und -Fehler sind in der [Referenz](../reference/errors-and-warnings.md)-Dokumentation aufgeführt.</span><span class="sxs-lookup"><span data-stu-id="8cebd-198">All NuGet warnings and errors are listed in the [reference](../reference/errors-and-warnings.md) documentation.</span></span>

<span data-ttu-id="8cebd-199">NuGet beachtet die folgenden Warnungseigenschaften:</span><span class="sxs-lookup"><span data-stu-id="8cebd-199">NuGet observes the following warning properties:</span></span>

- <span data-ttu-id="8cebd-200">`TreatWarningsAsErrors`, alle Warnungen als Fehler behandeln</span><span class="sxs-lookup"><span data-stu-id="8cebd-200">`TreatWarningsAsErrors`, treat all warnings as errors</span></span>
- <span data-ttu-id="8cebd-201">`WarningsAsErrors`, bestimmte Warnungen als Fehler behandeln</span><span class="sxs-lookup"><span data-stu-id="8cebd-201">`WarningsAsErrors`, treat specific warnings as errors</span></span>
- <span data-ttu-id="8cebd-202">`NoWarn`, bestimmte Warnungen ausblenden, entweder projekt- oder paketweit.</span><span class="sxs-lookup"><span data-stu-id="8cebd-202">`NoWarn`, hide specific warnings, either project-wide or package-wide.</span></span>

<span data-ttu-id="8cebd-203">Beispiele:</span><span class="sxs-lookup"><span data-stu-id="8cebd-203">Examples:</span></span>

```xml
<PropertyGroup>
    <TreatWarningsAsErrors>true</TreatWarningsAsErrors>
</PropertyGroup>
...
<PropertyGroup>
    <WarningsAsErrors>$(WarningsAsErrors);NU1603;NU1605</WarningsAsErrors>
</PropertyGroup>
...
<PropertyGroup>
    <NoWarn>$(NoWarn);NU5124</NoWarn>
</PropertyGroup>
...
<ItemGroup>
    <PackageReference Include="Contoso.Package" Version="1.0.0" NoWarn="NU1605" />
</ItemGroup>
```

### <a name="suppressing-nuget-warnings"></a><span data-ttu-id="8cebd-204">Unterdrücken von NuGet-Warnungen</span><span class="sxs-lookup"><span data-stu-id="8cebd-204">Suppressing NuGet warnings</span></span>

<span data-ttu-id="8cebd-205">Es wird empfohlen, alle NuGet-Warnungen während der Pack- und Wiederherstellungsvorgänge aufzulösen; in bestimmten Situationen wird deren Auflösung verlangt.</span><span class="sxs-lookup"><span data-stu-id="8cebd-205">While it is recommended that you resolve all NuGet warnings during your pack and restore operations, in certain situations suppressing them is warranted.</span></span>
<span data-ttu-id="8cebd-206">Für die projektweite Unterdrückung einer Warnung sollten Sie Folgendes in Erwägung ziehen:</span><span class="sxs-lookup"><span data-stu-id="8cebd-206">To suppress a warning project wide, consider doing:</span></span>

```xml
<PropertyGroup>
    <PackageVersion>5.0.0</PackageVersion>
    <NoWarn>$(NoWarn);NU5104</NoWarn>
</PropertyGroup>
<ItemGroup>
    <PackageReference Include="Contoso.Package" Version="1.0.0-beta.1"/>
</ItemGroup>
```

<span data-ttu-id="8cebd-207">Gelegentlich beziehen sich Warnungen nur auf ein bestimmtes Paket im Graph.</span><span class="sxs-lookup"><span data-stu-id="8cebd-207">Sometimes warnings apply only to a certain package in the graph.</span></span> <span data-ttu-id="8cebd-208">Sie können eine solche Warnung selektiv unterdrücken, indem Sie im PackageReference-Element `NoWarn` hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="8cebd-208">We can choose to suppress that warning more selectively by adding a `NoWarn` on the PackageReference item.</span></span> 

```xml
<PropertyGroup>
    <PackageVersion>5.0.0</PackageVersion>
</PropertyGroup>
<ItemGroup>
    <PackageReference Include="Contoso.Package" Version="1.0.0-beta.1" NoWarn="NU1603" />
</ItemGroup>
```

#### <a name="suppressing-nuget-package-warnings-in-visual-studio"></a><span data-ttu-id="8cebd-209">Unterdrücken von Warnungen für NuGet-Pakete in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="8cebd-209">Suppressing NuGet package warnings in Visual Studio</span></span>

<span data-ttu-id="8cebd-210">In Visual Studio ist das [Unterdrücken von Warnungen](/visualstudio/ide/how-to-suppress-compiler-warnings#suppress-warnings-for-nuget-packages
) auch über die IDE möglich.</span><span class="sxs-lookup"><span data-stu-id="8cebd-210">When in Visual Studio, you can also [suppress warnings](/visualstudio/ide/how-to-suppress-compiler-warnings#suppress-warnings-for-nuget-packages
) through the IDE.</span></span>

## <a name="locking-dependencies"></a><span data-ttu-id="8cebd-211">Sperren von Abhängigkeiten</span><span class="sxs-lookup"><span data-stu-id="8cebd-211">Locking dependencies</span></span>

<span data-ttu-id="8cebd-212">*Dieses Feature ist mit NuGet **4.9** oder höher und mit Visual Studio 2017 **15.9** oder höher verfügbar.*</span><span class="sxs-lookup"><span data-stu-id="8cebd-212">*This feature is available with NuGet **4.9** or above and with Visual Studio 2017 **15.9** or above.*</span></span>

<span data-ttu-id="8cebd-213">Die Eingabe für die NuGet-Wiederherstellung ist ein Satz mit Paketverweisen aus der Projektdatei (oberste Ebene oder direkte Abhängigkeiten). Die Ausgabe ist der vollständige Abschluss aller Paketabhängigkeiten einschließlich transitiver Abhängigkeiten.</span><span class="sxs-lookup"><span data-stu-id="8cebd-213">Input to NuGet restore is a set of Package References from the project file (top-level or direct dependencies) and the output is a full closure of all the package dependencies including transitive dependencies.</span></span> <span data-ttu-id="8cebd-214">NuGet versucht immer, den gleichen vollständigen Abschluss von Paketabhängigkeiten zu erzeugen, wenn sich die PackageReference-Eingabeliste nicht geändert hat.</span><span class="sxs-lookup"><span data-stu-id="8cebd-214">NuGet tries to always produce the same full closure of package dependencies if the input PackageReference list has not changed.</span></span> <span data-ttu-id="8cebd-215">Es gibt jedoch einige Szenarien, in denen dies nicht möglich ist.</span><span class="sxs-lookup"><span data-stu-id="8cebd-215">However, there are some scenarios where it is unable to do so.</span></span> <span data-ttu-id="8cebd-216">Zum Beispiel:</span><span class="sxs-lookup"><span data-stu-id="8cebd-216">For example:</span></span>

* <span data-ttu-id="8cebd-217">Beim Verwenden von unverankerten Versionen wie `<PackageReference Include="My.Sample.Lib" Version="4.*"/>`.</span><span class="sxs-lookup"><span data-stu-id="8cebd-217">When you use floating versions like `<PackageReference Include="My.Sample.Lib" Version="4.*"/>`.</span></span> <span data-ttu-id="8cebd-218">Während die Absicht hierbei darin liegt, bei jeder Wiederherstellung die neueste Version zu verwenden, gibt es Szenarien, in denen Benutzer anfordern, dass der Paketgraph auf eine bestimmte neueste Version festgelegt und zu einem späteren Zeitpunkt ggf. explizit eine höhere Version geändert werden kann.</span><span class="sxs-lookup"><span data-stu-id="8cebd-218">While the intention here is to float to the latest version on every restore of packages, there are scenarios where users require the graph to be locked to a certain latest version and float to a later version, if available, upon an explicit gesture.</span></span>
* <span data-ttu-id="8cebd-219">Eine neuere Version des Pakets, die den Anforderungen an die PackageReference-Version entspricht, wird veröffentlicht.</span><span class="sxs-lookup"><span data-stu-id="8cebd-219">A newer version of the package matching PackageReference version requirements is published.</span></span> <span data-ttu-id="8cebd-220">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="8cebd-220">E.g.</span></span> 

  * <span data-ttu-id="8cebd-221">Tag 1: Sie haben `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>` angegeben, aber die in den NuGet-Repositorys verfügbaren Versionen waren 4.1.0, 4.2.0 und 4.3.0.</span><span class="sxs-lookup"><span data-stu-id="8cebd-221">Day 1: if you specified `<PackageReference Include="My.Sample.Lib" Version="4.0.0"/>` but the versions available on the NuGet repositories were 4.1.0, 4.2.0 and 4.3.0.</span></span> <span data-ttu-id="8cebd-222">In diesem Fall verwendet NuGet die Version 4.1.0 (die nächste verfügbare Mindestversion).</span><span class="sxs-lookup"><span data-stu-id="8cebd-222">In this case, NuGet would have resolved to  4.1.0 (nearest minimum version)</span></span>

  * <span data-ttu-id="8cebd-223">Tag 2: Version 4.0.0 wird veröffentlicht.</span><span class="sxs-lookup"><span data-stu-id="8cebd-223">Day 2: Version 4.0.0 gets published.</span></span> <span data-ttu-id="8cebd-224">NuGet findet jetzt die exakte Übereinstimmung und beginnt mit der Verwendung von 4.0.0.</span><span class="sxs-lookup"><span data-stu-id="8cebd-224">NuGet will now find the exact match and start resolving to 4.0.0</span></span>

* <span data-ttu-id="8cebd-225">Eine bestimmte Paketversion wird aus dem Repository entfernt.</span><span class="sxs-lookup"><span data-stu-id="8cebd-225">A given package version is removed from the repository.</span></span> <span data-ttu-id="8cebd-226">Auch wenn nuget.org das Löschen von Paketen nicht erlaubt, weisen nicht alle Paketrepositorys diese Einschränkung auf.</span><span class="sxs-lookup"><span data-stu-id="8cebd-226">Though nuget.org does not allow package deletions, not all package repositories have this constraints.</span></span> <span data-ttu-id="8cebd-227">Daher sucht NuGet nach der besten Übereinstimmung, wenn die gelöschte Version nicht verwendet werden kann.</span><span class="sxs-lookup"><span data-stu-id="8cebd-227">This results in NuGet finding the best match when it cannot resolve to the deleted version.</span></span>

### <a name="enabling-lock-file"></a><span data-ttu-id="8cebd-228">Aktivieren einer Sperrdatei</span><span class="sxs-lookup"><span data-stu-id="8cebd-228">Enabling lock file</span></span>

<span data-ttu-id="8cebd-229">Um den vollständigen Abschluss von Paketabhängigkeiten beizubehalten, können Sie die Funktion einer Sperrdatei einrichten, indem Sie die MSBuild-Eigenschaft `RestorePackagesWithLockFile` für Ihr Projekt festlegen:</span><span class="sxs-lookup"><span data-stu-id="8cebd-229">In order to persist the full closure of package dependencies you can opt-in to the lock file feature by setting the MSBuild property `RestorePackagesWithLockFile` for your project:</span></span>

```xml
<PropertyGroup>
    <!--- ... -->
    <RestorePackagesWithLockFile>true</RestorePackagesWithLockFile>
    <!--- ... -->
</PropertyGroup>    
```

<span data-ttu-id="8cebd-230">Wenn diese Eigenschaft festgelegt ist, generiert NuGet eine Sperrdatei – `packages.lock.json`-Datei – im Projektstammverzeichnis, die alle Paketabhängigkeiten auflistet.</span><span class="sxs-lookup"><span data-stu-id="8cebd-230">If this property is set, NuGet restore will generate a lock file - `packages.lock.json` file at the project root directory that lists all the package dependencies.</span></span> 

> [!Note]
> <span data-ttu-id="8cebd-231">Sobald ein Projekt eine `packages.lock.json`-Datei im Stammverzeichnis enthält, wird die Sperrdatei bei der Wiederherstellung immer verwendet, auch wenn die Eigenschaft `RestorePackagesWithLockFile` nicht festgelegt ist.</span><span class="sxs-lookup"><span data-stu-id="8cebd-231">Once a project has `packages.lock.json` file in its root directory, the lock file is always used with restore even if the property `RestorePackagesWithLockFile` is not set.</span></span> <span data-ttu-id="8cebd-232">Eine andere Möglichkeit zur Verwendung dieser Funktion besteht also darin, eine leere `packages.lock.json`-Dummydatei im Stammverzeichnis des Projekts zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="8cebd-232">So another way to opt-in to this feature is to create a dummy blank `packages.lock.json` file in the project's root directory.</span></span>

### <a name="restore-behavior-with-lock-file"></a><span data-ttu-id="8cebd-233">`restore`-Verhalten mit Sperrdatei</span><span class="sxs-lookup"><span data-stu-id="8cebd-233">`restore` behavior with lock file</span></span>
<span data-ttu-id="8cebd-234">Wenn für ein Projekt eine Sperrdatei vorhanden ist, verwendet NuGet diese Sperrdatei zum Ausführen von `restore`.</span><span class="sxs-lookup"><span data-stu-id="8cebd-234">If a lock file is present for project, NuGet uses this lock file to run `restore`.</span></span> <span data-ttu-id="8cebd-235">NuGet überprüft, ob Änderungen an den Paketabhängigkeiten vorgenommen wurden, die in der Projektdatei (bzw. in Projektdateien von abhängigen Projekten) definiert wurden. Wenn keine Änderungen vorhanden sind, stellt NuGet einfach die in der Sperrdatei angegebenen Pakete wieder her.</span><span class="sxs-lookup"><span data-stu-id="8cebd-235">NuGet does a quick check to see if there were any changes in the package dependencies as mentioned in the project file (or dependent projects' files) and if there were no changes it just restores the packages mentioned in the lock file.</span></span> <span data-ttu-id="8cebd-236">Es erfolgt keine erneute Auswertung der Paketabhängigkeiten.</span><span class="sxs-lookup"><span data-stu-id="8cebd-236">There is no re-evaluation of package dependencies.</span></span>

<span data-ttu-id="8cebd-237">Wenn NuGet eine Änderung bei den in den Projektdateien definierten Abhängigkeiten ermittelt, wird der Paketgraph erneut ausgewertet, und die Sperrdatei wird aktualisiert, um den neuen Paketabschluss für das Projekt widerzuspiegeln.</span><span class="sxs-lookup"><span data-stu-id="8cebd-237">If NuGet detects a change in the defined dependencies as mentioned in the project file(s), it re-evaluates the package graph and updates the lock file to reflect the new package closure for the project.</span></span>

<span data-ttu-id="8cebd-238">Für CI/CD- und andere Szenarien, in denen Paketabhängigkeiten nicht dynamisch geändert werden dürfen, können Sie dies erreichen, indem Sie `lockedmode` auf `true` festlegen:</span><span class="sxs-lookup"><span data-stu-id="8cebd-238">For CI/CD and other scenarios, where you would not want to change the package dependencies on the fly, you can do so by setting the `lockedmode` to `true`:</span></span>

<span data-ttu-id="8cebd-239">Führen Sie für dotnet.exe folgenden Befehl aus:</span><span class="sxs-lookup"><span data-stu-id="8cebd-239">For dotnet.exe, run:</span></span>

```
> dotnet.exe restore --locked-mode
```

<span data-ttu-id="8cebd-240">Führen Sie für msbuild.exe folgenden Befehl aus:</span><span class="sxs-lookup"><span data-stu-id="8cebd-240">For msbuild.exe, run:</span></span>

```
> msbuild.exe -t:restore -p:RestoreLockedMode=true
```

<span data-ttu-id="8cebd-241">Sie können diese bedingte MSBuild-Eigenschaft auch in Ihrer Projektdatei festlegen:</span><span class="sxs-lookup"><span data-stu-id="8cebd-241">You may also set this conditional MSBuild property in your project file:</span></span>

```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreLockedMode>true</RestoreLockedMode>
    <!--- ... -->
</PropertyGroup> 
```

<span data-ttu-id="8cebd-242">Wenn der Sperrmodus `true` lautet, gilt Folgendes: Bei der Wiederherstellung werden entweder die Pakete genau so wiederhergestellt wie in der Sperrdatei aufgelistet, oder es tritt ein Fehler auf, wenn Sie die definierten Paketabhängigkeiten für das Projekt nach dem Erstellen der Sperrdatei aktualisiert haben.</span><span class="sxs-lookup"><span data-stu-id="8cebd-242">If locked mode is `true`, restore will either restore the exact packages as listed in the lock file or fail if you updated the defined package dependencies for the project after lock file was created.</span></span>

### <a name="make-lock-file-part-of-your-source-repository"></a><span data-ttu-id="8cebd-243">Einbinden der Sperrdatei als Teil Ihres Quellrepositorys</span><span class="sxs-lookup"><span data-stu-id="8cebd-243">Make lock file part of your source repository</span></span>
<span data-ttu-id="8cebd-244">Wenn Sie eine Anwendung oder eine ausführbare Datei erstellen und sich das fragliche Projekt am Anfang der Abhängigkeitskette befindet, checken Sie die Sperrdatei im Quellcoderepository ein, damit NuGet diese während der Wiederherstellung verwenden kann.</span><span class="sxs-lookup"><span data-stu-id="8cebd-244">If you are building an application, an executable and the project in question is at the start of the dependency chain then do check in the lock file to the source code repository so that NuGet can make use of it during restore.</span></span>

<span data-ttu-id="8cebd-245">Wenn es sich bei Ihrem Projekt aber um ein nicht auszulieferndes Bibliotheksprojekt oder ein Projekt mit gemeinsamem Code handelt, von dem andere Projekte abhängig sind, sollten Sie die Sperrdatei **nicht** als Teil Ihres Quellcodes einchecken.</span><span class="sxs-lookup"><span data-stu-id="8cebd-245">However, if your project is a library project that you do not ship or a common code project on which other projects depend upon, you **should not** check in the lock file as part of your source code.</span></span> <span data-ttu-id="8cebd-246">Es schadet nicht, die Sperrdatei zu behalten, aber die gesperrten Paketabhängigkeiten für das Projekt mit gemeinsamem Code werden möglicherweise während der Wiederherstellung bzw. Erstellung eines Projekts, das von diesem Projekt mit gemeinsamem Code abhängig ist, nicht wie in der Sperrdatei aufgelistet verwendet.</span><span class="sxs-lookup"><span data-stu-id="8cebd-246">There is no harm in keeping the lock file but the locked package dependencies for the common code project may not be used, as listed in the lock file, during the restore/build of a project that depends on this common-code project.</span></span>

<span data-ttu-id="8cebd-247">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="8cebd-247">Eg.</span></span>

```
ProjectA
  |------> PackageX 2.0.0
  |------> ProjectB
             |------>PackageX 1.0.0
```

<span data-ttu-id="8cebd-248">Wenn `ProjectA` eine Abhängigkeit von einer `PackageX`-Version `2.0.0` aufweist und auch auf `ProjectB` verweist, das von der `PackageX`-Version `1.0.0` abhängig ist, listet die Sperrdatei für `ProjectB` eine Abhängigkeit von der `PackageX`-Version `1.0.0` auf.</span><span class="sxs-lookup"><span data-stu-id="8cebd-248">If `ProjectA` has a dependency on a `PackageX` version `2.0.0` and also references `ProjectB` that depends on `PackageX` version `1.0.0`, then the lock file for `ProjectB` will list a dependency on `PackageX` version `1.0.0`.</span></span> <span data-ttu-id="8cebd-249">Wenn `ProjectA` jedoch erstellt wird, enthält die Sperrdatei eine Abhängigkeit von der `PackageX`-Version **`2.0.0`** und **nicht** von `1.0.0`, wie in der Sperrdatei für `ProjectB` aufgelistet.</span><span class="sxs-lookup"><span data-stu-id="8cebd-249">However, when `ProjectA` is built, its lock file will contain a dependency on `PackageX` version **`2.0.0`** and **not** `1.0.0` as listed in the lock file for `ProjectB`.</span></span> <span data-ttu-id="8cebd-250">Daher hat die Sperrdatei eines Projekts mit gemeinsamem Code nur wenig Aussagekraft für die verwendeten Pakete für Projekte, die von diesem Projekt abhängig sind.</span><span class="sxs-lookup"><span data-stu-id="8cebd-250">Thus, the lock file of a common code project has little say over the packages resolved for projects that depend on it.</span></span>

### <a name="lock-file-extensibility"></a><span data-ttu-id="8cebd-251">Erweiterbarkeit der Sperrdatei</span><span class="sxs-lookup"><span data-stu-id="8cebd-251">Lock file extensibility</span></span>

<span data-ttu-id="8cebd-252">Sie können mit einer Sperrdatei verschiedene Verhaltensweisen der Wiederherstellung steuern, wie im Folgenden beschrieben:</span><span class="sxs-lookup"><span data-stu-id="8cebd-252">You can control various behaviors of restore with lock file as described below:</span></span>

| <span data-ttu-id="8cebd-253">NuGet.exe-Option</span><span class="sxs-lookup"><span data-stu-id="8cebd-253">NuGet.exe option</span></span> | <span data-ttu-id="8cebd-254">dotnet-Option</span><span class="sxs-lookup"><span data-stu-id="8cebd-254">dotnet option</span></span> | <span data-ttu-id="8cebd-255">Entsprechende MSBuild-Option</span><span class="sxs-lookup"><span data-stu-id="8cebd-255">MSBuild equivalent option</span></span> | <span data-ttu-id="8cebd-256">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="8cebd-256">Description</span></span> |
|:--- |:--- |:--- |:--- |
| `-UseLockFile` |`--use-lock-file` | <span data-ttu-id="8cebd-257">RestorePackagesWithLockFile</span><span class="sxs-lookup"><span data-stu-id="8cebd-257">RestorePackagesWithLockFile</span></span> | <span data-ttu-id="8cebd-258">Ermöglicht die Verwendung einer Sperrdatei.</span><span class="sxs-lookup"><span data-stu-id="8cebd-258">Opts into the usage of a lock file.</span></span> |
| `-LockedMode` | `--locked-mode` | <span data-ttu-id="8cebd-259">RestoreLockedMode</span><span class="sxs-lookup"><span data-stu-id="8cebd-259">RestoreLockedMode</span></span> | <span data-ttu-id="8cebd-260">Ermöglicht den Sperrmodus für die Wiederherstellung.</span><span class="sxs-lookup"><span data-stu-id="8cebd-260">Enables locked mode for restore.</span></span> <span data-ttu-id="8cebd-261">Dies ist nützlich in CI/CD-Szenarien, in denen Sie wiederholbare Builds wünschen.</span><span class="sxs-lookup"><span data-stu-id="8cebd-261">This is useful in CI/CD scenarios where you want repeatable builds.</span></span>|   
| `-ForceEvaluate` | `--force-evaluate` | <span data-ttu-id="8cebd-262">RestoreForceEvaluate</span><span class="sxs-lookup"><span data-stu-id="8cebd-262">RestoreForceEvaluate</span></span> | <span data-ttu-id="8cebd-263">Diese Option ist nützlich bei Paketen, bei denen im Projekt unverankerte Versionen definiert sind.</span><span class="sxs-lookup"><span data-stu-id="8cebd-263">This option is useful with packages with floating version defined in the project.</span></span> <span data-ttu-id="8cebd-264">Standardmäßig aktualisiert die NuGet-Wiederherstellung die Paketversion nicht automatisch bei jedem Wiederherstellungsvorgang, wenn Sie diesen Vorgang nicht mit dieser Option ausführen.</span><span class="sxs-lookup"><span data-stu-id="8cebd-264">By default, NuGet restore will not update the package version automatically upon each restore unless you run restore with this option.</span></span> |
| `-LockFilePath` | `--lock-file-path` | <span data-ttu-id="8cebd-265">NuGetLockFilePath</span><span class="sxs-lookup"><span data-stu-id="8cebd-265">NuGetLockFilePath</span></span> | <span data-ttu-id="8cebd-266">Definiert einen benutzerdefinierten Speicherort der Sperrdatei für ein Projekt.</span><span class="sxs-lookup"><span data-stu-id="8cebd-266">Defines a custom lock file location for a project.</span></span> <span data-ttu-id="8cebd-267">Standardmäßig unterstützt NuGet `packages.lock.json` im Stammverzeichnis.</span><span class="sxs-lookup"><span data-stu-id="8cebd-267">By default, NuGet supports `packages.lock.json` at the root directory.</span></span> <span data-ttu-id="8cebd-268">Wenn Sie über mehrere Projekte im gleichen Verzeichnis verfügen, unterstützt NuGet die projektspezifische Sperrdatei `packages.<project_name>.lock.json`.</span><span class="sxs-lookup"><span data-stu-id="8cebd-268">If you have multiple projects in the same directory, NuGet supports project specific lock file `packages.<project_name>.lock.json`</span></span> |
