---
title: HTTP-Antwortcodes von APIs
titleSuffix: Azure
description: Es wird beschrieben, welche HTTP-Antwortcodes über die Erstellungs- und Endpunkt-APIs von LUIS zurückgegeben werden.
services: cognitive-services
author: diberry
manager: cgronlun
ms.custom: seodec18
ms.service: cognitive-services
ms.subservice: language-understanding
ms.topic: article
ms.date: 11/27/2018
ms.author: diberry
ms.openlocfilehash: fd0d8cc492a8a35d66aa4b20b792bf317b9e8c11
ms.sourcegitcommit: 95822822bfe8da01ffb061fe229fbcc3ef7c2c19
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/29/2019
ms.locfileid: "55218851"
---
# <a name="common-api-response-codes-and-their-meaning"></a>Allgemeine API-Antwortcodes und ihre Bedeutung

Die APIs für die Erstellung ([authoring](https://aka.ms/luis-authoring-apis)) und für Endpunkte ([endpoint](https://aka.ms/luis-endpoint-apis)) geben HTTP-Antwortcodes zurück. Antwortnachrichten enthalten spezifische Informationen zu einer Anforderung, aber es wird ein allgemeiner HTTP-Antwortstatuscode verwendet. 

## <a name="common-status-codes"></a>Häufige Statuscodes
In der folgenden Tabelle sind einige der häufigsten HTTP-Antwortstatuscodes für die [Erstellungs-](https://aka.ms/luis-authoring-apis) und [Endpunkt](https://aka.ms/luis-endpoint-apis)-APIs aufgeführt:

|Code|API|Erklärung|
|:--|--|--|
|400|Erstellung, Endpunkt|Die Parameter der Anforderung sind fehlerhaft, da die erforderlichen Parameter nicht vorhanden, falsch formatiert oder zu groß sind|
|400|Erstellung, Endpunkt|Der Text der Anforderung ist fehlerhaft, da der JSON-Code nicht vorhanden, falsch formatiert oder zu groß ist|
|401|Erstellen|Endpunkt-Abonnementschlüssel wurde anstelle des Erstellungsschlüssels verwendet|
|401|Erstellung, Endpunkt|Ungültig, falsch formatiert oder leerer Schlüssel|
|401|Erstellung, Endpunkt| Schlüssel stimmen nicht mit Region überein|
|401|Erstellen|Sie sind nicht der Besitzer oder Projektmitarbeiter|
|401|Erstellen|Ungültige Reihenfolge der API-Aufrufe|
|403|Erstellung, Endpunkt|Monatliche Kontingentgrenze für Schlüssel überschritten|
|409|Endpunkt|Anwendung wird noch geladen|
|410|Endpunkt|Anwendung muss neu trainiert und erneut veröffentlicht werden|
|414|Endpunkt|Abfrage überschreitet maximale Zeichenzahl|
|429|Erstellung, Endpunkt|Ratenlimit wurde überschritten (Anforderungen/Sekunde)|

## <a name="next-steps"></a>Nächste Schritte

* REST-API-Dokumentation für [Erstellung](https://westus.dev.cognitive.microsoft.com/docs/services/5890b47c39e2bb17b84a55ff/operations/5890b47c39e2bb052c5b9c2f) und [Endpunkt](https://westus.dev.cognitive.microsoft.com/docs/services/5819c76f40a6350ce09de1ac/operations/5819c77140a63516d81aee78)
