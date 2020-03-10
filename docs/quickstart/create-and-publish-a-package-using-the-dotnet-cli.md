---
title: Erstellen und Veröffentlichen eines NuGet-Pakets mithilfe der dotnet-CLI
description: Eine exemplarische Vorgehensweise zur Erstellung und Veröffentlichung eines NuGet-Pakets mit der .NET Core-CLI „dotnet“.
author: karann-msft
ms.author: karann
ms.date: 05/24/2019
ms.topic: quickstart
ms.openlocfilehash: 8c09d6d5662ed6ff0deffa5d45b823ad0992f399
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/02/2020
ms.locfileid: "78231304"
---
# <a name="quickstart-create-and-publish-a-package-dotnet-cli"></a><span data-ttu-id="c3f06-103">Schnellstart: Erstellen und Veröffentlichen eines Pakets (dotnet CLI)</span><span class="sxs-lookup"><span data-stu-id="c3f06-103">Quickstart: Create and publish a package (dotnet CLI)</span></span>

<span data-ttu-id="c3f06-104">Ein NuGet-Paket kann, mithilfe der `dotnet`-Befehlszeilenschnittstelle (CLI), problemlos über eine .NET-Klassenbibliothek erstellt und auf nuget.org veröffentlicht werden.</span><span class="sxs-lookup"><span data-stu-id="c3f06-104">It's a simple process to create a NuGet package from a .NET Class Library and publish it to nuget.org using the `dotnet` command-line interface (CLI).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="c3f06-105">Voraussetzungen</span><span class="sxs-lookup"><span data-stu-id="c3f06-105">Prerequisites</span></span>

