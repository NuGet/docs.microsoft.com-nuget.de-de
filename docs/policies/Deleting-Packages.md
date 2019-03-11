---
title: Löschen von NuGet-Paketen von nuget.org
description: Richtlinien für die Aufhebung der Auflistung von Paketen auf nuget.org. Dauerhaftes Löschen wird nur unterstützt, wenn durch Pakete andere Richtlinien verletzt werden.
author: karann-msft
ms.author: karann
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 833f4a67bc75c5d650e85180b52ecd8f69218f15
ms.sourcegitcommit: 85bf94e0efcfcee1f914650bdc142309ef3e06d9
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/01/2019
ms.locfileid: "57196186"
---
# <a name="deleting-packages"></a>Löschen von Paketen

Das dauerhafte Löschen von Paketen wird von nuget.org nicht unterstützt. Andernfalls würden sämtliche Projekte nicht mehr funktionieren, je nach Verfügbarkeit des Pakets. Dies trifft insbesondere bei Buildworkflows zu, die mit der Paketwiederherstellung arbeiten.

Nuget.org unterstützt jedoch das *Aufheben der Auflistung* eines Pakets. Dieser Vorgang kann auf der Website über die Seite zur Paketverwaltung durchgeführt werden. Nicht aufgelistete Pakete werden weder auf nuget.org noch auf der Benutzeroberfläche von Visual Studio angezeigt. Sie erscheinen auch nicht in den Suchergebnissen. Nicht aufgelistete Pakete können jedoch weiterhin mithilfe einer genauen Versionsnummer, die die Paketwiederherstellung unterstützt, heruntergeladen und installiert werden. Darüber hinaus können nicht aufgelistete Pakete in folgenden spezifischen Szenarios ggf. noch gefunden werden:

- Bei Paketwiederherstellung mithilfe von übergreifenden Versionen (z.B. `1.0.0-*`), wenn das neueste verfügbare Paket, das den Versions- oder Abhängigkeitseinschränkungen entspricht, ein nicht aufgelistetes Paket ist
- Replikation von Paketen durch den Katalog, da der Katalog ebenfalls nicht aufgelistete Pakete enthält

## <a name="exceptions"></a>Ausnahmen

In Ausnahmefällen, wie Urheberrechtsverletzungen und möglichen schädlichen Inhalten, können Pakete vom NuGet-Team auch manuell gelöscht werden. Sie können auf NuGet.org ein Paket auf der zugehörigen Detailseite durch Klick auf die Schaltfläche „Report abuse“ (Missbrauch melden) melden. Wenn Sie der Paketbesitzer sind, melden Sie sich bei Ihrem Konto auf NuGet.org an, um auf der Detailseite über die Schaltfläche „Contact support“ (Support kontaktieren) den Support zu kontaktieren.

## <a name="prohibited-use"></a>Unzulässige Verwendung

Pakete, auf die eines der folgenden Kriterien zutrifft, sind im öffentlichen NuGet-Katalog nicht erlaubt und werden daher umgehend entfernt. Die Besitzer der Pakete werden jedoch darüber informiert.

- Enthält Schadsoftware, Adware oder jegliche Art von Spyware
- Wurde entwickelt, um die Arbeitsstation eines Entwicklers oder dessen Organisation zu schädigen
- Verstößt gegen Urheberrechte oder verletzt Lizenzen
- Enthält illegale Inhalte
- Pakete, die nur dazu gedacht sind, Paketbezeichner zu belegen. Dazu zählen auch Pakete, die keinerlei produktiven Inhalt aufweisen. Pakete müssen Code enthalten. Andernfalls müssen die Besitzer den Bezeichner an jemanden abtreten, der tatsächlich ein Produkt anbieten möchte.
- Dient dem Versuch, dem Katalog Funktionen hinzuzufügen, die dessen Entwickler nicht explizit vorgesehen haben.

Wenn Sie bei einem Paket feststellen, dass ein Verstoß gegen einen oder mehrere dieser Punkte vorliegt, können Sie auf der Seite „Paketdetails“ auf den Link **Missbrauch melden** klicken und dies melden.

Beachten Sie, dass sich das NuGet-Team und .NET Foundation das Recht vorbehalten, diese Kriterien jederzeit zu ändern.
