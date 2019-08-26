---
title: Veröffentlichen von NuGet-Symbolpaketen mithilfe des neuen Formats für Symbolpakete „.snupkg“ | Microsoft-Dokumentation
author: cristinamanu
ms.author: cristinamanu
manager: skofman
ms.date: 10/30/2018
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Erstellen von NuGet-Symbolpaketen (.snupkg)
keywords: NuGet-Symbolpakete, Debugging von NuGet-Paketen, Unterstützung von NuGet-Debugging, Paketsymbole, Symbolpaketkonventionen
ms.reviewer:
- anangaur
- karann
ms.openlocfilehash: 992b3ddd04a1bb34e7aca25dfaa6f7df5485907b
ms.sourcegitcommit: 80cf99f40759911324468be1ec815c96aebf376d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 08/17/2019
ms.locfileid: "69564536"
---
# <a name="creating-symbol-packages-snupkg"></a>Erstellen von Symbolpaketen (.snupkg)

Mithilfe von Symbolpaketen kann das Debuggen von NuGet-Paketen verbessert werden.

## <a name="prerequisites"></a>Erforderliche Komponenten

[nuget.exe v4.9.0 oder höher](https://www.nuget.org/downloads) oder [dotnet.exe v2.2.0 oder höher](https://www.microsoft.com/net/download/dotnet-core/2.2), die die erforderlichen [NuGet-Protokolle](../api/nuget-protocols.md) implementieren.

## <a name="creating-a-symbol-package"></a>Erstellen eines Symbolpakets

Sie können ein snupkg-Symbolpaket mithilfe von „dotnet.exe“, „NuGet.exe“ oder MSBuild erstellen. Wenn Sie „NuGet.exe“ verwenden, können Sie folgende Befehle verwenden, um eine SNUPKG-Datei zusätzlich zur NUPKG-Datei zu erstellen:

```
nuget pack MyPackage.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack MyPackage.csproj -Symbols -SymbolPackageFormat snupkg
```

Wenn Sie „dotnet.exe“ oder MSBuild verwenden, können Sie folgende Schritte befolgen, um eine SNUPKG-Datei zusätzlich zur NUPKG-Datei zu erstellen:

1. Fügen Sie folgende Eigenschaften zur CSPROJ-Datei hinzu:

    ```xml
    <PropertyGroup>
      <IncludeSymbols>true</IncludeSymbols>
      <SymbolPackageFormat>snupkg</SymbolPackageFormat>
    </PropertyGroup>
    ```

1. Packen Sie Ihr Projekt mit `dotnet pack MyPackage.csproj` oder `msbuild -t:pack MyPackage.csproj`.

Die Eigenschaft [`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat) kann einen von zwei Werten besitzen: `symbols.nupkg` (Standard) oder `snupkg`. Wenn die Eigenschaft [`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat) nicht festgelegt wurde, wird ein älteres Symbolpaket erstellt.

> [!Note]
> Das ältere Format `.symbols.nupkg` wir noch immer unterstützt, jedoch nur aus Kompatibilitätsgründen (weitere Informationen unter [Erstellen von Symbolpaketen](Symbol-Packages.md)). Der NuGet.org-Symbolserver akzeptiert nur das neue Symbolpaketformat `.snupkg`.

## <a name="publishing-a-symbol-package"></a>Veröffentlichen eines Symbolpakets

1. Speichern Sie zunächst der Einfachheit halber Ihren API-Schlüssel mit NuGet (weitere Informationen unter [publish a package (Veröffentlichen eines Pakets)](../nuget-org/publish-a-package.md)).

    ```cli
    nuget SetApiKey Your-API-Key
    ```

1. Nachdem Sie Ihr primäres Paket auf nuget.org veröffentlicht haben, übertragen Sie Ihr Symbol mithilfe von Push wie hier dargestellt:

    ```cli
    nuget push MyPackage.snupkg
    ```

1. Sie können mit dem folgenden Befehl auch das primäre Paket und Symbolpakete gleichzeitig mithilfe von Push übertragen, um Zeit zu sparen. Die NUPKG- und SNUPKG-Dateien müssen jeweils im aktuellen Ordner vorhanden sein.

    ```cli
    nuget push MyPackage.nupkg
    ```

NuGet veröffentlicht beide Pakete auf nuget.org. `MyPackage.nupkg` wird zuerst veröffentlicht, gefolgt von `MyPackage.snupkg`.

> [!Note]
> Wenn das Symbolpaket nicht veröffentlicht wird, vergewissern Sie sich, dass Sie die NuGet.org-Quelle folgendermaßen konfiguriert haben: `https://api.nuget.org/v3/index.json`. Die Veröffentlichung des Symbolpakets wird nur von der [NuGet V3-API](../api/overview.md#versioning) unterstützt.

## <a name="nugetorg-symbol-server"></a>NuGet.org-Symbolserver

NuGet.org unterstützt das eigene Symbolserverrepository und akzeptiert ausschließlich das neue Symbolpaketformat `.snupkg`. Paketverbraucher können die auf nuget.org-Symbolservern veröffentlichen Symbole verwenden, indem sie `https://symbols.nuget.org/download/symbols` zu ihren Symbolquellen in Visual Studio hinzufügen, wodurch Paketcode im Visual Studio Debugger schrittweise verwendet werden kann. Weitere Einzelheiten zu diesem Prozess finden Sie unter [Angeben von Symbol- (PDB) und Quelldateien im Visual Studio Debugger](https://docs.microsoft.com/en-us/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger?view=vs-2017).

### <a name="nugetorg-symbol-package-constraints"></a>Einschränkungen für nuget.org-Symbolpakete

Die auf nuget.org unterstützten Symbolpakete unterliegen den folgenden Einschränkungen

- Es dürfen ausschließlich die folgenden Dateierweiterungen an ein Symbolpaket angefügt werden. ```.pdb,.nuspec,.xml,.psmdcp,.rels,.p7s```
- Auf dem NuGet-Symbolserver werden derzeit nur verwaltete und [portable PDB-Dateien](https://github.com/dotnet/corefx/blob/master/src/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) unterstützt.
- Die PDB-Dateien und zugehörigen NUPKG-DLLs müssen mit dem Compiler in Visual Studio 15.9 oder höher erstellt worden sein (weiter Informationen unter [pdb crypto hash (Kryptografiehash für PDB-Dateien)](https://github.com/dotnet/roslyn/issues/24429)).

Das auf nuget.org veröffentlichte Symbolpaket schlägt fehl, wenn ein anderer Dateityp in der SNUPKG-Datei enthalten ist.

### <a name="symbol-package-validation-and-indexing"></a>Symbolpaketvalidierung und -indizierung

Per Push an [NuGet.org](https://www.nuget.org/) übertragene Symbolpakete werden verschiedenen Prüfungen, wie z.B. auf Viren, unterzogen.

Wenn das Paket alle Validierungsüberprüfungen bestanden hat, kann es dennoch eine Weile dauern, bis die Symbole indiziert werden und zur Nutzung über die NuGet.org-Symbolserver bereitstehen. Wenn das Paket eine Validierungsüberprüfung nicht besteht, wird die Paketdetailansicht für NUPKG aktualisiert und zeigt den entsprechenden Fehler an. Auch dann erhalten Sie eine E-Mail-Benachrichtigung.

Die Validierung und Indizierung eines Pakets nimmt für gewöhnlich unter 15 Minuten in Anspruch. Wenn das Veröffentlichen des Pakets längere Zeit als erwartet in Anspruch nimmt, besuchen Sie [status.nuget.org](https://status.nuget.org/), um zu überprüfen, ob gerade eine Störung auf nuget.org vorliegt. Wenn alle Systeme in Betrieb sind und das Paket innerhalb einer Stunde nicht erfolgreich veröffentlicht wurde, melden Sie sich auf nuget.org an, und informieren Sie uns über den Link zum Support auf der Paketdetailseite.

## <a name="symbol-package-structure"></a>Symbolpaketstruktur

Die NUPKG-Datei wäre genau dieselbe wie heute, die SNUPKG-Datei würde jedoch folgende Eigenschaften aufweisen:

1) Die SNUPKG-Datei besitzt dieselbe ID und Version wie die entsprechende NUPKG-Datei.
2) Für jede DLL- oder EXE-Datei enthält die SNUPKG-Datei dann dieselbe Ordnerstruktur wie die NUPKG-Datei, mit dem einzigen Unterschied, dass die entsprechenden PDB-Dateien in der gleichen Ordnerhierarchie eingeschlossen werden würden (anstelle der DLL-/EXE-Dateien). Dateien und Ordner mit anderen Erweiterungen als PDB werden aus der SNUPKG-Datei ausgeschlossen.
3) Die NUSPEC-Datei im SNUPKG-Paket gibt auch einen neuen PackageType an, so wie unten dargestellt. Dieser sollte der einzige angegebene PackageType sein.

   ```xml
   <packageTypes>
      <packageType name="SymbolsPackage"/>
   </packageTypes>
   ```

4) Wenn sich ein Autor dazu entscheidet, eine benutzerdefinierte NUSPEC-Datei für die Erstellung von NUPKG- und SNUPKG-Dateien zu verwenden, muss die SNUPKG-Datei über die gleiche Ordnerhierarchie und die gleichen Dateien wie unter Punkt 2 beschrieben verfügen.
5) Die Felder ```authors``` und ```owners``` werden aus der NUSPEC-Datei von SNUPKG ausgeschlossen.
6) Verwenden Sie nicht das <license>-Element. Eine SNUPKG-Datei wird von der gleichen Lizenz abgedeckt wie die entsprechende NUPKG-Datei.

## <a name="see-also"></a>Siehe auch

[NuGet-Package-Debugging-&-Symbols-Improvements (Verbesserungen für das Debuggen und die Symbole von NuGet-Paketen)](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements)
