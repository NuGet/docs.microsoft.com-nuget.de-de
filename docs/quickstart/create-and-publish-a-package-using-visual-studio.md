---
title: Erstellen und Veröffentlichen eines .NET Standard-Pakets mithilfe von Visual Studio auf Windows
description: Exemplarische Vorgehensweise zum Erstellen und Veröffentlichen eines .NET Standard-NuGet-Pakets mit Visual Studio 2017 auf Windows.
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: quickstart
ms.openlocfilehash: c75785d361f25564c8a59d7a2d85924c570a7b9a
ms.sourcegitcommit: b9a134a6e10d7d8502613f389f7d5f9b9e206ec8
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/28/2019
ms.locfileid: "67467815"
---
# <a name="quickstart-create-and-publish-a-nuget-package-using-visual-studio-net-standard-windows-only"></a><span data-ttu-id="fd623-103">Schnellstart: Erstellen und Veröffentlichen eines NuGet-Pakets mithilfe von Visual Studio (.NET Standard, nur Windows)</span><span class="sxs-lookup"><span data-stu-id="fd623-103">Quickstart: Create and publish a NuGet package using Visual Studio (.NET Standard, Windows only)</span></span>

<span data-ttu-id="fd623-104">Ein NuGet-Paket kann problemlos über eine .NET Standard-Klassenbibliothek in Visual Studio unter Windows erstellt und dann durch Verwendung eines CLI-Tools auf nuget.org veröffentlicht werden.</span><span class="sxs-lookup"><span data-stu-id="fd623-104">It's a simple process to create a NuGet package from a .NET Standard Class Library in Visual Studio on Windows, and then publish it to nuget.org using a CLI tool.</span></span>

> [!Note]
> <span data-ttu-id="fd623-105">Dieser Schnellstart gilt ausschließlich für Visual Studio 2017 für Windows.</span><span class="sxs-lookup"><span data-stu-id="fd623-105">This Quickstart applies to Visual Studio 2017 for Windows only.</span></span> <span data-ttu-id="fd623-106">Visual Studio für Mac enthält nicht die hier beschriebenen Funktionen.</span><span class="sxs-lookup"><span data-stu-id="fd623-106">Visual Studio for Mac does not include the capabilities described here.</span></span> <span data-ttu-id="fd623-107">Verwenden Sie stattdessen die [dotnet-CLI-Tools](create-and-publish-a-package-using-the-dotnet-cli.md).</span><span class="sxs-lookup"><span data-stu-id="fd623-107">Use the [dotnet CLI tools](create-and-publish-a-package-using-the-dotnet-cli.md) instead.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="fd623-108">Erforderliche Komponenten</span><span class="sxs-lookup"><span data-stu-id="fd623-108">Prerequisites</span></span>

