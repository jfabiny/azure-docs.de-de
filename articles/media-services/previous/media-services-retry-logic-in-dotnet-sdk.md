---
title: Wiederholungslogik im Media Services SDK für .NET | Microsoft Docs
description: Dieses Thema enthält eine Übersicht über die Wiederholungslogik im Media Services SDK für .NET.
author: Juliako
manager: femila
editor: ''
services: media-services
documentationcenter: ''
ms.assetid: 527b61a6-c862-4bd8-bcbc-b9aea1ffdee3
ms.service: media-services
ms.workload: media
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/24/2018
ms.author: juliako
ms.openlocfilehash: a5171484bb4377e0f9cd84dc0a517f4ea84123e7
ms.sourcegitcommit: da3459aca32dcdbf6a63ae9186d2ad2ca2295893
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/07/2018
ms.locfileid: "51228316"
---
# <a name="retry-logic-in-the-media-services-sdk-for-net"></a>Wiederholungslogik im Media Services SDK für .NET
Bei der Arbeit mit Microsoft Azure-Diensten können vorübergehende Fehler auftreten. Wenn ein vorübergehender Fehler auftritt, ist der Vorgang in der Regel nach ein paar Wiederholungsversuchen erfolgreich. Das Media Services SDK für .NET implementiert die Wiederholungslogik zum Behandeln von vorübergehenden Fehlern, die mit Ausnahmen und Fehlern in Verbindung stehen, die durch Webanforderungen, das Ausführen von Abfragen, das Speichern von Änderungen und Speichervorgänge hervorgerufen werden.  Standardmäßig führt das Media Services SDK für .NET vier Wiederholungsversuche aus, bevor es die Ausnahme zu Ihrer Anwendung erneut auslöst. Der Code in Ihrer Anwendung muss diese Ausnahme dann ordnungsgemäß behandeln.  

 Im folgenden finden Sie einen kurzen Leitfaden zu den Richtlinien für die Webanforderung, den Speicher, die Abfrage und SaveChange:  

* Die Speicherrichtlinie wird fürBlob Storage-Vorgänge verwendet (Uploads oder Downloads von Medienobjektdateien).  
* Die Webanforderungsrichtlinie wird für allgemeine Webanforderungen verwendet (z.B. zum Erhalt eines Authentifizierungstokens und zum Auflösen des Clusterendpunkts der Benutzer).  
* Die Abfragerichtlinie wird zum Abfragen von Entitäten von REST verwendet (z.B. mediaContext.Assets.Where(…)).  
* Die SaveChanges-Richtlinie wird für alle Vorgänge verwendet, die Daten innerhalb des Diensts ändern (z.B. Erstellen einer Entität, die eine Entität aktualisiert, Aufrufen einer Dienstfunktion für einen Vorgang).  
  
  In diesem Thema werden Ausnahmetypen und Fehlercodes aufgelistet, die vom Media Services SDK für die .NET-Wiederholungslogik verarbeitet werden.  

## <a name="exception-types"></a>Ausnahmetypen
Die folgende Tabelle beschreibt die Ausnahmen, die das Media Services SDK für .NET verarbeitet oder für einige Vorgänge nicht verarbeitet, die möglicherweise vorübergehende Fehler auslösen könnten.  

