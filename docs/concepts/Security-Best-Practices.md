---
title: Bewährte Methoden für eine sichere Softwarelieferkette
description: Best Practices zum Schützen Ihrer Softwarelieferkette mithilfe von NuGet und GitHub
author: JonDouglas
ms.author: jodou
ms.date: 02/08/2021
ms.topic: conceptual
ms.openlocfilehash: 4575d4779ed90150cec667489c85875b7fb87a8d
ms.sourcegitcommit: 5f706c62c97b78bbe3d8c7e95659976535fe486f
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/23/2021
ms.locfileid: "122726976"
---
# <a name="best-practices-for-a-secure-software-supply-chain"></a>Bewährte Methoden für eine sichere Softwarelieferkette

Open Source ist überall. Man findet Open Source in vielen proprietären Codebasen und Communityprojekten. Organisationen und Einzelpersonen stellen sich heutzutage nicht die Frage, ob Software auf Open Source basiert oder nicht, sondern welcher Open-Source-Code verwendet werden sollte und in welchem Umfang.

Wenn Sie Ihre Lieferkette nicht kennen, kann ein Sicherheitsrisiko in einer Ihrer Abhängigkeiten in der vorgelagerten Lieferkette verheerend sein. Das führt dazu, dass Sie und Ihre Kunden für eine potenzielle Kompromittierung anfällig werden. In diesem Dokument wird ausführlicher darauf eingegangen, was mit dem Begriff „Softwarelieferkette“ gemeint ist, warum dieser von Bedeutung ist und wie Sie dazu beitragen können, die Lieferkette Ihres Projekts mit Best Practices zu schützen.

![The State of the Octoverse 2020 – Open Source](media/opensource-percent.png)

## <a name="dependencies"></a>Abhängigkeiten 

Der Begriff „Softwarelieferkette“ umfasst alle Elemente, die in Ihrer Software einfließen, und auch woher diese stammen. Dabei handelt es sich um die Abhängigkeiten und Eigenschaften Ihrer Abhängigkeiten, von denen Ihre Softwarelieferkette abhängt. Als Abhängigkeit werden alle Elemente bezeichnet, die Ihre Software benötigt, um ausgeführt werden zu können. Dabei kann es sich um Codeblöcke, Binärdateien oder andere Komponenten handeln und woher diese stammen, z. B. von einem Repository oder Paket-Manager.

Zur Lieferkette gehören außerdem die Person, die den Code geschrieben hat, der Zeitpunkt der Bereitstellung, die Art der Überprüfung auf Sicherheitsprobleme, bekannte Sicherheitsrisiken, unterstützte Versionen, Lizenzinformationen und alle sonstigen Prozesse.

Ihre Lieferkette umfasst auch andere Teile Ihres Stapels als nur die einzelne Anwendung, zum Beispiel Ihre Build- und Paketskripts oder die Software, die die Infrastruktur ausführt, auf der Ihre Anwendung basiert.

## <a name="vulnerabilities"></a>Sicherheitsrisiken

Heute sind Softwareabhängigkeiten in allen Bereichen zu finden. Es kommt häufig vor, dass Softwarehersteller Hunderte von Open-Source-Abhängigkeiten für Funktionalitäten verwenden, damit sie diese nicht selbst schreiben mussten. Dies kann bedeuten, dass der größte Teil Ihrer Anwendung aus Code besteht, den Sie nicht erstellt haben. 

![The State of the Octoverse 2020 – Abhängigkeiten](media/dependencies.png)

Da Sie Ihre Abhängigkeiten von Drittanbietern oder Open-Source-Abhängigkeiten vermutlich nicht so streng kontrollieren können wie den Code, den Sie selbst schreiben, können diese mögliche Sicherheitsrisiken in Ihrer Lieferkette hervorrufen.

Wenn Abhängigkeiten ein Sicherheitsrisiko aufweisen, ist die Wahrscheinlichkeit hoch, dass auch ein Sicherheitsrisiko bei Ihnen auftritt. Dies kann frustrierend sein, da sich eine Ihrer Abhängigkeiten unter Umständen ändert, ohne dass Sie dies überhaupt bemerken. Selbst wenn ein in einer Abhängigkeit vorhandenes Sicherheitsrisiko derzeit noch nicht ausnutzbar ist, kann es in der Zukunft so weit kommen. 

