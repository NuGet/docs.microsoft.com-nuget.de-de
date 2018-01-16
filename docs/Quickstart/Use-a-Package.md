---
title: "Einführender Leitfaden zur Verwendung von NuGet-Paketen | Microsoft-Dokumentation"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/04/2017
ms.topic: get-started-article
ms.prod: nuget
ms.technology: 
ms.assetid: f31f8259-20a8-4617-880e-5819299372d2
description: Ein Tutorial mit einer exemplarischen Vorgehensweise bei der Installation und Verwendung eines NuGet-Pakets in einem Projekt.
keywords: NuGet installieren, NuGet-Paketverbrauch, Installieren von NuGet-Paketen, NuGet-Paketverweise, Verwenden von NuGet-Paketen
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 639f4883f5ce904a44d8aa23d76c93ed79ea4b9d
ms.sourcegitcommit: bdcd2046b1b187d8b59716b9571142c02181c8fb
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/10/2018
---
# <a name="install-and-use-a-package"></a><span data-ttu-id="feff1-104">Installieren und Verwenden eines Pakets</span><span class="sxs-lookup"><span data-stu-id="feff1-104">Install and use a package</span></span>

<span data-ttu-id="feff1-105">NuGet-Pakete sind die Einheiten wiederverwendbaren Codes, die andere Entwickler Ihnen für die Verwendung in Ihren Projekten verfügbar machen.</span><span class="sxs-lookup"><span data-stu-id="feff1-105">NuGet packages are units of reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="feff1-106">Unter [Was ist NuGet?](../What-is-NuGet.md) finden Sie weitere Informationen.</span><span class="sxs-lookup"><span data-stu-id="feff1-106">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span>

[!INCLUDE [install-methods](../includes/install-methods.md)]

<span data-ttu-id="feff1-107">Beziehen Sie sich nach der Installation mit `using <namespace>` auf das Paket im Code, wobei \<Namespace\> für das von Ihnen verwendete Paket spezifisch ist.</span><span class="sxs-lookup"><span data-stu-id="feff1-107">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="feff1-108">Nachdem der Verweis erfolgt ist, können Sie das Paket über die zugehörige API aufrufen.</span><span class="sxs-lookup"><span data-stu-id="feff1-108">Once the reference is made, you can call the package through its API.</span></span>

<span data-ttu-id="feff1-109">Des Weiteren wird in diesem Abschnitt die Verwendung der Benutzeroberfläche des Paket-Managers für die Installation des beliebten Pakets [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) in einem UWP-Projekt (Universelle Windows-Plattform) erläutert.</span><span class="sxs-lookup"><span data-stu-id="feff1-109">The remainder of this topic walks through the process of using the Package Manager UI to install the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package in a Universal Windows Platform (UWP) project.</span></span> <span data-ttu-id="feff1-110">Anschließend wird ein Beispiel für die Verwendung des Pakets dargestellt.</span><span class="sxs-lookup"><span data-stu-id="feff1-110">It then shows an example of using the package.</span></span> <span data-ttu-id="feff1-111">Sie verwenden für praktisch jedes NuGet-Paket, das in einem Projekt verwendet wird, einen ähnlichen bzw. den gleichen Workflow.</span><span class="sxs-lookup"><span data-stu-id="feff1-111">You use a similar same workflow for virtually every NuGet package you use in a project.</span></span>

