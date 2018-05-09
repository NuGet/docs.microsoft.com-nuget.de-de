---
title: Auswirkungen von project.json auf Ersteller von NuGet-Paketen
description: Informationen darüber, was die Implementierung von „project.json“ in NuGet 3.x für Paketersteller bedeutet, z.B. nicht unterstützte Features und Paketformate sowie nicht unterstützter Inhalt.
author: kraigb
ms.author: kraigb
manager: douge
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 6163297075f741a4132afd748974498fa1600fbb
ms.sourcegitcommit: 3eab9c4dd41ea7ccd2c28bb5ab16f6fbbec13708
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 04/26/2018
---
# <a name="impact-of-projectjson-when-creating-packages"></a>Auswirkungen von „project.json“ auf das Erstellen von Paketen

> [!Important]
> Dieser Inhalt ist veraltet. Projekte sollten entweder das Format `packages.config` oder das PackageReference-Format verwenden.

Das in NuGet 3 und höher verwendete System `project.json` wirkt sich, wie in den folgenden Abschnitten beschrieben, für Paketersteller auf verschiedene Arten aus.

## <a name="changes-affecting-existing-packages-usage"></a>Änderungen, die das Verwenden vorhandener Pakete betreffen

NuGet-Pakete unterstützen üblicherweise einige Features, die nicht in die transitive Welt übertragen werden.

### <a name="install-and-uninstall-scripts-are-ignored"></a>Installations- und Deinstallationsskripts werden ignoriert.

Dem Modell zur transitiven Wiederherstellung, das in einem anderen Artikel im Abschnitt zum Thema [Abhängigkeitsauflösung](../consume-packages/dependency-resolution.md#dependency-resolution-with-packagereference) beschrieben wird, ist das Konzept der „Paketinstallationszeit“ nicht bekannt. Ein Paket ist entweder vorhanden oder nicht vorhanden. Es existiert also kein einheitlicher Prozess, der beim Installieren eines Pakets abläuft.

Des Weiteren wurden Installationsskripts nur in Visual Studio unterstützt. Andere integrierte Entwicklungsumgebungen konnten nur durch Modellieren der Visual Studio-Erweiterbarkeits-API versuchen, solche Skripts zu unterstützen. In üblichen Editoren und Befehlszeilentools war dagegen keine Unterstützung verfügbar.

### <a name="content-transforms-are-not-supported"></a>Transformationen von Inhalten werden nicht unterstützt.

Transformationen werden, ähnlich wie Installationsskripts, mithilfe des Prozesses der Paketinstallation ausgeführt und sind in der Regel nicht idempotent. Da das Konzept der „Installationszeit“ nicht mehr vorhanden ist, werden XDT Transform und ähnliche Features nicht unterstützt. Diese werden ignoriert, wenn ein entsprechendes Paket in einem transitiven Szenario verwendet wird.

### <a name="content"></a>Inhalt

NuGet-Pakete transportieren üblicherweise Inhaltsdateien, z.B. Quellcode- und Konfigurationsdateien. Diese werden in der Regel in zwei Szenarios verwendet:

1. Als Startdateien, die im Projekt abgelegt werden, damit der Benutzer diese zu einem späteren Zeitpunkt bearbeiten kann. Ein gängiges Beispiel dafür sind Standardkonfigurationsdateien.

1. Inhaltsdateien, die als Ergänzung zu den im Projekt installierten Assemblys verwendet werden. Ein Beispiel dafür wäre ein Logobild, das von einer Assembly verwendet wird.

Die Unterstützung von Inhaltsdateien ist derzeit aus ähnlichen Gründen deaktiviert, wie der für Skripts und Transformationen. Wir arbeiten jedoch bereits an deren Bereitstellung.

Inhaltsdateien können weiterhin in Pakete übertragen werden, werden aber derzeit ignoriert. Benutzer können diese dennoch an die richtige Stelle kopieren.

Sie können einen der Vorschläge, wie Inhaltsdateien wieder eingebunden werden könnten, hier einsehen und seinen Fortschritt verfolgen: [https://github.com/NuGet/Home/issues/627](https://github.com/NuGet/Home/issues/627).

## <a name="impact-for-package-authors"></a>Auswirkungen für Paketersteller

Pakete, die auf die oben genannten Features zurückgreifen, müssen einen anderen Mechanismus verwenden. Der in den meisten Fällen für diesen Zweck geeignete Mechanismus wäre „MSBuild-Ziele und -Eigenschaften“, da dieser weiterhin vollständig unterstützt wird. Das Buildsystem kann auch andere Konventionen aus dem Paket übernehmen. Auf diese Weise werden MSBuild-Ziele sowie Roslyn-Analysetools unterstützt. Es ist möglich, Pakete zu erstellen, die Ziele und Analysetools für die Szenarios `packages.config` und `project.json` unterstützen.

Pakete, die darauf abzielen, das Projekt zum Erleichtern des Starts zu verändern, können meist nur in wenigen Szenarios verwendet werden. Daher sollten die Pakete stattdessen eine Infodatei oder Richtlinien zum Verwenden des Pakets bereitstellen.

Bei den meisten vorhandenen Paketen ist das Verwenden des unten beschriebenen Paketformats nicht erforderlich.

Das Format ermöglicht, dass nativer Inhalt in einem erstklassigen Szenario verwendet werden kann. Dies bedeutet, dass verwaltete Assemblys davon abhängig sind, dass hardwaregebundene Implementierungen binäre Implementierungen neben verwalteten Assemblys auf Grundlage der Zielplattform liefern. Das Paket „System.IO.Compression“ nutzt diese Technologie beispielsweise. [https://www.nuget.org/packages/System.IO.Compression](https://www.nuget.org/packages/System.IO.Compression)

Falls die oben genannte Funktionalität nicht unbedingt erforderlich ist, empfiehlt es sich also, bei dem bestehenden Paketformat zu bleiben, da das hier beschriebene Format nur von NuGet 3.x und höher unterstützt wird.

Mithilfe von Shims ist es möglich, Pakete zu erstellen, die sowohl in `packages.config`- als auch in `project.json`-Szenarios funktionieren. Jedoch ist es oft leichter, die Pakete auf herkömmliche Weise zu strukturieren – ohne die oben erwähnten veralteten Funktionen.

## <a name="3x-package-format"></a>Paketformat „3.x“

Das Paketformat „3.x“ lässt mehrere zusätzliche Funktionen zu, die NuGet 2.x nicht zulässt:

1. Definieren einer Referenzassembly, die für die Kompilierung verwendet wird und mehrerer Implementierungsassemblys, die für die Laufzeit auf verschiedenen Plattformen bzw. Geräten verwendet werden. Dies ermöglicht es Ihnen, plattformspezifische APIs zu verwenden und zeitgleich für Ihre Benutzer eine gemeinsam genutzte Oberfläche bereitzustellen. Dadurch wird Ihnen insbesondere das Schreiben von portablen Zwischenbibliotheken erleichtert.

1. Ermöglicht Paketen, auf Plattformen, z.B. Betriebssystemen oder CPU-Architektur, zu pivotieren

1. Ermöglicht das Trennen von plattformspezifischen Implementierungen, um Pakete in Ergänzungen zu verwandeln

1. Unterstützen nativer Abhängigkeiten
