---
title: Festlegung von Zielversionen für NuGet-Pakete in Ihrer Projektdatei
description: Beschreibung der verschiedenen Methoden für die Ausrichtung mehrerer .NET Framework-Versionen aus einem einzelnen NuGet-Paket.
author: karann-msft
ms.author: karann
ms.date: 07/15/2019
ms.topic: conceptual
ms.openlocfilehash: 1d23759433efb405fa5f0035049befced2c43d6b
ms.sourcegitcommit: 363ec6843409b4714c91b75b105619a3a3184b43
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/16/2019
ms.locfileid: "72380675"
---
# <a name="support-multiple-net-framework-versions-in-your-project-file"></a>Unterstützung für mehrere .NET Framework-Versionen in der Projektdatei

Wenn Sie zum ersten Mal ein Projekt erstellen, empfehlen wir Ihnen, eine .NET Standard-Klassenbibliothek zu erstellen, da sie mit den meisten Projekten kompatibel ist. Durch die Verwendung von .NET Standard fügen Sie standardmäßig [plattformübergreifende Unterstützung](/dotnet/standard/library-guidance/cross-platform-targeting) zu einer .NET-Bibliothek hinzu. In einigen Szenarien müssen Sie jedoch möglicherweise auch Code einbeziehen, der auf ein bestimmtes Framework abzielt. In diesem Artikel erfahren Sie, wie Sie dabei für Projekte im [SDK-Stil](../resources/check-project-format.md) vorgehen.

Für Projekte im SDK-Stil können Sie die Unterstützung für mehrere Zielframeworks ([TFM](/dotnet/standard/frameworks)) in der Projektdatei konfigurieren und dann `dotnet pack` oder `msbuild /t:pack` verwenden, um das Paket zu erstellen.

> [!NOTE]
> Die nuget.exe-CLI unterstützt nicht das Packen von Projekten im SDK-Stil. Daher sollten Sie nur `dotnet pack` oder `msbuild /t:pack` verwenden. Wir empfehlen, dass Sie stattdessen [alle Eigenschaften einbeziehen](../reference/msbuild-targets.md#pack-target), die sich normalerweise in der `.nuspec`-Datei in der Projektdatei befinden. Wenn Sie mehrere .NET Framework-Versionen in einem Projekt im Nicht-SDK-Stil als Ziel verwenden möchten, finden Sie weitere Informationen unter [Unterstützen mehrerer .NET Framework-Versionen](supporting-multiple-target-frameworks.md).

## <a name="create-a-project-that-supports-multiple-net-framework-versions"></a>Erstellen eines Projekts, das mehrere .NET Framework-Versionen unterstützt

1. Erstellen Sie eine neue .NET Standard-Klassenbibliothek in Visual Studio, oder verwenden Sie `dotnet new classlib`.

   Es wird empfohlen, dass Sie eine .NET Standard-Klassenbibliothek erstellen, um die bestmögliche Kompatibilität zu erzielen.

2. Bearbeiten Sie die *CSPROJ*-Datei, damit diese das Zielframe unterstützt. Ändern Sie beispielsweise
   
   `<TargetFramework>netstandard2.0</TargetFramework>`
   
   in:
   
   `<TargetFrameworks>netstandard2.0;net45</TargetFrameworks>`

   Stellen Sie sicher, dass Sie das XML-Element ändern, das von Singular auf Plural geändert wurde (fügen Sie das „s“ sowohl zu den geöffneten als auch zu den schließenden Tags hinzu).

3. Wenn Sie einen Code haben, der nur in einem TFM funktioniert, können Sie mit `#if NET45` oder `#if NETSTANDARD2_0` den TFM-abhängigen Code trennen. (Weitere Informationen finden Sie unter [So legen Sie die Zielversion fest](/dotnet/core/tutorials/libraries#how-to-multitarget).) Verwenden Sie z.B. den folgenden Code:

   ```csharp
   public string Platform {
      get {
   #if NET45
         return ".NET Framework"
   #elif NETSTANDARD2_0
         return ".NET Standard"
   #else
   #error This code block does not match csproj TargetFrameworks list
   #endif
      }
   }
   ```

4. Fügen Sie alle gewünschten NuGet-Metadaten zur *CSPROJ*-Datei als MSBuild-Eigenschaften hinzu.

   Eine Liste der verfügbaren Paketmetadaten und der Namen der MSBuild-Eigenschaften finden Sie unter[Paketziel](../reference/msbuild-targets.md#pack-target). Weitere Informationen finden Sie zudem unter [Steuern von Abhängigkeitsobjekten](../consume-packages/package-references-in-project-files.md#controlling-dependency-assets).

   Wenn Sie die Build-bezogenen Eigenschaften von den NuGet-Metadaten trennen möchten, können Sie eine andere `PropertyGroup` verwenden oder die NuGet-Eigenschaften in eine andere Datei einfügen und die MSBuild-Anweisung `Import` verwenden, um sie einzubinden. Ab .NET Framework 15.0 werden `Directory.Build.Props` und `Directory.Build.Targets` ebenfalls unterstützt.

5. Verwenden Sie jetzt `dotnet pack`, und die daraus resultierende *NUPKG*-Datei ist sowohl auf .NET Standard 2.0 als auch .NET Framework 4.5 ausgerichtet.

Hier ist die *CSPROJ*-Datei, die mit den vorherigen Schritten und dem .NET Core SDK 2.2 generiert wird.

```xml
<Project Sdk="Microsoft.NET.Sdk">

  <PropertyGroup>
    <TargetFrameworks>netstandard2.0;net45</TargetFrameworks>
    <Description>Sample project that targets multiple TFMs</Description>
  </PropertyGroup>

</Project>
```

## <a name="see-also"></a>Siehe auch

* [Angeben von Zielframeworks](/dotnet/standard/frameworks#how-to-specify-target-frameworks)
* [Plattformübergreifende Ziele](/dotnet/standard/library-guidance/cross-platform-targeting)
