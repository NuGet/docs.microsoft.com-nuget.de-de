---
title: Was geschieht bei der Paketinstallation?
description: Detaillierte Informationen zum Vorgang der Paketinstallation
author: JonDouglas
ms.author: jodou
ms.date: 06/20/2019
ms.topic: conceptual
ms.openlocfilehash: 2a16c1cfe1ada0d1a78cefcdb2bdc69b9c6e84cf
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775093"
---
# <a name="what-happens-when-a-nuget-package-is-installed"></a>Was geschieht beim Installieren eines NuGet-Pakets?

Die verschiedenen NuGet-Tools erstellen typischerweise einen Verweis auf ein Paket in der Projektdatei oder `packages.config` und führen dann eine Paketwiederherstellung durch, die das Paket effektiv installiert. `nuget install` ist die Ausnahme, bei der das Paket nur in einen `packages`-Ordner erweitert wird, andere Dateien jedoch unverändert bleiben.

Im Allgemeinen läuft der Prozess wie folgt ab:

1. Der Paketbezeichner und die Paketversion werden in der Projektdatei oder `packages.config` aufgezeichnet (gilt für alle Tools mit Ausnahme von `nuget.exe`).

   Wenn als Installationstool Visual Studio oder die dotnet-CLI verwendet werden, wird zunächst versucht, das Paket zu installieren. Falls eine Inkompatibilität vorliegt, wird das Paket nicht zur Projektdatei oder zu `packages.config` hinzugefügt.

2. Erhalten des Pakets:
   - Überprüfen Sie, ob das Paket (mit exaktem Bezeichner und Versionsnummer) bereits im Ordner *global-packages* installiert ist, wie unter [Verwalten der globalen Paketordner und Cacheordner](../consume-packages/managing-the-global-packages-and-cache-folders.md) beschrieben.

   - Wenn sich das Paket nicht im Ordner *global-packages* befindet, versuchen Sie, es aus den in den [Konfigurationsdateien](../consume-packages/Configuring-NuGet-Behavior.md) aufgelisteten Quellen abzurufen. Bei Onlinequellen wird zunächst versucht, das Paket aus dem HTTP-Cache abzurufen, es sei denn, `-NoCache` wird mit `nuget.exe`-Befehlen oder `--no-cache` mit `dotnet restore` angegeben. (Visual Studio und `dotnet add package` verwenden immer den Cache.) Wenn ein Paket aus dem Cache verwendet wird, erscheint „CACHE“ in der Ausgabe. Die Ablaufzeit des Caches beträgt 30 Minuten.

   - Wenn das Paket mithilfe einer [unverankerten Version](../consume-packages/Package-References-in-Project-Files.md#floating-versions) angegeben wurde oder ohne Mindestversion, *kontaktiert NuGet* alle Quellen, um die beste Übereinstimmung zu finden.
   Beispiel: `1.*`, `(, 2.0.0]`.

   - Wenn sich das Paket nicht im HTTP-Cache befindet, wird versucht, es aus den in der Konfiguration aufgeführten Quellen herunterzuladen. Wird ein Paket heruntergeladen, erscheinen „GET“ und „OK“ in der Ausgabe. NuGet protokolliert den HTTP-Datenverkehr mit normaler Ausführlichkeit.

   - Wenn das Paket nicht erfolgreich aus einer Quelle bezogen werden kann, tritt bei der Installation an dieser Stelle ein Fehler auf, z.B. [NU1103](../reference/errors-and-warnings/NU1103.md). Beachten Sie, dass Fehler von `nuget.exe`-Befehlen nur die zuletzt geprüfte Quelle anzeigen, aber implizieren, dass das Paket aus keiner Quelle abgerufen werden konnte.

   Beim Beziehen des Pakets gilt möglicherweise die Reihenfolge der Quellen in der NuGet-Konfiguration:

   - NuGet überprüft zuerst die lokalen Ordner und Netzwerkfreigaben der Quellen und dann erst HTTP-Quellen.

3. Speicherung einer Kopie des Pakets und anderer Informationen im Ordner *http-cache*, wie unter [Verwalten der globalen Paketordner und Cacheordner](../consume-packages/managing-the-global-packages-and-cache-folders.md) beschrieben.

4. Wenn Sie das Paket heruntergeladen haben, installieren Sie es pro Benutzer im Ordner *global-packages*. NuGet erstellt einen Unterordner für jeden Paketbezeichner und erstellt dann Unterordner für jede installierte Version des Pakets.

5. NuGet installiert bei Bedarf Paketabhängigkeiten. Möglicherweise werden bei diesem Prozess Paketversionen im Prozess aktualisiert, wie in [Abhängigkeitsauflösung](../concepts/dependency-resolution.md) beschrieben.

6. Aktualisieren Sie andere Projektdateien und -ordner:

    - Bei Projekten, die PackageReference verwenden, aktualisieren Sie das in `obj/project.assets.json` gespeicherte Abhängigkeitsdiagramm für das Paket. Paketinhalte selbst werden nicht in einen Projektordner kopiert.
    - Aktualisieren Sie `app.config` und/oder `web.config`, wenn das Paket [Transformationen von Quell- und Konfigurationsdateien](../create-packages/source-and-config-file-transformations.md) verwendet.

7. (Nur Visual Studio) Zeigt die Infodatei des Pakets, falls vorhanden, in einem Visual Studio-Fenster.

Nutzen Sie NuGet-Pakete, um produktiv zu programmieren.
