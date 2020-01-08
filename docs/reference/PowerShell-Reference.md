---
title: Referenz zu nuget-PowerShell
description: Der umfassende Verweis auf PowerShell-Befehle, die in der nuget-Paket-Manager-Konsole in Visual Studio verfügbar sind.
author: karann-msft
ms.author: karann
ms.date: 10/02/2017
ms.topic: reference
ms.openlocfilehash: 2a82b1977265a8f8a15247759bc3de80a5efe228
ms.sourcegitcommit: 26a8eae00af2d4be581171e7a73009f94534c336
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/25/2019
ms.locfileid: "75385342"
---
# <a name="powershell-reference"></a>PowerShell-Referenz

Die Paket-Manager-Konsole bietet eine PowerShell-Schnittstelle in Visual Studio unter Windows für die Interaktion mit nuget über die unten aufgeführten spezifischen Befehle. (Die Konsole ist zurzeit nicht in Visual Studio für Mac verfügbar.) Eine Anleitung zur Verwendung der-Konsole finden Sie im Thema [Installieren und Verwalten von Paketen mit der Paket-Manager-Konsole](../consume-packages/install-use-packages-powershell.md) .

> [!Tip]
> Alle PowerShell-Befehle beziehen sich nur auf den Paket Verbrauch. Keine PowerShell-Befehle beziehen sich auf das Erstellen und Veröffentlichen von Paketen, außer in dem Umfang, in dem ein Paket auch Consumer anderer Pakete sein kann.

> [!Important]
> Die hier aufgeführten Befehle sind spezifisch für die Paket-Manager-Konsole in Visual Studio und unterscheiden sich von den [Paketverwaltung Module-Befehlen](/powershell/module/packagemanagement/?view=powershell-6) , die in einer allgemeinen PowerShell-Umgebung verfügbar sind. Insbesondere weist jede Umgebung Befehle auf, die in der anderen nicht verfügbar sind, und Befehle mit demselben Namen können sich auch in ihren spezifischen Argumenten unterscheiden. Wenn Sie die Paketverwaltung-Konsole in Visual Studio verwenden, gelten die in diesem Thema dokumentierten Befehle und Argumente.

| Allgemeine Befehle | Beschreibung | NuGet-Version |
| --- | --- | --- |
| [Install-Package](ps-reference/ps-ref-install-package.md) | Installiert ein Paket und seine Abhängigkeiten im Projekt. | Alle |
| [Update-Package](ps-reference/ps-ref-update-package.md) | Aktualisiert ein Paket und seine Abhängigkeiten oder alle Pakete in einem Projekt. | Alle |
| [Find-Package](ps-reference/ps-ref-find-package.md) | Durchsucht eine Paketquelle mithilfe einer Paket-ID oder eines Schlüssel Worts. | 3.0+ |
| [Get-Package](ps-reference/ps-ref-get-package.md) | Ruft die Liste der im lokalen Repository installierten Pakete ab oder listet die Pakete auf, die in einer Paketquelle verfügbar sind. | Alle |

| Sekundäre Befehle | Beschreibung | NuGet-Version |
| --- | --- | --- |
| [Add-BindingRedirect](ps-reference/ps-ref-add-bindingredirect.md) | Untersucht alle Assemblys im Ausgabepfad für ein Projekt und fügt bei Bedarf Bindungs Umleitungen an den `app.config` oder `web.config` hinzu. | Alle |
| [Get-Project](ps-reference/ps-ref-get-project.md) | Zeigt Informationen zum Standard-oder angegebenen Projekt an. | 3.0+ |
| [Open-PackagePage](ps-reference/ps-ref-open-packagepage.md) | Hiermit wird der Standardbrowser mit der URL für das Projekt, die Lizenz oder den Berichts Missbrauch für das angegebene Paket gestartet. | Veraltet in 3.0 und höher |
| [Register-TabExpansion](ps-reference/ps-ref-register-tabexpansion.md) | Registriert eine Registerkarten Erweiterung für die Parameter eines Befehls, sodass Sie angepasste Erweiterungen für häufig verwendete Parameterwerte erstellen können. | Alle |
| [Sync-Package](ps-reference/ps-ref-sync-package.md) | Die Version des installierten Pakets aus dem angegebenen Projekt erhalten und die Version mit den restlichen Projekten in der Projekt Mappe synchronisieren. | 3.0+ |
| [Uninstall-Package](ps-reference/ps-ref-uninstall-package.md) | Entfernt ein Paket aus einem Projekt und entfernt optional seine Abhängigkeiten. | Alle |

Um eine ausführliche Hilfe zu diesen Befehlen in der-Konsole zu erhalten, führen Sie einfach den folgenden Befehl mit dem fraglichen Befehlsnamen aus:

```ps
Get-Help <command> -full
```

Alle Befehle der Paket-Manager-Konsole unterstützen die folgenden [allgemeinen PowerShell-Parameter](https://go.microsoft.com/fwlink/?LinkID=113216):

- Debug
- ErrorAction
- ErrorVariable
- OutBuffer
- OutVariable
- PipelineVariable
- Ausführlich
- WarningAction
- WarningVariable

Weitere Informationen finden Sie in der Dokumentation zu [about_CommonParameters](https://go.microsoft.com/fwlink/?LinkID=113216) in der PowerShell-Dokumentation.
