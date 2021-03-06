---
title: Erneutes Installieren und Aktualisieren von NuGet-Paketen
description: Hier finden Sie Informationen dazu, wann es nötig ist, Pakete neu zu installieren und zu aktualisieren (z.B. bei fehlerhaften Paketverweisen in Visual Studio).
author: JonDouglas
ms.author: jodou
ms.date: 12/07/2017
ms.topic: conceptual
ms.openlocfilehash: 588d546352e5733ba8198061beb8006a79ecedac
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98774971"
---
# <a name="how-to-reinstall-and-update-packages"></a>Neuinstallieren und Aktualisieren von Paketen

Es gibt einige Situationen, die nachfolgend unter [Wann ein Paket neu installiert wird](#when-to-reinstall-a-package) beschrieben werden, in denen Verweise auf ein Paket innerhalb eines Visual Studio-Projekts fehlerhaft werden können. In diesen Fällen werden diese Verweise durch das Löschen und die Neuinstallation der gleichen Paketversion ordnungsgemäß wiederhergestellt. Ein Paket zu aktualisieren bedeutet einfach, eine aktualisierte Version zu installieren. So lässt sich ein Paket häufig ordnungsgemäß wiederherstellen.

In Visual Studio bietet die Paket-Manager-Konsole zahlreiche flexible Optionen für die Aktualisierung und erneute Installation von Paketen.

Das Aktualisieren und die Neuinstallation von Paketen erfolgt wie im Folgenden dargestellt:

| Methode | Aktualisieren | Neuinstallation |
| --- | --- | --- |
| Paket-Manager-Konsole (beschrieben unter [Verwenden des Updatepakets](#using-update-package)) | `Update-Package`-Befehl | `Update-Package -reinstall`-Befehl |
| Benutzeroberfläche des Paket-Managers | Wählen Sie auf der Registerkarte **Updates** mindestens ein Paket aus, und klicken Sie auf **Update** (Aktualisieren). | Wählen Sie auf der Registerkarte **Installiert** ein Paket aus, dokumentieren Sie dessen Namen, und klicken Sie dann auf **Deinstallieren**. Wechseln Sie zur Registerkarte **Durchsuchen**, suchen Sie nach dem Paketnamen, wählen Sie ihn aus, und klicken Sie dann auf **Installieren**. |
| nuget.exe-CLI | `nuget update`-Befehl | Löschen Sie für alle Pakete den Paketordner, und führen Sie dann `nuget install` aus. Löschen Sie für ein einzelnes Paket den Paketordner, und verwenden Sie `nuget install <id>`, um den gleichen Ordner neu zu installieren. |

> [!NOTE]
> Für die dotnet-CLI ist das entsprechende Verfahren nicht erforderlich. In einem ähnlichen Szenario können Sie [Pakete mit der dotnet-CLI wiederherstellen](package-restore.md#restore-using-the-dotnet-cli).

Inhalt dieses Artikels:

- [Wann ein Paket neu installiert werden sollte](#when-to-reinstall-a-package)
- [Einschränken von Updateversionen](#constraining-upgrade-versions)

## <a name="when-to-reinstall-a-package"></a>Wann ein Paket neu installiert werden sollte

1. **Fehlerhafte Verweise nach der Paketwiederherstellung:** Wenn Sie ein Projekt geöffnet und NuGet-Pakete wiederhergestellt haben, jedoch noch immer fehlerhafte Verweise angezeigt werden, versuchen Sie, jedes einzelne Paket wiederherzustellen.
1. **Projekt ist aufgrund gelöschter Dateien fehlerhaft:** NuGet hält Sie nicht davon ab, Elemente zu löschen, die aus Paketen hinzugefügt wurden. Es ist also einfach, versehentlich die aus einem Paket installierten Inhalte zu verändern und Ihr Projekt so zu zerstören. Installieren Sie die betroffenen Pakete erneut, um das Projekt wiederherzustellen.
1. **Das Paketupdate hat zu einem Fehler im Projekt geführt:** Wenn ein Update für ein Paket einen Fehler in einem Projekt verursacht, wurde dieser in der Regel von einem Abhängigkeitspaket ausgelöst, das möglicherweise auch aktualisiert wurde. Installieren Sie das spezifische Paket neu, um den Zustand der Abhängigkeit wiederherzustellen.
1. **Erneutes Zuweisen oder Upgrade eines Projekts:** Dies kann hilfreich sein, wenn ein Projekt erneut zugewiesen oder ein Upgrade für dieses durchgeführt wurde, und wenn das Paket eine Neuinstallation aufgrund der Änderung im Zielframework erfordert. NuGet zeigt in solchen Fällen sofort nach der Projektneuzuweisung einen Buildfehler an, und in nachfolgenden Buildwarnungen wird Ihnen mitgeteilt, dass das Paket möglicherweise neu installiert werden muss. Für das Projektupgrade zeigt NuGet einen Fehler im Projektupgradeprotokoll an.
1. **Neuinstallation eines Pakets während der Entwicklung:** Paketautoren müssen oft dieselbe Version des Pakets neu installieren, das Sie entwickeln, um das Verhalten zu testen. Der `Install-Package`-Befehl bietet keine Option zum Erzwingen einer Neuinstallation an. Verwenden Sie deshalb stattdessen `Update-Package -reinstall`.

## <a name="constraining-upgrade-versions"></a>Einschränken von Updateversionen

Standardmäßig wird durch die Neuinstallation oder das Update eines Pakets *immer* die neueste verfügbare Version aus der Paketquelle installiert.

In Projekten, die das `packages.config`-Verwaltungsformat verwenden, können Sie jedoch den Versionsbereich explizit einschränken. Wenn Sie z.B. wissen, dass Ihre Anwendung nur mit Version 1.x eines Pakets funktioniert, jedoch nicht mit 2.0 oder höher (vielleicht aufgrund einer größeren Änderung in der Paket-API), sollten Sie die Upgrades auf 1.x-Versionen beschränken. Dadurch werden versehentliche Updates verhindert, die die Anwendung zerstören würden.

Um eine Einschränkung festzulegen, öffnen Sie `packages.config` in einem Text-Editor, suchen Sie nach der betreffenden Abhängigkeit, und fügen Sie das Attribut `allowedVersions` mit einem Versionsbereich hinzu. Wenn Sie z.B. Updates auf Version 1.x beschränken möchten, legen Sie `allowedVersions` auf `[1,2)` fest:

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
    <package id="ExamplePackage" version="1.1.0" allowedVersions="[1,2)" />

    <!-- ... -->
</packages>
```

Verwenden Sie in jedem Fall die unter [Paketversionsverwaltung](../concepts/package-versioning.md#version-ranges) beschriebene Notation.

## <a name="using-update-package"></a>Verwenden eines Updatepakets

Unter Berücksichtigung der nachfolgend beschriebenen [Überlegungen](#considerations) können Sie einfach beliebige Pakete neu installieren, indem Sie den [Befehl Update-Package](../reference/ps-reference/ps-ref-update-package.md) in der Paket-Manager-Konsole von Visual Studio verwenden (**Extras** > **NuGet-Paket-Manager** > **Paket-Manager-Konsole**).

```ps
Update-Package -Id <package_name> –reinstall
```

Die Verwendung dieses Befehls ist viel einfacher als das Entfernen eines Pakets und der anschließende Versuch, dasselbe Paket im NuGet-Katalog mit der gleichen Version zu finden. Beachten Sie, dass der `-Id`-Schalter optional ist.

Wenn Sie den gleichen Befehl ohne `-reinstall` verwenden, wird ein Paket auf die neuere Version aktualisiert (falls zutreffend). Der Befehl gibt einen Fehler aus, wenn das betreffende Paket nicht bereits in einem Projekt installiert ist. Das bedeutet, dass `Update-Package` Pakete nicht direkt installiert.

```ps
Update-Package <package_name>
```

Standardmäßig wirkt sich `Update-Package` auf alle Projekte in einer Projektmappe aus. Verwenden Sie den Parameter `-ProjectName` mithilfe des Namens des Projekts, wie es im Projektmappen-Explorer dargestellt wird, um die Aktion auf ein bestimmtes Projekt zu beschränken:

```ps
# Reinstall the package in just MyProject
Update-Package <package_name> -ProjectName MyProject -reinstall
```

Um alle Pakete in einem Projekt zu *aktualisieren* (oder mithilfe von `-reinstall` neu zu installieren), verwenden Sie `-ProjectName` ohne Angabe eines bestimmten Pakets:

```ps
Update-Package -ProjectName MyProject
```

Verwenden Sie `Update-Package` nur ohne andere Argumente oder Parameter, um alle Pakete in einer Projektmappe zu aktualisieren. Verwenden Sie dieses Formular mit Bedacht, da es lange dauern kann, alle Updates auszuführen:

```ps
# Updates all packages in all projects in the solution
Update-Package 
```

Mit einem Update von Paketen in einem Projekt oder einer Projektmappe mithilfe von [PackageReference](../Consume-Packages/Package-References-in-Project-Files.md), wird immer ein Update auf die neueste Version des Pakets ausgeführt (Paketvorabversionen sind davon ausgeschlossen). Projekte, die `packages.config` verwenden, können – sofern gewünscht – die Updateversionen einschränken, so wie unten unter [Einschränken von Updateversionen](#constraining-upgrade-versions) beschrieben.

Ausführliche Informationen zu dem Befehl finden Sie unter [Updatepaket](../reference/ps-reference/ps-ref-update-package.md).

### <a name="considerations"></a>Überlegungen

Folgendes kann bei der Neuinstallation eines Pakets beeinträchtigt werden:

1. **Neuinstallation von Paketen gemäß der Neuzuweisung des Projektzielframeworks**
    - In einem einfachen Fall funktioniert die Neuinstallation eines Pakets mithilfe von `Update-Package –reinstall <package_name>`. Ein Paket, das für ein altes Zielframework installiert wurde, wird deinstalliert, und das gleiche Paket wird für das aktuelle Zielframework des Projekts installiert.
    - In einigen Fällen ist womöglich ein Paket vorhanden, das das neue Zielframework nicht unterstützt.
        - Wenn ein Paket portable Klassenbibliotheken (Portable Class Libraries, PCLs) unterstützt, und das Projekt einer Kombination aus Plattformen zugewiesen wird, die nicht länger vom Paket unterstützt werden, fehlen die Paketverweise nach der Neuinstallation.
        - Dadurch können Probleme für Pakete auftreten, die Sie direkt verwenden oder für Pakete, die als Abhängigkeiten installiert wurden. Es ist möglich, dass das von Ihnen direkt verwendete Paket das neue Zielframework unterstützt, obwohl dessen Abhängigkeit dies nicht tut.
        - Wenn Sie Pakete nach der Neuzuweisung Ihrer Anwendungsergebnisse in Build- oder Runtimefehlern neu installieren, sollten Sie Ihr Zielframework wiederherstellen oder nach alternativen Paketen suchen, die Ihr neues Zielframework ordnungsgemäß unterstützen.

1. **Das Attribut „requireReinstallation“ wurde in „packages.config“ nach der Projektneuzuweisung oder dem Projektupgrade hinzugefügt**
    - Wenn NuGet erkennt, dass Pakete von der Neuzuweisung oder einem Upgrade eines Projekts betroffen waren, wird allen betroffenen Paketverweisen ein `requireReinstallation="true"`-Attribut in `packages.config` hinzugefügt. Aus diesem Grund löst jeder nachfolgende Build in Visual Studio Buildwarnungen für diese Pakete aus, damit Sie daran erinnert werden, diese neu zu installieren.

1. **Neuinstallation von Paketen mit Abhängigkeiten**
    - `Update-Package –reinstall` installiert zwar die gleiche Version des ursprünglichen Pakets, es wird jedoch die neueste Version der Abhängigkeiten installiert, wenn keine bestimmten Versionseinschränkungen bereitgestellt werden. Dadurch können Sie nur die Abhängigkeiten aktualisieren, die zum Beheben eines Fehlers benötigt werden. Wenn dies jedoch eine Abhängigkeit auf eine ältere Version zurücksetzt, können Sie sie mit `Update-Package <dependency_name>` neu installieren, ohne das Abhängigkeitspaket zu beeinflussen.
    - `Update-Package –reinstall <packageName> -ignoreDependencies` installiert zwar die gleiche Version des ursprünglichen Pakets erneut, jedoch nicht die Abhängigkeiten. Nutzen Sie diese Maßnahme, wenn das Update von Paketabhängigkeiten zu einem unterbrochenen Zustand führen würde.

1. **Neuinstallation von Paketen, wenn abhängige Versionen involviert sind**
    - Wie oben erläutert, ändert die Neuinstallation von Paketen nicht die Versionen anderer installierter Pakete, die davon abhängig sind. Es ist dann möglich, dass die Neuinstallation einer Abhängigkeit das abhängige Paket zerstört.
