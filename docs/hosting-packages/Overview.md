---
title: Überblick über das Hosten eigener NuGet-Feeds
description: Ein Überblick über die Möglichkeiten, eigene Feeds oder Kataloge für NuGet-Pakete lokal oder remote zu hosten
author: karann-msft
ms.author: karann
ms.date: 08/25/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 3ca023c8d39b9b36388f5f517b50ca5cd2347cc0
ms.sourcegitcommit: 39f2ae79fbbc308e06acf67ee8e24cfcdb2c831b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/05/2019
ms.locfileid: "73610454"
---
# <a name="hosting-your-own-nuget-feeds"></a>Hosten eigener NuGet-Feeds

Möglicherweise möchten Sie Ihre Pakete nur für einen eingeschränkten Personenkreis freigeben, z.B. Ihre Organisation oder Arbeitsgruppe, anstatt diese öffentlich verfügbar zu machen. Darüber hinaus möchten einige Unternehmen ggf. vorgeben, welche Bibliotheken von Drittanbietern ihre Entwickler verwenden. Daher weisen diese die Entwickler an, auf eine spezielle Paketquelle zurückzugreifen, anstatt auf nuget.org.

Zu diesen Zwecken unterstützt NuGet das Einrichten privater Paketquellen auf folgende Arten:

- Lokaler Feed: Pakete werden einfach an einem passenden Netzwerkfreigabeort abgelegt. Idealerweise wurde mithilfe von `nuget init` und `nuget add` eine hierarchische Ordnerstruktur angelegt (NuGet 3.3 und höher). Weitere Einzelheiten finden Sie unter [Lokale Feeds](../hosting-packages/local-feeds.md).
- NuGet.Server: Pakete werden über einen lokalen HTTP-Server verfügbar gemacht. Weitere Einzelheiten finden Sie unter [NuGet.Server](../hosting-packages/nuget-server.md).
- NuGet-Katalog: Pakete werden mithilfe von [NuGet Gallery Project (Projekt „NuGet-Katalog“)](https://github.com/NuGet/NuGetGallery#build-and-run-the-gallery-in-arbitrary-number-easy-steps) (github.com) auf einem Internet-Server gehostet. Der NuGet-Katalog bietet Benutzerverwaltung und diverse Funktionen, z.B. eine umfangreiche Webbenutzeroberfläche, die es ermöglicht, direkt im Browser nach Paketen zu suchen und sich diese näher anzusehen, ähnlich wie nuget.org.

Es gibt auch einige andere NuGet-Hostingprodukte wie [Azure Artifacts](https://www.visualstudio.com/docs/package/nuget/publish) und die [GitHub-Paketregistrierung](https://help.github.com/articles/configuring-nuget-for-use-with-github-package-registry), die private Remotefeeds unterstützen. Im Folgenden werden diese Produkte aufgelistet:

- [Artifactory](https://www.jfrog.com/artifactory/) von JFrog
- [Azure Artifacts](https://www.visualstudio.com/docs/package/nuget/publish), was auch auf Team Foundation Server 2017 und höher verfügbar ist.
- [BaGet](https://github.com/loic-sharma/BaGet), eine Open Source-Implementierung von NuGet-V3-Server, die auf ASP.NET Core basiert.
- [Cloudsmith](https://cloudsmith.io/l/nuget-feed/), eine vollständig verwaltete SaaS-Paketverwaltung
- [GitHub-Paketregistrierung](https://help.github.com/articles/configuring-nuget-for-use-with-github-package-registry)
- [LiGet](https://github.com/ai-traders/liget), eine Open Source-Implementierung von NuGet V2-Server, die unter Kestrel in Docker ausgeführt wird.
- [MyGet](https://myget.org)
- [Nexus](https://www.sonatype.org/nexus/) von Sonatype
- [NuGet Server (Open Source)](https://github.com/svenkle/nuget-server), eine Open-Source-Implementierung, die NuGet Server von Inedo ähnelt
- [NuGet Server](http://nugetserver.net/), ein Communityprojekt von Inedo
- [ProGet](https://inedo.com/proget) von Inedo
- [Sleet](https://github.com/emgarten/sleet), ein statischer Open-Source-NuGet V3-Feedgenerator
- [TeamCity](https://www.jetbrains.com/teamcity/) von JetBrains

Unabhängig davon, wie Pakete gehostet werden, können Sie auf diese zugreifen, indem Sie diese der Liste verfügbarer Datenquellen in `NuGet.Config` hinzufügen. Dies kann in Visual Studio ausgeführt werden, wie im Absatz zum Thema [Paketquellen](../consume-packages/install-use-packages-visual-studio.md#package-sources) beschrieben, oder über die Befehlszeile mithilfe von [`nuget sources`](../reference/cli-reference/cli-ref-sources.md). Bei dem Pfad zu einer Datenquelle kann es sich um einen Pfadnamen für einen lokalen Ordner, um einen Netzwerknamen oder eine URL handeln.
