---
title: Häufig gestellte Fragen zu NuGet.org
description: Häufige Fragen und zugehörige Antworten zur Arbeit mit dem NuGet-Katalog
author: shishirx34
ms.author: shishirh
ms.date: 06/05/2019
ms.topic: conceptual
ms.openlocfilehash: 915f6e4cfc0b21d2b10006c62e8230720d07ce74
ms.sourcegitcommit: e9c1dd0679ddd8ba3ee992d817b405f13da0472a
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/29/2020
ms.locfileid: "76813740"
---
# <a name="nugetorg-frequently-asked-questions"></a>Häufig gestellte Fragen zu NuGet.org

## <a name="license-terms"></a>Lizenzbedingungen

**Welche Lizenzbedingungen gelten standardmäßig, wenn ein Paket keine spezifischen Lizenzbedingungen bereitstellt?**

Jedes Paket unterliegt den im Paket enthaltenen Bestimmungen. Sie sollten die geltenden Bestimmungen überprüfen, bevor Sie Pakete erwerben, herunterladen oder auf diese zugreifen. Verwenden Sie den Link **License Info** (Lizenzinformationen) auf der Seite für Pakete auf NuGet.org.

Wenn ein Paket keine Lizenzbedingungen festlegt, kontaktieren Sie den Paketbesitzer direkt, indem Sie den Link **Contact owners** (Besitzer kontaktieren) auf der Seite für Pakete auf NuGet.org verwenden. Microsoft lizenziert kein geistiges Eigentum von Drittanbietern für Pakete und ist nicht verantwortlich für die durch Drittanbieter bereitgestellten Inhalte.

## <a name="managing-packages-on-nugetorg"></a>Verwalten von Paketen auf NuGet.org

**Können Paketmetadaten nach dem Upload bearbeitet werden?**

Es wird empfohlen, dass Sie alle Pakete für NuGet signieren. Ein Entwurfsprinzip der Paketsignierung besteht darin, dass signierte Paketinhalte unveränderlich sein müssen. Dies schließt die NUSPEC-Datei ein. Durch das Bearbeiten der Paketmetadaten wird die NUSPEC-Datei geändert, wodurch bestehende Signaturen ungültig werden. Es wird empfohlen, vorhandene Workflows zu ändern, damit das Bearbeiten der Paketmetadaten nach dem Erstellen des Pakets nicht erforderlich ist.

Beachten Sie, dass die für Ihr Paket aufgeführten Abhängigkeiten automatisch vom Paket generiert werden und nicht bearbeitet werden können.

