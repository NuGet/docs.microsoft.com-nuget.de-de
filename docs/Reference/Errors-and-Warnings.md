---
title: NuGet Restore, Fehler und Warnungen-Referenz | Microsoft Docs
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/13/2017
ms.topic: reference
ms.prod: nuget
ms.technology: 
ms.assetid: b76b8a00-7155-4163-b533-894086d2ef78
description: "Vollständige Referenz für Warnungen und Fehler von NuGet ausgegeben werden, während der paketwiederherstellung"
keywords: NuGet-Fehler, Warnungen NuGet-Diagnose
ms.reviewer:
- anangaur
- karann-msft
- unniravindranathan
ms.openlocfilehash: 29eb72cbb6c095cd3aeb524fd8b28416ec5dc798
ms.sourcegitcommit: 6ccb963e065680ab2e7df1d8dd5492897fd56b04
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 01/23/2018
---
# <a name="errors-and-warnings"></a>Fehler und Warnungen

Im NuGet 4.3.0 Fehler und Warnungen werden nummeriert, wie in diesem Thema beschrieben und bieten detaillierte Informationen, damit Sie die Probleme zu beheben. 

Die Fehler und Warnungen, die hier aufgeführten stehen nur mit [PackageReference basierende](../Consume-Packages/Package-References-in-Project-Files.md) Projekte und NuGet-4.3.0. NuGet wird auch berücksichtigt, MSBuild-Eigenschaften zum Unterdrücken von Warnungen oder Fehler zu erhöhen. Weitere Informationen finden Sie unter [wie: Unterdrücken von Compiler-Warnungen](/visualstudio/ide/how-to-suppress-compiler-warnings) in der Visual Studio-Dokumentation.

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

## <a name="invalid-input-errors"></a>Ungültiger Eingabefehler

