---
title: 'Schnellstart: Suchen nach Bildern – Bing-Bildersuche-REST-API und Python'
titleSuffix: Azure Cognitive Services
description: Verwenden Sie diese Schnellstartanleitung, um Bildsuchanforderungen mithilfe von Python an die Bing-Bildersuche-REST-API zu senden und JSON-Antworten zu empfangen.
services: cognitive-services
author: aahill
manager: cgronlun
ms.service: cognitive-services
ms.subservice: bing-image-search
ms.topic: quickstart
ms.date: 8/20/2018
ms.author: aahi
ms.custom: seodec2018
ms.openlocfilehash: 018f2b4b3f75ed9cef3fbc63ac4e93b56a756e14
ms.sourcegitcommit: d3200828266321847643f06c65a0698c4d6234da
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/29/2019
ms.locfileid: "55174027"
---
# <a name="quickstart-search-for-images-using-the-bing-image-search-rest-api-and-python"></a>Schnellstart: Suchen nach Bildern mithilfe der Bing-Bildersuche-REST-API und Python

Verwenden Sie diesen Schnellstart, um die Bing-Bildersuche-API zum ersten Mal aufzurufen und eine JSON-Antwort zu erhalten. Diese einfache Python-Anwendung sendet eine Suchabfrage an die API und zeigt die Rohdatenergebnisse an.

Diese Anwendung ist zwar in Python geschrieben, an sich ist die API aber ein RESTful-Webdienst, der mit den meisten Programmiersprachen kompatibel ist.