| Ausnahme | Webanforderung | Speicher | Abfragen | SaveChanges |
| --- | --- | --- | --- | --- |
| WebException<br/>Weitere Informationen finden Sie im Abschnitt [WebException-Statuscodes](media-services-retry-logic-in-dotnet-sdk.md#WebExceptionStatus). |JA |Ja |Ja |JA |
| DataServiceClientException<br/> Weitere Informationen finden Sie unter [HTTP-Fehlerstatuscodes](media-services-retry-logic-in-dotnet-sdk.md#HTTPStatusCode). |Nein  |Ja |Ja |JA |
| DataServiceQueryException<br/> Weitere Informationen finden Sie unter [HTTP-Fehlerstatuscodes](media-services-retry-logic-in-dotnet-sdk.md#HTTPStatusCode). |Nein  |Ja |Ja |JA |
| DataServiceRequestException<br/> Weitere Informationen finden Sie unter [HTTP-Fehlerstatuscodes](media-services-retry-logic-in-dotnet-sdk.md#HTTPStatusCode). |Nein  |Ja |Ja |JA |
| DataServiceTransportException |Nein  |Nein  |Ja |JA |
| TimeoutException |JA |Ja |JA |Nein  |
| SocketException |JA |Ja |Ja |JA |
| StorageException |Nein  |Ja |Nein  |Nein  |
| IOException |Nein  |Ja |Nein  |Nein  |

### <a name="WebExceptionStatus"></a> WebException status codes
Die folgende Tabelle zeigt, für welche WebException-Fehlercodes die Wiederholungslogik implementiert ist. Die [WebExceptionStatus](https://msdn.microsoft.com/library/system.net.webexceptionstatus.aspx)-Enumeration definiert die Statuscodes.  

| Status | Webanforderung | Speicher | Abfragen | SaveChanges |
| --- | --- | --- | --- | --- |
| ConnectFailure |JA |Ja |Ja |JA |
| NameResolutionFailure |JA |Ja |Ja |JA |
| ProxyNameResolutionFailure |JA |Ja |Ja |JA |
| SendFailure |JA |Ja |Ja |JA |
| PipelineFailure |JA |Ja |JA |Nein  |
| ConnectionClosed |JA |Ja |JA |Nein  |
| KeepAliveFailure |JA |Ja |JA |Nein  |
| UnknownError |JA |Ja |JA |Nein  |
| ReceiveFailure |JA |Ja |JA |Nein  |
| RequestCanceled |JA |Ja |JA |Nein  |
| Timeout |JA |Ja |JA |Nein  |
| ProtocolError <br/>Die Wiederholung bei ProtocolError wird von der HTTP-Statuscodebehandlung gesteuert. Weitere Informationen finden Sie unter [HTTP-Fehlerstatuscodes](media-services-retry-logic-in-dotnet-sdk.md#HTTPStatusCode). |JA |Ja |Ja |JA |

### <a name="HTTPStatusCode"></a> HTTP-Fehlerstatuscodes
Wenn Abfrage- und SaveChanges-Vorgänge DataServiceClientException, DataServiceQueryException, oder DataServiceQueryException ausgeben, wird der HTTP-Fehlerstatuscode in der StatusCode-Eigenschaft zurückgegeben.  Die folgende Tabelle zeigt, für welche Fehlercodes die Wiederholungslogik implementiert ist.  

| Status | Webanforderung | Speicher | Abfragen | SaveChanges |
| --- | --- | --- | --- | --- |
| 401 |Nein  |Ja |Nein  |Nein  |
| 403 |Nein  |JA<br/>Behandeln von Wiederholungen mit längeren Wartezeiten. |Nein  |Nein  |
| 408 |JA |Ja |Ja |JA |
| 429 |JA |Ja |Ja |JA |
| 500 |JA |Ja |JA |Nein  |
| 502 |JA |Ja |JA |Nein  |
| 503 |JA |Ja |Ja |JA |
| 504 |JA |Ja |JA |Nein  |

Wenn Sie einen Blick auf die tatsächliche Implementierung s Media Services SDKs für die .NET-Wiederholungslogik werfen möchten, gehen Sie unter [azure-sdk-for-media-services](https://github.com/Azure/azure-sdk-for-media-services/tree/dev/src/net/Client/TransientFaultHandling).

## <a name="next-steps"></a>Nächste Schritte
[!INCLUDE [media-services-learning-paths-include](../../../includes/media-services-learning-paths-include.md)]

## <a name="provide-feedback"></a>Feedback geben
[!INCLUDE [media-services-user-voice-include](../../../includes/media-services-user-voice-include.md)]

