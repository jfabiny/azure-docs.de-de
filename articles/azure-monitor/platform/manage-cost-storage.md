---
title: Verwalten von Nutzung und Kosten für Azure Log Analytics | Microsoft-Dokumentation
description: Hier erfahren Sie, wie Sie in Azure den Tarif ändern und das Datenvolumen sowie die Aufbewahrungsrichtlinie für Ihren Log Analytics-Arbeitsbereich verwalten.
services: log-analytics
documentationcenter: log-analytics
author: mgoedtel
manager: carmonm
editor: ''
ms.assetid: ''
ms.service: log-analytics
ms.workload: na
ms.tgt_pltfrm: na
ms.topic: conceptual
ms.date: 01/10/2018
ms.author: magoedte
ms.subservice: ''
ms.openlocfilehash: 3372d399c339133fc0ee3dbfd031ec3c4c03cc3b
ms.sourcegitcommit: 644de9305293600faf9c7dad951bfeee334f0ba3
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2019
ms.locfileid: "54901158"
---
# <a name="manage-usage-and-costs-for-log-analytics"></a>Verwalten von Nutzung und Kosten für Log Analytics

> [!NOTE]
> In diesem Artikel wird beschrieben, wie Sie Ihre Kosten in Log Analytics durch Festlegen des Datenaufbewahrungszeitraums steuern.  Entsprechende Informationen finden Sie in den folgenden Artikeln.
> - [Analysieren der Datennutzung in Log Analytics](manage-cost-storage.md) beschreibt, wie Sie Ihre Datennutzung analysieren und Warnungen dazu ausgeben.
> - [Überwachen der Nutzung und der geschätzten Kosten](usage-estimated-costs.md) beschreibt, wie die Nutzung und geschätzten Kosten über mehrere Azure-Überwachungsfeatures hinweg für unterschiedliche Preismodelle angezeigt werden. Außerdem wird beschrieben, wie Sie Ihr Preismodell ändern können.

Log Analytics ist für die Skalierung und Unterstützung der täglichen Sammlung, Indizierung und Speicherung enormer Datenmengen aus beliebigen Quellen in Ihrem Unternehmen oder aus in Azure bereitgestellten Quellen konzipiert.  Dies ist zwar ggf. die primäre Motivation für die Verwendung in Ihrem Unternehmen, letztendlich geht es jedoch um Kosteneffizienz. In diesem Zusammenhang ist es wichtig zu wissen, dass die Kosten eines Log Analytics-Arbeitsbereichs nicht nur auf dem Umfang der gesammelten Daten basieren, sondern auch davon abhängen, welcher Tarif gewählt wurde und wie lange die von den verbundenen Quellen generierten Daten gespeichert werden sollen.  

In diesem Artikel erfahren Sie, wie Sie Datenvolumen und Speicherwachstum proaktiv überwachen und Grenzwerte festlegen, um die damit verbundenen Kosten zu steuern. 

Für Daten können abhängig von den folgenden Faktoren erhebliche Kosten anfallen: 

- Umfang der Daten, die generiert und im Arbeitsbereich erfasst werden 
    - Anzahl der aktivierten Verwaltungslösungen
    - Anzahl der überwachten Systeme
    - Typ der Daten, die von jeder überwachten Ressource gesammelt wurden 
- Die Zeitspanne, für Sie Ihre Daten aufbewahren möchten 

## <a name="understand-your-workspaces-usage-and-estimated-cost"></a>Verstehen von Nutzung und geschätzten Kosten Ihres Arbeitsbereichs
Mit Log Analytics können Sie auf der Grundlage aktueller Nutzungsmuster problemlos die zu erwartenden Kosten ermitteln.  Verwenden Sie **Analysieren der Datennutzung in Log Analytics**, um die Datennutzung zu überprüfen und zu analysieren. Hier wird angezeigt, wie viele Daten von jeder Lösung gesammelt werden, wie viele Daten aufbewahrt werden, und es wird eine Kostenschätzung angezeigt. Diese basiert auf der Menge an erfassten Daten und berücksichtigt eine eventuelle zusätzliche Aufbewahrung über die enthaltenen Menge hinaus.

![Nutzung und geschätzte Kosten](media/manage-cost-storage/usage-estimated-cost-dashboard-01.png)

Um Ihre Dateien ausführlicher zu untersuchen, klicken Sie auf der Seite **Nutzung und geschätzte Kosten** auf das Symbol oben rechts neben den Diagrammen. Sie können mit dieser Abfrage weitere Details zu Ihrer Nutzung abrufen.  

