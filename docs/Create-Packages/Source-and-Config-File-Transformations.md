---
title: "Quell- und Konfigurationsdateitransformationen für NuGet-Pakete | Microsoft-Dokumentation"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 4/24/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 20991d69-9e2e-4881-bbf2-96ae634e1872
description: "Einzelheiten zur Fähigkeit von NuGet-Paketen, Quellcode und Konfigurationsdateien (XML) nach ihrer Installation zu transformieren."
keywords: "NuGet-Paketinstallation, NuGet-Pakettransformationen, Ändern von Konfigurationsdateien, Ändern von Quellcode"
ms.reviewer:
- karann-msft
- unniravindranathan
- anangaur
ms.openlocfilehash: 7d380b7f2ff52ec39a2ac9a2b939ee51db6054f3
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/14/2017
---
# <a name="transforming-source-code-and-configuration-files"></a><span data-ttu-id="10a12-104">Transformieren von Quellcode und Konfigurationsdateien</span><span class="sxs-lookup"><span data-stu-id="10a12-104">Transforming source code and configuration files</span></span>

<span data-ttu-id="10a12-105">Bei Projekten, die die Datei `packages.config` oder `project.json` verwenden, unterstützt NuGet die Fähigkeit, bei Paketinstallationen und -deinstallationen Transformationen an dem Quellcode und den Konfigurationsdateien vorzunehmen.</span><span class="sxs-lookup"><span data-stu-id="10a12-105">For projects using `packages.config` or `project.json`, NuGet supports the ability to make transformations to source code and configuration files at package install and uninstall times.</span></span>

> [!Note]
> <span data-ttu-id="10a12-106">Quell- und Konfigurationsdateitransformationen finden keine Anwendung, wenn ein Paket über [Paketverweise in Projektdateien](../Consume-Packages/Package-References-in-Project-Files.md) installiert wird.</span><span class="sxs-lookup"><span data-stu-id="10a12-106">Source and configuration file transformations are not applied when a package is installed in a project using [Package References in project files](../Consume-Packages/Package-References-in-Project-Files.md).</span></span> 

