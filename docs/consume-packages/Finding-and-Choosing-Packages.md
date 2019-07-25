---
title: Suchen und Wählen von NuGet-Paketen
description: Eine Übersicht darüber, wie Sie die besten NuGet-Pakete für ein Projekt suchen und auswählen sowie Details zur Syntax der NuGet-Suche.
author: karann-msft
ms.author: karann
ms.date: 06/04/2018
ms.topic: conceptual
ms.openlocfilehash: 3af29e2f9b09ba5bd82779f9aacf314bd8933436
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/18/2019
ms.locfileid: "68317025"
---
# <a name="finding-and-evaluating-nuget-packages-for-your-project"></a>Suchen und Auswerten von NuGet-Paketen für Ihr Projekt

Wenn Sie ein .NET-Projekt starten oder bei Ihrer App bzw. Ihrem Dienst eine funktionale Anforderung vorliegt, können Sie viel Zeit und Aufwand sparen, indem Sie vorhandene NuGet-Pakete verwenden, um diese Anforderung zu erfüllen. Diese Pakete können von der öffentlichen Auflistung auf [nuget.org](http://www.nuget.org/packages/) oder von einer privaten Quelle stammen, die von Ihrer Organisation oder einem Drittanbieter bereitgestellt wird.

## <a name="finding-packages"></a>Suchen von Paketen

Wenn Sie nuget.org besuchen oder die Benutzeroberfläche des Paket-Managers in Visual Studio öffnen, wird Ihnen eine Liste der Pakete angezeigt, die nach der Gesamtanzahl der Downloads sortiert ist. Dadurch werden Ihnen sofort die für Millionen von .NET-Projekten am häufigsten verwendeten Pakete angezeigt. Es bestehen gute Chancen, dass mindestens eins der auf den ersten Seiten aufgelisteten Pakete für Ihre Projekte nützlich ist.

![Die Standardansicht von nuget.org/packages zeigt die beliebtesten Pakete an](media/Finding-01-Popularity.png)

Beachten Sie die Option **Vorabversion einbeziehen** in der oberen rechten Ecke der Seite. Wenn diese ausgewählt ist, zeigt nuget.org alle Version von Paketen an, einschließlich Betaversionen und anderen frühen Releases. Deaktivieren Sie diese Option, um nur stabile Releases anzuzeigen.

Bei besonderen Anforderungen ist das Suchen mithilfe von Tags (im Paket-Manager von Visual Studio oder in einem Portal wie nuget.org) die am häufigsten verwendete Vorgehensweise, um geeignete Pakete zu ermitteln. Wenn Sie beispielsweise nach „json“ suchen, werden alle NuGet-Pakete aufgelistet, die mit diesem Schlüsselwort kategorisiert sind und daher einen Bezug zum JSON-Datenformat aufweisen.

![Suchergebnisse für „json“ auf nuget.org](media/Finding-02-SearchResults.png)

Sie können ebenfalls mithilfe der Paket-ID suchen, falls Ihnen diese bekannt ist. Weitere Informationen finden Sie unter[Syntax der Suche](#search-syntax).

Derzeit sind die Suchergebnisse nur nach Relevanz sortiert, sodass Sie die ersten Seiten der Ergebnisse nach Paketen durchsuchen sollten, die Ihren Anforderungen entsprechen. Alternativ können Sie Ihre Suchbegriffe präzisieren, um spezifischere Ergebnisse zu erhalten.

### <a name="does-the-package-support-my-projects-target-framework"></a>Unterstützt das Paket das Zielframework des Projekts?

NuGet installiert ein Paket nur in ein Projekt, wenn die vom Paket unterstützten Frameworks das Zielframework des Projekts enthalten. Wenn das Paket nicht kompatibel ist, gibt NuGet einen Fehler aus.

Einige Pakete führen die unterstützten Frameworks direkt im Katalog von nuget.org auf, viele Pakete enthalten diese Auflistung jedoch nicht, da solche Daten nicht erforderlich sind. Derzeit gibt es keine Möglichkeit, nuget.org nach Paketen zu durchsuchen, die ein bestimmtes Zielframework unterstützen, dieses Feature befindet sich jedoch in der Diskussion. Weitere Informationen dazu finden Sie unter [NuGet Issue 2936 (NuGet-Problem 2936)](https://github.com/NuGet/NuGetGallery/issues/2936).

Es stehen jedoch zwei andere Möglichkeiten zur Verfügung, um unterstützte Frameworks zu bestimmen:

1. Versuchen Sie, ein Paket mithilfe des Befehls [`Install-Package`](../reference/ps-reference/ps-ref-install-package.md) über die Konsole des NuGet-Paket-Managers in ein Projekt zu installieren. Wenn das Paket nicht kompatibel ist, zeigt dieser Befehl Ihnen die unterstützten Frameworks des Pakets an.

1. Laden Sie das Paket von dessen Seite auf nuget.org herunter, indem Sie den Link **Manueller Download** unter **Info** verwenden. Ändern Sie die Erweiterung von `.nupkg` in `.zip`, und öffnen Sie die Datei, um den Inhalt des `lib`-Ordners zu überprüfen. Dort werden Ihnen die Unterordner für jedes unterstützte Framework angezeigt. Jeder dieser Unterordner ist mit einem Zielframeworkmoniker benannt (TFM, siehe [Target Frameworks (Zielframeworks)](../reference/target-frameworks.md)). Wenn unter `lib` keine Unterordner und nur eine einzige DLL angezeigt werden, müssen Sie versuchen, das Paket in Ihrem Projekt zu installieren, um die Kompatibilität zu ermitteln.

## <a name="pre-release-packages"></a>Vorabversionen von Paketen

Viele Paketersteller stellen Vorschau- und Betaversionen bereit, da weiterhin Verbesserungen vorgenommen werden und Feedback zu den aktuellen Revisionen gewünscht wird.

Standardmäßig zeigt nuget.org auch Vorabversionen von Paketen in den Suchergebnissen an. Deaktivieren Sie die Option **Vorabversion einbeziehen** in der oberen rechten Ecke der Seite, um ausschließlich nach stabilen Releases zu suchen.

![Kontrollkästchen „Vorabversion einbeziehen“ auf nuget.org](media/Finding-06-include-prerelease.png)

Wenn Sie Visual Studio und die NuGet- und dotnet-CLI-Tools verwenden, enthält NuGet standardmäßig keine Vorabversionen. Führen Sie folgende Schritte aus, um dieses Verhalten zu ändern:

- **Benutzeroberfläche des Paket-Managers in Visual Studio**: Aktivieren Sie in der Benutzeroberfläche **NuGet-Pakete verwalten** das Kontrollkästchen **Vorabversion einbeziehen**. Wenn Sie dieses Kontrollkästchen aktivieren oder deaktivieren, wird die Benutzeroberfläche des Paket-Managers sowie die Liste der verfügbaren Versionen aktualisiert, die Sie installieren können.

    ![Kontrollkästchen „Vorabversion einbeziehen“ in Visual Studio](media/Prerelease_02-CheckPrerelease.png)

- **Paket-Manager-Konsole**: Verwenden Sie den Schalter `-IncludePrerelease` zusammen mit den Befehlen `Find-Package`, `Get-Package`, `Install-Package`, `Sync-Package` und `Update-Package`. Lesen Sie hierzu die [PowerShell-Referenz](../reference/powershell-reference.md).

- **nuget.exe-CLI**: Verwenden Sie den Schalter `-prerelease` zusammen mit den Befehlen `install`, `update`, `delete` und `mirror`. Weitere Informationen finden Sie in der [NuGet CLI reference (Referenz für die NuGet-CLI)](../reference/nuget-exe-cli-reference.md).

- **dotnet.exe-CLI**: Geben Sie die genaue Vorabversion mit dem Argument `-v` an. Informationen finden Sie in der [Referenz zu „dotnet add package“](/dotnet/core/tools/dotnet-add-package).

<a name="native-cpp-packages"></a>

### <a name="native-c-packages"></a>Native C++-Pakete

NuGet unterstützt native C++-Pakete, die in C++-Projekten in Visual Studio verwendet werden können. Dadurch wird der Kontextmenübefehl **NuGet-Pakete verwalten** für Projekte aktiviert, das Zielframework `native` eingeführt und die Integration von MSBuild bereitgestellt.

Suchen Sie mit `tag:native`, um native Pakete auf [nuget.org](https://www.nuget.org/packages) zu finden. Solche Paketen stellen üblicherweise `.targets`- und `.props`-Dateien bereit, die NuGet automatisch importiert, wenn das Paket zu einem Projekt hinzugefügt wird.

## <a name="evaluating-packages"></a>Auswerten von Paketen

Am besten bewerten Sie, ob ein Paket nützlich ist, indem Sie es herunterladen und in Ihrem Code ausprobieren (alle Pakete auf nuget.org werden übrigens routinemäßig auf Viren überprüft). Jedes beliebte Paket wurde schließlich zuerst nur von wenigen Entwicklern verwendet. Sie könnten somit zu den Erstanwendern gehören.

Allerdings bedeutet das Verwenden eines NuGet-Pakets auch, dass eine Abhängigkeit davon entsteht. Darum sollten Sie sicherstellen, dass das Paket robust und zuverlässig ist. Da es sehr zeitaufwändig ist, ein Paket zu installieren und direkt zu testen, können Sie ebenfalls die Informationen auf der Angebotsseite eines Pakets verwenden, um mehr über die Qualität des Pakets zu erfahren.

- *Downloadstatistiken:* Der Abschnitt **Statistiken** auf der Seite für Pakete auf nuget.org zeigt die Gesamtanzahl der Downloads, die Anzahl von Downloads der aktuellen Version und die durchschnittliche Anzahl von Downloads pro Tag. Eine hohe Zahl gibt hierbei an, dass viele andere Entwickler eine Abhängigkeit von diesem Paket erstellt haben. Das bedeutet, dass das Paket sich bewiesen hat.

    ![Downloadstatistiken auf der Angebotsseite eines Pakets](media/Finding-03-Downloads.png)

- *Versionsverlauf:* Auf der Seite für Pakete wird unter **Info** das Datum des aktuellen Updates angezeigt, außerdem können Sie dort den **Versionsverlauf** überprüfen. Ein gut verwaltetes Paket verfügt über aktuelle Updates und einen umfangreichen Versionsverlauf. Ein schlecht verwaltetes Paket verfügt über wenige Updates bzw. wurde häufig für längere Zeit nicht mehr aktualisiert.

    ![Versionsverlauf auf der Angebotsseite eines Pakets](media/Finding-04-VersionHistory.png)

- *Aktuelle Installationen:* Klicken Sie auf der Seite für Pakete unter **Statistiken** auf **View full stats** (Vollständige Statistiken anzeigen). Die Seite „Vollständige Statistiken“ zeigt die Installationen des Pakets in den letzten sechs Wochen nach Versionsnummer geordnet an. Ein Paket, das aktiv von anderen Entwicklern verwendet wird, ist häufig eine bessere Wahl als eines, das nicht aktiv verwendet wird.

- *Support:* Klicken Sie auf der Seite für Pakete unter **Info** auf **Projektwebsite** (falls vorhanden), um die vom Autor angegebenen Supportoptionen anzuzeigen. Ein Projekt mit einer dedizierten Website wird üblicherweise besser unterstützt.

- *Entwicklerverlauf:* Wählen Sie auf der Seite für Pakete unter **Besitzer** einen Besitzer aus, um anzuzeigen, welche anderen Pakete dieser veröffentlicht hat. Bei Entwicklern, die mehrere Pakete veröffentlicht haben, ist es wahrscheinlicher, dass diese ihre Arbeit auch zukünftig fortsetzen.

- *Open Source-Beiträge:* Manche Pakete befinden sich in Open Source-Repositorys. Dadurch wird es Entwicklern ermöglicht, die von diesen abhängig sind, Problembehebungen und Verbesserungen von Features direkt beizutragen. Der Beitragsverlauf eines Pakets zeigt ebenfalls an, wie viele Entwickler sich aktiv am Paket beteiligen.

- *Kontaktieren der Besitzer:* Neue Entwickler können gleichermaßen dazu fähig sein, für Sie nützliche Pakete zu erstellen. Es ist daher ratsam, diesen eine Chance zu geben, NuGet mit neuen Inhalten zu bereichern. Nutzen Sie deshalb die Option **Contact Owners** (Besitzer kontaktieren), die sich auf der Angebotsseite unter **Info** befindet, um Paketentwickler direkt zu kontaktieren. Diese arbeiten sicherlich gerne mit Ihnen zusammen, um Ihre Vorstellungen umzusetzen.

- *Reservierte Paket-ID-Präfixe*: Viele Paketbesitzer haben ein [reserviertes Paket-ID-Präfix](../nuget-org/id-prefix-reservation.md) beantragt und erhalten. Wenn Sie auf [nuget.org](https://www.nuget.org/) oder in Visual Studio das Häkchen neben einer Paket-ID sehen, bedeutet dies, dass der Paketbesitzer unsere [Kriterien](../nuget-org/id-prefix-reservation.md#id-prefix-reservation-criteria) für die ID-Präfixreservierung erfüllt hat. Dies bedeutet, dass der Paketbesitzer sich und sein Paket eindeutig identifizieren kann.

> [!Note]
> Sie sollten stets die Lizenzbedingungen eines Pakets beachten. Diese können Sie anzeigen, indem Sie auf der Angebotsseite eines Pakets auf nuget.org auf **License Info** (Lizenzinformationen) klicken. Wenn ein Paket keine Lizenzbedingungen angibt, kontaktieren Sie den Paketbesitzer direkt, indem Sie den Link **Contact owners** (Besitzer kontaktieren) auf der Seite für Pakete verwenden. Microsoft lizenziert kein geistiges Eigentum von Drittanbietern für Pakete und ist nicht verantwortlich für die durch Drittanbieter bereitgestellten Inhalte.

## <a name="license-url-deprecation"></a>Veralten der Lizenz-URL
Beim Übergang von [licenseUrl](../reference/nuspec.md#licenseurl) zu [Lizenz](../reference/nuspec.md#license) haben einige NuGet-Clients und NuGet-Feeds möglicherweise in einigen Fällen noch nicht die Möglichkeit, Informationen zur Lizenzierung anzuzeigen. Um Abwärtskompatibilität zu gewährleisten, zeigt die Lizenz-URL auf dieses Dokument, das Informationen zum Abrufen der Lizenzinformationen in solchen Fällen enthält.

Wenn Sie durch Klicken auf die Lizenz-URL für ein Paket auf diese Seite weitergeleitet wurden, zeigt dies, dass das Paket eine Lizenzdatei enthält, und
* Sie sind mit einem Feed verbunden, der noch nicht weiß, wie die neuen Lizenzinformationen zu interpretieren sind und dem Client angezeigt werden müssen, **ODER**
* Sie verwenden einen Client, der noch nicht weiß, wie die neuen Lizenzinformationen zu interpretieren und zu lesen sind, die potenziell durch den Feed bereitgestellt werden, **ODER**
* eine Kombination aus beidem.

So könnten Sie die Informationen lesen, die in der Lizenzdatei des Pakets enthalten sind:
1. Laden Sie das NuGet-Paket herunter, und entzippen Sie seinen Inhalt in einen Ordner.
1. Öffnen Sie die `.nuspec`-Datei, die sich im Stammverzeichnis dieses Ordners befindet.
1. Sie sollte ein Tag wie `<license type="file">license\license.txt</license>` haben. Dies bedeutet, dass die Lizenzdatei den Namen `license.txt` hat und sich in einem Ordner namens `license` befindet, der sich auch im Stammverzeichnis dieses Ordners befindet.
1. Navigieren Sie zum `license`-Ordner, und öffnen Sie die `license.txt`-Datei.


## <a name="search-syntax"></a>Suchsyntax

Die NuGet-Paketsuche auf nuget.org, über die NuGet-CLI und mit der Erweiterung des NuGet-Paket-Managers in Visual Studio funktionieren auf die gleiche Weise. Im Allgemeinen wird die Suche auf Schlüsselwörter und auf die Paketbeschreibungen angewendet.

- **Schlüsselwörter:** Die Suche ermittelt relevante Pakete, die eines der bereitgestellten Schlüsselwörter enthalten. Beispiel: `modern UI` Verwenden Sie„+“ zwischen Begriffen wie `modern+UI`, um nach Paketen zu suchen, die alle der angegebenen Schlüsselwörter enthalten.
- **Ausdrücke:** Wenn Sie Begriffe in Anführungszeichen eingeben, ermittelt die Suche Übereinstimmungen mit diesen Begriffen, bei denen die Groß-/Kleinschreibung nicht berücksichtigt wird. Ein Beispiel: `"modern UI" package`
- **Filtern:** Sie können einen Suchbegriff auf eine bestimmte Eigenschaft anwenden, indem Sie die Syntax `<property>:<term>` verwenden. Hierbei kann `<property>` (Groß-/Kleinschreibung wird nicht berücksichtigt) `id`, `packageid`, `version`, `title`, `tags`, `author`, `description`, `summary` oder `owner` entsprechen. Bei Bedarf können diese Begriffe in Anführungszeichen eingegeben werden, außerdem können Sie nach mehreren Eigenschaften gleichzeitig suchen. Darüber hinaus handelt es sich bei Suchen mit der `id`-Eigenschaft um Übereinstimmungen von Teilzeichenfolgen, während mit `packageid` nach einer genauen Übereinstimmung gesucht wird. Beispiele:

    ```
    id:NuGet.Core                # Match any part of the id property
    Id:"Nuget.Core"
    ID:jQuery
    title:jquery                 # Searches title as shown on the package listing
    PackageId:jquery             # Match the package id exactly
    id:jquery id:ui              # Search for multiple terms in the id
    id:jquery tags:validation    # Search multiple properties
    id:"jquery.ui"               # Phrase search
    invalid:jquery ui            # Unsupported properties are ignored, so this
                                 # is the same as searching on jquery ui
    ```
