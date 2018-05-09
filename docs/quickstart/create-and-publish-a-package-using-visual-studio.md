---
title: Einführender Leitfaden zum Erstellen und Veröffentlichen eines .NET Standard-NuGet-Pakets mithilfe von Visual Studio
description: Exemplarische Vorgehensweise zum Erstellen und Veröffentlichen eines .NET Standard NuGet-Pakets mit Visual Studio 2017.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 03/18/2018
ms.topic: quickstart
ms.openlocfilehash: c5d58aa6312eae801607ca44a81bc092a7a7c15f
ms.sourcegitcommit: a6ca160b1e7e5c58b135af4eba0e9463127a59e8
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/28/2018
---
# <a name="quickstart-create-and-publish-a-nuget-package-using-visual-studio-net-standard"></a><span data-ttu-id="2e812-103">Schnellstart: Erstellen und Veröffentlichen eines NuGet-Pakets mithilfe von Visual Studio (.NET Standard)</span><span class="sxs-lookup"><span data-stu-id="2e812-103">Quickstart: Create and publish a NuGet package using Visual Studio (.NET Standard)</span></span>

<span data-ttu-id="2e812-104">Ein NuGet-Paket kann problemlos über eine .NET Standard-Klassenbibliothek in Visual Studio erstellt und dann, durch Verwendung eines CLI-Tools, auf nuget.org veröffentlicht werden.</span><span class="sxs-lookup"><span data-stu-id="2e812-104">It's a simple process to create a NuGet package from a .NET Standard Class Library in Visual Studio, and then publish it to nuget.org using a CLI tool.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="2e812-105">Erforderliche Komponenten</span><span class="sxs-lookup"><span data-stu-id="2e812-105">Prerequisites</span></span>

