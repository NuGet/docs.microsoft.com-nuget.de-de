---
title: Veröffentlichen von NuGet-Symbolpaketen mithilfe des neuen Formats für Symbolpakete „.snupkg“ | Microsoft-Dokumentation
author: JonDouglas
ms.author: jodou
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
ms.openlocfilehash: a62996a28348bf95e4581af180597d72cd5aa298
ms.sourcegitcommit: c8bf16420f235fc3e42c08cd0d56359e91d490e5
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/14/2021
ms.locfileid: "107387334"
---
# <a name="creating-symbol-packages-snupkg"></a>Erstellen von Symbolpaketen (.snupkg)

Für ein benutzerfreundliches Debugging sind Debugsymbole erforderlich, weil diese wichtige Informationen anzeigen, wie z. B. die Zuordnung des kompilierten Codes zum Quellcode, die Namen lokaler Variablen und Stapelüberwachungen. Mithilfe von Symbolpaketen (.snupkg) können Sie diese Symbole verteilen und das Debugging Ihrer NuGet-Pakete optimieren.

> Beachten Sie, dass ein Symbolpaket nicht die einzige Strategie ist, mit der die Debugsymbole den Consumern Ihrer Bibliothek zur Verfügung gestellt werden können. Sie können auch mit der folgenden Projekteigenschaft in die `dll`- oder die `exe`-Datei [eingebettet werden`embed`](/dotnet/core/deploying/single-file#include-pdb-files-inside-the-bundle): `<DebugType>embedded</DebugType>`

## <a name="prerequisites"></a>Voraussetzungen

[nuget.exe, Version 4.9.0 oder höher](https://www.nuget.org/downloads) oder die [.NET-CLI, Version 2.2.0 oder höher](https://www.microsoft.com/net/download/dotnet-core/2.2), da diese die erforderlichen [NuGet-Protokolle](../api/nuget-protocols.md) implementieren.

## <a name="creating-a-symbol-package"></a>Erstellen eines Symbolpakets

Wenn Sie die .NET-CLI oder MSBuild verwenden, müssen Sie die Eigenschaften `IncludeSymbols` und `SymbolPackageFormat` festlegen, um zusätzlich zur NUPKG-Datei eine SNUPKG-Datei zu erstellen.

* Fügen Sie entweder die folgenden Eigenschaften zur CSPROJ-Datei hinzu:

   ```xml
   <PropertyGroup>
      <IncludeSymbols>true</IncludeSymbols>
      <SymbolPackageFormat>snupkg</SymbolPackageFormat>
   </PropertyGroup>
   ```

* Geben Sie alternativ diese Eigenschaften in der Befehlszeile an:

     ```dotnetcli
     dotnet pack MyPackage.csproj -p:IncludeSymbols=true -p:SymbolPackageFormat=snupkg
     ```

  oder

  ```cli
  msbuild MyPackage.csproj /t:pack /p:IncludeSymbols=true /p:SymbolPackageFormat=snupkg
  ```

Wenn Sie „NuGet.exe“ verwenden, können Sie folgende Befehle verwenden, um eine SNUPKG-Datei zusätzlich zur NUPKG-Datei zu erstellen:

```cli
nuget pack MyPackage.nuspec -Symbols -SymbolPackageFormat snupkg

nuget pack MyPackage.csproj -Symbols -SymbolPackageFormat snupkg
```

Die Eigenschaft [`SymbolPackageFormat`](/dotnet/core/tools/csproj#symbolpackageformat) kann einen von zwei Werten besitzen: `symbols.nupkg` (Standard) oder `snupkg`. Wenn diese Eigenschaft nicht festgelegt wurde, wird ein älteres Legacypaket erstellt.

> [!Note]
> Das ältere Format `.symbols.nupkg` wird noch immer unterstützt, jedoch nur aus Kompatibilitätsgründen (z. B. native Pakete). Weitere Informationen finden Sie unter [Erstellen von Legacysymbolpaketen (.symbols.nupkg)](Symbol-Packages.md). Der NuGet.org-Symbolserver akzeptiert nur das neue Symbolpaketformat `.snupkg`.

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

NuGet.org unterstützt das eigene Symbolserverrepository und akzeptiert ausschließlich das neue Symbolpaketformat `.snupkg`. Paketverbraucher können die auf nuget.org-Symbolservern veröffentlichen Symbole verwenden, indem sie `https://symbols.nuget.org/download/symbols` zu ihren Symbolquellen in Visual Studio hinzufügen, wodurch Paketcode im Visual Studio Debugger schrittweise verwendet werden kann. Weitere Einzelheiten zu diesem Prozess finden Sie unter [Angeben von Symbol- (PDB) und Quelldateien im Visual Studio Debugger](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger).

### <a name="nugetorg-symbol-package-constraints"></a>Einschränkungen für NuGet.org-Symbolpakete

NuGet.org weist die folgenden Einschränkungen für Symbolpakete auf:

- Nur die folgenden Dateierweiterungen sind in Symbolpaketen zulässig: `.pdb`, `.nuspec`, `.xml`, `.psmdcp`, `.rels`, `.p7s`
- Auf dem NuGet-Symbolserver werden nur verwaltete [Portable PDB-Dateien](https://github.com/dotnet/runtime/blob/87572a799bfd37779c079faf28544e3f9a16be58/src/libraries/System.Reflection.Metadata/specs/PortablePdb-Metadata.md) unterstützt.
- Die PDB-Dateien und ihre zugehörigen NUPKG-DLLs müssen mit dem Compiler in Visual Studio 15.9 oder höher erstellt worden sein (weitere Informationen unter [PDB crypto hash (Kryptografiehash für PDB-Dateien)](https://github.com/dotnet/roslyn/issues/24429)).

Bei Symbol Paketen, die auf NuGet.org veröffentlicht werden, tritt bei der Überprüfung ein Fehler auf, wenn diese Bedingungen nicht erfüllt sind. 

> [!NOTE]
> Native Projekte wie C++-Projekte erzeugen Windows-PDB-Dateien anstelle von portierbaren PDB-Dateien. Diese werden vom Symbolserver von NuGet.org nicht unterstützt. Verwenden Sie stattdessen [Legacysymbolpakete](Symbol-Packages.md).

### <a name="symbol-package-validation-and-indexing"></a>Symbolpaketvalidierung und -indizierung

Per Push an [NuGet.org](https://www.nuget.org/) übertragene Symbolpakete werden verschiedenen Prüfungen unterzogen, darunter eine Prüfung auf Schadsoftware. Wenn bei einem Paket ein Fehler bei der Überprüfung auftritt, wird auf dessen Paketdetailseite eine Fehlermeldung angezeigt. Darüber hinaus erhalten die Besitzer des Pakets eine E-Mail mit Anweisungen zum Beheben der erkannten Probleme.

Wenn das Symbolpaket alle Überprüfungen bestanden hat, werden die Symbole von den Symbolservern von nuget.org indiziert und sind für die Verwendung verfügbar.

Die Validierung und Indizierung eines Pakets nimmt für gewöhnlich unter 15 Minuten in Anspruch. Wenn das Veröffentlichen des Pakets länger als erwartet dauert, besuchen Sie [status.nuget.org](https://status.nuget.org/), um zu überprüfen, ob gerade eine Störung auf nuget.org vorliegt. Wenn alle Systeme in Betrieb sind und das Paket innerhalb einer Stunde nicht erfolgreich veröffentlicht wurde, melden Sie sich auf nuget.org an, und informieren Sie uns über den Link zum Support auf der Paketdetailseite.

## <a name="symbol-package-structure"></a>Symbolpaketstruktur

Das Symbolpaket (.snupkg) weist die folgenden Eigenschaften auf:

1) Die SNUPKG-Datei hat dieselbe ID und Version wie das entsprechende NuGet-Paket (.nupkg).
2) Das Symbolpaket (.snupkg) weist bei allen DLL- oder EXE-Dateien dieselbe Ordnerstruktur wie die das NuGet-Paket (.nupkg) auf. Der einzige Unterschied ist, dass anstelle der DLL-/EXE-Dateien die entsprechenden PDB-Dateien in dieselbe Ordnerhierarchie aufgenommen werden. Dateien und Ordner mit anderen Erweiterungen als PDB werden aus der SNUPKG-Datei ausgeschlossen.
3) Die NUSPEC-Datei des Symbolpakets ist vom Pakettyp `SymbolsPackage`:

   ```xml
   <packageTypes>
      <packageType name="SymbolsPackage"/>
   </packageTypes>
   ```

4) Wenn sich ein Autor dazu entscheidet, eine benutzerdefinierte NUSPEC-Datei für die Erstellung von NUPKG- und SNUPKG-Dateien zu verwenden, muss die SNUPKG-Datei über die gleiche Ordnerhierarchie und die gleichen Dateien wie unter Punkt 2 beschrieben verfügen.
5) Die folgenden Felder werden aus der NUSPEC-Datei von SNUPKG ausgeschlossen: ```authors```, ```owners```, ```requireLicenseAcceptance```, ```license type```, ```licenseUrl``` und ```icon```.
6) Verwenden Sie nicht das ```<license>```-Element. Eine SNUPKG-Datei wird von der gleichen Lizenz abgedeckt wie die entsprechende NUPKG-Datei.

## <a name="see-also"></a>Siehe auch

Erwägen Sie die Verwendung von SourceLink, um das Debuggen des Quellcodes von .NET-Assemblys zu aktivieren. Weitere Informationen finden Sie in der [SourceLink-Anleitung](/dotnet/standard/library-guidance/sourcelink).

Weitere Informationen zu Symbolpaketen finden Sie in den Entwurfsspezifikationen für [NuGet Package Debugging & Symbols Improvements](https://github.com/NuGet/Home/wiki/NuGet-Package-Debugging-&-Symbols-Improvements) (Debuggen von NuGet-Paketen und Verbesserungen bei Symbolen).