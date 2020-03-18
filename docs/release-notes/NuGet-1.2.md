---
title: Anmerkungen zu dieser Version von nuget 1,2
description: Anmerkungen zu dieser Version von nuget 1,2 einschließlich bekannter Probleme, Fehlerbehebungen, hinzugefügter Features und dcrs.
author: karann-msft
ms.author: karann
ms.date: 11/11/2016
ms.topic: conceptual
ms.openlocfilehash: 5d10d6bf27614980a144c30c3af6f9892a109061
ms.sourcegitcommit: ddb52131e84dd54db199ce8331f6da18aa3feea1
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/16/2020
ms.locfileid: "79428366"
---
# <a name="nuget-12-release-notes"></a>Anmerkungen zu dieser Version von nuget 1,2

[Anmerkungen zu dieser Version von nuget 1,0 und 1,1](../release-notes/nuget-1.1.md) | Anmerkungen zu dieser [Version von nuget 1,3](../release-notes/nuget-1.3.md)

Nuget 1,2 wurde am 30. März 2011 veröffentlicht.

## <a name="new-features"></a>Neue Funktionen

### <a name="framework-profile-support"></a>Framework-Profil Unterstützung

Von Anfang an unterstützte nuget, dass Bibliotheken verschiedene Frameworks als Ziel haben. Jetzt können Pakete jedoch Assemblys enthalten, die bestimmte Profile wie das Windows Phone Profil als Ziel haben. Wenn Sie ein bestimmtes Profil eines Frameworks als Ziel haben, fügen Sie einen Bindestrich gefolgt von der Profil Abkürzung ein. Wenn Sie z. b. Silverlight als Ziel für eine Windows Phone (Windows Phone 7) ausführen möchten, können Sie eine Assembly in den Ordner "SL3-WP" einfügen, wie im folgenden Screenshot gezeigt.

![Layout des frameworkprofilordners](./media/framework-profile-support.png)

Vielleicht Fragen Sie sich, warum wir nicht einfach die Verwendung von "WP7" als Moniker gewählt haben. Wir gehen davon aus, dass Windows Phone 7 in Zukunft eine neuere Version von Silverlight ausführen kann. in diesem Fall müssen Sie möglicherweise genauer wissen, welches frameworkprofil Sie verwenden.

### <a name="automatically-add-binding-redirects"></a>Automatisches Hinzufügen von Bindungs Umleitungen

Wenn Sie ein Paket mit Assemblys mit starkem Namen installieren, kann nuget nun Fälle erkennen, in denen das Projekt Bindungs Umleitungen erfordert, die der Konfigurationsdatei hinzugefügt werden müssen, damit das Projekt kompiliert und automatisch hinzugefügt werden kann. Teil 3 der Blog Bereitstellung von David Ebbo in der nuget-Versionsverwaltung mit dem Titel "[Vereinheitlichung über Bindungs Umleitungen](http://blog.davidebbo.com/2011/01/nuget-versioning-part-3-unification-via.html)" behandelt den Zweck dieses Features im Detail.

<a name="framework-assembly-refs"></a>

### <a name="specifying-framework-assembly-references-gac"></a>Angeben von frameworkassemblyverweisen (GAC)

In einigen Fällen kann ein Paket von einer Assembly abhängen, die sich im .NET Framework befindet. Streng genommen ist es nicht immer erforderlich, dass der Consumer Ihres Pakets auf die FrameworkAssembly verweist. In einigen Fällen ist es jedoch wichtig, z. b. wenn der Entwickler Code für Typen in dieser Assembly programmieren muss, um das Paket zu verwenden. Das neue `frameworkAssemblies`-Element, ein untergeordnetes Element des Metadata-Elements, ermöglicht es Ihnen, eine Gruppe von `frameworkAssembly` Elementen anzugeben, die auf eine Frameworkassembly im GAC zeigen. Beachten Sie den Schwerpunkt auf Frameworkassemblys.
Diese Assemblys sind nicht in Ihrem Paket enthalten, da davon ausgegangen wird, dass Sie sich auf jedem Computer als Teil des .NET Framework befinden. In der folgenden Tabelle werden die Attribute des `frameworkAssembly`-Elements aufgelistet.


