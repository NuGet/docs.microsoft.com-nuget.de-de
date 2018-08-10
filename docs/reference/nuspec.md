---
title: NuSpec-Dateireferenz für NuGet
description: Die NUSPEC-Datei enthält Paketmetadaten, die bei der Erstellung eines Pakets verwendet werden, um für die Paketbenutzer Informationen bereitzustellen.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 08/29/2017
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: 110d1aa29fc7238f1a82c1a81ec6431dfe437420
ms.sourcegitcommit: e9c58dbfc1af2876337dcc37b1b070e8ddec0388
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 08/09/2018
ms.locfileid: "40020452"
---
# <a name="nuspec-reference"></a><span data-ttu-id="91a27-103">NUSPEC-Referenz</span><span class="sxs-lookup"><span data-stu-id="91a27-103">.nuspec reference</span></span>

<span data-ttu-id="91a27-104">Bei einer `.nuspec`-Datei handelt es sich um eine XML-Manifestdatei, die Paketmetadaten enthält.</span><span class="sxs-lookup"><span data-stu-id="91a27-104">A `.nuspec` file is an XML manifest that contains package metadata.</span></span> <span data-ttu-id="91a27-105">Diese Manifestdatei wird sowohl für die Erstellung des Pakets als auch zur Bereitstellung von Informationen für die Benutzer verwendet.</span><span class="sxs-lookup"><span data-stu-id="91a27-105">This manifest is used both to build the package and to provide information to consumers.</span></span> <span data-ttu-id="91a27-106">Manifestdateien sind in allen Paketen enthalten.</span><span class="sxs-lookup"><span data-stu-id="91a27-106">The manifest is always included in a package.</span></span>

<span data-ttu-id="91a27-107">In diesem Thema:</span><span class="sxs-lookup"><span data-stu-id="91a27-107">In this topic:</span></span>

