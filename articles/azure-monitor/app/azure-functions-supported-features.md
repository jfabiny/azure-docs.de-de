---
title: 'Azure Application Insights: Unterstützte Features von Azure Functions | Microsoft-Dokumentation'
description: In Application Insights unterstützte Features von Azure Functions
services: application-insights
documentationcenter: .net
author: MS-TimothyMothra
manager: ''
ms.service: application-insights
ms.workload: TBD
ms.tgt_pltfrm: ibiza
ms.topic: reference
ms.date: 10/05/2018
ms.reviewer: mbullwin
ms.author: tilee
ms.openlocfilehash: 06feece050835b2b9188eb702210770b44a6b49c
ms.sourcegitcommit: d3200828266321847643f06c65a0698c4d6234da
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/29/2019
ms.locfileid: "55185809"
---
# <a name="application-insights-for-azure-functions-supported-features"></a>Unterstützte Features in Application Insights für Azure Functions

Azure Functions bietet [von Haus aus Integration](https://docs.microsoft.com/azure/azure-functions/functions-monitoring) in Application Insights, die über die ILogger-Schnittstelle verfügbar ist. Unten folgt die Liste der aktuell unterstützten Features. Arbeiten Sie zum [Einstieg](https://github.com/Azure/Azure-Functions/wiki/App-Insights) das Azure Functions-Handbuch durch.

## <a name="supported-features"></a>Unterstützte Features

| Azure-Funktionen                       | V1                | V2 (Ignite 2018)  | 
|-----------------------------------    |---------------    |------------------ |
| **Application Insights .NET SDK**   | **2.5.0**       | **2.7.2**         |
| | | | 
| **Automatische Sammlung von**        |                 |                   |               
| &bull;Anforderungen                     | JA             | JA               | 
| &bull;Ausnahmen                   | JA             | JA               | 
| &bull;Abhängigkeiten                   |                   |                   |               
| &nbsp;&nbsp;&nbsp;&mdash; HTTP      |                 | JA               | 
| &nbsp;&nbsp;&nbsp;&mdash; ServiceBus|                 | JA               | 
| &nbsp;&nbsp;&nbsp;&mdash; EventHub  |                 | JA               | 
| &nbsp;&nbsp;&nbsp;&mdash; SQL       |                 | JA               | 
| | | | 
| **Unterstützte Features**                |                   |                   |               
| &bull; QuickPulse/LiveMetrics       | JA             | JA               | 
| &nbsp;&nbsp;&nbsp;&mdash; Sicherer Steuerkanal|                 | JA               | 
| &bull; Stichprobenentnahme                     | JA             | JA               | 
| &bull; Heartbeats                   |                 | JA               | 
| | | | 
| **Korrelation**                       |                   |                   |               
| &bull; ServiceBus                     |                   | JA               | 
| &bull; EventHub                       |                   | JA               | 
| | | | 
| **Konfigurierbar**                      |                   |                   |           
| &bull;Vollständig konfigurierbar.<br/>Anweisungen finden Sie unter [Azure Functions](https://github.com/Microsoft/ApplicationInsights-aspnetcore/issues/759#issuecomment-426687852).<br/>Alle Optionen finden Sie unter [Asp.NET Core](https://github.com/Microsoft/ApplicationInsights-aspnetcore/wiki/Custom-Configuration).               |                   | JA                   | 


## <a name="live-metrics--secure-control-channel"></a>Livemetriken und sicherer Steuerkanal

Die von Ihnen angegebenen benutzerdefinierten Filterkriterien werden an die Livemetrikkomponente des Application Insights SDK zurückgesendet. Der Filter können potenziell vertrauliche Informationen wie z.B. Kunden-IDs enthalten. Sie können den Kanal mit einem geheimen API-Schlüssel sicher machen. Anleitungen dazu finden Sie unter [Sichern des Steuerkanals](https://docs.microsoft.com/azure/azure-monitor/app/live-stream#secure-the-control-channel).

## <a name="sampling"></a>Stichproben

Azure Functions aktiviert die Stichprobenentnahme in der Konfiguration standardmäßig. Weitere Informationen finden Sie unter [Configure Sampling](https://docs.microsoft.com/azure/azure-functions/functions-monitoring#configure-sampling) (Konfigurieren der Stichprobenentnahme).