|attribute |BESCHREIBUNG|
|----------------|-----------|
|**assemblyName**|*Erforderlich*. Der Name der Assembly, z. b. `System.Net`.|
|**targetFramework**|*Optional:* Ermöglicht das Angeben eines Frameworks und Profil namens (oder Alias), auf den diese FrameworkAssembly angewendet wird, z. b. "net40" oder "SL4". Verwendet das gleiche Format wie bei der [Unterstützung mehrerer Ziel-Frameworks](../create-packages/supporting-multiple-target-frameworks.md).|

```xml
  <frameworkAssemblies>
    <frameworkAssembly assemblyName="System.ComponentModel.DataAnnotations" targetFramework="net40" />
    <frameworkAssembly assemblyName="System.ServiceModel" targetFramework="net40" />
  </frameworkAssemblies>
```

### <a name="nugetexe-now-is-able-to-store-api-key-credentials"></a>"nuget. exe" kann jetzt API-Schlüssel Anmelde Informationen speichern.

Wenn Sie das Befehlszeilen Tool "nuget. exe" verwenden, können Sie nun den Befehl "Set-Key" verwenden, um Ihren API-Schlüssel zu speichern. Auf diese Weise müssen Sie Sie nicht jedes Mal angeben, wenn Sie ein Paket pushen. Weitere Informationen zum Speichern Ihres API-Schlüssels mit "nuget. exe" [finden Sie in der Dokumentation zum Veröffentlichen eines Pakets](../nuget-org/publish-a-package.md).

### <a name="package-explorer"></a>Paket-Explorer
Der Paket-Explorer wurde aktualisiert, um nuget 1,2 zu unterstützen. Weitere Informationen finden Sie in den Anmerkungen zu dieser [Version des Paket-Explorers](http://nuget.codeplex.com/wikipage?title=New%20features%20in%20NuGet%20Package%20Explorer%201.0).

## <a name="other-featuresfixes"></a>Weitere Features/Korrekturen

Die vorherige Liste war das auffälligste der zahlreichen Features, die wir implementiert haben, und Fehler, die wir korrigiert haben. Insgesamt haben wir in dieser Version [59 Arbeitselemente](http://nuget.codeplex.com/workitem/list/advanced?keyword=&status=All&type=All&priority=All&release=NuGet%201.2&assignedTo=All&component=All&sortField=Votes&sortDirection=Descending&page=0) implementiert/korrigiert.

## <a name="known-issues"></a>Bekannte Probleme

* **1,2 Paket Inkompatibilität**: mit der neuesten Version des Befehlszeilen Tools ("nuget. exe" (> 1,2) erstellten Paketen können nicht mit älteren Versionen des nuget-vs-Add-Ins (z. b. 1,1) verwendet werden. Wenn eine Fehlermeldung angezeigt wird, die etwas über ein nicht kompatibles Schema angibt, wird dieser Fehler angezeigt. Aktualisieren Sie nuget auf die neueste Version.
* " **Nuget. Server" Inkompatibilität**: Wenn Sie einen internen nuget-Feed mit dem nuget. Server-Projekt verwenden, müssen Sie das Projekt mit der aktuellen Version von "nuget. Server" aktualisieren.
* **Fehler beim Signieren von Signaturen**: Wenn bei einem Upgrade ein Fehler auftritt, bei dem eine Meldung zu einer Signatur nicht übereinstimmt, müssen Sie zuerst nuget deinstallieren und dann installieren. Dies wird auf der [Seite "bekannte Probleme](../release-notes/known-issues.md) " aufgeführt, die weitere Details enthält. Das Problem betrifft nur diejenigen, die Visual Studio 2010 SP1 ausführen und eine Version von nuget 1,0 installiert haben, die falsch signiert wurde. Diese Version wurde nur für einen kurzen Zeitraum von der CodePlex-Website zur Verfügung gestellt, sodass dieses Problem nicht zu viele Personen betreffen sollte.