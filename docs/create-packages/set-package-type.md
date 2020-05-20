---
title: Festlegen eines NuGet-Pakettyps
description: Beschreibt Pakettypen, um die beabsichtigte Verwendung eines Pakets anzugeben.
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: 1d869f616ce0291cf1c0a17b7ff20fc61e6a3bd5
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/07/2020
ms.locfileid: "78230823"
---
# <a name="set-a-nuget-package-type"></a><span data-ttu-id="173c4-103">Festlegen eines NuGet-Pakettyps</span><span class="sxs-lookup"><span data-stu-id="173c4-103">Set a NuGet package type</span></span>

<span data-ttu-id="173c4-104">In NuGet 3.5 und höher können Pakete mit einem bestimmten *Pakettyp* gekennzeichnet werden, um den vorgesehenen Zweck anzugeben.</span><span class="sxs-lookup"><span data-stu-id="173c4-104">With NuGet 3.5+, packages can be marked with a specific *package type* to indicate its intended use.</span></span> <span data-ttu-id="173c4-105">Pakete ohne Typ, einschließlich aller mit früheren Versionen von NuGet erstellten Pakete, haben standardmäßig den Typ `Dependency`.</span><span class="sxs-lookup"><span data-stu-id="173c4-105">Packages not marked with a type, including all packages created with earlier versions of NuGet, default to the `Dependency` type.</span></span>

- <span data-ttu-id="173c4-106">Pakete mit Typ `Dependency` fügen Bibliotheken und Anwendungen Build- oder Laufzeitressourcen hinzu und können in jedem Projekttyp installiert werden, wenn sie kompatibel sind.</span><span class="sxs-lookup"><span data-stu-id="173c4-106">`Dependency` type packages add build- or run-time assets to libraries and applications, and can be installed in any project type (assuming they are compatible).</span></span>

- <span data-ttu-id="173c4-107">Pakete vom Typ `DotnetTool` sind Erweiterungen der [dotnet-CLI](/dotnet/articles/core/tools/index) und werden über die Befehlszeile aufgerufen.</span><span class="sxs-lookup"><span data-stu-id="173c4-107">`DotnetTool` type packages are extensions to the [dotnet CLI](/dotnet/articles/core/tools/index) and are invoked from the command line.</span></span> <span data-ttu-id="173c4-108">Solche Pakete können nur in .NET Core-Projekten installiert werden und haben keine Auswirkungen auf Wiederherstellungsvorgänge.</span><span class="sxs-lookup"><span data-stu-id="173c4-108">Such packages can be installed only in .NET Core projects and have no effect on restore operations.</span></span> <span data-ttu-id="173c4-109">Weitere Informationen zu diesen projektspezifischen Erweiterungen finden Sie in der Dokumentation zur [.NET Core-Erweiterbarkeit](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility).</span><span class="sxs-lookup"><span data-stu-id="173c4-109">More details about these per-project extensions are available in the  [.NET Core extensibility](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility) documentation.</span></span>

- <span data-ttu-id="173c4-110">Pakete vom Typ `Template` stellen [benutzerdefinierten Vorlagen](/dotnet/core/tools/custom-templates) bereit, mit denen sich Dateien oder Projekte wie Apps, Dienste, Tools oder Klassenbibliotheken erstellen lassen.</span><span class="sxs-lookup"><span data-stu-id="173c4-110">`Template` type packages provide [custom templates](/dotnet/core/tools/custom-templates) that can be used to create files or projects like an app, service, tool, or class library.</span></span>

- <span data-ttu-id="173c4-111">Pakete des benutzerdefinierten Typs verwenden einen willkürlichen Typbezeichner, der den gleichen Formatierungsregeln wie Paketbezeichner unterliegt.</span><span class="sxs-lookup"><span data-stu-id="173c4-111">Custom type packages use an arbitrary type identifier that conforms to the same format rules as package IDs.</span></span> <span data-ttu-id="173c4-112">Der NuGet-Paket-Manager in Visual Studio erkennt jedoch nur die Typen `Dependency` und `DotnetTool`.</span><span class="sxs-lookup"><span data-stu-id="173c4-112">Any type other than `Dependency` and `DotnetTool`, however, are not recognized by the NuGet Package Manager in Visual Studio.</span></span>

<span data-ttu-id="173c4-113">Pakettypen werden in der `.nuspec`-Datei festgelegt.</span><span class="sxs-lookup"><span data-stu-id="173c4-113">Package types are set in the `.nuspec` file.</span></span> <span data-ttu-id="173c4-114">Für die Abwärtskompatibilität wird empfohlen, den `Dependency`-Typ *nicht* explizit festzulegen und stattdessen NuGet entscheiden zu lassen, wenn kein Typ angegeben ist.</span><span class="sxs-lookup"><span data-stu-id="173c4-114">It's best for backwards compatibility to *not* explicitly set the `Dependency` type and to instead rely on NuGet assuming this type when no type is specified.</span></span>

- <span data-ttu-id="173c4-115">`.nuspec`: Geben Sie den Pakettyp innerhalb eines `packageTypes\packageType`-Knotens unter dem `<metadata>`-Element an:</span><span class="sxs-lookup"><span data-stu-id="173c4-115">`.nuspec`: Indicate the package type within a `packageTypes\packageType` node under the `<metadata>` element:</span></span>

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
        <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="DotnetTool" />
        </packageTypes>
        </metadata>
    </package>
    ```
