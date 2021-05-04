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
# <a name="set-a-nuget-package-type"></a>Festlegen eines NuGet-Pakettyps

Pakete können mit einem oder mehreren anderen *Pakettypen* markiert werden, um die beabsichtigte Verwendung anzuzeigen.

## <a name="known-package-types"></a>Bekannte Pakettypen

- Pakete mit Typ `Dependency` fügen Bibliotheken und Anwendungen Build- oder Laufzeitressourcen hinzu und können in jedem Projekttyp installiert werden, wenn sie kompatibel sind.

- Pakete vom Typ `DotnetTool` sind .NET-Tools, die von der [dotnet CLI](/dotnet/articles/core/tools/index) installiert werden können.

- Pakete vom Typ `Template` stellen [benutzerdefinierten Vorlagen](/dotnet/core/tools/custom-templates) bereit, mit denen sich Dateien oder Projekte wie Apps, Dienste, Tools oder Klassenbibliotheken erstellen lassen.

Pakete ohne Typ, einschließlich aller mit früheren Versionen von NuGet erstellten Pakete, haben standardmäßig den Typ `Dependency`.

> [!NOTE]
> Unterstützung für Pakettypen wurde in NuGet 3.5 hinzugefügt.
> Wenn Sie keinen benutzerdefinierten Pakettyp benötigen, sollten Sie den Pakettyp *nicht* explizit festlegen.
> NuGet verwendet standardmäßig den `Dependency`-Typ, wenn kein Typ angegeben wird.

## <a name="custom-package-types"></a>Benutzerdefinierte Pakettypen

Sie können Ihr Paket mit einem oder mehrere benutzerdefinierte Pakettypen markieren, wenn seine Verwendung nicht den bekannten [Pakettypen](#known-package-types) entspricht.

Stellen Sie sich beispielsweise vor, dass Kunden der `Contoso`-App Erweiterungen installieren können. Die App könnte von Erweiterungsautoren fordern, dass sie den benutzerdefinierten Pakettyp `ContosoExtension` verwenden, um ihre Pakete als geeignete Erweiterungen zu identifizieren, die den erforderlichen Konventionen entsprechen.

> [!WARNING]
> Ein Paket mit einem benutzerdefinierten Pakettyp kann weder von Visual Studio noch von nuget.exe installiert werden. Weitere Informationen finden Sie unter [NuGet/Home#10468](https://github.com/NuGet/Home/issues/10468).

# <a name="using-dotnet-cli"></a>[Verwenden der dotnet CLI](#tab/dotnet)

Pakettypen können in der Projektdatei (`.csproj`) festgelegt werden:

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>net5.0</TargetFramework>
    
    <PackageType>ContosoExtension</PackageType>
  </PropertyGroup>

</Project>
```

Pakete mit mehreren beabsichtigten Verwendungsarten können mithilfe des Trennzeichens `;` mit mehreren Pakettypen markiert werden:

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>net5.0</TargetFramework>
    
    <PackageType>PackageType1;PackageType2</PackageType>
  </PropertyGroup>

</Project>
```

Pakettypen können mithilfe des Trennzeichens `,` zwischen dem Pakettyp und seiner [`Version`](/dotnet/api/system.version)-Zeichenfolge mit einer Versionsangabe versehen werden:

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>net5.0</TargetFramework>
    
    <PackageType>PackageType1, 1.0.0.0;PackageType2</PackageType>
  </PropertyGroup>

</Project>
```

# <a name="using-nugetexe"></a>[Verwenden von nuget.exe](#tab/nugetexe)

Pakettypen werden in der Datei `.nuspec` innerhalb eines `packageTypes\packageType`-Knotens unter dem `<metadata>`-Element festgelegt:

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

Pakete mit mehreren beabsichtigten Verwendungsarten können mit mehreren Pakettypen gekennzeichnet werden:

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

Pakettypen können mithilfe der Zeichenfolge [`Version`](/dotnet/api/system.version) mit einer Versionsangabe versehen werden:

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

Das Format einer Pakettypzeichenfolge entspricht genau dem einer Paket-ID. Das heißt, ein Pakettyp ist eine Zeichenfolge ohne Berücksichtigung der Groß-/Kleinschreibung, die dem regulären Ausdruck `^\w+([_.-]\w+)*$` entspricht, der mindestens ein Zeichen und höchstens 100 Zeichen enthält.

Falls angegeben, ist die Pakettypversion eine [`Version`](/dotnet/api/system.version)-Zeichenfolge. Die Pakettypversion ist optional und nimmt den Standardwert `0.0` an.
