---
title: NuGet-Pakete in Visual Studio-Vorlagen
description: Anweisungen zum Einschließen von NuGet-Paketen als Teil von Visual Studio Projekt- und Elementvorlagen.
author: karann-msft
ms.author: karann
ms.date: 01/03/2018
ms.topic: conceptual
ms.openlocfilehash: 2dfbd793eee05169f051d9c8943bc065945b92da
ms.sourcegitcommit: cbc87fe51330cdd3eacaad3e8656eb4258882fc7
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/19/2020
ms.locfileid: "88622641"
---
# <a name="packages-in-visual-studio-templates"></a>Pakete in Visual Studio-Vorlagen

Bei Projekt- und Elementvorlagen in Visual Studio muss häufig sichergestellt werden, dass bestimmte Pakete installiert sind, wenn ein Projekt oder Element erstellt wird. Die ASP.NET MVC 3-Vorlage installiert z.B. jQuery, Modernizr und andere Pakete.

Autoren von Vorlagen können NuGet zum Installieren der erforderlichen Pakete anstatt einzelner Bibliotheken anweisen, um dies zu unterstützen. Entwickler können dann einfach diese Pakete zu einem späteren Zeitpunkt aktualisieren.

Weitere Informationen zum Erstellen von Vorlagen selbst finden Sie unter [Vorgehensweise: Erstellen von Projektvorlagen](/visualstudio/ide/how-to-create-project-templates) oder [Erstellen von benutzerdefinierten Projekt- und Elementvorlagen](/visualstudio/extensibility/creating-custom-project-and-item-templates).

Der übrige Teil dieses Abschnitts beschreibt die konkreten Schritte, die beim Erstellen einer Vorlage erforderlich sind, um NuGet-Pakete ordnungsgemäß einzubinden.

