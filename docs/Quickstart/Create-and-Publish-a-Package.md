---
title: "Einführender Leitfaden zur Erstellung und Veröffentlichung eines NuGet-Pakets | Microsoft-Dokumentation"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/3/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: 91781ed6-da5c-49f0-b973-16dd8ad84229
description: "Eine exemplarische Vorgehensweise zur Erstellung und Veröffentlichung eines NuGet-Pakets mit der Befehlszeilenschnittstelle von „NuGet.exe“ und Visual Studio."
keywords: "NuGet-Paketerstellung, NuGet-Paketveröffentlichung, NuGet-Tutorial"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 36a7c2b1d056dddf07a59737de1c3e94294689ac
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/14/2017
---
# <a name="create-and-publish-a-package"></a><span data-ttu-id="7a9a7-104">Erstellen und Veröffentlichen eines Pakets</span><span class="sxs-lookup"><span data-stu-id="7a9a7-104">Create and publish a package</span></span>

<span data-ttu-id="7a9a7-105">Ein NuGet-Paket kann problemlos über eine .NET-Klassenbibliothek erstellt und auf nuget.org veröffentlicht werden. Die folgenden Schritte führen Sie durch den Prozess, bei dem die NuGet-Befehlszeilenschnittstelle (Command-Line Interface, CLI) und Visual Studio verwendet werden:</span><span class="sxs-lookup"><span data-stu-id="7a9a7-105">It's a simple process to create a NuGet package from a .NET Class Library and publish it to nuget.org. The following steps walk you through the process using the NuGet command-line interface (CLI) and Visual Studio:</span></span>

