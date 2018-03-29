---
title: Zielframeworkverweise für NuGet | Microsoft-Dokumentation
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/11/2017
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Durch NuGet-Zielframeworkverweise werden die Framework-abhängigen Komponenten eines Pakets identifiziert und isoliert.
keywords: NuGet-Zielpaket, .NET Framework-Ziele, .NET Framework-Versionen
ms.reviewer:
- anangaur
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 0a9c45ef31e27c2242edce48e2cf272e5280dcff
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="target-frameworks"></a>Zielframeworks

NuGet verwendet Zielframeworkverweise an vielen Stellen, um die Framework-abhängigen Komponenten eines Pakets zu identifizieren und zu isolieren:

- [NUSPEC-Manifest:](../reference/nuspec.md) Ein Paket kann unterschiedliche Pakete angeben, die je nach Zielframework in ein Projekt eingeschlossen werden sollen.
- [NUPKG-Ordnername:](../create-packages/creating-a-package.md#from-a-convention-based-working-directory) Die Ordner innerhalb des `lib`-Ordners eines Pakets können dem Zielframework entsprechend benannt werden. Jeder Ordner enthält die DLLs und andere geeignete Inhalte für das jeweilige Framework.
- [packages.config:](../reference/packages-config.md) Das `targetframework`-Attribut einer Abhängigkeit gibt die Variante eines Pakets an, das installiert werden soll.

> [!Note]
> Der Quellcode des NuGet-Clients, der die folgenden Tabellen berechnet, befindet sich an folgenden Speicherorten:
> - Unterstützte Frameworknamen: [FrameworkConstants.cs](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Frameworks/FrameworkConstants.cs)
> - Rangfolge und Zuordnung von Frameworks: [DefaultFrameworkMappings.cs](https://github.com/NuGet/NuGet.Client/blob/dev/src/NuGet.Core/NuGet.Frameworks/DefaultFrameworkMappings.cs)

## <a name="supported-frameworks"></a>Unterstützte Frameworks

Auf ein Framework wird in der Regel durch einen kurzen Zielframeworkmoniker (Target Framework Moniker, TFM) verwiesen. In .NET Standard kann dies auch mit *TxM* generalisiert werden, um einen einzigen Verweis auf mehrere Frameworks zu ermöglichen.

Die NuGet-Clients unterstützen die in der folgenden Tabelle aufgelisteten Frameworks. Äquivalente werden in eckigen Klammern angegeben. Beachten Sie, dass einige Tools (z.B. `dotnet`) möglicherweise Variationen von kanonischen TFMs in einigen Dateien verwenden. `dotnet pack` verwendet beispielsweise `.NETCoreApp2.0` statt `netcoreapp2.0` in einer `.nuspec`-Datei. Die verschiedenen NuGet-Clienttools verarbeiten diese Variationen ordnungsgemäß, Sie sollten jedoch immer kanonische TFMs verwenden, wenn Sie Dateien direkt bearbeiten.

| name           | Abkürzung | TFMs/TxMs |
| -------------  | ------------ | --------- |
|.NET Framework  | net          | net11     |
|                |              | net20     |
|                |              | net35     |
|                |              | net40     |
|                |              | net403    |
|                |              | net45      |
|                |              | net451     |
|                |              | net452     |
|                |              | net46      |
|                |              | net461     |
|                |              | net462     |
|Microsoft Store (Windows Store) | netcore      | netcore [netcore45] |
|                |              | netcore45 [win, win8] |
|                |              | netcore451 [win81] |
|                |              | netcore50 |
|.NET MicroFramework | netmf    | netmf |
|Windows         | win          | win [win8, netcore45] |
| | | win8 [netcore45, win] |
| | | win81 [netcore451] |
| | | win10 (nicht von Windows 10 unterstützt) |
Silverlight | sl | sl4 |
| | | sl5 |
Windows Phone (SL) | wp | wp [wp7] |
| | | wp7 |
| | | wp75 |
| | | wp8 |
| | | wp81 |
Windows Phone (UWP) | | wpa81 |
Universelle Windows-Plattform | uap | uap [uap10.0] |
| | | uap10.0 |
.NET-Standard | netstandard | netstandard1.0 |
| | | netstandard1.1 |
| | | netstandard1.2 |
| | | netstandard1.3 |
| | | netstandard1.4 |
| | | netstandard1.5 |
| | | netstandard1.6 |
| | | netstandard2.0 |
.NET Core-App | netcoreapp | netcoreapp1.0 |
| | | netcoreapp1.1 |
| | | netcoreapp2.0 |
Tizen | tizen | tizen3 |
| | | tizen4 |

## <a name="deprecated-frameworks"></a>Veraltete Frameworks
Die folgenden Frameworks sind veraltet. Pakete, die für diese Frameworks ausgelegt sind, sollten zur jeweiligen Ersetzung migriert werden.

| Veraltetes Framework | Ersetzung
| --- | ---
| aspnet50 | netcoreapp |
| aspnetcore50 |
| dnxcore50 |
| dnx |
| dnx45 |
| dnx451 |
| dnx452 |
| dotnet | netstandard |
| dotnet50 | |
| dotnet51 | |
| dotnet52 | |
| dotnet53 | |
| dotnet54 | |
| dotnet55 | |
| dotnet56 | |
| winrt | win |

## <a name="precedence"></a>Rangfolge

Einige Frameworks sind miteinander verwandt und kompatibel, aber nicht notwendigerweise äquivalent:

| Framework | Darf verwenden |
| --- | --- |
| uap (Universelle Windows-Plattform) | win81 |
| | wpa81 |
| | netcore50 |
| win (Microsoft Store) | winrt |
| | | winrt45 |

## <a name="net-platform-standard"></a>.NET-Plattformstandard

Der [.NET-Plattformstandard](https://github.com/dotnet/corefx/blob/master/Documentation/architecture/net-platform-standard.md) vereinfacht Verweise zwischen binärkompatiblen Frameworks, wodurch ein einzelnes Zielframeworks auf eine Kombination aus anderen Frameworks verweisen kann. (Weitere Informationen finden Sie unter [.NET Primer (Einführung in .NET)](/dotnet/articles/standard/index).)

Das NuGet-Tool [Get Nearest Framework](https://aka.ms/s2m3th) simuliert, wie NuGet in einem Paket, das auf dem Framework des Projekts basiert, ein Framework aus vielen verfügbaren Frameworkobjekten auswählt.

Die `dotnet`-Reihe von Monikern sollte in NuGet 3.3 und früher verwendet werden. Die `netstandard`-Monikersyntax sollte in Version 3.4 und höher verwendet werden.

## <a name="portable-class-libraries"></a>Portable Klassenbibliotheken

> [!Warning]
> **Portable Klassenbibliotheken werden nicht empfohlen.** Obwohl portable Klassenbibliotheken unterstützt werden, sollten Paketersteller stattdessen netstandard unterstützen. Der .NET Plattform-Standard ist eine Weiterentwicklung der PCLs und stellt binäre Portabilität plattformübergreifend mit einem einzelnen Moniker, der an eine statische Bibliothek wie gebunden ist nicht *tragbaren-a + b + c* Moniker.

Verwenden Sie zum Definieren eines Zielframeworks, das auf mehrere untergeordnete Zielframeworks verweist, das `portable`-Schlüsselwort, um der Liste der Frameworks, auf die verwiesen wird, ein Präfix hinzuzufügen. Vermeiden Sie das künstliche Hinzufügen von zusätzlichen Frameworks, die nicht direkt kompiliert werden, da dies zu unbeabsichtigten Nebeneffekten bei diesen Frameworks führen kann.

Zusätzliche Frameworks, die von Drittanbietern definiert wurden, sind mit anderen Umgebungen kompatibel, auf die auf diese Weise zugegriffen werden kann. Darüber hinaus gibt es Kurzformen für verfügbare Profilnummern, die auf diese Kombinationen von verknüpften Frameworks als `Profile#` verweisen. Es wird jedoch nicht empfohlen, diese Nummern zu verwenden, da dadurch die Lesbarkeit der Ordner und `.nuspec`-Dateien reduziert wird.

| Profil # | Frameworks | Vollständiger Name | .NET-Standard |
 --- | --- | --- | ---
 Profile2 | .NETFramework 4.0 | portable-net40+win8+sl4+wp7 |
 | | Windows 8.0 | |
 | | Silverlight 4.0 |
 | | WindowsPhone 7.0|
 Profile3 | .NETFramework 4.0 | portable-net40+sl4
 | | Silverlight 4.0 |
 Profile4 | .NETFramework 4.5 | portable-net45+sl4+win8+wp7
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 7.0 |
 Profile5 | .NETFramework 4.0 | portable-net40+win8
 | | Windows 8.0 |
 Profile6 | .NETFramework 4.0.3 | portable-net403+win8
 | | Windows 8.0 |
 Profile7 | .NETFramework 4.5 | portable-net45+win8 | netstandard1.1
 | | Windows 8.0 |
 Profile14 | .NETFramework 4.0 | portable-net40+sl5
 | | Silverlight 5.0 |
 Profile18 | .NETFramework 4.0.3 | portable-net403+sl4
 | | Silverlight 4.0 |
 Profile19 | .NETFramework 4.0.3 | portable-net403+sl5
 | | Silverlight 5.0 |
 Profile23 | .NETFramework 4.5 | portable-net45+sl4
 | | Silverlight 4.0 |
 Profile24 | .NETFramework 4.5 | portable-net45+sl5
 | | Silverlight 5.0 |
 Profile31 | Windows 8.1 | portable-win81+wp81 | netstandard1.0
 | | WindowsPhone 8.1 (SL) |
 Profile32 | Windows 8.1 | portable-win81+wpa81 | netstandard1.2
 | | WindowsPhone 8.1 (UWP) |
 Profile36 | .NETFramework 4.0 | portable-net40+sl4+win8+wp8
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profile37 | .NETFramework 4.0 | portable-net40+sl5+win8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 Profile41 | .NETFramework 4.0.3 | portable-net403+sl4+win8
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 Profile42 | .NETFramework 4.0.3 | portable-net403+sl5+win8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 Profile44 | .NETFramework 4.5.1 | portable-net451+win81 | netstandard1.2
 | | Windows 8.1 |
 Profile46 | .NETFramework 4.5 | portable-net45+sl4+win8
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 Profile47 | .NETFramework 4.5 | portable-net45+sl5+win8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 Profile49 | .NETFramework 4.5 | portable-net45+wp8 | netstandard1.0
 | | WindowsPhone 8.0 (SL) |
 Profile78 | .NETFramework 4.5 | portable-net45+win8+wp8 | netstandard1.0
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profile84 | WindowsPhone 8.1 | portable-wp81+wpa81 | netstandard1.0
 | | WindowsPhone 8.1 (UWP) |
 Profile88 | .NETFramework 4.0 | portable-net40+sl4+win8+wp75
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 7.5 |
 Profile92 | .NETFramework 4.0 | portable-net40+win8+wpa81
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 Profile95 | .NETFramework 4.0.3 | portable-net403+sl4+win8+wp7
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 7.0 |
 Profile96 | .NETFramework 4.0.3 | portable-net403+sl4+win8+wp75
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 7.5 |
 Profile102 | .NETFramework 4.0.3 | portable-net403+win8+wpa81
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 Profile104 | .NETFramework 4.5 | portable-net45+sl4+win8+wp75
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 7.5 |
 Profile111 | .NETFramework 4.5 | portable-net45+win8+wpa81 | netstandard1.1
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 Profile136 | .NETFramework 4.0 | portable-net40+sl5+win8+wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profile143 | .NETFramework 4.0.3 | portable-net403+sl4+win8+wp8
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profile147 | .NETFramework 4.0.3 | portable-net403+sl5+win8+wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profile151 | NETFramework 4.5.1 | portable-net451+win81+wpa81 | netstandard1.2
 | | Windows 8.1 |
 | | WindowsPhone 8.1 (UWP) |
 Profile154 | .NETFramework 4.5 | portable-net45+sl4+win8+wp8
 | | Silverlight 4.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profile157 | Windows 8.1 | portable-win81+wp81+wpa81 | netstandard1.0
 | | WindowsPhone 8.1 (SL) |
 | | WindowsPhone 8.1 (UWP) |
 Profile158 | .NETFramework 4.5 | portable-net45+sl5+win8+wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.0 (SL) |
 Profile225 | .NETFramework 4.0 | portable-net40+sl5+win8+wpa81
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 Profile240 | .NETFramework 4.0.3 | portable-net403+sl5+win8+wpa8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 Profile255 | .NETFramework 4.5 | portable-net45+sl5+win8+wpa81
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 Profile259 | .NETFramework 4.5 | portable-net45+win8+wpa81+wp8 | netstandard1.0
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 | | WindowsPhone 8.0 (SL) |
 Profile328 | .NETFramework 4.0 | portable-net40+sl5+win8+wpa81+wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 | | WindowsPhone 8.0 (SL) |
 Profile336 | .NETFramework 4.0.3 | portable-net403+sl5+win8+wpa81+wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 | | WindowsPhone 8.0 (SL) |
 Profile344 | .NETFramework 4.5 | portable-net45+sl5+win8+wpa81+wp8
 | | Silverlight 5.0 |
 | | Windows 8.0 |
 | | WindowsPhone 8.1 (UWP) |
 | | WindowsPhone 8.0 (SL) |

Darüber hinaus können NuGet-Pakete, die Xamarin anzielen, zusätzliche für Xamarin definierte Frameworks verwenden. Weitere Informationen finden Sie unter [Creating NuGet packages for Xamarin (Erstellen von NuGet-Paketen für Xamarin)](https://developer.xamarin.com/guides/cross-platform/advanced/nuget/).

| name | Beschreibung | .NET-Standard |
| --- | --- | ---
| monoandroid | Mono-Unterstützung für Android | netstandard1.4 |
| monotouch | Mono-Unterstützung für iOS | netstandard1.4 |
| monomac | Mono-Unterstützung für OSX | netstandard1.4 |
| xamarinios | Xamarin-Unterstützung für iOS | netstandard1.4 |
| xamarinmac | Xamarin-Unterstützung für Mac | netstandard1.4 |
| xamarinpsthree | Xamarin-Unterstützung für Playstation 3 | netstandard1.4 |
| xamarinpsfour | Xamarin-Unterstützung für Playstation 4 | netstandard1.4 |
| xamarinpsvita | Xamarin-Unterstützung für PS Vita | netstandard1.4 |
| xamarinwatchos | Xamarin für watchOS | netstandard1.4 |
| xamarintvos | Xamarin für tvOS | netstandard1.4 |
| xamarinxboxthreesixty | Xamarin für Xbox 360 | netstandard1.4 |
| xamarinxboxone | Xamarin für Xbox One | netstandard1.4 |

> [!Note]
> Stephen Cleary hat ein Tool erstellt, das die unterstützten portablen Klassenbibliotheken (PCLs) auflistet. Dieses finden Sie in seinem Beitrag [Framework profiles in .NET (Frameworkprofile in .NET)](http://blog.stephencleary.com/2012/05/framework-profiles-in-net.html).
