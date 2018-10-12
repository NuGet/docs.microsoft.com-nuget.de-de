---
title: NuGet-Format „PackageReference“ (Paketverweise in Projektdateien)
description: Details zu NuGet-PackageReference in Projektdateien unterstützt durch NuGet 4.0 und höher und VS2017 sowie .NET Core 2.0
author: karann-msft
ms.author: karann
ms.date: 03/16/2018
ms.topic: conceptual
ms.openlocfilehash: 648b2679538e38b2451d7857beb5d070deeef7c5
ms.sourcegitcommit: 47858da1103848cc1b15bdc00ac7219c0ee4a6a0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/12/2018
ms.locfileid: "44516203"
---
# <a name="package-references-packagereference-in-project-files"></a><span data-ttu-id="04a8c-103">Paketverweise (PackageReference) in Projektdateien</span><span class="sxs-lookup"><span data-stu-id="04a8c-103">Package references (PackageReference) in project files</span></span>

<span data-ttu-id="04a8c-104">Paketverweise über den `PackageReference`-Knoten verwalten NuGet-Abhängigkeiten direkt in den Projektdateien. Es wird keine separate `packages.config`-Datei benötigt.</span><span class="sxs-lookup"><span data-stu-id="04a8c-104">Package references, using the `PackageReference` node, manage NuGet dependencies directly within project files (as opposed to a separate `packages.config` file).</span></span> <span data-ttu-id="04a8c-105">Wenn das PackageReference-Format verwendet wird, hat dies bei dessen Aufruf keine Auswirkungen auf andere Aspekte von NuGet. Einstellungen in Dateien vom Typ `NuGet.Config` (einschließlich Paketquellen) gelten beispielsweise weiterhin wie unter [Konfigurieren des NuGet-Verhaltens](configuring-nuget-behavior.md) beschrieben.</span><span class="sxs-lookup"><span data-stu-id="04a8c-105">Using PackageReference, as it's called, doesn't affect other aspects of NuGet; for example, settings in `NuGet.Config` files (including package sources) are still applied as explained in [Configuring NuGet Behavior](configuring-nuget-behavior.md).</span></span>

<span data-ttu-id="04a8c-106">Mit PackageReference können Sie auch MSBuild-Bedingungen für die Auswahl von Paketverweisen pro Zielframework, Konfiguration, Plattform oder anderen Gruppierungen verwenden.</span><span class="sxs-lookup"><span data-stu-id="04a8c-106">With PackageReference, you can also use MSBuild conditions to choose package references per target framework, configuration, platform, or other groupings.</span></span> <span data-ttu-id="04a8c-107">Zudem lässt er eine präzise Steuerung der Abhängigkeiten und des Inhaltsflusses zu.</span><span class="sxs-lookup"><span data-stu-id="04a8c-107">It also allows for fine-grained control over dependencies and content flow.</span></span> <span data-ttu-id="04a8c-108">(Informationen dazu finden Sie unter [NuGet pack and restore as MSBuild targets – restore target (Packen und Wiederherstellen von NuGet als MSBuild-Ziele: Paketwiederherstellung)](../reference/msbuild-targets.md).)</span><span class="sxs-lookup"><span data-stu-id="04a8c-108">(See For more details [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md).)</span></span>

<span data-ttu-id="04a8c-109">Außer für C++ UWP-Projekte wird PackageReference standardmäßig nur in .NET Core-, .NET Standard- und UWP-Projekten für Windows 10 Build 15063 (Creators Update) und höher unterstützt.</span><span class="sxs-lookup"><span data-stu-id="04a8c-109">By default, PackageReference is used for .NET Core projects, .NET Standard projects, and UWP projects targeting Windows 10 Build 15063 (Creators Update) and later, with the exception of C++ UWP projects.</span></span> <span data-ttu-id="04a8c-110">.NET Framework-Projekte unterstützen PackageReference. Standardmäßig wird jedoch `packages.config` verwendet.</span><span class="sxs-lookup"><span data-stu-id="04a8c-110">.NET Framework projects support PackageReference, but currently default to `packages.config`.</span></span> <span data-ttu-id="04a8c-111">Migrieren Sie zur Verwendung von PackageReference die Abhängigkeiten von `packages.config` zu Ihrer Projektdatei. Entfernen Sie anschließend packages.config.</span><span class="sxs-lookup"><span data-stu-id="04a8c-111">To use PackageReference, migrate the dependencies from `packages.config` into your project file, then remove packages.config.</span></span>

