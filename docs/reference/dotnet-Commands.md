---
title: DotNet-CLI-nuget-Befehle
description: Eine kurze Referenz für nuget-bezogene Befehle, die die dotnet-Befehlszeilenschnittstelle verwenden.
author: karann-msft
ms.author: karann
ms.date: 06/24/2019
ms.topic: conceptual
ms.openlocfilehash: 87cb3c8153931a0917338de9f7001406b5e12dfc
ms.sourcegitcommit: 53b06e27bcfef03500a69548ba2db069b55837f1
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/19/2020
ms.locfileid: "97699825"
---
# <a name="dotnet-cli-commands"></a>.NET-CLI-Befehle

Die `dotnet` Befehlszeilenschnittstelle (Command-Line Interface, CLI), die unter Windows, Mac OS X und Linux ausgeführt wird, bietet eine Reihe wichtiger Befehle, z. b. das installieren, wiederherstellen und Veröffentlichen von Paketen. Wenn dotnet Ihre Anforderungen erfüllt, ist es nicht erforderlich, zu verwenden `nuget.exe` .

Beispiele für die Verwendung dieser Befehle zum Verarbeiten von Paketen finden Sie unter [Installieren und Verwalten von Paketen mithilfe der dotnet-CLI](../consume-packages/install-use-packages-dotnet-cli.md). Beispiele für die Verwendung dieser Befehle zum Erstellen von Paketen finden Sie unter [Erstellen und Veröffentlichen eines Pakets mithilfe der dotnet-CLI](../quickstart/create-and-publish-a-package-using-the-dotnet-cli.md).

Die Befehlsreferenz für die Befehls `dotnet` Zeilen Schnittstelle finden Sie unter [.net Core CLI-Tools (Command-Line Interface, Befehlszeilenschnittstelle)](/dotnet/core/tools/?tabs=netcore2x).

## <a name="package-consumption"></a>Paket Verbrauch

- [**dotnet Add Package**](/dotnet/core/tools/dotnet-add-package): Fügt einen Paket Verweis zur Projektdatei hinzu und führt dann aus, `dotnet restore` um das Paket zu installieren.
- [**dotnet Remove Package**](/dotnet/core/tools/dotnet-remove-package): entfernt einen Paket Verweis aus der Projektdatei.
- [**dotnet Restore**](/dotnet/core/tools/dotnet-restore?tabs=netcore2x): stellt die Abhängigkeiten und Tools eines Projekts wieder her. Ab NuGet 4.0 wird derselbe Code ausgeführt wie für `nuget restore`.
- [**dotnet nuget Locals**](/dotnet/core/tools/dotnet-nuget-locals): Listet die Speicherorte der Ordner " *Global-Packages*", " *http-Cache*" und " *Temp* " auf und löscht den Inhalt dieser Ordner.
- [**dotnet New nugetconfig**](/dotnet/core/tools/dotnet-new): erstellt eine [`nuget.config`](../reference/nuget-config-file.md) Datei zum Konfigurieren des nuget-Verhaltens.

## <a name="package-creation"></a>Paket Erstellung

- [**dotnet Pack**](/dotnet/core/tools/dotnet-pack?tabs=netcore2x): packt den Code in ein nuget-Paket.
- [**dotnet nuget Push**](/dotnet/core/tools/dotnet-nuget-push): veröffentlicht ein Paket auf einem nuget-Server. Gilt für nuget.org-, Azure Artifacts-und [nuget-Server von Drittanbietern](../hosting-packages/overview.md).
- [**dotnet nuget DELETE**](/dotnet/core/tools/dotnet-nuget-delete): Löscht ein Paket von einem nuget-Server oder hebt die Auflistung auf. Gilt für nuget.org-, Azure Artifacts-und [nuget-Server von Drittanbietern](../hosting-packages/overview.md).
- [**dotnet nuget Verify**](/dotnet/core/tools/dotnet-nuget-verify): überprüft ein signiertes nuget-Paket.
