---
title: Erstellen und Veröffentlichen eines .NET Standard-NuGet-Pakets mithilfe von Visual Studio auf Windows
description: Exemplarische Vorgehensweise zum Erstellen und Veröffentlichen eines .NET Standard-NuGet-Pakets mit Visual Studio unter Windows.
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: quickstart
ms.openlocfilehash: 86e71460094de9b799384db83456a68db57647af
ms.sourcegitcommit: e65180e622f6233b51bb0b41d0e919688083eb26
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/23/2019
ms.locfileid: "68419925"
---
# <a name="quickstart-create-and-publish-a-nuget-package-using-visual-studio-net-standard-windows-only"></a><span data-ttu-id="67fea-103">Schnellstart: Erstellen und Veröffentlichen eines NuGet-Pakets mithilfe von Visual Studio (.NET Standard, nur Windows)</span><span class="sxs-lookup"><span data-stu-id="67fea-103">Quickstart: Create and publish a NuGet package using Visual Studio (.NET Standard, Windows only)</span></span>

<span data-ttu-id="67fea-104">Ein NuGet-Paket kann problemlos über eine .NET Standard-Klassenbibliothek in Visual Studio unter Windows erstellt und dann durch Verwendung eines CLI-Tools auf nuget.org veröffentlicht werden.</span><span class="sxs-lookup"><span data-stu-id="67fea-104">It's a simple process to create a NuGet package from a .NET Standard Class Library in Visual Studio on Windows, and then publish it to nuget.org using a CLI tool.</span></span>