1. <span data-ttu-id="2e812-106">Installieren Sie über [visualstudio.com](https://www.visualstudio.com/) eine beliebige Edition von Visual Studio 2017 mit einer beliebigen .NET-bezogenen Workload.</span><span class="sxs-lookup"><span data-stu-id="2e812-106">Install any edition of Visual Studio 2017 from [visualstudio.com](https://www.visualstudio.com/) with any .NET-related workload.</span></span> <span data-ttu-id="2e812-107">Visual Studio 2017 enthält automatisch NuGet-Funktionen, wenn eine .NET-Workload installiert ist.</span><span class="sxs-lookup"><span data-stu-id="2e812-107">Visual Studio 2017 automatically includes NuGet capabilities when a .NET workload is installed.</span></span>

1. <span data-ttu-id="2e812-108">Installieren Sie die `nuget.exe`-CLI, indem Sie sie von [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe) herunterladen, die `.exe`-Datei in einen geeigneten Ordner speichern und den Ordner der Umgebungsvariable PATH hinzufügen.</span><span class="sxs-lookup"><span data-stu-id="2e812-108">Install the `nuget.exe` CLI by downloading it from [nuget.org](https://dist.nuget.org/win-x86-commandline/latest/nuget.exe), saving that `.exe` file to a suitable folder, and adding that folder to your PATH environment variable.</span></span>

    <span data-ttu-id="2e812-109">Alternativ können Sie die `dotnet`-CLI verwenden, wenn Sie das [.NET Core SDK](https://www.microsoft.com/net/download/) installiert haben.</span><span class="sxs-lookup"><span data-stu-id="2e812-109">Alternately, if you have the [.NET Core SDK](https://www.microsoft.com/net/download/) installed, you can use the `dotnet` CLI.</span></span>

1. <span data-ttu-id="2e812-110">[Registrieren Sie sich für ein kostenloses Konto auf nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F), falls Sie noch kein Konto haben.</span><span class="sxs-lookup"><span data-stu-id="2e812-110">[Register for a free account on nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) if you don't have one already.</span></span> <span data-ttu-id="2e812-111">Wenn Sie ein neues Konto erstellen, wird Ihnen eine Bestätigungs-E-Mail gesendet.</span><span class="sxs-lookup"><span data-stu-id="2e812-111">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="2e812-112">Sie müssen das Konto bestätigen, bevor Sie ein Paket hochladen können.</span><span class="sxs-lookup"><span data-stu-id="2e812-112">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="2e812-113">Erstellen eines Klassenbibliotheksprojekts</span><span class="sxs-lookup"><span data-stu-id="2e812-113">Create a class library project</span></span>

<span data-ttu-id="2e812-114">Sie können ein vorhandenes Projekt in der .NET Standard-Klassenbibliothek für Code verwenden, den Sie packen wollen, oder wie folgt ein einfaches Projekt erstellen:</span><span class="sxs-lookup"><span data-stu-id="2e812-114">You can use an existing .NET Standard Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="2e812-115">Wählen Sie in Visual Studio **Datei > Neu > Projekt** aus, erweitern Sie den Knoten **Visual C#-> .NET Standard**, wählen Sie die Vorlage „Klassenbibliothek (.NET Standard)“ aus, geben Sie dem Projekt den Namen „AppLogger“, und klicken Sie auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="2e812-115">In Visual Studio, choose **File > New > Project**, expand the **Visual C# > .NET Standard** node, select the "Class Library (.NET Standard)" template, name the project AppLogger, and click **OK**.</span></span>

1. <span data-ttu-id="2e812-116">Klicken Sie mit der rechten Maustaste auf die resultierende Projektdatei, und wählen Sie **Erstellen** aus, um sicherzustellen, dass das Projekt ordnungsgemäß erstellt wurde.</span><span class="sxs-lookup"><span data-stu-id="2e812-116">Right-click on the resulting project file and select **Build** to make sure the project was created properly.</span></span> <span data-ttu-id="2e812-117">Die DLL befindet sich im Ordner „Debuggen“ (oder im Ordner „Release“, wenn Sie stattdessen diese Konfiguration erstellen).</span><span class="sxs-lookup"><span data-stu-id="2e812-117">The DLL is found within the Debug folder (or Release if you build that configuration instead).</span></span>

<span data-ttu-id="2e812-118">In einem echten NuGet-Paket implementieren Sie viele hilfreiche Features, mit denen andere Apps erstellen können.</span><span class="sxs-lookup"><span data-stu-id="2e812-118">Within a real NuGet package, of course, you implement many useful features with which others can build applications.</span></span> <span data-ttu-id="2e812-119">In dieser exemplarischen Vorgehensweise schreiben Sie jedoch keinen zusätzlichen Code, da eine Klassenbibliothek aus der Vorlage für die Erstellung eines Pakets ausreicht.</span><span class="sxs-lookup"><span data-stu-id="2e812-119">For this walkthrough, however, you won't write any additional code because a class library from the template is sufficient to create a package.</span></span> <span data-ttu-id="2e812-120">Wenn Sie noch immer Funktionscode für das Paket benötigen, verwenden Sie folgenden:</span><span class="sxs-lookup"><span data-stu-id="2e812-120">Still, if you'd like some functional code for the package, use the following:</span></span>

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
> <span data-ttu-id="2e812-121">Sofern es keinen Grund dafür gibt, der dagegen spricht, ist .NET Standard das bevorzugte Ziel für NuGet-Pakete, da es die größte Kompatibilitätsreichweite für verarbeitende Projekte bietet.</span><span class="sxs-lookup"><span data-stu-id="2e812-121">Unless you have a reason to choose otherwise, .NET Standard is the preferred target for NuGet packages, as it provides compatibility with the widest range of consuming projects.</span></span>

## <a name="configure-package-properties"></a><span data-ttu-id="2e812-122">Konfigurieren von Paketeigenschaften</span><span class="sxs-lookup"><span data-stu-id="2e812-122">Configure package properties</span></span>

1. <span data-ttu-id="2e812-123">Wählen Sie den Menübefehl **Projekt > Eigenschaften** und dann die Registerkarte **Paket** aus. (Die Registerkarte **Paket** wird nur in Projekten für die .NET Standard-Klassenbibliothek angezeigt. Wenn Sie ein Projekt für .NET Framework konzipieren, erhalten Sie Informationen unter [Create and publish a .NET Framework package (Erstellen und Veröffentlichen eines .NET Framework-Pakets)](create-and-publish-a-package-using-visual-studio-net-framework.md).</span><span class="sxs-lookup"><span data-stu-id="2e812-123">Select the **Project > Properties** menu command, then select the **Package** tab. (The **Package** tab appears only for .NET Standard class library projects; if you are targeting .NET Framework, see [Create and publish a .NET Framework package](create-and-publish-a-package-using-visual-studio-net-framework.md) instead.</span></span> <span data-ttu-id="2e812-124">Wenn sie nicht für ein .NET Standard-Projekt angezeigt wird, müssen Sie Visual Studio 2017 möglicherweise auf die neueste Version aktualisieren.)</span><span class="sxs-lookup"><span data-stu-id="2e812-124">If it doesn't appear for a .NET Standard project, you may need to update Visual Studio 2017 to the latest release.)</span></span>

    ![NuGet-Paketeigenschaften in einem Visual Studio-Projekt](media/qs_create-vs-01-package-properties.png)

    > [!Note]
    > <span data-ttu-id="2e812-126">Bei Paketen für die öffentliche Nutzung sollten Sie besonders auf die **Tags**-Eigenschaft achten, da Tags anderen dabei helfen, Ihr Paket zu finden und dessen Funktion zu verstehen.</span><span class="sxs-lookup"><span data-stu-id="2e812-126">For packages built for public consumption, pay special attention to the **Tags** property, as tags help others find your package and understand what it does.</span></span>

1. <span data-ttu-id="2e812-127">Geben Sie Ihrem Paket einen eindeutigen Bezeichner, und füllen Sie alle weiteren gewünschten Eigenschaften aus.</span><span class="sxs-lookup"><span data-stu-id="2e812-127">Give your package a unique identifier and fill out any other desired properties.</span></span> <span data-ttu-id="2e812-128">Eine Beschreibung der verschiedenen Eigenschaften finden Sie unter [.nuspec file reference (Referenz für NUSPEC-Dateien)](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="2e812-128">For a description of the different properties, see [.nuspec file reference](../reference/nuspec.md).</span></span> <span data-ttu-id="2e812-129">Alle diese Eigenschaften werden in das `.nuspec`-Manifest eingefügt, dass von Visual Studio für das Projekt erstellt wird.</span><span class="sxs-lookup"><span data-stu-id="2e812-129">All of the properties here go into the `.nuspec` manifest that Visual Studio creates for the project.</span></span>

    > [!Important]
    > <span data-ttu-id="2e812-130">Sie müssen dem Paket einen Bezeichner zuweisen, der auf nuget.org bzw. auf dem Host, den Sie verwenden, einzigartig ist.</span><span class="sxs-lookup"><span data-stu-id="2e812-130">You must give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="2e812-131">Für diese exemplarische Vorgehensweise wird empfohlen, im Namen „Sample“ oder „Test“ zu verwenden, da der Name in einem späteren Veröffentlichungsschritt öffentlich sichtbar gemacht wird (auch wenn es unwahrscheinlich ist, dass jemand versucht, es zu verwenden).</span><span class="sxs-lookup"><span data-stu-id="2e812-131">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>
    >
    > <span data-ttu-id="2e812-132">Bei dem Versuch, ein Paket mit einem Namen zu veröffentlichen, der bereits vorhanden ist, wird Ihnen ein Fehler angezeigt.</span><span class="sxs-lookup"><span data-stu-id="2e812-132">If you attempt to publish a package with a name that already exists, you see an error.</span></span>

1. <span data-ttu-id="2e812-133">Optional: Damit Sie die Eigenschaften direkt in der Projektdatei anzeigen können, führen Sie einen Rechtsklick im Projekt im Projektmappen-Explorer aus, und wählen Sie **Edit AppLogger.csproj** (AppLogger.csproj bearbeiten) aus.</span><span class="sxs-lookup"><span data-stu-id="2e812-133">Optional: to see the properties directly in the project file, right-click the project in Solution Explorer and select **Edit AppLogger.csproj**.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="2e812-134">Ausführen des Befehls pack</span><span class="sxs-lookup"><span data-stu-id="2e812-134">Run the pack command</span></span>

1. <span data-ttu-id="2e812-135">Legen Sie die Konfiguration auf **Release** (Freigeben) fest.</span><span class="sxs-lookup"><span data-stu-id="2e812-135">Set the configuration to **Release**.</span></span>

1. <span data-ttu-id="2e812-136">Klicken Sie im **Projektmappen-Explorer** mit der rechten Maustaste auf das Projekt, und wählen Sie den Befehl **Packen** aus:</span><span class="sxs-lookup"><span data-stu-id="2e812-136">Right click the project in **Solution Explorer** and select the **Pack** command:</span></span>

    ![Der NuGet-Befehl „pack“ im Kontextmenü des Visual Studio-Projekts](media/qs_create-vs-02-pack-command.png)

1. <span data-ttu-id="2e812-138">Visual Studio erstellt das Projekt und die `.nupkg`-Datei.</span><span class="sxs-lookup"><span data-stu-id="2e812-138">Visual Studio builds the project and creates the `.nupkg` file.</span></span> <span data-ttu-id="2e812-139">Überprüfen Sie das **Ausgabefenster** auf Angaben (ähnlich wie im folgenden Beispiel), die den Pfad zur Paketdatei enthalten.</span><span class="sxs-lookup"><span data-stu-id="2e812-139">Examine the **Output** window for details (similar to the following), which contains the path to the package file.</span></span> <span data-ttu-id="2e812-140">Beachten Sie außerdem, dass sich die erstellte Assembly in `bin\Release\netstandard2.0` befindet, wie es dem Ziel .NET Standard 2.0 entspricht.</span><span class="sxs-lookup"><span data-stu-id="2e812-140">Note also that the built assembly is in `bin\Release\netstandard2.0` as befits the .NET Standard 2.0 target.</span></span>

    ```output
    1>------ Build started: Project: AppLogger, Configuration: Release Any CPU ------
    1>AppLogger -> d:\proj\AppLogger\AppLogger\bin\Release\netstandard2.0\AppLogger.dll
    1>Successfully created package 'd:\proj\AppLogger\AppLogger\bin\Release\AppLogger.1.0.0.nupkg'.
    ========== Build: 1 succeeded, 0 failed, 0 up-to-date, 0 skipped ==========
    ```

### <a name="alternate-option-pack-with-msbuild"></a><span data-ttu-id="2e812-141">Alternative Option: „pack“ mit MSBuild</span><span class="sxs-lookup"><span data-stu-id="2e812-141">Alternate option: pack with MSBuild</span></span>

<span data-ttu-id="2e812-142">Als Alternative zur Verwendung des Menübefehls **Packen** unterstützen NuGet 4.x und höher und MSBuild 15.1 und höher ein `pack`-Ziel, wenn das Projekt die nötigen Paketdaten enthält.</span><span class="sxs-lookup"><span data-stu-id="2e812-142">As an alternate to using the **Pack** menu command, NuGet 4.x+ and MSBuild 15.1+ supports a `pack` target when the project contains the necessary package data.</span></span> <span data-ttu-id="2e812-143">Öffnen Sie eine Eingabeaufforderung, navigieren Sie zum Projektordner, und führen Sie den folgenden Befehl aus.</span><span class="sxs-lookup"><span data-stu-id="2e812-143">Open a command prompt, navigate to your project folder and run the following command.</span></span> <span data-ttu-id="2e812-144">(In der Regel sollten Sie die „Developer-Eingabeaufforderung für Visual Studio“ über das Startmenü starten, da dieses mit allen nötigen Pfaden für MSBuild konfiguriert ist.)</span><span class="sxs-lookup"><span data-stu-id="2e812-144">(You typically want to start the "Developer Command Prompt for Visual Studio" from the Start menu, as it will be configured with all the necessary paths for MSBuild.)</span></span>

```cli
msbuild /t:pack /p:Configuration=Release
```

<span data-ttu-id="2e812-145">Sie finden das Paket im Ordner `bin\Release`.</span><span class="sxs-lookup"><span data-stu-id="2e812-145">The package can then be found in the `bin\Release` folder.</span></span>

<span data-ttu-id="2e812-146">Zusätzliche Optionen zu `msbuild /t:pack` finden Sie unter [NuGet pack and restore as MSBuild targets (NuGet-Befehle „pack“ und „restore“ MSBuild-Ziele)](../reference/msbuild-targets.md#pack-target).</span><span class="sxs-lookup"><span data-stu-id="2e812-146">For additional options with `msbuild /t:pack`, see [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md#pack-target).</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="2e812-147">Veröffentlichen des Pakets</span><span class="sxs-lookup"><span data-stu-id="2e812-147">Publish the package</span></span>

<span data-ttu-id="2e812-148">Sobald Sie eine `.nupkg`-Datei haben, können Sie diese gemeinsam mit einem API-Schlüssel von nuget.org über die `nuget.exe`-CLI oder die `dotnet.exe`-CLI auf nuget.org veröffentlichen.</span><span class="sxs-lookup"><span data-stu-id="2e812-148">Once you have a `.nupkg` file, you publish it to nuget.org using either the `nuget.exe` CLI or the `dotnet.exe` CLI along with an API key acquired from nuget.org.</span></span>

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="2e812-149">Erwerben des API-Schlüssels</span><span class="sxs-lookup"><span data-stu-id="2e812-149">Acquire your API key</span></span>

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-nuget-push"></a><span data-ttu-id="2e812-150">Veröffentlichen mit dem Befehl „nuget push“</span><span class="sxs-lookup"><span data-stu-id="2e812-150">Publish with nuget push</span></span>

<span data-ttu-id="2e812-151">Dieser Schritt ist eine Alternative zur Verwendung von `dotnet.exe`.</span><span class="sxs-lookup"><span data-stu-id="2e812-151">This step is an alternative to using `dotnet.exe`.</span></span>

1. <span data-ttu-id="2e812-152">Navigieren Sie zum Ordner, der die `.nupkg`-Datei enthält.</span><span class="sxs-lookup"><span data-stu-id="2e812-152">Change to the folder containing the `.nupkg` file.</span></span>

1. <span data-ttu-id="2e812-153">Führen Sie den folgenden Befehl aus, geben Sie dabei Ihren Paketnamen an, und ersetzen Sie den Schlüsselwert durch Ihren API-Schlüssel:</span><span class="sxs-lookup"><span data-stu-id="2e812-153">Run the following command, specifying your package name and replacing the key value with your API key:</span></span>

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="2e812-154">In „NuGet.exe“ werden die Ergebnisse des Veröffentlichungsvorgangs angezeigt:</span><span class="sxs-lookup"><span data-stu-id="2e812-154">nuget.exe displays the results of the publishing process:</span></span>

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

<span data-ttu-id="2e812-155">Siehe [nuget push-Befehl](../tools/cli-ref-push.md).</span><span class="sxs-lookup"><span data-stu-id="2e812-155">See [nuget push](../tools/cli-ref-push.md).</span></span>

### <a name="publish-with-dotnet-nuget-push"></a><span data-ttu-id="2e812-156">Veröffentlichen mit „dotnet nuget push“</span><span class="sxs-lookup"><span data-stu-id="2e812-156">Publish with dotnet nuget push</span></span>

<span data-ttu-id="2e812-157">Dieser Schritt ist eine Alternative zur Verwendung von `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="2e812-157">This step is an alternative to using `nuget.exe`.</span></span>

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-errors"></a><span data-ttu-id="2e812-158">Veröffentlichungsfehler</span><span class="sxs-lookup"><span data-stu-id="2e812-158">Publish errors</span></span>

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="2e812-159">Verwalten des veröffentlichten Pakets</span><span class="sxs-lookup"><span data-stu-id="2e812-159">Manage the published package</span></span>

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="related-topics"></a><span data-ttu-id="2e812-160">Verwandte Themen</span><span class="sxs-lookup"><span data-stu-id="2e812-160">Related topics</span></span>

- [<span data-ttu-id="2e812-161">Erstellen eines Pakets</span><span class="sxs-lookup"><span data-stu-id="2e812-161">Create a Package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="2e812-162">Veröffentlichen eines Pakets</span><span class="sxs-lookup"><span data-stu-id="2e812-162">Publish a Package</span></span>](../create-packages/publish-a-package.md)
- [<span data-ttu-id="2e812-163">Vorabversionen von Paketen</span><span class="sxs-lookup"><span data-stu-id="2e812-163">Pre-release Packages</span></span>](../create-packages/Prerelease-Packages.md)
- [<span data-ttu-id="2e812-164">Unterstützung mehrerer Zielframeworks</span><span class="sxs-lookup"><span data-stu-id="2e812-164">Support multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="2e812-165">Paketversionsverwaltung</span><span class="sxs-lookup"><span data-stu-id="2e812-165">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="2e812-166">Erstellen von lokalisierten Paketen</span><span class="sxs-lookup"><span data-stu-id="2e812-166">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="2e812-167">Dokumentation zur .NET Standard-Bibliothek</span><span class="sxs-lookup"><span data-stu-id="2e812-167">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="2e812-168">Portieren von .NET Framework auf .NET Core</span><span class="sxs-lookup"><span data-stu-id="2e812-168">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)
