---
title: Anmerkungen zu dieser Version von nuget 2.6.1 für webmatrix
description: Anmerkungen zu dieser Version von nuget 2.6.1 für webmatrix einschließlich bekannter Probleme, Fehlerbehebungen, hinzugefügter Features und dcrs.
author: JonDouglas
ms.author: jodou
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: de568829efd5060f3b02c3129ccfee2b27782821
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98780424"
---
# <a name="nuget-261-for-webmatrix-release-notes"></a>Anmerkungen zu dieser Version von nuget 2.6.1 für webmatrix

Anmerkungen zu dieser [Version von nuget 2,6](../release-notes/nuget-2.6.md)  |  [Anmerkungen zu dieser Version von nuget 2,7](../release-notes/nuget-2.7.md)

Das nuget-Team hat am 26. März 2014 eine aktualisierte nuget-Paket-Manager-Erweiterung für webmatrix veröffentlicht.  Dieses Update kann mithilfe der folgenden Schritte aus dem [webmatrix-Erweiterungs](https://blogs.iis.net/webmatrix/retiring-the-webmatrix-extensions-gallery) Katalog installiert werden:

1. Webmatrix 3 Öffnen
1. Klicken Sie im Menüband Start auf das Symbol Erweiterungen.
1. Registerkarte "Updates" auswählen
1. Klicken Sie, um den nuget-Paket-Manager zu 2.6.1
1. Schließen und Neustarten von webmatrix 3

## <a name="notable-changes"></a>Wichtige Änderungen

Dieses Erweiterungs Update bezieht sich auf zwei der größten Probleme, die Benutzern bei der Nutzung von nuget-Paketen in webmatrix ausgesetzt waren.  Der erste war ein Fehler in der nuget-Schema Version, und der zweite war ein Fehler, der zu 0-Byte-DLLs im `bin` Ordner führte.

### <a name="nuget-schema-version-error"></a>Fehler bei der nuget-Schema Version

Seit der Veröffentlichung von webmatrix 3 wurden neue Features in nuget eingeführt, die eine neue Schema Version für die nuget-Pakete erfordern.  Wenn Sie versuchen, ihre nuget-Pakete auf Ihrer Website zu verwalten, können diese neuen Pakete zu Fehlern führen, die in webmatrix angezeigt werden.

![Ein Fehler ist aufgetreten. Die Schema Version ist nicht kompatibel. Aktualisieren Sie nuget auf die neueste Version.](./media/NuGet-2.8/webmatrix-schema-version.png)

Diese neueste Version bietet Kompatibilität mit den neuesten nuget-Paketen, wodurch dieser Fehler nicht mehr auftritt. Neue Versionen von Paketen einschließlich Microsoft. Aspnet. Webseiten können jetzt in webmatrix installiert werden.  Einige dieser Pakete verwendeten nuget-Features, wie z. b. [xdt-Konfigurations Transformationen](../release-notes/nuget-2.6.md#xdt), die bisher in webmatrix nicht unterstützt wurden.

### <a name="zero-byte-dlls-in-bin-folder"></a>Zero-Byte DLLs im Ordner "bin"

Einige Benutzer haben gemeldet, dass die DLLs nach der Installation von nuget-Paketen in webmatrix, die DLLs enthalten, die in bin kopiert werden, `bin` als 0-Byte-Dateien im Ordner angezeigt werden.  Dadurch wird die Anwendung zur Laufzeit unterbrochen.

[Dieses Problem](https://nuget.codeplex.com/workitem/4060) wurde jetzt behoben.

## <a name="other-recent-improvements"></a>Weitere aktuelle Verbesserungen

Als der nuget-Paket-Manager 2,8 für Visual Studio freigegeben wurde, haben wir auch den nuget-Paket-Manager 2.5.0 für webmatrix veröffentlicht.  Obwohl dies in den Anmerkungen zu dieser [Version von nuget 2,8](../release-notes/nuget-2.8.md#webmatrix-nuget-client-updates)erwähnt wurde, haben wir die neuen Features, die von Update eingeführt wurden, nicht erwähnt.

### <a name="update-all"></a>Alle aktualisieren

Sie können jetzt alle Pakete Ihrer Website in einem Schritt aktualisieren!  Wenn Sie die nuget-Erweiterung in webmatrix öffnen, sehen Sie die Liste aller Pakete im Katalog, die installiert und die Updates, die verfügbar sind.  Zuvor musste jedes Paket einzeln aktualisiert werden, aber jetzt gibt es eine nützliche Schaltfläche "Alle aktualisieren", die auf der Registerkarte "Updates" angezeigt wird.

![Klicken Sie auf alle aktualisieren, um alle Pakete mit verfügbaren Updates zu aktualisieren](./media/NuGet-2.8/webmatrix-update-all.png)

### <a name="overwrite-existing-files"></a>Vorhandene Dateien überschreiben

Wenn Sie Pakete installieren, die bereits auf der Website vorhandene Dateien enthalten, ignoriert nuget diese Dateien immer im Hintergrund (wobei die vorhandenen Dateien unverändert geblieben sind).  Dies könnte dazu führen, dass ein Paket ordnungsgemäß installiert oder aktualisiert wurde, wenn dies nicht der Fall war.  Nuget wird jetzt aufgefordert, Dateien zu überschreiben.

![Auflösung von Dateikonflikten](./media/NuGet-2.8/webmatrix-overwrite-file.png)