- [<span data-ttu-id="91a27-108">Allgemeine Form und Schema</span><span class="sxs-lookup"><span data-stu-id="91a27-108">General form and schema</span></span>](#general-form-and-schema)
- <span data-ttu-id="91a27-109">[Ersetzungstokens](#replacement-tokens) (bei der Verwendung in einem Visual Studio-Projekt)</span><span class="sxs-lookup"><span data-stu-id="91a27-109">[Replacement tokens](#replacement-tokens) (when used with a Visual Studio project)</span></span>
- [<span data-ttu-id="91a27-110">Abhängigkeiten</span><span class="sxs-lookup"><span data-stu-id="91a27-110">Dependencies</span></span>](#dependencies)
- [<span data-ttu-id="91a27-111">Explizite Assemblyverweise</span><span class="sxs-lookup"><span data-stu-id="91a27-111">Explicit assembly references</span></span>](#explicit-assembly-references)
- [<span data-ttu-id="91a27-112">Verweise auf Frameworkassemblys</span><span class="sxs-lookup"><span data-stu-id="91a27-112">Framework assembly references</span></span>](#framework-assembly-references)
- [<span data-ttu-id="91a27-113">Einfügen von Assemblydateien</span><span class="sxs-lookup"><span data-stu-id="91a27-113">Including assembly files</span></span>](#including-assembly-files)
- [<span data-ttu-id="91a27-114">Einfügen von Inhaltsdateien</span><span class="sxs-lookup"><span data-stu-id="91a27-114">Including content files</span></span>](#including-content-files)
- [<span data-ttu-id="91a27-115">Beispiel: Nuspec-Dateien</span><span class="sxs-lookup"><span data-stu-id="91a27-115">Example nuspec files</span></span>](#example-nuspec-files)

## <a name="general-form-and-schema"></a><span data-ttu-id="91a27-116">Allgemeine Form und Schema</span><span class="sxs-lookup"><span data-stu-id="91a27-116">General form and schema</span></span>

<span data-ttu-id="91a27-117">Die aktuelle `nuspec.xsd`-Schemadatei finden Sie im [NuGet GitHub-Repository](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span><span class="sxs-lookup"><span data-stu-id="91a27-117">The current `nuspec.xsd` schema file can be found in the [NuGet GitHub repository](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span></span>

<span data-ttu-id="91a27-118">Für dieses Schema gilt die im Folgenden dargestellte allgemeine Form für die `.nuspec`-Datei:</span><span class="sxs-lookup"><span data-stu-id="91a27-118">Within this schema, a `.nuspec` file has the following general form:</span></span>

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

<span data-ttu-id="91a27-119">Für eine übersichtliche Darstellung des Schemas öffnen Sie die Schemadatei im Entwurfsmodus in Visual Studio, und klicken Sie auf den Link **XML-Schema-Explorer**.</span><span class="sxs-lookup"><span data-stu-id="91a27-119">For a clear visual representation of the schema, open the schema file in Visual Studio in Design mode and click on the **XML Schema Explorer** link.</span></span> <span data-ttu-id="91a27-120">Alternativ können Sie auch die Datei als Code öffnen, mit der rechten Maustaste in den Editor klicken und **Show XML Schema Explorer** (XML-Schema-Explorer anzeigen) auswählen.</span><span class="sxs-lookup"><span data-stu-id="91a27-120">Alternately, open the file as code, right-click in the editor, and select **Show XML Schema Explorer**.</span></span> <span data-ttu-id="91a27-121">In beiden Fällen wird eine Ansicht zurückgegeben, die der in der folgenden Abbildung ähnlich ist, wenn Sie größtenteils erweitert ist:</span><span class="sxs-lookup"><span data-stu-id="91a27-121">Either way you get a view like the one below (when mostly expanded):</span></span>

![Visual Studio-Schema-Explorer mit geöffneter „nuspec.xsd“-Datei](media/SchemaExplorer.png)

### <a name="required-metadata-elements"></a><span data-ttu-id="91a27-123">Erforderliche Metadatenelemente</span><span class="sxs-lookup"><span data-stu-id="91a27-123">Required metadata elements</span></span>

<span data-ttu-id="91a27-124">Obwohl es sich bei den folgenden Elementen um die Mindestanforderungen für ein Paket handelt, sollten Sie in Erwägung ziehen, die [optionalen Metadatenelemente](#optional-metadata-elements) hinzuzufügen, damit Entwicklern die Arbeit mit Ihren Paketen erleichtert wird.</span><span class="sxs-lookup"><span data-stu-id="91a27-124">Although the following elements are the minimum requirements for a package, you should consider adding the [optional metadata elements](#optional-metadata-elements) to improve the overall experience developers have with your package.</span></span> 

<span data-ttu-id="91a27-125">Diese Elemente müssen in einem `<metadata>`-Element angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="91a27-125">These elements must appear within a `<metadata>` element.</span></span>

#### <a name="id"></a><span data-ttu-id="91a27-126">ID</span><span class="sxs-lookup"><span data-stu-id="91a27-126">id</span></span> 
<span data-ttu-id="91a27-127">Der Paketbezeichner, der die Groß- und Kleinschreibung nicht berücksichtigt und auf nuget.org oder im für das Paket verwendeten Katalog eindeutig sein muss.</span><span class="sxs-lookup"><span data-stu-id="91a27-127">The case-insensitive package identifier, which must be unique across nuget.org or whatever gallery the package resides in.</span></span> <span data-ttu-id="91a27-128">IDs dürfen keine Leerzeichen oder für eine URL unzulässige Zeichen enthalten. Sie müssen den Regeln für .NET-Namespaces entsprechen.</span><span class="sxs-lookup"><span data-stu-id="91a27-128">IDs may not contain spaces or characters that are not valid for a URL, and generally follow .NET namespace rules.</span></span> <span data-ttu-id="91a27-129">Informationen finden Sie unter [Choosing a unique package identifier (Auswählen eines eindeutigen Paketbezeichners)](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number).</span><span class="sxs-lookup"><span data-stu-id="91a27-129">See [Choosing a unique package identifier](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number) for guidance.</span></span> <span data-ttu-id="91a27-130">### Version die Version des Pakets nach dem *major.minor.patch* Muster.</span><span class="sxs-lookup"><span data-stu-id="91a27-130">#### version The version of the package, following the *major.minor.patch* pattern.</span></span> <span data-ttu-id="91a27-131">Versionsnummern enthalten möglicherweise, wie unter [Paketversionsverwaltung](../reference/package-versioning.md#pre-release-versions) beschrieben, ein Suffix der Vorabversion.</span><span class="sxs-lookup"><span data-stu-id="91a27-131">Version numbers may include a pre-release suffix as described in [Package versioning](../reference/package-versioning.md#pre-release-versions).</span></span> 
#### <a name="description"></a><span data-ttu-id="91a27-132">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="91a27-132">description</span></span>
<span data-ttu-id="91a27-133">Eine ausführliche Beschreibung des Pakets für die Anzeige der Benutzeroberfläche.</span><span class="sxs-lookup"><span data-stu-id="91a27-133">A long description of the package for UI display.</span></span> 
#### <a name="authors"></a><span data-ttu-id="91a27-134">authors</span><span class="sxs-lookup"><span data-stu-id="91a27-134">authors</span></span>
<span data-ttu-id="91a27-135">Eine durch Kommas getrennte Liste der Paketautoren, die mit Profilnamen unter nuget.org übereinstimmen. Diese werden im NuGet-Katalog unter nuget.org angezeigt und werden verwendet, um Querverweise auf Pakete von den gleichen Autoren zu geben.</span><span class="sxs-lookup"><span data-stu-id="91a27-135">A comma-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> 

### <a name="optional-metadata-elements"></a><span data-ttu-id="91a27-136">Optionale Metadatenelemente</span><span class="sxs-lookup"><span data-stu-id="91a27-136">Optional metadata elements</span></span>

#### <a name="title"></a><span data-ttu-id="91a27-137">Titel</span><span class="sxs-lookup"><span data-stu-id="91a27-137">title</span></span>
<span data-ttu-id="91a27-138">Ein benutzerfreundlicher Titel des Pakets, der in der Regel in der Benutzeroberfläche wie auf nuget.org angezeigt wird und der Paket-Manager in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="91a27-138">A human-friendly title of the package, typically used in UI displays as on nuget.org and the Package Manager in Visual Studio.</span></span> <span data-ttu-id="91a27-139">Wenn nicht angegeben, wird die Paket-ID verwendet.</span><span class="sxs-lookup"><span data-stu-id="91a27-139">If not specified, the package ID is used.</span></span> 
#### <a name="owners"></a><span data-ttu-id="91a27-140">owners</span><span class="sxs-lookup"><span data-stu-id="91a27-140">owners</span></span>
<span data-ttu-id="91a27-141">Eine durch Kommas getrennte Liste der Paketersteller, die auf nuget.org Profilnamen verwenden. Dabei handelt es sich häufig um dieselbe Liste wie in `authors`. Sie wird beim Hochladen der Pakete auf nuget.org ignoriert. Informationen dazu finden Sie unter [Managing package owners on nuget.org (Verwalten von Paketbesitzern auf nuget.org)](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg).</span><span class="sxs-lookup"><span data-stu-id="91a27-141">A comma-separated list of the package creators using profile names on nuget.org. This is often the same list as in `authors`, and is ignored when uploading the package to nuget.org. See [Managing package owners on nuget.org](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg).</span></span> 
#### <a name="projecturl"></a><span data-ttu-id="91a27-142">projectUrl</span><span class="sxs-lookup"><span data-stu-id="91a27-142">projectUrl</span></span>
<span data-ttu-id="91a27-143">Eine URL für die Paket-Homepage, häufig auf der Benutzeroberfläche sowie auf nuget.org angezeigt.</span><span class="sxs-lookup"><span data-stu-id="91a27-143">A URL for the package's home page, often shown in UI displays as well as nuget.org.</span></span> 
#### <a name="licenseurl"></a><span data-ttu-id="91a27-144">licenseUrl</span><span class="sxs-lookup"><span data-stu-id="91a27-144">licenseUrl</span></span>
<span data-ttu-id="91a27-145">Eine URL für die Paketlizenz, häufig auf der Benutzeroberfläche sowie auf nuget.org angezeigt.</span><span class="sxs-lookup"><span data-stu-id="91a27-145">A URL for the package's license, often shown in UI displays as well as nuget.org.</span></span>
#### <a name="iconurl"></a><span data-ttu-id="91a27-146">iconUrl</span><span class="sxs-lookup"><span data-stu-id="91a27-146">iconUrl</span></span>
<span data-ttu-id="91a27-147">Eine URL für ein 64x64-Bild mit transparentem Hintergrund, das als Symbol für das Paket in der Benutzeroberfläche verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="91a27-147">A URL for a 64x64 image with transparency background to use as the icon for the package in UI display.</span></span> <span data-ttu-id="91a27-148">Stellen Sie sicher, dass dieses Element die *direkte Bild-URL* und nicht nur die URL einer Webseite enthält, die das Bild enthält.</span><span class="sxs-lookup"><span data-stu-id="91a27-148">Be sure this element contains the *direct image URL* and not the URL of a web page containing the image.</span></span> <span data-ttu-id="91a27-149">Beispielsweise um ein Bild von GitHub verwenden möchten, verwenden die URL wie Rohdatendatei <em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>.</span><span class="sxs-lookup"><span data-stu-id="91a27-149">For example, to use an image from GitHub, use the raw file URL like <em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>.</span></span> 

#### <a name="requirelicenseacceptance"></a><span data-ttu-id="91a27-150">requireLicenseAcceptance</span><span class="sxs-lookup"><span data-stu-id="91a27-150">requireLicenseAcceptance</span></span>
<span data-ttu-id="91a27-151">Ein boolescher Wert, der angibt, ob der Client den Benutzer dazu auffordern muss, die Paketlizenz vor der Installation des Pakets zu akzeptieren.</span><span class="sxs-lookup"><span data-stu-id="91a27-151">A Boolean value specifying whether the client must prompt the consumer to accept the package license before installing the package.</span></span>
#### <a name="developmentdependency"></a><span data-ttu-id="91a27-152">developmentDependency</span><span class="sxs-lookup"><span data-stu-id="91a27-152">developmentDependency</span></span>
<span data-ttu-id="91a27-153">*(2.8 und höher)* Ein boolescher Wert, der angibt, ob das Paket mit einer Abhängigkeit markiert werden soll, die nur für die Entwicklung gilt, wodurch vermieden wird, dass das Paket als Abhängigkeit in andere Pakete eingefügt wird.</span><span class="sxs-lookup"><span data-stu-id="91a27-153">*(2.8+)* A Boolean value specifying whether the package is be marked as a development-only-dependency, which prevents the package from being included as a dependency in other packages.</span></span>
#### <a name="summary"></a><span data-ttu-id="91a27-154">Zusammenfassung</span><span class="sxs-lookup"><span data-stu-id="91a27-154">summary</span></span>
<span data-ttu-id="91a27-155">Eine kurze Beschreibung des Pakets für die Anzeige der Benutzeroberfläche.</span><span class="sxs-lookup"><span data-stu-id="91a27-155">A short description of the package for UI display.</span></span> <span data-ttu-id="91a27-156">Wenn diese nicht angegeben wird, wird eine gekürzte Version von `description` verwendet.</span><span class="sxs-lookup"><span data-stu-id="91a27-156">If omitted, a truncated version of `description` is used.</span></span>
#### <a name="releasenotes"></a><span data-ttu-id="91a27-157">releaseNotes</span><span class="sxs-lookup"><span data-stu-id="91a27-157">releaseNotes</span></span>
<span data-ttu-id="91a27-158">*(1.5 und höher)* Eine Beschreibung der in diesem Release des Pakets enthaltenen Änderungen, die häufig in Benutzeroberflächen wie der Registerkarte **Updates** des Visual Studio-Paket-Managers anstelle von Paketbeschreibungen verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="91a27-158">*(1.5+)* A description of the changes made in this release of the package, often used in UI like the **Updates** tab of the Visual Studio Package Manager in place of the package description.</span></span>
#### <a name="copyright"></a><span data-ttu-id="91a27-159">Copyright</span><span class="sxs-lookup"><span data-stu-id="91a27-159">copyright</span></span>
<span data-ttu-id="91a27-160">*(1.5 und höher)* Copyright-Informationen zum Paket.</span><span class="sxs-lookup"><span data-stu-id="91a27-160">*(1.5+)* Copyright details for the package.</span></span>
#### <a name="language"></a><span data-ttu-id="91a27-161">language</span><span class="sxs-lookup"><span data-stu-id="91a27-161">language</span></span>
<span data-ttu-id="91a27-162">Die Gebietsschema-ID des Pakets.</span><span class="sxs-lookup"><span data-stu-id="91a27-162">The locale ID for the package.</span></span> <span data-ttu-id="91a27-163">Informationen dazu finden Sie unter [Creating localized packages (Erstellen von lokalisierten Paketen)](../create-packages/creating-localized-packages.md).</span><span class="sxs-lookup"><span data-stu-id="91a27-163">See [Creating localized packages](../create-packages/creating-localized-packages.md).</span></span>
#### <a name="tags"></a><span data-ttu-id="91a27-164">Tags</span><span class="sxs-lookup"><span data-stu-id="91a27-164">tags</span></span>
<span data-ttu-id="91a27-165">Eine durch Leerzeichen getrennte Liste mit Tags und Schlüsselwörtern, die das Paket beschreiben und zum Ermitteln von Paketen über Suchvorgänge und Filter beitragen.</span><span class="sxs-lookup"><span data-stu-id="91a27-165">A space-delimited list of tags and keywords that describe the package and aid discoverability of packages through search and filtering.</span></span> 
#### <a name="serviceable"></a><span data-ttu-id="91a27-166">gewartet werden müssen</span><span class="sxs-lookup"><span data-stu-id="91a27-166">serviceable</span></span> 
<span data-ttu-id="91a27-167">*(3.3 und höher)* Nur für die interne Verwendung von NuGet.</span><span class="sxs-lookup"><span data-stu-id="91a27-167">*(3.3+)* For internal NuGet use only.</span></span>
#### <a name="repository"></a><span data-ttu-id="91a27-168">Repository</span><span class="sxs-lookup"><span data-stu-id="91a27-168">repository</span></span>
<span data-ttu-id="91a27-169">Repository-Metadaten, bestehend aus vier optionale Attribute: *Typ* und *Url* *(4.0 und höher)*, und *Branch* und *Commit* *(4.6 und höher)*.</span><span class="sxs-lookup"><span data-stu-id="91a27-169">Repository metadata, consisting of four optional attributes: *type* and *url* *(4.0+)*, and *branch* and *commit* *(4.6+)*.</span></span> <span data-ttu-id="91a27-170">Diese Attribute ermöglichen es Ihnen, der NUPKG-Datei in das Repository zuzuordnen, die sie mit der abzurufenden erstellt entsprechend den Details als einzelne Verzweigung oder Commit, das das Paket erstellt hat.</span><span class="sxs-lookup"><span data-stu-id="91a27-170">These attributes allow you to map the .nupkg to the repository that built it, with the potential to get as detailed as the individual branch or commit that built the package.</span></span> <span data-ttu-id="91a27-171">Dies sollte einer öffentlich zugänglichen Url sein, die direkt von einer Software zur Versionskontrolle aufgerufen werden kann.</span><span class="sxs-lookup"><span data-stu-id="91a27-171">This should be a publicly available url that can be invoked directly by a version control software.</span></span> <span data-ttu-id="91a27-172">Es sollte nicht auf eine html-Seite sein, wie dies für den Computer vorgesehen ist.</span><span class="sxs-lookup"><span data-stu-id="91a27-172">It should not be an html page as this is meant for the computer.</span></span> <span data-ttu-id="91a27-173">Verwenden Sie für das Projekt – Seite verknüpfen, die `projectUrl` Feld stattdessen. |</span><span class="sxs-lookup"><span data-stu-id="91a27-173">For linking to project page, use the `projectUrl` field, instead.|</span></span>

#### <a name="minclientversion"></a><span data-ttu-id="91a27-174">minClientVersion</span><span class="sxs-lookup"><span data-stu-id="91a27-174">minClientVersion</span></span>
<span data-ttu-id="91a27-175">Gibt die minimale Version des NuGet-Clients an, der dieses Paket installieren kann. Dies wird von nuget.exe und dem Paket-Manager von Visual Studio erzwungen.</span><span class="sxs-lookup"><span data-stu-id="91a27-175">Specifies the minimum version of the NuGet client that can install this package, enforced by nuget.exe and the Visual Studio Package Manager.</span></span> <span data-ttu-id="91a27-176">Dieses Attribut wird verwendet, wenn das Paket von bestimmten Funktionen der `.nuspec`-Datei abhängig ist, die in einer bestimmten Version des NuGet-Clients hinzugefügt wurden.</span><span class="sxs-lookup"><span data-stu-id="91a27-176">This is used whenever the package depends on specific features of the `.nuspec` file that were added in a particular version of the NuGet client.</span></span> <span data-ttu-id="91a27-177">Beispielsweise sollte ein Paket, das das `developmentDependency`-Attribut verwendet, „2.8“ für `minClientVersion` angeben.</span><span class="sxs-lookup"><span data-stu-id="91a27-177">For example, a package using the `developmentDependency` attribute should specify "2.8" for `minClientVersion`.</span></span> <span data-ttu-id="91a27-178">Genauso sollte ein Paket, das das `contentFiles`-Element verwendet (vgl. nächster Abschnitt), `minClientVersion` auf „3.3“ festlegen.</span><span class="sxs-lookup"><span data-stu-id="91a27-178">Similarly, a package using the `contentFiles` element (see the next section) should set `minClientVersion` to "3.3".</span></span> <span data-ttu-id="91a27-179">Beachten Sie außerdem, dass NuGet-Clients vor Version 2.5 diese Kennzeichnung nicht erkennen und daher die Installation des Pakets, unabhängig vom Inhalt von `minClientVersion`, *immer* verweigern.</span><span class="sxs-lookup"><span data-stu-id="91a27-179">Note also that because NuGet clients prior to 2.5 do not recognize this flag, they *always* refuse to install the package no matter what `minClientVersion` contains.</span></span>

#### <a name="collection-elements"></a><span data-ttu-id="91a27-180">Auflistungselemente</span><span class="sxs-lookup"><span data-stu-id="91a27-180">Collection elements</span></span>

#### <a name="packagetypes"></a><span data-ttu-id="91a27-181">PackageTypes</span><span class="sxs-lookup"><span data-stu-id="91a27-181">packageTypes</span></span>
<span data-ttu-id="91a27-182">*(3.5 und höher)* Eine Auflistung, die kein `<packageType>`-Element oder mindestens eins enthält und den Pakettyp angibt, wenn es sich nicht um ein gewöhnliches Abhängigkeitspaket handelt.</span><span class="sxs-lookup"><span data-stu-id="91a27-182">*(3.5+)* A collection of zero or more `<packageType>` elements specifying the type of the package if other than a traditional dependency package.</span></span> <span data-ttu-id="91a27-183">Jeder „packageType“ verfügt über Attribute von *name* und *version*.</span><span class="sxs-lookup"><span data-stu-id="91a27-183">Each packageType has attributes of *name* and *version*.</span></span> <span data-ttu-id="91a27-184">Informationen dazu finden Sie unter [Setting a package type (Festlegen eines Pakettypen)](../create-packages/creating-a-package.md#setting-a-package-type).</span><span class="sxs-lookup"><span data-stu-id="91a27-184">See [Setting a package type](../create-packages/creating-a-package.md#setting-a-package-type).</span></span>
#### <a name="dependencies"></a><span data-ttu-id="91a27-185">Abhängigkeiten</span><span class="sxs-lookup"><span data-stu-id="91a27-185">dependencies</span></span>
<span data-ttu-id="91a27-186">Eine Auflistung, die kein `<dependency>`-Element oder mindestens eins enthält und Abhängigkeiten für das Paket angibt.</span><span class="sxs-lookup"><span data-stu-id="91a27-186">A collection of zero or more `<dependency>` elements specifying the dependencies for the package.</span></span> <span data-ttu-id="91a27-187">Jede Abhängigkeit verfügt über Attribute von *id*, *version*, *include* und *exclude* (3.x und höher).</span><span class="sxs-lookup"><span data-stu-id="91a27-187">Each dependency has attributes of *id*, *version*, *include* (3.x+), and *exclude* (3.x+).</span></span> <span data-ttu-id="91a27-188">Informationen dazu finden Sie im Abschnitt [Abhängigkeiten](#dependencies-element).</span><span class="sxs-lookup"><span data-stu-id="91a27-188">See [Dependencies](#dependencies-element) below.</span></span>
#### <a name="frameworkassemblies"></a><span data-ttu-id="91a27-189">frameworkAssemblies</span><span class="sxs-lookup"><span data-stu-id="91a27-189">frameworkAssemblies</span></span>
<span data-ttu-id="91a27-190">*(1.2 und höher)* Eine Auflistung, die kein `<frameworkAssembly>`-Element oder mindestens eins enthält und die für das Paket erforderlichen Verweise auf .NET Framework-Assemblys erkennt und sicherstellt, dass Verweise zu Projekten hinzugefügt werden, die das Paket verarbeiten.</span><span class="sxs-lookup"><span data-stu-id="91a27-190">*(1.2+)* A collection of zero or more `<frameworkAssembly>` elements identifying .NET Framework assembly references that this package requires, which ensures that references are added to projects consuming the package.</span></span> <span data-ttu-id="91a27-191">Jedes frameworkAssembly-Element verfügt über die Attribute *assemblyName* und *targetFramework*.</span><span class="sxs-lookup"><span data-stu-id="91a27-191">Each frameworkAssembly has *assemblyName* and *targetFramework* attributes.</span></span> <span data-ttu-id="91a27-192">Informationen dazu finden Sie unter [Specifying framework assembly references GAC (Angeben von GAC-Verweisen auf Frameworkassemblys)](#specifying-framework-assembly-references-gac).</span><span class="sxs-lookup"><span data-stu-id="91a27-192">See [Specifying framework assembly references GAC](#specifying-framework-assembly-references-gac) below.</span></span> |
#### <a name="references"></a><span data-ttu-id="91a27-193">Referenzen</span><span class="sxs-lookup"><span data-stu-id="91a27-193">references</span></span>
<span data-ttu-id="91a27-194">*(1.5 und höher)* Eine Auflistung, die kein `<reference>`-Element oder mindestens eins enthält, das Assemblys in dem `lib`-Ordner des Pakets benennt, die als Projektverweise hinzugefügt werden.</span><span class="sxs-lookup"><span data-stu-id="91a27-194">*(1.5+)* A collection of zero or more `<reference>` elements naming assemblies in the package's `lib` folder that are added as project references.</span></span> <span data-ttu-id="91a27-195">Jeder Verweis verfügt über ein *file*-Attribut.</span><span class="sxs-lookup"><span data-stu-id="91a27-195">Each reference has a *file* attribute.</span></span> <span data-ttu-id="91a27-196">`<references>` kann außerdem ein `<group>`-Element mit einem *targetFramework*-Attribut enthalten, das anschließend `<reference>`-Elemente enthält.</span><span class="sxs-lookup"><span data-stu-id="91a27-196">`<references>` can also contain a `<group>` element with a *targetFramework* attribute, that then contains `<reference>` elements.</span></span> <span data-ttu-id="91a27-197">Wenn das Element nicht angegeben ist, werden alle Verweise in `lib` eingefügt.</span><span class="sxs-lookup"><span data-stu-id="91a27-197">If omitted, all references in `lib` are included.</span></span> <span data-ttu-id="91a27-198">Informationen dazu finden Sie unter [Specifying explicit assembly references (Angeben von expliziten Assemblyverweisen)](#specifying-explicit-assembly-references).</span><span class="sxs-lookup"><span data-stu-id="91a27-198">See [Specifying explicit assembly references](#specifying-explicit-assembly-references) below.</span></span>
#### <a name="contentfiles"></a><span data-ttu-id="91a27-199">contentFiles</span><span class="sxs-lookup"><span data-stu-id="91a27-199">contentFiles</span></span>
<span data-ttu-id="91a27-200">*(3.3 und höher)* Eine Auflistung von `<files>`-Elementen, die Inhaltsdateien ermitteln, die in das verarbeitende Projekt eingefügt werden sollen.</span><span class="sxs-lookup"><span data-stu-id="91a27-200">*(3.3+)* A collection of `<files>` elements that identify content files to include in the consuming project.</span></span> <span data-ttu-id="91a27-201">Diese Dateien werden zusammen mit mehreren Attributen angegeben, die beschreiben, wie sie in dem Projektsystem verwendet werden sollen.</span><span class="sxs-lookup"><span data-stu-id="91a27-201">These files are specified with a set of attributes that describe how they should be used within the project system.</span></span> <span data-ttu-id="91a27-202">Informationen dazu finden Sie unter [Specifying files to include in the package (Angeben von Dateien, die in das Paket eingefügt werden sollen)](#specifying-files-to-include-in-the-package).</span><span class="sxs-lookup"><span data-stu-id="91a27-202">See [Specifying files to include in the package](#specifying-files-to-include-in-the-package) below.</span></span>
#### <a name="files"></a><span data-ttu-id="91a27-203">Dateien</span><span class="sxs-lookup"><span data-stu-id="91a27-203">files</span></span> 
<span data-ttu-id="91a27-204">Der `<package>`-Knoten enthält möglicherweise einen `<files>`-Knoten, der `<metadata>` gleichgeordnet ist, und bzw. oder eine untergeordnete `<contentFiles>`-Datei unter `<metadata>`, um anzugeben, welche Assembly- und Inhaltsdateien in das Paket eingefügt werden sollen.</span><span class="sxs-lookup"><span data-stu-id="91a27-204">The `<package>` node may contain a `<files>` node as a sibling to `<metadata>`, and a or `<contentFiles>` child under `<metadata>`, to specify which assembly and content files to include in the package.</span></span> <span data-ttu-id="91a27-205">Details dazu finden Sie im Folgenden in den Abschnitten [Einfügen von Assemblydateien](#including-assembly-files) und [Einfügen von Inhaltsdateien](#including-content-files).</span><span class="sxs-lookup"><span data-stu-id="91a27-205">See [Including assembly files](#including-assembly-files) and [Including content files](#including-content-files) later in this topic for details.</span></span>

## <a name="replacement-tokens"></a><span data-ttu-id="91a27-206">Ersetzungstokens</span><span class="sxs-lookup"><span data-stu-id="91a27-206">Replacement tokens</span></span>

<span data-ttu-id="91a27-207">Bei der Erstellung eines Pakets ersetzt der [`nuget pack`-Befehl](../tools/cli-ref-pack.md) durch $ getrennte Tokens im `<metadata>`-Knoten der `.nuspec`-Datei durch Werte, die entweder einer Projektdatei oder dem `-properties`-Schalter des `pack`-Befehls entstammen.</span><span class="sxs-lookup"><span data-stu-id="91a27-207">When creating a package, the [`nuget pack` command](../tools/cli-ref-pack.md) replaces $-delimited tokens in the `.nuspec` file's `<metadata>` node with values that come from either a project file or the `pack` command's `-properties` switch.</span></span>

<span data-ttu-id="91a27-208">Geben Sie in der Befehlszeile die Tokenwerte mit `nuget pack -properties <name>=<value>;<name>=<value>` an.</span><span class="sxs-lookup"><span data-stu-id="91a27-208">On the command line, you specify token values with `nuget pack -properties <name>=<value>;<name>=<value>`.</span></span> <span data-ttu-id="91a27-209">Beispielsweise können Sie ein Token wie `$owners$` und `$desc$` in der `.nuspec`-Datei verwenden und die Werte zur Packzeit wie im Folgenden dargestellt bereitstellen:</span><span class="sxs-lookup"><span data-stu-id="91a27-209">For example, you can use a token such as `$owners$` and `$desc$` in the `.nuspec` and provide the values at packing time as follows:</span></span>

```ps
nuget pack MyProject.csproj -properties
    owners=janedoe,harikm,kimo,xiaop;desc="Awesome app logger utility"
```

<span data-ttu-id="91a27-210">Geben Sie die in der untenstehenden Tabelle beschriebenen Tokens an, um Werte aus einem Projekt zu verwenden (AssemblyInfo verweist auf Dateien wie `AssemblyInfo.cs` oder `AssemblyInfo.vb` in `Properties`).</span><span class="sxs-lookup"><span data-stu-id="91a27-210">To use values from a project, specify the tokens described in the table below (AssemblyInfo refers to the file in `Properties` such as `AssemblyInfo.cs` or `AssemblyInfo.vb`).</span></span>

<span data-ttu-id="91a27-211">Führen Sie anstelle von `.nuspec` nur `nuget pack` in der Projektdatei aus, um diese Tokens zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="91a27-211">To use these tokens, run `nuget pack` with the project file rather than just the `.nuspec`.</span></span> <span data-ttu-id="91a27-212">Beispielsweise werden bei der Verwendung des folgenden Befehls die Tokens `$id$` und `$version$` in einer `.nuspec`-Datei durch die Werte `AssemblyName` und `AssemblyVersion` des Projekts ersetzt:</span><span class="sxs-lookup"><span data-stu-id="91a27-212">For example, when using the following command, the `$id$` and `$version$` tokens in a `.nuspec` file are replaced with the project's `AssemblyName` and `AssemblyVersion` values:</span></span>

```ps
nuget pack MyProject.csproj
```

<span data-ttu-id="91a27-213">In der Regel erstellen Sie `.nuspec` in einem Projekt zuerst mithilfe von `nuget spec MyProject.csproj`, wodurch automatisch einige dieser Standardtokens eingefügt werden.</span><span class="sxs-lookup"><span data-stu-id="91a27-213">Typically, when you have a project, you create the `.nuspec` initially using `nuget spec MyProject.csproj` which automatically includes some of these standard tokens.</span></span> <span data-ttu-id="91a27-214">Wenn in einem Projekt allerdings keine Werte für erforderliche `.nuspec`-Elemente enthalten sind, schlägt `nuget pack` fehl.</span><span class="sxs-lookup"><span data-stu-id="91a27-214">However, if a project lacks values for required `.nuspec` elements, then `nuget pack` fails.</span></span> <span data-ttu-id="91a27-215">Stellen Sie außerdem bei der Änderung von Projektwerten sicher, dass Sie diese neu erstellen, bevor Sie das Paket erstellen. Dies können Sie ganz einfach über den `build`-Paketschalter des Befehls tun.</span><span class="sxs-lookup"><span data-stu-id="91a27-215">Furthermore, if you change project values, be sure to rebuild before creating the package; this can be done conveniently with the pack command's `build` switch.</span></span>

<span data-ttu-id="91a27-216">Mit Ausnahme von `$configuration$` werden Werte in dem Projekt gegenüber Werten bevorzugt, die demselben Token in der Befehlszeile zugeordnet sind.</span><span class="sxs-lookup"><span data-stu-id="91a27-216">With the exception of `$configuration$`, values in the project are used in preference to any assigned to the same token on the command line.</span></span>

| <span data-ttu-id="91a27-217">Token</span><span class="sxs-lookup"><span data-stu-id="91a27-217">Token</span></span> | <span data-ttu-id="91a27-218">Wertquelle</span><span class="sxs-lookup"><span data-stu-id="91a27-218">Value source</span></span> | <span data-ttu-id="91a27-219">Wert</span><span class="sxs-lookup"><span data-stu-id="91a27-219">Value</span></span>
| --- | --- | ---
| <span data-ttu-id="91a27-220">**$id$**</span><span class="sxs-lookup"><span data-stu-id="91a27-220">**$id$**</span></span> | <span data-ttu-id="91a27-221">Projektdatei</span><span class="sxs-lookup"><span data-stu-id="91a27-221">Project file</span></span> | <span data-ttu-id="91a27-222">"AssemblyName" (Titel) aus der Projektdatei</span><span class="sxs-lookup"><span data-stu-id="91a27-222">AssemblyName (title) from the project file</span></span> |
| <span data-ttu-id="91a27-223">**$version$**</span><span class="sxs-lookup"><span data-stu-id="91a27-223">**$version$**</span></span> | <span data-ttu-id="91a27-224">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="91a27-224">AssemblyInfo</span></span> | <span data-ttu-id="91a27-225">„AssemblyInformationalVersion“, falls vorhanden, andernfalls „AssemblyVersion“</span><span class="sxs-lookup"><span data-stu-id="91a27-225">AssemblyInformationalVersion if present, otherwise AssemblyVersion</span></span> |
| <span data-ttu-id="91a27-226">**$author$**</span><span class="sxs-lookup"><span data-stu-id="91a27-226">**$author$**</span></span> | <span data-ttu-id="91a27-227">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="91a27-227">AssemblyInfo</span></span> | <span data-ttu-id="91a27-228">AssemblyCompany</span><span class="sxs-lookup"><span data-stu-id="91a27-228">AssemblyCompany</span></span> |
| <span data-ttu-id="91a27-229">**$title$**</span><span class="sxs-lookup"><span data-stu-id="91a27-229">**$title$**</span></span> | <span data-ttu-id="91a27-230">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="91a27-230">AssemblyInfo</span></span> | <span data-ttu-id="91a27-231">AssemblyTitle</span><span class="sxs-lookup"><span data-stu-id="91a27-231">AssemblyTitle</span></span> |
| <span data-ttu-id="91a27-232">**$description$**</span><span class="sxs-lookup"><span data-stu-id="91a27-232">**$description$**</span></span> | <span data-ttu-id="91a27-233">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="91a27-233">AssemblyInfo</span></span> | <span data-ttu-id="91a27-234">AssemblyDescription</span><span class="sxs-lookup"><span data-stu-id="91a27-234">AssemblyDescription</span></span> |
| <span data-ttu-id="91a27-235">**$copyright$**</span><span class="sxs-lookup"><span data-stu-id="91a27-235">**$copyright$**</span></span> | <span data-ttu-id="91a27-236">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="91a27-236">AssemblyInfo</span></span> | <span data-ttu-id="91a27-237">AssemblyCopyright</span><span class="sxs-lookup"><span data-stu-id="91a27-237">AssemblyCopyright</span></span> |
| <span data-ttu-id="91a27-238">**$configuration$**</span><span class="sxs-lookup"><span data-stu-id="91a27-238">**$configuration$**</span></span> | <span data-ttu-id="91a27-239">Assembly-DLL</span><span class="sxs-lookup"><span data-stu-id="91a27-239">Assembly DLL</span></span> | <span data-ttu-id="91a27-240">Konfiguration, die zur Erstellung der Assembly verwendet wird und standardmäßig auf „Debuggen“ festgelegt ist.</span><span class="sxs-lookup"><span data-stu-id="91a27-240">Configuration used to build the assembly, defaulting to Debug.</span></span> <span data-ttu-id="91a27-241">Achten Sie darauf, dass Sie stets `-properties Configuration=Release` in der Befehlszeile verwenden, um mithilfe einer Releasekonfiguration ein Paket zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="91a27-241">Note that to create a package using a Release configuration, you always use `-properties Configuration=Release` on the command line.</span></span> |

<span data-ttu-id="91a27-242">Tokens können auch zum Auflösen von Pfaden verwendet werden, wenn Sie [Assemblydateien](#including-assembly-files) und [Inhaltsdateien](#including-content-files) hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="91a27-242">Tokens can also be used to resolve paths when you include [assembly files](#including-assembly-files) and [content files](#including-content-files).</span></span> <span data-ttu-id="91a27-243">Die Namen der Tokens und der MSBuild-Eigenschaften stimmen miteinander überein, wodurch Sie abhängig von der aktuellen Buildkonfiguration Dateien auswählen können, die eingefügt werden sollen.</span><span class="sxs-lookup"><span data-stu-id="91a27-243">The tokens have the same names as the MSBuild properties, making it possible to select files to be included depending on the current build configuration.</span></span> <span data-ttu-id="91a27-244">Wenn Sie beispielsweise die folgenden Tokens in der `.nuspec`-Datei verwenden</span><span class="sxs-lookup"><span data-stu-id="91a27-244">For example, if you use the following tokens in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="bin\$configuration$\$id$.pdb" target="lib\net40" />
</files>
```

<span data-ttu-id="91a27-245">und Sie eine Assembly mit der `Release`-Konfiguration in MSBuild erstellen, deren `AssemblyName` `LoggingLibrary` ist, sehen die dadurch entstandenen Zeilen in der `.nuspec`-Datei in den Paketen wie folgt aus:</span><span class="sxs-lookup"><span data-stu-id="91a27-245">And you build an assembly whose `AssemblyName` is `LoggingLibrary` with the `Release` configuration in MSBuild, the resulting lines in the `.nuspec` file in the package is as follows:</span></span>

```xml
<files>
    <file src="bin\Release\LoggingLibrary.pdb" target="lib\net40" />
</files>
```

## <a name="dependencies-element"></a><span data-ttu-id="91a27-246">Abhängigkeitselement</span><span class="sxs-lookup"><span data-stu-id="91a27-246">Dependencies element</span></span>

<span data-ttu-id="91a27-247">Das `<dependencies>`-Element in `<metadata>` enthält eine beliebige Anzahl von `<dependency>`-Elementen, die andere Pakete finden, von denen die Pakete auf der obersten Ebene abhängig sind.</span><span class="sxs-lookup"><span data-stu-id="91a27-247">The `<dependencies>` element within `<metadata>` contains any number of `<dependency>` elements that identify other packages upon which the top-level package depends.</span></span> <span data-ttu-id="91a27-248">Im Folgenden werden die Attribute für jede `<dependency>` dargestellt:</span><span class="sxs-lookup"><span data-stu-id="91a27-248">The attributes for each `<dependency>` are as follows:</span></span>

| <span data-ttu-id="91a27-249">Attribut</span><span class="sxs-lookup"><span data-stu-id="91a27-249">Attribute</span></span> | <span data-ttu-id="91a27-250">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="91a27-250">Description</span></span> |
| --- | --- |
| `id` | <span data-ttu-id="91a27-251">(Erforderlich) Die Paket-ID der Abhängigkeit, z.B. „EntityFramework“ und „NUnit“, die der Name des Pakets „nuget.org“ ist, wird auf einer Paketseite angezeigt.</span><span class="sxs-lookup"><span data-stu-id="91a27-251">(Required) The package ID of the dependency, such as "EntityFramework" and "NUnit", which is the name of the package nuget.org shows on a package page.</span></span> |
| `version` | <span data-ttu-id="91a27-252">(Erforderlich) Der Bereich an Versionen, die als Abhängigkeiten akzeptiert werden.</span><span class="sxs-lookup"><span data-stu-id="91a27-252">(Required) The range of versions acceptable as a dependency.</span></span> <span data-ttu-id="91a27-253">Die genaue Syntax finden Sie unter [Paketversionsverwaltung](../reference/package-versioning.md#version-ranges-and-wildcards).</span><span class="sxs-lookup"><span data-stu-id="91a27-253">See [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards) for exact syntax.</span></span> |
| <span data-ttu-id="91a27-254">include</span><span class="sxs-lookup"><span data-stu-id="91a27-254">include</span></span> | <span data-ttu-id="91a27-255">Eine durch Kommas abgetrennte Liste mit Include/Exclude-Tags (s. Tabelle unten), in der auf die Abhängigkeit verwiesen wird, die in das endgültige Paket eingefügt werden soll.</span><span class="sxs-lookup"><span data-stu-id="91a27-255">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to include in the final package.</span></span> <span data-ttu-id="91a27-256">Der Standardwert ist `none`.</span><span class="sxs-lookup"><span data-stu-id="91a27-256">The default value is `none`.</span></span> |
| <span data-ttu-id="91a27-257">exclude</span><span class="sxs-lookup"><span data-stu-id="91a27-257">exclude</span></span> | <span data-ttu-id="91a27-258">Eine durch Kommas abgetrennte Liste mit Include/Exclude-Tags (s. Tabelle unten), in der auf die Abhängigkeit verwiesen wird, die nicht in das endgültige Paket eingefügt werden soll.</span><span class="sxs-lookup"><span data-stu-id="91a27-258">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to exclude in the final package.</span></span> <span data-ttu-id="91a27-259">Der Standardwert ist `all`.</span><span class="sxs-lookup"><span data-stu-id="91a27-259">The  default value is `all`.</span></span> <span data-ttu-id="91a27-260">`exclude`-Tags haben Vorrang gegenüber `include`-Tags.</span><span class="sxs-lookup"><span data-stu-id="91a27-260">Tags specified with `exclude` take precedence over those specified with `include`.</span></span> <span data-ttu-id="91a27-261">Beispielsweise entspricht `include="runtime, compile" exclude="compile"` `include="runtime"`.</span><span class="sxs-lookup"><span data-stu-id="91a27-261">For example, `include="runtime, compile" exclude="compile"` is the same as `include="runtime"`.</span></span> |

| <span data-ttu-id="91a27-262">Include/Exclude-Tag</span><span class="sxs-lookup"><span data-stu-id="91a27-262">Include/Exclude tag</span></span> | <span data-ttu-id="91a27-263">Betroffene Ordner im Ziel</span><span class="sxs-lookup"><span data-stu-id="91a27-263">Affected folders of the target</span></span> |
| --- | --- |
| <span data-ttu-id="91a27-264">contentFiles</span><span class="sxs-lookup"><span data-stu-id="91a27-264">contentFiles</span></span> | <span data-ttu-id="91a27-265">Inhalt</span><span class="sxs-lookup"><span data-stu-id="91a27-265">Content</span></span> |
| <span data-ttu-id="91a27-266">Laufzeit</span><span class="sxs-lookup"><span data-stu-id="91a27-266">runtime</span></span> | <span data-ttu-id="91a27-267">Runtime, Ressourcen und Frameworkassemblys</span><span class="sxs-lookup"><span data-stu-id="91a27-267">Runtime, Resources, and FrameworkAssemblies</span></span> |
| <span data-ttu-id="91a27-268">compile</span><span class="sxs-lookup"><span data-stu-id="91a27-268">compile</span></span> | <span data-ttu-id="91a27-269">lib</span><span class="sxs-lookup"><span data-stu-id="91a27-269">lib</span></span> |
| <span data-ttu-id="91a27-270">Build</span><span class="sxs-lookup"><span data-stu-id="91a27-270">build</span></span> | <span data-ttu-id="91a27-271">Build (MSBuild-Eigenschaften und -Ziele)</span><span class="sxs-lookup"><span data-stu-id="91a27-271">build (MSBuild props and targets)</span></span> |
| <span data-ttu-id="91a27-272">Systemeigen</span><span class="sxs-lookup"><span data-stu-id="91a27-272">native</span></span> | <span data-ttu-id="91a27-273">Systemeigen</span><span class="sxs-lookup"><span data-stu-id="91a27-273">native</span></span> |
| <span data-ttu-id="91a27-274">Keine</span><span class="sxs-lookup"><span data-stu-id="91a27-274">none</span></span> | <span data-ttu-id="91a27-275">Keine Ordner</span><span class="sxs-lookup"><span data-stu-id="91a27-275">No folders</span></span> |
| <span data-ttu-id="91a27-276">alle</span><span class="sxs-lookup"><span data-stu-id="91a27-276">all</span></span> | <span data-ttu-id="91a27-277">Alle Ordner</span><span class="sxs-lookup"><span data-stu-id="91a27-277">All folders</span></span> |

<span data-ttu-id="91a27-278">Beispielsweise verweisen die folgenden Zeilen auf Abhängigkeiten auf `PackageA` Version 1.1.0 und höher und `PackageB` Version 1.x.</span><span class="sxs-lookup"><span data-stu-id="91a27-278">For example, the following lines indicate dependencies on `PackageA` version 1.1.0 or higher, and `PackageB` version 1.x.</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" />
    <dependency id="PackageB" version="[1,2)" />
</dependencies>
```

<span data-ttu-id="91a27-279">In den folgenden Zeilen wird zwar auf Abhängigkeiten von denselben Paketen verwiesen, allerdings wird auch angegeben, dass die Ordner `contentFiles` und `build` von `PackageA` sowie alle anderen Ordner bis auf `native` und `compile` von `PackageB` angegeben werden sollen.</span><span class="sxs-lookup"><span data-stu-id="91a27-279">The following lines indicate dependencies on the same packages, but specify to include the `contentFiles` and `build` folders of `PackageA` and everything but the `native` and `compile` folders of `PackageB`"</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" include="contentFiles, build" />
    <dependency id="PackageB" version="[1,2)" exclude="native, compile" />
</dependencies>
```

<span data-ttu-id="91a27-280">Hinweis: Bei der Erstellung von `.nuspec` mithilfe von `nuget spec` aus einem Projekt werden in diesem Projekt bestehende Abhängigkeiten automatisch in die resultierende `.nuspec`-Datei eingefügt.</span><span class="sxs-lookup"><span data-stu-id="91a27-280">Note: When creating a `.nuspec` from a project using `nuget spec`, dependencies that exist in that project are automatically included in the resulting `.nuspec` file.</span></span>

### <a name="dependency-groups"></a><span data-ttu-id="91a27-281">Abhängigkeitsgruppen</span><span class="sxs-lookup"><span data-stu-id="91a27-281">Dependency groups</span></span>

<span data-ttu-id="91a27-282">*Version 2.0 und höher*</span><span class="sxs-lookup"><span data-stu-id="91a27-282">*Version 2.0+*</span></span>

<span data-ttu-id="91a27-283">Als Alternative zu einer einzelnen flachen Liste können Abhängigkeiten auf der Grundlage des Frameworkprofils des Zielprojekts angegeben werden, das `<group>`-Elemente in `<dependencies>` verwendet.</span><span class="sxs-lookup"><span data-stu-id="91a27-283">As an alternative to a single flat list, dependencies can be specified according to the framework profile of the target project using `<group>` elements within `<dependencies>`.</span></span>

<span data-ttu-id="91a27-284">Jede Gruppe verfügt über ein Attribut mit dem Namen `targetFramework` und enthält entweder kein `<dependency>`-Element oder mindestens eins.</span><span class="sxs-lookup"><span data-stu-id="91a27-284">Each group has an attribute named `targetFramework` and contains zero or more `<dependency>` elements.</span></span> <span data-ttu-id="91a27-285">Diese Abhängigkeiten werden zusammen installiert, wenn das Zielframework kompatibel mit dem Frameworkprofil des Projekts ist.</span><span class="sxs-lookup"><span data-stu-id="91a27-285">Those dependencies are installed together when  the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="91a27-286">Das `<group>`-Element ohne ein `targetFramework`-Attribut wird als Standard- oder Ausweichliste der Abhängigkeiten verwendet.</span><span class="sxs-lookup"><span data-stu-id="91a27-286">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of dependencies.</span></span> <span data-ttu-id="91a27-287">Die genauen Frameworkbezeichner finden Sie unter [Zielframeworks](../reference/target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="91a27-287">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="91a27-288">Das Gruppenformat kann nicht mit einer flachen Liste vermischt werden.</span><span class="sxs-lookup"><span data-stu-id="91a27-288">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="91a27-289">Im folgenden Beispiel werden verschiedene Variationen des `<group>`-Elements dargestellt:</span><span class="sxs-lookup"><span data-stu-id="91a27-289">The following example shows different variations of the `<group>` element:</span></span>

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

## <a name="explicit-assembly-references"></a><span data-ttu-id="91a27-290">Explizite Assemblyverweise</span><span class="sxs-lookup"><span data-stu-id="91a27-290">Explicit assembly references</span></span>

<span data-ttu-id="91a27-291">Das `<references>`-Element gibt die genauen Assemblyverweise an, auf die das Zielprojekt bei der Verwendung des Pakets verweisen soll.</span><span class="sxs-lookup"><span data-stu-id="91a27-291">The `<references>` element explicitly specifies the assemblies that the target project should reference when using the package.</span></span> <span data-ttu-id="91a27-292">Wenn dieses Element vorhanden ist, fügt NuGet nur Verweise zu den aufgelisteten Assemblys hinzu. Es werden keine Verweise auf andere Assemblys in dem `lib`-Ordner des Pakets hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="91a27-292">When this element is present, NuGet add references to only the listed assemblies; it does not add references for any other assemblies in the package's `lib` folder.</span></span>

<span data-ttu-id="91a27-293">Beispielsweise gibt das folgende `<references>`-Element NuGet die Anweisung, Verweise nur zu `xunit.dll` und `xunit.extensions.dll` hinzuzufügen, wenn zusätzliche Assemblys in dem Paket enthalten sind:</span><span class="sxs-lookup"><span data-stu-id="91a27-293">For example, the following `<references>` element instructs NuGet to add references to only `xunit.dll` and `xunit.extensions.dll` even if there are additional assemblies in the package:</span></span>

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

<span data-ttu-id="91a27-294">In der Regel werden Verweise nur für Assemblys zur Entwurfszeit verwendet.</span><span class="sxs-lookup"><span data-stu-id="91a27-294">Explicit references are typically used for design-time only assemblies.</span></span> <span data-ttu-id="91a27-295">Beispielsweise müssen sich Vertragsassemblys bei der Verwendung von [Codeverträgen](/dotnet/framework/debug-trace-profile/code-contracts) neben den Runtimeassemblys befinden, die sie erweitern, damit Visual Studio sie finden kann. Allerdings muss das Projekt auf die Vertragsassemblys verweisen oder in den `bin`-Ordner des Projekts kopiert werden.</span><span class="sxs-lookup"><span data-stu-id="91a27-295">When using [Code Contracts](/dotnet/framework/debug-trace-profile/code-contracts), for example, contract assemblies need to be next to the runtime assemblies that they augment so that Visual Studio can find them, but the contract assemblies need not be referenced by the project or copied into the project's `bin` folder.</span></span>

<span data-ttu-id="91a27-296">Genauso können explizite Verweise für Komponententestframeworks wie XUnit verwendet werden, in denen sich zwar die Toolsassemblys neben den Runtimeassemblys befinden müssen, jedoch müssen diese nicht als Projektverweise eingefügt werden.</span><span class="sxs-lookup"><span data-stu-id="91a27-296">Similarly, explicit references can be used for unit test frameworks, such as XUnit, which needs its tools assemblies located next to the runtime assemblies, but does not need them included as project references.</span></span>

### <a name="reference-groups"></a><span data-ttu-id="91a27-297">Verweisgruppen</span><span class="sxs-lookup"><span data-stu-id="91a27-297">Reference groups</span></span>

<span data-ttu-id="91a27-298">Als Alternative zu einer einzelnen flachen Liste können Verweise auf der Grundlage des Frameworkprofils des Zielprojekts angegeben werden, das `<group>`-Elemente in `<references>` verwendet.</span><span class="sxs-lookup"><span data-stu-id="91a27-298">As an alternative to a single flat list, references can be specified according to the framework profile of the target project using `<group>` elements within `<references>`.</span></span>

<span data-ttu-id="91a27-299">Jede Gruppe verfügt über ein Attribut mit dem Namen `targetFramework` und enthält entweder kein `<reference>`-Element oder mindestens eins.</span><span class="sxs-lookup"><span data-stu-id="91a27-299">Each group has an attribute named `targetFramework` and contains zero or more `<reference>` elements.</span></span> <span data-ttu-id="91a27-300">Diese Verweise werden einem Projekt hinzugefügt, wenn das Zielframework mit dem Frameworkprofil des Projekts kompatibel ist.</span><span class="sxs-lookup"><span data-stu-id="91a27-300">Those references are added to a project when the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="91a27-301">Das `<group>`-Element ohne ein `targetFramework`-Attribut wird als Standard- oder Ausweichliste der Verweise verwendet.</span><span class="sxs-lookup"><span data-stu-id="91a27-301">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of references.</span></span> <span data-ttu-id="91a27-302">Die genauen Frameworkbezeichner finden Sie unter [Zielframeworks](../reference/target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="91a27-302">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="91a27-303">Das Gruppenformat kann nicht mit einer flachen Liste vermischt werden.</span><span class="sxs-lookup"><span data-stu-id="91a27-303">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="91a27-304">Im folgenden Beispiel werden verschiedene Variationen des `<group>`-Elements dargestellt:</span><span class="sxs-lookup"><span data-stu-id="91a27-304">The following example shows different variations of the `<group>` element:</span></span>

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

## <a name="framework-assembly-references"></a><span data-ttu-id="91a27-305">Verweise auf Frameworkassemblys</span><span class="sxs-lookup"><span data-stu-id="91a27-305">Framework assembly references</span></span>

<span data-ttu-id="91a27-306">Frameworkassemblys gehören zum .NET Framework und sollten für jeden vorhandenen Computer bereits im globalen Assemblycache vorhanden sein.</span><span class="sxs-lookup"><span data-stu-id="91a27-306">Framework assemblies are those that are part of the .NET framework and should already be in the global assembly cache (GAC) for any given machine.</span></span> <span data-ttu-id="91a27-307">Pakete können sicherstellen, dass die erforderlichen Verweise, falls nötig, dem Projekt hinzugefügt werden, indem es diese Assemblys im `<frameworkAssemblies>`-Element erkennt.</span><span class="sxs-lookup"><span data-stu-id="91a27-307">By identifying those assemblies within the `<frameworkAssemblies>` element, a package can ensure that required references are added to a project in the event that the project doesn't have such references already.</span></span> <span data-ttu-id="91a27-308">Solche Assemblys sind nicht von Anfang an in Paketen enthalten.</span><span class="sxs-lookup"><span data-stu-id="91a27-308">Such assemblies, of course, are not included in a package directly.</span></span>

<span data-ttu-id="91a27-309">Das `<frameworkAssemblies>`-Element enthält entweder kein `<frameworkAssembly>`-Element oder mindestens eins, das die folgenden Attribute angibt:</span><span class="sxs-lookup"><span data-stu-id="91a27-309">The `<frameworkAssemblies>` element contains zero or more `<frameworkAssembly>` elements, each of which specifies the following attributes:</span></span>

| <span data-ttu-id="91a27-310">Attribut</span><span class="sxs-lookup"><span data-stu-id="91a27-310">Attribute</span></span> | <span data-ttu-id="91a27-311">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="91a27-311">Description</span></span> |
| --- | --- |
| <span data-ttu-id="91a27-312">**assemblyName**</span><span class="sxs-lookup"><span data-stu-id="91a27-312">**assemblyName**</span></span> | <span data-ttu-id="91a27-313">(Erforderlich) Der vollqualifizierte Assemblyname.</span><span class="sxs-lookup"><span data-stu-id="91a27-313">(Required) The fully qualified assembly name.</span></span> |
| <span data-ttu-id="91a27-314">**targetFramework**</span><span class="sxs-lookup"><span data-stu-id="91a27-314">**targetFramework**</span></span> | <span data-ttu-id="91a27-315">(Optional) Gibt das Zielframework an, auf das sich dieser Verweis bezieht.</span><span class="sxs-lookup"><span data-stu-id="91a27-315">(Optional) Specifies the target framework to which this reference applies.</span></span> <span data-ttu-id="91a27-316">Wenn dieses Attribut nicht vorhanden ist, deutet dies darauf hin, dass sich der Verweis auf alle Frameworks bezieht.</span><span class="sxs-lookup"><span data-stu-id="91a27-316">If omitted, indicates that the reference applies to all frameworks.</span></span> <span data-ttu-id="91a27-317">Die genauen Frameworkbezeichner finden Sie unter [Zielframeworks](../reference/target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="91a27-317">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span> |

<span data-ttu-id="91a27-318">Im folgenden Beispiel werden Verweise auf `System.Net` für alle Zielframeworks und auf `System.ServiceModel` für ausschließlich .NET Framework 4.0 dargestellt:</span><span class="sxs-lookup"><span data-stu-id="91a27-318">The following example shows a reference to `System.Net` for all target frameworks, and a reference to `System.ServiceModel` for .NET Framework 4.0 only:</span></span>

```xml
<frameworkAssemblies>
    <frameworkAssembly assemblyName="System.Net"  />

    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
</frameworkAssemblies>
```

<a name="specifying-files-to-include-in-the-package"></a>

## <a name="including-assembly-files"></a><span data-ttu-id="91a27-319">Einfügen von Assemblydateien</span><span class="sxs-lookup"><span data-stu-id="91a27-319">Including assembly files</span></span>

<span data-ttu-id="91a27-320">Wenn Sie die unter [Creating a Package (Erstellen eines Pakets)](../create-packages/creating-a-package.md) beschriebenen Anweisungen ausführen, müssen Sie nicht explizit eine Liste mit Dateien in der `.nuspec`-Datei angeben.</span><span class="sxs-lookup"><span data-stu-id="91a27-320">If you follow the conventions described in [Creating a Package](../create-packages/creating-a-package.md), you do not have to explicitly specify a list of files in the `.nuspec` file.</span></span> <span data-ttu-id="91a27-321">Der `nuget pack`-Befehl ruft die benötigten Dateien automatisch ab.</span><span class="sxs-lookup"><span data-stu-id="91a27-321">The `nuget pack` command automatically picks up the necessary files.</span></span>

> [!Important]
> <span data-ttu-id="91a27-322">Wenn ein Paket in einem Projekt installiert wird, fügt NuGet automatisch der DLL des Pakets Assemblyverweise hinzu. Die Verweise, die mit `.resources.dll` benannt sind werden dabei allerdings *nicht* hinzugefügt, da angenommen wird, dass es sich dabei um lokalisierte Satellitenassemblys handelt.</span><span class="sxs-lookup"><span data-stu-id="91a27-322">When a package is installed into a project, NuGet automatically adds assembly references to the package's DLLs, *excluding* those that are named `.resources.dll` because they are assumed to be localized satellite assemblies.</span></span> <span data-ttu-id="91a27-323">Vermeiden Sie aus diesem Grund die Verwendung von `.resources.dll` für Dateien, die darüber hinaus wichtigen Paketcode enthalten.</span><span class="sxs-lookup"><span data-stu-id="91a27-323">For this reason, avoid using `.resources.dll` for files that otherwise contain essential package code.</span></span>

<span data-ttu-id="91a27-324">Legen Sie ein `<files>`-Element als untergeordnetes Element von `<package>` und als gleichgeordnetes Element von `<metadata>` fest, das jeder Datei ein separates `<file>`-Element zuordnet, um diese automatischen Vorgänge zu umgehen und genau zu kontrollieren, welche Dateien in einem Paket enthalten sind.</span><span class="sxs-lookup"><span data-stu-id="91a27-324">To bypass this automatic behavior and explicitly control which files are included in a package, place a `<files>` element as a child of `<package>` (and a sibling of `<metadata>`), identifying each file with a separate `<file>` element.</span></span> <span data-ttu-id="91a27-325">Zum Beispiel:</span><span class="sxs-lookup"><span data-stu-id="91a27-325">For example:</span></span>

```xml
<files>
    <file src="bin\Debug\*.dll" target="lib" />
    <file src="bin\Debug\*.pdb" target="lib" />
    <file src="tools\**\*.*" exclude="**\*.log" />
</files>
```

<span data-ttu-id="91a27-326">Das `<files>`-Element wird bei NuGet 2.x und früher sowie bei Projekten, die `packages.config` verwenden, außerdem verwendet, um unveränderliche Inhaltsdateien während der Paketinstallation einzufügen.</span><span class="sxs-lookup"><span data-stu-id="91a27-326">With NuGet 2.x and earlier, and projects using `packages.config`, the `<files>` element is also used to include immutable content files when a package is installed.</span></span> <span data-ttu-id="91a27-327">Bei NuGet 3.3 und höher und Projekten, die PackageReference verwenden, wird stattdessen das `<contentFiles>`-Element verwendet.</span><span class="sxs-lookup"><span data-stu-id="91a27-327">With NuGet 3.3+ and projects PackageReference, the `<contentFiles>` element is used instead.</span></span> <span data-ttu-id="91a27-328">Weitere Informationen finden Sie unter [Einfügen von Inhaltsdateien](#including-content-files).</span><span class="sxs-lookup"><span data-stu-id="91a27-328">See [Including content files](#including-content-files) below for details.</span></span>

### <a name="file-element-attributes"></a><span data-ttu-id="91a27-329">Dateielementattribute</span><span class="sxs-lookup"><span data-stu-id="91a27-329">File element attributes</span></span>

<span data-ttu-id="91a27-330">Jedes `<file>`-Element gibt die folgenden Attribute an:</span><span class="sxs-lookup"><span data-stu-id="91a27-330">Each `<file>` element specifies the following attributes:</span></span>

| <span data-ttu-id="91a27-331">Attribut</span><span class="sxs-lookup"><span data-stu-id="91a27-331">Attribute</span></span> | <span data-ttu-id="91a27-332">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="91a27-332">Description</span></span> |
| --- | --- |
| <span data-ttu-id="91a27-333">**src**</span><span class="sxs-lookup"><span data-stu-id="91a27-333">**src**</span></span> | <span data-ttu-id="91a27-334">Der Speicherort der Dateien, die eingefügt werden sollen, unterliegt Ausnahmen, die von dem `exclude`-Attribut angegeben werden.</span><span class="sxs-lookup"><span data-stu-id="91a27-334">The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="91a27-335">Der Pfad ist relativ zur `.nuspec`-Datei, wenn kein absoluter Pfad angegeben ist.</span><span class="sxs-lookup"><span data-stu-id="91a27-335">The path is relative to the `.nuspec` file unless an absolute path is specified.</span></span> <span data-ttu-id="91a27-336">Das Platzhalterzeichen `*` ist zulässig, und das zweifache Platzhalterzeichen `**` impliziert eine rekursive Ordnersuche.</span><span class="sxs-lookup"><span data-stu-id="91a27-336">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="91a27-337">**target**</span><span class="sxs-lookup"><span data-stu-id="91a27-337">**target**</span></span> | <span data-ttu-id="91a27-338">Der relative Pfad zu dem Ordner in dem Paket, in dem die Quelldateien platziert sind, der mit `lib`, `content`, `build` oder `tools` beginnt.</span><span class="sxs-lookup"><span data-stu-id="91a27-338">The relative path to the folder within the package where the source files are placed, which must begin with `lib`, `content`, `build`, or `tools`.</span></span> <span data-ttu-id="91a27-339">Informationen dazu finden Sie unter [Creating a .nuspec from a convention-based working directory (Erstellen einer NUSPEC-Datei aus einem auf Konventionen basierenden Arbeitsverzeichnis)](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span><span class="sxs-lookup"><span data-stu-id="91a27-339">See [Creating a .nuspec from a convention-based working directory](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span></span> |
| <span data-ttu-id="91a27-340">**exclude**</span><span class="sxs-lookup"><span data-stu-id="91a27-340">**exclude**</span></span> | <span data-ttu-id="91a27-341">Eine durch Semikolons abgetrennte Datei oder Dateimuster, die sich nicht im `src`-Speicherort befinden dürfen.</span><span class="sxs-lookup"><span data-stu-id="91a27-341">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="91a27-342">Das Platzhalterzeichen `*` ist zulässig, und das zweifache Platzhalterzeichen `**` impliziert eine rekursive Ordnersuche.</span><span class="sxs-lookup"><span data-stu-id="91a27-342">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |

### <a name="examples"></a><span data-ttu-id="91a27-343">Beispiele</span><span class="sxs-lookup"><span data-stu-id="91a27-343">Examples</span></span>

<span data-ttu-id="91a27-344">**Einzelne Assembly**</span><span class="sxs-lookup"><span data-stu-id="91a27-344">**Single assembly**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="library.dll" target="lib" />

    Packaged result:
        lib\library.dll

<span data-ttu-id="91a27-345">**Einzelne Assembly, die für ein Zielframework spezifisch ist**</span><span class="sxs-lookup"><span data-stu-id="91a27-345">**Single assembly specific to a target framework**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="assemblies\net40\library.dll" target="lib\net40" />

    Packaged result:
        lib\net40\library.dll

<span data-ttu-id="91a27-346">**Mehrere DLLS, die Platzhalterzeichen verwenden**</span><span class="sxs-lookup"><span data-stu-id="91a27-346">**Set of DLLs using a wildcard**</span></span>

    Source files:
        bin\release\libraryA.dll
        bin\release\libraryB.dll

    .nuspec entry:
        <file src="bin\release\*.dll" target="lib" />

    Packaged result:
        lib\libraryA.dll
        lib\libraryB.dll

<span data-ttu-id="91a27-347">**DLLs für verschiedene Frameworks**</span><span class="sxs-lookup"><span data-stu-id="91a27-347">**DLLs for different frameworks**</span></span>

    Source files:
        lib\net40\library.dll
        lib\net20\library.dll

    .nuspec entry (using ** recursive search):
        <file src="lib\**" target="lib" />

    Packaged result:
        lib\net40\library.dll
        lib\net20\library.dll

<span data-ttu-id="91a27-348">**Ausschließen von Dateien**</span><span class="sxs-lookup"><span data-stu-id="91a27-348">**Excluding files**</span></span>

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

## <a name="including-content-files"></a><span data-ttu-id="91a27-349">Einfügen von Inhaltsdateien</span><span class="sxs-lookup"><span data-stu-id="91a27-349">Including content files</span></span>

<span data-ttu-id="91a27-350">Bei Inhaltsdateien handelt es sich um unveränderliche Dateien, die ein Paket in ein Projekt einfügen muss.</span><span class="sxs-lookup"><span data-stu-id="91a27-350">Content files are immutable files that a package needs to include in a project.</span></span> <span data-ttu-id="91a27-351">Da sie unveränderlich sind, sollen sie auch nicht von dem verarbeitenden Projekt geändert werden.</span><span class="sxs-lookup"><span data-stu-id="91a27-351">Being immutable, they are not intended to be modified by the consuming project.</span></span> <span data-ttu-id="91a27-352">Zu den Inhaltsdateien gehören z.B.:</span><span class="sxs-lookup"><span data-stu-id="91a27-352">Example content files include:</span></span>

- <span data-ttu-id="91a27-353">Bilder, die als Ressourcen eingebettet werden</span><span class="sxs-lookup"><span data-stu-id="91a27-353">Images that are embedded as resources</span></span>
- <span data-ttu-id="91a27-354">Quelldateien, die bereits kompiliert sind</span><span class="sxs-lookup"><span data-stu-id="91a27-354">Source files that are already compiled</span></span>
- <span data-ttu-id="91a27-355">Skripts, die in die Buildausgabe des Projekts eingefügt werden müssen</span><span class="sxs-lookup"><span data-stu-id="91a27-355">Scripts that need to be included with the build output of the project</span></span>
- <span data-ttu-id="91a27-356">Konfigurationsdateien für das Paket, die zwar in das Projekt eingefügt werden müssen, an denen jedoch keine projektspezifischen Änderungen vorgenommen werden müssen.</span><span class="sxs-lookup"><span data-stu-id="91a27-356">Configuration files for the package that need to be included in the project but don't need any project-specific changes</span></span>

<span data-ttu-id="91a27-357">Inhaltsdateien werden in ein Paket eingefügt, das das `<files>`-Element verwendet, das den `content`-Ordner im `target`-Attribut angibt.</span><span class="sxs-lookup"><span data-stu-id="91a27-357">Content files are included in a package using the `<files>` element, specifying the `content` folder in the `target` attribute.</span></span> <span data-ttu-id="91a27-358">Allerdings werden diese Dateien ignoriert, wenn das Paket über PackageReference in ein Projekt installiert wird, das stattdessen das `<contentFiles>`-Element verwendet.</span><span class="sxs-lookup"><span data-stu-id="91a27-358">However, such files are ignored when the package is installed in a project using PackageReference, which instead uses the `<contentFiles>` element.</span></span>

<span data-ttu-id="91a27-359">Im Idealfall geben Pakete die Inhaltsdateien in beiden Elementen an, um ein höchstmögliches Maß an Kompatibilität mit den verarbeitenden Projekten zu erreichen.</span><span class="sxs-lookup"><span data-stu-id="91a27-359">For maximum compatibility with consuming projects, a package ideally specifies the content files in both elements.</span></span>

### <a name="using-the-files-element-for-content-files"></a><span data-ttu-id="91a27-360">Verwenden des Dateielements für Inhaltsdateien</span><span class="sxs-lookup"><span data-stu-id="91a27-360">Using the files element for content files</span></span>

<span data-ttu-id="91a27-361">Verwenden Sie für Inhaltsdateien einfach dasselbe Format wie für Assemblydateien. Geben Sie dabei allerdings `content` als Basisordner im `target`-Attribut an, wie in den folgenden Beispielen dargestellt wird.</span><span class="sxs-lookup"><span data-stu-id="91a27-361">For content files, simply use the same format as for assembly files, but specify `content` as the base folder in the `target` attribute as shown in the following examples.</span></span>

<span data-ttu-id="91a27-362">**Grundlegende Inhaltsdateien**</span><span class="sxs-lookup"><span data-stu-id="91a27-362">**Basic content files**</span></span>

    Source files:
        css\mobile\style1.css
        css\mobile\style2.css

    .nuspec entry:
        <file src="css\mobile\*.css" target="content\css\mobile" />

    Packaged result:
        content\css\mobile\style1.css
        content\css\mobile\style2.css

<span data-ttu-id="91a27-363">**Inhaltsdateien mit Verzeichnisstruktur**</span><span class="sxs-lookup"><span data-stu-id="91a27-363">**Content files with directory structure**</span></span>

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

<span data-ttu-id="91a27-364">**Inhaltsdatei, die für ein Zielframework spezifisch ist**</span><span class="sxs-lookup"><span data-stu-id="91a27-364">**Content file specific to a target framework**</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry
        <file src="css\cool\style.css" target="Content" />

    Packaged result:
        content\style.css

<span data-ttu-id="91a27-365">**Inhaltsdatei, die in einen Ordner mit einem Punkt im Namen kopiert wird**</span><span class="sxs-lookup"><span data-stu-id="91a27-365">**Content file copied to a folder with dot in name**</span></span>

<span data-ttu-id="91a27-366">In diesem Fall erkennt NuGet, dass die Erweiterung in `target` nicht mit der Erweiterung in `src` übereinstimmt, und behandelt dieses Bestandteil des Namens in `target` als einen Ordner:</span><span class="sxs-lookup"><span data-stu-id="91a27-366">In this case, NuGet sees that the extension in `target` does not match the extension in `src` and thus treats that part of the name in `target` as a folder:</span></span>

    Source file:
        images\picture.png

    .nuspec entry:
        <file src="images\picture.png" target="Content\images\package.icons" />

    Packaged result:
        content\images\package.icons\picture.png

<span data-ttu-id="91a27-367">**Inhaltsdateien ohne Erweiterungen**</span><span class="sxs-lookup"><span data-stu-id="91a27-367">**Content files without extensions**</span></span>

<span data-ttu-id="91a27-368">Verwenden Sie die Platzhalterzeichen `*` oder `**`, um Dateien ohne Erweiterungen einzufügen:</span><span class="sxs-lookup"><span data-stu-id="91a27-368">To include files without an extension, use the `*` or `**` wildcards:</span></span>

    Source file:
        flags\installed

    .nuspec entry:
        <file src="flags\**" target="flags" />

    Packaged result:
        flags\installed

<span data-ttu-id="91a27-369">**Inhaltsdateien mit tiefen Pfaden und tiefen Zielen**</span><span class="sxs-lookup"><span data-stu-id="91a27-369">**Content files with deep path and deep target**</span></span>

<span data-ttu-id="91a27-370">In diesem Fall nimmt NuGet an, dass das Ziel ein Dateiname und kein Ordner ist, da die Dateierweiterungen von Quelle und Ziel übereinstimmen:</span><span class="sxs-lookup"><span data-stu-id="91a27-370">In this case, because the file extensions of the source and target match, NuGet assumes that the target is a file name and not a folder:</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry:
        <file src="css\cool\style.css" target="Content\css\cool" />
        or:
        <file src="css\cool\style.css" target="Content\css\cool\style.css" />

    Packaged result:
        content\css\cool\style.css

<span data-ttu-id="91a27-371">**Umbenennen einer Inhaltsdatei im Paket**</span><span class="sxs-lookup"><span data-stu-id="91a27-371">**Renaming a content file in the package**</span></span>

    Source file:
        ie\css\style.css

    .nuspec entry:
        <file src="ie\css\style.css" target="Content\css\ie.css" />

    Packaged result:
        content\css\ie.css

<span data-ttu-id="91a27-372">**Ausschließen von Dateien**</span><span class="sxs-lookup"><span data-stu-id="91a27-372">**Excluding files**</span></span>

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

### <a name="using-the-contentfiles-element-for-content-files"></a><span data-ttu-id="91a27-373">Verwenden des contentFiles-Elements für Inhaltsdateien</span><span class="sxs-lookup"><span data-stu-id="91a27-373">Using the contentFiles element for content files</span></span>

<span data-ttu-id="91a27-374">*NuGet 4.0 und höher mit PackageReference*</span><span class="sxs-lookup"><span data-stu-id="91a27-374">*NuGet 4.0+ with PackageReference*</span></span>

<span data-ttu-id="91a27-375">Standardmäßig platzieren Pakete Inhalte in einem `contentFiles`-Ordner (s. unten), in den `nuget pack` alle Dateien mithilfe von Standardattributen eingefügt hat.</span><span class="sxs-lookup"><span data-stu-id="91a27-375">By default, a package places content in a `contentFiles` folder (see below) and `nuget pack` included all files in that folder using default attributes.</span></span> <span data-ttu-id="91a27-376">In diesem Fall ist es nicht notwendig, einen `contentFiles`-Knoten in `.nuspec` einzufügen.</span><span class="sxs-lookup"><span data-stu-id="91a27-376">In this case it's not necessary to include a `contentFiles` node in the `.nuspec` at all.</span></span>

<span data-ttu-id="91a27-377">Das `<contentFiles>`-Element gibt eine Auflistung von `<files>`-Elementen an, die die eingefügten Dateien erkennen, um zu kontrollieren, welche Dateien eingefügt wurden.</span><span class="sxs-lookup"><span data-stu-id="91a27-377">To control which files are included, the `<contentFiles>` element specifies is a collection of `<files>` elements that identify the exact files include.</span></span>

<span data-ttu-id="91a27-378">Diese Dateien werden zusammen mit mehreren Attributen angegeben, die beschreiben, wie sie in dem Projektsystem verwendet werden sollen:</span><span class="sxs-lookup"><span data-stu-id="91a27-378">These files are specified with a set of attributes that describe how they should be used within the project system:</span></span>

| <span data-ttu-id="91a27-379">Attribut</span><span class="sxs-lookup"><span data-stu-id="91a27-379">Attribute</span></span> | <span data-ttu-id="91a27-380">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="91a27-380">Description</span></span> |
| --- | --- |
| <span data-ttu-id="91a27-381">**include**</span><span class="sxs-lookup"><span data-stu-id="91a27-381">**include**</span></span> | <span data-ttu-id="91a27-382">(Erforderlich) Der Speicherort der Dateien, die eingefügt werden sollen, unterliegt Ausnahmen, die von dem `exclude`-Attribut angegeben werden.</span><span class="sxs-lookup"><span data-stu-id="91a27-382">(Required) The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="91a27-383">Der Pfad ist relativ zur `.nuspec`-Datei, wenn kein absoluter Pfad angegeben ist.</span><span class="sxs-lookup"><span data-stu-id="91a27-383">The path is relative to the `.nuspec` file unless an absolute path is specified.</span></span> <span data-ttu-id="91a27-384">Das Platzhalterzeichen `*` ist zulässig, und das zweifache Platzhalterzeichen `**` impliziert eine rekursive Ordnersuche.</span><span class="sxs-lookup"><span data-stu-id="91a27-384">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="91a27-385">**exclude**</span><span class="sxs-lookup"><span data-stu-id="91a27-385">**exclude**</span></span> | <span data-ttu-id="91a27-386">Eine durch Semikolons abgetrennte Datei oder Dateimuster, die sich nicht im `src`-Speicherort befinden dürfen.</span><span class="sxs-lookup"><span data-stu-id="91a27-386">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="91a27-387">Das Platzhalterzeichen `*` ist zulässig, und das zweifache Platzhalterzeichen `**` impliziert eine rekursive Ordnersuche.</span><span class="sxs-lookup"><span data-stu-id="91a27-387">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="91a27-388">**buildAction**</span><span class="sxs-lookup"><span data-stu-id="91a27-388">**buildAction**</span></span> | <span data-ttu-id="91a27-389">Die Buildaktion, die dem Inhaltselement für MSBuild zugewiesen werden soll. Z.B. `Content`, `None`, `Embedded Resource` oder `Compile`. Die Standardeinstellung ist `Compile`.</span><span class="sxs-lookup"><span data-stu-id="91a27-389">The build action to assign to the content item for MSBuild, such as `Content`, `None`, `Embedded Resource`, `Compile`, etc. The default is `Compile`.</span></span> |
| <span data-ttu-id="91a27-390">**copyToOutput**</span><span class="sxs-lookup"><span data-stu-id="91a27-390">**copyToOutput**</span></span> | <span data-ttu-id="91a27-391">Ein boolescher Wert, der angibt, ob der Ordner "Output" Inhaltselemente auf den Build zu kopieren (oder veröffentlichen).</span><span class="sxs-lookup"><span data-stu-id="91a27-391">A Boolean indicating whether to copy content items to the build (or publish) output folder.</span></span> <span data-ttu-id="91a27-392">Der Standardwert ist false.</span><span class="sxs-lookup"><span data-stu-id="91a27-392">The default is false.</span></span> |
| <span data-ttu-id="91a27-393">**flatten**</span><span class="sxs-lookup"><span data-stu-id="91a27-393">**flatten**</span></span> | <span data-ttu-id="91a27-394">Ein boolescher Wert, der angibt, ob Inhaltselemente in einen Ordner in der Buildausgabe kopiert werden sollen (TRUE) oder ob die Ordnerstruktur in den Paketen beibehalten werden soll (FALSE).</span><span class="sxs-lookup"><span data-stu-id="91a27-394">A Boolean indicating whether to copy content items to a single folder in the build output (true), or to preserve the folder structure in the package (false).</span></span> <span data-ttu-id="91a27-395">Diese Flag funktioniert nur, wenn das copyToOutput-Flag auf TRUE festgelegt ist.</span><span class="sxs-lookup"><span data-stu-id="91a27-395">This flag only works when copyToOutput flag is set to true.</span></span> <span data-ttu-id="91a27-396">Der Standardwert ist false.</span><span class="sxs-lookup"><span data-stu-id="91a27-396">The default is false.</span></span> |

<span data-ttu-id="91a27-397">NuGet wendet die untergeordneten Elemente von `<contentFiles>` bei der Installation eines Pakets von unten nach oben an.</span><span class="sxs-lookup"><span data-stu-id="91a27-397">When installing a package, NuGet applies the child elements of `<contentFiles>` from top to bottom.</span></span> <span data-ttu-id="91a27-398">Wenn mehrere Einträge in einer Datei vorhanden sind, werden sie alle angewendet.</span><span class="sxs-lookup"><span data-stu-id="91a27-398">If multiple entries match the same file then all entries are applied.</span></span> <span data-ttu-id="91a27-399">Der höher geordnete Eintrag setzt die untergeordneten Einträge außer Kraft, wenn ein Konflikt für ein Attribut entsteht.</span><span class="sxs-lookup"><span data-stu-id="91a27-399">The top-most entry overrides the lower entries if there is a conflict for the same attribute.</span></span>

#### <a name="package-folder-structure"></a><span data-ttu-id="91a27-400">Paketordnerstruktur</span><span class="sxs-lookup"><span data-stu-id="91a27-400">Package folder structure</span></span>

<span data-ttu-id="91a27-401">Das Paketprojekt sollte Inhalte mithilfe des folgenden Musters strukturieren:</span><span class="sxs-lookup"><span data-stu-id="91a27-401">The package project should structure content using the following pattern:</span></span>

    /contentFiles/{codeLanguage}/{TxM}/{any?}

- <span data-ttu-id="91a27-402">`codeLanguages` kann `cs`, `vb`, `fs`, `any` oder das klein geschriebene Äquivalent einer `$(ProjectLanguage)` sein.</span><span class="sxs-lookup"><span data-stu-id="91a27-402">`codeLanguages` may be `cs`, `vb`, `fs`, `any`, or the lowercase equivalent of a given `$(ProjectLanguage)`</span></span>
- <span data-ttu-id="91a27-403">`TxM` ist ein für das Zielframework zulässiger Moniker, der NuGet unterstützt (Informationen dazu finden Sie unter [Zielframeworks](../reference/target-frameworks.md)).</span><span class="sxs-lookup"><span data-stu-id="91a27-403">`TxM` is any legal target framework moniker that NuGet supports (see [Target frameworks](../reference/target-frameworks.md)).</span></span>
- <span data-ttu-id="91a27-404">An das Ende der Syntax kann eine beliebige Ordnerstruktur angehängt werden.</span><span class="sxs-lookup"><span data-stu-id="91a27-404">Any folder structure may be appended to the end of this syntax.</span></span>

<span data-ttu-id="91a27-405">Zum Beispiel:</span><span class="sxs-lookup"><span data-stu-id="91a27-405">For example:</span></span>

    Language- and framework-agnostic:
        /contentFiles/any/any/config.xml

    net45 content for all languages
        /contentFiles/any/net45/config.xml

    C#-specific content for net45 and up
        /contentFiles/cs/net45/sample.cs

<span data-ttu-id="91a27-406">Für leere Ordner kann `.` eingefügt werden, wenn diese keine Inhalte mehr für bestimmte Sprachen und TxM bereitstellen sollen. Z.B.:</span><span class="sxs-lookup"><span data-stu-id="91a27-406">Empty folders can use `.` to opt out of providing content for certain combinations of language and TxM, for example:</span></span>

    /contentFiles/vb/any/code.vb
    /contentFiles/cs/any/.

#### <a name="example-contentfiles-section"></a><span data-ttu-id="91a27-407">Beispiel: Abschnitt „contentFiles“</span><span class="sxs-lookup"><span data-stu-id="91a27-407">Example contentFiles section</span></span>

```xml
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
```

## <a name="example-nuspec-files"></a><span data-ttu-id="91a27-408">Beispiel: Nuspec-Dateien</span><span class="sxs-lookup"><span data-stu-id="91a27-408">Example nuspec files</span></span>

<span data-ttu-id="91a27-409">** Eine einfache `.nuspec`-Datei, die weder Abhängigkeiten noch Dateien enthält**</span><span class="sxs-lookup"><span data-stu-id="91a27-409">**A simple `.nuspec` that does not specify dependencies or files**</span></span>

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
        <licenseUrl>http://xunit.codeplex.com/license</licenseUrl>
    </metadata>
</package>
```

<span data-ttu-id="91a27-410">** Eine `.nuspec`-Datei mit Abhängigkeiten**</span><span class="sxs-lookup"><span data-stu-id="91a27-410">**A `.nuspec` with dependencies**</span></span>

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

<span data-ttu-id="91a27-411">**Eine `.nuspec`-Datei mit Dateien**</span><span class="sxs-lookup"><span data-stu-id="91a27-411">**A `.nuspec` with files**</span></span>

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

<span data-ttu-id="91a27-412">**Eine `.nuspec`-Datei mit Frameworkassemblys**</span><span class="sxs-lookup"><span data-stu-id="91a27-412">**A `.nuspec` with framework assemblies**</span></span>

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

<span data-ttu-id="91a27-413">In diesem Beispiel werden die folgenden Elemente für bestimmte Projektziele installiert:</span><span class="sxs-lookup"><span data-stu-id="91a27-413">In this example, the following are installed for specific project targets:</span></span>

- <span data-ttu-id="91a27-414">.NET4: `System.Web` und `System.Net`</span><span class="sxs-lookup"><span data-stu-id="91a27-414">.NET4 -> `System.Web`, `System.Net`</span></span>
- <span data-ttu-id="91a27-415">.NET4-Clientprofil: `System.Net`</span><span class="sxs-lookup"><span data-stu-id="91a27-415">.NET4 Client Profile -> `System.Net`</span></span>
- <span data-ttu-id="91a27-416">Silverlight 3: `System.Json`</span><span class="sxs-lookup"><span data-stu-id="91a27-416">Silverlight 3 -> `System.Json`</span></span>
- <span data-ttu-id="91a27-417">Silverlight 4: `System.Windows.Controls.DomainServices`</span><span class="sxs-lookup"><span data-stu-id="91a27-417">Silverlight 4 -> `System.Windows.Controls.DomainServices`</span></span>
- <span data-ttu-id="91a27-418">WindowsPhone: `Microsoft.Devices.Sensors`</span><span class="sxs-lookup"><span data-stu-id="91a27-418">WindowsPhone -> `Microsoft.Devices.Sensors`</span></span>
