---
title: Erstellen und Veröffentlichen eines NuGet-Pakets mithilfe der . NET CLI
description: Eine exemplarische Vorgehensweise zur Erstellung und Veröffentlichung eines NuGet-Pakets mit der .NET Core-CLI „dotnet“.
author: karann-msft
ms.author: karann
ms.date: 01/24/2018
ms.topic: quickstart
ms.openlocfilehash: 02aa7bb9d27352bbecfc718ef5bd6ee33501018d
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43548428"
---
# <a name="quickstart-create-and-publish-a-package-dotnet-cli"></a><span data-ttu-id="78a83-103">Schnellstart: Erstellen und Veröffentlichen eines Pakets (.NET CLI)</span><span class="sxs-lookup"><span data-stu-id="78a83-103">Quickstart: Create and publish a package (dotnet CLI)</span></span>

<span data-ttu-id="78a83-104">Ein NuGet-Paket kann, mithilfe der `dotnet`-Befehlszeilenschnittstelle (CLI), problemlos über eine .NET-Klassenbibliothek erstellt und auf nuget.org veröffentlicht werden.</span><span class="sxs-lookup"><span data-stu-id="78a83-104">It's a simple process to create a NuGet package from a .NET Class Library and publish it to nuget.org using the `dotnet` command-line interface (CLI).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="78a83-105">Erforderliche Komponenten</span><span class="sxs-lookup"><span data-stu-id="78a83-105">Prerequisites</span></span>