<span data-ttu-id="10a12-107">Bei einer **Quellcodetransformation** wird während der Installation des Pakets eine unidirektionale Tokenersetzung auf Dateien im Ordner `content` des Pakets angewendet. Dabei beziehen sich die Token auf die [Projekteigenschaften](https://msdn.microsoft.com/library/vslangproj.projectproperties_properties.aspx) von Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="10a12-107">A **source code transformation** applies one-way token replacement to files in the package's `content` folder when the package is installed, where tokens refer to Visual Studio [project properties](https://msdn.microsoft.com/library/vslangproj.projectproperties_properties.aspx).</span></span> <span data-ttu-id="10a12-108">Dies bietet Ihnen die Möglichkeit, eine Datei in den Namespace des Projekts einzufügen oder Code anzupassen, der normalerweise in `global.asax` in einem ASP.NET-Projekt eingefügt werden würde.</span><span class="sxs-lookup"><span data-stu-id="10a12-108">This allows you to insert a file into the project's namespace, or to customize code that would typically go into `global.asax` in an ASP.NET project.</span></span>

<span data-ttu-id="10a12-109">Bei einer **Konfigurationsdateitransformation** können Sie Dateien ändern, die bereits in einem Zielprojekt vorhanden sind, wie z.B. `web.config` und `app.config`.</span><span class="sxs-lookup"><span data-stu-id="10a12-109">A **config file transformation** allows you to modify files that already exist in a target project, such as `web.config` and `app.config`.</span></span> <span data-ttu-id="10a12-110">In Ihrem Paket müsste beispielsweise ein Element zu Abschnitt `modules` in der Konfigurationsdatei hinzugefügt werden.</span><span class="sxs-lookup"><span data-stu-id="10a12-110">For example, your package might need to add an item to the `modules` section in the config file.</span></span> <span data-ttu-id="10a12-111">Diese Transformation erfolgt durch das Einschließen spezieller Dateien in das Paket, in denen die zu den Konfigurationsdateien hinzuzufügenden Abschnitte beschrieben werden.</span><span class="sxs-lookup"><span data-stu-id="10a12-111">This transformation is done by including special files in the package that describe the sections to add to the configuration files.</span></span> <span data-ttu-id="10a12-112">Bei der Deinstallation eines Pakets werden diese Änderungen wieder zurückgesetzt, wodurch diese Transformation zu einer bidirektionalen Transformation wird.</span><span class="sxs-lookup"><span data-stu-id="10a12-112">When a package is uninstalled, those same changes are then reversed, making this a two-way transformation.</span></span>


## <a name="specifying-source-code-transformations"></a><span data-ttu-id="10a12-113">Angeben von Quellcodetransformationen</span><span class="sxs-lookup"><span data-stu-id="10a12-113">Specifying source code transformations</span></span>

1. <span data-ttu-id="10a12-114">Dateien, die Sie aus dem Paket in das Projekt einfügen möchten, müssen in dem Ordner `content` des Pakets enthalten sein.</span><span class="sxs-lookup"><span data-stu-id="10a12-114">Files that you want to insert from the package into the project must be located within the package's `content` folder.</span></span> <span data-ttu-id="10a12-115">Wenn Sie beispielsweise möchten, dass eine Datei mit dem Namen `ContosoData.cs` in dem Ordner `Models` des Zielprojekts installiert wird, muss diese im Ordner `content\Models` des Pakets enthalten sein.</span><span class="sxs-lookup"><span data-stu-id="10a12-115">For example, if you want a file called `ContosoData.cs` to be installed in a `Models` folder of the target project, it must be inside the `content\Models` folder in the package.</span></span>

2. <span data-ttu-id="10a12-116">Hängen Sie `.pp` an den Namen der Quellcodedatei an, um NuGet die Anweisung zu geben, die Tokenersetzung während der Installation anzuwenden.</span><span class="sxs-lookup"><span data-stu-id="10a12-116">To instruct NuGet to apply token replacement at install time, append `.pp` to the source code file name.</span></span> <span data-ttu-id="10a12-117">Nach der Installation weist die Datei nicht die Erweiterung `.pp` auf.</span><span class="sxs-lookup"><span data-stu-id="10a12-117">After installation, the file will not have the `.pp` extension.</span></span>

    <span data-ttu-id="10a12-118">Wenn Sie beispielsweise Transformationen in `ContosoData.cs` vornehmen möchten, nennen Sie die Datei in dem Paket `ContosoData.cs.pp`.</span><span class="sxs-lookup"><span data-stu-id="10a12-118">For example, to make transformations in `ContosoData.cs`, name the file in the package `ContosoData.cs.pp`.</span></span> <span data-ttu-id="10a12-119">Nach der Installation wird sie als `ContosoData.cs` angezeigt.</span><span class="sxs-lookup"><span data-stu-id="10a12-119">After installation it will appear as `ContosoData.cs`.</span></span>

3. <span data-ttu-id="10a12-120">Verwenden Sie für die Angabe von Werten, die NuGet durch Projekteigenschaften ersetzen sollte, in der Quellcodedatei Token im Format `$token$` ohne Beachtung der Groß-/Kleinschreibung:</span><span class="sxs-lookup"><span data-stu-id="10a12-120">In the source code file, use case-insensitive tokens of the form `$token$` to indicate values that NuGet should replace with project properties:</span></span>

    ```cs
    namespace $rootnamespace$.Models
    {
        public struct CategoryInfo
        {
            public string categoryid;
            public string description;
            public string htmlUrl;
            public string rssUrl;
            public string title;
        }
    }
    ```

    <span data-ttu-id="10a12-121">Bei der Installation ersetzt NuGet `$rootnamespace$`, wobei es davon ausgeht, dass `Fabrikam` das Zielprojekt ist, dessen Stammnamespace `Fabrikam` lautet.</span><span class="sxs-lookup"><span data-stu-id="10a12-121">Upon installation, NuGet replaces `$rootnamespace$` with `Fabrikam` assuming the target project's whose root namespace is `Fabrikam`.</span></span>

<span data-ttu-id="10a12-122">Das Token `$rootnamespace$` stellt die am häufigsten verwendete Projekteigenschaft dar. Alle weiteren Token werden in der Dokumentation zu [Projekteigenschaften](https://msdn.microsoft.com/library/vslangproj.projectproperties_properties.aspx) auf MSDN aufgeführt.</span><span class="sxs-lookup"><span data-stu-id="10a12-122">The `$rootnamespace$` token is the most commonly used project property; all others are listed in the [Project Properties](https://msdn.microsoft.com/library/vslangproj.projectproperties_properties.aspx) documentation on MSDN.</span></span> <span data-ttu-id="10a12-123">Bedenken Sie jedoch, dass einige Eigenschaften möglicherweise für den Projekttyp spezifisch sind.</span><span class="sxs-lookup"><span data-stu-id="10a12-123">Be mindful, of course, that some properties might be specific to the project type.</span></span>


## <a name="specifying-config-file-transformations"></a><span data-ttu-id="10a12-124">Angeben von Konfigurationsdateitransformationen</span><span class="sxs-lookup"><span data-stu-id="10a12-124">Specifying config file transformations</span></span>

<span data-ttu-id="10a12-125">Wie in den nachfolgenden Abschnitten beschrieben, können Konfigurationsdateitransformationen auf zwei Arten erfolgen:</span><span class="sxs-lookup"><span data-stu-id="10a12-125">As described in the sections that follow, config file transformations can be done in two ways:</span></span>

- <span data-ttu-id="10a12-126">Schließen Sie die Dateien `app.config.transform` und `web.config.transform` in den Ordner `content` Ihres Pakets ein. Dabei erkennt NuGet an der `.transform`-Erweiterung, dass diese Dateien den XML-Code enthalten, der bei der Installation des Pakets mit vorhandenen Konfigurationsdateien zusammengeführt werden soll.</span><span class="sxs-lookup"><span data-stu-id="10a12-126">Include `app.config.transform` and `web.config.transform` files in your package's `content` folder, where the `.transform` extension tells NuGet that these files contain the XML to merge with existing config files when the package is installed.</span></span> <span data-ttu-id="10a12-127">Bei der Deinstallation eines Pakets wird derselbe XML-Code entfernt.</span><span class="sxs-lookup"><span data-stu-id="10a12-127">When a package is uninstalled, that same XML is removed.</span></span>
- <span data-ttu-id="10a12-128">(NuGet ab Version 2.6) Schließen Sie die Dateien `app.config.install.xdt` und `web.config.install.xdt` in den Ordner `content` Ihres Pakets ein, und verwenden Sie dabei [XDT-Syntax](https://msdn.microsoft.com/library/dd465326.aspx) zur Beschreibung der gewünschten Änderungen.</span><span class="sxs-lookup"><span data-stu-id="10a12-128">(NuGet 2.6 and later) Include `app.config.install.xdt` and `web.config.install.xdt` files in your package's `content` folder, using [XDT syntax](https://msdn.microsoft.com/library/dd465326.aspx) to describe the desired changes.</span></span> <span data-ttu-id="10a12-129">Mit dieser Option können Sie auch eine Datei vom Typ `.uninstall.xdt` einschließen, um Änderungen zurückzusetzen, wenn das Paket aus dem Projekt entfernt wird.</span><span class="sxs-lookup"><span data-stu-id="10a12-129">With this option you can also include a `.uninstall.xdt` file to reverse changes when the package is removed from a project.</span></span>

> [!Note]
> <span data-ttu-id="10a12-130">Transformationen gelten nicht für `.config`-Dateien, auf die ein Link in Visual Studio verweist.</span><span class="sxs-lookup"><span data-stu-id="10a12-130">Transformations are not applied to `.config` files referenced as a link in Visual Studio.</span></span>

<span data-ttu-id="10a12-131">Der Vorteil bei der Verwendung von XDT besteht darin, dass zwei statische Dateien nicht einfach zusammengeführt werden, sondern eine Syntax für die Bearbeitung der Struktur eines Using-Elements in XML DOM sowie eines zugehörigen Attributs mit voller XPath-Unterstützung bereitgestellt wird.</span><span class="sxs-lookup"><span data-stu-id="10a12-131">The advantage of using XDT is that instead of simply merging two static files, it provides a syntax for manipulating the structure of an XML DOM using element and attribute matching using full XPath support.</span></span> <span data-ttu-id="10a12-132">XDT kann anschließend Elemente hinzufügen, aktualisieren oder entfernen, Elemente an einer bestimmten Stelle anordnen oder Elemente ersetzen/entfernen (einschließlich untergeordneter Knoten).</span><span class="sxs-lookup"><span data-stu-id="10a12-132">XDT can then add, update, or remove elements, place new elements at a specific location, or replace/remove elements (including child nodes).</span></span> <span data-ttu-id="10a12-133">Dadurch wird die Erstellung von Transformationen zur Deinstallation erleichtert, bei denen sämtliche Transformationen zurückgesetzt werden, die während der Paketinstallation erfolgt sind.</span><span class="sxs-lookup"><span data-stu-id="10a12-133">This makes it straightforward to create uninstall transforms that back out all transformations done during package installation.</span></span>

### <a name="xml-transforms"></a><span data-ttu-id="10a12-134">XML-Transformationen</span><span class="sxs-lookup"><span data-stu-id="10a12-134">XML transforms</span></span>

<span data-ttu-id="10a12-135">Die Dateien `app.config.transform` und `web.config.transform` in dem Ordner `content` eines Pakets enthalten nur die Elemente, die in den vorhandenen Dateien `app.config` und `web.config` des Projekts zusammengeführt werden sollen.</span><span class="sxs-lookup"><span data-stu-id="10a12-135">The `app.config.transform` and `web.config.transform` in a package's `content` folder contain only those elements to merge into the project's existing `app.config` and `web.config` files.</span></span>

<span data-ttu-id="10a12-136">Angenommen, das Projekt weist zu Beginn folgende Inhalte in der Datei `web.config` auf:</span><span class="sxs-lookup"><span data-stu-id="10a12-136">As an example, suppose the project initially contains the following content in `web.config`:</span></span>

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
        </modules>
    <system.webServer>
</configuration>
```

<span data-ttu-id="10a12-137">Wenn Sie ein `MyNuModule`-Element während der Paketinstallation zum Abschnitt `modules` hinzufügen möchten, erstellen Sie im Ordner `content` des Pakets eine Datei vom Typ `web.config.transform`, die wie folgt aussieht:</span><span class="sxs-lookup"><span data-stu-id="10a12-137">To add a `MyNuModule` element to the `modules` section during package install, create a `web.config.transform` file in the package's `content` folder that looks like this:</span></span>

    
```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="MyNuModule" type="Sample.MyNuModule" />
        </modules>
    <system.webServer>
</configuration>
```

<span data-ttu-id="10a12-138">Nach der Installation des Pakets durch NuGet wird die Datei `web.config` wie folgt angezeigt:</span><span class="sxs-lookup"><span data-stu-id="10a12-138">After NuGet installs the package, `web.config` will appear as follows:</span></span>

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
            <add name="MyNuModule" type="Sample.MyNuModule" />
        </modules>
    <system.webServer>
</configuration>
```

<span data-ttu-id="10a12-139">Beachten Sie, dass NuGet den Abschnitt `modules` nicht ersetzt hat. Der neue Eintrag wurde lediglich durch das Hinzufügen neuer Elemente und Attribute zusammengeführt.</span><span class="sxs-lookup"><span data-stu-id="10a12-139">Notice that NuGet didn't replace the `modules` section, it just merged the new entry into it by adding only new elements and attributes.</span></span> <span data-ttu-id="10a12-140">NuGet ändert keine vorhandenen Elemente oder Attribute.</span><span class="sxs-lookup"><span data-stu-id="10a12-140">NuGet will not change any existing elements or attributes.</span></span>

<span data-ttu-id="10a12-141">Wenn das Paket deinstalliert wird, überprüft NuGet die `.transform`-Dateien erneut und entfernt die enthaltenen Elemente aus den entsprechenden `.config`-Dateien.</span><span class="sxs-lookup"><span data-stu-id="10a12-141">When the package is uninstalled, NuGet will examine the `.transform` files again and remove the elements it contains from the appropriate `.config` files.</span></span> <span data-ttu-id="10a12-142">Beachten Sie, dass dieser Prozess keine Auswirkungen auf die Zeilen in der Datei `.config` hat, die Sie nach der Paketinstallation ändern.</span><span class="sxs-lookup"><span data-stu-id="10a12-142">Note that this process will not affect any lines in the `.config` file that you modify after package installation.</span></span>

<span data-ttu-id="10a12-143">In einem umfangreicheren Beispiel fügt das Paket [Error Logging Modules and Handlers for ASP.NET (ELMAH)](https://www.nuget.org/packages/elmah/) (Module für die Fehlerprotokollierung und Handlers für ASP.NET) viele Einträge zu `web.config` hinzu, die bei der Deinstallation eines Pakets wieder entfernt werden.</span><span class="sxs-lookup"><span data-stu-id="10a12-143">As a more extensive example, the [Error Logging Modules and Handlers for ASP.NET (ELMAH)](https://www.nuget.org/packages/elmah/) package adds many entries into `web.config`, which are again removed when a package is uninstalled.</span></span>

<span data-ttu-id="10a12-144">Wenn Sie die zugehörige Datei `web.config.transform` überprüfen möchten, laden Sie das ELMAH-Paket über den oben stehenden Link herunter, ändern Sie die Paketerweiterung von `.nupkg` in `.zip`, und öffnen Sie anschließend `content\web.config.transform` in dieser ZIP-Datei.</span><span class="sxs-lookup"><span data-stu-id="10a12-144">To examine its `web.config.transform` file, download the ELMAH package from the link above, change the package extension from `.nupkg` to `.zip`, and then open `content\web.config.transform` in that ZIP file.</span></span>

<span data-ttu-id="10a12-145">Erstellen Sie ein neues ASP.NET-Projekt in Visual Studio (die Vorlage ist unter **Visual C# > Web** im Dialogfeld „Neues Projekt“ zu finden), und wählen Sie eine leere ASP.NET-App aus, um die Auswirkungen der Installation und Deinstallation des Pakets sehen zu können.</span><span class="sxs-lookup"><span data-stu-id="10a12-145">To see the effect of installing and uninstalling the package, create a new ASP.NET project in Visual Studio (the template is under **Visual C# > Web** in the New Project dialog), and select an empty ASP.NET application.</span></span> <span data-ttu-id="10a12-146">Öffnen Sie `web.config`, um den zugehörigen ursprünglichen Status anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="10a12-146">Open `web.config` to see its initial state.</span></span> <span data-ttu-id="10a12-147">Klicken Sie anschließend mit der rechten Maustaste auf das Projekt, wählen Sie **NuGet-Pakete verwalten** aus, suchen Sie auf der Website nuget.org nach ELMAH, und installieren Sie die neueste Version.</span><span class="sxs-lookup"><span data-stu-id="10a12-147">Then right-click the project, select **Manage NuGet Packages**, browse for ELMAH on nuget.org, and install the latest version.</span></span> <span data-ttu-id="10a12-148">Beachten Sie alle an `web.config` vorgenommenen Änderungen.</span><span class="sxs-lookup"><span data-stu-id="10a12-148">Notice all the changes to `web.config`.</span></span> <span data-ttu-id="10a12-149">Wenn sie das Paket jetzt deinstallieren, können Sie sehen, wie `web.config` in den zugehörigen ursprünglichen Status zurückversetzt wird.</span><span class="sxs-lookup"><span data-stu-id="10a12-149">Now uninstall the package and you'll see `web.config` revert to its prior state.</span></span>


### <a name="xdt-transforms"></a><span data-ttu-id="10a12-150">XDT-Transformationen</span><span class="sxs-lookup"><span data-stu-id="10a12-150">XDT transforms</span></span>

<span data-ttu-id="10a12-151">Mit NuGet ab Version 2.6 können Sie Konfigurationsdateien über die [XDT-Syntax](https://msdn.microsoft.com/library/dd465326.aspx) ändern.</span><span class="sxs-lookup"><span data-stu-id="10a12-151">With NuGet 2.6 and later, you can modify config files using [XDT syntax](https://msdn.microsoft.com/library/dd465326.aspx).</span></span> <span data-ttu-id="10a12-152">Sie können auch veranlassen, dass NuGet Token über [Projekteigenschaften](https://msdn.microsoft.com/library/vslangproj.projectproperties_properties.aspx) ersetzt, indem der Eigenschaftenname innerhalb der Trennzeichen `$` (ohne Berücksichtigung der Groß-/Kleinschreibung) eingeschlossen wird.</span><span class="sxs-lookup"><span data-stu-id="10a12-152">You can also have NuGet replace tokens with [Project Properties](https://msdn.microsoft.com/library/vslangproj.projectproperties_properties.aspx) by including the property name within `$` delimeters (case-insensitive).</span></span>

<span data-ttu-id="10a12-153">In der folgenden Datei `app.config.install.xdt` wird beispielsweise ein `appSettings`-Element mit den Werten `FullPath`, `FileName`, und `ActiveConfigurationSettings` des Projekts in `app.config` eingefügt:</span><span class="sxs-lookup"><span data-stu-id="10a12-153">For example, the following `app.config.install.xdt` file will insert an `appSettings` element into `app.config` containing the `FullPath`, `FileName`, and `ActiveConfigurationSettings` values from the project:</span></span>

```xml
<?xml version="1.0"?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
    <appSettings xdt:Transform="Insert">
        <add key="FullPath" value="$FullPath$" />
        <add key="FileName" value="$filename$" />
        <add key="ActiveConfigurationSettings " value="$ActiveConfigurationSettings$" />
    </appSettings>
</configuration>
```

<span data-ttu-id="10a12-154">In einem weiteren Beispiel wird davon ausgegangen, dass das Projekt zu Beginn folgende Inhalte in der Datei `web.config` aufweist:</span><span class="sxs-lookup"><span data-stu-id="10a12-154">For another example, suppose the project initially contains the following content in `web.config`:</span></span>

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
        </modules>
    <system.webServer>
</configuration>
```

<span data-ttu-id="10a12-155">Wenn Sie während der Paketinstallation ein `MyNuModule`-Element zum Abschnitt `modules` hinzufügen möchten, würde die Datei `web.config.install.xdt` des Pakets Folgendes enthalten:</span><span class="sxs-lookup"><span data-stu-id="10a12-155">To add a `MyNuModule` element to the `modules` section during package install, the package's `web.config.install.xdt` would contain the following:</span></span>

```xml
<?xml version="1.0"?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
    <system.webServer>
        <modules>
            <add name="MyNuModule" type="Sample.MyNuModule" xdt:Transform="Insert" />
        </modules>
    </system.webServer>
</configuration>
```

<span data-ttu-id="10a12-156">Nach der Installation des Pakets sieht `web.config` wie folgt aus:</span><span class="sxs-lookup"><span data-stu-id="10a12-156">After installing the package, `web.config` will look like this:</span></span>

```xml
<configuration>
    <system.webServer>
        <modules>
            <add name="ContosoUtilities" type="Contoso.Utilities" />
            <add name="MyNuModule" type="Sample.MyNuModule" />
        </modules>
    <system.webServer>
</configuration>
```

<span data-ttu-id="10a12-157">Damit während der Deinstallation des Pakets nur das Element `MyNuModule` entfernt wird, sollte die Datei `web.config.uninstall.xdt` Folgendes enthalten:</span><span class="sxs-lookup"><span data-stu-id="10a12-157">To remove only the `MyNuModule` element during package uninstall, the `web.config.uninstall.xdt` file should contain the following:</span></span>

```xml
<?xml version="1.0"?>
<configuration xmlns:xdt="http://schemas.microsoft.com/XML-Document-Transform">
    <system.webServer>
        <modules>
            <add name="MyNuModule" xdt:Transform="Remove" xdt:Locator="Match(name)" />
        </modules>
    </system.webServer>
</configuration>
```
