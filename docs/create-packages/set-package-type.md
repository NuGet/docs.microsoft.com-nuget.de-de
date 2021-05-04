---
title: Festlegen eines NuGet-Pakettyps
description: Beschreibt Pakettypen, um die beabsichtigte Verwendung eines Pakets anzugeben.
author: JonDouglas
ms.author: jodou
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: fa369e8327330e13f5adda39a75008e42ac99896
ms.sourcegitcommit: 08c5b2c956a1a45f0ea9fb3f50f55e41312d8ce3
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/27/2021
ms.locfileid: "108067276"
---
# <a name="set-a-nuget-package-type"></a><span data-ttu-id="51818-103">Festlegen eines NuGet-Pakettyps</span><span class="sxs-lookup"><span data-stu-id="51818-103">Set a NuGet package type</span></span>

<span data-ttu-id="51818-104">Pakete können mit einem oder mehreren anderen *Pakettypen* markiert werden, um die beabsichtigte Verwendung anzuzeigen.</span><span class="sxs-lookup"><span data-stu-id="51818-104">Packages can be marked with one more more *package types* to indicate its intended use.</span></span>

## <a name="known-package-types"></a><span data-ttu-id="51818-105">Bekannte Pakettypen</span><span class="sxs-lookup"><span data-stu-id="51818-105">Known package types</span></span>

- <span data-ttu-id="51818-106">Pakete mit Typ `Dependency` fügen Bibliotheken und Anwendungen Build- oder Laufzeitressourcen hinzu und können in jedem Projekttyp installiert werden, wenn sie kompatibel sind.</span><span class="sxs-lookup"><span data-stu-id="51818-106">`Dependency` type packages add build- or run-time assets to libraries and applications, and can be installed in any project type (assuming they are compatible).</span></span>

- <span data-ttu-id="51818-107">Pakete vom Typ `DotnetTool` sind .NET-Tools, die von der [dotnet CLI](/dotnet/articles/core/tools/index) installiert werden können.</span><span class="sxs-lookup"><span data-stu-id="51818-107">`DotnetTool` type packages are .NET tools that can be installed by the [dotnet CLI](/dotnet/articles/core/tools/index).</span></span>

- <span data-ttu-id="51818-108">Pakete vom Typ `Template` stellen [benutzerdefinierten Vorlagen](/dotnet/core/tools/custom-templates) bereit, mit denen sich Dateien oder Projekte wie Apps, Dienste, Tools oder Klassenbibliotheken erstellen lassen.</span><span class="sxs-lookup"><span data-stu-id="51818-108">`Template` type packages provide [custom templates](/dotnet/core/tools/custom-templates) that can be used to create files or projects like an app, service, tool, or class library.</span></span>

<span data-ttu-id="51818-109">Pakete ohne Typ, einschließlich aller mit früheren Versionen von NuGet erstellten Pakete, haben standardmäßig den Typ `Dependency`.</span><span class="sxs-lookup"><span data-stu-id="51818-109">Packages not marked with a type, including all packages created with earlier versions of NuGet, default to the `Dependency` type.</span></span>

> [!NOTE]
> <span data-ttu-id="51818-110">Unterstützung für Pakettypen wurde in NuGet 3.5 hinzugefügt.</span><span class="sxs-lookup"><span data-stu-id="51818-110">Support for package types was added in NuGet 3.5.</span></span>
> <span data-ttu-id="51818-111">Wenn Sie keinen benutzerdefinierten Pakettyp benötigen, sollten Sie den Pakettyp *nicht* explizit festlegen.</span><span class="sxs-lookup"><span data-stu-id="51818-111">If you don't need a custom package type, it's best to *not* explicitly set the package type.</span></span>
> <span data-ttu-id="51818-112">NuGet verwendet standardmäßig den `Dependency`-Typ, wenn kein Typ angegeben wird.</span><span class="sxs-lookup"><span data-stu-id="51818-112">NuGet defaults to the `Dependency` type when no type is specified.</span></span>

## <a name="custom-package-types"></a><span data-ttu-id="51818-113">Benutzerdefinierte Pakettypen</span><span class="sxs-lookup"><span data-stu-id="51818-113">Custom package types</span></span>

