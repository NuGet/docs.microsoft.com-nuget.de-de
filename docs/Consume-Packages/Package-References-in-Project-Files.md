---
title: NuGet-PackageReference in Visual Studio-Projektdateien | Microsoft-Dokumentation
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 7/17/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 5a554e9d-1266-48c2-92e8-6dd00b1d6810
description: "Details zu NuGet-PackageReference in Projektdateien unterstützt durch NuGet 4.0 und höher und VS2017"
keywords: "Abhängigkeiten von NuGet-Paketen, Paketverweise, Projektdateien, PackageReference, „packages.config“, „project.json“, VS2017, Visual Studio 2017, NuGet 4"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 275957c94e4a4bb45f359cd48816acf4f286ebad
ms.sourcegitcommit: a40c1c1cc05a46410f317a72f695ad1d80f39fa2
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/05/2018
---
# <a name="package-references-packagereference-in-project-files"></a><span data-ttu-id="7c223-104">Paketverweise (PackageReference) in Projektdateien</span><span class="sxs-lookup"><span data-stu-id="7c223-104">Package references (PackageReference) in project files</span></span>

<span data-ttu-id="7c223-105">Mit Paketverweisen über den `PackageReference`-Knoten können Sie NuGet-Abhängigkeiten direkt innerhalb von Projektdateien verwalten und benötigen keine separate Datei `packages.config` oder `project.json`.</span><span class="sxs-lookup"><span data-stu-id="7c223-105">Package references, using the `PackageReference` node, allow you to manage NuGet dependencies directly within project files, rather than needing a separate `packages.config` or `project.json` file.</span></span> <span data-ttu-id="7c223-106">Diese Methode hat keine Auswirkungen auf andere Aspekte von NuGet; Einstellungen in Dateien vom Typ `NuGet.Config` (einschließlich Paketquellen) gelten beispielsweise weiterhin wie unter [Configuring NuGet Behavior (Konfigurieren des NuGet-Verhaltens)](Configuring-NuGet-Behavior.md) beschrieben.</span><span class="sxs-lookup"><span data-stu-id="7c223-106">This method doesn't affect other aspects of NuGet; for example, settings in `NuGet.Config` files (including package sources) are still applied as explained in [Configuring NuGet Behavior](Configuring-NuGet-Behavior.md).</span></span>

> [!Important]
> <span data-ttu-id="7c223-107">Zum aktuellen Zeitpunkt werden Paketverweise nur in Visual Studio 2017, für .NET Core-Projekte, .NET Standard-Projekte und UWP-Projekte für Windows 10 Build 15063 (Creators Update) unterstützt.</span><span class="sxs-lookup"><span data-stu-id="7c223-107">At present, package references are supported in Visual Studio 2017 only, for .NET Core projects, .NET Standard projects, and UWP projects targeting Windows 10 Build 15063 (Creators Update).</span></span>

<span data-ttu-id="7c223-108">Der `PackageReference`-Ansatz ermöglicht Ihnen die Verwendung von MSBuild-Bedingungen für die Auswahl von Paketverweisen pro Zielframework, Konfiguration, Plattform oder anderen Gruppierungen.</span><span class="sxs-lookup"><span data-stu-id="7c223-108">The `PackageReference` approach allows you to use MSBuild conditions to choose package references per target framework, configuration, platform, or other groupings.</span></span> <span data-ttu-id="7c223-109">Zudem lässt er eine präzise Steuerung der Abhängigkeiten und des Inhaltsflusses zu.</span><span class="sxs-lookup"><span data-stu-id="7c223-109">It also allows for fine-grained control over dependencies and content flow.</span></span> <span data-ttu-id="7c223-110">In Bezug auf das Verhalten und die [Abhängigkeitsauflösung](Dependency-Resolution.md) entspricht der Ansatz der Verwendung von `project.json`.</span><span class="sxs-lookup"><span data-stu-id="7c223-110">In terms of behavior and [dependency resolution](Dependency-Resolution.md), it's the same as using `project.json`.</span></span>

<span data-ttu-id="7c223-111">Weitere Einzelheiten zur Integration von MSBuild mit Paketverweisen in Projektdateien finden Sie unter [NuGet pack and restore as MSBuild targets (NuGet-Befehle „pack“ und „restore“ als MSBuild-Ziele)](../schema/msbuild-targets.md).</span><span class="sxs-lookup"><span data-stu-id="7c223-111">For more details on the integration of MSBuild with package references in project files, see [NuGet pack and restore as MSBuild targets](../schema/msbuild-targets.md).</span></span>

