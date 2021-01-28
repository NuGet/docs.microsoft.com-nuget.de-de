---
title: Löschen von NuGet-Paketen von nuget.org
description: Richtlinien für die Aufhebung der Auflistung von Paketen auf nuget.org. Dauerhaftes Löschen wird nur unterstützt, wenn durch Pakete andere Richtlinien verletzt werden.
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: e5c62177b40162cb8b6b37b0d272fb7a945156c1
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775707"
---
# <a name="deleting-packages"></a>Löschen von Paketen

Das dauerhafte Löschen von Paketen wird von nuget.org nicht unterstützt. Andernfalls würden sämtliche Projekte nicht mehr funktionieren, je nach Verfügbarkeit des Pakets. Dies trifft insbesondere bei Buildworkflows zu, die mit der Paketwiederherstellung arbeiten.

Nuget.org unterstützt jedoch das [Aufheben der Auflistung eines Pakets](#unlisting-a-package). Dieser Vorgang kann auf der Website über die Seite zur Paketverwaltung durchgeführt werden. Nicht aufgelistete Pakete werden weder auf nuget.org noch auf der Benutzeroberfläche von Visual Studio angezeigt. Sie erscheinen auch nicht in den Suchergebnissen. Nicht aufgelistete Pakete können jedoch weiterhin mithilfe einer genauen Versionsnummer, die die Paketwiederherstellung unterstützt, heruntergeladen und installiert werden. Darüber hinaus können nicht aufgelistete Pakete in folgenden spezifischen Szenarios ggf. noch gefunden werden:

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

Wenn Sie ein Paket finden, das gegen diese Regeln verstößt, klicken Sie auf der Seite „Paketdetails“ auf den Link **Missbrauch melden**, um einen Bericht zu übermitteln.

Beachten Sie, dass sich das NuGet-Team und .NET Foundation das Recht vorbehalten, diese Kriterien jederzeit zu ändern.

## <a name="unlisting-a-package"></a>Aufheben der Auflistung eines Pakets
Durch das Aufheben der Auflistung einer Paketversion wird diese bei der Suche und auf der Detailseite des Pakets auf nuget.org ausgeblendet. Dies ermöglicht es bestehenden Benutzern des Pakets, dieses weiterhin zu verwenden, reduziert aber die Anzahl neuer Benutzer des Pakets, da es bei der Suche nicht angezeigt wird.

Schritte zum Aufheben der Auflistung eines Pakets:

1. Klicken `Your account name` (Sie auf Ihren Kontonamen) (rechts oben in der Ecke) und anschließend auf `Manage packages` (Pakete verwalten) > `Published packages` (Veröffentlichte Pakete).
1. Klicken Sie auf das Symbol für „Manage package“ (Paket verwalten).
1. Klappen Sie den Bereich „Listing“ (Auflistung) auf, und klicken Sie auf die gewünschte Paketversion.
1. Deaktivieren Sie „List in search results“ (In Suchergebnissen aufführen), und klicken Sie auf „Speichern“.

Die Auflistung der ausgewählten Paketversion wurde nun aufgehoben. Melden Sie sich aus Ihrem Konto ab, und navigieren Sie zur Paketseite (ohne den Versionsteil), z. B. https://www.nuget.org/packages/YOUR-PACKAGE-NAME/, um dies zu überprüfen. Ihnen werden alle Versionen des Pakets angezeigt, für die die Auflistung **nicht** aufgehoben wurde. Der Paketbesitzer kann, wenn er angemeldet ist, allerdings alle Versionen und deren Auflistungsstatus sehen.

Es ist auch möglich, eine Paketversion als veraltet zu kennzeichnen (falls Sie diese nicht löschen können). Weitere Informationen zur Kennzeichnung von Paketversionen als veraltet finden Sie unter [Als veraltet gekennzeichnete Pakete](../deprecate-packages.md).
