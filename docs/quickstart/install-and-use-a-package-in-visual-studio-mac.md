---
title: Installieren und Verwenden eines NuGet-Pakets in Visual Studio für Mac
description: Ein Tutorial mit einer exemplarischen Vorgehensweise bei der Installation und Verwendung eines NuGet-Pakets in einem Visual Studio für Mac-Projekt.
author: jmatthiesen
ms.author: jomatthi
ms.date: 08/14/2019
ms.topic: quickstart
ms.openlocfilehash: 6f3fd4f2ffec0037a48aec845fddee258b5c1e7f
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/07/2020
ms.locfileid: "70238476"
---
# <a name="quickstart-install-and-use-a-package-in-visual-studio-for-mac"></a><span data-ttu-id="f9151-103">Schnellstart: Installieren und Verwenden eines Pakets in Visual Studio für Mac</span><span class="sxs-lookup"><span data-stu-id="f9151-103">Quickstart: Install and use a package in Visual Studio for Mac</span></span>

<span data-ttu-id="f9151-104">NuGet-Pakete enthalten wiederverwendbaren Code, der von anderen Entwicklern für die Verwendung in Ihren Projekten verfügbar gemacht wird.</span><span class="sxs-lookup"><span data-stu-id="f9151-104">NuGet packages contain reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="f9151-105">Unter [Was ist NuGet?](../What-is-NuGet.md) finden Sie weitere Informationen.</span><span class="sxs-lookup"><span data-stu-id="f9151-105">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span> <span data-ttu-id="f9151-106">Pakete werden über den NuGet-Paket-Manager in einem Visual Studio für Mac-Projekt installiert.</span><span class="sxs-lookup"><span data-stu-id="f9151-106">Packages are installed into a Visual Studio for Mac project using the NuGet Package Manager.</span></span> <span data-ttu-id="f9151-107">Dieser Artikel zeigt den Prozess mit dem beliebten [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/)-Paket und einem .NET Core-Konsolenprojekt.</span><span class="sxs-lookup"><span data-stu-id="f9151-107">This article demonstrates the process using the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package and a .NET Core console project.</span></span> <span data-ttu-id="f9151-108">Derselbe Prozess ist auch auf jedes andere Xamarin- oder .NET Core-Projekt anwendbar.</span><span class="sxs-lookup"><span data-stu-id="f9151-108">The same process applies to any other Xamarin or .NET Core project.</span></span>

<span data-ttu-id="f9151-109">Beziehen Sie sich nach der Installation mit `using <namespace>` auf das Paket im Code, wobei \<Namespace\> für das von Ihnen verwendete Paket spezifisch ist.</span><span class="sxs-lookup"><span data-stu-id="f9151-109">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="f9151-110">Nachdem der Verweis erfolgt ist, können Sie das Paket über die zugehörige API aufrufen.</span><span class="sxs-lookup"><span data-stu-id="f9151-110">Once the reference is made, you can call the package through its API.</span></span>

