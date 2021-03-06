---
title: Behandeln von Mausereignissen mit Azure Maps | Microsoft-Dokumentation
description: Erstellen einer interaktiven JavaScript-Karte mit Kartenereignissen
author: jingjing-z
ms.author: jinzh
ms.date: 11/29/2018
ms.topic: conceptual
ms.service: azure-maps
services: azure-maps
manager: ''
ms.custom: codepen
ms.openlocfilehash: 16455719f05688793e2aee6f10fa00a707d553c0
ms.sourcegitcommit: cf88cf2cbe94293b0542714a98833be001471c08
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/23/2019
ms.locfileid: "54469533"
---
# <a name="interact-with-the-map---mouse-events"></a>Interagieren mit der Karte – Mausereignisse

In diesem Artikel erfahren Sie, wie Sie die Eigenschaft [map class](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.map?view=azure-iot-typescript-latest) [events](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.map?view=azure-iot-typescript-latest) verwenden, um Ereignisse auf der Karte und auf verschiedenen Ebenen der Karte hervorzuheben. Außerdem wird beschrieben, wie Sie die Eigenschaft „map class events“ verwenden, um Ereignisse bei der Interaktion mit einem HTML-Marker hervorzuheben.

## <a name="interact-with-the-map"></a>Interaktion mit der Karte

<iframe height='600' scrolling='no' title='Interaktion mit der Karte – Mausereignisse' src='//codepen.io/azuremaps/embed/bLZEWd/?height=600&theme-id=0&default-tab=js,result&embed-version=2&editable=true' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'>Weitere Informationen finden Sie unter dem Pen <a href='https://codepen.io/azuremaps/pen/bLZEWd/'>Interact with the map – mouse events</a> (Interagieren mit der Karte – Mausereignisse) von Azure Maps (<a href='https://codepen.io/azuremaps'>@azuremaps</a>) auf <a href='https://codepen.io'>CodePen</a>.
</iframe>

Experimentieren Sie mit der oben gezeigten Karte, und sehen Sie die entsprechenden Mausereignisse hervorgehoben auf der rechten Seite. Sie können auf die Registerkarte **JS** klicken, um den JavaScript-Code anzuzeigen und zu bearbeiten. Außerdem können Sie auf die Schaltfläche **Auf CodePen bearbeiten** klicken und den Code auf CodePen bearbeiten.

## <a name="interact-with-map-layers"></a>Interaktion mit Kartenebenen

<iframe height='600' scrolling='no' title='Interaktion mit der Karte – Ebenenereignisse' src='//codepen.io/azuremaps/embed/bQRRPE/?height=600&theme-id=0&default-tab=js,result&embed-version=2&editable=true' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'>Weitere Informationen finden Sie unter dem Pen <a href='https://codepen.io/azuremaps/pen/bQRRPE/'>Interacting with the map – Layer Events</a> (Interaktion mit der Karte – Ebenenereignisse) von Azure Maps (<a href='https://codepen.io/azuremaps'>@azuremaps</a>) auf <a href='https://codepen.io'>CodePen</a>.
</iframe>

Der oben stehende Code hebt den Namen der Ereignisse hervor, die bei der Interaktion mit der Symbolebene ausgelöst werden. Die Symbol-, Blasen-, Linien- und Polygonebenen unterstützen den gleichen Satz von Ereignissen. Die Kachelebene unterstützt keines dieser Ereignisse.

## <a name="interact-with-html-marker"></a>Interaktion mit dem HTML-Marker

<iframe height='500' scrolling='no' title='Interaktion mit der Karte – HTML Markerereignisse' src='//codepen.io/azuremaps/embed/VVzKJY/?height=500&theme-id=0&default-tab=js,result&embed-version=2&editable=true' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'>Weitere Informationen finden Sie unter dem Pen <a href='https://codepen.io/azuremaps/pen/VVzKJY/'>Interacting with the map - HTML Marker events</a> (Interaktion mit der Karte – HTML Markerereignisse) von Azure Maps (<a href='https://codepen.io/azuremaps'>@azuremaps</a>) auf <a href='https://codepen.io'>CodePen</a>.
</iframe>

Der oben stehende Code fügt Javascript-Kartenereignisse zu einem HTML-Marker hinzu. Er hebt außerdem den Namen der Ereignisse hervor, die bei der Interaktion mit dem HTML-Marker ausgelöst werden.

## <a name="next-steps"></a>Nächste Schritte

Erfahren Sie mehr zu den in diesem Artikel verwendeten Klassen und Methoden:

> [!div class="nextstepaction"]
> [Map](https://docs.microsoft.com/javascript/api/azure-maps-control/atlas.map?view=azure-iot-typescript-latest)

Die folgenden Artikel enthalten vollständige Codebeispiele:

> [!div class="nextstepaction"]
> [Anzeigen von Suchergebnissen](./map-search-location.md)

> [!div class="nextstepaction"]
> [Seite für Beispielcode](https://aka.ms/AzureMapsSamples)
