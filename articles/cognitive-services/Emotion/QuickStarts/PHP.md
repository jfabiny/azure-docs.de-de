---
title: 'Schnellstart: Erkennen von Emotionen auf Gesichtern in einem Bild – Emotionen-API, PHP'
titlesuffix: Azure Cognitive Services
description: Informationen und Codebeispiele für den schnellen Einstieg in die Verwendung der Emotionen-API mit PHP.
services: cognitive-services
author: anrothMSFT
manager: cgronlun
ms.service: cognitive-services
ms.subservice: emotion-api
ms.topic: quickstart
ms.date: 05/23/2017
ms.author: anroth
ROBOTS: NOINDEX
ms.openlocfilehash: 3acf47ee26974ddff4f6063eef95bb29be61fce3
ms.sourcegitcommit: 95822822bfe8da01ffb061fe229fbcc3ef7c2c19
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/29/2019
ms.locfileid: "55215486"
---
# <a name="quickstart-build-an-app-to-recognize-emotions-on-faces-in-an-image"></a>Schnellstart: Erstellen einer App zur Erkennung von Emotionen auf Gesichtern in einem Bild

> [!IMPORTANT]
> Die Emotionen-API wird am 15. Februar 2019 eingestellt. Die Funktion zur Erkennung von Emotionen ist jetzt als Teil der [Gesichtserkennungs-API](https://docs.microsoft.com/azure/cognitive-services/face/) allgemein verfügbar. 

Dieser Artikel enthält Informationen und Codebeispiele für den schnellen Einstieg in die Verwendung der [Recognize-Methode der Emotionen-API](https://westus.dev.cognitive.microsoft.com/docs/services/5639d931ca73072154c1ce89/operations/563b31ea778daf121cc3a5fa) mit PHP zum Erkennen der von einer oder mehreren Personen auf einem Bild ausgedrückten Emotionen.

## <a name="prerequisite"></a>Voraussetzung
* Rufen Sie [hier](https://azure.microsoft.com/try/cognitive-services/) Ihren kostenlosen Abonnementschlüssel ab.

## <a name="recognize-emotions-php-example-request"></a>PHP-Beispielanforderung zur Emotionserkennung

Ändern Sie die REST-URL so, dass der Standort verwendet wird, an dem Sie Ihre Abonnementschlüssel erworben haben, ändern Sie den Textkörper in die URL eines Bilds, das Sie testen möchten, und ersetzen Sie den Wert von „Ocp-Apim-Subscription-Key“ durch Ihren gültigen Abonnementschlüssel.

```php
<?php
// This sample uses the Apache HTTP client from HTTP Components (http://hc.apache.org/httpcomponents-client-ga/)
require_once 'HTTP/Request2.php';

// NOTE: You must use the same region in your REST call as you used to obtain your subscription keys.
//   For example, if you obtained your subscription keys from westcentralus, replace "westus" in the
//   URL below with "westcentralus".
$request = new Http_Request2('https://westus.api.cognitive.microsoft.com/emotion/v1.0/recognize');
$url = $request->getUrl();

$headers = array(
    // Request headers
    'Content-Type' => 'application/json',

    // NOTE: Replace the "Ocp-Apim-Subscription-Key" value with a valid subscription key.
    'Ocp-Apim-Subscription-Key' => '13hc77781f7e4b19b5fcdd72a8df7156',
);

$request->setHeader($headers);

$parameters = array(
    // Request parameters
);

$url->setQueryVariables($parameters);

$request->setMethod(HTTP_Request2::METHOD_POST);

// Request body
$request->setBody('{"url": "http://www.example.com/images/image.jpg"}');

try
{
    $response = $request->send();
    echo $response->getBody();
}
catch (HttpException $ex)
{
    echo $ex;
}

?>
```

## <a name="recognize-emotions-sample-response"></a>Beispielantwort der Emotionserkennung
Ein erfolgreicher Aufruf gibt ein Array von Gesichtseinträgen zusammen mit den ihnen zugeordneten Emotionsbewertungen in der Rangfolge der Rechteckgröße der Gesichter in absteigender Reihenfolge zurück. Eine leere Antwort zeigt an, dass keine Gesichter erkannt wurden. Ein Emotionseintrag enthält die folgenden Felder:
* faceRectangle: Rechteckposition des Gesichts auf dem Bild
* scores: Emotionsbewertungen für jedes Gesicht auf dem Bild

```json
application/json
[
  {
    "faceRectangle": {
      "left": 68,
      "top": 97,
      "width": 64,
      "height": 97
    },
    "scores": {
      "anger": 0.00300731952,
      "contempt": 5.14648448E-08,
      "disgust": 9.180124E-06,
      "fear": 0.0001912825,
      "happiness": 0.9875571,
      "neutral": 0.0009861537,
      "sadness": 1.889955E-05,
      "surprise": 0.008229999
    }
  }
]