![Ansicht „Protokolle“](media/manage-cost-storage/logs.png)

Auf der Seite **Nutzung und geschätzte Kosten** können Sie Ihr Datenvolumen für den Monat überprüfen. Dieses beinhaltet alle Daten, die in Ihrem Log Analytics-Arbeitsbereich empfangen und aufbewahrt wurden.  Klicken Sie im oberen Bereich der Seite auf **Nutzungsdetails**, um das Dashboard „Nutzung“ anzuzeigen. Dort finden Sie Informationen zu Datenvolumentrends nach Quelle, Computern und Angebot. Klicken Sie auf **Datenmengenverwaltung**, um die tägliche Obergrenze anzuzeigen oder festzulegen oder um die Aufbewahrungsdauer zu ändern.
 
Die Gebühren für Log Analytics fließen in Ihre Azure-Rechnung ein. Die Details Ihrer Azure-Rechnung finden Sie im Bereich „Abrechnung“ des Azure-Portals oder im [Azure-Abrechnungsportal](https://account.windowsazure.com/Subscriptions).  

## <a name="daily-cap"></a>Tägliche Obergrenze
Sie können eine tägliche Obergrenze konfigurieren und die tägliche Erfassung für Ihren Arbeitsbereich einschränken. Dabei ist jedoch Vorsicht geboten, da dieses Limit möglichst nicht erreicht werden sollte.  Andernfalls verlieren Sie die Daten des restlichen Tages. Dies kann sich auf Azure-Dienste und -Lösungen auswirken, deren Funktionalität unter Umständen von der Verfügbarkeit aktueller Daten im Arbeitsbereich abhängt.  Infolgedessen kann auch die Integrität von Ressourcen, die IT-Diensten zugrunde liegen, nicht mehr zuverlässig überwacht werden, und es können keine Warnungen empfangen werden.  Die tägliche Obergrenze ist dazu gedacht, einen unerwarteten Anstieg des Datenvolumens aus Ihren verwalteten Ressourcen zu verhindern und den Grenzwert einzuhalten – oder einfach ungeplante Gebühren für Ihren Arbeitsbereich zu vermeiden.  

Bei Erreichen des Tageslimits werden für den Rest des Tages keine kostenpflichtigen Datentypen mehr gesammelt. Im oberen Seitenbereich erscheint ein Warnbanner für den ausgewählten Log Analytics-Arbeitsbereich, und an die Tabelle *Operation* wird unter der Kategorie **LogManagement** ein Vorgangsereignis gesendet. Die Datensammlung wird nach der unter *Daily limit will be set at* (Tageslimit wird festgelegt um) definierten Zurücksetzungszeit fortgesetzt. Es empfiehlt sich, eine Warnungsregel auf der Grundlage dieses Vorgangsereignisses zu definieren und so zu konfigurieren, dass bei Erreichen des Tageslimits für Daten eine Benachrichtigung erfolgt. 

### <a name="identify-what-daily-data-limit-to-define"></a>Identifizieren des zu definierenden Tageslimits für Daten 
Informieren Sie sich unter [Analysieren der Datennutzung in Log Analytics](usage-estimated-costs.md) über den Datenerfassungstrend sowie über die zu definierende tägliche Volumenobergrenze. Wählen Sie die Obergrenze mit Bedacht, da Sie Ihre Ressourcen nach Erreichen des Limits nicht mehr überwachen können. 

### <a name="manage-the-maximum-daily-data-volume"></a>Verwalten des maximalen täglichen Datenvolumens 
In den folgenden Schritten erfahren Sie, wie Sie ein Tageslimit für die von Log Analytics erfasste Datenmenge konfigurieren.  

1. Klicken Sie links in Ihrem Arbeitsbereich auf **Nutzung und geschätzte Kosten**.
2. Klicken Sie im oberen Bereich der Seite **Nutzung und geschätzte Kosten** für den ausgewählten Arbeitsbereich auf **Datenmengenverwaltung**. 
3. Die tägliche Obergrenze ist standardmäßig **AUS**. Klicken Sie auf **EIN**, um sie zu aktivieren, und legen Sie das Limit für das Datenvolumen in GB/Tag fest.<br><br> ![Konfigurieren des Log Analytics-Datenlimits](media/manage-cost-storage/set-daily-volume-cap-01.png)

### <a name="alert-when-daily-cap-reached"></a>Warnung bei Erreichen der täglichen Obergrenze
Im Azure-Portal wird bei Erreichen des Schwellenwerts für das Datenlimit zwar ein visueller Hinweis angezeigt, dieses Verhalten steht jedoch möglicherweise nicht im Einklang mit der gewünschten Behandlung von Betriebsproblemen, die eine umgehende Reaktion erfordern.  Wenn Sie eine Warnbenachrichtigung erhalten möchten, können Sie in Azure Monitor eine neue Warnregel erstellen.  Weitere Informationen finden Sie unter [Erstellen, Anzeigen und Verwalten von Warnungen mithilfe von Azure Monitor – Warnungen (Vorschauversion)](alerts-metric.md).      

Im Anschluss finden Sie die empfohlenen Einstellungen für die Warnung:

* Ziel: Wählen Sie Ihre Log Analytics-Ressource aus.
* Kriterien: 
   * Signalname: Benutzerdefinierte Protokollsuche
   * Suchabfrage: Operation | where Detail has 'OverQuota'
   * Basierend auf: Anzahl der Ergebnisse
   * Bedingung: Größer als
   * Schwellenwert: 0
   * Zeitraum: 5 (Minuten)
   * Häufigkeit: 5 (Minuten)
* Name der Warnungsregel: Daily data limit reached
* Schweregrad: Warnung (Schweregrad 1)

Nachdem die Warnung definiert wurde, wird bei Erreichen des Limits eine Warnung ausgelöst und die in der Aktionsgruppe definierte Reaktion ausgeführt. Dadurch kann Ihr Team per E-Mail und SMS benachrichtigt werden, und es können Aktionen mithilfe von Webhooks oder Automation-Runbooks oder mittels [Integration in eine externe ITSM-Lösung](itsmc-overview.md#create-itsm-work-items-from-azure-alerts) automatisiert werden. 

## <a name="change-the-data-retention-period"></a>Ändern des Datenaufbewahrungszeitraums 
Die folgenden Schritte zeigen, wie Sie die Aufbewahrungsdauer von Protokolldaten in Ihrem Arbeitsbereich konfigurieren.
 
1. Klicken Sie links in Ihrem Arbeitsbereich auf **Nutzung und geschätzte Kosten**.
2. Klicken Sie im oberen Bereich der Seite **Nutzung und geschätzte Kosten** auf **Datenmengenverwaltung**.
5. Passen Sie mithilfe des Schiebereglers die Anzahl von Tagen an, und klicken Sie anschließend auf **OK**.  Wenn Sie sich im Tarif *Free* befinden, können Sie den Datenaufbewahrungszeitraum nicht ändern. Sie müssen in einen kostenpflichtigen Tarif wechseln, um diese Einstellung zu steuern.<br><br> ![Ändern des Datenaufbewahrungszeitraums für den Arbeitsbereich](media/manage-cost-storage/manage-cost-change-retention-01.png)

## <a name="legacy-pricing-tiers"></a>Legacytarife

Wenn Sie ein Enterprise Agreement vor dem 1. Juli 2018 unterzeichnet haben oder wenn Sie bereits einen Log Analytics-Arbeitsbereich in einem Abonnement erstellt haben, können Sie weiterhin auf den Tarif *Free* zugreifen. Wenn Ihr Abonnement nicht an eine vorhandene EA-Registrierung gebunden ist, steht der Tarif *Free* nicht zur Verfügung, wenn Sie nach dem 2. April 2018 einen Arbeitsbereich in einem neuen Abonnement erstellen.  Im Tarif *Free* ist die Aufbewahrung von Daten auf sieben Tage beschränkt.  Für die Legacytarife *Eigenständig* oder *Pro Knoten* sowie den aktuellen einzigen Tarif für 2018 sind die gesammelten Daten für die letzten 31 Tage verfügbar. Im Tarif *Free* liegt das Erfassungslimit bei 500MB pro Tag. Sollten Sie dieses zulässige Volumen immer wieder überschreiten, können Sie Ihren Arbeitsbereich auf einen anderen Tarif umstellen, um Daten über diesen Grenzwert hinaus zu sammeln. 

> [!NOTE]
> Wenn Sie die Berechtigungen nutzen möchten, die Sie durch den Kauf der OMS E1-Suite, OMS E2-Suite oder des OMS-Add-Ons für System Center erwerben, wählen Sie den Tarif *Pro Knoten* für Log Analytics aus.

## <a name="changing-pricing-tier"></a>Ändern des Tarifs

Wenn Ihr Log Analytics-Arbeitsbereich über Zugriff auf Legacytarife verfügt, können Sie auf folgende Weise zwischen Legacytarifen wechseln:

1. Wählen Sie im Azure-Portal im Bereich mit den Log Analytics-Abonnements einen Arbeitsbereich aus.

2. Klicken Sie im Bereich des Arbeitsbereichs unter **Allgemein** auf **Tarif**.  

3. Wählen Sie unter **Tarif** einen Tarif aus, und klicken Sie anschließend auf **Auswählen**.  
    ![Ausgewählter Tarif](media/manage-cost-storage/workspace-pricing-tier-info.png)

Wenn Sie Ihren Arbeitsbereich in den aktuellen Tarif verschieben möchten, müssen Sie das [Überwachungspreismodell Ihres Abonnements in Azure Monitor ändern](https://docs.microsoft.com/en-us/azure/azure-monitor/platform/usage-estimated-costs#moving-to-the-new-pricing-model). Dadurch ändert sich der Tarif für alle Arbeitsbereiche in diesem Abonnement.

> [!NOTE]
> Falls Ihr Arbeitsbereich mit einem Automation-Konto verknüpft ist und Sie den Tarif *Standalone (Per GB)* (Eigenständig (pro GB)) auswählen möchten, müssen Sie zuvor alle Lösungen vom Typ **Automation & Control** löschen und die Verknüpfung mit dem Automation-Konto aufheben. Klicken Sie auf dem Blatt für den Arbeitsbereich unter **Allgemein** auf **Lösungen**, um die Lösungen anzuzeigen und zu löschen. Klicken Sie zum Aufheben der Verknüpfung mit dem Automation-Konto auf dem Blatt **Tarif** auf den Namen des Automatisierungskontos.


## <a name="troubleshooting-why-log-analytics-is-no-longer-collecting-data"></a>Beheben des Problems, dass Log Analytics keine Daten mehr erfasst
Wenn Sie den kostenlosen Legacytarif nutzen und an einem Tag mehr als 500MB Daten gesendet haben, wird die Datensammlung für den Rest des Tages beendet. Das Erreichen des Tageslimits ist häufig die Ursache dafür, dass Log Analytics die Datensammlung beendet oder Daten scheinbar fehlen.  Log Analytics erstellt ein Ereignis vom Typ „Operation“, wenn die Datensammlung beginnt und endet. Führen Sie die folgende Abfrage in der Suche aus, um zu überprüfen, ob Sie das Tageslimit erreichen und Daten fehlen: 

`Operation | where OperationCategory == 'Data Collection Status' `

Wenn die Datensammlung beendet wird, hat „OperationStatus“ den Wert „Warning“ (Warnung). Wenn die Datensammlung beginnt, hat „OperationStatus“ den Wert „Succeeded“ (Erfolgreich). Die folgende Tabelle beschreibt die Gründe, warum die Datensammlung endet, und eine empfohlene Aktion zum Fortsetzen der Datensammlung:  

|Grund für die Beendigung der Datensammlung| Lösung| 
|-----------------------|---------|
|Tageslimit oder kostenloser Legacytarif erreicht |Warten Sie, bis die Datensammlung am Folgetag automatisch neu gestartet wird, oder wechseln Sie zu einem kostenpflichtigen Tarif.|
|Tägliche Obergrenze des Arbeitsbereichs wurde erreicht|Warten Sie, bis die Datensammlung am Folgetag automatisch neu gestartet wird, oder erhöhen Sie das Tageslimit für das Datenvolumen, wie unter [Verwalten des maximalen täglichen Datenvolumens](#manage-the-maximum-daily-volume) beschrieben. Der Zeitpunkt für das Zurücksetzen der täglichen Obergrenze wird auf der Seite **Datenmengenverwaltung** angezeigt. |
|Das Azure-Abonnement befindet sich aus folgendem Grund in einem angehaltenen Zustand:<br> Kostenlose Testversion endete<br> Azure Pass ist abgelaufen<br> Monatliches Ausgabenlimit ist erreicht (z.B. in einem MSDN- oder Visual Studio-Abonnement)|Konvertieren in ein kostenpflichtiges Abonnement<br> Limit entfernen oder warten, bis das Limit zurückgesetzt wird|

Um benachrichtigt zu werden, wenn die Datensammlung endet, verwenden Sie die Schritte zum *Erstellen einer täglichen Datenobergrenze*, um eine Benachrichtigung zu erhalten, wenn die Datensammlung beendet wird, und verwenden Sie die Schritte zum Hinzufügen von Aktionen zu Warnungsregeln, um eine E-Mail-, Webhook- oder Runbook-Aktion für die Warnungsregel zu konfigurieren. 

## <a name="troubleshooting-why-usage-is-higher-than-expected"></a>Ermittlung per Problembehandlung, warum die Nutzung höher als erwartet ist
Eine höhere Nutzung wird durch eine bzw. beide der folgenden Bedingungen verursacht:
- Mehr Daten als erwartet werden an Log Analytics gesendet
- Mehr Knoten als erwartet senden Daten an Log Analytics

### <a name="data-volume"></a>Datenvolume 
Auf der Seite **Nutzung und geschätzte Kosten** zeigt das Diagramm *Datenerfassung pro Lösung* die Gesamtmenge an gesendeten Daten sowie die von jeder Lösung gesendete Datenmenge an. Auf diese Weise können Sie Trends ermitteln, z.B. ob die Gesamtdatennutzung (oder die Nutzung durch eine bestimmte Lösung) ansteigt, konstant bleibt oder abnimmt. Um diese Daten zu generieren, wird die folgende Abfrage verwendet:

`Usage| where TimeGenerated > startofday(ago(31d))| where IsBillable == true
| summarize TotalVolumeGB = sum(Quantity) / 1024 by bin(TimeGenerated, 1d), Solution| render barchart`

Beachten Sie, dass durch die Klausel „where IsBillable = true“ Datentypen bestimmter Lösungen herausgefiltert werden, für die keine Erfassungsgebühren anfallen. 

Sie können einen Drilldown durchführen, um Datentrends für spezifische Datentypen anzuzeigen. So können Sie beispielsweise die Daten aufgrund von IIS-Protokollen untersuchen:

`Usage| where TimeGenerated > startofday(ago(31d))| where IsBillable == true
| where DataType == "W3CIISLog"
| summarize TotalVolumeGB = sum(Quantity) / 1024 by bin(TimeGenerated, 1d), Solution| render barchart`

### <a name="nodes-sending-data"></a>Knoten, die Daten senden

Um die Anzahl von Computern (Knoten) zu ermitteln, die im letzten Monat täglich Daten gemeldet haben, verwenden Sie die folgende Abfrage:

`Heartbeat | where TimeGenerated > startofday(ago(31d))
| summarize dcount(Computer) by bin(TimeGenerated, 1d)    
| render timechart`

Zum Abrufen einer Liste von Computern, die **kostenpflichtige Datentypen** senden (einige Datentypen sind kostenlos), verwenden Sie die [_IsBillable](log-standard-properties.md#isbillable)-Eigenschaft:

`union withsource = tt * 
| where _IsBillable == true 
| extend computerName = tolower(tostring(split(Computer, '.')[0]))
| where computerName != ""
| summarize TotalVolumeBytes=sum(_BilledSize) by computerName`

Verwenden Sie diese `union withsource = tt *`-Abfragen mit Bedacht, da umfassende Scans verschiedener Datentypen kostenintensiv sind. 

Diese Abfrage kann so erweitert werden, dass die Anzahl von Computern pro Stunde zurückgegeben wird, die kostenpflichtige Datentypen senden:

`union withsource = tt * 
| where _IsBillable == true 
| extend computerName = tolower(tostring(split(Computer, '.')[0]))
| where computerName != ""
| summarize dcount(computerName) by bin(TimeGenerated, 1h) | sort by TimeGenerated asc`

Um die **Größe** der pro Computer erfassten abrechenbaren Ereignisse anzuzeigen, verwenden Sie die `_BilledSize`-Eigenschaft, die die Größe in Bytes bereitstellt:

`union withsource = tt * 
| where _IsBillable == true 
| summarize Bytes=sum(_BilledSize) by  Computer | sort by Bytes nulls last `

Diese Abfrage ersetzt die alte Abfrage durch den Datentyp für die Nutzung. 

Um die **Anzahl** von erfassten Ereignissen pro Computer anzuzeigen, führen Sie diese Abfrage aus:

`union withsource = tt *
| summarize count() by Computer | sort by count_ nulls last`

Um die Anzahl von Ereignissen pro Computer anzuzeigen, für die Gebühren anfallen, verwenden Sie diese Abfrage: 

`union withsource = tt * 
| where _IsBillable == true 
| summarize count() by Computer  | sort by count_ nulls last`

Wenn Sie die Anzahl für gebührenpflichtigen Datentypen anzeigen möchten, die Daten an einen bestimmten Computer senden, verwenden Sie Folgendes:

`union withsource = tt *
| where Computer == "computer name"
| where _IsBillable == true 
| summarize count() by tt | sort by count_ nulls last `

> [!NOTE]
> Einige der Felder vom Typ „Nutzungsdaten“ sind zwar weiterhin im Schema enthalten, jedoch veraltet, und ihre Werte werden nicht mehr aufgefüllt. Dies sind neben **Computer** Felder in Bezug auf die Erfassung: **TotalBatches**, **BatchesWithinSla**, **BatchesOutsideSla**, **BatchesCapped** und **AverageProcessingTimeMs**.

Wenn Sie die Datenquelle für einen bestimmten Datentyp näher untersuchen möchten, finden Sie hier einige nützliche Beispielabfragen:

+ **Sicherheitslösung**
  - `SecurityEvent | summarize AggregatedValue = count() by EventID`
+ **Protokollverwaltungslösung**
  - `Usage | where Solution == "LogManagement" and iff(isnotnull(toint(IsBillable)), IsBillable == true, IsBillable == "true") == true | summarize AggregatedValue = count() by DataType`
+ Datentyp **Perf**
  - `Perf | summarize AggregatedValue = count() by CounterPath`
  - `Perf | summarize AggregatedValue = count() by CounterName`
+ Datentyp **Event**
  - `Event | summarize AggregatedValue = count() by EventID`
  - `Event | summarize AggregatedValue = count() by EventLog, EventLevelName`
+ Datentyp **Syslog**
  - `Syslog | summarize AggregatedValue = count() by Facility, SeverityLevel`
  - `Syslog | summarize AggregatedValue = count() by ProcessName`
+ Datentyp **AzureDiagnostics**
  - `AzureDiagnostics | summarize AggregatedValue = count() by ResourceProvider, ResourceId`

### <a name="tips-for-reducing-data-volume"></a>Tipps zum Reduzieren der Datenmenge

Hier finden Sie einige Vorschläge zum Verringern der erfassten Protokolle:

| Quelle mit hohem Datenvolumen | Reduzieren des Datenvolumens |
| -------------------------- | ------------------------- |
| Sicherheitsereignisse            | Wählen Sie [Sicherheitsereignisse vom Typ „Allgemein“ oder „Minimal“](https://docs.microsoft.com/en-us/azure/security-center/security-center-enable-data-collection#data-collection-tier) aus. <br> Ändern der Sicherheitsüberwachungsrichtlinie, sodass nur benötigte Ereignisse erfasst werden. Überprüfen Sie insbesondere die Notwendigkeit zum Erfassen von Ereignissen für die <br> - [Überwachung der Filterplattform](https://technet.microsoft.com/library/dd772749(WS.10).aspx) <br> - [Überwachung der Registrierung](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd941614(v%3dws.10))<br> - [Überwachung des Dateisystems](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd772661(v%3dws.10))<br> - [Überwachung des Kernelobjekts](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd941615(v%3dws.10))<br> - [Überwachung der Handleänderung](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/dd772626(v%3dws.10))<br> - Überwachung von Wechselmedien |
| Leistungsindikatoren       | Ändern Sie [Leistungsindikatoren-Konfiguration](data-sources-performance-counters.md) in: <br> - Reduzieren der Sammlungshäufigkeit <br> - Reduzieren der Anzahl von Leistungsindikatoren |
| Ereignisprotokolle                 | Ändern Sie die [Ereignisprotokollkonfiguration](data-sources-windows-events.md) in: <br> - Reduzieren der Anzahl von erfassten Ereignisprotokollen <br> - Ausschließliches Erfassen von erforderlichen Ereignisebenen. Erfassen Sie beispielsweise keine Ereignisse der Ebene *Informationen*. |
| syslog                     | Ändern Sie die [syslog-Konfiguration](data-sources-syslog.md) in: <br> - Reduzieren der Anzahl von erfassten Einrichtungen <br> - Ausschließliches Erfassen von erforderlichen Ereignisebenen. Erfassen Sie beispielsweise keine Ereignisse der Ebenen *Informationen* und *Debuggen*. |
| AzureDiagnostics           | Ändern Sie die Ressourcenprotokollsammlung, um Folgendes zu erreichen: <br> - Verringern der Anzahl von Ressourcen, die Protokolle an Log Analytics senden <br> - Ausschließliches Erfassen von erforderlichen Protokollen |
| Lösungsdaten von Computern, für die die Lösung nicht erforderlich ist | Verwenden Sie die [Zielgruppenadressierung für Lösungen](../insights/solution-targeting.md), um Daten nur für erforderliche Gruppen mit Computern zu erfassen. |

### <a name="getting-node-counts"></a>Abrufen der Knotenanzahl 

Wenn Sie den Tarif „Pro Knoten (OMS)“ nutzen, erfolgt die Abrechnung basierend auf der Anzahl von verwendeten Knoten und Lösungen. Die Anzahl von Insights- und Analytics-Knoten, für die Sie Gebühren entrichten, wird in der Tabelle auf der Seite **Nutzung und geschätzte Kosten** angezeigt.  

Um die Anzahl der verschiedenen Sicherheitsknoten anzuzeigen, können Sie diese Abfrage verwenden:

`union
(
    Heartbeat
    | where (Solutions has 'security' or Solutions has 'antimalware' or Solutions has 'securitycenter')
    | project Computer
),
(
    ProtectionStatus
    | where Computer !in~
    (
        (
            Heartbeat
            | project Computer
        )
    )
    | project Computer
)
| distinct Computer
| project lowComputer = tolower(Computer)
| distinct lowComputer
| count`

Die Anzahl der verschiedenen Automation-Knoten können Sie mit dieser Abfrage anzeigen:

` ConfigurationData 
 | where (ConfigDataType == "WindowsServices" or ConfigDataType == "Software" or ConfigDataType =="Daemons") 
 | extend lowComputer = tolower(Computer) | summarize by lowComputer 
 | join (
     Heartbeat 
       | where SCAgentChannel == "Direct"
       | extend lowComputer = tolower(Computer) | summarize by lowComputer, ComputerEnvironment
 ) on lowComputer
 | summarize count() by ComputerEnvironment | sort by ComputerEnvironment asc`

## <a name="create-an-alert-when-data-collection-is-higher-than-expected"></a>Erstellen einer Warnung für den Fall, dass die Datensammlung höher als erwartet ist
In diesem Abschnitt wird beschrieben, wie Sie eine Warnung erstellen, wenn Folgendes gilt:
- Das Datenvolumen übersteigt eine angegebene Menge.
- Für das Datenvolumen besteht die Vorhersage, dass eine bestimmte Menge überschritten wird.

Azure-Warnungen unterstützen [Protokollwarnungen](alerts-unified-log.md), die Suchabfragen nutzen. 

Für die folgende Abfrage wird ein Ergebnis erzielt, wenn innerhalb der letzten 24 Stunden mehr als 100 GB an Daten gesammelt wurden:

`union withsource = $table Usage | where QuantityUnit == "MBytes" and iff(isnotnull(toint(IsBillable)), IsBillable == true, IsBillable == "true") == true | extend Type = $table | summarize DataGB = sum((Quantity / 1024)) by Type | where DataGB > 100`

Für die folgende Abfrage wird eine einfache Formel verwendet, um vorherzusagen, wenn an einem Tag mehr als 100 GB an Daten gesendet werden: 

`union withsource = $table Usage | where QuantityUnit == "MBytes" and iff(isnotnull(toint(IsBillable)), IsBillable == true, IsBillable == "true") == true | extend Type = $table | summarize EstimatedGB = sum(((Quantity * 8) / 1024)) by Type | where EstimatedGB > 100`

Wenn die Warnung für ein anderes Datenvolumen gelten soll, ändern Sie den Wert 100 in den Abfragen einfach in den gewünschten GB-Wert.

Führen Sie die Schritte unter [Erstellen, Anzeigen und Verwalten von Warnungen mithilfe von Azure Monitor](alerts-metric.md) aus, um eine Benachrichtigung zu erhalten, wenn die Datensammlung höher als erwartet ausfällt.

Legen Sie beim Erstellen der Warnung für die erste Abfrage Folgendes fest, wenn mehr als 100 GB an Daten innerhalb von 24 Stunden anfallen:  

- **Definieren der Warnungsbedingung**: Festlegen Ihres Log Analytics-Arbeitsbereichs als Ressourcenziel
- **Warnungskriterien**: Geben Sie Folgendes an:
   - **Signalname**: **Benutzerdefinierte Protokollsuche**
   - **Suchabfrage** auf `union withsource = $table Usage | where QuantityUnit == "MBytes" and iff(isnotnull(toint(IsBillable)), IsBillable == true, IsBillable == "true") == true | extend Type = $table | summarize DataGB = sum((Quantity / 1024)) by Type | where DataGB > 100`
   - **Warnungslogik**: **Basiert auf** *Anzahl von Ergebnissen* und **Bedingung** ist *Größer als* ein **Schwellenwert** von *0*
   - **Zeitraum**: *1440* Minuten, **Warnungshäufigkeit**: alle *60* Minuten, da die Nutzungsdaten nur einmal pro Stunde aktualisiert werden
- **Definieren der Warnungsdetails**:
   - **Name** auf *Datenvolumen größer als 100 GB in 24 Stunden*
   - **Schweregrad** auf *Warnung*

Geben Sie eine vorhandene [Aktionsgruppe](action-groups.md) an, oder erstellen Sie eine neue, damit Sie benachrichtigt werden, wenn die Protokollwarnung Kriterien erfüllt.

Legen Sie beim Erstellen der Warnung für die zweite Abfrage Folgendes fest, wenn die Vorhersage besteht, dass innerhalb von 24 Stunden mehr als 100 GB an Daten anfallen:

- **Definieren der Warnungsbedingung**: Festlegen Ihres Log Analytics-Arbeitsbereichs als Ressourcenziel
- **Warnungskriterien**: Geben Sie Folgendes an:
   - **Signalname**: **Benutzerdefinierte Protokollsuche**
   - **Suchabfrage** auf `union withsource = $table Usage | where QuantityUnit == "MBytes" and iff(isnotnull(toint(IsBillable)), IsBillable == true, IsBillable == "true") == true | extend Type = $table | summarize EstimatedGB = sum(((Quantity * 8) / 1024)) by Type | where EstimatedGB > 100`
   - **Warnungslogik**: **Basiert auf** *Anzahl von Ergebnissen* und **Bedingung** ist *Größer als* ein **Schwellenwert** von *0*
   - **Zeitraum**: *180* Minuten, **Warnungshäufigkeit**: alle *60* Minuten, da die Nutzungsdaten nur einmal pro Stunde aktualisiert werden
- **Definieren der Warnungsdetails**:
   - **Name** auf *Erwartetes Datenvolumen von mehr als 100 GB in 24 Stunden*
   - **Schweregrad** auf *Warnung*

Geben Sie eine vorhandene [Aktionsgruppe](action-groups.md) an, oder erstellen Sie eine neue, damit Sie benachrichtigt werden, wenn die Protokollwarnung Kriterien erfüllt.

Wenn Sie eine Warnung erhalten, können Sie die Schritte im folgenden Abschnitt verwenden, um per Problembehandlung zu ermitteln, warum die Nutzung höher als erwartet ist.

## <a name="next-steps"></a>Nächste Schritte
* Informationen dazu, wie Sie die Suchsprache verwenden, finden Sie unter [Protokollsuchen in Log Analytics](../log-query/log-query-overview.md). Sie können Suchabfragen verwenden, um für die Nutzungsdaten eine zusätzliche Analyse durchzuführen.
* Führen Sie die unter [Erstellen, Anzeigen und Verwalten von Warnungen mithilfe von Azure Monitor](alerts-metric.md) beschriebenen Schritte aus, um benachrichtigt zu werden, wenn ein Suchkriterium erfüllt ist.
* Verwenden Sie die [Zielgruppenadressierung für Lösungen](../insights/solution-targeting.md), um Daten nur für erforderliche Gruppen mit Computern zu erfassen.
* Lesen Sie zum Konfigurieren einer effektiven Richtlinie zur Erfassung von Ereignissen die Informationen unter [Datensammlung in Azure Security Center](../../security-center/security-center-enable-data-collection.md).
* Ändern Sie die [Leistungsindikatorenkonfiguration](data-sources-performance-counters.md).
* Informationen zum Ändern der Einstellungen für die Ereigniserfassung finden Sie unter [Datenquellen für Windows-Ereignisprotokolle in Log Analytics](data-sources-windows-events.md).
* Informationen zum Ändern der Einstellungen für die Syslog-Sammlung finden Sie unter [Syslog-Datenquellen in Log Analytics](data-sources-syslog.md).


