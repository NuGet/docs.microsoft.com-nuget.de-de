---
title: Anmerkungen zu NuGet Version 1.2
description: Anmerkungen zu NuGet 1.2, einschließlich der bekannten Probleme, Fehlerkorrekturen, hinzugefügter Features und DCRs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: b47f73c1c225540226d3780e17053427b8ea4a8a
ms.sourcegitcommit: 1d1406764c6af5fb7801d462e0c4afc9092fa569
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 09/04/2018
ms.locfileid: "43545686"
---
# <a name="nuget-12-release-notes"></a>Anmerkungen zu NuGet Version 1.2

[Anmerkungen zu NuGet 1.0 und 1.1](../release-notes/nuget-1.1.md) | [Anmerkungen zu NuGet 1.3](../release-notes/nuget-1.3.md)

NuGet 1.2 wurde am 30. März 2011 veröffentlicht.

## <a name="new-features"></a>Neue Funktionen

### <a name="framework-profile-support"></a>Framework-Profil-Unterstützung

Von Anfang NuGet unterstützt mit Bibliotheken verschiedene Zielframeworks. Aber jetzt Pakete Assemblys, die spezifischen Profil, z. B. das Windows Phone-Profil als Ziel enthalten können. Um ein bestimmtes Profil eines Frameworks als Ziel festzulegen, fügen Sie einen Gedankenstrich, gefolgt von der Abkürzung Profil ein. Um eine Windows Phone (auch bekannt als Windows Phone 7) unter SilverLight als Zielversion festlegen, können Sie z. B. eine Assembly im Ordner "3-wp" wie im folgenden Screenshot gezeigt einfügen.

![Ordnerlayout für Framework-Profil](./media/framework-profile-support.png)

Sie Fragen sich vielleicht warum wir einfach nicht "wp7" als Moniker verwenden möchten. Teilweise sind wir erwarten, dass Windows Phone 7 möglicherweise eine neuere Version von Silverlight in der Zukunft ausgeführt, die in diesem Fall müssen Sie möglicherweise spezifischer über welches Framework Sie erstellen ein Profil sind abzielt.

### <a name="automatically-add-binding-redirects"></a>Fügen Sie Bindungsumleitungen automatisch hinzu.

Wenn ein Paket mit Assemblys mit starkem Namen installieren möchten, kann NuGet nun Fälle zu erkennen, in dem das Projekt erfordert bindungsumleitungen in die Konfigurationsdatei in der Reihenfolge für das Projekt zu kompilieren, und fügen sie automatisch hinzugefügt werden. Teil 3 von David Ebbos blogreihe zur NuGet-Versionsverwaltung berechtigt "[Vereinheitlichung über Datenbindung leitet](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)" den Zweck dieser Funktion ausführlicher behandelt.

<a name="framework-assembly-refs"></a>

### <a name="specifying-framework-assembly-references-gac"></a>Verweise auf Frameworkassemblys (GAC) angeben

In einigen Fällen kann ein Paket von einer Assembly abhängen, die in .NET Framework ist. Genau genommen ist es nicht immer erforderlich, dass der Consumer des Pakets die Framework-Assembly verweisen. Aber in einigen Fällen ist es wichtig, wie z. B. wenn der Entwickler für Typen in dieser Assembly programmieren können, um das Paket zu verwenden muss. Die neue `frameworkAssemblies` Element ein untergeordnetes Element des Elements Metadaten können Sie eine Reihe von angeben `frameworkAssembly` Elemente, die auf einer Framework-Assembly im globalen Assemblycache verweist. Beachten Sie den Schwerpunkt auf Framework-Assembly.
Diese Assemblys sind nicht im Paket enthalten, da davon ausgegangen wird auf jedem Computer als Teil von .NET Framework verwendet werden soll. Die folgende Tabelle enthält die Attribute der `frameworkAssembly` Element.


|Attribut |Beschreibung|
|----------------|-----------|
|**assemblyName**|*Erforderliche*. Name der Assembly, z. B. `System.Net`.|
|**targetFramework**|*Optionale*. Ermöglicht es Ihnen, ein Framework und Profile-Name (oder Alias), die dieses Framework-Assembly, z. B. "net40" oder "sl4" gilt. Verwendet das gleiche Format, die in beschriebenen [unterstützen mehrerer Zielframeworks](../create-packages/supporting-multiple-target-frameworks.md).|

```xml
  <frameworkAssemblies>
    <frameworkAssembly assemblyName="System.ComponentModel.DataAnnotations" targetFramework="net40" />
    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
  </frameworkAssemblies>
```

### <a name="nugetexe-now-is-able-to-store-api-key-credentials"></a>NuGet.exe kann jetzt zum Speichern von Anmeldeinformationen von API-Schlüssel

Wenn Sie das Befehlszeilentool nuget.exe verwenden zu können, jetzt können den Befehl "SetApiKey" Sie um Ihren API-Schlüssel zu speichern. Auf diese Weise müssen Sie nicht jedes Mal, wenn Sie ein Paket per Push übertragen angegeben. Weitere Informationen zum Speichern von Ihren API-Schlüssels bei nuget.exe [finden Sie in der Dokumentation zum Veröffentlichen eines Pakets](../create-packages/publish-a-package.md).

### <a name="package-explorer"></a>Paket-Explorer
Paket-Explorer wurde zur Unterstützung von NuGet 1.2 aktualisiert. Weitere Informationen finden Sie in der [Paket-Explorer – Anmerkungen zu dieser](http://nuget.codeplex.com/wikipage?title=New%20features%20in%20NuGet%20Package%20Explorer%201.0).

## <a name="other-featuresfixes"></a>Weitere Features/Updates

Die vorherige Liste wurden die wichtigsten von den zahlreichen Features, die wir implementiert haben und Fehler, die wir behoben. Alles in allem ist es implementiert/fixed [59 Arbeitsaufgaben](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.2&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0) in dieser Version.

## <a name="known-issues"></a>Bekannte Probleme

* **1.2 Paket Inkompatibilität**: Pakete, die mit der neuesten Version des Tools über die Befehlszeile erstellt, nuget.exe (> 1.2) funktioniert nicht mit älteren Versionen des NuGet-VS-Add-Ins (z. B. 1.1). Wenn Sie eine Fehlermeldung etwas nicht kompatibles Schema wird feststellen, führen Sie diesen Fehler. Aktualisieren Sie NuGet, auf die neueste Version.
* **"NuGet.Server" Inkompatibilität**: Wenn Sie einen internen NuGet-Feeds, mit dem Projekt "NuGet.Server" hosten, müssen Sie das Projekt mit der neuesten Version von "NuGet.Server" aktualisieren.
* **Signatur stimmt nicht überein. Fehler**: Wenn ein Fehler während eines Upgrades mit einer Meldung über eine Signatur Konflikt auftreten, müssen Sie NuGet zuerst deinstallieren und installieren Sie es. Dieser wird aufgeführt, unserem [bekannte Probleme Seite](../release-notes/known-issues.md) die finden Sie weitere Details. Das Problem nur wirkt sich auf jene, die Visual Studio 2010 SP1 ausführen und eine Version von NuGet 1.0 installiert, die nicht ordnungsgemäß signiert wurde. Diese Version wurde von der CodePlex-Website nur verfügbar gemacht für einen kurzen Zeitraum damit dieses Problem zu viele Entwickler nicht beeinträchtigen sollte.