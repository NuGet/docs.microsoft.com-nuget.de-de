---
title: Übersicht über das NuGet-Ökosystem
description: Umfassende Ressourcen im NuGet-Ökosystem, einschließlich NuGet-Quellen, NuGet-Projekte von Drittanbietern, Hilfsprogramme und Schulungsmaterialien.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 52edc29fe8e9ec8927844a71a01e4983e47b1ce0
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818177"
---
# <a name="an-overview-of-the-nuget-ecosystem"></a>Übersicht über das NuGet-Ökosystem

Seit NuGet im Jahr 2010 veröffentlicht wurde, stellt es eine wichtige Möglichkeit dar, verschiedene Aspekte des Entwicklungsprozesses zu verbessern und zu automatisieren.

Da es sich bei NuGet um ein Open Source-Produkt unter der freizügigen [Apache v2-Lizenz](http://choosealicense.com/licenses/apache/) handelt, können andere Projekte NuGet nutzen, und Unternehmen können die Unterstützung dafür in ihre Produkte einbauen. Es spielt keine Rolle, ob Sie Open Source-Projekte oder Unternehmensanwendungen entwickeln, denn NuGet und andere Anwendungen, die auf NuGet basieren oder damit zusammenarbeiten, stellen ein vielseitiges Ökosystem an Tools bereit, die den Prozess der Softwareentwicklung verbessern.

All diese Projekte sind auch für Innovationen offen, da Entwickler Beiträge dazu leisten können. Leisten Sie Ihren Beitrag zu diesen Projekten und zu NuGet, indem Sie Fehler melden und Ideen für neue Funktionen mit uns teilen sowie Feedback geben, Dokumentation schreiben und, sofern möglich, Code bereitstellen.

## <a name="net-foundation-projects"></a>.NET Foundation-Projekte

NuGet stellt ein kostenloses Open Source-Paketverwaltungssystem für die Microsoft-Entwicklungsplattform bereit. Dieses System besteht aus einigen Clienttools und mehreren Diensten, die den [offiziellen NuGet-Katalog](http://www.nuget.org) umfassen. Zusammen bilden diese Komponenten das NuGet-Projekt, das von [.NET Foundation](http://www.dotnetfoundation.org/) verwaltet wird.

Die NuGet-Organisation enthält verschiedene Repositorys auf GitHub. Unter [https://github.com/Nuget/Home](https://github.com/Nuget/Home) finden Sie eine Übersicht aller Repositorys und Speicherorte der verschiedenen NuGet-Komponenten.

## <a name="microsoft-projects"></a>Microsoft-Projekte

Microsoft hat umfassend zu der Entwicklung von NuGet beigetragen. Alle von Microsoft-Mitarbeitern zur Verfügung gestellten Beiträge sind ebenfalls als Open Source-Komponenten verfügbar und wurden einschließlich des Copyrights an .NET Foundation gespendet.

## <a name="non-microsoft-projects"></a>Projekte von Drittanbietern

Viele andere Personen und Unternehmen haben wichtige Beiträge zu dem NuGet-Ökosystem geleistet. Alle im Folgenden aufgelisteten Projekte verfügen ggf. über andere Lizenzen als die Kernkomponenten von NuGet. Prüfen Sie daher vor der Verwendung die Lizenzbedingungen:

- [AppVeyor CI](https://www.appveyor.com/)
- [Artifactory](https://www.jfrog.com/artifactory/)
- [BoxStarter](http://boxstarter.org/)
- [Chocolatey](https://chocolatey.org/)
- [CoApp](http://coapp.org/)
- [JetBrains ReSharper](https://resharper-plugins.jetbrains.com/)
- [JetBrains TeamCity](https://www.jetbrains.com/teamcity/)
- [Klondike](https://github.com/themotleyfool/Klondike)
- [MinimalNugetServer](https://github.com/TanukiSharp/MinimalNugetServer)
- [MyGet (oder NuGet-as-a-Service)](http://www.myget.org/)
- [NuGet-Paket-Explorer](https://github.com/NuGetPackageExplorer/NuGetPackageExplorer)
- [NuGet Server](http://nugetserver.net/)
- [OctopusDeploy](https://octopus.com/)
- [Paket](https://fsprojects.github.io/Paket/)
- [ProGet (Inedo)](http://inedo.com/proget)
- [scriptcs](http://scriptcs.net/)
- [SharpDevelop](http://community.sharpdevelop.net/blogs/mattward/archive/2011/01/23/NuGetSupportInSharpDevelop.aspx)
- [Sonatype Nexus](http://www.sonatype.com/nexus-repository-sonatype)
- [SymbolSource](http://www.symbolsource.org/Public)
- [Xamarin und MonoDevelop](https://github.com/mrward/monodevelop-nuget-addin)

## <a name="other-nuget-based-utilities"></a>Andere Hilfsprogramme, die auf NuGet basieren

Die folgenden Tools und Hilfsprogramme bauen auf NuGet auf:

- [Glimpse-Erweiterungen](http://getglimpse.com/Packages) (Plug-Ins sind Pakete)
- [NuGetMustHaves.com](http://nugetmusthaves.com/)
- [Orchard](http://www.orchardproject.net/) (CMS-Module werden von einem NuGet-Feed der Version 1 im Orchard-Katalog abgerufen).
- [Java-Implementierung vom NuGet-Server](http://jonnyzzz.com/blog/2012/03/07/nuget-server-in-pure-java/)
- [NuGetLatest](https://twitter.com/NuGetLatest) (Twitter-Bot, der neue Paketveröffentlichungen twittert)
- [DefinitelyTyped](http://definitelytyped.org/) ([Automatischer](https://github.com/DefinitelyTyped/NugetAutomation/) TypeScript-Typ [auf NuGet veröffentlichte Definitionen](http://www.nuget.org/packages?q=DefinitelyTyped))

## <a name="training-materials-and-references"></a>Schulungsmaterialien und Referenzen

Wenn Sie ein neues Tool oder eine neue Technologie verwenden, gibt es in der Regel eine Lernkurve. Die Verwendung von NuGet ist jedoch nicht besonders kompliziert, und jeder kann ohne Schwierigkeiten unmittelbar mit [der Verarbeitung von Paketen beginnen](../quickstart/use-a-package.md).

Trotzdem sollten Sie die folgenden Ressourcen lesen, wenn Sie (gute) Pakete erstellen und NuGet in automatisierten Build- und Bereitstellungsvorgängen verwenden möchten:

- [NuGet-Blog](http://blog.nuget.org/)
- [NuGet-Team auf Twitter unter @nuget](http://twitter.com/nuget)
- Bücher:
  - [Apress Pro NuGet (Pro NuGet von Apress)](http://bit.ly/ProNuGet)
  - [NuGet 2 Essentials (NuGet 2: Grundlagen)](http://www.amazon.com/NuGet-2-Essentials-Damir-Arh-ebook/dp/B00GTQD5M4)

## <a name="documentation-for-individual-packages"></a>Dokumentation für individuelle Pakete

Über [NuDoq](http://nudoq.org) werden direkter Zugriff auf, Updates für und die Dokumentation zu NuGet-Paketen bereitgestellt.

NuDoq ruft regelmäßig die neusten Paketupdates auf dem Katalogserver unter „nuget.org“ ab, entpackt und verarbeitet die Dokumentationsdateien aus der Bibliothek und aktualisiert die Website entsprechend.

## <a name="adding-your-project"></a>Hinzufügen Ihres Projekts

Wenn Sie über ein Projekt im NuGet-Ökosystem verfügen, senden Sie bitte einen Pull Request mit einer Bearbeitung dieser Seite. Dies würde eine enorme Hilfe darstellen.
