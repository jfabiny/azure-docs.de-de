---
title: Endpunkt für die Bing-Vorschlagssuche
titlesuffix: Azure Cognitive Services
description: Überblick über den Bing-Vorschlagssuche-API-Endpunkt.
services: cognitive-services
author: mikedodaro
manager: cgronlun
ms.service: cognitive-services
ms.subservice: bing-autosuggest
ms.topic: conceptual
ms.date: 12/05/2017
ms.author: v-gedod
ms.openlocfilehash: 03f7ac11b08d9cad633e207337ff963114f2c68f
ms.sourcegitcommit: d3200828266321847643f06c65a0698c4d6234da
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/29/2019
ms.locfileid: "55149236"
---
# <a name="bing-autosuggest-endpoint"></a>Endpunkt für die Bing-Vorschlagssuche

Die **Bing-Vorschlagssuche-API** enthält einen Endpunkt, der für einen Teil des Suchbegriffs eine Liste mit vorgeschlagenen Abfragen zurückgibt.

## <a name="endpoint"></a>Endpunkt

Um mithilfe der Bing-API vorgeschlagene Abfragen zu erhalten, senden Sie eine `GET`-Anforderung an den folgenden Endpunkt. Verwenden Sie die Header und die URL-Parameter, um Spezifikationen genauer zu definieren.

**Endpunkt:** Gibt Suchvorschläge als JSON-Ergebnisse zurück, die für die mit `?q=""` definierte Eingabe des Benutzers relevant sind.

```http
GET https://api.cognitive.microsoft.com/bing/v7.0/Suggestions 
```

Weitere Informationen zu Headern, Parametern, Marktcodes, Antwortobjekten, Fehlern usw. finden Sie in der Referenz [Bing-Vorschlagssuche-API V7](https://docs.microsoft.com/rest/api/cognitiveservices/bing-autosuggest-api-v7-reference).

## <a name="response-json"></a>JSON-Antwort

Die Antwort auf eine Anforderung der Vorschlagssuche enthält Ergebnisse als JSON-Objekte. Beispiele für die Analyse der Ergebnisse finden Sie unter [Tutorial](tutorials/autosuggest.md) und [Quellcode](tutorials/autosuggest-source.md).

## <a name="next-steps"></a>Nächste Schritte

Die **Bing**-APIs unterstützen Suchaktionen, die Ergebnisse gemäß ihrem Typ zurückgeben. Alle Suchendpunkte geben Ergebnisse als JSON-Antwortobjekte zurück.
Alle Endpunkte unterstützen Abfragen, die eine bestimmte Sprache und/oder einen bestimmten Ort nach Längengrad, Breitengrad und Suchradius zurückgeben.

Die umfassenden Informationen zu den Parametern, die von jedem Endpunkt unterstützt werden, finden Sie auf den Referenzseiten des jeweiligen Typs.
Beispiele für grundlegende Anforderungen, die die Vorschlagssuche-API verwenden, finden Sie unter [Schnellstarts für die Vorschlagssuche](https://docs.microsoft.com/azure/cognitive-services/Bing-Autosuggest).
