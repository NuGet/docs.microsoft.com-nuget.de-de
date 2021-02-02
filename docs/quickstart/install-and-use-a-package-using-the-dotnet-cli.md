---
title: Installieren und Verwenden eines NuGet-Pakets mithilfe der dotnet-CLI
description: Ein Tutorial mit einer exemplarischen Vorgehensweise bei der Installation und Verwendung eines NuGet-Pakets in einem .NET Core-Projekt.
author: JonDouglas
ms.author: jodou
ms.date: 01/23/2018
ms.topic: quickstart
ms.openlocfilehash: adbf8f457d8520e3087e539b91ef932877aec3a0
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775443"
---
# <a name="quickstart-install-and-use-a-package-using-the-dotnet-cli"></a><span data-ttu-id="4e495-103">Schnellstart: Installieren und Verwenden eines Pakets mithilfe der .NET CLI</span><span class="sxs-lookup"><span data-stu-id="4e495-103">Quickstart: Install and use a package using the dotnet CLI</span></span>

<span data-ttu-id="4e495-104">NuGet-Pakete enthalten wiederverwendbaren Code, der von anderen Entwicklern für die Verwendung in Ihren Projekten verfügbar gemacht wird.</span><span class="sxs-lookup"><span data-stu-id="4e495-104">NuGet packages contain reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="4e495-105">Unter [Was ist NuGet?](../What-is-NuGet.md) finden Sie weitere Informationen.</span><span class="sxs-lookup"><span data-stu-id="4e495-105">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span> <span data-ttu-id="4e495-106">Pakete werden mithilfe des Befehls `dotnet add package` in einem .NET Core-Projekt installiert, wie in diesem Artikel für das beliebte [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/)-Paket beschrieben wird.</span><span class="sxs-lookup"><span data-stu-id="4e495-106">Packages are installed into a .NET Core project using the `dotnet add package` command as described in this article for the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package.</span></span>

<span data-ttu-id="4e495-107">Verweisen Sie nach der Installation mit `using <namespace>` auf das Paket im Code, wobei \<namespace\> speziell für das von Ihnen verwendete Paket gilt.</span><span class="sxs-lookup"><span data-stu-id="4e495-107">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="4e495-108">Sie können dann die Paket-API verwenden.</span><span class="sxs-lookup"><span data-stu-id="4e495-108">You can then use the package's API.</span></span>

> [!Tip]
> <span data-ttu-id="4e495-109">**Einstieg in nuget.org**: .NET-Entwickler finden Komponenten für die Verwendung in ihren eigenen Anwendungen üblicherweise durch das Durchsuchen von nuget.org.</span><span class="sxs-lookup"><span data-stu-id="4e495-109">**Start with nuget.org**: Browsing nuget.org is how .NET developers typically find components they can reuse in their own applications.</span></span> <span data-ttu-id="4e495-110">Sie können nuget.org direkt durchsuchen oder in Visual Studio nach Paketen suchen und diese installieren, wie in diesem Artikel dargestellt wird.</span><span class="sxs-lookup"><span data-stu-id="4e495-110">You can search nuget.org directly or find and install packages within Visual Studio as shown in this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="4e495-111">Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="4e495-111">Prerequisites</span></span>

