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
# <a name="package-readme-on-nugetorg"></a><span data-ttu-id="efa77-103">Paketinfodatei auf NuGet.org</span><span class="sxs-lookup"><span data-stu-id="efa77-103">Package readme on NuGet.org</span></span>

<span data-ttu-id="efa77-104">[Nehmen Sie eine Infodatei in Ihr NuGet-Paket auf](https://docs.microsoft.com/nuget/reference/msbuild-targets#packagereadmefile), um Ihren Benutzern umfangreichere und informativere Detailinformationen zum Paket zu geben.</span><span class="sxs-lookup"><span data-stu-id="efa77-104">[Include a readme file in your NuGet package](https://docs.microsoft.com/nuget/reference/msbuild-targets#packagereadmefile) to make your package details richer and more informative for your users!</span></span>

<span data-ttu-id="efa77-105">Dies ist wahrscheinlich eins der ersten Elemente, das Benutzer sehen, wenn sie Ihre Paketdetailseite auf NuGet.org anzeigen, und es ist wichtig, um einen guten Eindruck zu machen.</span><span class="sxs-lookup"><span data-stu-id="efa77-105">This is likely one of the first elements users will see when they view your package details page on NuGet.org and is essential to making a good impression!</span></span>

> [!IMPORTANT]
> <span data-ttu-id="efa77-106">NuGet.org unterstützt nur Infodateien im [Markdown](https://daringfireball.net/projects/markdown/)-Format und Bilder aus einer begrenzten Gruppe von Domänen.</span><span class="sxs-lookup"><span data-stu-id="efa77-106">NuGet.org only supports readme files in [Markdown](https://daringfireball.net/projects/markdown/) and images from a limited set of domains.</span></span> <span data-ttu-id="efa77-107">Sehen Sie sich unsere [zulässigen Domänen für Bilder](#allowed-domains-for-images-and-badges) und [unterstützte Markdown-Funktionen](#supported-markdown-features) an, um sicherzustellen, dass Ihre Infodatei ordnungsgemäß auf NuGet.org gerendert wird.</span><span class="sxs-lookup"><span data-stu-id="efa77-107">See our [allowed domains for images](#allowed-domains-for-images-and-badges) and [supported Markdown features](#supported-markdown-features) to ensure your readme renders correctly on NuGet.org.</span></span>

## <a name="what-should-my-readme-include"></a><span data-ttu-id="efa77-108">Was sollte meine Infodatei enthalten?</span><span class="sxs-lookup"><span data-stu-id="efa77-108">What should my readme include?</span></span>

<span data-ttu-id="efa77-109">Erwägen Sie, die folgenden Elemente in Ihre Infodatei aufzunehmen:</span><span class="sxs-lookup"><span data-stu-id="efa77-109">Consider including the following items in your readme:</span></span>
* <span data-ttu-id="efa77-110">Eine Einführung, was Ihr Paket ist und was es macht: welche Probleme löst es?</span><span class="sxs-lookup"><span data-stu-id="efa77-110">An introduction to what your package is and does - what problems does it solve?</span></span>
* <span data-ttu-id="efa77-111">Informationen zu den ersten Schritten mit Ihrem Paket: Gibt es bestimmte Anforderungen?</span><span class="sxs-lookup"><span data-stu-id="efa77-111">How to get started with your package - are there any specific requirements?</span></span>
* <span data-ttu-id="efa77-112">Links zu einer umfassenderen Dokumentation, wenn sie nicht in der Infodatei selbst enthalten ist.</span><span class="sxs-lookup"><span data-stu-id="efa77-112">Links to more comprehensive documentation if not included in the readme itself.</span></span>
* <span data-ttu-id="efa77-113">Mindestens einige Codeausschnitte/-beispiele oder Beispielbilder.</span><span class="sxs-lookup"><span data-stu-id="efa77-113">At least a few code snippets/samples or example images.</span></span>
* <span data-ttu-id="efa77-114">Wo und wie man Feedback hinterlasse kann, z. B. einen Link zu den Projektproblemen (project issues), Twitter, Bug Tracker oder einer anderen Plattform.</span><span class="sxs-lookup"><span data-stu-id="efa77-114">Where and how to leave feedback such as link to the project issues, Twitter, bug tracker, or other platform.</span></span>
* <span data-ttu-id="efa77-115">Wie man mitwirken kann, falls zutreffend.</span><span class="sxs-lookup"><span data-stu-id="efa77-115">How to contribute, if applicable.</span></span>

<span data-ttu-id="efa77-116">Beachten Sie, dass hochwertige Infodateien eine Vielzahl von Formaten, Formen und Größen annehmen können.</span><span class="sxs-lookup"><span data-stu-id="efa77-116">Keep in mind, high quality readmes can come in a wide variety of formats, shapes, and sizes!</span></span> <span data-ttu-id="efa77-117">Wenn Sie bereits über ein Paket verfügen, das auf NuGet.org verfügbar ist, ist es wahrscheinlich, dass Sie bereits über eine `readme.md` oder eine andere Dokumentationsdatei in Ihrem Repository verfügen, die eine gute Ergänzung Ihrer Detailseite auf NuGet.org wäre.</span><span class="sxs-lookup"><span data-stu-id="efa77-117">If you already have a package available on NuGet.org, chances are that you already have a `readme.md` or other documentation file in your repository that would be a great addition to your NuGet.org details page.</span></span>

## <a name="preview-your-readme"></a><span data-ttu-id="efa77-118">Anzeigen einer Vorschau Ihrer Infodatei</span><span class="sxs-lookup"><span data-stu-id="efa77-118">Preview your readme</span></span>

<span data-ttu-id="efa77-119">Um eine Vorschau Ihrer Infodatei anzuzeigen, bevor sie auf NuGet.org live geschaltet wird, laden Sie Ihr Paket über [„Upload Package“ (Paket hochladen) im Webportal auf NuGet.org](https://docs.microsoft.com/nuget/nuget-org/publish-a-package#web-portal-use-the-upload-package-tab-on-nugetorg) hoch, und scrollen Sie nach unten zum Abschnitt „Readme File“ (Infodatei) der Metadatenvorschau.</span><span class="sxs-lookup"><span data-stu-id="efa77-119">To preview your readme file before it's live on NuGet.org, upload your package using the [Upload Package web portal on NuGet.org](https://docs.microsoft.com/nuget/nuget-org/publish-a-package#web-portal-use-the-upload-package-tab-on-nugetorg) and scroll down to the "Readme File" section of the metadata preview.</span></span> <span data-ttu-id="efa77-120">Der Bericht könnte beispielsweise wie folgt aussehen:</span><span class="sxs-lookup"><span data-stu-id="efa77-120">It should look something like this:</span></span>

![Vorschau der Infodatei](media\readme-upload-preview.PNG)

<span data-ttu-id="efa77-122">Nehmen Sie sich Zeit, um Ihre Readme-Datei auf [Bilderkonformität](#allowed-domains-for-images-and-badges) und [unterstützte Formatierungen](#supported-markdown-features) zu überprüfen und in der Vorschau anzuzeigen, um sicherzustellen, dass sie potenziellen Benutzern einen guten ersten Eindruck vermittelt.</span><span class="sxs-lookup"><span data-stu-id="efa77-122">Consider taking time to review and preview your readme file for [image compliance](#allowed-domains-for-images-and-badges) and [supported formatting](#supported-markdown-features) to make sure it gives a great first impression to potential users!</span></span> <span data-ttu-id="efa77-123">Um Fehler in der Infodatei Ihres Pakets zu beheben, nachdem sie auf NuGet.org veröffentlicht wurde, müssen Sie eine aktualisierte Paketversion mit der Korrektur pushen.</span><span class="sxs-lookup"><span data-stu-id="efa77-123">To correct mistakes on your package readme once it's published to NuGet.org, you will need to push an updated package version with the fix.</span></span> <span data-ttu-id="efa77-124">Wenn Sie im Voraus sicherstellen, dass alles gut aussieht, kann Ihnen das Kopfschmerzen auf dem weiteren Weg ersparen.</span><span class="sxs-lookup"><span data-stu-id="efa77-124">Making sure everything looks good in advance may save you headache down the road.</span></span>
## <a name="allowed-domains-for-images-and-badges"></a><span data-ttu-id="efa77-125">Zulässige Domänen für Bilder und Badges</span><span class="sxs-lookup"><span data-stu-id="efa77-125">Allowed domains for images and badges</span></span>

<span data-ttu-id="efa77-126">Aus Sicherheits- und Datenschutzgründen schränkt NuGet.org Domänen ein, aus denen Bilder und Badges auf vertrauenswürdigen Hosts gerendert werden können.</span><span class="sxs-lookup"><span data-stu-id="efa77-126">Due to security and privacy concerns, NuGet.org restricts the domains from which images and badges can be rendered to trusted hosts.</span></span> 

<span data-ttu-id="efa77-127">NuGet.org lässt das Rendern aller Bilder, einschließlich Badges, aus den folgenden vertrauenswürdigen Domänen zu:</span><span class="sxs-lookup"><span data-stu-id="efa77-127">NuGet.org allows all images, including badges, from the following trusted domains to be rendered:</span></span>
* <span data-ttu-id="efa77-128">api.bintray.com</span><span class="sxs-lookup"><span data-stu-id="efa77-128">api.bintray.com</span></span>
* <span data-ttu-id="efa77-129">api.codacy.com</span><span class="sxs-lookup"><span data-stu-id="efa77-129">api.codacy.com</span></span>
* <span data-ttu-id="efa77-130">api.codeclimate.com</span><span class="sxs-lookup"><span data-stu-id="efa77-130">api.codeclimate.com</span></span>
* <span data-ttu-id="efa77-131">api.dependabot.com</span><span class="sxs-lookup"><span data-stu-id="efa77-131">api.dependabot.com</span></span>
* <span data-ttu-id="efa77-132">api.travis-ci.com</span><span class="sxs-lookup"><span data-stu-id="efa77-132">api.travis-ci.com</span></span>
* <span data-ttu-id="efa77-133">api.travis-ci.org</span><span class="sxs-lookup"><span data-stu-id="efa77-133">api.travis-ci.org</span></span>
* <span data-ttu-id="efa77-134">app.fossa.io</span><span class="sxs-lookup"><span data-stu-id="efa77-134">app.fossa.io</span></span>
* <span data-ttu-id="efa77-135">badge.fury.io</span><span class="sxs-lookup"><span data-stu-id="efa77-135">badge.fury.io</span></span>
* <span data-ttu-id="efa77-136">badgen.net</span><span class="sxs-lookup"><span data-stu-id="efa77-136">badgen.net</span></span>
* <span data-ttu-id="efa77-137">badges.gitter.im</span><span class="sxs-lookup"><span data-stu-id="efa77-137">badges.gitter.im</span></span>
* <span data-ttu-id="efa77-138">bettercodehub.com</span><span class="sxs-lookup"><span data-stu-id="efa77-138">bettercodehub.com</span></span>
* <span data-ttu-id="efa77-139">buildstats.info</span><span class="sxs-lookup"><span data-stu-id="efa77-139">buildstats.info</span></span>
* <span data-ttu-id="efa77-140">camo.githubusercontent.com</span><span class="sxs-lookup"><span data-stu-id="efa77-140">camo.githubusercontent.com</span></span>
* <span data-ttu-id="efa77-141">ci.appveyor.com</span><span class="sxs-lookup"><span data-stu-id="efa77-141">ci.appveyor.com</span></span>
* <span data-ttu-id="efa77-142">circleci.com</span><span class="sxs-lookup"><span data-stu-id="efa77-142">circleci.com</span></span>
* <span data-ttu-id="efa77-143">codecov.io</span><span class="sxs-lookup"><span data-stu-id="efa77-143">codecov.io</span></span>
* <span data-ttu-id="efa77-144">codefactor.io</span><span class="sxs-lookup"><span data-stu-id="efa77-144">codefactor.io</span></span>
* <span data-ttu-id="efa77-145">coveralls.io</span><span class="sxs-lookup"><span data-stu-id="efa77-145">coveralls.io</span></span>
* <span data-ttu-id="efa77-146">dev.azure.com</span><span class="sxs-lookup"><span data-stu-id="efa77-146">dev.azure.com</span></span>
* <span data-ttu-id="efa77-147">github.com/.../workflows/.../badge.svg</span><span class="sxs-lookup"><span data-stu-id="efa77-147">github.com/.../workflows/.../badge.svg</span></span>
* <span data-ttu-id="efa77-148">gitlab.com</span><span class="sxs-lookup"><span data-stu-id="efa77-148">gitlab.com</span></span>
* <span data-ttu-id="efa77-149">img.shields.io</span><span class="sxs-lookup"><span data-stu-id="efa77-149">img.shields.io</span></span>
* <span data-ttu-id="efa77-150">isitmaintained.com</span><span class="sxs-lookup"><span data-stu-id="efa77-150">isitmaintained.com</span></span>
* <span data-ttu-id="efa77-151">opencollective.com</span><span class="sxs-lookup"><span data-stu-id="efa77-151">opencollective.com</span></span>
* <span data-ttu-id="efa77-152">raw.github.com</span><span class="sxs-lookup"><span data-stu-id="efa77-152">raw.github.com</span></span>
* <span data-ttu-id="efa77-153">raw.githubusercontent.com</span><span class="sxs-lookup"><span data-stu-id="efa77-153">raw.githubusercontent.com</span></span>
* <span data-ttu-id="efa77-154">snyk.io</span><span class="sxs-lookup"><span data-stu-id="efa77-154">snyk.io</span></span>
* <span data-ttu-id="efa77-155">sonarcloud.io</span><span class="sxs-lookup"><span data-stu-id="efa77-155">sonarcloud.io</span></span>
* <span data-ttu-id="efa77-156">user-images.githubusercontent.com</span><span class="sxs-lookup"><span data-stu-id="efa77-156">user-images.githubusercontent.com</span></span>

<span data-ttu-id="efa77-157">Wenn Sie der Ansicht sind, dass der Zulassungsliste eine weitere Domäne hinzugefügt werden sollte, können Sie gerne [ein Problem melden](https://github.com/NuGet/NuGetGallery/issues), das dann von unserem Technikteam auf Datenschutz- und Sicherheitskonformität überprüft wird.</span><span class="sxs-lookup"><span data-stu-id="efa77-157">If you feel that another domain should be added to the allow-list, please feel free to [file an issue](https://github.com/NuGet/NuGetGallery/issues) and it will be reviewed by our engineering team for privacy and security compliance.</span></span> <span data-ttu-id="efa77-158">Bilder mit relativen lokalen Pfaden und Bilder, die von nicht unterstützten Domänen gehostet werden, werden nicht gerendert und erzeugen eine Warnung in der Vorschau der Infodatei sowie auf der Seite mit den Paketdetails, die nur dem Paketbesitzer angezeigt wird.</span><span class="sxs-lookup"><span data-stu-id="efa77-158">Images with relative local paths and images hosted from unsupported domains will not be rendered and will produce a warning on the readme file preview and package details page that is only visible to the package owners.</span></span>

## <a name="supported-markdown-features"></a><span data-ttu-id="efa77-159">Unterstützte Markdown-Funktionen</span><span class="sxs-lookup"><span data-stu-id="efa77-159">Supported Markdown features</span></span>
<span data-ttu-id="efa77-160">[Markdown](https://daringfireball.net/projects/markdown/) ist eine schlanke Markupsprache mit Nur-Text-Formatierungssyntax.</span><span class="sxs-lookup"><span data-stu-id="efa77-160">[Markdown](https://daringfireball.net/projects/markdown/) is a lightweight markup language with plain text formatting syntax.</span></span> <span data-ttu-id="efa77-161">NuGet.org-Infodateien unterstützen [CommonMark](https://commonmark.org/)-konformes Markdown über die Analyse-Engine [Markdig](https://github.com/lunet-io/markdig).</span><span class="sxs-lookup"><span data-stu-id="efa77-161">NuGet.org readmes support [CommonMark](https://commonmark.org/) compliant Markdown through the [Markdig](https://github.com/lunet-io/markdig) parsing engine.</span></span>

<span data-ttu-id="efa77-162">NuGet.org unterstützt derzeit die folgenden Markdown-Funktionen:</span><span class="sxs-lookup"><span data-stu-id="efa77-162">NuGet.org currently supports the following Markdown features:</span></span>
* [<span data-ttu-id="efa77-163">Headers</span><span class="sxs-lookup"><span data-stu-id="efa77-163">Headers</span></span>](https://spec.commonmark.org/0.29/#atx-headings)
* [<span data-ttu-id="efa77-164">Bilder</span><span class="sxs-lookup"><span data-stu-id="efa77-164">Images</span></span>](https://spec.commonmark.org/0.29/#images)
* [<span data-ttu-id="efa77-165">Zusätzliche Hervorhebung</span><span class="sxs-lookup"><span data-stu-id="efa77-165">Extra emphasis</span></span>](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/EmphasisExtraSpecs.md)
* [<span data-ttu-id="efa77-166">Listen</span><span class="sxs-lookup"><span data-stu-id="efa77-166">Lists</span></span>](https://spec.commonmark.org/0.29/#lists)
* [<span data-ttu-id="efa77-167">Links</span><span class="sxs-lookup"><span data-stu-id="efa77-167">Links</span></span>](https://spec.commonmark.org/0.29/#links)
* [<span data-ttu-id="efa77-168">Blockzitate</span><span class="sxs-lookup"><span data-stu-id="efa77-168">Block quotes</span></span>](https://spec.commonmark.org/0.29/#block-quotes)
* [<span data-ttu-id="efa77-169">Umgekehrter Schrägstrich als Escapezeichen</span><span class="sxs-lookup"><span data-stu-id="efa77-169">Backslash escapes</span></span>](https://spec.commonmark.org/0.29/#backslash-escapes)
* [<span data-ttu-id="efa77-170">„Code Spans“ (Codes-Bereiche)</span><span class="sxs-lookup"><span data-stu-id="efa77-170">Code spans</span></span>](https://spec.commonmark.org/0.29/#code-spans)
* [<span data-ttu-id="efa77-171">Aufgabenlisten</span><span class="sxs-lookup"><span data-stu-id="efa77-171">Task lists</span></span>](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/TaskListSpecs.md)
* [<span data-ttu-id="efa77-172">Tabellen</span><span class="sxs-lookup"><span data-stu-id="efa77-172">Tables</span></span>](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/PipeTableSpecs.md)
* [<span data-ttu-id="efa77-173">Emojis</span><span class="sxs-lookup"><span data-stu-id="efa77-173">Emojis</span></span>](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/EmojiSpecs.md)
* [<span data-ttu-id="efa77-174">Automatische Links</span><span class="sxs-lookup"><span data-stu-id="efa77-174">Auto-links</span></span>](https://github.com/xoofx/markdig/blob/master/src/Markdig.Tests/Specs/AutoLinks.md)

