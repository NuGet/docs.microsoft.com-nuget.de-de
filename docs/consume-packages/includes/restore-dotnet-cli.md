---
ms.openlocfilehash: ef54f102352a3d088181ad6f7c356b8c7eeac166
ms.sourcegitcommit: fe34b1fc79d6a9b2943a951f70b820037d2dd72d
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/04/2019
ms.locfileid: "74825173"
---
Verwenden Sie den Befehl [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x), der Pakete wiederherstellt, die in der Projektdatei aufgelistet sind (siehe [PackageReference](../../consume-packages/package-references-in-project-files.md)). In .NET Core 2.0 und höher erfolgt die Wiederherstellung automatisch mit `dotnet build` und `dotnet run`. Ab NuGet 4.0 wird derselbe Code ausgeführt wie für `nuget restore`.

Öffnen Sie wie bei anderen `dotnet`-CLI-Befehlen zunächst eine Befehlszeile, und wechseln Sie zu dem Verzeichnis, das die Projektdatei enthält.

Wiederherstellen eines Pakets mit `dotnet restore`:

```dotnetcli
dotnet restore 
```