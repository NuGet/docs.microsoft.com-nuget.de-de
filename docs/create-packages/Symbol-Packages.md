---
title: 'Gewusst wie: Erstellen von NuGet-Symbolpaketen'
description: Vorgehensweise bei der Erstellung von NuGet-Paketen, die nur Symbole für die Unterstützung des Debuggings anderer NuGet-Pakete in Visual Studio enthalten.
author: karann-msft
ms.author: karann
ms.date: 09/12/2017
ms.topic: conceptual
ms.reviewer: anangaur
ms.openlocfilehash: 40f934f3c3fcea62acae66639c22108a93363b8b
ms.sourcegitcommit: b6810860b77b2d50aab031040b047c20a333aca3
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 06/28/2019
ms.locfileid: "67426780"
---
# <a name="creating-symbol-packages-legacy"></a>Erstellen von Symbolpaketen (Legacy)

> [!Important]
> Das neue empfohlene Format für Symbolpakete ist „.snupkg“. Weitere Informationen finden Sie unter [Erstellen von Symbolpaketen (.snupkg)](Symbol-Packages-snupkg.md). </br>
> Das Format „.symbols.nupkg“ wird aus Kompatibilitätsgründen noch immer unterstützt.

Neben der Erstellung von Paketen für nuget.org oder anderen Quellen, unterstützt NuGet auch die Erstellung zugehöriger Symbolpakete sowie die Veröffentlichung dieser Pakete im SymbolSource-Repository.

Paketverbraucher können anschließend `https://nuget.smbsrc.net` zu ihren Symbolquellen in Visual Studio hinzufügen, wodurch Paketcode im Visual Studio Debugger schrittweise verwendet werden kann. Weitere Einzelheiten zu diesem Prozess finden Sie unter [Angeben von Symbol- (PDB) und Quelldateien im Visual Studio Debugger](/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger).

## <a name="creating-a-symbol-package"></a>Erstellen eines Symbolpakets

Folgen Sie den folgenden Konventionen, um ein Symbolpaket zu erstellen:

- Geben Sie dem Primärpaket (mit Ihrem Code) den Namen `{identifier}.nupkg`, und schließen Sie alle Dateien außer `.pdb` ein.
- Geben Sie dem Symbolpaket den Namen `{identifier}.symbols.nupkg`, und schließen Sie Ihre Assembly-DLL, `.pdb`-Dateien, XML DOC-Dateien und Quelldateien ein (siehe die folgenden Abschnitte).

Sie können beide Pakete mit der Option `-Symbols` aus einer `.nuspec`-Datei oder einer Projektdatei erstellen:

```cli
nuget pack MyPackage.nuspec -Symbols

nuget pack MyProject.csproj -Symbols
```

Beachten Sie, dass für `pack` Mono 4.4.2 unter Mac OS X erforderlich ist und dass dieser Befehl auf Linux-Systemen nicht funktioniert. Auf einem Mac müssen Sie ebenfalls Windows-Pfadnamen in der `.nuspec`-Datei in Pfade im Unix-Format konvertieren.

## <a name="symbol-package-structure"></a>Symbolpaketstruktur

Ein Symbolpaket kann auf die gleiche Weise wie ein Bibliothekspaket auf mehrere Zielframeworks abzielen. Die Struktur des Ordners `lib` müsste demnach mit dem Primärpaket identisch sein, darin inbegriffen sind neben der DLL lediglich `.pdb`-Dateien.

Ein Symbolpaket, das .NET 4.0 und Silverlight 4 ansteuert, würde beispielsweise folgendes Layout aufweisen:

    \lib
        \net40
            \MyAssembly.dll
            \MyAssembly.pdb
        \sl40
            \MyAssembly.dll
            \MyAssembly.pdb

Quelldateien werden dann in einem separaten speziellen Ordner mit dem Namen `src` angeordnet. Dabei muss die relative Struktur Ihres Quellrepositorys eingehalten werden. Grund dafür ist, dass PDB-Dateien absolute Pfade zu Quelldateien für die Kompilierung der entsprechenden DLL enthalten und diese während des Veröffentlichungsprozesses gefunden werden müssen. Ein Basispfad (allgemeine Pfadpräfix) kann entfernt werden. Angenommen beispielsweise, eine Bibliothek wird aus folgenden Dateien erstellt:

    C:\Projects
        \MyProject
            \Common
                \MyClass.cs
            \Full
                \Properties
                    \AssemblyInfo.cs
                \MyAssembly.csproj (producing \lib\net40\MyAssembly.dll)
            \Silverlight
                \Properties
                    \AssemblyInfo.cs
                \MySilverlightExtensions.cs
                \MyAssembly.csproj (producing \lib\sl4\MyAssembly.dll)

