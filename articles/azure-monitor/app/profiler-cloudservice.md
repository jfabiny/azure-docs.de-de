---
title: Erstellen von Profilen für Azure Cloud Services-Liveinstanzen mit Application Insights | Microsoft-Dokumentation
description: Aktivieren von Application Insights Profiler für Azure Cloud Services.
services: application-insights
documentationcenter: ''
author: mrbullwinkle
manager: carmonm
ms.service: application-insights
ms.workload: tbd
ms.tgt_pltfrm: ibiza
ms.topic: conceptual
ms.reviewer: cawa
ms.date: 08/06/2018
ms.author: mbullwin
ms.openlocfilehash: 76512a2c930f44ae5a9b57d85ca34544788a538a
ms.sourcegitcommit: 9999fe6e2400cf734f79e2edd6f96a8adf118d92
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/22/2019
ms.locfileid: "54435888"
---
# <a name="profile-live-azure-cloud-services-with-application-insights"></a>Erstellen von Profilen für Azure Cloud Services-Liveinstanzen mit Application Insights

Application Insights Profiler kann auch für diese Dienste bereitgestellt werden:
* [Azure App Service](profiler.md?toc=/azure/azure-monitor/toc.json)
* [Azure Service Fabric-Anwendungen](profiler-servicefabric.md?toc=/azure/azure-monitor/toc.json)
* [Dokumentation zu virtuellen Computern](profiler-vm.md?toc=/azure/azure-monitor/toc.json)

Application Insights Profiler wird mit der Azure-Diagnoseerweiterung installiert. Sie müssen Azure-Diagnose nur so konfigurieren, dass Profiler installiert wird und Profile an Ihre Application Insights-Ressource sendet.

## <a name="enable-profiler-for-azure-cloud-services"></a>Aktivieren von Profiler für Azure Cloud Services
1. Stellen Sie sicher, dass Sie [.NET Framework 4.6.1](https://docs.microsoft.com/dotnet/framework/migration-guide/how-to-determine-which-versions-are-installed) oder höher verwenden. Dazu ist es ausreichend zu bestätigen, dass die *ServiceConfiguration.\*.cscfg*-Dateien einen `osFamily`-Wert von „5“ oder höher haben.

1. Fügen Sie das [Application Insights SDK für Azure Cloud Services](../../azure-monitor/app/cloudservices.md?toc=/azure/azure-monitor/toc.json) hinzu.

1. Verfolgen Sie Anforderungen mit Application Insights:

    * Für ASP.NET-Webrollen kann Application Insights die Anforderungen automatisch verfolgen.

    * Für Workerrollen müssen Sie [Code hinzufügen, um Anforderungen nachzuverfolgen](profiler-trackrequests.md?toc=/azure/azure-monitor/toc.json).

1. Konfigurieren Sie die Azure-Diagnoseerweiterung zum Aktivieren von Profiler. Gehen Sie dazu wie folgt vor:

    a. Suchen Sie wie hier gezeigt die [Azure-Diagnose](https://docs.microsoft.com/azure/monitoring-and-diagnostics/azure-diagnostics)-Datei *diagnostics.wadcfgx* für Ihre Anwendungsrolle:  

      ![Speicherort der Konfigurationsdatei für die Diagnose](./media/profiler-cloudservice/cloudservice-solutionexplorer.png)  

      Wenn Sie die Datei nicht finden können, lesen Sie [Einrichten der Diagnose für Azure Cloud Services und virtuelle Azure-Computer](https://docs.microsoft.com/azure/vs-azure-tools-diagnostics-for-cloud-services-and-virtual-machines#enable-diagnostics-in-cloud-service-projects-before-deploying-them).

    b. Fügen Sie den folgenden `SinksConfig`-Abschnitt als untergeordnetes Element von `WadCfg` hinzu:  

      ```xml
      <WadCfg>
        <DiagnosticMonitorConfiguration>...</DiagnosticMonitorConfiguration>
        <SinksConfig>
          <Sink name="MyApplicationInsightsProfiler">
            <!-- Replace with your own Application Insights instrumentation key. -->
            <ApplicationInsightsProfiler>00000000-0000-0000-0000-000000000000</ApplicationInsightsProfiler>
          </Sink>
        </SinksConfig>
      </WadCfg>
      ```

    > [!NOTE]
    > Wenn die Datei *diagnostics.wadcfgx* auch eine andere Senke vom Typ „ApplicationInsights“ enthält, müssen alle drei der folgenden Instrumentierungsschlüssel übereinstimmen:  
    > * Der von Ihrer Anwendung verwendete Schlüssel 
    > * Der von der „ApplicationInsights“-Senke verwendete Schlüssel 
    > * Der von der „ApplicationInsightsProfiler“-Senke verwendete Schlüssel 
    >
    > Sie finden den von der `ApplicationInsights`-Senke verwendeten tatsächlichen Instrumentierungsschlüsselwert in den *ServiceConfiguration.\*.cscfg*-Dateien. 
    > Ab dem Visual Studio 15.5 Azure SDK-Release müssen nur noch die von der Anwendung und der „ApplicationInsightsProfiler“-Senke verwendeten Instrumentierungsschlüssel übereinstimmen.

1. Stellen Sie Ihren Dienst mit der neuen Diagnosekonfiguration bereit, und Application Insights Profiler ist für die Ausführung in Ihrem Dienst konfiguriert.
 
## <a name="next-steps"></a>Nächste Schritte

* Generieren Sie Datenverkehr zu Ihrer Anwendung (starten Sie z.B. einen [Verfügbarkeitstest](monitor-web-app-availability.md)). Warten Sie dann 10 bis 15 Minuten, bis das Senden der Ablaufverfolgungen an die Application Insights-Instanz beginnt.
* Weitere Informationen finden Sie unter [Profiler-Ablaufverfolgungen](profiler-overview.md?toc=/azure/azure-monitor/toc.json) im Azure-Portal.
* Informationen zur Behandlung von Profiler-Problemen finden Sie unter [Problembehandlung für den Profiler](profiler-troubleshooting.md?toc=/azure/azure-monitor/toc.json).
