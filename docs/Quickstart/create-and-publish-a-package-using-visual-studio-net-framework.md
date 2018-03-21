---
title: "Einführender Leitfaden für das Erstellen und Veröffentlichen eines .NET Framework NuGet-Pakets mithilfe von Visual Studio | Microsoft-Dokumentation"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 03/13/2018
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
description: "Eine exemplarische Vorgehensweise zum Erstellen und Veröffentlichen eines .NET Framework NuGet-Pakets mit Visual Studio 2017."
keywords: "NuGet-Paketerstellung, NuGet-Paketveröffentlichung, NuGet-Tutorial, NuGet-Paket in Visual Studio erstellen, MSBuild-Pack"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 613cb6e8cf5762f354d69aa271c1e2f0d4851c97
ms.sourcegitcommit: 74c21b406302288c158e8ae26057132b12960be8
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/15/2018
---
# <a name="create-and-publish-a-package-using-visual-studio-net-framework"></a><span data-ttu-id="d65e7-104">Erstellen und Veröffentlichen eines Pakets mithilfe von Visual Studio (.NET Framework)</span><span class="sxs-lookup"><span data-stu-id="d65e7-104">Create and publish a package using Visual Studio (.NET Framework)</span></span>

<span data-ttu-id="d65e7-105">Das Erstellen eines NuGet-Pakets aus einer .NET Framework-Klassenbibliothek umfasst das Erstellen der DLL in Visual Studio, gefolgt von der Verwendung des Befehlszeilentools „nuget.exe“ zum Erstellen und Veröffentlichen des Pakets.</span><span class="sxs-lookup"><span data-stu-id="d65e7-105">Creating a NuGet package from a .NET Framework Class Library involves creating the DLL in Visual Studio, then using the nuget.exe command line tool to create and publish the package.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="d65e7-106">Erforderliche Komponenten</span><span class="sxs-lookup"><span data-stu-id="d65e7-106">Prerequisites</span></span>

