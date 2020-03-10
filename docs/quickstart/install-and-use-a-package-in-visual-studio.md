---
title: Installieren und Verwenden eines NuGet-Pakets in Visual Studio
description: Ein Tutorial mit einer exemplarischen Vorgehensweise bei der Installation und Verwendung eines NuGet-Pakets in einem Visual Studio-Projekt.
author: karann-msft
ms.author: karann
ms.date: 07/24/2018
ms.topic: quickstart
ms.openlocfilehash: 96e138561390984d9def495ba5e091c43023cc92
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231330"
---
# <a name="quickstart-install-and-use-a-package-in-visual-studio-windows-only"></a><span data-ttu-id="7dd2e-103">Schnellstart: Installieren und Verwenden eines Pakets in Visual Studio (nur Windows)</span><span class="sxs-lookup"><span data-stu-id="7dd2e-103">Quickstart: Install and use a package in Visual Studio (Windows only)</span></span>

<span data-ttu-id="7dd2e-104">NuGet-Pakete enthalten wiederverwendbaren Code, der von anderen Entwicklern für die Verwendung in Ihren Projekten verfügbar gemacht wird.</span><span class="sxs-lookup"><span data-stu-id="7dd2e-104">NuGet packages contain reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="7dd2e-105">Unter [Was ist NuGet?](../What-is-NuGet.md) finden Sie weitere Informationen.</span><span class="sxs-lookup"><span data-stu-id="7dd2e-105">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span> <span data-ttu-id="7dd2e-106">Pakete werden über den NuGet-Paket-Manager oder die Paket-Manager-Konsole in einem Visual Studio-Projekt installiert.</span><span class="sxs-lookup"><span data-stu-id="7dd2e-106">Packages are installed into a Visual Studio project using the NuGet Package Manager or the Package Manager Console.</span></span> <span data-ttu-id="7dd2e-107">Dieser Artikel zeigt den Prozess mit dem beliebten [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/)-Paket und einem WPF-Projekt (Windows Presentation Foundation).</span><span class="sxs-lookup"><span data-stu-id="7dd2e-107">This article demonstrates the process using the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package and a Windows Presentation Foundation (WPF) project.</span></span> <span data-ttu-id="7dd2e-108">Derselbe Prozess ist auch auf jedes andere .NET oder .NET Core-Projekt anwendbar.</span><span class="sxs-lookup"><span data-stu-id="7dd2e-108">The same process applies to any other .NET or .NET Core project.</span></span>

<span data-ttu-id="7dd2e-109">Beziehen Sie sich nach der Installation mit `using <namespace>` auf das Paket im Code, wobei \<Namespace\> für das von Ihnen verwendete Paket spezifisch ist.</span><span class="sxs-lookup"><span data-stu-id="7dd2e-109">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="7dd2e-110">Nachdem der Verweis erfolgt ist, können Sie das Paket über die zugehörige API aufrufen.</span><span class="sxs-lookup"><span data-stu-id="7dd2e-110">Once the reference is made, you can call the package through its API.</span></span>

