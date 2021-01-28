---
title: NuGet-Projektgovernance
description: Das Governancemodell für NuGet mit Rollen und Zuständigkeiten von Committern, Mitwirkenden und Benutzern.
author: JonDouglas
ms.author: jodou
ms.date: 01/18/2018
ms.topic: conceptual
ms.openlocfilehash: 2edaac0218dc936ea6bfe1814c0aab963028ea87
ms.sourcegitcommit: ee6c3f203648a5561c809db54ebeb1d0f0598b68
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2021
ms.locfileid: "98775590"
---
# <a name="nuget-governance"></a>NuGet-Governance

> Dieser Artikel basiert auf dem [Governancemodell des wohlmeinenden Diktators](http://www.oss-watch.ac.uk/resources/benevolentdictatorgovernancemodel) der University of Oxford. Es steht unter der Creative Commons-Lizenz [Namensnennung-Weitergabe unter gleichen Bedingungen 2.0 UK: England & Wales](http://creativecommons.org/licenses/by-sa/2.0/uk/).

Das NuGet-Projekt wird von einem wohlmeinenden Diktator geleitet und von der Community verwaltet. Das bedeutet, dass die Community aktiv an der täglichen Wartung des Projekts mitwirkt, aber die strategische Leitung dem wohlmeinenden Diktator zufällt. Im Zweifelsfall hat der wohlmeinende Diktator das letzte Wort.

Die Aufgabe des wohlmeinenden Diktators ist es, Uneinigkeit innerhalb der Community zu klären und sicherzustellen, dass das Projekt koordiniert bearbeitet wird. Es ist wiederum die Aufgabe der Community, dem wohlmeinenden Diktator die Entscheidungsfindung durch aktive Teilnahme und engagiertes Mitwirken zu ermöglichen.

## <a name="roles-and-responsibilities"></a>Rollen und Zuständigkeiten

An dieser Stelle werden vier Rollen beschrieben: der wohlmeinende Diktator, Committer, Mitwirkende und Benutzer.

### <a name="benevolent-dictator"></a>Wohlmeinender Diktator

Das NuGet-Kernteam weist selbst einen wohlmeinenden Diktator oder eine Projektleitung zu. Da die Community immer forken kann, ist das Team für die Community verantwortlich. Die Projektleitung muss die Community als Ganzes verstehen und sich bemühen, so viele unterschiedliche Bedürfnisse wie möglich zu erfüllen, während gleichzeitig das langfristige Bestehen des Projekts sichergestellt wird.

In vielerlei Hinsicht besteht die Rolle des wohlmeinenden Diktators weniger im Bestimmen als im Vermitteln. Der entscheidende Punkt ist, den Richtigen Verantwortung für das Projekt zu übertragen, während dieses wächst, sodass die Community gemeinsam die Idee der Projektleitung verwirklichen kann. Die Aufgabe der Projektleitung ist es, sicherzustellen, dass die Committers (siehe unten) die für das Projekt richtigen Entscheidungen treffen. Prinzipiell bedeutet dies, dass die Projektleitung nicht in deren Vorgehen eingreift, solange dieses der Strategie des Projekts entspricht.

Zusätzlich ist die Projektleitung die wichtigste bzw. die erste Anlaufstelle für NuGet für .NET Foundation-Mitarbeiter bei Geschäftsvorgängen wie der Domänenregistrierung und bei technischen Diensten (z.B. Codesignierung).

### <a name="committers"></a>Committers

Committers sind Mitwirkende, die nützliche Beiträge zu NuGet geleistet haben. Sie werden vom wohlmeinenden Diktator ernannt. Ab ihrer Ernennung sollen Committers sowohl Code direkt in das Repository schreiben als auch die Beiträge anderer überprüfen. Committers sind häufig Entwickler, können aber auch anderweitig zu einem Projekt beitragen.

Normalerweise konzentriert sich ein Committer auf einen bestimmten Aspekt des Projekts. Dabei bringt er wichtiges Fachwissen und ein umfassendes Verständnis mit, die für das Projekt wesentlich sind. Die Rolle eines Committers ist keine offizielle Rolle, sondern eine Position, die einflussreiche Mitglieder der Community einnehmen, um die Projektleitung zu unterstützen.

Committers haben bei der Ausrichtung von NuGet keine Entscheidungsgewalt. Allerdings haben sie das Vertrauen der Projektleitung, die mit Fragen an sie herantritt. Committers sollen sicherstellen, dass die Projektleitung über die Bedürfnisse und die gemeinsamen Ziele der Community informiert ist, und sie sollen Beiträge zum Projekt leisten oder in die Wege leiten. Häufig erhalten Committers die inoffizielle Kontrolle über ihren Zuständigkeitsbereich, und ihnen werden Berechtigungen zum direkten Anpassen gewisser Abschnitte des Quellcodes erteilt. Das heißt also, dass Committers zwar keine Entscheidungsbefugnis haben, ihre Handlungen aber häufig mit den Entscheidungen der Projektleitung übereinstimmen.

### <a name="contributors"></a>Beitragende

Mitwirkende sind Mitglieder der Community, die Patches in NuGet einreichen. Diese Patches können sowohl einmal als auch mehrmals über einen längeren Zeitraum vorkommen. Es wird erwartet, dass Mitwirkende Patches einreichen, die zunächst klein sind und mit wachsendem Vertrauen des Mitwirkenden, der Committers und der Projektleitung in die Qualität von Patches des Mitwirkenden immer größer werden. Mitwirkende werden in den Anmerkungen zu der jeweiligen Version des Produkts anerkannt.

Bevor der erste Patch eines Mitwirkenden in das Repository aufgenommen wird, muss er eine [Lizenzvereinbarung für Mitwirkende](http://en.wikipedia.org/wiki/Contributor_License_Agreement) oder einen Abtretungsvertrag für .NET Foundation unterzeichnen. Der Patch kann eingereicht und besprochen werden, aber er kann ohne die entsprechenden Dokumente nicht im Repository committet werden. Senden Sie eine E-Mail an [contributions@nuget.org](mailto:contributions@nuget.org), um eine Lizenzvereinbarung für Mitwirkende anzufordern.

Reichen Sie einen Pull Request in einem der folgenden Repositorys ein, um Mitwirkender zu werden:

- [NuGet-Client](https://github.com/NuGet/NuGet.Client)
- [NuGet-Katalog](https://github.com/nuget/nugetgallery)
- [NuGet-Dokumente](https://github.com/nuget/nugetdocs)

Der genaue Prozess zum Einreichen eines Pull Requests unterscheidet sich je nach Repository:

- [Anweisungen zum Beitragen zum NuGet-Client und NuGet-Katalog](https://github.com/NuGet/Home/wiki/Contributing-to-NuGet)
- [Anweisungen zum Beitragen zu NuGet-Dokumenten](https://github.com/NuGet/NuGetDocs/wiki/Contributing-to-NuGet-Documentation)

### <a name="users"></a>Benutzer

Benutzer sind Mitglieder der Community, die NuGet benötigen und verwenden, sei es als Paketnutzer oder als -ersteller (oder beides). Benutzer sind die wichtigsten Mitglieder der Community, denn ohne sie hätte das Projekt keinen Nutzen. Jeder kann ein Benutzer sein. Es gibt keine besonderen Anforderungen.

Benutzer werden dazu angehalten, sich so viel wie möglich am Lebenszyklus von NuGet und an der Community zu beteiligen. Durch Beiträge von Benutzern kann das Projektteam sicherstellen, dass sie auf die Bedürfnisse der Benutzer eingehen. Zu üblichen Benutzeraktivitäten zählt u.a. Folgendes:

- das Einsetzen für den Gebrauch des Pakets
- das Melden der Stärken und Schwächen eines Projekt aus der Perspektive eines neuen Benutzers
- moralische Unterstützung (auch mal Danke sagen)
- Schreiben von Dokumentationen und Tutorials
- Einreichen von Problemberichten und Featureanforderungen
- die Teilname an Communityereignissen wie Bug Bashes
- das Beteiligen an Diskussionen oder in Foren

Wenn Benutzer sich fortlaufend an einem Projekt und der dazugehörigen Community beteiligen, wird ihre Beteiligung immer größer. Dann kann es sein, dass diese Benutzer wie oben beschrieben zu Mitwirkenden werden.

## <a name="package-succession-under-special-circumstances"></a>Nachfolge unter besonderen Umständen

Wenn der Besitzer eines NuGet-Kontos arbeitsunfähig ist oder verstirbt, versuchen wir in Zusammenarbeit mit der Community einen oder mehrere Nachfolger als Besitzer für Pakete zu finden, für die das betroffene Konto der alleinige Besitzer war und die unter einer [OSI-genehmigten Lizenz](https://opensource.org/licenses/alphabetical) veröffentlicht wurden. Um den Besitz zu beantragen, müssen Sie uns folgende Dokumente schicken:

1. eine Kopie Ihres Ausweises mit Foto
1. eines der folgenden Dokumente, das den Zustand des vorherigen Besitzers bestätigt: 
    - eine offizielle, von der Regierung ausgestellte Sterbeurkunde, wenn der vorherige Besitzer verstorben ist, oder
    - eine Bescheinigung, z.B. eine ärztliche Bescheinigung, in der bestätigt wird, dass der Kontoinhaber arbeitsunfähig ist
1. eines der folgenden Dokumente, in dem Ihr Recht zum Besitz bestätigt wird: 
    - eine Heiratsurkunde, die belegt, dass Sie der Ehepartner des verstorbenen Kontoinhabers sind,
    - eine unterschriebene Bevollmächtigung,
    - eine Kopie eines Testaments oder Treuhanddokuments, die Sie als Vollstrecker oder Begünstigten nennen,
    - eine Geburtsurkunde des Kontoinhabers, falls Sie ein Elternteil sind oder
    - Vormundschaftsdokumente, falls Sie der Vormund des Kontoinhabers sind.

Falls Sie diese Vorkehrung in Anspruch nehmen müssen, senden Sie uns eine E-Mail an [support@nuget.org](mailto:support@nuget.org) mit der ID und der Version des Pakets.

## <a name="transparency"></a>Transparenz

Der Erfolg eines Open Source-Projekts hängt im Wesentlichen vom Vertrauen der Community in die Governance ab. Deshalb müssen Entscheidungen transparent und offen getroffen werden. Eine Diskussion über die Ausrichtung eines Projekts muss öffentlich geführt werden. Die Community sollte niemals von einer Entscheidung des wohlmeinenden Diktators überrascht werden. Darüber hinaus müssen Diskussionen über Projektentscheidungen archiviert werden, damit Mitglieder der Community den Prozess und Kontext einer Entscheidung verstehen können.
