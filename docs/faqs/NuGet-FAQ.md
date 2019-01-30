---
title: Häufig gestellte Fragen zu NuGet
description: Häufig gestellte Fragen und entsprechende Antworten zur Verwendung von NuGet über die Befehlszeile und in Visual Studio sowie zum Arbeiten mit dem NuGet-Katalog.
author: shishirx34
ms.author: shishirh
ms.date: 01/15/2019
ms.topic: conceptual
ms.openlocfilehash: dbdd171321c2560adc06feccbd60fc4e84dcf0a3
ms.sourcegitcommit: a801052aa728a3a137225ca3ef3ff89f2d1c6b76
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/18/2019
ms.locfileid: "54403209"
---
# <a name="nuget-frequently-asked-questions"></a>Häufig gestellte Fragen zu NuGet

**Was ist erforderlich, um NuGet auszuführen?**

Sämtliche Informationen zur Benutzeroberfläche und zu den Befehlszeilentools sind im [Installationshandbuch](../install-nuget-client-tools.md) verfügbar.

**Wird Mono von NuGet unterstützt?**

Das Befehlszeilentool (`nuget.exe`) erstellt und führt unter Mono 3.2 und höher aus und kann Pakete in Mono erstellen.

`nuget.exe` funktioniert unter Windows problemlos, es gibt jedoch bekannte Probleme unter Linux und OS X. Weitere Informationen finden Sie auf GitHub unter [Mono issues (Probleme mit Mono)](https://github.com/NuGet/Home/issues?utf8=%E2%9C%93&q=is%3Aissue+is%3Aopen+mono).

Ein [grafischer Client](https://github.com/mrward/monodevelop-nuget-addin) ist als Add-In für MonoDevelop verfügbar.

**Wie kann bestimmt werden, was in einem Paket enthalten ist und ob die Inhalte stabil und nützlich für meine Anwendung sind?**

Die Primärquelle für Informationen zu einem Paket ist dessen Angebotsseite auf nuget.org (oder einem anderen privaten Feed). Jede Seite für ein Paket auf nuget.org enthält eine Beschreibung des Pakets, den Versionsverlauf und Nutzungsstatistiken. Der Abschnitt **Info** auf der Seite des Pakets enthält ebenfalls einen Link zur Website des Projekts, auf der Sie in der Regel zahlreiche Beispiele und weitere Dokumentationen finden, die Sie beim Verwenden des Pakets unterstützen.

Weitere Informationen finden Sie unter [Finding and choosing packages (Suchen und Auswählen von Paketen)](../consume-packages/finding-and-choosing-packages.md).

## <a name="nuget-in-visual-studio"></a>NuGet in Visual Studio

**Wie wird NuGet in verschiedenen Visual Studio-Produkten unterstützt?**

- Visual Studio unter Windows unterstützt die [Benutzeroberfläche des Paket-Managers](../tools/package-manager-ui.md) und die [Konsole des Paket-Managers](../tools/package-manager-console.md).
- Visual Studio für Mac verfügt wie unter [Including a NuGet package in your project (Einschließen eines NuGet-Pakets in Ihr Projekt)](/visualstudio/mac/nuget-walkthrough) beschrieben über integrierte NuGet-Funktionen.
- Visual Studio Code (alle Plattformen) verfügt nicht über eine direkte NuGet-Integration. Verwenden Sie die [NuGet-CLI](../tools/nuget-exe-cli-reference.md) oder die [dotnet-CLI](../tools/dotnet-commands.md).
- Azure DevOps stellt [einen Buildschritt für das Wiederherstellen von NuGet-Paketen](/vsts/build-release/tasks/package/nuget) bereit. Sie können auch [private NuGet-Paketfeeds auf Azure DevOps hosten](https://docs.microsoft.com/azure/devops/artifacts/nuget/publish).

**Wie kann überprüft werden, ob die richtige Version der NuGet-Tools installiert ist?**

Verwenden Sie in Visual Studio den Befehl **Hilfe > Info**, und achten Sie auf die Version, die neben dem **NuGet-Paket-Manager** angezeigt wird.

Führen Sie alternativ die Konsole des Paket-Managers (**Tools > NuGet-Paket-Manager > Paket-Manager-Konsole**) aus, und geben Sie `$host` ein, um Informationen über NuGet anzuzeigen, die ebenfalls die Version enthalten.

**Welche Programmiersprachen werden von NuGet unterstützt?**

NuGet funktioniert im Allgemeinen mit .NET-Sprachen und wurde dafür entwickelt, .NET-Bibliotheken in Projekte einzubinden. Da NuGet ebenfalls die MSBuild- und Visual Studio-Automatisierung für einige Projekttypen unterstützt, werden teilweise auch andere Projekte und Sprachen unterstützt.

Die neueste Version von NuGet unterstützt C#, Visual Basic, F#, WiX und C++.

**Welche Projektvorlagen werden von NuGet unterstützt?**

NuGet unterstützt eine Vielzahl von Projektvorlagen vollständig, z.B. Windows, Web, Cloud, SharePoint, WiX usw.

**Wie können Pakete aktualisiert werden, die Teil von Visual Studio-Vorlagen sind?**

Wechseln Sie zur Registerkarte **Updates** in der Benutzeroberfläche des Paket-Managers, und klicken Sie auf **Alle aktualisieren**. Verwenden Sie alternativ den [Befehl `Update-Package`](../tools/ps-ref-update-package.md) über die Konsole des Paket-Managers.

Sie müssen das Repository der Vorlage manuell aktualisieren, um die Vorlage zu aktualisieren. Weitere Informationen zu diesem Thema finden Sie in diesem Blogbeitrag von [Xavier Decoster](http://www.xavierdecoster.com/update-project-template-to-latest-nuget-packages). Beachten Sie, dass Sie diesen Vorgang auf Ihr eigenes Risiko durchführen, denn manuelle Updates können die Vorlage beschädigen, wenn die aktuellen Versionen aller Abhängigkeiten nicht miteinander kompatibel sind.

**Kann NuGet außerhalb von Visual Studio verwendet werden?**

Ja, NuGet funktioniert direkt über die Befehlszeile. Weitere Informationen finden Sie im [Installationshandbuch](../install-nuget-client-tools.md) und in der [CLI-Referenz](../tools/nuget-exe-cli-reference.md).

## <a name="nuget-command-line"></a>NuGet-Befehlszeile

**Wie erhalte ich die aktuelle Version des NuGet-Befehlszeilentools?**

Weitere Informationen finden Sie im [Installationshandbuch](../install-nuget-client-tools.md).

**Welche Lizenzbestimmungen gelten für „nuget.exe“?**

Sie dürfen „nuget.exe“ unter den Bedingungen der MIT-Lizenz weiterverteilen. Sie sind für das Aktualisieren und Warten aller Kopien von „nuget.exe“ verantwortlich, die Sie weiterverteilen.

**Ist es möglich, das NuGet-Befehlszeilentool zu erweitern?**

Ja, es ist möglich, benutzerdefinierte Befehle zu `nuget.exe` hinzuzufügen. Dieser Vorgang wird in einem Blogbeitrag von [Rob Reynold](http://geekswithblogs.net/robz/archive/2011/07/15/extend-nuget-command-line.aspx) beschrieben.

## <a name="nuget-package-manager-console-visual-studio-on-windows"></a>Konsole des NuGet-Paket-Managers (Visual Studio unter Windows)

**Wie kann auf das DTE-Objekt in der Konsole des Paket-Managers zugegriffen werden?**

Das Objekt auf der obersten Ebene des Visual Studio-Automatisierungsobjektmodells wird als DTE-Objekt (Development Tools Environment) bezeichnet. Die Konsole stellt dieses Objekt über die Variable `$DTE` bereit. Weitere Informationen finden Sie in der Dokumentation zur Erweiterbarkeit von Visual Studio unter [Automation Model Overview (Übersicht über das Automatisierungsmodell)](/visualstudio/extensibility/internals/automation-model-overview).

**Ich versuche, die $DTE-Variable in den Typ DTE2 umzuwandeln, erhalte aber folgende Fehlermeldung: Ein Wert vom Typ "EnvDTE.DTEClass" kann nicht in den Typ "EnvDTE80.DTE2" konvertiert werden. Wo liegt der Fehler?**

Dabei handelt es sich um ein bekanntes Problem bei der Interaktion von PowerShell mit COM-Objekten. Versuchen Sie Folgendes:

```ps
`$dte2 = Get-Interface $dte ([EnvDTE80.DTE2])`
```

Bei `Get-Interface` handelt es sich um eine Hilfsfunktionen, die vom PowerShell-Host für NuGet hinzugefügt wurde.

## <a name="creating-and-publishing-packages"></a>Erstellen und Veröffentlichen von Paketen

**Wie kann ein Paket in einem Feed aufgeführt werden?**

Weitere Informationen finden Sie unter [Creating and publishing a package (Erstellen und Veröffentlichen von Paketen)](../quickstart/create-and-publish-a-package.md).

**Es gibt mehrere Versionen meiner Bibliothek, die verschiedene Versionen von .NET-Framework anzielen. Wie kann ein einziges Paket erstellt werden, das dies unterstützt?**

Weitere Informationen finden Sie unter [Supporting Multiple .NET Framework Versions and Profiles (Unterstützen mehrerer .NET Framework-Versionen und -Profile)](../create-packages/supporting-multiple-target-frameworks.md).

**Wie können eigene Repositorys oder Feeds eingerichtet werden?**

Weitere Informationen finden Sie unter [Hosting packages overview (Übersicht über das Hosten von Paketen)](../hosting-packages/overview.md).

**Wie können Pakete in einer Massenoperation an meinen NuGet-Feed hochgeladen werden**

Weitere Informationen finden Sie unter [Bulk publishing NuGet packages (Massenveröffentlichen von NuGet-Paketen)](http://jeffhandley.com/archive/2012/12/13/Bulk-Publishing-NuGet-Packages.aspx) (jeffhandly.com).

## <a name="working-with-packages"></a>Arbeiten mit Paketen

**Wo liegt der Unterschied zwischen einem Paket auf Projektebene und einem Paket auf Projektmappenebene?**

Ein Paket auf Projektmappenebene (NuGet 3.x und höher) wird nur einmal in einer Projektmappe installiert und ist dann für alle Projekte in der Projektmappe verfügbar. Ein Paket auf Projektebene wird in jedem Projekt installiert, das dieses verwendet. Durch ein Paket auf Projektmappenebene können ebenfalls neue Befehle installiert werden, die von der Konsole des Paket-Managers aus aufgerufen werden können.

**Ist es möglich, NuGet-Pakete ohne Internetverbindung zu installieren?**

Ja. Weitere Informationen dazu finden Sie im Blogbeitrag [How to access NuGet when nuget.org is down (or you're on a plane) (Zugriff auf NuGet, wenn nuget.org offline ist (oder wenn Sie sich in einem Flugzeug befinden))](http://www.hanselman.com/blog/HowToAccessNuGetWhenNuGetorgIsDownOrYoureOnAPlane.aspx) von Scott Hanselman (hanselman.com).

**Wie können Pakete an einem anderen Speicherort als dem Standardordner für Pakete installiert werden?**

Legen Sie die Einstellung [`repositoryPath`](../reference/nuget-config-file.md#config-section) in `Nuget.Config` mithilfe von `nuget config -set repositoryPath=<path>` fest.

**Wie kann vermieden werden, dass der Ordner für NuGet-Pakete der Quellcodeverwaltung hinzugefügt wird?**

Legen Sie die Einstellung [`disableSourceControlIntegration`](../reference/nuget-config-file.md#solution-section) in `Nuget.Config` auf `true` fest. Dieser Schlüssel funktioniert auf Projektmappenebene und muss daher zur `$(Solutiondir)\.nuget\Nuget.Config`-Datei hinzugefügt werden. Durch das Aktivieren der Paketwiederherstellung in Visual Studio wird diese Datei automatisch erstellt.

**Wie kann die Paketwiederherstellung deaktiviert werden?**

Weitere Informationen finden Sie unter [Enabling and disabling package restore (Aktivieren und Deaktivieren der Paketwiederherstellung)](../consume-packages/package-restore.md#enabling-and-disabling-package-restore).

**Warum wird die Fehlermeldung „Der Abhängigkeitsfehler kann nicht aufgelöst werden.“ angezeigt, wenn ein lokales Paket mit Remoteabhängigkeiten installiert wird?**

Sie müssen die Quelle **Alle** auswählen, wenn Sie ein lokales Paket im Projekt installieren. Dadurch werden alle Feeds anstelle von einem einzigen verwendet. Diese Fehlermeldung wird angezeigt, weil Benutzer von lokalen Repositorys aufgrund von Unternehmensrichtlinien häufig verhindern möchten, dass ein Remotepaket versehentlich installiert wird.

**Es gibt mehrere Projekte im selben Ordner, wie können für jedes Projekt separate PACKAGES.CONFIG-Dateien verwendet werden?**

In den meisten Projekten, in denen sich separate Projekte in separaten Ordnern befinden, ist dies kein Problem, da NuGet die `packages.config`-Dateien in jedem Projekt identifiziert. Wenn sich ab NuGet 3.3 und höher mehrere Projekte im gleichen Ordner befinden, können Sie den Namen des Projekts zu den `packages.config`-Dateinamen hinzufügen, damit NuGet diese Datei verwendet. Verwenden Sie dabei das Muster `packages.{project-name}.config`.

Dies stellt kein Problem dar, wenn Sie PackageReference verwenden, da jede Projektdatei eine eigene Liste der Abhängigkeiten enthält.

**nuget.org wird nicht in der Liste der Repositorys angezeigt, wie kann dies geändert werden?**

- Fügen Sie `https://api.nuget.org/v3/index.json` zur Liste der Quellen hinzu, oder
- Löschen Sie `%appdata%\.nuget\NuGet.Config` (Windows) oder `~/.nuget/NuGet/NuGet.Config` (Mac/Linux), damit NuGet diese Dateien neu erstellen kann.

**Welche Lizenzbedingungen gelten standardmäßig, wenn ein Paket keine spezifischen Lizenzbedingungen bereitstellt?**

Jedes Paket unterliegt den im Paket enthaltenen Bestimmungen. Sie sollten die geltenden Bestimmungen überprüfen, bevor Sie Pakete erwerben, herunterladen oder auf diese zugreifen. Verwenden Sie den Link **Lizenzinformationen** auf der Seite für Pakete auf nuget.org.

Wenn ein Paket keine Lizenzbedingungen angibt, kontaktieren Sie den Paketbesitzer direkt, indem Sie den Link **Contact owners** (Besitzer kontaktieren) auf der Seite für Pakete auf nuget.org verwenden. Microsoft lizenziert kein geistiges Eigentum von Drittanbietern für Pakete und ist nicht verantwortlich für die durch Drittanbieter bereitgestellten Inhalte.

## <a name="managing-packages-on-nugetorg"></a>Verwalten von Paketen auf nuget.org

**Können Paketmetadaten nach dem Upload bearbeitet werden?**

Es wird empfohlen, dass Sie alle Pakete für NuGet signieren. Ein Entwurfsprinzip der Paketsignierung besteht darin, dass signierte Paketinhalte unveränderlich sein müssen. Dies schließt die NUSPEC-Datei ein. Durch das Bearbeiten der Paketmetadaten wird die NUSPEC-Datei geändert, wodurch bestehende Signaturen ungültig werden. Es wird empfohlen, vorhandene Workflows zu ändern, damit das Bearbeiten der Paketmetadaten nach dem Erstellen des Pakets nicht erforderlich ist.

Beachten Sie, dass die für Ihr Paket aufgeführten Abhängigkeiten automatisch vom Paket generiert werden und nicht bearbeitet werden können.

Zusätzlich stellt das Hochladen von Paketen auf [int.nugettest.org](https://int.nugettest.org) eine gute Möglichkeit zum Testen und Überprüfen des Pakets dar, ohne dieses im öffentlichen Katalog zur Verfügung zu stellen.

**Ist es möglich, Namen für Pakete zu reservieren, die in Zukunft veröffentlicht werden sollen?**

Ja. Sie können IDs für Pakete auf [nuget.org](https://www.nuget.org/) reservieren, indem Sie ein Präfix für eine Paket-ID für Ihr Konto anfordern. Wenn Sie ein Präfix für die Paket-ID anfordern möchten, folgen Sie den Anweisungen in der [Dokumentation](https://docs.microsoft.com/nuget/reference/id-prefix-reservation).

**Wie kann der Besitz eines Pakets beansprucht werden?**

Weitere Informationen finden Sie unter [Managing package owners on nuget.org (Verwalten von Paketbesitzern auf nuget.org)](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg).

**Wie kann vorgegangen werden, wenn ein Paketbesitzer meine Softwarelizenzbedingungen verletzt?**

Es wird empfohlen, dass die NuGet-Community zusammenarbeitet, um Streitfälle zwischen Paketbesitzern und den Besitzern von anderer Software zu klären. Es wurde eine [Vorgehensweise zum Lösen von Streitfällen](../policies/dispute-resolution.md) entworfen, die Sie befolgen sollten, bevor Sie um das Eingreifen der Administratoren von nuget.org bitten.

**Ist es empfehlenswert, meine Testpakete auf nuget.org hochzuladen?**

Für Testzwecke können Sie [int.nugettest.org](https://int.nugettest.org) oder alternative öffentliche NuGet-Server wie [myget.org](https://myget.org) oder [Azure DevOps](https://blogs.msdn.microsoft.com/visualstudioalm/2015/08/27/announcing-package-management-support-for-vsotfs/) verwenden.

Beachten Sie, dass Pakete, die auf int.nugettest.org hochgeladen werden, nicht beibehalten werden.

**Was ist die maximale Größe für Pakete, die auf nuget.org hochgeladen werden?**

Auf nuget.org sind Pakete bis 250 MB zugelassen. Es wird jedoch empfohlen, die Pakete nach Möglichkeit kleiner als 1 MB zu halten und Abhängigkeiten zu verwenden, um die Pakete miteinander zu verknüpfen. Als Faustregel gilt, dass Pakete nur eine Assembly enthalten sollten, um Konflikte zu vermeiden.

NuGet verwendet HTTP zum Herunterladen von Paketen. Bei größeren Paketen ist es daher wahrscheinlicher als bei kleineren, dass die Installation fehlschlägt.

Es ist möglich, Abhängigkeiten zwischen mehreren Paketen freizugeben. Dadurch wird die Gesamtgröße des Downloads für die Nutzer Ihrer NuGet-Pakete reduziert.

Abhängigkeiten sind überwiegend statisch und ändern sich nie. Wenn Sie einen Fehler im Code beheben, müssen die Abhängigkeiten möglicherweise nicht aktualisiert werden. Wenn Sie Abhängigkeiten bündeln, werden die Pakete, die Sie erneut versenden müssen, jedes Mal größer. Indem Sie NuGet-Pakete in verknüpfte Abhängigkeiten aufteilen, wodurch präzisere Upgrades für die Nutzer Ihrer Pakete ermöglicht werden.

## <a name="nugetorg-not-accessible"></a>Auf nuget.org kann nicht zugegriffen werden

**Warum kann ich keine Pakete auf nuget.org hochladen oder von nuget.org herunterladen?**

Stellen Sie zunächst sicher, dass Sie die aktuelle Version von NuGet verwenden. Wenn auch bei dieser Version Fehler auftreten, [kontaktieren Sie den Support](https://www.nuget.org/policies/Contact), und stellen Sie die folgenden zusätzlichen Informationen für die Problembehandlung der Verbindung zur Verfügung:

- Die von Ihnen verwendete NuGet-Version
- Die von Ihnen verwendeten Paketquellen
- Ein Wiederherstellungsprotokoll mit detailliertem Ausführlichkeitsgrad
- MTR oder eine Fiddler-Ablaufverfolgung (siehe unten)
- Ihre geografische Region
- Angabe, ob Ihr Computer einen Proxy oder eine Firewall verwendet
- Angabe, ob Ihr Computer sich im Rechenzentrum eines Cloudanbieters (z. B. Azure oder AWS) befindet – falls ja, geben Sie den Namen des Anbieters und die Region an.

*Erfassen von MTR:*

- Laden Sie über [http://winmtr.net/download/](http://winmtr.net/) WinMTR herunter.
- Geben Sie `api.nuget.org` als Hostname ein, und klicken Sie auf **Start**.
- Warten Sie, bis der Wert der Spalte **Gesendet** größer oder gleich 100 ist.

    ![Erfassen von MTR](media/mtr.png)

- Kopieren Sie den Text in die Zwischenablage.

*Erfassen von Fiddler:*

- Installieren Sie die aktuelle Version von [Fiddler](http://www.telerik.com/download/fiddler).
- Starten Sie Fiddler, und deaktivieren Sie die Erfassung des Datenverkehrs mithilfe des Menüs **File > Capture Traffic** (Datei > Datenverkehr erfassen).
- Entfernen Sie alle Sitzungen, indem Sie alle Elemente in der Liste auswählen und die **ENTF**-Taste drücken.
- Konfigurieren Sie Fiddler dafür, den HTTPS-Datenverkehr zu erfassen, indem Sie **Decrypt HTTPS traffic** (HTTPS-Datenverkehr entschlüsseln) auf der Registerkarte **HTTPS** des Menüs **Tools > Fiddler Options...** (Tools > Fiddler-Optionen...) überprüfen.
- Schließen Sie Visual Studio.
- Aktivieren Sie das Menü **File > Capture Traffic** (Datei > Datenverkehr erfassen).
- Starten Sie Visual Studio oder „nuget.exe“, und führen Sie die Aktionen aus, die nicht funktionieren. Der Datenverkehr, der durch diese Aktionen generiert wird, sollte in Fiddler angezeigt werden.
- Sobald die Aktionen ausgeführt wurden, verwenden Sie **Tools > Speichern > Alle Sitzungen**, um die erfassten Sitzungen zu speichern.

Hinweis: Es kann erforderlich sein, die Umgebungsvariable `HTTP_PROXY` auf `http://127.0.0.1:8888` festzulegen, um den NuGet-Datenverkehr an Fiddler weiterzuleiten.

Wenn dies fehlschlägt, befolgen Sie die Ratschläge [in diesem StackOverflow-Beitrag](http://stackoverflow.com/questions/21049908/using-fiddler-to-sniff-visual-studio-2013-requests-proxy-firewall).

**Welche API-Endpunkte gibt es für nuget.org?**

- V3: `https://api.nuget.org/v3/index.json`
- V2: `https://www.nuget.org/api/v2/` (Beachten Sie, dass die V2-API veraltet ist und nicht mit NuGet 4 und höher funktioniert.)

## <a name="nugetorg-account-management"></a>Kontoverwaltung auf nuget.org

### <a name="how-to-create-a-new-nugetorg-account"></a>Wie wird ein neues Konto auf nuget.org erstellt?

Sie müssen ein persönliches Microsoft-Konto (Managed Service Account, MSA) oder ein Azure Active Directory-Konto (AAD) besitzen, um ein Konto auf nuget.org erstellen zu können. Wenn Sie kein Konto besitzen, können Sie eines [erstellen](https://signup.live.com). Befolgen Sie diese Schritte, wenn Sie ein MSA- oder AAD-Konto besitzen.
1. Navigieren Sie zur [Anmeldeseite von nuget.org](https://www.nuget.org/users/account/LogOn).
1. Klicken Sie auf **Sign in with Microsoft** (Mit Microsoft anmelden).
1. Geben Sie die Anmeldeinformationen für Ihr MSA- oder AAD-Konto ein.
1. Stimmen Sie den Berechtigungen zu, die der *NuGet.org*-Anwendung erteilt werden.
1. Sie werden auf nuget.org umgeleitet und dazu aufgefordert, einen Benutzernamen zu registrieren.
1. Legen Sie den Benutzernamen im Eingabefeld fest. Bitte beachten Sie, dass beim Benutzernamen die **Groß- und Kleinschreibung** beachtet wird und er im Nachhinein nicht geändert werden kann.
1. Klicken Sie auf **Register** (Registrieren).

Sie besitzen nun ein Konto auf nuget.org. Sie können Ihr Konto über die Seite [account settings](https://www.nuget.org/account) (Kontoeinstellungen) verwalten.

### <a name="how-to-recover-nugetorg-password-login"></a>Wie kann ich das Kennwort für mein Konto auf nuget.org wiederherstellen?

Bitte beachten Sie, dass die [Anmeldung mit dem Kennwort für nuget.org nicht mehr unterstützt wird](https://blog.nuget.org/20180515/NuGet.org-will-only-support-MSA-AAD-starting-June.html). Sie können Sich nur noch mit einem persönlichen Microsoft-Konto (MSA) oder mit einem Azure Active Directory-Konto (AAD) auf nuget.org anmelden. Falls Sie jedoch nicht mehr auf das zugehörige MSA- oder AAD-Konto zugreifen können, müssen Sie möglicherweise die Anmeldung über das Kennwort durchführen, um Ihr Konto für nuget.org wiederherzustellen. Führen Sie in diesem Fall die folgenden Schritte durch.
- **Voraussetzung:** Sie müssen auf die E-Mail-Adresse zugreifen können, die dem Konto zugeordnet ist, dessen Kennwort Sie wiederherstellen möchten.
- Navigieren Sie zur Seite [Forgot password](https://www.nuget.org/account/ForgotPassword) (Kennwort vergessen).
- Geben Sie die **E-Mail-Adresse** ein, die dem Konto auf nuget.org zugeordnet ist, das Sie wiederherstellen möchten.
- Klicken Sie auf die Schaltfläche **Senden**.
- Sie erhalten in diesem E-Mail-Konto eine Nachricht, die einen Link zum Zurücksetzen des Kennworts enthält. Klicken Sie auf diesen Link, und legen Sie das neue Kennwort fest. Wenn Sie die Nachricht nicht finden können, überprüfen Sie auch den Spam-oder Junk-Ordner.
- Danach können Sie sich mit Ihrem Benutzernamen und Ihrem Kennwort bei NuGet anmelden.
- Verwenden Sie den Link **Sign in using Nuget.org account** (Mit Nuget.org-Konto anmelden) auf der [Anmeldeseite von nuget.org](https://www.nuget.org/users/account/LogOn), um sich mit Ihrem Benutzernamen und Ihrem Kennwort anzumelden.

### <a name="which-microsoft-account-is-linked-to-my-nugetorg-account"></a>Welches Microsoft-Konto ist mit meinem Konto auf nuget.org verknüpft?

Wenn Sie nicht mehr wissen, welches Microsoft-Konto mit Ihrem Konto auf nuget.org verknüpft ist, sollten Sie folgende Schritte durchführen.
1. Navigieren Sie zur [Anmeldeseite von nuget.org](https://www.nuget.org/users/account/LogOn), und klicken Sie auf den Link **Need assistance signing in?** (Benötigen Sie bei der Anmeldung Hilfe?).
1. Dadurch wird das Dialogfeld für die Hilfe angezeigt. Befolgen Sie die Schritte in diesem Dialogfeld, um das Microsoft-Konto bzw. die Microsoft-Konten zu ermitteln, die dem Konto auf nuget.org zugeordnet sind.

### <a name="how-to-change-the-microsoft-account-i-use-for-nugetorg-login"></a>Wie kann das Microsoft-Konto geändert werden, das für die Anmeldung auf nuget.org verwendet wird?
Wenn Sie das Microsoft-Konto für Ihr Konto auf nuget.org ändern möchten, müssen Sie folgende Schritte durchführen. Gehen Sie in diesem Beispiel davon aus, dass Ihr Microsoft-Konto mit der E-Mail-Adresse `account1@outlook.com` dem Konto auf nuget.org mit dem Benutzernamen `MyNuGetAccount` zugeordnet ist. Sie möchten die Anmeldung nun mit einem anderen Microsoft-Konto durchführen, das die E-Mail-Adresse `account2@outlook.com` aufweist.
1. Melden Sie sich über die [Anmeldeseite](https://www.nuget.org/users/account/LogOn) mit dem **derzeit zugeordneten Microsoft-Konto** (z. B. `account1@outlook.com`) an, indem Sie auf **Sign in with Microsoft** (Mit Microsoft anmelden) klicken.
1. Navigieren Sie zur Seite [account settings](https://www.nuget.org/account) (Kontoeinstellungen), nachdem Sie sich angemeldet haben.
1. Erweitern Sie den Bereich **Login Account** (Konto für die Anmeldung). Klicken Sie auf **Change Account** (Konto ändern).
1. Sie werden nun zur Microsoft-Anmeldeseite weitergeleitet. Melden Sie sich mit dem Konto an, das nun zugeordnet werden soll, z. B. `account2@outlook.com`. **Hinweis:** Sie müssen während der Anmeldung auf **Sign out and sign in with different account** (Abmelden und mit anderem Konto anmelden) klicken, damit Sie sich mit einem anderen Microsoft-Konto anmelden können.
1. Wenn folgender Fehler angezeigt wird, finden Sie weitere Informationen im Abschnitt [Das Microsoft-Konto ist mit einem anderen Konto auf nuget.org verknüpft](#microsoft-account-is-linked-with-another-nugetorg-account).
    >_Failed to update the Microsoft account with 'account2 <account2@outlook.com>'. This could happen if it is already linked to another NuGet account. Contact support for more information. (Das Microsoft-Konto konnte nicht durch „account2 account2@outlook.com“ ersetzt werden. Möglicherweise ist das Konto bereits mit einem anderen NuGet-Konto verknüpft. Wenden Sie sich an den Support, um weitere Informationen zu erhalten.)_

1. Wenn Sie sich erfolgreich bei Ihrem zweiten Konto angemeldet haben, werden Sie zur Seite „account settings“ (Kontoeinstellungen) auf nuget.org zurück geleitet. Nun sollte das Microsoft-Konto angezeigt werden, das als Konto für die Anmeldung verwendet wird. Sie sollten ab diesem Zeitpunkt dieses Konto für die Anmeldung auf nuget.org verwenden.

### <a name="microsoft-account-is-linked-with-another-nugetorg-account"></a>Das Microsoft-Konto ist mit einem anderen Konto auf nuget.org verknüpft

Möglicherweise wurde dieser Fehler angezeigt, als Sie versucht haben, Ihr Microsoft-Konto für die Anmeldung zu ändern:
> _Failed to update the Microsoft account with 'account2 <account2@outlook.com>'. This could happen if it is already linked to another NuGet account. Contact support for more information. (Das Microsoft-Konto konnte nicht durch „account2 account2@outlook.com“ ersetzt werden. Möglicherweise ist das Konto bereits mit einem anderen NuGet-Konto verknüpft. Wenden Sie sich an den Support, um weitere Informationen zu erhalten.)_

Angenommen, Sie haben versucht, das Microsoft-Konto für die Anmeldung für den Benutzernamen `MyNuGetAccount1` auf nuget.org von `account1@outlook.com` in ein anderes Microsoft-Konto mit der E-Mail-Adresse `account2@outlook.com` zu ändern. Nun wird Ihnen diese Fehlermeldung angezeigt.

**Was bedeutet diese Fehlermeldung?**

Sie bedeutet, dass ein anderes Konto auf nuget.org bereits mit dem Microsoft-Konto verknüpft ist, das Sie für die Anmeldung verwenden möchten. Im oben genannten Beispiel ist das Microsoft-Konto mit der E-Mail-Adresse `<account2@outlook.com>` bereits einem anderen Konto auf nuget.org (z. B. `MyNuGetAccount2`) zugeordnet.

Sie können das für die Anmeldung verwendete Konto nicht durch ein Microsoft-Konto ersetzen, das mit einem anderen Konto auf nuget.org verknüpft ist.

**Ich habe vergessen, dass ich schon ein Konto auf nuget.org besitze. Wie finde heraus, um welches Konto es sich handelt?**

Melden Sie sich mit dem zweiten Microsoft-Konto auf der [Anmeldeseite](https://www.nuget.org/users/account/LogOn?returnUrl=%2F# "Anmeldeseite") an. Dadurch werden Sie bei dem Konto auf nuget.org angemeldet, dem das zweite Microsoft-Konto derzeit zugeordnet ist. Sie können dann die hochgeladenen Pakete sehen und das Konto verwalten.

**Ich benötige das zweite Konto auf nuget.org nicht, sondern möchte nur die Anmeldung für das erste Konto durch das zweite Microsoft-Konto ersetzen. Wie gehe ich vor?**

Wenn Sie das zweite Konto auf nuget.org nicht benötigen und das zugeordnete Microsoft-Konto mit der E-Mail-Adresse `account2@outlook.com` freigeben und erneut verwenden möchten, 

können Sie die Verknüpfung des Microsoft-Kontos mit dem NuGet-Konto aufheben, indem Sie das entsprechende Konto auf nuget.org löschen.
1. Befolgen Sie die Schritte zum [Löschen eines Benutzers](#how-to-delete-my-nugetorg-account) für das zweite Konto auf nuget.org (`MyNuGetAccount2`). 
1. Nachdem dieses Konto gelöscht wurde, können Sie die Schritte zum [Ändern des Microsoft-Kontos für die Anmeldung](#how-to-change-the-microsoft-account-i-use-for-nugetorg-login) wiederholen.

**Ich benötige das zweite Konto ebenfalls. Ich möchte dieses Konto behalten und das Konto für die Anmeldung beim ersten Konto ändern.**

Sie müssen ein drittes Microsoft-Konto erstellen oder verwenden (z. B. mit der E-Mail-Adresse `account3@outlook.com`). 
1. Zunächst sollten Sie sich mit dem zweiten Microsoft-Konto (`account2@outlook.com`) auf nuget.org anmelden. Befolgen Sie die oben aufgeführten Schritte, um die zugehörigen Konten für die Anmeldung zu ändern und das dritte Microsoft-Konto diesem Konto auf nuget.org zuzuordnen.
1. Anschließend kann Ihr zweites Microsoft-Konto mit der E-Mail-Adresse `account2@outlook.com` dem ersten Konto auf nuget.org (`MyNuGetAccount1`) zugeordnet werden. Befolgen Sie die gleichen Schritte erneut, um das Microsoft-Konto für die Anmeldung auf das zweite Microsoft-Konto festzulegen.

### <a name="signing-in-with-microsoft-account-shows-me-my-email-is-linked-to-another-microsoft-account"></a>Bei der Anmeldung mit dem Microsoft-Konto wird angezeigt, dass die E-Mail-Adresse mit einem anderen Microsoft-Konto verknüpft ist
Sie haben versucht, sich mit Ihrem Microsoft-Konto anzumelden (z. B. mit der E-Mail-Adresse `account1@outlook.com`), und es wird folgende Fehlermeldung angezeigt:
> _The account with email 'account1@outlook.com' is linked with another Microsoft account._ (Das Konto mit der E-Mail-Adresse „account1@outlook.com“ ist mit einem anderen Microsoft-Konto verknüpft.)
>
> _If you would like to update the linked Microsoft account you can do so from the account settings page._ (Sie können das verlinkte Microsoft-Konto über die Seite „Kontoeinstellungen“ ändern.)

**Was bedeutet diese Fehlermeldung?**

Wenn ein Konto auf nuget.org erstellt wird, ist diesem eine E-Mail-Adresse für die Kommunikation zugeordnet. Diese entspricht üblicherweise der E-Mail-Adresse des zugeordneten Microsoft-Kontos. Sie können jedoch eine andere E-Mail-Adresse festlegen, über die die Kommunikation erfolgen soll. Sie können also ein anderes Microsoft-Konto besitzen (z. B. mit der E-Mail-Adresse `account2@outlook.com`), das mit einem Konto auf nuget.org verknüpft ist, dessen E-Mail-Adresse für die Kommunikation auf `account1@outlook.com` festgelegt ist.

Der oben aufgeführte Fehler bedeutet also, dass bereits ein Konto auf nuget.org vorhanden ist, dessen E-Mail-Adresse für die Kommunikation auf `account1@outlook.com` festgelegt ist, das mit einem anderen Microsoft-Konto verknüpft ist, dessen E-Mail-Adresse **nicht** `account1@outlook.com` lautet.

**Wie finde ich heraus, welches Microsoft-Konto mit meinem Konto auf nuget.org verknüpft ist?**

Sie sollten sich die Anleitung zur [Hilfe bei der Anmeldung](#which-microsoft-account-is-linked-to-my-nugetorg-account) befolgen, um herauszufinden, welches Microsoft-Konto mit dem Konto auf nuget.org verknüpft ist, das beispielsweise die E-Mail-Adresse `account1@outlook.com` aufweist.

**Ich möchte dieses Konto durch mein Microsoft-Konto ersetzen**

Befolgen Sie die Schritte im Abschnitt [Ich kann mein Microsoft-Konto nicht verwenden. Wie kann ich mein Konto auf nuget.org wiederherstellen?](#unable-to-use-microsoft-login-how-do-i-recover-my-nugetorg-account), um Ihr Microsoft-Konto mit dem vorhandenen Konto auf nuget.org zu verknüpfen.

### <a name="unable-to-use-microsoft-login-how-do-i-recover-my-nugetorg-account"></a>Ich kann mein Microsoft-Konto nicht verwenden. Wie kann ich mein Konto auf nuget.org wiederherstellen?

Wenn Sie die Anleitung zur [Hilfe bei der Anmeldung](#which-microsoft-account-is-linked-to-my-nugetorg-account) befolgt haben und dennoch nicht auf das Microsoft-Konto zugreifen können, das dem Konto auf nuget.org zugeordnet ist, befolgen Sie diese Schritte, um ein neues Microsoft-Konto mit Ihrem Konto auf nuget.org zu verknüpfen.
1. **Voraussetzung:** Sie müssen auf ein Microsoft-Konto zugreifen können (das mit keinem vorhandenen Konto auf nuget.org verknüpft ist). Wenn Sie kein Konto besitzen, können Sie eines [erstellen](https://signup.live.com).
2. Befolgen Sie die [Schritte zum Wiederherstellen Ihres Kennworts](#how-to-recover-nugetorg-password-login). Wenn Sie Ihr Kennwort nicht vergessen haben, können Sie diesen Schritt überspringen.
3. [Melden Sie sich mit Ihrem Benutzernamen und Kennwort auf nuget.org an.](https://www.nuget.org/users/account/LogOnNuGetAccount)
4. Nach der Anmeldung wird ein Popupfenster angezeigt. In diesem Dialogfeld werden Sie über die Aufhebung des Kennworts informiert.
5. **HINWEIS**: Ignorieren Sie die Anweisung, sich mit dem angegebenen Microsoft-Konto anzumelden. Sie können Ihr Konto auf nuget.org nun mit einem anderen Microsoft-Konto verknüpfen.
6. Klicken Sie auf **Sign in with Microsoft** (Mit Microsoft anmelden), und melden Sie sich wie in Schritt 1 erläutert mit dem Microsoft-Konto an, auf das Sie zugreifen können.
7. Ihr Konto wird nun mit dem neuen Microsoft-Konto verknüpft, und Sie können sich mit diesem Konto nun auf nuget.org anmelden.

    ![Dialogfeld: Verknüpfung des MSA-Kontos](media/link-msa-dialog.png)

### <a name="how-to-transform-my-nugetorg-account-to-an-organization"></a>Wie kann ich mein Konto auf nuget.org auf ein Organisationskonto umstellen?

Wenn Sie Ihr Konto auf ein Organisationskonto umstellen möchten und diesem bereits ein Microsoft-Konto für die Anmeldung zugeordnet ist, befolgen Sie die Schritte in der Dokumentation für [Organisationen auf nuget.org](https://docs.microsoft.com/en-us/nuget/reference/organizations-on-nuget-org).

Wenn Ihr Konto auf nuget.org jedoch nicht mit einem Microsoft-Konto verknüpft ist, können Sie folgende Schritte befolgen, um dieses Konto auf ein Organisationskonto umzustellen.
1. **Voraussetzung:** Sie müssen zunächst ein einzelnes Konto auf nuget.org erstellen, das als Administrator für das Organisationskonto fungiert. Wenn Sie noch kein Konto besitzen, [erstellen Sie ein neues auf nuget.org](#how-to-create-a-nugetorg-account).
2. Befolgen Sie die [Schritte zum Wiederherstellen des Kennworts](#how-to-recover-nugetorg-password-login) für Ihr Konto auf nuget.org, wenn Sie Ihr Kennwort vergessen haben. Wenn das nicht der Fall ist, können Sie diesen Schritt überspringen.
3. [Melden Sie sich mit Ihrem Benutzernamen und Kennwort auf nuget.org an.](https://www.nuget.org/users/account/LogOnNuGetAccount)
4. Nach der Anmeldung wird ein Popupfenster angezeigt. In diesem Dialogfeld werden Sie über die Aufhebung des Kennworts informiert. 
    > [!Important]
    > Ignorieren Sie dieses Dialogfeld. Klicken Sie **nicht** auf **Sign in with Microsoft** (Mit Microsoft anmelden).

5. Wechseln Sie zu [https://www.nuget.org/account/transform](https://www.nuget.org/account/transform). Dort können Sie Ihr Konto auf nuget.org auf ein Organisationskonto umstellen, ohne dieses mit einem Microsoft-Konto zu verknüpfen.
6. Geben Sie den Administratorbenutzernamen für Ihr persönliches Konto auf nuget.org an bzw. für das Konto, das Sie in Schritt 1 erstellt haben.
7. Befolgen Sie die Anweisungen, um die Umstellung des Kontos auf ein Organisationskonto abzuschließen.

    ![Dialogfeld: Verknüpfung des MSA-Kontos](media/link-msa-dialog.png)

### <a name="nugetorg-login-issues-for-aad-accounts-with-unmanaged-tenant"></a>Probleme bei der Anmeldung auf nuget.org mit AAD-Konten mit nicht verwalteten Mandanten

Wenn bei der Anmeldung mit Ihrer E-Mail-Kontodomäne (@yourdomain.com) folgender Fehler angezeigt wird, befolgen Sie diese Schritte, um Ihr Konto auf nuget.org wiederherzustellen.

<p align="center">
    <img src="media/unmanaged-aad-tenant.png" />
</p>

**Was bedeutet der Status „Nicht verwaltet“ während der Anmeldung? Warum wird dieser angezeigt?** 

Ihr Konto wurde als persönliches Microsoft-Konto registriert und hat problemlos funktioniert. Nun wurde Ihr Konto jedoch als Mandant mit dem Status „Nicht verwaltet“ in Azure Active Directory registriert (der Identitätsdienst, der verwendet wird, um Microsoft-Konten zu authentifizieren). 

Dies kann der Fall sein, wenn Sie oder ein Mitglied Ihrer Organisation (mit der E-Mail-Adresse @yourdomain.com) sich bei einem integrierten AAD-Dienst registriert oder die [Self-Service-Registrierung für Azure Active Directory](https://docs.microsoft.com/en-us/azure/active-directory/users-groups-roles/directory-self-service-signup) eingerichtet haben. Dadurch wird ein Mandant mit dem Status „Nicht verwaltet“ für die verwendete Microsoft-Kontodomäne (in diesem Fall @yourdomain.com) erstellt. 

**Wie kann ich mein Konto wiederherstellen?**

Derzeit ist es nicht möglich, Konten auf nuget.org zu authentifizieren, die in Azure Active Directory den Status „Nicht verwaltet“ aufweisen. Es wird jedoch an einer Möglichkeit gearbeitet, solche Konten authentifizieren zu können.

Wenn Sie sich auf nuget.org mit Ihrem Microsoft-Konto (@yourdomain.com) anmelden möchten, müssen Sie (oder ein Administrator Ihres Unternehmens) den Besitz des AAD-Kontos beanspruchen, indem Sie eine DNS-Überprüfung durchführen, um Benutzer mit der E-Mail-Adresse @yourdomain.com zu authentifizieren. Befolgen Sie die Schritte zur [Übernahme von Domänen durch Administratoren](https://docs.microsoft.com/en-us/azure/active-directory/users-groups-roles/domains-admin-takeover), die in der Dokumentation zu Azure Active Directory beschrieben werden. Anschließend sollten Sie sich mit diesem Konto anmelden können.

**Ich möchte diese Methode nicht anwenden. Gibt es eine andere Möglichkeit, mein Konto wiederherzustellen?**

Sie können ein neues Microsoft-Konto [erstellen](https://www.microsoft.com/en-us/account), dessen E-Mail-Adresse **nicht** zu @yourdomain.com gehört. Befolgen Sie hierfür die Schritte im Abschnitt zum [Wiederherstellen von Konten auf nuget.org](#unable-to-use-microsoft-login-how-do-i-recover-my-nugetorg-account).

### <a name="how-do-i-change-my-nugetorg-account-username"></a>Wie kann ich den Benutzernamen meines Kontos auf nuget.org ändern?

Sie können den Benutzernamen nicht ändern. Gemäß unseren Richtlinien ist eine Änderung des Benutzernamens derzeit nicht zulässig. Sie können Ihren Benutzernamen lediglich ändern, indem Sie ein neues Konto mit dem gewünschten Benutzernamen erstellen. Es wird empfohlen, Ihr bestehendes Konto zu löschen, bevor Sie ein neues erstellen. Andernfalls können Sie Ihr registriertes Microsoft-Konto nicht für das neue Konto verwenden.
> [!Important]
> Durch das Löschen des Kontos bleibt der `username` dennoch **reserviert**. Sie können den gleichen Benutzernamen nicht noch einmal verwenden, auch dann nicht, wenn Sie **die Groß- und Kleinschreibung ändern**. Wenn Sie beispielsweise ein Konto mit dem Benutzernamen `mycoolname` erstellt haben und diesen in `MyCoolName` (geänderte Groß- und Kleinschreibung) ändern möchten, ist dieser Vorgang auch nach dem Löschen des Kontos nicht möglich.

Befolgen Sie die Schritte im Abschnitt zum [Löschen Ihres Kontos auf nuget.org](#how-to-delete-my-nugetorg-account) und zum [Registrieren eines neuen Kontos](#how-to-create-a-new-nugetorg-account), um ein Konto mit einem zulässigen Benutzernamen zu erstellen.

### <a name="how-to-delete-my-nugetorg-account"></a>Wie kann ich mein Konto auf nuget.org löschen?

Es wird empfohlen, den Besitz aller Pakete, deren alleiniger Besitzer Sie sind, auf ein anderes Konto zu übertragen, bevor Sie Ihr Konto löschen. Weitere Informationen zu diesem Thema finden Sie unter [Verwalten von Paketbesitzern auf nuget.org](https://docs.microsoft.com/en-us/nuget/create-packages/publish-a-package#managing-package-owners-on-nugetorg). Hierdurch können wir Ihre Anforderung schneller verarbeiten.

> [!Important]
> Das Löschen Ihres Kontos hat folgende Auswirkungen:
>  1. Zugehörige API-Schlüssel werden widerrufen. 
>  2. Das Konto wird als Besitzer aller untergeordneten Pakete entfernt.
>  3. Alle ID-Präfixe, die mit diesem Konto reserviert wurden, werden freigegeben.
>  4. Die Mitgliedschaft des Kontos in sämtlichen Organisationen wird aufgehoben.
>  5. Ihr Benutzername wird reserviert, und kein Benutzer kann ihn ohne die entsprechende Berechtigung erneut verwenden.

Befolgen Sie diese Schritte, um mit der Löschung Ihres Kontos fortzufahren:
1. [Melden Sie sich mit dem Konto auf nuget.org an](https://www.nuget.org/users/account/LogOn), das Sie löschen möchten.
2. Klicken Sie auf die URL [https://www.nuget.org/account/delete](https://www.nuget.org/account/delete), und befolgen Sie die Schritte, um die Anforderung zum Löschen des Kontos zu übermitteln.

Der Kundensupport verarbeitet Ihre Anforderung und löscht das Konto.