> [!Tip]
> <span data-ttu-id="7dd2e-111">**Einstieg in nuget.org**: .NET-Entwickler finden Komponenten für die Verwendung in ihren eigenen Anwendungen üblicherweise durch das Durchsuchen von *nuget.org*.</span><span class="sxs-lookup"><span data-stu-id="7dd2e-111">**Start with nuget.org**: Browsing *nuget.org* is how .NET developers typically find components they can reuse in their own applications.</span></span> <span data-ttu-id="7dd2e-112">Sie können *nuget.org* direkt durchsuchen oder in Visual Studio nach Paketen suchen und diese installieren, wie in diesem Artikel dargestellt wird.</span><span class="sxs-lookup"><span data-stu-id="7dd2e-112">You can search *nuget.org* directly or find and install packages within Visual Studio as shown in this article.</span></span> <span data-ttu-id="7dd2e-113">Allgemeine Informationen finden Sie [Suchen und Auswerten von NuGet-Paketen](../consume-packages/finding-and-choosing-packages.md).</span><span class="sxs-lookup"><span data-stu-id="7dd2e-113">For general information, see [Find and evaluate NuGet packages](../consume-packages/finding-and-choosing-packages.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7dd2e-114">Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="7dd2e-114">Prerequisites</span></span>

- <span data-ttu-id="7dd2e-115">Visual Studio 2019 mit der .NET Desktop Development-Workload.</span><span class="sxs-lookup"><span data-stu-id="7dd2e-115">Visual Studio 2019 with the .NET Desktop Development workload.</span></span>

<span data-ttu-id="7dd2e-116">Sie können die 2019 Community-Edition kostenlos von [visualstudio.com](https://www.visualstudio.com/) installieren oder die Professional oder Enterprise Edition verwenden.</span><span class="sxs-lookup"><span data-stu-id="7dd2e-116">You can install the 2019 Community edition for free from [visualstudio.com](https://www.visualstudio.com/) or use the Professional or Enterprise editions.</span></span>

<span data-ttu-id="7dd2e-117">Wenn Sie Visual Studio für Mac verwenden, lesen Sie [Installieren und Verwenden eines Pakets in Visual Studio für Mac](install-and-use-a-package-in-visual-studio-mac.md).</span><span class="sxs-lookup"><span data-stu-id="7dd2e-117">If you're using Visual Studio for Mac, see [Install and use a package in Visual Studio for Mac](install-and-use-a-package-in-visual-studio-mac.md).</span></span>

## <a name="create-a-project"></a><span data-ttu-id="7dd2e-118">Erstellen eines Projekts</span><span class="sxs-lookup"><span data-stu-id="7dd2e-118">Create a project</span></span>

<span data-ttu-id="7dd2e-119">NuGet-Pakete können in jedem beliebigen .NET-Projekt installiert werden, vorausgesetzt, das Paket unterstützt dasselbe Zielframework wie das Projekt.</span><span class="sxs-lookup"><span data-stu-id="7dd2e-119">NuGet packages can be installed into any .NET project, provided that the package supports the same target framework as the project.</span></span>

<span data-ttu-id="7dd2e-120">Verwenden Sie für diese exemplarische Vorgehensweise eine einfache WPF-App.</span><span class="sxs-lookup"><span data-stu-id="7dd2e-120">For this walkthrough, use a simple WPF app.</span></span> <span data-ttu-id="7dd2e-121">Erstellen Sie ein Projekt in Visual Studio mit **Datei** > **Neues Projekt**, geben Sie **.NET** in das Suchfeld ein, und wählen Sie dann die **WPF App (.NET Framework)** aus.</span><span class="sxs-lookup"><span data-stu-id="7dd2e-121">Create a project in Visual Studio using **File** > **New Project**, typing **.NET** in the search box, and then selecting the **WPF App (.NET Framework)**.</span></span> <span data-ttu-id="7dd2e-122">Klicken Sie auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="7dd2e-122">Click **Next**.</span></span> <span data-ttu-id="7dd2e-123">Akzeptieren Sie die Standardwerte für **Framework**, wenn Sie dazu aufgefordert werden.</span><span class="sxs-lookup"><span data-stu-id="7dd2e-123">Accept the default values for **Framework** when prompted.</span></span>

<span data-ttu-id="7dd2e-124">Visual Studio erstellt das Projekt, das im Projektmappen-Explorer geöffnet wird.</span><span class="sxs-lookup"><span data-stu-id="7dd2e-124">Visual Studio creates the project, which opens in Solution Explorer.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="7dd2e-125">Hinzufügen des NuGet-Pakets „Newtonsoft.Json“</span><span class="sxs-lookup"><span data-stu-id="7dd2e-125">Add the Newtonsoft.Json NuGet package</span></span>

<span data-ttu-id="7dd2e-126">Sie können entweder dem NuGet-Paket-Manager oder die Paket-Manager-Konsole verwenden, um das Paket zu installieren.</span><span class="sxs-lookup"><span data-stu-id="7dd2e-126">To install the package, you can use either the NuGet Package Manager or the Package Manager Console.</span></span> <span data-ttu-id="7dd2e-127">Beim Installieren eines Pakets zeichnet NuGet die Abhängigkeit entweder in Ihrer Projektdatei oder in einer `packages.config`-Datei auf (je nach Projektformat).</span><span class="sxs-lookup"><span data-stu-id="7dd2e-127">When you install a package, NuGet records the dependency in either your project file or a `packages.config` file (depending on the project format).</span></span> <span data-ttu-id="7dd2e-128">Weitere Informationen finden Sie unter [Übersicht und Workflow für die Paketerstellung](../consume-packages/Overview-and-Workflow.md).</span><span class="sxs-lookup"><span data-stu-id="7dd2e-128">For more information, see [Package consumption overview and workflow](../consume-packages/Overview-and-Workflow.md).</span></span>

### <a name="nuget-package-manager"></a><span data-ttu-id="7dd2e-129">NuGet-Paket-Manager</span><span class="sxs-lookup"><span data-stu-id="7dd2e-129">NuGet Package Manager</span></span>

1. <span data-ttu-id="7dd2e-130">Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf **Verweise**, und wählen Sie **NuGet-Pakete verwalten** aus.</span><span class="sxs-lookup"><span data-stu-id="7dd2e-130">In Solution Explorer, right-click **References** and choose **Manage NuGet Packages**.</span></span>

    ![Verwalten des Befehls für NuGet-Pakete bei Projektverweisen](media/QS_Use-02-ManageNuGetPackages.png)

1. <span data-ttu-id="7dd2e-132">Wählen Sie als **Paketquelle** nuget.org aus. Wählen Sie anschließend die Registerkarte **Durchsuchen** aus, suchen Sie nach dem Paket **Newtonsoft.Json**, und wählen Sie das Paket in der Liste sowie anschließend **Installieren** aus:</span><span class="sxs-lookup"><span data-stu-id="7dd2e-132">Choose "nuget.org" as the **Package source**, select the **Browse** tab, search for **Newtonsoft.Json**, select that package in the list, and select **Install**:</span></span>

    ![Suchen des Pakets „Newtonsoft.Json“](media/QS_Use-03-NewtonsoftJson.png)

    <span data-ttu-id="7dd2e-134">Weitere Informationen zum NuGet-Paket-Manager finden Sie unter [Installieren und Verwalten von Paketen mithilfe von Visual Studio.](../consume-packages/install-use-packages-visual-studio.md)</span><span class="sxs-lookup"><span data-stu-id="7dd2e-134">If you want more information on the NuGet Package Manager, see [Install and manage packages using Visual Studio](../consume-packages/install-use-packages-visual-studio.md).</span></span>

1. <span data-ttu-id="7dd2e-135">Akzeptieren Sie die Lizenzbedingungen.</span><span class="sxs-lookup"><span data-stu-id="7dd2e-135">Accept any license prompts.</span></span>

1. <span data-ttu-id="7dd2e-136">(Nur Visual Studio 2017) Wenn Sie dazu aufgefordert werden, ein Format für die Paketverwaltung auszuwählen, wählen Sie **PackageReference in Projektdatei**:</span><span class="sxs-lookup"><span data-stu-id="7dd2e-136">(Visual Studio 2017 only) If prompted to select a package management format, select **PackageReference in project file**:</span></span>

    ![Auswahl eines Paketverwaltungsformats](media/QS_Use-03b-SelectFormat.png)

1. <span data-ttu-id="7dd2e-138">Wählen Sie **OK** aus, wenn Sie dazu aufgefordert werden, Änderungen zu überprüfen.</span><span class="sxs-lookup"><span data-stu-id="7dd2e-138">If prompted to review changes, select **OK**.</span></span>

### <a name="package-manager-console"></a><span data-ttu-id="7dd2e-139">Paket-Manager-Konsole</span><span class="sxs-lookup"><span data-stu-id="7dd2e-139">Package Manager Console</span></span>

1. <span data-ttu-id="7dd2e-140">Wählen Sie den Menübefehl **Tools** > **NuGet-Paket-Manager** > **Paket-Manager-Konsole** aus.</span><span class="sxs-lookup"><span data-stu-id="7dd2e-140">Select the **Tools** > **NuGet Package Manager** > **Package Manager Console** menu command.</span></span>

1. <span data-ttu-id="7dd2e-141">Wenn die Konsole geöffnet wird, überprüfen Sie, ob die Dropdownliste **Standardprojekt** das Projekt anzeigt, in das Sie das Paket installieren möchten.</span><span class="sxs-lookup"><span data-stu-id="7dd2e-141">Once the console opens, check that the **Default project** drop-down list shows the project into which you want to install the package.</span></span> <span data-ttu-id="7dd2e-142">Wenn Sie ein einzelnes Projekt in der Projektmappe haben, ist es bereits ausgewählt.</span><span class="sxs-lookup"><span data-stu-id="7dd2e-142">If you have a single project in the solution, it is already selected.</span></span>

    ![Suchen des Pakets „Newtonsoft.Json“](media/QS_Use-08-Console1.png)

1. <span data-ttu-id="7dd2e-144">Geben Sie den Befehl `Install-Package Newtonsoft.Json` ein (siehe [Install-Package](../reference/ps-reference/ps-ref-install-package.md)).</span><span class="sxs-lookup"><span data-stu-id="7dd2e-144">Enter the command `Install-Package Newtonsoft.Json` (see [Install-Package](../reference/ps-reference/ps-ref-install-package.md)).</span></span> <span data-ttu-id="7dd2e-145">Das Konsolenfenster zeigt die Ausgabe des Befehls.</span><span class="sxs-lookup"><span data-stu-id="7dd2e-145">The console window shows output for the command.</span></span> <span data-ttu-id="7dd2e-146">Fehler deuten normalerweise darauf hin, dass das Paket nicht mit dem Zielframework des Projekts kompatibel ist.</span><span class="sxs-lookup"><span data-stu-id="7dd2e-146">Errors typically indicate that the package isn't compatible with the project's target framework.</span></span>

   <span data-ttu-id="7dd2e-147">Weitere Informationen zur Paket-Manager-Konsole finden Sie unter [Installieren und Verwalten von Paketen mithilfe der Paket-Manager-Konsole.](../consume-packages/install-use-packages-powershell.md)</span><span class="sxs-lookup"><span data-stu-id="7dd2e-147">If you want more information on the Package Manager Console, see [Install and manage packages using Package Manager Console](../consume-packages/install-use-packages-powershell.md).</span></span>

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="7dd2e-148">Verwenden der API „Newtonsoft.Json“ in der App</span><span class="sxs-lookup"><span data-stu-id="7dd2e-148">Use the Newtonsoft.Json API in the app</span></span>

<span data-ttu-id="7dd2e-149">Wenn das Paket „Newtonsoft.Json“ im Projekt enthalten ist, können Sie die zugehörige `JsonConvert.SerializeObject`-Methode aufrufen, um ein Objekt in eine lesbare Zeichenfolge zu konvertieren.</span><span class="sxs-lookup"><span data-stu-id="7dd2e-149">With the Newtonsoft.Json package in the project, you can call its `JsonConvert.SerializeObject` method to convert an object to a human-readable string.</span></span>

1. <span data-ttu-id="7dd2e-150">Öffnen Sie `MainWindow.xaml`, und ersetzen Sie das vorhandene `Grid`-Element mit folgendem:</span><span class="sxs-lookup"><span data-stu-id="7dd2e-150">Open `MainWindow.xaml` and replace the existing `Grid` element with the following:</span></span>

    ```xaml
    <Grid Background="White">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Width="100px" HorizontalAlignment="Center" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" HorizontalAlignment="Center" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. <span data-ttu-id="7dd2e-151">Öffnen Sie die Datei `MainWindow.xaml.cs` (befindet sich in Projektmappen-Explorer unter dem Knoten `MainWindow.xaml`), und fügen Sie den folgenden Code in der `MainWindow`-Klasse ein:</span><span class="sxs-lookup"><span data-stu-id="7dd2e-151">Open the `MainWindow.xaml.cs` file (located in Solution Explorer under the `MainWindow.xaml` node), and insert the following code inside the `MainWindow` class:</span></span>

    ```cs
    public class Account
    {
        public string Name { get; set; }
        public string Email { get; set; }
        public DateTime DOB { get; set; }
    }

    private void Button_Click(object sender, RoutedEventArgs e)
    {
        Account account = new Account
        {
            Name = "John Doe",
            Email = "john@microsoft.com",
            DOB = new DateTime(1980, 2, 20, 0, 0, 0, DateTimeKind.Utc),
        };
        string json = JsonConvert.SerializeObject(account, Formatting.Indented);
        TextBlock.Text = json;
    }
    ```

1. <span data-ttu-id="7dd2e-152">Obwohl Sie das Paket „Newtonsoft.Json“ zum Projekt hinzugefügt haben, erscheinen unter `JsonConvert` rote Wellenlinien, da eine `using`-Anweisung am Anfang der Codedatei erforderlich ist:</span><span class="sxs-lookup"><span data-stu-id="7dd2e-152">Even though you added the Newtonsoft.Json package to the project, red squiggles appears under `JsonConvert` because you need a `using` statement at the top of the code file:</span></span>

    ```cs
    using Newtonsoft.Json;
    ```

1. <span data-ttu-id="7dd2e-153">Erstellen Sie die App, und führen Sie sie aus, indem Sie F5 drücken oder **Debuggen** > **Debuggen starten** auswählen:</span><span class="sxs-lookup"><span data-stu-id="7dd2e-153">Build and run the app by pressing F5 or selecting **Debug** > **Start Debugging**:</span></span>

    ![Ursprüngliche Ausgabe der WPF-App](media/QS_Use-06-AppStart.png)

1. <span data-ttu-id="7dd2e-155">Klicken Sie auf die Schaltfläche, um die Inhalte des Elements „TextBlock“ anzuzeigen, das durch JSON-Text ersetzt wurde:</span><span class="sxs-lookup"><span data-stu-id="7dd2e-155">Select on the button to see the contents of the TextBlock replaced with some JSON text:</span></span>

    ![Ausgabe der WPF-App nach Klicken auf die Schaltfläche](media/QS_Use-07-AppEnd.png)

## <a name="related-video"></a><span data-ttu-id="7dd2e-157">Zugehörige Videos</span><span class="sxs-lookup"><span data-stu-id="7dd2e-157">Related video</span></span>

> [!Video https://channel9.msdn.com/Series/NuGet-101/Install-and-Use-a-NuGet-Package-with-Visual-Studio-2-of-5/player]

<span data-ttu-id="7dd2e-158">Auf [Channel 9](https://channel9.msdn.com/Series/NuGet-101) und auf [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_) finden Sie weitere Videos zu NuGet.</span><span class="sxs-lookup"><span data-stu-id="7dd2e-158">Find more NuGet videos on [Channel 9](https://channel9.msdn.com/Series/NuGet-101) and [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_).</span></span>

## <a name="next-steps"></a><span data-ttu-id="7dd2e-159">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="7dd2e-159">Next steps</span></span>

<span data-ttu-id="7dd2e-160">Herzlichen Glückwunsch zur Installation und Verwendung Ihres ersten NuGet-Pakets!</span><span class="sxs-lookup"><span data-stu-id="7dd2e-160">Congratulations on installing and using your first NuGet package!</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="7dd2e-161">Installieren und Verwalten von Paketen mit Visual Studio</span><span class="sxs-lookup"><span data-stu-id="7dd2e-161">Install and manage packages using Visual Studio</span></span>](../consume-packages/install-use-packages-visual-studio.md)

> [!div class="nextstepaction"]
> [<span data-ttu-id="7dd2e-162">Installieren und Verwalten von Paketen mit der Paket-Manager-Konsole</span><span class="sxs-lookup"><span data-stu-id="7dd2e-162">Install and manage packages using Package Manager Console</span></span>](../consume-packages/install-use-packages-powershell.md)

<span data-ttu-id="7dd2e-163">Klicken Sie für weitere Informationen zu den Features von NuGet auf folgende Links.</span><span class="sxs-lookup"><span data-stu-id="7dd2e-163">To explore more that NuGet has to offer, select the links below.</span></span>

- [<span data-ttu-id="7dd2e-164">Übersicht über den Paketverbrauch und dessen Workflows</span><span class="sxs-lookup"><span data-stu-id="7dd2e-164">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="7dd2e-165">Suchen und Auswählen von Paketen</span><span class="sxs-lookup"><span data-stu-id="7dd2e-165">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="7dd2e-166">Paketverweise in Projektdateien</span><span class="sxs-lookup"><span data-stu-id="7dd2e-166">Package references in project files</span></span>](../consume-packages/package-references-in-project-files.md)
