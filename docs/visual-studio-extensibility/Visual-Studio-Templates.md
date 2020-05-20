---
title: NuGet-Pakete in Visual Studio-Vorlagen
description: Anweisungen zum Einschließen von NuGet-Paketen als Teil von Visual Studio Projekt- und Elementvorlagen.
author: karann-msft
ms.author: karann
ms.date: 01/03/2018
ms.topic: conceptual
ms.openlocfilehash: be7c10fb6ce60375f77e38f9b604ec33063e52fc
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/07/2020
ms.locfileid: "64498237"
---
# <a name="packages-in-visual-studio-templates"></a><span data-ttu-id="f7b31-103">Pakete in Visual Studio-Vorlagen</span><span class="sxs-lookup"><span data-stu-id="f7b31-103">Packages in Visual Studio templates</span></span>

<span data-ttu-id="f7b31-104">Bei Projekt- und Elementvorlagen in Visual Studio muss häufig sichergestellt werden, dass bestimmte Pakete installiert sind, wenn ein Projekt oder Element erstellt wird.</span><span class="sxs-lookup"><span data-stu-id="f7b31-104">Visual Studio project and item templates often need to ensure that certain packages are installed when a project or item is created.</span></span> <span data-ttu-id="f7b31-105">Die ASP.NET MVC 3-Vorlage installiert z.B. jQuery, Modernizr und andere Pakete.</span><span class="sxs-lookup"><span data-stu-id="f7b31-105">For example, the ASP.NET MVC 3 template installs jQuery, Modernizr, and other packages.</span></span>

<span data-ttu-id="f7b31-106">Autoren von Vorlagen können NuGet zum Installieren der erforderlichen Pakete anstatt einzelner Bibliotheken anweisen, um dies zu unterstützen.</span><span class="sxs-lookup"><span data-stu-id="f7b31-106">To support this, template authors can instruct NuGet to install the necessary packages, rather than individual libraries.</span></span> <span data-ttu-id="f7b31-107">Entwickler können dann einfach diese Pakete zu einem späteren Zeitpunkt aktualisieren.</span><span class="sxs-lookup"><span data-stu-id="f7b31-107">Developers can then easily update those packages at any later time.</span></span>

<span data-ttu-id="f7b31-108">Weitere Informationen zum Erstellen von Vorlagen selbst finden Sie unter [Vorgehensweise: Erstellen von Projektvorlagen](/visualstudio/ide/how-to-create-project-templates) oder [Erstellen von benutzerdefinierten Projekt- und Elementvorlagen](/visualstudio/extensibility/creating-custom-project-and-item-templates).</span><span class="sxs-lookup"><span data-stu-id="f7b31-108">To learn more about authoring templates themselves, refer to [How to: Create Project Templates](/visualstudio/ide/how-to-create-project-templates) or [Creating Custom Project and Item Templates](/visualstudio/extensibility/creating-custom-project-and-item-templates).</span></span>

<span data-ttu-id="f7b31-109">Der übrige Teil dieses Abschnitts beschreibt die konkreten Schritte, die beim Erstellen einer Vorlage erforderlich sind, um NuGet-Pakete ordnungsgemäß einzubinden.</span><span class="sxs-lookup"><span data-stu-id="f7b31-109">The remainder of this section describes the specific steps to take when authoring a template to properly include NuGet packages.</span></span>

