---
title: Häufig gestellte Fragen zu NuGet
description: Häufig gestellte Fragen und entsprechende Antworten zur Verwendung von NuGet über die Befehlszeile und in Visual Studio sowie zum Arbeiten mit dem NuGet-Katalog.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 01/11/2018
ms.topic: conceptual
ms.openlocfilehash: 3fe59ef03632053182b034052e93a5f2e6f444bd
ms.sourcegitcommit: c643dd2c44e085601551ff7079d696bcc3ad2b49
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/21/2018
ms.locfileid: "42792938"
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
- Visual Studio Team Services stellt [einen Buildschritt für das Wiederherstellen von NuGet-Paketen](/vsts/build-release/tasks/package/nuget) bereit. Sie können ebenfalls [private NuGet-Paketfeeds auf Team Services hosten](https://www.visualstudio.com/docs/package/nuget/publish).

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

**Beim Versuch, die $DTE-Variable in den Typ DTE2 umzuwandeln, wird eine Fehlermeldung ausgegeben: „Der Wert ‚EnvDTE.DTEClass‘ vom Typ ‚EnvDTE.DTEClass‘ kann nicht in den Typ ‚EnvDTE80.DTE2‘ konvertiert werden.“ Wo liegt der Fehler?**

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

Zusätzlich stellt das Hochladen von Paketen auf [staging.nuget.org](http://staging.nuget.org) eine gute Möglichkeit zum Testen und Überprüfen des Pakets dar, ohne dieses im öffentlichen Katalog zur Verfügung zu stellen.

**Ist es möglich, Namen für Pakete zu reservieren, die in Zukunft veröffentlicht werden sollen?**

Ja. Sie können IDs für Pakete auf [nuget.org](https://www.nuget.org/) reservieren, indem Sie ein Präfix für eine Paket-ID für Ihr Konto anfordern. Wenn Sie ein Präfix für die Paket-ID anfordern möchten, folgen Sie den Anweisungen in der [Dokumentation](https://docs.microsoft.com/nuget/reference/id-prefix-reservation).

**Wie kann der Besitz eines Pakets beansprucht werden?**

Weitere Informationen finden Sie unter [Managing package owners on nuget.org (Verwalten von Paketbesitzern auf nuget.org)](../create-packages/publish-a-package.md#managing-package-owners-on-nugetorg).

**Wie kann vorgegangen werden, wenn ein Paketbesitzer meine Softwarelizenzbedingungen verletzt?**

Es wird empfohlen, dass die NuGet-Community zusammenarbeitet, um Streitfälle zwischen Paketbesitzern und den Besitzern von anderer Software zu klären. Es wurde eine [Vorgehensweise zum Lösen von Streitfällen](../policies/dispute-resolution.md) entworfen, die Sie befolgen sollten, bevor Sie um das Eingreifen der Administratoren von nuget.org bitten.

**Ist es empfehlenswert, meine Testpakete auf nuget.org hochzuladen?**

Für Testzwecke können Sie [staging.nuget.org](http://staging.nuget.org), öffentliche NuGet-Server wie [myget.org](https://myget.org) oder [Visual Studio Team Services](https://blogs.msdn.microsoft.com/visualstudioalm/2015/08/27/announcing-package-management-support-for-vsotfs/) verwenden.

Beachten Sie, dass Pakete, die auf staging.nuget.org hochgeladen werden, nicht beibehalten werden. Weitere Informationen finden Sie im Artikel [Goodbye preview.nuget.org. Hello staging.nuget.org! (preview.nuget.org wird durch staging.nuget.org ersetzt)](http://blog.nuget.org/20130419/goodbye-preview.html).

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
- Die Version Ihres Betriebssystems
- Die Konfiguration Ihres Computers (CPU, Netzwerk, Festplatte)
- Angabe, ob Ihr Computer einen Proxy oder eine Firewall verwendet
- Die auf Ihrem Computer installierten Versionen von .NET
- Die Versionen der von Ihnen verwendeten plattformübergreifenden Tools wie z.B. die .NET-CLI oder DNU

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

V3: `https://api.nuget.org/v3/index.json` V2: `https://www.nuget.org/api/v2/` (Beachten Sie, dass die V2-API veraltet ist und nicht mit NuGet 4 und höher funktioniert.)