Die Tatsache, dass Sie die Arbeit Tausender Open-Source-Entwickler und Bibliotheksersteller nutzen können, bedeutet auch, dass Tausende fremder Entwickler effektiv an Ihrem Produktionscode mitarbeiten können. Ihr Produkt wird durch Ihre Softwarelieferkette durch nicht gepatchte Sicherheitsrisiken, arglose Fehler oder sogar böswillige Angriffe auf Abhängigkeiten beeinträchtigt.

## <a name="supply-chain-compromises"></a>Kompromittierungen in der Lieferkette

Die gängige Definition einer Lieferkette stammt aus der Fertigungsindustrie und bezeichnet die Prozesskette von der Herstellung bis zum Vertrieb. Diese umfasst die Planung, die Materialbeschaffung, den Herstellungsprozess und den Verkauf. Eine Softwarelieferkette ist ähnlich, nur dass anstelle der Materialien Code genutzt wird. Die Fertigung ist hier die Entwicklung. Anstatt das Erz aus der Erde zu holen, wird Code von Anbietern bezogen (kommerziell oder Open Source), und in der Regel stammt Open-Source-Code aus Repositorys. Das Hinzufügen von Code aus einem Repository bedeutet, dass Ihr Produkt von diesem Code abhängig ist.

Ein Angriff auf die Softwarelieferkette liegt beispielsweise vor, wenn bösartiger Code absichtlich zu einer Abhängigkeit hinzugefügt wird, wobei der Code mithilfe der Lieferkette dieser Abhängigkeit an die Opfer verteilt wird. Angriffe auf Lieferketten sind ernst zu nehmen. Es gibt viele Methoden zum Angriff auf eine Lieferkette, zum Beispiel das direkte Einfügen von schädlichem Code als neuer Mitwirkender, das Übernehmen des Kontos eines Mitwirkenden, ohne dass andere dies bemerken, oder sogar das Kompromittieren eines Signaturschlüssels, um Software zu verteilen, die nicht offiziell Teil der Abhängigkeit ist.

Ein Angriff auf eine Softwarelieferkette ist an und für sich selten das Endziel, sondern eine erste gute Gelegenheit für einen Angreifer, Schadsoftware einzuschleusen oder eine Hintertür für zukünftigen Zugriff bereitzustellen.

![The State of the Octoverse 2020 – Lebenszyklus eines Sicherheitsrisikos](media/vulnerability-lifecycle.png)

## <a name="unpatched-software"></a>Nicht gepatchte Software

Die Verwendung von Open Source hat beträchtliche Ausmaße erreicht und wird wahrscheinlich nicht so bald wieder abnehmen. Da wir die Verwendung von Open-Source-Software nicht unterbinden, stellt die nicht gepatchte Software die größte Bedrohung für die Sicherheit von Lieferketten dar. Wie können Sie ausgehend von dieser Tatsache mit dem Risiko umgehen, dass eine Abhängigkeit Ihres Projekts ein Sicherheitsrisiko aufweist?

- **Kenntnis Ihrer Umgebung:** Dies erfordert die Ermittlung Ihrer Abhängigkeiten und der transitiven Abhängigkeiten, um die Risiken dieser Abhängigkeiten wie Sicherheitsrisiken oder Lizenzierungseinschränkungen zu verstehen.
- **Verwalten Ihrer Abhängigkeiten:** Wenn ein neues Sicherheitsrisiko erkannt wird, müssen Sie feststellen, ob Sie betroffen sind. Wenn dies der Fall ist, führen Sie ein Update auf die aktuelle Version und das neueste verfügbare Sicherheitspatch durch. Dies ist besonders wichtig, um Änderungen zu prüfen, die neue Abhängigkeiten einführen, oder ältere Abhängigkeiten in regelmäßigen Abständen zu überprüfen.
- **Überwachen der Lieferkette:** Die Überwachung erfolgt durch Überprüfung der Kontrollmechanismen, die Ihnen zum Verwalten Ihrer Abhängigkeiten zur Verfügung stehen. Auf diese Weise können Sie restriktivere Bedingungen für Ihre Abhängigkeiten erzwingen.

