---
title: "NUSPEC-Dateireferenz für NuGet | Microsoft-Dokumentation"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 08/29/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
description: "Die NUSPEC-Datei enthält Paketmetadaten, die bei der Erstellung eines Pakets verwendet werden, um für die Paketbenutzer Informationen bereitzustellen."
keywords: NUSPEC-Referenz, NuGet-Paketmetadaten, NuGet-Paketmanifest, NUSPEC-Schema
ms.reviewer:
- anangaur
- karann-msft
- unniravindranathan
ms.openlocfilehash: 95f86d8cd11bce8f0f1fed068370311f575601de
ms.sourcegitcommit: 24997b5345a997501fff846c9bd73610245ae0a6
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/31/2018
---
# <a name="nuspec-reference"></a><span data-ttu-id="ae703-104">NUSPEC-Referenz</span><span class="sxs-lookup"><span data-stu-id="ae703-104">.nuspec reference</span></span>

<span data-ttu-id="ae703-105">Bei einer `.nuspec`-Datei handelt es sich um eine XML-Manifestdatei, die Paketmetadaten enthält.</span><span class="sxs-lookup"><span data-stu-id="ae703-105">A `.nuspec` file is an XML manifest that contains package metadata.</span></span> <span data-ttu-id="ae703-106">Diese Manifestdatei wird sowohl für die Erstellung des Pakets als auch zur Bereitstellung von Informationen für die Benutzer verwendet.</span><span class="sxs-lookup"><span data-stu-id="ae703-106">This manifest is used both to build the package and to provide information to consumers.</span></span> <span data-ttu-id="ae703-107">Manifestdateien sind in allen Paketen enthalten.</span><span class="sxs-lookup"><span data-stu-id="ae703-107">The manifest is always included in a package.</span></span>

<span data-ttu-id="ae703-108">In diesem Thema:</span><span class="sxs-lookup"><span data-stu-id="ae703-108">In this topic:</span></span>

