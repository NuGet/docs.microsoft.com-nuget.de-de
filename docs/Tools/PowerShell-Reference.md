---
title: NuGet-PowerShell-Referenz | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 10/2/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: cd08b869-44c6-480e-90f7-494a6d08e6d0
description: "Die vollständige Referenz zu PowerShell-Befehle in der NuGet-Paket-Manager-Konsole in Visual Studio verfügbar."
keywords: NuGet-Paket-Manager-Konsole NuGet Powershell-Befehle, NuGet Powershell-Referenz
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: c0da5c88447784fdd49d824bbd03b11f73c22ebc
ms.sourcegitcommit: d0ba99bfe019b779b75731bafdca8a37e35ef0d9
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 12/14/2017
---
# <a name="powershell-reference"></a>PowerShell-Referenz

Der Paket-Manager-Konsole bietet eine PowerShell-Schnittstelle innerhalb von Visual Studio unter Windows für die Interaktion mit NuGet, über die spezifischen Befehle unten aufgeführt. (Die Konsole ist nicht in Visual Studio für Mac gegenwärtig verfügbar) Eine Anleitung zur Verwendung der Konsole, finden Sie unter der [Package Manager Console](../tools/package-manager-console.md) Thema.

> [!Tip]
> Alle PowerShell-Befehle beziehen sich nur auf Paket Verbrauch. Keine PowerShell-Befehle beziehen sich auf erstellen und Veröffentlichen von Paketen, außer, wenn ein Paket kann auch ein Consumer von anderen Paketen sein.

> [!Important]
> Die hier aufgeführten Befehle sind spezifisch für die Paket-Manager-Konsole in Visual Studio und unterscheiden sich von der [Packagemanagement-Modul Befehle](https://msdn.microsoft.com/powershell/reference/6/packagemanagement/packagemanagement) , die in eine allgemeine PowerShell-Umgebung verfügbar sind. Insbesondere wird jede Umgebung verfügt über Befehle, die in anderen nicht verfügbar sind, und Befehle mit dem gleichen Namen unterscheidet sich auch in ihren bestimmten Argumenten. Wenn Sie die Paket-Verwaltungskonsole in Visual Studio verwenden, gelten die Befehle und Argumente, die in diesem Thema vorhanden dokumentiert.

| Häufig verwendete Befehle | Beschreibung | NuGet-Version |
| --- | --- | --- |
| [Install-Package](ps-ref-install-package.md) | Installiert ein Paket und seine Abhängigkeiten im Projekt. | Alle |
| [Update-Paket](ps-ref-update-package.md) | Aktualisiert ein Paket und seine Abhängigkeiten oder alle Pakete in einem Projekt. | Alle |
| [Find-Package](ps-ref-find-package.md) | Durchsucht eine Paketquelle eine Paket-ID oder Schlüsselwörter verwenden. | 3.0+ |
| [Get-Package](ps-ref-get-package.md) | Ruft die Liste der Pakete, die im lokalen Repository installiert oder von einem Paketquelle verfügbaren Pakete aufgeführt. | Alle |

| Sekundäre Befehle | Beschreibung | NuGet-Version |
| --- | --- | --- |
| [BindingRedirect-hinzufügen](ps-ref-add-bindingredirect.md) | Untersucht alle Assemblys im Ausgabepfad auf ein Projekt und fügt Sie bindungsumleitungen zu den `app.config` oder `web.config` bei Bedarf. | Alle |
| [Get-Projekt](ps-ref-get-project.md) | Zeigt Informationen zu den Standardwert oder die angegebene Projekt. | 3.0+ |
| [Open-PackagePage](ps-ref-open-packagepage.md) | Startet den Standardbrowser mit dem Projekt, Lizenzen oder Missbrauch Berichts-URL für das angegebene Paket. | In 3.0 veraltet |
| [Register-"tabexpansion"](ps-ref-register-tabexpansion.md) | Registriert eine Tab-Taste für die Parameter eines Befehls, sodass Sie benutzerdefinierte Erweiterungen für häufig verwendete Parameterwerte zu erstellen. | Alle |
| [Sync-Pakets](ps-ref-sync-package.md) | Abrufen der Version des Pakets aus einer installiert Projekt angegeben und synchronisiert die Version mit den restlichen Projekten in der Projektmappe. | 3.0+ |
| [Uninstall-Package](ps-ref-uninstall-package.md) | Entfernt ein Paket aus einem Projekt, und optional die abhängigen Elemente entfernen. | Alle |

Vollständige, ausführliche Hilfe zu allen diesen Befehlen in der Konsole führen Sie den folgenden nur mit den betreffenden Befehlsnamen:

```ps
Get-Help <command> -full
```

Alle Package Manager Console Befehle unterstützen die folgenden [allgemeine PowerShell-Parameter](http://go.microsoft.com/fwlink/?LinkID=113216):

- Debuggen
- ErrorAction
- ErrorVariable
- OutBuffer
- OutVariable
- Mit "pipelinevariable"
- Ausführlich
- WarningAction
- WarningVariable

Weitere Informationen finden Sie in [About_CommonParameters](http://go.microsoft.com/fwlink/?LinkID=113216) in der PowerShell-Dokumentation.
