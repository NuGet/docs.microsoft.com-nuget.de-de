---
title: NuGet-Pakete in Visual Studio-Vorlagen | Microsoft-Dokumentation
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 2/8/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 0b2cf228-f028-475d-8792-c012dffdb26f
description: "Anweisungen zum Einschließen von NuGet-Paketen als Teil von Visual Studio Projekt- und Elementvorlagen."
keywords: "NuGet in Visual Studio, Visual Studio-Projektvorlagen, Elementvorlagen für Visual Studio, Pakete in Projektvorlagen, Pakete in Elementvorlagen"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 5b2ad7616578b5f54d917c4555e861c847814da9
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/14/2017
---
# <a name="packages-in-visual-studio-templates"></a><span data-ttu-id="5f417-104">Pakete in Visual Studio-Vorlagen</span><span class="sxs-lookup"><span data-stu-id="5f417-104">Packages in Visual Studio templates</span></span>

<span data-ttu-id="5f417-105">Bei Projekt- und Elementvorlagen in Visual Studio muss häufig sicherstellt werden, dass bestimmte Pakete installiert sind, wenn das Projekt oder Element erstellt wird.</span><span class="sxs-lookup"><span data-stu-id="5f417-105">Visual Studio project and item templates often need to ensure that certain packages are installed into when the project or item is created.</span></span> <span data-ttu-id="5f417-106">Die ASP.NET MVC 3-Vorlage installiert z.B. jQuery, Modernizr und andere Pakete.</span><span class="sxs-lookup"><span data-stu-id="5f417-106">For example, the ASP.NET MVC 3 template installs jQuery, Modernizr, and other packages.</span></span>

<span data-ttu-id="5f417-107">Autoren von Vorlagen können NuGet zum Installieren der erforderlichen Pakete anstatt einzelner Bibliotheken anweisen, um dies zu unterstützen.</span><span class="sxs-lookup"><span data-stu-id="5f417-107">To support this, template authors can instruct NuGet to install the necessary packages, rather than individual libraries.</span></span> <span data-ttu-id="5f417-108">Entwickler können dann einfach diese Pakete zu einem späteren Zeitpunkt aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="5f417-108">Developers can then easily update those packages at any later time.</span></span>