- [<span data-ttu-id="7a9a7-106">Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="7a9a7-106">Pre-requisites</span></span>](#install-pre-requisites)
- [<span data-ttu-id="7a9a7-107">Erstellen der NUSPEC-Paketmanifestdatei</span><span class="sxs-lookup"><span data-stu-id="7a9a7-107">Create the .nuspec package manifest file</span></span>](#create-the-nuspec-package-manifest-file)
- [<span data-ttu-id="7a9a7-108">Ausführen des Befehls pack</span><span class="sxs-lookup"><span data-stu-id="7a9a7-108">Run the pack command</span></span>](#run-the-pack-command)
- [<span data-ttu-id="7a9a7-109">Veröffentlichen des Pakets</span><span class="sxs-lookup"><span data-stu-id="7a9a7-109">Publish the package</span></span>](#publish-the-package)

## <a name="pre-requisites"></a><span data-ttu-id="7a9a7-110">Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="7a9a7-110">Pre-requisites</span></span>

1. <span data-ttu-id="7a9a7-111">Installieren Sie eine beliebige Edition von Visual Studio 2017 über [visualstudio.com](https://www.visualstudio.com/).</span><span class="sxs-lookup"><span data-stu-id="7a9a7-111">Install any edition of Visual Studio 2017 from [visualstudio.com](https://www.visualstudio.com/).</span></span>

1. <span data-ttu-id="7a9a7-112">Installieren Sie das NuGet-CLI-Tool, `nuget.exe`, indem Sie die aktuelle Version von `nuget.exe` über [nuget.org/downloads](https://nuget.org/downloads) herunterladen, und speichern Sie die `.exe` an einem Speicherort in Ihrem Pfad.</span><span class="sxs-lookup"><span data-stu-id="7a9a7-112">Install the NuGet CLI tool, `nuget.exe`, by downloading the latest version of `nuget.exe` from [nuget.org/downloads](https://nuget.org/downloads), and saving the `.exe` to a location in your PATH.</span></span> <span data-ttu-id="7a9a7-113">Beachten Sie, dass es sich bei dem Download um *das Tool selbst* handelt, nicht um einen Installer.</span><span class="sxs-lookup"><span data-stu-id="7a9a7-113">Note that the download *is* the tool itself, not an installer.</span></span>

1. <span data-ttu-id="7a9a7-114">Erstellen Sie für den zu verpackenden Code ein geeignetes Projekt in der .NET-Klassenbibliothek.</span><span class="sxs-lookup"><span data-stu-id="7a9a7-114">Create a suitable .NET Class Library project for the code you want to package.</span></span> <span data-ttu-id="7a9a7-115">Wenn Sie noch nicht über ein Projekt verfügen, können Sie ein einfaches Projekt erstellen, indem Sie wie folgt vorgehen:</span><span class="sxs-lookup"><span data-stu-id="7a9a7-115">If you don't already have a project, you can create a simple one as follows:</span></span>
    1. <span data-ttu-id="7a9a7-116">Wählen Sie in Visual Studio **Datei > Neu > Projekt** aus, erweitern Sie den Knoten **Visual C#-> Windows**, wählen Sie die Vorlage „Klassenbibliothek“ aus, geben Sie dem Projekt den Namen AppLogger, und klicken Sie auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="7a9a7-116">In Visual Studio, choose **File > New > Project**, expand the **Visual C# > Windows** node, select the "Class Library" template, name the project AppLogger, and click **OK**.</span></span>
    1. <span data-ttu-id="7a9a7-117">Klicken Sie mit der rechten Maustaste auf die resultierende Projektdatei, und wählen Sie **Erstellen** aus, um sicherzustellen, dass das Projekt ordnungsgemäß erstellt wurde.</span><span class="sxs-lookup"><span data-stu-id="7a9a7-117">Right-click on the resulting project file and select **Build** to make sure the project was created properly.</span></span> <span data-ttu-id="7a9a7-118">Die DLL befindet sich im Ordner „Debuggen“ (oder im Ordner „Release“, wenn Sie stattdessen diese Konfiguration erstellen).</span><span class="sxs-lookup"><span data-stu-id="7a9a7-118">The DLL is found within the Debug folder (or Release if you build that configuration instead).</span></span>

    <span data-ttu-id="7a9a7-119">In einem echten NuGet-Paket implementieren Sie natürlich viele hilfreiche Features, mit denen unter anderem Apps erstellt werden können.</span><span class="sxs-lookup"><span data-stu-id="7a9a7-119">Within a real NuGet package, of course, you'll implement many useful features upon which others can build applications.</span></span> <span data-ttu-id="7a9a7-120">In dieser exemplarischen Vorgehensweise schreiben Sie jedoch keinen zusätzlichen Code, da eine Klassenbibliothek aus der Vorlage für die Erstellung eines Pakets ausreicht.</span><span class="sxs-lookup"><span data-stu-id="7a9a7-120">For this walkthrough, however, you won't write any additional code because a class library from the template is sufficient to create a package.</span></span>

## <a name="create-the-nuspec-package-manifest-file"></a><span data-ttu-id="7a9a7-121">Erstellen der NUSPEC-Paketmanifestdatei</span><span class="sxs-lookup"><span data-stu-id="7a9a7-121">Create the .nuspec package manifest file</span></span>

<span data-ttu-id="7a9a7-122">Für jedes NuGet-Paket ist für die Beschreibung der zugehörigen Inhalte und Abhängigkeiten ein Manifest, &mdash;eine `.nuspec`-Datei&mdash;, erforderlich.</span><span class="sxs-lookup"><span data-stu-id="7a9a7-122">Every NuGet package needs a manifest&mdash;a `.nuspec` file&mdash;to describe its contents and its dependencies.</span></span> <span data-ttu-id="7a9a7-123">Der Befehl `nuget spec` erstellt diese Datei für Sie, die Sie anschließend anpassen können.</span><span class="sxs-lookup"><span data-stu-id="7a9a7-123">The `nuget spec` command creates this file for you, which you then customize.</span></span> <span data-ttu-id="7a9a7-124">In diesem Beispiel erstellen Sie die `.nuspec`-Datei aus einer Projektdatei; Sie können das Manifest auch mithilfe anderer Methoden erstellen, wie unter [Erstellen eines Pakets](../create-packages/creating-a-package.md) beschrieben.</span><span class="sxs-lookup"><span data-stu-id="7a9a7-124">In this example you create the `.nuspec` from a project file; you can also create the manifest through other means as described on [Create a Package](../create-packages/creating-a-package.md).</span></span>

1. <span data-ttu-id="7a9a7-125">Öffnen Sie eine Eingabeaufforderung, und navigieren Sie zu dem Ordner mit Ihrer Projektdatei (`.csproj`).</span><span class="sxs-lookup"><span data-stu-id="7a9a7-125">Open a command prompt and navigate to the folder containing your project file (`.csproj`).</span></span>

1. <span data-ttu-id="7a9a7-126">Führen Sie den NuGet-CLI-Befehl `spec` aus, um das Manifest zu generieren, das nach Ihrem Projekt benannt wird, z.B. `AppLogger.nuspec`:</span><span class="sxs-lookup"><span data-stu-id="7a9a7-126">Run the NuGet CLI `spec` command to generate the manifest, which is named after your project, such as `AppLogger.nuspec`:</span></span>

    ```
    nuget spec
    ```

1. <span data-ttu-id="7a9a7-127">Öffnen Sie die Datei in einem Text-Editor.</span><span class="sxs-lookup"><span data-stu-id="7a9a7-127">Open the file in a text editor.</span></span> <span data-ttu-id="7a9a7-128">Das Manifest sieht in etwa wie der folgende Code aus. Dabei werden die Token im Format *$`<token>`$* während des Paketerstellungsprozesses durch Werte aus der Datei „Properties/AssemblyInfo.cs“ des Projekts ersetzt.</span><span class="sxs-lookup"><span data-stu-id="7a9a7-128">The manifest looks something like the code below, where tokens in the form *$`<token>`$* are be replaced during the packaging process with values from the project's Properties/AssemblyInfo.cs file.</span></span> <span data-ttu-id="7a9a7-129">Weitere Einzelheiten zu Token finden Sie unter [Erstellen einer NUSPEC-Datei](../create-packages/creating-a-package.md#creating-the-nuspec-file).</span><span class="sxs-lookup"><span data-stu-id="7a9a7-129">For more details on tokens, see [Creating a .nuspec file](../create-packages/creating-a-package.md#creating-the-nuspec-file).</span></span>

    ```xml
    <?xml version="1.0"?>
    <package>
        <metadata>
        <id>$id$</id>
        <version>$version$</version>
        <title>$title$</title>
        <authors>$author$</authors>
        <owners>$author$</owners>
        <licenseUrl>http://LICENSE_URL_HERE_OR_DELETE_THIS_LINE</licenseUrl>
        <projectUrl>http://PROJECT_URL_HERE_OR_DELETE_THIS_LINE</projectUrl>
        <iconUrl>http://ICON_URL_HERE_OR_DELETE_THIS_LINE</iconUrl>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>$description$</description>
        <releaseNotes>Summary of changes made in this release of the package.</releaseNotes>
        <copyright>Copyright 2016</copyright>
        <tags>Tag1 Tag2</tags>
        </metadata>
    </package>
    ```

1. <span data-ttu-id="7a9a7-130">Wählen Sie eine Paket-ID aus, die auf nuget.org websiteübergreifend eindeutig ist. Es wird empfohlen, die unter [Erstellen eines Pakets](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number) beschriebenen Namenskonventionen zu verwenden.</span><span class="sxs-lookup"><span data-stu-id="7a9a7-130">Select a package ID that is unique across nuget.org. We recommend using the naming conventions described in [Creating a package](../create-packages/creating-a-package.md#choosing-a-unique-package-identifier-and-setting-the-version-number).</span></span> <span data-ttu-id="7a9a7-131">Achten Sie darauf, dass Sie die die Author- und Description-Tags aktualisieren. Andernfalls tritt im nächsten Schritt ein Fehler auf.</span><span class="sxs-lookup"><span data-stu-id="7a9a7-131">Be sure to update the author and description tags or you get an error in the next step.</span></span> <span data-ttu-id="7a9a7-132">Im Folgenden wird eine aktualisierte `.nuspec`-Datei als Beispiel aufgeführt:</span><span class="sxs-lookup"><span data-stu-id="7a9a7-132">Here's an updated `.nuspec` file as an example:</span></span>

    ```xml
    <?xml version="1.0"?>
    <package>
        <metadata>
        <id>MyCompanyName.MyProductName.MyPackageName</id>
        <version>$version$</version>
        <title>$title$</title>
        <authors>kraigb</authors>
        <owners>kraigb</owners>
        <requireLicenseAcceptance>false</requireLicenseAcceptance>
        <description>Awesome application logging utility</description>
        <releaseNotes>First release</releaseNotes>
        <copyright>Copyright 2016</copyright>
        <tags>application app logger logging logs</tags>
        </metadata>
    </package>
    ```

> [!Note]
> <span data-ttu-id="7a9a7-133">Bei Paketen, die für die öffentliche Nutzung bereitgestellt werden, sollten Sie besonders auf das `<tags>`-Element achten, da diese Tags andere Personen dabei unterstützen, nach Ihrem Paket zu suchen und dessen Zweck nachzuvollziehen.</span><span class="sxs-lookup"><span data-stu-id="7a9a7-133">For packages built for public consumption, pay special attention to the `<tags>` element, as these tags help others find your package and understand what it does.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="7a9a7-134">Ausführen des Befehls pack</span><span class="sxs-lookup"><span data-stu-id="7a9a7-134">Run the pack command</span></span>

<span data-ttu-id="7a9a7-135">Führen Sie den Befehl `pack` aus, um ein NuGet-Paket (eine `.nupkg`-Datei) aus einem Projekt zu erstellen:</span><span class="sxs-lookup"><span data-stu-id="7a9a7-135">To build a NuGet package (a `.nupkg` file) from a project, run the `pack` command:</span></span>

```
nuget pack AppLogger.csproj
```

<span data-ttu-id="7a9a7-136">Dieser Befehl erstellt `AppLogger.1.0.0.0.nupkg` mithilfe des Paketnamens und der Versionsnummer aus der `.nuspec`-Datei.</span><span class="sxs-lookup"><span data-stu-id="7a9a7-136">This command creates `AppLogger.1.0.0.0.nupkg` using the package name and version number from the `.nuspec` file.</span></span> <span data-ttu-id="7a9a7-137">Der Befehl gibt Warnungen aus, wenn Sie die Standardwerte der verschiedenen Felder in der `.nuspec`-Datei nicht aktualisiert haben.</span><span class="sxs-lookup"><span data-stu-id="7a9a7-137">The command issues warnings if you haven't updated various fields in the `.nuspec` file from their default values.</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="7a9a7-138">Veröffentlichen des Pakets</span><span class="sxs-lookup"><span data-stu-id="7a9a7-138">Publish the package</span></span>

<span data-ttu-id="7a9a7-139">Sobald Sie eine `.nupkg`-Datei erstellt haben, veröffentlichen Sie diese mit dem Befehl `push` auf nuget.org.</span><span class="sxs-lookup"><span data-stu-id="7a9a7-139">Once you have a `.nupkg` file, you publish it to nuget.org using the `push` command.</span></span> <span data-ttu-id="7a9a7-140">(Alternativ können Sie den [Workflow für die Veröffentlichung auf nuget.org](../create-packages/publish-a-package.md#publish-to-nugetorg) verwenden.)</span><span class="sxs-lookup"><span data-stu-id="7a9a7-140">(Alternately, you can use the [nuget.org publishing workflow](../create-packages/publish-a-package.md#publish-to-nugetorg).</span></span>

> [!Warning]
> <span data-ttu-id="7a9a7-141">Die von Ihnen auf nuget.org veröffentlichten Pakete sind für andere Entwickler öffentlich sichtbar.</span><span class="sxs-lookup"><span data-stu-id="7a9a7-141">The packages you publish to nuget.org are publicly visible to other developers.</span></span> <span data-ttu-id="7a9a7-142">Informationen zum privaten Hosten von Paketen finden Sie unter [Hosting packages](../hosting-packages/overview.md) (Hosten von Paketen).</span><span class="sxs-lookup"><span data-stu-id="7a9a7-142">To host packages privately, see [Hosting packages](../hosting-packages/overview.md).</span></span>


1. <span data-ttu-id="7a9a7-143">Erstellen Sie auf [nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) ein kostenloses Konto, oder melden Sie sich an, wenn Sie bereits über ein Konto verfügen.</span><span class="sxs-lookup"><span data-stu-id="7a9a7-143">Create a free account on [nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F), or log in if you already have one.</span></span> <span data-ttu-id="7a9a7-144">Wenn Sie ein neues Konto erstellen, wird Ihnen eine Bestätigungs-E-Mail gesendet.</span><span class="sxs-lookup"><span data-stu-id="7a9a7-144">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="7a9a7-145">Sie müssen das Konto bestätigen, bevor Sie ein Paket hochladen können.</span><span class="sxs-lookup"><span data-stu-id="7a9a7-145">You must confirm the account before you can upload a package.</span></span>

1. <span data-ttu-id="7a9a7-146">Wählen sie nach der Anmeldung Ihren Benutzernamen (oben rechts) und anschließend **API-Schlüssel** aus.</span><span class="sxs-lookup"><span data-stu-id="7a9a7-146">Once logged in, select your user name (on the upper right), then select **API Keys**.</span></span>

1. <span data-ttu-id="7a9a7-147">Wählen Sie **Erstellen** aus, geben Sie einen Namen für Ihren Schlüssel an, wählen Sie unter **API-Schlüssel** die Option **Bereiche auswählen > Push** aus, geben Sie * für **Globmuster** ein, und wählen Sie anschließend **Erstellen** aus.</span><span class="sxs-lookup"><span data-stu-id="7a9a7-147">Select **Create**, provide a name for your key, select **Select Scopes > Push**Under **API Key**, enter * for **Glob pattern**, then select **Create**.</span></span>

1. <span data-ttu-id="7a9a7-148">Nachdem der Schlüssel erstellt wurde, können Sie **Kopieren** auswählen, um den Zugriffsschlüssel abzurufen, den Sie in der CLI benötigen:</span><span class="sxs-lookup"><span data-stu-id="7a9a7-148">Once the key is created, select **Copy** to retrieve the access key you'll need in the CLI:</span></span>

    ![Kopieren des API-Schlüssels in die Zwischenablage](media/QS_Create-02-APIKey.png)

    > [!Warning]
    > <span data-ttu-id="7a9a7-150">Speichern Sie Ihren Schlüssel an einem sicheren Ort, und halten Sie ihn geheim.</span><span class="sxs-lookup"><span data-stu-id="7a9a7-150">Save your key in a secure location and keep is a secret.</span></span> <span data-ttu-id="7a9a7-151">Wenn Ihr Schlüssel versehentlich offengelegt wird, können Sie ihn jederzeit erneut generieren.</span><span class="sxs-lookup"><span data-stu-id="7a9a7-151">If your key is accidentally revealed, you can always regenerate it at any time.</span></span> <span data-ttu-id="7a9a7-152">Sie können den API-Schlüssel auch entfernen, wenn sie keine Pakete mehr mithilfe von Push über die CLI übertragen möchten.</span><span class="sxs-lookup"><span data-stu-id="7a9a7-152">You can also remove the API key if you no longer want to push packages via the CLI.</span></span>

1. <span data-ttu-id="7a9a7-153">Führen Sie den folgenden Befehl in einer Eingabeaufforderung aus; geben Sie dabei Ihren Paketnamen an und ersetzen Sie den Schlüssel durch den in Schritt 4 kopierten Wert:</span><span class="sxs-lookup"><span data-stu-id="7a9a7-153">At a command prompt, run the following command, specifying your package name and replacing the key with the value copied in step 4:</span></span>

    ```
    nuget push AppLogger.1.0.0.0.nupkg 47be3377-c434-4c29-8576-af7f6993a54b -Source https://api.nuget.org/v3/index.json
    ```
    
1. <span data-ttu-id="7a9a7-154">In „NuGet.exe“ werden die Ergebnisse des Veröffentlichungsvorgangs angezeigt:</span><span class="sxs-lookup"><span data-stu-id="7a9a7-154">nuget.exe displays the results of the publishing process:</span></span>

    ```
    Pushing AppLogger.1.0.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed. 
    ```

1. <span data-ttu-id="7a9a7-155">Wählen Sie in Ihrem Profil auf nuget.org **Pakete verwalten** aus, um das gerade veröffentlichte Paket anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="7a9a7-155">From your profile on nuget.org, Select **Manage Packages** to see the one you just published.</span></span> <span data-ttu-id="7a9a7-156">Sie erhalten auch eine Bestätigungs-E-Mail.</span><span class="sxs-lookup"><span data-stu-id="7a9a7-156">You also receive a confirmation email.</span></span> <span data-ttu-id="7a9a7-157">Beachten Sie, dass es möglicherweise etwas dauert, bis Ihr Paket indiziert wurde und anderen Benutzern in den Suchergebnissen angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="7a9a7-157">Note that it might take a while for your package to be indexed and appear in search results where others can find it.</span></span> <span data-ttu-id="7a9a7-158">In diesem Zeitraum wird auf Ihrer Paketseite folgende Nachricht angezeigt:</span><span class="sxs-lookup"><span data-stu-id="7a9a7-158">During that time your package page shows the message below:</span></span>

    ![Dieses Paket wurde noch nicht indiziert.](media/QS_Create-03-NotIndexed.png)

> [!Note]
> <span data-ttu-id="7a9a7-161">**Virenprüfung**: Alle auf nuget.org hochgeladenen Pakete werden auf Viren überprüft und abgelehnt, falls Viren erkannt werden.</span><span class="sxs-lookup"><span data-stu-id="7a9a7-161">**Virus scanning**: All packages uploaded to nuget.org are scanned for viruses and rejected if any viruses are found.</span></span> <span data-ttu-id="7a9a7-162">Alle auf nuget.org aufgelisteten Pakete werden zudem regelmäßig überprüft.</span><span class="sxs-lookup"><span data-stu-id="7a9a7-162">All packages listed on nuget.org are also scanned periodically.</span></span>

<span data-ttu-id="7a9a7-163">Und das ist schon alles!</span><span class="sxs-lookup"><span data-stu-id="7a9a7-163">And that's it!</span></span> <span data-ttu-id="7a9a7-164">Sie haben gerade Ihr erstes NuGet-Paket auf [nuget.org](https://www.nuget.org/) veröffentlicht, das andere Entwickler nun in ihren eigenen Projekten verwenden können.</span><span class="sxs-lookup"><span data-stu-id="7a9a7-164">You've just published your first NuGet package to [nuget.org](https://www.nuget.org/), that other developers can use in their own projects.</span></span>

## <a name="related-topics"></a><span data-ttu-id="7a9a7-165">Verwandte Themen</span><span class="sxs-lookup"><span data-stu-id="7a9a7-165">Related topics</span></span>

- [<span data-ttu-id="7a9a7-166">Erstellen eines Pakets</span><span class="sxs-lookup"><span data-stu-id="7a9a7-166">Create a Package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="7a9a7-167">Veröffentlichen eines Pakets</span><span class="sxs-lookup"><span data-stu-id="7a9a7-167">Publish a Package</span></span>](../create-packages/publish-a-package.md)
- [<span data-ttu-id="7a9a7-168">Unterstützung mehrerer Zielframeworks</span><span class="sxs-lookup"><span data-stu-id="7a9a7-168">Support multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="7a9a7-169">Paketversionsverwaltung</span><span class="sxs-lookup"><span data-stu-id="7a9a7-169">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="7a9a7-170">Erstellen von lokalisierten Paketen</span><span class="sxs-lookup"><span data-stu-id="7a9a7-170">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