1. <span data-ttu-id="fd623-109">Installieren Sie über [visualstudio.com](https://www.visualstudio.com/) eine beliebige Edition von Visual Studio 2017 mit einer beliebigen .NET-bezogenen Workload.</span><span class="sxs-lookup"><span data-stu-id="fd623-109">Install any edition of Visual Studio 2017 from [visualstudio.com](https://www.visualstudio.com/) with any .NET-related workload.</span></span> <span data-ttu-id="fd623-110">Visual Studio 2017 enthält automatisch NuGet-Funktionen, wenn eine .NET-Workload installiert ist.</span><span class="sxs-lookup"><span data-stu-id="fd623-110">Visual Studio 2017 automatically includes NuGet capabilities when a .NET workload is installed.</span></span>

1. <span data-ttu-id="fd623-111">Installieren Sie eines der CLI-Tools.</span><span class="sxs-lookup"><span data-stu-id="fd623-111">Install one of the CLI tools.</span></span>

   * <span data-ttu-id="fd623-112">Für die `dotnet`-CLI installieren Sie das [.NET Core SDK](https://www.microsoft.com/net/download/).</span><span class="sxs-lookup"><span data-stu-id="fd623-112">For the `dotnet` CLI, install the [.NET Core SDK](https://www.microsoft.com/net/download/).</span></span> <span data-ttu-id="fd623-113">Die dotnet-CLI ist für .NET Standard-Projekte erforderlich, die das Format im SDK-Stil (SDK-Attribut) verwenden.</span><span class="sxs-lookup"><span data-stu-id="fd623-113">The dotnet CLI is required for .NET Standard projects that use the SDK-style format (SDK attribute).</span></span>

   * <span data-ttu-id="fd623-114">Installieren Sie die `nuget.exe`-CLI, indem Sie sie von [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe) herunterladen, die `.exe`-Datei in einem geeigneten Ordner speichern und den Ordner der Umgebungsvariable PATH hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="fd623-114">For the `nuget.exe` CLI, download it from [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), saving the `.exe` file to a suitable folder, and adding that folder to your PATH environment variable.</span></span> <span data-ttu-id="fd623-115">Die nuget.exe-CLI wird für .NET Standard-Bibliotheken im Nicht-SDK-Format verwendet.</span><span class="sxs-lookup"><span data-stu-id="fd623-115">The nuget.exe CLI is used for .NET Standard libraries in the non-SDK-style format.</span></span>

1. <span data-ttu-id="fd623-116">[Registrieren Sie sich für ein kostenloses Konto auf nuget.org](https://docs.microsoft.com/en-us/nuget/nuget-org/individual-accounts#add-a-new-individual-account), falls Sie noch kein Konto haben.</span><span class="sxs-lookup"><span data-stu-id="fd623-116">[Register for a free account on nuget.org](https://docs.microsoft.com/en-us/nuget/nuget-org/individual-accounts#add-a-new-individual-account) if you don't have one already.</span></span> <span data-ttu-id="fd623-117">Wenn Sie ein neues Konto erstellen, wird Ihnen eine Bestätigungs-E-Mail gesendet.</span><span class="sxs-lookup"><span data-stu-id="fd623-117">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="fd623-118">Sie müssen das Konto bestätigen, bevor Sie ein Paket hochladen können.</span><span class="sxs-lookup"><span data-stu-id="fd623-118">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="fd623-119">Erstellen eines Klassenbibliotheksprojekts</span><span class="sxs-lookup"><span data-stu-id="fd623-119">Create a class library project</span></span>

<span data-ttu-id="fd623-120">Sie können ein vorhandenes Projekt in der .NET Standard-Klassenbibliothek für Code verwenden, den Sie packen wollen, oder wie folgt ein einfaches Projekt erstellen:</span><span class="sxs-lookup"><span data-stu-id="fd623-120">You can use an existing .NET Standard Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="fd623-121">Wählen Sie in Visual Studio **Datei > Neu > Projekt** aus, erweitern Sie den Knoten **Visual C#-> .NET Standard**, wählen Sie die Vorlage „Klassenbibliothek (.NET Standard)“ aus, geben Sie dem Projekt den Namen „AppLogger“, und klicken Sie auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="fd623-121">In Visual Studio, choose **File > New > Project**, expand the **Visual C# > .NET Standard** node, select the "Class Library (.NET Standard)" template, name the project AppLogger, and click **OK**.</span></span>

1. <span data-ttu-id="fd623-122">Klicken Sie mit der rechten Maustaste auf die resultierende Projektdatei, und wählen Sie **Erstellen** aus, um sicherzustellen, dass das Projekt ordnungsgemäß erstellt wurde.</span><span class="sxs-lookup"><span data-stu-id="fd623-122">Right-click on the resulting project file and select **Build** to make sure the project was created properly.</span></span> <span data-ttu-id="fd623-123">Die DLL befindet sich im Ordner „Debuggen“ (oder im Ordner „Release“, wenn Sie stattdessen diese Konfiguration erstellen).</span><span class="sxs-lookup"><span data-stu-id="fd623-123">The DLL is found within the Debug folder (or Release if you build that configuration instead).</span></span>

<span data-ttu-id="fd623-124">In einem echten NuGet-Paket implementieren Sie viele hilfreiche Features, mit denen andere Apps erstellen können.</span><span class="sxs-lookup"><span data-stu-id="fd623-124">Within a real NuGet package, of course, you implement many useful features with which others can build applications.</span></span> <span data-ttu-id="fd623-125">In dieser exemplarischen Vorgehensweise schreiben Sie jedoch keinen zusätzlichen Code, da eine Klassenbibliothek aus der Vorlage für die Erstellung eines Pakets ausreicht.</span><span class="sxs-lookup"><span data-stu-id="fd623-125">For this walkthrough, however, you won't write any additional code because a class library from the template is sufficient to create a package.</span></span> <span data-ttu-id="fd623-126">Wenn Sie noch immer Funktionscode für das Paket benötigen, verwenden Sie folgenden:</span><span class="sxs-lookup"><span data-stu-id="fd623-126">Still, if you'd like some functional code for the package, use the following:</span></span>

```cs
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
> <span data-ttu-id="fd623-127">Sofern es keinen Grund dafür gibt, der dagegen spricht, ist .NET Standard das bevorzugte Ziel für NuGet-Pakete, da es die größte Kompatibilitätsreichweite für verarbeitende Projekte bietet.</span><span class="sxs-lookup"><span data-stu-id="fd623-127">Unless you have a reason to choose otherwise, .NET Standard is the preferred target for NuGet packages, as it provides compatibility with the widest range of consuming projects.</span></span>

## <a name="configure-package-properties"></a><span data-ttu-id="fd623-128">Konfigurieren von Paketeigenschaften</span><span class="sxs-lookup"><span data-stu-id="fd623-128">Configure package properties</span></span>

1. <span data-ttu-id="fd623-129">Wählen Sie den Menübefehl **Projekt > Eigenschaften** und dann die Registerkarte **Paket** aus. (Die Registerkarte **Paket** wird nur in Projekten für die .NET Standard-Klassenbibliothek angezeigt. Wenn Sie ein Projekt für .NET Framework konzipieren, erhalten Sie Informationen unter [Create and publish a .NET Framework package (Erstellen und Veröffentlichen eines .NET Framework-Pakets)](create-and-publish-a-package-using-visual-studio-net-framework.md).</span><span class="sxs-lookup"><span data-stu-id="fd623-129">Select the **Project > Properties** menu command, then select the **Package** tab. (The **Package** tab appears only for .NET Standard class library projects; if you are targeting .NET Framework, see [Create and publish a .NET Framework package](create-and-publish-a-package-using-visual-studio-net-framework.md) instead.</span></span> <span data-ttu-id="fd623-130">Wenn sie nicht für ein .NET Standard-Projekt angezeigt wird, müssen Sie Visual Studio 2017 möglicherweise auf die neueste Version aktualisieren.)</span><span class="sxs-lookup"><span data-stu-id="fd623-130">If it doesn't appear for a .NET Standard project, you may need to update Visual Studio 2017 to the latest release.)</span></span>

    ![NuGet-Paketeigenschaften in einem Visual Studio-Projekt](media/qs_create-vs-01-package-properties.png)

    > [!Note]
    > <span data-ttu-id="fd623-132">Bei Paketen für die öffentliche Nutzung sollten Sie besonders auf die **Tags**-Eigenschaft achten, da Tags anderen dabei helfen, Ihr Paket zu finden und dessen Funktion zu verstehen.</span><span class="sxs-lookup"><span data-stu-id="fd623-132">For packages built for public consumption, pay special attention to the **Tags** property, as tags help others find your package and understand what it does.</span></span>

1. <span data-ttu-id="fd623-133">Geben Sie Ihrem Paket einen eindeutigen Bezeichner, und füllen Sie alle weiteren gewünschten Eigenschaften aus.</span><span class="sxs-lookup"><span data-stu-id="fd623-133">Give your package a unique identifier and fill out any other desired properties.</span></span> <span data-ttu-id="fd623-134">Eine Beschreibung der verschiedenen Eigenschaften finden Sie unter [.nuspec file reference (Referenz für NUSPEC-Dateien)](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="fd623-134">For a description of the different properties, see [.nuspec file reference](../reference/nuspec.md).</span></span> <span data-ttu-id="fd623-135">Alle diese Eigenschaften werden in das `.nuspec`-Manifest eingefügt, dass von Visual Studio für das Projekt erstellt wird.</span><span class="sxs-lookup"><span data-stu-id="fd623-135">All of the properties here go into the `.nuspec` manifest that Visual Studio creates for the project.</span></span>

    > [!Important]
    > <span data-ttu-id="fd623-136">Sie müssen dem Paket einen Bezeichner zuweisen, der auf nuget.org bzw. auf dem Host, den Sie verwenden, einzigartig ist.</span><span class="sxs-lookup"><span data-stu-id="fd623-136">You must give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="fd623-137">Für diese exemplarische Vorgehensweise wird empfohlen, im Namen „Sample“ oder „Test“ zu verwenden, da der Name in einem späteren Veröffentlichungsschritt öffentlich sichtbar gemacht wird (auch wenn es unwahrscheinlich ist, dass jemand versucht, es zu verwenden).</span><span class="sxs-lookup"><span data-stu-id="fd623-137">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>
    >
    > <span data-ttu-id="fd623-138">Bei dem Versuch, ein Paket mit einem Namen zu veröffentlichen, der bereits vorhanden ist, wird Ihnen ein Fehler angezeigt.</span><span class="sxs-lookup"><span data-stu-id="fd623-138">If you attempt to publish a package with a name that already exists, you see an error.</span></span>

1. <span data-ttu-id="fd623-139">Optional: Damit Sie die Eigenschaften direkt in der Projektdatei anzeigen können, führen Sie einen Rechtsklick im Projekt im Projektmappen-Explorer aus, und wählen Sie **Edit AppLogger.csproj** (AppLogger.csproj bearbeiten) aus.</span><span class="sxs-lookup"><span data-stu-id="fd623-139">Optional: to see the properties directly in the project file, right-click the project in Solution Explorer and select **Edit AppLogger.csproj**.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="fd623-140">Ausführen des Befehls pack</span><span class="sxs-lookup"><span data-stu-id="fd623-140">Run the pack command</span></span>

1. <span data-ttu-id="fd623-141">Legen Sie die Konfiguration auf **Release** (Freigeben) fest.</span><span class="sxs-lookup"><span data-stu-id="fd623-141">Set the configuration to **Release**.</span></span>

1. <span data-ttu-id="fd623-142">Klicken Sie im **Projektmappen-Explorer** mit der rechten Maustaste auf das Projekt, und wählen Sie den Befehl **Packen** aus:</span><span class="sxs-lookup"><span data-stu-id="fd623-142">Right click the project in **Solution Explorer** and select the **Pack** command:</span></span>

    ![Der NuGet-Befehl „pack“ im Kontextmenü des Visual Studio-Projekts](media/qs_create-vs-02-pack-command.png)

1. <span data-ttu-id="fd623-144">Visual Studio erstellt das Projekt und die `.nupkg`-Datei.</span><span class="sxs-lookup"><span data-stu-id="fd623-144">Visual Studio builds the project and creates the `.nupkg` file.</span></span> <span data-ttu-id="fd623-145">Überprüfen Sie das **Ausgabefenster** auf Angaben (ähnlich wie im folgenden Beispiel), die den Pfad zur Paketdatei enthalten.</span><span class="sxs-lookup"><span data-stu-id="fd623-145">Examine the **Output** window for details (similar to the following), which contains the path to the package file.</span></span> <span data-ttu-id="fd623-146">Beachten Sie außerdem, dass sich die erstellte Assembly in `bin\Release\netstandard2.0` befindet, wie es dem Ziel .NET Standard 2.0 entspricht.</span><span class="sxs-lookup"><span data-stu-id="fd623-146">Note also that the built assembly is in `bin\Release\netstandard2.0` as befits the .NET Standard 2.0 target.</span></span>

    ```output
    1>------ Build started: Project: AppLogger, Configuration: Release Any CPU ------
    1>AppLogger -> d:\proj\AppLogger\AppLogger\bin\Release\netstandard2.0\AppLogger.dll
    1>Successfully created package 'd:\proj\AppLogger\AppLogger\bin\Release\AppLogger.1.0.0.nupkg'.
    ========== Build: 1 succeeded, 0 failed, 0 up-to-date, 0 skipped ==========
    ```

### <a name="alternate-option-pack-with-msbuild"></a><span data-ttu-id="fd623-147">Alternative Option: „pack“ mit MSBuild</span><span class="sxs-lookup"><span data-stu-id="fd623-147">Alternate option: pack with MSBuild</span></span>

<span data-ttu-id="fd623-148">Als Alternative zur Verwendung des Menübefehls **Packen** unterstützen NuGet 4.x und höher und MSBuild 15.1 und höher ein `pack`-Ziel, wenn das Projekt die nötigen Paketdaten enthält.</span><span class="sxs-lookup"><span data-stu-id="fd623-148">As an alternate to using the **Pack** menu command, NuGet 4.x+ and MSBuild 15.1+ supports a `pack` target when the project contains the necessary package data.</span></span> <span data-ttu-id="fd623-149">Öffnen Sie eine Eingabeaufforderung, navigieren Sie zum Projektordner, und führen Sie den folgenden Befehl aus.</span><span class="sxs-lookup"><span data-stu-id="fd623-149">Open a command prompt, navigate to your project folder and run the following command.</span></span> <span data-ttu-id="fd623-150">(In der Regel sollten Sie die „Developer-Eingabeaufforderung für Visual Studio“ über das Startmenü starten, da dieses mit allen nötigen Pfaden für MSBuild konfiguriert ist.)</span><span class="sxs-lookup"><span data-stu-id="fd623-150">(You typically want to start the "Developer Command Prompt for Visual Studio" from the Start menu, as it will be configured with all the necessary paths for MSBuild.)</span></span>

```cli
msbuild -t:pack -p:Configuration=Release
```

<span data-ttu-id="fd623-151">Sie finden das Paket im Ordner `bin\Release`.</span><span class="sxs-lookup"><span data-stu-id="fd623-151">The package can then be found in the `bin\Release` folder.</span></span>

<span data-ttu-id="fd623-152">Zusätzliche Optionen zu `msbuild -t:pack` finden Sie unter [NuGet pack and restore as MSBuild targets (NuGet-Befehle „pack“ und „restore“ MSBuild-Ziele)](../reference/msbuild-targets.md#pack-target).</span><span class="sxs-lookup"><span data-stu-id="fd623-152">For additional options with `msbuild -t:pack`, see [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md#pack-target).</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="fd623-153">Veröffentlichen des Pakets</span><span class="sxs-lookup"><span data-stu-id="fd623-153">Publish the package</span></span>

<span data-ttu-id="fd623-154">Sobald Sie eine `.nupkg`-Datei haben, können Sie diese gemeinsam mit einem API-Schlüssel von nuget.org über die `nuget.exe`-CLI oder die `dotnet.exe`-CLI auf nuget.org veröffentlichen.</span><span class="sxs-lookup"><span data-stu-id="fd623-154">Once you have a `.nupkg` file, you publish it to nuget.org using either the `nuget.exe` CLI or the `dotnet.exe` CLI along with an API key acquired from nuget.org.</span></span>

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="fd623-155">Erwerben des API-Schlüssels</span><span class="sxs-lookup"><span data-stu-id="fd623-155">Acquire your API key</span></span>

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-dotnet-nuget-push-dotnet-cli"></a><span data-ttu-id="fd623-156">Veröffentlichen mit „dotnet nuget push“ (dotnet-CLI)</span><span class="sxs-lookup"><span data-stu-id="fd623-156">Publish with dotnet nuget push (dotnet CLI)</span></span>

<span data-ttu-id="fd623-157">Dieser Schritt ist eine Alternative zur Verwendung von `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="fd623-157">This step is an alternative to using `nuget.exe`.</span></span>

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-with-nuget-push-nugetexe-cli"></a><span data-ttu-id="fd623-158">Veröffentlichen mit „nuget push“ (nuget.exe-CLI)</span><span class="sxs-lookup"><span data-stu-id="fd623-158">Publish with nuget push (nuget.exe CLI)</span></span>

<span data-ttu-id="fd623-159">Dieser Schritt ist eine Alternative zur Verwendung von `dotnet.exe`.</span><span class="sxs-lookup"><span data-stu-id="fd623-159">This step is an alternative to using `dotnet.exe`.</span></span>

1. <span data-ttu-id="fd623-160">Navigieren Sie zum Ordner, der die `.nupkg`-Datei enthält.</span><span class="sxs-lookup"><span data-stu-id="fd623-160">Change to the folder containing the `.nupkg` file.</span></span>

1. <span data-ttu-id="fd623-161">Führen Sie den folgenden Befehl aus, geben Sie dabei Ihren Paketnamen an, und ersetzen Sie den Schlüsselwert durch Ihren API-Schlüssel:</span><span class="sxs-lookup"><span data-stu-id="fd623-161">Run the following command, specifying your package name and replacing the key value with your API key:</span></span>

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="fd623-162">In „NuGet.exe“ werden die Ergebnisse des Veröffentlichungsvorgangs angezeigt:</span><span class="sxs-lookup"><span data-stu-id="fd623-162">nuget.exe displays the results of the publishing process:</span></span>

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

<span data-ttu-id="fd623-163">Siehe [nuget push-Befehl](../tools/cli-ref-push.md).</span><span class="sxs-lookup"><span data-stu-id="fd623-163">See [nuget push](../tools/cli-ref-push.md).</span></span>

### <a name="publish-errors"></a><span data-ttu-id="fd623-164">Veröffentlichungsfehler</span><span class="sxs-lookup"><span data-stu-id="fd623-164">Publish errors</span></span>

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="fd623-165">Verwalten des veröffentlichten Pakets</span><span class="sxs-lookup"><span data-stu-id="fd623-165">Manage the published package</span></span>

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="adding-a-readme-and-other-files"></a><span data-ttu-id="fd623-166">Hinzufügen einer Infodatei und anderer Dateien</span><span class="sxs-lookup"><span data-stu-id="fd623-166">Adding a readme and other files</span></span>

<span data-ttu-id="fd623-167">Bearbeiten Sie die Projektdatei, und verwenden Sie die `content`-Eigenschaft, um Dateien, die im Paket eingeschlossen werden sollen, direkt anzugeben:</span><span class="sxs-lookup"><span data-stu-id="fd623-167">To directly specify files to include in the package, edit the project file and use the `content` property:</span></span>

```xml
<ItemGroup>
  <Content Include="readme.txt">
    <Pack>true</Pack>
    <PackagePath>\</PackagePath>
  </Content>
</ItemGroup>
```

<span data-ttu-id="fd623-168">Dies schließt eine Datei namens `readme.txt` im Stammverzeichnis ein.</span><span class="sxs-lookup"><span data-stu-id="fd623-168">This will include a file named `readme.txt` in the package root.</span></span> <span data-ttu-id="fd623-169">Visual Studio zeigt unmittelbar nach der direkten Installation des Pakets den Inhalt der Datei als Nur-Text an.</span><span class="sxs-lookup"><span data-stu-id="fd623-169">Visual Studio displays the contents of that file as plain text immediately after installing the package directly.</span></span> <span data-ttu-id="fd623-170">Für Pakete, die als Abhängigkeiten installiert wurden, werden keine Infodateien angezeigt.</span><span class="sxs-lookup"><span data-stu-id="fd623-170">(Readme files are not displayed for packages installed as dependencies).</span></span> <span data-ttu-id="fd623-171">Die Infodatei für das Paket „HtmlAgilityPack“ wird z.B. folgendermaßen angezeigt:</span><span class="sxs-lookup"><span data-stu-id="fd623-171">For example, here's how the readme for the HtmlAgilityPack package appears:</span></span>

![Anzeige einer Infodatei für ein NuGet-Paket nach der Installation](../create-packages/media/Create_01-ShowReadme.png)

> [!Note]
> <span data-ttu-id="fd623-173">Wenn Sie die Datei „readme.txt“ lediglich im Stammverzeichnis hinzufügen, wird diese nicht im resultierenden Paket eingeschlossen.</span><span class="sxs-lookup"><span data-stu-id="fd623-173">Merely adding the readme.txt at the project root will not result in it being included in the resulting package.</span></span>

## <a name="related-topics"></a><span data-ttu-id="fd623-174">Verwandte Themen</span><span class="sxs-lookup"><span data-stu-id="fd623-174">Related topics</span></span>

- [<span data-ttu-id="fd623-175">Erstellen eines Pakets</span><span class="sxs-lookup"><span data-stu-id="fd623-175">Create a Package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="fd623-176">Veröffentlichen eines Pakets</span><span class="sxs-lookup"><span data-stu-id="fd623-176">Publish a Package</span></span>](../nuget-org/publish-a-package.md)
- [<span data-ttu-id="fd623-177">Vorabversionen von Paketen</span><span class="sxs-lookup"><span data-stu-id="fd623-177">Pre-release Packages</span></span>](../create-packages/Prerelease-Packages.md)
- [<span data-ttu-id="fd623-178">Unterstützung mehrerer Zielframeworks</span><span class="sxs-lookup"><span data-stu-id="fd623-178">Support multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="fd623-179">Paketversionsverwaltung</span><span class="sxs-lookup"><span data-stu-id="fd623-179">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="fd623-180">Erstellen von lokalisierten Paketen</span><span class="sxs-lookup"><span data-stu-id="fd623-180">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="fd623-181">Dokumentation zur .NET Standard-Bibliothek</span><span class="sxs-lookup"><span data-stu-id="fd623-181">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="fd623-182">Portieren von .NET Framework auf .NET Core</span><span class="sxs-lookup"><span data-stu-id="fd623-182">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)