[NU1001](#nu1001) | [NU1002](#nu1002) | [NU1003](#nu1003)

### <a name="nu1001"></a>NU1001

| | |
| --- | --- |
| **Problem** | Das Projekt enthält eine oder mehrere Frameworks. |
| **Häufige Ursachen** | Das Projekt enthält eine `TargetFramework` oder `TargetFrameworks` Eigenschaft. |
| **Beispiel-Nachricht** | *Das Projekt ProjA gibt keine Zielframeworks in c:\tmp\projA.csproj* |

### <a name="nu1002"></a>NU1002

| | |
| --- | --- |
| **Problem** | Ungültige Kombination von Eingaben zusammen mit einem CLEAR-Schlüsselwort. |
| **Häufige Ursachen** | Deaktivieren Sie möglicherweise nicht mit anderen Eingaben kombiniert werden. |
| **Beispiel-Nachricht** | *Zusammen mit anderen Werten 'CLEAR' kann nicht verwendet werden* |

### <a name="nu1003"></a>NU1003

| | |
| --- | --- |
| **Problem** | `PackageTargetFallback`und `AssetTargetFallback` bieten anderes Verhalten für die Auswahl von Ressourcen und können nicht zusammen verwendet werden. |
| **Häufige Ursachen** | Beide `PackageTargetFallback` und `AssetTargetFallback` im Projekt vorhanden. |
| **Beispiel-Nachricht** | *PackageTargetFallback und AssetTargetFallback können nicht zusammen verwendet werden. Entfernen Sie PackageTargetFallback(deprecated) Verweise aus der Projekt-Umgebung.* |

## <a name="missing-package-and-project-errors"></a>Fehler aufgrund fehlender Pakets und der Projektparameter

[NU1100](#nu1100) | [NU1101](#nu1101) | [NU1102](#nu1102) | [NU1103](#nu1103) | [NU1104](#nu1104) | [NU1105](#nu1105) | [NU1106](#nu1106)

### <a name="nu1100"></a>NU1100

| | |
| --- | --- |
| **Problem** | Eine Abhängigkeitsgruppe werden nicht aufgelöst. Dies ist eine generische Problem für Typen, die keine Pakete oder Projekte sind. |
| **Häufige Ursachen** | Das Projekt enthält eine Abhängigkeit auf ein Element, das nicht vorhanden ist. |
| **Beispiel-Nachricht** | *Kann nicht für net45 System.Missing aufgelöst* |

### <a name="nu1101"></a>NU1101

| | |
| --- | --- |
| **Problem** | Das Paket kann auf alle Quellen nicht gefunden werden. |
| **Häufige Ursachen** | Die richtige Paketquelle fehlt, oder die Paket-ID ist falsch. |
| **Beispiel-Nachricht** | *Nicht Paket System.Missing gefunden. Mit dieser Id in Quellen keine keine Pakete vorhanden: ein Dotnet-Core, Dotnet Roslyn, nuget.org* |

### <a name="nu1102"></a>NU1102

| | |
| --- | --- |
| **Problem** | Die Paket-ID wurde gefunden, aber eine Version innerhalb des Bereichs für die angegebene Abhängigkeit kann auf der Quellen nicht gefunden werden. |
| **Häufige Ursachen** | Die richtige Paketquelle fehlt, oder die Abhängigkeit Bereich ist falsch. Der Bereich kann durch ein Paket und nicht für den Benutzer angegeben werden. Möglicherweise muss der Benutzer auf eine verfügbare Version zu wechseln, wenn dieses Paket direkt vom Projekt verwiesen wird. |
| **Beispiel-Nachricht** | *Nicht Paket NuGet.Versioning Version gefunden (> = 9.0.1)<br/> -30 gefunden Version(en) in nuget.org [nächste Version: 4.0.0]<br/> -gefunden-10-Versionen in Dotnet-Buildtools [am nächsten Version: 4.0.0-rc-2129]<br/> -9 gefunden Versionen in NuGetVolatile [nächste Version: 3.0.0-beta-00032]<br/> -0 Version(en) in Dotnet Kernen gefunden<br/> -0 Version(en) in Dotnet Roslyn gefunden* |

### <a name="nu1103"></a>NU1103

| | |
| --- | --- |
| **Problem** | Im Bereich Abhängigkeit wurden keine stabilen Versionen gefunden. Vorabversionen wurden gefunden, aber es sind nicht zulässig. |
| **Häufige Ursachen** | Das Projekt angegeben eine stabile Version für den Bereich der Abhängigkeit. Benutzer müssen die Versionsbereich Einbeziehung von Vorabversionen zu ändern. |
| **Beispiel-Nachricht** | *Nicht stabiles Paket NuGet.Versioning mit Version gefunden (> = 3.0.0)<br/> -gefunden-10-Versionen in Dotnet-Buildtools [nächste Version: 4.0.0-rc-2129]<br/> -gefunden 9 Version(en) in NuGetVolatile [nächste Version: 3.0.0-beta-00032] <br/> -0 Version(en) in Dotnet Kernen gefunden<br/> -0-Versionen in Dotnet Roslyn gefunden* |

### <a name="nu1104"></a>NU1104

| | |
| --- | --- |
| **Problem** | Eine ProjectReference verweist auf eine Datei, die nicht vorhanden ist. |
| **Häufige Ursachen** | Die Projektdatei wird vom Datenträger fehlt, oder der Verweis ist falsch. |
| **Beispiel-Nachricht** | *Projekt-Verweises ist "c:\a.csproj" nicht vorhanden. Überprüfen Sie, dass der Projektverweis gültig ist und die Datei vorhanden ist.* |

### <a name="nu1105"></a>NU1105

| | |
| --- | --- |
| **Problem** | Die Projektdatei vorhanden, aber keine Informationen zum Wiederherstellen der für sie bereitgestellt wurde. |
| **Häufige Ursachen** | In Visual Studio könnte dies bedeuten, dass das Projekt entladen wurde. Über die Befehlszeile könnte dies bedeuten, dass die Datei beschädigt ist oder dass er das benutzerdefinierte nach Importe Ziel erforderlich sind, für die Wiederherstellung, lesen das Projekt enthält, informieren. |
| **Beispiel-Nachricht** | *Lesen von Projektinformationen für 'c:\a.csproj' kann nicht ausgeführt werden. Die Projektdatei möglicherweise ungültige oder fehlende Ziele, die für die Wiederherstellung erforderlich sind.* |

### <a name="nu1106"></a>NU1106

| | |
| --- | --- |
| **Problem** | Abhängigkeit Einschränkungen können nicht aufgelöst werden. |
| **Häufige Ursachen** | Pakete enthalten Abhängigkeit genaue Versionen eines Pakets anstelle von begrenzten Bereichen. |
| **Beispiel-Nachricht** | *Können nicht erfüllt einen Konflikt verursachenden Anforderungen für {Id}: {Konflikt Path} Framework: {Zieldiagramm}* |

<a name="nu1107"></a> 

### <a name="nu1107-previously-nu1607"></a>NU1107 (zuvor NU1607)

| | |
| --- | --- |
| **Problem** | Kann nicht auf Einschränkungen der Abhängigkeit zwischen Paketen zu beheben. |
| **Häufige Ursachen** | Pakete mit Abhängigkeit Beschränkungen exakte Version lassen nicht anderen Paketen für die Version bei Bedarf zu erhöhen. |
| **Beispiel-Nachricht** | *Versionskonflikt für NuGet.Versioning erkannt. Verweisen auf das Paket direkt aus dem Projekt aus, um dieses Problem zu beheben.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning (= 3.5.0)<br/>  NuGet.Configuration 4.0.0 -> NuGet.Versioning (= 4.0.0)* |

<a name="nu1108"></a>

### <a name="nu1108-previously-nu1606"></a>NU1108 (zuvor NU1606)

| | |
| --- | --- |
| **Problem** | Eine ringabhängigkeit wurde festgestellt. |
| **Häufige Ursachen** | Ein Paket ist nicht richtig. |
| **Beispiel-Nachricht** | *Zyklus erkannt: A-B > -> ein* |

## <a name="compatibility-errors"></a>Kompatibilitätsfehler

[NU1201](#nu1201) | [NU1202](#nu1202) | [NU1203](#nu1203) | [NU1401](#nu1401)

### <a name="nu1201"></a>NU1201

| | |
| --- | --- |
| **Problem** | Eine Abhängigkeit-Projekt enthält kein Framework, die kompatibel mit dem aktuellen Projekt. |
| **Häufige Ursachen** | Zielframework des Projekts ist eine spätere Version als das betreffende Projekt. |
| **Beispiel-Nachricht** | *Projekt ServerWeb ist nicht kompatibel mit netstandard1.3 (. Netstandard-, Version = V1. 3). Projekt ServerWeb unterstützt:<br/> -netstandard1.6 (. Netstandard-, Version = V1. 6)<br/> -netcoreapp1.0 (. NETCoreApp, Version = V1. 0)* |

### <a name="nu1202"></a>NU1202

| | |
| --- | --- |
| **Problem** | Eine Abhängigkeit keine Objekte, die kompatibel mit dem Projekt enthalten. |
| **Häufige Ursachen** | Das Paket unterstützt keine Zielframework des Projekts. |
| **Beispiel-Nachricht** | *Paket System.ComponentModel.EventBasedAsync 4.0.11 ist nicht kompatibel mit netstandard1.3 (. Netstandard-, Version = V1. 3). Package System.ComponentModel.EventBasedAsync 4.0.11 supports:<br/>  - monoandroid10 (MonoAndroid,Version=v1.0)<br/>  - monotouch10 (MonoTouch,Version=v1.0)<br/>  - net45 (.NETFramework,Version=v4.5)<br/>  - netcore50 (.NETCore,Version=v5.0)<br/>  - netstandard1.0 (.NETStandard,Version=v1.0)<br/>  - portable-net45+win8+wp8+wpa81 (.NETPortable,Version=v0.0,Profile=Profile259)<br/>  - win8 (Windows,Version=v8.0)<br/>  - wp8 (WindowsPhone,Version=v8.0)<br/>  - wpa81 (WindowsPhoneApp,Version=v8.1)<br/>  - xamarinios10 (Xamarin.iOS,Version=v1.0)<br/>  - xamarinmac20 (Xamarin.Mac,Version=v2.0)<br/>  - xamarintvos10 (Xamarin.TVOS,Version=v1.0)<br/>  - xamarinwatchos10 (Xamarin.WatchOS,Version=v1.0)*|

### <a name="nu1203"></a>NU1203

| | |
| --- | --- |
| **Problem** | Das Paket unterstützt nicht des Projekts `RuntimeIdentifier`. |
| **Häufige Ursachen** | Das Paket unterstützt nicht die aktuelle `RuntimeIdentifier`. Ändern der `RuntimeIdentifier` Werte, die im Projekt verwendet werden, wenn erforderlich. |
| **Beispiel-Nachricht** | *System.Example 1.0.0 bietet eine Kompilierung Verweisassembly für a.dll für net461, jedoch keine kompatible Laufzeitassembly vorhanden ist.* |

### <a name="nu1401"></a>NU1401

| | |
| --- | --- |
| **Problem** | Das Paket erfordert, Funktionen oder Frameworks, die von der installierten Version von NuGet derzeit nicht unterstützt. |
| **Häufige Ursachen** | Ein Upgrade von NuGet, um das Problem zu beheben. |
| **Beispiel-Nachricht** | *Das Paket "NuGet.Versioning" erfordert die NuGet-Clientversion '5.0.0' oder höher, aber die aktuelle NuGet-Version ist "4.3.0". Um das Upgrade von NuGet ausführen, wechseln Sie zu http://docs.nuget.org/consume/installing-nuget.* |

## <a name="invalid-input-warnings"></a>Ungültige Eingabe Warnungen

[NU1501](#nu1501) | [NU1502](#nu1502) | [NU1503](#nu1503)

### <a name="nu1501"></a>NU1501

| | |
| --- | --- |
| **Problem** | Die Projekt-Wiederherstellung wird versucht, Betrieb auf wurde nicht gefunden. |
| **Häufige Ursachen** | Das Projekt ist nicht vorhanden. |
| **Beispiel-Nachricht** | *Der Ordner "c:\projects\a" enthält kein Projekt wiederhergestellt.* |

### <a name="nu1502"></a>NU1502

| | |
| --- | --- |
| **Problem** | `RuntimeSupports`enthält ein ungültiges Profil. |
| **Häufige Ursachen** | Unterstützt das Profil wurde nicht gefunden, eine `runtime.json` -Datei aus der aktuellen abhängigkeitspakete. |
| **Beispiel-Nachricht** | *Unbekannte Kompatibilitätsprofil: aaa* |

### <a name="nu1503"></a>NU1503

| | |
| --- | --- |
| **Problem** | NuGet Restore Ziele importieren Sie ein Projekt für die Abhängigkeit nicht. Dies ist vergleichbar mit NU1105 jedoch hier das Projekt wird übersprungen und ignoriert alle Wiederherstellung fehl und es erfolgt keine. In komplexen Lösungen sind häufig die anderen Projekttypen, die Wiederherstellung möglicherweise nicht unterstützen. |
| **Häufige Ursachen** | Dies kann geschehen für Projekte, die nicht häufig Props/Ziele importieren, die Wiederherstellung automatisch importiert. Wenn das Projekt nicht wiederhergestellt werden, kann dies ignoriert werden. |
| **Beispiel-Nachricht** | *Überspringen die Wiederherstellung für Projekt "c:\a.csproj". Die Projektdatei möglicherweise ungültige oder fehlende Ziele, die für die Wiederherstellung erforderlich sind.* |

## <a name="unexpected-package-version-warnings"></a>Unerwarteter Paket Version Warnungen

[NU1601](#nu1601) | [NU1602](#nu1602) | [NU1603](#nu1603) | [NU1604](#nu1604) | [NU1605](#nu1605)

### <a name="nu1601"></a>NU1601

| | |
| --- | --- |
| **Problem** | Direkte projektabhängigkeit wurde an eine spätere Version als das angegebene Projekt deaktivieren. |
| **Häufige Ursachen** | Eine andere abhängigkeitspakets eine höhere Version erforderlich, und deaktivieren das Paket von. |
| **Beispiel-Nachricht** | *Angegebene Abhängigkeit war NuGet.Versioning (> = 3.5.0), aber mit NuGet.Versioning 4.0.0 endete.* |

### <a name="nu1602"></a>NU1602

| | |
| --- | --- |
| **Problem** | Eine paketabhängigkeit fehlt eine Untergrenze. Dies lässt nicht die Wiederherstellung mithilfe der Softwareoption der *beste Übereinstimmung*. Jede Wiederherstellung wird float abwärts versuchen, eine niedrigere Version zu finden, die verwendet werden kann. Dies bedeutet, dass die Wiederherstellung überprüft alle Datenquellen jedes Mal statt der Pakete, die bereits existieren im Ordner "Benutzer-Paket" online geschaltet. |
| **Häufige Ursachen** | Dies ist normalerweise ein Paket erstellen Fehler. |
| **Beispiel-Nachricht** | *Im NuGet.Packaging 4.0.0 bietet eine inklusive untere Grenze keine Abhängigkeitsinformationen NuGet.Versioning (3.5.0 >). Eine ungefähre beste Übereinstimmung der 3.6.0 wurde aufgelöst.* |

### <a name="nu1603"></a>NU1603

| | |
| --- | --- |
| **Problem** | Eine paketabhängigkeit angegeben, eine Version, die nicht gefunden werden konnte. Eine höhere Version wurde stattdessen verwendet die unterscheidet sich von was für das Paket erstellt wurde.<br/><br/>Dies bedeutet, dass die Wiederherstellung wurde nicht gefunden. die *beste Übereinstimmung*. Jede Wiederherstellung wird float abwärts versuchen, eine niedrigere Version zu finden, die verwendet werden kann. Dies bedeutet, dass die Wiederherstellung überprüft alle Datenquellen jedes Mal statt der Pakete, die bereits existieren im Ordner "Benutzer-Paket" online geschaltet. |
| **Häufige Ursachen** | Die Paketquellen enthalten nicht die erwartete Untergrenze-Version. Wenn das Paket erwartet nicht freigegeben wurde, kann dies ein Paket erstellen Fehler sein. |
| **Beispiel-Nachricht** | Im NuGet.Packaging 4.0.0 hängt NuGet.Versioning (> = 4.0.0) aber 4.0.0 wurde nicht gefunden. Eine ungefähre beste Übereinstimmung der 5.0.0 wurde aufgelöst. |

### <a name="nu1604"></a>NU1604

| | |
| --- | --- |
| **Problem** | Projektabhängigkeit nicht mit eine unteren Grenze definiert.<br/><br/>Dies bedeutet, dass die Wiederherstellung wurde nicht gefunden. die *beste Übereinstimmung*. Jede Wiederherstellung wird float abwärts versuchen, eine niedrigere Version zu finden, die verwendet werden kann. Dies bedeutet, dass die Wiederherstellung überprüft alle Datenquellen jedes Mal statt der Pakete, die bereits existieren im Ordner "Benutzer-Paket" online geschaltet. |
| **Häufige Ursachen** | Des Projekts *PackageReference* *Version* Attribut aktualisiert werden soll, um eine Untergrenze einzuschließen. |
| **Beispiel-Nachricht** | *Abhängigkeit NuGet.Versioning Projekt (< = 9.0.0) Doe keine inklusive untere Grenze enthalten. Schließen Sie eine untere Grenze in die Version der Abhängigkeit, Wiederherstellung konsistente Ergebnisse sicherzustellen.* |

### <a name="nu1605"></a>NU1605

| | |
| --- | --- |
| **Problem** | Eine abhängigkeitspakets angegeben, eine versionseinschränkung für eine spätere Version eines Pakets als wiederherstellen, die letztlich aufgelöst. |
| **Häufige Ursachen** | Nächste Wins beim Auflösen von Paketen. Ein näher Paket im Diagramm möglicherweise ein entfernten Paket außer Kraft gesetzt haben. |
| **Beispiel-Nachricht** | *Downgrade für die Paket erkannt: NuGet.Versioning aus 4.0.0 auf 3.5.0. Verweisen auf das Paket direkt aus dem Projekt eine andere Version auswählen.<br/>  NuGet.Packaging 3.5.0 -> NuGet.Versioning 3.5.0<br/>  NuGet.Commands 4.0.0 -> NuGet.Configuration 4.0.0 -> NuGet.Versioning 4.0.0* |

## <a name="resolver-conflict-warnings"></a>Konfliktlöser Konflikt Warnungen

### <a name="nu1608"></a>NU1608

| | |
| --- | --- |
| **Problem** | Ein Resolve-Paket ist größer als eine Abhängigkeit Einschränkung zulässt. In einigen Fällen ist dies beabsichtigt, und die Warnung unterdrückt werden kann. |
| **Häufige Ursachen** | Ein Paket auf die direkt von einem Projekt verwiesen wird, werden Einschränkungen der Abhängigkeit von anderen Paketen überschrieben.   |
| **Beispiel-Nachricht** | *Erkannte Paketversion außerhalb Abhängigkeit Einschränkung: x 1.0.0 erfordert y (= 1.0.0), aber Version y 2.0.0 aufgelöst wurde.* |

## <a name="package-fallback-warnings"></a>Paket-fallback-Warnungen

### <a name="nu1701"></a>NU1701

| | |
| --- | --- |
| **Problem** | *PackageTargetFallback/AssetTargetFallback* wurde verwendet, um Ressourcen aus einem Paket auszuwählen. Dies ist eine Warnung, damit der Benutzer wissen, dass die Ressourcen nicht 100 % kompatibel sein. |
| **Häufige Ursachen** | Das Paket unterstützt nicht das Framework des Projekts. |
| **Beispiel-Nachricht** | *Paket "NuGet.Versioning" wurde mit "Portable net45 + win8" stattdessen das Zielframework des Projekts "netstandard1.5" wiederhergestellt. Dieses Paket möglicherweise nicht vollständig kompatibel ist, während das Projekt.* |

## <a name="feed-warnings"></a>Feed-Warnungen

### <a name="nu1801"></a>NU1801

| | |
| --- | --- |
| **Problem** | Fehler beim Lesen von Feeds beim `IgnoreFailedSources` festgelegt ist auf "true", und konvertieren ihn in eine schwerwiegende Warnung. Dies kann eine beliebige Nachricht enthalten und ist generisch. |
| **Häufige Ursachen** | Die Quelle ist ungültig. |
| **Beispiel-Nachricht** | n/v |

## <a name="nuget-internal-errors-and-warnings"></a>NuGet-interne Fehler und Warnungen

[NU1000](#nu1000) | [NU1500](#nu1500)

### <a name="nu1000"></a>NU1000

| | |
| --- | --- |
| **Problem** | Ein nicht spezifizierter interne Fehler von NuGet. |
| **Häufige Ursachen** | Überprüfen Sie die Ereignisprotokolle auf Weitere Informationen |

### <a name="nu1500"></a>NU1500

| | |
| --- | --- |
| **Problem** | Eine nicht bestimmte interne Warnung von NuGet. |
| **Häufige Ursachen** | Überprüfen Sie die Ereignisprotokolle auf Weitere Informationen |
