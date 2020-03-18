---
title: NUSPEC-Dateireferenz für NuGet
description: Die NUSPEC-Datei enthält Paketmetadaten, die bei der Erstellung eines Pakets verwendet werden, um für die Paketbenutzer Informationen bereitzustellen.
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 19e7934e2f249056c532369fa5e8ee6e35cc8086
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/16/2020
ms.locfileid: "79428378"
---
# <a name="nuspec-reference"></a><span data-ttu-id="513b3-103">NUSPEC-Referenz</span><span class="sxs-lookup"><span data-stu-id="513b3-103">.nuspec reference</span></span>

<span data-ttu-id="513b3-104">Bei einer `.nuspec`-Datei handelt es sich um eine XML-Manifestdatei, die Paketmetadaten enthält.</span><span class="sxs-lookup"><span data-stu-id="513b3-104">A `.nuspec` file is an XML manifest that contains package metadata.</span></span> <span data-ttu-id="513b3-105">Diese Manifestdatei wird sowohl für die Erstellung des Pakets als auch zur Bereitstellung von Informationen für die Benutzer verwendet.</span><span class="sxs-lookup"><span data-stu-id="513b3-105">This manifest is used both to build the package and to provide information to consumers.</span></span> <span data-ttu-id="513b3-106">Manifestdateien sind in allen Paketen enthalten.</span><span class="sxs-lookup"><span data-stu-id="513b3-106">The manifest is always included in a package.</span></span>

<span data-ttu-id="513b3-107">Inhalte dieses Themas:</span><span class="sxs-lookup"><span data-stu-id="513b3-107">In this topic:</span></span>

