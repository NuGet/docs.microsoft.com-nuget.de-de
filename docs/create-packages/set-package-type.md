---
title: Festlegen eines NuGet-Pakettyps
description: Beschreibt Pakettypen, um die beabsichtigte Verwendung eines Pakets anzugeben.
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: 1d869f616ce0291cf1c0a17b7ff20fc61e6a3bd5
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/07/2020
ms.locfileid: "78230823"
---
# <a name="set-a-nuget-package-type"></a>Festlegen eines NuGet-Pakettyps

In NuGet 3.5 und höher können Pakete mit einem bestimmten *Pakettyp* gekennzeichnet werden, um den vorgesehenen Zweck anzugeben. Pakete ohne Typ, einschließlich aller mit früheren Versionen von NuGet erstellten Pakete, haben standardmäßig den Typ `Dependency`.

- Pakete mit Typ `Dependency` fügen Bibliotheken und Anwendungen Build- oder Laufzeitressourcen hinzu und können in jedem Projekttyp installiert werden, wenn sie kompatibel sind.

- Pakete vom Typ `DotnetTool` sind Erweiterungen der [dotnet-CLI](/dotnet/articles/core/tools/index) und werden über die Befehlszeile aufgerufen. Solche Pakete können nur in .NET Core-Projekten installiert werden und haben keine Auswirkungen auf Wiederherstellungsvorgänge. Weitere Informationen zu diesen projektspezifischen Erweiterungen finden Sie in der Dokumentation zur [.NET Core-Erweiterbarkeit](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility).

- Pakete vom Typ `Template` stellen [benutzerdefinierten Vorlagen](/dotnet/core/tools/custom-templates) bereit, mit denen sich Dateien oder Projekte wie Apps, Dienste, Tools oder Klassenbibliotheken erstellen lassen.

- Pakete des benutzerdefinierten Typs verwenden einen willkürlichen Typbezeichner, der den gleichen Formatierungsregeln wie Paketbezeichner unterliegt. Der NuGet-Paket-Manager in Visual Studio erkennt jedoch nur die Typen `Dependency` und `DotnetTool`.

Pakettypen werden in der `.nuspec`-Datei festgelegt. Für die Abwärtskompatibilität wird empfohlen, den *-Typ* nicht`Dependency` explizit festzulegen und stattdessen NuGet entscheiden zu lassen, wenn kein Typ angegeben ist.

- `.nuspec`: Geben Sie den Pakettyp innerhalb eines `packageTypes\packageType`-Knotens unter dem `<metadata>`-Element an:

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <package xmlns="http://schemas.microsoft.com/packaging/2010/07/nuspec.xsd">
        <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="DotnetTool" />
        </packageTypes>
        </metadata>
    </package>
    ```