- [Hinzufügen von Paketen zu einer Vorlage](#adding-packages-to-a-template)
- [bewährten Methoden](#best-practices)

Ein Beispiel finden Sie unter [NuGetInVsTemplates sample (NuGetInVsTemplates-Beispiel)](https://bitbucket.org/marcind/nugetinvstemplates).

## <a name="adding-packages-to-a-template"></a>Hinzufügen von Paketen zu einer Vorlage

Wenn eine Vorlage instanziiert wird, wird ein [Vorlagen-Assistent](/visualstudio/extensibility/how-to-use-wizards-with-project-templates) aufgerufen, um die Liste der zu installierenden Pakete zu laden, zusammen mit Informationen, wo diese Pakete zu finden sind. Pakete können in VSIX oder in der Vorlage eingebettet werden oder befinden sich auf der lokalen Festplatte, wobei Sie in diesem Fall einen Registrierungsschlüssel verwenden, um auf den Dateipfad zu verweisen. Details zu diesen Speicherorten werden weiter unten in diesem Abschnitt beschrieben.

Vorinstallierte Pakete funktionieren mithilfe von [Vorlagen-Assistenten](/visualstudio/extensibility/how-to-use-wizards-with-project-templates). Wenn die Vorlage instanziiert wird, wird ein spezieller Assistent aufgerufen. Der Assistent lädt die Liste der Pakete, die installiert werden müssen, und übergibt diese Informationen an die entsprechenden NuGet-APIs.

Schritte zum Einschließen von Paketen in eine Vorlage:

1. In Ihrer `vstemplate`-Datei fügen Sie einen Verweis auf den NuGet-Vorlagen-Assistenten hinzu, indem Sie ein [`WizardExtension`](/visualstudio/extensibility/wizardextension-element-visual-studio-templates)-Element hinzufügen:

    ```xml
    <WizardExtension>
        <Assembly>NuGet.VisualStudio.Interop, Version=1.0.0.0, Culture=neutral, PublicKeyToken=b03f5f7f11d50a3a</Assembly>
        <FullClassName>NuGet.VisualStudio.TemplateWizard</FullClassName>
    </WizardExtension>
    ```

    `NuGet.VisualStudio.Interop.dll` ist eine Assembly, die nur die `TemplateWizard`-Klasse enthält, die einen einfachen Wrapper darstellt, der die tatsächliche Implementierung in `NuGet.VisualStudio.dll` aufruft. Die Version der Assembly wird nie geändert, sodass Projekt-/Elementvorlagen mit neuen Versionen von NuGet weiterhin funktionieren.

1. Fügen Sie die Liste der Pakete hinzu, die im Projekt installiert werden sollen:

    ```xml
    <WizardData>
        <packages>
            <package id="jQuery" version="1.6.2" />
        </packages>
    </WizardData>
    ```

    Der Assistent unterstützt mehrere `<package>`-Elemente zur Unterstützung mehrerer Paketquellen. Sowohl die `id`- als auch die `version`-Attribute werden benötigt. Dies bedeutet, dass die jeweilige Version eines Pakets selbst dann installiert wird, wenn eine neuere Version verfügbar ist. Dadurch wird verhindert, dass Paketupdates die Vorlage unterbrechen und die Wahl, das Paket zu aktualisieren, dem Entwickler überlassen wird, der die Vorlage verwendet.

1. Geben Sie das Repository an, in dem NuGet die Pakete, wie in den folgenden Abschnitten beschrieben, finden kann.

### <a name="vsix-package-repository"></a>VSIX-Paketrepository

Der empfohlene Bereitstellungsansatz für Visual Studio-Projekt-/Elementvorlagen ist eine [VSIX-Erweiterung](/visualstudio/extensibility/shipping-visual-studio-extensions), da sie Ihnen die Möglichkeit gibt, mehrere Projekt-/Elementvorlagen zusammen zu packen, und Entwicklern erlaubt, mühelos Ihre Vorlagen durch Verwenden des Visual Studio-Erweiterungsmanagers oder der Visual Studio Gallery zu ermitteln. Updates der Erweiterung können genauso einfach mit [automatischen Updates für den Visual Studio-Erweiterungsmanager](/visualstudio/extensibility/how-to-update-a-visual-studio-extension) bereitgestellt werden.

VSIX selbst kann als Quelle für die von der Vorlage benötigten Pakete dienen:

1. Ändern Sie das `<packages>`-Element in der `.vstemplate`-Datei wie folgt:

    ```xml
    <packages repository="extension" repositoryId="MyTemplateContainerExtensionId">
        <!-- ... -->
    </packages>
    ```

    Das `repository`-Attribut gibt den Typ des Repositorys als `extension` an, während `repositoryId` der eindeutige Bezeichner des VSIX-Projekts selbst ist (dies ist der Wert des `ID`-Attributs in der Datei `vsixmanifest` der Datei der Erweiterung. Informationen dazu finden Sie in der [Referenz zum VSIX-Erweiterungsschema 2.0](/visualstudio/extensibility/vsix-extension-schema-2-0-reference)).

1. Speichern Sie Ihre `nupkg`-Dateien in einem Ordner namens `Packages` im VSIX-Projekt.

1. Fügen Sie die erforderlichen Paketdateien Ihrer `vsixmanifest`-Datei als `<Asset>` hinzu (Informationen hierzu finden Sie in der [Referenz zum VSIX-Erweiterungsschema 2.0](/visualstudio/extensibility/vsix-extension-schema-2-0-reference)):

    ```xml
    <Asset Type="Moq.4.0.10827.nupkg" d:Source="File" Path="Packages\Moq.4.0.10827.nupkg" d:VsixSubPath="Packages" />
    ```

1. Beachten Sie, dass Sie Pakete in derselben Instanz von VSIX wie die Projektvorlagen übermitteln können, oder Sie können diese in einer separaten VSIX-Instanz einfügen, wenn dies für Ihr Szenario sinnvoller ist. Verweisen Sie jedoch auf keine Instanz von VSIX, die Sie nicht selbst steuern, da Änderungen für diese Erweiterung Ihre Vorlage beschädigen könnten.

### <a name="template-package-repository"></a>Vorlage „Paketrepository“

Wenn Sie nur eine einzelne Projekt-/Elementvorlage verteilen und nicht unterschiedliche Vorlagen zusammen packen müssen, können Sie einen einfacheren, aber eingeschränkteren Ansatz verwenden, der Pakete direkt in die Projekt-/Elementvorlagen ZIP-Datei einschließt:

1. Ändern Sie das `<packages>`-Element in der `.vstemplate`-Datei wie folgt:

    ```xml
    <packages repository="template">
        <!-- ... -->
    </packages>
    ```

    Das `repository`-Attribut hat den Wert `template`, und das `repositoryId`-Attribut ist nicht erforderlich.

1. Platzieren Sie Pakete im Stammordner der ZIP-Datei der Projekt-/Elementvorlagen.

Beachten Sie, dass es bei Verwenden dieses Ansatzes in einer VSIX-Instanz mit mehreren Vorlagen zu einer unnötigen Überfrachtung kommen kann, wenn ein oder mehrere Pakete den Vorlagen gemeinsam sind. In solchen Fällen verwenden Sie [VSIX als Repository](#vsix-package-repository) wie im vorherigen Abschnitt beschrieben.

### <a name="registry-specified-folder-path"></a>Von der Registrierung angegebener Ordnerpfad

SDKs, die mit MSI installiert werden, können direkt auf dem Computer des Entwicklers NuGet-Pakete installieren. Dies ermöglicht eine unmittelbare Verfügbarkeit, wenn eine Projekt- oder Elementvorlage verwendet wird, anstatt sie während dieser Zeit extrahieren zu müssen. Vorlagen für ASP.NET verwenden diesen Ansatz.

1. Lassen Sie MSI Pakete auf dem Computer installieren. Sie können nur `.nupkg`-Dateien installieren, oder Sie können diese zusammen mit den erweiterten Inhalten installieren, wodurch ein zusätzlicher Schritt bei Verwendung der Vorlage eingespart wird. Halten Sie sich in diesem Fall an die Standardordnerstruktur von NuGet, wobei sich die `.nupkg`-Dateien im Stammordner befinden. Jedes Paket verfügt dann über einen Unterordner mit dem ID-/Versionspaar als Name des Unterordners.

1. Schreiben Sie einen Registrierungsschlüssel, um den Speicherort des Pakets zu identifizieren:

    - Speicherort des Schlüssels: entweder das computerweite `HKEY_LOCAL_MACHINE\SOFTWARE[\Wow6432Node]\NuGet\Repository` verwenden oder, wenn es sich um Einzelbenutzervorlagen und Pakete handelt, alternativ `HKEY_CURRENT_USER\SOFTWARE\NuGet\Repository`.
    - Schlüsselname: Verwenden Sie einen Namen, der für Sie eindeutig ist. Die ASP.NET MVC 4-Vorlagen von Visual Studio 2012 verwenden z.B. `AspNetMvc4VS11`.
    - Werte: der vollständige Pfad zum Ordner „Pakete“.

1. Fügen Sie im `<packages>`-Element in der `.vstemplate`-Datei das Attribut `repository="registry"` hinzu, und geben Sie Ihren Registrierungsschlüsselnamen im `keyName`-Attribut an.

    - Wenn Sie bereits Pakete entpackt haben, verwenden Sie das `isPreunzipped="true"`-Attribut.
    - *(NuGet 3.2+)* Wenn Sie einen Build zur Entwurfszeit am Ende der Paketinstallation erzwingen möchten, fügen Sie das `forceDesignTimeBuild="true"`-Attribut hinzu.
    - Fügen Sie zur Optimierung `skipAssemblyReferences="true"` hinzu, da die Vorlage selbst bereits die erforderlichen Verweise enthält.

        ```xml
        <packages repository="registry" keyName="AspNetMvc4VS11" isPreunzipped="true">
            <package id="EntityFramework" version="5.0.0" skipAssemblyReferences="true" />
            <-- ... -->
        </packages>
        ```

## <a name="best-practices"></a>Empfehlungen

1. Deklarieren Sie eine Abhängigkeit in NuGet-VSIX, indem Sie im VSIX-Manifest einen Verweis darauf hinzufügen:

    ```xml
    <Reference Id="NuPackToolsVsix.Microsoft.67e54e40-0ae3-42c5-a949-fddf5739e7a5" MinVersion="1.7.30402.9028">
        <Name>NuGet Package Manager</Name>
        <MoreInfoUrl>http://docs.microsoft.com/nuget/</MoreInfoUrl>
    </Reference>
    <!-- ... -->
    ```

1. Erfordern Sie, dass Projekt-/Elementvorlagen bei der Erstellung gespeichert werden, indem Sie [`<PromptForSaveOnCreation>true</PromptForSaveOnCreation>`](/visualstudio/extensibility/promptforsaveoncreation-element-visual-studio-templates) in die `.vstemplate`-Datei einschließen.

1. Vorlagen enthalten keine `packages.config`-Datei, und enthalten keinerlei Verweise oder Inhalte, die bei der Installation von NuGet-Paketen hinzugefügt werden.