- <span data-ttu-id="4e495-112">Das [.NET Core SDK](https://www.microsoft.com/net/download/), das das Befehlszeilentool `dotnet` bietet.</span><span class="sxs-lookup"><span data-stu-id="4e495-112">The [.NET Core SDK](https://www.microsoft.com/net/download/), which provides the `dotnet` command-line tool.</span></span> <span data-ttu-id="4e495-113">Ab Visual Studio 2017 wird die dotnet-CLI automatisch mit jeder .NET Core-bezogenen Workload installiert.</span><span class="sxs-lookup"><span data-stu-id="4e495-113">Starting in Visual Studio 2017, the dotnet CLI is automatically installed with any .NET Core related workloads.</span></span>

## <a name="create-a-project"></a><span data-ttu-id="4e495-114">Erstellen eines Projekts</span><span class="sxs-lookup"><span data-stu-id="4e495-114">Create a project</span></span>

<span data-ttu-id="4e495-115">NuGet-Pakete können in beliebigen .NET-Projekten installiert werden.</span><span class="sxs-lookup"><span data-stu-id="4e495-115">NuGet packages can be installed into a .NET project of some kind.</span></span> <span data-ttu-id="4e495-116">Erstellen Sie für diese exemplarische Vorgehensweise folgendermaßen ein einfaches .NET Core-Konsolenprojekt:</span><span class="sxs-lookup"><span data-stu-id="4e495-116">For this walkthrough, create a simple .NET Core console project as follows:</span></span>

1. <span data-ttu-id="4e495-117">Erstellen Sie einen Ordner für das Projekt.</span><span class="sxs-lookup"><span data-stu-id="4e495-117">Create a folder for the project.</span></span>

1. <span data-ttu-id="4e495-118">Öffnen Sie eine Eingabeaufforderung, und navigieren Sie zum neuen Ordner.</span><span class="sxs-lookup"><span data-stu-id="4e495-118">Open a command prompt and switch to the new folder.</span></span>

1. <span data-ttu-id="4e495-119">Erstellen Sie das Projekt mithilfe des folgenden Befehls:</span><span class="sxs-lookup"><span data-stu-id="4e495-119">Create the project using the following command:</span></span>

    ```dotnetcli
    dotnet new console
    ```

1. <span data-ttu-id="4e495-120">Verwenden Sie den Befehl `dotnet run`, um zu prüfen, ob die App ordnungsgemäß erstellt wurde.</span><span class="sxs-lookup"><span data-stu-id="4e495-120">Use `dotnet run` to test that the app has been created properly.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="4e495-121">Hinzufügen des NuGet-Pakets „Newtonsoft.Json“</span><span class="sxs-lookup"><span data-stu-id="4e495-121">Add the Newtonsoft.Json NuGet package</span></span>

1. <span data-ttu-id="4e495-122">Verwenden Sie folgenden Befehl, um das `Newtonsoft.json`-Paket zu installieren:</span><span class="sxs-lookup"><span data-stu-id="4e495-122">Use the following command to install the `Newtonsoft.json` package:</span></span>

    ```dotnetcli
    dotnet add package Newtonsoft.Json
    ```

2. <span data-ttu-id="4e495-123">Öffnen Sie die `.csproj`-Datei, um den hinzugefügten Verweis zu sehen, nachdem der Befehl abgeschlossen wurde:</span><span class="sxs-lookup"><span data-stu-id="4e495-123">After the command completes, open the `.csproj` file to see the added reference:</span></span>

    ```xml
   <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="12.0.1" />
   </ItemGroup>
    ```

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="4e495-124">Verwenden der API „Newtonsoft.Json“ in der App</span><span class="sxs-lookup"><span data-stu-id="4e495-124">Use the Newtonsoft.Json API in the app</span></span>

1. <span data-ttu-id="4e495-125">Öffnen Sie die Datei `Program.cs`, und fügen Sie die folgende Zeile am Anfang der Datei hinzu:</span><span class="sxs-lookup"><span data-stu-id="4e495-125">Open the `Program.cs` file and add the following line at the top of the file:</span></span>

    ```cs
    using Newtonsoft.Json;
    ```

1. <span data-ttu-id="4e495-126">Fügen Sie den folgenden Code vor der Zeile `class Program` hinzu:</span><span class="sxs-lookup"><span data-stu-id="4e495-126">Add the following code before the `class Program` line:</span></span>

    ```cs
    public class Account
    {
        public string Name { get; set; }
        public string Email { get; set; }
        public DateTime DOB { get; set; }
    }
    ```

1. <span data-ttu-id="4e495-127">Ersetzen Sie die `Main`-Funktion durch den folgendes:</span><span class="sxs-lookup"><span data-stu-id="4e495-127">Replace the `Main` function with the following:</span></span>

    ```cs
    static void Main(string[] args)
    {
        Account account = new Account
        {
            Name = "John Doe",
            Email = "john@nuget.org",
            DOB = new DateTime(1980, 2, 20, 0, 0, 0, DateTimeKind.Utc),
        };

        string json = JsonConvert.SerializeObject(account, Formatting.Indented);
        Console.WriteLine(json);
    }
    ```

1. <span data-ttu-id="4e495-128">Erstellen Sie die App mit dem Befehl `dotnet run`, und führen Sie sie aus.</span><span class="sxs-lookup"><span data-stu-id="4e495-128">Build and run the app by using the `dotnet run` command.</span></span> <span data-ttu-id="4e495-129">Die Ausgabe sollte die JSON-Darstellung des `Account`-Objekts im Code sein:</span><span class="sxs-lookup"><span data-stu-id="4e495-129">The output should be the JSON representation of the `Account` object in the code:</span></span>

    ```output
    {
      "Name": "John Doe",
      "Email": "john@nuget.org",
      "DOB": "1980-02-20T00:00:00Z"
    }
    ```
## <a name="related-video"></a><span data-ttu-id="4e495-130">Zugehörige Videos</span><span class="sxs-lookup"><span data-stu-id="4e495-130">Related video</span></span>

> [!Video https://channel9.msdn.com/Series/NuGet-101/Install-and-Use-a-NuGet-Package-with-the-NET-CLI-3-of-5/player]

<span data-ttu-id="4e495-131">Auf [Channel 9](https://channel9.msdn.com/Series/NuGet-101) und auf [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_) finden Sie weitere Videos zu NuGet.</span><span class="sxs-lookup"><span data-stu-id="4e495-131">Find more NuGet videos on [Channel 9](https://channel9.msdn.com/Series/NuGet-101) and [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_).</span></span>

## <a name="next-steps"></a><span data-ttu-id="4e495-132">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="4e495-132">Next steps</span></span>

<span data-ttu-id="4e495-133">Herzlichen Glückwunsch zur Installation und Verwendung Ihres ersten NuGet-Pakets!</span><span class="sxs-lookup"><span data-stu-id="4e495-133">Congratulations on installing and using your first NuGet package!</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="4e495-134">Installieren und Verwalten von Paketen mit der dotnet-CLI</span><span class="sxs-lookup"><span data-stu-id="4e495-134">Install and use packages using the dotnet CLI</span></span>](../consume-packages/install-use-packages-dotnet-cli.md)

<span data-ttu-id="4e495-135">Klicken Sie für weitere Informationen zu den Features von NuGet auf folgende Links.</span><span class="sxs-lookup"><span data-stu-id="4e495-135">To explore more that NuGet has to offer, select the links below.</span></span>

- [<span data-ttu-id="4e495-136">Übersicht über den Paketverbrauch und dessen Workflows</span><span class="sxs-lookup"><span data-stu-id="4e495-136">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="4e495-137">Suchen und Auswählen von Paketen</span><span class="sxs-lookup"><span data-stu-id="4e495-137">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="4e495-138">Paketverweise in Projektdateien</span><span class="sxs-lookup"><span data-stu-id="4e495-138">Package references in project files</span></span>](../consume-packages/package-references-in-project-files.md)
