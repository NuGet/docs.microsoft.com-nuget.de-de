---
title: NuGet-Format „PackageReference“ (Paketverweise in Projektdateien)
description: Details zu NuGet-PackageReference in Projektdateien unterstützt durch NuGet 4.0 und höher und VS2017 sowie .NET Core 2.0
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: 8f277a8af7f988d6fdcfa75c43a10b3792c2ae22
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="package-references-packagereference-in-project-files"></a><span data-ttu-id="af49f-103">Paketverweise (PackageReference) in Projektdateien</span><span class="sxs-lookup"><span data-stu-id="af49f-103">Package references (PackageReference) in project files</span></span>

<span data-ttu-id="af49f-104">Paketverweise über den `PackageReference`-Knoten verwalten NuGet-Abhängigkeiten direkt in den Projektdateien. Es wird keine separate `packages.config`-Datei benötigt.</span><span class="sxs-lookup"><span data-stu-id="af49f-104">Package references, using the `PackageReference` node, manage NuGet dependencies directly within project files (as opposed to a separate `packages.config` file).</span></span> <span data-ttu-id="af49f-105">Wenn das PackageReference-Format verwendet wird, hat dies bei dessen Aufruf keine Auswirkungen auf andere Aspekte von NuGet. Einstellungen in Dateien vom Typ `NuGet.Config` (einschließlich Paketquellen) gelten beispielsweise weiterhin wie unter [Konfigurieren des NuGet-Verhaltens](configuring-nuget-behavior.md) beschrieben.</span><span class="sxs-lookup"><span data-stu-id="af49f-105">Using PackageReference, as it's called, doesn't affect other aspects of NuGet; for example, settings in `NuGet.Config` files (including package sources) are still applied as explained in [Configuring NuGet Behavior](configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="af49f-106">Mit PackageReference können Sie auch MSBuild-Bedingungen für die Auswahl von Paketverweisen pro Zielframework, Konfiguration, Plattform oder anderen Gruppierungen verwenden.</span><span class="sxs-lookup"><span data-stu-id="af49f-106">With PackageReference, you can also use MSBuild conditions to choose package references per target framework, configuration, platform, or other groupings.</span></span> <span data-ttu-id="af49f-107">Zudem lässt er eine präzise Steuerung der Abhängigkeiten und des Inhaltsflusses zu.</span><span class="sxs-lookup"><span data-stu-id="af49f-107">It also allows for fine-grained control over dependencies and content flow.</span></span> <span data-ttu-id="af49f-108">(Informationen dazu finden Sie unter [NuGet pack and restore as MSBuild targets – restore target (Packen und Wiederherstellen von NuGet als MSBuild-Ziele: Paketwiederherstellung)](../reference/msbuild-targets.md).)</span><span class="sxs-lookup"><span data-stu-id="af49f-108">(See For more details [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).)</span></span>

<span data-ttu-id="af49f-109">Außer für C++ UWP-Projekte wird PackageReference standardmäßig nur in .NET Core-, .NET Standard- und UWP-Projekten für Windows 10 Build 15063 (Creators Update) und höher unterstützt.</span><span class="sxs-lookup"><span data-stu-id="af49f-109">By default, PackageReference is used for .NET Core projects, .NET Standard projects, and UWP projects targeting Windows 10 Build 15063 (Creators Update) and later, with the exception of C++ UWP projects.</span></span> <span data-ttu-id="af49f-110">Vollständige .NET Framework-Projekte unterstützen PackageReference. Standardmäßig wird jedoch `packages.config` verwendet.</span><span class="sxs-lookup"><span data-stu-id="af49f-110">.NET full framework projects support PackageReference, but currently default to `packages.config`.</span></span> <span data-ttu-id="af49f-111">Migrieren Sie zur Verwendung von PackageReference die Abhängigkeiten von `packages.config` zu Ihrer Projektdatei. Entfernen Sie anschließend packages.config.</span><span class="sxs-lookup"><span data-stu-id="af49f-111">To use PackageReference, migrate the dependencies from `packages.config` into your project file, then remove packages.config.</span></span>

## <a name="adding-a-packagereference"></a><span data-ttu-id="af49f-112">Hinzufügen einer PackageReference</span><span class="sxs-lookup"><span data-stu-id="af49f-112">Adding a PackageReference</span></span>

<span data-ttu-id="af49f-113">Fügen Sie mit der folgenden Syntax eine Abhängigkeit in Ihrer Projektdatei hinzu:</span><span class="sxs-lookup"><span data-stu-id="af49f-113">Add a dependency in your project file using the following syntax:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a><span data-ttu-id="af49f-114">Steuern die Abhängigkeitsversion</span><span class="sxs-lookup"><span data-stu-id="af49f-114">Controlling dependency version</span></span>

<span data-ttu-id="af49f-115">Die Konvention für die Angabe der Version eines Pakets entspricht der Verwendung von `packages.config`:</span><span class="sxs-lookup"><span data-stu-id="af49f-115">The convention for specifying the version of a package is the same as when using `packages.config`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="af49f-116">Im obigen Beispiel steht 3.6.0 für eine beliebige Version >= 3.6.0, wobei die niedrigste Version bevorzugt wird, wie unter [Paketversionsverwaltung](../reference/package-versioning.md#version-ranges-and-wildcards) beschrieben.</span><span class="sxs-lookup"><span data-stu-id="af49f-116">In the example above, 3.6.0 means any version that is >=3.6.0 with preference for the lowest version, as described on [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards).</span></span>

## <a name="floating-versions"></a><span data-ttu-id="af49f-117">Unverankerte Versionen</span><span class="sxs-lookup"><span data-stu-id="af49f-117">Floating Versions</span></span>

<span data-ttu-id="af49f-118">[Unverankerte Versionen](../consume-packages/dependency-resolution.md#floating-versions) werden mit `PackageReference` unterstützt:</span><span class="sxs-lookup"><span data-stu-id="af49f-118">[Floating versions](../consume-packages/dependency-resolution.md#floating-versions) are supported with `PackageReference`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a><span data-ttu-id="af49f-119">Steuern von Abhängigkeitsobjekten</span><span class="sxs-lookup"><span data-stu-id="af49f-119">Controlling dependency assets</span></span>

<span data-ttu-id="af49f-120">Sie verwenden eine Abhängigkeit möglicherweise rein als Entwicklungsumgebung und möchten diese nicht für Projekte verfügbar machen, die Ihr Paket nutzen.</span><span class="sxs-lookup"><span data-stu-id="af49f-120">You might be using a dependency purely as a development harness and might not want to expose that to projects that will consume your package.</span></span> <span data-ttu-id="af49f-121">In diesem Szenario können Sie dieses Verhalten über die `PrivateAssets`-Metadaten steuern.</span><span class="sxs-lookup"><span data-stu-id="af49f-121">In this scenario, you can use the `PrivateAssets` metadata to control this behavior.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="af49f-122">Mit den folgenden Metadatentags werden Abhängigkeitsobjekte gesteuert:</span><span class="sxs-lookup"><span data-stu-id="af49f-122">The following metadata tags control dependency assets:</span></span>

| <span data-ttu-id="af49f-123">Tag</span><span class="sxs-lookup"><span data-stu-id="af49f-123">Tag</span></span> | <span data-ttu-id="af49f-124">description</span><span class="sxs-lookup"><span data-stu-id="af49f-124">Description</span></span> | <span data-ttu-id="af49f-125">Standardwert</span><span class="sxs-lookup"><span data-stu-id="af49f-125">Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="af49f-126">IncludeAssets</span><span class="sxs-lookup"><span data-stu-id="af49f-126">IncludeAssets</span></span> | <span data-ttu-id="af49f-127">Diese Objekte werden verbraucht</span><span class="sxs-lookup"><span data-stu-id="af49f-127">These assets will be consumed</span></span> | <span data-ttu-id="af49f-128">alle</span><span class="sxs-lookup"><span data-stu-id="af49f-128">all</span></span> |
| <span data-ttu-id="af49f-129">ExcludeAssets</span><span class="sxs-lookup"><span data-stu-id="af49f-129">ExcludeAssets</span></span> | <span data-ttu-id="af49f-130">Diese Objekte werden nicht verbraucht</span><span class="sxs-lookup"><span data-stu-id="af49f-130">These assets will not be consumed</span></span> | <span data-ttu-id="af49f-131">Keine</span><span class="sxs-lookup"><span data-stu-id="af49f-131">none</span></span> |
| <span data-ttu-id="af49f-132">PrivateAssets</span><span class="sxs-lookup"><span data-stu-id="af49f-132">PrivateAssets</span></span> | <span data-ttu-id="af49f-133">Diese Objekte werden verbraucht, aber nicht in das übergeordnete Projekt übertragen</span><span class="sxs-lookup"><span data-stu-id="af49f-133">These assets will be consumed but won't flow to the parent project</span></span> | <span data-ttu-id="af49f-134">contentfiles;analyzers;build</span><span class="sxs-lookup"><span data-stu-id="af49f-134">contentfiles;analyzers;build</span></span> |

<span data-ttu-id="af49f-135">Folgende Werte sind für diese Tags zulässig, wobei mehrere Werte durch ein Semikolon (;) getrennt sind; eine Ausnahme stellen `all` und `none` dar, die nur alleine dargestellt werden dürfen:</span><span class="sxs-lookup"><span data-stu-id="af49f-135">Allowable values for these tags are as follows, with multiple values separated by a semicolon except with `all` and `none` which must appear by themselves:</span></span>

| <span data-ttu-id="af49f-136">Wert</span><span class="sxs-lookup"><span data-stu-id="af49f-136">Value</span></span> | <span data-ttu-id="af49f-137">description</span><span class="sxs-lookup"><span data-stu-id="af49f-137">Description</span></span> |
| --- | ---
| <span data-ttu-id="af49f-138">compile</span><span class="sxs-lookup"><span data-stu-id="af49f-138">compile</span></span> | <span data-ttu-id="af49f-139">Inhalt des Ordners `lib` und steuert, ob Ihr Projekt anhand der Assemblys im Ordner kompiliert werden kann</span><span class="sxs-lookup"><span data-stu-id="af49f-139">Contents of the `lib` folder and controls whether your project can compile against the assemblies within the folder</span></span> |
| <span data-ttu-id="af49f-140">Laufzeit</span><span class="sxs-lookup"><span data-stu-id="af49f-140">runtime</span></span> | <span data-ttu-id="af49f-141">Inhalt der Ordner `lib` und `runtimes` und steuert, ob diese Assemblys in das Buildausgabeverzeichnis kopiert werden</span><span class="sxs-lookup"><span data-stu-id="af49f-141">Contents of the `lib` and `runtimes` folder and controls whether these assemblies will be copied out to the build output directory</span></span> |
| <span data-ttu-id="af49f-142">contentFiles</span><span class="sxs-lookup"><span data-stu-id="af49f-142">contentFiles</span></span> | <span data-ttu-id="af49f-143">Inhalte des Ordners `contentfiles`</span><span class="sxs-lookup"><span data-stu-id="af49f-143">Contents of the `contentfiles` folder</span></span> |
| <span data-ttu-id="af49f-144">Build</span><span class="sxs-lookup"><span data-stu-id="af49f-144">build</span></span> | <span data-ttu-id="af49f-145">Eigenschaften und Ziele im Ordner `build`</span><span class="sxs-lookup"><span data-stu-id="af49f-145">Props and targets in the `build` folder</span></span> |
| <span data-ttu-id="af49f-146">Analysetools</span><span class="sxs-lookup"><span data-stu-id="af49f-146">analyzers</span></span> | <span data-ttu-id="af49f-147">.NET-Analystetools</span><span class="sxs-lookup"><span data-stu-id="af49f-147">.NET analyzers</span></span> |
| <span data-ttu-id="af49f-148">Systemeigen</span><span class="sxs-lookup"><span data-stu-id="af49f-148">native</span></span> | <span data-ttu-id="af49f-149">Inhalte des Ordners `native`</span><span class="sxs-lookup"><span data-stu-id="af49f-149">Contents of the `native` folder</span></span> |
| <span data-ttu-id="af49f-150">Keine</span><span class="sxs-lookup"><span data-stu-id="af49f-150">none</span></span> | <span data-ttu-id="af49f-151">Keiner der obigen Werte wird verwendet.</span><span class="sxs-lookup"><span data-stu-id="af49f-151">None of the above are used.</span></span> |
| <span data-ttu-id="af49f-152">alle</span><span class="sxs-lookup"><span data-stu-id="af49f-152">all</span></span> | <span data-ttu-id="af49f-153">Alle oben genannten Werte (mit Ausnahme von `none`)</span><span class="sxs-lookup"><span data-stu-id="af49f-153">All of the above (except `none`)</span></span> |

<span data-ttu-id="af49f-154">Im folgenden Beispiel wird im Projekt bis auf die Inhaltsdateien aus dem Paket alles verwendet, und alles bis auf die Inhaltsdateien und Analysetools wird in das übergeordnete Projekt übertragen.</span><span class="sxs-lookup"><span data-stu-id="af49f-154">In the following example, everything except the content files from the package would be consumed by the project and everything except content files and analyzers would flow to the parent project.</span></span>

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

<span data-ttu-id="af49f-155">Beachten Sie Folgendes: Da `build` nicht in `PrivateAssets` enthalten ist, *werden* Ziele und Eigenschaften an das übergeordnete Projekt übergeben.</span><span class="sxs-lookup"><span data-stu-id="af49f-155">Note that because `build` is not included with `PrivateAssets`, targets and props *will* flow to the parent project.</span></span> <span data-ttu-id="af49f-156">Angenommen, der obenstehende Verweis wird in einem Projekt verwendet, in dem ein NuGet-Paket mit dem Namen AppLogger erstellt wird.</span><span class="sxs-lookup"><span data-stu-id="af49f-156">Consider, for example, that the reference above is used in a project that builds a NuGet package called AppLogger.</span></span> <span data-ttu-id="af49f-157">AppLogger kann die Ziele und Eigenschaften aus `Contoso.Utility.UsefulStuff` verarbeiten, wie Projekte, die AppLogger verarbeiten.</span><span class="sxs-lookup"><span data-stu-id="af49f-157">AppLogger can consume the targets and props from `Contoso.Utility.UsefulStuff`, as can projects that consume AppLogger.</span></span>

## <a name="adding-a-packagereference-condition"></a><span data-ttu-id="af49f-158">Hinzufügen einer PackageReference-Bedingung</span><span class="sxs-lookup"><span data-stu-id="af49f-158">Adding a PackageReference condition</span></span>

<span data-ttu-id="af49f-159">Sie können mithilfe einer Bedingung steuern, ob ein Paket eingeschlossen wird. Dabei kann in Bedingungen eine beliebige MSBuild-Variable oder eine in der Ziel- oder Eigenschaftendatei definierte Variable verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="af49f-159">You can use a condition to control whether a package is included, where conditions can use any MSBuild variable or a variable defined in the targets or props file.</span></span> <span data-ttu-id="af49f-160">Zum aktuellen Zeitpunkt wird jedoch nur die Variable `TargetFramework` unterstützt.</span><span class="sxs-lookup"><span data-stu-id="af49f-160">However, at presently, only the `TargetFramework` variable is supported.</span></span>

<span data-ttu-id="af49f-161">Angenommen, Ihre Zielgruppen lauten `netstandard1.4` und `net452`, die vorhandene Abhängigkeit gilt jedoch nur für `net452`.</span><span class="sxs-lookup"><span data-stu-id="af49f-161">For example, say you're targeting `netstandard1.4` as well as `net452` but have a dependency that is applicable only for `net452`.</span></span> <span data-ttu-id="af49f-162">In diesem Fall sollte diese unnötige Abhängigkeit nicht zu einem `netstandard1.4`-Projekt hinzugefügt werden, in dem Ihr Paket verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="af49f-162">In this case you don't want a `netstandard1.4` project that's consuming your package to add that unnecessary dependency.</span></span> <span data-ttu-id="af49f-163">Sie geben in der `PackageReference` eine Bedingung an, um dies zu verhindern, die wie folgt lautet:</span><span class="sxs-lookup"><span data-stu-id="af49f-163">To prevent this, you specify a condition on the `PackageReference` as follows:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="af49f-164">Ein Paket, das in diesem Projekt erstellt wurde, zeigt an, dass die Datei „Newtonsoft.json“ nur als Abhängigkeit für ein `net452`-Ziel enthalten ist:</span><span class="sxs-lookup"><span data-stu-id="af49f-164">A package built using this project will show that Newtonsoft.json is included as a dependency only for a `net452` target:</span></span>

![Das Ergebnis der Anwendung einer Bedingung auf die PackageReference mit VS2017](media/PackageReference-Condition.png)

<span data-ttu-id="af49f-166">Bedingungen können auch auf der `ItemGroup`-Ebene angewendet werden und gelten dann für alle untergeordneten `PackageReference`-Elemente:</span><span class="sxs-lookup"><span data-stu-id="af49f-166">Conditions can also be applied at the `ItemGroup` level and will apply to all children `PackageReference` elements:</span></span>

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```
