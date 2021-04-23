---
title: NuGet PowerShell-Referenz
description: Die vollständige Referenz zu PowerShell-Befehlen, die in der NuGet-Paket-Manager-Konsole in Visual Studio.
author: JonDouglas
ms.author: jodou
ms.date: 10/02/2017
ms.topic: reference
ms.openlocfilehash: 7bc0395a98e75fe006e048b91d84cb5c17220161
ms.sourcegitcommit: 40c039ace0330dd9e68922882017f9878f4283d1
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 04/22/2021
ms.locfileid: "107901888"
---
# <a name="powershell-reference"></a>PowerShell-Referenz

Die Paket-Manager-Konsole stellt eine PowerShell-Schnittstelle in Visual Studio unter Windows bereit, um über die unten aufgeführten spezifischen Befehle mit NuGet zu interagieren. (Die Konsole ist derzeit nicht in der Visual Studio für Mac.) Eine Anleitung zur Verwendung der -Konsole finden Sie im Thema Installieren und Verwalten von Paketen [mit Paket-Manager Console.](../consume-packages/install-use-packages-powershell.md)

> [!Tip]
> Alle PowerShell-Befehle beziehen sich nur auf den Paketverbrauch. PowerShell-Befehle beziehen sich nicht auf das Erstellen und Veröffentlichen von Paketen, außer in dem Umfang, in dem ein Paket auch ein Consumer anderer Pakete sein kann.

> [!Important]
> Die hier aufgeführten Befehle sind spezifisch für die Paket-Manager-Konsole in Visual Studio und unterscheiden sich von den [Befehlen für das Paket-Manager-Modul](/powershell/module/packagemanagement), die in einer allgemeinen PowerShell-Umgebung zur Verfügung stehen. Genau genommen verfügt jede Umgebung über Befehle, die in der jeweils anderen nicht verfügbar sind. Außerdem können sich Befehle mit identischem Namen in Bezug auf ihre spezifischen Argumente unterscheiden. Wenn die Paket-Manager-Konsole in Visual Studio verwendet wird, gelten nur die in diesem Thema erläuterten Befehle und Argumente.

| Allgemeine Befehle | Beschreibung | NuGet-Version |
| --- | --- | --- |
| [Install-Package](ps-reference/ps-ref-install-package.md) | Installiert ein Paket und seine Abhängigkeiten im Projekt. | All |
| [Update-Package](ps-reference/ps-ref-update-package.md) | Aktualisiert ein Paket und seine Abhängigkeiten oder alle Pakete in einem Projekt. | All |
| [Find-Package](ps-reference/ps-ref-find-package.md) | Durchsucht eine Paketquelle mithilfe einer Paket-ID oder schlüsselwörtern. | 3.0+ |
| [Get-Package](ps-reference/ps-ref-get-package.md) | Ruft die Liste der im lokalen Repository installierten Pakete ab oder listet pakete auf, die aus einer Paketquelle verfügbar sind. | All |

| Sekundäre Befehle | Beschreibung | NuGet-Version |
| --- | --- | --- |
| [Add-BindingRedirect](ps-reference/ps-ref-add-bindingredirect.md) | Überprüft alle Assemblys innerhalb des Ausgabepfads für ein Projekt und fügt bei Bedarf Bindungsumleitungen zu `app.config` oder `web.config` hinzu. | All |
| [Get-Project](ps-reference/ps-ref-get-project.md) | Zeigt Informationen über das Standardprojekt oder das angegebene Projekt an. | 3.0+ |
| [Open-PackagePage](ps-reference/ps-ref-open-packagepage.md) | Startet den Standardbrowser mit der Projekt-, Lizenz- oder Berichts-Missbrauchs-URL für das angegebene Paket. | Veraltet in 3.0+ |
| [Register-TabExpansion](ps-reference/ps-ref-register-tabexpansion.md) | Registriert eine Registerkartenerweiterung für die Parameter eines Befehls, sodass Sie benutzerdefinierte Erweiterungen für häufig verwendete Parameterwerte erstellen können. | All |
| [Sync-Package](ps-reference/ps-ref-sync-package.md) | Sie erhalten die Version des installierten Pakets aus dem angegebenen Projekt und synchronisieren die Version mit den restlichen Projekten in der Projektmappe. | 3.0+ |
| [Uninstall-Package](ps-reference/ps-ref-uninstall-package.md) | Entfernt ein Paket aus einem Projekt und entfernt optional seine Abhängigkeiten. | All |

Um eine vollständige, ausführliche Hilfe zu einem dieser Befehle in der Konsole zu erhalten, führen Sie einfach den folgenden Befehlsnamen mit dem angegebenen Befehlsnamen aus:

```ps
Get-Help <command> -full
```

Alle Paket-Manager-Konsolenbefehle unterstützen die folgenden [allgemeinen PowerShell-Parameter:](/powershell/module/microsoft.powershell.core/about/about_commonparameters)

- Debuggen
- ErrorAction
- ErrorVariable
- OutBuffer
- OutVariable
- PipelineVariable
- Ausführlich
- WarningAction
- WarningVariable

Ausführliche Informationen finden Sie in [about_CommonParameters](/powershell/module/microsoft.powershell.core/about/about_commonparameters) in der PowerShell-Dokumentation.