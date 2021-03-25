---
title: Auswählen von Assemblys, auf die von Projekten verwiesen wird
description: Stellen Sie im Paket eine Teilmenge der Assemblys für den Compiler zur Verfügung – zur Laufzeit stehen alle Assemblys zur Verfügung.
author: zivkan
ms.author: zivkan
ms.date: 05/24/2019
ms.topic: conceptual
ms.openlocfilehash: b2202946d0060e09828250d240f931044d1bf485
ms.sourcegitcommit: bb9560dcc7055bde84b4940c5eb0db402bf46a48
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 03/23/2021
ms.locfileid: "104859030"
---
# <a name="select-assemblies-referenced-by-projects"></a>Auswählen von Assemblys, auf die von Projekten verwiesen wird

Explizite Assemblyverweise ermöglichen es, eine Teilmenge von Assemblys für IntelliSense und Kompilierung zu nutzen, während zur Laufzeit alle Assemblys zur Verfügung stehen. `PackageReference` und `packages.config` funktionieren unterschiedlich. Aus diesem Grund müssen Paketautoren beim Erstellen von Paketen darauf achten, dass diese mit beiden Projekttypen kompatibel sind.

> [!Note]
> Explizite Assemblyverweise beziehen sich auf .NET-Assemblys. Sie sind keine Methode zum Verteilen nativer Assemblys, die durch eine verwaltete Assembly über „P/Invoke“ aufgerufen werden.

## <a name="packagereference-support"></a>`PackageReference`-Unterstützung

Wenn ein Projekt ein Paket mit `PackageReference` verwendet und das Paket ein `ref\<tfm>\`-Verzeichnis enthält, klassifiziert NuGet diese Assemblys als Kompilierzeitressourcen, während `lib\<tfm>\`-Assemblys als Laufzeitressourcen klassifiziert werden. Assemblys in `ref\<tfm>\` werden nicht zur Laufzeit verwendet. Dies bedeutet, dass jede Assembly in `ref\<tfm>\` über eine entsprechende Assembly in `lib\<tfm>\` oder einem relevanten `runtime\`-Verzeichnis verfügen muss. Andernfalls kommt es wahrscheinlich zu Laufzeitfehlern. Da Assemblys in `ref\<tfm>\` nicht zur Laufzeit verwendet werden, kann es sich um [reine Metadatenassemblys](https://github.com/dotnet/roslyn/blob/main/docs/features/refout.md) zum Verringern der Paketgröße handeln.

> [!Important]
> Wenn ein Paket das nuspec-Element `<references>` umfasst (von `packages.config` verwendet, siehe unten) und in `ref\<tfm>\` keine Assemblys enthält, kündigt NuGet die im nuspec-Element `<references>` aufgeführten Assemblys sowohl als Kompilierzeit- als auch als Laufzeitressourcen an. Dies bedeutet, dass es zu Laufzeitausnahmen kommt, wenn die referenzierten Assemblys eine andere Assembly im `lib\<tfm>\`-Verzeichnis laden müssen.

> [!Note]
> Wenn das Paket ein `runtime\`-Verzeichnis enthält, darf NuGet die Ressourcen im `lib\`-Verzeichnis nicht verwenden.

## <a name="packagesconfig-support"></a>`packages.config`-Unterstützung

Projekte mit Verwendung von `packages.config` zum Verwalten von NuGet-Paketen fügen normalerweise Verweise auf alle Assemblys im `lib\<tfm>\`-Verzeichnis hinzu. Das `ref\`-Verzeichnis wurde hinzugefügt, um `PackageReference` zu unterstützen und wird deshalb bei Verwendung von `packages.config` nicht berücksichtigt. Um explizit über `packages.config` festzulegen, welche Assemblys für Projekte referenziert werden, muss das Paket das [`<references>`-Element in der nuspec-Datei](../reference/nuspec.md#explicit-assembly-references) verwenden. Zum Beispiel:

```xml
<references>
    <group targetFramework="net45">
        <reference file="MyLibrary.dll" />
    </group>
</references>
```

> [!Note]
> Das Projekt `packages.config` verwendet einen Prozess namens [ResolveAssemblyReference](https://github.com/Microsoft/msbuild/blob/main/documentation/wiki/ResolveAssemblyReference.md), um Assemblys in das Ausgabeverzeichnis `bin\<configuration>\` zu kopieren. Ihre Projektassembly wird kopiert, anschließend sucht das Buildsystem im Assemblymanifest nach referenzierten Assemblys und kopiert diese Assemblys. Dieser Vorgang wird rekursiv für alle Assemblys wiederholt. Dies bedeutet Folgendes: Wenn eine der Assemblys in Ihrem Verzeichnis `lib\<tfm>\` nicht als Abhängigkeit im Manifest einer anderen Assembly aufgeführt ist (wenn die Assembly zur Laufzeit über `Assembly.Load`, MEF oder ein anderes Framework zur Abhängigkeitsinjektion geladen wird), dann wird sie möglicherweise nicht in das Ausgabeverzeichnis `bin\<configuration>\` Ihres Projekts kopiert, obwohl sie in `bin\<tfm>\` enthalten ist.

## <a name="example"></a>Beispiel

Das Beispielpaket enthält drei Assemblys – `MyLib.dll`, `MyHelpers.dll` und `MyUtilities.dll` –, die auf .NET Framework 4.7.2 ausgerichtet sind. `MyUtilities.dll` enthält Klassen, die nur von den anderen zwei Assemblys verwendet werden sollen, deshalb sollen diese Klassen nicht in IntelliSense oder zur Kompilierzeit für Projekte zur Verfügung stehen, die das Beispielpaket verwenden. Die Datei `nuspec` muss folgende XML-Elemente enthalten:

```xml
<references>
    <group targetFramework="net472">
        <reference file="MyLib.dll" />
        <reference file="MyHelpers.dll" />
    </group>
</references>
```

Im Paket sind folgende Dateien enthalten:

```text
lib\net472\MyLib.dll
lib\net472\MyHelpers.dll
lib\net472\MyUtilities.dll
ref\net472\MyLib.dll
ref\net472\MyHelpers.dll
```