## <a name="adding-a-packagereference"></a><span data-ttu-id="04a8c-112">Hinzufügen einer PackageReference</span><span class="sxs-lookup"><span data-stu-id="04a8c-112">Adding a PackageReference</span></span>

<span data-ttu-id="04a8c-113">Fügen Sie mit der folgenden Syntax eine Abhängigkeit in Ihrer Projektdatei hinzu:</span><span class="sxs-lookup"><span data-stu-id="04a8c-113">Add a dependency in your project file using the following syntax:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-version"></a><span data-ttu-id="04a8c-114">Steuern die Abhängigkeitsversion</span><span class="sxs-lookup"><span data-stu-id="04a8c-114">Controlling dependency version</span></span>

<span data-ttu-id="04a8c-115">Die Konvention für die Angabe der Version eines Pakets entspricht der Verwendung von `packages.config`:</span><span class="sxs-lookup"><span data-stu-id="04a8c-115">The convention for specifying the version of a package is the same as when using `packages.config`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="04a8c-116">Im obigen Beispiel steht 3.6.0 für eine beliebige Version >= 3.6.0, wobei die niedrigste Version bevorzugt wird, wie unter [Paketversionsverwaltung](../reference/package-versioning.md#version-ranges-and-wildcards) beschrieben.</span><span class="sxs-lookup"><span data-stu-id="04a8c-116">In the example above, 3.6.0 means any version that is >=3.6.0 with preference for the lowest version, as described on [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards).</span></span>

## <a name="using-packagereference-for-a-project-with-no-packagereferences"></a><span data-ttu-id="04a8c-117">Verwenden von PackageReference für ein Projekt ohne PackageReferences</span><span class="sxs-lookup"><span data-stu-id="04a8c-117">Using PackageReference for a project with no PackageReferences</span></span>
<span data-ttu-id="04a8c-118">Erweitert: Wenn Sie keine Pakete in einem Projekt installiert haben (keine PackageReferences in der Projektdatei oder der packages.config-Datei), aber das Projekt mit dem Format von PackageReference wiederherstellen möchten, können Sie in der Projektdatei eine RestoreProjectStyle-Projekteigenschaft auf PackageReference festlegen.</span><span class="sxs-lookup"><span data-stu-id="04a8c-118">Advanced: If you have no packages installed in a project (no PackageReferences in project file and no packages.config file), but want the project to be restored as PackageReference style, you can set a Project property RestoreProjectStyle to PackageReference in your project file.</span></span>
```xml
<PropertyGroup>
    <!--- ... -->
    <RestoreProjectStyle>PackageReference</RestoreProjectStyle>
    <!--- ... -->
</PropertyGroup>    
```
<span data-ttu-id="04a8c-119">Dies kann sich als nützlich erweisen, wenn Sie auf Projekte verweisen, die das Format von PackageReference aufweisen (vorhandene Projekte im CSPROJ- oder SDK-Format).</span><span class="sxs-lookup"><span data-stu-id="04a8c-119">This may be useful, if you reference projects which are PackageReference styled (existing csproj or SDK-style projects).</span></span> <span data-ttu-id="04a8c-120">Dadurch kann Ihr Projekt „transitiv“ auf die Pakete verweisen, auf die diese Projekte verweisen.</span><span class="sxs-lookup"><span data-stu-id="04a8c-120">This will enable packages that those projects refer to, to be "transitively" referenced by your project.</span></span>

## <a name="floating-versions"></a><span data-ttu-id="04a8c-121">Unverankerte Versionen</span><span class="sxs-lookup"><span data-stu-id="04a8c-121">Floating Versions</span></span>

<span data-ttu-id="04a8c-122">[Unverankerte Versionen](../consume-packages/dependency-resolution.md#floating-versions) werden mit `PackageReference` unterstützt:</span><span class="sxs-lookup"><span data-stu-id="04a8c-122">[Floating versions](../consume-packages/dependency-resolution.md#floating-versions) are supported with `PackageReference`:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.*" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0-beta*" />
    <!-- ... -->
</ItemGroup>
```

## <a name="controlling-dependency-assets"></a><span data-ttu-id="04a8c-123">Steuern von Abhängigkeitsobjekten</span><span class="sxs-lookup"><span data-stu-id="04a8c-123">Controlling dependency assets</span></span>

<span data-ttu-id="04a8c-124">Sie verwenden eine Abhängigkeit möglicherweise rein als Entwicklungsumgebung und möchten diese nicht für Projekte verfügbar machen, die Ihr Paket nutzen.</span><span class="sxs-lookup"><span data-stu-id="04a8c-124">You might be using a dependency purely as a development harness and might not want to expose that to projects that will consume your package.</span></span> <span data-ttu-id="04a8c-125">In diesem Szenario können Sie dieses Verhalten über die `PrivateAssets`-Metadaten steuern.</span><span class="sxs-lookup"><span data-stu-id="04a8c-125">In this scenario, you can use the `PrivateAssets` metadata to control this behavior.</span></span>

```xml
<ItemGroup>
    <!-- ... -->

    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0">
        <PrivateAssets>all</PrivateAssets>
    </PackageReference>

    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="04a8c-126">Mit den folgenden Metadatentags werden Abhängigkeitsobjekte gesteuert:</span><span class="sxs-lookup"><span data-stu-id="04a8c-126">The following metadata tags control dependency assets:</span></span>

| <span data-ttu-id="04a8c-127">Tag</span><span class="sxs-lookup"><span data-stu-id="04a8c-127">Tag</span></span> | <span data-ttu-id="04a8c-128">Beschreibung </span><span class="sxs-lookup"><span data-stu-id="04a8c-128">Description</span></span> | <span data-ttu-id="04a8c-129">Standardwert</span><span class="sxs-lookup"><span data-stu-id="04a8c-129">Default Value</span></span> |
| --- | --- | --- |
| <span data-ttu-id="04a8c-130">IncludeAssets</span><span class="sxs-lookup"><span data-stu-id="04a8c-130">IncludeAssets</span></span> | <span data-ttu-id="04a8c-131">Diese Objekte werden verbraucht</span><span class="sxs-lookup"><span data-stu-id="04a8c-131">These assets will be consumed</span></span> | <span data-ttu-id="04a8c-132">alle</span><span class="sxs-lookup"><span data-stu-id="04a8c-132">all</span></span> |
| <span data-ttu-id="04a8c-133">ExcludeAssets</span><span class="sxs-lookup"><span data-stu-id="04a8c-133">ExcludeAssets</span></span> | <span data-ttu-id="04a8c-134">Diese Objekte werden nicht verbraucht</span><span class="sxs-lookup"><span data-stu-id="04a8c-134">These assets will not be consumed</span></span> | <span data-ttu-id="04a8c-135">Keine</span><span class="sxs-lookup"><span data-stu-id="04a8c-135">none</span></span> |
| <span data-ttu-id="04a8c-136">PrivateAssets</span><span class="sxs-lookup"><span data-stu-id="04a8c-136">PrivateAssets</span></span> | <span data-ttu-id="04a8c-137">Diese Objekte werden verbraucht, aber nicht in das übergeordnete Projekt übertragen</span><span class="sxs-lookup"><span data-stu-id="04a8c-137">These assets will be consumed but won't flow to the parent project</span></span> | <span data-ttu-id="04a8c-138">contentfiles;analyzers;build</span><span class="sxs-lookup"><span data-stu-id="04a8c-138">contentfiles;analyzers;build</span></span> |

<span data-ttu-id="04a8c-139">Folgende Werte sind für diese Tags zulässig, wobei mehrere Werte durch ein Semikolon (;) getrennt sind; eine Ausnahme stellen `all` und `none` dar, die nur alleine dargestellt werden dürfen:</span><span class="sxs-lookup"><span data-stu-id="04a8c-139">Allowable values for these tags are as follows, with multiple values separated by a semicolon except with `all` and `none` which must appear by themselves:</span></span>

| <span data-ttu-id="04a8c-140">Wert</span><span class="sxs-lookup"><span data-stu-id="04a8c-140">Value</span></span> | <span data-ttu-id="04a8c-141">Beschreibung </span><span class="sxs-lookup"><span data-stu-id="04a8c-141">Description</span></span> |
| --- | ---
| <span data-ttu-id="04a8c-142">compile</span><span class="sxs-lookup"><span data-stu-id="04a8c-142">compile</span></span> | <span data-ttu-id="04a8c-143">Inhalt des Ordners `lib` und steuert, ob Ihr Projekt anhand der Assemblys im Ordner kompiliert werden kann</span><span class="sxs-lookup"><span data-stu-id="04a8c-143">Contents of the `lib` folder and controls whether your project can compile against the assemblies within the folder</span></span> |
| <span data-ttu-id="04a8c-144">Laufzeit</span><span class="sxs-lookup"><span data-stu-id="04a8c-144">runtime</span></span> | <span data-ttu-id="04a8c-145">Inhalt der Ordner `lib` und `runtimes` und steuert, ob diese Assemblys in das Buildausgabeverzeichnis kopiert werden</span><span class="sxs-lookup"><span data-stu-id="04a8c-145">Contents of the `lib` and `runtimes` folder and controls whether these assemblies will be copied out to the build output directory</span></span> |
| <span data-ttu-id="04a8c-146">contentFiles</span><span class="sxs-lookup"><span data-stu-id="04a8c-146">contentFiles</span></span> | <span data-ttu-id="04a8c-147">Inhalte des Ordners `contentfiles`</span><span class="sxs-lookup"><span data-stu-id="04a8c-147">Contents of the `contentfiles` folder</span></span> |
| <span data-ttu-id="04a8c-148">Build</span><span class="sxs-lookup"><span data-stu-id="04a8c-148">build</span></span> | <span data-ttu-id="04a8c-149">Eigenschaften und Ziele im Ordner `build`</span><span class="sxs-lookup"><span data-stu-id="04a8c-149">Props and targets in the `build` folder</span></span> |
| <span data-ttu-id="04a8c-150">Analysetools</span><span class="sxs-lookup"><span data-stu-id="04a8c-150">analyzers</span></span> | <span data-ttu-id="04a8c-151">.NET-Analystetools</span><span class="sxs-lookup"><span data-stu-id="04a8c-151">.NET analyzers</span></span> |
| <span data-ttu-id="04a8c-152">Systemeigen</span><span class="sxs-lookup"><span data-stu-id="04a8c-152">native</span></span> | <span data-ttu-id="04a8c-153">Inhalte des Ordners `native`</span><span class="sxs-lookup"><span data-stu-id="04a8c-153">Contents of the `native` folder</span></span> |
| <span data-ttu-id="04a8c-154">Keine</span><span class="sxs-lookup"><span data-stu-id="04a8c-154">none</span></span> | <span data-ttu-id="04a8c-155">Keiner der obigen Werte wird verwendet.</span><span class="sxs-lookup"><span data-stu-id="04a8c-155">None of the above are used.</span></span> |
| <span data-ttu-id="04a8c-156">alle</span><span class="sxs-lookup"><span data-stu-id="04a8c-156">all</span></span> | <span data-ttu-id="04a8c-157">Alle oben genannten Werte (mit Ausnahme von `none`)</span><span class="sxs-lookup"><span data-stu-id="04a8c-157">All of the above (except `none`)</span></span> |

<span data-ttu-id="04a8c-158">Im folgenden Beispiel wird im Projekt bis auf die Inhaltsdateien aus dem Paket alles verwendet, und alles bis auf die Inhaltsdateien und Analysetools wird in das übergeordnete Projekt übertragen.</span><span class="sxs-lookup"><span data-stu-id="04a8c-158">In the following example, everything except the content files from the package would be consumed by the project and everything except content files and analyzers would flow to the parent project.</span></span>

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

<span data-ttu-id="04a8c-159">Beachten Sie Folgendes: Da `build` nicht in `PrivateAssets` enthalten ist, *werden* Ziele und Eigenschaften an das übergeordnete Projekt übergeben.</span><span class="sxs-lookup"><span data-stu-id="04a8c-159">Note that because `build` is not included with `PrivateAssets`, targets and props *will* flow to the parent project.</span></span> <span data-ttu-id="04a8c-160">Angenommen, der obenstehende Verweis wird in einem Projekt verwendet, in dem ein NuGet-Paket mit dem Namen AppLogger erstellt wird.</span><span class="sxs-lookup"><span data-stu-id="04a8c-160">Consider, for example, that the reference above is used in a project that builds a NuGet package called AppLogger.</span></span> <span data-ttu-id="04a8c-161">AppLogger kann die Ziele und Eigenschaften aus `Contoso.Utility.UsefulStuff` verarbeiten, wie Projekte, die AppLogger verarbeiten.</span><span class="sxs-lookup"><span data-stu-id="04a8c-161">AppLogger can consume the targets and props from `Contoso.Utility.UsefulStuff`, as can projects that consume AppLogger.</span></span>

## <a name="adding-a-packagereference-condition"></a><span data-ttu-id="04a8c-162">Hinzufügen einer PackageReference-Bedingung</span><span class="sxs-lookup"><span data-stu-id="04a8c-162">Adding a PackageReference condition</span></span>

<span data-ttu-id="04a8c-163">Sie können mithilfe einer Bedingung steuern, ob ein Paket eingeschlossen wird. Dabei kann in Bedingungen eine beliebige MSBuild-Variable oder eine in der Ziel- oder Eigenschaftendatei definierte Variable verwendet werden.</span><span class="sxs-lookup"><span data-stu-id="04a8c-163">You can use a condition to control whether a package is included, where conditions can use any MSBuild variable or a variable defined in the targets or props file.</span></span> <span data-ttu-id="04a8c-164">Zum aktuellen Zeitpunkt wird jedoch nur die Variable `TargetFramework` unterstützt.</span><span class="sxs-lookup"><span data-stu-id="04a8c-164">However, at presently, only the `TargetFramework` variable is supported.</span></span>

<span data-ttu-id="04a8c-165">Angenommen, Ihre Zielgruppen lauten `netstandard1.4` und `net452`, die vorhandene Abhängigkeit gilt jedoch nur für `net452`.</span><span class="sxs-lookup"><span data-stu-id="04a8c-165">For example, say you're targeting `netstandard1.4` as well as `net452` but have a dependency that is applicable only for `net452`.</span></span> <span data-ttu-id="04a8c-166">In diesem Fall sollte diese unnötige Abhängigkeit nicht zu einem `netstandard1.4`-Projekt hinzugefügt werden, in dem Ihr Paket verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="04a8c-166">In this case you don't want a `netstandard1.4` project that's consuming your package to add that unnecessary dependency.</span></span> <span data-ttu-id="04a8c-167">Sie geben in der `PackageReference` eine Bedingung an, um dies zu verhindern, die wie folgt lautet:</span><span class="sxs-lookup"><span data-stu-id="04a8c-167">To prevent this, you specify a condition on the `PackageReference` as follows:</span></span>

```xml
<ItemGroup>
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" Condition="'$(TargetFramework)' == 'net452'" />
    <!-- ... -->
</ItemGroup>
```

<span data-ttu-id="04a8c-168">Ein Paket, das in diesem Projekt erstellt wurde, zeigt an, dass die Datei „Newtonsoft.json“ nur als Abhängigkeit für ein `net452`-Ziel enthalten ist:</span><span class="sxs-lookup"><span data-stu-id="04a8c-168">A package built using this project will show that Newtonsoft.Json is included as a dependency only for a `net452` target:</span></span>

![Das Ergebnis der Anwendung einer Bedingung auf die PackageReference mit VS2017](media/PackageReference-Condition.png)

<span data-ttu-id="04a8c-170">Bedingungen können auch auf der `ItemGroup`-Ebene angewendet werden und gelten dann für alle untergeordneten `PackageReference`-Elemente:</span><span class="sxs-lookup"><span data-stu-id="04a8c-170">Conditions can also be applied at the `ItemGroup` level and will apply to all children `PackageReference` elements:</span></span>

```xml
<ItemGroup Condition = "'$(TargetFramework)' == 'net452'">
    <!-- ... -->
    <PackageReference Include="Newtonsoft.Json" Version="9.0.1" />
    <PackageReference Include="Contoso.Utility.UsefulStuff" Version="3.6.0" />
    <!-- ... -->
</ItemGroup>
```