- [<span data-ttu-id="ae703-109">Allgemeine Form und Schema</span><span class="sxs-lookup"><span data-stu-id="ae703-109">General form and schema</span></span>](#general-form-and-schema)
- <span data-ttu-id="ae703-110">[Ersetzungstokens](#replacement-tokens) (bei der Verwendung in einem Visual Studio-Projekt)</span><span class="sxs-lookup"><span data-stu-id="ae703-110">[Replacement tokens](#replacement-tokens) (when used with a Visual Studio project)</span></span>
- [<span data-ttu-id="ae703-111">Abhängigkeiten</span><span class="sxs-lookup"><span data-stu-id="ae703-111">Dependencies</span></span>](#dependencies)
- [<span data-ttu-id="ae703-112">Explizite Assemblyverweise</span><span class="sxs-lookup"><span data-stu-id="ae703-112">Explicit assembly references</span></span>](#explicit-assembly-references)
- [<span data-ttu-id="ae703-113">Verweise auf Frameworkassemblys</span><span class="sxs-lookup"><span data-stu-id="ae703-113">Framework assembly references</span></span>](#framework-assembly-references)
- [<span data-ttu-id="ae703-114">Einfügen von Assemblydateien</span><span class="sxs-lookup"><span data-stu-id="ae703-114">Including assembly files</span></span>](#including-assembly-files)
- [<span data-ttu-id="ae703-115">Einfügen von Inhaltsdateien</span><span class="sxs-lookup"><span data-stu-id="ae703-115">Including content files</span></span>](#including-content-files)
- [<span data-ttu-id="ae703-116">Beispiele</span><span class="sxs-lookup"><span data-stu-id="ae703-116">Examples</span></span>](#examples)

## <a name="general-form-and-schema"></a><span data-ttu-id="ae703-117">Allgemeine Form und Schema</span><span class="sxs-lookup"><span data-stu-id="ae703-117">General form and schema</span></span>

<span data-ttu-id="ae703-118">Die aktuelle `nuspec.xsd`-Schemadatei finden Sie im [NuGet GitHub-Repository](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span><span class="sxs-lookup"><span data-stu-id="ae703-118">The current `nuspec.xsd` schema file can be found in the [NuGet GitHub repository](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span></span>

<span data-ttu-id="ae703-119">Für dieses Schema gilt die im Folgenden dargestellte allgemeine Form für die `.nuspec`-Datei:</span><span class="sxs-lookup"><span data-stu-id="ae703-119">Within this schema, a `.nuspec` file has the following general form:</span></span>

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

<span data-ttu-id="ae703-120">Für eine übersichtliche Darstellung des Schemas öffnen Sie die Schemadatei im Entwurfsmodus in Visual Studio, und klicken Sie auf den Link **XML-Schema-Explorer**.</span><span class="sxs-lookup"><span data-stu-id="ae703-120">For a clear visual representation of the schema, open the schema file in Visual Studio in Design mode and click on the **XML Schema Explorer** link.</span></span> <span data-ttu-id="ae703-121">Alternativ können Sie auch die Datei als Code öffnen, mit der rechten Maustaste in den Editor klicken und **Show XML Schema Explorer** (XML-Schema-Explorer anzeigen) auswählen.</span><span class="sxs-lookup"><span data-stu-id="ae703-121">Alternately, open the file as code, right-click in the editor, and select **Show XML Schema Explorer**.</span></span> <span data-ttu-id="ae703-122">In beiden Fällen wird eine Ansicht zurückgegeben, die der in der folgenden Abbildung ähnlich ist, wenn Sie größtenteils erweitert ist:</span><span class="sxs-lookup"><span data-stu-id="ae703-122">Either way you get a view like the one below (when mostly expanded):</span></span>

![Visual Studio-Schema-Explorer mit geöffneter „nuspec.xsd“-Datei](media/SchemaExplorer.png)

### <a name="metadata-attributes"></a><span data-ttu-id="ae703-124">Metadatenattribute</span><span class="sxs-lookup"><span data-stu-id="ae703-124">Metadata attributes</span></span>

<span data-ttu-id="ae703-125">Das `<metadata>`-Element unterstützt die in der folgenden Tabelle beschriebenen Attribute.</span><span class="sxs-lookup"><span data-stu-id="ae703-125">The `<metadata>` element supports the attributes described in the following table.</span></span>

| <span data-ttu-id="ae703-126">Attribut</span><span class="sxs-lookup"><span data-stu-id="ae703-126">Attribute</span></span> | <span data-ttu-id="ae703-127">Erforderlich</span><span class="sxs-lookup"><span data-stu-id="ae703-127">Required</span></span> | <span data-ttu-id="ae703-128">description</span><span class="sxs-lookup"><span data-stu-id="ae703-128">Description</span></span> |
| --- | --- | --- | 
| <span data-ttu-id="ae703-129">**minClientVersion**</span><span class="sxs-lookup"><span data-stu-id="ae703-129">**minClientVersion**</span></span> | <span data-ttu-id="ae703-130">Nein</span><span class="sxs-lookup"><span data-stu-id="ae703-130">No</span></span> | <span data-ttu-id="ae703-131">Gibt die minimale Version des NuGet-Clients an, der dieses Paket installieren kann. Dies wird von nuget.exe und dem Paket-Manager von Visual Studio erzwungen.</span><span class="sxs-lookup"><span data-stu-id="ae703-131">Specifies the minimum version of the NuGet client that can install this package, enforced by nuget.exe and the Visual Studio Package Manager.</span></span> <span data-ttu-id="ae703-132">Dieses Attribut wird verwendet, wenn das Paket von bestimmten Funktionen der `.nuspec`-Datei abhängig ist, die in einer bestimmten Version des NuGet-Clients hinzugefügt wurden.</span><span class="sxs-lookup"><span data-stu-id="ae703-132">This is used whenever the package depends on specific features of the `.nuspec` file that were added in a particular version of the NuGet client.</span></span> <span data-ttu-id="ae703-133">Beispielsweise sollte ein Paket, das das `developmentDependency`-Attribut verwendet, „2.8“ für `minClientVersion` angeben.</span><span class="sxs-lookup"><span data-stu-id="ae703-133">For example, a package using the `developmentDependency` attribute should specify "2.8" for `minClientVersion`.</span></span> <span data-ttu-id="ae703-134">Genauso sollte ein Paket, das das `contentFiles`-Element verwendet (vgl. nächster Abschnitt), `minClientVersion` auf „3.3“ festlegen.</span><span class="sxs-lookup"><span data-stu-id="ae703-134">Similarly, a package using the `contentFiles` element (see the next section) should set `minClientVersion` to "3.3".</span></span> <span data-ttu-id="ae703-135">Beachten Sie außerdem, dass NuGet-Clients vor Version 2.5 diese Kennzeichnung nicht erkennen und daher die Installation des Pakets, unabhängig vom Inhalt von `minClientVersion`, *immer* verweigern.</span><span class="sxs-lookup"><span data-stu-id="ae703-135">Note also that because NuGet clients prior to 2.5 do not recognize this flag, they *always* refuse to install the package no matter what `minClientVersion` contains.</span></span> |

### <a name="required-metadata-elements"></a><span data-ttu-id="ae703-136">Erforderliche Metadatenelemente</span><span class="sxs-lookup"><span data-stu-id="ae703-136">Required metadata elements</span></span>

<span data-ttu-id="ae703-137">Obwohl es sich bei den folgenden Elementen um die Mindestanforderungen für ein Paket handelt, sollten Sie in Erwägung ziehen, die [optionalen Metadatenelemente](#optional-metadata-elements) hinzuzufügen, damit Entwicklern die Arbeit mit Ihren Paketen erleichtert wird.</span><span class="sxs-lookup"><span data-stu-id="ae703-137">Although the following elements are the minimum requirements for a package, you should consider adding the [optional metadata elements](#optional-metadata-elements) to improve the overall experience developers have with your package.</span></span>

<span data-ttu-id="ae703-138">Diese Elemente müssen in einem `<metadata>`-Element angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="ae703-138">These elements must appear within a `<metadata>` element.</span></span>

| <span data-ttu-id="ae703-139">Element</span><span class="sxs-lookup"><span data-stu-id="ae703-139">Element</span></span> | <span data-ttu-id="ae703-140">description</span><span class="sxs-lookup"><span data-stu-id="ae703-140">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ae703-141">**ID**</span><span class="sxs-lookup"><span data-stu-id="ae703-141">**id**</span></span> | <span data-ttu-id="ae703-142">Der Paketbezeichner, der die Groß- und Kleinschreibung nicht berücksichtigt und auf nuget.org oder im für das Paket verwendeten Katalog eindeutig sein muss.</span><span class="sxs-lookup"><span data-stu-id="ae703-142">The case-insensitive package identifier, which must be unique across nuget.org or whatever gallery the package resides in.</span></span> <span data-ttu-id="ae703-143">IDs dürfen keine Leerzeichen oder für eine URL unzulässige Zeichen enthalten. Sie müssen den Regeln für .NET-Namespaces entsprechen.</span><span class="sxs-lookup"><span data-stu-id="ae703-143">IDs may not contain spaces or characters that are not valid for a URL, and generally follow .NET namespace rules.</span></span> <span data-ttu-id="ae703-144">Informationen finden Sie unter [Choosing a unique package identifier (Auswählen eines eindeutigen Paketbezeichners)](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number).</span><span class="sxs-lookup"><span data-stu-id="ae703-144">See [Choosing a unique package identifier](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number) for guidance.</span></span> |
| <span data-ttu-id="ae703-145">**version**</span><span class="sxs-lookup"><span data-stu-id="ae703-145">**version**</span></span> | <span data-ttu-id="ae703-146">Die Version des Pakets, die dem Muster *Hauptversion.Nebenversion.Patch* folgt.</span><span class="sxs-lookup"><span data-stu-id="ae703-146">The version of the package, following the *major.minor.patch* pattern.</span></span> <span data-ttu-id="ae703-147">Versionsnummern enthalten möglicherweise, wie unter [Paketversionsverwaltung](../reference/package-versioning.md#pre-release-versions) beschrieben, ein Suffix der Vorabversion.</span><span class="sxs-lookup"><span data-stu-id="ae703-147">Version numbers may include a pre-release suffix as described in [Package versioning](../reference/package-versioning.md#pre-release-versions).</span></span> |
| <span data-ttu-id="ae703-148">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="ae703-148">**description**</span></span> | <span data-ttu-id="ae703-149">Eine ausführliche Beschreibung des Pakets für die Anzeige der Benutzeroberfläche.</span><span class="sxs-lookup"><span data-stu-id="ae703-149">A long description of the package for UI display.</span></span> |
| <span data-ttu-id="ae703-150">**authors**</span><span class="sxs-lookup"><span data-stu-id="ae703-150">**authors**</span></span> | <span data-ttu-id="ae703-151">Eine durch Kommas getrennte Liste der Paketautoren, die mit Profilnamen unter nuget.org übereinstimmen. Diese werden im NuGet-Katalog unter nuget.org angezeigt und werden verwendet, um Querverweise auf Pakete von den gleichen Autoren zu geben.</span><span class="sxs-lookup"><span data-stu-id="ae703-151">A comma-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> |

### <a name="optional-metadata-elements"></a><span data-ttu-id="ae703-152">Optionale Metadatenelemente</span><span class="sxs-lookup"><span data-stu-id="ae703-152">Optional metadata elements</span></span>

<span data-ttu-id="ae703-153">Diese Elemente auftreten in einem `<metadata>`-Element angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="ae703-153">These elements may appear within a `<metadata>` element.</span></span>

#### <a name="single-elements"></a><span data-ttu-id="ae703-154">Einzelne Elemente</span><span class="sxs-lookup"><span data-stu-id="ae703-154">Single elements</span></span>

| <span data-ttu-id="ae703-155">Element</span><span class="sxs-lookup"><span data-stu-id="ae703-155">Element</span></span> | <span data-ttu-id="ae703-156">description</span><span class="sxs-lookup"><span data-stu-id="ae703-156">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ae703-157">**title**</span><span class="sxs-lookup"><span data-stu-id="ae703-157">**title**</span></span> | <span data-ttu-id="ae703-158">Ein benutzerfreundlicher Titel des Pakets, der in der Regel in der Benutzeroberfläche wie auf nuget.org angezeigt wird und der Paket-Manager in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="ae703-158">A human-friendly title of the package, typically used in UI displays as on nuget.org and the Package Manager in Visual Studio.</span></span> <span data-ttu-id="ae703-159">Wenn nicht angegeben, wird die Paket-ID verwendet.</span><span class="sxs-lookup"><span data-stu-id="ae703-159">If not specified, the package ID is used.</span></span> |
| <span data-ttu-id="ae703-160">**owners**</span><span class="sxs-lookup"><span data-stu-id="ae703-160">**owners**</span></span> | <span data-ttu-id="ae703-161">Eine durch Kommas getrennte Liste der Paketersteller, die auf nuget.org Profilnamen verwenden. Dabei handelt es sich häufig um dieselbe Liste wie in `authors`. Sie wird beim Hochladen der Pakete auf nuget.org ignoriert. Informationen dazu finden Sie unter [Managing package owners on nuget.org (Verwalten von Paketbesitzern auf nuget.org)](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg).</span><span class="sxs-lookup"><span data-stu-id="ae703-161">A comma-separated list of the package creators using profile names on nuget.org. This is often the same list as in `authors`, and is ignored when uploading the package to nuget.org. See [Managing package owners on nuget.org](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg).</span></span> |
| <span data-ttu-id="ae703-162">**projectUrl**</span><span class="sxs-lookup"><span data-stu-id="ae703-162">**projectUrl**</span></span> | <span data-ttu-id="ae703-163">Eine URL für die Paket-Homepage, häufig auf der Benutzeroberfläche sowie auf nuget.org angezeigt.</span><span class="sxs-lookup"><span data-stu-id="ae703-163">A URL for the package's home page, often shown in UI displays as well as nuget.org.</span></span> |
| <span data-ttu-id="ae703-164">**licenseUrl**</span><span class="sxs-lookup"><span data-stu-id="ae703-164">**licenseUrl**</span></span> | <span data-ttu-id="ae703-165">Eine URL für die Paketlizenz, häufig auf der Benutzeroberfläche sowie auf nuget.org angezeigt.</span><span class="sxs-lookup"><span data-stu-id="ae703-165">A URL for the package's license, often shown in UI displays as well as nuget.org.</span></span> |
| <span data-ttu-id="ae703-166">**iconUrl**</span><span class="sxs-lookup"><span data-stu-id="ae703-166">**iconUrl**</span></span> | <span data-ttu-id="ae703-167">Eine URL für ein 64x64-Bild mit transparentem Hintergrund, das als Symbol für das Paket in der Benutzeroberfläche verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="ae703-167">A URL for a 64x64 image with transparency background to use as the icon for the package in UI display.</span></span> <span data-ttu-id="ae703-168">Stellen Sie sicher, dass dieses Element die *direkte Bild-URL* und nicht nur die URL einer Webseite enthält, die das Bild enthält.</span><span class="sxs-lookup"><span data-stu-id="ae703-168">Be sure this element contains the *direct image URL* and not the URL of a web page containing the image.</span></span> <span data-ttu-id="ae703-169">Mithilfe der URL einer Rohdatendatei wie `https://github.com/<username>/<repository>/raw/<branch>/<logo.png>` können Sie beispielsweise ein Bild von GitHub verwenden.</span><span class="sxs-lookup"><span data-stu-id="ae703-169">For example, to use an image from GitHub, use the raw file URL like `https://github.com/<username>/<repository>/raw/<branch>/<logo.png>`.</span></span> |
| <span data-ttu-id="ae703-170">**requireLicenseAcceptance**</span><span class="sxs-lookup"><span data-stu-id="ae703-170">**requireLicenseAcceptance**</span></span> | <span data-ttu-id="ae703-171">Ein boolescher Wert, der angibt, ob der Client den Benutzer dazu auffordern muss, die Paketlizenz vor der Installation des Pakets zu akzeptieren.</span><span class="sxs-lookup"><span data-stu-id="ae703-171">A Boolean value specifying whether the client must prompt the consumer to accept the package license before installing the package.</span></span> |
| <span data-ttu-id="ae703-172">**developmentDependency**</span><span class="sxs-lookup"><span data-stu-id="ae703-172">**developmentDependency**</span></span> | <span data-ttu-id="ae703-173">*(2.8 und höher)* Ein boolescher Wert, der angibt, ob das Paket mit einer Abhängigkeit markiert werden soll, die nur für die Entwicklung gilt, wodurch vermieden wird, dass das Paket als Abhängigkeit in andere Pakete eingefügt wird.</span><span class="sxs-lookup"><span data-stu-id="ae703-173">*(2.8+)* A Boolean value specifying whether the package is be marked as a development-only-dependency, which prevents the package from being included as a dependency in other packages.</span></span> |
| <span data-ttu-id="ae703-174">**summary**</span><span class="sxs-lookup"><span data-stu-id="ae703-174">**summary**</span></span> | <span data-ttu-id="ae703-175">Eine kurze Beschreibung des Pakets für die Anzeige der Benutzeroberfläche.</span><span class="sxs-lookup"><span data-stu-id="ae703-175">A short description of the package for UI display.</span></span> <span data-ttu-id="ae703-176">Wenn diese nicht angegeben wird, wird eine gekürzte Version von `description` verwendet.</span><span class="sxs-lookup"><span data-stu-id="ae703-176">If omitted, a truncated version of `description` is used.</span></span> |
| <span data-ttu-id="ae703-177">**releaseNotes**</span><span class="sxs-lookup"><span data-stu-id="ae703-177">**releaseNotes**</span></span> | <span data-ttu-id="ae703-178">*(1.5 und höher)* Eine Beschreibung der in diesem Release des Pakets enthaltenen Änderungen, die häufig in Benutzeroberflächen wie der Registerkarte **Updates** des Visual Studio-Paket-Managers anstelle von Paketbeschreibungen verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="ae703-178">*(1.5+)* A description of the changes made in this release of the package, often used in UI like the **Updates** tab of the Visual Studio Package Manager in place of the package description.</span></span> |
| <span data-ttu-id="ae703-179">**copyright**</span><span class="sxs-lookup"><span data-stu-id="ae703-179">**copyright**</span></span> | <span data-ttu-id="ae703-180">*(1.5 und höher)* Copyright-Informationen zum Paket.</span><span class="sxs-lookup"><span data-stu-id="ae703-180">*(1.5+)* Copyright details for the package.</span></span> |
| <span data-ttu-id="ae703-181">**language**</span><span class="sxs-lookup"><span data-stu-id="ae703-181">**language**</span></span> | <span data-ttu-id="ae703-182">Die Gebietsschema-ID des Pakets.</span><span class="sxs-lookup"><span data-stu-id="ae703-182">The locale ID for the package.</span></span> <span data-ttu-id="ae703-183">Informationen dazu finden Sie unter [Creating localized packages (Erstellen von lokalisierten Paketen)](../create-packages/creating-localized-packages.md).</span><span class="sxs-lookup"><span data-stu-id="ae703-183">See [Creating localized packages](../create-packages/creating-localized-packages.md).</span></span> |
| <span data-ttu-id="ae703-184">**tags**</span><span class="sxs-lookup"><span data-stu-id="ae703-184">**tags**</span></span> | <span data-ttu-id="ae703-185">Eine durch Leerzeichen getrennte Liste mit Tags und Schlüsselwörtern, die das Paket beschreiben und zum Ermitteln von Paketen über Suchvorgänge und Filter beitragen.</span><span class="sxs-lookup"><span data-stu-id="ae703-185">A space-delimited list of tags and keywords that describe the package and aid discoverability of packages through search and filtering.</span></span> |
| <span data-ttu-id="ae703-186">**serviceable**</span><span class="sxs-lookup"><span data-stu-id="ae703-186">**serviceable**</span></span> | <span data-ttu-id="ae703-187">*(3.3 und höher)* Nur für die interne Verwendung von NuGet.</span><span class="sxs-lookup"><span data-stu-id="ae703-187">*(3.3+)* For internal NuGet use only.</span></span> |

#### <a name="collection-elements"></a><span data-ttu-id="ae703-188">Auflistungselemente</span><span class="sxs-lookup"><span data-stu-id="ae703-188">Collection elements</span></span>

| <span data-ttu-id="ae703-189">Element</span><span class="sxs-lookup"><span data-stu-id="ae703-189">Element</span></span> | <span data-ttu-id="ae703-190">description</span><span class="sxs-lookup"><span data-stu-id="ae703-190">Description</span></span> |
| --- | --- |
<span data-ttu-id="ae703-191">**packageTypes**</span><span class="sxs-lookup"><span data-stu-id="ae703-191">**packageTypes**</span></span> | <span data-ttu-id="ae703-192">*(3.5 und höher)* Eine Auflistung, die kein `<packageType>`-Element oder mindestens eins enthält und den Pakettyp angibt, wenn es sich nicht um ein gewöhnliches Abhängigkeitspaket handelt.</span><span class="sxs-lookup"><span data-stu-id="ae703-192">*(3.5+)* A collection of zero or more `<packageType>` elements specifying the type of the package if other than a traditional dependency package.</span></span> <span data-ttu-id="ae703-193">Jeder „packageType“ verfügt über Attribute von *name* und *version*.</span><span class="sxs-lookup"><span data-stu-id="ae703-193">Each packageType has attributes of *name* and *version*.</span></span> <span data-ttu-id="ae703-194">Informationen dazu finden Sie unter [Setting a package type (Festlegen eines Pakettypen)](../create-packages/creating-a-package.md#setting-a-package-type).</span><span class="sxs-lookup"><span data-stu-id="ae703-194">See [Setting a package type](../create-packages/creating-a-package.md#setting-a-package-type).</span></span> |
| <span data-ttu-id="ae703-195">**dependencies**</span><span class="sxs-lookup"><span data-stu-id="ae703-195">**dependencies**</span></span> | <span data-ttu-id="ae703-196">Eine Auflistung, die kein `<dependency>`-Element oder mindestens eins enthält und Abhängigkeiten für das Paket angibt.</span><span class="sxs-lookup"><span data-stu-id="ae703-196">A collection of zero or more `<dependency>` elements specifying the dependencies for the package.</span></span> <span data-ttu-id="ae703-197">Jede Abhängigkeit verfügt über Attribute von *id*, *version*, *include* und *exclude* (3.x und höher).</span><span class="sxs-lookup"><span data-stu-id="ae703-197">Each dependency has attributes of *id*, *version*, *include* (3.x+), and *exclude* (3.x+).</span></span> <span data-ttu-id="ae703-198">Informationen dazu finden Sie im Abschnitt [Abhängigkeiten](#dependencies).</span><span class="sxs-lookup"><span data-stu-id="ae703-198">See [Dependencies](#dependencies) below.</span></span> |
| <span data-ttu-id="ae703-199">**frameworkAssemblies**</span><span class="sxs-lookup"><span data-stu-id="ae703-199">**frameworkAssemblies**</span></span> | <span data-ttu-id="ae703-200">*(1.2 und höher)* Eine Auflistung, die kein `<frameworkAssembly>`-Element oder mindestens eins enthält und die für das Paket erforderlichen Verweise auf .NET Framework-Assemblys erkennt und sicherstellt, dass Verweise zu Projekten hinzugefügt werden, die das Paket verarbeiten.</span><span class="sxs-lookup"><span data-stu-id="ae703-200">*(1.2+)* A collection of zero or more `<frameworkAssembly>` elements identifying .NET Framework assembly references that this package requires, which ensures that references are added to projects consuming the package.</span></span> <span data-ttu-id="ae703-201">Jedes frameworkAssembly-Element verfügt über die Attribute *assemblyName* und *targetFramework*.</span><span class="sxs-lookup"><span data-stu-id="ae703-201">Each frameworkAssembly has *assemblyName* and *targetFramework* attributes.</span></span> <span data-ttu-id="ae703-202">Informationen dazu finden Sie unter [Specifying framework assembly references GAC (Angeben von GAC-Verweisen auf Frameworkassemblys)](#specifying-framework-assembly-references-gac).</span><span class="sxs-lookup"><span data-stu-id="ae703-202">See [Specifying framework assembly references GAC](#specifying-framework-assembly-references-gac) below.</span></span> |
| <span data-ttu-id="ae703-203">**references**</span><span class="sxs-lookup"><span data-stu-id="ae703-203">**references**</span></span> | <span data-ttu-id="ae703-204">*(1.5 und höher)* Eine Auflistung, die kein `<reference>`-Element oder mindestens eins enthält, das Assemblys in dem `lib`-Ordner des Pakets benennt, die als Projektverweise hinzugefügt werden.</span><span class="sxs-lookup"><span data-stu-id="ae703-204">*(1.5+)* A collection of zero or more `<reference>` elements naming assemblies in the package's `lib` folder that are added as project references.</span></span> <span data-ttu-id="ae703-205">Jeder Verweis verfügt über ein *file*-Attribut.</span><span class="sxs-lookup"><span data-stu-id="ae703-205">Each reference has a *file* attribute.</span></span> <span data-ttu-id="ae703-206">`<references>` kann außerdem ein `<group>`-Element mit einem *targetFramework*-Attribut enthalten, das anschließend `<reference>`-Elemente enthält.</span><span class="sxs-lookup"><span data-stu-id="ae703-206">`<references>` can also contain a `<group>` element with a *targetFramework* attribute, that then contains `<reference>` elements.</span></span> <span data-ttu-id="ae703-207">Wenn das Element nicht angegeben ist, werden alle Verweise in `lib` eingefügt.</span><span class="sxs-lookup"><span data-stu-id="ae703-207">If omitted, all references in `lib` are included.</span></span> <span data-ttu-id="ae703-208">Informationen dazu finden Sie unter [Specifying explicit assembly references (Angeben von expliziten Assemblyverweisen)](#specifying-explicit-assembly-references).</span><span class="sxs-lookup"><span data-stu-id="ae703-208">See [Specifying explicit assembly references](#specifying-explicit-assembly-references) below.</span></span> |
| <span data-ttu-id="ae703-209">**contentFiles**</span><span class="sxs-lookup"><span data-stu-id="ae703-209">**contentFiles**</span></span> | <span data-ttu-id="ae703-210">*(3.3 und höher)* Eine Auflistung von `<files>`-Elementen, die Inhaltsdateien ermitteln, die in das verarbeitende Projekt eingefügt werden sollen.</span><span class="sxs-lookup"><span data-stu-id="ae703-210">*(3.3+)* A collection of `<files>` elements that identify content files to include in the consuming project.</span></span> <span data-ttu-id="ae703-211">Diese Dateien werden zusammen mit mehreren Attributen angegeben, die beschreiben, wie sie in dem Projektsystem verwendet werden sollen.</span><span class="sxs-lookup"><span data-stu-id="ae703-211">These files are specified with a set of attributes that describe how they should be used within the project system.</span></span> <span data-ttu-id="ae703-212">Informationen dazu finden Sie unter [Specifying files to include in the package (Angeben von Dateien, die in das Paket eingefügt werden sollen)](#specifying-files-to-include-in-the-package).</span><span class="sxs-lookup"><span data-stu-id="ae703-212">See [Specifying files to include in the package](#specifying-files-to-include-in-the-package) below.</span></span> |

### <a name="files-element"></a><span data-ttu-id="ae703-213">Files-Element</span><span class="sxs-lookup"><span data-stu-id="ae703-213">Files element</span></span>

<span data-ttu-id="ae703-214">Der `<package>`-Knoten enthält möglicherweise einen `<files>`-Knoten, der `<metadata>` gleichgeordnet ist, und bzw. oder eine untergeordnete `<contentFiles>`-Datei unter `<metadata>`, um anzugeben, welche Assembly- und Inhaltsdateien in das Paket eingefügt werden sollen.</span><span class="sxs-lookup"><span data-stu-id="ae703-214">The `<package>` node may contain a `<files>` node as a sibling to `<metadata>`, and a or `<contentFiles>` child under `<metadata>`, to specify which assembly and content files to include in the package.</span></span> <span data-ttu-id="ae703-215">Details dazu finden Sie im Folgenden in den Abschnitten [Einfügen von Assemblydateien](#including-assembly-files) und [Einfügen von Inhaltsdateien](#including-content-files).</span><span class="sxs-lookup"><span data-stu-id="ae703-215">See [Including assembly files](#including-assembly-files) and [Including content files](#including-content-files) later in this topic for details.</span></span>

## <a name="replacement-tokens"></a><span data-ttu-id="ae703-216">Ersetzungstokens</span><span class="sxs-lookup"><span data-stu-id="ae703-216">Replacement tokens</span></span>

<span data-ttu-id="ae703-217">Bei der Erstellung eines Pakets ersetzt der [`nuget pack`-Befehl](../tools/cli-ref-pack.md) durch $ getrennte Tokens im `<metadata>`-Knoten der `.nuspec`-Datei durch Werte, die entweder einer Projektdatei oder dem `-properties`-Schalter des `pack`-Befehls entstammen.</span><span class="sxs-lookup"><span data-stu-id="ae703-217">When creating a package, the [`nuget pack` command](../tools/cli-ref-pack.md) replaces $-delimited tokens in the `.nuspec` file's `<metadata>` node with values that come from either a project file or the `pack` command's `-properties` switch.</span></span>

<span data-ttu-id="ae703-218">Geben Sie in der Befehlszeile die Tokenwerte mit `nuget pack -properties <name>=<value>;<name>=<value>` an.</span><span class="sxs-lookup"><span data-stu-id="ae703-218">On the command line, you specify token values with `nuget pack -properties <name>=<value>;<name>=<value>`.</span></span> <span data-ttu-id="ae703-219">Beispielsweise können Sie ein Token wie `$owners$` und `$desc$` in der `.nuspec`-Datei verwenden und die Werte zur Packzeit wie im Folgenden dargestellt bereitstellen:</span><span class="sxs-lookup"><span data-stu-id="ae703-219">For example, you can use a token such as `$owners$` and `$desc$` in the `.nuspec` and provide the values at packing time as follows:</span></span>

```ps
nuget pack MyProject.csproj -properties
    owners=janedoe,harikm,kimo,xiaop;desc="Awesome app logger utility"
```

<span data-ttu-id="ae703-220">Geben Sie die in der untenstehenden Tabelle beschriebenen Tokens an, um Werte aus einem Projekt zu verwenden (AssemblyInfo verweist auf Dateien wie `AssemblyInfo.cs` oder `AssemblyInfo.vb` in `Properties`).</span><span class="sxs-lookup"><span data-stu-id="ae703-220">To use values from a project, specify the tokens described in the table below (AssemblyInfo refers to the file in `Properties` such as `AssemblyInfo.cs` or `AssemblyInfo.vb`).</span></span>

<span data-ttu-id="ae703-221">Führen Sie anstelle von `.nuspec` nur `nuget pack` in der Projektdatei aus, um diese Tokens zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="ae703-221">To use these tokens, run `nuget pack` with the project file rather than just the `.nuspec`.</span></span> <span data-ttu-id="ae703-222">Beispielsweise werden bei der Verwendung des folgenden Befehls die Tokens `$id$` und `$version$` in einer `.nuspec`-Datei durch die Werte `AssemblyName` und `AssemblyVersion` des Projekts ersetzt:</span><span class="sxs-lookup"><span data-stu-id="ae703-222">For example, when using the following command, the `$id$` and `$version$` tokens in a `.nuspec` file are replaced with the project's `AssemblyName` and `AssemblyVersion` values:</span></span>

```ps
nuget pack MyProject.csproj
```

<span data-ttu-id="ae703-223">In der Regel erstellen Sie `.nuspec` in einem Projekt zuerst mithilfe von `nuget spec MyProject.csproj`, wodurch automatisch einige dieser Standardtokens eingefügt werden.</span><span class="sxs-lookup"><span data-stu-id="ae703-223">Typically, when you have a project, you create the `.nuspec` initially using `nuget spec MyProject.csproj` which automatically includes some of these standard tokens.</span></span> <span data-ttu-id="ae703-224">Wenn in einem Projekt allerdings keine Werte für erforderliche `.nuspec`-Elemente enthalten sind, schlägt `nuget pack` fehl.</span><span class="sxs-lookup"><span data-stu-id="ae703-224">However, if a project lacks values for required `.nuspec` elements, then `nuget pack` fails.</span></span> <span data-ttu-id="ae703-225">Stellen Sie außerdem bei der Änderung von Projektwerten sicher, dass Sie diese neu erstellen, bevor Sie das Paket erstellen. Dies können Sie ganz einfach über den `build`-Paketschalter des Befehls tun.</span><span class="sxs-lookup"><span data-stu-id="ae703-225">Furthermore, if you change project values, be sure to rebuild before creating the package; this can be done conveniently with the pack command's `build` switch.</span></span>

<span data-ttu-id="ae703-226">Mit Ausnahme von `$configuration$` werden Werte in dem Projekt gegenüber Werten bevorzugt, die demselben Token in der Befehlszeile zugeordnet sind.</span><span class="sxs-lookup"><span data-stu-id="ae703-226">With the exception of `$configuration$`, values in the project are used in preference to any assigned to the same token on the command line.</span></span>

| <span data-ttu-id="ae703-227">Token</span><span class="sxs-lookup"><span data-stu-id="ae703-227">Token</span></span> | <span data-ttu-id="ae703-228">Wertquelle</span><span class="sxs-lookup"><span data-stu-id="ae703-228">Value source</span></span> | <span data-ttu-id="ae703-229">Wert</span><span class="sxs-lookup"><span data-stu-id="ae703-229">Value</span></span>
| --- | --- | ---
| <span data-ttu-id="ae703-230">**$id$**</span><span class="sxs-lookup"><span data-stu-id="ae703-230">**$id$**</span></span> | <span data-ttu-id="ae703-231">Projektdatei</span><span class="sxs-lookup"><span data-stu-id="ae703-231">Project file</span></span> | <span data-ttu-id="ae703-232">„AssemblyName“ aus der Projektdatei</span><span class="sxs-lookup"><span data-stu-id="ae703-232">AssemblyName from the project file</span></span> |
| <span data-ttu-id="ae703-233">**$version$**</span><span class="sxs-lookup"><span data-stu-id="ae703-233">**$version$**</span></span> | <span data-ttu-id="ae703-234">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="ae703-234">AssemblyInfo</span></span> | <span data-ttu-id="ae703-235">„AssemblyInformationalVersion“, falls vorhanden, andernfalls „AssemblyVersion“</span><span class="sxs-lookup"><span data-stu-id="ae703-235">AssemblyInformationalVersion if present, otherwise AssemblyVersion</span></span> |
| <span data-ttu-id="ae703-236">**$author$**</span><span class="sxs-lookup"><span data-stu-id="ae703-236">**$author$**</span></span> | <span data-ttu-id="ae703-237">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="ae703-237">AssemblyInfo</span></span> | <span data-ttu-id="ae703-238">AssemblyCompany</span><span class="sxs-lookup"><span data-stu-id="ae703-238">AssemblyCompany</span></span> |
| <span data-ttu-id="ae703-239">**$description$**</span><span class="sxs-lookup"><span data-stu-id="ae703-239">**$description$**</span></span> | <span data-ttu-id="ae703-240">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="ae703-240">AssemblyInfo</span></span> | <span data-ttu-id="ae703-241">AssemblyDescription</span><span class="sxs-lookup"><span data-stu-id="ae703-241">AssemblyDescription</span></span> |
| <span data-ttu-id="ae703-242">**$copyright$**</span><span class="sxs-lookup"><span data-stu-id="ae703-242">**$copyright$**</span></span> | <span data-ttu-id="ae703-243">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="ae703-243">AssemblyInfo</span></span> | <span data-ttu-id="ae703-244">AssemblyCopyright</span><span class="sxs-lookup"><span data-stu-id="ae703-244">AssemblyCopyright</span></span> |
| <span data-ttu-id="ae703-245">**$configuration$**</span><span class="sxs-lookup"><span data-stu-id="ae703-245">**$configuration$**</span></span> | <span data-ttu-id="ae703-246">Assembly-DLL</span><span class="sxs-lookup"><span data-stu-id="ae703-246">Assembly DLL</span></span> | <span data-ttu-id="ae703-247">Konfiguration, die zur Erstellung der Assembly verwendet wird und standardmäßig auf „Debuggen“ festgelegt ist.</span><span class="sxs-lookup"><span data-stu-id="ae703-247">Configuration used to build the assembly, defaulting to Debug.</span></span> <span data-ttu-id="ae703-248">Achten Sie darauf, dass Sie stets `-properties Configuration=Release` in der Befehlszeile verwenden, um mithilfe einer Releasekonfiguration ein Paket zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="ae703-248">Note that to create a package using a Release configuration, you always use `-properties Configuration=Release` on the command line.</span></span> |

<span data-ttu-id="ae703-249">Tokens können auch zum Auflösen von Pfaden verwendet werden, wenn Sie [Assemblydateien](#including-assembly-files) und [Inhaltsdateien](#including-content-files) hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="ae703-249">Tokens can also be used to resolve paths when you include [assembly files](#including-assembly-files) and [content files](#including-content-files).</span></span> <span data-ttu-id="ae703-250">Die Namen der Tokens und der MSBuild-Eigenschaften stimmen miteinander überein, wodurch Sie abhängig von der aktuellen Buildkonfiguration Dateien auswählen können, die eingefügt werden sollen.</span><span class="sxs-lookup"><span data-stu-id="ae703-250">The tokens have the same names as the MSBuild properties, making it possible to select files to be included depending on the current build configuration.</span></span> <span data-ttu-id="ae703-251">Wenn Sie beispielsweise die folgenden Tokens in der `.nuspec`-Datei verwenden</span><span class="sxs-lookup"><span data-stu-id="ae703-251">For example, if you use the following tokens in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="bin\$configuration$\$id$.pdb" target="lib\net40" />
</files>
```

<span data-ttu-id="ae703-252">und Sie eine Assembly mit der `Release`-Konfiguration in MSBuild erstellen, deren `AssemblyName` `LoggingLibrary` ist, sehen die dadurch entstandenen Zeilen in der `.nuspec`-Datei in den Paketen wie folgt aus:</span><span class="sxs-lookup"><span data-stu-id="ae703-252">And you build an assembly whose `AssemblyName` is `LoggingLibrary` with the `Release` configuration in MSBuild, the resulting lines in the `.nuspec` file in the package is as follows:</span></span>

```xml
<files>
    <file src="bin\Release\LoggingLibrary.pdb" target="lib\net40" />
</files>
```

## <a name="dependencies"></a><span data-ttu-id="ae703-253">Abhängigkeiten</span><span class="sxs-lookup"><span data-stu-id="ae703-253">Dependencies</span></span>

<span data-ttu-id="ae703-254">Das `<dependencies>`-Element in `<metadata>` enthält eine beliebige Anzahl von `<dependency>`-Elementen, die andere Pakete finden, von denen die Pakete auf der obersten Ebene abhängig sind.</span><span class="sxs-lookup"><span data-stu-id="ae703-254">The `<dependencies>` element within `<metadata>` contains any number of `<dependency>` elements that identify other packages upon which the top-level package depends.</span></span> <span data-ttu-id="ae703-255">Im Folgenden werden die Attribute für jede `<dependency>` dargestellt:</span><span class="sxs-lookup"><span data-stu-id="ae703-255">The attributes for each `<dependency>` are as follows:</span></span>

| <span data-ttu-id="ae703-256">Attribut</span><span class="sxs-lookup"><span data-stu-id="ae703-256">Attribute</span></span> | <span data-ttu-id="ae703-257">description</span><span class="sxs-lookup"><span data-stu-id="ae703-257">Description</span></span> |
| --- | --- |
| `id` | <span data-ttu-id="ae703-258">(Erforderlich) Die Paket-ID der Abhängigkeit, z.B. „EntityFramework“ und „NUnit“, die der Name des Pakets „nuget.org“ ist, wird auf einer Paketseite angezeigt.</span><span class="sxs-lookup"><span data-stu-id="ae703-258">(Required) The package ID of the dependency, such as "EntityFramework" and "NUnit", which is the name of the package nuget.org shows on a package page.</span></span> |
| `version` | <span data-ttu-id="ae703-259">(Erforderlich) Der Bereich an Versionen, die als Abhängigkeiten akzeptiert werden.</span><span class="sxs-lookup"><span data-stu-id="ae703-259">(Required) The range of versions acceptable as a dependency.</span></span> <span data-ttu-id="ae703-260">Die genaue Syntax finden Sie unter [Paketversionsverwaltung](../reference/package-versioning.md#version-ranges-and-wildcards).</span><span class="sxs-lookup"><span data-stu-id="ae703-260">See [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards) for exact syntax.</span></span> |
| <span data-ttu-id="ae703-261">include</span><span class="sxs-lookup"><span data-stu-id="ae703-261">include</span></span> | <span data-ttu-id="ae703-262">Eine durch Kommas abgetrennte Liste mit Include/Exclude-Tags (s. Tabelle unten), in der auf die Abhängigkeit verwiesen wird, die in das endgültige Paket eingefügt werden soll.</span><span class="sxs-lookup"><span data-stu-id="ae703-262">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to include in the final package.</span></span> <span data-ttu-id="ae703-263">Der Standardwert ist `none`.</span><span class="sxs-lookup"><span data-stu-id="ae703-263">The default value is `none`.</span></span> |
| <span data-ttu-id="ae703-264">exclude</span><span class="sxs-lookup"><span data-stu-id="ae703-264">exclude</span></span> | <span data-ttu-id="ae703-265">Eine durch Kommas abgetrennte Liste mit Include/Exclude-Tags (s. Tabelle unten), in der auf die Abhängigkeit verwiesen wird, die nicht in das endgültige Paket eingefügt werden soll.</span><span class="sxs-lookup"><span data-stu-id="ae703-265">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to exclude in the final package.</span></span> <span data-ttu-id="ae703-266">Der Standardwert ist `all`.</span><span class="sxs-lookup"><span data-stu-id="ae703-266">The  default value is `all`.</span></span> <span data-ttu-id="ae703-267">`exclude`-Tags haben Vorrang gegenüber `include`-Tags.</span><span class="sxs-lookup"><span data-stu-id="ae703-267">Tags specified with `exclude` take precedence over those specified with `include`.</span></span> <span data-ttu-id="ae703-268">Beispielsweise entspricht `include="runtime, compile" exclude="compile"` `include="runtime"`.</span><span class="sxs-lookup"><span data-stu-id="ae703-268">For example, `include="runtime, compile" exclude="compile"` is the same as `include="runtime"`.</span></span> |

| <span data-ttu-id="ae703-269">Include/Exclude-Tag</span><span class="sxs-lookup"><span data-stu-id="ae703-269">Include/Exclude tag</span></span> | <span data-ttu-id="ae703-270">Betroffene Ordner im Ziel</span><span class="sxs-lookup"><span data-stu-id="ae703-270">Affected folders of the target</span></span> |
| --- | --- |
| <span data-ttu-id="ae703-271">contentFiles</span><span class="sxs-lookup"><span data-stu-id="ae703-271">contentFiles</span></span> | <span data-ttu-id="ae703-272">Inhalt</span><span class="sxs-lookup"><span data-stu-id="ae703-272">Content</span></span>  |
| <span data-ttu-id="ae703-273">Laufzeit</span><span class="sxs-lookup"><span data-stu-id="ae703-273">runtime</span></span> | <span data-ttu-id="ae703-274">Runtime, Ressourcen und Frameworkassemblys</span><span class="sxs-lookup"><span data-stu-id="ae703-274">Runtime, Resources, and FrameworkAssemblies</span></span>  |
| <span data-ttu-id="ae703-275">compile</span><span class="sxs-lookup"><span data-stu-id="ae703-275">compile</span></span> | <span data-ttu-id="ae703-276">lib</span><span class="sxs-lookup"><span data-stu-id="ae703-276">lib</span></span> |
| <span data-ttu-id="ae703-277">Build</span><span class="sxs-lookup"><span data-stu-id="ae703-277">build</span></span> | <span data-ttu-id="ae703-278">Build (MSBuild-Eigenschaften und -Ziele)</span><span class="sxs-lookup"><span data-stu-id="ae703-278">build (MSBuild props and targets)</span></span> |
| <span data-ttu-id="ae703-279">Systemeigen</span><span class="sxs-lookup"><span data-stu-id="ae703-279">native</span></span> | <span data-ttu-id="ae703-280">Systemeigen</span><span class="sxs-lookup"><span data-stu-id="ae703-280">native</span></span> |
| <span data-ttu-id="ae703-281">Keine</span><span class="sxs-lookup"><span data-stu-id="ae703-281">none</span></span> | <span data-ttu-id="ae703-282">Keine Ordner</span><span class="sxs-lookup"><span data-stu-id="ae703-282">No folders</span></span> |
| <span data-ttu-id="ae703-283">alle</span><span class="sxs-lookup"><span data-stu-id="ae703-283">all</span></span> | <span data-ttu-id="ae703-284">Alle Ordner</span><span class="sxs-lookup"><span data-stu-id="ae703-284">All folders</span></span> |

<span data-ttu-id="ae703-285">Beispielsweise verweisen die folgenden Zeilen auf Abhängigkeiten auf `PackageA` Version 1.1.0 und höher und `PackageB` Version 1.x.</span><span class="sxs-lookup"><span data-stu-id="ae703-285">For example, the following lines indicate dependencies on `PackageA` version 1.1.0 or higher, and `PackageB` version 1.x.</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" />
    <dependency id="PackageB" version="[1,2)" />
</dependencies>
```

<span data-ttu-id="ae703-286">In den folgenden Zeilen wird zwar auf Abhängigkeiten von denselben Paketen verwiesen, allerdings wird auch angegeben, dass die Ordner `contentFiles` und `build` von `PackageA` sowie alle anderen Ordner bis auf `native` und `compile` von `PackageB` angegeben werden sollen.</span><span class="sxs-lookup"><span data-stu-id="ae703-286">The following lines indicate dependencies on the same packages, but specify to include the `contentFiles` and `build` folders of `PackageA` and everything but the `native` and `compile` folders of `PackageB`"</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" include="contentFiles, build" />
    <dependency id="PackageB" version="[1,2)" exclude="native, compile" />
</dependencies>
```

<span data-ttu-id="ae703-287">Hinweis: Bei der Erstellung von `.nuspec` mithilfe von `nuget spec` aus einem Projekt werden in diesem Projekt bestehende Abhängigkeiten automatisch in die resultierende `.nuspec`-Datei eingefügt.</span><span class="sxs-lookup"><span data-stu-id="ae703-287">Note: When creating a `.nuspec` from a project using `nuget spec`, dependencies that exist in that project are automatically included in the resulting `.nuspec` file.</span></span>

### <a name="dependency-groups"></a><span data-ttu-id="ae703-288">Abhängigkeitsgruppen</span><span class="sxs-lookup"><span data-stu-id="ae703-288">Dependency groups</span></span>

<span data-ttu-id="ae703-289">*Version 2.0 und höher*</span><span class="sxs-lookup"><span data-stu-id="ae703-289">*Version 2.0+*</span></span>

<span data-ttu-id="ae703-290">Als Alternative zu einer einzelnen flachen Liste können Abhängigkeiten auf der Grundlage des Frameworkprofils des Zielprojekts angegeben werden, das `<group>`-Elemente in `<dependencies>` verwendet.</span><span class="sxs-lookup"><span data-stu-id="ae703-290">As an alternative to a single flat list, dependencies can be specified according to the framework profile of the target project using `<group>` elements within `<dependencies>`.</span></span>

<span data-ttu-id="ae703-291">Jede Gruppe verfügt über ein Attribut mit dem Namen `targetFramework` und enthält entweder kein `<dependency>`-Element oder mindestens eins.</span><span class="sxs-lookup"><span data-stu-id="ae703-291">Each group has an attribute named `targetFramework` and contains zero or more `<dependency>` elements.</span></span> <span data-ttu-id="ae703-292">Diese Abhängigkeiten werden zusammen installiert, wenn das Zielframework kompatibel mit dem Frameworkprofil des Projekts ist.</span><span class="sxs-lookup"><span data-stu-id="ae703-292">Those dependencies are installed together when  the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="ae703-293">Das `<group>`-Element ohne ein `targetFramework`-Attribut wird als Standard- oder Ausweichliste der Abhängigkeiten verwendet.</span><span class="sxs-lookup"><span data-stu-id="ae703-293">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of dependencies.</span></span> <span data-ttu-id="ae703-294">Die genauen Frameworkbezeichner finden Sie unter [Zielframeworks](../schema/target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="ae703-294">See [Target frameworks](../schema/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="ae703-295">Das Gruppenformat kann nicht mit einer flachen Liste vermischt werden.</span><span class="sxs-lookup"><span data-stu-id="ae703-295">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="ae703-296">Im folgenden Beispiel werden verschiedene Variationen des `<group>`-Elements dargestellt:</span><span class="sxs-lookup"><span data-stu-id="ae703-296">The following example shows different variations of the `<group>` element:</span></span>

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

## <a name="explicit-assembly-references"></a><span data-ttu-id="ae703-297">Explizite Assemblyverweise</span><span class="sxs-lookup"><span data-stu-id="ae703-297">Explicit assembly references</span></span>

<span data-ttu-id="ae703-298">Das `<references>`-Element gibt die genauen Assemblyverweise an, auf die das Zielprojekt bei der Verwendung des Pakets verweisen soll.</span><span class="sxs-lookup"><span data-stu-id="ae703-298">The `<references>` element explicitly specifies the assemblies that the target project should reference when using the package.</span></span> <span data-ttu-id="ae703-299">Wenn dieses Element vorhanden ist, fügt NuGet nur Verweise zu den aufgelisteten Assemblys hinzu. Es werden keine Verweise auf andere Assemblys in dem `lib`-Ordner des Pakets hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="ae703-299">When this element is present, NuGet add references to only the listed assemblies; it does not add references for any other assemblies in the package's `lib` folder.</span></span>

<span data-ttu-id="ae703-300">Beispielsweise gibt das folgende `<references>`-Element NuGet die Anweisung, Verweise nur zu `xunit.dll` und `xunit.extensions.dll` hinzuzufügen, wenn zusätzliche Assemblys in dem Paket enthalten sind:</span><span class="sxs-lookup"><span data-stu-id="ae703-300">For example, the following `<references>` element instructs NuGet to add references to only `xunit.dll` and `xunit.extensions.dll` even if there are additional assemblies in the package:</span></span>

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

<span data-ttu-id="ae703-301">In der Regel werden Verweise nur für Assemblys zur Entwurfszeit verwendet.</span><span class="sxs-lookup"><span data-stu-id="ae703-301">Explicit references are typically used for design-time only assemblies.</span></span> <span data-ttu-id="ae703-302">Beispielsweise müssen sich Vertragsassemblys bei der Verwendung von [Codeverträgen](/dotnet/framework/debug-trace-profile/code-contracts) neben den Runtimeassemblys befinden, die sie erweitern, damit Visual Studio sie finden kann. Allerdings muss das Projekt auf die Vertragsassemblys verweisen oder in den `bin`-Ordner des Projekts kopiert werden.</span><span class="sxs-lookup"><span data-stu-id="ae703-302">When using [Code Contracts](/dotnet/framework/debug-trace-profile/code-contracts), for example, contract assemblies need to be next to the runtime assemblies that they augment so that Visual Studio can find them, but the contract assemblies need not be referenced by the project or copied into the project's `bin` folder.</span></span>

<span data-ttu-id="ae703-303">Genauso können explizite Verweise für Komponententestframeworks wie XUnit verwendet werden, in denen sich zwar die Toolsassemblys neben den Runtimeassemblys befinden müssen, jedoch müssen diese nicht als Projektverweise eingefügt werden.</span><span class="sxs-lookup"><span data-stu-id="ae703-303">Similarly, explicit references can be used for unit test frameworks, such as XUnit, which needs its tools assemblies located next to the runtime assemblies, but does not need them included as project references.</span></span>

### <a name="reference-groups"></a><span data-ttu-id="ae703-304">Verweisgruppen</span><span class="sxs-lookup"><span data-stu-id="ae703-304">Reference groups</span></span>

<span data-ttu-id="ae703-305">Als Alternative zu einer einzelnen flachen Liste können Verweise auf der Grundlage des Frameworkprofils des Zielprojekts angegeben werden, das `<group>`-Elemente in `<references>` verwendet.</span><span class="sxs-lookup"><span data-stu-id="ae703-305">As an alternative to a single flat list, references can be specified according to the framework profile of the target project using `<group>` elements within `<references>`.</span></span>

<span data-ttu-id="ae703-306">Jede Gruppe verfügt über ein Attribut mit dem Namen `targetFramework` und enthält entweder kein `<reference>`-Element oder mindestens eins.</span><span class="sxs-lookup"><span data-stu-id="ae703-306">Each group has an attribute named `targetFramework` and contains zero or more `<reference>` elements.</span></span> <span data-ttu-id="ae703-307">Diese Verweise werden einem Projekt hinzugefügt, wenn das Zielframework mit dem Frameworkprofil des Projekts kompatibel ist.</span><span class="sxs-lookup"><span data-stu-id="ae703-307">Those references are added to a project when the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="ae703-308">Das `<group>`-Element ohne ein `targetFramework`-Attribut wird als Standard- oder Ausweichliste der Verweise verwendet.</span><span class="sxs-lookup"><span data-stu-id="ae703-308">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of references.</span></span> <span data-ttu-id="ae703-309">Die genauen Frameworkbezeichner finden Sie unter [Zielframeworks](../schema/target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="ae703-309">See [Target frameworks](../schema/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="ae703-310">Das Gruppenformat kann nicht mit einer flachen Liste vermischt werden.</span><span class="sxs-lookup"><span data-stu-id="ae703-310">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="ae703-311">Im folgenden Beispiel werden verschiedene Variationen des `<group>`-Elements dargestellt:</span><span class="sxs-lookup"><span data-stu-id="ae703-311">The following example shows different variations of the `<group>` element:</span></span>

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

## <a name="framework-assembly-references"></a><span data-ttu-id="ae703-312">Verweise auf Frameworkassemblys</span><span class="sxs-lookup"><span data-stu-id="ae703-312">Framework assembly references</span></span>

<span data-ttu-id="ae703-313">Frameworkassemblys gehören zum .NET Framework und sollten für jeden vorhandenen Computer bereits im globalen Assemblycache vorhanden sein.</span><span class="sxs-lookup"><span data-stu-id="ae703-313">Framework assemblies are those that are part of the .NET framework and should already be in the global assembly cache (GAC) for any given machine.</span></span> <span data-ttu-id="ae703-314">Pakete können sicherstellen, dass die erforderlichen Verweise, falls nötig, dem Projekt hinzugefügt werden, indem es diese Assemblys im `<frameworkAssemblies>`-Element erkennt.</span><span class="sxs-lookup"><span data-stu-id="ae703-314">By identifying those assemblies within the `<frameworkAssemblies>` element, a package can ensure that required references are added to a project in the event that the project doesn't have such references already.</span></span> <span data-ttu-id="ae703-315">Solche Assemblys sind nicht von Anfang an in Paketen enthalten.</span><span class="sxs-lookup"><span data-stu-id="ae703-315">Such assemblies, of course, are not included in a package directly.</span></span>

<span data-ttu-id="ae703-316">Das `<frameworkAssemblies>`-Element enthält entweder kein `<frameworkAssembly>`-Element oder mindestens eins, das die folgenden Attribute angibt:</span><span class="sxs-lookup"><span data-stu-id="ae703-316">The `<frameworkAssemblies>` element contains zero or more `<frameworkAssembly>` elements, each of which specifies the following attributes:</span></span>

| <span data-ttu-id="ae703-317">Attribut</span><span class="sxs-lookup"><span data-stu-id="ae703-317">Attribute</span></span> | <span data-ttu-id="ae703-318">description</span><span class="sxs-lookup"><span data-stu-id="ae703-318">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ae703-319">**assemblyName**</span><span class="sxs-lookup"><span data-stu-id="ae703-319">**assemblyName**</span></span> | <span data-ttu-id="ae703-320">(Erforderlich) Der vollqualifizierte Assemblyname.</span><span class="sxs-lookup"><span data-stu-id="ae703-320">(Required) The fully qualified assembly name.</span></span> |
| <span data-ttu-id="ae703-321">**targetFramework**</span><span class="sxs-lookup"><span data-stu-id="ae703-321">**targetFramework**</span></span> | <span data-ttu-id="ae703-322">(Optional) Gibt das Zielframework an, auf das sich dieser Verweis bezieht.</span><span class="sxs-lookup"><span data-stu-id="ae703-322">(Optional) Specifies the target framework to which this reference applies.</span></span> <span data-ttu-id="ae703-323">Wenn dieses Attribut nicht vorhanden ist, deutet dies darauf hin, dass sich der Verweis auf alle Frameworks bezieht.</span><span class="sxs-lookup"><span data-stu-id="ae703-323">If omitted, indicates that the reference applies to all frameworks.</span></span> <span data-ttu-id="ae703-324">Die genauen Frameworkbezeichner finden Sie unter [Zielframeworks](../schema/target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="ae703-324">See [Target frameworks](../schema/target-frameworks.md) for the exact framework identifiers.</span></span> |

<span data-ttu-id="ae703-325">Im folgenden Beispiel werden Verweise auf `System.Net` für alle Zielframeworks und auf `System.ServiceModel` für ausschließlich .NET Framework 4.0 dargestellt:</span><span class="sxs-lookup"><span data-stu-id="ae703-325">The following example shows a reference to `System.Net` for all target frameworks, and a reference to `System.ServiceModel` for .NET Framework 4.0 only:</span></span>

```xml
<frameworkAssemblies>
    <frameworkAssembly assemblyName="System.Net"  />

    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
</frameworkAssemblies>
```

<a name="specifying-files-to-include-in-the-package"></a>

## <a name="including-assembly-files"></a><span data-ttu-id="ae703-326">Einfügen von Assemblydateien</span><span class="sxs-lookup"><span data-stu-id="ae703-326">Including assembly files</span></span>

<span data-ttu-id="ae703-327">Wenn Sie die unter [Creating a Package (Erstellen eines Pakets)](../create-packages/creating-a-package.md) beschriebenen Anweisungen ausführen, müssen Sie nicht explizit eine Liste mit Dateien in der `.nuspec`-Datei angeben.</span><span class="sxs-lookup"><span data-stu-id="ae703-327">If you follow the conventions described in [Creating a Package](../create-packages/creating-a-package.md), you do not have to explicitly specify a list of files in the `.nuspec` file.</span></span> <span data-ttu-id="ae703-328">Der `nuget pack`-Befehl ruft die benötigten Dateien automatisch ab.</span><span class="sxs-lookup"><span data-stu-id="ae703-328">The `nuget pack` command automatically picks up the necessary files.</span></span>

> [!Important]
> <span data-ttu-id="ae703-329">Wenn ein Paket in einem Projekt installiert wird, fügt NuGet automatisch der DLL des Pakets Assemblyverweise hinzu. Die Verweise, die mit `.resources.dll` benannt sind werden dabei allerdings *nicht* hinzugefügt, da angenommen wird, dass es sich dabei um lokalisierte Satellitenassemblys handelt.</span><span class="sxs-lookup"><span data-stu-id="ae703-329">When a package is installed into a project, NuGet automatically adds assembly references to the package's DLLs, *excluding* those that are named `.resources.dll` because they are assumed to be localized satellite assemblies.</span></span> <span data-ttu-id="ae703-330">Vermeiden Sie aus diesem Grund die Verwendung von `.resources.dll` für Dateien, die darüber hinaus wichtigen Paketcode enthalten.</span><span class="sxs-lookup"><span data-stu-id="ae703-330">For this reason, avoid using `.resources.dll` for files that otherwise contain essential package code.</span></span>

<span data-ttu-id="ae703-331">Legen Sie ein `<files>`-Element als untergeordnetes Element von `<package>` und als gleichgeordnetes Element von `<metadata>` fest, das jeder Datei ein separates `<file>`-Element zuordnet, um diese automatischen Vorgänge zu umgehen und genau zu kontrollieren, welche Dateien in einem Paket enthalten sind.</span><span class="sxs-lookup"><span data-stu-id="ae703-331">To bypass this automatic behavior and explicitly control which files are included in a package, place a `<files>` element as a child of `<package>` (and a sibling of `<metadata>`), identifying each file with a separate `<file>` element.</span></span> <span data-ttu-id="ae703-332">Zum Beispiel:</span><span class="sxs-lookup"><span data-stu-id="ae703-332">For example:</span></span>

```xml
<files>
    <file src="bin\Debug\*.dll" target="lib" />
    <file src="bin\Debug\*.pdb" target="lib" />
    <file src="tools\**\*.*" exclude="**\*.log" />
</files>
```

<span data-ttu-id="ae703-333">Das `<files>`-Element wird bei NuGet 2.x und früher sowie bei Projekten, die `packages.config` verwenden, außerdem verwendet, um unveränderliche Inhaltsdateien während der Paketinstallation einzufügen.</span><span class="sxs-lookup"><span data-stu-id="ae703-333">With NuGet 2.x and earlier, and projects using `packages.config`, the `<files>` element is also used to include immutable content files when a package is installed.</span></span> <span data-ttu-id="ae703-334">Bei NuGet 3.3 und höher und Projekten, die PackageReference verwenden, wird stattdessen das `<contentFiles>`-Element verwendet.</span><span class="sxs-lookup"><span data-stu-id="ae703-334">With NuGet 3.3+ and projects PackageReference, the `<contentFiles>` element is used instead.</span></span> <span data-ttu-id="ae703-335">Weitere Informationen finden Sie unter [Einfügen von Inhaltsdateien](#including-content-files).</span><span class="sxs-lookup"><span data-stu-id="ae703-335">See [Including content files](#including-content-files) below for details.</span></span>

### <a name="file-element-attributes"></a><span data-ttu-id="ae703-336">Dateielementattribute</span><span class="sxs-lookup"><span data-stu-id="ae703-336">File element attributes</span></span>

<span data-ttu-id="ae703-337">Jedes `<file>`-Element gibt die folgenden Attribute an:</span><span class="sxs-lookup"><span data-stu-id="ae703-337">Each `<file>` element specifies the following attributes:</span></span>

| <span data-ttu-id="ae703-338">Attribut</span><span class="sxs-lookup"><span data-stu-id="ae703-338">Attribute</span></span> | <span data-ttu-id="ae703-339">description</span><span class="sxs-lookup"><span data-stu-id="ae703-339">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ae703-340">**src**</span><span class="sxs-lookup"><span data-stu-id="ae703-340">**src**</span></span> | <span data-ttu-id="ae703-341">Der Speicherort der Dateien, die eingefügt werden sollen, unterliegt Ausnahmen, die von dem `exclude`-Attribut angegeben werden.</span><span class="sxs-lookup"><span data-stu-id="ae703-341">The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="ae703-342">Der Pfad ist relativ zur `.nuspec`-Datei, wenn kein absoluter Pfad angegeben ist.</span><span class="sxs-lookup"><span data-stu-id="ae703-342">The path is relative to the `.nuspec` file unless an absolute path is specified.</span></span> <span data-ttu-id="ae703-343">Das Platzhalterzeichen `*` ist zulässig, und das zweifache Platzhalterzeichen `**` impliziert eine rekursive Ordnersuche.</span><span class="sxs-lookup"><span data-stu-id="ae703-343">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="ae703-344">**target**</span><span class="sxs-lookup"><span data-stu-id="ae703-344">**target**</span></span> | <span data-ttu-id="ae703-345">Der relative Pfad zu dem Ordner in dem Paket, in dem die Quelldateien platziert sind, der mit `lib`, `content`, `build` oder `tools` beginnt.</span><span class="sxs-lookup"><span data-stu-id="ae703-345">The relative path to the folder within the package where the source files are placed, which must begin with `lib`, `content`, `build`, or `tools`.</span></span> <span data-ttu-id="ae703-346">Informationen dazu finden Sie unter [Creating a .nuspec from a convention-based working directory (Erstellen einer NUSPEC-Datei aus einem auf Konventionen basierenden Arbeitsverzeichnis)](../Create-Packages/Creating-a-Package.md#from-a-convention-based-working-directory).</span><span class="sxs-lookup"><span data-stu-id="ae703-346">See [Creating a .nuspec from a convention-based working directory](../Create-Packages/Creating-a-Package.md#from-a-convention-based-working-directory).</span></span> |
| <span data-ttu-id="ae703-347">**exclude**</span><span class="sxs-lookup"><span data-stu-id="ae703-347">**exclude**</span></span> | <span data-ttu-id="ae703-348">Eine durch Semikolons abgetrennte Datei oder Dateimuster, die sich nicht im `src`-Speicherort befinden dürfen.</span><span class="sxs-lookup"><span data-stu-id="ae703-348">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="ae703-349">Das Platzhalterzeichen `*` ist zulässig, und das zweifache Platzhalterzeichen `**` impliziert eine rekursive Ordnersuche.</span><span class="sxs-lookup"><span data-stu-id="ae703-349">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |

### <a name="examples"></a><span data-ttu-id="ae703-350">Beispiele</span><span class="sxs-lookup"><span data-stu-id="ae703-350">Examples</span></span>

<span data-ttu-id="ae703-351">**Einzelne Assembly**</span><span class="sxs-lookup"><span data-stu-id="ae703-351">**Single assembly**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="library.dll" target="lib" />

    Packaged result:
        lib\library.dll

<span data-ttu-id="ae703-352">**Einzelne Assembly, die für ein Zielframework spezifisch ist**</span><span class="sxs-lookup"><span data-stu-id="ae703-352">**Single assembly specific to a target framework**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="assemblies\net40\library.dll" target="lib\net40" />

    Packaged result:
        lib\net40\library.dll

<span data-ttu-id="ae703-353">**Mehrere DLLS, die Platzhalterzeichen verwenden**</span><span class="sxs-lookup"><span data-stu-id="ae703-353">**Set of DLLs using a wildcard**</span></span>

    Source files:
        bin\release\libraryA.dll
        bin\release\libraryB.dll

    .nuspec entry:
        <file src="bin\release\*.dll" target="lib" />

    Packaged result:
        lib\libraryA.dll
        lib\libraryB.dll

<span data-ttu-id="ae703-354">**DLLs für verschiedene Frameworks**</span><span class="sxs-lookup"><span data-stu-id="ae703-354">**DLLs for different frameworks**</span></span>

    Source files:
        lib\net40\library.dll
        lib\net20\library.dll

    .nuspec entry (using ** recursive search):
        <file src="lib\**" target="lib" />

    Packaged result:
        lib\net40\library.dll
        lib\net20\library.dll

<span data-ttu-id="ae703-355">**Ausschließen von Dateien**</span><span class="sxs-lookup"><span data-stu-id="ae703-355">**Excluding files**</span></span>

    Source files:
        \tools\*.bak
        \tools\*.log
        \tools\build\*.log

    .nuspec entries:
        <file src="tools\*.*" target="tools" exclude="tools\*.bak" />
        <file src="tools\**\*.*" target="tools" exclude="**\*.log" />

    Package result:
        (no files)

## <a name="including-content-files"></a><span data-ttu-id="ae703-356">Einfügen von Inhaltsdateien</span><span class="sxs-lookup"><span data-stu-id="ae703-356">Including content files</span></span>

<span data-ttu-id="ae703-357">Bei Inhaltsdateien handelt es sich um unveränderliche Dateien, die ein Paket in ein Projekt einfügen muss.</span><span class="sxs-lookup"><span data-stu-id="ae703-357">Content files are immutable files that a package needs to include in a project.</span></span> <span data-ttu-id="ae703-358">Da sie unveränderlich sind, sollen sie auch nicht von dem verarbeitenden Projekt geändert werden.</span><span class="sxs-lookup"><span data-stu-id="ae703-358">Being immutable, they are not intended to be modified by the consuming project.</span></span> <span data-ttu-id="ae703-359">Zu den Inhaltsdateien gehören z.B.:</span><span class="sxs-lookup"><span data-stu-id="ae703-359">Example content files include:</span></span>

- <span data-ttu-id="ae703-360">Bilder, die als Ressourcen eingebettet werden</span><span class="sxs-lookup"><span data-stu-id="ae703-360">Images that are embedded as resources</span></span>
- <span data-ttu-id="ae703-361">Quelldateien, die bereits kompiliert sind</span><span class="sxs-lookup"><span data-stu-id="ae703-361">Source files that are already compiled</span></span>
- <span data-ttu-id="ae703-362">Skripts, die in die Buildausgabe des Projekts eingefügt werden müssen</span><span class="sxs-lookup"><span data-stu-id="ae703-362">Scripts that need to be included with the build output of the project</span></span>
- <span data-ttu-id="ae703-363">Konfigurationsdateien für das Paket, die zwar in das Projekt eingefügt werden müssen, an denen jedoch keine projektspezifischen Änderungen vorgenommen werden müssen.</span><span class="sxs-lookup"><span data-stu-id="ae703-363">Configuration files for the package that need to be included in the project but don't need any project-specific changes</span></span>

<span data-ttu-id="ae703-364">Inhaltsdateien werden in ein Paket eingefügt, das das `<files>`-Element verwendet, das den `content`-Ordner im `target`-Attribut angibt.</span><span class="sxs-lookup"><span data-stu-id="ae703-364">Content files are included in a package using the `<files>` element, specifying the `content` folder in the `target` attribute.</span></span> <span data-ttu-id="ae703-365">Allerdings werden diese Dateien ignoriert, wenn das Paket über PackageReference in ein Projekt installiert wird, das stattdessen das `<contentFiles>`-Element verwendet.</span><span class="sxs-lookup"><span data-stu-id="ae703-365">However, such files are ignored when the package is installed in a project using PackageReference, which instead uses the `<contentFiles>` element.</span></span>

<span data-ttu-id="ae703-366">Im Idealfall geben Pakete die Inhaltsdateien in beiden Elementen an, um ein höchstmögliches Maß an Kompatibilität mit den verarbeitenden Projekten zu erreichen.</span><span class="sxs-lookup"><span data-stu-id="ae703-366">For maximum compatibility with consuming projects, a package ideally specifies the content files in both elements.</span></span>

### <a name="using-the-files-element-for-content-files"></a><span data-ttu-id="ae703-367">Verwenden des Dateielements für Inhaltsdateien</span><span class="sxs-lookup"><span data-stu-id="ae703-367">Using the files element for content files</span></span>

<span data-ttu-id="ae703-368">Verwenden Sie für Inhaltsdateien einfach dasselbe Format wie für Assemblydateien. Geben Sie dabei allerdings `content` als Basisordner im `target`-Attribut an, wie in den folgenden Beispielen dargestellt wird.</span><span class="sxs-lookup"><span data-stu-id="ae703-368">For content files, simply use the same format as for assembly files, but specify `content` as the base folder in the `target` attribute as shown in the following examples.</span></span>

<span data-ttu-id="ae703-369">**Grundlegende Inhaltsdateien**</span><span class="sxs-lookup"><span data-stu-id="ae703-369">**Basic content files**</span></span>

    Source files:
        css\mobile\style1.css
        css\mobile\style2.css

    .nuspec entry:
        <file src="css\mobile\*.css" target="content\css\mobile" />

    Packaged result:
        content\css\mobile\style1.css
        content\css\mobile\style2.css

<span data-ttu-id="ae703-370">**Inhaltsdateien mit Verzeichnisstruktur**</span><span class="sxs-lookup"><span data-stu-id="ae703-370">**Content files with directory structure**</span></span>

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

<span data-ttu-id="ae703-371">**Inhaltsdatei, die für ein Zielframework spezifisch ist**</span><span class="sxs-lookup"><span data-stu-id="ae703-371">**Content file specific to a target framework**</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry
        <file src="css\cool\style.css" target="Content" />

    Packaged result:
        content\style.css

<span data-ttu-id="ae703-372">**Inhaltsdatei, die in einen Ordner mit einem Punkt im Namen kopiert wird**</span><span class="sxs-lookup"><span data-stu-id="ae703-372">**Content file copied to a folder with dot in name**</span></span>

<span data-ttu-id="ae703-373">In diesem Fall erkennt NuGet, dass die Erweiterung in `target` nicht mit der Erweiterung in `src` übereinstimmt, und behandelt dieses Bestandteil des Namens in `target` als einen Ordner:</span><span class="sxs-lookup"><span data-stu-id="ae703-373">In this case, NuGet sees that the extension in `target` does not match the extension in `src` and thus treats that part of the name in `target` as a folder:</span></span>

    Source file:
        images\picture.png

    .nuspec entry:
        <file src="images\picture.png" target="Content\images\package.icons" />

    Packaged result:
        content\images\package.icons\picture.png

<span data-ttu-id="ae703-374">**Inhaltsdateien ohne Erweiterungen**</span><span class="sxs-lookup"><span data-stu-id="ae703-374">**Content files without extensions**</span></span>

<span data-ttu-id="ae703-375">Verwenden Sie die Platzhalterzeichen `*` oder `**`, um Dateien ohne Erweiterungen einzufügen:</span><span class="sxs-lookup"><span data-stu-id="ae703-375">To include files without an extension, use the `*` or `**` wildcards:</span></span>

    Source file:
        flags\installed

    .nuspec entry:
        <file src="flags\**" target="flags" />

    Packaged result:
        flags\installed

<span data-ttu-id="ae703-376">**Inhaltsdateien mit tiefen Pfaden und tiefen Zielen**</span><span class="sxs-lookup"><span data-stu-id="ae703-376">**Content files with deep path and deep target**</span></span>

<span data-ttu-id="ae703-377">In diesem Fall nimmt NuGet an, dass das Ziel ein Dateiname und kein Ordner ist, da die Dateierweiterungen von Quelle und Ziel übereinstimmen:</span><span class="sxs-lookup"><span data-stu-id="ae703-377">In this case, because the file extensions of the source and target match, NuGet assumes that the target is a file name and not a folder:</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry:
        <file src="css\cool\style.css" target="Content\css\cool" />
        or:
        <file src="css\cool\style.css" target="Content\css\cool\style.css" />

    Packaged result:
        content\css\cool\style.css

<span data-ttu-id="ae703-378">**Umbenennen einer Inhaltsdatei im Paket**</span><span class="sxs-lookup"><span data-stu-id="ae703-378">**Renaming a content file in the package**</span></span>

    Source file:
        ie\css\style.css

    .nuspec entry:
        <file src="ie\css\style.css" target="Content\css\ie.css" />

    Packaged result:
        content\css\ie.css

<span data-ttu-id="ae703-379">**Ausschließen von Dateien**</span><span class="sxs-lookup"><span data-stu-id="ae703-379">**Excluding files**</span></span>

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

### <a name="using-the-contentfiles-element-for-content-files"></a><span data-ttu-id="ae703-380">Verwenden des contentFiles-Elements für Inhaltsdateien</span><span class="sxs-lookup"><span data-stu-id="ae703-380">Using the contentFiles element for content files</span></span>

<span data-ttu-id="ae703-381">*NuGet 4.0 und höher mit PackageReference*</span><span class="sxs-lookup"><span data-stu-id="ae703-381">*NuGet 4.0+ with PackageReference*</span></span>

<span data-ttu-id="ae703-382">Standardmäßig platzieren Pakete Inhalte in einem `contentFiles`-Ordner (s. unten), in den `nuget pack` alle Dateien mithilfe von Standardattributen eingefügt hat.</span><span class="sxs-lookup"><span data-stu-id="ae703-382">By default, a package places content in a `contentFiles` folder (see below) and `nuget pack` included all files in that folder using default attributes.</span></span> <span data-ttu-id="ae703-383">In diesem Fall ist es nicht notwendig, einen `contentFiles`-Knoten in `.nuspec` einzufügen.</span><span class="sxs-lookup"><span data-stu-id="ae703-383">In this case it's not necessary to include a `contentFiles` node in the `.nuspec` at all.</span></span>

<span data-ttu-id="ae703-384">Das `<contentFiles>`-Element gibt eine Auflistung von `<files>`-Elementen an, die die eingefügten Dateien erkennen, um zu kontrollieren, welche Dateien eingefügt wurden.</span><span class="sxs-lookup"><span data-stu-id="ae703-384">To control which files are included, the `<contentFiles>` element specifies is a collection of `<files>` elements that identify the exact files include.</span></span>

<span data-ttu-id="ae703-385">Diese Dateien werden zusammen mit mehreren Attributen angegeben, die beschreiben, wie sie in dem Projektsystem verwendet werden sollen:</span><span class="sxs-lookup"><span data-stu-id="ae703-385">These files are specified with a set of attributes that describe how they should be used within the project system:</span></span>

| <span data-ttu-id="ae703-386">Attribut</span><span class="sxs-lookup"><span data-stu-id="ae703-386">Attribute</span></span> | <span data-ttu-id="ae703-387">description</span><span class="sxs-lookup"><span data-stu-id="ae703-387">Description</span></span> |
| --- | --- |
| <span data-ttu-id="ae703-388">**include**</span><span class="sxs-lookup"><span data-stu-id="ae703-388">**include**</span></span> | <span data-ttu-id="ae703-389">(Erforderlich) Der Speicherort der Dateien, die eingefügt werden sollen, unterliegt Ausnahmen, die von dem `exclude`-Attribut angegeben werden.</span><span class="sxs-lookup"><span data-stu-id="ae703-389">(Required) The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="ae703-390">Der Pfad ist relativ zur `.nuspec`-Datei, wenn kein absoluter Pfad angegeben ist.</span><span class="sxs-lookup"><span data-stu-id="ae703-390">The path is relative to the `.nuspec` file unless an absolute path is specified.</span></span> <span data-ttu-id="ae703-391">Das Platzhalterzeichen `*` ist zulässig, und das zweifache Platzhalterzeichen `**` impliziert eine rekursive Ordnersuche.</span><span class="sxs-lookup"><span data-stu-id="ae703-391">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="ae703-392">**exclude**</span><span class="sxs-lookup"><span data-stu-id="ae703-392">**exclude**</span></span> | <span data-ttu-id="ae703-393">Eine durch Semikolons abgetrennte Datei oder Dateimuster, die sich nicht im `src`-Speicherort befinden dürfen.</span><span class="sxs-lookup"><span data-stu-id="ae703-393">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="ae703-394">Das Platzhalterzeichen `*` ist zulässig, und das zweifache Platzhalterzeichen `**` impliziert eine rekursive Ordnersuche.</span><span class="sxs-lookup"><span data-stu-id="ae703-394">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="ae703-395">**buildAction**</span><span class="sxs-lookup"><span data-stu-id="ae703-395">**buildAction**</span></span> | <span data-ttu-id="ae703-396">Die Buildaktion, die dem Inhaltselement für MSBuild zugewiesen werden soll. Z.B. `Content`, `None`, `Embedded Resource` oder `Compile`. Die Standardeinstellung ist `Compile`.</span><span class="sxs-lookup"><span data-stu-id="ae703-396">The build action to assign to the content item for MSBuild, such as `Content`, `None`, `Embedded Resource`, `Compile`, etc. The default is `Compile`.</span></span> |
| <span data-ttu-id="ae703-397">**copyToOutput**</span><span class="sxs-lookup"><span data-stu-id="ae703-397">**copyToOutput**</span></span> | <span data-ttu-id="ae703-398">Ein boolescher Wert, der angibt, ob Inhaltselemente in den Ausgabeordner des Builds kopiert werden sollen.</span><span class="sxs-lookup"><span data-stu-id="ae703-398">A Boolean indicating whether to copy content items to the build output folder.</span></span> <span data-ttu-id="ae703-399">Der Standardwert ist false.</span><span class="sxs-lookup"><span data-stu-id="ae703-399">The default is false.</span></span> |
| <span data-ttu-id="ae703-400">**flatten**</span><span class="sxs-lookup"><span data-stu-id="ae703-400">**flatten**</span></span> | <span data-ttu-id="ae703-401">Ein boolescher Wert, der angibt, ob Inhaltselemente in einen Ordner in der Buildausgabe kopiert werden sollen (TRUE) oder ob die Ordnerstruktur in den Paketen beibehalten werden soll (FALSE).</span><span class="sxs-lookup"><span data-stu-id="ae703-401">A Boolean indicating whether to copy content items to a single folder in the build output (true), or to preserve the folder structure in the package (false).</span></span> <span data-ttu-id="ae703-402">Diese Flag funktioniert nur, wenn das copyToOutput-Flag auf TRUE festgelegt ist.</span><span class="sxs-lookup"><span data-stu-id="ae703-402">This flag only works when copyToOutput flag is set to true.</span></span> <span data-ttu-id="ae703-403">Der Standardwert ist false.</span><span class="sxs-lookup"><span data-stu-id="ae703-403">The default is false.</span></span> |

<span data-ttu-id="ae703-404">NuGet wendet die untergeordneten Elemente von `<contentFiles>` bei der Installation eines Pakets von unten nach oben an.</span><span class="sxs-lookup"><span data-stu-id="ae703-404">When installing a package, NuGet applies the child elements of `<contentFiles>` from top to bottom.</span></span> <span data-ttu-id="ae703-405">Wenn mehrere Einträge in einer Datei vorhanden sind, werden sie alle angewendet.</span><span class="sxs-lookup"><span data-stu-id="ae703-405">If multiple entries match the same file then all entries are applied.</span></span> <span data-ttu-id="ae703-406">Der höher geordnete Eintrag setzt die untergeordneten Einträge außer Kraft, wenn ein Konflikt für ein Attribut entsteht.</span><span class="sxs-lookup"><span data-stu-id="ae703-406">The top-most entry overrides the lower entries if there is a conflict for the same attribute.</span></span>

#### <a name="package-folder-structure"></a><span data-ttu-id="ae703-407">Paketordnerstruktur</span><span class="sxs-lookup"><span data-stu-id="ae703-407">Package folder structure</span></span>

<span data-ttu-id="ae703-408">Das Paketprojekt sollte Inhalte mithilfe des folgenden Musters strukturieren:</span><span class="sxs-lookup"><span data-stu-id="ae703-408">The package project should structure content using the following pattern:</span></span>

    /contentFiles/{codeLanguage}/{TxM}/{any?}

- <span data-ttu-id="ae703-409">`codeLanguages` kann `cs`, `vb`, `fs`, `any` oder das klein geschriebene Äquivalent einer `$(ProjectLanguage)` sein.</span><span class="sxs-lookup"><span data-stu-id="ae703-409">`codeLanguages` may be `cs`, `vb`, `fs`, `any`, or the lowercase equivalent of a given `$(ProjectLanguage)`</span></span>
- <span data-ttu-id="ae703-410">`TxM` ist ein für das Zielframework zulässiger Moniker, der NuGet unterstützt (Informationen dazu finden Sie unter [Zielframeworks](../schema/target-frameworks.md)).</span><span class="sxs-lookup"><span data-stu-id="ae703-410">`TxM` is any legal target framework moniker that NuGet supports (see [Target frameworks](../schema/target-frameworks.md)).</span></span>
- <span data-ttu-id="ae703-411">An das Ende der Syntax kann eine beliebige Ordnerstruktur angehängt werden.</span><span class="sxs-lookup"><span data-stu-id="ae703-411">Any folder structure may be appended to the end of this syntax.</span></span>

<span data-ttu-id="ae703-412">Zum Beispiel:</span><span class="sxs-lookup"><span data-stu-id="ae703-412">For example:</span></span>

    Language- and framework-agnostic:
        /contentFiles/any/any/config.xml

    net45 content for all languages
        /contentFiles/any/net45/config.xml

    C#-specific content for net45 and up
        /contentFiles/cs/net45/sample.cs

<span data-ttu-id="ae703-413">Für leere Ordner kann `.` eingefügt werden, wenn diese keine Inhalte mehr für bestimmte Sprachen und TxM bereitstellen sollen. Z.B.:</span><span class="sxs-lookup"><span data-stu-id="ae703-413">Empty folders can use `.` to opt out of providing content for certain combinations of language and TxM, for example:</span></span>

    /contentFiles/vb/any/code.vb
    /contentFiles/cs/any/.

#### <a name="example-contentfiles-section"></a><span data-ttu-id="ae703-414">Beispiel: Abschnitt „contentFiles“</span><span class="sxs-lookup"><span data-stu-id="ae703-414">Example contentFiles section</span></span>

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

## <a name="example-nuspec-files"></a><span data-ttu-id="ae703-415">Beispiel: NUSPEC-Dateien</span><span class="sxs-lookup"><span data-stu-id="ae703-415">Example .nuspec files</span></span>

<span data-ttu-id="ae703-416">**Eine einfache `.nuspec`-Datei, die weder Abhängigkeiten noch Dateien enthält**</span><span class="sxs-lookup"><span data-stu-id="ae703-416">**A simple `.nuspec` that does not specify dependencies or files**</span></span>

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

<span data-ttu-id="ae703-417">**Eine `.nuspec`-Datei mit Abhängigkeiten**</span><span class="sxs-lookup"><span data-stu-id="ae703-417">**A `.nuspec` with dependencies**</span></span>

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

<span data-ttu-id="ae703-418">**Eine `.nuspec`-Datei mit Dateien**</span><span class="sxs-lookup"><span data-stu-id="ae703-418">**A `.nuspec` with files**</span></span>

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

<span data-ttu-id="ae703-419">**Eine `.nuspec`-Datei mit Frameworkassemblys**</span><span class="sxs-lookup"><span data-stu-id="ae703-419">**A `.nuspec` with framework assemblies**</span></span>

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

<span data-ttu-id="ae703-420">In diesem Beispiel werden die folgenden Elemente für bestimmte Projektziele installiert:</span><span class="sxs-lookup"><span data-stu-id="ae703-420">In this example, the following are installed for specific project targets:</span></span>

- <span data-ttu-id="ae703-421">.NET4: `System.Web` und `System.Net`</span><span class="sxs-lookup"><span data-stu-id="ae703-421">.NET4 -> `System.Web`, `System.Net`</span></span>
- <span data-ttu-id="ae703-422">.NET4-Clientprofil: `System.Net`</span><span class="sxs-lookup"><span data-stu-id="ae703-422">.NET4 Client Profile -> `System.Net`</span></span>
- <span data-ttu-id="ae703-423">Silverlight 3: `System.Json`</span><span class="sxs-lookup"><span data-stu-id="ae703-423">Silverlight 3 -> `System.Json`</span></span>
- <span data-ttu-id="ae703-424">Silverlight 4: `System.Windows.Controls.DomainServices`</span><span class="sxs-lookup"><span data-stu-id="ae703-424">Silverlight 4 -> `System.Windows.Controls.DomainServices`</span></span>
- <span data-ttu-id="ae703-425">WindowsPhone: `Microsoft.Devices.Sensors`</span><span class="sxs-lookup"><span data-stu-id="ae703-425">WindowsPhone -> `Microsoft.Devices.Sensors`</span></span>
