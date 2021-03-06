---
title: app()-Ausdruck in Azure Log Analytics-Abfragen | Microsoft-Dokumentation
description: Der app-Ausdruck wird in Log Analytics-Abfragen verwendet, um Daten aus einer bestimmten Application Insights-Anwendung in der gleichen Ressourcengruppe, einer anderen Ressourcengruppe oder einem anderen Abonnement abzurufen.
services: log-analytics
documentationcenter: ''
author: bwren
manager: carmonm
editor: ''
ms.assetid: ''
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.topic: article
ms.date: 01/25/2019
ms.author: bwren
ms.openlocfilehash: 2d6f3517e988d6bd66ee9007e072ee87c71d1340
ms.sourcegitcommit: eecd816953c55df1671ffcf716cf975ba1b12e6b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/28/2019
ms.locfileid: "55104659"
---
# <a name="app-expression-in-log-analytics-query"></a>app()-Ausdruck in Log Analytics-Abfragen

Der Ausdruck `app` wird in Log Analytics-Abfragen verwendet, um Daten aus einer bestimmten Application Insights-Anwendung in der gleichen Ressourcengruppe, einer anderen Ressourcengruppe oder einem anderen Abonnement abzurufen. Dies ist nützlich, um Anwendungsdaten in einer Log Analytics-Abfrage einzuschließen und Daten übergreifend über mehrere Anwendungen in einer Application Insights-Abfrage abzufragen.



## <a name="syntax"></a>Syntax

`app(`*Bezeichner*`)`


## <a name="arguments"></a>Argumente

- *Bezeichner*: Identifiziert die Anwendung mit einem der Formate in der folgenden Tabelle.

| Bezeichner | BESCHREIBUNG | Beispiel
|:---|:---|:---|
| Ressourcenname | Für Menschen lesbarer Name der Anwendung (auch als „Komponentenname“ bezeichnet) | app("fabrikamapp") |
| Qualifizierter Name | Vollständiger Name der Anwendung in der Form: „Abonnementname/Ressourcengruppe/Komponentenname“ | app('AI-Prototype/Fabrikam/fabrikamapp') |
| ID | GUID der Anwendung | app("988ba129-363e-4415-8fe7-8cbab5447518") |
| Azure-Ressourcen-ID | Bezeichner für die Azure-Ressource |app("/subscriptions/7293b69-db12-44fc-9a66-9c2005c3051d/resourcegroups/Fabrikam/providers/microsoft.insights/components/fabrikamapp") |


## <a name="notes"></a>Notizen

* Sie benötigen Lesezugriff auf die Anwendung.
* Bei der Identifizierung einer Anwendung über ihren Namen wird vorausgesetzt, dass er in allen zugänglichen Abonnements eindeutig ist. Sollten mehrere Anwendungen mit dem angegebenen Namen vorhanden sein, ist die Abfrage aufgrund der Mehrdeutigkeit nicht erfolgreich. In diesem Fall muss einer der anderen Bezeichner verwendet werden.
* Verwenden Sie den verwandten Ausdruck [workspace](workspace-expression.md) für übergreifende Abfragen über Log Analytics-Arbeitsbereiche.
* Der app()-Ausdruck wird derzeit bei Verwendung des Azure-Portals nur dann zum Erstellen einer [benutzerdefinierten Warnungsregel für die Protokollsuche](../platform/alerts-log.md) in der Suchabfrage unterstützt, wenn als Ressource für die Warnungsregel eine Application Insights-Anwendung verwendet wird.

## <a name="examples"></a>Beispiele

```Kusto
app("fabrikamapp").requests | count
```
```Kusto
app("AI-Prototype/Fabrikam/fabrikamapp").requests | count
```
```Kusto
app("b438b4f6-912a-46d5-9cb1-b44069212ab4").requests | count
```
```Kusto
app("/subscriptions/7293b69-db12-44fc-9a66-9c2005c3051d/resourcegroups/Fabrikam/providers/microsoft.insights/components/fabrikamapp").requests | count
```
```Kusto
union 
(workspace("myworkspace").Heartbeat | where Computer contains "Con"),
(app("myapplication").requests | where cloud_RoleInstance contains "Con")
| count  
```
```Kusto
union 
(workspace("myworkspace").Heartbeat), (app("myapplication").requests)
| where TimeGenerated between(todatetime("2018-02-08 15:00:00") .. todatetime("2018-12-08 15:05:00"))
```

## <a name="next-steps"></a>Nächste Schritte

- Informationen zum Verweisen auf Log Analytics-Arbeitsbereiche finden Sie unter [workspace-Ausdruck](workspace-expression.md).
- Informationen über die Art der [Speicherung von Log Analytics-Daten](../../azure-monitor/log-query/log-query-overview.md).