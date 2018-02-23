---
title: NuGet 1.2 Versionshinweise | Microsoft Docs
author: karann-msft
ms.author: karann-msft
manager: ghogen
ms.date: 11/11/2016
ms.topic: article
ms.prod: nuget
ms.technology: 
description: "Versionshinweise für NuGet 1.2 einschließlich bekannte Probleme, Fehlerbehebungen, Funktionen und Archivierung von dcrs Design."
keywords: "NuGet 1.2 Anmerkungen zu dieser Version, aufgrund von Fehlerbehebungen, bekannte Probleme, zusätzliche Funktionen, Archivierung von dcrs Design"
ms.reviewer:
- karann-msft
- unniravindranathan
ms.openlocfilehash: 9c8fff67eb61ab673eb62113e0cc46c0868be237
ms.sourcegitcommit: 7969f6cd94eccfee5b62031bb404422139ccc383
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 02/20/2018
---
# <a name="nuget-12-release-notes"></a>NuGet 1.2-Versionshinweise

[NuGet-Hinweise mit dem Version 1.0 und 1.1](../release-notes/nuget-1.1.md) | [NuGet 1.3-Versionshinweise](../release-notes/nuget-1.3.md)

NuGet 1.2 wurde am 30. März 2011 veröffentlicht.

## <a name="new-features"></a>Neue Funktionen

### <a name="framework-profile-support"></a>Framework-Profil-Unterstützung

Vom Start und NuGet unterstützt mit verschiedenen Frameworks als Ziel Bibliotheken. Aber jetzt Pakete Assemblys, die bestimmte Profile z. B. das Profil für Windows Phone abzielen enthalten können. Um ein bestimmtes Profil von einem Framework als Ziel festzulegen, fügen Sie einen Bindestrich gefolgt von der Abkürzung Profil. Zum Ausführen auf einem Windows Phone (aka Windows Phone 7) SilverLight als Zielversion festlegen, können Sie z. B. eine Assembly im Ordner "3 wp" wie im folgenden Screenshot gezeigt einfügen.

![Framework-Profil-Ordnerstruktur](./media/framework-profile-support.png)

Sie Fragen sich vielleicht warum wir einfach aus gewählt haben, verwenden Sie "wp7" als Moniker. Wir sind teilweise vorhersehen, dass Windows Phone 7 möglicherweise in Zukunft eine neuere Version von Silverlight ausgeführt werden, in diesem Fall müssen Sie möglicherweise finden Sie spezifischere Informationen zu der Framework erstellen ein Profil werden Anwendung sind.

### <a name="automatically-add-binding-redirects"></a>Fügen Sie Bindungsumleitungen automatisch hinzu.

Beim Installieren eines Pakets mit Assemblys mit starkem Namen kann NuGet jetzt Fälle erkennen, in denen das Projekt bindungsumleitungen erfordert hinzugefügt werden, in die Konfigurationsdatei in der Reihenfolge für das Projekt kompiliert und automatisch hinzugefügt. Teil 3 von David Ebbos blogreihe auf NuGet-Versioning Anspruch "[Vereinheitlichung über binden leitet](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)" werden den Zweck dieser Funktion ausführlicher behandelt.

<a name="framework-assembly-refs"></a>

### <a name="specifying-framework-assembly-references-gac"></a>Framework-Assemblyverweise (GAC) angeben

In einigen Fällen kann ein Paket von einer Assembly abhängen, die in .NET Framework enthalten ist. Streng genommen ist es nicht immer notwendig, dass der Consumer des Pakets die Framework-Assembly verweisen. Aber in einigen Fällen ist es wichtig, z. B. wenn der Entwickler für die Typen in dieser Assembly codiert werden, um das Paket zu verwenden muss. Die neue `frameworkAssemblies` Element, ein untergeordnetes Element des Elements Metadaten können Sie an einen Satz von `frameworkAssembly` Elemente, die auf ein Framework-Assembly im globalen Assemblycache verweist. Beachten Sie, liegt den Schwerpunkt auf Framework-Assembly.
Diese Assemblys sind nicht im Paket enthalten, da sie davon sind auf jedem Computer als Teil von .NET Framework verwendet werden soll. Die folgende Tabelle enthält die Attribute der `frameworkAssembly` Element.


