---
title: Festlegen eines NuGet-Pakettyps
description: Beschreibt Pakettypen, um die beabsichtigte Verwendung eines Pakets anzugeben.
author: karann-msft
ms.author: karann
ms.date: 07/09/2019
ms.topic: conceptual
ms.openlocfilehash: 8a3ba6af19125b75af17cab8c093e89485e20324
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/12/2019
ms.locfileid: "67843492"
---
# <a name="set-a-nuget-package-type"></a>Festlegen eines NuGet-Pakettyps

In NuGet 3.5 und höher können Pakete mit einem bestimmten *Pakettyp* gekennzeichnet werden, um den vorgesehenen Zweck anzugeben. Pakete ohne Typ, einschließlich aller mit früheren Versionen von NuGet erstellten Pakete, haben standardmäßig den Typ `Dependency`.

- Pakete mit Typ `Dependency` fügen Bibliotheken und Anwendungen Build- oder Laufzeitressourcen hinzu und können in jedem Projekttyp installiert werden, wenn sie kompatibel sind.

- Pakete vom Typ `DotnetCliTool` sind Erweiterungen der [dotnet-CLI](/dotnet/articles/core/tools/index) und werden über die Befehlszeile aufgerufen. Solche Pakete können nur in .NET Core-Projekten installiert werden und haben keine Auswirkungen auf Wiederherstellungsvorgänge. Weitere Informationen zu diesen projektspezifischen Erweiterungen finden Sie in der Dokumentation zur [.NET Core-Erweiterbarkeit](/dotnet/articles/core/tools/extensibility#per-project-based-extensibility).

- Pakete des benutzerdefinierten Typs verwenden einen willkürlichen Typbezeichner, der den gleichen Formatierungsregeln wie Paketbezeichner unterliegt. Der NuGet-Paket-Manager in Visual Studio erkennt jedoch nur die Typen `Dependency` und `DotnetCliTool`.

Pakettypen werden in der `.nuspec`-Datei festgelegt. Für die Abwärtskompatibilität wird empfohlen, den `Dependency`-Typ *nicht* explizit festzulegen und stattdessen NuGet entscheiden zu lassen, wenn kein Typ angegeben ist.

- `.nuspec`: Geben Sie den Pakettyp innerhalb eines `packageTypes\packageType`-Knotens unter dem `<metadata>`-Element an:

    ```xml
    <?xml version="1.0" encoding="utf-8"?>
    <package xmlns="http://schemas.microsoft.com/packaging/2012/06/nuspec.xsd">
        <metadata>
        <!-- ... -->
        <packageTypes>
            <packageType name="DotnetCliTool" />
        </packageTypes>
        </metadata>
    </package>
    ```
