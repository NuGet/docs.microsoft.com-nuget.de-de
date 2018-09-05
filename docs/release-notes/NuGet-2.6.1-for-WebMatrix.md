---
title: NuGet 2.6.1 für WebMatrix-Versionshinweise
description: Anmerkungen zu NuGet 2.6.1 für WebMatrix, einschließlich der bekannten Probleme, Fehlerkorrekturen, hinzugefügter Features und DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 10d80a921cbc34b537f91644da97efc44530fa75
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43550316"
---
# <a name="nuget-261-for-webmatrix-release-notes"></a>NuGet 2.6.1 für WebMatrix-Versionshinweise

[Anmerkungen zu NuGet 2.6](../release-notes/nuget-2.6.md) | [Anmerkungen zu NuGet 2.7](../release-notes/nuget-2.7.md)

Das NuGet-Team hat eine aktualisierte NuGet-Paket-Manager-Erweiterung für WebMatrix 26 März 2014 veröffentlicht.  Dieses Update installiert werden kann, aus der [WebMatrix-Erweiterungskatalog](https://blogs.iis.net/webmatrix/retiring-the-webmatrix-extensions-gallery) verwenden die folgenden Schritte aus:

1. Öffnen Sie WebMatrix 3
1. Klicken Sie auf das Symbol "Erweiterungen" im Menüband "Start"
1. Wählen Sie die Registerkarte "Updates"
1. Klicken Sie auf, um NuGet-Paket-Manager auf 2.6.1 zu aktualisieren.
1. Schließen Sie und starten Sie WebMatrix 3

## <a name="notable-changes"></a>Wichtige Änderungen

Diese Erweiterung Update behandelt zwei der größten Probleme Benutzer haben verwendeten NuGet-Pakete in WebMatrix konfrontiert.  Die erste war ein NuGet-Schemafehler Version und das zweite ein Fehler auf 0 (null)-Byte-DLLs in führenden der `bin` Ordner.

### <a name="nuget-schema-version-error"></a>Fehler beim Version des NuGet-Schemas

Da WebMatrix 3 veröffentlicht wurde, wurden neue Features in NuGet, die eine neue Schemaversion für die NuGet-Pakete erfordern eingeführt.  Beim Versuch, Ihr NuGet-Pakete in Ihre Website zu verwalten, können diese neue Pakete zu Fehlern führen, die Sie in WebMatrix zu sehen.

![Es ist ein Fehler aufgetreten. Die Schemaversion ist nicht kompatibel. Führen Sie ein upgrade NuGet, auf die neueste Version zu erhalten.](./media/NuGet-2.8/webmatrix-schema-version.png)

Dieses neueste Release bietet Kompatibilität mit den neuesten NuGet-Pakete, die verhindert, dass dieser Fehler auftritt. Neue Versionen der Pakete einschließlich Microsoft.AspNet.WebPages können jetzt in WebMatrix installiert werden.  Einige dieser Pakete wurden mithilfe von NuGet-Features wie [XDT Konfigurationstransformationen](../release-notes/nuget-2.6.md#xdt), dies war nicht in WebMatrix unterstützt, bis jetzt.

### <a name="zero-byte-dlls-in-bin-folder"></a>0-Byte-DLLs im Ordner "bin" "

Einige Benutzer haben gemeldet, dass nach dem Installieren von NuGet Pakete Sie in WebMatrix, die DLLs enthalten, die kopiert werden, in den Papierkorb, die die DLLs zeigen die `bin` Ordner Dateien mit 0 Byte.  Dies unterbricht die Anwendung zur Laufzeit.

[Dieses Problem](https://nuget.codeplex.com/workitem/4060) hat sich geändert.

## <a name="other-recent-improvements"></a>Weitere Verbesserungen

Als NuGet-Paket-Manager 2.8 für Visual Studio veröffentlicht wurde, veröffentlicht haben wir auch NuGet Package Manager 2.5.0 für WebMatrix.  Während dies im erwähnt wurde die [NuGet 2.8 Release Notes](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates), wir jedoch nicht erwähnt die spezifischen neue Funktionen, die Updates eingeführt wurden.

### <a name="update-all"></a>Alle aktualisieren

Sie können alle Pakete von der Website in einem Schritt jetzt aktualisieren!  Wenn Sie die NuGet-Erweiterung in WebMatrix öffnen, sehen Sie die Liste aller Pakete auf den Katalog, die installiert und diejenigen mit verfügbaren Updates.  Früher jedes Paket einzeln aktualisiert werden müsste, aber jetzt befindet sich eine nützliche "Alle aktualisieren"-Schaltfläche, die auf der Registerkarte "Updates" wird angezeigt.

![Klicken Sie auf "Alle aktualisieren", um alle Pakete mit verfügbaren Updates zu aktualisieren.](./media/NuGet-2.8/webmatrix-update-all.png)

### <a name="overwrite-existing-files"></a>Vorhandene Dateien überschreiben

Beim Installieren von Paketen, die Dateien enthalten, die auf der Website bereits vorhanden sind, hat NuGet immer nur diese Dateien (vorhandenen Dateien allein verlassen) ignoriert.  Dies kann auf den Eindruck führen, dass ein Paket installiert wurde oder wenn in der Tat es war nicht korrekt aktualisiert.  NuGet fordert nun Dateien überschrieben werden sollen.

![Lösung von Konflikten](./media/NuGet-2.8/webmatrix-overwrite-file.png)