Neben dem Ordner `lib` müsste ein Symbolpaket folgendes Layout enthalten:

    \src
        \Common
            \MyClass.cs
        \Full
            \Properties
                \AssemblyInfo.cs
        \Silverlight
            \Properties
                \AssemblyInfo.cs
            \MySilverlightExtensions.cs

## <a name="referring-to-files-in-the-nuspec"></a>Verweisen auf Dateien in der NUSPEC-Datei

Ein Symbolpaket kann, wie im vorherigen Abschnitt beschrieben, nach Konventionen aus einer Ordnerstruktur erstellt werden oder durch Angabe der zugehörigen Inhalte im Abschnitt `files` des Manifests. Verwenden Sie für die Erstellung des im vorherigen Abschnitts angezeigten Pakets beispielsweise Folgendes in der `.nuspec`-Datei:

```xml
<files>
    <file src="Full\bin\Debug\*.dll" target="lib\net40" />
    <file src="Full\bin\Debug\*.pdb" target="lib\net40" />
    <file src="Silverlight\bin\Debug\*.dll" target="lib\sl40" />
    <file src="Silverlight\bin\Debug\*.pdb" target="lib\sl40" />
    <file src="**\*.cs" target="src" />
</files>
```

## <a name="publishing-a-symbol-package"></a>Veröffentlichen eines Symbolpakets

> [!Important]
> Sie müssen [nuget.exe v4.9.1 oder höher](https://www.nuget.org/downloads) verwenden, um Pakete per Push an nuget.org übertragen zu können, da so die erforderlichen [NuGet-Protokolle](../api/nuget-protocols.md) implementiert werden.

1. Speichern Sie Ihren API-Schlüssel der Einfachheit halber zunächst mit NuGet (siehe [Paket veröffentlichen](../nuget-org/publish-a-package.md)). Dieser gilt dann für nuget.org und symbolsource.org, da symbolsource.org mit nuget.org überprüft, ob Sie der Paketbesitzer sind.

    ```cli
    nuget SetApiKey Your-API-Key
    ```

2. Nachdem Sie Ihr primäres Paket auf nuget.org veröffentlicht haben, übertragen Sie das Symbolpaket wie folgt mithilfe von Push, wobei symbolsource.org automatisch als Ziel verwendet wird, da `.symbols` im Dateinamen enthalten ist:

    ```cli
    nuget push MyPackage.symbols.nupkg
    ```

3. Verwenden Sie die Option `-Source`, um ein anderes Symbolrepository zu veröffentlichen oder um ein Symbolpaket per Push zu übertragen, das nicht den Namenskonventionen folgt:

    ```cli
    nuget push MyPackage.symbols.nupkg -source https://nuget.smbsrc.net/
    ```

4. Sie können auch das primäre Paket und Symbolpakete gleichzeitig mithilfe von Push in beide Repositorys übertragen, indem Sie Folgendes verwenden:

    ```cli
    nuget push MyPackage.nupkg
    ```

   > [!Note]
   > Bei nuget.exe 4.5.0 oder höher werden die Symbolpakete nicht automatisch mithilfe von Push auf symbolsource.org übertragen. Sie müssten die Symbolpakete separat mithilfe von Push übertragen, wie im nächsten Schritt beschrieben wird.
   
In diesem Fall veröffentlicht NuGet `MyPackage.symbols.nupkg`, falls vorhanden, auf https://nuget.smbsrc.net/ (die Push-URL für symbolsource.org), nachdem das primäre Paket auf nuget.org veröffentlicht wurde.

## <a name="see-also"></a>Siehe auch

[Moving to the new SymbolSource engine (Umstieg auf die neue SymbolSource-Engine)](https://tripleemcoder.com/2015/10/04/moving-to-the-new-symbolsource-engine/) (symbolsource.org)