1. <span data-ttu-id="c3f06-106">Installieren Sie das [.NET Core SDK](https://www.microsoft.com/net/download/), das die `dotnet`-CLI enthält.</span><span class="sxs-lookup"><span data-stu-id="c3f06-106">Install the [.NET Core SDK](https://www.microsoft.com/net/download/), which includes the `dotnet` CLI.</span></span> <span data-ttu-id="c3f06-107">Ab Visual Studio 2017 wird die dotnet-CLI automatisch mit jeder .NET Core-bezogenen Workload installiert.</span><span class="sxs-lookup"><span data-stu-id="c3f06-107">Starting in Visual Studio 2017, the dotnet CLI is automatically installed with any .NET Core related workloads.</span></span>

1. <span data-ttu-id="c3f06-108">[Registrieren Sie sich für ein kostenloses Konto auf nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F), falls Sie noch kein Konto haben.</span><span class="sxs-lookup"><span data-stu-id="c3f06-108">[Register for a free account on nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) if you don't have one already.</span></span> <span data-ttu-id="c3f06-109">Wenn Sie ein neues Konto erstellen, wird Ihnen eine Bestätigungs-E-Mail gesendet.</span><span class="sxs-lookup"><span data-stu-id="c3f06-109">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="c3f06-110">Sie müssen das Konto bestätigen, bevor Sie ein Paket hochladen können.</span><span class="sxs-lookup"><span data-stu-id="c3f06-110">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="c3f06-111">Erstellen eines Klassenbibliotheksprojekts</span><span class="sxs-lookup"><span data-stu-id="c3f06-111">Create a class library project</span></span>

<span data-ttu-id="c3f06-112">Sie können ein vorhandenes Projekt in der .NET-Klassenbibliothek für Code verwenden, den Sie packen wollen, oder ein einfaches Projekt wie folgt erstellen:</span><span class="sxs-lookup"><span data-stu-id="c3f06-112">You can use an existing .NET Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="c3f06-113">Erstellen Sie einen Ordner mit dem Namen `AppLogger`.</span><span class="sxs-lookup"><span data-stu-id="c3f06-113">Create a folder called `AppLogger`.</span></span>

1. <span data-ttu-id="c3f06-114">Öffnen Sie eine Eingabeaufforderung, und navigieren Sie zum Ordner `AppLogger`.</span><span class="sxs-lookup"><span data-stu-id="c3f06-114">Open a command prompt and switch to the `AppLogger` folder.</span></span>

1. <span data-ttu-id="c3f06-115">Geben Sie `dotnet new classlib` ein. Der Name des aktuellen Ordners wird für das Projekt verwendet.</span><span class="sxs-lookup"><span data-stu-id="c3f06-115">Type `dotnet new classlib`, which uses the name of the current folder for the project.</span></span>

   <span data-ttu-id="c3f06-116">Das neue Projekt wird erstellt.</span><span class="sxs-lookup"><span data-stu-id="c3f06-116">This creates the new project.</span></span>

## <a name="add-package-metadata-to-the-project-file"></a><span data-ttu-id="c3f06-117">Hinzufügen von Paketmetadaten zu einer Projektdatei</span><span class="sxs-lookup"><span data-stu-id="c3f06-117">Add package metadata to the project file</span></span>

<span data-ttu-id="c3f06-118">Jedes NuGet-Paket benötigt ein Manifest, das die Inhalte und Abhängigkeiten des Pakets beschreibt.</span><span class="sxs-lookup"><span data-stu-id="c3f06-118">Every NuGet package needs a manifest that describes the package's contents and dependencies.</span></span> <span data-ttu-id="c3f06-119">In dem letzten Paket ist das Manifest eine `.nuspec`-Datei, die aus NuGet-Metadateneigenschaften erstellt wird, die Sie in der Projektdatei einbeziehen.</span><span class="sxs-lookup"><span data-stu-id="c3f06-119">In a final package, the manifest is a `.nuspec` file that is generated from the NuGet metadata properties that you include in the project file.</span></span>

1. <span data-ttu-id="c3f06-120">Öffnen Sie Ihre Projektdatei (`.csproj`), und fügen Sie die folgenden mindestens erforderlichen Eigenschaften in das vorhandene `<PropertyGroup>`-Tag ein, und passen Sie die Werte entsprechend an:</span><span class="sxs-lookup"><span data-stu-id="c3f06-120">Open your project file (`.csproj`) and add the following minimal properties inside the existing `<PropertyGroup>` tag, changing the values as appropriate:</span></span>

    ```xml
    <PackageId>AppLogger</PackageId>
    <Version>1.0.0</Version>
    <Authors>your_name</Authors>
    <Company>your_company</Company>
    ```

    > [!Important]
    > <span data-ttu-id="c3f06-121">Weisen Sie dem Paket einen Bezeichner zu, der auf nuget.org bzw. auf dem Host, den Sie verwenden, einzigartig ist.</span><span class="sxs-lookup"><span data-stu-id="c3f06-121">Give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="c3f06-122">Für diese exemplarische Vorgehensweise wird empfohlen, im Namen „Sample“ oder „Test“ zu verwenden, da der Name in einem späteren Veröffentlichungsschritt öffentlich sichtbar gemacht wird (auch wenn es unwahrscheinlich ist, dass jemand versucht, es zu verwenden).</span><span class="sxs-lookup"><span data-stu-id="c3f06-122">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>

1. <span data-ttu-id="c3f06-123">Fügen Sie optionale Eigenschaften wie unter [NuGet-Metadateneigenschaften](/dotnet/core/tools/csproj#nuget-metadata-properties) beschrieben hinzu.</span><span class="sxs-lookup"><span data-stu-id="c3f06-123">Add any optional properties described on [NuGet metadata properties](/dotnet/core/tools/csproj#nuget-metadata-properties).</span></span>

    > [!Note]
    > <span data-ttu-id="c3f06-124">Bei Paketen für die öffentliche Nutzung sollten Sie besonders auf die **PackageTags**-Eigenschaft achten, da Tags anderen dabei helfen, Ihr Paket zu finden und dessen Funktion zu verstehen.</span><span class="sxs-lookup"><span data-stu-id="c3f06-124">For packages built for public consumption, pay special attention to the **PackageTags** property, as tags help others find your package and understand what it does.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="c3f06-125">Ausführen des Befehls pack</span><span class="sxs-lookup"><span data-stu-id="c3f06-125">Run the pack command</span></span>

<span data-ttu-id="c3f06-126">Um ein NuGet-Paket (eine `.nupkg`-Datei) aus dem Projekt zu erstellen, führen Sie den `dotnet pack`-Befehl aus, der auch das Projekt automatisch erstellt:</span><span class="sxs-lookup"><span data-stu-id="c3f06-126">To build a NuGet package (a `.nupkg` file) from the project, run the `dotnet pack` command, which also builds the project automatically:</span></span>

```dotnetcli
# Uses the project file in the current folder by default
dotnet pack
```

<span data-ttu-id="c3f06-127">Die Ausgabe zeigt den Pfad zu der `.nupkg`-Datei:</span><span class="sxs-lookup"><span data-stu-id="c3f06-127">The output shows the path to the `.nupkg` file:</span></span>

```output
Microsoft (R) Build Engine version 15.5.180.51428 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 29.91 ms for D:\proj\AppLoggerNet\AppLogger\AppLogger.csproj.
  AppLogger -> D:\proj\AppLoggerNet\AppLogger\bin\Debug\netstandard2.0\AppLogger.dll
  Successfully created package 'D:\proj\AppLoggerNet\AppLogger\bin\Debug\AppLogger.1.0.0.nupkg'.
```

### <a name="automatically-generate-package-on-build"></a><span data-ttu-id="c3f06-128">Automatisches Generieren des Pakets bei der Erstellung</span><span class="sxs-lookup"><span data-stu-id="c3f06-128">Automatically generate package on build</span></span>

<span data-ttu-id="c3f06-129">Um automatisch `dotnet pack` auszuführen, wenn Sie `dotnet build` ausführen, fügen Sie folgende Zeile zu Ihrer Projektdatei in `<PropertyGroup>` hinzu:</span><span class="sxs-lookup"><span data-stu-id="c3f06-129">To automatically run `dotnet pack` when you run `dotnet build`, add the following line to your project file within `<PropertyGroup>`:</span></span>

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

## <a name="publish-the-package"></a><span data-ttu-id="c3f06-130">Veröffentlichen des Pakets</span><span class="sxs-lookup"><span data-stu-id="c3f06-130">Publish the package</span></span>

<span data-ttu-id="c3f06-131">Sobald Sie eine `.nupkg`-Datei haben, können Sie diese, gemeinsam mit einem API-Schlüssel von nuget.org, über den Befehl `dotnet nuget push` auf nuget.org veröffentlichen.</span><span class="sxs-lookup"><span data-stu-id="c3f06-131">Once you have a `.nupkg` file, you publish it to nuget.org using the `dotnet nuget push` command along with an API key acquired from nuget.org.</span></span>

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="c3f06-132">Erwerben des API-Schlüssels</span><span class="sxs-lookup"><span data-stu-id="c3f06-132">Acquire your API key</span></span>

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-dotnet-nuget-push"></a><span data-ttu-id="c3f06-133">Veröffentlichen mit „dotnet nuget push“</span><span class="sxs-lookup"><span data-stu-id="c3f06-133">Publish with dotnet nuget push</span></span>

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-errors"></a><span data-ttu-id="c3f06-134">Veröffentlichungsfehler</span><span class="sxs-lookup"><span data-stu-id="c3f06-134">Publish errors</span></span>

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="c3f06-135">Verwalten des veröffentlichten Pakets</span><span class="sxs-lookup"><span data-stu-id="c3f06-135">Manage the published package</span></span>

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="related-video"></a><span data-ttu-id="c3f06-136">Zugehörige Videos</span><span class="sxs-lookup"><span data-stu-id="c3f06-136">Related video</span></span>

> [!Video https://channel9.msdn.com/Series/NuGet-101/Create-and-Publish-a-NuGet-Package-with-the-NET-CLI-5-of-5/player]

<span data-ttu-id="c3f06-137">Auf [Channel 9](https://channel9.msdn.com/Series/NuGet-101) und auf [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_) finden Sie weitere Videos zu NuGet.</span><span class="sxs-lookup"><span data-stu-id="c3f06-137">Find more NuGet videos on [Channel 9](https://channel9.msdn.com/Series/NuGet-101) and [YouTube](https://www.youtube.com/playlist?list=PLdo4fOcmZ0oVLvfkFk8O9h6v2Dcdh2bh_).</span></span>

## <a name="next-steps"></a><span data-ttu-id="c3f06-138">Nächste Schritte</span><span class="sxs-lookup"><span data-stu-id="c3f06-138">Next steps</span></span>

<span data-ttu-id="c3f06-139">Herzlichen Glückwunsch zur Erstellung Ihres ersten NuGet-Pakets!</span><span class="sxs-lookup"><span data-stu-id="c3f06-139">Congratulations on creating your first NuGet package!</span></span>

> [!div class="nextstepaction"]
> [<span data-ttu-id="c3f06-140">Erstellen eines Pakets</span><span class="sxs-lookup"><span data-stu-id="c3f06-140">Create a Package</span></span>](../create-packages/creating-a-package-dotnet-cli.md)

<span data-ttu-id="c3f06-141">Klicken Sie für weitere Informationen zu den Features von NuGet auf folgende Links.</span><span class="sxs-lookup"><span data-stu-id="c3f06-141">To explore more that NuGet has to offer, select the links below.</span></span>

- [<span data-ttu-id="c3f06-142">Veröffentlichen eines Pakets</span><span class="sxs-lookup"><span data-stu-id="c3f06-142">Publish a Package</span></span>](../nuget-org/publish-a-package.md)
- [<span data-ttu-id="c3f06-143">Vorabversionen von Paketen</span><span class="sxs-lookup"><span data-stu-id="c3f06-143">Pre-release Packages</span></span>](../create-packages/Prerelease-Packages.md)
- [<span data-ttu-id="c3f06-144">Unterstützung mehrerer Zielframeworks</span><span class="sxs-lookup"><span data-stu-id="c3f06-144">Support multiple target frameworks</span></span>](../create-packages/multiple-target-frameworks-project-file.md)
- [<span data-ttu-id="c3f06-145">Paketversionsverwaltung</span><span class="sxs-lookup"><span data-stu-id="c3f06-145">Package versioning</span></span>](../concepts/package-versioning.md)
- [<span data-ttu-id="c3f06-146">Erstellen von lokalisierten Paketen</span><span class="sxs-lookup"><span data-stu-id="c3f06-146">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="c3f06-147">Erstellen von Symbolpaketen</span><span class="sxs-lookup"><span data-stu-id="c3f06-147">Creating symbol packages</span></span>](../create-packages/symbol-packages-snupkg.md)
- [<span data-ttu-id="c3f06-148">Signieren von Paketen</span><span class="sxs-lookup"><span data-stu-id="c3f06-148">Signing packages</span></span>](../create-packages/Sign-a-package.md)
