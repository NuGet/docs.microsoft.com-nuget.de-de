---
title: Bereichsbezogene API-Schlüssel
description: Nehmen Sie Einstellungen für API-Schlüssel vor, die Sie zum Pushen von Paketen verwenden.
author: mikejo5000
ms.author: mikejo
ms.date: 06/04/2019
ms.topic: conceptual
ms.openlocfilehash: 12d12d5294a474c4d3e4f5d3cad468bb515d21d5
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/07/2020
ms.locfileid: "67426945"
---
# <a name="scoped-api-keys"></a>Bereichsbezogene API-Schlüssel

Sie können API-Schlüssel anhand von Bereichen einschränken, um NuGet eine sicherere Umgebung zur Verteilung von Paketen zu machen.

Wenn Sie Bereiche für Ihre API-Schlüssel festlegen können, können Sie Ihre APIs besser kontrollieren. Ihre Möglichkeiten:

- Sie können API-Schlüssel mit mehreren Bereichen erstellen, die für unterschiedliche Pakete mit verschiedenen Ablauffristen erstellt werden können.
- Sie können API-Schlüssel sicher erhalten.
- Sie können vorhandene API-Schlüssel bearbeiten, um die Anwendbarkeit des Pakets anzupassen.
- Sie können vorhandene API-Schlüssel aktualisieren oder löschen, ohne Vorgänge mit anderen Schlüsseln zu beeinträchtigen.

## <a name="why-do-we-support-scoped-api-keys"></a>Warum werden bereichsbezogene API-Schlüssel unterstützt?

Bereiche für API-Schlüssel werden unterstützt, damit Sie genauere Berechtigungen festlegen können. In der Vergangenheit hat NuGet einen API-Schlüssel für ein Konto zugelassen. Dieser Ansatz hatte mehrere Nachteile:

- **Ein API-Schlüssel für alle Pakete:** Mit einem API-Schlüssel zum Verwalten aller Pakete ist es schwer, den Schlüssel sicher zu teilen, wenn mehrere Entwickler mit verschiedenen Paketen involviert sind und ein Herausgeberkonto gemeinsam verwenden.
- **Entweder alle oder keine Berechtigungen:** Jeder Benutzer mit Zugriffsberechtigungen für den API-Schlüssel hat alle Berechtigungen (Veröffentlichen, Pushen und Aufheben der Auflistung). Das ist in Umgebungen mit mehreren Teams oft unerwünscht.
- **Einzelne Fehlerquelle**. Ein einziger API-Schlüssel bedeutet auch ein Single Point of Failure. Wenn der Schlüssel kompromittiert wird, sind auch alle Pakete, die mit dem Konto verknüpft sind, potenziell kompromittiert. Diese Bedrohung kann nur durch eine Änderung des API-Schlüssels behoben werden. Zudem kann nur so eine Unterbrechung Ihres CI/CD-Workflows vermieden werden. Darüber hinaus kann es Fälle geben, in denen Sie den Zugriff auf den API-Schlüssel für eine Einzelperson widerrufen möchten (wenn z. B. ein Angestellter die Organisation verlässt). Das kann momentan noch nicht unkompliziert gelöst werden.

Mit bereichsbezogenen API-Schlüsseln möchten wir diese Probleme beheben und gleichzeitig sicherstellen, dass keine der bestehenden Workflows beeinträchtigt werden.

## <a name="acquire-an-api-key"></a>Erhalten eines API-Schlüssels

[!INCLUDE [publish-api-key](../quickstart/includes/publish-api-key.md)]

## <a name="create-scoped-api-keys"></a>Erstellen eines bereichsbezogenen API-Schlüssels

Sie können mehrere API-Schlüssel basierend auf Ihren Umgebungen erstellen. Ein API-Schlüssel kann für eines oder mehrere Pakete gelten, mehrere Bereiche mit bestimmten Berechtigungen aufweisen und ein Ablaufdatum haben.

Im folgenden Beispiel wird der API-Schlüssel `Contoso service CI` verwendet, mit dem Pakete für bestimmte `Contoso.Service`-Pakete gepusht werden können und der 365 Tage gültig ist. Das ist ein typisches Beispiel, bei dem verschiedene Teams in derselben Organisation an verschiedenen Paketen arbeiten und die Teammitglieder den Schlüssel bereitstellen, durch den sie Berechtigungen für das Paket haben, an dem sie arbeiten. Durch die Ablauffrist werden alte oder vergessene Schlüssel vermieden.

![Erstellen von API-Schlüsseln](media/scoped-api-keys-create-new.png)

## <a name="use-glob-patterns"></a>Verwenden von Globmustern

Wenn Sie mit mehreren Paketen arbeiten und eine lange Liste mit Paketen verwalten müssen, können sie Globmuster verwenden, um mehrere Pakete auf einmal auszuwählen. Wenn sie z. B. einem Schlüssel für alle Pakete, deren ID mit `Fabrikam.Service` beginnt, bestimmte Bereiche zuweisen möchten, können Sie dazu `fabrikam.service.*` im Textfeld **Glob pattern** (Globmuster) angeben.

![Erstellen von API-Schlüsseln](media/scoped-api-keys-glob-pattern.png)

Das Verwenden von Globmustern zum Bestimmen von API-Schlüssel-Berechtigungen gilt auch für neue Pakete, die mit dem Globmuster übereinstimmen. Wenn Sie z. B. versuchen, ein neues Paket mit dem Namen `Fabrikam.Service.Framework` zu pushen, können Sie dies mit dem vormals erstellten Schlüssel tun, da das Paket mit dem Globmuster `fabrikam.service.*` übereinstimmt.

