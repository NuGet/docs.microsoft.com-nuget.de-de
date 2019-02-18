---
title: Erstellen und Veröffentlichen eines NuGet-Pakets mithilfe der . NET CLI
description: Eine exemplarische Vorgehensweise zur Erstellung und Veröffentlichung eines NuGet-Pakets mit der .NET Core-CLI „dotnet“.
author: karann-msft
ms.author: karann
ms.date: 01/24/2018
ms.topic: quickstart
ms.openlocfilehash: 3e459999eea45c5ae705a7e07c1a0fbb2e0cd1a1
ms.sourcegitcommit: d5a35a097e6b461ae791d9f66b3a85d5219d7305
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/12/2019
ms.locfileid: "56145617"
---
# <a name="quickstart-create-and-publish-a-package-dotnet-cli"></a>Schnellstart: Erstellen und Veröffentlichen eines Pakets (dotnet CLI)

Ein NuGet-Paket kann, mithilfe der `dotnet`-Befehlszeilenschnittstelle (CLI), problemlos über eine .NET-Klassenbibliothek erstellt und auf nuget.org veröffentlicht werden.

## <a name="prerequisites"></a>Erforderliche Komponenten

1. Installieren Sie das [.NET Core SDK](https://www.microsoft.com/net/download/), das die `dotnet`-CLI enthält.

1. [Registrieren Sie sich für ein kostenloses Konto auf nuget.org](https://www.nuget.org/users/account/LogOn?returnUrl=%2F), falls Sie noch kein Konto haben. Wenn Sie ein neues Konto erstellen, wird Ihnen eine Bestätigungs-E-Mail gesendet. Sie müssen das Konto bestätigen, bevor Sie ein Paket hochladen können.

## <a name="create-a-class-library-project"></a>Erstellen eines Klassenbibliotheksprojekts

Sie können ein vorhandenes Projekt in der .NET-Klassenbibliothek für Code verwenden, den Sie packen wollen, oder ein einfaches Projekt wie folgt erstellen:

1. Erstellen Sie einen Ordner namens `AppLogger` und öffnen diesen.

1. Erstellen Sie das Projekt mit dem Befehl `dotnet new classlib`, der den Namen des aktuellen Ordners für das Projekt verwendet.

## <a name="add-package-metadata-to-the-project-file"></a>Hinzufügen von Paketmetadaten zu einer Projektdatei

Jedes NuGet-Paket benötigt ein Manifest, das die Inhalte und Abhängigkeiten des Pakets beschreibt. In dem letzten Paket ist das Manifest eine `.nuspec`-Datei, die aus NuGet-Metadateneigenschaften erstellt wird, die Sie in der Projektdatei einbeziehen.

1. Öffnen Sie Ihre Projektdatei (`.csproj`), und fügen Sie die folgenden mindestens erforderlichen Eigenschaften in das vorhandene `<PropertyGroup>`-Tag ein, und passen Sie die Werte entsprechend an:

    ```xml
    <PackageId>AppLogger</PackageId>
    <Version>1.0.0</Version>
    <Authors>your_name</Authors>
    <Company>your_company</Company>
    ```

    > [!Important]
    > Weisen Sie dem Paket einen Bezeichner zu, der auf nuget.org bzw. auf dem Host, den Sie verwenden, einzigartig ist. Für diese exemplarische Vorgehensweise wird empfohlen, im Namen „Sample“ oder „Test“ zu verwenden, da der Name in einem späteren Veröffentlichungsschritt öffentlich sichtbar gemacht wird (auch wenn es unwahrscheinlich ist, dass jemand versucht, es zu verwenden).

1. Fügen Sie optionale Eigenschaften wie unter [NuGet-Metadateneigenschaften](/dotnet/core/tools/csproj#nuget-metadata-properties) beschrieben hinzu.

    > [!Note]
    > Bei Paketen für die öffentliche Nutzung sollten Sie besonders auf die **PackageTags**-Eigenschaft achten, da Tags anderen dabei helfen, Ihr Paket zu finden und dessen Funktion zu verstehen.

## <a name="run-the-pack-command"></a>Ausführen des Befehls pack

Um ein NuGet-Paket (eine `.nupkg`-Datei) aus dem Projekt zu erstellen, führen Sie den `dotnet pack`-Befehl aus, der auch das Projekt automatisch erstellt:

```cli
# Uses the project file in the current folder by default
dotnet pack
```

Die Ausgabe zeigt den Pfad zu der `.nupkg`-Datei:

```output
Microsoft (R) Build Engine version 15.5.180.51428 for .NET Core
Copyright (C) Microsoft Corporation. All rights reserved.

  Restore completed in 29.91 ms for D:\proj\AppLoggerNet\AppLogger\AppLogger.csproj.
  AppLogger -> D:\proj\AppLoggerNet\AppLogger\bin\Debug\netstandard2.0\AppLogger.dll
  Successfully created package 'D:\proj\AppLoggerNet\AppLogger\bin\Debug\AppLogger.1.0.0.nupkg'.
```

### <a name="automatically-generate-package-on-build"></a>Automatisches Generieren des Pakets bei der Erstellung

Um automatisch `dotnet pack` auszuführen, wenn Sie `dotnet build` ausführen, fügen Sie folgende Zeile zu Ihrer Projektdatei in `<PropertyGroup>` hinzu:

```xml
<GeneratePackageOnBuild>true</GeneratePackageOnBuild>
```

## <a name="publish-the-package"></a>Veröffentlichen des Pakets

Sobald Sie eine `.nupkg`-Datei haben, können Sie diese, gemeinsam mit einem API-Schlüssel von nuget.org, über den Befehl `dotnet nuget push` auf nuget.org veröffentlichen.

[!INCLUDE [publish-notes](includes/publish-notes.md)]

### <a name="acquire-your-api-key"></a>Erwerben des API-Schlüssels

[!INCLUDE [publish-api-key](includes/publish-api-key.md)]

### <a name="publish-with-dotnet-nuget-push"></a>Veröffentlichen mit „dotnet nuget push“

[!INCLUDE [publish-dotnet](includes/publish-dotnet.md)]

### <a name="publish-errors"></a>Veröffentlichungsfehler

[!INCLUDE [publish-errors](includes/publish-errors.md)]

### <a name="manage-the-published-package"></a>Verwalten des veröffentlichten Pakets

[!INCLUDE [publish-manage](includes/publish-manage.md)]

## <a name="related-topics"></a>Verwandte Themen

- [Erstellen eines Pakets](../create-packages/creating-a-package.md)
- [Veröffentlichen eines Pakets](../create-packages/publish-a-package.md)
- [Vorabversionen von Paketen](../create-packages/Prerelease-Packages.md)
- [Unterstützung mehrerer Zielframeworks](../create-packages/supporting-multiple-target-frameworks.md)
- [Paketversionsverwaltung](../reference/package-versioning.md)
- [Erstellen von lokalisierten Paketen](../create-packages/creating-localized-packages.md)
- [Erstellen von Symbolpaketen](../create-packages/symbol-packages-snupkg.md)
- [Signieren von Paketen](../create-packages/Sign-a-package.md)
