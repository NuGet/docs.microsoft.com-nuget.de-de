---
title: NuGet Fehler und Warnungen-Referenz
description: Vollständige Referenz für Warnungen und Fehler von NuGet während verschiedener NuGet Vorgänge ausgegeben.
author: karann-msft
ms.author: karann
manager: unnir
ms.date: 05/18/2018
ms.topic: reference
ms.reviewer: anangaur
f1_keywords:
- NU1000
- NU1001
- NU1002
- NU1003
- NU1100
- NU1101
- NU1102
- NU1103
- NU1104
- NU1105
- NU1106
- NU1107
- NU1108
- NU1201
- NU1202
- NU1203
- NU1401
- NU1500
- NU1501
- NU1502
- NU1503
- NU1601
- NU1602
- NU1603
- NU1604
- NU1605
- NU1608
- NU1701
- NU1801
- NU3000
- NU3001
- NU3002
- NU3004
- NU3008
- NU3018
- NU3028
ms.openlocfilehash: 368a9554c5caf92b709f9b29e16b8a7cdb264eec
ms.sourcegitcommit: 2a6d200012cdb4cbf5ab1264f12fecf9ae12d769
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 06/06/2018
ms.locfileid: "34818515"
---
# <a name="errors-and-warnings"></a>Fehler und Warnungen

In NuGet 4.3.0+ Fehler und Warnungen werden nummeriert, wie in diesem Thema beschrieben und bieten detaillierte Informationen, damit Sie die Probleme zu beheben.

Die Fehler und Warnungen, die hier aufgeführten stehen nur mit [PackageReference basierende](../consume-packages/package-references-in-project-files.md) Projekte und NuGet-4.3.0+. NuGet wird auch berücksichtigt, MSBuild-Eigenschaften zum Unterdrücken von Warnungen oder Fehler zu erhöhen. Weitere Informationen finden Sie unter [wie: Unterdrücken von Compiler-Warnungen](/visualstudio/ide/how-to-suppress-compiler-warnings) in der Visual Studio-Dokumentation.

**Fehler**