## <a name="obtain-api-keys-securely"></a>Sicheren Abrufen von API-Schlüsseln

Aus Sicherheitsgründen wird ein neu erstellter Schlüssel niemals angezeigt und kann nur über die Schaltfläche **Copy** (Kopieren) verwendet werden. Gleichfalls können Sie nicht mehr auf den Schlüssel zugreifen, nachdem die Seite aktualisiert wurde.

![Erstellen von API-Schlüsseln](media/scoped-api-keys-obtain-keys.png)

## <a name="edit-existing-api-keys"></a>Bearbeiten vorhandener API-Schlüssel

Sie sollten auch die Schlüsselberechtigungen und Bereiche aktualisieren, ohne den Schlüssel an sich zu ändern. Wenn Sie einen Schlüssel mit einem bestimmten Bereich oder bestimmten Bereichen für ein einzelnes Paket haben, können Sie denselben Bereich oder dieselben Bereichen auf eines oder mehrere andere Pakete anwenden.

![Erstellen von API-Schlüsseln](media/scoped-api-keys-edit.png)

## <a name="refresh-or-delete-existing-api-keys"></a>Aktualisieren oder Löschen vorhandener API-Schlüssel

Der Kontobesitzer kann den Schlüssel aktualisieren. In diesem Fall bleiben die Berechtigungen der Pakete, der Bereich und das Ablaufdatum dieselben, aber es wird ein neuer Schlüssel erstellt, sodass der alte nicht mehr verwendet werden kann. Das ist beim Verwalten veralteter Schlüssel oder bei einem potenziellen API-Schlüsselverlust nützlich.

![Erstellen von API-Schlüsseln](media/scoped-api-keys-refresh.png)

Sie können diese Schlüssel auch löschen, wenn Sie sie nicht mehr benötigen. Wenn Sie den Schlüssel löschen, kann er nicht mehr verwendet werden.

## <a name="faqs"></a>Häufig gestellte Fragen

### <a name="what-happens-to-my-old-legacy-api-key"></a>Was geschieht mit meinem alten (Legacy-)API-Schlüssel?

Ihr alter (Legacy-)API-Schlüssel funktioniert auch weiterhin, solange Sie Ihn benötigen. Diese Schlüssel werden entfernt, wenn sie mehr als 365 Tage nicht mehr zum Pushen von Paketen verwendet wurden. Weitere Informationen finden Sie im Blogbeitrag [Changes to expiring API keys (Änderungen an ablaufenden API-Schlüsseln)](https://blog.nuget.org/20160825/Changes-to-Expiring-API-Keys.html). Sie können diesen Schlüssel nicht mehr aktualisieren. Sie müssen den Legacyschlüssel löschen oder stattdessen einen bereichsbezogenen Schlüssel erstellen.

> [!NOTE]
> Dieser Schlüssel hat alle Berechtigungen für alle Pakete, und er läuft nicht ab. Überlegen Sie sich, ob Sie diesen Schlüssel löschen und neue Schlüssel mit bereichsbezogenen Berechtigungen und Ablauffristen erstellen möchten.

### <a name="how-many-api-keys-can-i-create"></a>Wie viele API-Schlüssel kann ich erstellen?

Sie können unendlich viele API-Schlüssel erstellen. Es wird jedoch empfohlen, es bei einer übersichtlichen Anzahl zu belassen, damit Sie sich nicht um zu viele veraltete Schlüssel kümmern müssen, ohne zu wissen, wo und von wem sie eingesetzt werden.

### <a name="can-i-delete-my-legacy-api-key-or-discontinue-using-now"></a>Kann ich meine Legacy-API-Schlüssel löschen oder aufhören, sie zu verwenden?

Ja. Sie können – und sollten – ihre Legacy-API-Schlüssel löschen.

### <a name="can-i-get-back-my-api-key-that-i-deleted-by-mistake"></a>Kann ich API-Schlüssel wiederherstellen, die ich versehentlich gelöscht habe?

Nein. Wenn Sie einen Schlüssel gelöscht haben, können Sie nur neue Schlüssel erstellen. Es gibt keine Wiederherstellungsmöglichkeit für versehentlich gelöschte Schlüssel.

### <a name="does-the-old-api-key-continue-to-work-upon-api-key-refresh"></a>Funktioniert der alte API-Schlüssel weiterhin, wenn ich den API-Schlüssel aktualisiere?

Nein. Wenn Sie einen Schlüssel aktualisieren, wird ein neuer Schlüssel mit demselben Bereich, denselben Berechtigungen und demselben Ablaufdatum wie der alte Schlüssel generiert. Der alte Schlüssel existiert nicht mehr.

### <a name="can-i-give-more-permissions-to-an-existing-api-key"></a>Kann ich einem vorhandenen API-Schlüssel mehr Berechtigungen zuweisen?

Sie können den Bereich nicht anpassen, aber Sie können die Paketliste bearbeiten, für die er gilt.

### <a name="how-do-i-know-if-any-of-my-keys-expired-or-are-getting-expired"></a>Wie kann ich bestimmen, ob einer meiner Schlüssel abgelaufen ist oder bald abläuft?

Wenn ein Schlüssel abläuft, wird eine Warnmeldung am oberen Rand der Seite angezeigt. Außerdem erhält der Kontobesitzer zehn Tage vor Ablauf des Schlüssels eine Warnung per E-Mail, sodass er entsprechende Maßnahmen einleiten kann.