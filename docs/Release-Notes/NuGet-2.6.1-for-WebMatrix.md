---
title: NuGet 2.6.1 WebMatrix Versionshinweise | Microsoft Docs
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
ms.assetid: 119ea65b-b38b-4a8c-a4ed-6ea06f1aad09
description: "Versionshinweise für NuGet 2.6.1 für WebMatrix, einschließlich der bekannten Probleme, Fehlerbehebungen, Funktionen und Archivierung von dcrs Design."
keywords: "NuGet 2.6.1 für WebMatrix-Versionshinweise, Fehlerbehebungen, bekannten Problemen, die zusätzliche Funktionen, Archivierung von dcrs Design"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 9c37ddc998378b8aaa477dd5df814bab6f0b3c58
ms.sourcegitcommit: 262d026beeffd4f3b6fc47d780a2f701451663a8
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2018
---
# <a name="nuget-261-for-webmatrix-release-notes"></a>NuGet 2.6.1 WebMatrix-Versionshinweise

[Anmerkungen zur Version des NuGet-2.6](../release-notes/nuget-2.6.md) | [NuGet 2.7-Versionshinweise](../release-notes/nuget-2.7.md)

Das NuGet-Team hat eine aktualisierte NuGet-Paket-Manager-Erweiterung für WebMatrix 26 März 2014 veröffentlicht.  Dieses Update installiert werden kann, aus der [WebMatrix Erweiterungskatalog](http://extensions.webmatrix.com/packages/NuGetPackageManager/) mithilfe der folgenden Schritte:

1. Öffnen Sie WebMatrix 3
2. Klicken Sie auf das Symbol "Erweiterungen" im Menüband Home
3. Wählen Sie die Registerkarte "Softwareupdates"
4. Klicken Sie auf, um NuGet-Paket-Manager auf 2.6.1 zu aktualisieren.
6. Schließen Sie, und starten Sie die WebMatrix-3

## <a name="notable-changes"></a>Wichtige Änderungen

Diese Erweiterung behebt zwei der größten Probleme Benutzer haben verbrauchende NuGet-Pakete in WebMatrix Datenwachstums.  Das erste ist ein NuGet-Schema-Version-Fehler und die zweite wurde ein Fehler auf 0 Byte-DLLs in führenden der `bin` Ordner.

### <a name="nuget-schema-version-error"></a>NuGet-Version Schemafehler

Seit der Freigabe von WebMatrix 3 wurden neue Funktionen eingeführt in NuGet, die eine neue Version des Datenbankschemas für die NuGet-Pakete erfordern.  Beim Versuch, die NuGet-Pakete auf der Website zu verwalten, können diese neue Pakete zu Fehlern führen, die Sie in WebMatrix sehen.

![Es ist ein Fehler aufgetreten. Die Schemaversion ist nicht kompatibel. Sie ein upgrade von NuGet auf die neueste Version.](./media/NuGet-2.8/webmatrix-schema-version.png)

Diese neueste Version bietet Kompatibilität mit den neuesten NuGet-Pakete verhindern, dass dieser Fehler auftritt. Neue Versionen der Pakete, einschließlich Microsoft.AspNet.WebPages können jetzt in WebMatrix installiert werden.  Einige dieser Pakete wurden mithilfe von NuGet-Funktionen wie [XDT Config transformiert](../release-notes/nuget-2.6.md#xdt), dies wurde nicht in WebMatrix unterstützt, die bisher.

### <a name="zero-byte-dlls-in-bin-folder"></a>0 Byte-DLLs im Ordner "bin" "

Einige Benutzer haben gemeldet, dass nach dem Installieren von NuGet Pakete einrichten in WebMatrix mit DLLs, die kopiert werden, um zu klassifizieren, die DLLs zum Anzeigen der `bin` Ordner als 0-Byte-Dateien.  Dieser Vorgang ist die Anwendung zur Laufzeit.

[Dieses Problem](https://nuget.codeplex.com/workitem/4060) wurde jetzt behoben.

## <a name="other-recent-improvements"></a>Weitere Verbesserungen

NuGet-Paket-Manager 2.8 für Visual Studio veröffentlicht wurde, veröffentlicht haben wir auch NuGet Package Manager 2.5.0 für WebMatrix.  Während dies, in erwähnt wurde der [NuGet 2.8-Anmerkungen zu dieser Version](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates), haben nicht wir erwähnt, die spezifische neue Funktionen, die Updates eingeführt.

### <a name="update-all"></a>Alle aktualisieren

Sie können alle Ihre Website-Pakete in einem Schritt jetzt aktualisieren!  Wenn Sie das NuGet-Erweiterung in WebMatrix öffnen, sehen Sie die Liste aller Pakete in der Galerie, installiert und die Beziehungen und Updates verfügbar.  Zuvor jedes Paket müssten einzeln aktualisiert werden, aber jetzt besteht eine nützliche "Alle aktualisieren"-Schaltfläche, die auf der Registerkarte "Updates" wird angezeigt.

![Klicken Sie auf "Alle aktualisieren", um alle Pakete mit verfügbaren Updates aktualisieren](./media/NuGet-2.8/webmatrix-update-all.png)

### <a name="overwrite-existing-files"></a>Vorhandene Dateien überschreiben

Installieren von Paketen, die Dateien enthalten, die auf der Website bereits vorhanden sind, verfügt über NuGet immer nur im Hintergrund (vorhandenen Dateien allein verlassen) Dateien ignoriert.  Dies kann auf den Eindruck führen, dass ein Paket installiert wurde oder wenn tatsächlich war nicht ordnungsgemäß aktualisiert.  NuGet fordert nun Dateien überschrieben werden sollen.

![Auflösung des Konflikts zwischen Datei](./media/NuGet-2.8/webmatrix-overwrite-file.png)
