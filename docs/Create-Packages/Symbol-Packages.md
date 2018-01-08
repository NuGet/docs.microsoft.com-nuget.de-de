---
title: 'Vorgehensweise: Erstellen von NuGet-Symbolpaketen | Microsoft-Dokumentation'
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 9/12/2017
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 4667a70d-5a17-4f1e-b2f2-b8d0c6af3882
description: "Vorgehensweise bei der Erstellung von NuGet-Paketen, die nur Symbole für die Unterstützung des Debuggings anderer NuGet-Pakete in Visual Studio enthalten."
keywords: "NuGet-Symbolpakete, Debugging von NuGet-Paketen, Unterstützung von NuGet-Debugging, Paketsymbole, Symbolpaketkonventionen"
ms.reviewer:
- anangaur
- karann-msft
- unniravindranathan
ms.openlocfilehash: b1a29fe6e9a3dec6847dbed07761e28fb8eb9b19
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/14/2017
---
# <a name="creating-symbol-packages"></a>Erstellen von Symbolpaketen

Neben der Erstellung von Paketen für nuget.org oder andere Quellen unterstützt NuGet auch die Erstellung zugehöriger Symbolpakete sowie die Veröffentlichung dieser Pakete im [SymbolSource-Repository](http://www.symbolsource.org/Public).

Paketverbraucher können anschließend `http://srv.symbolsource.org/pdb/Public` zu ihren Symbolquellen in Visual Studio hinzufügen, wodurch Paketcode im Visual Studio Debugger schrittweise verwendet werden kann. Weitere Einzelheiten zu diesem Prozess finden Sie unter [Angeben von Symbol- (PDB) und Quelldateien im Visual Studio Debugger](https://docs.microsoft.com/visualstudio/debugger/specify-symbol-dot-pdb-and-source-files-in-the-visual-studio-debugger).


## <a name="creating-a-symbol-package"></a>Erstellen eines Symbolpakets

Folgen Sie den folgenden Konventionen, um ein Symbolpaket zu erstellen:

- Geben Sie dem Primärpaket (mit Ihrem Code) den Namen `{identifier}.nupkg`, und schließen Sie alle Dateien außer `.pdb` ein.
- Geben Sie dem Symbolpaket den Namen `{identifier}.symbols.nupkg`, und schließen Sie Ihre Assembly-DLL, `.pdb`-Dateien, XML DOC-Dateien und Quelldateien ein (siehe die folgenden Abschnitte).

Sie können beide Pakete mit der Option `-Symbols` aus einer `.nuspec`-Datei oder einer Projektdatei erstellen:

```
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
> Sie müssen [nuget.exe v4.1.0 oder höher](https://www.nuget.org/downloads) verwenden, um Pakete per Push an nuget.org übertragen zu können, da so die erforderlichen [NuGet-Protokolle](../api/nuget-protocols.md) implementiert werden.

1. Speichern Sie Ihren API-Schlüssel der Einfachheit halber zunächst mit NuGet (siehe [Paket veröffentlichen](../create-packages/publish-a-package.md)). Dieser gilt dann für nuget.org und symbolsource.org, da symbolsource.org mit nuget.org überprüft, ob Sie der Paketbesitzer sind.

    ```
    nuget SetApiKey Your-API-Key
    ```

1. Nachdem Sie Ihr primäres Paket auf nuget.org veröffentlicht haben, übertragen Sie das Symbolpaket wie folgt mithilfe von Push, wobei symbolsource.org automatisch als Ziel verwendet wird, da `.symbols` im Dateinamen enthalten ist:

    ```
    nuget push MyPackage.symbols.nupkg
    ```
> [!Note]
> Bei nuget.exe 4.5.0 oder höher werden die Symbolpakete nicht automatisch mithilfe von Push auf symbolsource.org übertragen. Sie müssten die Symbolpakete separat mithilfe von Push übertragen, wie im nächsten Schritt beschrieben wird.

1. Verwenden Sie die Option `-Source`, um ein anderes Symbolrepository zu veröffentlichen oder um ein Symbolpaket per Push zu übertragen, das nicht den Namenskonventionen folgt:

    ```
    nuget push MyPackage.symbols.nupkg -source https://nuget.smbsrc.net/
    ```

1. Sie können auch das primäre Paket und Symbolpakete gleichzeitig mithilfe von Push in beide Repositorys übertragen, indem Sie Folgendes verwenden:

    ```
    nuget push MyPackage.nupkg
    ```

In diesem Fall veröffentlicht NuGet `MyPackage.symbols.nupkg`, falls vorhanden, auf https://nuget.smbsrc.net/ (die Push-URL für symbolsource.org), nachdem das primäre Paket auf nuget.org veröffentlicht wurde.

## <a name="see-also"></a>Siehe auch

 - <a href="https://www.symbolsource.org/Public/Wiki/Using" target="_blank">Verwenden von SymbolSource</a> (symbolsource.org)
