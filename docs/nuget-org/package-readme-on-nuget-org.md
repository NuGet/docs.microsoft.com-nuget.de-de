---
title: Paketinfodatei auf NuGet.org
description: Ausführliche Erläuterung, wie Infodateien auf NuGet.org gerendert werden, und was zu tun ist, wenn Probleme auftreten.
author: chgill-MSFT
ms.author: chgill
ms.date: 02/23/2021
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: a5d68329128c9e9d047fe10e08ce41f1ae0895b4
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/22/2021
ms.locfileid: "107902224"
---
# <a name="package-readme-on-nugetorg"></a>Paketinfodatei auf NuGet.org

[Nehmen Sie eine Infodatei in Ihr NuGet-Paket auf](https://docs.microsoft.com/nuget/reference/msbuild-targets#packagereadmefile), um Ihren Benutzern umfangreichere und informativere Detailinformationen zum Paket zu geben.

Dies ist wahrscheinlich eins der ersten Elemente, das Benutzer sehen, wenn sie Ihre Paketdetailseite auf NuGet.org anzeigen, und es ist wichtig, um einen guten Eindruck zu machen.

> [!IMPORTANT]
> NuGet.org unterstützt nur Infodateien im [Markdown](https://daringfireball.net/projects/markdown/)-Format und Bilder aus einer begrenzten Gruppe von Domänen. Sehen Sie sich unsere [zulässigen Domänen für Bilder](#allowed-domains-for-images-and-badges) und [unterstützte Markdown-Funktionen](#supported-markdown-features) an, um sicherzustellen, dass Ihre Infodatei ordnungsgemäß auf NuGet.org gerendert wird.

## <a name="what-should-my-readme-include"></a>Was sollte meine Infodatei enthalten?

Erwägen Sie, die folgenden Elemente in Ihre Infodatei aufzunehmen:
* Eine Einführung, was Ihr Paket ist und was es macht: welche Probleme löst es?
* Informationen zu den ersten Schritten mit Ihrem Paket: Gibt es bestimmte Anforderungen?
* Links zu einer umfassenderen Dokumentation, wenn sie nicht in der Infodatei selbst enthalten ist.
* Mindestens einige Codeausschnitte/-beispiele oder Beispielbilder.
* Wo und wie man Feedback hinterlasse kann, z. B. einen Link zu den Projektproblemen (project issues), Twitter, Bug Tracker oder einer anderen Plattform.
* Wie man mitwirken kann, falls zutreffend.

Beachten Sie, dass hochwertige Infodateien eine Vielzahl von Formaten, Formen und Größen annehmen können. Wenn Sie bereits über ein Paket verfügen, das auf NuGet.org verfügbar ist, ist es wahrscheinlich, dass Sie bereits über eine `readme.md` oder eine andere Dokumentationsdatei in Ihrem Repository verfügen, die eine gute Ergänzung Ihrer Detailseite auf NuGet.org wäre.

## <a name="preview-your-readme"></a>Anzeigen einer Vorschau Ihrer Infodatei

Um eine Vorschau Ihrer Infodatei anzuzeigen, bevor sie auf NuGet.org live geschaltet wird, laden Sie Ihr Paket über [„Upload Package“ (Paket hochladen) im Webportal auf NuGet.org](https://docs.microsoft.com/nuget/nuget-org/publish-a-package#web-portal-use-the-upload-package-tab-on-nugetorg) hoch, und scrollen Sie nach unten zum Abschnitt „Readme File“ (Infodatei) der Metadatenvorschau. Der Bericht könnte beispielsweise wie folgt aussehen:

![Vorschau der Infodatei](media\readme-upload-preview.PNG)

Nehmen Sie sich Zeit, um Ihre Readme-Datei auf [Bilderkonformität](#allowed-domains-for-images-and-badges) und [unterstützte Formatierungen](#supported-markdown-features) zu überprüfen und in der Vorschau anzuzeigen, um sicherzustellen, dass sie potenziellen Benutzern einen guten ersten Eindruck vermittelt. Um Fehler in der Infodatei Ihres Pakets zu beheben, nachdem sie auf NuGet.org veröffentlicht wurde, müssen Sie eine aktualisierte Paketversion mit der Korrektur pushen. Wenn Sie im Voraus sicherstellen, dass alles gut aussieht, kann Ihnen das Kopfschmerzen auf dem weiteren Weg ersparen.
## <a name="allowed-domains-for-images-and-badges"></a>Zulässige Domänen für Bilder und Badges

Aus Sicherheits- und Datenschutzgründen schränkt NuGet.org Domänen ein, aus denen Bilder und Badges auf vertrauenswürdigen Hosts gerendert werden können. 

NuGet.org lässt das Rendern aller Bilder, einschließlich Badges, aus den folgenden vertrauenswürdigen Domänen zu:
* api.bintray.com
* api.codacy.com
* api.codeclimate.com
* api.dependabot.com
* api.travis-ci.com
* api.travis-ci.org
* app.fossa.io
* badge.fury.io
* badgen.net
* badges.gitter.im
* bettercodehub.com
* buildstats.info
* camo.githubusercontent.com
* ci.appveyor.com
* circleci.com
* codecov.io
* codefactor.io
* coveralls.io
* dev.azure.com
* github.com/.../workflows/.../badge.svg
* gitlab.com
* img.shields.io
* isitmaintained.com
* opencollective.com
* raw.github.com
* raw.githubusercontent.com
* snyk.io
* sonarcloud.io
* user-images.githubusercontent.com

Wenn Sie der Ansicht sind, dass der Zulassungsliste eine weitere Domäne hinzugefügt werden sollte, können Sie gerne [ein Problem melden](https://github.com/NuGet/NuGetGallery/issues), das dann von unserem Technikteam auf Datenschutz- und Sicherheitskonformität überprüft wird. Bilder mit relativen lokalen Pfaden und Bilder, die von nicht unterstützten Domänen gehostet werden, werden nicht gerendert und erzeugen eine Warnung in der Vorschau der Infodatei sowie auf der Seite mit den Paketdetails, die nur dem Paketbesitzer angezeigt wird.

## <a name="supported-markdown-features"></a>Unterstützte Markdown-Funktionen
[Markdown](https://daringfireball.net/projects/markdown/) ist eine schlanke Markupsprache mit Nur-Text-Formatierungssyntax. NuGet.org-Infodateien unterstützen [CommonMark](https://commonmark.org/)-konformes Markdown über die Analyse-Engine [Markdig](https://github.com/lunet-io/markdig).

NuGet.org unterstützt derzeit die folgenden Markdown-Funktionen:
* [Headers](https://spec.commonmark.org/0.29/#atx-headings)
* [Bilder](https://spec.commonmark.org/0.29/#images)
* [Zusätzliche Hervorhebung](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/EmphasisExtraSpecs.md)
* [Listen](https://spec.commonmark.org/0.29/#lists)
* [Links](https://spec.commonmark.org/0.29/#links)
* [Blockzitate](https://spec.commonmark.org/0.29/#block-quotes)
* [Umgekehrter Schrägstrich als Escapezeichen](https://spec.commonmark.org/0.29/#backslash-escapes)
* [„Code Spans“ (Codes-Bereiche)](https://spec.commonmark.org/0.29/#code-spans)
* [Aufgabenlisten](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/TaskListSpecs.md)
* [Tabellen](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/PipeTableSpecs.md)
* [Emojis](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/EmojiSpecs.md)
* [Automatische Links](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/AutoLinks.md)