<span data-ttu-id="5f417-109">Weitere Informationen zum Erstellen von Vorlagen selbst finden Sie unter [Erstellen von Projekt- und Elementvorlagen in Visual Studio](https://msdn.microsoft.com/library/s365byhx.aspx) oder [Erstellen von benutzerdefinierten Projekt- und Elementvorlagen mit dem Visual Studio SDK](https://msdn.microsoft.com/library/ff527340.aspx).</span><span class="sxs-lookup"><span data-stu-id="5f417-109">To learn more about authoring templates themselves, refer to [Creating Project and Item Templates in Visual Studio](https://msdn.microsoft.com/library/s365byhx.aspx) or [Creating Custom Project and Item Templates with the Visual Studio SDK](https://msdn.microsoft.com/library/ff527340.aspx).</span></span>

<span data-ttu-id="5f417-110">Der übrige Teil dieses Abschnitts beschreibt die konkreten Schritte, die beim Erstellen einer Vorlage erforderlich sind, um NuGet-Pakete ordnungsgemäß einzubinden.</span><span class="sxs-lookup"><span data-stu-id="5f417-110">The remainder of this section describes the specific steps to take when authoring a template to properly include NuGet packages.</span></span>

- [<span data-ttu-id="5f417-111">Hinzufügen von Paketen zu einer Vorlage</span><span class="sxs-lookup"><span data-stu-id="5f417-111">Adding packages to a template</span></span>](#adding-packages-to-a-template)
- [<span data-ttu-id="5f417-112">Bewährte Methoden</span><span class="sxs-lookup"><span data-stu-id="5f417-112">Best practices</span></span>](#best-practices)

<span data-ttu-id="5f417-113">Ein Beispiel finden Sie unter [NuGetInVsTemplates sample (NuGetInVsTemplates-Beispiel)](https://bitbucket.org/marcind/nugetinvstemplates).</span><span class="sxs-lookup"><span data-stu-id="5f417-113">For an example, see the [NuGetInVsTemplates sample](https://bitbucket.org/marcind/nugetinvstemplates).</span></span>


## <a name="adding-packages-to-a-template"></a><span data-ttu-id="5f417-114">Hinzufügen von Paketen zu einer Vorlage</span><span class="sxs-lookup"><span data-stu-id="5f417-114">Adding packages to a template</span></span>

<span data-ttu-id="5f417-115">Wenn eine Vorlage instanziiert wird, wird ein [Vorlagen-Assistent](https://msdn.microsoft.com/library/ms185301.aspx) aufgerufen, um die Liste der zu installierenden Pakete zu laden, zusammen mit Informationen, wo diese Pakete zu finden sind.</span><span class="sxs-lookup"><span data-stu-id="5f417-115">When a template is instantiated, a [template wizard](https://msdn.microsoft.com/library/ms185301.aspx) is invoked to load the list of packages to install along with information about where to find those packages.</span></span> <span data-ttu-id="5f417-116">Pakete können in VSIX oder in der Vorlage eingebettet werden oder befinden sich auf der lokalen Festplatte, wobei Sie in diesem Fall einen Registrierungsschlüssel verwenden, um auf den Dateipfad zu verweisen.</span><span class="sxs-lookup"><span data-stu-id="5f417-116">Packages can be embedded in the VSIX, embedded in the template, or located on the local hard drive in which case you use a registry key to reference the file path.</span></span> <span data-ttu-id="5f417-117">Details zu diesen Speicherorten werden weiter unten in diesem Abschnitt beschrieben.</span><span class="sxs-lookup"><span data-stu-id="5f417-117">Details on these locations are given later in this section.</span></span>

<span data-ttu-id="5f417-118">Vorinstallierte Pakete funktionieren mithilfe von [Vorlagen-Assistenten](http://msdn.microsoft.com/library/ms185301.aspx).</span><span class="sxs-lookup"><span data-stu-id="5f417-118">Preinstalled packages work using [template wizards](http://msdn.microsoft.com/library/ms185301.aspx).</span></span> <span data-ttu-id="5f417-119">Wenn die Vorlage instanziiert wird, wird ein spezieller Assistent aufgerufen.</span><span class="sxs-lookup"><span data-stu-id="5f417-119">A special wizard gets invoked when the template gets instantiated.</span></span> <span data-ttu-id="5f417-120">Der Assistent lädt die Liste der Pakete, die installiert werden müssen, und übergibt diese Informationen an die entsprechenden NuGet-APIs.</span><span class="sxs-lookup"><span data-stu-id="5f417-120">The wizard loads the list of packages that need to be installed and passes that information to the appropriate NuGet APIs.</span></span>

<span data-ttu-id="5f417-121">Schritte zum Einschließen von Paketen in eine Vorlage:</span><span class="sxs-lookup"><span data-stu-id="5f417-121">Steps to include packages in a template:</span></span>

1. <span data-ttu-id="5f417-122">In Ihrer `vstemplate`-Datei fügen Sie einen Verweis auf den NuGet-Vorlagen-Assistenten hinzu, indem Sie ein [`WizardExtension`](http://msdn.microsoft.com/library/ms171411.aspx)-Element hinzufügen:</span><span class="sxs-lookup"><span data-stu-id="5f417-122">In your `vstemplate` file, add a reference to the NuGet template wizard by adding a [`WizardExtension`](http://msdn.microsoft.com/library/ms171411.aspx) element:</span></span>

    ```xml
    <WizardExtension>
        <Assembly>NuGet.VisualStudio.Interop, Version=1.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a</Assembly>
        <FullClassName>NuGet.VisualStudio.TemplateWizard</FullClassName>
    </WizardExtension>
    ```

    <span data-ttu-id="5f417-123">`NuGet.VisualStudio.Interop.dll` ist eine Assembly, die nur die `TemplateWizard`-Klasse enthält, die einen einfachen Wrapper darstellt, der die tatsächliche Implementierung in `NuGet.VisualStudio.dll` aufruft.</span><span class="sxs-lookup"><span data-stu-id="5f417-123">`NuGet.VisualStudio.Interop.dll` is an assembly that contains only the `TemplateWizard` class, which is a simple wrapper that calls into the actual implementation in `NuGet.VisualStudio.dll`.</span></span> <span data-ttu-id="5f417-124">Die Version der Assembly wird nie geändert, sodass Projekt-/Elementvorlagen mit neuen Versionen von NuGet weiterhin funktionieren.</span><span class="sxs-lookup"><span data-stu-id="5f417-124">The assembly version will never change so that project/item templates continue to work with new versions of NuGet.</span></span>

1. <span data-ttu-id="5f417-125">Fügen Sie die Liste der Pakete hinzu, die im Projekt installiert werden sollen:</span><span class="sxs-lookup"><span data-stu-id="5f417-125">Add the list of packages to install in the project:</span></span>

    ```xml
    <WizardData>
        <packages>
            <package id="jQuery" version="1.6.2" />
        </packages>
    </WizardData>
    ```

    <span data-ttu-id="5f417-126">*(NuGet 2.2.1+)*  Der Assistent unterstützt mehrere `<package>`-Elemente zur Unterstützung mehrerer Paketquellen.</span><span class="sxs-lookup"><span data-stu-id="5f417-126">*(NuGet 2.2.1+)* The wizard supports multiple `<package>` elements to support multiple package sources.</span></span> <span data-ttu-id="5f417-127">Sowohl die `id`- als auch die `version`-Attribute werden benötigt. Dies bedeutet, dass die jeweilige Version eines Pakets selbst dann installiert wird, wenn eine neuere Version verfügbar ist.</span><span class="sxs-lookup"><span data-stu-id="5f417-127">Both the `id` and `version` attributes are required, meaning that specific version of a package will be installed even if a newer version is available.</span></span> <span data-ttu-id="5f417-128">Dadurch wird verhindert, dass Paketupdates die Vorlage unterbrechen und die Wahl, das Paket zu aktualisieren, dem Entwickler überlassen wird, der die Vorlage verwendet.</span><span class="sxs-lookup"><span data-stu-id="5f417-128">This prevents package updates from breaking the template, leaving the choice to update the package to the developer using the template.</span></span>


1. <span data-ttu-id="5f417-129">Geben Sie das Repository an, in dem NuGet die Pakete, wie in den folgenden Abschnitten beschrieben, finden kann.</span><span class="sxs-lookup"><span data-stu-id="5f417-129">Specify the repository where NuGet can find the packages as described in the following sections.</span></span>

### <a name="vsix-package-repository"></a><span data-ttu-id="5f417-130">VSIX-Paketrepository</span><span class="sxs-lookup"><span data-stu-id="5f417-130">VSIX package repository</span></span>

<span data-ttu-id="5f417-131">Der empfohlene Bereitstellungsansatz für Visual Studio-Projekt-/Elementvorlagen ist eine [VSIX-Erweiterung](http://msdn.microsoft.com/library/ff363239.aspx), da sie Ihnen die Möglichkeit gibt, mehrere Projekt-/Elementvorlagen zusammen zu packen, und Entwicklern erlaubt, mühelos Ihre Vorlagen durch Verwenden des Visual Studio-Erweiterungsmanagers oder der Visual Studio Gallery zu ermitteln.</span><span class="sxs-lookup"><span data-stu-id="5f417-131">The recommended deployment approach for Visual Studio project/item templates is a [VSIX extension](http://msdn.microsoft.com/library/ff363239.aspx) because it allows you to package multiple project/item templates together and allows developers to easily discover your templates using the VS Extension Manager or the Visual Studio Gallery.</span></span> <span data-ttu-id="5f417-132">Updates der Erweiterung können genauso einfach mit [automatischen Updates für den Visual Studio-Erweiterungsmanager](http://msdn.microsoft.com/library/dd997169.aspx) bereitgestellt werden.</span><span class="sxs-lookup"><span data-stu-id="5f417-132">Updates to the extension are also easy to deploy using the [Visual Studio Extension Manager automatic update mechanism](http://msdn.microsoft.com/library/dd997169.aspx).</span></span>

<span data-ttu-id="5f417-133">VSIX selbst kann als Quelle für die von der Vorlage benötigten Pakete dienen:</span><span class="sxs-lookup"><span data-stu-id="5f417-133">The VSIX itself can serve as the source for packages required by the template:</span></span>

1. <span data-ttu-id="5f417-134">Ändern Sie das `<packages>`-Element in der `.vstemplate`-Datei wie folgt:</span><span class="sxs-lookup"><span data-stu-id="5f417-134">Modify the `<packages>` element in the `.vstemplate` file as follows:</span></span>

    ```xml
    <packages repository="extension" repositoryId="MyTemplateContainerExtensionId">
        <!-- ... -->
    </packages>
    ```

    <span data-ttu-id="5f417-135">Das `repository`-Attribut gibt den Typ des Repositorys als `extension` an, während `repositoryId` der eindeutige Bezeichner des VSIX-Projekts selbst ist (dies ist der Wert des [`ID`-Attributs](http://msdn.microsoft.com/library/dd393688.aspx) in der Datei `vsixmanifest` der Erweiterung).</span><span class="sxs-lookup"><span data-stu-id="5f417-135">The `repository` attribute specifies the type of repository as `extension` while `repositoryId` is the unique identifier of the VSIX itself (This is the value of the [`ID` attribute](http://msdn.microsoft.com/library/dd393688.aspx) in the extension’s `vsixmanifest` file).</span></span>

1. <span data-ttu-id="5f417-136">Speichern Sie Ihre `nupkg`-Dateien in einem Ordner namens `Packages` im VSIX-Projekt.</span><span class="sxs-lookup"><span data-stu-id="5f417-136">Place your `nupkg` files in a folder called `Packages` within the VSIX.</span></span>
1. <span data-ttu-id="5f417-137">Fügen Sie die erforderlichen Paketdateien als [benutzerdefinierten Erweiterungsinhalt](http://msdn.microsoft.com/library/dd393737.aspx) in Ihrer `source.extension.vsixmanifest`-Datei hinzu.</span><span class="sxs-lookup"><span data-stu-id="5f417-137">Add the necessary package files as [custom extension content](http://msdn.microsoft.com/library/dd393737.aspx) in your `source.extension.vsixmanifest` file.</span></span> <span data-ttu-id="5f417-138">Wenn Sie das 2.0-Schema verwenden, sollte es wie folgt aussehen:</span><span class="sxs-lookup"><span data-stu-id="5f417-138">If you're using the 2.0 schema it should look like this:</span></span>

    ```xml
    <Asset Type="Moq.4.0.10827.nupkg" d:Source="File" Path="Packages\Moq.4.0.10827.nupkg" d:VsixSubPath="Packages" />
    ```

    <span data-ttu-id="5f417-139">Wenn Sie das 1.0-Schema verwenden, sollte es wie folgt aussehen:</span><span class="sxs-lookup"><span data-stu-id="5f417-139">If you're using the 1.0 schema it should look like this:</span></span>

    ```xml
    <CustomExtension Type="Moq.4.0.10827.nupkg">
        packages/Moq.4.0.10827.nupkg
    </CustomExtension>
    ```

1. <span data-ttu-id="5f417-140">Beachten Sie, dass Sie Pakete in derselben Instanz von VSIX wie die Projektvorlagen übermitteln können, oder Sie können diese in einer separaten VSIX-Instanz einfügen, wenn dies für Ihr Szenario sinnvoller ist.</span><span class="sxs-lookup"><span data-stu-id="5f417-140">Note that you can deliver packages in the same VSIX as your project templates or you can put them in a separate VSIX if that makes more sense for your scenario.</span></span> <span data-ttu-id="5f417-141">Verweisen Sie jedoch auf keine Instanz von VSIX, die Sie nicht selbst steuern, da Änderungen für diese Erweiterung Ihre Vorlage beschädigen könnten.</span><span class="sxs-lookup"><span data-stu-id="5f417-141">However, do not reference any VSIX over which you do not have control, because changes to that extension could break your template.</span></span>


### <a name="template-package-repository"></a><span data-ttu-id="5f417-142">Vorlage „Paketrepository“</span><span class="sxs-lookup"><span data-stu-id="5f417-142">Template package repository</span></span>

<span data-ttu-id="5f417-143">Wenn Sie nur eine einzelne Projekt-/Elementvorlage verteilen und nicht unterschiedliche Vorlagen zusammen packen müssen, können Sie einen einfacheren, aber eingeschränkteren Ansatz verwenden, der Pakete direkt in die Projekt-/Elementvorlagen ZIP-Datei einschließt:</span><span class="sxs-lookup"><span data-stu-id="5f417-143">If you are distributing only a single project/item template and do not need to package multiple templates together, you can use a simpler but more limited approach that includes packages directly in the project/item template ZIP file:</span></span>

1. <span data-ttu-id="5f417-144">Ändern Sie das `<packages>`-Element in der `.vstemplate`-Datei wie folgt:</span><span class="sxs-lookup"><span data-stu-id="5f417-144">Modify the `<packages>` element in the `.vstemplate` file as follows:</span></span>

    ```xml
    <packages repository="template"">
        <!-- ... -->
    </packages>
    ```

    <span data-ttu-id="5f417-145">Das `repository`-Attribut hat den Wert `template`, und das `repositoryId`-Attribut ist nicht erforderlich.</span><span class="sxs-lookup"><span data-stu-id="5f417-145">The `repository` attribute has the value `template` and the `repositoryId` attribute is not required.</span></span>

1. <span data-ttu-id="5f417-146">Platzieren Sie Pakete im Stammordner der ZIP-Datei der Projekt-/Elementvorlagen.</span><span class="sxs-lookup"><span data-stu-id="5f417-146">Place packages in the root folder of the project/item template ZIP file.</span></span>

<span data-ttu-id="5f417-147">Beachten Sie, dass es bei Verwenden dieses Ansatzes in einer VSIX-Instanz mit mehreren Vorlagen zu einer unnötigen Überfrachtung kommen kann, wenn ein oder mehrere Pakete den Vorlagen gemeinsam sind.</span><span class="sxs-lookup"><span data-stu-id="5f417-147">Note that using this approach in a VSIX that contains multiple templates leads to unnecessary bloat when one or more packages are common to the templates.</span></span> <span data-ttu-id="5f417-148">In solchen Fällen verwenden Sie [VSIX als Repository](#vsix-package-repository) wie im vorherigen Abschnitt beschrieben.</span><span class="sxs-lookup"><span data-stu-id="5f417-148">In such cases, use the [VSIX as the repository](#vsix-package-repository) as described in the previous section.</span></span>


### <a name="registry-specified-folder-path"></a><span data-ttu-id="5f417-149">Von der Registrierung angegebener Ordnerpfad</span><span class="sxs-lookup"><span data-stu-id="5f417-149">Registry-specified folder path</span></span>

<span data-ttu-id="5f417-150">SDKs, die mit MSI installiert werden, können direkt auf dem Computer des Entwicklers NuGet-Pakete installieren.</span><span class="sxs-lookup"><span data-stu-id="5f417-150">SDKs that are installed using an MSI can install NuGet packages directly on the developer's machine.</span></span> <span data-ttu-id="5f417-151">Dies ermöglicht eine unmittelbare Verfügbarkeit, wenn eine Projekt- oder Elementvorlage verwendet wird, anstatt sie während dieser Zeit extrahieren zu müssen.</span><span class="sxs-lookup"><span data-stu-id="5f417-151">This makes them immediately available when a project or item template is used, rather than having to extract them during that time.</span></span> <span data-ttu-id="5f417-152">Vorlagen für ASP.NET verwenden diesen Ansatz.</span><span class="sxs-lookup"><span data-stu-id="5f417-152">ASP.NET templates use this approach.</span></span>

1. <span data-ttu-id="5f417-153">Lassen Sie MSI Pakete auf dem Computer installieren.</span><span class="sxs-lookup"><span data-stu-id="5f417-153">Have the MSI install packages to the machine.</span></span> <span data-ttu-id="5f417-154">Sie können nur `.nupkg`-Dateien installieren, oder Sie können diese zusammen mit den erweiterten Inhalten installieren, wodurch ein zusätzlicher Schritt bei Verwendung der Vorlage eingespart wird.</span><span class="sxs-lookup"><span data-stu-id="5f417-154">You can install only the `.nupkg` files, or you can install those along with the expanded contents, which saves an additional step when the template is used.</span></span> <span data-ttu-id="5f417-155">Halten Sie sich in diesem Fall an die Standardordnerstruktur von NuGet, wobei sich die `.nupkg`-Dateien im Stammordner befinden. Jedes Paket verfügt dann über einen Unterordner mit dem ID-/Versionspaar als Name des Unterordners.</span><span class="sxs-lookup"><span data-stu-id="5f417-155">In this case, follow NuGet's standard folder structure wherein the `.nupkg` files are in the root folder, and then each package has a subfolder with the id/version pair as the subfolder name.</span></span>

1. <span data-ttu-id="5f417-156">Schreiben Sie einen Registrierungsschlüssel, um den Speicherort des Pakets zu identifizieren:</span><span class="sxs-lookup"><span data-stu-id="5f417-156">Write a registry key to identify the package location:</span></span>

    - <span data-ttu-id="5f417-157">Speicherort des Schlüssels: entweder das computerweite `HKEY_LOCAL_MACHINE\SOFTWARE[\Wow6432Node]\NuGet\Repository` verwenden oder, wenn es sich um Einzelbenutzervorlagen und Pakete handelt, alternativ `HKEY_CURRENT_USER\SOFTWARE\NuGet\Repository`.</span><span class="sxs-lookup"><span data-stu-id="5f417-157">Key location: Either the machine-wide `HKEY_LOCAL_MACHINE\SOFTWARE[\Wow6432Node]\NuGet\Repository` or if it's per-user installed templates and packages, alternatively use `HKEY_CURRENT_USER\SOFTWARE\NuGet\Repository`</span></span>
    - <span data-ttu-id="5f417-158">Schlüsselname: Verwenden Sie einen Namen, der für Sie eindeutig ist.</span><span class="sxs-lookup"><span data-stu-id="5f417-158">Key name: use a name that's unique to you.</span></span> <span data-ttu-id="5f417-159">Die ASP.NET MVC 4-Vorlagen von Visual Studio 2012 verwenden z.B. `AspNetMvc4VS11`.</span><span class="sxs-lookup"><span data-stu-id="5f417-159">For example, the ASP.NET MVC 4 templates for VS 2012 use `AspNetMvc4VS11`.</span></span>
    - <span data-ttu-id="5f417-160">Werte: der vollständige Pfad zum Ordner „Pakete“.</span><span class="sxs-lookup"><span data-stu-id="5f417-160">Values: the full path to the packages folder.</span></span>

1. <span data-ttu-id="5f417-161">Fügen Sie im `<packages>`-Element in der `.vstemplate`-Datei das Attribut `repository="registry"` hinzu, und geben Sie Ihren Registrierungsschlüsselnamen im `keyName`-Attribut an.</span><span class="sxs-lookup"><span data-stu-id="5f417-161">In the `<packages>` element in the `.vstemplate` file, add the attribute `repository="registry"` and specify your registry key name in the `keyName` attribute.</span></span>

    - <span data-ttu-id="5f417-162">Wenn Sie bereits Pakete entpackt haben, verwenden Sie das `isPreunzipped="true"`-Attribut.</span><span class="sxs-lookup"><span data-stu-id="5f417-162">If you have pre-unzipped your packages, use the `isPreunzipped="true"` attribute.</span></span>
    - <span data-ttu-id="5f417-163">*(NuGet 3.2+)* Wenn Sie einen Build zur Entwurfszeit am Ende der Paketinstallation erzwingen möchten, fügen Sie das `forceDesignTimeBuild="true"`-Attribut hinzu.</span><span class="sxs-lookup"><span data-stu-id="5f417-163">*(NuGet 3.2+)* If you want to force a design-time build at the end of package installation, add the `forceDesignTimeBuild="true"` attribute.</span></span>
    - <span data-ttu-id="5f417-164">Fügen Sie zur Optimierung `skipAssemblyReferences="true"` hinzu, da die Vorlage selbst bereits die erforderlichen Verweise enthält.</span><span class="sxs-lookup"><span data-stu-id="5f417-164">As an optimization, add `skipAssemblyReferences="true"` because the template itself already includes the necessary references.</span></span>

        ```xml
        <packages repository="registry" keyName="AspNetMvc4VS11" isPreunzipped="true">
            <package id="EntityFramework" version="5.0.0" skipAssemblyReferences="true" />
            <-- ... -->
        </packages>
        ```

## <a name="best-practices"></a><span data-ttu-id="5f417-165">Bewährte Methoden</span><span class="sxs-lookup"><span data-stu-id="5f417-165">Best Practices</span></span>

1. <span data-ttu-id="5f417-166">Deklarieren Sie eine Abhängigkeit in NuGet-VSIX, indem Sie im VSIX-Manifest einen Verweis darauf hinzufügen:</span><span class="sxs-lookup"><span data-stu-id="5f417-166">Declare a dependency on the NuGet VSIX by adding a reference to it in your VSIX manifest:</span></span>

    ```xml
    <Reference Id="NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5" MinVersion="1.7.30402.9028">
        <Name>NuGet Package Manager</Name>
        <MoreInfoUrl>http://docs.microsoft.com/nuget/</MoreInfoUrl>
    </Reference>
    <!-- ... -->
    ```

1. <span data-ttu-id="5f417-167">Erfordern Sie, dass Projekt-/Elementvorlagen bei der Erstellung gespeichert werden, indem Sie [`<PromptForSaveOnCreation>`](http://msdn.microsoft.com/library/twfxayz5.aspx) in der `.vstemplate`-Datei festlegen.</span><span class="sxs-lookup"><span data-stu-id="5f417-167">Require project/item templates to be saved on creation by setting [`<PromptForSaveOnCreation>`](http://msdn.microsoft.com/library/twfxayz5.aspx) in the `.vstemplate` file.</span></span>

1. <span data-ttu-id="5f417-168">Vorlagen enthalten keine `packages.config`- oder `project.json`-Datei, und enthalten keinerlei Verweise oder Inhalt, die bei der Installation von NuGet-Paketen hinzugefügt werden.</span><span class="sxs-lookup"><span data-stu-id="5f417-168">Templates do not include a `packages.config` or `project.json` file, and do not include or any references or content that would be added when NuGet packages are installed.</span></span>
