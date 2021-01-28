---
title: Benutzerdatenanforderungen
description: Richtlinien zum Anfordern von Benutzerdatenexport und -löschung
author: JonDouglas
ms.author: jodou
ms.date: 05/01/2018
ms.topic: conceptual
ms.openlocfilehash: e0ec429469a992c9558d1635890fd568398206a1
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775720"
---
# <a name="user-data-requests"></a>Benutzerdatenanforderungen

Benutzer von nuget.org können Anforderungen zum Löschen von Informationen und Exportanforderungen über [nuget.org](https://www.nuget.org) senden. Beide Typen werden in Form von Supportanfragen übermittelt und müssen von den nuget.org-Administratoren innerhalb von 30 Tagen ausgeführt werden.

Auf die folgenden Benutzerdaten kann über nuget.org direkt zugegriffen werden:

* Kontobezogene Daten, z.B. E-Mail-Adresse, Anmeldekonto, Profilfoto und Einstellungen für E-Mail-Benachrichtigungen
* Im Besitz befindliche API-Schlüssel
* Liste der im Besitz befindlichen Pakete

Diese Daten sind nicht in den Daten enthalten, die über die Supportanfrage exportiert werden.

## <a name="identifying-customer-data"></a>Identifizieren von Kundendaten

Kundendaten können als nuget.org-Benutzerkontonamen identifiziert werden.

## <a name="deleting-customer-data"></a>Löschen von Kundendaten

So fordern Sie das Löschen von Benutzerdaten von nuget.org an:

1. Der Benutzer muss sich bei [nuget.org](https://www.nuget.org) anmelden.
1. Der Benutzer muss eine Anforderung zum Löschen seines Kontos an [nuget.org/account/delete](https://www.nuget.org/account/delete) übermitteln.

Benutzern, die alleinige Besitzer von Paketen sind, wird empfohlen, neue Besitzer zu finden, bevor Sie um die Löschung ihres Kontos bitten. Wenn der Paketbesitz nicht übertragen wird, wird das NuGet-Paket aus der Liste entfernt und ist daher in Suchabfragen in Visual Studio oder auf der nuget.org-Website nicht mehr verfügbar. Vor dem Löschen des Kontos arbeiten die nuget.org-Administratoren mit dem Benutzer zusammen, um neue Besitzer für die Pakete zu finden, die er besitzt.

Die Löschaktion des Kontos wird vom nuget.org-Administrator innerhalb von 30 Tagen ab dem Datum der Anforderung abgeschlossen.

Bei der Kontolöschung werden alle Daten des Benutzers aus dem nuget.org-System entfernt, und die folgenden Aktionen werden ausgeführt:

* Die Registrierung des gelöschten Kontos bei nuget.org wird aufgehoben.
* Alle API-Schlüssel im Besitzt werden gelöscht.
* Alle reservierten Namespaces werden freigegeben.
* Jeglicher Paketbesitz wird entfernt.

Die im Besitz befindlichen Pakete werden *nicht* gelöscht. Obwohl sie in den Suchergebnissen nicht mehr aufgeführt werden, bleiben sie über die Paketwiederherstellung für Projekte verfügbar, die von ihnen abhängen.

## <a name="exporting-customer-data"></a>Exportieren von Kundendaten

Nach der Anmeldung bei nuget.org kann ein Benutzer eine Exportanforderung über [nuget.org/policies/Contact](https://www.nuget.org/policies/Contact) übermitteln.

Die exportierten Daten werden dem Benutzer zum Herunterladen über ein Azure-Blob 48 Stunden lang zur Verfügung gestellt. Nach 48 Stunden läuft der Zugriff ab, und der Benutzer muss bei Bedarf eine neue Exportanforderung übermitteln.

Die exportierten Daten enthalten Folgendes:

* Die Supportanfragen des Benutzers
* Die Aktionen des Benutzers (Veröffentlichen eines Pakets, Erstellen eines Kontos,) wie in den Überwachungsprotokollen persistent gespeichert
* Alle Benutzerinformationen (wie in den IIS-Protokollen persistent gespeichert)
