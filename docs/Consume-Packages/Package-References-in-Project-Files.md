---
title: NuGet PackageReference-Format (Paketverweise in Projektdateien) | Microsoft-Dokumentation
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/16/2018
ms.topic: article
ms.prod: nuget
ms.technology: ''
description: Details zu NuGet-PackageReference in Projektdateien unterstützt durch NuGet 4.0 und höher und VS2017 sowie .NET Core 2.0
keywords: Abhängigkeiten von NuGet-Paketen, Paketverweise, Projektdateien, PackageReference, „packages.config“, VS2017, Visual Studio 2017, NuGet 4, .NET Core 2.0
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 99caf371ca1bd85e6af4e879741e3e2caab6e860
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="package-references-packagereference-in-project-files"></a><span data-ttu-id="3ccee-104">Paketverweise (PackageReference) in Projektdateien</span><span class="sxs-lookup"><span data-stu-id="3ccee-104">Package references (PackageReference) in project files</span></span>

<span data-ttu-id="3ccee-105">Paketverweise über den `PackageReference`-Knoten verwalten NuGet-Abhängigkeiten direkt in den Projektdateien. Es wird keine separate `packages.config`-Datei benötigt.</span><span class="sxs-lookup"><span data-stu-id="3ccee-105">Package references, using the `PackageReference` node, manage NuGet dependencies directly within project files (as opposed to a separate `packages.config` file).</span></span> <span data-ttu-id="3ccee-106">Wenn das PackageReference-Format verwendet wird, hat dies bei dessen Aufruf keine Auswirkungen auf andere Aspekte von NuGet. Einstellungen in Dateien vom Typ `NuGet.Config` (einschließlich Paketquellen) gelten beispielsweise weiterhin wie unter [Konfigurieren des NuGet-Verhaltens](configuring-nuget-behavior.md) beschrieben.</span><span class="sxs-lookup"><span data-stu-id="3ccee-106">Using PackageReference, as it's called, doesn't affect other aspects of NuGet; for example, settings in `NuGet.Config` files (including package sources) are still applied as explained in [Configuring NuGet Behavior](configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="3ccee-107">Mit PackageReference können Sie auch MSBuild-Bedingungen für die Auswahl von Paketverweisen pro Zielframework, Konfiguration, Plattform oder anderen Gruppierungen verwenden.</span><span class="sxs-lookup"><span data-stu-id="3ccee-107">With PackageReference, you can also use MSBuild conditions to choose package references per target framework, configuration, platform, or other groupings.</span></span> <span data-ttu-id="3ccee-108">Zudem lässt er eine präzise Steuerung der Abhängigkeiten und des Inhaltsflusses zu.</span><span class="sxs-lookup"><span data-stu-id="3ccee-108">It also allows for fine-grained control over dependencies and content flow.</span></span> <span data-ttu-id="3ccee-109">(Informationen dazu finden Sie unter [NuGet pack and restore as MSBuild targets – restore target (Packen und Wiederherstellen von NuGet als MSBuild-Ziele: Paketwiederherstellung)](../reference/msbuild-targets.md).)</span><span class="sxs-lookup"><span data-stu-id="3ccee-109">(See For more details [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).)</span></span>

<span data-ttu-id="3ccee-110">Außer für C++ UWP-Projekte wird PackageReference standardmäßig nur in .NET Core-, .NET Standard- und UWP-Projekten für Windows 10 Build 15063 (Creators Update) und höher unterstützt.</span><span class="sxs-lookup"><span data-stu-id="3ccee-110">By default, PackageReference is used for .NET Core projects, .NET Standard projects, and UWP projects targeting Windows 10 Build 15063 (Creators Update) and later, with the exception of C++ UWP projects.</span></span> <span data-ttu-id="3ccee-111">Vollständige .NET Framework-Projekte unterstützen PackageReference. Standardmäßig wird jedoch `packages.config` verwendet.</span><span class="sxs-lookup"><span data-stu-id="3ccee-111">.NET full framework projects support PackageReference, but currently default to `packages.config`.</span></span> <span data-ttu-id="3ccee-112">Migrieren Sie zur Verwendung von PackageReference die Abhängigkeiten von `packages.config` zu Ihrer Projektdatei. Entfernen Sie anschließend packages.config.</span><span class="sxs-lookup"><span data-stu-id="3ccee-112">To use PackageReference, migrate the dependencies from `packages.config` into your project file, then remove packages.config.</span></span>

## <a name="adding-a-packagereference"></a><span data-ttu-id="3ccee-113">Hinzufügen einer PackageReference</span><span class="sxs-lookup"><span data-stu-id="3ccee-113">Adding a PackageReference</span></span>

<span data-ttu-id="3ccee-114">Fügen Sie mit der folgenden Syntax eine Abhängigkeit in Ihrer Projektdatei hinzu:</span><span class="sxs-lookup"><span data-stu-id="3ccee-114">Add a dependency in your project file using the following syntax:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a><span data-ttu-id="3ccee-115">Steuern die Abhängigkeitsversion</span><span class="sxs-lookup"><span data-stu-id="3ccee-115">Controlling dependency version</span></span>

<span data-ttu-id="3ccee-116">Die Konvention für die Angabe der Version eines Pakets entspricht der Verwendung von `packages.config`:</span><span class="sxs-lookup"><span data-stu-id="3ccee-116">The convention for specifying the version of a package is the same as when using `packages.config`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="3ccee-117">Im obigen Beispiel steht 3.6.0 für eine beliebige Version >= 3.6.0, wobei die niedrigste Version bevorzugt wird, wie unter [Paketversionsverwaltung](../reference/package-versioning.md#version-ranges-and-wildcards) beschrieben.</span><span class="sxs-lookup"><span data-stu-id="3ccee-117">In the example above, 3.6.0 means any version that is >=3.6.0 with preference for the lowest version, as described on [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards).</span></span>

## <a name="floating-versions"></a><span data-ttu-id="3ccee-118">Unverankerte Versionen</span><span class="sxs-lookup"><span data-stu-id="3ccee-118">Floating Versions</span></span>

<span data-ttu-id="3ccee-119">[Unverankerte Versionen](../consume-packages/dependency-resolution.md#floating-versions) werden mit `PackageReference` unterstützt:</span><span class="sxs-lookup"><span data-stu-id="3ccee-119">[Floating versions](../consume-packages/dependency-resolution.md#floating-versions) are supported with `PackageReference`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a><span data-ttu-id="3ccee-120">Steuern von Abhängigkeitsobjekten</span><span class="sxs-lookup"><span data-stu-id="3ccee-120">Controlling dependency assets</span></span>

<span data-ttu-id="3ccee-121">Sie verwenden eine Abhängigkeit möglicherweise rein als Entwicklungsumgebung und möchten diese nicht für Projekte verfügbar machen, die Ihr Paket nutzen.</span><span class="sxs-lookup"><span data-stu-id="3ccee-121">You might be using a dependency purely as a development harness and might not want to expose that to projects that will consume your package.</span></span> <span data-ttu-id="3ccee-122">In diesem Szenario können Sie dieses Verhalten über die `PrivateAssets`-Metadaten steuern.</span><span class="sxs-lookup"><span data-stu-id="3ccee-122">In this scenario, you can use the `PrivateAssets` metadata to control this behavior.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="3ccee-123">Mit den folgenden Metadatentags werden Abhängigkeitsobjekte gesteuert:</span><span class="sxs-lookup"><span data-stu-id="3ccee-123">The following metadata tags control dependency assets:</span></span>

| <span data-ttu-id="3ccee-124">Tag</span><span class="sxs-lookup"><span data-stu-id="3ccee-124">Tag</span></span> | <span data-ttu-id="3ccee-125">description</span><span class="sxs-lookup"><span data-stu-id="3ccee-125">Description</span></span> | <span data-ttu-id="3ccee-126">Standardwert</span><span class="sxs-lookup"><span data-stu-id="3ccee-126">Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="3ccee-127">IncludeAssets</span><span class="sxs-lookup"><span data-stu-id="3ccee-127">IncludeAssets</span></span> | <span data-ttu-id="3ccee-128">Diese Objekte werden verbraucht</span><span class="sxs-lookup"><span data-stu-id="3ccee-128">These assets will be consumed</span></span> | <span data-ttu-id="3ccee-129">alle</span><span class="sxs-lookup"><span data-stu-id="3ccee-129">all</span></span> |
| <span data-ttu-id="3ccee-130">ExcludeAssets</span><span class="sxs-lookup"><span data-stu-id="3ccee-130">ExcludeAssets</span></span> | <span data-ttu-id="3ccee-131">Diese Objekte werden nicht verbraucht</span><span class="sxs-lookup"><span data-stu-id="3ccee-131">These assets will not be consumed</span></span> | <span data-ttu-id="3ccee-132">Keine</span><span class="sxs-lookup"><span data-stu-id="3ccee-132">none</span></span> |
| <span data-ttu-id="3ccee-133">PrivateAssets</span><span class="sxs-lookup"><span data-stu-id="3ccee-133">PrivateAssets</span></span> | <span data-ttu-id="3ccee-134">Diese Objekte werden verbraucht, aber nicht in das übergeordnete Projekt übertragen</span><span class="sxs-lookup"><span data-stu-id="3ccee-134">These assets will be consumed but won't flow to the parent project</span></span> | <span data-ttu-id="3ccee-135">contentfiles;analyzers;build</span><span class="sxs-lookup"><span data-stu-id="3ccee-135">contentfiles;analyzers;build</span></span> |

<span data-ttu-id="3ccee-136">Folgende Werte sind für diese Tags zulässig, wobei mehrere Werte durch ein Semikolon (;) getrennt sind; eine Ausnahme stellen `all` und `none` dar, die nur alleine dargestellt werden dürfen:</span><span class="sxs-lookup"><span data-stu-id="3ccee-136">Allowable values for these tags are as follows, with multiple values separated by a semicolon except with `all` and `none` which must appear by themselves:</span></span>

| <span data-ttu-id="3ccee-137">Wert</span><span class="sxs-lookup"><span data-stu-id="3ccee-137">Value</span></span> | <span data-ttu-id="3ccee-138">description</span><span class="sxs-lookup"><span data-stu-id="3ccee-138">Description</span></span> |
| --- | ---
| <span data-ttu-id="3ccee-139">compile</span><span class="sxs-lookup"><span data-stu-id="3ccee-139">compile</span></span> | <span data-ttu-id="3ccee-140">Inhalte des Ordners `lib`</span><span class="sxs-lookup"><span data-stu-id="3ccee-140">Contents of the `lib` folder</span></span> |
| <span data-ttu-id="3ccee-141">Laufzeit</span><span class="sxs-lookup"><span data-stu-id="3ccee-141">runtime</span></span> | <span data-ttu-id="3ccee-142">Inhalte des Ordners `runtimes`</span><span class="sxs-lookup"><span data-stu-id="3ccee-142">Contents of the `runtimes` folder</span></span> |
| <span data-ttu-id="3ccee-143">contentFiles</span><span class="sxs-lookup"><span data-stu-id="3ccee-143">contentFiles</span></span> | <span data-ttu-id="3ccee-144">Inhalte des Ordners `contentfiles`</span><span class="sxs-lookup"><span data-stu-id="3ccee-144">Contents of the `contentfiles` folder</span></span> |
| <span data-ttu-id="3ccee-145">Build</span><span class="sxs-lookup"><span data-stu-id="3ccee-145">build</span></span> | <span data-ttu-id="3ccee-146">Eigenschaften und Ziele im Ordner `build`</span><span class="sxs-lookup"><span data-stu-id="3ccee-146">Props and targets in the `build` folder</span></span> |
| <span data-ttu-id="3ccee-147">Analysetools</span><span class="sxs-lookup"><span data-stu-id="3ccee-147">analyzers</span></span> | <span data-ttu-id="3ccee-148">.NET-Analystetools</span><span class="sxs-lookup"><span data-stu-id="3ccee-148">.NET analyzers</span></span> |
| <span data-ttu-id="3ccee-149">Systemeigen</span><span class="sxs-lookup"><span data-stu-id="3ccee-149">native</span></span> | <span data-ttu-id="3ccee-150">Inhalte des Ordners `native`</span><span class="sxs-lookup"><span data-stu-id="3ccee-150">Contents of the `native` folder</span></span> |
| <span data-ttu-id="3ccee-151">Keine</span><span class="sxs-lookup"><span data-stu-id="3ccee-151">none</span></span> | <span data-ttu-id="3ccee-152">Keiner der obigen Werte wird verwendet.</span><span class="sxs-lookup"><span data-stu-id="3ccee-152">None of the above are used.</span></span> |
| <span data-ttu-id="3ccee-153">alle</span><span class="sxs-lookup"><span data-stu-id="3ccee-153">all</span></span> | <span data-ttu-id="3ccee-154">Alle oben genannten Werte (mit Ausnahme von `none`)</span><span class="sxs-lookup"><span data-stu-id="3ccee-154">All of the above (except `none`)</span></span> |

<span data-ttu-id="3ccee-155">Im folgenden Beispiel wird im Projekt bis auf die Inhaltsdateien aus dem Paket alles verwendet, und alles bis auf die Inhaltsdateien und Analysetools wird in das übergeordnete Projekt übertragen.</span><span class="sxs-lookup"><span data-stu-id="3ccee-155">In the following example, everything except the content files from the package would be consumed by the project and everything except content files and analyzers would flow to the parent project.</span></span>

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

<span data-ttu-id="3ccee-156">Beachten Sie Folgendes: Da `build` nicht in `PrivateAssets` enthalten ist, *werden* Ziele und Eigenschaften an das übergeordnete Projekt übergeben.</span><span class="sxs-lookup"><span data-stu-id="3ccee-156">Note that because `build` is not included with `PrivateAssets`, targets and props *will* flow to the parent project.</span></span> <span data-ttu-id="3ccee-157">Angenommen, der obenstehende Verweis wird in einem Projekt verwendet, in dem ein NuGet-Paket mit dem Namen AppLogger erstellt wird.</span><span class="sxs-lookup"><span data-stu-id="3ccee-157">Consider, for example, that the reference above is used in a project that builds a NuGet package called AppLogger.</span></span> <span data-ttu-id="3ccee-158">AppLogger kann die Ziele und Eigenschaften aus `Contoso.Utility.UsefulStuff` verarbeiten, wie Projekte, die AppLogger verarbeiten.</span><span class="sxs-lookup"><span data-stu-id="3ccee-158">AppLogger can consume the targets and props from `Contoso.Utility.UsefulStuff`, as can projects that consume AppLogger.</span></span>

## <a name="adding-a-packagereference-condition"></a><span data-ttu-id="3ccee-159">Hinzufügen einer PackageReference-Bedingung</span><span class="sxs-lookup"><span data-stu-id="3ccee-159">Adding a PackageReference condition</span></span>

<span data-ttu-id="3ccee-160">Sie können mithilfe einer Bedingung steuern, ob ein Paket eingeschlossen wird. Dabei kann in Bedingungen eine beliebige MSBuild-Variable oder eine in der Ziel- oder Eigenschaftendatei definierte Variable verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="3ccee-160">You can use a condition to control whether a package is included, where conditions can use any MSBuild variable or a variable defined in the targets or props file.</span></span> <span data-ttu-id="3ccee-161">Zum aktuellen Zeitpunkt wird jedoch nur die Variable `TargetFramework` unterstützt.</span><span class="sxs-lookup"><span data-stu-id="3ccee-161">However, at presently, only the `TargetFramework` variable is supported.</span></span>

<span data-ttu-id="3ccee-162">Angenommen, Ihre Zielgruppen lauten `netstandard1.4` und `net452`, die vorhandene Abhängigkeit gilt jedoch nur für `net452`.</span><span class="sxs-lookup"><span data-stu-id="3ccee-162">For example, say you're targeting `netstandard1.4` as well as `net452` but have a dependency that is applicable only for `net452`.</span></span> <span data-ttu-id="3ccee-163">In diesem Fall sollte diese unnötige Abhängigkeit nicht zu einem `netstandard1.4`-Projekt hinzugefügt werden, in dem Ihr Paket verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="3ccee-163">In this case you don't want a `netstandard1.4` project that's consuming your package to add that unnecessary dependency.</span></span> <span data-ttu-id="3ccee-164">Sie geben in der `PackageReference` eine Bedingung an, um dies zu verhindern, die wie folgt lautet:</span><span class="sxs-lookup"><span data-stu-id="3ccee-164">To prevent this, you specify a condition on the `PackageReference` as follows:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="3ccee-165">Ein Paket, das in diesem Projekt erstellt wurde, zeigt an, dass die Datei „Newtonsoft.json“ nur als Abhängigkeit für ein `net452`-Ziel enthalten ist:</span><span class="sxs-lookup"><span data-stu-id="3ccee-165">A package built using this project will show that Newtonsoft.json is included as a dependency only for a `net452` target:</span></span>

![Das Ergebnis der Anwendung einer Bedingung auf die PackageReference mit VS2017](media/PackageReference-Condition.png)

<span data-ttu-id="3ccee-167">Bedingungen können auch auf der `ItemGroup`-Ebene angewendet werden und gelten dann für alle untergeordneten `PackageReference`-Elemente:</span><span class="sxs-lookup"><span data-stu-id="3ccee-167">Conditions can also be applied at the `ItemGroup` level and will apply to all children `PackageReference` elements:</span></span>

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```