![The State of the Octoverse 2020 – Empfehlungen](media/advisories.png)

Nachfolgend werden verschiedene Tools und Techniken behandelt, die von NuGet und GitHub bereitstellt werden und die Sie sofort nutzen können, um potenzielle Risiken in Ihrem Projekt zu beheben. 

## <a name="knowing-what-is-in-your-environment"></a>Wissen, was sich in Ihrer Umgebung befindet

### <a name="nuget-dependency-graph"></a>NuGet-Abhängigkeitsdiagramm

**📦 Paketnutzer**

Sie können Ihre NuGet-Abhängigkeiten in Ihrem Projekt anzeigen, indem Sie direkt die entsprechende Projektdatei öffnen.

Diese ist in der Regel an zwei Stellen vorhanden:

-   [`packages.config`](../reference/packages-config.md) – im Projektstamm
-   [`<PackageReference>`](../consume-packages/package-references-in-project-files.md) – in der Projektdatei 

Je nachdem, welche Methode Sie zum Verwalten Ihrer NuGet-Abhängigkeiten verwenden, können Sie auch Visual Studio verwenden, um Ihre Abhängigkeiten direkt im [Projektmappen-Explorer](/visualstudio/ide/solutions-and-projects-in-visual-studio#solution-explorer) oder im [NuGet-Paket-Manager](../consume-packages/install-use-packages-visual-studio.md) anzuzeigen.

In CLI-Umgebungen können Sie den Befehl [`dotnet list package`](/dotnet/core/tools/dotnet-list-package) verwenden, um Ihr Projekt oder die Abhängigkeiten der Projektmappe aufzulisten. 

Weitere Informationen zum Verwalten von NuGet-Abhängigkeiten finden Sie in der [folgenden Dokumentation](../consume-packages/overview-and-workflow.md).

### <a name="github-dependency-graph"></a>GitHub-Abhängigkeitsdiagramm 

**📦 Paketnutzer | 📦🖊 Paketersteller**

Sie können das Abhängigkeitsdiagramm von GitHub verwenden, um die Pakete, von denen Ihr Projekt abhängt, und die von ihm abhängigen Repositorys anzuzeigen. Dies kann Ihnen dabei helfen, erkannte Sicherheitsrisiken in den Abhängigkeiten anzuzeigen.

Weitere Informationen zu Repositoryabhängigkeiten von GitHub finden Sie [in der folgenden Dokumentation](https://github.co/dependency-graph).

### <a name="dependency-versions"></a>Abhängigkeitsversionen

**📦 Paketnutzer | 📦🖊 Paketersteller**

Um eine sichere Lieferkette von Abhängigkeiten sicherzustellen, sollten Sie darauf achten, dass alle Ihre Abhängigkeiten und Tools regelmäßig auf die neueste stabile Version aktualisiert werden, da diese häufig die neuesten Funktionen und Sicherheitspatches für bekannte Schwachstellen enthält. Ihre Abhängigkeiten können Code, von dem Sie abhängig sind, von Ihnen verwendete Binärdateien, von Ihnen verwendete Tools und andere Komponenten enthalten. Das können beispielsweise sein:

-   [Visual Studio](https://visualstudio.microsoft.com/downloads/)
-   [.NET SDK und .NET-Runtime](https://dotnet.microsoft.com/download)
-   [NuGet](https://www.nuget.org/downloads)
-   [NuGet-Pakete](../consume-packages/reinstalling-and-updating-packages.md)

## <a name="manage-your-dependencies"></a>Verwalten Ihrer Abhängigkeiten

### <a name="nuget-deprecated-and-vulnerable-dependencies"></a>Veraltete und anfällige NuGet-Abhängigkeiten

**📦 Paketnutzer | 📦🖊 Paketersteller**

Sie können die [dotnet-CLI](/dotnet/core/tools/dotnet-list-package) verwenden, um alle bekannten veralteten oder anfälligen Abhängigkeiten aufzulisten, die sich möglicherweise in Ihrem Projekt oder in der Projektmappe befinden. Sie können den Befehl `dotnet list package --deprecated` oder `dotnet list package --vulnerable` verwenden, um eine Liste bekannter veralteter Elemente oder Sicherheitsrisiken bereitzustellen.

### <a name="github-vulnerable-dependencies"></a>Anfällige GitHub-Abhängigkeiten

**📦 Paketnutzer | 📦🖊 Paketersteller**

Wenn Ihr Projekt auf GitHub gehostet wird, können Sie die [GitHub-Sicherheit](https://docs.github.com/en/free-pro-team@latest/github/finding-security-vulnerabilities-and-errors-in-your-code/automatically-scanning-your-code-for-vulnerabilities-and-errors) nutzen, um Sicherheitsrisiken und Fehler in Ihrem Projekt zu finden. Dependabot behebt diese Fehler anschließend, indem ein Pull Request für Ihre Codebasis eröffnet wird. 

Ein Ziel der [„Shift Left“](https://en.wikipedia.org/wiki/Shift-left_testing)-Bewegung (Linksverschiebung) ist das Abfangen anfälliger Abhängigkeiten vor deren Einführung. Wenn Sie Informationen zu Ihren Abhängigkeiten wie die Lizenz, transitive Abhängigkeiten und das Alter der Abhängigkeiten haben, können Sie genau das tun.

Weitere Informationen zu Dependabot-Warnungen und -Sicherheitsupdates finden Sie [in der folgenden Dokumentation](https://docs.github.com/en/github/managing-security-vulnerabilities/about-alerts-for-vulnerable-dependencies).

### <a name="nuget-feeds"></a>NuGet-Feeds

**📦 Paketnutzer**

Wenn Sie mehrere öffentliche und private NuGet-Quellfeeds verwenden, kann ein Paket aus allen Feeds heruntergeladen werden. Sie sollten wissen, aus welchen Feeds Ihr Paket stammt, um sicherzustellen, dass Ihr Build vorhersagbar und sicher vor bekannten Angriffen wie einer [Dependency Confusion](https://medium.com/@alex.birsan/dependency-confusion-4a5d60fec610) (Abhängigkeitsverwechslung) ist. Sie können einen einzelnen Feed oder privaten Feed mit Upstreamingfunktionen für den Schutz verwenden.

Weitere Informationen zum Schützen Ihrer Paketfeeds finden Sie unter [3 Möglichkeiten zur Risikominderung mit privaten Paketfeeds](https://azure.microsoft.com/resources/3-ways-to-mitigate-risk-using-private-package-feeds/).

### <a name="client-trust-policies"></a>Clientvertrauensrichtlinien

**📦 Paketnutzer**

Es gibt Richtlinien, die Sie aktivieren können und die erfordern, dass Ihre verwendeten Pakete signiert sind. So können Sie einem Paket vertrauen, sofern es vom Ersteller signiert ist oder sich im Besitz eines bestimmten Benutzers oder Kontos ist, dessen Repository von NuGet.org signiert wurde.

Informationen zum Konfigurieren von Clientvertrauensrichtlinien finden Sie in [der folgenden Dokumentation](../consume-packages/installing-signed-packages.md).

### <a name="lock-files"></a>Sperrdateien

**📦 Paketnutzer**

Sperrdateien speichern den Hash des Paketinhalts. Wenn der Inhaltshash eines Pakets, das Sie installieren möchten, mit der Sperrdatei übereinstimmt, wird die Wiederholbarkeit des Pakets sichergestellt.

Informationen zum Aktivieren von Sperrdateien finden Sie in [der folgenden Dokumentation](../consume-packages/package-references-in-project-files.md#locking-dependencies).

## <a name="monitor-your-supply-chain"></a>Überwachen der Lieferkette

### <a name="github-secret-scanning"></a>Geheime Überprüfung in GitHub

**📦🖊 Paketersteller**

GitHub durchsucht Repositorys nach NuGet-API-Schlüsseln, um betrügerische Fälle von Geheimnisnutzung zu verhindern, die versehentlich committet wurden. 

Weitere Informationen zur Geheimnisüberprüfung finden Sie in den [Infos zur Geheimnisüberprüfung](https://docs.github.com/en/github/administering-a-repository/about-secret-scanning).

### <a name="author-package-signing"></a>Erstellen der Paketsignierung

**📦🖊 Paketersteller**

Die [Erstellung von Signierungen](../reference/signed-packages-reference.md) ermöglicht einem Paketersteller, ein Paket mit seiner Identität zu versehen, sodass ein Kunde nachverfolgen kann, ob es von diesem Ersteller stammt. Sie werden so vor Inhaltsmanipulation geschützt. Zudem fungiert diese Methode als „Single Source of Truth“(einziger Punkt der Wahrheit) bezüglich des Ursprungs und der Echtheit des Pakets. In Kombination mit Clientvertrauensrichtlinien können Sie so überprüfen, ob ein Paket von einem bestimmten Ersteller stammt.

Informationen zum Signieren eines Pakets als Ersteller finden Sie unter [Signieren eines Pakets](../create-packages/sign-a-package.md).

### <a name="two-factor-authentication-2fa"></a>Zweistufige Authentifizierung

**📦🖊 Paketersteller**

Durch die Aktivierung der zweistufigen Authentifizierung (Two-Factor Authentication, 2FA) kann der [Anmeldung bei GitHub](https://docs.github.com/en/github/authenticating-to-github/securing-your-account-with-two-factor-authentication-2fa) oder dem [öffentlichen NuGet.org-Paketrepository](../nuget-org/individual-accounts.md#enable-two-factor-authentication-2fa) eine zusätzliche Sicherheitsebene hinzugefügt werden. Es wird empfohlen, die zweistufige Authentifizierung zu aktivieren, um Ihr Konto zu schützen.

### <a name="package-id-prefix-reservation"></a>Reservierung für Paket-ID-Präfixe 

**📦🖊 Paketersteller**

Wenn Sie die Identität Ihrer Pakete schützen möchten, können Sie ein Paket-ID-Präfix mit Ihrem Namespace reservieren, um dem Paket einen Besitzer zuzuordnen. Voraussetzung dafür ist, dass das Paket-ID-Präfix ordnungsgemäß die [festgelegten Kriterien](../nuget-org/id-prefix-reservation.md#id-prefix-reservation-criteria) erfüllt. 

Informationen zum Reservieren von ID-Präfixen finden Sie unter [Reservierung von Paket-ID-Präfix](../nuget-org/id-prefix-reservation.md).

### <a name="deprecating-and-unlisting-a-vulnerable-package"></a>Einstellen und Aufheben der Auflistung eines anfälligen Pakets

**📦🖊 Paketersteller**

Wenn Sie ein Sicherheitsrisiko in einem von Ihnen erstellten Paket erkannt haben, sollten Sie das Paket zum Schutz des .NET-Paketökosystems einstellen und die Auflistung dafür aufheben, sodass Benutzer, die nach Paketen suchen, es nicht mehr finden können. Wenn Sie ein Paket nutzen, das veraltet und nicht aufgelistet ist, sollten Sie es unbedingt außer Betrieb nehmen.

In der folgenden Dokumentation unter [Als veraltet gekennzeichnete Pakete](../nuget-org/deprecate-packages.md) und [Aufheben der Auflistung eines Pakets](../nuget-org/policies/deleting-packages.md#unlisting-a-package) erfahren Sie, wie Sie ein Paket als veraltetet markieren und aus einer Auflistung entfernen.

## <a name="summary"></a>Zusammenfassung

Ihre Softwarelieferkette besteht aus allen Elementen, die in Ihren Code einfließen und sich auf diesen auswirken. Obwohl Kompromittierungen in der Lieferkette ein aktuelles Thema sind und immer öfter auftreten, sind sie noch immer selten. Es hat also höchste Priorität, Ihre Lieferkette zu schützen, indem Sie sich **Ihre Abhängigkeiten bewusst machen und diese verwalten** sowie **Ihre Lieferkette überwachen**.

Sie haben unterschiedliche Methoden kennengelernt, die von NuGet und [GitHub](/learn/modules/maintain-secure-repository-github/) bereitgestellt werden, mit denen Sie noch heute Ihre Einblicke, die Verwaltung und die Überwachung Ihrer Lieferkette optimieren können.

Weitere Informationen zum Schützen der weltweit eingesetzten Software finden Sie im [Sicherheitsbericht von „The State of the Octoverse 2020“](https://octoverse.github.com/static/github-octoverse-2020-security-report.pdf).
