---
title: 'Schnellstart: Bing-Rechtschreibprüfungs-API, C#'
titlesuffix: Azure Cognitive Services
description: Informationen und Codebeispiele für den schnellen Einstieg in die Verwendung der Bing-Rechtschreibprüfungs-API.
services: cognitive-services
author: aahill
manager: cgronlun
ms.service: cognitive-services
ms.subservice: bing-spell-check
ms.topic: quickstart
ms.date: 09/14/2017
ms.author: aahi
ms.openlocfilehash: 77ad43b63d5548cf57024bc0c2b707e51f1c8496
ms.sourcegitcommit: d3200828266321847643f06c65a0698c4d6234da
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/29/2019
ms.locfileid: "55189815"
---
# <a name="quickstart-for-bing-spell-check-api-with-c"></a>Schnellstart für die Bing-Rechtschreibprüfungs-API mit C#

In diesem Artikel erfahren Sie, wie Sie die [Bing-Rechtschreibprüfungs-API](https://azure.microsoft.com/services/cognitive-services/spell-check/) mit C# verwenden. Die Rechtschreibprüfungs-API gibt eine Liste mit nicht erkannten Wörtern und Ersetzungsvorschlägen zurück. Normalerweise übergeben Sie Text an die API und nehmen dann entweder die vorgeschlagenen Ersetzungen im Text vor oder zeigen sie für den Benutzer Ihrer Anwendung an, damit er selbst entscheiden kann, ob er die Ersetzungen vornehmen möchte. In diesem Artikel wird erläutert, wie Sie eine Anforderung mit dem Text „Hollo, wrld!“ senden. Die vorgeschlagenen Ersetzungen sind „Hello“ und „world“.

## <a name="prerequisites"></a>Voraussetzungen

Sie benötigen [Visual Studio 2017](https://www.visualstudio.com/downloads/), um diesen Code unter Windows ausführen zu können. (Die kostenlose Community Edition ist hierfür geeignet.) Siehe auch [Cognitive Services-Preise – Bing-Suche-API](https://azure.microsoft.com/pricing/details/cognitive-services/search-api/)

Sie benötigen ein [Cognitive Services-API-Konto](https://docs.microsoft.com/azure/cognitive-services/cognitive-services-apis-create-account) mit der **Bing-Rechtschreibprüfungs-API v7**. Die [kostenlose Testversion](https://azure.microsoft.com/try/cognitive-services/#lang) ist für diesen Schnellstart ausreichend. Sie benötigen den Zugriffsschlüssel, den Sie beim Aktivieren Ihrer kostenlosen Testversion erhalten, oder Sie können den Schlüssel eines kostenpflichtigen Abonnements von Ihrem Azure-Dashboard verwenden.

## <a name="get-spell-check-results"></a>Abrufen der Ergebnisse der Rechtschreibprüfung

1. Erstellen Sie in Ihrer bevorzugten IDE ein neues C#-Projekt.
2. Fügen Sie den unten stehenden Code hinzu.
3. Ersetzen Sie den `subscriptionKey`-Wert durch einen für Ihr Abonnement gültigen Zugriffsschlüssel.
4. Führen Sie das Programm aus.

```csharp
using System;
using System.Collections.Generic;
using System.Linq;
using System.Net.Http;
using System.Net.Http.Headers;
using System.Text;

namespace SpellCheckSample1
{
    class Program
    {
        static string host = "https://api.cognitive.microsoft.com";
        static string path = "/bing/v7.0/spellcheck?";

        // For a list of available markets, go to:
        // https://docs.microsoft.com/rest/api/cognitiveservices/bing-autosuggest-api-v7-reference#market-codes
        static string params_ = "mkt=en-US&mode=proof";

        // NOTE: Replace this example key with a valid subscription key.
        static string key = "ENTER KEY HERE";

        static string text = "Hollo, wrld!";

        // These properties are used for optional headers (see below).
        // static string ClientId = "<Client ID from Previous Response Goes Here>";
        //static string ClientId = "2325577A61966D252A475CD760C96C03";
        // static string ClientIp = "999.999.999.999";
        // static string ClientLocation = "+90.0000000000000;long: 00.0000000000000;re:100.000000000000";

        async static void SpellCheck()
        {
            HttpClient client = new HttpClient();
            client.DefaultRequestHeaders.Add("Ocp-Apim-Subscription-Key", key);

            // The following headers are optional, but it is recommended they be treated as required.
            // These headers help the service return more accurate results.
            //client.DefaultRequestHeaders.Add("X-Search-Location", ClientLocation);
            //client.DefaultRequestHeaders.Add("X-MSEdge-ClientID", ClientId);
            //client.DefaultRequestHeaders.Add("X-MSEdge-ClientIP", ClientIp);

            HttpResponseMessage response = new HttpResponseMessage();
            string uri = host + path + params_;

            List<KeyValuePair<string, string>> values = new List<KeyValuePair<string, string>>();
            values.Add(new KeyValuePair<string, string>("text", text));

            using (FormUrlEncodedContent content = new FormUrlEncodedContent(values))
            {
                content.Headers.ContentType = new MediaTypeHeaderValue("application/x-www-form-urlencoded");
                response = await client.PostAsync(uri, content);
            }

            string client_id;
            if (response.Headers.TryGetValues("X-MSEdge-ClientID", out IEnumerable<string> header_values))
            {
                client_id = header_values.First();
                Console.WriteLine("Client ID: " + client_id);
            }

            string contentString = await response.Content.ReadAsStringAsync();
            Console.WriteLine(JsonPrettyPrint(contentString));

        }

        static void Main(string[] args)
        {
            SpellCheck();
            Console.ReadLine();
        }

        static string JsonPrettyPrint(string json)
        {
            if (string.IsNullOrEmpty(json))
            {
                return string.Empty;
            }

            json = json.Replace(Environment.NewLine, "").Replace("\t", "");

            StringBuilder sb = new StringBuilder();
            bool quote = false;
            bool ignore = false;
            char last = ' ';
            int offset = 0;
            int indentLength = 3;

            foreach (char ch in json)
            {
                switch (ch)
                {
                    case '"':
                        if (!ignore) quote = !quote;
                        break;
                    case '\\':
                        if (quote && last != '\\') ignore = true;
                        break;
                }

                if (quote)
                {
                    sb.Append(ch);
                    if (last == '\\' && ignore) ignore = false;
                }
                else
                {
                    switch (ch)
                    {
                        case '{':
                        case '[':
                            sb.Append(ch);
                            sb.Append(Environment.NewLine);
                            sb.Append(new string(' ', ++offset * indentLength));
                            break;
                        case '}':
                        case ']':
                            sb.Append(Environment.NewLine);
                            sb.Append(new string(' ', --offset * indentLength));
                            sb.Append(ch);
                            break;
                        case ',':
                            sb.Append(ch);
                            sb.Append(Environment.NewLine);
                            sb.Append(new string(' ', offset * indentLength));
                            break;
                        case ':':
                            sb.Append(ch);
                            sb.Append(' ');
                            break;
                        default:
                            if (quote || ch != ' ') sb.Append(ch);
                            break;
                    }
                }
                last = ch;
            }

            return sb.ToString().Trim();
        }
    }
}
```

**Antwort**

Es wird eine erfolgreiche Antwort im JSON-Format zurückgegeben, wie im folgenden Beispiel gezeigt: 

```json
{
   "_type": "SpellCheck",
   "flaggedTokens": [
      {
         "offset": 0,
         "token": "Hollo",
         "type": "UnknownToken",
         "suggestions": [
            {
               "suggestion": "Hello",
               "score": 0.9115257530801
            },
            {
               "suggestion": "Hollow",
               "score": 0.858039839213461
            },
            {
               "suggestion": "Hallo",
               "score": 0.597385084464481
            }
         ]
      },
      {
         "offset": 7,
         "token": "wrld",
         "type": "UnknownToken",
         "suggestions": [
            {
               "suggestion": "world",
               "score": 0.9115257530801
            }
         ]
      }
   ]
}
```

## <a name="next-steps"></a>Nächste Schritte

> [!div class="nextstepaction"]
> [Tutorial zur Bing-Rechtschreibprüfung](../tutorials/spellcheck.md)

## <a name="see-also"></a>Weitere Informationen

- [Übersicht über die Bing-Rechtschreibprüfung](../proof-text.md)
- [Referenz zur Bing-Rechtschreibprüfungs-API v7](https://docs.microsoft.com/rest/api/cognitiveservices/bing-spell-check-api-v7-reference)
