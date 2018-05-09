---
title: .NuSpec-Dateiverweis für NuGet
description: Die NUSPEC-Datei enthält Paketmetadaten, die bei der Erstellung eines Pakets verwendet werden, um für die Paketbenutzer Informationen bereitzustellen.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 08/29/2017
ms.topic: reference
ms.reviewer: anangaur
ms.openlocfilehash: c11b50aa1637c00f0f0e71a6e20ce5d435db402b
ms.sourcegitcommit: a6ca160b1e7e5c58b135af4eba0e9463127a59e8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/28/2018
---
# <a name="nuspec-reference"></a><span data-ttu-id="1b5bd-103">NUSPEC-Referenz</span><span class="sxs-lookup"><span data-stu-id="1b5bd-103">.nuspec reference</span></span>

<span data-ttu-id="1b5bd-104">Bei einer `.nuspec`-Datei handelt es sich um eine XML-Manifestdatei, die Paketmetadaten enthält.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-104">A `.nuspec` file is an XML manifest that contains package metadata.</span></span> <span data-ttu-id="1b5bd-105">Diese Manifestdatei wird sowohl für die Erstellung des Pakets als auch zur Bereitstellung von Informationen für die Benutzer verwendet.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-105">This manifest is used both to build the package and to provide information to consumers.</span></span> <span data-ttu-id="1b5bd-106">Manifestdateien sind in allen Paketen enthalten.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-106">The manifest is always included in a package.</span></span>

<span data-ttu-id="1b5bd-107">In diesem Thema:</span><span class="sxs-lookup"><span data-stu-id="1b5bd-107">In this topic:</span></span>