- [<span data-ttu-id="513b3-108">Allgemeine Form und Schema</span><span class="sxs-lookup"><span data-stu-id="513b3-108">General form and schema</span></span>](#general-form-and-schema)
- <span data-ttu-id="513b3-109">[Ersetzungstokens](#replacement-tokens) (bei der Verwendung in einem Visual Studio-Projekt)</span><span class="sxs-lookup"><span data-stu-id="513b3-109">[Replacement tokens](#replacement-tokens) (when used with a Visual Studio project)</span></span>
- [<span data-ttu-id="513b3-110">Abhängigkeiten</span><span class="sxs-lookup"><span data-stu-id="513b3-110">Dependencies</span></span>](#dependencies)
- [<span data-ttu-id="513b3-111">Explizite Assemblyverweise</span><span class="sxs-lookup"><span data-stu-id="513b3-111">Explicit assembly references</span></span>](#explicit-assembly-references)
- [<span data-ttu-id="513b3-112">Verweise auf Frameworkassemblys</span><span class="sxs-lookup"><span data-stu-id="513b3-112">Framework assembly references</span></span>](#framework-assembly-references)
- [<span data-ttu-id="513b3-113">Einfügen von Assemblydateien</span><span class="sxs-lookup"><span data-stu-id="513b3-113">Including assembly files</span></span>](#including-assembly-files)
- [<span data-ttu-id="513b3-114">Einfügen von Inhaltsdateien</span><span class="sxs-lookup"><span data-stu-id="513b3-114">Including content files</span></span>](#including-content-files)
- [<span data-ttu-id="513b3-115">Nuspec-Beispieldateien</span><span class="sxs-lookup"><span data-stu-id="513b3-115">Example nuspec files</span></span>](#example-nuspec-files)

## <a name="project-type-compatibility"></a><span data-ttu-id="513b3-116">Projekttyp Kompatibilität</span><span class="sxs-lookup"><span data-stu-id="513b3-116">Project type compatibility</span></span>

- <span data-ttu-id="513b3-117">Verwenden Sie `.nuspec` mit `nuget.exe pack` für Projekte ohne SDK-Stil, die `packages.config`verwenden.</span><span class="sxs-lookup"><span data-stu-id="513b3-117">Use `.nuspec` with `nuget.exe pack` for non-SDK-style projects that use `packages.config`.</span></span>

- <span data-ttu-id="513b3-118">Eine `.nuspec`-Datei ist nicht erforderlich, um Pakete für [Projekte im SDK-Stil](../resources/check-project-format.md) zu erstellen (in der Regel .net Core-und .NET Standard-Projekte, die das [SDK-Attribut](/dotnet/core/tools/csproj#additions)verwenden).</span><span class="sxs-lookup"><span data-stu-id="513b3-118">A `.nuspec` file is not required to create packages for [SDK-style projects](../resources/check-project-format.md) (typically .NET Core and .NET Standard projects that use the [SDK attribute](/dotnet/core/tools/csproj#additions)).</span></span> <span data-ttu-id="513b3-119">(Beachten Sie, dass ein `.nuspec` generiert wird, wenn Sie das Paket erstellen.)</span><span class="sxs-lookup"><span data-stu-id="513b3-119">(Note that a `.nuspec` is generated when you create the package.)</span></span>

   <span data-ttu-id="513b3-120">Wenn Sie ein Paket mit `dotnet.exe pack` oder `msbuild pack target`erstellen, empfiehlt es sich, stattdessen [alle Eigenschaften](../reference/msbuild-targets.md#pack-target) , die normalerweise in der `.nuspec`-Datei enthalten sind, in die Projektdatei einzubeziehen.</span><span class="sxs-lookup"><span data-stu-id="513b3-120">If you are creating a package using `dotnet.exe pack` or `msbuild pack target`, we recommend that you [include all the properties](../reference/msbuild-targets.md#pack-target) that are usually in the `.nuspec` file in the project file instead.</span></span> <span data-ttu-id="513b3-121">Stattdessen können Sie jedoch auch [eine `.nuspec` Datei verwenden, um Sie mit `dotnet.exe` oder `msbuild pack target`zu verpacken ](../reference/msbuild-targets.md#packing-using-a-nuspec).</span><span class="sxs-lookup"><span data-stu-id="513b3-121">However, you can instead choose to [use a `.nuspec` file to pack using `dotnet.exe` or `msbuild pack target`](../reference/msbuild-targets.md#packing-using-a-nuspec).</span></span>

- <span data-ttu-id="513b3-122">Für Projekte, die von `packages.config` zu [packagereferenzierung](../consume-packages/package-references-in-project-files.md)migriert wurden, ist eine `.nuspec` Datei zum Erstellen des Pakets nicht erforderlich.</span><span class="sxs-lookup"><span data-stu-id="513b3-122">For projects migrated from `packages.config` to [PackageReference](../consume-packages/package-references-in-project-files.md), a `.nuspec` file is not required to create the package.</span></span> <span data-ttu-id="513b3-123">Verwenden Sie stattdessen [msbuild-t:Pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).</span><span class="sxs-lookup"><span data-stu-id="513b3-123">Instead, use [msbuild -t:pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration).</span></span>

## <a name="general-form-and-schema"></a><span data-ttu-id="513b3-124">Allgemeine Form und Schema</span><span class="sxs-lookup"><span data-stu-id="513b3-124">General form and schema</span></span>

<span data-ttu-id="513b3-125">Die aktuelle `nuspec.xsd`-Schemadatei finden Sie im [NuGet GitHub-Repository](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span><span class="sxs-lookup"><span data-stu-id="513b3-125">The current `nuspec.xsd` schema file can be found in the [NuGet GitHub repository](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span></span>

<span data-ttu-id="513b3-126">Für dieses Schema gilt die im Folgenden dargestellte allgemeine Form für die `.nuspec`-Datei:</span><span class="sxs-lookup"><span data-stu-id="513b3-126">Within this schema, a `.nuspec` file has the following general form:</span></span>

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

<span data-ttu-id="513b3-127">Für eine übersichtliche Darstellung des Schemas öffnen Sie die Schemadatei im Entwurfsmodus in Visual Studio, und klicken Sie auf den Link **XML-Schema-Explorer**.</span><span class="sxs-lookup"><span data-stu-id="513b3-127">For a clear visual representation of the schema, open the schema file in Visual Studio in Design mode and click on the **XML Schema Explorer** link.</span></span> <span data-ttu-id="513b3-128">Alternativ können Sie auch die Datei als Code öffnen, mit der rechten Maustaste in den Editor klicken und **Show XML Schema Explorer** (XML-Schema-Explorer anzeigen) auswählen.</span><span class="sxs-lookup"><span data-stu-id="513b3-128">Alternately, open the file as code, right-click in the editor, and select **Show XML Schema Explorer**.</span></span> <span data-ttu-id="513b3-129">In beiden Fällen wird eine Ansicht zurückgegeben, die der in der folgenden Abbildung ähnlich ist, wenn Sie größtenteils erweitert ist:</span><span class="sxs-lookup"><span data-stu-id="513b3-129">Either way you get a view like the one below (when mostly expanded):</span></span>

![Visual Studio-Schema-Explorer mit geöffneter „nuspec.xsd“-Datei](media/SchemaExplorer.png)

### <a name="required-metadata-elements"></a><span data-ttu-id="513b3-131">Erforderliche Metadatenelemente</span><span class="sxs-lookup"><span data-stu-id="513b3-131">Required metadata elements</span></span>

<span data-ttu-id="513b3-132">Obwohl es sich bei den folgenden Elementen um die Mindestanforderungen für ein Paket handelt, sollten Sie in Erwägung ziehen, die [optionalen Metadatenelemente](#optional-metadata-elements) hinzuzufügen, damit Entwicklern die Arbeit mit Ihren Paketen erleichtert wird.</span><span class="sxs-lookup"><span data-stu-id="513b3-132">Although the following elements are the minimum requirements for a package, you should consider adding the [optional metadata elements](#optional-metadata-elements) to improve the overall experience developers have with your package.</span></span> 

<span data-ttu-id="513b3-133">Diese Elemente müssen in einem `<metadata>`-Element angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="513b3-133">These elements must appear within a `<metadata>` element.</span></span>

#### <a name="id"></a><span data-ttu-id="513b3-134">id</span><span class="sxs-lookup"><span data-stu-id="513b3-134">id</span></span> 
<span data-ttu-id="513b3-135">Der Paketbezeichner, der die Groß- und Kleinschreibung nicht berücksichtigt und auf nuget.org oder im für das Paket verwendeten Katalog eindeutig sein muss.</span><span class="sxs-lookup"><span data-stu-id="513b3-135">The case-insensitive package identifier, which must be unique across nuget.org or whatever gallery the package resides in.</span></span> <span data-ttu-id="513b3-136">IDs dürfen keine Leerzeichen oder für eine URL unzulässige Zeichen enthalten. Sie müssen den Regeln für .NET-Namespaces entsprechen.</span><span class="sxs-lookup"><span data-stu-id="513b3-136">IDs may not contain spaces or characters that are not valid for a URL, and generally follow .NET namespace rules.</span></span> <span data-ttu-id="513b3-137">Informationen finden Sie unter [Choosing a unique package identifier (Auswählen eines eindeutigen Paketbezeichners)](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number).</span><span class="sxs-lookup"><span data-stu-id="513b3-137">See [Choosing a unique package identifier](../create-packages/creating-a-package.md#choose-a-unique-package-identifier-and-setting-the-version-number) for guidance.</span></span>
#### <a name="version"></a><span data-ttu-id="513b3-138">version</span><span class="sxs-lookup"><span data-stu-id="513b3-138">version</span></span>
<span data-ttu-id="513b3-139">Die Version des Pakets, die dem Muster *Hauptversion.Nebenversion.Patch* folgt.</span><span class="sxs-lookup"><span data-stu-id="513b3-139">The version of the package, following the *major.minor.patch* pattern.</span></span> <span data-ttu-id="513b3-140">Versionsnummern enthalten möglicherweise, wie unter [Paketversionsverwaltung](../concepts/package-versioning.md#pre-release-versions) beschrieben, ein Suffix der Vorabversion.</span><span class="sxs-lookup"><span data-stu-id="513b3-140">Version numbers may include a pre-release suffix as described in [Package versioning](../concepts/package-versioning.md#pre-release-versions).</span></span> 
#### <a name="description"></a><span data-ttu-id="513b3-141">description</span><span class="sxs-lookup"><span data-stu-id="513b3-141">description</span></span>
<span data-ttu-id="513b3-142">Eine Beschreibung des Pakets für die Anzeige der Benutzeroberfläche.</span><span class="sxs-lookup"><span data-stu-id="513b3-142">A description of the package for UI display.</span></span>
#### <a name="authors"></a><span data-ttu-id="513b3-143">authors</span><span class="sxs-lookup"><span data-stu-id="513b3-143">authors</span></span>
<span data-ttu-id="513b3-144">Eine durch Trennzeichen getrennte Liste von Paket Autoren, die mit den Profilnamen auf nuget.org übereinstimmen. Diese werden in der nuget-Galerie auf nuget.org angezeigt und werden verwendet, um die Verweise auf Pakete durch dieselben Autoren zu über verweisen.</span><span class="sxs-lookup"><span data-stu-id="513b3-144">A comma-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> 

### <a name="optional-metadata-elements"></a><span data-ttu-id="513b3-145">Optionale Metadatenelemente</span><span class="sxs-lookup"><span data-stu-id="513b3-145">Optional metadata elements</span></span>

#### <a name="owners"></a><span data-ttu-id="513b3-146">owners</span><span class="sxs-lookup"><span data-stu-id="513b3-146">owners</span></span>
<span data-ttu-id="513b3-147">Eine durch Trennzeichen getrennte Liste der Paket Ersteller, die Profilnamen auf nuget.org verwenden. Dies ist oft die gleiche Liste wie in `authors`und wird beim Hochladen des Pakets in nuget.org ignoriert. Weitere Informationen finden Sie [unter Verwalten von Paket Besitzern auf nuget.org](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg).</span><span class="sxs-lookup"><span data-stu-id="513b3-147">A comma-separated list of the package creators using profile names on nuget.org. This is often the same list as in `authors`, and is ignored when uploading the package to nuget.org. See [Managing package owners on nuget.org](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg).</span></span> 

#### <a name="projecturl"></a><span data-ttu-id="513b3-148">projectUrl</span><span class="sxs-lookup"><span data-stu-id="513b3-148">projectUrl</span></span>
<span data-ttu-id="513b3-149">Eine URL für die Paket-Homepage, häufig auf der Benutzeroberfläche sowie auf nuget.org angezeigt.</span><span class="sxs-lookup"><span data-stu-id="513b3-149">A URL for the package's home page, often shown in UI displays as well as nuget.org.</span></span> 

#### <a name="licenseurl"></a><span data-ttu-id="513b3-150">licenseUrl</span><span class="sxs-lookup"><span data-stu-id="513b3-150">licenseUrl</span></span>
> [!Important]
> <span data-ttu-id="513b3-151">"licenaburl" ist veraltet.</span><span class="sxs-lookup"><span data-stu-id="513b3-151">licenseUrl is deprecated.</span></span> <span data-ttu-id="513b3-152">Verwenden Sie stattdessen die Lizenz.</span><span class="sxs-lookup"><span data-stu-id="513b3-152">Use license instead.</span></span>

<span data-ttu-id="513b3-153">Eine URL für die Lizenz des Pakets, die häufig in Benutzeroberflächen wie nuget.org angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="513b3-153">A URL for the package's license, often shown in UIs like nuget.org.</span></span>

#### <a name="license"></a><span data-ttu-id="513b3-154">license</span><span class="sxs-lookup"><span data-stu-id="513b3-154">license</span></span>
<span data-ttu-id="513b3-155">Ein spdx-Lizenz Ausdruck oder Pfad zu einer Lizenzdatei innerhalb des Pakets, die häufig in Benutzeroberflächen wie nuget.org angezeigt wird. Wenn Sie das Paket unter einer gemeinsamen Lizenz lizenzieren, wie z. b. mit oder der BSD-2-Klausel, verwenden Sie den zugehörigen [spdx-Lizenz Bezeichner](https://spdx.org/licenses/).</span><span class="sxs-lookup"><span data-stu-id="513b3-155">An SPDX license expression or path to a license file within the package, often shown in UIs like nuget.org. If you're licensing the package under a common license, like MIT or BSD-2-Clause, use the associated [SPDX license identifier](https://spdx.org/licenses/).</span></span> <span data-ttu-id="513b3-156">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="513b3-156">For example:</span></span>

`<license type="expression">MIT</license>`

> [!Note]
> <span data-ttu-id="513b3-157">NuGet.org akzeptiert nur Lizenz Ausdrücke, die von der Open Source-Initiative oder der kostenlosen Software Foundation genehmigt werden.</span><span class="sxs-lookup"><span data-stu-id="513b3-157">NuGet.org only accepts license expressions that are approved by the Open Source Initiative or the Free Software Foundation.</span></span>

<span data-ttu-id="513b3-158">Wenn Ihr Paket unter mehreren gängigen Lizenzen lizenziert ist, können Sie eine zusammengesetzte Lizenz mithilfe der [spdx-Ausdruckssyntax Version 2,0](https://spdx.org/spdx-specification-21-web-version#h.jxpfx0ykyb60)angeben.</span><span class="sxs-lookup"><span data-stu-id="513b3-158">If your package is licensed under multiple common licenses, you can specify a composite license using the [SPDX expression syntax version 2.0](https://spdx.org/spdx-specification-21-web-version#h.jxpfx0ykyb60).</span></span> <span data-ttu-id="513b3-159">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="513b3-159">For example:</span></span>

`<license type="expression">BSD-2-Clause OR MIT</license>`

<span data-ttu-id="513b3-160">Wenn Sie eine benutzerdefinierte Lizenz verwenden, die nicht von Lizenz Ausdrücken unterstützt wird, können Sie eine `.txt` oder eine `.md` Datei mit dem Lizenztext verpacken.</span><span class="sxs-lookup"><span data-stu-id="513b3-160">If you use a custom license that isn't supported by license expressions, you can package a `.txt` or `.md` file with the license's text.</span></span> <span data-ttu-id="513b3-161">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="513b3-161">For example:</span></span>

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

<span data-ttu-id="513b3-162">Die MSBuild-Entsprechung finden Sie unter [packen eines Lizenz Ausdrucks oder einer Lizenzdatei](msbuild-targets.md#packing-a-license-expression-or-a-license-file).</span><span class="sxs-lookup"><span data-stu-id="513b3-162">For the MSBuild equivalent, take a look at [Packing a license expression or a license file](msbuild-targets.md#packing-a-license-expression-or-a-license-file).</span></span>

<span data-ttu-id="513b3-163">Die genaue Syntax der nuget-Lizenz Ausdrücke wird unten in [ABNF](https://tools.ietf.org/html/rfc5234)beschrieben.</span><span class="sxs-lookup"><span data-stu-id="513b3-163">The exact syntax of NuGet's license expressions is described below in [ABNF](https://tools.ietf.org/html/rfc5234).</span></span>
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

#### <a name="iconurl"></a><span data-ttu-id="513b3-164">iconUrl</span><span class="sxs-lookup"><span data-stu-id="513b3-164">iconUrl</span></span>

> [!Important]
> <span data-ttu-id="513b3-165">IconUrl ist veraltet.</span><span class="sxs-lookup"><span data-stu-id="513b3-165">iconUrl is deprecated.</span></span> <span data-ttu-id="513b3-166">Verwenden Sie stattdessen das-Symbol.</span><span class="sxs-lookup"><span data-stu-id="513b3-166">Use icon instead.</span></span>

<span data-ttu-id="513b3-167">Eine URL für ein 128 x 128-Bild mit Transparenz Hintergrund, das als Symbol für das Paket in der Anzeige der Benutzeroberfläche verwendet werden soll.</span><span class="sxs-lookup"><span data-stu-id="513b3-167">A URL for a 128x128 image with transparency background to use as the icon for the package in UI display.</span></span> <span data-ttu-id="513b3-168">Stellen Sie sicher, dass dieses Element die *direkte Bild-URL* und nicht nur die URL einer Webseite enthält, die das Bild enthält.</span><span class="sxs-lookup"><span data-stu-id="513b3-168">Be sure this element contains the *direct image URL* and not the URL of a web page containing the image.</span></span> <span data-ttu-id="513b3-169">Wenn Sie z. b. ein Image von GitHub verwenden möchten, verwenden Sie die URL der Rohdatendatei wie <em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>.</span><span class="sxs-lookup"><span data-stu-id="513b3-169">For example, to use an image from GitHub, use the raw file URL like <em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>.</span></span> 
   
#### <a name="icon"></a><span data-ttu-id="513b3-170">icon</span><span class="sxs-lookup"><span data-stu-id="513b3-170">icon</span></span>

<span data-ttu-id="513b3-171">Dabei handelt es sich um einen Pfad zu einer Bilddatei innerhalb des Pakets, die häufig in UIs like nuget.org als Paket Symbol angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="513b3-171">It is a path to an image file within the package, often shown in UIs like nuget.org as the package icon.</span></span> <span data-ttu-id="513b3-172">Die Größe der Bild Datei ist auf 1 MB beschränkt.</span><span class="sxs-lookup"><span data-stu-id="513b3-172">Image file size is limited to 1 MB.</span></span> <span data-ttu-id="513b3-173">Unterstützte Dateiformate sind JPEG und PNG.</span><span class="sxs-lookup"><span data-stu-id="513b3-173">Supported file formats include JPEG and PNG.</span></span> <span data-ttu-id="513b3-174">Wir empfehlen eine Bildauflösung von 128 x 128.</span><span class="sxs-lookup"><span data-stu-id="513b3-174">We recommend an image resolution of 128x128.</span></span>

<span data-ttu-id="513b3-175">Beim Erstellen eines Pakets mithilfe von "nuget. exe" fügen Sie z. b. Folgendes zu "nuspec" hinzu:</span><span class="sxs-lookup"><span data-stu-id="513b3-175">For example, you would add the following to your nuspec when creating a package using nuget.exe:</span></span>

```xml
<package>
  <metadata>
    ...
    <icon>images\icon.png</icon>
    ...
  </metadata>
  <files>
    ...
    <file src="..\icon.png" target="images\" />
    ...
  </files>
</package>
```

[<span data-ttu-id="513b3-176">Paket Symbol nuspec-Beispiel.</span><span class="sxs-lookup"><span data-stu-id="513b3-176">Package Icon nuspec sample.</span></span>](https://github.com/NuGet/Samples/tree/master/PackageIconNuspecExample)

<span data-ttu-id="513b3-177">Wenn Sie die MSBuild-Entsprechung benötigen, sehen Sie sich das [Packen einer Symbolbild Datei](msbuild-targets.md#packing-an-icon-image-file)an.</span><span class="sxs-lookup"><span data-stu-id="513b3-177">For the MSBuild equivalent, take a look at [Packing an icon image file](msbuild-targets.md#packing-an-icon-image-file).</span></span>

> [!Tip]
> <span data-ttu-id="513b3-178">Sie können sowohl `icon` als auch `iconUrl` angeben, um die Abwärtskompatibilität mit Quellen zu gewährleisten, die `icon`nicht unterstützen.</span><span class="sxs-lookup"><span data-stu-id="513b3-178">You can specify both `icon` and `iconUrl` to maintain backward compatibility with sources that do not support `icon`.</span></span> <span data-ttu-id="513b3-179">Visual Studio unterstützt `icon` für Pakete, die in einer zukünftigen Version aus einer Ordner basierten Quelle stammen.</span><span class="sxs-lookup"><span data-stu-id="513b3-179">Visual Studio will support `icon` for packages coming from a folder-based source in a future release.</span></span>

#### <a name="requirelicenseacceptance"></a><span data-ttu-id="513b3-180">requireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="513b3-180">requireLicenseAcceptance</span></span>
<span data-ttu-id="513b3-181">Ein boolescher Wert, der angibt, ob der Client den Benutzer dazu auffordern muss, die Paketlizenz vor der Installation des Pakets zu akzeptieren.</span><span class="sxs-lookup"><span data-stu-id="513b3-181">A Boolean value specifying whether the client must prompt the consumer to accept the package license before installing the package.</span></span>

#### <a name="developmentdependency"></a><span data-ttu-id="513b3-182">developmentDependency</span><span class="sxs-lookup"><span data-stu-id="513b3-182">developmentDependency</span></span>
<span data-ttu-id="513b3-183">*(2.8 und höher)* Ein boolescher Wert, der angibt, ob das Paket mit einer Abhängigkeit markiert werden soll, die nur für die Entwicklung gilt, wodurch vermieden wird, dass das Paket als Abhängigkeit in andere Pakete eingefügt wird.</span><span class="sxs-lookup"><span data-stu-id="513b3-183">*(2.8+)* A Boolean value specifying whether the package is be marked as a development-only-dependency, which prevents the package from being included as a dependency in other packages.</span></span> <span data-ttu-id="513b3-184">Mit packagereferen(nuget 4.8 und höher) bedeutet dieses Flag auch, dass die Kompilierzeit Ressourcen von der Kompilierung ausgeschlossen werden.</span><span class="sxs-lookup"><span data-stu-id="513b3-184">With PackageReference (NuGet 4.8+), this flag also means that it will exclude compile-time assets from compilation.</span></span> <span data-ttu-id="513b3-185">Weitere Informationen finden Sie [unter Unterstützung von "developmentdependependenz](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference) "</span><span class="sxs-lookup"><span data-stu-id="513b3-185">See [DevelopmentDependency support for PackageReference](https://github.com/NuGet/Home/wiki/DevelopmentDependency-support-for-PackageReference)</span></span>

#### <a name="summary"></a><span data-ttu-id="513b3-186">summary</span><span class="sxs-lookup"><span data-stu-id="513b3-186">summary</span></span>
> [!Important]
> <span data-ttu-id="513b3-187">`summary` ist veraltet.</span><span class="sxs-lookup"><span data-stu-id="513b3-187">`summary` is being deprecated.</span></span> <span data-ttu-id="513b3-188">Verwenden Sie stattdessen `description`.</span><span class="sxs-lookup"><span data-stu-id="513b3-188">Use `description` instead.</span></span>

<span data-ttu-id="513b3-189">Eine kurze Beschreibung des Pakets für die Anzeige der Benutzeroberfläche.</span><span class="sxs-lookup"><span data-stu-id="513b3-189">A short description of the package for UI display.</span></span> <span data-ttu-id="513b3-190">Wenn diese nicht angegeben wird, wird eine gekürzte Version von `description` verwendet.</span><span class="sxs-lookup"><span data-stu-id="513b3-190">If omitted, a truncated version of `description` is used.</span></span>

#### <a name="releasenotes"></a><span data-ttu-id="513b3-191">releaseNotes</span><span class="sxs-lookup"><span data-stu-id="513b3-191">releaseNotes</span></span>
<span data-ttu-id="513b3-192">*(1.5 und höher)* Eine Beschreibung der in diesem Release des Pakets enthaltenen Änderungen, die häufig in Benutzeroberflächen wie der Registerkarte **Updates** des Visual Studio-Paket-Managers anstelle von Paketbeschreibungen verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="513b3-192">*(1.5+)* A description of the changes made in this release of the package, often used in UI like the **Updates** tab of the Visual Studio Package Manager in place of the package description.</span></span>

#### <a name="copyright"></a><span data-ttu-id="513b3-193">Copyright</span><span class="sxs-lookup"><span data-stu-id="513b3-193">copyright</span></span>
<span data-ttu-id="513b3-194">*(1.5 und höher)* Copyright-Informationen zum Paket.</span><span class="sxs-lookup"><span data-stu-id="513b3-194">*(1.5+)* Copyright details for the package.</span></span>

#### <a name="language"></a><span data-ttu-id="513b3-195">language</span><span class="sxs-lookup"><span data-stu-id="513b3-195">language</span></span>
<span data-ttu-id="513b3-196">Die Gebietsschema-ID des Pakets.</span><span class="sxs-lookup"><span data-stu-id="513b3-196">The locale ID for the package.</span></span> <span data-ttu-id="513b3-197">Informationen dazu finden Sie unter [Creating localized packages (Erstellen von lokalisierten Paketen)](../create-packages/creating-localized-packages.md).</span><span class="sxs-lookup"><span data-stu-id="513b3-197">See [Creating localized packages](../create-packages/creating-localized-packages.md).</span></span>

#### <a name="tags"></a><span data-ttu-id="513b3-198">tags</span><span class="sxs-lookup"><span data-stu-id="513b3-198">tags</span></span>
<span data-ttu-id="513b3-199">Eine durch Leerzeichen getrennte Liste mit Tags und Schlüsselwörtern, die das Paket beschreiben und zum Ermitteln von Paketen über Suchvorgänge und Filter beitragen.</span><span class="sxs-lookup"><span data-stu-id="513b3-199">A space-delimited list of tags and keywords that describe the package and aid discoverability of packages through search and filtering.</span></span> 

#### <a name="serviceable"></a><span data-ttu-id="513b3-200">serviceable</span><span class="sxs-lookup"><span data-stu-id="513b3-200">serviceable</span></span> 
<span data-ttu-id="513b3-201">*(3.3 und höher)* Nur für die interne Verwendung von NuGet.</span><span class="sxs-lookup"><span data-stu-id="513b3-201">*(3.3+)* For internal NuGet use only.</span></span>

#### <a name="repository"></a><span data-ttu-id="513b3-202">repository</span><span class="sxs-lookup"><span data-stu-id="513b3-202">repository</span></span>
<span data-ttu-id="513b3-203">Repository-Metadaten, bestehend aus vier optionalen Attributen: `type` und `url` *(4.0*und höher) sowie `branch` und `commit` *(4.6*und höher).</span><span class="sxs-lookup"><span data-stu-id="513b3-203">Repository metadata, consisting of four optional attributes: `type` and `url` *(4.0+)*, and `branch` and `commit` *(4.6+)*.</span></span> <span data-ttu-id="513b3-204">Diese Attribute ermöglichen es Ihnen, den `.nupkg` dem Repository zuzuordnen, von dem es erstellt wurde, und mit der Möglichkeit, den einzelnen branchnamen und/oder den SHA-1-Hash, der das Paket erstellt hat, so detailliert wie möglich zu machen.</span><span class="sxs-lookup"><span data-stu-id="513b3-204">These attributes allow you to map the `.nupkg` to the repository that built it, with the potential to get as detailed as the individual branch name and / or commit SHA-1 hash that built the package.</span></span> <span data-ttu-id="513b3-205">Hierbei sollte es sich um eine öffentlich zugängliche URL handeln, die direkt von einer Versionskontrollsoftware aufgerufen werden kann.</span><span class="sxs-lookup"><span data-stu-id="513b3-205">This should be a publicly available url that can be invoked directly by a version control software.</span></span> <span data-ttu-id="513b3-206">Dagegen sollte es keine HTML-Seite sein, da diese für den Computer vorgesehen ist.</span><span class="sxs-lookup"><span data-stu-id="513b3-206">It should not be an html page as this is meant for the computer.</span></span> <span data-ttu-id="513b3-207">Verwenden Sie zum Verknüpfen mit Project Seite stattdessen das Feld `projectUrl`.</span><span class="sxs-lookup"><span data-stu-id="513b3-207">For linking to project page, use the `projectUrl` field, instead.</span></span>

<span data-ttu-id="513b3-208">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="513b3-208">For example:</span></span>
```xml
<?xml version="1.0"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        ...
        <repository type="git" url="https://github.com/NuGet/NuGet.Client.git" branch="dev" commit="e1c65e4524cd70ee6e22abe33e6cb6ec73938cb3" />
        ...
    </metadata>
</package>
```

#### <a name="title"></a><span data-ttu-id="513b3-209">title</span><span class="sxs-lookup"><span data-stu-id="513b3-209">title</span></span>
<span data-ttu-id="513b3-210">Ein benutzerfreundlicher Titel des Pakets, das in einigen Benutzeroberflächen anzeigen verwendet werden kann.</span><span class="sxs-lookup"><span data-stu-id="513b3-210">A human-friendly title of the package which may be used in some UI displays.</span></span> <span data-ttu-id="513b3-211">(nuget.org und der Paket-Manager in Visual Studio zeigen keinen Titel an.)</span><span class="sxs-lookup"><span data-stu-id="513b3-211">(nuget.org and the Package Manager in Visual Studio do not show title)</span></span>

#### <a name="collection-elements"></a><span data-ttu-id="513b3-212">Auflistungselemente</span><span class="sxs-lookup"><span data-stu-id="513b3-212">Collection elements</span></span>

#### <a name="packagetypes"></a><span data-ttu-id="513b3-213">packageTypes</span><span class="sxs-lookup"><span data-stu-id="513b3-213">packageTypes</span></span>
<span data-ttu-id="513b3-214">*(3.5 und höher)* Eine Auflistung, die kein `<packageType>`-Element oder mindestens eins enthält und den Pakettyp angibt, wenn es sich nicht um ein gewöhnliches Abhängigkeitspaket handelt.</span><span class="sxs-lookup"><span data-stu-id="513b3-214">*(3.5+)* A collection of zero or more `<packageType>` elements specifying the type of the package if other than a traditional dependency package.</span></span> <span data-ttu-id="513b3-215">Jeder „packageType“ verfügt über Attribute von *name* und *version*.</span><span class="sxs-lookup"><span data-stu-id="513b3-215">Each packageType has attributes of *name* and *version*.</span></span> <span data-ttu-id="513b3-216">Informationen dazu finden Sie unter [Setting a package type (Festlegen eines Pakettypen)](../create-packages/set-package-type.md).</span><span class="sxs-lookup"><span data-stu-id="513b3-216">See [Setting a package type](../create-packages/set-package-type.md).</span></span>
#### <a name="dependencies"></a><span data-ttu-id="513b3-217">dependencies</span><span class="sxs-lookup"><span data-stu-id="513b3-217">dependencies</span></span>
<span data-ttu-id="513b3-218">Eine Auflistung, die kein `<dependency>`-Element oder mindestens eins enthält und Abhängigkeiten für das Paket angibt.</span><span class="sxs-lookup"><span data-stu-id="513b3-218">A collection of zero or more `<dependency>` elements specifying the dependencies for the package.</span></span> <span data-ttu-id="513b3-219">Jede Abhängigkeit verfügt über Attribute von *id*, *version*, *include* und *exclude* (3.x und höher).</span><span class="sxs-lookup"><span data-stu-id="513b3-219">Each dependency has attributes of *id*, *version*, *include* (3.x+), and *exclude* (3.x+).</span></span> <span data-ttu-id="513b3-220">Informationen dazu finden Sie im Abschnitt [Abhängigkeiten](#dependencies-element).</span><span class="sxs-lookup"><span data-stu-id="513b3-220">See [Dependencies](#dependencies-element) below.</span></span>
#### <a name="frameworkassemblies"></a><span data-ttu-id="513b3-221">frameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="513b3-221">frameworkAssemblies</span></span>
<span data-ttu-id="513b3-222">*(1.2 und höher)* Eine Auflistung, die kein `<frameworkAssembly>`-Element oder mindestens eins enthält und die für das Paket erforderlichen Verweise auf .NET Framework-Assemblys erkennt und sicherstellt, dass Verweise zu Projekten hinzugefügt werden, die das Paket verarbeiten.</span><span class="sxs-lookup"><span data-stu-id="513b3-222">*(1.2+)* A collection of zero or more `<frameworkAssembly>` elements identifying .NET Framework assembly references that this package requires, which ensures that references are added to projects consuming the package.</span></span> <span data-ttu-id="513b3-223">Jedes frameworkAssembly-Element verfügt über die Attribute *assemblyName* und *targetFramework*.</span><span class="sxs-lookup"><span data-stu-id="513b3-223">Each frameworkAssembly has *assemblyName* and *targetFramework* attributes.</span></span> <span data-ttu-id="513b3-224">Informationen dazu finden Sie unter [Specifying framework assembly references GAC (Angeben von GAC-Verweisen auf Frameworkassemblys)](#specifying-framework-assembly-references-gac).</span><span class="sxs-lookup"><span data-stu-id="513b3-224">See [Specifying framework assembly references GAC](#specifying-framework-assembly-references-gac) below.</span></span>
#### <a name="references"></a><span data-ttu-id="513b3-225">Verweise</span><span class="sxs-lookup"><span data-stu-id="513b3-225">references</span></span>
<span data-ttu-id="513b3-226">*(1.5 und höher)* Eine Auflistung, die kein `<reference>`-Element oder mindestens eins enthält, das Assemblys in dem `lib`-Ordner des Pakets benennt, die als Projektverweise hinzugefügt werden.</span><span class="sxs-lookup"><span data-stu-id="513b3-226">*(1.5+)* A collection of zero or more `<reference>` elements naming assemblies in the package's `lib` folder that are added as project references.</span></span> <span data-ttu-id="513b3-227">Jeder Verweis verfügt über ein *file*-Attribut.</span><span class="sxs-lookup"><span data-stu-id="513b3-227">Each reference has a *file* attribute.</span></span> <span data-ttu-id="513b3-228">`<references>` kann außerdem ein `<group>`-Element mit einem *targetFramework*-Attribut enthalten, das anschließend `<reference>`-Elemente enthält.</span><span class="sxs-lookup"><span data-stu-id="513b3-228">`<references>` can also contain a `<group>` element with a *targetFramework* attribute, that then contains `<reference>` elements.</span></span> <span data-ttu-id="513b3-229">Wenn das Element nicht angegeben ist, werden alle Verweise in `lib` eingefügt.</span><span class="sxs-lookup"><span data-stu-id="513b3-229">If omitted, all references in `lib` are included.</span></span> <span data-ttu-id="513b3-230">Informationen dazu finden Sie unter [Specifying explicit assembly references (Angeben von expliziten Assemblyverweisen)](#specifying-explicit-assembly-references).</span><span class="sxs-lookup"><span data-stu-id="513b3-230">See [Specifying explicit assembly references](#specifying-explicit-assembly-references) below.</span></span>
#### <a name="contentfiles"></a><span data-ttu-id="513b3-231">contentFiles</span><span class="sxs-lookup"><span data-stu-id="513b3-231">contentFiles</span></span>
<span data-ttu-id="513b3-232">*(3.3 und höher)* Eine Auflistung von `<files>`-Elementen, die Inhaltsdateien ermitteln, die in das verarbeitende Projekt eingefügt werden sollen.</span><span class="sxs-lookup"><span data-stu-id="513b3-232">*(3.3+)* A collection of `<files>` elements that identify content files to include in the consuming project.</span></span> <span data-ttu-id="513b3-233">Diese Dateien werden zusammen mit mehreren Attributen angegeben, die beschreiben, wie sie in dem Projektsystem verwendet werden sollen.</span><span class="sxs-lookup"><span data-stu-id="513b3-233">These files are specified with a set of attributes that describe how they should be used within the project system.</span></span> <span data-ttu-id="513b3-234">Informationen dazu finden Sie unter [Specifying files to include in the package (Angeben von Dateien, die in das Paket eingefügt werden sollen)](#specifying-files-to-include-in-the-package).</span><span class="sxs-lookup"><span data-stu-id="513b3-234">See [Specifying files to include in the package](#specifying-files-to-include-in-the-package) below.</span></span>
#### <a name="files"></a><span data-ttu-id="513b3-235">files</span><span class="sxs-lookup"><span data-stu-id="513b3-235">files</span></span> 
<span data-ttu-id="513b3-236">Der `<package>` Knoten kann einen `<files>` Knoten als gleich geordnetes Element für `<metadata>`und ein untergeordnetes `<contentFiles>` unter `<metadata>`enthalten, um anzugeben, welche Assembly-und Inhalts Dateien in das Paket eingeschlossen werden sollen.</span><span class="sxs-lookup"><span data-stu-id="513b3-236">The `<package>` node may contain a `<files>` node as a sibling to `<metadata>`, and a `<contentFiles>` child under `<metadata>`, to specify which assembly and content files to include in the package.</span></span> <span data-ttu-id="513b3-237">Details dazu finden Sie im Folgenden in den Abschnitten [Einfügen von Assemblydateien](#including-assembly-files) und [Einfügen von Inhaltsdateien](#including-content-files).</span><span class="sxs-lookup"><span data-stu-id="513b3-237">See [Including assembly files](#including-assembly-files) and [Including content files](#including-content-files) later in this topic for details.</span></span>

### <a name="metadata-attributes"></a><span data-ttu-id="513b3-238">Metadatenattribute</span><span class="sxs-lookup"><span data-stu-id="513b3-238">metadata attributes</span></span>

#### <a name="minclientversion"></a><span data-ttu-id="513b3-239">minClientVersion</span><span class="sxs-lookup"><span data-stu-id="513b3-239">minClientVersion</span></span>
<span data-ttu-id="513b3-240">Gibt die minimale Version des NuGet-Clients an, der dieses Paket installieren kann. Dies wird von nuget.exe und dem Paket-Manager von Visual Studio erzwungen.</span><span class="sxs-lookup"><span data-stu-id="513b3-240">Specifies the minimum version of the NuGet client that can install this package, enforced by nuget.exe and the Visual Studio Package Manager.</span></span> <span data-ttu-id="513b3-241">Dieses Attribut wird verwendet, wenn das Paket von bestimmten Funktionen der `.nuspec`-Datei abhängig ist, die in einer bestimmten Version des NuGet-Clients hinzugefügt wurden.</span><span class="sxs-lookup"><span data-stu-id="513b3-241">This is used whenever the package depends on specific features of the `.nuspec` file that were added in a particular version of the NuGet client.</span></span> <span data-ttu-id="513b3-242">Beispielsweise sollte ein Paket, das das `developmentDependency`-Attribut verwendet, „2.8“ für `minClientVersion` angeben.</span><span class="sxs-lookup"><span data-stu-id="513b3-242">For example, a package using the `developmentDependency` attribute should specify "2.8" for `minClientVersion`.</span></span> <span data-ttu-id="513b3-243">Genauso sollte ein Paket, das das `contentFiles`-Element verwendet (vgl. nächster Abschnitt), `minClientVersion` auf „3.3“ festlegen.</span><span class="sxs-lookup"><span data-stu-id="513b3-243">Similarly, a package using the `contentFiles` element (see the next section) should set `minClientVersion` to "3.3".</span></span> <span data-ttu-id="513b3-244">Beachten Sie außerdem, dass NuGet-Clients vor Version 2.5 diese Kennzeichnung nicht erkennen und daher die Installation des Pakets, unabhängig vom Inhalt von *,* immer`minClientVersion` verweigern.</span><span class="sxs-lookup"><span data-stu-id="513b3-244">Note also that because NuGet clients prior to 2.5 do not recognize this flag, they *always* refuse to install the package no matter what `minClientVersion` contains.</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata minClientVersion="100.0.0.1">
        <id>dasdas</id>
        <version>2.0.0</version>
        <title />
        <authors>dsadas</authors>
        <owners />
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>My package description.</description>
    </metadata>
    <files>
        <file src="content\one.txt" target="content\one.txt" />
    </files>
</package>
```

## <a name="replacement-tokens"></a><span data-ttu-id="513b3-245">Ersetzungstokens</span><span class="sxs-lookup"><span data-stu-id="513b3-245">Replacement tokens</span></span>

<span data-ttu-id="513b3-246">Bei der Erstellung eines Pakets ersetzt der [`nuget pack`-Befehl](../reference/cli-reference/cli-ref-pack.md) durch $ getrennte Tokens im `.nuspec`-Knoten der `<metadata>`-Datei durch Werte, die entweder einer Projektdatei oder dem `pack`-Schalter des `-properties`-Befehls entstammen.</span><span class="sxs-lookup"><span data-stu-id="513b3-246">When creating a package, the [`nuget pack` command](../reference/cli-reference/cli-ref-pack.md) replaces $-delimited tokens in the `.nuspec` file's `<metadata>` node with values that come from either a project file or the `pack` command's `-properties` switch.</span></span>

<span data-ttu-id="513b3-247">Geben Sie in der Befehlszeile die Tokenwerte mit `nuget pack -properties <name>=<value>;<name>=<value>` an.</span><span class="sxs-lookup"><span data-stu-id="513b3-247">On the command line, you specify token values with `nuget pack -properties <name>=<value>;<name>=<value>`.</span></span> <span data-ttu-id="513b3-248">Beispielsweise können Sie ein Token wie `$owners$` und `$desc$` in der `.nuspec`-Datei verwenden und die Werte zur Packzeit wie im Folgenden dargestellt bereitstellen:</span><span class="sxs-lookup"><span data-stu-id="513b3-248">For example, you can use a token such as `$owners$` and `$desc$` in the `.nuspec` and provide the values at packing time as follows:</span></span>

```ps
nuget pack MyProject.csproj -properties
    owners=janedoe,harikm,kimo,xiaop;desc="Awesome app logger utility"
```

<span data-ttu-id="513b3-249">Geben Sie die in der untenstehenden Tabelle beschriebenen Tokens an, um Werte aus einem Projekt zu verwenden (AssemblyInfo verweist auf Dateien wie `Properties` oder `AssemblyInfo.cs` in `AssemblyInfo.vb`).</span><span class="sxs-lookup"><span data-stu-id="513b3-249">To use values from a project, specify the tokens described in the table below (AssemblyInfo refers to the file in `Properties` such as `AssemblyInfo.cs` or `AssemblyInfo.vb`).</span></span>

<span data-ttu-id="513b3-250">Führen Sie anstelle von `nuget pack` nur `.nuspec` in der Projektdatei aus, um diese Tokens zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="513b3-250">To use these tokens, run `nuget pack` with the project file rather than just the `.nuspec`.</span></span> <span data-ttu-id="513b3-251">Beispielsweise werden bei der Verwendung des folgenden Befehls die Tokens `$id$` und `$version$` in einer `.nuspec`-Datei durch die Werte `AssemblyName` und `AssemblyVersion` des Projekts ersetzt:</span><span class="sxs-lookup"><span data-stu-id="513b3-251">For example, when using the following command, the `$id$` and `$version$` tokens in a `.nuspec` file are replaced with the project's `AssemblyName` and `AssemblyVersion` values:</span></span>

```ps
nuget pack MyProject.csproj
```

<span data-ttu-id="513b3-252">In der Regel erstellen Sie `.nuspec` in einem Projekt zuerst mithilfe von `nuget spec MyProject.csproj`, wodurch automatisch einige dieser Standardtokens eingefügt werden.</span><span class="sxs-lookup"><span data-stu-id="513b3-252">Typically, when you have a project, you create the `.nuspec` initially using `nuget spec MyProject.csproj` which automatically includes some of these standard tokens.</span></span> <span data-ttu-id="513b3-253">Wenn in einem Projekt allerdings keine Werte für erforderliche `.nuspec`-Elemente enthalten sind, schlägt `nuget pack` fehl.</span><span class="sxs-lookup"><span data-stu-id="513b3-253">However, if a project lacks values for required `.nuspec` elements, then `nuget pack` fails.</span></span> <span data-ttu-id="513b3-254">Stellen Sie außerdem bei der Änderung von Projektwerten sicher, dass Sie diese neu erstellen, bevor Sie das Paket erstellen. Dies können Sie ganz einfach über den `build`-Paketschalter des Befehls tun.</span><span class="sxs-lookup"><span data-stu-id="513b3-254">Furthermore, if you change project values, be sure to rebuild before creating the package; this can be done conveniently with the pack command's `build` switch.</span></span>

<span data-ttu-id="513b3-255">Mit Ausnahme von `$configuration$` werden Werte in dem Projekt gegenüber Werten bevorzugt, die demselben Token in der Befehlszeile zugeordnet sind.</span><span class="sxs-lookup"><span data-stu-id="513b3-255">With the exception of `$configuration$`, values in the project are used in preference to any assigned to the same token on the command line.</span></span>

| <span data-ttu-id="513b3-256">Token</span><span class="sxs-lookup"><span data-stu-id="513b3-256">Token</span></span> | <span data-ttu-id="513b3-257">Wertquelle</span><span class="sxs-lookup"><span data-stu-id="513b3-257">Value source</span></span> | <span data-ttu-id="513b3-258">value</span><span class="sxs-lookup"><span data-stu-id="513b3-258">Value</span></span>
| --- | --- | ---
| <span data-ttu-id="513b3-259">**$id$**</span><span class="sxs-lookup"><span data-stu-id="513b3-259">**$id$**</span></span> | <span data-ttu-id="513b3-260">Projektdatei</span><span class="sxs-lookup"><span data-stu-id="513b3-260">Project file</span></span> | <span data-ttu-id="513b3-261">"AssemblyName" (Titel) aus der Projektdatei</span><span class="sxs-lookup"><span data-stu-id="513b3-261">AssemblyName (title) from the project file</span></span> |
| <span data-ttu-id="513b3-262">**$version$**</span><span class="sxs-lookup"><span data-stu-id="513b3-262">**$version$**</span></span> | <span data-ttu-id="513b3-263">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="513b3-263">AssemblyInfo</span></span> | <span data-ttu-id="513b3-264">„AssemblyInformationalVersion“, falls vorhanden, andernfalls „AssemblyVersion“</span><span class="sxs-lookup"><span data-stu-id="513b3-264">AssemblyInformationalVersion if present, otherwise AssemblyVersion</span></span> |
| <span data-ttu-id="513b3-265">**$author$**</span><span class="sxs-lookup"><span data-stu-id="513b3-265">**$author$**</span></span> | <span data-ttu-id="513b3-266">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="513b3-266">AssemblyInfo</span></span> | <span data-ttu-id="513b3-267">AssemblyCompany</span><span class="sxs-lookup"><span data-stu-id="513b3-267">AssemblyCompany</span></span> |
| <span data-ttu-id="513b3-268">**$Title $**</span><span class="sxs-lookup"><span data-stu-id="513b3-268">**$title$**</span></span> | <span data-ttu-id="513b3-269">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="513b3-269">AssemblyInfo</span></span> | <span data-ttu-id="513b3-270">AssemblyTitle</span><span class="sxs-lookup"><span data-stu-id="513b3-270">AssemblyTitle</span></span> |
| <span data-ttu-id="513b3-271">**$description$**</span><span class="sxs-lookup"><span data-stu-id="513b3-271">**$description$**</span></span> | <span data-ttu-id="513b3-272">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="513b3-272">AssemblyInfo</span></span> | <span data-ttu-id="513b3-273">AssemblyDescription</span><span class="sxs-lookup"><span data-stu-id="513b3-273">AssemblyDescription</span></span> |
| <span data-ttu-id="513b3-274">**$copyright$**</span><span class="sxs-lookup"><span data-stu-id="513b3-274">**$copyright$**</span></span> | <span data-ttu-id="513b3-275">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="513b3-275">AssemblyInfo</span></span> | <span data-ttu-id="513b3-276">AssemblyCopyright</span><span class="sxs-lookup"><span data-stu-id="513b3-276">AssemblyCopyright</span></span> |
| <span data-ttu-id="513b3-277">**$configuration$**</span><span class="sxs-lookup"><span data-stu-id="513b3-277">**$configuration$**</span></span> | <span data-ttu-id="513b3-278">Assembly-DLL</span><span class="sxs-lookup"><span data-stu-id="513b3-278">Assembly DLL</span></span> | <span data-ttu-id="513b3-279">Konfiguration, die zur Erstellung der Assembly verwendet wird und standardmäßig auf „Debuggen“ festgelegt ist.</span><span class="sxs-lookup"><span data-stu-id="513b3-279">Configuration used to build the assembly, defaulting to Debug.</span></span> <span data-ttu-id="513b3-280">Achten Sie darauf, dass Sie stets `-properties Configuration=Release` in der Befehlszeile verwenden, um mithilfe einer Releasekonfiguration ein Paket zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="513b3-280">Note that to create a package using a Release configuration, you always use `-properties Configuration=Release` on the command line.</span></span> |

<span data-ttu-id="513b3-281">Tokens können auch zum Auflösen von Pfaden verwendet werden, wenn Sie [Assemblydateien](#including-assembly-files) und [Inhaltsdateien](#including-content-files) hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="513b3-281">Tokens can also be used to resolve paths when you include [assembly files](#including-assembly-files) and [content files](#including-content-files).</span></span> <span data-ttu-id="513b3-282">Die Namen der Tokens und der MSBuild-Eigenschaften stimmen miteinander überein, wodurch Sie abhängig von der aktuellen Buildkonfiguration Dateien auswählen können, die eingefügt werden sollen.</span><span class="sxs-lookup"><span data-stu-id="513b3-282">The tokens have the same names as the MSBuild properties, making it possible to select files to be included depending on the current build configuration.</span></span> <span data-ttu-id="513b3-283">Wenn Sie beispielsweise die folgenden Tokens in der `.nuspec`-Datei verwenden</span><span class="sxs-lookup"><span data-stu-id="513b3-283">For example, if you use the following tokens in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="bin\$configuration$\$id$.pdb" target="lib\net40" />
</files>
```

<span data-ttu-id="513b3-284">und Sie eine Assembly mit der `AssemblyName`-Konfiguration in MSBuild erstellen, deren `LoggingLibrary``Release` ist, sehen die dadurch entstandenen Zeilen in der `.nuspec`-Datei in den Paketen wie folgt aus:</span><span class="sxs-lookup"><span data-stu-id="513b3-284">And you build an assembly whose `AssemblyName` is `LoggingLibrary` with the `Release` configuration in MSBuild, the resulting lines in the `.nuspec` file in the package is as follows:</span></span>

```xml
<files>
    <file src="bin\Release\LoggingLibrary.pdb" target="lib\net40" />
</files>
```

## <a name="dependencies-element"></a><span data-ttu-id="513b3-285">Abhängigkeitselement</span><span class="sxs-lookup"><span data-stu-id="513b3-285">Dependencies element</span></span>

<span data-ttu-id="513b3-286">Das `<dependencies>`-Element in `<metadata>` enthält eine beliebige Anzahl von `<dependency>`-Elementen, die andere Pakete finden, von denen die Pakete auf der obersten Ebene abhängig sind.</span><span class="sxs-lookup"><span data-stu-id="513b3-286">The `<dependencies>` element within `<metadata>` contains any number of `<dependency>` elements that identify other packages upon which the top-level package depends.</span></span> <span data-ttu-id="513b3-287">Im Folgenden werden die Attribute für jede `<dependency>` dargestellt:</span><span class="sxs-lookup"><span data-stu-id="513b3-287">The attributes for each `<dependency>` are as follows:</span></span>

| <span data-ttu-id="513b3-288">attribute</span><span class="sxs-lookup"><span data-stu-id="513b3-288">Attribute</span></span> | <span data-ttu-id="513b3-289">BESCHREIBUNG</span><span class="sxs-lookup"><span data-stu-id="513b3-289">Description</span></span> |
| --- | --- |
| `id` | <span data-ttu-id="513b3-290">(Erforderlich) Die Paket-ID der Abhängigkeit, z.B. „EntityFramework“ und „NUnit“, die der Name des Pakets „nuget.org“ ist, wird auf einer Paketseite angezeigt.</span><span class="sxs-lookup"><span data-stu-id="513b3-290">(Required) The package ID of the dependency, such as "EntityFramework" and "NUnit", which is the name of the package nuget.org shows on a package page.</span></span> |
| `version` | <span data-ttu-id="513b3-291">(Erforderlich) Der Bereich an Versionen, die als Abhängigkeiten akzeptiert werden.</span><span class="sxs-lookup"><span data-stu-id="513b3-291">(Required) The range of versions acceptable as a dependency.</span></span> <span data-ttu-id="513b3-292">Die genaue Syntax finden Sie unter [Paketversionsverwaltung](../concepts/package-versioning.md#version-ranges).</span><span class="sxs-lookup"><span data-stu-id="513b3-292">See [Package versioning](../concepts/package-versioning.md#version-ranges) for exact syntax.</span></span> <span data-ttu-id="513b3-293">Gleit Komma Versionen werden nicht unterstützt.</span><span class="sxs-lookup"><span data-stu-id="513b3-293">Floating versions are not supported.</span></span> |
| <span data-ttu-id="513b3-294">include</span><span class="sxs-lookup"><span data-stu-id="513b3-294">include</span></span> | <span data-ttu-id="513b3-295">Eine durch Kommas abgetrennte Liste mit Include/Exclude-Tags (s. Tabelle unten), in der auf die Abhängigkeit verwiesen wird, die in das endgültige Paket eingefügt werden soll.</span><span class="sxs-lookup"><span data-stu-id="513b3-295">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to include in the final package.</span></span> <span data-ttu-id="513b3-296">Standardwert: `all`.</span><span class="sxs-lookup"><span data-stu-id="513b3-296">The default value is `all`.</span></span> |
| <span data-ttu-id="513b3-297">ausschließen</span><span class="sxs-lookup"><span data-stu-id="513b3-297">exclude</span></span> | <span data-ttu-id="513b3-298">Eine durch Kommas abgetrennte Liste mit Include/Exclude-Tags (s. Tabelle unten), in der auf die Abhängigkeit verwiesen wird, die nicht in das endgültige Paket eingefügt werden soll.</span><span class="sxs-lookup"><span data-stu-id="513b3-298">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to exclude in the final package.</span></span> <span data-ttu-id="513b3-299">Der Standardwert ist `build,analyzers`, der überschrieben werden kann.</span><span class="sxs-lookup"><span data-stu-id="513b3-299">The  default value is `build,analyzers` which can be over-written.</span></span> <span data-ttu-id="513b3-300">`content/ ContentFiles` werden jedoch auch implizit im endgültigen Paket ausgeschlossen, das nicht überschrieben werden kann.</span><span class="sxs-lookup"><span data-stu-id="513b3-300">But `content/ ContentFiles` are also implicitly excluded in the final package which can't be over-written.</span></span> <span data-ttu-id="513b3-301">`exclude`-Tags haben Vorrang gegenüber `include`-Tags.</span><span class="sxs-lookup"><span data-stu-id="513b3-301">Tags specified with `exclude` take precedence over those specified with `include`.</span></span> <span data-ttu-id="513b3-302">Beispielsweise entspricht `include="runtime, compile" exclude="compile"``include="runtime"`.</span><span class="sxs-lookup"><span data-stu-id="513b3-302">For example, `include="runtime, compile" exclude="compile"` is the same as `include="runtime"`.</span></span> |

| <span data-ttu-id="513b3-303">Include/Exclude-Tag</span><span class="sxs-lookup"><span data-stu-id="513b3-303">Include/Exclude tag</span></span> | <span data-ttu-id="513b3-304">Betroffene Ordner im Ziel</span><span class="sxs-lookup"><span data-stu-id="513b3-304">Affected folders of the target</span></span> |
| --- | --- |
| <span data-ttu-id="513b3-305">contentFiles</span><span class="sxs-lookup"><span data-stu-id="513b3-305">contentFiles</span></span> | <span data-ttu-id="513b3-306">Inhalt</span><span class="sxs-lookup"><span data-stu-id="513b3-306">Content</span></span> |
| <span data-ttu-id="513b3-307">Laufzeit</span><span class="sxs-lookup"><span data-stu-id="513b3-307">runtime</span></span> | <span data-ttu-id="513b3-308">Runtime, Ressourcen und Frameworkassemblys</span><span class="sxs-lookup"><span data-stu-id="513b3-308">Runtime, Resources, and FrameworkAssemblies</span></span> |
| <span data-ttu-id="513b3-309">Kompilieren</span><span class="sxs-lookup"><span data-stu-id="513b3-309">compile</span></span> | <span data-ttu-id="513b3-310">lib</span><span class="sxs-lookup"><span data-stu-id="513b3-310">lib</span></span> |
| <span data-ttu-id="513b3-311">build</span><span class="sxs-lookup"><span data-stu-id="513b3-311">build</span></span> | <span data-ttu-id="513b3-312">Build (MSBuild-Eigenschaften und -Ziele)</span><span class="sxs-lookup"><span data-stu-id="513b3-312">build (MSBuild props and targets)</span></span> |
| <span data-ttu-id="513b3-313">Systemeigen</span><span class="sxs-lookup"><span data-stu-id="513b3-313">native</span></span> | <span data-ttu-id="513b3-314">Systemeigen</span><span class="sxs-lookup"><span data-stu-id="513b3-314">native</span></span> |
| <span data-ttu-id="513b3-315">none</span><span class="sxs-lookup"><span data-stu-id="513b3-315">none</span></span> | <span data-ttu-id="513b3-316">Keine Ordner</span><span class="sxs-lookup"><span data-stu-id="513b3-316">No folders</span></span> |
| <span data-ttu-id="513b3-317">all</span><span class="sxs-lookup"><span data-stu-id="513b3-317">all</span></span> | <span data-ttu-id="513b3-318">Alle Ordner</span><span class="sxs-lookup"><span data-stu-id="513b3-318">All folders</span></span> |

<span data-ttu-id="513b3-319">Beispielsweise verweisen die folgenden Zeilen auf Abhängigkeiten auf `PackageA` Version 1.1.0 und höher und `PackageB` Version 1.x.</span><span class="sxs-lookup"><span data-stu-id="513b3-319">For example, the following lines indicate dependencies on `PackageA` version 1.1.0 or higher, and `PackageB` version 1.x.</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" />
    <dependency id="PackageB" version="[1,2)" />
</dependencies>
```

<span data-ttu-id="513b3-320">In den folgenden Zeilen wird zwar auf Abhängigkeiten von denselben Paketen verwiesen, allerdings wird auch angegeben, dass die Ordner `contentFiles` und `build` von `PackageA` sowie alle anderen Ordner bis auf `native` und `compile` von `PackageB` angegeben werden sollen.</span><span class="sxs-lookup"><span data-stu-id="513b3-320">The following lines indicate dependencies on the same packages, but specify to include the `contentFiles` and `build` folders of `PackageA` and everything but the `native` and `compile` folders of `PackageB`"</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" include="contentFiles, build" />
    <dependency id="PackageB" version="[1,2)" exclude="native, compile" />
</dependencies>
```

> [!Important]
> <span data-ttu-id="513b3-321">Beim Erstellen einer `.nuspec` aus einem Projekt mithilfe von `nuget spec`werden Abhängigkeiten, die in diesem Projekt vorhanden sind, nicht automatisch in die resultierende `.nuspec` Datei eingeschlossen.</span><span class="sxs-lookup"><span data-stu-id="513b3-321">When creating a `.nuspec` from a project using `nuget spec`, dependencies that exist in that project are not automatically included in the resulting `.nuspec` file.</span></span> <span data-ttu-id="513b3-322">Verwenden Sie stattdessen `nuget pack myproject.csproj`, und holen Sie sich die *nuspec* -Datei aus der generierten *nupkg* -Datei.</span><span class="sxs-lookup"><span data-stu-id="513b3-322">Instead, use `nuget pack myproject.csproj`, and get the *.nuspec* file from within the generated *.nupkg* file.</span></span> <span data-ttu-id="513b3-323">Diese *. nuspec* -Datei enthält die Abhängigkeiten.</span><span class="sxs-lookup"><span data-stu-id="513b3-323">This *.nuspec* contains the dependencies.</span></span>

### <a name="dependency-groups"></a><span data-ttu-id="513b3-324">Abhängigkeitsgruppen</span><span class="sxs-lookup"><span data-stu-id="513b3-324">Dependency groups</span></span>

<span data-ttu-id="513b3-325">*Version 2.0 und höher*</span><span class="sxs-lookup"><span data-stu-id="513b3-325">*Version 2.0+*</span></span>

<span data-ttu-id="513b3-326">Als Alternative zu einer einzelnen flachen Liste können Abhängigkeiten auf der Grundlage des Frameworkprofils des Zielprojekts angegeben werden, das `<group>`-Elemente in `<dependencies>` verwendet.</span><span class="sxs-lookup"><span data-stu-id="513b3-326">As an alternative to a single flat list, dependencies can be specified according to the framework profile of the target project using `<group>` elements within `<dependencies>`.</span></span>

<span data-ttu-id="513b3-327">Jede Gruppe verfügt über ein Attribut mit dem Namen `targetFramework` und enthält entweder kein `<dependency>`-Element oder mindestens eins.</span><span class="sxs-lookup"><span data-stu-id="513b3-327">Each group has an attribute named `targetFramework` and contains zero or more `<dependency>` elements.</span></span> <span data-ttu-id="513b3-328">Diese Abhängigkeiten werden zusammen installiert, wenn das Zielframework kompatibel mit dem Frameworkprofil des Projekts ist.</span><span class="sxs-lookup"><span data-stu-id="513b3-328">Those dependencies are installed together when  the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="513b3-329">Das `<group>`-Element ohne ein `targetFramework`-Attribut wird als Standard- oder Ausweichliste der Abhängigkeiten verwendet.</span><span class="sxs-lookup"><span data-stu-id="513b3-329">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of dependencies.</span></span> <span data-ttu-id="513b3-330">Die genauen Frameworkbezeichner finden Sie unter [Zielframeworks](../reference/target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="513b3-330">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="513b3-331">Das Gruppenformat kann nicht mit einer flachen Liste vermischt werden.</span><span class="sxs-lookup"><span data-stu-id="513b3-331">The group format cannot be intermixed with a flat list.</span></span>

> [!Note]
> <span data-ttu-id="513b3-332">Das im `lib/ref` Ordner verwendete Format des [zielframeworkmonikers (Target Framework Moniker, TFM)](../reference/target-frameworks.md) ist im Vergleich zum in `dependency groups`verwendeten TFM anders.</span><span class="sxs-lookup"><span data-stu-id="513b3-332">The format of [Target Framework Moniker (TFM)](../reference/target-frameworks.md) used in `lib/ref` folder is different when compared to the TFM used in `dependency groups`.</span></span> <span data-ttu-id="513b3-333">Wenn die Ziel Framework-Frameworks, die im `dependencies group` und im Ordner `lib/ref` der `.nuspec` Datei deklariert sind, nicht über exakte Übereinstimmungen verfügen, wird mit `pack` Befehl [nuget Warning NU5128](../reference/errors-and-warnings/nu5128.md)ausgegeben.</span><span class="sxs-lookup"><span data-stu-id="513b3-333">If the target frameworks declared in the `dependencies group` and the `lib/ref` folder of `.nuspec` file do not have exact matches then `pack` command will raise [NuGet Warning NU5128](../reference/errors-and-warnings/nu5128.md).</span></span>

<span data-ttu-id="513b3-334">Im folgenden Beispiel werden verschiedene Variationen des `<group>`-Elements dargestellt:</span><span class="sxs-lookup"><span data-stu-id="513b3-334">The following example shows different variations of the `<group>` element:</span></span>

```xml
<dependencies>
    <group>
        <dependency id="RouteMagic" version="1.1.0" />
    </group>

    <group targetFramework=".NETFramework4.7.2">
        <dependency id="jQuery" version="1.6.2" />
        <dependency id="WebActivator" version="1.4.4" />
    </group>

    <group targetFramework="netcoreapp3.1">
    </group>
</dependencies>
```

<a name="specifying-explicit-assembly-references"></a>

## <a name="explicit-assembly-references"></a><span data-ttu-id="513b3-335">Explizite Assemblyverweise</span><span class="sxs-lookup"><span data-stu-id="513b3-335">Explicit assembly references</span></span>

<span data-ttu-id="513b3-336">Das `<references>`-Element wird von Projekten verwendet, die `packages.config` verwenden, um explizit die Assemblys anzugeben, auf die das Ziel Projekt bei Verwendung des Pakets verweisen soll.</span><span class="sxs-lookup"><span data-stu-id="513b3-336">The `<references>` element is used by projects using `packages.config` to explicitly specify the assemblies that the target project should reference when using the package.</span></span> <span data-ttu-id="513b3-337">In der Regel werden Verweise nur für Assemblys zur Entwurfszeit verwendet.</span><span class="sxs-lookup"><span data-stu-id="513b3-337">Explicit references are typically used for design-time only assemblies.</span></span> <span data-ttu-id="513b3-338">Weitere Informationen finden Sie auf der Seite zum [Auswählen von](../create-packages/select-assemblies-referenced-by-projects.md) Assemblys, auf die von-Projekten verwiesen wird.</span><span class="sxs-lookup"><span data-stu-id="513b3-338">For more information, see the page on [selecting assemblies referenced by projects](../create-packages/select-assemblies-referenced-by-projects.md) for more information.</span></span>

<span data-ttu-id="513b3-339">Beispielsweise gibt das folgende `<references>`-Element NuGet die Anweisung, Verweise nur zu `xunit.dll` und `xunit.extensions.dll` hinzuzufügen, wenn zusätzliche Assemblys in dem Paket enthalten sind:</span><span class="sxs-lookup"><span data-stu-id="513b3-339">For example, the following `<references>` element instructs NuGet to add references to only `xunit.dll` and `xunit.extensions.dll` even if there are additional assemblies in the package:</span></span>

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

### <a name="reference-groups"></a><span data-ttu-id="513b3-340">Verweisgruppen</span><span class="sxs-lookup"><span data-stu-id="513b3-340">Reference groups</span></span>

<span data-ttu-id="513b3-341">Als Alternative zu einer einzelnen flachen Liste können Verweise auf der Grundlage des Frameworkprofils des Zielprojekts angegeben werden, das `<group>`-Elemente in `<references>` verwendet.</span><span class="sxs-lookup"><span data-stu-id="513b3-341">As an alternative to a single flat list, references can be specified according to the framework profile of the target project using `<group>` elements within `<references>`.</span></span>

<span data-ttu-id="513b3-342">Jede Gruppe verfügt über ein Attribut mit dem Namen `targetFramework` und enthält entweder kein `<reference>`-Element oder mindestens eins.</span><span class="sxs-lookup"><span data-stu-id="513b3-342">Each group has an attribute named `targetFramework` and contains zero or more `<reference>` elements.</span></span> <span data-ttu-id="513b3-343">Diese Verweise werden einem Projekt hinzugefügt, wenn das Zielframework mit dem Frameworkprofil des Projekts kompatibel ist.</span><span class="sxs-lookup"><span data-stu-id="513b3-343">Those references are added to a project when the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="513b3-344">Das `<group>`-Element ohne ein `targetFramework`-Attribut wird als Standard- oder Ausweichliste der Verweise verwendet.</span><span class="sxs-lookup"><span data-stu-id="513b3-344">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of references.</span></span> <span data-ttu-id="513b3-345">Die genauen Frameworkbezeichner finden Sie unter [Zielframeworks](../reference/target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="513b3-345">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="513b3-346">Das Gruppenformat kann nicht mit einer flachen Liste vermischt werden.</span><span class="sxs-lookup"><span data-stu-id="513b3-346">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="513b3-347">Im folgenden Beispiel werden verschiedene Variationen des `<group>`-Elements dargestellt:</span><span class="sxs-lookup"><span data-stu-id="513b3-347">The following example shows different variations of the `<group>` element:</span></span>

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

## <a name="framework-assembly-references"></a><span data-ttu-id="513b3-348">Verweise auf Frameworkassemblys</span><span class="sxs-lookup"><span data-stu-id="513b3-348">Framework assembly references</span></span>

<span data-ttu-id="513b3-349">Frameworkassemblys gehören zum .NET Framework und sollten für jeden vorhandenen Computer bereits im globalen Assemblycache vorhanden sein.</span><span class="sxs-lookup"><span data-stu-id="513b3-349">Framework assemblies are those that are part of the .NET framework and should already be in the global assembly cache (GAC) for any given machine.</span></span> <span data-ttu-id="513b3-350">Pakete können sicherstellen, dass die erforderlichen Verweise, falls nötig, dem Projekt hinzugefügt werden, indem es diese Assemblys im `<frameworkAssemblies>`-Element erkennt.</span><span class="sxs-lookup"><span data-stu-id="513b3-350">By identifying those assemblies within the `<frameworkAssemblies>` element, a package can ensure that required references are added to a project in the event that the project doesn't have such references already.</span></span> <span data-ttu-id="513b3-351">Solche Assemblys sind nicht von Anfang an in Paketen enthalten.</span><span class="sxs-lookup"><span data-stu-id="513b3-351">Such assemblies, of course, are not included in a package directly.</span></span>

<span data-ttu-id="513b3-352">Das `<frameworkAssemblies>`-Element enthält entweder kein `<frameworkAssembly>`-Element oder mindestens eins, das die folgenden Attribute angibt:</span><span class="sxs-lookup"><span data-stu-id="513b3-352">The `<frameworkAssemblies>` element contains zero or more `<frameworkAssembly>` elements, each of which specifies the following attributes:</span></span>

| <span data-ttu-id="513b3-353">attribute</span><span class="sxs-lookup"><span data-stu-id="513b3-353">Attribute</span></span> | <span data-ttu-id="513b3-354">BESCHREIBUNG</span><span class="sxs-lookup"><span data-stu-id="513b3-354">Description</span></span> |
| --- | --- |
| <span data-ttu-id="513b3-355">**assemblyName**</span><span class="sxs-lookup"><span data-stu-id="513b3-355">**assemblyName**</span></span> | <span data-ttu-id="513b3-356">(Erforderlich) Der vollqualifizierte Assemblyname.</span><span class="sxs-lookup"><span data-stu-id="513b3-356">(Required) The fully qualified assembly name.</span></span> |
| <span data-ttu-id="513b3-357">**targetFramework**</span><span class="sxs-lookup"><span data-stu-id="513b3-357">**targetFramework**</span></span> | <span data-ttu-id="513b3-358">(Optional) Gibt das Zielframework an, auf das sich dieser Verweis bezieht.</span><span class="sxs-lookup"><span data-stu-id="513b3-358">(Optional) Specifies the target framework to which this reference applies.</span></span> <span data-ttu-id="513b3-359">Wenn dieses Attribut nicht vorhanden ist, deutet dies darauf hin, dass sich der Verweis auf alle Frameworks bezieht.</span><span class="sxs-lookup"><span data-stu-id="513b3-359">If omitted, indicates that the reference applies to all frameworks.</span></span> <span data-ttu-id="513b3-360">Die genauen Frameworkbezeichner finden Sie unter [Zielframeworks](../reference/target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="513b3-360">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span> |

<span data-ttu-id="513b3-361">Im folgenden Beispiel werden Verweise auf `System.Net` für alle Zielframeworks und auf `System.ServiceModel` für ausschließlich .NET Framework 4.0 dargestellt:</span><span class="sxs-lookup"><span data-stu-id="513b3-361">The following example shows a reference to `System.Net` for all target frameworks, and a reference to `System.ServiceModel` for .NET Framework 4.0 only:</span></span>

```xml
<frameworkAssemblies>
    <frameworkAssembly assemblyName="System.Net"  />

    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
</frameworkAssemblies>
```

<a name="specifying-files-to-include-in-the-package"></a>

## <a name="including-assembly-files"></a><span data-ttu-id="513b3-362">Einfügen von Assemblydateien</span><span class="sxs-lookup"><span data-stu-id="513b3-362">Including assembly files</span></span>

<span data-ttu-id="513b3-363">Wenn Sie die unter [Creating a Package (Erstellen eines Pakets)](../create-packages/creating-a-package.md) beschriebenen Anweisungen ausführen, müssen Sie nicht explizit eine Liste mit Dateien in der `.nuspec`-Datei angeben.</span><span class="sxs-lookup"><span data-stu-id="513b3-363">If you follow the conventions described in [Creating a Package](../create-packages/creating-a-package.md), you do not have to explicitly specify a list of files in the `.nuspec` file.</span></span> <span data-ttu-id="513b3-364">Der `nuget pack`-Befehl ruft die benötigten Dateien automatisch ab.</span><span class="sxs-lookup"><span data-stu-id="513b3-364">The `nuget pack` command automatically picks up the necessary files.</span></span>

> [!Important]
> <span data-ttu-id="513b3-365">Wenn ein Paket in einem Projekt installiert wird, fügt NuGet automatisch der DLL des Pakets Assemblyverweise hinzu. Die Verweise, die mit *benannt sind werden dabei allerdings*nicht`.resources.dll` hinzugefügt, da angenommen wird, dass es sich dabei um lokalisierte Satellitenassemblys handelt.</span><span class="sxs-lookup"><span data-stu-id="513b3-365">When a package is installed into a project, NuGet automatically adds assembly references to the package's DLLs, *excluding* those that are named `.resources.dll` because they are assumed to be localized satellite assemblies.</span></span> <span data-ttu-id="513b3-366">Vermeiden Sie aus diesem Grund die Verwendung von `.resources.dll` für Dateien, die darüber hinaus wichtigen Paketcode enthalten.</span><span class="sxs-lookup"><span data-stu-id="513b3-366">For this reason, avoid using `.resources.dll` for files that otherwise contain essential package code.</span></span>

<span data-ttu-id="513b3-367">Legen Sie ein `<files>`-Element als untergeordnetes Element von `<package>` und als gleichgeordnetes Element von `<metadata>` fest, das jeder Datei ein separates `<file>`-Element zuordnet, um diese automatischen Vorgänge zu umgehen und genau zu kontrollieren, welche Dateien in einem Paket enthalten sind.</span><span class="sxs-lookup"><span data-stu-id="513b3-367">To bypass this automatic behavior and explicitly control which files are included in a package, place a `<files>` element as a child of `<package>` (and a sibling of `<metadata>`), identifying each file with a separate `<file>` element.</span></span> <span data-ttu-id="513b3-368">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="513b3-368">For example:</span></span>

```xml
<files>
    <file src="bin\Debug\*.dll" target="lib" />
    <file src="bin\Debug\*.pdb" target="lib" />
    <file src="tools\**\*.*" exclude="**\*.log" />
</files>
```

<span data-ttu-id="513b3-369">Das `packages.config`-Element wird bei NuGet 2.x und früher sowie bei Projekten, die `<files>` verwenden, außerdem verwendet, um unveränderliche Inhaltsdateien während der Paketinstallation einzufügen.</span><span class="sxs-lookup"><span data-stu-id="513b3-369">With NuGet 2.x and earlier, and projects using `packages.config`, the `<files>` element is also used to include immutable content files when a package is installed.</span></span> <span data-ttu-id="513b3-370">Bei NuGet 3.3 und höher und Projekten, die PackageReference verwenden, wird stattdessen das `<contentFiles>`-Element verwendet.</span><span class="sxs-lookup"><span data-stu-id="513b3-370">With NuGet 3.3+ and projects PackageReference, the `<contentFiles>` element is used instead.</span></span> <span data-ttu-id="513b3-371">Weitere Informationen finden Sie unter [Einfügen von Inhaltsdateien](#including-content-files).</span><span class="sxs-lookup"><span data-stu-id="513b3-371">See [Including content files](#including-content-files) below for details.</span></span>

### <a name="file-element-attributes"></a><span data-ttu-id="513b3-372">Dateielementattribute</span><span class="sxs-lookup"><span data-stu-id="513b3-372">File element attributes</span></span>

<span data-ttu-id="513b3-373">Jedes `<file>`-Element gibt die folgenden Attribute an:</span><span class="sxs-lookup"><span data-stu-id="513b3-373">Each `<file>` element specifies the following attributes:</span></span>

| <span data-ttu-id="513b3-374">attribute</span><span class="sxs-lookup"><span data-stu-id="513b3-374">Attribute</span></span> | <span data-ttu-id="513b3-375">BESCHREIBUNG</span><span class="sxs-lookup"><span data-stu-id="513b3-375">Description</span></span> |
| --- | --- |
| <span data-ttu-id="513b3-376">**src**</span><span class="sxs-lookup"><span data-stu-id="513b3-376">**src**</span></span> | <span data-ttu-id="513b3-377">Der Speicherort der Dateien, die eingefügt werden sollen, unterliegt Ausnahmen, die von dem `exclude`-Attribut angegeben werden.</span><span class="sxs-lookup"><span data-stu-id="513b3-377">The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="513b3-378">Der Pfad ist relativ zur `.nuspec`-Datei, wenn kein absoluter Pfad angegeben ist.</span><span class="sxs-lookup"><span data-stu-id="513b3-378">The path is relative to the `.nuspec` file unless an absolute path is specified.</span></span> <span data-ttu-id="513b3-379">Das Platzhalterzeichen `*` ist zulässig, und das zweifache Platzhalterzeichen `**` impliziert eine rekursive Ordnersuche.</span><span class="sxs-lookup"><span data-stu-id="513b3-379">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="513b3-380">**Ziel**</span><span class="sxs-lookup"><span data-stu-id="513b3-380">**target**</span></span> | <span data-ttu-id="513b3-381">Der relative Pfad zu dem Ordner in dem Paket, in dem die Quelldateien platziert sind, der mit `lib`, `content`, `build` oder `tools` beginnt.</span><span class="sxs-lookup"><span data-stu-id="513b3-381">The relative path to the folder within the package where the source files are placed, which must begin with `lib`, `content`, `build`, or `tools`.</span></span> <span data-ttu-id="513b3-382">Informationen dazu finden Sie unter [Creating a .nuspec from a convention-based working directory (Erstellen einer NUSPEC-Datei aus einem auf Konventionen basierenden Arbeitsverzeichnis)](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span><span class="sxs-lookup"><span data-stu-id="513b3-382">See [Creating a .nuspec from a convention-based working directory](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span></span> |
| <span data-ttu-id="513b3-383">**exclude**</span><span class="sxs-lookup"><span data-stu-id="513b3-383">**exclude**</span></span> | <span data-ttu-id="513b3-384">Eine durch Semikolons abgetrennte Datei oder Dateimuster, die sich nicht im `src`-Speicherort befinden dürfen.</span><span class="sxs-lookup"><span data-stu-id="513b3-384">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="513b3-385">Das Platzhalterzeichen `*` ist zulässig, und das zweifache Platzhalterzeichen `**` impliziert eine rekursive Ordnersuche.</span><span class="sxs-lookup"><span data-stu-id="513b3-385">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |

### <a name="examples"></a><span data-ttu-id="513b3-386">Beispiele</span><span class="sxs-lookup"><span data-stu-id="513b3-386">Examples</span></span>

<span data-ttu-id="513b3-387">**Einzelne Assembly**</span><span class="sxs-lookup"><span data-stu-id="513b3-387">**Single assembly**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="library.dll" target="lib" />

    Packaged result:
        lib\library.dll

<span data-ttu-id="513b3-388">**Einzelne Assembly, die für ein Zielframework spezifisch ist**</span><span class="sxs-lookup"><span data-stu-id="513b3-388">**Single assembly specific to a target framework**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="assemblies\net40\library.dll" target="lib\net40" />

    Packaged result:
        lib\net40\library.dll

<span data-ttu-id="513b3-389">**Mehrere DLLS, die Platzhalterzeichen verwenden**</span><span class="sxs-lookup"><span data-stu-id="513b3-389">**Set of DLLs using a wildcard**</span></span>

    Source files:
        bin\release\libraryA.dll
        bin\release\libraryB.dll

    .nuspec entry:
        <file src="bin\release\*.dll" target="lib" />

    Packaged result:
        lib\libraryA.dll
        lib\libraryB.dll

<span data-ttu-id="513b3-390">**DLLs für verschiedene Frameworks**</span><span class="sxs-lookup"><span data-stu-id="513b3-390">**DLLs for different frameworks**</span></span>

    Source files:
        lib\net40\library.dll
        lib\net20\library.dll

    .nuspec entry (using ** recursive search):
        <file src="lib\**" target="lib" />

    Packaged result:
        lib\net40\library.dll
        lib\net20\library.dll

<span data-ttu-id="513b3-391">**Ausschließen von Dateien**</span><span class="sxs-lookup"><span data-stu-id="513b3-391">**Excluding files**</span></span>

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

## <a name="including-content-files"></a><span data-ttu-id="513b3-392">Einfügen von Inhaltsdateien</span><span class="sxs-lookup"><span data-stu-id="513b3-392">Including content files</span></span>

<span data-ttu-id="513b3-393">Bei Inhaltsdateien handelt es sich um unveränderliche Dateien, die ein Paket in ein Projekt einfügen muss.</span><span class="sxs-lookup"><span data-stu-id="513b3-393">Content files are immutable files that a package needs to include in a project.</span></span> <span data-ttu-id="513b3-394">Da sie unveränderlich sind, sollen sie auch nicht von dem verarbeitenden Projekt geändert werden.</span><span class="sxs-lookup"><span data-stu-id="513b3-394">Being immutable, they are not intended to be modified by the consuming project.</span></span> <span data-ttu-id="513b3-395">Zu den Inhaltsdateien gehören z.B.:</span><span class="sxs-lookup"><span data-stu-id="513b3-395">Example content files include:</span></span>

- <span data-ttu-id="513b3-396">Bilder, die als Ressourcen eingebettet werden</span><span class="sxs-lookup"><span data-stu-id="513b3-396">Images that are embedded as resources</span></span>
- <span data-ttu-id="513b3-397">Quelldateien, die bereits kompiliert sind</span><span class="sxs-lookup"><span data-stu-id="513b3-397">Source files that are already compiled</span></span>
- <span data-ttu-id="513b3-398">Skripts, die in die Buildausgabe des Projekts eingefügt werden müssen</span><span class="sxs-lookup"><span data-stu-id="513b3-398">Scripts that need to be included with the build output of the project</span></span>
- <span data-ttu-id="513b3-399">Konfigurationsdateien für das Paket, die zwar in das Projekt eingefügt werden müssen, an denen jedoch keine projektspezifischen Änderungen vorgenommen werden müssen.</span><span class="sxs-lookup"><span data-stu-id="513b3-399">Configuration files for the package that need to be included in the project but don't need any project-specific changes</span></span>

<span data-ttu-id="513b3-400">Inhaltsdateien werden in ein Paket eingefügt, das das `<files>`-Element verwendet, das den `content`-Ordner im `target`-Attribut angibt.</span><span class="sxs-lookup"><span data-stu-id="513b3-400">Content files are included in a package using the `<files>` element, specifying the `content` folder in the `target` attribute.</span></span> <span data-ttu-id="513b3-401">Allerdings werden diese Dateien ignoriert, wenn das Paket über PackageReference in ein Projekt installiert wird, das stattdessen das `<contentFiles>`-Element verwendet.</span><span class="sxs-lookup"><span data-stu-id="513b3-401">However, such files are ignored when the package is installed in a project using PackageReference, which instead uses the `<contentFiles>` element.</span></span>

<span data-ttu-id="513b3-402">Im Idealfall geben Pakete die Inhaltsdateien in beiden Elementen an, um ein höchstmögliches Maß an Kompatibilität mit den verarbeitenden Projekten zu erreichen.</span><span class="sxs-lookup"><span data-stu-id="513b3-402">For maximum compatibility with consuming projects, a package ideally specifies the content files in both elements.</span></span>

### <a name="using-the-files-element-for-content-files"></a><span data-ttu-id="513b3-403">Verwenden des Dateielements für Inhaltsdateien</span><span class="sxs-lookup"><span data-stu-id="513b3-403">Using the files element for content files</span></span>

<span data-ttu-id="513b3-404">Verwenden Sie für Inhaltsdateien einfach dasselbe Format wie für Assemblydateien. Geben Sie dabei allerdings `content` als Basisordner im `target`-Attribut an, wie in den folgenden Beispielen dargestellt wird.</span><span class="sxs-lookup"><span data-stu-id="513b3-404">For content files, simply use the same format as for assembly files, but specify `content` as the base folder in the `target` attribute as shown in the following examples.</span></span>

<span data-ttu-id="513b3-405">**Grundlegende Inhaltsdateien**</span><span class="sxs-lookup"><span data-stu-id="513b3-405">**Basic content files**</span></span>

    Source files:
        css\mobile\style1.css
        css\mobile\style2.css

    .nuspec entry:
        <file src="css\mobile\*.css" target="content\css\mobile" />

    Packaged result:
        content\css\mobile\style1.css
        content\css\mobile\style2.css

<span data-ttu-id="513b3-406">**Inhaltsdateien mit Verzeichnisstruktur**</span><span class="sxs-lookup"><span data-stu-id="513b3-406">**Content files with directory structure**</span></span>

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

<span data-ttu-id="513b3-407">**Inhaltsdatei, die für ein Zielframework spezifisch ist**</span><span class="sxs-lookup"><span data-stu-id="513b3-407">**Content file specific to a target framework**</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry
        <file src="css\cool\style.css" target="Content" />

    Packaged result:
        content\style.css

<span data-ttu-id="513b3-408">**Inhaltsdatei, die in einen Ordner mit einem Punkt im Namen kopiert wird**</span><span class="sxs-lookup"><span data-stu-id="513b3-408">**Content file copied to a folder with dot in name**</span></span>

<span data-ttu-id="513b3-409">In diesem Fall erkennt NuGet, dass die Erweiterung in `target` nicht mit der Erweiterung in `src` übereinstimmt, und behandelt dieses Bestandteil des Namens in `target` als einen Ordner:</span><span class="sxs-lookup"><span data-stu-id="513b3-409">In this case, NuGet sees that the extension in `target` does not match the extension in `src` and thus treats that part of the name in `target` as a folder:</span></span>

    Source file:
        images\picture.png

    .nuspec entry:
        <file src="images\picture.png" target="Content\images\package.icons" />

    Packaged result:
        content\images\package.icons\picture.png

<span data-ttu-id="513b3-410">**Inhaltsdateien ohne Erweiterungen**</span><span class="sxs-lookup"><span data-stu-id="513b3-410">**Content files without extensions**</span></span>

<span data-ttu-id="513b3-411">Verwenden Sie die Platzhalterzeichen `*` oder `**`, um Dateien ohne Erweiterungen einzufügen:</span><span class="sxs-lookup"><span data-stu-id="513b3-411">To include files without an extension, use the `*` or `**` wildcards:</span></span>

    Source file:
        flags\installed

    .nuspec entry:
        <file src="flags\**" target="flags" />

    Packaged result:
        flags\installed

<span data-ttu-id="513b3-412">**Inhaltsdateien mit tiefen Pfaden und tiefen Zielen**</span><span class="sxs-lookup"><span data-stu-id="513b3-412">**Content files with deep path and deep target**</span></span>

<span data-ttu-id="513b3-413">In diesem Fall nimmt NuGet an, dass das Ziel ein Dateiname und kein Ordner ist, da die Dateierweiterungen von Quelle und Ziel übereinstimmen:</span><span class="sxs-lookup"><span data-stu-id="513b3-413">In this case, because the file extensions of the source and target match, NuGet assumes that the target is a file name and not a folder:</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry:
        <file src="css\cool\style.css" target="Content\css\cool" />
        or:
        <file src="css\cool\style.css" target="Content\css\cool\style.css" />

    Packaged result:
        content\css\cool\style.css

<span data-ttu-id="513b3-414">**Umbenennen einer Inhaltsdatei im Paket**</span><span class="sxs-lookup"><span data-stu-id="513b3-414">**Renaming a content file in the package**</span></span>

    Source file:
        ie\css\style.css

    .nuspec entry:
        <file src="ie\css\style.css" target="Content\css\ie.css" />

    Packaged result:
        content\css\ie.css

<span data-ttu-id="513b3-415">**Ausschließen von Dateien**</span><span class="sxs-lookup"><span data-stu-id="513b3-415">**Excluding files**</span></span>

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

### <a name="using-the-contentfiles-element-for-content-files"></a><span data-ttu-id="513b3-416">Verwenden des contentFiles-Elements für Inhaltsdateien</span><span class="sxs-lookup"><span data-stu-id="513b3-416">Using the contentFiles element for content files</span></span>

<span data-ttu-id="513b3-417">*NuGet 4.0 und höher mit PackageReference*</span><span class="sxs-lookup"><span data-stu-id="513b3-417">*NuGet 4.0+ with PackageReference*</span></span>

<span data-ttu-id="513b3-418">Standardmäßig platzieren Pakete Inhalte in einem `contentFiles`-Ordner (s. unten), in den `nuget pack` alle Dateien mithilfe von Standardattributen eingefügt hat.</span><span class="sxs-lookup"><span data-stu-id="513b3-418">By default, a package places content in a `contentFiles` folder (see below) and `nuget pack` included all files in that folder using default attributes.</span></span> <span data-ttu-id="513b3-419">In diesem Fall ist es nicht notwendig, einen `contentFiles`-Knoten in `.nuspec` einzufügen.</span><span class="sxs-lookup"><span data-stu-id="513b3-419">In this case it's not necessary to include a `contentFiles` node in the `.nuspec` at all.</span></span>

<span data-ttu-id="513b3-420">Das `<contentFiles>`-Element gibt eine Auflistung von `<files>`-Elementen an, die die eingefügten Dateien erkennen, um zu kontrollieren, welche Dateien eingefügt wurden.</span><span class="sxs-lookup"><span data-stu-id="513b3-420">To control which files are included, the `<contentFiles>` element specifies is a collection of `<files>` elements that identify the exact files include.</span></span>

<span data-ttu-id="513b3-421">Diese Dateien werden zusammen mit mehreren Attributen angegeben, die beschreiben, wie sie in dem Projektsystem verwendet werden sollen:</span><span class="sxs-lookup"><span data-stu-id="513b3-421">These files are specified with a set of attributes that describe how they should be used within the project system:</span></span>

| <span data-ttu-id="513b3-422">attribute</span><span class="sxs-lookup"><span data-stu-id="513b3-422">Attribute</span></span> | <span data-ttu-id="513b3-423">BESCHREIBUNG</span><span class="sxs-lookup"><span data-stu-id="513b3-423">Description</span></span> |
| --- | --- |
| <span data-ttu-id="513b3-424">**include**</span><span class="sxs-lookup"><span data-stu-id="513b3-424">**include**</span></span> | <span data-ttu-id="513b3-425">(Erforderlich) Der Speicherort der Dateien, die eingefügt werden sollen, unterliegt Ausnahmen, die von dem `exclude`-Attribut angegeben werden.</span><span class="sxs-lookup"><span data-stu-id="513b3-425">(Required) The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="513b3-426">Der Pfad ist relativ zum `contentFiles` Ordner, es sei denn, es wurde ein absoluter Pfad angegeben.</span><span class="sxs-lookup"><span data-stu-id="513b3-426">The path is relative to the `contentFiles` folder unless an absolute path is specified.</span></span> <span data-ttu-id="513b3-427">Das Platzhalterzeichen `*` ist zulässig, und das zweifache Platzhalterzeichen `**` impliziert eine rekursive Ordnersuche.</span><span class="sxs-lookup"><span data-stu-id="513b3-427">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="513b3-428">**exclude**</span><span class="sxs-lookup"><span data-stu-id="513b3-428">**exclude**</span></span> | <span data-ttu-id="513b3-429">Eine durch Semikolons abgetrennte Datei oder Dateimuster, die sich nicht im `src`-Speicherort befinden dürfen.</span><span class="sxs-lookup"><span data-stu-id="513b3-429">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="513b3-430">Das Platzhalterzeichen `*` ist zulässig, und das zweifache Platzhalterzeichen `**` impliziert eine rekursive Ordnersuche.</span><span class="sxs-lookup"><span data-stu-id="513b3-430">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="513b3-431">**buildAction**</span><span class="sxs-lookup"><span data-stu-id="513b3-431">**buildAction**</span></span> | <span data-ttu-id="513b3-432">Die Buildaktion, die dem Inhalts Element für MSBuild zugewiesen werden soll, z. b. `Content`, `None`, `Embedded Resource`, `Compile`usw. Der Standardwert ist `Compile`.</span><span class="sxs-lookup"><span data-stu-id="513b3-432">The build action to assign to the content item for MSBuild, such as `Content`, `None`, `Embedded Resource`, `Compile`, etc. The default is `Compile`.</span></span> |
| <span data-ttu-id="513b3-433">**copyToOutput**</span><span class="sxs-lookup"><span data-stu-id="513b3-433">**copyToOutput**</span></span> | <span data-ttu-id="513b3-434">Boolescher Wert, mit dem angegeben wird, ob Inhaltselemente in den Buildausgabeordner (oder den Veröffentlichungsausgabeordner) kopiert werden sollen.</span><span class="sxs-lookup"><span data-stu-id="513b3-434">A Boolean indicating whether to copy content items to the build (or publish) output folder.</span></span> <span data-ttu-id="513b3-435">Die Standardeinstellung ist „false“.</span><span class="sxs-lookup"><span data-stu-id="513b3-435">The default is false.</span></span> |
| <span data-ttu-id="513b3-436">**flatten**</span><span class="sxs-lookup"><span data-stu-id="513b3-436">**flatten**</span></span> | <span data-ttu-id="513b3-437">Ein boolescher Wert, der angibt, ob Inhaltselemente in einen Ordner in der Buildausgabe kopiert werden sollen (TRUE) oder ob die Ordnerstruktur in den Paketen beibehalten werden soll (FALSE).</span><span class="sxs-lookup"><span data-stu-id="513b3-437">A Boolean indicating whether to copy content items to a single folder in the build output (true), or to preserve the folder structure in the package (false).</span></span> <span data-ttu-id="513b3-438">Diese Flag funktioniert nur, wenn das copyToOutput-Flag auf TRUE festgelegt ist.</span><span class="sxs-lookup"><span data-stu-id="513b3-438">This flag only works when copyToOutput flag is set to true.</span></span> <span data-ttu-id="513b3-439">Die Standardeinstellung ist „false“.</span><span class="sxs-lookup"><span data-stu-id="513b3-439">The default is false.</span></span> |

<span data-ttu-id="513b3-440">NuGet wendet die untergeordneten Elemente von `<contentFiles>` bei der Installation eines Pakets von unten nach oben an.</span><span class="sxs-lookup"><span data-stu-id="513b3-440">When installing a package, NuGet applies the child elements of `<contentFiles>` from top to bottom.</span></span> <span data-ttu-id="513b3-441">Wenn mehrere Einträge in einer Datei vorhanden sind, werden sie alle angewendet.</span><span class="sxs-lookup"><span data-stu-id="513b3-441">If multiple entries match the same file then all entries are applied.</span></span> <span data-ttu-id="513b3-442">Der höher geordnete Eintrag setzt die untergeordneten Einträge außer Kraft, wenn ein Konflikt für ein Attribut entsteht.</span><span class="sxs-lookup"><span data-stu-id="513b3-442">The top-most entry overrides the lower entries if there is a conflict for the same attribute.</span></span>

#### <a name="package-folder-structure"></a><span data-ttu-id="513b3-443">Paketordnerstruktur</span><span class="sxs-lookup"><span data-stu-id="513b3-443">Package folder structure</span></span>

<span data-ttu-id="513b3-444">Das Paketprojekt sollte Inhalte mithilfe des folgenden Musters strukturieren:</span><span class="sxs-lookup"><span data-stu-id="513b3-444">The package project should structure content using the following pattern:</span></span>

    /contentFiles/{codeLanguage}/{TxM}/{any?}

- <span data-ttu-id="513b3-445">`codeLanguages` kann `cs`, `vb`, `fs`, `any` oder das klein geschriebene Äquivalent einer `$(ProjectLanguage)` sein.</span><span class="sxs-lookup"><span data-stu-id="513b3-445">`codeLanguages` may be `cs`, `vb`, `fs`, `any`, or the lowercase equivalent of a given `$(ProjectLanguage)`</span></span>
- <span data-ttu-id="513b3-446">`TxM` ist ein für das Zielframework zulässiger Moniker, der NuGet unterstützt (Informationen dazu finden Sie unter [Zielframeworks](../reference/target-frameworks.md)).</span><span class="sxs-lookup"><span data-stu-id="513b3-446">`TxM` is any legal target framework moniker that NuGet supports (see [Target frameworks](../reference/target-frameworks.md)).</span></span>
- <span data-ttu-id="513b3-447">An das Ende der Syntax kann eine beliebige Ordnerstruktur angehängt werden.</span><span class="sxs-lookup"><span data-stu-id="513b3-447">Any folder structure may be appended to the end of this syntax.</span></span>

<span data-ttu-id="513b3-448">Beispiel:</span><span class="sxs-lookup"><span data-stu-id="513b3-448">For example:</span></span>

    Language- and framework-agnostic:
        /contentFiles/any/any/config.xml

    net45 content for all languages
        /contentFiles/any/net45/config.xml

    C#-specific content for net45 and up
        /contentFiles/cs/net45/sample.cs

<span data-ttu-id="513b3-449">Für leere Ordner kann `.` eingefügt werden, wenn diese keine Inhalte mehr für bestimmte Sprachen und TxM bereitstellen sollen. Z.B.:</span><span class="sxs-lookup"><span data-stu-id="513b3-449">Empty folders can use `.` to opt out of providing content for certain combinations of language and TxM, for example:</span></span>

    /contentFiles/vb/any/code.vb
    /contentFiles/cs/any/.

#### <a name="example-contentfiles-section"></a><span data-ttu-id="513b3-450">Beispiel: Abschnitt „contentFiles“</span><span class="sxs-lookup"><span data-stu-id="513b3-450">Example contentFiles section</span></span>

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

## <a name="framework-reference-groups"></a><span data-ttu-id="513b3-451">Framework-Verweis Gruppen</span><span class="sxs-lookup"><span data-stu-id="513b3-451">Framework reference groups</span></span>

<span data-ttu-id="513b3-452">*Nur Version 5.1 + voranstellen packagereferenzierung*</span><span class="sxs-lookup"><span data-stu-id="513b3-452">*Version 5.1+ wih PackageReference only*</span></span>

<span data-ttu-id="513b3-453">Frameworkverweise sind ein .net Core-Konzept, das freigegebene Frameworks wie WPF oder Windows Forms darstellt.</span><span class="sxs-lookup"><span data-stu-id="513b3-453">Framework References are a .NET Core concept representing shared frameworks such as WPF or Windows Forms.</span></span>
<span data-ttu-id="513b3-454">Durch die Angabe eines freigegebenen Frameworks stellt das Paket sicher, dass alle frameworkabhängigkeiten im verweisenden Projekt enthalten sind.</span><span class="sxs-lookup"><span data-stu-id="513b3-454">By specifying a shared framework, the package ensures that all its framework dependencies are included in the referencing project.</span></span>

<span data-ttu-id="513b3-455">Jedes `<group>` Element erfordert ein `targetFramework` Attribut und 0 (null) oder mehr `<frameworkReference>` Elemente.</span><span class="sxs-lookup"><span data-stu-id="513b3-455">Each `<group>` element requires a `targetFramework` attribute and zero or more `<frameworkReference>` elements.</span></span>

<span data-ttu-id="513b3-456">Das folgende Beispiel zeigt eine nuspec, die für ein .net Core-WPF-Projekt generiert wurde.</span><span class="sxs-lookup"><span data-stu-id="513b3-456">The following example shows a nuspec generated for a .NET Core WPF project.</span></span>
<span data-ttu-id="513b3-457">Beachten Sie, dass das manuelle Erstellen von nuspecs, die frameworkverweise enthalten, nicht empfohlen wird.</span><span class="sxs-lookup"><span data-stu-id="513b3-457">Note that hand authoring nuspecs that contain framework references is not recommended.</span></span> <span data-ttu-id="513b3-458">Ziehen Sie stattdessen die Verwendung des [Targets](msbuild-targets.md) -Pakets in Erwägung, das automatisch aus dem Projekt abgeleitet wird.</span><span class="sxs-lookup"><span data-stu-id="513b3-458">Consider using the [targets](msbuild-targets.md) pack instead, which will automatically infer them from the project.</span></span>

```xml
<package xmlns="http://schemas.microsoft.com/packaging/2012/06/nuspec.xsd">
  <metadata>
    <dependencies>
      <group targetFramework=".NETCoreApp3.1" />
    </dependencies>
    <frameworkReferences>
      <group targetFramework=".NETCoreApp3.1">
        <frameworkReference name="Microsoft.WindowsDesktop.App.WPF" />
      </group>
    </frameworkReferences>
  </metadata>
</package>
```

## <a name="example-nuspec-files"></a><span data-ttu-id="513b3-459">NUSPEC-Beispieldateien</span><span class="sxs-lookup"><span data-stu-id="513b3-459">Example nuspec files</span></span>

<span data-ttu-id="513b3-460">**Eine einfache `.nuspec`-Datei, die weder Abhängigkeiten noch Dateien enthält**</span><span class="sxs-lookup"><span data-stu-id="513b3-460">**A simple `.nuspec` that does not specify dependencies or files**</span></span>

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

<span data-ttu-id="513b3-461">**Eine `.nuspec`-Datei mit Abhängigkeiten**</span><span class="sxs-lookup"><span data-stu-id="513b3-461">**A `.nuspec` with dependencies**</span></span>

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

<span data-ttu-id="513b3-462">**Eine `.nuspec`-Datei mit Dateien**</span><span class="sxs-lookup"><span data-stu-id="513b3-462">**A `.nuspec` with files**</span></span>

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

<span data-ttu-id="513b3-463">**Eine `.nuspec`-Datei mit Frameworkassemblys**</span><span class="sxs-lookup"><span data-stu-id="513b3-463">**A `.nuspec` with framework assemblies**</span></span>

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

<span data-ttu-id="513b3-464">In diesem Beispiel werden die folgenden Elemente für bestimmte Projektziele installiert:</span><span class="sxs-lookup"><span data-stu-id="513b3-464">In this example, the following are installed for specific project targets:</span></span>

- <span data-ttu-id="513b3-465">.NET4: `System.Web` und `System.Net`</span><span class="sxs-lookup"><span data-stu-id="513b3-465">.NET4 -> `System.Web`, `System.Net`</span></span>
- <span data-ttu-id="513b3-466">.NET4-Clientprofil: `System.Net`</span><span class="sxs-lookup"><span data-stu-id="513b3-466">.NET4 Client Profile -> `System.Net`</span></span>
- <span data-ttu-id="513b3-467">Silverlight 3: `System.Json`</span><span class="sxs-lookup"><span data-stu-id="513b3-467">Silverlight 3 -> `System.Json`</span></span>
- <span data-ttu-id="513b3-468">WindowsPhone: `Microsoft.Devices.Sensors`</span><span class="sxs-lookup"><span data-stu-id="513b3-468">WindowsPhone -> `Microsoft.Devices.Sensors`</span></span>
