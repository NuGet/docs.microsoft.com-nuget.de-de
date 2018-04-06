---
title: Einführender Leitfaden zur Verwendung von NuGet-Paketen innerhalb von Visual Studio | Microsoft-Dokumentation
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/23/2018
ms.topic: quickstart
ms.prod: nuget
ms.technology: ''
description: Ein Tutorial mit einer exemplarischen Vorgehensweise bei der Installation und Verwendung eines NuGet-Pakets in einem Visual Studio-Projekt.
keywords: NuGet installieren, NuGet-Paketverbrauch, Installieren von NuGet-Paketen, NuGet-Paketverweise, Verwenden von NuGet-Paketen
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 4205893cc02cffff8926513a555393d10c046f43
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="install-and-use-a-package-in-visual-studio"></a><span data-ttu-id="9d5aa-104">Installieren und Verwenden eines Pakets in Visual Studio</span><span class="sxs-lookup"><span data-stu-id="9d5aa-104">Install and use a package in Visual Studio</span></span>

<span data-ttu-id="9d5aa-105">NuGet-Pakete enthalten wiederverwendbaren Code, der von anderen Entwicklern für die Verwendung in Ihren Projekten verfügbar gemacht wird.</span><span class="sxs-lookup"><span data-stu-id="9d5aa-105">NuGet packages contain reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="9d5aa-106">Unter [Was ist NuGet?](../What-is-NuGet.md) finden Sie weitere Informationen.</span><span class="sxs-lookup"><span data-stu-id="9d5aa-106">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span> <span data-ttu-id="9d5aa-107">Pakete werden über die Paket-Manager-Benutzeroberfläche oder die Paket-Manager-Konsole in einem Visual Studio-Projekt installiert.</span><span class="sxs-lookup"><span data-stu-id="9d5aa-107">Packages are installed into a Visual Studio project using the Package Manager UI or the Package Manager Console.</span></span> <span data-ttu-id="9d5aa-108">Dieser Artikel zeigt den Prozess mit dem beliebten [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/)-Paket und einem UWP-Projekt (Universelle Windows-Plattform).</span><span class="sxs-lookup"><span data-stu-id="9d5aa-108">This article demonstrates the process using the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package and a Universal Windows Platform (UWP) project.</span></span> <span data-ttu-id="9d5aa-109">Derselbe Prozess ist auch auf jedes andere .NET oder .NET Core-Projekt anwendbar.</span><span class="sxs-lookup"><span data-stu-id="9d5aa-109">The same process applies to any other .NET or .NET Core project.</span></span>

<span data-ttu-id="9d5aa-110">Beziehen Sie sich nach der Installation mit `using <namespace>` auf das Paket im Code, wobei \<Namespace\> für das von Ihnen verwendete Paket spezifisch ist.</span><span class="sxs-lookup"><span data-stu-id="9d5aa-110">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="9d5aa-111">Nachdem der Verweis erfolgt ist, können Sie das Paket über die zugehörige API aufrufen.</span><span class="sxs-lookup"><span data-stu-id="9d5aa-111">Once the reference is made, you can call the package through its API.</span></span>

> [!Tip]
> <span data-ttu-id="9d5aa-112">**Einstieg in nuget.org**: .NET-Entwickler finden Komponenten für die Verwendung in ihren eigenen Anwendungen üblicherweise durch das Durchsuchen von nuget.org.</span><span class="sxs-lookup"><span data-stu-id="9d5aa-112">**Start with nuget.org**: Browsing nuget.org is how .NET developers typically find components they can reuse in their own applications.</span></span> <span data-ttu-id="9d5aa-113">Sie können nuget.org direkt durchsuchen oder in Visual Studio nach Paketen suchen und diese installieren, wie in diesem Artikel dargestellt wird.</span><span class="sxs-lookup"><span data-stu-id="9d5aa-113">You can search nuget.org directly or find and install packages within Visual Studio as shown in this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="9d5aa-114">Erforderliche Komponenten</span><span class="sxs-lookup"><span data-stu-id="9d5aa-114">Prerequisites</span></span>

