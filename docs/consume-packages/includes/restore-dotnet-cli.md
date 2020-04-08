---
ms.openlocfilehash: ef54f102352a3d088181ad6f7c356b8c7eeac166
ms.sourcegitcommit: 2b50c450cca521681a384aa466ab666679a40213
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/07/2020
ms.locfileid: "74825173"
---
Verwenden Sie den Befehl [dotnet restore](/dotnet/core/tools/dotnet-restore?tabs=netcore2x), der Pakete wiederherstellt, die in der Projektdatei aufgelistet sind (siehe [PackageReference](../../consume-packages/package-references-in-project-files.md)). In .NET Core 2.0 und höher erfolgt die Wiederherstellung automatisch mit `dotnet build` und `dotnet run`. Ab NuGet 4.0 wird derselbe Code ausgeführt wie für `nuget restore`.

Öffnen Sie wie bei anderen `dotnet`-CLI-Befehlen zunächst eine Befehlszeile, und wechseln Sie zu dem Verzeichnis, das die Projektdatei enthält.

Wiederherstellen eines Pakets mit `dotnet restore`:

```dotnetcli
dotnet restore 
```