|Attribut |Beschreibung|
|----------------|-----------|
|**assemblyName**|*Erforderliche*. Name der Assembly, z. B. `System.Net`.|
|**targetFramework**|*Optionale*. Ermöglicht die Angabe ein Framework und Profile-Name (oder Alias), die diese Frameworkassembly betrifft, z. B. "net40" oder "sl4". Verwendet das gleiche Format, die in beschriebenen [unterstützen mehrere Zielframeworks](../create-packages/supporting-multiple-target-frameworks.md).|

```xml
  <frameworkAssemblies>
    <frameworkAssembly assemblyName="System.ComponentModel.DataAnnotations" targetFramework="net40" />
    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
  </frameworkAssemblies>
```

### <a name="nugetexe-now-is-able-to-store-api-key-credentials"></a>NuGet.exe kann nun um API-Schlüssel-Anmeldeinformationen zu speichern

Wenn Sie das Befehlszeilentool nuget.exe verwenden, können Sie jetzt die SetApiKey-Befehl verwenden, um Ihren API-Schlüssel zu speichern. Auf diese Weise wird nicht müssen Sie ihn jedes Mal, wenn Sie ein Paket push angeben. Weitere Informationen zum Speichern von Ihren API-Schlüssels mit nuget.exe [lesen Sie die Dokumentation zum Veröffentlichen eines Pakets](../create-packages/publish-a-package.md).

### <a name="package-explorer"></a>Paket-Explorer
Paket-Explorer wurde zur Unterstützung von NuGet 1.2 aktualisiert. Weitere Informationen finden Sie die [Anmerkungen zur Version des Paket-Explorer](http://nuget.codeplex.com/wikipage?title=New%20features%20in%20NuGet%20Package%20Explorer%201.0).

## <a name="other-featuresfixes"></a>Andere Features/Updates

Die vorherige Liste unter wurden am deutlichsten viele Funktionen, die wir implementiert und Fehlern, die wir behoben. Alles in allem wir implementiert/fixed [59 Typen von Arbeitsaufgaben](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.2&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0) in dieser Version.

## <a name="known-issues"></a>Bekannte Probleme

* **1.2 Paket Inkompatibilität**: Pakete, erstellt wurden, mit der neuesten Version des des-Befehlszeilentools, nuget.exe (> 1.2) funktioniert nicht mit älteren Versionen des NuGet-VS-Add-Ins (z. B. 1.1). Wenn Sie eine Fehlermeldung zu inkompatible Schema auftreten, werden Sie in dieser Fehler ausgeführt. Aktualisieren Sie NuGet, auf die neueste Version.
* **NuGet.Server in Inkompatibilität**: Wenn Sie eine interne NuGet feed mithilfe des Projekts NuGet.Server in hosten, müssen Sie mit der neuesten Version des NuGet.Server in diesem Projekt zu aktualisieren.
* **Es besteht ein Konflikt Signaturfehler**: Wenn ein Fehler während eines Upgrades mit einer Meldung über eine Signatur besteht ein Konflikt auftreten, müssen Sie NuGet zunächst deinstallieren und installieren Sie es. Diese wird aufgelistet, unserem [Seite "Bekannte Probleme"](../release-notes/known-issues.md) stellt weitere Details. Das Problem nur wirkt sich auf die Visual Studio 2010 SP1 ausführen und haben Version 1.0 von NuGet installiert, die nicht ordnungsgemäß signiert wurde. Diese Version wurde nur zur Verfügung gestellt von der CodePlex-Website für einen kurzen Zeitraum so viele Benutzer sollten nicht von diesem Problem betroffen.