1. <span data-ttu-id="78a83-106">Installieren Sie das [.NET Core SDK](https://www.microsoft.com/net/download/), das die `dotnet`-CLI enthält.</span><span class="sxs-lookup"><span data-stu-id="78a83-106">Install the [.NET Core SDK](https://www.microsoft.com/net/download/), which includes the `dotnet` CLI.</span></span>

1. <span data-ttu-id="78a83-107">[Registrieren Sie sich für ein kostenloses Konto auf nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F), falls Sie noch kein Konto haben.</span><span class="sxs-lookup"><span data-stu-id="78a83-107">[Register for a free account on nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F) if you don't have one already.</span></span> <span data-ttu-id="78a83-108">Wenn Sie ein neues Konto erstellen, wird Ihnen eine Bestätigungs-E-Mail gesendet.</span><span class="sxs-lookup"><span data-stu-id="78a83-108">Creating a new account sends a confirmation email.</span></span> <span data-ttu-id="78a83-109">Sie müssen das Konto bestätigen, bevor Sie ein Paket hochladen können.</span><span class="sxs-lookup"><span data-stu-id="78a83-109">You must confirm the account before you can upload a package.</span></span>

## <a name="create-a-class-library-project"></a><span data-ttu-id="78a83-110">Erstellen eines Klassenbibliotheksprojekts</span><span class="sxs-lookup"><span data-stu-id="78a83-110">Create a class library project</span></span>

<span data-ttu-id="78a83-111">Sie können ein vorhandenes Projekt in der .NET-Klassenbibliothek für Code verwenden, den Sie packen wollen, oder ein einfaches Projekt wie folgt erstellen:</span><span class="sxs-lookup"><span data-stu-id="78a83-111">You can use an existing .NET Class Library project for the code you want to package, or create a simple one as follows:</span></span>

1. <span data-ttu-id="78a83-112">Erstellen Sie einen Ordner namens `AppLogger` und öffnen diesen.</span><span class="sxs-lookup"><span data-stu-id="78a83-112">Create a folder called `AppLogger` and change into it.</span></span>

1. <span data-ttu-id="78a83-113">Erstellen Sie das Projekt mit dem Befehl `dotnet new classlib`, der den Namen des aktuellen Ordners für das Projekt verwendet.</span><span class="sxs-lookup"><span data-stu-id="78a83-113">Create the project using `dotnet new classlib`, which uses the name of the current folder for the project.</span></span>

## <a name="add-package-metadata-to-the-project-file"></a><span data-ttu-id="78a83-114">Hinzufügen von Paketmetadaten zu einer Projektdatei</span><span class="sxs-lookup"><span data-stu-id="78a83-114">Add package metadata to the project file</span></span>

<span data-ttu-id="78a83-115">Jedes NuGet-Paket benötigt ein Manifest, das die Inhalte und Abhängigkeiten des Pakets beschreibt.</span><span class="sxs-lookup"><span data-stu-id="78a83-115">Every NuGet package needs a manifest that describes the package's contents and dependencies.</span></span> <span data-ttu-id="78a83-116">In dem letzten Paket ist das Manifest eine `.nuspec`-Datei, die aus NuGet-Metadateneigenschaften erstellt wird, die Sie in der Projektdatei einbeziehen.</span><span class="sxs-lookup"><span data-stu-id="78a83-116">In a final package, the manifest is a `.nuspec` file that is generated from the NuGet metadata properties that you include in the project file.</span></span>

1. <span data-ttu-id="78a83-117">Öffnen Sie Ihre Projektdatei (`.csproj`), und fügen Sie die folgenden mindestens erforderlichen Eigenschaften in das vorhandene `<PropertyGroup>`-Tag ein, und passen Sie die Werte entsprechend an:</span><span class="sxs-lookup"><span data-stu-id="78a83-117">Open your project file (`.csproj`) and add the following minimal properties inside the existing `<PropertyGroup>` tag, changing the values as appropriate:</span></span>

    ```xml
    <PackageId>AppLogger</PackageId>
    <Version>1.0.0</Version>
    <Authors>your_name</Authors>
    <Company>your_company</Company>
    ```

    > [!Important]
    > <span data-ttu-id="78a83-118">Weisen Sie dem Paket einen Bezeichner zu, der auf nuget.org bzw. auf dem Host, den Sie verwenden, einzigartig ist.</span><span class="sxs-lookup"><span data-stu-id="78a83-118">Give the package an identifier that's unique across nuget.org or whatever host you're using.</span></span> <span data-ttu-id="78a83-119">Für diese exemplarische Vorgehensweise wird empfohlen, im Namen „Sample“ oder „Test“ zu verwenden, da der Name in einem späteren Veröffentlichungsschritt öffentlich sichtbar gemacht wird (auch wenn es unwahrscheinlich ist, dass jemand versucht, es zu verwenden).</span><span class="sxs-lookup"><span data-stu-id="78a83-119">For this walkthrough we recommend including "Sample" or "Test" in the name as the later publishing step does make the package publicly visible (though it's unlikely anyone will actually use it).</span></span>

1. <span data-ttu-id="78a83-120">Fügen Sie optionale Eigenschaften wie unter [NuGet-Metadateneigenschaften](/dotnet/core/tools/csproj#nuget-metadata-properties) beschrieben hinzu.</span><span class="sxs-lookup"><span data-stu-id="78a83-120">Add any optional properties described on [NuGet metadata properties](/dotnet/core/tools/csproj#nuget-metadata-properties).</span></span>

    > [!Note]
    > <span data-ttu-id="78a83-121">Bei Paketen für die öffentliche Nutzung sollten Sie besonders auf die **PackageTags**-Eigenschaft achten, da Tags anderen dabei helfen, Ihr Paket zu finden und dessen Funktion zu verstehen.</span><span class="sxs-lookup"><span data-stu-id="78a83-121">For packages built for public consumption, pay special attention to the **PackageTags** property, as tags help others find your package and understand what it does.</span></span>

## <a name="run-the-pack-command"></a><span data-ttu-id="78a83-122">Ausführen des Befehls pack</span><span class="sxs-lookup"><span data-stu-id="78a83-122">Run the pack command</span></span>

<span data-ttu-id="78a83-123">Um ein NuGet-Paket (eine `.nupkg`-Datei) aus dem Projekt zu erstellen, führen Sie den `dotnet pack`-Befehl aus, der auch das Projekt automatisch erstellt:</span><span class="sxs-lookup"><span data-stu-id="78a83-123">To build a NuGet package (a `.nupkg` file) from the project, run the `dotnet pack` command, which also builds the project automatically:</span></span>

```cli
# Uses the project file in the current folder by default
dotnet pack
```

<span data-ttu-id="78a83-124">Die Ausgabe zeigt den Pfad zu der `.nupkg`-Datei:</span><span class="sxs-lookup"><span data-stu-id="78a83-124">The output shows the path to the `.nupkg` file:</span></span>

```output
Microsoft (R) Build Engine version 15.5.180.51428 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 29.91 ms for D:\proj\AppLoggerNet\AppLogger\AppLogger.csproj.
  AppLogger -> D:\proj\AppLoggerNet\AppLogger\bin\Debug\netstandard2.0\AppLogger.dll
  Successfully created package 'D:\proj\AppLoggerNet\AppLogger\bin\Debug\AppLogger.1.0.0.nupkg'.
```

### <a name="automatically-generate-package-on-build"></a><span data-ttu-id="78a83-125">Automatisches Generieren des Pakets bei der Erstellung</span><span class="sxs-lookup"><span data-stu-id="78a83-125">Automatically generate package on build</span></span>

<span data-ttu-id="78a83-126">Um automatisch `dotnet pack` auszuführen, wenn Sie `dotnet build` ausführen, fügen Sie folgende Zeile zu Ihrer Projektdatei in `<PropertyGroup>` hinzu:</span><span class="sxs-lookup"><span data-stu-id="78a83-126">To automatically run `dotnet pack` when you run `dotnet build`, add the following line to your project file within `<PropertyGroup>`:</span></span>

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

## <a name="publish-the-package"></a><span data-ttu-id="78a83-127">Veröffentlichen des Pakets</span><span class="sxs-lookup"><span data-stu-id="78a83-127">Publish the package</span></span>

<span data-ttu-id="78a83-128">Sobald Sie eine `.nupkg`-Datei haben, können Sie diese, gemeinsam mit einem API-Schlüssel von nuget.org, über den Befehl `dotnet nuget push` auf nuget.org veröffentlichen.</span><span class="sxs-lookup"><span data-stu-id="78a83-128">Once you have a `.nupkg` file, you publish it to nuget.org using the `dotnet nuget push` command along with an API key acquired from nuget.org.</span></span>

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a><span data-ttu-id="78a83-129">Erwerben des API-Schlüssels</span><span class="sxs-lookup"><span data-stu-id="78a83-129">Acquire your API key</span></span>

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-dotnet-nuget-push"></a><span data-ttu-id="78a83-130">Veröffentlichen mit „dotnet nuget push“</span><span class="sxs-lookup"><span data-stu-id="78a83-130">Publish with dotnet nuget push</span></span>

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-errors"></a><span data-ttu-id="78a83-131">Veröffentlichungsfehler</span><span class="sxs-lookup"><span data-stu-id="78a83-131">Publish errors</span></span>

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a><span data-ttu-id="78a83-132">Verwalten des veröffentlichten Pakets</span><span class="sxs-lookup"><span data-stu-id="78a83-132">Manage the published package</span></span>

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="related-topics"></a><span data-ttu-id="78a83-133">Verwandte Themen</span><span class="sxs-lookup"><span data-stu-id="78a83-133">Related topics</span></span>

- [<span data-ttu-id="78a83-134">Erstellen eines Pakets</span><span class="sxs-lookup"><span data-stu-id="78a83-134">Create a Package</span></span>](../create-packages/creating-a-package.md)
- [<span data-ttu-id="78a83-135">Veröffentlichen eines Pakets</span><span class="sxs-lookup"><span data-stu-id="78a83-135">Publish a Package</span></span>](../create-packages/publish-a-package.md)
- [<span data-ttu-id="78a83-136">Vorabversionen von Paketen</span><span class="sxs-lookup"><span data-stu-id="78a83-136">Pre-release Packages</span></span>](../create-packages/Prerelease-Packages.md)
- [<span data-ttu-id="78a83-137">Unterstützung mehrerer Zielframeworks</span><span class="sxs-lookup"><span data-stu-id="78a83-137">Support multiple target frameworks</span></span>](../create-packages/supporting-multiple-target-frameworks.md)
- [<span data-ttu-id="78a83-138">Paketversionsverwaltung</span><span class="sxs-lookup"><span data-stu-id="78a83-138">Package versioning</span></span>](../reference/package-versioning.md)
- [<span data-ttu-id="78a83-139">Erstellen von lokalisierten Paketen</span><span class="sxs-lookup"><span data-stu-id="78a83-139">Creating localized packages</span></span>](../create-packages/creating-localized-packages.md)
- [<span data-ttu-id="78a83-140">Signieren von Paketen</span><span class="sxs-lookup"><span data-stu-id="78a83-140">Signing packages</span></span>](../create-packages/Sign-a-package.md)