| Gruppieren | Fehlernummern |
| --- | --- |
| [Ungültiger Eingabefehler](#invalid-input-errors) | [NU1001](#nu1001), [NU1002](#nu1002), [NU1003](#nu1003) |
| [Fehler aufgrund fehlender Pakets und der Projektparameter](#missing-package-and-project-errors) | [NU1100](#nu1100), [NU1101](#nu1101), [NU1102](#nu1102), [NU1103](#nu1103), [NU1104](#nu1104), [NU1105](#nu1105), [NU1106](#nu1106), [NU1107](#nu1107) (previously NU1607), [NU1108](#nu1108) (previously NU1606) |
| [Kompatibilitätsfehler](#compatibility-errors) | [NU1201](#nu1201), [NU1202](#nu1202), [NU1203](#nu1203), [NU1401](#nu1401) |

**Warnungen**

| Gruppieren | Warnungsnummern jeweils |
| --- | --- |
| [Ungültige Eingabe Warnungen](#invalid-input-warnings) | [NU1501](#nu1501), [NU1502](#nu1502), [NU1503](#nu1503) |
| [Unerwarteter Paket Version Warnungen](#unexpected-package-version-warnings) | [NU1601](#nu1601), [NU1602](#nu1602), [NU1603](#nu1603), [NU1604](#nu1604), [NU1605](#nu1605) |
| [Konfliktlöser Konflikt Warnungen](#resolver-conflict-warnings) | [NU1608](#nu1608) |
| [Paket-fallback-Warnungen](#package-fallback-warnings) | [NU1701](#nu1701) |
| [Feed-Warnungen](#feed-warnings) | [NU1801](#nu1801) |
| [NuGet-interne Fehler und Warnungen](#nuget-internal-errors-and-warnings) | [NU1000](#nu1000), [NU1500](#nu1500) |
| [Signierte Pakete (lizenzerstellung und Verifizierung)](#signed-packages-creation-and-verification)| [NU3000](#nu3000), [NU3001](#nu3001), [NU3002](#nu3002), [NU3004](#nu3004), [NU3008](#nu3008), [NU3018](#nu3018), [NU3028](#nu3028) |

## <a name="invalid-input-errors"></a>Ungültiger Eingabefehler

[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)

### <a name="nu1001"></a>NU1001

| | |
| --- | --- |
| **Problem** | Das Projekt enthält eine oder mehrere Frameworks. |
| **Beispiel-Nachricht** | *Das Projekt ProjA gibt keine Zielframeworks in c:\tmp\projA.csproj* |
| **Projektmappen** | Hinzufügen einer `TargetFramework` oder `TargetFrameworks` Eigenschaft der angegebenen Projektdatei. |

### <a name="nu1002"></a>NU1002

| | |
| --- | --- |
| **Problem** | Ungültige Kombination von Eingaben zusammen mit einem CLEAR-Schlüsselwort. |
| **Beispiel-Nachricht** | *Zusammen mit anderen Werten 'CLEAR' kann nicht verwendet werden* |
| **Projektmappen** | Verwenden von sich selbst deaktivieren, und lassen Sie alle anderen Eingaben aus. |

### <a name="nu1003"></a>NU1003

| | |
| --- | --- |
| **Problem** | `PackageTargetFallback` und `AssetTargetFallback` bieten anderes Verhalten für die Auswahl von Ressourcen und können nicht zusammen verwendet werden. |
| **Beispiel-Nachricht** | *PackageTargetFallback und AssetTargetFallback können nicht zusammen verwendet werden. Entfernen Sie PackageTargetFallback(deprecated) Verweise aus der Projekt-Umgebung.* |
| **Projektmappen** | Entfernen des veralteten `PackageTargetFallback` Element aus dem Projekt. |

## <a name="missing-package-and-project-errors"></a>Fehler aufgrund fehlender Pakets und der Projektparameter

[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104](#nu1104) | [NU1105](#nu1105) | [NU1106](#nu1106)

### <a name="nu1100"></a>NU1100

| | |
| --- | --- |
| **Problem** | Eine Abhängigkeitsgruppe werden nicht aufgelöst. Dies ist eine generische Problem für Typen, die keine Pakete oder Projekte sind. |
| **Beispiel-Nachricht** | *Kann nicht für net45 System.Missing aufgelöst* |
| **Projektmappen** | Öffnen Sie die Projektdatei, und untersuchen Sie die Liste der abhängigen Elemente. Überprüfen Sie, dass jede Abhängigkeit auf die Paketquellen vorhanden ist, die Sie verwenden und das Paket Zielframework des Projekts unterstützt. |

### <a name="nu1101"></a>NU1101

| | |
| --- | --- |
| **Problem** | Das Paket kann auf alle Quellen nicht gefunden werden. |
| **Beispiel-Nachricht** | *Nicht Paket System.Missing gefunden. Mit dieser Id in Quellen keine keine Pakete vorhanden: ein Dotnet-Core, Dotnet Roslyn, nuget.org* |
| **Projektmappen** | Untersuchen Sie das Projekt Abhängigkeiten in Visual Studio, um sicherzustellen, dass Sie das richtige Paket Bezeichner und die Versionsnummer Anzahl verwenden. Außerdem überprüfen, die die [NuGet-Konfiguration](../consume-packages/Configuring-NuGet-Behavior.md) identifiziert die Paketquellen Ihrer voraussichtlich verwenden werden. Wenn Sie Pakete mit verwendet werden [Semantischer Versionsverwaltung 2.0.0](../reference/package-versioning.md#semantic-versioning-200), stellen Sie sicher, dass Sie dem feed, V3 verwenden `https://api.nuget.org/v3/index.json`in der [NuGet-Konfiguration](../consume-packages/Configuring-NuGet-Behavior.md). |

### <a name="nu1102"></a>NU1102

| | |
| --- | --- |
| **Problem** | Die Paket-ID wurde gefunden, aber eine Version innerhalb des Bereichs für die angegebene Abhängigkeit kann auf der Quellen nicht gefunden werden. Der Bereich kann durch ein Paket und nicht für den Benutzer angegeben werden. |
| **Beispiel-Nachricht** | *Nicht Paket NuGet.Versioning Version gefunden (> = 9.0.1)<br/> -30 gefunden Version(en) in nuget.org [nächste Version: 4.0.0]<br/> -gefunden-10-Versionen in Dotnet-Buildtools [am nächsten Version: 4.0.0-rc-2129]<br/> -9 gefunden Versionen in NuGetVolatile [nächste Version: 3.0.0-beta-00032]<br/> -0 Version(en) in Dotnet Kernen gefunden<br/> -0 Version(en) in Dotnet Roslyn gefunden* |
| **Projektmappen** | Bearbeiten Sie die Projektdatei, um die Version des Pakets zu beheben. Außerdem überprüfen, die die [NuGet-Konfiguration](../consume-packages/Configuring-NuGet-Behavior.md) identifiziert die Paketquellen Ihrer voraussichtlich verwenden werden. Sie müssen möglicherweise die Requeted-Version ändern, wenn dieses Paket direkt vom Projekt verwiesen wird. |

### <a name="nu1103"></a>NU1103

| | |
| --- | --- |
| **Problem** | Das Projekt angegeben, eine stabile Version für den Bereich der Abhängigkeit, aber keine stabilen Versionen wurden in diesem Bereich gefunden. Vorabversionen wurden gefunden, aber es sind nicht zulässig. |
| **Beispiel-Nachricht** | *Nicht stabiles Paket NuGet.Versioning mit Version gefunden (> = 3.0.0)<br/> -gefunden-10-Versionen in Dotnet-Buildtools [nächste Version: 4.0.0-rc-2129]<br/> -gefunden 9 Version(en) in NuGetVolatile [nächste Version: 3.0.0-beta-00032] <br/> -0 Version(en) in Dotnet Kernen gefunden<br/> -0-Versionen in Dotnet Roslyn gefunden* |
| **Projektmappen** |  Bearbeiten der Versionsbereich in der Projektdatei, um Vorabversionen einzuschließen. Finden Sie unter [Paket versionsverwaltung](../reference/Package-Versioning.md). |

### <a name="nu1104"></a>NU1104

| | |
| --- | --- |
| **Problem** | Eine ProjectReference verweist auf eine Datei, die nicht vorhanden ist. |
| **Beispiel-Nachricht** | *Projekt-Verweises ist "c:\a.csproj" nicht vorhanden. Überprüfen Sie, dass der Projektverweis gültig ist und die Datei vorhanden ist.* |
| **Projektmappen** | Bearbeiten die Projektdatei, korrigieren den Pfad zu dem Projekt entweder oder den Verweis entfernen vollständig, wenn es nicht mehr benötigt wird. |

### <a name="nu1105"></a>NU1105

| | |
| --- | --- |
| **Problem** | Die Projektdatei vorhanden, aber keine Informationen zum Wiederherstellen der für sie bereitgestellt wurde. |
| **Beispiel-Nachricht** | *Lesen von Projektinformationen für 'c:\a.csproj' kann nicht ausgeführt werden. Die Projektdatei möglicherweise ungültige oder fehlende Ziele, die für die Wiederherstellung erforderlich sind.* |
| **Projektmappen** | In Visual Studio kann der Fehler dies bedeuten, dass das Projekt entladen wird, in diesem Fall das Projekt erneut laden. Über die Befehlszeile, könnte dies bedeuten, dass die Datei beschädigt ist oder dass er das benutzerdefinierte "nach dem Importe" enthalten nicht Ziel für die Wiederherstellung, lesen das Projekt erforderlich sind. Überprüfen Sie, ob die Projektdatei enthält ein "after" Importe"Ziel gültig ist. |

### <a name="nu1106"></a>NU1106

| | |
| --- | --- |
| **Problem** | Abhängigkeit Einschränkungen können nicht aufgelöst werden. |
| **Beispiel-Nachricht** | *Können nicht erfüllt einen Konflikt verursachenden Anforderungen für {Id}: {Konflikt Path} Framework: {Zieldiagramm}* |
| **Projektmappen** | Bearbeiten Sie die Projektdatei, um mehr offene Bereiche für eine genaue Version, anstatt die Abhängigkeit angeben. |
|

<a name="nu1107"></a>

### <a name="nu1107-previously-nu1607"></a>NU1107 (zuvor NU1607)

| | |
| --- | --- |
| **Problem** | Kann nicht auf Einschränkungen der Abhängigkeit zwischen Paketen zu beheben. |
| **Beispiel-Nachricht** | *Versionskonflikt für NuGet.Versioning erkannt. Verweisen auf das Paket direkt aus dem Projekt aus, um dieses Problem zu beheben.<br/>  Im NuGet.Packaging 3.5.0 -> (= 3.5.0) NuGet.Versioning<br/> NuGet.Configuration 4.0.0 -> NuGet.Versioning (4.0.0 =)* |
| **Projektmappen** | Pakete mit Abhängigkeit Beschränkungen exakte Version lassen nicht anderen Paketen für die Version bei Bedarf zu erhöhen. Fügen Sie einen Verweis auf das Paket direkt (in der Projektdatei), die genaue Version, die erforderlich sind. |

<a name="nu1108"></a>

### <a name="nu1108-previously-nu1606"></a>NU1108 (zuvor NU1606)

| | |
| --- | --- |
| **Problem** | Eine ringabhängigkeit wurde festgestellt. |
| **Beispiel-Nachricht** | *Zyklus erkannt: A-B > -> ein* |
| **Projektmappen** | Das Paket ist nicht ordnungsgemäß erstellt. Wenden Sie sich an den Besitzer des Pakets, um den Fehler zu beheben. |

## <a name="compatibility-errors"></a>Kompatibilitätsfehler

[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)

### <a name="nu1201"></a>NU1201

| | |
| --- | --- |
| **Problem** | Eine Abhängigkeit-Projekt enthält kein Framework, die kompatibel mit dem aktuellen Projekt. Zielframework des Projekts ist i. d. r. eine spätere Version als das betreffende Projekt. |
| **Beispiel-Nachricht** | *Projekt ServerWeb ist nicht kompatibel mit netstandard1.3 (. Netstandard-, Version = V1. 3). Projekt ServerWeb unterstützt:<br/> -netstandard1.6 (. Netstandard-, Version = V1. 6)<br/> -netcoreapp1.0 (. NETCoreApp, Version = V1. 0)* |
| **Projektmappen** | Ändern Sie Zielframework des Projekts in eine dieselbe oder eine niedrigere Version als das betreffende Projekt. |

### <a name="nu1202"></a>NU1202

| | |
| --- | --- |
| **Problem** | Eine Abhängigkeit keine Objekte, die kompatibel mit dem Projekt enthalten. |
| **Beispiel-Nachricht** | *Paket System.ComponentModel.EventBasedAsync 4.0.11 ist nicht kompatibel mit netstandard1.3 (. Netstandard-, Version = V1. 3). Paket System.ComponentModel.EventBasedAsync 4.0.11 unterstützt:<br/> -monoandroid10 (MonoAndroid, Version = V1. 0)<br/> -monotouch10 (MonoTouch, Version = V1. 0)<br/> -net45 (. NETFramework, Version = v4. 5)<br/> -netcore50 (. NETCore, Version = V5. 0)<br/> -netstandard1.0 (. Netstandard-, Version = V1. 0)<br/> -Portable net45 + win8 wp8 + wpa81 (. NETPortable, Version = V0.0 Profil = Profile259)<br/> -win8 (Windows, Version = v8. 0)<br/> -wp8 (WindowsPhone, Version = v8. 0)<br/> -wpa81 (WindowsPhoneApp, Version = v8. 1)<br/> -xamarinios10 ( Xamarin.iOS,Version=v1.0)<br/> -xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/> -xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/> -xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*|
| **Projektmappen** | Ändern Sie Zielframework des Projekts, sodass das Paket unterstützt. |

### <a name="nu1203"></a>NU1203

| | |
| --- | --- |
| **Problem** | Das Paket unterstützt nicht des Projekts `RuntimeIdentifier`. |
| **Beispiel-Nachricht** | *System.Example 1.0.0 bietet eine Kompilierung Verweisassembly für a.dll für net461, jedoch keine kompatible Laufzeitassembly vorhanden ist.* |
| **Projektmappen** | Ändern der `RuntimeIdentifier` Werte, die im Projekt verwendete nach Bedarf. |

### <a name="nu1401"></a>NU1401

| | |
| --- | --- |
| **Problem** | Das Paket erfordert, Funktionen oder Frameworks, die von der installierten Version von NuGet derzeit nicht unterstützt. |
| **Beispiel-Nachricht** | *Das Paket "NuGet.Versioning" erfordert die NuGet-Clientversion '5.0.0' oder höher, aber die aktuelle NuGet-Version ist "4.3.0".* |
| **Projektmappen** | Installieren Sie eine neuere Version von NuGet. Finden Sie unter [Installing NuGet-Clienttools](../install-nuget-client-tools.md). |

## <a name="invalid-input-warnings"></a>Ungültige Eingabe Warnungen

[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)

### <a name="nu1501"></a>NU1501

| | |
| --- | --- |
| **Problem** | Die Projekt-Wiederherstellung wird versucht, Betrieb auf wurde nicht gefunden. |
| **Beispiel-Nachricht** | *Der Ordner "c:\projects\a" enthält kein Projekt wiederhergestellt.* |
| **Projektmappen** | Führen Sie die NuGet-Wiederherstellung in einen Ordner, der ein Projekt enthält. |

### <a name="nu1502"></a>NU1502

| | |
| --- | --- |
| **Problem** | `RuntimeSupports` enthält ein ungültiges Profil. Das Profil unterstützt wurde in der Regel nicht gefunden, eine `runtime.json` -Datei aus der aktuellen abhängigkeitspakete.|
| **Beispiel-Nachricht** | *Unbekannte Kompatibilitätsprofil: aaa* |
| **Projektmappen** | Überprüfen Sie die `RuntimeSupports` Wert in Ihrem Projekt. |

### <a name="nu1503"></a>NU1503

| | |
| --- | --- |
| **Problem** | NuGet Restore Ziele importieren Sie ein Projekt für die Abhängigkeit nicht. Dies ist vergleichbar mit NU1105 jedoch hier das Projekt wird übersprungen und ignoriert alle Wiederherstellung fehl und es erfolgt keine. In komplexen Lösungen sind häufig die anderen Projekttypen, die Wiederherstellung möglicherweise nicht unterstützen. |
| **Beispiel-Nachricht** | *Überspringen die Wiederherstellung für Projekt "c:\a.csproj". Die Projektdatei möglicherweise ungültige oder fehlende Ziele, die für die Wiederherstellung erforderlich sind.* |
| **Projektmappen** | Dies kann geschehen für Projekte, die nicht häufig Props/Ziele importieren, die Wiederherstellung automatisch importiert. Wenn das Projekt nicht wiederhergestellt werden, kann dies ignoriert werden. Andernfalls bearbeiten Sie Projekt, die betroffene um Ziele für die Wiederherstellung hinzuzufügen. |

## <a name="unexpected-package-version-warnings"></a>Unerwarteter Paket Version Warnungen

[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)

### <a name="nu1601"></a>NU1601

| | |
| --- | --- |
| **Problem** | Direkte projektabhängigkeit wurde an eine spätere Version als das angegebene Projekt deaktivieren. |
| **Beispiel-Nachricht** | *Angegebene Abhängigkeit war NuGet.Versioning (> = 3.5.0), aber mit NuGet.Versioning 4.0.0 endete.* |
| **Projektmappen** | Aktualisieren Sie die Abhängigkeit im Projekt auf eine entsprechende Version. |

### <a name="nu1602"></a>NU1602

| | |
| --- | --- |
| **Problem** | Eine paketabhängigkeit fehlt eine Untergrenze. Dies lässt nicht die Wiederherstellung mithilfe der Softwareoption der *beste Übereinstimmung*. Jede Wiederherstellung wird float abwärts versuchen, eine niedrigere Version zu finden, die verwendet werden kann. Dies bedeutet, dass die Wiederherstellung überprüft alle Datenquellen jedes Mal statt der Pakete, die bereits existieren im Ordner "Benutzer-Paket" online geschaltet. |
| **Beispiel-Nachricht** | *Im NuGet.Packaging 4.0.0 bietet eine inklusive untere Grenze keine Abhängigkeitsinformationen NuGet.Versioning (3.5.0 >). Eine ungefähre beste Übereinstimmung der 3.6.0 wurde aufgelöst.* |
| **Projektmappen** | Dies ist normalerweise ein Paket erstellen Fehler. Wenden Sie sich an den Paketersteller, um das Problem zu beheben. |

### <a name="nu1603"></a>NU1603

| | |
| --- | --- |
| **Problem** | Eine paketabhängigkeit angegeben, eine Version, die nicht gefunden werden konnte. In der Regel enthalten die Paketquellen nicht die erwartete Untergrenze-Version. Eine höhere Version wurde stattdessen verwendet die unterscheidet sich von was für das Paket erstellt wurde.<br/><br/>Dies bedeutet, dass die Wiederherstellung wurde nicht gefunden. die *beste Übereinstimmung*. Jede Wiederherstellung wird float abwärts versuchen, eine niedrigere Version zu finden, die verwendet werden kann. Dies bedeutet, dass die Wiederherstellung überprüft alle Datenquellen jedes Mal statt der Pakete, die bereits existieren im Ordner "Benutzer-Paket" online geschaltet. |
| **Beispiel-Nachricht** | Im NuGet.Packaging 4.0.0 hängt NuGet.Versioning (> = 4.0.0) aber 4.0.0 wurde nicht gefunden. Eine ungefähre beste Übereinstimmung der 5.0.0 wurde aufgelöst. |
| **Projektmappen** | Wenn das Paket erwartet nicht freigegeben wurde, kann dies ein Paket erstellen Fehler sein. Wenden Sie sich an den Paketersteller, um das Problem zu beheben. Wenn das Paket freigegeben wurde, überprüfen Sie, dass es auf die Paketquellen vorliegt, die Sie verwenden. Wenn Sie eine private Datenquelle zu verwenden, müssen Sie das Paket auf diesem feed zu aktualisieren. |

### <a name="nu1604"></a>NU1604

| | |
| --- | --- |
| **Problem** | Projektabhängigkeit nicht mit eine unteren Grenze definiert.<br/><br/>Dies bedeutet, dass die Wiederherstellung wurde nicht gefunden. die *beste Übereinstimmung*. Jede Wiederherstellung wird float abwärts versuchen, eine niedrigere Version zu finden, die verwendet werden kann. Dies bedeutet, dass die Wiederherstellung überprüft alle Datenquellen jedes Mal statt der Pakete, die bereits existieren im Ordner "Benutzer-Paket" online geschaltet. |
| **Beispiel-Nachricht** | *Abhängigkeit NuGet.Versioning Projekt (< = 9.0.0) Doe keine inklusive untere Grenze enthalten. Schließen Sie eine untere Grenze in die Version der Abhängigkeit, Wiederherstellung konsistente Ergebnisse sicherzustellen.* |
| **Projektmappen** | Aktualisieren Sie des Projekts `PackageReference` `Version` Attribut um eine Untergrenze einzuschließen. |

### <a name="nu1605"></a>NU1605

| | |
| --- | --- |
| **Problem** | Eine abhängigkeitspakets angegeben, eine versionseinschränkung für eine spätere Version eines Pakets als wiederherstellen, die letztlich aufgelöst. D. h. aufgrund der "Nächster gewinnt" Regel beim Auflösen von Paketen, ein näher Paket im Diagramm möglicherweise ein entfernten Paket außer Kraft gesetzt haben. |
| **Beispiel-Nachricht** | *Downgrade für die Paket erkannt: NuGet.Versioning aus 4.0.0 auf 3.5.0. Verweisen auf das Paket direkt aus dem Projekt eine andere Version auswählen.<br/>  Im NuGet.Packaging 3.5.0 -> NuGet.Versioning 3.5.0<br/> NuGet.Commands 4.0.0 -> NuGet.Configuration 4.0.0 -> NuGet.Versioning 4.0.0* |
| **Projektmappen** | Fügen Sie einen direkten Verweis auf das Projekt für die höhere Version des Pakets, das Sie verwenden möchten. |

## <a name="resolver-conflict-warnings"></a>Konfliktlöser Konflikt Warnungen

### <a name="nu1608"></a>NU1608

| | |
| --- | --- |
| **Problem** | Ein aufgelöst Paket ist größer als eine Abhängigkeit Einschränkung zulässt. Dies bedeutet, dass ein Paket verwiesen wird, direkt von einem Projekt Abhängigkeit Einschränkungen von anderen Paketen überschreibt.|
| **Beispiel-Nachricht** | *Erkannte Paketversion außerhalb Abhängigkeit Einschränkung: x 1.0.0 erfordert y (= 1.0.0), aber Version y 2.0.0 aufgelöst wurde.* |
| **Projektmappen** | In einigen Fällen ist dies beabsichtigt, und die Warnung unterdrückt werden kann. Ändern Sie andernfalls den Projektverweis, zu dem Paket, deren Version Einschränkungen erweitert werden. |

## <a name="package-fallback-warnings"></a>Paket-fallback-Warnungen

### <a name="nu1701"></a>NU1701

| | |
| --- | --- |
| **Problem** | `PackageTargetFallback` / `AssetTargetFallback` wurde verwendet, um Ressourcen aus einem Paket auszuwählen. Die Warnung kann Benutzer wissen, dass die Ressourcen nicht 100 % kompatibel sein. |
| **Beispiel-Nachricht** | *Paket "NuGet.Versioning" wurde mit "Portable net45 + win8" stattdessen das Zielframework des Projekts "netstandard1.5" wiederhergestellt. Dieses Paket möglicherweise nicht vollständig kompatibel ist, während das Projekt.* |
| **Projektmappen** | Ändern Sie Zielframework des Projekts, sodass das Paket unterstützt. |

## <a name="feed-warnings"></a>Feed-Warnungen

### <a name="nu1801"></a>NU1801

| | |
| --- | --- |
| **Problem** | Fehler beim Lesen von Feeds beim `IgnoreFailedSources` festgelegt ist auf "true", und konvertieren ihn in eine schwerwiegende Warnung. Dies kann eine beliebige Nachricht enthalten und ist generisch. |
| **Beispiel-Nachricht** | n/v |
| **Projektmappen** | Bearbeiten Sie die Konfiguration, um gültige Quellen angeben. |

## <a name="nuget-internal-errors-and-warnings"></a>NuGet-interne Fehler und Warnungen

[NU1000](#nu1000) | [NU1500](#nu1500)

### <a name="nu1000"></a>NU1000

| | |
| --- | --- |
| **Problem** | Ein nicht spezifizierter interne Fehler von NuGet. |
| **Projektmappen** | Überprüfen Sie die Ereignisprotokolle auf Weitere Informationen |

### <a name="nu1500"></a>NU1500

| | |
| --- | --- |
| **Problem** | Eine nicht bestimmte interne Warnung von NuGet. |
| **Projektmappen** | Überprüfen Sie die Ereignisprotokolle auf Weitere Informationen |

## <a name="signed-packages-creation-and-verification"></a>Signierte Pakete (lizenzerstellung und Verifizierung)

*NuGet-4.6.0+*

[NU3000](#nu3000) | [NU3001](#nu3001) | [NU3002](#nu3002) | [NU3004](#nu3004) | [NU3008](#nu3008) | [NU3018](#nu3018) | [NU3028](#nu3028)

### <a name="nu3000"></a>NU3000

| | |
| --- | --- |
| **Problem** | Ein nicht-spezifische Fehler im Zusammenhang mit paketsignierung und paketüberprüfung signiert. |
| **Projektmappen** | Überprüfen Sie die Ereignisprotokolle auf Weitere Informationen. |

### <a name="nu3001"></a>NU3001

| | |
| --- | --- |
| **Problem** | Ungültige Argumente auf den [Signieren Befehl](../tools/cli-ref-sign.md) oder [Befehl überprüfen](../tools/cli-ref-verify.md). |
| **Projektmappen** | Überprüfen Sie, und beheben Sie die angegebenen Argumenten. |

### <a name="nu3002"></a>NU3002

| | |
| --- | --- |
| **Problem** | Die `-Timestamper` Option wurde nicht angegeben, mit der [NuGet-Anmelde-Befehls](../tools/cli-ref-sign.md). |
| **Beispiel-Nachricht** | *Die '-Timestamper' Option wurde nicht angegeben. Das signierte Paket kann nicht mit einem Zeitstempel versehen werden.* |
| **Projektmappen** | Geben Sie die `-Timestamper` mit option `nuget sign`. |

### <a name="nu3004"></a>NU3004

| | |
| --- | --- |
| **Problem** | Ein Paket ohne Vorzeichen bereitgestellt wurde, um die [Nuget überprüfen Befehl](../tools/cli-ref-verify.md). |
| **Projektmappen** | Führen Sie `nuget verify` mit eines signierten Pakets. Finden Sie unter [Signieren eines Pakets](../create-packages/Sign-a-Package.md). |

### <a name="nu3008"></a>NU3008

| | |
| --- | --- |
| **Problem** | Die Paket-integritätsprüfung ist fehlgeschlagen, was bedeutet, dass ein signiertes Pakets manipuliert wurde, seit Sie durch die Anmeldung an. |
| **Projektmappen** | Scannen des Computers mit Antivirus-Software. Entfernen Sie das Paket vom Computer, installieren Sie ihn erneut, und wiederholen Sie den Vorgang. Wenn das Problem weiterhin besteht, wenden Sie sich an den Besitzer der Paketquelle und Besitzer des Pakets. |

### <a name="nu3018"></a>NU3018

| | |
| --- | --- |
| **Problem** | Fehler bei der kettenerstellung dieses Zertifikat für die primäre Signatur. Das primäre Signaturzertifikat nicht vertrauenswürdig ist, gesperrt, oder die Sperrinformationen für das Zertifikat ist nicht verfügbar. |
| **Beispiel-Nachricht** | *Warnung: NU3018: die Sperrfunktion konnte die Sperrung des Zertifikats zu überprüfen.* |
| **Projektmappen** | Verwenden Sie ein Zertifikat vertrauenswürdig ist und gültig. Überprüfen Sie die Internet-Konnektivität. |

### <a name="nu3028"></a>NU3028

| | |
| --- | --- |
| **Problem** | Fehler bei der kettenerstellung dieses Zertifikat für die Timestamp-Signatur. Der Timestamp-Signaturzertifikat nicht vertrauenswürdig ist, gesperrt, oder Sperrinformationen für das Zertifikat ist nicht verfügbar. |
| **Beispiel-Nachricht** | *Warnung: NU3028: die Sperrfunktion konnte die Sperrung des Zertifikats zu überprüfen.* |
| **Projektmappen** | Verwenden Sie ein Zertifikat vertrauenswürdig ist und gültig. Überprüfen Sie die Internet-Konnektivität. |
