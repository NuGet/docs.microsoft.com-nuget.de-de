---
title: "Konfliktlösung bei Namen von NuGet-Paketen | Microsoft-Dokumentation"
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 01/18/2018
ms.topic: article
ms.prod: nuget
ms.technology: 
description: Der Prozess zum Beilegen von Streitigkeiten zwischen Herausgebern von NuGet-Paketen, die im Zusammenhang mit Branding, Marken und anderen Konfliktsituationen stehen
keywords: Streitigkeiten wegen NuGet-Paketen, Beilegen von NuGet-Streitigkeiten, Prozess zum Beilegen von Streitigkeiten
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 589fe4e7d2b05f3d589dcc70e78e7199d7e717c8
ms.sourcegitcommit: 4651b16a3a08f6711669fc4577f5d63b600f8f58
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/02/2018
---
# <a name="resolving-disputes-over-nuget-package-names"></a>Auflösen von Konflikten im Zusammenhang mit den Namen von NuGet-Paketen

Dieser Artikel enthält Empfehlungen, wie Communitymitglieder beim Lösen von Konflikten mit anderen NuGet-Herausgebern vorgehen sollten.

Nehmen wir beispielsweise an, dass Northwind Traders ein CRM-System erstellt, für welches das Unternehmen auf seiner Website Clienttreiber in einer herunterladbaren MSI-Datei bereitstellt. Die unabhängige Entwicklerin Nancy möchte das Verwenden der Clientbibliothek von Northwind vereinfachen und erstellt daraus ein NuGet-Paket namens `NorthwindTraders.Client`. Später möchte Northwind selbst ein offizielles NuGet-Paket aus dieser Clientbibliothek erstellen und daher Nancy das Eigentumsrecht für jenen Paketnamen absprechen.

In diesem Szenario scheint Nancy nicht aus böser Absicht zu handeln, da sie ja Unterstützung für die Kunden und Tools von Northwind bietet, indem Sie den in ihrer Freizeit erstellten Code zur Verfügung stellt. Dennoch ist Northwind der rechtmäßige Besitzer des Namens „Northwind“.

Wenn beide Parteien wie unten beschrieben vorgehen, können sie gemeinsam eine geeignete Lösung erarbeiten. Schließlich sind beide ja daran interessiert, die Entwicklercommunity zu unterstützen. Es ist in der Regel nicht erforderlich, dass das NuGet-Team einschreitet; eine Kollaboration ist in den meisten Fällen die beste Lösung. Bisher wurde jeder Konflikt geklärt, bei dem das NuGet-Team eingeschaltet wurde, und zwar ohne, dass das Team überhaupt ein Urteil abgeben musste.

## <a name="process"></a>Prozess

1. Kontaktieren Sie auf der Seite „Paketdetails“ mithilfe des Links **Contact Owners** (Besitzer kontaktieren) die Besitzer des jeweiligen Pakets. Erläutern Sie Ihr Problem auf freundliche, aber unmissverständliche Art und Weise.
1. Senden Sie eine Kopie der Nachricht an [support@nuget.org](mailto:support@nuget.org), damit die für NuGet und .NET Foundation zuständigen Mitarbeiter über Ihren Streitfall informiert sind.
1. Warten Sie maximal 30 Tage darauf, dass der Streitfall entschieden wird, und benachrichtigen Sie andernfalls [support@nuget.org](mailto:support@nuget.org) erneut. Das Supportteam von nuget.org schaltet sich dann ein und arbeitet mit beiden Parteien am Beilegen der Streitigkeiten.