> [!Note]
> <span data-ttu-id="67fea-105">Wenn Sie Visual Studio für Mac verwenden, lesen Sie [diese Informationen](/xamarin/cross-platform/app-fundamentals/nuget-multiplatform-libraries/existing-library) zum Erstellen eines NuGet-Pakets, oder verwenden Sie die [dotnet-CLI-Tools](create-and-publish-a-package-using-the-dotnet-cli.md).</span><span class="sxs-lookup"><span data-stu-id="67fea-105">If you are using Visual Studio for Mac, refer to [this information](/xamarin/cross-platform/app-fundamentals/nuget-multiplatform-libraries/existing-library) on creating a NuGet package, or use the [dotnet CLI tools](create-and-publish-a-package-using-the-dotnet-cli.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="67fea-106">Erforderliche Komponenten</span><span class="sxs-lookup"><span data-stu-id="67fea-106">Prerequisites</span></span>

1. <span data-ttu-id="67fea-107">Installieren Sie über [visualstudio.com](https://www.visualstudio.com/) eine beliebige Edition von Visual Studio 2017 oder höher mit einer .NET Core-bezogenen Workload.</span><span class="sxs-lookup"><span data-stu-id="67fea-107">Install any edition of Visual Studio 2017 or higher from [visualstudio.com](https://www.visualstudio.com/) with a .NET Core related workload.</span></span>

1. <span data-ttu-id="67fea-108">Sofern noch nicht installiert, installieren Sie die `dotnet`-CLI.</span><span class="sxs-lookup"><span data-stu-id="67fea-108">If it's not already installed, install the `dotnet` CLI.</span></span>

   <span data-ttu-id="67fea-109">Zur `dotnet`-CLI: Ab Visual Studio 2017 wird die `dotnet`-CLI automatisch mit jeder .NET Core-bezogenen Workload installiert.</span><span class="sxs-lookup"><span data-stu-id="67fea-109">For the `dotnet` CLI, starting in Visual Studio 2017, the `dotnet` CLI is automatically installed with any .NET Core related workloads.</span></span> <span data-ttu-id="67fea-110">Installieren Sie andernfalls das [.NET Core SDK](https://www.microsoft.com/net/download/), um die `dotnet`-CLI zu erhalten.</span><span class="sxs-lookup"><span data-stu-id="67fea-110">Otherwise, install the [.NET Core SDK](https://www.microsoft.com/net/download/) to get the `dotnet` CLI.</span></span> <span data-ttu-id="67fea-111">Die `dotnet`-CLI ist für .NET Standard-Projekte erforderlich, die das [SDK-Format](../resources/check-project-format.md) (SDK-Attribut) verwenden.</span><span class="sxs-lookup"><span data-stu-id="67fea-111">The `dotnet` CLI is required for .NET Standard projects that use the [SDK-style format](../resources/check-project-format.md) (SDK attribute).</span></span> <span data-ttu-id="67fea-112">In der Standard-Klassenbibliotheksvorlage in Visual Studio 2017 und höher, die in diesem Artikel genutzt wird, wird das SDK-Attribut verwendet.</span><span class="sxs-lookup"><span data-stu-id="67fea-112">The default class library template in Visual Studio 2017 and higher, which is used in this article, uses the SDK attribute.</span></span>
   
   > [!Important]
   > <span data-ttu-id="67fea-113">In diesem Artikel wird die `dotnet`-CLI empfohlen.</span><span class="sxs-lookup"><span data-stu-id="67fea-113">For this article, the `dotnet` CLI is recommended.</span></span> <span data-ttu-id="67fea-114">Sie können zwar mit der `nuget.exe`-CLI jedes NuGet-Paket veröffentlichen, jedoch gelten einige der Schritte in diesem Artikel speziell für Projekte im SDK-Format und die dotnet-CLI.</span><span class="sxs-lookup"><span data-stu-id="67fea-114">Although you can publish any NuGet package using the `nuget.exe` CLI, some of the steps in this article are specific to SDK-style projects and the dotnet CLI.</span></span> <span data-ttu-id="67fea-115">Die nuget.exe-CLI wird für [Projekte im Nicht-SDK-Format](../resources/check-project-format.md) (in der Regel .NET Framework) verwendet.</span><span class="sxs-lookup"><span data-stu-id="67fea-115">The nuget.exe CLI is used for [non-SDK-style projects](../resources/check-project-format.md) (typically .NET Framework).</span></span> <span data-ttu-id="67fea-116">Wenn Sie mit einem Projekt im Nicht-SDK-Format arbeiten, befolgen Sie die Anweisungen unter [Erstellen und Veröffentlichen eines .NET Framework-Pakets (Visual Studio)](create-and-publish-a-package-using-visual-studio-net-framework.md), um das Paket zu erstellen und zu veröffentlichen.</span><span class="sxs-lookup"><span data-stu-id="67fea-116">If you are working with a non-SDK-style project, follow the procedures in [Create and publish a .NET Framework package (Visual Studio)](create-and-publish-a-package-using-visual-studio-net-framework.md) to create and publish the package.</span></span>

1. <span data-ttu-id="67fea-117">[Registrieren Sie sich für ein kostenloses Konto auf nuget.org](https://docs.microsoft.com/en-us/nuget/nuget-org/individual-accounts#add-a-new-individual-account), falls Sie noch kein Konto haben.</span><span class="sxs-lookup"><span data-stu-id="67fea-117">[Register for a free account on nuget.org](https://docs.microsoft.com/en-us/nuget/nuget-org/individual-accounts#add-a-new-individual-account) if you don't have one already.</span></span> <span data-ttu-id="67fea-118">Wenn Sie ein neues Konto erstellen, wird Ihnen eine Bestätigungs-E-Mail gesendet.</span><span class="sxs-lookup"><span data-stu-id="67fea-118">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="67fea-119">Sie müssen das Konto bestätigen, bevor Sie ein Paket hochladen können.</span><span class="sxs-lookup"><span data-stu-id="67fea-119">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="67fea-120">Erstellen eines Klassenbibliotheksprojekts</span><span class="sxs-lookup"><span data-stu-id="67fea-120">Create a class library project</span></span>

<span data-ttu-id="67fea-121">Sie können ein vorhandenes Projekt in der .NET Standard-Klassenbibliothek für Code verwenden, den Sie packen wollen, oder wie folgt ein einfaches Projekt erstellen:</span><span class="sxs-lookup"><span data-stu-id="67fea-121">You can use an existing .NET Standard Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="67fea-122">Wählen Sie in Visual Studio **Datei > Neu > Projekt** aus, erweitern Sie den Knoten **Visual C#-> .NET Standard**, wählen Sie die Vorlage „Klassenbibliothek (.NET Standard)“ aus, geben Sie dem Projekt den Namen „AppLogger“, und klicken Sie auf **OK**.</span><span class="sxs-lookup"><span data-stu-id="67fea-122">In Visual Studio, choose **File > New > Project**, expand the **Visual C# > .NET Standard** node, select the "Class Library (.NET Standard)" template, name the project AppLogger, and click **OK**.</span></span>

1. <span data-ttu-id="67fea-123">Klicken Sie mit der rechten Maustaste auf die resultierende Projektdatei, und wählen Sie **Erstellen** aus, um sicherzustellen, dass das Projekt ordnungsgemäß erstellt wurde.</span><span class="sxs-lookup"><span data-stu-id="67fea-123">Right-click on the resulting project file and select **Build** to make sure the project was created properly.</span></span> <span data-ttu-id="67fea-124">Die DLL befindet sich im Ordner „Debuggen“ (oder im Ordner „Release“, wenn Sie stattdessen diese Konfiguration erstellen).</span><span class="sxs-lookup"><span data-stu-id="67fea-124">The DLL is found within the Debug folder (or Release if you build that configuration instead).</span></span>

<span data-ttu-id="67fea-125">In einem echten NuGet-Paket implementieren Sie viele hilfreiche Features, mit denen andere Apps erstellen können.</span><span class="sxs-lookup"><span data-stu-id="67fea-125">Within a real NuGet package, of course, you implement many useful features with which others can build applications.</span></span> <span data-ttu-id="67fea-126">In dieser exemplarischen Vorgehensweise schreiben Sie jedoch keinen zusätzlichen Code, da eine Klassenbibliothek aus der Vorlage für die Erstellung eines Pakets ausreicht.</span><span class="sxs-lookup"><span data-stu-id="67fea-126">For this walkthrough, however, you won't write any additional code because a class library from the template is sufficient to create a package.</span></span> <span data-ttu-id="67fea-127">Wenn Sie noch immer Funktionscode für das Paket benötigen, verwenden Sie folgenden:</span><span class="sxs-lookup"><span data-stu-id="67fea-127">Still, if you'd like some functional code for the package, use the following:</span></span>

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
> <span data-ttu-id="67fea-128">Sofern es keinen Grund dafür gibt, der dagegen spricht, ist .NET Standard das bevorzugte Ziel für NuGet-Pakete, da es die größte Kompatibilitätsreichweite für verarbeitende Projekte bietet.</span><span class="sxs-lookup"><span data-stu-id="67fea-128">Unless you have a reason to choose otherwise, .NET Standard is the preferred target for NuGet packages, as it provides compatibility with the widest range of consuming projects.</span></span>

## <a name="configure-package-properties"></a><span data-ttu-id="67fea-129">Konfigurieren von Paketeigenschaften</span><span class="sxs-lookup"><span data-stu-id="67fea-129">Configure package properties</span></span>

1. <span data-ttu-id="67fea-130">Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste, und wählen Sie den Menübefehl **Eigenschaften** und dann die Registerkarte **Paket** aus.</span><span class="sxs-lookup"><span data-stu-id="67fea-130">Right-click the project in Solution Explorer, and choose **Properties** menu command, then select the **Package** tab.</span></span>

   <span data-ttu-id="67fea-131">Die Registerkarte **Paket** wird nur für Projekte im SDK-Format in Visual Studio angezeigt, in der Regel .NET Standard- oder .NET Core-Klassenbibliotheksprojekte. Wenn Sie mit einem Projekt im Nicht-SDK-Format arbeiten (in der Regel .NET Framework), [migrieren Sie das Projekt](../reference/migrate-packages-config-to-package-reference.md), und verwenden Sie die `dotnet`-CLI, oder befolgen Sie die Anleitungen unter [Erstellen und Veröffentlichen ](create-and-publish-a-package-using-visual-studio-net-framework.md) [eines .NET Framework-Pakets](create-and-publish-a-package-using-visual-studio-net-framework.md).</span><span class="sxs-lookup"><span data-stu-id="67fea-131">The **Package** tab appears only for SDK-style projects in Visual Studio, typically .NET Standard or .NET Core class library projects; if you are targeting a non-SDK style project (typically .NET Framework), either [migrate the project](../reference/migrate-packages-config-to-package-reference.md) and use `dotnet` CLI, or see [Create and publish a .NET Framework package](create-and-publish-a-package-using-visual-studio-net-framework.md) or see [Create and publish a .NET Framework package](create-and-publish-a-package-using-visual-studio-net-framework.md) instead for step-by-step instructions.</span></span>

    ![NuGet-Paketeigenschaften in einem Visual Studio-Projekt](media/qs_create-vs-01-package-properties.png)

    > [!Note]
    > <span data-ttu-id="67fea-133">Bei Paketen für die öffentliche Nutzung sollten Sie besonders auf die **Tags**-Eigenschaft achten, da Tags anderen dabei helfen, Ihr Paket zu finden und dessen Funktion zu verstehen.</span><span class="sxs-lookup"><span data-stu-id="67fea-133">For packages built for public consumption, pay special attention to the **Tags** property, as tags help others find your package and understand what it does.</span></span>

1. <span data-ttu-id="67fea-134">Geben Sie Ihrem Paket einen eindeutigen Bezeichner, und füllen Sie alle weiteren gewünschten Eigenschaften aus.</span><span class="sxs-lookup"><span data-stu-id="67fea-134">Give your package a unique identifier and fill out any other desired properties.</span></span> <span data-ttu-id="67fea-135">Eine Beschreibung der verschiedenen Eigenschaften finden Sie unter [.nuspec file reference (Referenz für NUSPEC-Dateien)](../reference/nuspec.md).</span><span class="sxs-lookup"><span data-stu-id="67fea-135">For a description of the different properties, see [.nuspec file reference](../reference/nuspec.md).</span></span> <span data-ttu-id="67fea-136">Alle diese Eigenschaften werden in das `.nuspec`-Manifest eingefügt, dass von Visual Studio für das Projekt erstellt wird.</span><span class="sxs-lookup"><span data-stu-id="67fea-136">All of the properties here go into the `.nuspec` manifest that Visual Studio creates for the project.</span></span>

    > [!Important]
    > <span data-ttu-id="67fea-137">Sie müssen dem Paket einen Bezeichner zuweisen, der auf nuget.org bzw. auf dem Host, den Sie verwenden, einzigartig ist.</span><span class="sxs-lookup"><span data-stu-id="67fea-137">You must give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="67fea-138">Für diese exemplarische Vorgehensweise wird empfohlen, im Namen „Sample“ oder „Test“ zu verwenden, da der Name in einem späteren Veröffentlichungsschritt öffentlich sichtbar gemacht wird (auch wenn es unwahrscheinlich ist, dass jemand versucht, es zu verwenden).</span><span class="sxs-lookup"><span data-stu-id="67fea-138">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>
    >
    > <span data-ttu-id="67fea-139">Bei dem Versuch, ein Paket mit einem Namen zu veröffentlichen, der bereits vorhanden ist, wird Ihnen ein Fehler angezeigt.</span><span class="sxs-lookup"><span data-stu-id="67fea-139">If you attempt to publish a package with a name that already exists, you see an error.</span></span>

1. <span data-ttu-id="67fea-140">Optional: Damit Sie die Eigenschaften direkt in der Projektdatei anzeigen können, führen Sie einen Rechtsklick im Projekt im Projektmappen-Explorer aus, und wählen Sie **Edit AppLogger.csproj** (AppLogger.csproj bearbeiten) aus.</span><span class="sxs-lookup"><span data-stu-id="67fea-140">Optional: to see the properties directly in the project file, right-click the project in Solution Explorer and select **Edit AppLogger.csproj**.</span></span>

   <span data-ttu-id="67fea-141">Diese Option ist nur ab Visual Studio 2017 für Projekte verfügbar, die das SDK-Attribut verwenden.</span><span class="sxs-lookup"><span data-stu-id="67fea-141">This option is only available starting in Visual Studio 2017 for projects that use the SDK-style attribute.</span></span> <span data-ttu-id="67fea-142">Klicken Sie andernfalls mit der rechten Maustaste auf das Projekt, und wählen Sie **Projekt entladen** aus.</span><span class="sxs-lookup"><span data-stu-id="67fea-142">Otherwise, right-click the project and choose **Unload Project**.</span></span> <span data-ttu-id="67fea-143">Klicken Sie dann mit der rechten Maustaste auf das entladene Projekt, und wählen Sie **"AppLogger" bearbeiten** aus.</span><span class="sxs-lookup"><span data-stu-id="67fea-143">Then right-click the unloaded project and choose **Edit AppLogger.csproj**.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="67fea-144">Ausführen des Befehls pack</span><span class="sxs-lookup"><span data-stu-id="67fea-144">Run the pack command</span></span>

1. <span data-ttu-id="67fea-145">Legen Sie die Konfiguration auf **Release** (Freigeben) fest.</span><span class="sxs-lookup"><span data-stu-id="67fea-145">Set the configuration to **Release**.</span></span>

1. <span data-ttu-id="67fea-146">Klicken Sie im **Projektmappen-Explorer** mit der rechten Maustaste auf das Projekt, und wählen Sie den Befehl **Packen** aus:</span><span class="sxs-lookup"><span data-stu-id="67fea-146">Right click the project in **Solution Explorer** and select the **Pack** command:</span></span>

    ![Der NuGet-Befehl „pack“ im Kontextmenü des Visual Studio-Projekts](media/qs_create-vs-02-pack-command.png)

    <span data-ttu-id="67fea-148">Wenn der Befehl **Packen** nicht angezeigt wird, weist das Projekt wahrscheinlich nicht das SDK-Format auf, und Sie müssen die `nuget.exe`-CLI verwenden.</span><span class="sxs-lookup"><span data-stu-id="67fea-148">If you don't see the **Pack** command, your project is probably not an SDK-style project and you need to use the `nuget.exe` CLI.</span></span> <span data-ttu-id="67fea-149">[Migrieren Sie das Projekt](../reference/migrate-packages-config-to-package-reference.md), und verwenden Sie die `dotnet`-CLI, oder befolgen Sie die Anleitungen unter [Erstellen und Veröffentlichen eines .NET Framework-Pakets](create-and-publish-a-package-using-visual-studio-net-framework.md).</span><span class="sxs-lookup"><span data-stu-id="67fea-149">Either [migrate the project](../reference/migrate-packages-config-to-package-reference.md) and use `dotnet` CLI, or see [Create and publish a .NET Framework package](create-and-publish-a-package-using-visual-studio-net-framework.md) instead for step-by-step instructions.</span></span>

1. <span data-ttu-id="67fea-150">Visual Studio erstellt das Projekt und die `.nupkg`-Datei.</span><span class="sxs-lookup"><span data-stu-id="67fea-150">Visual Studio builds the project and creates the `.nupkg` file.</span></span> <span data-ttu-id="67fea-151">Überprüfen Sie das **Ausgabefenster** auf Angaben (ähnlich wie im folgenden Beispiel), die den Pfad zur Paketdatei enthalten.</span><span class="sxs-lookup"><span data-stu-id="67fea-151">Examine the **Output** window for details (similar to the following), which contains the path to the package file.</span></span> <span data-ttu-id="67fea-152">Beachten Sie außerdem, dass sich die erstellte Assembly in `bin\Release\netstandard2.0` befindet, wie es dem Ziel .NET Standard 2.0 entspricht.</span><span class="sxs-lookup"><span data-stu-id="67fea-152">Note also that the built assembly is in `bin\Release\netstandard2.0` as befits the .NET Standard 2.0 target.</span></span>

    ```output
    1>------ Build started: Project: AppLogger, Configuration: Release Any CPU ------
    1>AppLogger -> d:\proj\AppLogger\AppLogger\bin\Release\netstandard2.0\AppLogger.dll
    1>Successfully created package 'd:\proj\AppLogger\AppLogger\bin\Release\AppLogger.1.0.0.nupkg'.
    ========== Build: 1 succeeded, 0 failed, 0 up-to-date, 0 skipped ==========
    ```

### <a name="alternate-option-pack-with-msbuild"></a><span data-ttu-id="67fea-153">Alternative Option: „pack“ mit MSBuild</span><span class="sxs-lookup"><span data-stu-id="67fea-153">Alternate option: pack with MSBuild</span></span>

<span data-ttu-id="67fea-154">Als Alternative zur Verwendung des Menübefehls **Packen** unterstützen NuGet 4.x und höher und MSBuild 15.1 und höher ein `pack`-Ziel, wenn das Projekt die nötigen Paketdaten enthält.</span><span class="sxs-lookup"><span data-stu-id="67fea-154">As an alternate to using the **Pack** menu command, NuGet 4.x+ and MSBuild 15.1+ supports a `pack` target when the project contains the necessary package data.</span></span> <span data-ttu-id="67fea-155">Öffnen Sie eine Eingabeaufforderung, navigieren Sie zum Projektordner, und führen Sie den folgenden Befehl aus.</span><span class="sxs-lookup"><span data-stu-id="67fea-155">Open a command prompt, navigate to your project folder and run the following command.</span></span> <span data-ttu-id="67fea-156">(In der Regel sollten Sie die „Developer-Eingabeaufforderung für Visual Studio“ über das Startmenü starten, da dieses mit allen nötigen Pfaden für MSBuild konfiguriert ist.)</span><span class="sxs-lookup"><span data-stu-id="67fea-156">(You typically want to start the "Developer Command Prompt for Visual Studio" from the Start menu, as it will be configured with all the necessary paths for MSBuild.)</span></span>

```cli
msbuild -t:pack -p:Configuration=Release
```

<span data-ttu-id="67fea-157">Sie finden das Paket im Ordner `bin\Release`.</span><span class="sxs-lookup"><span data-stu-id="67fea-157">The package can then be found in the `bin\Release` folder.</span></span>

<span data-ttu-id="67fea-158">Zusätzliche Optionen zu `msbuild -t:pack` finden Sie unter [NuGet pack and restore as MSBuild targets (NuGet-Befehle „pack“ und „restore“ MSBuild-Ziele)](../reference/msbuild-targets.md#pack-target).</span><span class="sxs-lookup"><span data-stu-id="67fea-158">For additional options with `msbuild -t:pack`, see [NuGet pack and restore as MSBuild targets](../reference/msbuild-targets.md#pack-target).</span></span>

## <a name="publish-the-package"></a><span data-ttu-id="67fea-159">Veröffentlichen des Pakets</span><span class="sxs-lookup"><span data-stu-id="67fea-159">Publish the package</span></span>

<span data-ttu-id="67fea-160">Sobald Sie eine `.nupkg`-Datei haben, können Sie diese gemeinsam mit einem API-Schlüssel von nuget.org über die `nuget.exe`-CLI oder die `dotnet.exe`-CLI auf nuget.org veröffentlichen.</span><span class="sxs-lookup"><span data-stu-id="67fea-160">Once you have a `.nupkg` file, you publish it to nuget.org using either the `nuget.exe` CLI or the `dotnet.exe` CLI along with an API key acquired from nuget.org.</span></span>

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="67fea-161">Erwerben des API-Schlüssels</span><span class="sxs-lookup"><span data-stu-id="67fea-161">Acquire your API key</span></span>

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-dotnet-nuget-push-dotnet-cli"></a><span data-ttu-id="67fea-162">Veröffentlichen mit „dotnet nuget push“ (dotnet-CLI)</span><span class="sxs-lookup"><span data-stu-id="67fea-162">Publish with dotnet nuget push (dotnet CLI)</span></span>

<span data-ttu-id="67fea-163">Dieser Schritt ist die empfohlene Alternative zur Verwendung von `nuget.exe`.</span><span class="sxs-lookup"><span data-stu-id="67fea-163">This step is the recommended alternative to using `nuget.exe`.</span></span>

<span data-ttu-id="67fea-164">Bevor Sie das Paket veröffentlichen können, müssen Sie eine Befehlszeile öffnen.</span><span class="sxs-lookup"><span data-stu-id="67fea-164">Before you can publish the package, you must first open a command line.</span></span>

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-with-nuget-push-nugetexe-cli"></a><span data-ttu-id="67fea-165">Veröffentlichen mit „nuget push“ (nuget.exe-CLI)</span><span class="sxs-lookup"><span data-stu-id="67fea-165">Publish with nuget push (nuget.exe CLI)</span></span>

<span data-ttu-id="67fea-166">Dieser Schritt ist eine Alternative zur Verwendung von `dotnet.exe`.</span><span class="sxs-lookup"><span data-stu-id="67fea-166">This step is an alternative to using `dotnet.exe`.</span></span>

1. <span data-ttu-id="67fea-167">Öffnen Sie eine Befehlszeile, und navigieren Sie zu dem Ordner, der die `.nupkg`-Datei enthält.</span><span class="sxs-lookup"><span data-stu-id="67fea-167">Open a command line and change to the folder containing the `.nupkg` file.</span></span>

1. <span data-ttu-id="67fea-168">Führen Sie den folgenden Befehl aus, geben Sie dabei den Paketnamen (eindeutige Paket-ID) an, und ersetzen Sie den Schlüsselwert durch den API-Schlüssel:</span><span class="sxs-lookup"><span data-stu-id="67fea-168">Run the following command, specifying your package name (unique package ID) and replacing the key value with your API key:</span></span>

    ```cli
    nuget push AppLogger.1.0.0.nupkg qz2jga8pl3dvn2akksyquwcs9ygggg4exypy3bhxy6w6x6 -Source https://api.nuget.org/v3/index.json
    ```

1. <span data-ttu-id="67fea-169">In „NuGet.exe“ werden die Ergebnisse des Veröffentlichungsvorgangs angezeigt:</span><span class="sxs-lookup"><span data-stu-id="67fea-169">nuget.exe displays the results of the publishing process:</span></span>

    ```output
    Pushing AppLogger.1.0.0.nupkg to 'https://www.nuget.org/api/v2/package'...
        PUT https://www.nuget.org/api/v2/package/
        Created https://www.nuget.org/api/v2/package/ 6829ms
    Your package was pushed.
    ```

<span data-ttu-id="67fea-170">Siehe [nuget push-Befehl](../reference/cli-reference/cli-ref-push.md).</span><span class="sxs-lookup"><span data-stu-id="67fea-170">See [nuget push](../reference/cli-reference/cli-ref-push.md).</span></span>

### <a name="publish-errors"></a><span data-ttu-id="67fea-171">Veröffentlichungsfehler</span><span class="sxs-lookup"><span data-stu-id="67fea-171">Publish errors</span></span>

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="67fea-172">Verwalten des veröffentlichten Pakets</span><span class="sxs-lookup"><span data-stu-id="67fea-172">Manage the published package</span></span>

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="adding-a-readme-and-other-files"></a><span data-ttu-id="67fea-173">Hinzufügen einer Infodatei und anderer Dateien</span><span class="sxs-lookup"><span data-stu-id="67fea-173">Adding a readme and other files</span></span>

<span data-ttu-id="67fea-174">Bearbeiten Sie die Projektdatei, und verwenden Sie die `content`-Eigenschaft, um Dateien, die im Paket eingeschlossen werden sollen, direkt anzugeben:</span><span class="sxs-lookup"><span data-stu-id="67fea-174">To directly specify files to include in the package, edit the project file and use the `content` property:</span></span>

```xml
<ItemGroup>
  <Content Include="readme.txt">
    <Pack>true</Pack>
    <PackagePath>\</PackagePath>
  </Content>
</ItemGroup>
```

<span data-ttu-id="67fea-175">Dies schließt eine Datei namens `readme.txt` im Stammverzeichnis ein.</span><span class="sxs-lookup"><span data-stu-id="67fea-175">This will include a file named `readme.txt` in the package root.</span></span> <span data-ttu-id="67fea-176">Visual Studio zeigt unmittelbar nach der direkten Installation des Pakets den Inhalt der Datei als Nur-Text an.</span><span class="sxs-lookup"><span data-stu-id="67fea-176">Visual Studio displays the contents of that file as plain text immediately after installing the package directly.</span></span> <span data-ttu-id="67fea-177">Für Pakete, die als Abhängigkeiten installiert wurden, werden keine Infodateien angezeigt.</span><span class="sxs-lookup"><span data-stu-id="67fea-177">(Readme files are not displayed for packages installed as dependencies).</span></span> <span data-ttu-id="67fea-178">Die Infodatei für das Paket „HtmlAgilityPack“ wird z.B. folgendermaßen angezeigt:</span><span class="sxs-lookup"><span data-stu-id="67fea-178">For example, here's how the readme for the HtmlAgilityPack package appears:</span></span>

![Anzeige einer Infodatei für ein NuGet-Paket nach der Installation](../create-packages/media/Create_01-ShowReadme.png)

> [!Note]
> <span data-ttu-id="67fea-180">Wenn Sie die Datei „readme.txt“ lediglich im Stammverzeichnis hinzufügen, wird diese nicht im resultierenden Paket eingeschlossen.</span><span class="sxs-lookup"><span data-stu-id="67fea-180">Merely adding the readme.txt at the project root will not result in it being included in the resulting package.</span></span>

## <a name="related-topics"></a><span data-ttu-id="67fea-181">Verwandte Themen</span><span class="sxs-lookup"><span data-stu-id="67fea-181">Related topics</span></span>

- [<span data-ttu-id="67fea-182">Erstellen eines Pakets</span><span class="sxs-lookup"><span data-stu-id="67fea-182">Create a Package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="67fea-183">Veröffentlichen eines Pakets</span><span class="sxs-lookup"><span data-stu-id="67fea-183">Publish a Package</span></span>](../nuget-org/publish-a-package.md)
- [<span data-ttu-id="67fea-184">Vorabversionen von Paketen</span><span class="sxs-lookup"><span data-stu-id="67fea-184">Pre-release Packages</span></span>](../create-packages/Prerelease-Packages.md)
- [<span data-ttu-id="67fea-185">Unterstützung mehrerer Zielframeworks</span><span class="sxs-lookup"><span data-stu-id="67fea-185">Support multiple target frameworks</span></span>](../create-packages/multiple-target-frameworks-project-file.md)
- [<span data-ttu-id="67fea-186">Paketversionsverwaltung</span><span class="sxs-lookup"><span data-stu-id="67fea-186">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="67fea-187">Erstellen von lokalisierten Paketen</span><span class="sxs-lookup"><span data-stu-id="67fea-187">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="67fea-188">Dokumentation zur .NET Standard-Bibliothek</span><span class="sxs-lookup"><span data-stu-id="67fea-188">.NET Standard Library documentation</span></span>](/dotnet/articles/standard/library)
- [<span data-ttu-id="67fea-189">Portieren von .NET Framework auf .NET Core</span><span class="sxs-lookup"><span data-stu-id="67fea-189">Porting to .NET Core from .NET Framework</span></span>](/dotnet/articles/core/porting/index)