- [<span data-ttu-id="1b5bd-108">Allgemeine Form und Schema</span><span class="sxs-lookup"><span data-stu-id="1b5bd-108">General form and schema</span></span>](#general-form-and-schema)
- <span data-ttu-id="1b5bd-109">[Ersetzungstokens](#replacement-tokens) (bei der Verwendung in einem Visual Studio-Projekt)</span><span class="sxs-lookup"><span data-stu-id="1b5bd-109">[Replacement tokens](#replacement-tokens) (when used with a Visual Studio project)</span></span>
- [<span data-ttu-id="1b5bd-110">Abhängigkeiten</span><span class="sxs-lookup"><span data-stu-id="1b5bd-110">Dependencies</span></span>](#dependencies)
- [<span data-ttu-id="1b5bd-111">Explizite Assemblyverweise</span><span class="sxs-lookup"><span data-stu-id="1b5bd-111">Explicit assembly references</span></span>](#explicit-assembly-references)
- [<span data-ttu-id="1b5bd-112">Verweise auf Frameworkassemblys</span><span class="sxs-lookup"><span data-stu-id="1b5bd-112">Framework assembly references</span></span>](#framework-assembly-references)
- [<span data-ttu-id="1b5bd-113">Einfügen von Assemblydateien</span><span class="sxs-lookup"><span data-stu-id="1b5bd-113">Including assembly files</span></span>](#including-assembly-files)
- [<span data-ttu-id="1b5bd-114">Einfügen von Inhaltsdateien</span><span class="sxs-lookup"><span data-stu-id="1b5bd-114">Including content files</span></span>](#including-content-files)
- [<span data-ttu-id="1b5bd-115">Beispiele</span><span class="sxs-lookup"><span data-stu-id="1b5bd-115">Examples</span></span>](#examples)

## <a name="general-form-and-schema"></a><span data-ttu-id="1b5bd-116">Allgemeine Form und Schema</span><span class="sxs-lookup"><span data-stu-id="1b5bd-116">General form and schema</span></span>

<span data-ttu-id="1b5bd-117">Die aktuelle `nuspec.xsd`-Schemadatei finden Sie im [NuGet GitHub-Repository](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span><span class="sxs-lookup"><span data-stu-id="1b5bd-117">The current `nuspec.xsd` schema file can be found in the [NuGet GitHub repository](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Packaging/compiler/resources/nuspec.xsd).</span></span>

<span data-ttu-id="1b5bd-118">Für dieses Schema gilt die im Folgenden dargestellte allgemeine Form für die `.nuspec`-Datei:</span><span class="sxs-lookup"><span data-stu-id="1b5bd-118">Within this schema, a `.nuspec` file has the following general form:</span></span>

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

<span data-ttu-id="1b5bd-119">Für eine übersichtliche Darstellung des Schemas öffnen Sie die Schemadatei im Entwurfsmodus in Visual Studio, und klicken Sie auf den Link **XML-Schema-Explorer**.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-119">For a clear visual representation of the schema, open the schema file in Visual Studio in Design mode and click on the **XML Schema Explorer** link.</span></span> <span data-ttu-id="1b5bd-120">Alternativ können Sie auch die Datei als Code öffnen, mit der rechten Maustaste in den Editor klicken und **Show XML Schema Explorer** (XML-Schema-Explorer anzeigen) auswählen.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-120">Alternately, open the file as code, right-click in the editor, and select **Show XML Schema Explorer**.</span></span> <span data-ttu-id="1b5bd-121">In beiden Fällen wird eine Ansicht zurückgegeben, die der in der folgenden Abbildung ähnlich ist, wenn Sie größtenteils erweitert ist:</span><span class="sxs-lookup"><span data-stu-id="1b5bd-121">Either way you get a view like the one below (when mostly expanded):</span></span>

![Visual Studio-Schema-Explorer mit geöffneter „nuspec.xsd“-Datei](media/SchemaExplorer.png)

### <a name="metadata-attributes"></a><span data-ttu-id="1b5bd-123">Metadatenattribute</span><span class="sxs-lookup"><span data-stu-id="1b5bd-123">Metadata attributes</span></span>

<span data-ttu-id="1b5bd-124">Das `<metadata>`-Element unterstützt die in der folgenden Tabelle beschriebenen Attribute.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-124">The `<metadata>` element supports the attributes described in the following table.</span></span>

| <span data-ttu-id="1b5bd-125">Attribut</span><span class="sxs-lookup"><span data-stu-id="1b5bd-125">Attribute</span></span> | <span data-ttu-id="1b5bd-126">Erforderlich</span><span class="sxs-lookup"><span data-stu-id="1b5bd-126">Required</span></span> | <span data-ttu-id="1b5bd-127">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="1b5bd-127">Description</span></span> |
| --- | --- | --- | 
| <span data-ttu-id="1b5bd-128">**minClientVersion**</span><span class="sxs-lookup"><span data-stu-id="1b5bd-128">**minClientVersion**</span></span> | <span data-ttu-id="1b5bd-129">Nein</span><span class="sxs-lookup"><span data-stu-id="1b5bd-129">No</span></span> | <span data-ttu-id="1b5bd-130">Gibt die minimale Version des NuGet-Clients an, der dieses Paket installieren kann. Dies wird von nuget.exe und dem Paket-Manager von Visual Studio erzwungen.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-130">Specifies the minimum version of the NuGet client that can install this package, enforced by nuget.exe and the Visual Studio Package Manager.</span></span> <span data-ttu-id="1b5bd-131">Dieses Attribut wird verwendet, wenn das Paket von bestimmten Funktionen der `.nuspec`-Datei abhängig ist, die in einer bestimmten Version des NuGet-Clients hinzugefügt wurden.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-131">This is used whenever the package depends on specific features of the `.nuspec` file that were added in a particular version of the NuGet client.</span></span> <span data-ttu-id="1b5bd-132">Beispielsweise sollte ein Paket, das das `developmentDependency`-Attribut verwendet, „2.8“ für `minClientVersion` angeben.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-132">For example, a package using the `developmentDependency` attribute should specify "2.8" for `minClientVersion`.</span></span> <span data-ttu-id="1b5bd-133">Genauso sollte ein Paket, das das `contentFiles`-Element verwendet (vgl. nächster Abschnitt), `minClientVersion` auf „3.3“ festlegen.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-133">Similarly, a package using the `contentFiles` element (see the next section) should set `minClientVersion` to "3.3".</span></span> <span data-ttu-id="1b5bd-134">Beachten Sie außerdem, dass NuGet-Clients vor Version 2.5 diese Kennzeichnung nicht erkennen und daher die Installation des Pakets, unabhängig vom Inhalt von `minClientVersion`, *immer* verweigern.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-134">Note also that because NuGet clients prior to 2.5 do not recognize this flag, they *always* refuse to install the package no matter what `minClientVersion` contains.</span></span> |

### <a name="required-metadata-elements"></a><span data-ttu-id="1b5bd-135">Erforderliche Metadatenelemente</span><span class="sxs-lookup"><span data-stu-id="1b5bd-135">Required metadata elements</span></span>

<span data-ttu-id="1b5bd-136">Obwohl es sich bei den folgenden Elementen um die Mindestanforderungen für ein Paket handelt, sollten Sie in Erwägung ziehen, die [optionalen Metadatenelemente](#optional-metadata-elements) hinzuzufügen, damit Entwicklern die Arbeit mit Ihren Paketen erleichtert wird.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-136">Although the following elements are the minimum requirements for a package, you should consider adding the [optional metadata elements](#optional-metadata-elements) to improve the overall experience developers have with your package.</span></span>

<span data-ttu-id="1b5bd-137">Diese Elemente müssen in einem `<metadata>`-Element angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-137">These elements must appear within a `<metadata>` element.</span></span>

| <span data-ttu-id="1b5bd-138">Element</span><span class="sxs-lookup"><span data-stu-id="1b5bd-138">Element</span></span> | <span data-ttu-id="1b5bd-139">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="1b5bd-139">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1b5bd-140">**ID**</span><span class="sxs-lookup"><span data-stu-id="1b5bd-140">**id**</span></span> | <span data-ttu-id="1b5bd-141">Der Paketbezeichner, der die Groß- und Kleinschreibung nicht berücksichtigt und auf nuget.org oder im für das Paket verwendeten Katalog eindeutig sein muss.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-141">The case-insensitive package identifier, which must be unique across nuget.org or whatever gallery the package resides in.</span></span> <span data-ttu-id="1b5bd-142">IDs dürfen keine Leerzeichen oder für eine URL unzulässige Zeichen enthalten. Sie müssen den Regeln für .NET-Namespaces entsprechen.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-142">IDs may not contain spaces or characters that are not valid for a URL, and generally follow .NET namespace rules.</span></span> <span data-ttu-id="1b5bd-143">Informationen finden Sie unter [Choosing a unique package identifier (Auswählen eines eindeutigen Paketbezeichners)](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number).</span><span class="sxs-lookup"><span data-stu-id="1b5bd-143">See [Choosing a unique package identifier](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number) for guidance.</span></span> |
| <span data-ttu-id="1b5bd-144">**version**</span><span class="sxs-lookup"><span data-stu-id="1b5bd-144">**version**</span></span> | <span data-ttu-id="1b5bd-145">Die Version des Pakets, die dem Muster *Hauptversion.Nebenversion.Patch* folgt.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-145">The version of the package, following the *major.minor.patch* pattern.</span></span> <span data-ttu-id="1b5bd-146">Versionsnummern enthalten möglicherweise, wie unter [Paketversionsverwaltung](../reference/package-versioning.md#pre-release-versions) beschrieben, ein Suffix der Vorabversion.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-146">Version numbers may include a pre-release suffix as described in [Package versioning](../reference/package-versioning.md#pre-release-versions).</span></span> |
| <span data-ttu-id="1b5bd-147">**Beschreibung**</span><span class="sxs-lookup"><span data-stu-id="1b5bd-147">**description**</span></span> | <span data-ttu-id="1b5bd-148">Eine ausführliche Beschreibung des Pakets für die Anzeige der Benutzeroberfläche.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-148">A long description of the package for UI display.</span></span> |
| <span data-ttu-id="1b5bd-149">**authors**</span><span class="sxs-lookup"><span data-stu-id="1b5bd-149">**authors**</span></span> | <span data-ttu-id="1b5bd-150">Eine durch Kommas getrennte Liste der Paketautoren, die mit Profilnamen unter nuget.org übereinstimmen. Diese werden im NuGet-Katalog unter nuget.org angezeigt und werden verwendet, um Querverweise auf Pakete von den gleichen Autoren zu geben.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-150">A comma-separated list of packages authors, matching the profile names on nuget.org. These are displayed in the NuGet Gallery on nuget.org and are used to cross-reference packages by the same authors.</span></span> |

### <a name="optional-metadata-elements"></a><span data-ttu-id="1b5bd-151">Optionale Metadatenelemente</span><span class="sxs-lookup"><span data-stu-id="1b5bd-151">Optional metadata elements</span></span>

<span data-ttu-id="1b5bd-152">Diese Elemente auftreten in einem `<metadata>`-Element angezeigt werden.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-152">These elements may appear within a `<metadata>` element.</span></span>

#### <a name="single-elements"></a><span data-ttu-id="1b5bd-153">Einzelne Elemente</span><span class="sxs-lookup"><span data-stu-id="1b5bd-153">Single elements</span></span>

| <span data-ttu-id="1b5bd-154">Element</span><span class="sxs-lookup"><span data-stu-id="1b5bd-154">Element</span></span> | <span data-ttu-id="1b5bd-155">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="1b5bd-155">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1b5bd-156">**title**</span><span class="sxs-lookup"><span data-stu-id="1b5bd-156">**title**</span></span> | <span data-ttu-id="1b5bd-157">Ein benutzerfreundlicher Titel des Pakets, der in der Regel in der Benutzeroberfläche wie auf nuget.org angezeigt wird und der Paket-Manager in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-157">A human-friendly title of the package, typically used in UI displays as on nuget.org and the Package Manager in Visual Studio.</span></span> <span data-ttu-id="1b5bd-158">Wenn nicht angegeben, wird die Paket-ID verwendet.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-158">If not specified, the package ID is used.</span></span> |
| <span data-ttu-id="1b5bd-159">**owners**</span><span class="sxs-lookup"><span data-stu-id="1b5bd-159">**owners**</span></span> | <span data-ttu-id="1b5bd-160">Eine durch Kommas getrennte Liste der Paketersteller, die auf nuget.org Profilnamen verwenden. Dabei handelt es sich häufig um dieselbe Liste wie in `authors`. Sie wird beim Hochladen der Pakete auf nuget.org ignoriert. Informationen dazu finden Sie unter [Managing package owners on nuget.org (Verwalten von Paketbesitzern auf nuget.org)](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg).</span><span class="sxs-lookup"><span data-stu-id="1b5bd-160">A comma-separated list of the package creators using profile names on nuget.org. This is often the same list as in `authors`, and is ignored when uploading the package to nuget.org. See [Managing package owners on nuget.org](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg).</span></span> |
| <span data-ttu-id="1b5bd-161">**projectUrl**</span><span class="sxs-lookup"><span data-stu-id="1b5bd-161">**projectUrl**</span></span> | <span data-ttu-id="1b5bd-162">Eine URL für die Paket-Homepage, häufig auf der Benutzeroberfläche sowie auf nuget.org angezeigt.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-162">A URL for the package's home page, often shown in UI displays as well as nuget.org.</span></span> |
| <span data-ttu-id="1b5bd-163">**licenseUrl**</span><span class="sxs-lookup"><span data-stu-id="1b5bd-163">**licenseUrl**</span></span> | <span data-ttu-id="1b5bd-164">Eine URL für die Paketlizenz, häufig auf der Benutzeroberfläche sowie auf nuget.org angezeigt.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-164">A URL for the package's license, often shown in UI displays as well as nuget.org.</span></span> |
| <span data-ttu-id="1b5bd-165">**iconUrl**</span><span class="sxs-lookup"><span data-stu-id="1b5bd-165">**iconUrl**</span></span> | <span data-ttu-id="1b5bd-166">Eine URL für ein 64x64-Bild mit transparentem Hintergrund, das als Symbol für das Paket in der Benutzeroberfläche verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-166">A URL for a 64x64 image with transparency background to use as the icon for the package in UI display.</span></span> <span data-ttu-id="1b5bd-167">Stellen Sie sicher, dass dieses Element die *direkte Bild-URL* und nicht nur die URL einer Webseite enthält, die das Bild enthält.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-167">Be sure this element contains the *direct image URL* and not the URL of a web page containing the image.</span></span> <span data-ttu-id="1b5bd-168">Z. B. um ein Bild von GitHub verwenden zu können, verwenden die Rohdatendatei URL wie  <em>https://github.com/ \<Benutzername\>/\<Repository\>/raw/\<Verzweigung\> / \<"Logo.png"\></em>.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-168">For example, to use an image from GitHub, use the raw file URL like <em>https://github.com/\<username\>/\<repository\>/raw/\<branch\>/\<logo.png\></em>.</span></span> |
| <span data-ttu-id="1b5bd-169">**requireLicenseAcceptance**</span><span class="sxs-lookup"><span data-stu-id="1b5bd-169">**requireLicenseAcceptance**</span></span> | <span data-ttu-id="1b5bd-170">Ein boolescher Wert, der angibt, ob der Client den Benutzer dazu auffordern muss, die Paketlizenz vor der Installation des Pakets zu akzeptieren.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-170">A Boolean value specifying whether the client must prompt the consumer to accept the package license before installing the package.</span></span> |
| <span data-ttu-id="1b5bd-171">**developmentDependency**</span><span class="sxs-lookup"><span data-stu-id="1b5bd-171">**developmentDependency**</span></span> | <span data-ttu-id="1b5bd-172">*(2.8 und höher)* Ein boolescher Wert, der angibt, ob das Paket mit einer Abhängigkeit markiert werden soll, die nur für die Entwicklung gilt, wodurch vermieden wird, dass das Paket als Abhängigkeit in andere Pakete eingefügt wird.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-172">*(2.8+)* A Boolean value specifying whether the package is be marked as a development-only-dependency, which prevents the package from being included as a dependency in other packages.</span></span> |
| <span data-ttu-id="1b5bd-173">**summary**</span><span class="sxs-lookup"><span data-stu-id="1b5bd-173">**summary**</span></span> | <span data-ttu-id="1b5bd-174">Eine kurze Beschreibung des Pakets für die Anzeige der Benutzeroberfläche.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-174">A short description of the package for UI display.</span></span> <span data-ttu-id="1b5bd-175">Wenn diese nicht angegeben wird, wird eine gekürzte Version von `description` verwendet.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-175">If omitted, a truncated version of `description` is used.</span></span> |
| <span data-ttu-id="1b5bd-176">**releaseNotes**</span><span class="sxs-lookup"><span data-stu-id="1b5bd-176">**releaseNotes**</span></span> | <span data-ttu-id="1b5bd-177">*(1.5 und höher)* Eine Beschreibung der in diesem Release des Pakets enthaltenen Änderungen, die häufig in Benutzeroberflächen wie der Registerkarte **Updates** des Visual Studio-Paket-Managers anstelle von Paketbeschreibungen verwendet wird.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-177">*(1.5+)* A description of the changes made in this release of the package, often used in UI like the **Updates** tab of the Visual Studio Package Manager in place of the package description.</span></span> |
| <span data-ttu-id="1b5bd-178">**copyright**</span><span class="sxs-lookup"><span data-stu-id="1b5bd-178">**copyright**</span></span> | <span data-ttu-id="1b5bd-179">*(1.5 und höher)* Copyright-Informationen zum Paket.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-179">*(1.5+)* Copyright details for the package.</span></span> |
| <span data-ttu-id="1b5bd-180">**language**</span><span class="sxs-lookup"><span data-stu-id="1b5bd-180">**language**</span></span> | <span data-ttu-id="1b5bd-181">Die Gebietsschema-ID des Pakets.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-181">The locale ID for the package.</span></span> <span data-ttu-id="1b5bd-182">Informationen dazu finden Sie unter [Creating localized packages (Erstellen von lokalisierten Paketen)](../create-packages/creating-localized-packages.md).</span><span class="sxs-lookup"><span data-stu-id="1b5bd-182">See [Creating localized packages](../create-packages/creating-localized-packages.md).</span></span> |
| <span data-ttu-id="1b5bd-183">**tags**</span><span class="sxs-lookup"><span data-stu-id="1b5bd-183">**tags**</span></span>  | <span data-ttu-id="1b5bd-184">Eine durch Leerzeichen getrennte Liste mit Tags und Schlüsselwörtern, die das Paket beschreiben und zum Ermitteln von Paketen über Suchvorgänge und Filter beitragen.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-184">A space-delimited list of tags and keywords that describe the package and aid discoverability of packages through search and filtering.</span></span> |
| <span data-ttu-id="1b5bd-185">**serviceable**</span><span class="sxs-lookup"><span data-stu-id="1b5bd-185">**serviceable**</span></span> | <span data-ttu-id="1b5bd-186">*(3.3 und höher)* Nur für die interne Verwendung von NuGet.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-186">*(3.3+)* For internal NuGet use only.</span></span> |

#### <a name="collection-elements"></a><span data-ttu-id="1b5bd-187">Auflistungselemente</span><span class="sxs-lookup"><span data-stu-id="1b5bd-187">Collection elements</span></span>

| <span data-ttu-id="1b5bd-188">Element</span><span class="sxs-lookup"><span data-stu-id="1b5bd-188">Element</span></span> | <span data-ttu-id="1b5bd-189">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="1b5bd-189">Description</span></span> |
| --- | --- |
<span data-ttu-id="1b5bd-190">**packageTypes**</span><span class="sxs-lookup"><span data-stu-id="1b5bd-190">**packageTypes**</span></span> | <span data-ttu-id="1b5bd-191">*(3.5 und höher)* Eine Auflistung, die kein `<packageType>`-Element oder mindestens eins enthält und den Pakettyp angibt, wenn es sich nicht um ein gewöhnliches Abhängigkeitspaket handelt.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-191">*(3.5+)* A collection of zero or more `<packageType>` elements specifying the type of the package if other than a traditional dependency package.</span></span> <span data-ttu-id="1b5bd-192">Jeder „packageType“ verfügt über Attribute von *name* und *version*.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-192">Each packageType has attributes of *name* and *version*.</span></span> <span data-ttu-id="1b5bd-193">Informationen dazu finden Sie unter [Setting a package type (Festlegen eines Pakettypen)](../create-packages/creating-a-package.md#setting-a-package-type).</span><span class="sxs-lookup"><span data-stu-id="1b5bd-193">See [Setting a package type](../create-packages/creating-a-package.md#setting-a-package-type).</span></span> |
| <span data-ttu-id="1b5bd-194">**dependencies**</span><span class="sxs-lookup"><span data-stu-id="1b5bd-194">**dependencies**</span></span> | <span data-ttu-id="1b5bd-195">Eine Auflistung, die kein `<dependency>`-Element oder mindestens eins enthält und Abhängigkeiten für das Paket angibt.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-195">A collection of zero or more `<dependency>` elements specifying the dependencies for the package.</span></span> <span data-ttu-id="1b5bd-196">Jede Abhängigkeit verfügt über Attribute von *id*, *version*, *include* und *exclude* (3.x und höher).</span><span class="sxs-lookup"><span data-stu-id="1b5bd-196">Each dependency has attributes of *id*, *version*, *include* (3.x+), and *exclude* (3.x+).</span></span> <span data-ttu-id="1b5bd-197">Informationen dazu finden Sie im Abschnitt [Abhängigkeiten](#dependencies).</span><span class="sxs-lookup"><span data-stu-id="1b5bd-197">See [Dependencies](#dependencies) below.</span></span> |
| <span data-ttu-id="1b5bd-198">**frameworkAssemblies**</span><span class="sxs-lookup"><span data-stu-id="1b5bd-198">**frameworkAssemblies**</span></span> | <span data-ttu-id="1b5bd-199">*(1.2 und höher)* Eine Auflistung, die kein `<frameworkAssembly>`-Element oder mindestens eins enthält und die für das Paket erforderlichen Verweise auf .NET Framework-Assemblys erkennt und sicherstellt, dass Verweise zu Projekten hinzugefügt werden, die das Paket verarbeiten.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-199">*(1.2+)* A collection of zero or more `<frameworkAssembly>` elements identifying .NET Framework assembly references that this package requires, which ensures that references are added to projects consuming the package.</span></span> <span data-ttu-id="1b5bd-200">Jedes frameworkAssembly-Element verfügt über die Attribute *assemblyName* und *targetFramework*.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-200">Each frameworkAssembly has *assemblyName* and *targetFramework* attributes.</span></span> <span data-ttu-id="1b5bd-201">Informationen dazu finden Sie unter [Specifying framework assembly references GAC (Angeben von GAC-Verweisen auf Frameworkassemblys)](#specifying-framework-assembly-references-gac).</span><span class="sxs-lookup"><span data-stu-id="1b5bd-201">See [Specifying framework assembly references GAC](#specifying-framework-assembly-references-gac) below.</span></span> |
| <span data-ttu-id="1b5bd-202">**references**</span><span class="sxs-lookup"><span data-stu-id="1b5bd-202">**references**</span></span> | <span data-ttu-id="1b5bd-203">*(1.5 und höher)* Eine Auflistung, die kein `<reference>`-Element oder mindestens eins enthält, das Assemblys in dem `lib`-Ordner des Pakets benennt, die als Projektverweise hinzugefügt werden.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-203">*(1.5+)* A collection of zero or more `<reference>` elements naming assemblies in the package's `lib` folder that are added as project references.</span></span> <span data-ttu-id="1b5bd-204">Jeder Verweis verfügt über ein *file*-Attribut.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-204">Each reference has a *file* attribute.</span></span> <span data-ttu-id="1b5bd-205">`<references>` kann außerdem ein `<group>`-Element mit einem *targetFramework*-Attribut enthalten, das anschließend `<reference>`-Elemente enthält.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-205">`<references>` can also contain a `<group>` element with a *targetFramework* attribute, that then contains `<reference>` elements.</span></span> <span data-ttu-id="1b5bd-206">Wenn das Element nicht angegeben ist, werden alle Verweise in `lib` eingefügt.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-206">If omitted, all references in `lib` are included.</span></span> <span data-ttu-id="1b5bd-207">Informationen dazu finden Sie unter [Specifying explicit assembly references (Angeben von expliziten Assemblyverweisen)](#specifying-explicit-assembly-references).</span><span class="sxs-lookup"><span data-stu-id="1b5bd-207">See [Specifying explicit assembly references](#specifying-explicit-assembly-references) below.</span></span> |
| <span data-ttu-id="1b5bd-208">**contentFiles**</span><span class="sxs-lookup"><span data-stu-id="1b5bd-208">**contentFiles**</span></span> | <span data-ttu-id="1b5bd-209">*(3.3 und höher)* Eine Auflistung von `<files>`-Elementen, die Inhaltsdateien ermitteln, die in das verarbeitende Projekt eingefügt werden sollen.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-209">*(3.3+)* A collection of `<files>` elements that identify content files to include in the consuming project.</span></span> <span data-ttu-id="1b5bd-210">Diese Dateien werden zusammen mit mehreren Attributen angegeben, die beschreiben, wie sie in dem Projektsystem verwendet werden sollen.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-210">These files are specified with a set of attributes that describe how they should be used within the project system.</span></span> <span data-ttu-id="1b5bd-211">Informationen dazu finden Sie unter [Specifying files to include in the package (Angeben von Dateien, die in das Paket eingefügt werden sollen)](#specifying-files-to-include-in-the-package).</span><span class="sxs-lookup"><span data-stu-id="1b5bd-211">See [Specifying files to include in the package](#specifying-files-to-include-in-the-package) below.</span></span> |

### <a name="files-element"></a><span data-ttu-id="1b5bd-212">Files-Element</span><span class="sxs-lookup"><span data-stu-id="1b5bd-212">Files element</span></span>

<span data-ttu-id="1b5bd-213">Der `<package>`-Knoten enthält möglicherweise einen `<files>`-Knoten, der `<metadata>` gleichgeordnet ist, und bzw. oder eine untergeordnete `<contentFiles>`-Datei unter `<metadata>`, um anzugeben, welche Assembly- und Inhaltsdateien in das Paket eingefügt werden sollen.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-213">The `<package>` node may contain a `<files>` node as a sibling to `<metadata>`, and a or `<contentFiles>` child under `<metadata>`, to specify which assembly and content files to include in the package.</span></span> <span data-ttu-id="1b5bd-214">Details dazu finden Sie im Folgenden in den Abschnitten [Einfügen von Assemblydateien](#including-assembly-files) und [Einfügen von Inhaltsdateien](#including-content-files).</span><span class="sxs-lookup"><span data-stu-id="1b5bd-214">See [Including assembly files](#including-assembly-files) and [Including content files](#including-content-files) later in this topic for details.</span></span>

## <a name="replacement-tokens"></a><span data-ttu-id="1b5bd-215">Ersetzungstokens</span><span class="sxs-lookup"><span data-stu-id="1b5bd-215">Replacement tokens</span></span>

<span data-ttu-id="1b5bd-216">Bei der Erstellung eines Pakets ersetzt der [`nuget pack`-Befehl](../tools/cli-ref-pack.md) durch $ getrennte Tokens im `<metadata>`-Knoten der `.nuspec`-Datei durch Werte, die entweder einer Projektdatei oder dem `-properties`-Schalter des `pack`-Befehls entstammen.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-216">When creating a package, the [`nuget pack` command](../tools/cli-ref-pack.md) replaces $-delimited tokens in the `.nuspec` file's `<metadata>` node with values that come from either a project file or the `pack` command's `-properties` switch.</span></span>

<span data-ttu-id="1b5bd-217">Geben Sie in der Befehlszeile die Tokenwerte mit `nuget pack -properties <name>=<value>;<name>=<value>` an.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-217">On the command line, you specify token values with `nuget pack -properties <name>=<value>;<name>=<value>`.</span></span> <span data-ttu-id="1b5bd-218">Beispielsweise können Sie ein Token wie `$owners$` und `$desc$` in der `.nuspec`-Datei verwenden und die Werte zur Packzeit wie im Folgenden dargestellt bereitstellen:</span><span class="sxs-lookup"><span data-stu-id="1b5bd-218">For example, you can use a token such as `$owners$` and `$desc$` in the `.nuspec` and provide the values at packing time as follows:</span></span>

```ps
nuget pack MyProject.csproj -properties
    owners=janedoe,harikm,kimo,xiaop;desc="Awesome app logger utility"
```

<span data-ttu-id="1b5bd-219">Geben Sie die in der untenstehenden Tabelle beschriebenen Tokens an, um Werte aus einem Projekt zu verwenden (AssemblyInfo verweist auf Dateien wie `AssemblyInfo.cs` oder `AssemblyInfo.vb` in `Properties`).</span><span class="sxs-lookup"><span data-stu-id="1b5bd-219">To use values from a project, specify the tokens described in the table below (AssemblyInfo refers to the file in `Properties` such as `AssemblyInfo.cs` or `AssemblyInfo.vb`).</span></span>

<span data-ttu-id="1b5bd-220">Führen Sie anstelle von `.nuspec` nur `nuget pack` in der Projektdatei aus, um diese Tokens zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-220">To use these tokens, run `nuget pack` with the project file rather than just the `.nuspec`.</span></span> <span data-ttu-id="1b5bd-221">Beispielsweise werden bei der Verwendung des folgenden Befehls die Tokens `$id$` und `$version$` in einer `.nuspec`-Datei durch die Werte `AssemblyName` und `AssemblyVersion` des Projekts ersetzt:</span><span class="sxs-lookup"><span data-stu-id="1b5bd-221">For example, when using the following command, the `$id$` and `$version$` tokens in a `.nuspec` file are replaced with the project's `AssemblyName` and `AssemblyVersion` values:</span></span>

```ps
nuget pack MyProject.csproj
```

<span data-ttu-id="1b5bd-222">In der Regel erstellen Sie `.nuspec` in einem Projekt zuerst mithilfe von `nuget spec MyProject.csproj`, wodurch automatisch einige dieser Standardtokens eingefügt werden.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-222">Typically, when you have a project, you create the `.nuspec` initially using `nuget spec MyProject.csproj` which automatically includes some of these standard tokens.</span></span> <span data-ttu-id="1b5bd-223">Wenn in einem Projekt allerdings keine Werte für erforderliche `.nuspec`-Elemente enthalten sind, schlägt `nuget pack` fehl.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-223">However, if a project lacks values for required `.nuspec` elements, then `nuget pack` fails.</span></span> <span data-ttu-id="1b5bd-224">Stellen Sie außerdem bei der Änderung von Projektwerten sicher, dass Sie diese neu erstellen, bevor Sie das Paket erstellen. Dies können Sie ganz einfach über den `build`-Paketschalter des Befehls tun.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-224">Furthermore, if you change project values, be sure to rebuild before creating the package; this can be done conveniently with the pack command's `build` switch.</span></span>

<span data-ttu-id="1b5bd-225">Mit Ausnahme von `$configuration$` werden Werte in dem Projekt gegenüber Werten bevorzugt, die demselben Token in der Befehlszeile zugeordnet sind.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-225">With the exception of `$configuration$`, values in the project are used in preference to any assigned to the same token on the command line.</span></span>

| <span data-ttu-id="1b5bd-226">Token</span><span class="sxs-lookup"><span data-stu-id="1b5bd-226">Token</span></span> | <span data-ttu-id="1b5bd-227">Wertquelle</span><span class="sxs-lookup"><span data-stu-id="1b5bd-227">Value source</span></span> | <span data-ttu-id="1b5bd-228">Wert</span><span class="sxs-lookup"><span data-stu-id="1b5bd-228">Value</span></span>
| --- | --- | ---
| <span data-ttu-id="1b5bd-229">**$id$**</span><span class="sxs-lookup"><span data-stu-id="1b5bd-229">**$id$**</span></span> | <span data-ttu-id="1b5bd-230">Projektdatei</span><span class="sxs-lookup"><span data-stu-id="1b5bd-230">Project file</span></span> | <span data-ttu-id="1b5bd-231">AssemblyName (Titel) aus der Projektdatei</span><span class="sxs-lookup"><span data-stu-id="1b5bd-231">AssemblyName (title) from the project file</span></span> |
| <span data-ttu-id="1b5bd-232">**$version$**</span><span class="sxs-lookup"><span data-stu-id="1b5bd-232">**$version$**</span></span> | <span data-ttu-id="1b5bd-233">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="1b5bd-233">AssemblyInfo</span></span> | <span data-ttu-id="1b5bd-234">„AssemblyInformationalVersion“, falls vorhanden, andernfalls „AssemblyVersion“</span><span class="sxs-lookup"><span data-stu-id="1b5bd-234">AssemblyInformationalVersion if present, otherwise AssemblyVersion</span></span> |
| <span data-ttu-id="1b5bd-235">**$author$**</span><span class="sxs-lookup"><span data-stu-id="1b5bd-235">**$author$**</span></span> | <span data-ttu-id="1b5bd-236">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="1b5bd-236">AssemblyInfo</span></span> | <span data-ttu-id="1b5bd-237">AssemblyCompany</span><span class="sxs-lookup"><span data-stu-id="1b5bd-237">AssemblyCompany</span></span> |
| <span data-ttu-id="1b5bd-238">**$title$**</span><span class="sxs-lookup"><span data-stu-id="1b5bd-238">**$title$**</span></span> | <span data-ttu-id="1b5bd-239">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="1b5bd-239">AssemblyInfo</span></span> | <span data-ttu-id="1b5bd-240">AssemblyTitle</span><span class="sxs-lookup"><span data-stu-id="1b5bd-240">AssemblyTitle</span></span> |
| <span data-ttu-id="1b5bd-241">**$description$**</span><span class="sxs-lookup"><span data-stu-id="1b5bd-241">**$description$**</span></span> | <span data-ttu-id="1b5bd-242">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="1b5bd-242">AssemblyInfo</span></span> | <span data-ttu-id="1b5bd-243">AssemblyDescription</span><span class="sxs-lookup"><span data-stu-id="1b5bd-243">AssemblyDescription</span></span> |
| <span data-ttu-id="1b5bd-244">**$copyright$**</span><span class="sxs-lookup"><span data-stu-id="1b5bd-244">**$copyright$**</span></span> | <span data-ttu-id="1b5bd-245">AssemblyInfo</span><span class="sxs-lookup"><span data-stu-id="1b5bd-245">AssemblyInfo</span></span> | <span data-ttu-id="1b5bd-246">AssemblyCopyright</span><span class="sxs-lookup"><span data-stu-id="1b5bd-246">AssemblyCopyright</span></span> |
| <span data-ttu-id="1b5bd-247">**$configuration$**</span><span class="sxs-lookup"><span data-stu-id="1b5bd-247">**$configuration$**</span></span> | <span data-ttu-id="1b5bd-248">Assembly-DLL</span><span class="sxs-lookup"><span data-stu-id="1b5bd-248">Assembly DLL</span></span> | <span data-ttu-id="1b5bd-249">Konfiguration, die zur Erstellung der Assembly verwendet wird und standardmäßig auf „Debuggen“ festgelegt ist.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-249">Configuration used to build the assembly, defaulting to Debug.</span></span> <span data-ttu-id="1b5bd-250">Achten Sie darauf, dass Sie stets `-properties Configuration=Release` in der Befehlszeile verwenden, um mithilfe einer Releasekonfiguration ein Paket zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-250">Note that to create a package using a Release configuration, you always use `-properties Configuration=Release` on the command line.</span></span> |

<span data-ttu-id="1b5bd-251">Tokens können auch zum Auflösen von Pfaden verwendet werden, wenn Sie [Assemblydateien](#including-assembly-files) und [Inhaltsdateien](#including-content-files) hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-251">Tokens can also be used to resolve paths when you include [assembly files](#including-assembly-files) and [content files](#including-content-files).</span></span> <span data-ttu-id="1b5bd-252">Die Namen der Tokens und der MSBuild-Eigenschaften stimmen miteinander überein, wodurch Sie abhängig von der aktuellen Buildkonfiguration Dateien auswählen können, die eingefügt werden sollen.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-252">The tokens have the same names as the MSBuild properties, making it possible to select files to be included depending on the current build configuration.</span></span> <span data-ttu-id="1b5bd-253">Wenn Sie beispielsweise die folgenden Tokens in der `.nuspec`-Datei verwenden</span><span class="sxs-lookup"><span data-stu-id="1b5bd-253">For example, if you use the following tokens in the `.nuspec` file:</span></span>

```xml
<files>
    <file src="bin\$configuration$\$id$.pdb" target="lib\net40" />
</files>
```

<span data-ttu-id="1b5bd-254">und Sie eine Assembly mit der `Release`-Konfiguration in MSBuild erstellen, deren `AssemblyName` `LoggingLibrary` ist, sehen die dadurch entstandenen Zeilen in der `.nuspec`-Datei in den Paketen wie folgt aus:</span><span class="sxs-lookup"><span data-stu-id="1b5bd-254">And you build an assembly whose `AssemblyName` is `LoggingLibrary` with the `Release` configuration in MSBuild, the resulting lines in the `.nuspec` file in the package is as follows:</span></span>

```xml
<files>
    <file src="bin\Release\LoggingLibrary.pdb" target="lib\net40" />
</files>
```

## <a name="dependencies"></a><span data-ttu-id="1b5bd-255">Abhängigkeiten</span><span class="sxs-lookup"><span data-stu-id="1b5bd-255">Dependencies</span></span>

<span data-ttu-id="1b5bd-256">Das `<dependencies>`-Element in `<metadata>` enthält eine beliebige Anzahl von `<dependency>`-Elementen, die andere Pakete finden, von denen die Pakete auf der obersten Ebene abhängig sind.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-256">The `<dependencies>` element within `<metadata>` contains any number of `<dependency>` elements that identify other packages upon which the top-level package depends.</span></span> <span data-ttu-id="1b5bd-257">Im Folgenden werden die Attribute für jede `<dependency>` dargestellt:</span><span class="sxs-lookup"><span data-stu-id="1b5bd-257">The attributes for each `<dependency>` are as follows:</span></span>

| <span data-ttu-id="1b5bd-258">Attribut</span><span class="sxs-lookup"><span data-stu-id="1b5bd-258">Attribute</span></span> | <span data-ttu-id="1b5bd-259">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="1b5bd-259">Description</span></span> |
| --- | --- |
| `id` | <span data-ttu-id="1b5bd-260">(Erforderlich) Die Paket-ID der Abhängigkeit, z.B. „EntityFramework“ und „NUnit“, die der Name des Pakets „nuget.org“ ist, wird auf einer Paketseite angezeigt.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-260">(Required) The package ID of the dependency, such as "EntityFramework" and "NUnit", which is the name of the package nuget.org shows on a package page.</span></span> |
| `version` | <span data-ttu-id="1b5bd-261">(Erforderlich) Der Bereich an Versionen, die als Abhängigkeiten akzeptiert werden.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-261">(Required) The range of versions acceptable as a dependency.</span></span> <span data-ttu-id="1b5bd-262">Die genaue Syntax finden Sie unter [Paketversionsverwaltung](../reference/package-versioning.md#version-ranges-and-wildcards).</span><span class="sxs-lookup"><span data-stu-id="1b5bd-262">See [Package versioning](../reference/package-versioning.md#version-ranges-and-wildcards) for exact syntax.</span></span> |
| <span data-ttu-id="1b5bd-263">include</span><span class="sxs-lookup"><span data-stu-id="1b5bd-263">include</span></span> | <span data-ttu-id="1b5bd-264">Eine durch Kommas abgetrennte Liste mit Include/Exclude-Tags (s. Tabelle unten), in der auf die Abhängigkeit verwiesen wird, die in das endgültige Paket eingefügt werden soll.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-264">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to include in the final package.</span></span> <span data-ttu-id="1b5bd-265">Der Standardwert ist `none`.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-265">The default value is `none`.</span></span> |
| <span data-ttu-id="1b5bd-266">exclude</span><span class="sxs-lookup"><span data-stu-id="1b5bd-266">exclude</span></span> | <span data-ttu-id="1b5bd-267">Eine durch Kommas abgetrennte Liste mit Include/Exclude-Tags (s. Tabelle unten), in der auf die Abhängigkeit verwiesen wird, die nicht in das endgültige Paket eingefügt werden soll.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-267">A comma-delimited list of include/exclude tags (see below) indicating of the dependency to exclude in the final package.</span></span> <span data-ttu-id="1b5bd-268">Der Standardwert ist `all`.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-268">The  default value is `all`.</span></span> <span data-ttu-id="1b5bd-269">`exclude`-Tags haben Vorrang gegenüber `include`-Tags.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-269">Tags specified with `exclude` take precedence over those specified with `include`.</span></span> <span data-ttu-id="1b5bd-270">Beispielsweise entspricht `include="runtime, compile" exclude="compile"` `include="runtime"`.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-270">For example, `include="runtime, compile" exclude="compile"` is the same as `include="runtime"`.</span></span> |

| <span data-ttu-id="1b5bd-271">Include/Exclude-Tag</span><span class="sxs-lookup"><span data-stu-id="1b5bd-271">Include/Exclude tag</span></span> | <span data-ttu-id="1b5bd-272">Betroffene Ordner im Ziel</span><span class="sxs-lookup"><span data-stu-id="1b5bd-272">Affected folders of the target</span></span> |
| --- | --- |
| <span data-ttu-id="1b5bd-273">contentFiles</span><span class="sxs-lookup"><span data-stu-id="1b5bd-273">contentFiles</span></span> | <span data-ttu-id="1b5bd-274">Inhalt</span><span class="sxs-lookup"><span data-stu-id="1b5bd-274">Content</span></span> |
| <span data-ttu-id="1b5bd-275">Laufzeit</span><span class="sxs-lookup"><span data-stu-id="1b5bd-275">runtime</span></span> | <span data-ttu-id="1b5bd-276">Runtime, Ressourcen und Frameworkassemblys</span><span class="sxs-lookup"><span data-stu-id="1b5bd-276">Runtime, Resources, and FrameworkAssemblies</span></span> |
| <span data-ttu-id="1b5bd-277">compile</span><span class="sxs-lookup"><span data-stu-id="1b5bd-277">compile</span></span> | <span data-ttu-id="1b5bd-278">lib</span><span class="sxs-lookup"><span data-stu-id="1b5bd-278">lib</span></span> |
| <span data-ttu-id="1b5bd-279">Build</span><span class="sxs-lookup"><span data-stu-id="1b5bd-279">build</span></span> | <span data-ttu-id="1b5bd-280">Build (MSBuild-Eigenschaften und -Ziele)</span><span class="sxs-lookup"><span data-stu-id="1b5bd-280">build (MSBuild props and targets)</span></span> |
| <span data-ttu-id="1b5bd-281">Systemeigen</span><span class="sxs-lookup"><span data-stu-id="1b5bd-281">native</span></span> | <span data-ttu-id="1b5bd-282">Systemeigen</span><span class="sxs-lookup"><span data-stu-id="1b5bd-282">native</span></span> |
| <span data-ttu-id="1b5bd-283">Keine</span><span class="sxs-lookup"><span data-stu-id="1b5bd-283">none</span></span> | <span data-ttu-id="1b5bd-284">Keine Ordner</span><span class="sxs-lookup"><span data-stu-id="1b5bd-284">No folders</span></span> |
| <span data-ttu-id="1b5bd-285">alle</span><span class="sxs-lookup"><span data-stu-id="1b5bd-285">all</span></span> | <span data-ttu-id="1b5bd-286">Alle Ordner</span><span class="sxs-lookup"><span data-stu-id="1b5bd-286">All folders</span></span> |

<span data-ttu-id="1b5bd-287">Beispielsweise verweisen die folgenden Zeilen auf Abhängigkeiten auf `PackageA` Version 1.1.0 und höher und `PackageB` Version 1.x.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-287">For example, the following lines indicate dependencies on `PackageA` version 1.1.0 or higher, and `PackageB` version 1.x.</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" />
    <dependency id="PackageB" version="[1,2)" />
</dependencies>
```

<span data-ttu-id="1b5bd-288">In den folgenden Zeilen wird zwar auf Abhängigkeiten von denselben Paketen verwiesen, allerdings wird auch angegeben, dass die Ordner `contentFiles` und `build` von `PackageA` sowie alle anderen Ordner bis auf `native` und `compile` von `PackageB` angegeben werden sollen.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-288">The following lines indicate dependencies on the same packages, but specify to include the `contentFiles` and `build` folders of `PackageA` and everything but the `native` and `compile` folders of `PackageB`"</span></span>

```xml
<dependencies>
    <dependency id="PackageA" version="1.1.0" include="contentFiles, build" />
    <dependency id="PackageB" version="[1,2)" exclude="native, compile" />
</dependencies>
```

<span data-ttu-id="1b5bd-289">Hinweis: Bei der Erstellung von `.nuspec` mithilfe von `nuget spec` aus einem Projekt werden in diesem Projekt bestehende Abhängigkeiten automatisch in die resultierende `.nuspec`-Datei eingefügt.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-289">Note: When creating a `.nuspec` from a project using `nuget spec`, dependencies that exist in that project are automatically included in the resulting `.nuspec` file.</span></span>

### <a name="dependency-groups"></a><span data-ttu-id="1b5bd-290">Abhängigkeitsgruppen</span><span class="sxs-lookup"><span data-stu-id="1b5bd-290">Dependency groups</span></span>

<span data-ttu-id="1b5bd-291">*Version 2.0 und höher*</span><span class="sxs-lookup"><span data-stu-id="1b5bd-291">*Version 2.0+*</span></span>

<span data-ttu-id="1b5bd-292">Als Alternative zu einer einzelnen flachen Liste können Abhängigkeiten auf der Grundlage des Frameworkprofils des Zielprojekts angegeben werden, das `<group>`-Elemente in `<dependencies>` verwendet.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-292">As an alternative to a single flat list, dependencies can be specified according to the framework profile of the target project using `<group>` elements within `<dependencies>`.</span></span>

<span data-ttu-id="1b5bd-293">Jede Gruppe verfügt über ein Attribut mit dem Namen `targetFramework` und enthält entweder kein `<dependency>`-Element oder mindestens eins.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-293">Each group has an attribute named `targetFramework` and contains zero or more `<dependency>` elements.</span></span> <span data-ttu-id="1b5bd-294">Diese Abhängigkeiten werden zusammen installiert, wenn das Zielframework kompatibel mit dem Frameworkprofil des Projekts ist.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-294">Those dependencies are installed together when  the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="1b5bd-295">Das `<group>`-Element ohne ein `targetFramework`-Attribut wird als Standard- oder Ausweichliste der Abhängigkeiten verwendet.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-295">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of dependencies.</span></span> <span data-ttu-id="1b5bd-296">Die genauen Frameworkbezeichner finden Sie unter [Zielframeworks](../reference/target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="1b5bd-296">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="1b5bd-297">Das Gruppenformat kann nicht mit einer flachen Liste vermischt werden.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-297">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="1b5bd-298">Im folgenden Beispiel werden verschiedene Variationen des `<group>`-Elements dargestellt:</span><span class="sxs-lookup"><span data-stu-id="1b5bd-298">The following example shows different variations of the `<group>` element:</span></span>

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

## <a name="explicit-assembly-references"></a><span data-ttu-id="1b5bd-299">Explizite Assemblyverweise</span><span class="sxs-lookup"><span data-stu-id="1b5bd-299">Explicit assembly references</span></span>

<span data-ttu-id="1b5bd-300">Das `<references>`-Element gibt die genauen Assemblyverweise an, auf die das Zielprojekt bei der Verwendung des Pakets verweisen soll.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-300">The `<references>` element explicitly specifies the assemblies that the target project should reference when using the package.</span></span> <span data-ttu-id="1b5bd-301">Wenn dieses Element vorhanden ist, fügt NuGet nur Verweise zu den aufgelisteten Assemblys hinzu. Es werden keine Verweise auf andere Assemblys in dem `lib`-Ordner des Pakets hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-301">When this element is present, NuGet add references to only the listed assemblies; it does not add references for any other assemblies in the package's `lib` folder.</span></span>

<span data-ttu-id="1b5bd-302">Beispielsweise gibt das folgende `<references>`-Element NuGet die Anweisung, Verweise nur zu `xunit.dll` und `xunit.extensions.dll` hinzuzufügen, wenn zusätzliche Assemblys in dem Paket enthalten sind:</span><span class="sxs-lookup"><span data-stu-id="1b5bd-302">For example, the following `<references>` element instructs NuGet to add references to only `xunit.dll` and `xunit.extensions.dll` even if there are additional assemblies in the package:</span></span>

```xml
<references>
    <reference file="xunit.dll" />
    <reference file="xunit.extensions.dll" />
</references>
```

<span data-ttu-id="1b5bd-303">In der Regel werden Verweise nur für Assemblys zur Entwurfszeit verwendet.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-303">Explicit references are typically used for design-time only assemblies.</span></span> <span data-ttu-id="1b5bd-304">Beispielsweise müssen sich Vertragsassemblys bei der Verwendung von [Codeverträgen](/dotnet/framework/debug-trace-profile/code-contracts) neben den Runtimeassemblys befinden, die sie erweitern, damit Visual Studio sie finden kann. Allerdings muss das Projekt auf die Vertragsassemblys verweisen oder in den `bin`-Ordner des Projekts kopiert werden.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-304">When using [Code Contracts](/dotnet/framework/debug-trace-profile/code-contracts), for example, contract assemblies need to be next to the runtime assemblies that they augment so that Visual Studio can find them, but the contract assemblies need not be referenced by the project or copied into the project's `bin` folder.</span></span>

<span data-ttu-id="1b5bd-305">Genauso können explizite Verweise für Komponententestframeworks wie XUnit verwendet werden, in denen sich zwar die Toolsassemblys neben den Runtimeassemblys befinden müssen, jedoch müssen diese nicht als Projektverweise eingefügt werden.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-305">Similarly, explicit references can be used for unit test frameworks, such as XUnit, which needs its tools assemblies located next to the runtime assemblies, but does not need them included as project references.</span></span>

### <a name="reference-groups"></a><span data-ttu-id="1b5bd-306">Verweisgruppen</span><span class="sxs-lookup"><span data-stu-id="1b5bd-306">Reference groups</span></span>

<span data-ttu-id="1b5bd-307">Als Alternative zu einer einzelnen flachen Liste können Verweise auf der Grundlage des Frameworkprofils des Zielprojekts angegeben werden, das `<group>`-Elemente in `<references>` verwendet.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-307">As an alternative to a single flat list, references can be specified according to the framework profile of the target project using `<group>` elements within `<references>`.</span></span>

<span data-ttu-id="1b5bd-308">Jede Gruppe verfügt über ein Attribut mit dem Namen `targetFramework` und enthält entweder kein `<reference>`-Element oder mindestens eins.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-308">Each group has an attribute named `targetFramework` and contains zero or more `<reference>` elements.</span></span> <span data-ttu-id="1b5bd-309">Diese Verweise werden einem Projekt hinzugefügt, wenn das Zielframework mit dem Frameworkprofil des Projekts kompatibel ist.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-309">Those references are added to a project when the target framework is compatible with the project's framework profile.</span></span>

<span data-ttu-id="1b5bd-310">Das `<group>`-Element ohne ein `targetFramework`-Attribut wird als Standard- oder Ausweichliste der Verweise verwendet.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-310">The `<group>` element without a `targetFramework` attribute is used as the default or fallback list of references.</span></span> <span data-ttu-id="1b5bd-311">Die genauen Frameworkbezeichner finden Sie unter [Zielframeworks](../reference/target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="1b5bd-311">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span>

> [!Important]
> <span data-ttu-id="1b5bd-312">Das Gruppenformat kann nicht mit einer flachen Liste vermischt werden.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-312">The group format cannot be intermixed with a flat list.</span></span>

<span data-ttu-id="1b5bd-313">Im folgenden Beispiel werden verschiedene Variationen des `<group>`-Elements dargestellt:</span><span class="sxs-lookup"><span data-stu-id="1b5bd-313">The following example shows different variations of the `<group>` element:</span></span>

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

## <a name="framework-assembly-references"></a><span data-ttu-id="1b5bd-314">Verweise auf Frameworkassemblys</span><span class="sxs-lookup"><span data-stu-id="1b5bd-314">Framework assembly references</span></span>

<span data-ttu-id="1b5bd-315">Frameworkassemblys gehören zum .NET Framework und sollten für jeden vorhandenen Computer bereits im globalen Assemblycache vorhanden sein.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-315">Framework assemblies are those that are part of the .NET framework and should already be in the global assembly cache (GAC) for any given machine.</span></span> <span data-ttu-id="1b5bd-316">Pakete können sicherstellen, dass die erforderlichen Verweise, falls nötig, dem Projekt hinzugefügt werden, indem es diese Assemblys im `<frameworkAssemblies>`-Element erkennt.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-316">By identifying those assemblies within the `<frameworkAssemblies>` element, a package can ensure that required references are added to a project in the event that the project doesn't have such references already.</span></span> <span data-ttu-id="1b5bd-317">Solche Assemblys sind nicht von Anfang an in Paketen enthalten.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-317">Such assemblies, of course, are not included in a package directly.</span></span>

<span data-ttu-id="1b5bd-318">Das `<frameworkAssemblies>`-Element enthält entweder kein `<frameworkAssembly>`-Element oder mindestens eins, das die folgenden Attribute angibt:</span><span class="sxs-lookup"><span data-stu-id="1b5bd-318">The `<frameworkAssemblies>` element contains zero or more `<frameworkAssembly>` elements, each of which specifies the following attributes:</span></span>

| <span data-ttu-id="1b5bd-319">Attribut</span><span class="sxs-lookup"><span data-stu-id="1b5bd-319">Attribute</span></span> | <span data-ttu-id="1b5bd-320">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="1b5bd-320">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1b5bd-321">**assemblyName**</span><span class="sxs-lookup"><span data-stu-id="1b5bd-321">**assemblyName**</span></span> | <span data-ttu-id="1b5bd-322">(Erforderlich) Der vollqualifizierte Assemblyname.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-322">(Required) The fully qualified assembly name.</span></span> |
| <span data-ttu-id="1b5bd-323">**targetFramework**</span><span class="sxs-lookup"><span data-stu-id="1b5bd-323">**targetFramework**</span></span> | <span data-ttu-id="1b5bd-324">(Optional) Gibt das Zielframework an, auf das sich dieser Verweis bezieht.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-324">(Optional) Specifies the target framework to which this reference applies.</span></span> <span data-ttu-id="1b5bd-325">Wenn dieses Attribut nicht vorhanden ist, deutet dies darauf hin, dass sich der Verweis auf alle Frameworks bezieht.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-325">If omitted, indicates that the reference applies to all frameworks.</span></span> <span data-ttu-id="1b5bd-326">Die genauen Frameworkbezeichner finden Sie unter [Zielframeworks](../reference/target-frameworks.md).</span><span class="sxs-lookup"><span data-stu-id="1b5bd-326">See [Target frameworks](../reference/target-frameworks.md) for the exact framework identifiers.</span></span> |

<span data-ttu-id="1b5bd-327">Im folgenden Beispiel werden Verweise auf `System.Net` für alle Zielframeworks und auf `System.ServiceModel` für ausschließlich .NET Framework 4.0 dargestellt:</span><span class="sxs-lookup"><span data-stu-id="1b5bd-327">The following example shows a reference to `System.Net` for all target frameworks, and a reference to `System.ServiceModel` for .NET Framework 4.0 only:</span></span>

```xml
<frameworkAssemblies>
    <frameworkAssembly assemblyName="System.Net"  />

    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
</frameworkAssemblies>
```

<a name="specifying-files-to-include-in-the-package"></a>

## <a name="including-assembly-files"></a><span data-ttu-id="1b5bd-328">Einfügen von Assemblydateien</span><span class="sxs-lookup"><span data-stu-id="1b5bd-328">Including assembly files</span></span>

<span data-ttu-id="1b5bd-329">Wenn Sie die unter [Creating a Package (Erstellen eines Pakets)](../create-packages/creating-a-package.md) beschriebenen Anweisungen ausführen, müssen Sie nicht explizit eine Liste mit Dateien in der `.nuspec`-Datei angeben.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-329">If you follow the conventions described in [Creating a Package](../create-packages/creating-a-package.md), you do not have to explicitly specify a list of files in the `.nuspec` file.</span></span> <span data-ttu-id="1b5bd-330">Der `nuget pack`-Befehl ruft die benötigten Dateien automatisch ab.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-330">The `nuget pack` command automatically picks up the necessary files.</span></span>

> [!Important]
> <span data-ttu-id="1b5bd-331">Wenn ein Paket in einem Projekt installiert wird, fügt NuGet automatisch der DLL des Pakets Assemblyverweise hinzu. Die Verweise, die mit `.resources.dll` benannt sind werden dabei allerdings *nicht* hinzugefügt, da angenommen wird, dass es sich dabei um lokalisierte Satellitenassemblys handelt.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-331">When a package is installed into a project, NuGet automatically adds assembly references to the package's DLLs, *excluding* those that are named `.resources.dll` because they are assumed to be localized satellite assemblies.</span></span> <span data-ttu-id="1b5bd-332">Vermeiden Sie aus diesem Grund die Verwendung von `.resources.dll` für Dateien, die darüber hinaus wichtigen Paketcode enthalten.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-332">For this reason, avoid using `.resources.dll` for files that otherwise contain essential package code.</span></span>

<span data-ttu-id="1b5bd-333">Legen Sie ein `<files>`-Element als untergeordnetes Element von `<package>` und als gleichgeordnetes Element von `<metadata>` fest, das jeder Datei ein separates `<file>`-Element zuordnet, um diese automatischen Vorgänge zu umgehen und genau zu kontrollieren, welche Dateien in einem Paket enthalten sind.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-333">To bypass this automatic behavior and explicitly control which files are included in a package, place a `<files>` element as a child of `<package>` (and a sibling of `<metadata>`), identifying each file with a separate `<file>` element.</span></span> <span data-ttu-id="1b5bd-334">Zum Beispiel:</span><span class="sxs-lookup"><span data-stu-id="1b5bd-334">For example:</span></span>

```xml
<files>
    <file src="bin\Debug\*.dll" target="lib" />
    <file src="bin\Debug\*.pdb" target="lib" />
    <file src="tools\**\*.*" exclude="**\*.log" />
</files>
```

<span data-ttu-id="1b5bd-335">Das `<files>`-Element wird bei NuGet 2.x und früher sowie bei Projekten, die `packages.config` verwenden, außerdem verwendet, um unveränderliche Inhaltsdateien während der Paketinstallation einzufügen.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-335">With NuGet 2.x and earlier, and projects using `packages.config`, the `<files>` element is also used to include immutable content files when a package is installed.</span></span> <span data-ttu-id="1b5bd-336">Bei NuGet 3.3 und höher und Projekten, die PackageReference verwenden, wird stattdessen das `<contentFiles>`-Element verwendet.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-336">With NuGet 3.3+ and projects PackageReference, the `<contentFiles>` element is used instead.</span></span> <span data-ttu-id="1b5bd-337">Weitere Informationen finden Sie unter [Einfügen von Inhaltsdateien](#including-content-files).</span><span class="sxs-lookup"><span data-stu-id="1b5bd-337">See [Including content files](#including-content-files) below for details.</span></span>

### <a name="file-element-attributes"></a><span data-ttu-id="1b5bd-338">Dateielementattribute</span><span class="sxs-lookup"><span data-stu-id="1b5bd-338">File element attributes</span></span>

<span data-ttu-id="1b5bd-339">Jedes `<file>`-Element gibt die folgenden Attribute an:</span><span class="sxs-lookup"><span data-stu-id="1b5bd-339">Each `<file>` element specifies the following attributes:</span></span>

| <span data-ttu-id="1b5bd-340">Attribut</span><span class="sxs-lookup"><span data-stu-id="1b5bd-340">Attribute</span></span> | <span data-ttu-id="1b5bd-341">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="1b5bd-341">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1b5bd-342">**src**</span><span class="sxs-lookup"><span data-stu-id="1b5bd-342">**src**</span></span> | <span data-ttu-id="1b5bd-343">Der Speicherort der Dateien, die eingefügt werden sollen, unterliegt Ausnahmen, die von dem `exclude`-Attribut angegeben werden.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-343">The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="1b5bd-344">Der Pfad ist relativ zur `.nuspec`-Datei, wenn kein absoluter Pfad angegeben ist.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-344">The path is relative to the `.nuspec` file unless an absolute path is specified.</span></span> <span data-ttu-id="1b5bd-345">Das Platzhalterzeichen `*` ist zulässig, und das zweifache Platzhalterzeichen `**` impliziert eine rekursive Ordnersuche.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-345">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="1b5bd-346">**target**</span><span class="sxs-lookup"><span data-stu-id="1b5bd-346">**target**</span></span> | <span data-ttu-id="1b5bd-347">Der relative Pfad zu dem Ordner in dem Paket, in dem die Quelldateien platziert sind, der mit `lib`, `content`, `build` oder `tools` beginnt.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-347">The relative path to the folder within the package where the source files are placed, which must begin with `lib`, `content`, `build`, or `tools`.</span></span> <span data-ttu-id="1b5bd-348">Informationen dazu finden Sie unter [Creating a .nuspec from a convention-based working directory (Erstellen einer NUSPEC-Datei aus einem auf Konventionen basierenden Arbeitsverzeichnis)](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span><span class="sxs-lookup"><span data-stu-id="1b5bd-348">See [Creating a .nuspec from a convention-based working directory](../create-packages/creating-a-package.md#from-a-convention-based-working-directory).</span></span> |
| <span data-ttu-id="1b5bd-349">**exclude**</span><span class="sxs-lookup"><span data-stu-id="1b5bd-349">**exclude**</span></span> | <span data-ttu-id="1b5bd-350">Eine durch Semikolons abgetrennte Datei oder Dateimuster, die sich nicht im `src`-Speicherort befinden dürfen.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-350">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="1b5bd-351">Das Platzhalterzeichen `*` ist zulässig, und das zweifache Platzhalterzeichen `**` impliziert eine rekursive Ordnersuche.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-351">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |

### <a name="examples"></a><span data-ttu-id="1b5bd-352">Beispiele</span><span class="sxs-lookup"><span data-stu-id="1b5bd-352">Examples</span></span>

<span data-ttu-id="1b5bd-353">**Einzelne Assembly**</span><span class="sxs-lookup"><span data-stu-id="1b5bd-353">**Single assembly**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="library.dll" target="lib" />

    Packaged result:
        lib\library.dll

<span data-ttu-id="1b5bd-354">**Einzelne Assembly, die für ein Zielframework spezifisch ist**</span><span class="sxs-lookup"><span data-stu-id="1b5bd-354">**Single assembly specific to a target framework**</span></span>

    Source file:
        library.dll

    .nuspec entry:
        <file src="assemblies\net40\library.dll" target="lib\net40" />

    Packaged result:
        lib\net40\library.dll

<span data-ttu-id="1b5bd-355">**Mehrere DLLS, die Platzhalterzeichen verwenden**</span><span class="sxs-lookup"><span data-stu-id="1b5bd-355">**Set of DLLs using a wildcard**</span></span>

    Source files:
        bin\release\libraryA.dll
        bin\release\libraryB.dll

    .nuspec entry:
        <file src="bin\release\*.dll" target="lib" />

    Packaged result:
        lib\libraryA.dll
        lib\libraryB.dll

<span data-ttu-id="1b5bd-356">**DLLs für verschiedene Frameworks**</span><span class="sxs-lookup"><span data-stu-id="1b5bd-356">**DLLs for different frameworks**</span></span>

    Source files:
        lib\net40\library.dll
        lib\net20\library.dll

    .nuspec entry (using ** recursive search):
        <file src="lib\**" target="lib" />

    Packaged result:
        lib\net40\library.dll
        lib\net20\library.dll

<span data-ttu-id="1b5bd-357">**Ausschließen von Dateien**</span><span class="sxs-lookup"><span data-stu-id="1b5bd-357">**Excluding files**</span></span>

    Source files:
        \tools\*.bak
        \tools\*.log
        \tools\build\*.log

    .nuspec entries:
        <file src="tools\*.*" target="tools" exclude="tools\*.bak" />
        <file src="tools\**\*.*" target="tools" exclude="**\*.log" />

    Package result:
        (no files)

## <a name="including-content-files"></a><span data-ttu-id="1b5bd-358">Einfügen von Inhaltsdateien</span><span class="sxs-lookup"><span data-stu-id="1b5bd-358">Including content files</span></span>

<span data-ttu-id="1b5bd-359">Bei Inhaltsdateien handelt es sich um unveränderliche Dateien, die ein Paket in ein Projekt einfügen muss.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-359">Content files are immutable files that a package needs to include in a project.</span></span> <span data-ttu-id="1b5bd-360">Da sie unveränderlich sind, sollen sie auch nicht von dem verarbeitenden Projekt geändert werden.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-360">Being immutable, they are not intended to be modified by the consuming project.</span></span> <span data-ttu-id="1b5bd-361">Zu den Inhaltsdateien gehören z.B.:</span><span class="sxs-lookup"><span data-stu-id="1b5bd-361">Example content files include:</span></span>

- <span data-ttu-id="1b5bd-362">Bilder, die als Ressourcen eingebettet werden</span><span class="sxs-lookup"><span data-stu-id="1b5bd-362">Images that are embedded as resources</span></span>
- <span data-ttu-id="1b5bd-363">Quelldateien, die bereits kompiliert sind</span><span class="sxs-lookup"><span data-stu-id="1b5bd-363">Source files that are already compiled</span></span>
- <span data-ttu-id="1b5bd-364">Skripts, die in die Buildausgabe des Projekts eingefügt werden müssen</span><span class="sxs-lookup"><span data-stu-id="1b5bd-364">Scripts that need to be included with the build output of the project</span></span>
- <span data-ttu-id="1b5bd-365">Konfigurationsdateien für das Paket, die zwar in das Projekt eingefügt werden müssen, an denen jedoch keine projektspezifischen Änderungen vorgenommen werden müssen.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-365">Configuration files for the package that need to be included in the project but don't need any project-specific changes</span></span>

<span data-ttu-id="1b5bd-366">Inhaltsdateien werden in ein Paket eingefügt, das das `<files>`-Element verwendet, das den `content`-Ordner im `target`-Attribut angibt.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-366">Content files are included in a package using the `<files>` element, specifying the `content` folder in the `target` attribute.</span></span> <span data-ttu-id="1b5bd-367">Allerdings werden diese Dateien ignoriert, wenn das Paket über PackageReference in ein Projekt installiert wird, das stattdessen das `<contentFiles>`-Element verwendet.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-367">However, such files are ignored when the package is installed in a project using PackageReference, which instead uses the `<contentFiles>` element.</span></span>

<span data-ttu-id="1b5bd-368">Im Idealfall geben Pakete die Inhaltsdateien in beiden Elementen an, um ein höchstmögliches Maß an Kompatibilität mit den verarbeitenden Projekten zu erreichen.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-368">For maximum compatibility with consuming projects, a package ideally specifies the content files in both elements.</span></span>

### <a name="using-the-files-element-for-content-files"></a><span data-ttu-id="1b5bd-369">Verwenden des Dateielements für Inhaltsdateien</span><span class="sxs-lookup"><span data-stu-id="1b5bd-369">Using the files element for content files</span></span>

<span data-ttu-id="1b5bd-370">Verwenden Sie für Inhaltsdateien einfach dasselbe Format wie für Assemblydateien. Geben Sie dabei allerdings `content` als Basisordner im `target`-Attribut an, wie in den folgenden Beispielen dargestellt wird.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-370">For content files, simply use the same format as for assembly files, but specify `content` as the base folder in the `target` attribute as shown in the following examples.</span></span>

<span data-ttu-id="1b5bd-371">**Grundlegende Inhaltsdateien**</span><span class="sxs-lookup"><span data-stu-id="1b5bd-371">**Basic content files**</span></span>

    Source files:
        css\mobile\style1.css
        css\mobile\style2.css

    .nuspec entry:
        <file src="css\mobile\*.css" target="content\css\mobile" />

    Packaged result:
        content\css\mobile\style1.css
        content\css\mobile\style2.css

<span data-ttu-id="1b5bd-372">**Inhaltsdateien mit Verzeichnisstruktur**</span><span class="sxs-lookup"><span data-stu-id="1b5bd-372">**Content files with directory structure**</span></span>

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

<span data-ttu-id="1b5bd-373">**Inhaltsdatei, die für ein Zielframework spezifisch ist**</span><span class="sxs-lookup"><span data-stu-id="1b5bd-373">**Content file specific to a target framework**</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry
        <file src="css\cool\style.css" target="Content" />

    Packaged result:
        content\style.css

<span data-ttu-id="1b5bd-374">**Inhaltsdatei, die in einen Ordner mit einem Punkt im Namen kopiert wird**</span><span class="sxs-lookup"><span data-stu-id="1b5bd-374">**Content file copied to a folder with dot in name**</span></span>

<span data-ttu-id="1b5bd-375">In diesem Fall erkennt NuGet, dass die Erweiterung in `target` nicht mit der Erweiterung in `src` übereinstimmt, und behandelt dieses Bestandteil des Namens in `target` als einen Ordner:</span><span class="sxs-lookup"><span data-stu-id="1b5bd-375">In this case, NuGet sees that the extension in `target` does not match the extension in `src` and thus treats that part of the name in `target` as a folder:</span></span>

    Source file:
        images\picture.png

    .nuspec entry:
        <file src="images\picture.png" target="Content\images\package.icons" />

    Packaged result:
        content\images\package.icons\picture.png

<span data-ttu-id="1b5bd-376">**Inhaltsdateien ohne Erweiterungen**</span><span class="sxs-lookup"><span data-stu-id="1b5bd-376">**Content files without extensions**</span></span>

<span data-ttu-id="1b5bd-377">Verwenden Sie die Platzhalterzeichen `*` oder `**`, um Dateien ohne Erweiterungen einzufügen:</span><span class="sxs-lookup"><span data-stu-id="1b5bd-377">To include files without an extension, use the `*` or `**` wildcards:</span></span>

    Source file:
        flags\installed

    .nuspec entry:
        <file src="flags\**" target="flags" />

    Packaged result:
        flags\installed

<span data-ttu-id="1b5bd-378">**Inhaltsdateien mit tiefen Pfaden und tiefen Zielen**</span><span class="sxs-lookup"><span data-stu-id="1b5bd-378">**Content files with deep path and deep target**</span></span>

<span data-ttu-id="1b5bd-379">In diesem Fall nimmt NuGet an, dass das Ziel ein Dateiname und kein Ordner ist, da die Dateierweiterungen von Quelle und Ziel übereinstimmen:</span><span class="sxs-lookup"><span data-stu-id="1b5bd-379">In this case, because the file extensions of the source and target match, NuGet assumes that the target is a file name and not a folder:</span></span>

    Source file:
        css\cool\style.css

    .nuspec entry:
        <file src="css\cool\style.css" target="Content\css\cool" />
        or:
        <file src="css\cool\style.css" target="Content\css\cool\style.css" />

    Packaged result:
        content\css\cool\style.css

<span data-ttu-id="1b5bd-380">**Umbenennen einer Inhaltsdatei im Paket**</span><span class="sxs-lookup"><span data-stu-id="1b5bd-380">**Renaming a content file in the package**</span></span>

    Source file:
        ie\css\style.css

    .nuspec entry:
        <file src="ie\css\style.css" target="Content\css\ie.css" />

    Packaged result:
        content\css\ie.css

<span data-ttu-id="1b5bd-381">**Ausschließen von Dateien**</span><span class="sxs-lookup"><span data-stu-id="1b5bd-381">**Excluding files**</span></span>

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

### <a name="using-the-contentfiles-element-for-content-files"></a><span data-ttu-id="1b5bd-382">Verwenden des contentFiles-Elements für Inhaltsdateien</span><span class="sxs-lookup"><span data-stu-id="1b5bd-382">Using the contentFiles element for content files</span></span>

<span data-ttu-id="1b5bd-383">*NuGet 4.0 und höher mit PackageReference*</span><span class="sxs-lookup"><span data-stu-id="1b5bd-383">*NuGet 4.0+ with PackageReference*</span></span>

<span data-ttu-id="1b5bd-384">Standardmäßig platzieren Pakete Inhalte in einem `contentFiles`-Ordner (s. unten), in den `nuget pack` alle Dateien mithilfe von Standardattributen eingefügt hat.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-384">By default, a package places content in a `contentFiles` folder (see below) and `nuget pack` included all files in that folder using default attributes.</span></span> <span data-ttu-id="1b5bd-385">In diesem Fall ist es nicht notwendig, einen `contentFiles`-Knoten in `.nuspec` einzufügen.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-385">In this case it's not necessary to include a `contentFiles` node in the `.nuspec` at all.</span></span>

<span data-ttu-id="1b5bd-386">Das `<contentFiles>`-Element gibt eine Auflistung von `<files>`-Elementen an, die die eingefügten Dateien erkennen, um zu kontrollieren, welche Dateien eingefügt wurden.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-386">To control which files are included, the `<contentFiles>` element specifies is a collection of `<files>` elements that identify the exact files include.</span></span>

<span data-ttu-id="1b5bd-387">Diese Dateien werden zusammen mit mehreren Attributen angegeben, die beschreiben, wie sie in dem Projektsystem verwendet werden sollen:</span><span class="sxs-lookup"><span data-stu-id="1b5bd-387">These files are specified with a set of attributes that describe how they should be used within the project system:</span></span>

| <span data-ttu-id="1b5bd-388">Attribut</span><span class="sxs-lookup"><span data-stu-id="1b5bd-388">Attribute</span></span> | <span data-ttu-id="1b5bd-389">Beschreibung</span><span class="sxs-lookup"><span data-stu-id="1b5bd-389">Description</span></span> |
| --- | --- |
| <span data-ttu-id="1b5bd-390">**include**</span><span class="sxs-lookup"><span data-stu-id="1b5bd-390">**include**</span></span> | <span data-ttu-id="1b5bd-391">(Erforderlich) Der Speicherort der Dateien, die eingefügt werden sollen, unterliegt Ausnahmen, die von dem `exclude`-Attribut angegeben werden.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-391">(Required) The location of the file or files to include, subject to exclusions specified by the `exclude` attribute.</span></span> <span data-ttu-id="1b5bd-392">Der Pfad ist relativ zur `.nuspec`-Datei, wenn kein absoluter Pfad angegeben ist.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-392">The path is relative to the `.nuspec` file unless an absolute path is specified.</span></span> <span data-ttu-id="1b5bd-393">Das Platzhalterzeichen `*` ist zulässig, und das zweifache Platzhalterzeichen `**` impliziert eine rekursive Ordnersuche.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-393">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="1b5bd-394">**exclude**</span><span class="sxs-lookup"><span data-stu-id="1b5bd-394">**exclude**</span></span> | <span data-ttu-id="1b5bd-395">Eine durch Semikolons abgetrennte Datei oder Dateimuster, die sich nicht im `src`-Speicherort befinden dürfen.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-395">A semicolon-delimited list of files or file patterns to exclude from the `src` location.</span></span> <span data-ttu-id="1b5bd-396">Das Platzhalterzeichen `*` ist zulässig, und das zweifache Platzhalterzeichen `**` impliziert eine rekursive Ordnersuche.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-396">The wildcard character `*` is allowed, and the double wildcard `**` implies a recursive folder search.</span></span> |
| <span data-ttu-id="1b5bd-397">**buildAction**</span><span class="sxs-lookup"><span data-stu-id="1b5bd-397">**buildAction**</span></span> | <span data-ttu-id="1b5bd-398">Die Buildaktion, die dem Inhaltselement für MSBuild zugewiesen werden soll. Z.B. `Content`, `None`, `Embedded Resource` oder `Compile`. Die Standardeinstellung ist `Compile`.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-398">The build action to assign to the content item for MSBuild, such as `Content`, `None`, `Embedded Resource`, `Compile`, etc. The default is `Compile`.</span></span> |
| <span data-ttu-id="1b5bd-399">**copyToOutput**</span><span class="sxs-lookup"><span data-stu-id="1b5bd-399">**copyToOutput**</span></span> | <span data-ttu-id="1b5bd-400">Ein boolescher Wert, der angibt, ob Ausgabeordner Inhaltselemente in das Buildausgabeverzeichnis zu kopieren (oder veröffentlichen).</span><span class="sxs-lookup"><span data-stu-id="1b5bd-400">A Boolean indicating whether to copy content items to the build (or publish) output folder.</span></span> <span data-ttu-id="1b5bd-401">Der Standardwert ist false.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-401">The default is false.</span></span> |
| <span data-ttu-id="1b5bd-402">**flatten**</span><span class="sxs-lookup"><span data-stu-id="1b5bd-402">**flatten**</span></span> | <span data-ttu-id="1b5bd-403">Ein boolescher Wert, der angibt, ob Inhaltselemente in einen Ordner in der Buildausgabe kopiert werden sollen (TRUE) oder ob die Ordnerstruktur in den Paketen beibehalten werden soll (FALSE).</span><span class="sxs-lookup"><span data-stu-id="1b5bd-403">A Boolean indicating whether to copy content items to a single folder in the build output (true), or to preserve the folder structure in the package (false).</span></span> <span data-ttu-id="1b5bd-404">Diese Flag funktioniert nur, wenn das copyToOutput-Flag auf TRUE festgelegt ist.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-404">This flag only works when copyToOutput flag is set to true.</span></span> <span data-ttu-id="1b5bd-405">Der Standardwert ist false.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-405">The default is false.</span></span> |

<span data-ttu-id="1b5bd-406">NuGet wendet die untergeordneten Elemente von `<contentFiles>` bei der Installation eines Pakets von unten nach oben an.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-406">When installing a package, NuGet applies the child elements of `<contentFiles>` from top to bottom.</span></span> <span data-ttu-id="1b5bd-407">Wenn mehrere Einträge in einer Datei vorhanden sind, werden sie alle angewendet.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-407">If multiple entries match the same file then all entries are applied.</span></span> <span data-ttu-id="1b5bd-408">Der höher geordnete Eintrag setzt die untergeordneten Einträge außer Kraft, wenn ein Konflikt für ein Attribut entsteht.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-408">The top-most entry overrides the lower entries if there is a conflict for the same attribute.</span></span>

#### <a name="package-folder-structure"></a><span data-ttu-id="1b5bd-409">Paketordnerstruktur</span><span class="sxs-lookup"><span data-stu-id="1b5bd-409">Package folder structure</span></span>

<span data-ttu-id="1b5bd-410">Das Paketprojekt sollte Inhalte mithilfe des folgenden Musters strukturieren:</span><span class="sxs-lookup"><span data-stu-id="1b5bd-410">The package project should structure content using the following pattern:</span></span>

    /contentFiles/{codeLanguage}/{TxM}/{any?}

- <span data-ttu-id="1b5bd-411">`codeLanguages` kann `cs`, `vb`, `fs`, `any` oder das klein geschriebene Äquivalent einer `$(ProjectLanguage)` sein.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-411">`codeLanguages` may be `cs`, `vb`, `fs`, `any`, or the lowercase equivalent of a given `$(ProjectLanguage)`</span></span>
- <span data-ttu-id="1b5bd-412">`TxM` ist ein für das Zielframework zulässiger Moniker, der NuGet unterstützt (Informationen dazu finden Sie unter [Zielframeworks](../reference/target-frameworks.md)).</span><span class="sxs-lookup"><span data-stu-id="1b5bd-412">`TxM` is any legal target framework moniker that NuGet supports (see [Target frameworks](../reference/target-frameworks.md)).</span></span>
- <span data-ttu-id="1b5bd-413">An das Ende der Syntax kann eine beliebige Ordnerstruktur angehängt werden.</span><span class="sxs-lookup"><span data-stu-id="1b5bd-413">Any folder structure may be appended to the end of this syntax.</span></span>

<span data-ttu-id="1b5bd-414">Zum Beispiel:</span><span class="sxs-lookup"><span data-stu-id="1b5bd-414">For example:</span></span>

    Language- and framework-agnostic:
        /contentFiles/any/any/config.xml

    net45 content for all languages
        /contentFiles/any/net45/config.xml

    C#-specific content for net45 and up
        /contentFiles/cs/net45/sample.cs

<span data-ttu-id="1b5bd-415">Für leere Ordner kann `.` eingefügt werden, wenn diese keine Inhalte mehr für bestimmte Sprachen und TxM bereitstellen sollen. Z.B.:</span><span class="sxs-lookup"><span data-stu-id="1b5bd-415">Empty folders can use `.` to opt out of providing content for certain combinations of language and TxM, for example:</span></span>

    /contentFiles/vb/any/code.vb
    /contentFiles/cs/any/.

#### <a name="example-contentfiles-section"></a><span data-ttu-id="1b5bd-416">Beispiel: Abschnitt „contentFiles“</span><span class="sxs-lookup"><span data-stu-id="1b5bd-416">Example contentFiles section</span></span>

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

## <a name="example-nuspec-files"></a><span data-ttu-id="1b5bd-417">Beispiel: NUSPEC-Dateien</span><span class="sxs-lookup"><span data-stu-id="1b5bd-417">Example .nuspec files</span></span>

<span data-ttu-id="1b5bd-418">**Eine einfache `.nuspec`-Datei, die weder Abhängigkeiten noch Dateien enthält**</span><span class="sxs-lookup"><span data-stu-id="1b5bd-418">**A simple `.nuspec` that does not specify dependencies or files**</span></span>

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

<span data-ttu-id="1b5bd-419">**Eine `.nuspec`-Datei mit Abhängigkeiten**</span><span class="sxs-lookup"><span data-stu-id="1b5bd-419">**A `.nuspec` with dependencies**</span></span>

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

<span data-ttu-id="1b5bd-420">**Eine `.nuspec`-Datei mit Dateien**</span><span class="sxs-lookup"><span data-stu-id="1b5bd-420">**A `.nuspec` with files**</span></span>

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

<span data-ttu-id="1b5bd-421">**Eine `.nuspec`-Datei mit Frameworkassemblys**</span><span class="sxs-lookup"><span data-stu-id="1b5bd-421">**A `.nuspec` with framework assemblies**</span></span>

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

<span data-ttu-id="1b5bd-422">In diesem Beispiel werden die folgenden Elemente für bestimmte Projektziele installiert:</span><span class="sxs-lookup"><span data-stu-id="1b5bd-422">In this example, the following are installed for specific project targets:</span></span>

- <span data-ttu-id="1b5bd-423">.NET4: `System.Web` und `System.Net`</span><span class="sxs-lookup"><span data-stu-id="1b5bd-423">.NET4 -> `System.Web`, `System.Net`</span></span>
- <span data-ttu-id="1b5bd-424">.NET4-Clientprofil: `System.Net`</span><span class="sxs-lookup"><span data-stu-id="1b5bd-424">.NET4 Client Profile -> `System.Net`</span></span>
- <span data-ttu-id="1b5bd-425">Silverlight 3: `System.Json`</span><span class="sxs-lookup"><span data-stu-id="1b5bd-425">Silverlight 3 -> `System.Json`</span></span>
- <span data-ttu-id="1b5bd-426">Silverlight 4: `System.Windows.Controls.DomainServices`</span><span class="sxs-lookup"><span data-stu-id="1b5bd-426">Silverlight 4 -> `System.Windows.Controls.DomainServices`</span></span>
- <span data-ttu-id="1b5bd-427">WindowsPhone: `Microsoft.Devices.Sensors`</span><span class="sxs-lookup"><span data-stu-id="1b5bd-427">WindowsPhone -> `Microsoft.Devices.Sensors`</span></span>
