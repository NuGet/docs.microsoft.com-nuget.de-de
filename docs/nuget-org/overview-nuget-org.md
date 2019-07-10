---
title: Übersicht über NuGet.org
description: Übersicht über NuGet.org
author: mikejo5000
ms.author: mikejo
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 9a75ecbc589afa664e5684005e077b02913e8039
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/28/2019
ms.locfileid: "67427015"
---
# <a name="overview-of-nugetorg"></a>Übersicht über NuGet.org

NuGet.org ist ein öffentlicher Host für NuGet-Pakete, der täglich von Millionen von .NET- und .NET Core-Entwicklern genutzt wird.

## <a name="role-of-nugetorg-in-the-nuget-ecosystem"></a>Rolle von NuGet.org im NuGet-Ökosystem

In seiner Rolle als öffentlicher Host verwaltet NuGet selbst das zentrale Repository von über 100.000 eindeutigen Paketen auf [nuget.org](https://www.nuget.org). NuGet.org ist jedoch nicht der einzige mögliche Host für Pakete. Mit der NuGet-Technologie können Sie auch Pakete privat in der Cloud (z.B. in Azure DevOps), in einem privaten Netzwerk oder sogar nur auf Ihrem lokalen Dateisystem hosten. Wenn Sie an einem anderen Host oder einer anderen Hostingoption interessiert sind, finden Sie weitere Informationen unter [Hosten eigener NuGet-Feeds](../hosting-packages/overview.md).

NuGet.org dient, wie jeder andere Host für NuGet-Pakete, als Verbindungspunkt zwischen *Paketerstellern* und *Paketconsumern*. Paketersteller erstellen nützliche NuGet-Pakete und veröffentlichen sie. Benutzer suchen dann nach nützlichen und kompatiblen Paketen auf zugänglichen Hosts, laden diese Pakete herunter und schließen sie in Ihre Projekte ein. Nach der Installation in einem Projekt sind die Paket-APIs für den restlichen Projektcode verfügbar.

![Beziehung zwischen Paketerstellern, Pakethosts und Paketbenutzer](media/nuget-roles.png)

## <a name="accounts"></a>Konten

Um Pakete auf NuGet.org zu veröffentlichen, erstellen Sie zunächst ein [individuelles Benutzerkonto](individual-accounts.md). Dieses Konto ist Ihre Identität auf NuGet.org.

NuGet.org ermöglicht außerdem das Erstellen von [Organisationskonten](organizations-on-nuget-org.md). Ein Organisationskonto umfasst mehrere Einzelkonten als Mitglieder. Diese Mitglieder können einen Paketsatz verwalten und hierbei eine einzige Identität für den Besitz nutzen. Durch Ihr individuelles Konto können Sie Mitglied in einer beliebigen Anzahl von Organisationen sein.

Ein Paket kann einem Organisationskonto ebenso angehören wie einem individuellen Konto. Paketconsumer erkennen keinen Unterschied zwischen einem individuellen Konto oder dem Organisationskonto: beide werden als Paket `owners` angezeigt.

## <a name="api-keys"></a>API-Schlüssel

Sobald Sie über ein NuGet-Paket ( *.nupkg*-Datei) für die Veröffentlichung verfügen, können Sie es zusammen mit einem von NuGet.org abgerufenen [API-Schlüssel](scoped-api-keys.md) entweder über die nuget.exe-CLI oder die dotnet.exe-CLI veröffentlichen.

Wenn Sie ein [Paket veröffentlichen](../create-packages/creating-a-package.md), schließen Sie den API-Schlüsselwert in den CLI-Befehl ein.

## <a name="id-prefixes"></a>ID-Präfixe

Wenn Sie Pakete veröffentlichen, können Sie Ihre Identität durch das [Reservieren von ID-Präfixen](id-prefix-reservation.md) schützen. Paketconsumer erhalten beim Installieren eines Pakets zusätzliche Informationen und werden darauf hingewiesen, dass das genutzte Paket hinsichtlich identifizierender Eigenschaften eindeutig ist.

## <a name="api-endpoint-for-nugetorg"></a>API-Endpunkt für NuGet.org

Um NuGet.org als Paketrepository mit NuGet-Clients verwenden zu können, müssen Sie den folgenden V3-API-Endpunkt verwenden: 

`https://api.nuget.org/v3/index.json`

Ältere Clients können weiterhin das V2-Protokoll verwenden, um NuGet.org zu erreichen. Beachten Sie jedoch, dass NuGet-Clients der Version 3.0 oder höher mit dem V2-Protokoll einen langsameren und weniger zuverlässigen Dienst in Kauf nehmen müssen:

`https://www.nuget.org/api/v2` (**Das V2-Protokoll ist veraltet!** )