- [<span data-ttu-id="f7b31-110">Hinzufügen von Paketen zu einer Vorlage</span><span class="sxs-lookup"><span data-stu-id="f7b31-110">Adding packages to a template</span></span>](#adding-packages-to-a-template)
- [<span data-ttu-id="f7b31-111">bewährten Methoden</span><span class="sxs-lookup"><span data-stu-id="f7b31-111">Best practices</span></span>](#best-practices)

<span data-ttu-id="f7b31-112">Ein Beispiel finden Sie unter [NuGetInVsTemplates sample (NuGetInVsTemplates-Beispiel)](https://bitbucket.org/marcind/nugetinvstemplates).</span><span class="sxs-lookup"><span data-stu-id="f7b31-112">For an example, see the [NuGetInVsTemplates sample](https://bitbucket.org/marcind/nugetinvstemplates).</span></span>

## <a name="adding-packages-to-a-template"></a><span data-ttu-id="f7b31-113">Hinzufügen von Paketen zu einer Vorlage</span><span class="sxs-lookup"><span data-stu-id="f7b31-113">Adding packages to a template</span></span>

<span data-ttu-id="f7b31-114">Wenn eine Vorlage instanziiert wird, wird ein [Vorlagen-Assistent](/visualstudio/extensibility/how-to-use-wizards-with-project-templates) aufgerufen, um die Liste der zu installierenden Pakete zu laden, zusammen mit Informationen, wo diese Pakete zu finden sind.</span><span class="sxs-lookup"><span data-stu-id="f7b31-114">When a template is instantiated, a [template wizard](/visualstudio/extensibility/how-to-use-wizards-with-project-templates) is invoked to load the list of packages to install along with information about where to find those packages.</span></span> <span data-ttu-id="f7b31-115">Pakete können in VSIX oder in der Vorlage eingebettet werden oder befinden sich auf der lokalen Festplatte, wobei Sie in diesem Fall einen Registrierungsschlüssel verwenden, um auf den Dateipfad zu verweisen.</span><span class="sxs-lookup"><span data-stu-id="f7b31-115">Packages can be embedded in the VSIX, embedded in the template, or located on the local hard drive in which case you use a registry key to reference the file path.</span></span> <span data-ttu-id="f7b31-116">Details zu diesen Speicherorten werden weiter unten in diesem Abschnitt beschrieben.</span><span class="sxs-lookup"><span data-stu-id="f7b31-116">Details on these locations are given later in this section.</span></span>

<span data-ttu-id="f7b31-117">Vorinstallierte Pakete funktionieren mithilfe von [Vorlagen-Assistenten](/visualstudio/extensibility/how-to-use-wizards-with-project-templates).</span><span class="sxs-lookup"><span data-stu-id="f7b31-117">Preinstalled packages work using [template wizards](/visualstudio/extensibility/how-to-use-wizards-with-project-templates).</span></span> <span data-ttu-id="f7b31-118">Wenn die Vorlage instanziiert wird, wird ein spezieller Assistent aufgerufen.</span><span class="sxs-lookup"><span data-stu-id="f7b31-118">A special wizard gets invoked when the template gets instantiated.</span></span> <span data-ttu-id="f7b31-119">Der Assistent lädt die Liste der Pakete, die installiert werden müssen, und übergibt diese Informationen an die entsprechenden NuGet-APIs.</span><span class="sxs-lookup"><span data-stu-id="f7b31-119">The wizard loads the list of packages that need to be installed and passes that information to the appropriate NuGet APIs.</span></span>

<span data-ttu-id="f7b31-120">Schritte zum Einschließen von Paketen in eine Vorlage:</span><span class="sxs-lookup"><span data-stu-id="f7b31-120">Steps to include packages in a template:</span></span>

1. <span data-ttu-id="f7b31-121">In Ihrer `vstemplate`-Datei fügen Sie einen Verweis auf den NuGet-Vorlagen-Assistenten hinzu, indem Sie ein [`WizardExtension`](/visualstudio/extensibility/wizardextension-element-visual-studio-templates)-Element hinzufügen:</span><span class="sxs-lookup"><span data-stu-id="f7b31-121">In your `vstemplate` file, add a reference to the NuGet template wizard by adding a [`WizardExtension`](/visualstudio/extensibility/wizardextension-element-visual-studio-templates) element:</span></span>

    ```xml
    <WizardExtension>
        <Assembly>NuGet.VisualStudio.Interop, Version=1.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a</Assembly>
        <FullClassName>NuGet.VisualStudio.TemplateWizard</FullClassName>
    </WizardExtension>
    ```

    <span data-ttu-id="f7b31-122">`NuGet.VisualStudio.Interop.dll` ist eine Assembly, die nur die `TemplateWizard`-Klasse enthält, die einen einfachen Wrapper darstellt, der die tatsächliche Implementierung in `NuGet.VisualStudio.dll` aufruft.</span><span class="sxs-lookup"><span data-stu-id="f7b31-122">`NuGet.VisualStudio.Interop.dll` is an assembly that contains only the `TemplateWizard` class, which is a simple wrapper that calls into the actual implementation in `NuGet.VisualStudio.dll`.</span></span> <span data-ttu-id="f7b31-123">Die Version der Assembly wird nie geändert, sodass Projekt-/Elementvorlagen mit neuen Versionen von NuGet weiterhin funktionieren.</span><span class="sxs-lookup"><span data-stu-id="f7b31-123">The assembly version will never change so that project/item templates continue to work with new versions of NuGet.</span></span>

1. <span data-ttu-id="f7b31-124">Fügen Sie die Liste der Pakete hinzu, die im Projekt installiert werden sollen:</span><span class="sxs-lookup"><span data-stu-id="f7b31-124">Add the list of packages to install in the project:</span></span>

    ```xml
    <WizardData>
        <packages>
            <package id="jQuery" version="1.6.2" />
        </packages>
    </WizardData>
    ```

    <span data-ttu-id="f7b31-125">Der Assistent unterstützt mehrere `<package>`-Elemente zur Unterstützung mehrerer Paketquellen.</span><span class="sxs-lookup"><span data-stu-id="f7b31-125">The wizard supports multiple `<package>` elements to support multiple package sources.</span></span> <span data-ttu-id="f7b31-126">Sowohl die `id`- als auch die `version`-Attribute werden benötigt. Dies bedeutet, dass die jeweilige Version eines Pakets selbst dann installiert wird, wenn eine neuere Version verfügbar ist.</span><span class="sxs-lookup"><span data-stu-id="f7b31-126">Both the `id` and `version` attributes are required, meaning that specific version of a package will be installed even if a newer version is available.</span></span> <span data-ttu-id="f7b31-127">Dadurch wird verhindert, dass Paketupdates die Vorlage unterbrechen und die Wahl, das Paket zu aktualisieren, dem Entwickler überlassen wird, der die Vorlage verwendet.</span><span class="sxs-lookup"><span data-stu-id="f7b31-127">This prevents package updates from breaking the template, leaving the choice to update the package to the developer using the template.</span></span>

1. <span data-ttu-id="f7b31-128">Geben Sie das Repository an, in dem NuGet die Pakete, wie in den folgenden Abschnitten beschrieben, finden kann.</span><span class="sxs-lookup"><span data-stu-id="f7b31-128">Specify the repository where NuGet can find the packages as described in the following sections.</span></span>

### <a name="vsix-package-repository"></a><span data-ttu-id="f7b31-129">VSIX-Paketrepository</span><span class="sxs-lookup"><span data-stu-id="f7b31-129">VSIX package repository</span></span>

<span data-ttu-id="f7b31-130">Der empfohlene Bereitstellungsansatz für Visual Studio-Projekt-/Elementvorlagen ist eine [VSIX-Erweiterung](/visualstudio/extensibility/shipping-visual-studio-extensions), da sie Ihnen die Möglichkeit gibt, mehrere Projekt-/Elementvorlagen zusammen zu packen, und Entwicklern erlaubt, mühelos Ihre Vorlagen durch Verwenden des Visual Studio-Erweiterungsmanagers oder der Visual Studio Gallery zu ermitteln.</span><span class="sxs-lookup"><span data-stu-id="f7b31-130">The recommended deployment approach for Visual Studio project/item templates is a [VSIX extension](/visualstudio/extensibility/shipping-visual-studio-extensions) because it allows you to package multiple project/item templates together and allows developers to easily discover your templates using the VS Extension Manager or the Visual Studio Gallery.</span></span> <span data-ttu-id="f7b31-131">Updates der Erweiterung können genauso einfach mit [automatischen Updates für den Visual Studio-Erweiterungsmanager](/visualstudio/extensibility/how-to-update-a-visual-studio-extension) bereitgestellt werden.</span><span class="sxs-lookup"><span data-stu-id="f7b31-131">Updates to the extension are also easy to deploy using the [Visual Studio Extension Manager automatic update mechanism](/visualstudio/extensibility/how-to-update-a-visual-studio-extension).</span></span>

<span data-ttu-id="f7b31-132">VSIX selbst kann als Quelle für die von der Vorlage benötigten Pakete dienen:</span><span class="sxs-lookup"><span data-stu-id="f7b31-132">The VSIX itself can serve as the source for packages required by the template:</span></span>

1. <span data-ttu-id="f7b31-133">Ändern Sie das `<packages>`-Element in der `.vstemplate`-Datei wie folgt:</span><span class="sxs-lookup"><span data-stu-id="f7b31-133">Modify the `<packages>` element in the `.vstemplate` file as follows:</span></span>

    ```xml
    <packages repository="extension" repositoryId="MyTemplateContainerExtensionId">
        <!-- ... -->
    </packages>
    ```

    <span data-ttu-id="f7b31-134">Das `repository`-Attribut gibt den Typ des Repositorys als `extension` an, während `repositoryId` der eindeutige Bezeichner des VSIX-Projekts selbst ist (dies ist der Wert des `ID`-Attributs in der Datei `vsixmanifest` der Datei der Erweiterung. Informationen dazu finden Sie in der [Referenz zum VSIX-Erweiterungsschema 2.0](/visualstudio/extensibility/vsix-extension-schema-2-0-reference)).</span><span class="sxs-lookup"><span data-stu-id="f7b31-134">The `repository` attribute specifies the type of repository as `extension` while `repositoryId` is the unique identifier of the VSIX itself (This is the value of the `ID` attribute in the extension’s `vsixmanifest` file, see [VSIX Extension Schema 2.0 Reference](/visualstudio/extensibility/vsix-extension-schema-2-0-reference)).</span></span>

1. <span data-ttu-id="f7b31-135">Speichern Sie Ihre `nupkg`-Dateien in einem Ordner namens `Packages` im VSIX-Projekt.</span><span class="sxs-lookup"><span data-stu-id="f7b31-135">Place your `nupkg` files in a folder called `Packages` within the VSIX.</span></span>

1. <span data-ttu-id="f7b31-136">Fügen Sie die erforderlichen Paketdateien Ihrer `vsixmanifest`-Datei als `<Asset>` hinzu (Informationen hierzu finden Sie in der [Referenz zum VSIX-Erweiterungsschema 2.0](/visualstudio/extensibility/vsix-extension-schema-2-0-reference)):</span><span class="sxs-lookup"><span data-stu-id="f7b31-136">Add the necessary package files as `<Asset>` in your `vsixmanifest` file (see [VSIX Extension Schema 2.0 Reference](/visualstudio/extensibility/vsix-extension-schema-2-0-reference)):</span></span>

    ```xml
    <Asset Type="Moq.4.0.10827.nupkg" d:Source="File" Path="Packages\Moq.4.0.10827.nupkg" d:VsixSubPath="Packages" />
    ```

1. <span data-ttu-id="f7b31-137">Beachten Sie, dass Sie Pakete in derselben Instanz von VSIX wie die Projektvorlagen übermitteln können, oder Sie können diese in einer separaten VSIX-Instanz einfügen, wenn dies für Ihr Szenario sinnvoller ist.</span><span class="sxs-lookup"><span data-stu-id="f7b31-137">Note that you can deliver packages in the same VSIX as your project templates or you can put them in a separate VSIX if that makes more sense for your scenario.</span></span> <span data-ttu-id="f7b31-138">Verweisen Sie jedoch auf keine Instanz von VSIX, die Sie nicht selbst steuern, da Änderungen für diese Erweiterung Ihre Vorlage beschädigen könnten.</span><span class="sxs-lookup"><span data-stu-id="f7b31-138">However, do not reference any VSIX over which you do not have control, because changes to that extension could break your template.</span></span>

### <a name="template-package-repository"></a><span data-ttu-id="f7b31-139">Vorlage „Paketrepository“</span><span class="sxs-lookup"><span data-stu-id="f7b31-139">Template package repository</span></span>

<span data-ttu-id="f7b31-140">Wenn Sie nur eine einzelne Projekt-/Elementvorlage verteilen und nicht unterschiedliche Vorlagen zusammen packen müssen, können Sie einen einfacheren, aber eingeschränkteren Ansatz verwenden, der Pakete direkt in die Projekt-/Elementvorlagen ZIP-Datei einschließt:</span><span class="sxs-lookup"><span data-stu-id="f7b31-140">If you are distributing only a single project/item template and do not need to package multiple templates together, you can use a simpler but more limited approach that includes packages directly in the project/item template ZIP file:</span></span>

1. <span data-ttu-id="f7b31-141">Ändern Sie das `<packages>`-Element in der `.vstemplate`-Datei wie folgt:</span><span class="sxs-lookup"><span data-stu-id="f7b31-141">Modify the `<packages>` element in the `.vstemplate` file as follows:</span></span>

    ```xml
    <packages repository="template"">
        <!-- ... -->
    </packages>
    ```

    <span data-ttu-id="f7b31-142">Das `repository`-Attribut hat den Wert `template`, und das `repositoryId`-Attribut ist nicht erforderlich.</span><span class="sxs-lookup"><span data-stu-id="f7b31-142">The `repository` attribute has the value `template` and the `repositoryId` attribute is not required.</span></span>

1. <span data-ttu-id="f7b31-143">Platzieren Sie Pakete im Stammordner der ZIP-Datei der Projekt-/Elementvorlagen.</span><span class="sxs-lookup"><span data-stu-id="f7b31-143">Place packages in the root folder of the project/item template ZIP file.</span></span>

<span data-ttu-id="f7b31-144">Beachten Sie, dass es bei Verwenden dieses Ansatzes in einer VSIX-Instanz mit mehreren Vorlagen zu einer unnötigen Überfrachtung kommen kann, wenn ein oder mehrere Pakete den Vorlagen gemeinsam sind.</span><span class="sxs-lookup"><span data-stu-id="f7b31-144">Note that using this approach in a VSIX that contains multiple templates leads to unnecessary bloat when one or more packages are common to the templates.</span></span> <span data-ttu-id="f7b31-145">In solchen Fällen verwenden Sie [VSIX als Repository](#vsix-package-repository) wie im vorherigen Abschnitt beschrieben.</span><span class="sxs-lookup"><span data-stu-id="f7b31-145">In such cases, use the [VSIX as the repository](#vsix-package-repository) as described in the previous section.</span></span>

### <a name="registry-specified-folder-path"></a><span data-ttu-id="f7b31-146">Von der Registrierung angegebener Ordnerpfad</span><span class="sxs-lookup"><span data-stu-id="f7b31-146">Registry-specified folder path</span></span>

<span data-ttu-id="f7b31-147">SDKs, die mit MSI installiert werden, können direkt auf dem Computer des Entwicklers NuGet-Pakete installieren.</span><span class="sxs-lookup"><span data-stu-id="f7b31-147">SDKs that are installed using an MSI can install NuGet packages directly on the developer's machine.</span></span> <span data-ttu-id="f7b31-148">Dies ermöglicht eine unmittelbare Verfügbarkeit, wenn eine Projekt- oder Elementvorlage verwendet wird, anstatt sie während dieser Zeit extrahieren zu müssen.</span><span class="sxs-lookup"><span data-stu-id="f7b31-148">This makes them immediately available when a project or item template is used, rather than having to extract them during that time.</span></span> <span data-ttu-id="f7b31-149">Vorlagen für ASP.NET verwenden diesen Ansatz.</span><span class="sxs-lookup"><span data-stu-id="f7b31-149">ASP.NET templates use this approach.</span></span>

1. <span data-ttu-id="f7b31-150">Lassen Sie MSI Pakete auf dem Computer installieren.</span><span class="sxs-lookup"><span data-stu-id="f7b31-150">Have the MSI install packages to the machine.</span></span> <span data-ttu-id="f7b31-151">Sie können nur `.nupkg`-Dateien installieren, oder Sie können diese zusammen mit den erweiterten Inhalten installieren, wodurch ein zusätzlicher Schritt bei Verwendung der Vorlage eingespart wird.</span><span class="sxs-lookup"><span data-stu-id="f7b31-151">You can install only the `.nupkg` files, or you can install those along with the expanded contents, which saves an additional step when the template is used.</span></span> <span data-ttu-id="f7b31-152">Halten Sie sich in diesem Fall an die Standardordnerstruktur von NuGet, wobei sich die `.nupkg`-Dateien im Stammordner befinden. Jedes Paket verfügt dann über einen Unterordner mit dem ID-/Versionspaar als Name des Unterordners.</span><span class="sxs-lookup"><span data-stu-id="f7b31-152">In this case, follow NuGet's standard folder structure wherein the `.nupkg` files are in the root folder, and then each package has a subfolder with the id/version pair as the subfolder name.</span></span>

1. <span data-ttu-id="f7b31-153">Schreiben Sie einen Registrierungsschlüssel, um den Speicherort des Pakets zu identifizieren:</span><span class="sxs-lookup"><span data-stu-id="f7b31-153">Write a registry key to identify the package location:</span></span>

    - <span data-ttu-id="f7b31-154">Speicherort des Schlüssels: entweder das computerweite `HKEY_LOCAL_MACHINE\SOFTWARE[\Wow6432Node]\NuGet\Repository` verwenden oder, wenn es sich um Einzelbenutzervorlagen und Pakete handelt, alternativ `HKEY_CURRENT_USER\SOFTWARE\NuGet\Repository`.</span><span class="sxs-lookup"><span data-stu-id="f7b31-154">Key location: Either the machine-wide `HKEY_LOCAL_MACHINE\SOFTWARE[\Wow6432Node]\NuGet\Repository` or if it's per-user installed templates and packages, alternatively use `HKEY_CURRENT_USER\SOFTWARE\NuGet\Repository`</span></span>
    - <span data-ttu-id="f7b31-155">Schlüsselname: Verwenden Sie einen Namen, der für Sie eindeutig ist.</span><span class="sxs-lookup"><span data-stu-id="f7b31-155">Key name: use a name that's unique to you.</span></span> <span data-ttu-id="f7b31-156">Die ASP.NET MVC 4-Vorlagen von Visual Studio 2012 verwenden z.B. `AspNetMvc4VS11`.</span><span class="sxs-lookup"><span data-stu-id="f7b31-156">For example, the ASP.NET MVC 4 templates for VS 2012 use `AspNetMvc4VS11`.</span></span>
    - <span data-ttu-id="f7b31-157">Werte: der vollständige Pfad zum Ordner „Pakete“.</span><span class="sxs-lookup"><span data-stu-id="f7b31-157">Values: the full path to the packages folder.</span></span>

1. <span data-ttu-id="f7b31-158">Fügen Sie im `<packages>`-Element in der `.vstemplate`-Datei das Attribut `repository="registry"` hinzu, und geben Sie Ihren Registrierungsschlüsselnamen im `keyName`-Attribut an.</span><span class="sxs-lookup"><span data-stu-id="f7b31-158">In the `<packages>` element in the `.vstemplate` file, add the attribute `repository="registry"` and specify your registry key name in the `keyName` attribute.</span></span>

    - <span data-ttu-id="f7b31-159">Wenn Sie bereits Pakete entpackt haben, verwenden Sie das `isPreunzipped="true"`-Attribut.</span><span class="sxs-lookup"><span data-stu-id="f7b31-159">If you have pre-unzipped your packages, use the `isPreunzipped="true"` attribute.</span></span>
    - <span data-ttu-id="f7b31-160">*(NuGet 3.2+)* Wenn Sie einen Build zur Entwurfszeit am Ende der Paketinstallation erzwingen möchten, fügen Sie das `forceDesignTimeBuild="true"`-Attribut hinzu.</span><span class="sxs-lookup"><span data-stu-id="f7b31-160">*(NuGet 3.2+)* If you want to force a design-time build at the end of package installation, add the `forceDesignTimeBuild="true"` attribute.</span></span>
    - <span data-ttu-id="f7b31-161">Fügen Sie zur Optimierung `skipAssemblyReferences="true"` hinzu, da die Vorlage selbst bereits die erforderlichen Verweise enthält.</span><span class="sxs-lookup"><span data-stu-id="f7b31-161">As an optimization, add `skipAssemblyReferences="true"` because the template itself already includes the necessary references.</span></span>

        ```xml
        <packages repository="registry" keyName="AspNetMvc4VS11" isPreunzipped="true">
            <package id="EntityFramework" version="5.0.0" skipAssemblyReferences="true" />
            <-- ... -->
        </packages>
        ```

## <a name="best-practices"></a><span data-ttu-id="f7b31-162">Bewährte Methoden</span><span class="sxs-lookup"><span data-stu-id="f7b31-162">Best Practices</span></span>

1. <span data-ttu-id="f7b31-163">Deklarieren Sie eine Abhängigkeit in NuGet-VSIX, indem Sie im VSIX-Manifest einen Verweis darauf hinzufügen:</span><span class="sxs-lookup"><span data-stu-id="f7b31-163">Declare a dependency on the NuGet VSIX by adding a reference to it in your VSIX manifest:</span></span>

    ```xml
    <Reference Id="NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5" MinVersion="1.7.30402.9028">
        <Name>NuGet Package Manager</Name>
        <MoreInfoUrl>http://docs.microsoft.com/nuget/</MoreInfoUrl>
    </Reference>
    <!-- ... -->
    ```

1. <span data-ttu-id="f7b31-164">Erfordern Sie, dass Projekt-/Elementvorlagen bei der Erstellung gespeichert werden, indem Sie [`<PromptForSaveOnCreation>true</PromptForSaveOnCreation>`](/visualstudio/extensibility/promptforsaveoncreation-element-visual-studio-templates) in die `.vstemplate`-Datei einschließen.</span><span class="sxs-lookup"><span data-stu-id="f7b31-164">Require project/item templates to be saved on creation by including [`<PromptForSaveOnCreation>true</PromptForSaveOnCreation>`](/visualstudio/extensibility/promptforsaveoncreation-element-visual-studio-templates) in the `.vstemplate` file.</span></span>

1. <span data-ttu-id="f7b31-165">Vorlagen enthalten keine `packages.config`-Datei, und enthalten keinerlei Verweise oder Inhalte, die bei der Installation von NuGet-Paketen hinzugefügt werden.</span><span class="sxs-lookup"><span data-stu-id="f7b31-165">Templates do not include a `packages.config` file, and do not include or any references or content that would be added when NuGet packages are installed.</span></span>