## <a name="adding-a-packagereference"></a><span data-ttu-id="7c223-112">Hinzufügen einer PackageReference</span><span class="sxs-lookup"><span data-stu-id="7c223-112">Adding a PackageReference</span></span>

<span data-ttu-id="7c223-113">Fügen Sie mit der folgenden Syntax eine Abhängigkeit in Ihrer Projektdatei hinzu:</span><span class="sxs-lookup"><span data-stu-id="7c223-113">Add a dependency in your project file using the following syntax:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />    
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a><span data-ttu-id="7c223-114">Steuern die Abhängigkeitsversion</span><span class="sxs-lookup"><span data-stu-id="7c223-114">Controlling dependency version</span></span>

<span data-ttu-id="7c223-115">Die Konvention für die Angabe der Version eines Pakets entspricht der Verwendung von `packages.config` oder `project.json`:</span><span class="sxs-lookup"><span data-stu-id="7c223-115">The convention for specifying the version of a package is the same as when using `packages.config` or `project.json`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="7c223-116">Im obigen Beispiel steht 3.6.0 für eine beliebige Version >= 3.6.0, wobei die niedrigste Version bevorzugt wird, wie unter [Paketversionsverwaltung](../reference/package-versioning.md#version-ranges-and-wildcards) beschrieben.</span><span class="sxs-lookup"><span data-stu-id="7c223-116">In the example above, 3.6.0 means any version that is >=3.6.0 with preference for the lowest version, as described on [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards).</span></span>

## <a name="floating-versions"></a><span data-ttu-id="7c223-117">Unverankerte Versionen</span><span class="sxs-lookup"><span data-stu-id="7c223-117">Floating Versions</span></span>

<span data-ttu-id="7c223-118">[Unverankerte Versionen](../consume-packages/dependency-resolution.md#floating-versions) werden mit `PackageReference` unterstützt:</span><span class="sxs-lookup"><span data-stu-id="7c223-118">[Floating versions](../consume-packages/dependency-resolution.md#floating-versions) are supported with `PackageReference`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a><span data-ttu-id="7c223-119">Steuern von Abhängigkeitsobjekten</span><span class="sxs-lookup"><span data-stu-id="7c223-119">Controlling dependency assets</span></span>

<span data-ttu-id="7c223-120">Sie verwenden eine Abhängigkeit möglicherweise rein als Entwicklungsumgebung und möchten diese nicht für Projekte verfügbar machen, die Ihr Paket nutzen.</span><span class="sxs-lookup"><span data-stu-id="7c223-120">You might be using a dependency purely as a development harness and might not want to expose that to projects that will consume your package.</span></span> <span data-ttu-id="7c223-121">In diesem Szenario können Sie dieses Verhalten über die `PrivateAssets`-Metadaten steuern.</span><span class="sxs-lookup"><span data-stu-id="7c223-121">In this scenario, you can use the `PrivateAssets` metadata to control this behavior.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="7c223-122">Mit den folgenden Metadatentags werden Abhängigkeitsobjekte gesteuert:</span><span class="sxs-lookup"><span data-stu-id="7c223-122">The following metadata tags control dependency assets:</span></span>

| <span data-ttu-id="7c223-123">Tag</span><span class="sxs-lookup"><span data-stu-id="7c223-123">Tag</span></span> | <span data-ttu-id="7c223-124">description</span><span class="sxs-lookup"><span data-stu-id="7c223-124">Description</span></span> | <span data-ttu-id="7c223-125">Standardwert</span><span class="sxs-lookup"><span data-stu-id="7c223-125">Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7c223-126">IncludeAssets</span><span class="sxs-lookup"><span data-stu-id="7c223-126">IncludeAssets</span></span> | <span data-ttu-id="7c223-127">Diese Objekte werden verbraucht</span><span class="sxs-lookup"><span data-stu-id="7c223-127">These assets will be consumed</span></span> | <span data-ttu-id="7c223-128">alle</span><span class="sxs-lookup"><span data-stu-id="7c223-128">all</span></span> |
| <span data-ttu-id="7c223-129">ExcludeAssets</span><span class="sxs-lookup"><span data-stu-id="7c223-129">ExcludeAssets</span></span> | <span data-ttu-id="7c223-130">Diese Objekte werden nicht verbraucht</span><span class="sxs-lookup"><span data-stu-id="7c223-130">These assets will not be consumed</span></span> | <span data-ttu-id="7c223-131">Keine</span><span class="sxs-lookup"><span data-stu-id="7c223-131">none</span></span> | 
| <span data-ttu-id="7c223-132">PrivateAssets</span><span class="sxs-lookup"><span data-stu-id="7c223-132">PrivateAssets</span></span> | <span data-ttu-id="7c223-133">Diese Objekte werden verbraucht, aber nicht in das übergeordnete Projekt übertragen</span><span class="sxs-lookup"><span data-stu-id="7c223-133">These assets will be consumed but won't flow to the parent project</span></span> | <span data-ttu-id="7c223-134">contentfiles;analyzers;build</span><span class="sxs-lookup"><span data-stu-id="7c223-134">contentfiles;analyzers;build</span></span> |


<span data-ttu-id="7c223-135">Folgende Werte sind für diese Tags zulässig, wobei mehrere Werte durch ein Semikolon (;) getrennt sind; eine Ausnahme stellen `all` und `none` dar, die nur alleine dargestellt werden dürfen:</span><span class="sxs-lookup"><span data-stu-id="7c223-135">Allowable values for these tags are as follows, with multiple values separated by a semicolon except with `all` and `none` which must appear by themselves:</span></span>

| <span data-ttu-id="7c223-136">Wert</span><span class="sxs-lookup"><span data-stu-id="7c223-136">Value</span></span> | <span data-ttu-id="7c223-137">description</span><span class="sxs-lookup"><span data-stu-id="7c223-137">Description</span></span> |
| --- | ---
| <span data-ttu-id="7c223-138">compile</span><span class="sxs-lookup"><span data-stu-id="7c223-138">compile</span></span> | <span data-ttu-id="7c223-139">Inhalte des Ordners `lib`</span><span class="sxs-lookup"><span data-stu-id="7c223-139">Contents of the `lib` folder</span></span> |
| <span data-ttu-id="7c223-140">Laufzeit</span><span class="sxs-lookup"><span data-stu-id="7c223-140">runtime</span></span> | <span data-ttu-id="7c223-141">Inhalte des Ordners `runtime`</span><span class="sxs-lookup"><span data-stu-id="7c223-141">Contents of the `runtime` folder</span></span> |
| <span data-ttu-id="7c223-142">contentFiles</span><span class="sxs-lookup"><span data-stu-id="7c223-142">contentFiles</span></span> | <span data-ttu-id="7c223-143">Inhalte des Ordners `contentfiles`</span><span class="sxs-lookup"><span data-stu-id="7c223-143">Contents of the `contentfiles` folder</span></span> |
| <span data-ttu-id="7c223-144">Build</span><span class="sxs-lookup"><span data-stu-id="7c223-144">build</span></span> | <span data-ttu-id="7c223-145">Eigenschaften und Ziele im Ordner `build`</span><span class="sxs-lookup"><span data-stu-id="7c223-145">Props and targets in the `build` folder</span></span> |
| <span data-ttu-id="7c223-146">Analysetools</span><span class="sxs-lookup"><span data-stu-id="7c223-146">analyzers</span></span> | <span data-ttu-id="7c223-147">.NET-Analystetools</span><span class="sxs-lookup"><span data-stu-id="7c223-147">.NET analyzers</span></span> |
| <span data-ttu-id="7c223-148">Systemeigen</span><span class="sxs-lookup"><span data-stu-id="7c223-148">native</span></span> | <span data-ttu-id="7c223-149">Inhalte des Ordners `native`</span><span class="sxs-lookup"><span data-stu-id="7c223-149">Contents of the `native` folder</span></span> |
| <span data-ttu-id="7c223-150">Keine</span><span class="sxs-lookup"><span data-stu-id="7c223-150">none</span></span> | <span data-ttu-id="7c223-151">Keiner der obigen Werte wird verwendet.</span><span class="sxs-lookup"><span data-stu-id="7c223-151">None of the above are used.</span></span> |
| <span data-ttu-id="7c223-152">alle</span><span class="sxs-lookup"><span data-stu-id="7c223-152">all</span></span> | <span data-ttu-id="7c223-153">Alle oben genannten Werte (mit Ausnahme von `none`)</span><span class="sxs-lookup"><span data-stu-id="7c223-153">All of the above (except `none`)</span></span> |

<span data-ttu-id="7c223-154">Im folgenden Beispiel wird im Projekt bis auf die Inhaltsdateien aus dem Paket alles verwendet, und alles bis auf die Inhaltsdateien und Analysetools wird in das übergeordnete Projekt übertragen.</span><span class="sxs-lookup"><span data-stu-id="7c223-154">In the following example, everything except the content files from the package would be consumed by the project and everything except content files and analyzers would flow to the parent project.</span></span>

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

<span data-ttu-id="7c223-155">Beachten Sie Folgendes: Da `build` nicht in `PrivateAssets` enthalten ist, *werden* Ziele und Eigenschaften an das übergeordnete Projekt übergeben.</span><span class="sxs-lookup"><span data-stu-id="7c223-155">Note that because `build` is not included with `PrivateAssets`, targets and props *will* flow to the parent project.</span></span> <span data-ttu-id="7c223-156">Angenommen, der obenstehende Verweis wird in einem Projekt verwendet, in dem ein NuGet-Paket mit dem Namen AppLogger erstellt wird.</span><span class="sxs-lookup"><span data-stu-id="7c223-156">Consider, for example, that the reference above is used in a project that builds a NuGet package called AppLogger.</span></span> <span data-ttu-id="7c223-157">AppLogger kann die Ziele und Eigenschaften aus `Contoso.Utility.UsefulStuff` verarbeiten, wie Projekte, die AppLogger verarbeiten.</span><span class="sxs-lookup"><span data-stu-id="7c223-157">AppLogger can consume the targets and props from `Contoso.Utility.UsefulStuff`, as can projects that consume AppLogger.</span></span>

## <a name="adding-a-packagereference-condition"></a><span data-ttu-id="7c223-158">Hinzufügen einer PackageReference-Bedingung</span><span class="sxs-lookup"><span data-stu-id="7c223-158">Adding a PackageReference condition</span></span>

<span data-ttu-id="7c223-159">Sie können mithilfe einer Bedingung steuern, ob ein Paket eingeschlossen wird. Dabei kann in Bedingungen eine beliebige MSBuild-Variable oder eine in der Ziel- oder Eigenschaftendatei definierte Variable verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="7c223-159">You can use a condition to control whether a package is included, where conditions can use any MSBuild variable or a variable defined in the targets or props file.</span></span> <span data-ttu-id="7c223-160">Zum aktuellen Zeitpunkt wird jedoch nur die Variable `TargetFramework` unterstützt.</span><span class="sxs-lookup"><span data-stu-id="7c223-160">However, at presently, only the `TargetFramework` variable is supported.</span></span>

<span data-ttu-id="7c223-161">Angenommen, Ihre Zielgruppen lauten `netstandard1.4` und `net452`, die vorhandene Abhängigkeit gilt jedoch nur für `net452`.</span><span class="sxs-lookup"><span data-stu-id="7c223-161">For example, say you're targeting `netstandard1.4` as well as `net452` but have a dependency that is applicable only for `net452`.</span></span> <span data-ttu-id="7c223-162">In diesem Fall sollte diese unnötige Abhängigkeit nicht zu einem `netstandard1.4`-Projekt hinzugefügt werden, in dem Ihr Paket verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="7c223-162">In this case you don't want a `netstandard1.4` project that's consuming your package to add that unnecessary dependency.</span></span> <span data-ttu-id="7c223-163">Sie geben in der `PackageReference` eine Bedingung an, um dies zu verhindern, die wie folgt lautet:</span><span class="sxs-lookup"><span data-stu-id="7c223-163">To prevent this, you specify a condition on the `PackageReference` as follows:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />    
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="7c223-164">Ein Paket, das in diesem Projekt erstellt wurde, zeigt an, dass die Datei „Newtonsoft.json“ nur als Abhängigkeit für ein `net452`-Ziel enthalten ist:</span><span class="sxs-lookup"><span data-stu-id="7c223-164">A package built using this project will show that Newtonsoft.json is included as a dependency only for a `net452` target:</span></span>

![Das Ergebnis der Anwendung einer Bedingung auf die PackageReference mit VS2017](media/PackageReference-Condition.png)

<span data-ttu-id="7c223-166">Bedingungen können auch auf der `ItemGroup`-Ebene angewendet werden und gelten dann für alle untergeordneten `PackageReference`-Elemente:</span><span class="sxs-lookup"><span data-stu-id="7c223-166">Conditions can also be applied at the `ItemGroup` level and will apply to all children `PackageReference` elements:</span></span>

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```
