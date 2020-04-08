---
title: Identifizieren des Projektformats
description: Beschreibt, wie Sie das Projektformat identifizieren
author: mikejo5000
ms.author: mikejo
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: b151547e40e567b38acc2b0b9ee84c50d85000c9
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/07/2020
ms.locfileid: "69488477"
---
# <a name="identify-the-project-format"></a>Identifizieren des Projektformats

NuGet kann für alle .NET-Projekte verwendet werden. Das Projektformat (SDK-Format oder Nicht-SDK-Format) bestimmt jedoch einige der Tools und Methoden, die zum Verwenden und Erstellen von NuGet-Paketen erforderlich sind. Projekte im SDK-Format verwenden das [SDK-Attribut](/dotnet/core/tools/csproj#additions). Es ist wichtig, den Projekttyp zu identifizieren, da die Methoden und Tools, mit denen Sie NuGet-Pakete verwenden und erstellen, vom Projektformat abhängen. Für Projekte im Nicht-SDK-Format hängen die Methoden und Tools ebenfalls davon ab, ob das Projekt zum `PackageReference`-Format migriert wurde.

Ob es sich um ein Projekt im SDK-Format handelt, hängt von der Methode ab, die zum Erstellen des Projekts verwendet wurde. In der folgenden Tabelle werden das Standardprojektformat und das zugehörige CLI-Tool für das Projekt angegeben, wenn Sie es mit Visual Studio 2017 oder einer neueren Version erstellen.

| Projekt&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Standard-projekt-format | CLI-Tool&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Notizen |
|:------------- |:-------------|:-----|:-----|
| .NET Standard | SDK-Format | [dotnet-CLI](../install-nuget-client-tools.md#dotnetexe-cli) | Projekte, die vor Visual Studio 2017 erstellt wurden, weisen nicht das SDK-Format auf. Verwenden Sie die `nuget.exe`-CLI. |
| .NET Core | SDK-Format | [dotnet-CLI](../install-nuget-client-tools.md#dotnetexe-cli) | Projekte, die vor Visual Studio 2017 erstellt wurden, weisen nicht das SDK-Format auf. Verwenden Sie die `nuget.exe`-CLI. |
| .NET Framework | Nicht-SDK-Format | [nuget.exe-CLI](../install-nuget-client-tools.md#nugetexe-cli) | .NET Framework Projekte, die mit anderen Methoden erstellt werden, sind möglicherweise Projekte im SDK-Format. Verwenden Sie für diese stattdessen die [dotnet-CLI](../install-nuget-client-tools.md#dotnetexe-cli). |
| [Migriertes](../consume-packages/migrate-packages-config-to-package-reference.md) .NET-Projekt | Nicht-SDK-Format| Verwenden Sie zum Erstellen von Paketen [msbuild -t:pack](../consume-packages/migrate-packages-config-to-package-reference.md#create-a-package-after-migration). | Zum Erstellen von Paketen wird `msbuild -t:pack` empfohlen. Verwenden Sie andernfalls die [dotnet-CLI](../install-nuget-client-tools.md#dotnetexe-cli). Migrierte Projekte sind keine Projekte im SDK-Format. |

## <a name="check-the-project-format"></a>Überprüfen des Projektformats

Wenn Sie sich nicht sicher sind, ob ein Projekt das SDK-Format aufweist, suchen Sie in der Projektdatei (für C# ist dies die CSPROJ-Datei) das SDK-Attribut im `<Project>`-Element. Wenn es vorhanden ist, handelt es sich um ein Projekt im SDK-Format.

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFramework>netstandard2.0</TargetFramework>
    <Authors>authorname</Authors>
    <PackageId>mypackageid</PackageId>
    <Company>mycompanyname</Company>
  </PropertyGroup>

</Project>
```

## <a name="check-the-project-format-in-visual-studio"></a>Überprüfen des Projektformats in Visual Studio

Wenn Sie in Visual Studio arbeiten, können Sie mit einer der folgenden Methoden das Projektformat schnell überprüfen:

- Klicken Sie mit der rechten Maustaste im Projektmappen-Explorer, und wählen Sie **"myprojectname.csproj" bearbeiten** aus.

   Diese Option ist nur ab Visual Studio 2017 für Projekte verfügbar, die das SDK-Attribut verwenden. Verwenden Sie andernfalls die andere Methode.

   ![Bearbeiten der Projektdatei](media/edit-project-file.png)

   Für ein Projekt im SDK-Format wird in der Projektdatei das [SDK-Attribut](/dotnet/core/tools/csproj#additions) angezeigt.
   
- Wählen Sie im Menü **Projekt** die Option **Projekt entladen** aus (oder klicken Sie mit der rechten Maustaste auf das Projekt, und wählen Sie **Projekt entladen** aus).

   In der Projektdatei dieses Projekts ist das SDK-Attribut nicht enthalten. Es handelt sich nicht um ein Projekt im SDK-Format.

   ![Entladen des Projekts](media/unload-project.png)

   Klicken Sie dann mit der rechten Maustaste auf das entladene Projekt, und wählen Sie **"myprojectname.csproj" bearbeiten** aus.

## <a name="see-also"></a>Weitere Informationen

- [Erstellen von .NET Standard-Paketen mit der dotnet-CLI](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md)
- [Erstellen von .NET Standard-Paketen mit Visual Studio](../quickstart/create-and-publish-a-package-using-visual-studio.md)
- [Erstellen und Veröffentlichen eines .NET Framework-Pakets (Visual Studio)](../quickstart/create-and-publish-a-package-using-visual-studio-net-framework.md)
- [NuGet-Befehle „pack“ und „restore“ als MSBuild-Ziele](../reference/msbuild-targets.md)
