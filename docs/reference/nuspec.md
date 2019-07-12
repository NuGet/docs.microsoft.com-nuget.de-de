---
title: NUSPEC-Dateireferenz für NuGet
description: Die NUSPEC-Datei enthält Paketmetadaten, die bei der Erstellung eines Pakets verwendet werden, um für die Paketconsumer Informationen bereitzustellen.
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: fd6ecab05a392a2a0b4ddf1ac15eb108f2653703
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842411"
---
# <a name="nuspec-reference"></a><span data-ttu-id="8c1d6-103">NUSPEC-Referenz</span><span class="sxs-lookup"><span data-stu-id="8c1d6-103">.nuspec reference</span></span>

<span data-ttu-id="8c1d6-104">Bei einer `.nuspec`-Datei handelt es sich um eine XML-Manifestdatei, die Paketmetadaten enthält.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-104">A `.nuspec` file is an XML manifest that contains package metadata.</span></span> <span data-ttu-id="8c1d6-105">Diese Manifestdatei wird sowohl für die Erstellung des Pakets als auch zur Bereitstellung von Informationen für die Consumer verwendet.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-105">This manifest is used both to build the package and to provide information to consumers.</span></span> <span data-ttu-id="8c1d6-106">Manifestdateien sind in allen Paketen enthalten.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-106">The manifest is always included in a package.</span></span>

<span data-ttu-id="8c1d6-107">In diesem Thema:</span><span class="sxs-lookup"><span data-stu-id="8c1d6-107">In this topic:</span></span>