<span data-ttu-id="51818-114">Sie können Ihr Paket mit einem oder mehrere benutzerdefinierte Pakettypen markieren, wenn seine Verwendung nicht den bekannten [Pakettypen](#known-package-types) entspricht.</span><span class="sxs-lookup"><span data-stu-id="51818-114">You can mark your package with one or more custom package types if its use does not fit the [known package types](#known-package-types).</span></span>

<span data-ttu-id="51818-115">Stellen Sie sich beispielsweise vor, dass Kunden der `Contoso`-App Erweiterungen installieren können.</span><span class="sxs-lookup"><span data-stu-id="51818-115">For example, imagine that customers of the `Contoso` app can install extensions.</span></span> <span data-ttu-id="51818-116">Die App könnte von Erweiterungsautoren fordern, dass sie den benutzerdefinierten Pakettyp `ContosoExtension` verwenden, um ihre Pakete als geeignete Erweiterungen zu identifizieren, die den erforderlichen Konventionen entsprechen.</span><span class="sxs-lookup"><span data-stu-id="51818-116">The app could require extension authors to use the custom package type `ContosoExtension` to identify their packages as proper extensions that follow the required conventions.</span></span>

> [!WARNING]
> <span data-ttu-id="51818-117">Ein Paket mit einem benutzerdefinierten Pakettyp kann weder von Visual Studio noch von nuget.exe installiert werden.</span><span class="sxs-lookup"><span data-stu-id="51818-117">A package with a custom package type cannot be installed by Visual Studio or nuget.exe.</span></span> <span data-ttu-id="51818-118">Weitere Informationen finden Sie unter [NuGet/Home#10468](https://github.com/NuGet/Home/issues/10468).</span><span class="sxs-lookup"><span data-stu-id="51818-118">See [NuGet/Home#10468](https://github.com/NuGet/Home/issues/10468) for more information.</span></span>

# <a name="using-dotnet-cli"></a>[<span data-ttu-id="51818-119">Verwenden der dotnet CLI</span><span class="sxs-lookup"><span data-stu-id="51818-119">Using dotnet CLI</span></span>](#tab/dotnet)

<span data-ttu-id="51818-120">Pakettypen können in der Projektdatei (`.csproj`) festgelegt werden:</span><span class="sxs-lookup"><span data-stu-id="51818-120">Package types can be set in the project file (`.csproj`):</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>net5.0</TargetFramework>
    
    <PackageType>ContosoExtension</PackageType>
  </PropertyGroup>

</Project>
```

<span data-ttu-id="51818-121">Pakete mit mehreren beabsichtigten Verwendungsarten können mithilfe des Trennzeichens `;` mit mehreren Pakettypen markiert werden:</span><span class="sxs-lookup"><span data-stu-id="51818-121">Packages with multiple intended uses can be marked with multiple package types using the `;` delimiter:</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>net5.0</TargetFramework>
    
    <PackageType>PackageType1;PackageType2</PackageType>
  </PropertyGroup>

</Project>
```

<span data-ttu-id="51818-122">Pakettypen können mithilfe des Trennzeichens `,` zwischen dem Pakettyp und seiner [`Version`](/dotnet/api/system.version)-Zeichenfolge mit einer Versionsangabe versehen werden:</span><span class="sxs-lookup"><span data-stu-id="51818-122">Package types can be versioned using a `,` delimiter between the package type and its [`Version`](/dotnet/api/system.version) string:</span></span>

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>net5.0</TargetFramework>
    
    <PackageType>PackageType1, 1.0.0.0;PackageType2</PackageType>
  </PropertyGroup>

</Project>
```

# <a name="using-nugetexe"></a>[<span data-ttu-id="51818-123">Verwenden von nuget.exe</span><span class="sxs-lookup"><span data-stu-id="51818-123">Using nuget.exe</span></span>](#tab/nugetexe)

<span data-ttu-id="51818-124">Pakettypen werden in der Datei `.nuspec` innerhalb eines `packageTypes\packageType`-Knotens unter dem `<metadata>`-Element festgelegt:</span><span class="sxs-lookup"><span data-stu-id="51818-124">Package types are set in the `.nuspec` file within a `packageTypes\packageType` node under the `<metadata>` element:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="ContosoExtension" />
        </packageTypes>
    </metadata>
</package>
```

<span data-ttu-id="51818-125">Pakete mit mehreren beabsichtigten Verwendungsarten können mit mehreren Pakettypen gekennzeichnet werden:</span><span class="sxs-lookup"><span data-stu-id="51818-125">Packages with multiple intended uses may be marked with multiple package types:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="PackageType1" />
            <packageType name="PackageType2" />
        </packageTypes>
    </metadata>
</package>
```

<span data-ttu-id="51818-126">Pakettypen können mithilfe der Zeichenfolge [`Version`](/dotnet/api/system.version) mit einer Versionsangabe versehen werden:</span><span class="sxs-lookup"><span data-stu-id="51818-126">Package types can be versioned using a [`Version`](/dotnet/api/system.version) string:</span></span>

```xml
<?xml version="1.0" encoding="utf-8"?>
<package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
    <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="PackageType1" version="1.0.0.0" />
            <packageType name="PackageType2" />
        </packageTypes>
    </metadata>
</package>
```

---

<span data-ttu-id="51818-127">Das Format einer Pakettypzeichenfolge entspricht genau dem einer Paket-ID.</span><span class="sxs-lookup"><span data-stu-id="51818-127">The format of a package type string is exactly like a package ID.</span></span> <span data-ttu-id="51818-128">Das heißt, ein Pakettyp ist eine Zeichenfolge ohne Berücksichtigung der Groß-/Kleinschreibung, die dem regulären Ausdruck `^\w+([_.-]\w+)*$` entspricht, der mindestens ein Zeichen und höchstens 100 Zeichen enthält.</span><span class="sxs-lookup"><span data-stu-id="51818-128">That is, a package type is a case-insensitive string matching the regular expression `^\w+([_.-]\w+)*$` having at least one character and at most 100 characters.</span></span>

<span data-ttu-id="51818-129">Falls angegeben, ist die Pakettypversion eine [`Version`](/dotnet/api/system.version)-Zeichenfolge.</span><span class="sxs-lookup"><span data-stu-id="51818-129">If provided, the package type version is a [`Version`](/dotnet/api/system.version) string.</span></span> <span data-ttu-id="51818-130">Die Pakettypversion ist optional und nimmt den Standardwert `0.0` an.</span><span class="sxs-lookup"><span data-stu-id="51818-130">The package type version is optional and defaults to `0.0`.</span></span>
