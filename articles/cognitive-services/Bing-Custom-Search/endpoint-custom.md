---
title: Endpunkt für die benutzerdefinierte Bing-Suche
titlesuffix: Azure Cognitive Services
description: Enthält einen Überblick über den API-Endpunkt für die benutzerdefinierte Bing-Suche.
services: cognitive-services
author: mikedodaro
manager: cgronlun
ms.service: cognitive-services
ms.subservice: bing-custom-search
ms.topic: conceptual
ms.date: 12/05/2017
ms.author: v-gedod
ms.openlocfilehash: ed420676ddc4c83be93939874f2943126f9209e8
ms.sourcegitcommit: d3200828266321847643f06c65a0698c4d6234da
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/29/2019
ms.locfileid: "55176623"
---
# <a name="custom-search"></a>Benutzerdefinierte Suche
Die benutzerdefinierte Bing-Suche ermöglicht das Erstellen einer maßgeschneiderten Suchbenutzeroberfläche für Themen, die Sie interessieren. Ihre Benutzer sehen Suchergebnisse, die auf den gewünschten Inhalt zugeschnitten sind, anstatt durch allgemeine Suchergebnisse mit irrelevanten Inhalten blättern zu müssen.

## <a name="custom-search-endpoint"></a>Endpunkt für die benutzerdefinierte Suche
Um mithilfe der API für die benutzerdefinierte Bing-Suche Ergebnisse zu erhalten, senden Sie eine `GET`-Anforderung an den folgenden Endpunkt. Verwenden Sie die Header und die URL-Parameter, um Spezifikationen genauer zu definieren.

Endpunkt: Gibt Suchvorschläge als JSON-Ergebnisse zurück, die für die mit `?q=""` definierte Eingabe des Benutzers relevant sind.
```  
 GET https://api.cognitive.microsoft.com/bingcustomsearch/v7.0/search  
```

Beispiele, in denen das Einrichten von Quellen für die benutzerdefinierte Suche beschrieben wird, finden Sie im [Tutorial](https://docs.microsoft.com/azure/cognitive-services/bing-custom-search/tutorials/custom-search-web-page). Weitere Informationen zu Headern, Parametern, Marktcodes, Antwortobjekten, Fehlern usw. finden Sie in der Referenz zur [API für die benutzerdefinierte Bing-Suche v7](https://docs.microsoft.com/rest/api/cognitiveservices/bing-custom-search-api-v7-reference).

## <a name="custom-search-response-json"></a>JSON-Antwort für die benutzerdefinierte Suche
Eine benutzerdefinierte Suchanforderung gibt Ergebnisse als JSON-Objekte zurück (siehe [Antwortobjekte](https://docs.microsoft.com/rest/api/cognitiveservices/bing-custom-search-api-v7-reference#response-objects)). 

## <a name="custom-autosuggest"></a>Benutzerdefinierte Vorschlagssuche
Mit der API für die benutzerdefinierte Vorschlagssuche können Sie einen Teil eines Suchbegriffs an Bing senden und erhalten dann eine Liste mit vorgeschlagenen Begriffen zurück, die Sie konfigurieren können. Mit der benutzerdefinierten Vorschlagssuche fügen Sie Vorschläge hinzu, die von der API zurückgegeben werden, und können optional angeben, ob von Bing generierte Vorschläge eingefügt werden sollen.

## <a name="custom-autosuggest-endpoint"></a>Endpunkt für die benutzerdefinierte Vorschlagssuche
Um Vorschläge für benutzerdefinierte Suchbegriffe zu erhalten, senden Sie eine GET-Anforderung an:

```
https://api.cognitive.microsoft.com/bingcustomsearch/v7.0/Suggestions
```  

Informationen zum Definieren von benutzerdefinierten Vorschlägen finden Sie unter [Define custom search suggestions](define-custom-suggestions.md) (Definieren von Vorschlägen für die benutzerdefinierte Suche).

## <a name="custom-image-search"></a>Benutzerdefinierte Bildersuche
Mit der API für die benutzerdefinierte Bildersuche können Sie eine Suchabfrage an Bing senden und erhalten eine Liste mit relevanten Bildern von Ihrer Instanz für die benutzerdefinierte Suche zurück.

## <a name="custom-image-search-endpoint"></a>Endpunkt für die benutzerdefinierte Bildersuche
Senden Sie eine GET-Anforderung an die folgende URL, um Bilder von Ihrer Instanz der benutzerdefinierten Suche anzufordern:

```
https://api.cognitive.microsoft.com/bingcustomsearch/v7.0/images/search
```

Weitere Informationen zum Konfigurieren einer Instanz der benutzerdefinierten Suche finden Sie unter [Konfigurieren der Benutzeroberfläche für die benutzerdefinierte Suche](https://docs.microsoft.com/azure/cognitive-services/bing-custom-search/define-your-custom-view).

## <a name="next-steps"></a>Nächste Schritte
Die **Bing**-APIs unterstützen Suchaktionen, die Ergebnisse gemäß ihrem Typ zurückgeben. Alle Suchendpunkte geben Ergebnisse als JSON-Antwortobjekte zurück.  Alle Endpunkte unterstützen Abfragen, die eine bestimmte Sprache und/oder einen bestimmten Ort nach Längengrad, Breitengrad und Suchradius zurückgeben.

Die umfassenden Informationen zu den Parametern, die von jedem Endpunkt unterstützt werden, finden Sie auf den Referenzseiten des jeweiligen Typs.
Beispiele für grundlegende Anforderungen mithilfe der API für die benutzerdefinierte Suche finden Sie in den [Schnellstartanleitungen zur benutzerdefinierten Suche](https://docs.microsoft.com/azure/cognitive-services/bing-custom-search/).
