---
title: DotNet-CLI-nuget-Befehle
description: Eine kurze Referenz für nuget-bezogene Befehle, die die dotnet-Befehlszeilenschnittstelle verwenden.
author: karann-msft
ms.author: karann
ms.date: 06/24/2019
ms.topic: conceptual
ms.openlocfilehash: ff011e60d3de3b0999db56e1e30e97e538bd9fb4
ms.sourcegitcommit: efc18d484fdf0c7a8979b564dcb191c030601bb4
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/18/2019
ms.locfileid: "68327487"
---
# <a name="dotnet-cli-commands"></a>DotNet-CLI-Befehle

Die `dotnet` Befehlszeilenschnittstelle (Command-Line Interface, CLI), die unter Windows, Mac OS X und Linux ausgeführt wird, bietet eine Reihe wichtiger Befehle, z. b. das installieren, wiederherstellen und Veröffentlichen von Paketen. Wenn dotnet Ihre Anforderungen erfüllt, ist es nicht erforderlich, zu `nuget.exe`verwenden.

Beispiele für die Verwendung dieser Befehle zum Verarbeiten von Paketen finden Sie unter [Installieren und Verwalten von Paketen mithilfe der dotnet-CLI](../consume-packages/install-use-packages-dotnet-cli.md). Beispiele für die Verwendung dieser Befehle zum Erstellen von Paketen finden Sie unter [Erstellen und Veröffentlichen eines Pakets mithilfe der dotnet-CLI](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md).

Die Befehlsreferenz `dotnet` für die Befehlszeilenschnittstelle finden Sie unter [.net Core CLI-Tools (Command-Line Interface, Befehlszeilenschnittstelle)](/dotnet/core/tools/?tabs=netcore2x).

## <a name="package-consumption"></a>Paket Verbrauch

- [**dotnet Add-Paket**](/dotnet/core/tools/dotnet-add-package): Fügt der Projektdatei einen Paket Verweis hinzu und führt `dotnet restore` dann aus, um das Paket zu installieren.
- [**Paket "dotnet Remove**](/dotnet/core/tools/dotnet-remove-package)": Entfernt einen Paket Verweis aus der Projektdatei.
- [**dotnet Restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): Stellt die Abhängigkeiten und Tools eines Projekts wieder her. Ab NuGet 4.0 wird derselbe Code ausgeführt wie für `nuget restore`.
- [**dotnet nuget-lokale**](/dotnet/core/tools/dotnet-nuget-locals)Variablen: Listet die Speicherorte der Ordner " *Global-Packages*", " *http-Cache*" und " *Temp* " auf und löscht den Inhalt dieser Ordner.
- [**dotnet New nugetconfig**](/dotnet/core/tools/dotnet-new): Erstellt eine [`nuget.config`](../reference/nuget-config-file.md) Datei zum Konfigurieren des nuget-Verhaltens.

## <a name="package-creation"></a>Paket Erstellung

- [**dotnet Pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): Packt den Code in ein nuget-Paket.
- [**dotnet-nuget-Push**](/dotnet/core/tools/dotnet-nuget-push): Veröffentlicht ein Paket auf einem nuget-Server. Gilt für nuget.org-, Azure Artifacts-und [nuget-Server von Drittanbietern](../hosting-packages/overview.md).
- [**dotnet nuget-Löschung**](/dotnet/core/tools/dotnet-nuget-delete): Löscht ein Paket von einem nuget-Server oder hebt die Auflistung auf. Gilt für nuget.org-, Azure Artifacts-und [nuget-Server von Drittanbietern](../hosting-packages/overview.md).
