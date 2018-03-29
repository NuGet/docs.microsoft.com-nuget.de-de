---
title: Verweis auf NuGet-Datei „packages.config“ | Microsoft-Dokumentation
author: kraigb
ms.author: kraigb
manager: ghogen
ms.date: 12/07/2017
ms.topic: reference
ms.prod: nuget
ms.technology: ''
description: Bei einigen Projekttypen wird in der Datei „packages.config“ die Liste der im Projekt verwendeten Pakete verwaltet.
keywords: NuGet-Datei „packages.config“, NuGet-Paketverweise, NuGet-Abhängigkeiten
ms.reviewer:
- karann-msft
- unniravindranathan
ms.workload:
- dotnet
- aspnet
ms.openlocfilehash: 38d4724d25476d372a936cb8ebf08e2b53fcf9f4
ms.sourcegitcommit: beb229893559824e8abd6ab16707fd5fe1c6ac26
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/28/2018
---
# <a name="packagesconfig-reference"></a>Verweis auf „packages.config“

Die Datei `packages.config` wird bei einigen Projekttypen für die Verwaltung der Pakete verwendet, auf die vom Projekt verwiesen wird. Auf diese Weise kann NuGet die Projektabhängigkeiten problemlos wiederherstellen, wenn das Projekt ohne all diese Pakete auf ein anderes System, z.B. einen Buildserver, übertragen werden soll.

## <a name="schema"></a>Schema

Das Schema ist einfach: Dem XML-Standardheader folgt ein `<packages>`-Einzelknoten, der mindestens ein `<package>`-Element enthält (jeweils eines für jeden Verweis). Jedes `<package>`-Element kann die folgenden Attribute aufweisen:

| Attribut | Erforderlich | Beschreibung |
| --- | --- | --- |
| ID | Ja | Der Bezeichner des Pakets, z.B. „Newtonsoft.json“ oder „Microsoft.AspNet.Mvc“. | 
| Version | Ja | Die genaue Version des zu installierenden Pakets, z.B. 3.1.1 oder 4.2.5.11-beta. Eine Versionszeichenfolge muss mindestens drei Ziffern aufweisen, eine vierte Ziffer und ein Vorabreleasesuffix sind optional. Bereiche sind nicht zulässig. | 
| targetFramework | Nein | Der [Zielframeworkmoniker](target-frameworks.md) (Target Framework Moniker, TFM), der bei der Installation des Pakets angewendet werden soll. Er wird bei der Installation eines Pakets zuerst auf das Projektziel festgelegt. Dadurch können unterschiedliche `<package>`-Elemente unterschiedliche TFMs aufweisen. Wenn Sie beispielsweise ein Projekt erstellen, das für .NET 4.5.2 erstellt wurde, verwenden an diesem Punkt installierte Pakete den TFM von net452. Wenn Sie das Projekt später dem neuen Ziel .NET 4.6 zuweisen und weitere Pakete hinzufügen, verwenden diese den TFM von net46. Bei einer fehlenden Übereinstimmung zwischen dem Projektziel und den `targetFramework`-Attributen werden Warnungen generiert. In diesem Fall können Sie die betroffenen Pakete erneut installieren. | 
| allowedVersions | Nein | Ein Bereich mit zulässigen Versionen für dieses Paket, die während der Paketaktualisierung angewendet werden (weitere Informationen finden Sie unter [Constraining upgrade versions (Einschränkung von Upgradeversionen)](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions)). Dies hat *keine* Auswirkungen darauf, welches Paket während einer Installation oder Wiederherstellung installiert wird. Die Syntax finden Sie unter [Paketversionsverwaltung](../reference/package-versioning.md#version-ranges-and-wildcards). Die Benutzeroberfläche von PackageManager deaktiviert auch alle Versionen außerhalb des zulässigen Bereichs. | 
| developmentDependency | Nein | Wenn im verwendeten Projekt selbst ein NuGet-Paket erstellt wird, wird durch eine Festlegung des Pakets auf `true` bei einer Abhängigkeit verhindert, dass das Paket bei der Erstellung des verwendeten Projekts eingeschlossen wird. Die Standardeinstellung ist `false`. | 

## <a name="examples"></a>Beispiele

Die folgende Datei `packages.config` bezieht sich auf zwei Abhängigkeiten:

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
  <package id="jQuery" version="3.1.1" targetFramework="net46" />
  <package id="NLog" version="4.3.10" targetFramework="net46" />
</packages>
```

Die folgende Datei `packages.config` bezieht sich auf neun Pakete, bei der Erstellung des Verbrauchspakets wird `Microsoft.Net.Compilers` jedoch aufgrund des Attributs `developmentDependency` nicht eingeschlossen. Durch den Verweis auf die Datei „Newtonsoft.Json“ werden Updates zudem nur auf die Versionen 8.x und 9.x beschränkt.

```xml
<?xml version="1.0" encoding="utf-8"?>
<packages>
  <package id="Microsoft.CodeDom.Providers.DotNetCompilerPlatform" version="1.0.0" targetFramework="net46" />
  <package id="Microsoft.Net.Compilers" version="1.0.0" targetFramework="net46" developmentDependency="true" />
  <package id="Microsoft.Web.Infrastructure" version="1.0.0.0" targetFramework="net46" />
  <package id="Microsoft.Web.Xdt" version="2.1.1" targetFramework="net46" />
  <package id="Newtonsoft.Json" version="8.0.3" allowedVersions="[8,10)" targetFramework="net46" />
  <package id="NuGet.Core" version="2.11.1" targetFramework="net46" />
  <package id="NuGet.Server" version="2.11.2" targetFramework="net46" />
  <package id="RouteMagic" version="1.3" targetFramework="net46" />
  <package id="WebActivatorEx" version="2.1.0" targetFramework="net46" />
</packages>
```