Sie können dieses Beispiel als Jupyter Notebook in [MyBinder](https://mybinder.org) ausführen, indem Sie auf das Binder-Badge klicken:

[![Binder](https://mybinder.org/badge.svg)](https://mybinder.org/v2/gh/Microsoft/cognitive-services-notebooks/master?filepath=BingImageSearchAPI.ipynb)


Den Quellcode des Beispiels finden Sie außerdem auf [GitHub](https://github.com/Azure-Samples/cognitive-services-REST-api-samples/blob/master/python/Search/BingImageSearchv7.py).

## <a name="prerequisites"></a>Voraussetzungen

[!INCLUDE [cognitive-services-bing-image-search-signup-requirements](../../../../includes/cognitive-services-bing-image-search-signup-requirements.md)]

Siehe auch [Cognitive Services-Preise – Bing-Suche-API](https://azure.microsoft.com/pricing/details/cognitive-services/search-api/)

## <a name="running-the-quickstart"></a>Ausführen des Schnellstarts

Legen Sie als Erstes für `subscription_key` einen gültigen Abonnementschlüssel für den Bing-API-Dienst fest.

```python
subscription_key = None
assert subscription_key
```

Als Nächstes überprüfen Sie, ob der `search_url`-Endpunkt richtig ist. Zu dem Zeitpunkt, als dieser Artikel geschrieben wurde, wurde nur ein Endpunkt für Bing-Suche-APIs verwendet. Wenn Ihnen Autorisierungsfehler auffallen, vergleichen Sie diesen Wert mit dem Bing-Suche-Endpunkt in Ihrem Azure-Dashboard.


```python
search_url = "https://api.cognitive.microsoft.com/bing/v7.0/images/search"
```

Legen Sie `search_term` für die Suche von Bildern von Welpen fest.


```python
search_term = "puppies"
```

Der folgende Block verwendet die `requests`-Bibliothek in Python, um die Bing-Suche-APIs aufzurufen und die Ergebnisse als JSON-Objekt zurückzugeben. Beachten Sie, dass wir den API-Schlüssel über das `headers`-Wörterbuch übergeben und den Suchbegriff über das `params`-Wörterbuch. Die vollständige Liste der zum Filtern von Suchergebnissen verwendbaren Optionen finden Sie in der [REST-API](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference)-Dokumentation.


```python
import requests

headers = {"Ocp-Apim-Subscription-Key" : subscription_key}
params  = {"q": search_term, "license": "public", "imageType": "photo"}
response = requests.get(search_url, headers=headers, params=params)
response.raise_for_status()
search_results = response.json()
```

Das `search_results`-Objekt enthält die tatsächlichen Bilder zusammen mit umfassenden Metadaten wie verwandten Elementen. Die folgende Codezeile kann z.B. die Miniaturansicht-URLs für die ersten 16 Ergebnisse extrahieren.


```python
thumbnail_urls = [img["thumbnailUrl"] for img in search_results["value"][:16]]
```

Laden Sie dann mithilfe der `PIL`-Bibliothek die Miniaturbilder herunterladen, und rendern Sie mithilfe der `matplotlib`-Bibliothek die Berichte auf einem $4\x 4$-Raster.


```python
%matplotlib inline
import matplotlib.pyplot as plt
from PIL import Image
from io import BytesIO

f, axes = plt.subplots(4, 4)
for i in range(4):
    for j in range(4):
        image_data = requests.get(thumbnail_urls[i+4*j])
        image_data.raise_for_status()
        image = Image.open(BytesIO(image_data.content))        
        axes[i][j].imshow(image)
        axes[i][j].axis("off")
plt.show()
```

## <a name="sample-json-response"></a>JSON-Beispielantwort

Antworten der Bing-Bildersuche-API werden im JSON-Format zurückgegeben. Diese Beispielantwort wurde gekürzt, damit nur ein Ergebnis angezeigt wird.

```json
{
"_type":"Images",
"instrumentation":{
    "_type":"ResponseInstrumentation"
},
"readLink":"images\/search?q=tropical ocean",
"webSearchUrl":"https:\/\/www.bing.com\/images\/search?q=tropical ocean&FORM=OIIARP",
"totalEstimatedMatches":842,
"nextOffset":47,
"value":[
    {
        "webSearchUrl":"https:\/\/www.bing.com\/images\/search?view=detailv2&FORM=OIIRPO&q=tropical+ocean&id=8607ACDACB243BDEA7E1EF78127DA931E680E3A5&simid=608027248313960152",
        "name":"My Life in the Ocean | The greatest WordPress.com site in ...",
        "thumbnailUrl":"https:\/\/tse3.mm.bing.net\/th?id=OIP.fmwSKKmKpmZtJiBDps1kLAHaEo&pid=Api",
        "datePublished":"2017-11-03T08:51:00.0000000Z",
        "contentUrl":"https:\/\/mylifeintheocean.files.wordpress.com\/2012\/11\/tropical-ocean-wallpaper-1920x12003.jpg",
        "hostPageUrl":"https:\/\/mylifeintheocean.wordpress.com\/",
        "contentSize":"897388 B",
        "encodingFormat":"jpeg",
        "hostPageDisplayUrl":"https:\/\/mylifeintheocean.wordpress.com",
        "width":1920,
        "height":1200,
        "thumbnail":{
        "width":474,
        "height":296
        },
        "imageInsightsToken":"ccid_fmwSKKmK*mid_8607ACDACB243BDEA7E1EF78127DA931E680E3A5*simid_608027248313960152*thid_OIP.fmwSKKmKpmZtJiBDps1kLAHaEo",
        "insightsMetadata":{
        "recipeSourcesCount":0,
        "bestRepresentativeQuery":{
            "text":"Tropical Beaches Desktop Wallpaper",
            "displayText":"Tropical Beaches Desktop Wallpaper",
            "webSearchUrl":"https:\/\/www.bing.com\/images\/search?q=Tropical+Beaches+Desktop+Wallpaper&id=8607ACDACB243BDEA7E1EF78127DA931E680E3A5&FORM=IDBQDM"
        },
        "pagesIncludingCount":115,
        "availableSizesCount":44
        },
        "imageId":"8607ACDACB243BDEA7E1EF78127DA931E680E3A5",
        "accentColor":"0050B2"
    }
}
```

## <a name="next-steps"></a>Nächste Schritte

> [!div class="nextstepaction"]
> [Tutorial: Einseitige Web-App für die Bing-Bildersuche](../tutorial-bing-image-search-single-page-app.md)

## <a name="see-also"></a>Weitere Informationen

* [Was ist die Bing-Bildersuche?](https://docs.microsoft.com/azure/cognitive-services/bing-image-search/overview)  
* [Interaktive Onlinedemo testen](https://azure.microsoft.com/services/cognitive-services/bing-image-search-api/)  
* [Abrufen eines kostenlosen Cognitive Services-Zugriffsschlüssels](https://azure.microsoft.com/try/cognitive-services/?api=bing-image-search-api)  
* [Dokumentation zu Azure Cognitive Services](https://docs.microsoft.com/azure/cognitive-services)
* [Referenz zur Bing-Bildersuche-API](https://docs.microsoft.com/rest/api/cognitiveservices/bing-images-api-v7-reference)
