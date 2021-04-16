---
title: Bewährte Methoden für die Paketerstellung
description: Eine allgemeine Anleitung mit bewährten Methoden zum Erstellen von NuGet-Paketen mit hoher Qualität.
author: chgill-MSFT
ms.author: chgill
ms.date: 09/17/2020
ms.topic: conceptual
ms.openlocfilehash: aae05b63921f3494376b430186d3605eeff174c1
ms.sourcegitcommit: c8bf16420f235fc3e42c08cd0d56359e91d490e5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/14/2021
ms.locfileid: "107387360"
---
# <a name="package-authoring-best-practices"></a>Bewährte Methoden für die Paketerstellung

Diese Anleitung ist eine vereinfachte Referenz zum Erstellen und Veröffentlichen hochwertiger Pakete für NuGet-Paketautoren. Sie konzentriert sich in erster Linie auf paketspezifische bewährte Methoden wie Metadaten und Verpacken. Ausführlichere Empfehlungen zum Entwickeln hochwertiger Bibliotheken finden Sie im [Leitfaden für die Open Source-Bibliothek](/dotnet/standard/library-guidance/) für .NET.

## <a name="types-of-recommendations"></a>Empfehlungstypen

Jeder Artikel enthält vier Empfehlungstypen: **Do**, **Erwägen**, **Vermeiden** und **Do not**. Der Empfehlungstyp gibt an, wie strikt die Empfehlung befolgt werden sollte.

Eine **Do**-Empfehlung sollten Sie fast immer befolgen. Beispiel:

✔️ Beziehen Sie eine kurze Beschreibung des Zwecks Ihres Pakets ein.

Andererseits sollten auf **Erwägungen** bezogene Empfehlungen im Allgemeinen befolgt werden, berechtigte Ausnahmen bestätigen jedoch die Regel:

✔️ Wählen Sie einen NuGet-Paketnamen mit einem Präfix aus, das den [Kriterien](../nuget-org/id-prefix-reservation.md) der NuGet-Präfixreservierung entspricht.

Empfehlungen hinsichtlich **Vermeiden** geben Dinge an, die allgemein als keine gute Idee angesehen werden, jedoch kann das Brechen dieser Regel manchmal auch sinnvoll sein:

❌ Vermeiden Sie NuGet-Paketverweise, die eine exakte Version erfordern.

Schließlich kennzeichnen **Do not**-Empfehlungen Vorgänge, die Sie niemals ausführen sollten:

❌ Verwenden Sie die Metadateneigenschaft `LicenseUrl` NICHT.

## <a name="create-a-nuget-package"></a>Erstellen eines NuGet-Pakets

