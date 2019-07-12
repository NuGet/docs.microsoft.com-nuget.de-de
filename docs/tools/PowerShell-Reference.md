---
title: NuGet-PowerShell-Referenz
description: Die vollständige Referenz zu PowerShell-Befehle, die in der NuGet-Paket-Manager-Konsole in Visual Studio verfügbar.
author: karann-msft
ms.author: karann
ms.date: 10/02/2017
ms.topic: reference
ms.openlocfilehash: 425ba736eba4609ebd6b5185ae3f1f976ab07a67
ms.sourcegitcommit: 0dea3b153ef823230a9d5f38351b7cef057cb299
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 07/12/2019
ms.locfileid: "67842561"
---
# <a name="powershell-reference"></a>PowerShell-Referenz

Der Paket-Manager-Konsole enthält eine PowerShell-Schnittstelle in Visual Studio unter Windows für die Interaktion mit NuGet über die spezifischen Befehle aufgeführt. (Die Konsole ist nicht in Visual Studio für Mac derzeit verfügbar) Eine Anleitung zur Verwendung der Konsole, finden Sie unter [installieren und Verwalten von Paketen mithilfe der Paket-Manager-Konsole](../tools/package-manager-console.md) Thema.

> [!Tip]
> Alle PowerShell-Befehle beziehen sich nur auf paketverbrauch. Keine PowerShell-Befehle beziehen sich auf erstellen und veröffentlichen Pakete mit Ausnahme aus, in dem Umfang, ein Paket kann auch ein Consumer von anderen Paketen sein.

> [!Important]
> Die hier aufgeführten Befehle beziehen sich auf die Paket-Manager-Konsole in Visual Studio und unterscheiden sich von der [Paketverwaltung modulbefehle](/powershell/module/packagemanagement/?view=powershell-6) , die in einer allgemeinen PowerShell-Umgebung verfügbar sind. Insbesondere jeder Umgebung sind Befehle, die nicht in der anderen verfügbar sind, und Befehle, mit dem gleichen Namen unterscheiden sich auch in ihren bestimmten Argumenten. Wenn Sie die Paketverwaltungskonsole in Visual Studio verwenden zu können, gelten die Befehle und Argumente, die in diesem Thema dokumentiert.

| Häufig verwendete Befehle | Beschreibung | NuGet-Version |
| --- | --- | --- |
| [Install-Package](ps-ref-install-package.md) | Installiert ein Paket und seine Abhängigkeiten in das Projekt an. | All |
| [Update-Package](ps-ref-update-package.md) | Aktualisiert ein Paket und seine Abhängigkeiten oder alle Pakete in einem Projekt. | All |
| [Find-Package](ps-ref-find-package.md) | Sucht eine Paketquelle, die mit einer Paket-ID oder Schlüsselwörter. | 3.0+ |
| [Get-Package](ps-ref-get-package.md) | Ruft die Liste der Pakete, die im lokalen Repository installiert, oder aus der Paketquelle verfügbaren Pakete aufgeführt. | All |

| Sekundäre Befehle | Beschreibung | NuGet-Version |
| --- | --- | --- |
| [Add-BindingRedirect](ps-ref-add-bindingredirect.md) | Untersucht alle Assemblys im Ausgabepfad für ein Projekt und fügt Sie bindungsumleitungen zu den `app.config` oder `web.config` bei Bedarf. | All |
| [Get-Project](ps-ref-get-project.md) | Zeigt Informationen zu den Standardwert oder die angegebene Projekt. | 3.0+ |
| [Open-PackagePage](ps-ref-open-packagepage.md) | Startet den Standardbrowser mit dem Projekt, Lizenz oder Missbrauch Berichts-URL für das angegebene Paket. | Veraltetes Feature in 3.0 und höher |
| [Register-TabExpansion](ps-ref-register-tabexpansion.md) | Registriert eine Erweiterung der Registerkarte für die Parameter eines Befehls, sodass Sie benutzerdefinierte Erweiterungen für häufig verwendete Parameterwerte zu erstellen. | All |
| [Sync-Package](ps-ref-sync-package.md) | Die Version des Pakets aus einer installiert Get angegebene Projekt und synchronisiert die Version für den Rest der Projekte in der Projektmappe. | 3.0+ |
| [Uninstall-Package](ps-ref-uninstall-package.md) | Entfernt ein Paket aus einem Projekt, und seine Abhängigkeiten optional zu entfernen. | All |

Führen Sie für vollständige, ausführliche Hilfe zu diesen Befehlen in der Konsole den folgenden nur mit den Namen des jeweiligen Befehls:

```ps
Get-Help <command> -full
```

Alle Befehle der Paket-Manager-Konsole unterstützt die folgenden [allgemeine PowerShell-Parameter](http://go.microsoft.com/fwlink/?LinkID=113216):

- Debug
- ErrorAction
- ErrorVariable
- OutBuffer
- OutVariable
- PipelineVariable
- Ausführlich
- WarningAction
- WarningVariable

Weitere Informationen finden Sie unter [About_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216) in der PowerShell-Dokumentation.