1. <span data-ttu-id="d65e7-107">Installieren Sie über [visualstudio.com](https://www.visualstudio.com/) eine beliebige Edition von Visual Studio 2017 mit einer beliebigen .NET-bezogenen Workload.</span><span class="sxs-lookup"><span data-stu-id="d65e7-107">Install any edition of Visual Studio 2017 from [visualstudio.com](https://www.visualstudio.com/) with any .NET-related workload.</span></span> <span data-ttu-id="d65e7-108">Visual Studio 2017 enthält automatisch NuGet-Funktionen, wenn eine .NET-Workload installiert ist.</span><span class="sxs-lookup"><span data-stu-id="d65e7-108">Visual Studio 2017 automatically includes NuGet capabilities when a .NET workload is installed.</span></span>

1. <span data-ttu-id="d65e7-109">Installieren Sie die `nuget.exe`-CLI, indem Sie sie von [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe) herunterladen, die `.exe`-Datei in einen geeigneten Ordner speichern und den Ordner der Umgebungsvariable PATH hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="d65e7-109">Install the `nuget.exe` CLI by downloading it from [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), saving that `.exe` file to a suitable folder, and adding that folder to your PATH environment variable.</span></span>

1. <span data-ttu-id="d65e7-110">[Registrieren Sie sich für ein kostenloses Konto auf nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F), falls Sie noch kein Konto haben.</span><span class="sxs-lookup"><span data-stu-id="d65e7-110">[Register for a free account on nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) if you don't have one already.</span></span> <span data-ttu-id="d65e7-111">Wenn Sie ein neues Konto erstellen, wird Ihnen eine Bestätigungs-E-Mail gesendet.</span><span class="sxs-lookup"><span data-stu-id="d65e7-111">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="d65e7-112">Sie müssen das Konto bestätigen, bevor Sie ein Paket hochladen können.</span><span class="sxs-lookup"><span data-stu-id="d65e7-112">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="d65e7-113">Erstellen eines Klassenbibliotheksprojekts</span><span class="sxs-lookup"><span data-stu-id="d65e7-113">Create a class library project</span></span>

<span data-ttu-id="d65e7-114">Sie können ein vorhandenes Projekt in der .NET Framework-Klassenbibliothek für den Code verwenden, den Sie packen möchten, oder wie folgt ein einfaches Projekt erstellen:</span><span class="sxs-lookup"><span data-stu-id="d65e7-114">You can use an existing .NET Framework Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="d65e7-115">Klicken Sie in Visual Studio auf **Datei > Neu > Projekt**, wählen Sie den Knoten **Visual C#** und dann die Vorlage „Klassenbibliothek (.NET Framework)“ aus, nennen Sie das Projekt „AppLogger“, und klicken Sie dann auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="d65e7-115">In Visual Studio, choose **File > New > Project**, select the **Visual C#** node, select the "Class Library (.NET Framework)" template, name the project AppLogger, and click **OK**.</span></span>

1. <span data-ttu-id="d65e7-116">Klicken Sie mit der rechten Maustaste auf die resultierende Projektdatei, und wählen Sie **Erstellen** aus, um sicherzustellen, dass das Projekt ordnungsgemäß erstellt wurde.</span><span class="sxs-lookup"><span data-stu-id="d65e7-116">Right-click on the resulting project file and select **Build** to make sure the project was created properly.</span></span> <span data-ttu-id="d65e7-117">Die DLL befindet sich im Ordner „Debuggen“ (oder im Ordner „Release“, wenn Sie stattdessen diese Konfiguration erstellen).</span><span class="sxs-lookup"><span data-stu-id="d65e7-117">The DLL is found within the Debug folder (or Release if you build that configuration instead).</span></span>

<span data-ttu-id="d65e7-118">In einem echten NuGet-Paket implementieren Sie viele hilfreiche Features, mit denen andere Apps erstellen können.</span><span class="sxs-lookup"><span data-stu-id="d65e7-118">Within a real NuGet package, of course, you implement many useful features with which others can build applications.</span></span> <span data-ttu-id="d65e7-119">Sie können die Zielframeworks beliebig festlegen.</span><span class="sxs-lookup"><span data-stu-id="d65e7-119">You can also set the target frameworks however you like.</span></span> <span data-ttu-id="d65e7-120">Beispiele finden Sie in den Leitfäden zu [UWP](../guides/create-uwp-packages.md) und [Xamarin](../guides/create-packages-for-xamarin.md).</span><span class="sxs-lookup"><span data-stu-id="d65e7-120">For example, see the guides for [UWP](../guides/create-uwp-packages.md) and [Xamarin](../guides/create-packages-for-xamarin.md).</span></span>

<span data-ttu-id="d65e7-121">In dieser exemplarischen Vorgehensweise schreiben Sie jedoch keinen zusätzlichen Code, da eine Klassenbibliothek aus der Vorlage für die Erstellung eines Pakets ausreicht.</span><span class="sxs-lookup"><span data-stu-id="d65e7-121">For this walkthrough, however, you won't write any additional code because a class library from the template is sufficient to create a package.</span></span> <span data-ttu-id="d65e7-122">Wenn Sie noch immer Funktionscode für das Paket benötigen, verwenden Sie folgenden:</span><span class="sxs-lookup"><span data-stu-id="d65e7-122">Still, if you'd like some functional code for the package, use the following:</span></span>

```cs
using System;

namespace AppLogger
{
    public class Logger
    {
        public void Log(string text)
        {
            Console.WriteLine(text);
        }
    }
}
```

> [!Tip]
> <span data-ttu-id="d65e7-123">Sofern es keinen Grund dafür gibt, der dagegen spricht, ist .NET Standard das bevorzugte Ziel für NuGet-Pakete, da es die größte Kompatibilitätsreichweite für verarbeitende Projekte bietet.</span><span class="sxs-lookup"><span data-stu-id="d65e7-123">Unless you have a reason to choose otherwise, .NET Standard is the preferred target for NuGet packages, as it provides compatibility with the widest range of consuming projects.</span></span> <span data-ttu-id="d65e7-124">Informationen dazu finden Sie unter [Erstellen und Veröffentlichen eines Pakets mithilfe von Visual Studio (.NET Standard)](create-and-publish-a-package-using-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="d65e7-124">See [Create and publish a package using Visual Studio (.NET Standard)](create-and-publish-a-package-using-visual-studio.md).</span></span>

## <a name="configure-project-properties-for-the-package"></a><span data-ttu-id="d65e7-125">Konfigurieren der Projekteigenschaften für das Paket</span><span class="sxs-lookup"><span data-stu-id="d65e7-125">Configure project properties for the package</span></span>

<span data-ttu-id="d65e7-126">Ein NuGet-Paket enthält ein Manifest (eine `.nuspec`-Datei), das relevante Metadaten enthält, z.B. den Paketbezeichner, die Versionsnummer, die Beschreibung, usw.</span><span class="sxs-lookup"><span data-stu-id="d65e7-126">A NuGet package contains a manifest (a `.nuspec` file), that contains relevant metadata such as the package identifier, version number, description, and more.</span></span> <span data-ttu-id="d65e7-127">Einige von diesen Metadaten können direkt aus den Projekteigenschaften entnommen werden, wodurch vermieden werden kann, dass diese im Projekt und im Manifest separat aktualisiert werden müssen.</span><span class="sxs-lookup"><span data-stu-id="d65e7-127">Some of these can be drawn from the project properties directly, which avoids having to separately update them in both the project and the manifest.</span></span> <span data-ttu-id="d65e7-128">Dieser Abschnitt beschreibt, wo die entsprechenden Eigenschaften festgelegt werden müssen.</span><span class="sxs-lookup"><span data-stu-id="d65e7-128">This section describes where to set the applicable properties.</span></span>

1. <span data-ttu-id="d65e7-129">Wählen Sie den Menübefehl **Projekt > Eigenschaften** und dann die Registerkarte **Anwendung** aus.</span><span class="sxs-lookup"><span data-stu-id="d65e7-129">Select the **Project > Properties** menu command, then select the **Application** tab.</span></span>

1. <span data-ttu-id="d65e7-130">Legen Sie im Feld **Assemblyname** einen eindeutigen Bezeichner für Ihr Paket fest.</span><span class="sxs-lookup"><span data-stu-id="d65e7-130">In the **Assembly name** field, give your package a unique identifier.</span></span>

    > [!Important]
    > <span data-ttu-id="d65e7-131">Sie müssen dem Paket einen Bezeichner zuweisen, der auf nuget.org bzw. auf dem Host, den Sie verwenden, einzigartig ist.</span><span class="sxs-lookup"><span data-stu-id="d65e7-131">You must give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="d65e7-132">Für diese exemplarische Vorgehensweise wird empfohlen, im Namen „Sample“ oder „Test“ zu verwenden, da der Name in einem späteren Veröffentlichungsschritt öffentlich sichtbar gemacht wird (auch wenn es unwahrscheinlich ist, dass jemand versucht, es zu verwenden).</span><span class="sxs-lookup"><span data-stu-id="d65e7-132">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>
    >
    > <span data-ttu-id="d65e7-133">Bei dem Versuch, ein Paket mit einem Namen zu veröffentlichen, der bereits vorhanden ist, wird Ihnen ein Fehler angezeigt.</span><span class="sxs-lookup"><span data-stu-id="d65e7-133">If you attempt to publish a package with a name that already exists, you see an error.</span></span>

1. <span data-ttu-id="d65e7-134">Klicken Sie auf die Schaltfläche **Assemblyinformationen**, wodurch ein Dialogfeld geöffnet wird, in dem Sie weitere Eigenschaften eingeben können, die dann im Manifest übernommen werden (siehe [.nuspec file reference - replacement tokens (NUSPEC-Referenz: Ersetzungstoken)](../reference/nuspec.md#replacement-tokens)).</span><span class="sxs-lookup"><span data-stu-id="d65e7-134">Select the **Assembly Information...** button, which brings up a dialog box in which you can enter other properties that carry into the manifest (see [.nuspec file reference - replacement tokens](../reference/nuspec.md#replacement-tokens)).</span></span> <span data-ttu-id="d65e7-135">Die am häufigsten verwendeten Felder sind **Titel**, **Beschreibung**, **Unternehmen**, **Copyright** und **Assemblyversion**.</span><span class="sxs-lookup"><span data-stu-id="d65e7-135">The most commonly used fields are **Title**, **Description**, **Company**, **Copyright**, and **Assembly version**.</span></span> <span data-ttu-id="d65e7-136">Diese Eigenschaften werden letztlich mit Ihrem Paket auf einem Host wie nuget.org angezeigt, weshalb Sie sich vergewissern sollten, dass diese ausführlich beschrieben sind.</span><span class="sxs-lookup"><span data-stu-id="d65e7-136">These properties ultimately appear with your package on a host like nuget.org, so make sure they're fully descriptive.</span></span>

    ![Assemblyinformationen in einem .NET Framework-Projekt in Visual Studio](media/qs_create-vs-01b-project-properties.png)

1. <span data-ttu-id="d65e7-138">Optional: Öffnen Sie zum direkten Anzeigen und Bearbeiten der Eigenschaften die Datei `Properties/AssemblyInfo.cs` im Projekt.</span><span class="sxs-lookup"><span data-stu-id="d65e7-138">Optional: to see and edit the properties directly, open the `Properties/AssemblyInfo.cs` file in the project.</span></span>

1. <span data-ttu-id="d65e7-139">Wenn die Eigenschaften festgelegt sind, legen Sie die Projektkonfiguration auf **Release** fest, und erstellen Sie das Projekt neu, um die aktualisierte DLL zu generieren.</span><span class="sxs-lookup"><span data-stu-id="d65e7-139">When the properties are set, set the project configuration to **Release** and rebuild the project to generate the updated DLL.</span></span>

## <a name="generate-the-initial-manifest"></a><span data-ttu-id="d65e7-140">Erstellen des ersten Manifests</span><span class="sxs-lookup"><span data-stu-id="d65e7-140">Generate the initial manifest</span></span>

<span data-ttu-id="d65e7-141">Mit einer DLL und den festgelegten Projekteigenschaften können Sie nun den Befehl `nuget spec` verwenden, um eine `.nuspec`-Startdatei aus dem Projekt zu erstellen.</span><span class="sxs-lookup"><span data-stu-id="d65e7-141">With a DLL in hand and project properties set, you now use the `nuget spec` command to generate an initial `.nuspec` file from the project.</span></span> <span data-ttu-id="d65e7-142">Dieser Schritt umfasst die relevanten Ersetzungstoken zum Auslesen von Informationen aus der Projektdatei.</span><span class="sxs-lookup"><span data-stu-id="d65e7-142">This step includes the relevant replacement tokens to draw information from the project file.</span></span>

<span data-ttu-id="d65e7-143">Führen Sie `nuget spec` nur einmal aus, um das Startmanifest zu generieren.</span><span class="sxs-lookup"><span data-stu-id="d65e7-143">You run `nuget spec` only once to generate the initial manifest.</span></span> <span data-ttu-id="d65e7-144">Beim Aktualisieren des Pakets ändern Sie die Werte in Ihrem Projekt, oder Sie bearbeiten das Manifest direkt.</span><span class="sxs-lookup"><span data-stu-id="d65e7-144">When updating the package, you either change values in your project or edit the manifest directly.</span></span>

1. <span data-ttu-id="d65e7-145">Öffnen Sie eine Eingabeaufforderung, und navigieren Sie zum Projektordner, der die Datei `AppLogger.csproj` enthält.</span><span class="sxs-lookup"><span data-stu-id="d65e7-145">Open a command prompt and navigate to the project folder containing `AppLogger.csproj` file.</span></span>

1. <span data-ttu-id="d65e7-146">Führen Sie den folgenden Befehl aus: `nuget spec AppLogger.csproj`</span><span class="sxs-lookup"><span data-stu-id="d65e7-146">Run the following command: `nuget spec AppLogger.csproj`.</span></span> <span data-ttu-id="d65e7-147">Durch das Angeben eines Projekts erstellt NuGet ein Manifest, das dem Namen des Projekts entspricht, in diesem Fall `AppLogger.nuspec`.</span><span class="sxs-lookup"><span data-stu-id="d65e7-147">By specifying a project, NuGet creates a manifest that matches the name of the project, in this case `AppLogger.nuspec`.</span></span> <span data-ttu-id="d65e7-148">Ebenfalls werden die Ersetzungstoken im Manifest eingeschlossen.</span><span class="sxs-lookup"><span data-stu-id="d65e7-148">It also include replacement tokens in the manifest.</span></span>

1. <span data-ttu-id="d65e7-149">Öffnen Sie `AppLogger.nuspec` in einem Text-Editor, um die Inhalte zu überprüfen, die wie folgt angezeigt werden sollten:</span><span class="sxs-lookup"><span data-stu-id="d65e7-149">Open `AppLogger.nuspec` in a text editor to examine its contents, which should appear as follows:</span></span>

    ```xml
    <?xml version="1.0"?>
    <package >
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
        <copyright>Copyright 2018</copyright>
        <tags>Tag1 Tag2</tags>
      </metadata>
    </package>
    ```

## <a name="edit-the-manifest"></a><span data-ttu-id="d65e7-150">Bearbeiten des Manifests</span><span class="sxs-lookup"><span data-stu-id="d65e7-150">Edit the manifest</span></span>

1. <span data-ttu-id="d65e7-151">NuGet löst einen Fehler aus, wenn Sie versuchen, ein Paket mit Standardwerten in Ihrer `.nuspec`-Datei zu erstellen. Bevor Sie fortfahren können, müssen Sie deshalb die folgenden Felder bearbeiten.</span><span class="sxs-lookup"><span data-stu-id="d65e7-151">NuGet produces an error if you try to create a package with default values in your `.nuspec` file, so you must edit the following fields before proceeding.</span></span> <span data-ttu-id="d65e7-152">Eine Beschreibung dazu, wie diese verwendet werden, finden Sie unter [.nuspec file reference - single elements (NUSPEC-Referenz: Einzelne Elemente)](../reference/nuspec.md#single-elements).</span><span class="sxs-lookup"><span data-stu-id="d65e7-152">See [.nuspec file reference - single elements](../reference/nuspec.md#single-elements) for a description of how these are used.</span></span>

    - <span data-ttu-id="d65e7-153">licenseUrl</span><span class="sxs-lookup"><span data-stu-id="d65e7-153">licenseUrl</span></span>
    - <span data-ttu-id="d65e7-154">projectUrl</span><span class="sxs-lookup"><span data-stu-id="d65e7-154">projectUrl</span></span>
    - <span data-ttu-id="d65e7-155">iconUrl</span><span class="sxs-lookup"><span data-stu-id="d65e7-155">iconUrl</span></span>
    - <span data-ttu-id="d65e7-156">releaseNotes</span><span class="sxs-lookup"><span data-stu-id="d65e7-156">releaseNotes</span></span>
    - <span data-ttu-id="d65e7-157">Tags</span><span class="sxs-lookup"><span data-stu-id="d65e7-157">tags</span></span>

1. <span data-ttu-id="d65e7-158">Bei Paketen für die öffentliche Nutzung sollten Sie besonders auf die **Tags**-Eigenschaft achten, da Tags anderen dabei helfen, Ihr Paket auf Quellen wie nuget.org zu finden und dessen Funktion zu verstehen.</span><span class="sxs-lookup"><span data-stu-id="d65e7-158">For packages built for public consumption, pay special attention to the **Tags** property, as tags help others find your package on sources like nuget.org and understand what it does.</span></span>

1. <span data-ttu-id="d65e7-159">Zu diesem Zeitpunkt können Sie auch weitere Elemente zu Ihrem Manifest hinzufügen, wie unter [.nuspec file reference (NUSPEC-Referenz)](../reference/nuspec.md) beschrieben wird.</span><span class="sxs-lookup"><span data-stu-id="d65e7-159">You can also add any other elements to the manifest at this time, as described on [.nuspec file reference](../reference/nuspec.md).</span></span>

1. <span data-ttu-id="d65e7-160">Speichern Sie die Datei, bevor Sie fortfahren.</span><span class="sxs-lookup"><span data-stu-id="d65e7-160">Save the file before proceeding.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="d65e7-161">Ausführen des Befehls pack</span><span class="sxs-lookup"><span data-stu-id="d65e7-161">Run the pack command</span></span>

1. <span data-ttu-id="d65e7-162">Führen Sie den Befehl `nuget pack` über eine Eingabeaufforderung im Ordner mit Ihrer `.nuspec`-Datei aus.</span><span class="sxs-lookup"><span data-stu-id="d65e7-162">From a command prompt in the folder containing your `.nuspec` file, run the command `nuget pack`.</span></span>

1. <span data-ttu-id="d65e7-163">NuGet generiert im aktuellen Ordner eine `.nupkg`-Datei in Form von *identifier-version.nupkg*.</span><span class="sxs-lookup"><span data-stu-id="d65e7-163">NuGet generates a `.nupkg` file in the form of *identifier-version.nupkg*, which you'll find in the current folder.</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="d65e7-164">Veröffentlichen des Pakets</span><span class="sxs-lookup"><span data-stu-id="d65e7-164">Publish the package</span></span>

<span data-ttu-id="d65e7-165">Sobald Sie eine `.nupkg`-Datei haben, können Sie diese, gemeinsam mit einem API-Schlüssel von nuget.org, über `nuget.exe` auf nuget.org veröffentlichen. Für nuget.org benötigen Sie `nuget.exe` 4.1.0 oder höher.</span><span class="sxs-lookup"><span data-stu-id="d65e7-165">Once you have a `.nupkg` file, you publish it to nuget.org using `nuget.exe` with an API key acquired from nuget.org. For nuget.org you must use `nuget.exe` 4.1.0 or higher.</span></span>

[!INCLUDE[publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="d65e7-166">Erwerben des API-Schlüssels</span><span class="sxs-lookup"><span data-stu-id="d65e7-166">Acquire your API key</span></span>

[!INCLUDE[publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-nuget-push"></a><span data-ttu-id="d65e7-167">Veröffentlichen mit dem Befehl „nuget push“</span><span class="sxs-lookup"><span data-stu-id="d65e7-167">Publish with nuget push</span></span>

1. <span data-ttu-id="d65e7-168">Navigieren Sie zum Ordner, der die `.nupkg`-Datei enthält.</span><span class="sxs-lookup"><span data-stu-id="d65e7-168">Change to the folder containing the `.nupkg` file.</span></span>

1. <span data-ttu-id="d65e7-169">Führen Sie den folgenden Befehl aus, geben Sie dabei Ihren Paketnamen an, und ersetzen Sie den Schlüsselwert durch Ihren API-Schlüssel:</span><span class="sxs-lookup"><span data-stu-id="d65e7-169">Run the following command, specifying your package name and replacing the key value with your API key:</span></span>

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="d65e7-170">In „NuGet.exe“ werden die Ergebnisse des Veröffentlichungsvorgangs angezeigt:</span><span class="sxs-lookup"><span data-stu-id="d65e7-170">nuget.exe displays the results of the publishing process:</span></span>

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

<span data-ttu-id="d65e7-171">Siehe [nuget push-Befehl](../tools/cli-ref-push.md).</span><span class="sxs-lookup"><span data-stu-id="d65e7-171">See [nuget push](../tools/cli-ref-push.md).</span></span>

### <a name="publish-errors"></a><span data-ttu-id="d65e7-172">Veröffentlichungsfehler</span><span class="sxs-lookup"><span data-stu-id="d65e7-172">Publish errors</span></span>

[!INCLUDE[publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="d65e7-173">Verwalten des veröffentlichten Pakets</span><span class="sxs-lookup"><span data-stu-id="d65e7-173">Manage the published package</span></span>

[!INCLUDE[publish-manage](includes/publish-manage.md)]

## <a name="related-topics"></a><span data-ttu-id="d65e7-174">Verwandte Themen</span><span class="sxs-lookup"><span data-stu-id="d65e7-174">Related topics</span></span>

- [<span data-ttu-id="d65e7-175">Erstellen eines Pakets</span><span class="sxs-lookup"><span data-stu-id="d65e7-175">Create a Package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="d65e7-176">Veröffentlichen eines Pakets</span><span class="sxs-lookup"><span data-stu-id="d65e7-176">Publish a Package</span></span>](../create-packages/publish-a-package.md)
- [<span data-ttu-id="d65e7-177">Unterstützung mehrerer Zielframeworks</span><span class="sxs-lookup"><span data-stu-id="d65e7-177">Support multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="d65e7-178">Paketversionsverwaltung</span><span class="sxs-lookup"><span data-stu-id="d65e7-178">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="d65e7-179">Erstellen von lokalisierten Paketen</span><span class="sxs-lookup"><span data-stu-id="d65e7-179">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