- [<span data-ttu-id="8c1d6-108">Allgemeine Form und Schema</span><span class="sxs-lookup"><span data-stu-id="8c1d6-108">General form and schema</span></span>](#general-form-and-schema)
- <span data-ttu-id="8c1d6-109">[Ersetzungstokens](#replacement-tokens) (bei der Verwendung in einem Visual Studio-Projekt)</span><span class="sxs-lookup"><span data-stu-id="8c1d6-109">[Replacement tokens](#replacement-tokens) (when used with a Visual Studio project)</span></span>
- [<span data-ttu-id="8c1d6-110">Abhängigkeiten</span><span class="sxs-lookup"><span data-stu-id="8c1d6-110">Dependencies</span></span>](#dependencies)
- [<span data-ttu-id="8c1d6-111">Explizite Assemblyverweise</span><span class="sxs-lookup"><span data-stu-id="8c1d6-111">Explicit assembly references</span></span>](#explicit-assembly-references)
- [<span data-ttu-id="8c1d6-112">Verweise auf Frameworkassemblys</span><span class="sxs-lookup"><span data-stu-id="8c1d6-112">Framework assembly references</span></span>](#framework-assembly-references)
- [<span data-ttu-id="8c1d6-113">Einschließen von Assemblydateien</span><span class="sxs-lookup"><span data-stu-id="8c1d6-113">Including assembly files</span></span>](#including-assembly-files)
- [<span data-ttu-id="8c1d6-114">Einschließen von Inhaltsdateien</span><span class="sxs-lookup"><span data-stu-id="8c1d6-114">Including content files</span></span>](#including-content-files)
- [<span data-ttu-id="8c1d6-115">NUSPEC-Beispieldateien</span><span class="sxs-lookup"><span data-stu-id="8c1d6-115">Example nuspec files</span></span>](#example-nuspec-files)

## <a name="project-type-compatibility"></a><span data-ttu-id="8c1d6-116">Projektkompatibilität-Typ</span><span class="sxs-lookup"><span data-stu-id="8c1d6-116">Project type compatibility</span></span>

- <span data-ttu-id="8c1d6-117">Verwenden Sie `.nuspec` mit `nuget.exe pack` für nicht-SDK-Style Projekten, in denen `packages.config`.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-117">Use `.nuspec` with `nuget.exe pack` for non-SDK-style projects that use `packages.config`.</span></span>

- <span data-ttu-id="8c1d6-118">Ein `.nuspec` Datei ist nicht erforderlich, zum Erstellen von Paketen für [SDK-Projekten](../resources/check-project-format.md) (in der Regel .NET Core und .NET Standard Projekten, in denen die [SDK-Attribut](/dotnet/core/tools/csproj#additions)).</span><span class="sxs-lookup"><span data-stu-id="8c1d6-118">A `.nuspec` file is not required to create packages for [SDK-style projects](../resources/check-project-format.md) (typically .NET Core and .NET Standard projects that use the [SDK attribute](/dotnet/core/tools/csproj#additions)).</span></span> <span data-ttu-id="8c1d6-119">(Beachten Sie, dass eine `.nuspec` wird generiert, wenn Sie das Paket zu erstellen.)</span><span class="sxs-lookup"><span data-stu-id="8c1d6-119">(Note that a `.nuspec` is generated when you create the package.)</span></span>

   <span data-ttu-id="8c1d6-120">Wenn Sie ein Paket mit erstellen `dotnet.exe pack` oder `msbuild pack target`, es wird empfohlen, die Sie [enthalten alle Eigenschaften](../reference/msbuild-targets.md#pack-target) , sind in der Regel in der `.nuspec` stattdessen in der Projektdatei Datei.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-120">If you are creating a package using `dotnet.exe pack` or `msbuild pack target`, we recommend that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead.</span></span> <span data-ttu-id="8c1d6-121">Aber Sie können stattdessen auch [verwenden eine `.nuspec` Datei packen mit `dotnet.exe` oder `msbuild pack target` ](../reference/msbuild-targets.md#packing-using-a-nuspec).</span><span class="sxs-lookup"><span data-stu-id="8c1d6-121">However, you can instead choose to [use a `.nuspec` file to pack using `dotnet.exe` or `msbuild pack target`](../reference/msbuild-targets.md#packing-using-a-nuspec).</span></span>

- <span data-ttu-id="8c1d6-122">Für Projekte von migriert `packages.config` zu ["packagereference"](../consume-packages/package-references-in-project-files.md), `.nuspec` Datei ist nicht erforderlich, um das Paket zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-122">For projects migrated from `packages.config` to [PackageReference](../consume-packages/package-references-in-project-files.md), a `.nuspec` file is not required to create the package.</span></span> <span data-ttu-id="8c1d6-123">Verwenden Sie stattdessen [Msbuild-Pack](../reference/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).</span><span class="sxs-lookup"><span data-stu-id="8c1d6-123">Instead, use [msbuild pack](../reference/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).</span></span>

## <a name="general-form-and-schema"></a><span data-ttu-id="8c1d6-124">Allgemeine Form und Schema</span><span class="sxs-lookup"><span data-stu-id="8c1d6-124">General form and schema</span></span>

<span data-ttu-id="8c1d6-125">Die aktuelle `nuspec.xsd`-Schemadatei finden Sie im [NuGet-GitHub-Repository](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span><span class="sxs-lookup"><span data-stu-id="8c1d6-125">The current `nuspec.xsd` schema file can be found in the [NuGet GitHub repository](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span></span>

<span data-ttu-id="8c1d6-126">Für dieses Schema gilt die im Folgenden dargestellte allgemeine Form für die `.nuspec`-Datei:</span><span class="sxs-lookup"><span data-stu-id="8c1d6-126">Within this schema, a `.nuspec` file has the following general form:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <!-- Required elements-->
        <id></id>
        <version></version>
        <description></description>
        <authors></authors>

        <!-- Optional elements -->
        <!-- ... -->
    </metadata>
    <!-- Optional 'files' node -->
</package>
```

<span data-ttu-id="8c1d6-127">Um eine übersichtliche Darstellung des Schemas anzuzeigen, öffnen Sie die Schemadatei im Entwurfsmodus in Visual Studio und klicken dann auf den Link **XML-Schema-Explorer**.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-127">For a clear visual representation of the schema, open the schema file in Visual Studio in Design mode and click on the **XML Schema Explorer** link.</span></span> <span data-ttu-id="8c1d6-128">Alternativ können Sie die Datei auch als Code öffnen, mit der rechten Maustaste in den Editor klicken und **Show XML Schema Explorer** (XML-Schema-Explorer anzeigen) auswählen.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-128">Alternately, open the file as code, right-click in the editor, and select **Show XML Schema Explorer**.</span></span> <span data-ttu-id="8c1d6-129">In beiden Fällen wird eine Ansicht zurückgegeben, die der in der folgenden Abbildung gezeigten ähnlich ist (bei erweiterter Darstellung):</span><span class="sxs-lookup"><span data-stu-id="8c1d6-129">Either way you get a view like the one below (when mostly expanded):</span></span>

![Visual Studio-Schema-Explorer mit geöffneter „nuspec.xsd“-Datei](media/SchemaExplorer.png)

### <a name="required-metadata-elements"></a><span data-ttu-id="8c1d6-131">Erforderliche Metadatenelemente</span><span class="sxs-lookup"><span data-stu-id="8c1d6-131">Required metadata elements</span></span>

<span data-ttu-id="8c1d6-132">Obwohl es sich bei den folgenden Elementen um die Mindestanforderungen für ein Paket handelt, sollten Sie in Erwägung ziehen, die [optionalen Metadatenelemente](#optional-metadata-elements) hinzuzufügen, damit Entwicklern die Arbeit mit Ihren Paketen erleichtert wird.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-132">Although the following elements are the minimum requirements for a package, you should consider adding the [optional metadata elements](#optional-metadata-elements) to improve the overall experience developers have with your package.</span></span> 

<span data-ttu-id="8c1d6-133">Die folgenden Elemente müssen in einem `<metadata>`-Element vorhanden sein.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-133">These elements must appear within a `<metadata>` element.</span></span>

#### <a name="id"></a><span data-ttu-id="8c1d6-134">id</span><span class="sxs-lookup"><span data-stu-id="8c1d6-134">id</span></span> 
<span data-ttu-id="8c1d6-135">Paketbezeichner, der auf nuget.org oder im für das Paket verwendeten Katalog eindeutig sein muss. Die Groß-/Kleinschreibung wird nicht berücksichtigt.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-135">The case-insensitive package identifier, which must be unique across nuget.org or whatever gallery the package resides in.</span></span> <span data-ttu-id="8c1d6-136">IDs dürfen keine Leerzeichen oder in URLs unzulässige Zeichen enthalten. Im Wesentlichen müssen sie den Regeln für .NET-Namespaces entsprechen.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-136">IDs may not contain spaces or characters that are not valid for a URL, and generally follow .NET namespace rules.</span></span> <span data-ttu-id="8c1d6-137">Informationen finden Sie unter [Auswählen eines eindeutigen Paketbezeichners und Festlegen der Versionsnummer](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number).</span><span class="sxs-lookup"><span data-stu-id="8c1d6-137">See [Choosing a unique package identifier](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number) for guidance.</span></span>
#### <a name="version"></a><span data-ttu-id="8c1d6-138">version</span><span class="sxs-lookup"><span data-stu-id="8c1d6-138">version</span></span>
<span data-ttu-id="8c1d6-139">Die Version des Pakets. Das Format lautet *Hauptversion.Nebenversion.Patch*.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-139">The version of the package, following the *major.minor.patch* pattern.</span></span> <span data-ttu-id="8c1d6-140">Versionsnummern enthalten möglicherweise, wie unter [Version Ranges and Wildcards (Versionsbereiche und Platzhalter)](../reference/package-versioning.md#pre-release-versions) beschrieben, ein Suffix der Vorabversion.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-140">Version numbers may include a pre-release suffix as described in [Package versioning](../reference/package-versioning.md#pre-release-versions).</span></span> 
#### <a name="description"></a><span data-ttu-id="8c1d6-141">description</span><span class="sxs-lookup"><span data-stu-id="8c1d6-141">description</span></span>
<span data-ttu-id="8c1d6-142">Eine ausführliche Beschreibung des Pakets zur Anzeige auf der Benutzeroberfläche.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-142">A long description of the package for UI display.</span></span> 
#### <a name="authors"></a><span data-ttu-id="8c1d6-143">authors</span><span class="sxs-lookup"><span data-stu-id="8c1d6-143">authors</span></span>
<span data-ttu-id="8c1d6-144">Eine durch Kommas getrennte Liste der Paketautoren entsprechend den Profilnamen unter nuget.org. Diese werden im NuGet-Katalog auf nuget.org angezeigt und verwendet, um auf Pakete derselben Autoren zu verweisen.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-144">A comma-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> 

### <a name="optional-metadata-elements"></a><span data-ttu-id="8c1d6-145">Optionale Metadatenelemente</span><span class="sxs-lookup"><span data-stu-id="8c1d6-145">Optional metadata elements</span></span>

#### <a name="owners"></a><span data-ttu-id="8c1d6-146">owners</span><span class="sxs-lookup"><span data-stu-id="8c1d6-146">owners</span></span>
<span data-ttu-id="8c1d6-147">Eine durch Kommas getrennte Liste der Paketersteller mit den auf nuget.org verwendeten Profilnamen. Dabei handelt es sich häufig um dieselbe Liste wie in `authors`. Sie wird beim Hochladen der Pakete auf nuget.org ignoriert. Informationen hierzu finden Sie unter [Verwalten von Paketbesitzern auf nuget.org](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg).</span><span class="sxs-lookup"><span data-stu-id="8c1d6-147">A comma-separated list of the package creators using profile names on nuget.org. This is often the same list as in `authors`, and is ignored when uploading the package to nuget.org. See [Managing package owners on nuget.org](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg).</span></span> 

#### <a name="projecturl"></a><span data-ttu-id="8c1d6-148">projectUrl</span><span class="sxs-lookup"><span data-stu-id="8c1d6-148">projectUrl</span></span>
<span data-ttu-id="8c1d6-149">URL der Homepage des Pakets, wird häufig auf Benutzeroberflächen und auf nuget.org angezeigt.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-149">A URL for the package's home page, often shown in UI displays as well as nuget.org.</span></span> 

#### <a name="licenseurl"></a><span data-ttu-id="8c1d6-150">licenseUrl</span><span class="sxs-lookup"><span data-stu-id="8c1d6-150">licenseUrl</span></span>
> [!Important]
> <span data-ttu-id="8c1d6-151">"licenseUrl" ist veraltet.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-151">licenseUrl is being deprecated.</span></span> <span data-ttu-id="8c1d6-152">Verwenden Sie stattdessen die Lizenz.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-152">Use license instead.</span></span>

<span data-ttu-id="8c1d6-153">Eine URL für die paketlizenz, häufig in Benutzeroberflächen wie nuget.org angezeigt.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-153">A URL for the package's license, often shown in UIs like nuget.org.</span></span>

#### <a name="license"></a><span data-ttu-id="8c1d6-154">Lizenz</span><span class="sxs-lookup"><span data-stu-id="8c1d6-154">license</span></span>
<span data-ttu-id="8c1d6-155">Ein Ausdruck der SPDX-Lizenz oder der Pfad zu einer Lizenzdatei, in dem Paket, das häufig in Benutzeroberflächen wie nuget.org angezeigt werden soll. Wenn Sie das Paket unter dem eine allgemeine Lizenz, z. B. MIT oder BSD-2-Klausel, lizenzieren verwenden Sie die zugeordnete [SPDX Lizenz-ID](https://spdx.org/licenses/).</span><span class="sxs-lookup"><span data-stu-id="8c1d6-155">An SPDX license expression or path to a license file within the package, often shown in UIs like nuget.org. If you're licensing the package under a common license, like MIT or BSD-2-Clause, use the associated [SPDX license identifier](https://spdx.org/licenses/).</span></span> <span data-ttu-id="8c1d6-156">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="8c1d6-156">For example:</span></span>

`<license type="expression">MIT</license>`

> [!Note]
> <span data-ttu-id="8c1d6-157">"NuGet.org" akzeptiert nur Lizenz-Ausdrücke, die von der Open Source-Initiative oder die Free Software Foundation genehmigt werden.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-157">NuGet.org only accepts license expressions that are approved by the Open Source Initiative or the Free Software Foundation.</span></span>

<span data-ttu-id="8c1d6-158">Wenn Ihr Paket in mehrere allgemeine-Lizenzen lizenziert ist, können Sie angeben, eine zusammengesetzte Lizenz mithilfe der [SPDX Expression Syntaxversion 2.0](https://spdx.org/spdx-specification-21-web-version#h.jxpfx0ykyb60).</span><span class="sxs-lookup"><span data-stu-id="8c1d6-158">If your package is licensed under multiple common licenses, you can specify a composite license using the [SPDX expression syntax version 2.0](https://spdx.org/spdx-specification-21-web-version#h.jxpfx0ykyb60).</span></span> <span data-ttu-id="8c1d6-159">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="8c1d6-159">For example:</span></span>

`<license type="expression">BSD-2-Clause OR MIT</license>`

<span data-ttu-id="8c1d6-160">Wenn Sie eine angepasste Lizenz, die Lizenz Ausdrücke unterstützt wird verwenden, können Sie Verpacken einer `.txt` oder `.md` -Datei mit der Lizenz des Texts.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-160">If you use a custom license that isn't supported by license expressions, you can package a `.txt` or `.md` file with the license's text.</span></span> <span data-ttu-id="8c1d6-161">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="8c1d6-161">For example:</span></span>

```xml
<package>
  <metadata>
    ...
    <license type="file">LICENSE.txt</license>
    ...
  </metadata>
  <files>
    ...
    <file src="licenses\LICENSE.txt" target="" />
    ...
  </files>
</package>
```

<span data-ttu-id="8c1d6-162">Für die MSBuild-Entsprechung, sehen Sie sich [Packen eines Ausdrucks für die Lizenz oder eine Lizenzdatei](msbuild-targets.md#packing-a-license-expression-or-a-license-file).</span><span class="sxs-lookup"><span data-stu-id="8c1d6-162">For the MSBuild equivalent, take a look at [Packing a license expression or a license file](msbuild-targets.md#packing-a-license-expression-or-a-license-file).</span></span>

<span data-ttu-id="8c1d6-163">Die genaue Syntax für Ausdrücke für die NuGet-Lizenz wird im folgenden beschrieben in [ABNF](https://tools.ietf.org/html/rfc5234).</span><span class="sxs-lookup"><span data-stu-id="8c1d6-163">The exact syntax of NuGet's license expressions is described below in [ABNF](https://tools.ietf.org/html/rfc5234).</span></span>
```cli
license-id            = <short form license identifier from https://spdx.org/spdx-specification-21-web-version#h.luq9dgcle9mo>

license-exception-id  = <short form license exception identifier from https://spdx.org/spdx-specification-21-web-version#h.ruv3yl8g6czd>

simple-expression = license-id / license-id”+”

compound-expression =  1*1(simple-expression /
                simple-expression "WITH" license-exception-id /
                compound-expression "AND" compound-expression /
                compound-expression "OR" compound-expression ) /                
                "(" compound-expression ")" )

license-expression =  1*1(simple-expression / compound-expression / UNLICENSED)
```

#### <a name="iconurl"></a><span data-ttu-id="8c1d6-164">iconUrl</span><span class="sxs-lookup"><span data-stu-id="8c1d6-164">iconUrl</span></span>
<span data-ttu-id="8c1d6-165">URL eines 64 × 64 Pixel großen Bilds mit transparentem Hintergrund, das als Symbol für das Paket auf der Benutzeroberfläche verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-165">A URL for a 64x64 image with transparency background to use as the icon for the package in UI display.</span></span> <span data-ttu-id="8c1d6-166">Stellen Sie sicher, dass dieses Element die *direkte Bild-URL* und nicht die URL einer Webseite enthält, auf der das Bild zu finden ist.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-166">Be sure this element contains the *direct image URL* and not the URL of a web page containing the image.</span></span> <span data-ttu-id="8c1d6-167">Wenn Sie beispielsweise ein Bild auf GitHub verwenden möchten, geben Sie die URL der Rohdatendatei an (z. B. <em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>).</span><span class="sxs-lookup"><span data-stu-id="8c1d6-167">For example, to use an image from GitHub, use the raw file URL like <em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>.</span></span> 

#### <a name="requirelicenseacceptance"></a><span data-ttu-id="8c1d6-168">requireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="8c1d6-168">requireLicenseAcceptance</span></span>
<span data-ttu-id="8c1d6-169">Ein boolescher Wert, der angibt, ob der Client den Consumer dazu auffordern muss, die Paketlizenz vor der Installation des Pakets zu akzeptieren.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-169">A Boolean value specifying whether the client must prompt the consumer to accept the package license before installing the package.</span></span>

#### <a name="developmentdependency"></a><span data-ttu-id="8c1d6-170">developmentDependency</span><span class="sxs-lookup"><span data-stu-id="8c1d6-170">developmentDependency</span></span>
<span data-ttu-id="8c1d6-171">*(ab Version 2.8)* Boolescher Wert, der angibt, ob das Paket mit einer Abhängigkeit markiert werden soll, die nur für die Entwicklung gilt. Hierdurch wird vermieden, dass das Paket als Abhängigkeit in andere Pakete eingeschlossen wird.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-171">*(2.8+)* A Boolean value specifying whether the package is be marked as a development-only-dependency, which prevents the package from being included as a dependency in other packages.</span></span> <span data-ttu-id="8c1d6-172">Mit "packagereference" (NuGet 4.8) bedeutet dieses Flag auch, dass es während der Kompilierung von Ressourcen aus der Kompilierung ausgeschlossen werden.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-172">With PackageReference (NuGet 4.8+), this flag also means that it will exclude compile-time assets from compilation.</span></span> <span data-ttu-id="8c1d6-173">Finden Sie unter [DevelopmentDependency-Unterstützung für PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)</span><span class="sxs-lookup"><span data-stu-id="8c1d6-173">See [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)</span></span>

#### <a name="summary"></a><span data-ttu-id="8c1d6-174">summary</span><span class="sxs-lookup"><span data-stu-id="8c1d6-174">summary</span></span>
<span data-ttu-id="8c1d6-175">Kurzbeschreibung des Pakets zur Anzeige auf der Benutzeroberfläche.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-175">A short description of the package for UI display.</span></span> <span data-ttu-id="8c1d6-176">Wenn diese nicht angegeben ist, wird eine gekürzte Version von `description` verwendet.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-176">If omitted, a truncated version of `description` is used.</span></span>

#### <a name="releasenotes"></a><span data-ttu-id="8c1d6-177">releaseNotes</span><span class="sxs-lookup"><span data-stu-id="8c1d6-177">releaseNotes</span></span>
<span data-ttu-id="8c1d6-178">*(ab Version 1.5)* Beschreibung der in diesem Release des Pakets enthaltenen Änderungen, die häufig auf Benutzeroberflächen wie der Registerkarte **Updates** des Visual Studio-Paket-Managers anstelle von Paketbeschreibungen verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-178">*(1.5+)* A description of the changes made in this release of the package, often used in UI like the **Updates** tab of the Visual Studio Package Manager in place of the package description.</span></span>

#### <a name="copyright"></a><span data-ttu-id="8c1d6-179">copyright</span><span class="sxs-lookup"><span data-stu-id="8c1d6-179">copyright</span></span>
<span data-ttu-id="8c1d6-180">*(ab Version 1.5)* Urheberrechtliche Hinweise zum Paket.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-180">*(1.5+)* Copyright details for the package.</span></span>

#### <a name="language"></a><span data-ttu-id="8c1d6-181">language</span><span class="sxs-lookup"><span data-stu-id="8c1d6-181">language</span></span>
<span data-ttu-id="8c1d6-182">Gebietsschema-ID des Pakets.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-182">The locale ID for the package.</span></span> <span data-ttu-id="8c1d6-183">Informationen hierzu finden Sie unter [Erstellen lokalisierter NuGet-Pakete](../create-packages/creating-localized-packages.md).</span><span class="sxs-lookup"><span data-stu-id="8c1d6-183">See [Creating localized packages](../create-packages/creating-localized-packages.md).</span></span>

#### <a name="tags"></a><span data-ttu-id="8c1d6-184">tags</span><span class="sxs-lookup"><span data-stu-id="8c1d6-184">tags</span></span>
<span data-ttu-id="8c1d6-185">Eine durch Leerzeichen getrennte Liste mit Tags und Schlüsselwörtern, die das Paket beschreiben und das Auffinden von Paketen mithilfe von Suchvorgängen und Filtern erleichtern.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-185">A space-delimited list of tags and keywords that describe the package and aid discoverability of packages through search and filtering.</span></span> 

#### <a name="serviceable"></a><span data-ttu-id="8c1d6-186">serviceable</span><span class="sxs-lookup"><span data-stu-id="8c1d6-186">serviceable</span></span> 
<span data-ttu-id="8c1d6-187">*(ab Version 3.3)* Nur zur internen Verwendung von NuGet.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-187">*(3.3+)* For internal NuGet use only.</span></span>

#### <a name="repository"></a><span data-ttu-id="8c1d6-188">repository</span><span class="sxs-lookup"><span data-stu-id="8c1d6-188">repository</span></span>
<span data-ttu-id="8c1d6-189">Repositorymetadaten. Sie umfassen vier optionale Attribute: *type* und *url* *(ab Version 4.0)* sowie *branch* und *commit* *(ab Version 4.6)* .</span><span class="sxs-lookup"><span data-stu-id="8c1d6-189">Repository metadata, consisting of four optional attributes: *type* and *url* *(4.0+)*, and *branch* and *commit* *(4.6+)*.</span></span> <span data-ttu-id="8c1d6-190">Mit diesen Attributen können Sie die NUPKG-Datei dem Repository zuordnen, mit dem es erstellt wurde. Dabei lässt sich eine Detailtiefe bis hinab zum einzelnen Branch oder Commit erzielen, durch den das Paket erstellt wurde.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-190">These attributes allow you to map the .nupkg to the repository that built it, with the potential to get as detailed as the individual branch or commit that built the package.</span></span> <span data-ttu-id="8c1d6-191">Hierbei sollte es sich um eine öffentlich zugängliche URL handeln, die direkt von einer Versionskontrollsoftware aufgerufen werden kann.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-191">This should be a publicly available url that can be invoked directly by a version control software.</span></span> <span data-ttu-id="8c1d6-192">Dagegen sollte es keine HTML-Seite sein, da diese für den Computer vorgesehen ist.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-192">It should not be an html page as this is meant for the computer.</span></span> <span data-ttu-id="8c1d6-193">Zur Verknüpfung mit der Projektseite verwenden Sie stattdessen das Feld `projectUrl`.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-193">For linking to project page, use the `projectUrl` field, instead.</span></span>

#### <a name="minclientversion"></a><span data-ttu-id="8c1d6-194">minClientVersion</span><span class="sxs-lookup"><span data-stu-id="8c1d6-194">minClientVersion</span></span>
<span data-ttu-id="8c1d6-195">Gibt die mindestens erforderliche Version des NuGet-Clients an, der dieses Paket installieren kann. Dies wird von nuget.exe und dem Paket-Manager von Visual Studio erzwungen.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-195">Specifies the minimum version of the NuGet client that can install this package, enforced by nuget.exe and the Visual Studio Package Manager.</span></span> <span data-ttu-id="8c1d6-196">Das Attribut wird verwendet, wenn das Paket von bestimmten Funktionen der `.nuspec`-Datei abhängig ist, die in einer bestimmten Version des NuGet-Clients hinzugefügt wurden.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-196">This is used whenever the package depends on specific features of the `.nuspec` file that were added in a particular version of the NuGet client.</span></span> <span data-ttu-id="8c1d6-197">Beispielsweise sollte ein Paket, das das `developmentDependency`-Attribut verwendet, „2.8“ für `minClientVersion` angeben.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-197">For example, a package using the `developmentDependency` attribute should specify "2.8" for `minClientVersion`.</span></span> <span data-ttu-id="8c1d6-198">Genauso sollte ein Paket, das das `contentFiles`-Element verwendet (vgl. nächster Abschnitt), `minClientVersion` auf „3.3“ festlegen.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-198">Similarly, a package using the `contentFiles` element (see the next section) should set `minClientVersion` to "3.3".</span></span> <span data-ttu-id="8c1d6-199">Beachten Sie außerdem, dass NuGet-Clients vor Version 2.5 dieses Flag nicht erkennen und daher die Installation des Pakets unabhängig vom Inhalt von `minClientVersion` *immer* verweigern.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-199">Note also that because NuGet clients prior to 2.5 do not recognize this flag, they *always* refuse to install the package no matter what `minClientVersion` contains.</span></span>

#### <a name="title"></a><span data-ttu-id="8c1d6-200">title</span><span class="sxs-lookup"><span data-stu-id="8c1d6-200">title</span></span>
<span data-ttu-id="8c1d6-201">Ein Benutzerfreundlicher Titel des Pakets in einer Benutzeroberfläche verwendet werden kann, werden angezeigt.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-201">A human-friendly title of the package which may be used in some UI displays.</span></span> <span data-ttu-id="8c1d6-202">("NuGet.org" und die Paket-Manager in Visual Studio nicht Titel anzeigen)</span><span class="sxs-lookup"><span data-stu-id="8c1d6-202">(nuget.org and the Package Manager in Visual Studio do not show title)</span></span>

#### <a name="collection-elements"></a><span data-ttu-id="8c1d6-203">Sammlungselemente</span><span class="sxs-lookup"><span data-stu-id="8c1d6-203">Collection elements</span></span>

#### <a name="packagetypes"></a><span data-ttu-id="8c1d6-204">packageTypes</span><span class="sxs-lookup"><span data-stu-id="8c1d6-204">packageTypes</span></span>
<span data-ttu-id="8c1d6-205">*(ab Version 3.5)* Eine Sammlung mit null oder mehr `<packageType>`-Elementen, die den Pakettyp angibt, sofern es sich nicht um ein gewöhnliches Abhängigkeitspaket handelt.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-205">*(3.5+)* A collection of zero or more `<packageType>` elements specifying the type of the package if other than a traditional dependency package.</span></span> <span data-ttu-id="8c1d6-206">Jedes packageType-Element verfügt über die Attribute *name* und *version*.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-206">Each packageType has attributes of *name* and *version*.</span></span> <span data-ttu-id="8c1d6-207">Informationen hierzu finden Sie unter [Festlegen eines Pakettyps](../create-packages/set-package-type.md).</span><span class="sxs-lookup"><span data-stu-id="8c1d6-207">See [Setting a package type](../create-packages/set-package-type.md).</span></span>
#### <a name="dependencies"></a><span data-ttu-id="8c1d6-208">dependencies</span><span class="sxs-lookup"><span data-stu-id="8c1d6-208">dependencies</span></span>
<span data-ttu-id="8c1d6-209">Eine Sammlung mit null oder mehr `<dependency>`-Elementen, die die Abhängigkeiten für das Paket angibt.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-209">A collection of zero or more `<dependency>` elements specifying the dependencies for the package.</span></span> <span data-ttu-id="8c1d6-210">Jede Abhängigkeit verfügt über die Attribute *id*, *version*, *include* und *exclude* (ab Version 3.x).</span><span class="sxs-lookup"><span data-stu-id="8c1d6-210">Each dependency has attributes of *id*, *version*, *include* (3.x+), and *exclude* (3.x+).</span></span> <span data-ttu-id="8c1d6-211">Informationen hierzu finden Sie im Abschnitt [Abhängigkeiten](#dependencies-element) weiter unten.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-211">See [Dependencies](#dependencies-element) below.</span></span>
#### <a name="frameworkassemblies"></a><span data-ttu-id="8c1d6-212">frameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="8c1d6-212">frameworkAssemblies</span></span>
<span data-ttu-id="8c1d6-213">*(ab Version 1.2)* Eine Sammlung mit null oder mehr `<frameworkAssembly>`-Elementen, die die für das Paket erforderlichen Verweise auf .NET Framework-Assemblys benennt. Hierdurch wird sichergestellt, dass Verweise auf Projekte hinzugefügt werden, die das Paket verarbeiten.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-213">*(1.2+)* A collection of zero or more `<frameworkAssembly>` elements identifying .NET Framework assembly references that this package requires, which ensures that references are added to projects consuming the package.</span></span> <span data-ttu-id="8c1d6-214">Jedes frameworkAssembly-Element verfügt über die Attribute *assemblyName* und *targetFramework*.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-214">Each frameworkAssembly has *assemblyName* and *targetFramework* attributes.</span></span> <span data-ttu-id="8c1d6-215">Informationen hierzu finden Sie unter [Verweise auf Frameworkassemblys](#specifying-framework-assembly-references-gac).</span><span class="sxs-lookup"><span data-stu-id="8c1d6-215">See [Specifying framework assembly references GAC](#specifying-framework-assembly-references-gac) below.</span></span> |
#### <a name="references"></a><span data-ttu-id="8c1d6-216">references</span><span class="sxs-lookup"><span data-stu-id="8c1d6-216">references</span></span>
<span data-ttu-id="8c1d6-217">*(ab Version 1.5)* Eine Sammlung mit null oder mehr `<reference>`-Elementen, die Assemblys im `lib`-Ordner des Pakets benennt, die als Projektverweise hinzugefügt werden.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-217">*(1.5+)* A collection of zero or more `<reference>` elements naming assemblies in the package's `lib` folder that are added as project references.</span></span> <span data-ttu-id="8c1d6-218">Jeder Verweis verfügt über ein *file*-Attribut.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-218">Each reference has a *file* attribute.</span></span> <span data-ttu-id="8c1d6-219">`<references>` kann außerdem ein `<group>`-Element mit einem *targetFramework*-Attribut enthalten, das seinerseits `<reference>`-Elemente enthält.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-219">`<references>` can also contain a `<group>` element with a *targetFramework* attribute, that then contains `<reference>` elements.</span></span> <span data-ttu-id="8c1d6-220">Wenn das Element nicht angegeben ist, werden alle Verweise in `lib` eingeschlossen.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-220">If omitted, all references in `lib` are included.</span></span> <span data-ttu-id="8c1d6-221">Informationen hierzu finden Sie unter [Explizite Assemblyverweise](#specifying-explicit-assembly-references).</span><span class="sxs-lookup"><span data-stu-id="8c1d6-221">See [Specifying explicit assembly references](#specifying-explicit-assembly-references) below.</span></span>
#### <a name="contentfiles"></a><span data-ttu-id="8c1d6-222">contentFiles</span><span class="sxs-lookup"><span data-stu-id="8c1d6-222">contentFiles</span></span>
<span data-ttu-id="8c1d6-223">*(ab Version 3.3)* Eine Sammlung von `<files>`-Elementen, die Inhaltsdateien angeben, die in das verarbeitende Projekt eingeschlossen werden sollen.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-223">*(3.3+)* A collection of `<files>` elements that identify content files to include in the consuming project.</span></span> <span data-ttu-id="8c1d6-224">Diese Dateien werden zusammen mit Attributen angegeben, die beschreiben, wie sie im Projektsystem verwendet werden sollen.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-224">These files are specified with a set of attributes that describe how they should be used within the project system.</span></span> <span data-ttu-id="8c1d6-225">Informationen hierzu finden Sie weiter unten unter [Einschließen von Assemblydateien](#specifying-files-to-include-in-the-package).</span><span class="sxs-lookup"><span data-stu-id="8c1d6-225">See [Specifying files to include in the package](#specifying-files-to-include-in-the-package) below.</span></span>
#### <a name="files"></a><span data-ttu-id="8c1d6-226">files</span><span class="sxs-lookup"><span data-stu-id="8c1d6-226">files</span></span> 
<span data-ttu-id="8c1d6-227">Die `<package>` -Knoten enthält möglicherweise eine `<files>` Knoten einen gleichgeordneten Knoten zu `<metadata>`, und ein `<contentFiles>` untergeordnetes Element unter `<metadata>`, um anzugeben, welche Dateien Assembly- und Inhaltsdateien im Paket enthalten.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-227">The `<package>` node may contain a `<files>` node as a sibling to `<metadata>`, and a `<contentFiles>` child under `<metadata>`, to specify which assembly and content files to include in the package.</span></span> <span data-ttu-id="8c1d6-228">Ausführliche Informationen hierzu finden Sie weiter unten in den Abschnitten [Einschließen von Assemblydateien](#including-assembly-files) und [Einschließen von Inhaltsdateien](#including-content-files).</span><span class="sxs-lookup"><span data-stu-id="8c1d6-228">See [Including assembly files](#including-assembly-files) and [Including content files](#including-content-files) later in this topic for details.</span></span>

## <a name="replacement-tokens"></a><span data-ttu-id="8c1d6-229">Ersetzungstoken</span><span class="sxs-lookup"><span data-stu-id="8c1d6-229">Replacement tokens</span></span>

<span data-ttu-id="8c1d6-230">Bei der Erstellung eines Pakets ersetzt der [`nuget pack`-Befehl](../tools/cli-ref-pack.md) durch $ getrennte Token im `<metadata>`-Knoten der `.nuspec`-Datei durch Werte, die entweder einer Projektdatei oder der `-properties`-Option des `pack`-Befehls entstammen.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-230">When creating a package, the [`nuget pack` command](../tools/cli-ref-pack.md) replaces $-delimited tokens in the `.nuspec` file's `<metadata>` node with values that come from either a project file or the `pack` command's `-properties` switch.</span></span>

<span data-ttu-id="8c1d6-231">Geben Sie in der Befehlszeile die Tokenwerte mit `nuget pack -properties <name>=<value>;<name>=<value>` an.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-231">On the command line, you specify token values with `nuget pack -properties <name>=<value>;<name>=<value>`.</span></span> <span data-ttu-id="8c1d6-232">Beispielsweise können Sie ein Token wie `$owners$` und `$desc$` in der `.nuspec`-Datei verwenden und die Werte zur Packzeit wie im Folgenden dargestellt bereitstellen:</span><span class="sxs-lookup"><span data-stu-id="8c1d6-232">For example, you can use a token such as `$owners$` and `$desc$` in the `.nuspec` and provide the values at packing time as follows:</span></span>

```ps
nuget pack MyProject.csproj -properties
    owners=janedoe,harikm,kimo,xiaop;desc="Awesome app logger utility"
```

<span data-ttu-id="8c1d6-233">Geben Sie die in der untenstehenden Tabelle beschriebenen Token an, um Werte aus einem Projekt zu verwenden (AssemblyInfo verweist auf Dateien wie `AssemblyInfo.cs` oder `AssemblyInfo.vb` in `Properties`).</span><span class="sxs-lookup"><span data-stu-id="8c1d6-233">To use values from a project, specify the tokens described in the table below (AssemblyInfo refers to the file in `Properties` such as `AssemblyInfo.cs` or `AssemblyInfo.vb`).</span></span>

<span data-ttu-id="8c1d6-234">Führen Sie anstelle von `.nuspec` nur `nuget pack` in der Projektdatei aus, um diese Token zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-234">To use these tokens, run `nuget pack` with the project file rather than just the `.nuspec`.</span></span> <span data-ttu-id="8c1d6-235">Beispielsweise werden bei der Verwendung des folgenden Befehls die Token `$id$` und `$version$` in einer `.nuspec`-Datei durch die Werte `AssemblyName` und `AssemblyVersion` des Projekts ersetzt:</span><span class="sxs-lookup"><span data-stu-id="8c1d6-235">For example, when using the following command, the `$id$` and `$version$` tokens in a `.nuspec` file are replaced with the project's `AssemblyName` and `AssemblyVersion` values:</span></span>

```ps
nuget pack MyProject.csproj
```

<span data-ttu-id="8c1d6-236">In der Regel erstellen Sie die `.nuspec`-Datei in einem Projekt zuerst mithilfe von `nuget spec MyProject.csproj`, wodurch automatisch einige dieser Standardtoken eingeschlossen werden.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-236">Typically, when you have a project, you create the `.nuspec` initially using `nuget spec MyProject.csproj` which automatically includes some of these standard tokens.</span></span> <span data-ttu-id="8c1d6-237">Wenn in einem Projekt allerdings keine Werte für erforderliche `.nuspec`-Elemente enthalten sind, tritt bei `nuget pack` ein Fehler auf.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-237">However, if a project lacks values for required `.nuspec` elements, then `nuget pack` fails.</span></span> <span data-ttu-id="8c1d6-238">Stellen Sie außerdem bei der Änderung von Projektwerten sicher, dass Sie diese neu erstellen, bevor Sie das Paket erstellen. Dies können Sie ganz einfach über die Option `build` des Packbefehls tun.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-238">Furthermore, if you change project values, be sure to rebuild before creating the package; this can be done conveniently with the pack command's `build` switch.</span></span>

<span data-ttu-id="8c1d6-239">Mit Ausnahme von `$configuration$` werden Werte im Projekt gegenüber Werten bevorzugt, die demselben Token in der Befehlszeile zugeordnet sind.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-239">With the exception of `$configuration$`, values in the project are used in preference to any assigned to the same token on the command line.</span></span>

| <span data-ttu-id="8c1d6-240">Token</span><span class="sxs-lookup"><span data-stu-id="8c1d6-240">Token</span></span> | <span data-ttu-id="8c1d6-241">Wertquelle</span><span class="sxs-lookup"><span data-stu-id="8c1d6-241">Value source</span></span> | <span data-ttu-id="8c1d6-242">Wert</span><span class="sxs-lookup"><span data-stu-id="8c1d6-242">Value</span></span>
| --- | --- | ---
| <span data-ttu-id="8c1d6-243">**$id$**</span><span class="sxs-lookup"><span data-stu-id="8c1d6-243">**$id$**</span></span> | <span data-ttu-id="8c1d6-244">Projektdatei</span><span class="sxs-lookup"><span data-stu-id="8c1d6-244">Project file</span></span> | <span data-ttu-id="8c1d6-245">"AssemblyName" (Titel) aus der Projektdatei</span><span class="sxs-lookup"><span data-stu-id="8c1d6-245">AssemblyName (title) from the project file</span></span> |
| <span data-ttu-id="8c1d6-246">**$version$**</span><span class="sxs-lookup"><span data-stu-id="8c1d6-246">**$version$**</span></span> | <span data-ttu-id="8c1d6-247">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="8c1d6-247">AssemblyInfo</span></span> | <span data-ttu-id="8c1d6-248">„AssemblyInformationalVersion“, falls vorhanden, andernfalls „AssemblyVersion“</span><span class="sxs-lookup"><span data-stu-id="8c1d6-248">AssemblyInformationalVersion if present, otherwise AssemblyVersion</span></span> |
| <span data-ttu-id="8c1d6-249">**$author$**</span><span class="sxs-lookup"><span data-stu-id="8c1d6-249">**$author$**</span></span> | <span data-ttu-id="8c1d6-250">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="8c1d6-250">AssemblyInfo</span></span> | <span data-ttu-id="8c1d6-251">AssemblyCompany</span><span class="sxs-lookup"><span data-stu-id="8c1d6-251">AssemblyCompany</span></span> |
| <span data-ttu-id="8c1d6-252">**$title$**</span><span class="sxs-lookup"><span data-stu-id="8c1d6-252">**$title$**</span></span> | <span data-ttu-id="8c1d6-253">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="8c1d6-253">AssemblyInfo</span></span> | <span data-ttu-id="8c1d6-254">AssemblyTitle</span><span class="sxs-lookup"><span data-stu-id="8c1d6-254">AssemblyTitle</span></span> |
| <span data-ttu-id="8c1d6-255">**$description$**</span><span class="sxs-lookup"><span data-stu-id="8c1d6-255">**$description$**</span></span> | <span data-ttu-id="8c1d6-256">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="8c1d6-256">AssemblyInfo</span></span> | <span data-ttu-id="8c1d6-257">AssemblyDescription</span><span class="sxs-lookup"><span data-stu-id="8c1d6-257">AssemblyDescription</span></span> |
| <span data-ttu-id="8c1d6-258">**$copyright$**</span><span class="sxs-lookup"><span data-stu-id="8c1d6-258">**$copyright$**</span></span> | <span data-ttu-id="8c1d6-259">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="8c1d6-259">AssemblyInfo</span></span> | <span data-ttu-id="8c1d6-260">AssemblyCopyright</span><span class="sxs-lookup"><span data-stu-id="8c1d6-260">AssemblyCopyright</span></span> |
| <span data-ttu-id="8c1d6-261">**$configuration$**</span><span class="sxs-lookup"><span data-stu-id="8c1d6-261">**$configuration$**</span></span> | <span data-ttu-id="8c1d6-262">Assembly-DLL</span><span class="sxs-lookup"><span data-stu-id="8c1d6-262">Assembly DLL</span></span> | <span data-ttu-id="8c1d6-263">Konfiguration, die zur Erstellung der Assembly verwendet wird und standardmäßig auf „Debug“ festgelegt ist.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-263">Configuration used to build the assembly, defaulting to Debug.</span></span> <span data-ttu-id="8c1d6-264">Achten Sie darauf, dass Sie stets `-properties Configuration=Release` in der Befehlszeile verwenden, um mithilfe einer Releasekonfiguration ein Paket zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-264">Note that to create a package using a Release configuration, you always use `-properties Configuration=Release` on the command line.</span></span> |

<span data-ttu-id="8c1d6-265">Token können auch zum Auflösen von Pfaden verwendet werden, wenn Sie [Assemblydateien](#including-assembly-files) und [Inhaltsdateien](#including-content-files) hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-265">Tokens can also be used to resolve paths when you include [assembly files](#including-assembly-files) and [content files](#including-content-files).</span></span> <span data-ttu-id="8c1d6-266">Die Namen der Token und der MSBuild-Eigenschaften sind identisch, wodurch Sie abhängig von der aktuellen Buildkonfiguration Dateien auswählen können, die eingeschlossen werden sollen.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-266">The tokens have the same names as the MSBuild properties, making it possible to select files to be included depending on the current build configuration.</span></span> <span data-ttu-id="8c1d6-267">Wenn Sie beispielsweise die folgenden Token in der `.nuspec`-Datei verwenden</span><span class="sxs-lookup"><span data-stu-id="8c1d6-267">For example, if you use the following tokens in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="bin\$configuration$\$id$.pdb" target="lib\net40" />
</files>
```

<span data-ttu-id="8c1d6-268">und eine Assembly mit der `Release`-Konfiguration in MSBuild erstellen, deren `AssemblyName` den Wert `LoggingLibrary` hat, sehen die dadurch entstandenen Zeilen in der `.nuspec`-Datei in den Paketen wie folgt aus:</span><span class="sxs-lookup"><span data-stu-id="8c1d6-268">And you build an assembly whose `AssemblyName` is `LoggingLibrary` with the `Release` configuration in MSBuild, the resulting lines in the `.nuspec` file in the package is as follows:</span></span>

```xml
<files>
    <file src="bin\Release\LoggingLibrary.pdb" target="lib\net40" />
</files>
```

## <a name="dependencies-element"></a><span data-ttu-id="8c1d6-269">Abhängigkeitselement</span><span class="sxs-lookup"><span data-stu-id="8c1d6-269">Dependencies element</span></span>

<span data-ttu-id="8c1d6-270">Das `<dependencies>`-Element in `<metadata>` enthält eine beliebige Anzahl von `<dependency>`-Elementen, die andere Pakete angeben, von denen das Paket der obersten Ebene abhängig ist.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-270">The `<dependencies>` element within `<metadata>` contains any number of `<dependency>` elements that identify other packages upon which the top-level package depends.</span></span> <span data-ttu-id="8c1d6-271">Im Folgenden werden die Attribute für jede `<dependency>` dargestellt:</span><span class="sxs-lookup"><span data-stu-id="8c1d6-271">The attributes for each `<dependency>` are as follows:</span></span>

| <span data-ttu-id="8c1d6-272">Attribut</span><span class="sxs-lookup"><span data-stu-id="8c1d6-272">Attribute</span></span> | <span data-ttu-id="8c1d6-273">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="8c1d6-273">Description</span></span> |
| --- | --- |
| `id` | <span data-ttu-id="8c1d6-274">(Erforderlich) Paket-ID der Abhängigkeit, z.B. „EntityFramework“ und „NUnit“. Dies ist der Name des Pakets, der auf nuget.org auf einer Paketseite angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-274">(Required) The package ID of the dependency, such as "EntityFramework" and "NUnit", which is the name of the package nuget.org shows on a package page.</span></span> |
| `version` | <span data-ttu-id="8c1d6-275">(Erforderlich) Bereich an Versionen, die als Abhängigkeiten akzeptiert werden.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-275">(Required) The range of versions acceptable as a dependency.</span></span> <span data-ttu-id="8c1d6-276">Die genaue Syntax finden Sie unter [Version Ranges and Wildcards (Versionsbereiche und Platzhalter)](../reference/package-versioning.md#version-ranges-and-wildcards).</span><span class="sxs-lookup"><span data-stu-id="8c1d6-276">See [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards) for exact syntax.</span></span> |
| <span data-ttu-id="8c1d6-277">include</span><span class="sxs-lookup"><span data-stu-id="8c1d6-277">include</span></span> | <span data-ttu-id="8c1d6-278">Eine kommagetrennte Liste mit include- und exclude-Tags (siehe nachfolgende Tabelle), die die Abhängigkeit angibt, die in das endgültige Paket eingeschlossen werden soll.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-278">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to include in the final package.</span></span> <span data-ttu-id="8c1d6-279">Der Standardwert ist `all`.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-279">The default value is `all`.</span></span> |
| <span data-ttu-id="8c1d6-280">exclude</span><span class="sxs-lookup"><span data-stu-id="8c1d6-280">exclude</span></span> | <span data-ttu-id="8c1d6-281">Eine kommagetrennte Liste mit include- und exclude-Tags (siehe nachfolgende Tabelle), die die Abhängigkeit angibt, die aus dem endgültigen Paket ausgeschlossen werden soll.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-281">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to exclude in the final package.</span></span> <span data-ttu-id="8c1d6-282">Der Standardwert ist `build,analyzers`. Er kann überschrieben werden.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-282">The  default value is `build,analyzers` which can be over-written.</span></span> <span data-ttu-id="8c1d6-283">Allerdings werden implizit auch `content/ ContentFiles` aus dem endgültigen Paket ausgeschlossen, was sich nicht überschreiben lässt.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-283">But `content/ ContentFiles` are also implicitly excluded in the final package which can't be over-written.</span></span> <span data-ttu-id="8c1d6-284">`exclude`-Tags haben Vorrang vor `include`-Tags.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-284">Tags specified with `exclude` take precedence over those specified with `include`.</span></span> <span data-ttu-id="8c1d6-285">Beispielsweise hat `include="runtime, compile" exclude="compile"` die gleiche Wirkung wie `include="runtime"`.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-285">For example, `include="runtime, compile" exclude="compile"` is the same as `include="runtime"`.</span></span> |

| <span data-ttu-id="8c1d6-286">Include-/Exclude-Tag</span><span class="sxs-lookup"><span data-stu-id="8c1d6-286">Include/Exclude tag</span></span> | <span data-ttu-id="8c1d6-287">Betroffene Ordner auf dem Ziel</span><span class="sxs-lookup"><span data-stu-id="8c1d6-287">Affected folders of the target</span></span> |
| --- | --- |
| <span data-ttu-id="8c1d6-288">contentFiles</span><span class="sxs-lookup"><span data-stu-id="8c1d6-288">contentFiles</span></span> | <span data-ttu-id="8c1d6-289">Content</span><span class="sxs-lookup"><span data-stu-id="8c1d6-289">Content</span></span> |
| <span data-ttu-id="8c1d6-290">runtime</span><span class="sxs-lookup"><span data-stu-id="8c1d6-290">runtime</span></span> | <span data-ttu-id="8c1d6-291">Runtime, Resources und FrameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="8c1d6-291">Runtime, Resources, and FrameworkAssemblies</span></span> |
| <span data-ttu-id="8c1d6-292">compile</span><span class="sxs-lookup"><span data-stu-id="8c1d6-292">compile</span></span> | <span data-ttu-id="8c1d6-293">lib</span><span class="sxs-lookup"><span data-stu-id="8c1d6-293">lib</span></span> |
| <span data-ttu-id="8c1d6-294">Build</span><span class="sxs-lookup"><span data-stu-id="8c1d6-294">build</span></span> | <span data-ttu-id="8c1d6-295">Build (MSBuild-Eigenschaften und -Ziele)</span><span class="sxs-lookup"><span data-stu-id="8c1d6-295">build (MSBuild props and targets)</span></span> |
| <span data-ttu-id="8c1d6-296">native</span><span class="sxs-lookup"><span data-stu-id="8c1d6-296">native</span></span> | <span data-ttu-id="8c1d6-297">native</span><span class="sxs-lookup"><span data-stu-id="8c1d6-297">native</span></span> |
| <span data-ttu-id="8c1d6-298">none</span><span class="sxs-lookup"><span data-stu-id="8c1d6-298">none</span></span> | <span data-ttu-id="8c1d6-299">Keine Ordner</span><span class="sxs-lookup"><span data-stu-id="8c1d6-299">No folders</span></span> |
| <span data-ttu-id="8c1d6-300">all</span><span class="sxs-lookup"><span data-stu-id="8c1d6-300">all</span></span> | <span data-ttu-id="8c1d6-301">Alle Ordner</span><span class="sxs-lookup"><span data-stu-id="8c1d6-301">All folders</span></span> |

<span data-ttu-id="8c1d6-302">Beispielsweise verweisen die folgenden Zeilen auf Abhängigkeiten von `PackageA` Version 1.1.0 und höher und `PackageB` Version 1.x.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-302">For example, the following lines indicate dependencies on `PackageA` version 1.1.0 or higher, and `PackageB` version 1.x.</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" />
    <dependency id="PackageB" version="[1,2)" />
</dependencies>
```

<span data-ttu-id="8c1d6-303">In den folgenden Zeilen wird zwar auf Abhängigkeiten von denselben Paketen verwiesen, allerdings wird auch angegeben, dass die Ordner `contentFiles` und `build` aus `PackageA` sowie alle anderen Ordner bis auf `native` und `compile` aus `PackageB` eingeschlossen werden sollen.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-303">The following lines indicate dependencies on the same packages, but specify to include the `contentFiles` and `build` folders of `PackageA` and everything but the `native` and `compile` folders of `PackageB`"</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" include="contentFiles, build" />
    <dependency id="PackageB" version="[1,2)" exclude="native, compile" />
</dependencies>
```

<span data-ttu-id="8c1d6-304">Hinweis: Beim Erstellen einer `.nuspec` aus einem Projekt mit `nuget spec`, Abhängigkeiten, die in diesem Projekt vorhanden sind, sind automatisch im resultierenden enthalten `.nuspec` Datei.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-304">Note: When creating a `.nuspec` from a project using `nuget spec`, dependencies that exist in that project are automatically included in the resulting `.nuspec` file.</span></span>

### <a name="dependency-groups"></a><span data-ttu-id="8c1d6-305">Abhängigkeitsgruppen</span><span class="sxs-lookup"><span data-stu-id="8c1d6-305">Dependency groups</span></span>

<span data-ttu-id="8c1d6-306">*Version 2.0 und höher*</span><span class="sxs-lookup"><span data-stu-id="8c1d6-306">*Version 2.0+*</span></span>

<span data-ttu-id="8c1d6-307">Als Alternative zu einer einzelnen flachen Liste können Abhängigkeiten auf der Grundlage des Frameworkprofils des Zielprojekts mithilfe von `<group>`-Elementen in `<dependencies>` angegeben werden.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-307">As an alternative to a single flat list, dependencies can be specified according to the framework profile of the target project using `<group>` elements within `<dependencies>`.</span></span>

<span data-ttu-id="8c1d6-308">Jede Gruppe verfügt über ein Attribut mit dem Namen `targetFramework` und enthält null oder mehr `<dependency>`-Elemente.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-308">Each group has an attribute named `targetFramework` and contains zero or more `<dependency>` elements.</span></span> <span data-ttu-id="8c1d6-309">Diese Abhängigkeiten werden gemeinsam installiert, wenn das Zielframework kompatibel mit dem Frameworkprofil des Projekts ist.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-309">Those dependencies are installed together when  the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="8c1d6-310">Das `<group>`-Element ohne ein `targetFramework`-Attribut wird als Standard- oder Fallbackliste der Abhängigkeiten verwendet.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-310">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of dependencies.</span></span> <span data-ttu-id="8c1d6-311">Die genauen Frameworkbezeichner finden Sie unter [Zielframeworks](../reference/target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="8c1d6-311">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="8c1d6-312">Das Gruppenformat kann nicht mit einer flachen Liste vermischt werden.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-312">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="8c1d6-313">Im folgenden Beispiel werden verschiedene Variationen des `<group>`-Elements dargestellt:</span><span class="sxs-lookup"><span data-stu-id="8c1d6-313">The following example shows different variations of the `<group>` element:</span></span>

```xml
<dependencies>
    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>

    <group targetFramework="net40">
        <dependency id="jQuery" />
        <dependency id="WebActivator" />
    </group>

    <group targetFramework="sl30">
    </group>
</dependencies>
```

<a name="specifying-explicit-assembly-references"></a>

## <a name="explicit-assembly-references"></a><span data-ttu-id="8c1d6-314">Explizite Assemblyverweise</span><span class="sxs-lookup"><span data-stu-id="8c1d6-314">Explicit assembly references</span></span>

<span data-ttu-id="8c1d6-315">Die `<references>` Element dient der Projekte mit `packages.config` explizit auf die Assemblys angeben, die das Zielprojekt verweisen soll, wenn das Paket verwendet.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-315">The `<references>` element is used by projects using `packages.config` to explicitly specify the assemblies that the target project should reference when using the package.</span></span> <span data-ttu-id="8c1d6-316">In der Regel werden Verweise nur für Assemblys zur Entwurfszeit verwendet.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-316">Explicit references are typically used for design-time only assemblies.</span></span> <span data-ttu-id="8c1d6-317">Weitere Informationen finden Sie auf der Seite [Assemblys, die auf die verwiesen wird von Projekten auswählen](../create-packages/select-assemblies-referenced-by-projects.md) für Weitere Informationen.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-317">For more information, see the page on [selecting assemblies referenced by projects](../create-packages/select-assemblies-referenced-by-projects.md) for more information.</span></span>

<span data-ttu-id="8c1d6-318">Beispielsweise gibt das folgende `<references>`-Element NuGet die Anweisung, Verweise auch dann nur auf `xunit.dll` und `xunit.extensions.dll` hinzuzufügen, wenn zusätzliche Assemblys im Paket enthalten sind:</span><span class="sxs-lookup"><span data-stu-id="8c1d6-318">For example, the following `<references>` element instructs NuGet to add references to only `xunit.dll` and `xunit.extensions.dll` even if there are additional assemblies in the package:</span></span>

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

### <a name="reference-groups"></a><span data-ttu-id="8c1d6-319">Verweisgruppen</span><span class="sxs-lookup"><span data-stu-id="8c1d6-319">Reference groups</span></span>

<span data-ttu-id="8c1d6-320">Als Alternative zu einer einzelnen flachen Liste können mithilfe von `<group>`-Elementen in `<references>` Verweise auf der Grundlage des Frameworkprofils des Zielprojekts angegeben werden.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-320">As an alternative to a single flat list, references can be specified according to the framework profile of the target project using `<group>` elements within `<references>`.</span></span>

<span data-ttu-id="8c1d6-321">Jede Gruppe verfügt über ein Attribut namens `targetFramework` und enthält null oder mehr `<reference>`-Elemente.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-321">Each group has an attribute named `targetFramework` and contains zero or more `<reference>` elements.</span></span> <span data-ttu-id="8c1d6-322">Diese Verweise werden einem Projekt hinzugefügt, wenn das Zielframework mit dem Frameworkprofil des Projekts kompatibel ist.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-322">Those references are added to a project when the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="8c1d6-323">Das `<group>`-Element ohne `targetFramework`-Attribut wird als Standard- oder Fallbackliste für Verweise verwendet.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-323">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of references.</span></span> <span data-ttu-id="8c1d6-324">Die genauen Frameworkbezeichner finden Sie unter [Zielframeworks](../reference/target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="8c1d6-324">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="8c1d6-325">Das Gruppenformat kann nicht mit einer flachen Liste vermischt werden.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-325">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="8c1d6-326">Im folgenden Beispiel werden verschiedene Variationen des `<group>`-Elements dargestellt:</span><span class="sxs-lookup"><span data-stu-id="8c1d6-326">The following example shows different variations of the `<group>` element:</span></span>

```xml
<references>
    <group>
        <reference file="a.dll" />
    </group>

    <group targetFramework="net45">
        <reference file="b45.dll" />
    </group>

    <group targetFramework="netcore45">
        <reference file="bcore45.dll" />
    </group>
</references>
```

<a name="specifying-framework-assembly-references-gac"></a>

## <a name="framework-assembly-references"></a><span data-ttu-id="8c1d6-327">Verweise auf Frameworkassemblys</span><span class="sxs-lookup"><span data-stu-id="8c1d6-327">Framework assembly references</span></span>

<span data-ttu-id="8c1d6-328">Frameworkassemblys gehören zum .NET Framework und sollten für jeden vorhandenen Computer bereits im globalen Assemblycache vorhanden sein.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-328">Framework assemblies are those that are part of the .NET framework and should already be in the global assembly cache (GAC) for any given machine.</span></span> <span data-ttu-id="8c1d6-329">Durch Angabe dieser Assemblys im `<frameworkAssemblies>`-Element können Pakete sicherstellen, dass erforderliche Verweise einem Projekt hinzugefügt werden, falls das Projekt noch nicht über solche Verweise verfügt.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-329">By identifying those assemblies within the `<frameworkAssemblies>` element, a package can ensure that required references are added to a project in the event that the project doesn't have such references already.</span></span> <span data-ttu-id="8c1d6-330">Derartige Assemblys sind natürlich nicht von Anfang an in Paketen enthalten.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-330">Such assemblies, of course, are not included in a package directly.</span></span>

<span data-ttu-id="8c1d6-331">Das `<frameworkAssemblies>`-Element enthält null oder mehr `<frameworkAssembly>`-Elemente, die jeweils die folgenden Attribute angeben:</span><span class="sxs-lookup"><span data-stu-id="8c1d6-331">The `<frameworkAssemblies>` element contains zero or more `<frameworkAssembly>` elements, each of which specifies the following attributes:</span></span>

| <span data-ttu-id="8c1d6-332">Attribut</span><span class="sxs-lookup"><span data-stu-id="8c1d6-332">Attribute</span></span> | <span data-ttu-id="8c1d6-333">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="8c1d6-333">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8c1d6-334">**assemblyName**</span><span class="sxs-lookup"><span data-stu-id="8c1d6-334">**assemblyName**</span></span> | <span data-ttu-id="8c1d6-335">(Erforderlich) Vollqualifizierter Assemblyname.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-335">(Required) The fully qualified assembly name.</span></span> |
| <span data-ttu-id="8c1d6-336">**targetFramework**</span><span class="sxs-lookup"><span data-stu-id="8c1d6-336">**targetFramework**</span></span> | <span data-ttu-id="8c1d6-337">(Optional) Gibt das Zielframework an, auf das sich dieser Verweis bezieht.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-337">(Optional) Specifies the target framework to which this reference applies.</span></span> <span data-ttu-id="8c1d6-338">Das Fehlen des Attributs weist darauf hin, dass der Verweis für alle Frameworks gilt.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-338">If omitted, indicates that the reference applies to all frameworks.</span></span> <span data-ttu-id="8c1d6-339">Die genauen Frameworkbezeichner finden Sie unter [Zielframeworks](../reference/target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="8c1d6-339">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span> |

<span data-ttu-id="8c1d6-340">Das folgende Beispiel zeigt einen Verweis auf `System.Net` für alle Zielframeworks sowie einen weiteren Verweis auf `System.ServiceModel`, der ausschließlich für .NET Framework 4.0 gilt:</span><span class="sxs-lookup"><span data-stu-id="8c1d6-340">The following example shows a reference to `System.Net` for all target frameworks, and a reference to `System.ServiceModel` for .NET Framework 4.0 only:</span></span>

```xml
<frameworkAssemblies>
    <frameworkAssembly assemblyName="System.Net"  />

    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
</frameworkAssemblies>
```

<a name="specifying-files-to-include-in-the-package"></a>

## <a name="including-assembly-files"></a><span data-ttu-id="8c1d6-341">Einschließen von Assemblydateien</span><span class="sxs-lookup"><span data-stu-id="8c1d6-341">Including assembly files</span></span>

<span data-ttu-id="8c1d6-342">Wenn Sie die unter [Erstellen von NuGet-Paketen](../create-packages/creating-a-package.md) beschriebenen Konventionen beachten, müssen Sie nicht explizit eine Liste mit Dateien in der `.nuspec`-Datei angeben.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-342">If you follow the conventions described in [Creating a Package](../create-packages/creating-a-package.md), you do not have to explicitly specify a list of files in the `.nuspec` file.</span></span> <span data-ttu-id="8c1d6-343">Der `nuget pack`-Befehl ruft die benötigten Dateien automatisch ab.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-343">The `nuget pack` command automatically picks up the necessary files.</span></span>

> [!Important]
> <span data-ttu-id="8c1d6-344">Wenn ein Paket in einem Projekt installiert wird, fügt NuGet der DLL des Pakets automatisch Assemblyverweise hinzu. Verweise namens `.resources.dll` werden dabei allerdings *nicht* hinzugefügt, da angenommen wird, dass es sich dabei um lokalisierte Satellitenassemblys handelt.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-344">When a package is installed into a project, NuGet automatically adds assembly references to the package's DLLs, *excluding* those that are named `.resources.dll` because they are assumed to be localized satellite assemblies.</span></span> <span data-ttu-id="8c1d6-345">Vermeiden Sie aus diesem Grund die Verwendung von `.resources.dll` für Dateien, die darüber hinaus wichtigen Paketcode enthalten.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-345">For this reason, avoid using `.resources.dll` for files that otherwise contain essential package code.</span></span>

<span data-ttu-id="8c1d6-346">Wenn Sie diese automatischen Abläufe umgehen und explizit steuern möchten, welche Dateien in einem Paket enthalten sein sollen, legen Sie ein `<files>`-Element als untergeordnetes Element von `<package>` (und gleichgeordnetes Element von `<metadata>`) fest, das jede Datei mit einem separaten `<file>`-Element benennt.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-346">To bypass this automatic behavior and explicitly control which files are included in a package, place a `<files>` element as a child of `<package>` (and a sibling of `<metadata>`), identifying each file with a separate `<file>` element.</span></span> <span data-ttu-id="8c1d6-347">Zum Beispiel:</span><span class="sxs-lookup"><span data-stu-id="8c1d6-347">For example:</span></span>

```xml
<files>
    <file src="bin\Debug\*.dll" target="lib" />
    <file src="bin\Debug\*.pdb" target="lib" />
    <file src="tools\**\*.*" exclude="**\*.log" />
</files>
```

<span data-ttu-id="8c1d6-348">Das `<files>`-Element wird außerdem bei NuGet 2.x und früher sowie bei Projekten, die `packages.config` verwenden, zum Einschließen unveränderlicher Inhaltsdateien während der Paketinstallation benutzt.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-348">With NuGet 2.x and earlier, and projects using `packages.config`, the `<files>` element is also used to include immutable content files when a package is installed.</span></span> <span data-ttu-id="8c1d6-349">Seit NuGet 3.3 und bei Projekten, die PackageReference verwenden, wird stattdessen das `<contentFiles>`-Element verwendet.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-349">With NuGet 3.3+ and projects PackageReference, the `<contentFiles>` element is used instead.</span></span> <span data-ttu-id="8c1d6-350">Weitere Informationen finden Sie unter [Einschließen von Inhaltsdateien](#including-content-files).</span><span class="sxs-lookup"><span data-stu-id="8c1d6-350">See [Including content files](#including-content-files) below for details.</span></span>

### <a name="file-element-attributes"></a><span data-ttu-id="8c1d6-351">Dateielementattribute</span><span class="sxs-lookup"><span data-stu-id="8c1d6-351">File element attributes</span></span>

<span data-ttu-id="8c1d6-352">Jedes `<file>`-Element gibt die folgenden Attribute an:</span><span class="sxs-lookup"><span data-stu-id="8c1d6-352">Each `<file>` element specifies the following attributes:</span></span>

| <span data-ttu-id="8c1d6-353">Attribut</span><span class="sxs-lookup"><span data-stu-id="8c1d6-353">Attribute</span></span> | <span data-ttu-id="8c1d6-354">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="8c1d6-354">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8c1d6-355">**src**</span><span class="sxs-lookup"><span data-stu-id="8c1d6-355">**src**</span></span> | <span data-ttu-id="8c1d6-356">Speicherort der einzuschließenden Dateien. Hierbei werden die vom `exclude`-Attribut angegebenen Ausschlüsse berücksichtigt.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-356">The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="8c1d6-357">Der Pfad ist relativ zur `.nuspec`-Datei, sofern kein absoluter Pfad angegeben ist.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-357">The path is relative to the `.nuspec` file unless an absolute path is specified.</span></span> <span data-ttu-id="8c1d6-358">Das Platzhalterzeichen `*` ist zulässig, und das doppelte Platzhalterzeichen `**` impliziert eine rekursive Ordnersuche.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-358">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="8c1d6-359">**target**</span><span class="sxs-lookup"><span data-stu-id="8c1d6-359">**target**</span></span> | <span data-ttu-id="8c1d6-360">Relativer Pfad zu dem Ordner im Paket, in dem die Quelldateien abgelegt sind. Dieser muss mit `lib`, `content`, `build` oder `tools` beginnen.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-360">The relative path to the folder within the package where the source files are placed, which must begin with `lib`, `content`, `build`, or `tools`.</span></span> <span data-ttu-id="8c1d6-361">Informationen hierzu finden Sie unter [Erstellen der NUSPEC-Datei > Aus einem konventionsbasierten Arbeitsverzeichnis](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span><span class="sxs-lookup"><span data-stu-id="8c1d6-361">See [Creating a .nuspec from a convention-based working directory](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span></span> |
| <span data-ttu-id="8c1d6-362">**exclude**</span><span class="sxs-lookup"><span data-stu-id="8c1d6-362">**exclude**</span></span> | <span data-ttu-id="8c1d6-363">Eine mit Semikolons getrennte Datei oder ein Muster für Dateien, die aus dem `src`-Speicherort ausgeschlossen werden.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-363">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="8c1d6-364">Das Platzhalterzeichen `*` ist zulässig, und das doppelte Platzhalterzeichen `**` impliziert eine rekursive Ordnersuche.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-364">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |

### <a name="examples"></a><span data-ttu-id="8c1d6-365">Beispiele</span><span class="sxs-lookup"><span data-stu-id="8c1d6-365">Examples</span></span>

<span data-ttu-id="8c1d6-366">**Einzelne Assembly**</span><span class="sxs-lookup"><span data-stu-id="8c1d6-366">**Single assembly**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="library.dll" target="lib" />

    Packaged result:
        lib\library.dll

<span data-ttu-id="8c1d6-367">**Einzelne Assembly, die für ein Zielframework spezifisch ist**</span><span class="sxs-lookup"><span data-stu-id="8c1d6-367">**Single assembly specific to a target framework**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="assemblies\net40\library.dll" target="lib\net40" />

    Packaged result:
        lib\net40\library.dll

<span data-ttu-id="8c1d6-368">**Mehrere DLLs mit Verwendung eines Platzhalterzeichens**</span><span class="sxs-lookup"><span data-stu-id="8c1d6-368">**Set of DLLs using a wildcard**</span></span>

    Source files:
        bin\release\libraryA.dll
        bin\release\libraryB.dll

    .nuspec entry:
        <file src="bin\release\*.dll" target="lib" />

    Packaged result:
        lib\libraryA.dll
        lib\libraryB.dll

<span data-ttu-id="8c1d6-369">**DLLs für verschiedene Frameworks**</span><span class="sxs-lookup"><span data-stu-id="8c1d6-369">**DLLs for different frameworks**</span></span>

    Source files:
        lib\net40\library.dll
        lib\net20\library.dll

    .nuspec entry (using ** recursive search):
        <file src="lib\**" target="lib" />

    Packaged result:
        lib\net40\library.dll
        lib\net20\library.dll

<span data-ttu-id="8c1d6-370">**Ausschließen von Dateien**</span><span class="sxs-lookup"><span data-stu-id="8c1d6-370">**Excluding files**</span></span>

    Source files:
        \tools\fileA.bak
        \tools\fileB.bak
        \tools\fileA.log
        \tools\build\fileB.log

    .nuspec entries:
        <file src="tools\*.*" target="tools" exclude="tools\*.bak" />
        <file src="tools\**\*.*" target="tools" exclude="**\*.log" />

    Package result:
        (no files)

## <a name="including-content-files"></a><span data-ttu-id="8c1d6-371">Einschließen von Inhaltsdateien</span><span class="sxs-lookup"><span data-stu-id="8c1d6-371">Including content files</span></span>

<span data-ttu-id="8c1d6-372">Bei Inhaltsdateien handelt es sich um unveränderliche Dateien, die ein Paket in ein Projekt einschließen muss.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-372">Content files are immutable files that a package needs to include in a project.</span></span> <span data-ttu-id="8c1d6-373">Da sie unveränderlich sind, sollten sie auch nicht von dem verarbeitenden Projekt geändert werden.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-373">Being immutable, they are not intended to be modified by the consuming project.</span></span> <span data-ttu-id="8c1d6-374">Zu den Inhaltsdateien gehören z.B.:</span><span class="sxs-lookup"><span data-stu-id="8c1d6-374">Example content files include:</span></span>

- <span data-ttu-id="8c1d6-375">Bilder, die als Ressourcen eingebettet werden</span><span class="sxs-lookup"><span data-stu-id="8c1d6-375">Images that are embedded as resources</span></span>
- <span data-ttu-id="8c1d6-376">bereits kompilierte Quelldateien</span><span class="sxs-lookup"><span data-stu-id="8c1d6-376">Source files that are already compiled</span></span>
- <span data-ttu-id="8c1d6-377">Skripts, die in die Buildausgabe des Projekts eingeschlossen werden müssen</span><span class="sxs-lookup"><span data-stu-id="8c1d6-377">Scripts that need to be included with the build output of the project</span></span>
- <span data-ttu-id="8c1d6-378">Konfigurationsdateien für das Paket, die zwar in das Projekt eingeschlossen werden müssen, an denen jedoch keine projektspezifischen Änderungen vorgenommen werden müssen</span><span class="sxs-lookup"><span data-stu-id="8c1d6-378">Configuration files for the package that need to be included in the project but don't need any project-specific changes</span></span>

<span data-ttu-id="8c1d6-379">Inhaltsdateien werden mithilfe eines `<files>`-Elements in ein Paket eingeschlossen. Dieses Element gibt den `content`-Ordner im `target`-Attribut an.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-379">Content files are included in a package using the `<files>` element, specifying the `content` folder in the `target` attribute.</span></span> <span data-ttu-id="8c1d6-380">Allerdings werden diese Dateien ignoriert, wenn das Paket per PackageReference in einem Projekt installiert wird, das stattdessen das `<contentFiles>`-Element verwendet.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-380">However, such files are ignored when the package is installed in a project using PackageReference, which instead uses the `<contentFiles>` element.</span></span>

<span data-ttu-id="8c1d6-381">Im Idealfall geben Pakete die Inhaltsdateien in beiden Elementen an, um ein Höchstmaß an Kompatibilität mit den verarbeitenden Projekten zu erreichen.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-381">For maximum compatibility with consuming projects, a package ideally specifies the content files in both elements.</span></span>

### <a name="using-the-files-element-for-content-files"></a><span data-ttu-id="8c1d6-382">Verwenden des Dateielements für Inhaltsdateien</span><span class="sxs-lookup"><span data-stu-id="8c1d6-382">Using the files element for content files</span></span>

<span data-ttu-id="8c1d6-383">Verwenden Sie für Inhaltsdateien einfach dasselbe Format wie für Assemblydateien. Geben Sie dabei allerdings  wie in den folgenden Beispielen dargestellt `content` als Basisordner im `target`-Attribut an.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-383">For content files, simply use the same format as for assembly files, but specify `content` as the base folder in the `target` attribute as shown in the following examples.</span></span>

<span data-ttu-id="8c1d6-384">**Grundlegende Inhaltsdateien**</span><span class="sxs-lookup"><span data-stu-id="8c1d6-384">**Basic content files**</span></span>

    Source files:
        css\mobile\style1.css
        css\mobile\style2.css

    .nuspec entry:
        <file src="css\mobile\*.css" target="content\css\mobile" />

    Packaged result:
        content\css\mobile\style1.css
        content\css\mobile\style2.css

<span data-ttu-id="8c1d6-385">**Inhaltsdateien mit Verzeichnisstruktur**</span><span class="sxs-lookup"><span data-stu-id="8c1d6-385">**Content files with directory structure**</span></span>

    Source files:
        css\mobile\style.css
        css\mobile\wp7\style.css
        css\browser\style.css

    .nuspec entry:
        <file src="css\**\*.css" target="content\css" />

    Packaged result:
        content\css\mobile\style.css
        content\css\mobile\wp7\style.css
        content\css\browser\style.css

<span data-ttu-id="8c1d6-386">**Inhaltsdatei für ein bestimmtes Zielframework**</span><span class="sxs-lookup"><span data-stu-id="8c1d6-386">**Content file specific to a target framework**</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry
        <file src="css\cool\style.css" target="Content" />

    Packaged result:
        content\style.css

<span data-ttu-id="8c1d6-387">**Inhaltsdatei, die in einen Ordner mit einem Punkt im Namen kopiert wird**</span><span class="sxs-lookup"><span data-stu-id="8c1d6-387">**Content file copied to a folder with dot in name**</span></span>

<span data-ttu-id="8c1d6-388">In diesem Fall erkennt NuGet, dass die Erweiterung in `target` nicht mit der Erweiterung in `src` übereinstimmt, und behandelt diesen Namensbestandteil in `target` als Ordner:</span><span class="sxs-lookup"><span data-stu-id="8c1d6-388">In this case, NuGet sees that the extension in `target` does not match the extension in `src` and thus treats that part of the name in `target` as a folder:</span></span>

    Source file:
        images\picture.png

    .nuspec entry:
        <file src="images\picture.png" target="Content\images\package.icons" />

    Packaged result:
        content\images\package.icons\picture.png

<span data-ttu-id="8c1d6-389">**Inhaltsdateien ohne Erweiterungen**</span><span class="sxs-lookup"><span data-stu-id="8c1d6-389">**Content files without extensions**</span></span>

<span data-ttu-id="8c1d6-390">Verwenden Sie die Platzhalterzeichen `*` oder `**`, um Dateien ohne Erweiterungen einzuschließen:</span><span class="sxs-lookup"><span data-stu-id="8c1d6-390">To include files without an extension, use the `*` or `**` wildcards:</span></span>

    Source file:
        flags\installed

    .nuspec entry:
        <file src="flags\**" target="flags" />

    Packaged result:
        flags\installed

<span data-ttu-id="8c1d6-391">**Inhaltsdateien mit langen Pfaden und langen Zielen**</span><span class="sxs-lookup"><span data-stu-id="8c1d6-391">**Content files with deep path and deep target**</span></span>

<span data-ttu-id="8c1d6-392">In diesem Fall nimmt NuGet an, dass das Ziel ein Dateiname und kein Ordner ist, da die Dateierweiterungen von Quelle und Ziel übereinstimmen:</span><span class="sxs-lookup"><span data-stu-id="8c1d6-392">In this case, because the file extensions of the source and target match, NuGet assumes that the target is a file name and not a folder:</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry:
        <file src="css\cool\style.css" target="Content\css\cool" />
        or:
        <file src="css\cool\style.css" target="Content\css\cool\style.css" />

    Packaged result:
        content\css\cool\style.css

<span data-ttu-id="8c1d6-393">**Umbenennen einer Inhaltsdatei im Paket**</span><span class="sxs-lookup"><span data-stu-id="8c1d6-393">**Renaming a content file in the package**</span></span>

    Source file:
        ie\css\style.css

    .nuspec entry:
        <file src="ie\css\style.css" target="Content\css\ie.css" />

    Packaged result:
        content\css\ie.css

<span data-ttu-id="8c1d6-394">**Ausschließen von Dateien**</span><span class="sxs-lookup"><span data-stu-id="8c1d6-394">**Excluding files**</span></span>

    Source file:
        docs\*.txt (multiple files)

    .nuspec entry:
        <file src="docs\*.txt" target="content\docs" exclude="docs\admin.txt" />
        or
        <file src="*.txt" target="content\docs" exclude="admin.txt;log.txt" />

    Packaged result:
        All .txt files from docs except admin.txt (first example)
        All .txt files from docs except admin.txt and log.txt (second example)

<a name="using-contentfiles-element-for-content-files"></a>

### <a name="using-the-contentfiles-element-for-content-files"></a><span data-ttu-id="8c1d6-395">Verwenden des contentFiles-Elements für Inhaltsdateien</span><span class="sxs-lookup"><span data-stu-id="8c1d6-395">Using the contentFiles element for content files</span></span>

<span data-ttu-id="8c1d6-396">*NuGet 4.0 und höher mit PackageReference*</span><span class="sxs-lookup"><span data-stu-id="8c1d6-396">*NuGet 4.0+ with PackageReference*</span></span>

<span data-ttu-id="8c1d6-397">Standardmäßig legen Pakete Inhalte in einem `contentFiles`-Ordner (siehe unten) ab, in den `nuget pack` alle Dateien mithilfe von Standardattributen eingeschlossen hat.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-397">By default, a package places content in a `contentFiles` folder (see below) and `nuget pack` included all files in that folder using default attributes.</span></span> <span data-ttu-id="8c1d6-398">In diesem Fall ist es gar nicht notwendig, einen `contentFiles`-Knoten in `.nuspec` einzuschließen.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-398">In this case it's not necessary to include a `contentFiles` node in the `.nuspec` at all.</span></span>

<span data-ttu-id="8c1d6-399">Um zu steuern, welche Dateien eingeschlossen werden, gibt das `<contentFiles>`-Element eine Sammlung mit `<files>`-Elementen an, die die einzuschließenden Dateien präzise angeben.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-399">To control which files are included, the `<contentFiles>` element specifies is a collection of `<files>` elements that identify the exact files include.</span></span>

<span data-ttu-id="8c1d6-400">Die Angabe der Dateien erfolgt mithilfe mehrerer Attribute, die beschreiben, wie sie im Projektsystem verwendet werden sollen:</span><span class="sxs-lookup"><span data-stu-id="8c1d6-400">These files are specified with a set of attributes that describe how they should be used within the project system:</span></span>

| <span data-ttu-id="8c1d6-401">Attribut</span><span class="sxs-lookup"><span data-stu-id="8c1d6-401">Attribute</span></span> | <span data-ttu-id="8c1d6-402">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="8c1d6-402">Description</span></span> |
| --- | --- |
| <span data-ttu-id="8c1d6-403">**include**</span><span class="sxs-lookup"><span data-stu-id="8c1d6-403">**include**</span></span> | <span data-ttu-id="8c1d6-404">(Erforderlich) Speicherort der Dateien, die eingeschlossen werden sollen. Hierbei werden die vom `exclude`-Attribut angegebenen Ausschlüsse berücksichtigt.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-404">(Required) The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="8c1d6-405">Der Pfad ist relativ zur `.nuspec`-Datei, sofern kein absoluter Pfad angegeben ist.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-405">The path is relative to the `.nuspec` file unless an absolute path is specified.</span></span> <span data-ttu-id="8c1d6-406">Das Platzhalterzeichen `*` ist zulässig, und das doppelte Platzhalterzeichen `**` impliziert eine rekursive Ordnersuche.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-406">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="8c1d6-407">**exclude**</span><span class="sxs-lookup"><span data-stu-id="8c1d6-407">**exclude**</span></span> | <span data-ttu-id="8c1d6-408">Eine mit Semikolons getrennte Datei oder ein Muster für Dateien, die aus dem `src`-Speicherort ausgeschlossen werden.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-408">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="8c1d6-409">Das Platzhalterzeichen `*` ist zulässig, und das doppelte Platzhalterzeichen `**` impliziert eine rekursive Ordnersuche.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-409">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="8c1d6-410">**buildAction**</span><span class="sxs-lookup"><span data-stu-id="8c1d6-410">**buildAction**</span></span> | <span data-ttu-id="8c1d6-411">Die Buildaktion, die dem Inhaltselement für MSBuild zugewiesen werden soll, z.B. `Content`, `None`, `Embedded Resource` oder `Compile`. Die Standardeinstellung ist `Compile`.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-411">The build action to assign to the content item for MSBuild, such as `Content`, `None`, `Embedded Resource`, `Compile`, etc. The default is `Compile`.</span></span> |
| <span data-ttu-id="8c1d6-412">**copyToOutput**</span><span class="sxs-lookup"><span data-stu-id="8c1d6-412">**copyToOutput**</span></span> | <span data-ttu-id="8c1d6-413">Boolescher Wert, mit dem angegeben wird, ob Inhaltselemente in den Buildausgabeordner (oder den Veröffentlichungsausgabeordner) kopiert werden sollen.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-413">A Boolean indicating whether to copy content items to the build (or publish) output folder.</span></span> <span data-ttu-id="8c1d6-414">Der Standardwert ist FALSE.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-414">The default is false.</span></span> |
| <span data-ttu-id="8c1d6-415">**flatten**</span><span class="sxs-lookup"><span data-stu-id="8c1d6-415">**flatten**</span></span> | <span data-ttu-id="8c1d6-416">Boolescher Wert, der angibt, ob Inhaltselemente in einen Ordner in der Buildausgabe kopiert werden sollen (TRUE) oder die Ordnerstruktur in den Paketen beibehalten werden soll (FALSE).</span><span class="sxs-lookup"><span data-stu-id="8c1d6-416">A Boolean indicating whether to copy content items to a single folder in the build output (true), or to preserve the folder structure in the package (false).</span></span> <span data-ttu-id="8c1d6-417">Dieses Flag funktioniert nur, wenn das copyToOutput-Flag auf TRUE festgelegt ist.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-417">This flag only works when copyToOutput flag is set to true.</span></span> <span data-ttu-id="8c1d6-418">Der Standardwert ist FALSE.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-418">The default is false.</span></span> |

<span data-ttu-id="8c1d6-419">Beim Installieren eines Pakets wendet NuGet die untergeordneten Elemente von `<contentFiles>` von oben nach unten an.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-419">When installing a package, NuGet applies the child elements of `<contentFiles>` from top to bottom.</span></span> <span data-ttu-id="8c1d6-420">Wenn mehrere Einträge derselben Datei entsprechen, werden sie alle angewendet.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-420">If multiple entries match the same file then all entries are applied.</span></span> <span data-ttu-id="8c1d6-421">Der oberste Eintrag hat im Falle eines Attributkonflikts Vorrang vor den untergeordneten Einträgen.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-421">The top-most entry overrides the lower entries if there is a conflict for the same attribute.</span></span>

#### <a name="package-folder-structure"></a><span data-ttu-id="8c1d6-422">Paketordnerstruktur</span><span class="sxs-lookup"><span data-stu-id="8c1d6-422">Package folder structure</span></span>

<span data-ttu-id="8c1d6-423">Das Paketprojekt sollte Inhalte anhand des folgenden Musters strukturieren:</span><span class="sxs-lookup"><span data-stu-id="8c1d6-423">The package project should structure content using the following pattern:</span></span>

    /contentFiles/{codeLanguage}/{TxM}/{any?}

- <span data-ttu-id="8c1d6-424">`codeLanguages` kann `cs`, `vb`, `fs`, `any` oder das klein geschriebene Äquivalent einer `$(ProjectLanguage)` sein.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-424">`codeLanguages` may be `cs`, `vb`, `fs`, `any`, or the lowercase equivalent of a given `$(ProjectLanguage)`</span></span>
- <span data-ttu-id="8c1d6-425">`TxM` ist ein für das Zielframework zulässiger Moniker, den NuGet unterstützt (Informationen hierzu finden Sie unter [Zielframeworks](../reference/target-frameworks.md)).</span><span class="sxs-lookup"><span data-stu-id="8c1d6-425">`TxM` is any legal target framework moniker that NuGet supports (see [Target frameworks](../reference/target-frameworks.md)).</span></span>
- <span data-ttu-id="8c1d6-426">Ans Ende dieser Syntax kann eine beliebige Ordnerstruktur angehängt werden.</span><span class="sxs-lookup"><span data-stu-id="8c1d6-426">Any folder structure may be appended to the end of this syntax.</span></span>

<span data-ttu-id="8c1d6-427">Zum Beispiel:</span><span class="sxs-lookup"><span data-stu-id="8c1d6-427">For example:</span></span>

    Language- and framework-agnostic:
        /contentFiles/any/any/config.xml

    net45 content for all languages
        /contentFiles/any/net45/config.xml

    C#-specific content for net45 and up
        /contentFiles/cs/net45/sample.cs

<span data-ttu-id="8c1d6-428">Für leere Ordner kann `.` eingefügt werden, wenn diese keine Inhalte mehr für bestimmte Sprachen und TxM bereitstellen sollen. Zum Beispiel:</span><span class="sxs-lookup"><span data-stu-id="8c1d6-428">Empty folders can use `.` to opt out of providing content for certain combinations of language and TxM, for example:</span></span>

    /contentFiles/vb/any/code.vb
    /contentFiles/cs/any/.

#### <a name="example-contentfiles-section"></a><span data-ttu-id="8c1d6-429">contentFiles-Beispielabschnitt</span><span class="sxs-lookup"><span data-stu-id="8c1d6-429">Example contentFiles section</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        ...
        <contentFiles>
            <!-- Embed image resources -->
            <files include="any/any/images/dnf.png" buildAction="EmbeddedResource" />
            <files include="any/any/images/ui.png" buildAction="EmbeddedResource" />

            <!-- Embed all image resources under contentFiles/cs/ -->
            <files include="cs/**/*.png" buildAction="EmbeddedResource" />

            <!-- Copy config.xml to the root of the output folder -->
            <files include="cs/uap/config/config.xml" buildAction="None" copyToOutput="true" flatten="true" />

            <!-- Copy run.cmd to the output folder and keep the directory structure -->
            <files include="cs/commands/run.cmd" buildAction="None" copyToOutput="true" flatten="false" />

            <!-- Include everything in the scripts folder except exe files -->
            <files include="cs/net45/scripts/*" exclude="**/*.exe"  buildAction="None" copyToOutput="true" />
        </contentFiles>
        </metadata>
</package>
```

## <a name="example-nuspec-files"></a><span data-ttu-id="8c1d6-430">NUSPEC-Beispieldateien</span><span class="sxs-lookup"><span data-stu-id="8c1d6-430">Example nuspec files</span></span>

<span data-ttu-id="8c1d6-431">**Einfache `.nuspec`-Datei, die weder Abhängigkeiten noch Dateien enthält**</span><span class="sxs-lookup"><span data-stu-id="8c1d6-431">**A simple `.nuspec` that does not specify dependencies or files**</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>sample</id>
        <version>1.2.3</version>
        <authors>Kim Abercrombie, Franck Halmaert</authors>
        <description>Sample exists only to show a sample .nuspec file.</description>
        <language>en-US</language>
        <projectUrl>http://xunit.codeplex.com/</projectUrl>
        <license type="expression">MIT</license>
    </metadata>
</package>
```

<span data-ttu-id="8c1d6-432">**`.nuspec`-Datei mit Abhängigkeiten**</span><span class="sxs-lookup"><span data-stu-id="8c1d6-432">**A `.nuspec` with dependencies**</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>sample</id>
        <version>1.0.0</version>
        <authors>Microsoft</authors>
        <dependencies>
            <dependency id="another-package" version="3.0.0" />
            <dependency id="yet-another-package" version="1.0.0" />
        </dependencies>
    </metadata>
</package>
```

<span data-ttu-id="8c1d6-433">**`.nuspec`-Datei mit Dateien**</span><span class="sxs-lookup"><span data-stu-id="8c1d6-433">**A `.nuspec` with files**</span></span>

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>routedebugger</id>
        <version>1.0.0</version>
        <authors>Jay Hamlin</authors>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Route Debugger is a little utility I wrote...</description>
    </metadata>
    <files>
        <file src="bin\Debug\*.dll" target="lib" />
    </files>
</package>
```

<span data-ttu-id="8c1d6-434">**`.nuspec`-Datei mit Frameworkassemblys**</span><span class="sxs-lookup"><span data-stu-id="8c1d6-434">**A `.nuspec` with framework assemblies**</span></span>

```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <id>PackageWithGacReferences</id>
        <version>1.0</version>
        <authors>Author here</authors>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>
            A package that has framework assemblyReferences depending
            on the target framework.
        </description>
        <frameworkAssemblies>
            <frameworkAssembly assemblyName="System.Web" targetFramework="net40" />
            <frameworkAssembly assemblyName="System.Net" targetFramework="net40-client, net40" />
            <frameworkAssembly assemblyName="Microsoft.Devices.Sensors" targetFramework="sl4-wp" />
            <frameworkAssembly assemblyName="System.Json" targetFramework="sl3" />
        </frameworkAssemblies>
    </metadata>
</package>
```

<span data-ttu-id="8c1d6-435">In diesem Beispiel werden die folgenden Elemente für bestimmte Projektziele installiert:</span><span class="sxs-lookup"><span data-stu-id="8c1d6-435">In this example, the following are installed for specific project targets:</span></span>

- <span data-ttu-id="8c1d6-436">.NET4: `System.Web` und `System.Net`</span><span class="sxs-lookup"><span data-stu-id="8c1d6-436">.NET4 -> `System.Web`, `System.Net`</span></span>
- <span data-ttu-id="8c1d6-437">.NET4-Clientprofil: `System.Net`</span><span class="sxs-lookup"><span data-stu-id="8c1d6-437">.NET4 Client Profile -> `System.Net`</span></span>
- <span data-ttu-id="8c1d6-438">Silverlight 3: `System.Json`</span><span class="sxs-lookup"><span data-stu-id="8c1d6-438">Silverlight 3 -> `System.Json`</span></span>
- <span data-ttu-id="8c1d6-439">WindowsPhone: `Microsoft.Devices.Sensors`</span><span class="sxs-lookup"><span data-stu-id="8c1d6-439">WindowsPhone -> `Microsoft.Devices.Sensors`</span></span>
