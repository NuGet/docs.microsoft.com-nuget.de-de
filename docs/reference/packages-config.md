---
title: Verweis auf die Datei "nuget Packages. config"
description: Bei einigen Projekttypen wird in der Datei „packages.config“ die Liste der im Projekt verwendeten Pakete verwaltet.
author: karann-msft
ms.author: karann
ms.date: 05/21/2018
ms.topic: reference
ms.openlocfilehash: 3665989d35d7362b30a106cf6b4ed0210619efee
ms.sourcegitcommit: c81561e93a7be467c1983d639158d4e3dc25b93a
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 03/02/2020
ms.locfileid: "78230567"
---
# <a name="packagesconfig-reference"></a>Verweis auf „packages.config“

Die Datei `packages.config` wird bei einigen Projekttypen für die Verwaltung der Pakete verwendet, auf die vom Projekt verwiesen wird. Auf diese Weise kann NuGet die Projektabhängigkeiten problemlos wiederherstellen, wenn das Projekt ohne all diese Pakete auf ein anderes System, z.B. einen Buildserver, übertragen werden soll.

Wenn Sie verwendet wird, befindet sich `packages.config` in der Regel in einem Projektstamm Verzeichnis. Sie wird automatisch erstellt, wenn der erste nuget-Vorgang ausgeführt wird. Sie kann jedoch auch manuell erstellt werden, bevor Befehle wie `nuget restore`ausgeführt werden.

Projekte, die [packagereferenzierung](../consume-packages/Package-References-in-Project-Files.md) verwenden, verwenden keine `packages.config`.

## <a name="schema"></a>Schema

Das Schema ist einfach: Dem XML-Standardheader folgt ein `<packages>`-Einzelknoten, der mindestens ein `<package>`-Element enthält (jeweils eines für jeden Verweis). Jedes `<package>`-Element kann die folgenden Attribute aufweisen:

| attribute | Erforderlich | BESCHREIBUNG |
| --- | --- | --- |
| id | Ja | Der Bezeichner des Pakets, z.B. „Newtonsoft.json“ oder „Microsoft.AspNet.Mvc“. | 
| version | Ja | Die genaue Version des zu installierenden Pakets, z.B. 3.1.1 oder 4.2.5.11-beta. Eine Versionszeichenfolge muss mindestens drei Ziffern aufweisen, eine vierte Ziffer und ein Vorabreleasesuffix sind optional. Bereiche sind nicht zulässig. | 
| targetFramework | Nein  | Der [Zielframeworkmoniker](target-frameworks.md) (Target Framework Moniker, TFM), der bei der Installation des Pakets angewendet werden soll. Er wird bei der Installation eines Pakets zuerst auf das Projektziel festgelegt. Dadurch können unterschiedliche `<package>`-Elemente unterschiedliche TFMs aufweisen. Wenn Sie beispielsweise ein Projekt erstellen, das für .NET 4.5.2 erstellt wurde, verwenden an diesem Punkt installierte Pakete den TFM von net452. Wenn Sie das Projekt später dem neuen Ziel .NET 4.6 zuweisen und weitere Pakete hinzufügen, verwenden diese den TFM von net46. Bei einer fehlenden Übereinstimmung zwischen dem Projektziel und den `targetFramework`-Attributen werden Warnungen generiert. In diesem Fall können Sie die betroffenen Pakete erneut installieren. | 
| allowedVersions | Nein  | Ein Bereich mit zulässigen Versionen für dieses Paket, die während der Paketaktualisierung angewendet werden (weitere Informationen finden Sie unter [Constraining upgrade versions (Einschränkung von Upgradeversionen)](../consume-packages/reinstalling-and-updating-packages.md#constraining-upgrade-versions)). Dies hat *keine* Auswirkungen darauf, welches Paket während einer Installation oder Wiederherstellung installiert wird. Die Syntax finden Sie unter [Paketversionsverwaltung](../concepts/package-versioning.md#version-ranges). Die Benutzeroberfläche von PackageManager deaktiviert auch alle Versionen außerhalb des zulässigen Bereichs. | 
| developmentDependency | Nein  | Wenn im verwendeten Projekt selbst ein NuGet-Paket erstellt wird, wird durch eine Festlegung des Pakets auf `true` bei einer Abhängigkeit verhindert, dass das Paket bei der Erstellung des verwendeten Projekts eingeschlossen wird. Der Standardwert lautet `false`. | 

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