Zusätzlich stellt das Hochladen von Paketen auf [int.nugettest.org](https://int.nugettest.org) eine gute Möglichkeit zum Testen und Überprüfen des Pakets dar, ohne dieses im öffentlichen Katalog zur Verfügung zu stellen. API-Endpunkt: https://apiint.nugettest.org/v3/index.json

**Kann ich ein Paket löschen, das auf NuGet.org veröffentlicht wurde?**

Im Allgemeinen wird das Löschen eines Pakets, das auf NuGet.org veröffentlicht wurde, nicht unterstützt. Weitere Informationen finden Sie in der [Richtlinie zum Löschen von Paketen](policies/deleting-packages.md).

**Ist es möglich, Namen für Pakete zu reservieren, die in Zukunft veröffentlicht werden sollen?**

Ja. Sie können IDs für Pakete auf [NuGet.org](https://www.nuget.org/) reservieren, indem Sie ein Präfix für eine Paket-ID für Ihr Konto anfordern. Wenn Sie ein Präfix für die Paket-ID anfordern möchten, folgen Sie den Anweisungen in der [Dokumentation](id-prefix-reservation.md).

**Wie kann der Besitz eines Pakets beansprucht werden?**

Weitere Informationen finden Sie unter [Verwalten von Paketbesitzern auf NuGet.org](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg).

**Wie kann vorgegangen werden, wenn ein Paketbesitzer meine Softwarelizenzbedingungen verletzt?**

Es wird empfohlen, dass die NuGet-Community zusammenarbeitet, um Streitfälle zwischen Paketbesitzern und den Besitzern von anderer Software zu klären. Es wurde eine [Vorgehensweise zum Lösen von Streitfällen](policies/dispute-resolution.md) entworfen, die Sie befolgen sollten, bevor Sie um das Eingreifen der Administratoren von NuGet.org bitten.

**Ist es empfehlenswert, meine Testpakete auf NuGet.org hochzuladen?**

Für Testzwecke können Sie [int.nugettest.org](https://int.nugettest.org) oder alternative öffentliche NuGet-Server wie [myget.org](https://myget.org) oder [Azure DevOps](https://blogs.msdn.microsoft.com/visualstudioalm/2015/08/27/announcing-package-management-support-for-vsotfs/) verwenden.

Beachten Sie, dass Pakete, die auf int.nugettest.org hochgeladen werden, nicht beibehalten werden.

**Was ist die maximale Größe für Pakete, die ich auf NuGet.org hochladen kann?**

Auf NuGet.org sind Pakete bis 250 MB zugelassen. Es wird jedoch empfohlen, die Pakete nach Möglichkeit kleiner als 1 MB zu halten und Abhängigkeiten zu verwenden, um die Pakete miteinander zu verknüpfen. Als Faustregel gilt, dass Pakete nur eine Assembly enthalten sollten, um Konflikte zu vermeiden.

NuGet verwendet HTTP zum Herunterladen von Paketen. Bei größeren Paketen ist es daher wahrscheinlicher als bei kleineren, dass die Installation fehlschlägt.

Es ist möglich, Abhängigkeiten zwischen mehreren Paketen freizugeben. Dadurch wird die Gesamtgröße des Downloads für die Nutzer Ihrer NuGet-Pakete reduziert.

Abhängigkeiten sind überwiegend statisch und ändern sich nie. Wenn Sie einen Fehler im Code beheben, müssen die Abhängigkeiten möglicherweise nicht aktualisiert werden. Wenn Sie Abhängigkeiten bündeln, werden die Pakete, die Sie erneut versenden müssen, jedes Mal größer. Indem Sie NuGet-Pakete in verknüpfte Abhängigkeiten aufteilen, wodurch präzisere Upgrades für die Nutzer Ihrer Pakete ermöglicht werden.

## <a name="nugetorg-not-accessible"></a>Auf NuGet.org kann nicht zugegriffen werden

**Warum kann ich keine Pakete auf NuGet.org hochladen oder von dort herunterladen?**

Stellen Sie zunächst sicher, dass Sie die aktuelle Version von NuGet verwenden. Wenn auch bei dieser Version Fehler auftreten, [kontaktieren Sie den Support](https://www.nuget.org/policies/Contact), und stellen Sie die folgenden zusätzlichen Informationen für die Problembehandlung der Verbindung zur Verfügung:

- Die von Ihnen verwendete NuGet-Version
- Die von Ihnen verwendeten Paketquellen
- Ein Wiederherstellungsprotokoll mit detailliertem Ausführlichkeitsgrad
- MTR oder eine Fiddler-Ablaufverfolgung (siehe unten)
- Ihre geografische Region
- Angabe, ob Ihr Computer einen Proxy oder eine Firewall verwendet
- Angabe, ob Ihr Computer sich im Rechenzentrum eines Cloudanbieters (z. B. Azure oder AWS) befindet – falls ja, geben Sie den Namen des Anbieters und die Region an.

*Erfassen von MTR:*

- Laden Sie [WinMTR](https://sourceforge.net/projects/winmtr/files/WinMTR-v092.zip/download) herunter.
- Geben Sie `api.nuget.org` als Hostname ein, und klicken Sie auf **Start**.
- Warten Sie, bis der Wert der Spalte **Gesendet** größer oder gleich 100 ist.

    ![Erfassen von MTR](media/mtr.png)

- Kopieren Sie den Text in die Zwischenablage.

*Erfassen von Fiddler:*

- Installieren Sie die aktuelle Version von [Fiddler](https://www.telerik.com/download/fiddler).
- Starten Sie Fiddler, und deaktivieren Sie die Erfassung des Datenverkehrs mithilfe des Menüs **File > Capture Traffic** (Datei > Datenverkehr erfassen).
- Entfernen Sie alle Sitzungen, indem Sie alle Elemente in der Liste auswählen und die **ENTF**-Taste drücken.
- Konfigurieren Sie Fiddler dafür, den HTTPS-Datenverkehr zu erfassen, indem Sie **Decrypt HTTPS traffic** (HTTPS-Datenverkehr entschlüsseln) auf der Registerkarte **HTTPS** des Menüs **Tools > Fiddler Options...** (Tools > Fiddler-Optionen...) überprüfen.
- Schließen Sie Visual Studio.
- Aktivieren Sie das Menü **File > Capture Traffic** (Datei > Datenverkehr erfassen).
- Starten Sie Visual Studio oder „nuget.exe“, und führen Sie die Aktionen aus, die nicht funktionieren. Der Datenverkehr, der durch diese Aktionen generiert wird, sollte in Fiddler angezeigt werden.
- Sobald die Aktionen ausgeführt wurden, verwenden Sie **Tools > Speichern > Alle Sitzungen**, um die erfassten Sitzungen zu speichern.

Hinweis: Es kann erforderlich sein, die Umgebungsvariable `HTTP_PROXY` auf `http://127.0.0.1:8888` festzulegen, um den NuGet-Datenverkehr an Fiddler weiterzuleiten.

Wenn dies fehlschlägt, befolgen Sie die Ratschläge [in diesem StackOverflow-Beitrag](https://stackoverflow.com/questions/21049908/using-fiddler-to-sniff-visual-studio-2013-requests-proxy-firewall).

## <a name="nugetorg-account-management"></a>Kontoverwaltung auf NuGet.org

### <a name="how-to-recover-nugetorg-password-login"></a>Wie kann ich die Anmeldung mit Kennwort auf NuGet.org wiederherstellen?

Bitte beachten Sie, dass die [Anmeldung mit Kennwort für NuGet.org nicht mehr unterstützt wird](https://blog.nuget.org/20180515/NuGet.org-will-only-support-MSA-AAD-starting-June.html). Sie können sich nur noch mit einem persönlichen Microsoft-Konto (MSA) oder mit einem Azure Active Directory-Konto (AAD) auf NuGet.org anmelden. Falls Sie jedoch nicht mehr auf das zugehörige MSA- oder AAD-Konto zugreifen können, müssen Sie möglicherweise die Anmeldung über das Kennwort durchführen, um Ihr Konto für NuGet.org wiederherzustellen. Führen Sie in diesem Fall die folgenden Schritte durch.
- **Voraussetzung:** Sie müssen auf die E-Mail-Adresse zugreifen können, die dem Konto zugeordnet ist, dessen Kennwort Sie wiederherstellen möchten.
- Navigieren Sie zur Seite [Forgot password](https://www.nuget.org/account/ForgotPassword) (Kennwort vergessen).
- Geben Sie die **E-Mail-Adresse** ein, die dem Konto auf NuGet.org zugeordnet ist, das Sie wiederherstellen möchten.
- Klicken Sie auf die Schaltfläche **Senden**.
- Sie erhalten in diesem E-Mail-Konto eine Nachricht, die einen Link zum Zurücksetzen des Kennworts enthält. Klicken Sie auf diesen Link, und legen Sie das neue Kennwort fest. Wenn Sie die Nachricht nicht finden können, überprüfen Sie auch den Spam-oder Junk-Ordner.
- Danach können Sie sich mit Ihrem Benutzernamen und Ihrem Kennwort bei NuGet anmelden.
- Verwenden Sie den Link **Sign in using NuGet.org account** (Mit NuGet.org-Konto anmelden) auf der [Anmeldeseite von NuGet.org](https://www.nuget.org/users/account/LogOn), um sich mit Ihrem Benutzernamen und Ihrem Kennwort anzumelden.

### <a name="which-microsoft-account-is-linked-to-my-nugetorg-account"></a>Welches Microsoft-Konto ist mit meinem Konto auf NuGet.org verknüpft?

Wenn Sie nicht mehr wissen, welches Microsoft-Konto mit Ihrem Konto auf NuGet.org verknüpft ist, sollten Sie folgende Schritte durchführen.
1. Navigieren Sie zur [Anmeldeseite von NuGet.org](https://www.nuget.org/users/account/LogOn), und klicken Sie auf den Link **Need assistance signing in?** (Benötigen Sie Hilfe bei der Anmeldung?).
1. Dadurch wird das Dialogfeld für die Hilfe angezeigt. Befolgen Sie die Schritte in diesem Dialogfeld, um das Microsoft-Konto bzw. die Microsoft-Konten zu ermitteln, die dem Konto auf NuGet.org zugeordnet sind.

### <a name="how-to-change-the-microsoft-account-i-use-for-nugetorg-login"></a>Wie kann ich das Microsoft-Konto ändern, das ich für die Anmeldung auf NuGet.org verwende?
Wenn Sie das Microsoft-Konto für Ihren Benutzer auf NuGet.org ändern möchten, müssen Sie folgende Schritte durchführen. Gehen wir davon aus, dass Ihr Microsoft-Konto mit der E-Mail-Adresse `account1@outlook.com` dem NuGet.org-Konto mit dem Benutzernamen `MyNuGetAccount` zugeordnet ist. Sie möchten die Anmeldung nun mit einem anderen Microsoft-Konto durchführen, das die E-Mail-Adresse `account2@outlook.com` aufweist.
1. Melden Sie sich über die [Anmeldeseite](https://www.nuget.org/users/account/LogOn) mit dem **derzeit zugeordneten Microsoft-Konto** (z. B. `account1@outlook.com`) an, indem Sie auf **Sign in with Microsoft** (Mit Microsoft anmelden) klicken.
1. Navigieren Sie zur Seite [account settings](https://www.nuget.org/account) (Kontoeinstellungen), nachdem Sie sich angemeldet haben.
1. Erweitern Sie den Bereich **Login Account** (Konto für die Anmeldung). Klicken Sie auf **Change Account** (Konto ändern).
1. Sie werden nun zur Microsoft-Anmeldeseite weitergeleitet. Melden Sie sich mit dem Konto an, das nun zugeordnet werden soll, z. B. `account2@outlook.com`. **Hinweis:** Sie müssen während der Anmeldung auf **Sign out and sign in with different account** (Abmelden und mit anderem Konto anmelden) klicken, damit Sie sich mit einem anderen Microsoft-Konto anmelden können.
1. Falls folgender Fehler angezeigt wird, finden Sie weitere Informationen im Abschnitt [Das Microsoft-Konto ist mit einem anderen NuGet.org-Konto verknüpft](#microsoft-account-is-linked-with-another-nugetorg-account).
    >_Failed to update the Microsoft account with 'account2 <account2@outlook.com>'. This could happen if it is already linked to another NuGet account. Contact support for more information. (Das Microsoft-Konto konnte nicht durch „account2 account2@outlook.com“ ersetzt werden. Möglicherweise ist das Konto bereits mit einem anderen NuGet-Konto verknüpft. Wenden Sie sich an den Support, um weitere Informationen zu erhalten.)_

1. Wenn Sie sich erfolgreich bei Ihrem zweiten Konto angemeldet haben, werden Sie zurück zur Seite „account settings“ (Kontoeinstellungen) auf NuGet.org geleitet. Nun sollte das Microsoft-Konto angezeigt werden, das als Konto für die Anmeldung verwendet wird. Sie sollten ab diesem Zeitpunkt dieses Konto für die Anmeldung auf NuGet.org verwenden.

### <a name="microsoft-account-is-linked-with-another-nugetorg-account"></a>Das Microsoft-Konto ist mit einem anderen NuGet.org-Konto verknüpft.

Möglicherweise wurde dieser Fehler angezeigt, als Sie versucht haben, Ihr Microsoft-Konto für die Anmeldung zu ändern:
> _Failed to update the Microsoft account with 'account2 <account2@outlook.com>'. This could happen if it is already linked to another NuGet account. Contact support for more information. (Das Microsoft-Konto konnte nicht durch „account2 account2@outlook.com“ ersetzt werden. Möglicherweise ist das Konto bereits mit einem anderen NuGet-Konto verknüpft. Wenden Sie sich an den Support, um weitere Informationen zu erhalten.)_

Angenommen, Sie haben versucht, das Microsoft-Konto für die Anmeldung für den Benutzernamen `MyNuGetAccount1` auf NuGet.org von `account1@outlook.com` in ein anderes Microsoft-Konto mit der E-Mail-Adresse `account2@outlook.com` zu ändern. Nun wird Ihnen diese Fehlermeldung angezeigt.

**Was bedeutet diese Fehlermeldung?**

Sie bedeutet, dass ein anderes NuGet.org-Konto bereits mit dem Microsoft-Konto verknüpft ist, das Sie für die Anmeldung verwenden möchten. Im oben genannten Beispiel ist das Microsoft-Konto mit der E-Mail-Adresse `<account2@outlook.com>` bereits einem anderen NuGet.org-Konto (z. B. `MyNuGetAccount2`) zugeordnet.

Sie können das für die Anmeldung verwendete Konto nicht durch ein Microsoft-Konto ersetzen, das mit einem anderen NuGet.org-Konto verknüpft ist.

**Ich habe vergessen, dass ich schon ein NuGet.org-Konto besitze. Wie finde heraus, um welches Konto es sich handelt?**

Melden Sie sich mit dem zweiten Microsoft-Konto bei der [Anmeldeseite](https://www.nuget.org/users/account/LogOn?returnUrl=%2F# "Anmeldeseite") an. Dadurch werden Sie bei dem NuGet.org-Konto angemeldet, dem das zweite Microsoft-Konto derzeit zugeordnet ist. Sie können dann die hochgeladenen Pakete sehen und das Konto verwalten.

**Ich benötige das zweite NuGet.org-Konto nicht, sondern möchte nur die Anmeldung für das erste Konto durch das zweite Microsoft-Konto ersetzen. Wie gehe ich vor?**

Wenn Sie das zweite NuGet.org-Konto nicht benötigen und das zugeordnete Microsoft-Konto mit der E-Mail-Adresse `account2@outlook.com` freigeben und erneut verwenden möchten, 

können Sie die Verknüpfung des Microsoft-Kontos mit dem NuGet.org-Konto aufheben, indem Sie das entsprechende NuGet.org-Konto löschen.
1. Befolgen Sie die Schritte zum [Löschen eines Benutzers](#how-to-delete-my-nugetorg-account) für das zweite NuGet.org-Konto (`MyNuGetAccount2`). 
1. Nachdem dieses Konto gelöscht wurde, können Sie die Schritte zum [Ändern des Microsoft-Kontos für die Anmeldung](#how-to-change-the-microsoft-account-i-use-for-nugetorg-login) wiederholen.

**Ich benötige das zweite Konto ebenfalls. Ich möchte dieses Konto behalten und das Konto für die Anmeldung beim ersten Konto ändern.**

Sie müssen ein drittes Microsoft-Konto erstellen oder verwenden (z. B. mit der E-Mail-Adresse `account3@outlook.com`). 
1. Zunächst sollten Sie sich mit dem zweiten Microsoft-Konto (`account2@outlook.com`) auf NuGet.org anmelden. Befolgen Sie die oben aufgeführten Schritte, um die zugehörigen Konten für die Anmeldung zu ändern und das dritte Microsoft-Konto diesem NuGet.org-Konto zuzuordnen.
1. Anschließend kann Ihr zweites Microsoft-Konto mit der E-Mail-Adresse `account2@outlook.com` dem ersten NuGet.org-Konto (`MyNuGetAccount1`) zugeordnet werden. Befolgen Sie die gleichen Schritte erneut, um das Microsoft-Konto für die Anmeldung auf das zweite Microsoft-Konto festzulegen.

### <a name="signing-in-with-microsoft-account-shows-me-my-email-is-linked-to-another-microsoft-account"></a>Bei der Anmeldung mit dem Microsoft-Konto wird angezeigt, dass die E-Mail-Adresse mit einem anderen Microsoft-Konto verknüpft ist

Sie haben versucht, sich mit Ihrem Microsoft-Konto anzumelden (z. B. mit der E-Mail-Adresse `account1@outlook.com`), und es wird folgende Fehlermeldung angezeigt:
> _The account with email 'account1@outlook.com' is linked with another Microsoft account._ (Das Konto mit der E-Mail-Adresse „account1@outlook.com“ ist mit einem anderen Microsoft-Konto verknüpft.)
>
> _If you would like to update the linked Microsoft account you can do so from the account settings page._ (Sie können das verlinkte Microsoft-Konto über die Seite „Kontoeinstellungen“ ändern.)

**Was bedeutet diese Fehlermeldung?**

Wenn ein Konto auf NuGet.org erstellt wird, ist diesem eine E-Mail-Adresse für die Kommunikation zugeordnet. Diese entspricht üblicherweise der E-Mail-Adresse des zugeordneten Microsoft-Kontos. Sie können jedoch eine andere E-Mail-Adresse festlegen, über die die Kommunikation erfolgen soll. Sie können also ein anderes Microsoft-Konto besitzen (z. B. mit der E-Mail-Adresse `account2@outlook.com`), das mit einem NuGet.org-Konto verknüpft ist, dessen E-Mail-Adresse für die Kommunikation auf `account1@outlook.com` festgelegt ist.

Der oben aufgeführte Fehler bedeutet also, dass bereits ein NuGet.org-Konto vorhanden ist, dessen E-Mail-Adresse für die Kommunikation auf `account1@outlook.com` festgelegt ist, das jedoch mit einem anderen Microsoft-Konto verknüpft ist, dessen E-Mail-Adresse **nicht** `account1@outlook.com` lautet.

**Wie finde ich heraus, welches Microsoft-Konto mit meinem NuGet.org-Konto verknüpft ist?**

Sie sollten die Anleitung zur [Hilfe bei der Anmeldung](#which-microsoft-account-is-linked-to-my-nugetorg-account) befolgen, um herauszufinden, welches Microsoft-Konto mit dem NuGet.org-Konto verknüpft ist, für das die E-Mail-Adresse `account1@outlook.com` angegeben ist.

**Ich möchte dieses Konto durch mein Microsoft-Konto ersetzen**

Befolgen Sie die Schritte im Abschnitt [Ich kann mein Microsoft-Konto nicht verwenden. Wie kann ich mein NuGet.org-Konto wiederherstellen?](#unable-to-use-microsoft-login-how-do-i-recover-my-nugetorg-account), um Ihr Microsoft-Konto mit dem vorhandenen NuGet.org-Konto zu verknüpfen.

### <a name="unable-to-use-microsoft-login-how-do-i-recover-my-nugetorg-account"></a>Ich kann mich nicht mit dem Microsoft-Konto anmelden. Wie kann ich mein NuGet.org-Konto wiederherstellen?

Wenn Sie die Anleitung zur [Hilfe bei der Anmeldung](#which-microsoft-account-is-linked-to-my-nugetorg-account) befolgt haben und dennoch nicht auf das Microsoft-Konto zugreifen können, das dem NuGet.org-Konto zugeordnet ist, befolgen Sie diese Schritte, um ein neues Microsoft-Konto mit Ihrem NuGet.org-Konto zu verknüpfen.
1. **Voraussetzung:** Sie müssen auf ein Microsoft-Konto zugreifen können, das mit keinem vorhandenen NuGet.org-Konto verknüpft ist. Wenn Sie kein Konto besitzen, können Sie eines [erstellen](https://signup.live.com).
2. Wenn Sie Ihren Benutzernamen und das Kennwort für Ihr NuGet.org-Konto vergessen haben, befolgen Sie die [Schritte zum Wiederherstellen Ihres Kennworts](#how-to-recover-nugetorg-password-login).
3. [Melden Sie sich mit Ihrem Benutzernamen und Kennwort auf NuGet.org an](https://www.nuget.org/users/account/LogOnNuGetAccount).
4. Nach der Anmeldung wird ein Popupfenster angezeigt. In diesem Dialogfeld werden Sie über die Aufhebung des Kennworts informiert.
5. **HINWEIS**: Ignorieren Sie die Anweisung, sich mit dem angegebenen Microsoft-Konto anzumelden. Sie können Ihr NuGet.org-Konto nun mit einem anderen Microsoft-Konto verknüpfen.
6. Klicken Sie auf **Sign in with Microsoft** (Mit Microsoft anmelden), und melden Sie sich wie in Schritt 1 erläutert mit dem Microsoft-Konto an, auf das Sie zugreifen können.
7. Ihr Konto wird nun mit dem neuen Microsoft-Konto verknüpft, und Sie können sich jetzt mit diesem Konto auf NuGet.org anmelden.

    ![Dialogfeld: Verknüpfung des MSA-Kontos](media/link-msa-dialog.png)

### <a name="how-to-transform-my-nugetorg-account-to-an-organization"></a>Wie kann ich mein NuGet.org-Konto auf ein Organisationskonto umstellen?

Wenn Sie Ihr Konto auf ein Organisationskonto umstellen möchten und diesem bereits ein Microsoft-Konto für die Anmeldung zugeordnet ist, befolgen Sie die Schritte in der Dokumentation für [Organisationen auf nuget.org](organizations-on-nuget-org.md).

Wenn Ihr NuGet.org-Konto jedoch nicht mit einem Microsoft-Konto verknüpft ist, können Sie die folgenden Schritte ausführen, um dieses Konto auf ein Organisationskonto umzustellen.
1. **Voraussetzung:** Sie müssen zunächst ein einzelnes Konto auf NuGet.org erstellen, das als Administrator für das Organisationskonto fungiert. Wenn Sie noch kein NuGet.org-Konto besitzen, [erstellen Sie ein neues](individual-accounts.md).
2. Befolgen Sie die [Schritte zum Wiederherstellen des Kennworts](#how-to-recover-nugetorg-password-login) für Ihr NuGet.org-Konto, wenn Sie Ihr Kennwort vergessen haben. Wenn das nicht der Fall ist, können Sie diesen Schritt überspringen.
3. [Melden Sie sich mit Ihrem Benutzernamen und Kennwort auf NuGet.org an](https://www.nuget.org/users/account/LogOnNuGetAccount).
4. Nach der Anmeldung wird ein Popupfenster angezeigt. In diesem Dialogfeld werden Sie über die Aufhebung des Kennworts informiert. 
    > [!Important]
    > Ignorieren Sie dieses Dialogfeld. Klicken Sie **nicht** auf **Sign in with Microsoft** (Mit Microsoft anmelden).

5. Wechseln Sie zu [https://www.nuget.org/account/transform](https://www.nuget.org/account/transform). Dort können Sie Ihr Konto auf NuGet.org auf ein Organisationskonto umstellen, ohne dieses mit einem Microsoft-Konto zu verknüpfen.
6. Geben Sie den Administratorbenutzernamen für Ihr persönliches NuGet.org-Konto bzw. für das Konto an, das Sie in Schritt 1 erstellt haben.
7. Befolgen Sie die Anweisungen, um die Umstellung des Kontos auf ein Organisationskonto abzuschließen.

    ![Dialogfeld: Verknüpfung des MSA-Kontos](media/link-msa-dialog.png)

### <a name="nugetorg-login-issues-for-aad-accounts-with-unmanaged-tenant"></a>Haben Sie Probleme bei der Anmeldung auf NuGet.org mit AAD-Konten mit nicht verwalteten Mandanten?

Wenn bei der Anmeldung mit Ihrer E-Mail-Kontodomäne (@yourdomain.com) folgender Fehler angezeigt wird, führen Sie die nachfolgenden Schritte durch, um Ihr NuGet.org-Konto wiederherzustellen.

<p align="center">
    <img src="media/unmanaged-aad-tenant.png" />
</p>

**Was bedeutet der Status „Nicht verwaltet“ während der Anmeldung? Warum wird dieser angezeigt?** 

Ihr Konto wurde als persönliches Microsoft-Konto registriert und hat problemlos funktioniert. Nun wurde Ihr Konto jedoch als Mandant mit dem Status „Nicht verwaltet“ in Azure Active Directory registriert (der Identitätsdienst, der verwendet wird, um Microsoft-Konten zu authentifizieren). 

Dies kann der Fall sein, wenn Sie oder ein Mitglied Ihrer Organisation (mit der E-Mail-Adresse @yourdomain.com) sich bei einem integrierten AAD-Dienst registriert oder die [Self-Service-Registrierung für Azure Active Directory](https://docs.microsoft.com/azure/active-directory/users-groups-roles/directory-self-service-signup) eingerichtet haben. Dadurch wird ein Mandant mit dem Status „Nicht verwaltet“ für die verwendete Microsoft-Kontodomäne (in diesem Fall @yourdomain.com) erstellt. 

**Wie kann ich mein Konto wiederherstellen?**

Derzeit ist es nicht möglich, Konten auf NuGet.org zu authentifizieren, die in Azure Active Directory den Status „Nicht verwaltet“ aufweisen. Es wird jedoch an einer Möglichkeit gearbeitet, solche Konten authentifizieren zu können.

Wenn Sie sich auf NuGet.org mit Ihrem Microsoft-Konto (@yourdomain.com) anmelden möchten, müssen Sie (oder ein Administrator Ihres Unternehmens) den Besitz des AAD-Kontos beanspruchen, indem Sie eine DNS-Überprüfung durchführen, um Benutzer mit der E-Mail-Adresse „@yourdomain.com“ zu authentifizieren. Befolgen Sie die Schritte zur [Übernahme von Domänen durch Administratoren](https://docs.microsoft.com/azure/active-directory/users-groups-roles/domains-admin-takeover), die in der Dokumentation zu Azure Active Directory beschrieben werden. Anschließend sollten Sie sich mit diesem Konto anmelden können.

**Ich möchte diese Methode nicht anwenden. Gibt es eine andere Möglichkeit, mein Konto wiederherzustellen?**

Sie können ein neues Microsoft-Konto [erstellen](https://www.microsoft.com/account), dessen E-Mail-Adresse **nicht** zu @yourdomain.com gehört. Befolgen Sie hierfür die Schritte im Abschnitt zum [Wiederherstellen Ihres NuGet.org-Kontos](#unable-to-use-microsoft-login-how-do-i-recover-my-nugetorg-account).

### <a name="how-do-i-change-my-nugetorg-account-username"></a>Wie kann ich den Benutzernamen meines NuGet.org-Kontos ändern?

Sie können den Benutzernamen nicht ändern. Gemäß der Richtlinien von Microsoft ist eine Änderung des Benutzernamens nicht zulässig. Eine Änderung des Benutzernamens wäre ein Breaking Change für Benutzer, die [auf dem Paketbesitzer basierende Vertrauensrichtlinien für Pakete](../consume-packages/installing-signed-packages.md#trust-package-owners) definiert haben. Sie können Ihren Benutzernamen lediglich ändern, indem Sie ein neues Konto mit dem gewünschten Benutzernamen erstellen. Es wird empfohlen, Ihr bestehendes Konto zu löschen, bevor Sie ein neues erstellen. Andernfalls können Sie Ihr registriertes Microsoft-Konto nicht für das neue Konto verwenden.
> [!Important]
> Durch das Löschen des Kontos bleibt der `username` dennoch **reserviert**. Sie können den gleichen Benutzernamen nicht noch einmal verwenden, auch dann nicht, wenn Sie **die Groß- und Kleinschreibung ändern**. Wenn Sie beispielsweise ein Konto mit dem Benutzernamen `mycoolname` erstellt haben und diesen in `MyCoolName` (geänderte Groß- und Kleinschreibung) ändern möchten, ist dieser Vorgang auch nach dem Löschen des Kontos nicht möglich.

Befolgen Sie die Schritte im Abschnitt zum [Löschen Ihres NuGet.org-Kontos](#how-to-delete-my-nugetorg-account) und zum [Registrieren eines neuen Kontos](individual-accounts.md) mit einem zulässigen Benutzernamen.

### <a name="how-to-delete-my-nugetorg-account"></a>Wie kann ich mein NuGet.org-Konto löschen?

Es wird empfohlen, den Besitz aller Pakete, deren alleiniger Besitzer Sie sind, auf ein anderes Konto zu übertragen, bevor Sie Ihr Konto löschen. Weitere Informationen zu diesem Thema finden Sie unter [Verwalten von Paketbesitzern auf nuget.org](../nuget-org/publish-a-package.md#managing-package-owners-on-nugetorg). Hierdurch können wir Ihre Anforderung schneller verarbeiten.

Wenn Sie Ihr Konto auf ein Organisationskonto umstellen möchten, führen Sie die in [Wie kann ich mein NuGet.org-Konto auf ein Organisationskonto umstellen?](#how-to-transform-my-nugetorg-account-to-an-organization) beschriebenen Schritte aus.

> [!Important]
> Das Löschen Ihres Kontos hat folgende Auswirkungen:
>  1. Ihr Benutzername ist reserviert und kann nicht erneut verwendet werden, um ein einzelnes Konto oder ein Organisationskonto zu erstellen.
>  1. Zugehörige API-Schlüssel werden widerrufen. 
>  1. Das Konto wird als Besitzer aller untergeordneten Pakete entfernt.
>  1. Alle ID-Präfixe, die mit diesem Konto reserviert wurden, werden freigegeben.
>  1. Die Mitgliedschaft des Kontos in sämtlichen Organisationen wird aufgehoben.

Befolgen Sie diese Schritte, um mit der Löschung Ihres Kontos fortzufahren:
1. [Melden Sie sich auf NuGet.org mit dem Konto an](https://www.nuget.org/users/account/LogOn), das Sie löschen möchten.
2. Klicken Sie auf die URL [https://www.nuget.org/account/delete](https://www.nuget.org/account/delete), und befolgen Sie die Schritte, um die Anforderung zum Löschen des Kontos zu übermitteln.

Der Kundensupport verarbeitet Ihre Anforderung und löscht das Konto.
