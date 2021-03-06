---
title: Häufig gestellte Fragen zu Azure Media Services v3 | Microsoft-Dokumentation
description: Dieser Artikel enthält Antworten auf häufig gestellte Fragen zu Azure Media Services v3.
services: media-services
documentationcenter: ''
author: Juliako
manager: femila
editor: ''
ms.service: media-services
ms.workload: ''
ms.topic: article
ms.date: 11/05/2018
ms.author: juliako
ms.openlocfilehash: 26661a213b5df5424bf9ab9ad799345ae35620ea
ms.sourcegitcommit: f0c2758fb8ccfaba76ce0b17833ca019a8a09d46
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2018
ms.locfileid: "51036766"
---
# <a name="azure-media-services-v3-frequently-asked-questions"></a>Häufig gestellte Fragen zu Azure Media Services v3

Dieser Artikel enthält Antworten auf häufig gestellte Fragen zu Azure Media Services (AMS) v3.

## <a name="can-i-use-the-azure-portal-to-manage-v3-resources"></a>Kann ich v3-Ressourcen im Azure-Portal verwalten?

Bisher nicht. Sie können eines der unterstützten SDKs verwenden. Informationen finden Sie in den Lernprogrammen und Beispielen in dieser Dokumentation.

## <a name="is-there-an-api-for-configuring-media-reserved-units"></a>Gibt es eine API zum Konfigurieren von reservierten Einheiten für Medien?

Derzeit müssen Sie zum Konfigurieren von reservierten Einheiten für Medien APIs von AMS v2 verwenden (wie unter [Skalieren der Medienverarbeitung](../previous/media-services-scale-media-processing-overview.md) beschrieben). 

Wenn Sie **VideoAnalyzerPreset** und/oder **AudioAnalyzerPreset** verwenden, legen Sie Ihr Media Services-Konto auf zehn reservierte S3-Einheiten für Medien fest.

## <a name="does-v3-asset-have-no-assetfile-concept"></a>Umfasst „Asset“ in V3 kein AssetFile-Konzept?

„AssetFile“ wurde aus der AMS-API entfernt. So ist Media Services nicht länger vom Storage SDK abhängig. Ab jetzt sind die Informationen, die zu Azure Storage gehören, in Storage enthalten und nicht mehr in Media Services. 

## <a name="where-did-client-side-storage-encryption-go"></a>Wo ist die clientseitige Speicherverschlüsselung geblieben?

Wir empfehlen ab jetzt die serverseitige Speicherverschlüsselung (die standardmäßig aktiviert ist). Weitere Informationen finden Sie unter [Azure Storage Service Encryption für ruhende Daten](https://docs.microsoft.com/azure/storage/common/storage-service-encryption).

## <a name="what-is-the-recommended-upload-method"></a>Welche Uploadmethode wird empfohlen?

Wir empfehlen die Verwendung der HTTP(s)-Erfassung. Weitere Informationen finden Sie im Thema zur [HTTP(s)-Erfassung](job-input-from-http-how-to.md).

## <a name="how-does-pagination-work"></a>Wie funktioniert die Paginierung?

Media Services unterstützt $top für Ressourcen, die OData unterstützen. Allerdings muss der an $top übergebene Wert kleiner als 1000 sein (z. B. die Seitengröße für die Paginierung).

Dadurch können Sie entweder mithilfe von $top eine kleine Stichprobe der Elemente abrufen (z. B. die 100 zuletzt verwendeten Elemente) oder mithilfe der Paginierung alle Elemente durchlaufen. 

Das Durchlaufen von Daten mit einer benutzerdefinierten Seitengröße wird von Media Services nicht unterstützt.

Weitere Informationen finden Sie unter [Filterung, Sortierung, Paging](assets-concept.md#filtering-ordering-paging).

## <a name="how-to-retrieve-an-entity-in-media-services-v3"></a>Wie wird eine Entität in Media Services v3 abgerufen?

v3 basiert auf einer vereinheitlichten API-Oberfläche, die sowohl Verwaltungs- als auch Betriebsfunktionen auf der Basis von **Azure Resource Manager** bereitstellt. Ressourcennahmen sind in Übereinstimmung mit dem **Azure Resource Manager** immer eindeutig. Daher können Sie beliebige Zeichenfolgen für eindeutige Bezeichner (beispielsweise GUIDs) als Ressourcennamen verwenden. 

## <a name="next-steps"></a>Nächste Schritte

> [!div class="nextstepaction"]
> [Media Services v3 – Übersicht](media-services-overview.md)