Die aktuelle empfohlene Methode ist das Erstellen eines NuGet-Pakets von einem [Projekt im SDK-Stil](../resources/check-project-format.md) aus. Die Eigenschaften eines Projekts im SDK-Stil einschließlich [Zielframework](/dotnet/standard/frameworks) und [Paketmetadaten](#package-metadata) werden in der [Projektdatei](/visualstudio/ide/solutions-and-projects-in-visual-studio#project-file) definiert.

Erstellen Sie ein Paket von Ihrem Projekt im SDK-Stil aus, indem Sie die erforderlichen Eigenschaften definieren und in [Visual Studio](../quickstart/create-and-publish-a-package-using-visual-studio.md?tabs=netcore-cli) oder der [dotnet-CLI](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md) verpacken.

✔️ Erstellen Sie ein Projekt im SDK-Stil und erstellen (verpacken) Sie Ihr Paket mithilfe von Visual Studio oder der dotnet-CLI.

Ausführlichere Anleitungen zur Paketerstellung einschließlich der erforderlichen Clienttools, des Projektdateibeispiels und der Befehle finden Sie unter [Erstellen eines NuGet-Pakets mithilfe der dotnet-CLI](./creating-a-package-dotnet-cli.md).

Informationen zur Entscheidung, welche .NET-Frameworks als Ziel festzulegen sind, finden Sie in unserem [neuesten Leitfaden für plattformübergreifende Ziele](/dotnet/standard/library-guidance/cross-platform-targeting).

## <a name="package-metadata"></a>Paketmetadaten

Metadaten sind eine grundlegende Komponente jedes NuGet-Pakets. Die Qualität ihrer Metadaten kann die Auffindbarkeit, Nutzbarkeit und Vertrauenswürdigkeit des Pakets erheblich beeinflussen.

In Visual Studio sollten Sie zum Angeben von Paketmetadaten zu „Projekt > [Projektname]-Eigenschaften > Paket“ navigieren.

Elemente von Paketmetadaten können auch [direkt in der Projektdatei angegeben werden](./creating-a-package-msbuild.md#set-properties).

Im Folgenden finden Sie eine Tabellenzuordnung und Beschreibung verfügbarer Paketmetadatenelemente:

| Visual Studio-Eigenschaftsname                       | [Projektdatei/MSBuild-Eigenschaftsname](https://docs.microsoft.com/dotnet/core/tools/csproj#packagereleasenotes)                            | [Nuspec-Eigenschaftsname](https://docs.microsoft.com/nuget/reference/nuspec#general-form-and-schema)     | BESCHREIBUNG                                                                                                           |
|-----------------------------------------------    |-----------------------------------------------------------------------------------------------------------------------------------------  |---------------------------------------------------------------------------------------------------    |-------------------------------------------------------------------------------------------------------------------    |
| [`Package id`](#package-id)                       | [`PackageId`](https://docs.microsoft.com/dotnet/core/tools/csproj#packageid)                                                              | [`id`](https://docs.microsoft.com/nuget/reference/nuspec#id)                                          | Der Paketname oder Bezeichner.                                                                                       |
| [`Package version`](#package-version)             | [`PackageVersion`](https://docs.microsoft.com/dotnet/core/tools/csproj#packageversion)                                                    | [`version`](https://docs.microsoft.com/nuget/reference/nuspec#version)                                | Die NuGet-Paketversion.                                                                                                |
| [`Authors`](#authors)                             | [`Authors`](https://docs.microsoft.com/dotnet/core/tools/csproj#authors)                                                                  | [`authors`](https://docs.microsoft.com/nuget/reference/nuspec#authors)                                | Eine durch Trennzeichen getrennte Liste von Paketautoren, wo häufig der Anzeigename der Person oder einer Organisation verwendet wird.           |
| [`Description`](#description)                     | [`Description`](https://docs.microsoft.com/dotnet/core/tools/csproj#description)                                                          | [`description`](https://docs.microsoft.com/nuget/reference/nuspec#description)                        | Eine Beschreibung des Pakets.                                                                                         |
| [`Copyright`](#copyright)                         | [`Copyright`](https://docs.microsoft.com/dotnet/core/tools/csproj#copyright)                                                              | [`copyright`](https://docs.microsoft.com/nuget/reference/nuspec#copyright)                            | Copyright-Informationen für das Paket.                                                                                    |
| [`Licensing - Expression`](#licensing)            | [`PackageLicenseExpression`](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-a-license-expression-or-a-license-file)   | [`license type="expression"`](https://docs.microsoft.com/nuget/reference/nuspec#license)              | Ein SPDX-Lizenzausdruck.                                                                                           |
| [`Licensing - File`](#licensing)                  | [`PackageLicenseFile`](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-a-license-expression-or-a-license-file)         | [`license type="file"`](https://docs.microsoft.com/nuget/reference/nuspec#license)                    | Pfad zu einer benutzerdefinierten Lizenzdatei.                                                                                        |
| [`Project URL`](#project-url)                     | `PackageProjectUrl`                                                                                                                       | [`projectUrl`](https://docs.microsoft.com/nuget/reference/nuspec#projecturl)                          | Eine App-URL für die Projekthomepage.                                                                                       |
| [`Icon File`](#icon)                              | [`PackageIcon`](https://docs.microsoft.com/nuget/reference/msbuild-targets#packing-an-icon-image-file)                                    | [`icon`](https://docs.microsoft.com/nuget/reference/nuspec#icon)                                      | Pfad zur Paketsymbol-Bilddatei.                                                                                  |
| [`Repository URL`](#repository-type-and-url)      | [`RepositoryUrl`](https://docs.microsoft.com/dotnet/core/tools/csproj#repositoryurl)                                                      | [`repository url`](https://docs.microsoft.com/nuget/reference/nuspec#repository)                      | Die URL zu dem Repository, von dem aus das Paket erstellt wurde.                                                               |
| [`Repository type`](#repository-type-and-url)     | [`RespositoryType`](https://docs.microsoft.com/dotnet/core/tools/csproj#repositorytype)                                                   | [`repository type`](https://docs.microsoft.com/nuget/reference/nuspec#repository)                     | Repositorytyp, auf den die Repository-URL verweist (d. h. „git“).                                                    |
| [`Tags`](#tags)                                   | [`PackageTags`](https://docs.microsoft.com/dotnet/core/tools/csproj#packagetags)                                                          | [`tags`](https://docs.microsoft.com/nuget/reference/nuspec#tags)                                      | Eine durch Leerzeichen getrennte Liste von Tags und Schlüsselwörtern, die das Paket beschreiben. Tags werden bei der Suche nach Paketen verwendet.     |
| [`Release notes`](#release-notes)                 | [`PackageReleaseNotes`](https://docs.microsoft.com/dotnet/core/tools/csproj#packagereleasenotes)                                          | [`releaseNotes`](https://docs.microsoft.com/nuget/reference/nuspec#releasenotes)                      | Eine Beschreibung der Änderungen, die in diesem Release des Pakets vorgenommen wurden.                                                     |
### <a name="package-id"></a>Paket-ID

Wenn Sie ein vollständig neues Paket veröffentlichen:

✔️ Wählen Sie eine eindeutige Paket-ID aus, die sich deutlich von vorhandenen Paketen auf NuGet.org unterscheidet.
> Sie können überprüfen, ob eine Paket-ID eindeutig ist und sich unterscheidet, indem Sie auf NuGet.org nach der ID suchen oder überprüfen, ob der folgende Link vorhanden ist: https://www.nuget.org/packages/<package Paketname\>.

✔️ ERWÄGEN Sie die Auswahl eines NuGet-Paketnamens mit einem Präfix, das den [Kriterien der NuGet-Präfixreservierung](../nuget-org/id-prefix-reservation.md#id-prefix-reservation-criteria) entspricht.
> Wenn Sie die Präfix-ID für Ihr Paket reservieren, wird das „Überprüft“-Häkchen angezeigt: ![Abbildung](media/Verified-check-mark.png)
> 
> Weitere Informationen finden Sie in der Dokumentation zur [Reservierung für Paket-ID-Präfixe](../nuget-org/id-prefix-reservation.md).

### <a name="package-version"></a>Paketversion

✔️ ERWÄGEN Sie, [SemVer](https://semver.org/) für die Versionskontrolle Ihres NuGet-Pakets zu verwenden.
> Dies bedeutet im Wesentlichen, dass das Format „Major.Minor.Patch[-prerelease]“ verwendet wird.

✔️ Veröffentlichen Sie ein Paket als [Vorabversionspaket](./prerelease-packages.md), wenn es nicht stabil ist oder als Vorschauversion verfügbar ist.

Eine ausführlichere Anleitung finden Sie im [Handbuch zur Versionsverwaltung von .NET-Bibliotheken](/dotnet/standard/library-guidance/versioning).

### <a name="authors"></a>Authors

✔️ Verwenden Sie das Feld „Autor“ für Ihren Anzeigenamen oder den Ihrer Organisation.
> Wenn Ihr NuGet.org-Benutzername beispielsweise „jdoe“ lautet, können Consumer Sie leichter als Autorin erkennen, wenn „Jane Doe“ im Feld „Autor“ steht. Wenn der NuGet.org-Benutzername Ihrer Organisation „ContosoToolkit“ lautet, kann die Verwendung von „Contoso Corporation“ die Erkennbarkeit verbessern und die Vertrauenswürdigkeit bei Consumern steigern.
### <a name="description"></a>BESCHREIBUNG

✔️ Beziehen Sie eine kurze Beschreibung (bis zu 4.000 Zeichen) ein, um das Paket zu beschreiben.
> Die Paketbeschreibung ist eines der wichtigsten Felder, die in der NuGet-Suche angezeigt werden, und wahrscheinlich das erste, was potenzielle Consumer anzeigen, um festzustellen, ob ein Paket für sie geeignet ist.

### <a name="copyright"></a>Copyright

✔️ ERWÄGEN Sie, Ihr Paket mit dem Copyrighthinweis „Copyright (c) <Name/Unternehmen\> <Jahr\>“ zu versehen.
>Ein Copyrighthinweis gibt im Wesentlichen an, dass Ihre Arbeit ohne Ihre Berechtigung nicht kopiert werden kann. Ein Copyrighthinweis lässt sich einfach in Ihr Paket einbeziehen und schadet nicht!

Beispiel: Copyright (c) Contoso 2020

### <a name="licensing"></a>Lizenzierung

✔️ Beziehen Sie [einen Lizenzausdruck oder eine Lizenzdatei in Ihr Paket ein](../reference/msbuild-targets.md#packing-a-license-expression-or-a-license-file).
> [!IMPORTANT]
> Für ein Projekt ohne Lizenz gilt standardmäßig ein [exklusives Copyright](https://choosealicense.com/no-permission/), was bedeutet, dass Sie niemandem eine Berechtigung zur Verwendung Ihres Projekts erteilt haben.

❌ Verwenden Sie KEINE veraltete `LicenseUrl`-Metadateneigenschaft.
> Dies führt zu einer rechtlichen Unklarheit, da Lizenzänderungen an der URL die angezeigte Lizenz für vorherige Paketversionen rückwirkend ändern.

#### <a name="if-your-package-is-open-source"></a>Wenn Ihr Paket ein [Open-Source](https://opensource.org/osd)-Paket ist

✔️ [Wählen Sie eine Open-Source-Lizenz aus](https://choosealicense.com/), um Ihr Paket zu einem Open-Source-Paket zu machen.
> *„Open-Source-Lizenzen sind Lizenzen, die der Open-Source-Definition entsprechen – kurz gesagt, sie ermöglichen die Software frei Nutzung, Änderung und Freigabe von Software.“* – Open-Source-Initiative. Weitere Informationen zu Open-Source-Software und der Open-Source-Initiative finden Sie unter https://opensource.org/.

✔️ ERWÄGEN Sie, [einen Lizenzausdruck in Ihr Paket einzubeziehen](../reference/msbuild-targets.md#packing-a-license-expression-or-a-license-file).
> Lizenzausdrücke werden am deutlichsten angezeigt und zeigen Consumern klarer, ob sie das Paket verwenden können, oder ob sich die Lizenz geändert hat. 
> [!Note]
> NuGet.org akzeptiert nur Lizenzausdrücke für Lizenzen, die von der Open-Source-Initiative oder der Free Software Foundation genehmigt wurden.

#### <a name="if-your-package-is-not-open-source"></a>Wenn Ihr Paket kein Open-Source-Paket ist

✔️ Beziehen Sie [einen Lizenzausdruck in Ihr Paket ein](../reference/msbuild-targets.md#packing-a-license-expression-or-a-license-file).
> Alle Lizenzdateien (TXT oder MD) können dem Paket hinzugefügt werden, einschließlich nicht standardmäßiger Lizenzen. 

### <a name="project-url"></a>Projekt-URL

✔️ ERWÄGEN Sie, einen Link zu einem zugeordneten Projekt, Repository oder einer Unternehmenswebsite einzuschließen.
> Ihre Projektwebsite sollte alles enthalten, was Benutzer über Ihr Paket wissen müssen, und sich dort befinden, wo Benutzer wahrscheinlich nach Dokumentation suchen.

### <a name="icon"></a>Symbol

✔️ ERWÄGEN Sie, [ein Symbol mit Ihrem Paket einzubeziehen](../reference/msbuild-targets.md#packing-an-icon-image-file), damit es visuell unterschieden werden kann. Es handelt sich um einen relativ kleinen Zusatz, der die Wahrnehmung der Paketqualität verbessern kann.
> Es kommen für einzelne Pakete spezifische Symbole oder Markenlogos infrage.

✔️ Verwenden Sie ein Bild, das 128x128 groß ist und einen transparenten Hintergrund (PNG) für die ideale Darstellung hat.
> NuGet skaliert Ihr Bild automatisch für den Client, auf dem es angezeigt wird.

❌ Verwenden Sie KEINE veraltete `IconUrl`-Metadateneigenschaft.

### <a name="repository-type-and-url"></a>Repositorytyp und URL

✔️ ERWÄGEN Sie die Einrichtung von [SourceLink](/dotnet/standard/library-guidance/sourcelink), um dem NuGet-Paket automatisch Quellcodeverwaltungs-Metadaten hinzuzufügen und das Debuggen der Bibliothek zu vereinfachen.
> SourceLink fügt automatisch `Repository URL`- und `Repository Type`-Paketmetadaten hinzu. Außerdem wird der spezifische Commit hinzugefügt, der ihrer Paketversion zugeordnet ist.

### <a name="tags"></a>`Tags`

✔️ Beziehen Sie mehrere Tags mit wichtigen Begriffen zu Ihrem Paket ein, um die Auffindbarkeit zu verbessern.
> Tags werden im Suchalgorithmus von NuGet.org berücksichtigt und sind besonders hilfreich für Begriffe, die nicht in der Paket-ID vorliegen, aber relevant sind.

Wenn Sie z. B. ein Paket zum Protokollieren von Zeichenfolgen in der Konsole veröffentlicht haben, sollten Sie „Protokollierung, Protokoll, Konsole, Zeichenfolge, Ausgabe“ einschließen.

### <a name="release-notes"></a>Versionshinweise

✔️ ERWÄGEN Sie, Versionshinweise in jedes Update einzuschließen, die beschreiben, welche Änderungen vorgenommen wurden.
> Es ist zwar kein bestimmtes Format für Versionshinweise vorgegeben, aber Sie sollten Folgendes einschließen:
>
> 1. Aktuelle Änderungen
> 2. Neue Funktionen
> 3. Behebung von Programmfehlern
> 
> Wenn Sie bereits Versionshinweise oder ein Änderungsprotokoll in Ihrem Repository nachverfolgen, können Sie auch einen Link zur entsprechenden Datei einschließen.

## <a name="related-topics"></a>Verwandte Themen

- [Erstellen und Veröffentlichen eines Pakets (dotnet CLI)](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md)
- [Erstellen und Veröffentlichen eines Pakets (Visual Studio)](../quickstart/create-and-publish-a-package-using-visual-studio.md?tabs=netcore-cli)