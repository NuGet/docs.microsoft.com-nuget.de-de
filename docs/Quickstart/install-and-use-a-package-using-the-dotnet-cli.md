---
title: Einführender Leitfaden zur Verwendung von NuGet-Paketen durch die dotnet-CLI | Microsoft-Dokumentation
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/23/2018
ms.topic: quickstart
ms.prod: nuget
ms.technology: ''
description: Ein Tutorial mit einer exemplarischen Vorgehensweise bei der Installation und Verwendung eines NuGet-Pakets in einem .NET Core-Projekt.
keywords: NuGet installieren, NuGet-Paketverbrauch, Installieren von NuGet-Paketen, NuGet-Paketverweise, Verwenden von NuGet-Paketen
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 87a37a733ebbbbf9bc161247b657a69f30ed4fb3
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="install-and-use-a-package-using-the-dotnet-cli"></a><span data-ttu-id="8cd3d-104">Installieren und Verwenden eines Pakets mithilfe der dotnet-CLI</span><span class="sxs-lookup"><span data-stu-id="8cd3d-104">Install and use a package using the dotnet CLI</span></span>

<span data-ttu-id="8cd3d-105">NuGet-Pakete enthalten wiederverwendbaren Code, der von anderen Entwicklern für die Verwendung in Ihren Projekten verfügbar gemacht wird.</span><span class="sxs-lookup"><span data-stu-id="8cd3d-105">NuGet packages contain reusable code that other developers make available to you for use in your projects.</span></span> <span data-ttu-id="8cd3d-106">Unter [Was ist NuGet?](../What-is-NuGet.md) finden Sie weitere Informationen.</span><span class="sxs-lookup"><span data-stu-id="8cd3d-106">See [What is NuGet?](../What-is-NuGet.md) for background.</span></span> <span data-ttu-id="8cd3d-107">Pakete werden mithilfe des Befehls `dotnet add package` in einem .NET Core-Projekt installiert, wie in diesem Artikel für das beliebte [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/)-Paket beschrieben wird.</span><span class="sxs-lookup"><span data-stu-id="8cd3d-107">Packages are installed into a .NET Core project using the `dotnet add package` command as described in this article for the popular [Newtonsoft.Json](https://www.nuget.org/packages/Newtonsoft.Json/) package.</span></span>

<span data-ttu-id="8cd3d-108">Beziehen Sie sich nach der Installation mit `using <namespace>` auf das Paket im Code, wobei \<Namespace\> für das von Ihnen verwendete Paket spezifisch ist.</span><span class="sxs-lookup"><span data-stu-id="8cd3d-108">Once installed, refer to the package in code with `using <namespace>` where \<namespace\> is specific to the package you're using.</span></span> <span data-ttu-id="8cd3d-109">Sie können dann die Paket-API verwenden.</span><span class="sxs-lookup"><span data-stu-id="8cd3d-109">You can then use the package's API.</span></span>

> [!Tip]
> <span data-ttu-id="8cd3d-110">**Einstieg in nuget.org**: .NET-Entwickler finden Komponenten für die Verwendung in ihren eigenen Anwendungen üblicherweise durch das Durchsuchen von nuget.org.</span><span class="sxs-lookup"><span data-stu-id="8cd3d-110">**Start with nuget.org**: Browsing nuget.org is how .NET developers typically find components they can reuse in their own applications.</span></span> <span data-ttu-id="8cd3d-111">Sie können nuget.org direkt durchsuchen oder in Visual Studio nach Paketen suchen und diese installieren, wie in diesem Artikel dargestellt wird.</span><span class="sxs-lookup"><span data-stu-id="8cd3d-111">You can search nuget.org directly or find and install packages within Visual Studio as shown in this article.</span></span>

## <a name="prerequisites"></a><span data-ttu-id="8cd3d-112">Erforderliche Komponenten</span><span class="sxs-lookup"><span data-stu-id="8cd3d-112">Prerequisites</span></span>

- <span data-ttu-id="8cd3d-113">Das [.NET Core SDK](https://www.microsoft.com/net/download/), das das Befehlszeilentool `dotnet` bietet.</span><span class="sxs-lookup"><span data-stu-id="8cd3d-113">The [.NET Core SDK](https://www.microsoft.com/net/download/), which provides the `dotnet` command-line tool.</span></span>

## <a name="create-a-project"></a><span data-ttu-id="8cd3d-114">Erstellen eines Projekts</span><span class="sxs-lookup"><span data-stu-id="8cd3d-114">Create a project</span></span>

<span data-ttu-id="8cd3d-115">NuGet-Pakete können in beliebigen .NET-Projekten installiert werden.</span><span class="sxs-lookup"><span data-stu-id="8cd3d-115">NuGet packages can be installed into a .NET project of some kind.</span></span> <span data-ttu-id="8cd3d-116">Erstellen Sie für diese exemplarische Vorgehensweise folgendermaßen ein einfaches .NET Core-Konsolenprojekt:</span><span class="sxs-lookup"><span data-stu-id="8cd3d-116">For this walkthrough, create a simple .NET Core console project as follows:</span></span>

1. <span data-ttu-id="8cd3d-117">Erstellen Sie einen Ordner für das Projekt.</span><span class="sxs-lookup"><span data-stu-id="8cd3d-117">Create a folder for the project.</span></span>

1. <span data-ttu-id="8cd3d-118">Erstellen Sie das Projekt mithilfe des folgenden Befehls:</span><span class="sxs-lookup"><span data-stu-id="8cd3d-118">Create the project using the following command:</span></span>

    ```cli
    dotnet new console
    ```

1. <span data-ttu-id="8cd3d-119">Verwenden Sie den Befehl `dotnet run`, um zu prüfen, ob die App ordnungsgemäß erstellt wurde.</span><span class="sxs-lookup"><span data-stu-id="8cd3d-119">Use `dotnet run` to test that the app has been created properly.</span></span>

## <a name="add-the-newtonsoftjson-nuget-package"></a><span data-ttu-id="8cd3d-120">Hinzufügen des NuGet-Pakets „Newtonsoft.Json“</span><span class="sxs-lookup"><span data-stu-id="8cd3d-120">Add the Newtonsoft.Json NuGet package</span></span>

1. <span data-ttu-id="8cd3d-121">Verwenden Sie folgenden Befehl, um das `Newtonsoft.json`-Paket zu installieren:</span><span class="sxs-lookup"><span data-stu-id="8cd3d-121">Use the following command to install the `Newtonsoft.json` package:</span></span>

    ```cli
    dotnet add package Newtonsoft.Json
    ```

1. <span data-ttu-id="8cd3d-122">Öffnen Sie die `.csproj`-Datei, um den hinzugefügten Verweis zu sehen, nachdem der Befehl abgeschlossen wurde:</span><span class="sxs-lookup"><span data-stu-id="8cd3d-122">After the command completes, open the `.csproj` file to see the added reference:</span></span>

    ```xml
  <ItemGroup>
    <PackageReference Include="Newtonsoft.Json" Version="10.0.3" />
  </ItemGroup>
    ```

## <a name="use-the-newtonsoftjson-api-in-the-app"></a><span data-ttu-id="8cd3d-123">Verwenden der API „Newtonsoft.Json“ in der App</span><span class="sxs-lookup"><span data-stu-id="8cd3d-123">Use the Newtonsoft.Json API in the app</span></span>

1. <span data-ttu-id="8cd3d-124">Öffnen Sie die Datei `Program.cs`, und fügen Sie die folgende Zeile am Anfang der Datei hinzu:</span><span class="sxs-lookup"><span data-stu-id="8cd3d-124">Open the `Program.cs` file and add the following line at the top of the file:</span></span>

    ```cs
    using Newtonsoft.Json;
    ```

1. <span data-ttu-id="8cd3d-125">Fügen Sie den folgenden Code vor der Zeile `class Program` hinzu:</span><span class="sxs-lookup"><span data-stu-id="8cd3d-125">Add the following code before the `class Program` line:</span></span>

    ```cs
    public class Account
    {
        public string Name { get; set; }
        public string Email { get; set; }
        public DateTime DOB { get; set; }
    }
    ```

1. <span data-ttu-id="8cd3d-126">Ersetzen Sie die `Main`-Funktion durch den folgendes:</span><span class="sxs-lookup"><span data-stu-id="8cd3d-126">Replace the `Main` function with the following:</span></span>

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

1. <span data-ttu-id="8cd3d-127">Erstellen Sie die App mit dem Befehl `dotnet run`, und führen Sie sie aus.</span><span class="sxs-lookup"><span data-stu-id="8cd3d-127">Build and run the app by using the `dotnet run` command.</span></span> <span data-ttu-id="8cd3d-128">Die Ausgabe sollte die JSON-Darstellung des `Account`-Objekts im Code sein:</span><span class="sxs-lookup"><span data-stu-id="8cd3d-128">The output should be the JSON representation of the `Account` object in the code:</span></span>

    ```output
    {
      "Name": "John Doe",
      "Email": "john@nuget.org",
      "DOB": "1980-02-20T00:00:00Z"
    }
    ```

## <a name="related-articles"></a><span data-ttu-id="8cd3d-129">Verwandte Artikel</span><span class="sxs-lookup"><span data-stu-id="8cd3d-129">Related articles</span></span>

- [<span data-ttu-id="8cd3d-130">Übersicht über den Paketverbrauch und dessen Workflows</span><span class="sxs-lookup"><span data-stu-id="8cd3d-130">Overview and workflow of package consumption</span></span>](../consume-packages/overview-and-workflow.md)
- [<span data-ttu-id="8cd3d-131">Suchen und Auswählen von Paketen</span><span class="sxs-lookup"><span data-stu-id="8cd3d-131">Finding and choosing packages</span></span>](../consume-packages/finding-and-choosing-packages.md)
- [<span data-ttu-id="8cd3d-132">So können Sie ein Paket erstellen</span><span class="sxs-lookup"><span data-stu-id="8cd3d-132">Ways to install a package</span></span>](../consume-packages/ways-to-install-a-package.md)
- [<span data-ttu-id="8cd3d-133">Konfigurieren von NuGet-Verhalten</span><span class="sxs-lookup"><span data-stu-id="8cd3d-133">Configuring NuGet Behavior</span></span>](../consume-packages/configuring-nuget-behavior.md)
