---
title: NuGet-Client-SDK
description: Die API sich entwickelnden und noch nicht dokumentiert, aber Beispiele stehen Dave Glicks-Blog.
author: karann-msft
ms.author: karann
ms.date: 01/09/2018
ms.topic: conceptual
ms.openlocfilehash: 8f96bf289e8121fd25262fb95c2f36dfc89045c5
ms.sourcegitcommit: 573af6133a39601136181c1d98c09303f51a1ab2
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/18/2019
ms.locfileid: "58911035"
---
# <a name="nuget-client-sdk"></a>NuGet-Client-SDK

> [!Note]
> Nicht zu verwechseln mit der [NuGet *Web* API](https://docs.microsoft.com/en-us/nuget/api/overview)

Die *NuGet-Client-SDK* bezieht sich auf eine Gruppe von Bibliotheken für .NET zentraler Punkt [NuGet.Commands](https://www.nuget.org/packages/NuGet.Commands), [Nuget.Packaging](https://www.nuget.org/packages/NuGet.Packaging), und [NuGet.Protocol](https://www.nuget.org/packages/NuGet.Protocol). Diese Pakete ersetzt die frühere [NuGet.Core](https://www.nuget.org/packages/NuGet.Core/) Bibliothek.

Wir arbeiten, haben Sie eine stabile Oberfläche, die wir in Kürze dokumentiert werden können.

## <a name="source-code"></a>Quellcode

Der Quellcode ist im Projekt auf GitHub veröffentlichten [NuGet/NuGet.Client](https://github.com/NuGet/NuGet.Client).

## <a name="third-party-documentation"></a>Drittanbieter-Dokumentation

Sie finden Beispiele und Dokumentation für einige der API in den folgenden Blog von Dave Glick, 2016 veröffentlicht:

- [Untersuchen die NuGet-v3-Bibliotheken, Teil 1: Einführung und Konzepte](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-1)
- [Untersuchen die NuGet-v3-Bibliotheken, Teil 2: Pakete werden gesucht](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-2)
- [Untersuchen die NuGet-v3-Bibliotheken, Teil 3: Installieren von Paketen](http://daveaglick.com/posts/exploring-the-nuget-v3-libraries-part-3)

> [!Note]
> Diese Blogbeiträge wurde kurz nach der **3.4.3** Version des NuGet Client-SDK-Pakete wurden veröffentlicht.
> Neuere Versionen der Pakete möglicherweise nicht kompatibel mit den Informationen in den Blogbeiträgen.

Martin Björkström hat einen Blogbeitrag zur nachverfolgung Dave Glicks Blog-Reihe, in denen führt er eines anderen Ansatzes zur Verwendung des NuGet-Client-SDK für die Installation von NuGet-Pakete:

- [Öffnen Sie erneut die NuGet-v3-Bibliotheken](https://martinbjorkstrom.com/posts/2018-09-19-revisiting-nuget-client-libraries)