- <span data-ttu-id="9d5aa-115">Visual Studio 2017 mit der Entwicklungsworkload für die Universelle Windows-Plattform, oder</span><span class="sxs-lookup"><span data-stu-id="9d5aa-115">Visual Studio 2017 with the Universal Windows Platform development workload, or</span></span>
- <span data-ttu-id="9d5aa-116">Visual Studio 2015 Update 3 mit Tools für universelle Windows-Apps.</span><span class="sxs-lookup"><span data-stu-id="9d5aa-116">Visual Studio 2015 Update 3 with Tools for Universal Windows Apps.</span></span>

<span data-ttu-id="9d5aa-117">Sie können die 2017 Community Edition kostenlos über [visualstudio.com](https://www.visualstudio.com/) installieren oder die Professional bzw. Enterprise Edition verwenden.</span><span class="sxs-lookup"><span data-stu-id="9d5aa-117">You can install the 2017 Community edition for free from [visualstudio.com](https://www.visualstudio.com/) or use the Professional or Enterprise editions.</span></span>

## <a name="create-a-project"></a><span data-ttu-id="9d5aa-118">Erstellen eines Projekts</span><span class="sxs-lookup"><span data-stu-id="9d5aa-118">Create a project</span></span>

<span data-ttu-id="9d5aa-119">NuGet-Pakete können in jedem beliebigen .NET-Projekt installiert werden, vorausgesetzt, das Paket unterstützt dasselbe Zielframework wie das Projekt.</span><span class="sxs-lookup"><span data-stu-id="9d5aa-119">NuGet packages can be installed into any .NET project, provided that the package supports the same target framework as the project.</span></span>

<span data-ttu-id="9d5aa-120">In dieser exemplarischen Vorgehensweise verwenden Sie eine einfach universelle Windows-App (UWP).</span><span class="sxs-lookup"><span data-stu-id="9d5aa-120">For this walkthrough, use a simple Universal Windows (UWP) app.</span></span> <span data-ttu-id="9d5aa-121">Erstellen Sie ein Projekt in Visual Studio, indem Sie auf **Datei > Neues Projekt...** klicken und **Windows Universal > Leere App (Universal Windows)** auswählen.</span><span class="sxs-lookup"><span data-stu-id="9d5aa-121">Create a project in Visual Studio using **File > New Project...** and selecting the **Windows Universal > Blank App (Universal Windows)**.</span></span> <span data-ttu-id="9d5aa-122">Übernehmen Sie die Standardwerte für „Zielversion“ und „Mindestens erforderliche Version“, wenn Sie dazu aufgefordert werden.</span><span class="sxs-lookup"><span data-stu-id="9d5aa-122">Accept the default values for Target Version and Minimum Version when prompted.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="9d5aa-123">Hinzufügen des NuGet-Pakets „Newtonsoft.Json“</span><span class="sxs-lookup"><span data-stu-id="9d5aa-123">Add the Newtonsoft.Json NuGet package</span></span>

<span data-ttu-id="9d5aa-124">Sie können entweder die Benutzeroberfläche oder die Konsole von Paket-Manager verwenden, um das Paket zu installieren.</span><span class="sxs-lookup"><span data-stu-id="9d5aa-124">To install the package, you can use either the Package Manager UI or the Package Manager Console.</span></span> <span data-ttu-id="9d5aa-125">Beim Installieren eines Pakets zeichnet NuGet die Abhängigkeit entweder in Ihrer Projektdatei oder in einer `packages.config`-Datei auf.</span><span class="sxs-lookup"><span data-stu-id="9d5aa-125">When you install a package, NuGet records the dependency in either your project file or a `packages.config` file.</span></span> <span data-ttu-id="9d5aa-126">Weitere Informationen finden Sie unter [Übersicht und Workflow für die Paketerstellung](../consume-packages/Overview-and-Workflow.md).</span><span class="sxs-lookup"><span data-stu-id="9d5aa-126">For more information, see [Package consumption overview and workflow](../consume-packages/Overview-and-Workflow.md).</span></span>

### <a name="package-manager-ui"></a><span data-ttu-id="9d5aa-127">Benutzeroberfläche des Paket-Managers</span><span class="sxs-lookup"><span data-stu-id="9d5aa-127">Package Manager UI</span></span>

1. <span data-ttu-id="9d5aa-128">Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf **Verweise**, und wählen Sie **NuGet-Pakete verwalten** aus.</span><span class="sxs-lookup"><span data-stu-id="9d5aa-128">In Solution Explorer, right-click **References** and choose **Manage NuGet Packages**.</span></span>

    ![Verwalten des Befehls für NuGet-Pakete bei Projektverweisen](media/QS_Use-02-ManageNuGetPackages.png)

1. <span data-ttu-id="9d5aa-130">Wählen Sie als **Paketquelle** nuget.org aus. Wählen Sie anschließend die Registerkarte **Durchsuchen** aus, suchen Sie nach dem Paket **Newtonsoft.Json**, und wählen Sie das Paket in der Liste sowie anschließend **Installieren** aus:</span><span class="sxs-lookup"><span data-stu-id="9d5aa-130">Choose "nuget.org" as the **Package source**, select the **Browse** tab, search for **Newtonsoft.Json**, select that package in the list, and select **Install**:</span></span>

    ![Suchen des Pakets „Newtonsoft.Json“](media/QS_Use-03-NewtonsoftJson.png)

1. <span data-ttu-id="9d5aa-132">Akzeptieren Sie die Lizenzbedingungen.</span><span class="sxs-lookup"><span data-stu-id="9d5aa-132">Accept any license prompts.</span></span>

1. <span data-ttu-id="9d5aa-133">(Visual Studio 2017) Wenn Sie dazu aufgefordert werden, ein Format für die Paketverwaltung auszuwählen, wählen Sie **PackageReference in Projektdatei**:</span><span class="sxs-lookup"><span data-stu-id="9d5aa-133">(Visual Studio 2017) If prompted to select a package management format, select **PackageReference in project file**:</span></span>

    ![Auswahl eines Paketverwaltungsformats](media/QS_Use-03b-SelectFormat.png)

1. <span data-ttu-id="9d5aa-135">Wählen Sie **OK** aus, wenn Sie dazu aufgefordert werden, Änderungen zu überprüfen.</span><span class="sxs-lookup"><span data-stu-id="9d5aa-135">If prompted to review changes, select **OK**.</span></span>

### <a name="package-manager-console"></a><span data-ttu-id="9d5aa-136">Paket-Manager-Konsole</span><span class="sxs-lookup"><span data-stu-id="9d5aa-136">Package Manager Console</span></span>

1. <span data-ttu-id="9d5aa-137">Wählen Sie den Menübefehl **Tools > NuGet-Paket-Manager > Paket-Manager-Konsole** aus.</span><span class="sxs-lookup"><span data-stu-id="9d5aa-137">Select the **Tools > NuGet Package Manager > Package Manager Console** menu command.</span></span>

1. <span data-ttu-id="9d5aa-138">Wenn die Konsole geöffnet wird, überprüfen Sie, ob die Dropdownliste **Standardprojekt** das Projekt anzeigt, in das Sie das Paket installieren möchten.</span><span class="sxs-lookup"><span data-stu-id="9d5aa-138">Once the console opens, check that the **Default project** drop-down list shows the project into which you want to install the package.</span></span> <span data-ttu-id="9d5aa-139">Wenn Sie ein einzelnes Projekt in der Projektmappe haben, ist es bereits ausgewählt.</span><span class="sxs-lookup"><span data-stu-id="9d5aa-139">If you have a single project in the solution, it is already selected.</span></span>

    ![Suchen des Pakets „Newtonsoft.Json“](media/QS_Use-08-Console1.png)

1. <span data-ttu-id="9d5aa-141">Geben Sie den Befehl `Install-Package Newtonsoft.json` ein (siehe [Install-Package](../tools/ps-ref-install-package.md)).</span><span class="sxs-lookup"><span data-stu-id="9d5aa-141">Enter the command `Install-Package Newtonsoft.json` (see [Install-Package](../tools/ps-ref-install-package.md)).</span></span> <span data-ttu-id="9d5aa-142">Das Konsolenfenster zeigt die Ausgabe des Befehls.</span><span class="sxs-lookup"><span data-stu-id="9d5aa-142">The console window shows output for the command.</span></span> <span data-ttu-id="9d5aa-143">Fehler deuten normalerweise darauf hin, dass das Paket nicht mit dem Zielframework des Projekts kompatibel ist.</span><span class="sxs-lookup"><span data-stu-id="9d5aa-143">Errors typically indicate that the package isn't compatible with the project's target framework.</span></span>

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="9d5aa-144">Verwenden der API „Newtonsoft.Json“ in der App</span><span class="sxs-lookup"><span data-stu-id="9d5aa-144">Use the Newtonsoft.Json API in the app</span></span>

<span data-ttu-id="9d5aa-145">Wenn das Paket „Newtonsoft.Json“ im Projekt enthalten ist, können Sie die zugehörige `JsonConvert.SerializeObject`-Methode aufrufen, um ein Objekt in eine lesbare Zeichenfolge zu konvertieren.</span><span class="sxs-lookup"><span data-stu-id="9d5aa-145">With the Newtonsoft.Json package in the project, you can call its `JsonConvert.SerializeObject` method to convert an object to a human-readable string.</span></span>

1. <span data-ttu-id="9d5aa-146">Öffnen Sie `MainPage.xaml`, und ersetzen Sie das vorhandene `Grid`-Element mit folgendem:</span><span class="sxs-lookup"><span data-stu-id="9d5aa-146">Open `MainPage.xaml` and replace the existing `Grid` element with the following:</span></span>

    ```xaml
    <Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. <span data-ttu-id="9d5aa-147">Öffnen Sie die Datei `MainPage.xaml.cs` (befindet sich in Projektmappen-Explorer unter dem Knoten `MainPage.xaml`), und fügen Sie den folgenden Code im Konstruktor `MainPage` ein:</span><span class="sxs-lookup"><span data-stu-id="9d5aa-147">Open the `MainPage.xaml.cs` file (located in Solution Explorer under the `MainPage.xaml` node), and insert the following code inside the `MainPage` constructor:</span></span>

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

1. <span data-ttu-id="9d5aa-148">Obwohl Sie das Paket „Newtonsoft.Json“ zum Projekt hinzugefügt haben, erscheinen unter `JsonConvert` rote Wellenlinien, da eine `using`-Anweisung am Anfang der Codedatei erforderlich ist:</span><span class="sxs-lookup"><span data-stu-id="9d5aa-148">Even though you added the Newtonsoft.Json package to the project, red squiggles appears under `JsonConvert` because you need a `using` statement at the top of the code file:</span></span>

    ```cs
    using Newtonsoft.json;
    ```

1. <span data-ttu-id="9d5aa-149">Erstellen Sie die App, und führen Sie sie aus, indem Sie F5 drücken oder **Debuggen > Debuggen starten** auswählen:</span><span class="sxs-lookup"><span data-stu-id="9d5aa-149">Build and run the app by pressing F5 or selecting **Debug > Start Debugging**:</span></span>

    ![Ursprüngliche Ausgabe der UWP-App](media/QS_Use-06-AppStart.png)

1. <span data-ttu-id="9d5aa-151">Klicken Sie auf die Schaltfläche, um die Inhalte des Elements „TextBlock“ anzuzeigen, das durch JSON-Text ersetzt wurde:</span><span class="sxs-lookup"><span data-stu-id="9d5aa-151">Select on the button to see the contents of the TextBlock replaced with some JSON text:</span></span>

    ![Ausgabe der UWP-App nach Klicken auf die Schaltfläche](media/QS_Use-07-AppEnd.png)

## <a name="related-articles"></a><span data-ttu-id="9d5aa-153">Verwandte Artikel</span><span class="sxs-lookup"><span data-stu-id="9d5aa-153">Related articles</span></span>

- [<span data-ttu-id="9d5aa-154">Übersicht über den Paketverbrauch und dessen Workflows</span><span class="sxs-lookup"><span data-stu-id="9d5aa-154">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="9d5aa-155">Suchen und Auswählen von Paketen</span><span class="sxs-lookup"><span data-stu-id="9d5aa-155">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="9d5aa-156">So können Sie ein Paket erstellen</span><span class="sxs-lookup"><span data-stu-id="9d5aa-156">Ways to install a package</span></span>](../consume-packages/ways-to-install-a-package.md)
- [<span data-ttu-id="9d5aa-157">Konfigurieren von NuGet-Verhalten</span><span class="sxs-lookup"><span data-stu-id="9d5aa-157">Configuring NuGet Behavior</span></span>](../consume-packages/configuring-nuget-behavior.md)