> [!Tip]
> <span data-ttu-id="f9151-111">**Einstieg in nuget.org**: .NET-Entwickler finden Komponenten für die Verwendung in ihren eigenen Anwendungen üblicherweise durch das Durchsuchen von *nuget.org*.</span><span class="sxs-lookup"><span data-stu-id="f9151-111">**Start with nuget.org**: Browsing *nuget.org* is how .NET developers typically find components they can reuse in their own applications.</span></span> <span data-ttu-id="f9151-112">Sie können *nuget.org* direkt durchsuchen oder in Visual Studio nach Paketen suchen und diese installieren, wie in diesem Artikel dargestellt wird.</span><span class="sxs-lookup"><span data-stu-id="f9151-112">You can search *nuget.org* directly or find and install packages within Visual Studio as shown in this article.</span></span> <span data-ttu-id="f9151-113">Allgemeine Informationen finden Sie [Suchen und Auswerten von NuGet-Paketen](../consume-packages/finding-and-choosing-packages.md).</span><span class="sxs-lookup"><span data-stu-id="f9151-113">For general information, see [Find and evaluate NuGet packages](../consume-packages/finding-and-choosing-packages.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="f9151-114">Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="f9151-114">Prerequisites</span></span>

- <span data-ttu-id="f9151-115">Visual Studio 2019 für Mac.</span><span class="sxs-lookup"><span data-stu-id="f9151-115">Visual Studio 2019 for Mac.</span></span>

<span data-ttu-id="f9151-116">Sie können die 2019 Community-Edition kostenlos von [visualstudio.com](https://www.visualstudio.com/) installieren oder die Professional oder Enterprise Edition verwenden.</span><span class="sxs-lookup"><span data-stu-id="f9151-116">You can install the 2019 Community edition for free from [visualstudio.com](https://www.visualstudio.com/) or use the Professional or Enterprise editions.</span></span>

<span data-ttu-id="f9151-117">Wenn Sie Visual Studio unter Windows verwenden, lesen Sie [Installieren und Verwenden eines Pakets in Visual Studio (nur Windows)](install-and-use-a-package-in-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="f9151-117">If you're using Visual Studio on Windows, see [Install and use a package in Visual Studio (Windows Only)](install-and-use-a-package-in-visual-studio.md).</span></span>

## <a name="create-a-project"></a><span data-ttu-id="f9151-118">Erstellen eines Projekts</span><span class="sxs-lookup"><span data-stu-id="f9151-118">Create a project</span></span>

<span data-ttu-id="f9151-119">NuGet-Pakete können in jedem beliebigen .NET-Projekt installiert werden, vorausgesetzt, das Paket unterstützt dasselbe Zielframework wie das Projekt.</span><span class="sxs-lookup"><span data-stu-id="f9151-119">NuGet packages can be installed into any .NET project, provided that the package supports the same target framework as the project.</span></span>

<span data-ttu-id="f9151-120">Verwenden Sie für diese exemplarische Vorgehensweise eine einfache .NET Core-Konsolen-App.</span><span class="sxs-lookup"><span data-stu-id="f9151-120">For this walkthrough, use a simple .NET Core Console app.</span></span> <span data-ttu-id="f9151-121">Erstellen Sie ein Projekt in Visual Studio für Mac mit **Datei > Neue Projektmappe**, und wählen Sie die Vorlage **.NET Core > App > Konsolenanwendung** aus.</span><span class="sxs-lookup"><span data-stu-id="f9151-121">Create a project in Visual Studio for Mac using **File > New Solution...**, select the **.NET Core > App > Console Application** template.</span></span> <span data-ttu-id="f9151-122">Klicken Sie auf **Weiter**.</span><span class="sxs-lookup"><span data-stu-id="f9151-122">Click **Next**.</span></span> <span data-ttu-id="f9151-123">Akzeptieren Sie die Standardwerte für **Zielframework**, wenn Sie dazu aufgefordert werden.</span><span class="sxs-lookup"><span data-stu-id="f9151-123">Accept the default values for **Target Framework** when prompted.</span></span>

<span data-ttu-id="f9151-124">Visual Studio erstellt das Projekt, das im Projektmappen-Explorer geöffnet wird.</span><span class="sxs-lookup"><span data-stu-id="f9151-124">Visual Studio creates the project, which opens in Solution Explorer.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="f9151-125">Hinzufügen des NuGet-Pakets „Newtonsoft.Json“</span><span class="sxs-lookup"><span data-stu-id="f9151-125">Add the Newtonsoft.Json NuGet package</span></span>

<span data-ttu-id="f9151-126">Verwenden Sie zum Installieren des Pakets den NuGet-Paket-Manager.</span><span class="sxs-lookup"><span data-stu-id="f9151-126">To install the package, you use the NuGet Package Manager.</span></span> <span data-ttu-id="f9151-127">Beim Installieren eines Pakets zeichnet NuGet die Abhängigkeit entweder in Ihrer Projektdatei oder in einer `packages.config`-Datei auf (je nach Projektformat).</span><span class="sxs-lookup"><span data-stu-id="f9151-127">When you install a package, NuGet records the dependency in  either your project file or a `packages.config` file (depending on the project format).</span></span> <span data-ttu-id="f9151-128">Weitere Informationen finden Sie unter [Übersicht und Workflow für die Paketerstellung](../consume-packages/Overview-and-Workflow.md).</span><span class="sxs-lookup"><span data-stu-id="f9151-128">For more information, see [Package consumption overview and workflow](../consume-packages/Overview-and-Workflow.md).</span></span>

### <a name="nuget-package-manager"></a><span data-ttu-id="f9151-129">NuGet-Paket-Manager</span><span class="sxs-lookup"><span data-stu-id="f9151-129">NuGet Package Manager</span></span>

1. <span data-ttu-id="f9151-130">Klicken Sie im Projektmappen-Explorer mit der rechten Maustaste auf **Abhängigkeiten**, und wählen Sie **Pakete hinzufügen** aus.</span><span class="sxs-lookup"><span data-stu-id="f9151-130">In Solution Explorer, right-click **Dependencies** and choose **Add Packages...**.</span></span>

    ![Verwalten des Befehls für NuGet-Pakete bei Projektverweisen](media/QS_Use_Mac-02-ManageNuGetPackages.png)

1. <span data-ttu-id="f9151-132">Wählen Sie „nuget.org“ in der linken oberen Ecke des Dialogfelds als **Paketquelle** aus, suchen Sie nach **Newtonsoft.Json**, und wählen Sie das Paket in der Liste und dann **Pakete hinzufügen** aus:</span><span class="sxs-lookup"><span data-stu-id="f9151-132">Choose "nuget.org" as the **Package source** in the top left corner of the dialog, and search for **Newtonsoft.Json**, select that package in the list, and select **Add Packages...**:</span></span>

    ![Suchen des Pakets „Newtonsoft.Json“](media/QS_Use_Mac-03-NewtonsoftJson.png)

    <span data-ttu-id="f9151-134">Weitere Informationen zum NuGet-Paket-Manager finden Sie unter [Installieren und Verwalten von Paketen mithilfe von Visual Studio für Mac](../consume-packages/install-use-packages-visual-studio.md).</span><span class="sxs-lookup"><span data-stu-id="f9151-134">If you want more information on the NuGet Package Manager, see [Install and manage packages using Visual Studio for Mac](../consume-packages/install-use-packages-visual-studio.md).</span></span>

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="f9151-135">Verwenden der API „Newtonsoft.Json“ in der App</span><span class="sxs-lookup"><span data-stu-id="f9151-135">Use the Newtonsoft.Json API in the app</span></span>

<span data-ttu-id="f9151-136">Wenn das Paket „Newtonsoft.Json“ im Projekt enthalten ist, können Sie die zugehörige `JsonConvert.SerializeObject`-Methode aufrufen, um ein Objekt in eine lesbare Zeichenfolge zu konvertieren.</span><span class="sxs-lookup"><span data-stu-id="f9151-136">With the Newtonsoft.Json package in the project, you can call its `JsonConvert.SerializeObject` method to convert an object to a human-readable string.</span></span>

1. <span data-ttu-id="f9151-137">Öffnen Sie die `Program.cs`-Datei (befindet sich im Lösungspad), und ersetzen Sie den Inhalt der Datei durch den folgenden Code:</span><span class="sxs-lookup"><span data-stu-id="f9151-137">Open the `Program.cs` file (located in the Solution Pad) and replace the file contents with the following code:</span></span>

    ```cs
    using System;
    using Newtonsoft.Json;

    namespace NuGetDemo
    {
        public class Account
        {
            public string Name { get; set; }
            public string Email { get; set; }
            public DateTime DOB { get; set; }
        }
    
        class Program
        {
            static void Main(string[] args)
            {
                Account account = new Account()
                {
                    Name = "Joe Doe",
                    Email = "joe@test.com",
                    DOB = new DateTime(1976, 3, 24)
                };
                string json = JsonConvert.SerializeObject(account);
                Console.WriteLine(json);
            }
        }
    }
    ```

1. <span data-ttu-id="f9151-138">Erstellen Sie die App, und führen Sie sie mit Auswahl von **Ausführen > Debugging starten** aus:</span><span class="sxs-lookup"><span data-stu-id="f9151-138">Build and run the app by selecting **Run > Start Debugging**:</span></span>

1. <span data-ttu-id="f9151-139">Sobald die App ausgeführt wird, wird die serialisierte JSON-Ausgabe in der Konsole angezeigt:</span><span class="sxs-lookup"><span data-stu-id="f9151-139">Once the app runs, you'll see the serialized JSON output appear in the console:</span></span>

  ![Ausgabe der Konsolen-App](media/QS_Use_Mac-06-AppStart.png)

## <a name="next-steps"></a><span data-ttu-id="f9151-141">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="f9151-141">Next steps</span></span>
<span data-ttu-id="f9151-142">Herzlichen Glückwunsch zur Installation und Verwendung Ihres ersten NuGet-Pakets!</span><span class="sxs-lookup"><span data-stu-id="f9151-142">Congratulations on installing and using your first NuGet package!</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="f9151-143">Installieren und Verwalten von Paketen mit Visual Studio für Mac</span><span class="sxs-lookup"><span data-stu-id="f9151-143">Install and manage packages using Visual Studio for Mac</span></span>](/visualstudio/mac/nuget-walkthrough?toc=/nuget/toc.json)

<span data-ttu-id="f9151-144">Klicken Sie für weitere Informationen zu den Features von NuGet auf folgende Links.</span><span class="sxs-lookup"><span data-stu-id="f9151-144">To explore more that NuGet has to offer, select the links below.</span></span>

- [<span data-ttu-id="f9151-145">Übersicht über den Paketverbrauch und dessen Workflows</span><span class="sxs-lookup"><span data-stu-id="f9151-145">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="f9151-146">Paketverweise in Projektdateien</span><span class="sxs-lookup"><span data-stu-id="f9151-146">Package references in project files</span></span>](../consume-packages/package-references-in-project-files.md)
