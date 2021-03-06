---
title: Indexdefinition und Konzepte – Azure Search
description: Einführung in Indexbegriffe und Konzepte in Azure Search, einschließlich der physischen Struktur eines invertierten Index.
author: brjohnstmsft
manager: jlembicz
ms.author: brjohnst
services: search
ms.service: search
ms.topic: conceptual
ms.date: 11/08/2017
ms.custom: seodec2018
ms.openlocfilehash: 5a39021367c2f51125876081e9174eb372d7b9c9
ms.sourcegitcommit: a1cf88246e230c1888b197fdb4514aec6f1a8de2
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/16/2019
ms.locfileid: "54353157"
---
# <a name="indexes-and-indexing-overview-in-azure-search"></a>Übersicht über Indizes und Indizierung in Azure Search

In Azure Search ist ein *Index* ein dauerhafter Speicher von *Dokumenten* und anderen Konstrukten, die von einem Azure Search-Dienst für die gefilterte und Volltextsuche verwendet werden. Ein Dokument ist eine einzelne Einheit mit durchsuchbaren Daten im Index. Ein Internetversandhändler verfügt beispielsweise über ein Dokument für jeden angebotenen Artikel, eine Nachrichtenagentur über ein Dokument pro Zeitungsartikel usw. So lassen sich diese Konzepte vertrauteren Entsprechungen in der Datenbank zuordnen: Ein *Index* entspricht etwa einer *Tabelle*, und *Dokumente* entsprechen ungefähr den *Zeilen* einer Tabelle.

Wenn Sie Dokumente hinzufügen oder hochladen oder Suchabfragen an Azure Search übermitteln, senden Sie Anforderungen an einen bestimmten Index in Ihrem Suchdienst. Der Prozess des Hinzufügens von Dokumenten zu einem Index wird *Indizierung* genannt.

## <a name="field-types-and-attributes-in-an-azure-search-index"></a>Feldtypen und Attribute in einem Azure Search-Index
Wenn Sie Ihr Schema definieren, müssen Sie den Namen, den Typ und die Attribute jedes Felds in Ihrem Index festlegen. Der Feldtyp klassifiziert die Daten, die in dem Feld gespeichert sind. Attribute werden für einzelne Felder festlegen, um anzugeben, wie das Feld verwendet wird. Die folgende Tabelle listet die Typen und Attribute auf, die Sie angeben können.

### <a name="field-types"></a>Feldtypen
| Typ | BESCHREIBUNG |
| --- | --- |
| *Edm.String* |Text, der optional für die Volltextsuche (Worttrennung, Wortstammerkennung usw.) mit einem Token versehen werden kann |
| *Collection(Edm.String)* |Eine Liste von Zeichenfolgen, die für die Volltextsuche mit einem Token versehen werden können. Für die Anzahl der Elemente in einer Sammlung gibt es keine Obergrenze, allerdings gilt die Obergrenze für die Größe der Nutzlast von 16 MB auch für Sammlungen. |
| *Edm.Boolean* |Enthält TRUE/FALSE-Werte |
| *Edm.Int32* |32-Bit-Ganzzahlwerte |
| *Edm.Int64* |64-Bit-Ganzzahlwerte |
| *Edm.Double* |Numerische Daten mit doppelter Genauigkeit |
| *Edm.DateTimeOffset* |Datums-/Uhrzeitwerte im OData V4-Format (z. B. `yyyy-MM-ddTHH:mm:ss.fffZ` oder `yyyy-MM-ddTHH:mm:ss.fff[+/-]HH:mm`) |
| *Edm.GeographyPoint* |Ein Punkt, der einen weltweiten geografischen Standort darstellt |

Ausführlichere Informationen zu den von Azure Search unterstützten Datentypen finden Sie [hier](https://docs.microsoft.com/rest/api/searchservice/Supported-data-types).

### <a name="field-attributes"></a>Feldattribute
| Attribut | BESCHREIBUNG |
| --- | --- |
| *Schlüssel* |Eine Zeichenfolge, die die eindeutige ID der einzelnen Dokumente darstellt und für die Dokumentsuche verwendet wird. Jeder Index muss über einen Schlüssel verfügen. Als Schlüssel kann immer nur ein einzelnes Feld fungieren, und sein Typ muss auf „Edm.String“ festgelegt sein. |
| *Abrufbar* |Gibt an, ob ein Feld in einem Suchergebnis zurückgegeben werden kann. |
| *Filterbar* |Ermöglicht die Verwendung des Felds in Filterabfragen. |
| *Sortierbar* |Ermöglicht einer Abfrage das Sortieren von Suchergebnissen mithilfe dieses Felds. |
| *Facettierbar* |Ermöglicht die Verwendung eines Felds in einer [Facettennavigationsstruktur](search-faceted-navigation.md) für benutzerdefiniertes Filtern. Repetitive Werte, mit denen sich mehrere Dokumente zu einer Gruppe zusammenfassen lassen (etwa mehrere Dokumente der gleichen Marken- oder Dienstleistungskategorie), sind in der Regel am besten für die Verwendung als Facetten geeignet. |
| *Durchsuchbar* |Markiert das Feld als in die Volltextsuche einbeziehbar. |

Ausführlichere Informationen zu den Indexattributen von Azure Search finden Sie [hier](https://docs.microsoft.com/rest/api/searchservice/Create-Index).

## <a name="guidance-for-defining-an-index-schema"></a>Anleitung zum Definieren eines Indexschemas
Nehmen Sie sich beim Entwerfen Ihres Indexes in der Planungsphase genügend Zeit, um jede Entscheidung sorgfältig zu durchdenken. Berücksichtigen Sie beim Gestalten des Indexes die Benutzerfreundlichkeit und die geschäftlichen Anforderungen, da jedem Feld die [richtigen Attribute](https://docs.microsoft.com/rest/api/searchservice/Create-Index)zugewiesen sein müssen. Das Ändern eines Indexes nach seiner Bereitstellung erfordert dessen Neuerstellung und das erneute Laden der Daten.

Wenn sich die Datenspeicheranforderungen mit der Zeit ändern, können Sie die Kapazität erhöhen oder verringern, indem Sie Partitionen hinzufügen oder entfernen. Weitere Informationen finden Sie unter [Verwalten Ihres Suchdiensts in Azure](search-manage.md) oder [Grenzwerte für Dienste](search-limits-quotas-capacity.md).