- [<span data-ttu-id="feff1-112">Installieren von Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="feff1-112">Install pre-requisites</span></span>](#install-pre-requisites)
- [<span data-ttu-id="feff1-113">Erstellen eines Projekts</span><span class="sxs-lookup"><span data-stu-id="feff1-113">Create a project</span></span>](#create-a-project)
- [<span data-ttu-id="feff1-114">Hinzufügen des NuGet-Pakets „Newtonsoft.Json“</span><span class="sxs-lookup"><span data-stu-id="feff1-114">Add the Newtonsoft.Json NuGet package</span></span>](#add-the-newtonsoftjson-nuget-package)
- [<span data-ttu-id="feff1-115">Verwenden der API „Newtonsoft.Json“ in der App</span><span class="sxs-lookup"><span data-stu-id="feff1-115">Use the Newtonsoft.Json API in the app</span></span>](#use-the-newtonsoftjson-api-in-the-app)

> [!Tip]
> <span data-ttu-id="feff1-116">**Beginnen Sie mit nuget.org**: Das Installieren von Paketen über nuget.org ist ein gängiger Workflow, den .NET-Entwickler für die Suche nach Komponenten verwenden, die sie in ihren eigenen Apps wiederverwenden können.</span><span class="sxs-lookup"><span data-stu-id="feff1-116">**Start with nuget.org**: Installing packages from nuget.org is a common workflow that .NET developers use to find components they can reuse in their own applications.</span></span> <span data-ttu-id="feff1-117">Sie können nuget.org immer direkt durchsuchen oder in Visual Studio nach Paketen suchen und diese installieren, wie in diesem Abschnitt dargestellt wird.</span><span class="sxs-lookup"><span data-stu-id="feff1-117">You can always search nuget.org directly or find and install packages within Visual Studio as shown in this topic.</span></span>

## <a name="install-pre-requisites"></a><span data-ttu-id="feff1-118">Installieren von Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="feff1-118">Install pre-requisites</span></span>

<span data-ttu-id="feff1-119">Für dieses Tutorial ist Visual Studio 2015, Update 3 mit Tools für universelle Windows-Apps oder Visual Studio 2017 mit der Entwicklungsworkload für die universelle Windows-Plattform erforderlich.</span><span class="sxs-lookup"><span data-stu-id="feff1-119">This tutorial requires Visual Studio 2015 Update 3 with Tools for Universal Windows Apps, or Visual Studio 2017 with the Universal Windows Platform development workload.</span></span> <span data-ttu-id="feff1-120">Wenn Sie Visual Studio bereits installiert haben, können Sie das Installationsprogramm erneut ausführen, um die UWP-Tools hinzuzufügen.</span><span class="sxs-lookup"><span data-stu-id="feff1-120">If you already have Visual Studio installed, you can run the installer again to add the UWP tools.</span></span>

<span data-ttu-id="feff1-121">Sie können die Community Edition kostenlos über [visualstudio.com](https://www.visualstudio.com/) installieren oder die Professional bzw. Enterprise Edition verwenden.</span><span class="sxs-lookup"><span data-stu-id="feff1-121">You can install the Community edition for free from [visualstudio.com](https://www.visualstudio.com/) or use the Professional or Enterprise editions.</span></span> 

## <a name="create-a-project"></a><span data-ttu-id="feff1-122">Erstellen eines Projekts</span><span class="sxs-lookup"><span data-stu-id="feff1-122">Create a project</span></span>

<span data-ttu-id="feff1-123">Sie benötigen für die Installation eines NuGet-Pakets ein .NET-basiertes Projekt in Visual Studio.</span><span class="sxs-lookup"><span data-stu-id="feff1-123">To install a NuGet package, you need some kind of .NET-based project in Visual Studio.</span></span> <span data-ttu-id="feff1-124">In dieser exemplarischen Vorgehensweise können Sie eine einfache WPF- oder UWP-App verwenden (WPF = Windows Presentation Foundation, UWP = universelle Windows-Plattform):</span><span class="sxs-lookup"><span data-stu-id="feff1-124">For this walkthrough, you can use use a simple Windows Presentation Foundation (WPF) or Universal Windows (UWP) app:</span></span>

- <span data-ttu-id="feff1-125">Wählen Sie bei WPF (Windows 7 und höher) die Option **Datei > Neu > Projekt** aus, erweitern Sie **Visual C#**, und wählen Sie anschließend **Klassischer Windows-Desktop > WPF-App (.NET Framework)** und **OK** aus.</span><span class="sxs-lookup"><span data-stu-id="feff1-125">For WPF (Windows 7+), choose **File > New > Project**, expand **Visual C#**, select **Windows Classic Desktop > WPF App (.NET Framework)**, and select **OK**.</span></span>
- <span data-ttu-id="feff1-126">Verwenden Sie bei UWP (Windows 10) stattdessen die Option **Windows Universal > Leere App (Universal Windows)**.</span><span class="sxs-lookup"><span data-stu-id="feff1-126">For UWP (Windows 10), use the **Windows Universal > Blank App (Universal Windows)** instead.</span></span> <span data-ttu-id="feff1-127">Übernehmen Sie die Standardwerte für „Zielversion“ und „Mindestens erforderliche Version“, wenn Sie dazu aufgefordert werden.</span><span class="sxs-lookup"><span data-stu-id="feff1-127">Accept the default values for Target Version and Minimum Version when prompted.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="feff1-128">Hinzufügen des NuGet-Pakets „Newtonsoft.Json“</span><span class="sxs-lookup"><span data-stu-id="feff1-128">Add the Newtonsoft.Json NuGet package</span></span>

1. <span data-ttu-id="feff1-129">Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf **Verweise**, und wählen Sie **NuGet-Pakete verwalten** aus.</span><span class="sxs-lookup"><span data-stu-id="feff1-129">In Solution Explorer, right-click **References** and choose **Manage NuGet Packages**.</span></span>

    ![Verwalten des Befehls für NuGet-Pakete bei Projektverweisen](media/QS_Use-02-ManageNuGetPackages.png)

1. <span data-ttu-id="feff1-131">Wählen Sie als **Paketquelle** nuget.org aus. Wählen Sie anschließend die Registerkarte **Durchsuchen** aus, suchen Sie nach dem Paket **Newtonsoft.Json**, und wählen Sie das Paket in der Liste sowie anschließend **Installieren** aus:</span><span class="sxs-lookup"><span data-stu-id="feff1-131">Choose "nuget.org" as the **Package source**, select the **Browse** tab, search for **Newtonsoft.Json**, select that package in the list, and select **Install**:</span></span>

    ![Suchen des Pakets „Newtonsoft.Json“](media/QS_Use-03-NewtonsoftJson.png)

1. <span data-ttu-id="feff1-133">Wenn Sie dazu aufgefordert werden, ein Format für die Paketverwaltung auszuwählen, können Sie sich zwischen den Formaten „PackageReference“ (empfohlen) und `packages.config` entscheiden:</span><span class="sxs-lookup"><span data-stu-id="feff1-133">If prompted to select a package management format, choose between PackageReference (recommended) and `packages.config`:</span></span>

    ![Auswählen eines Formats für den Paketverweis](media/QS_Use-03b-SelectFormat.png)

1. <span data-ttu-id="feff1-135">Wählen Sie **OK** aus, wenn Sie dazu aufgefordert werden, Änderungen zu überprüfen.</span><span class="sxs-lookup"><span data-stu-id="feff1-135">If prompted to review changes, select **OK**.</span></span>

1. <span data-ttu-id="feff1-136">Klicken Sie mit der rechten Maustaste in den Projektmappen-Explorer, und wählen Sie **Projektmappe erstellen** aus.</span><span class="sxs-lookup"><span data-stu-id="feff1-136">Right-click the solution in Solution Explorer and select **Build Solution**.</span></span> <span data-ttu-id="feff1-137">Dadurch werden alle unter **Verweise** aufgeführten NuGet-Pakete wiederhergestellt.</span><span class="sxs-lookup"><span data-stu-id="feff1-137">This restores any NuGet packages listed under **References**.</span></span> <span data-ttu-id="feff1-138">Weitere Informationen finden Sie unter [Paketwiederherstellung](../consume-packages/package-restore.md).</span><span class="sxs-lookup"><span data-stu-id="feff1-138">For more details, see [Package Restore](../consume-packages/package-restore.md).</span></span>

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="feff1-139">Verwenden der API „Newtonsoft.Json“ in der App</span><span class="sxs-lookup"><span data-stu-id="feff1-139">Use the Newtonsoft.Json API in the app</span></span>

<span data-ttu-id="feff1-140">Wenn das Paket „Newtonsoft.Json“ im Projekt enthalten ist, können Sie die zugehörige `JsonConvert.SerializeObject`-Methode aufrufen, um ein Objekt in eine lesbare Zeichenfolge zu konvertieren.</span><span class="sxs-lookup"><span data-stu-id="feff1-140">With the Newtonsoft.Json package in the project, you can call its `JsonConvert.SerializeObject` method to convert an object to a human-readable string.</span></span>

1. <span data-ttu-id="feff1-141">Öffnen Sie `MainWindow.xaml` (WPF) oder `MainPage.xaml` (UWP), und ersetzen Sie das vorhandene `Grid`-Element wie folgt:</span><span class="sxs-lookup"><span data-stu-id="feff1-141">Open `MainWindow.xaml` (WPF) or `MainPage.xaml` (UWP) and replace the existing `Grid` element with the following:</span></span>

    ```xaml
    <Grid Background="{ThemeResource ApplicationPageBackgroundThemeBrush}">
        <StackPanel VerticalAlignment="Center">
            <Button Click="Button_Click" Content="Click Me" Margin="10"/>
            <TextBlock Name="TextBlock" Text="TextBlock" Margin="10"/>
        </StackPanel>
    </Grid>
    ```

1. <span data-ttu-id="feff1-142">Erweitern Sie im Projektmappen-Explorer den Knoten `MainWindow.xaml` (WPF) oder `MainPage.xaml` (UWP), öffnen Sie die Datei `.cs`, und fügen Sie den folgenden Code nach dem Konstruktor in die Klasse `MainWindow` oder `MainPage` ein:</span><span class="sxs-lookup"><span data-stu-id="feff1-142">Expand the `MainWindow.xaml` (WPF) or `MainPage.xaml` (UWP) node in Solution Explorer, open the `.cs` file, and insert the following code inside the `MainWindow` or `MainPage` class, after the constructor:</span></span>

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

1. <span data-ttu-id="feff1-143">Obwohl Sie das Paket „Newtonsoft.Json“ zum Projekt hinzugefügt haben, erscheinen unter `JsonConvert` rote Wellenlinien, da eine `using`-Anweisung erforderlich ist.</span><span class="sxs-lookup"><span data-stu-id="feff1-143">Even though you added the Newtonsoft.Json package to the project, red squiggles appears under `JsonConvert` because you need a `using` statement.</span></span> <span data-ttu-id="feff1-144">Wenn Sie mit dem Mauszeiger auf das unterstrichene `JsonConvert` zeigen, erscheint eine Glühbirne mit der Option **Mögliche Korrekturen anzeigen**:</span><span class="sxs-lookup"><span data-stu-id="feff1-144">Hover over the underlined `JsonConvert` and you'll see the Lightbulb and the option to **Show potential fixes**:</span></span>

    ![Glühbirne mit Befehl für die Anzeige möglicher Korrekturen](media/QS_Use-04-ShowPotentialFixes.png)


1. <span data-ttu-id="feff1-146">Klicken Sie auf **Mögliche Korrekturen anzeigen** (oder auf die Glühbirne), und wählen Sie die erste vorgeschlagene Korrektur aus: `using Newtonsoft.Json;`.</span><span class="sxs-lookup"><span data-stu-id="feff1-146">Click on **Show potential fixes** (or the Lightbulb) and select the first suggested fix, `using Newtonsoft.Json;`.</span></span> <span data-ttu-id="feff1-147">Dadurch wird die erforderliche Zeile am Dateianfang hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="feff1-147">This adds the necessary line to the top of the file.</span></span>

    ![Glühbirne mit Option zum Hinzufügen einer Using-Anweisung](media/QS_Use-05-AddUsing.png)

1. <span data-ttu-id="feff1-149">Entwickeln Sie die App, und führen Sie sie aus, indem Sie F5 drücken oder **Debuggen > Debugging starten** auswählen (in der Abbildung wird zwar UWP dargestellt, WPF ist jedoch ähnlich):</span><span class="sxs-lookup"><span data-stu-id="feff1-149">Build and run the app by pressing F5 or selecting **Debug > Start Debugging** (UWP shown here; WPF is similar):</span></span>

    ![Ursprüngliche Ausgabe der UWP-App](media/QS_Use-06-AppStart.png)

1. <span data-ttu-id="feff1-151">Klicken Sie auf die Schaltfläche, um die Inhalte des Elements „TextBlock“ anzuzeigen, das durch JSON-Text ersetzt wurde:</span><span class="sxs-lookup"><span data-stu-id="feff1-151">Select on the button to see the contents of the TextBlock replaced with some JSON text:</span></span>

    ![Ausgabe der UWP-App nach Klicken auf die Schaltfläche](media/QS_Use-07-AppEnd.png)

## <a name="related-topics"></a><span data-ttu-id="feff1-153">Verwandte Themen</span><span class="sxs-lookup"><span data-stu-id="feff1-153">Related topics</span></span>

- [<span data-ttu-id="feff1-154">Übersicht über den Paketverbrauch und dessen Workflows</span><span class="sxs-lookup"><span data-stu-id="feff1-154">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="feff1-155">Suchen und Auswählen von Paketen</span><span class="sxs-lookup"><span data-stu-id="feff1-155">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="feff1-156">Konfigurieren von NuGet-Verhalten</span><span class="sxs-lookup"><span data-stu-id="feff1-156">Configuring NuGet Behavior</span></span>](../consume-packages/configuring-nuget-behavior.md)
