---
title: Includedatei
description: Includedatei
services: virtual-machines-linux, virtual-machines-windows
author: dlepow
ms.service: multiple
ms.topic: include
ms.date: 01/15/2019
ms.author: danlep
ms.custom: include file
ms.openlocfilehash: 7a136f34a7dd9fada23a4225b60223220c92c665
ms.sourcegitcommit: 9999fe6e2400cf734f79e2edd6f96a8adf118d92
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/22/2019
ms.locfileid: "54440420"
---
Organisationen haben hohen Computing-Bedarf. Zu diesen Big Compute-Workloads zählen unter anderem technische Entwicklungen und Analysen, die Berechnung finanzieller Risiken, das Rendern von Bildern, komplexe Modelle sowie Monte Carlo-Simulationen. 

Verwenden Sie die Azure-Cloud, um rechenintensive Linux- und Windows-Workloads effizient auszuführen – von parallelen Batchaufträgen bis hin zu herkömmlichen HPC-Simulationen. Führen Sie Ihre HPC- und Batchworkloads auf der Azure-Infrastruktur aus, und wählen Sie die Computedienste, Raster-Manager, Marketplace-Lösungen und von Anbietern gehosteten Anwendungen (SaaS) je nach Bedarf aus. In Azure werden flexible Lösungen bereitgestellt, mit denen Arbeit verteilt und auf Tausende VMs oder Kerne skaliert werden kann. Später können Sie das zentrale Herunterskalieren durchführen, wenn Sie weniger Ressourcen benötigen. 

## <a name="solution-options"></a>Lösungsoptionen

* **Do-It-Yourself-Lösungen**
    * Richten Sie auf virtuellen Azure-Computern oder in [VM-Skalierungsgruppen](../articles/virtual-machine-scale-sets/virtual-machine-scale-sets-overview.md) Ihre eigene Clusterumgebung ein. 
    * Führen Sie für einen lokalen Cluster einen Lift & Shift-Vorgang durch, oder stellen Sie in Azure einen neuen Cluster bereit, um die Kapazität zu erhöhen. 
    * Verwenden Sie Azure Resource Manager-Vorlagen, um führende [Workload-Manager](#workload-managers), Infrastruktur und [Anwendungen](#hpc-applications) bereitzustellen. 
    * Wählen Sie [HPC- und GPU-VM-Größen](#hpc-and-gpu-sizes) aus, die spezielle Hardware und Netzwerkverbindungen für MPI- oder GPU-Workloads enthalten. 
    * Fügen Sie [Hochleistungsspeicher](#hpc-storage) für Workloads mit hoher E/A-Intensität hinzu.
* **Hybridlösungen**
    * Erweitern Ihrer lokalen Lösung, um Spitzenworkloads auf die Azure-Infrastruktur zu verlagern („Burst“)
    * Verwenden Sie bei Bedarf das Cloud Computing für Ihren vorhandenen [Workload-Manager](#workload-manager).
    * Nutzen Sie [HPC- und GPU-VM-Größen](#hpc-and-gpu-sizes) für MPI- oder GPU-Workloads.
* **Big Compute-Lösungen als Dienst**
    * Entwickeln Sie benutzerdefinierte Big Compute-Lösungen und -Workflows, indem Sie [Azure CycleCloud](#azure-cyclecloud), [Azure Batch](#azure-batch) und die dazugehörigen [Azure-Dienste](#related-azure-services) verwenden.
    * Führen Sie Azure-fähige Engineering -und Simulationslösungen verschiedener Anbieter aus, z.B. [Altair](http://www.altair.com/), [Rescale](https://www.rescale.com/azure/) und [Cycle Computing](https://cyclecomputing.com/) (jetzt [Teil von Microsoft](https://blogs.microsoft.com/blog/2017/08/15/microsoft-acquires-cycle-computing-accelerate-big-computing-cloud/)).
    * Verwenden Sie einen [Cray-Supercomputer](https://www.cray.com/solutions/supercomputing-as-a-service/cray-in-azure) als in Azure gehosteten Dienst.
* **Marketplace-Lösungen**
    * Nutzen Sie die vielen Möglichkeiten der [HPC-Anwendungen](#hpc-applications) und [Lösungen](#marketplace-solutions), die über den [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/) erhältlich sind. 
    
Die folgenden Abschnitte enthalten weitere Informationen zu den unterstützenden Technologien und Links zu Anleitungen.

## <a name="marketplace-solutions"></a>Marketplace-Lösungen

Images und Lösungen für HPC-fähige virtuelle Linux- und Windows-Computer finden Sie im [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace/). Beispiele:

* [CentOS-basiertes HPC von RogueWave](https://azuremarketplace.microsoft.com/marketplace/apps/RogueWave.CentOSbased74HPC?tab=Overview)
* [SUSE Linux Enterprise Server für HPC](https://azure.microsoft.com/marketplace/partners/suse/suselinuxenterpriseserver12optimizedforhighperformancecompute/)
*  [TIBCO Grid Server Engine](https://azuremarketplace.microsoft.com/marketplace/apps/tibco-software.gridserverlinuxengine?tab=Overview)
* [Virtueller Computer für Data Science für Linux und Windows](../articles/machine-learning/machine-learning-data-science-virtual-machine-overview.md)
* [D3View](https://azuremarketplace.microsoft.com/marketplace/apps/xfinityinc.d3view-v5?tab=Overview)
* [UberCloud](https://azure.microsoft.com/search/marketplace/?q=ubercloud)

## <a name="hpc-applications"></a>HPC-Anwendungen

Führen Sie benutzerdefinierte oder kommerzielle HPC-Anwendungen in Azure aus. Für mehrere Beispiele in diesem Abschnitt wurden Benchmarks erstellt, um eine effiziente Skalierung mit zusätzlichen virtuellen Computern oder Computekernen zu ermöglichen. Besuchen Sie den [Azure Marketplace](https://azuremarketplace.microsoft.com/marketplace), um auf Lösungen zuzugreifen, die sofort bereitgestellt werden können.

> [!NOTE]
> Informieren Sie sich bei Verwendung kommerzieller Anwendungen beim jeweiligen Hersteller über lizenzbedingte oder anderweitige Einschränkungen für die Ausführung in der Cloud. Nicht alle Hersteller bieten ein nutzungsbasiertes Lizenzmodell an. Unter Umständen benötigen Sie für Ihre Lösung einen Lizenzserver in der Cloud oder eine Verbindung mit einem lokalen Lizenzserver.

### <a name="engineering-applications"></a>Technische Anwendungen

* [Altair RADIOSS](https://azure.microsoft.com/blog/availability-of-altair-radioss-rdma-on-microsoft-azure/)
* [ANSYS CFD](https://azure.microsoft.com/blog/ansys-cfd-and-microsoft-azure-perform-the-best-hpc-scalability-in-the-cloud/)
* [MATLAB Distributed Computing Server](../articles/virtual-machines/windows/matlab-mdcs-cluster.md)
* [StarCCM+](https://blogs.msdn.microsoft.com/azurecat/2017/07/07/run-star-ccm-in-an-azure-hpc-cluster/)
* [OpenFOAM](https://simulation.azure.com/casestudies/Team-182-ABB-UC-Final.pdf)

### <a name="graphics-and-rendering"></a>Grafik und Rendering

* [Renderinganwendungen](../articles/batch/batch-rendering-service.md) in Azure Batch, einschließlich Autodesk Maya, 3ds Max und Arnold, Chaos Group V-Ray und Blender

### <a name="ai-and-deep-learning"></a>KI und Deep Learning

* [Microsoft Cognitive Toolkit](https://docs.microsoft.com/cognitive-toolkit/cntk-on-azure)
* [Virtueller Deep Learning-Computer](https://azuremarketplace.microsoft.com/marketplace/apps/microsoft-ads.dsvm-deep-learning)
* [Batch Shipyard-Rezepte für Deep Learning](https://github.com/Azure/batch-shipyard/tree/master/recipes#deeplearning)

## <a name="hpc-and-gpu-vm-sizes"></a>VM-Größen mit HPC und GPU

Azure bietet eine Reihe von Größen für virtuelle Computer unter [Linux](../articles/virtual-machines/linux/sizes.md?toc=%2fazure%2fvirtual-machines%2flinux%2ftoc.json) und [Windows](../articles/virtual-machines/windows/sizes.md?toc=%2fazure%2fvirtual-machines%2fwindows%2ftoc.json), darunter auch Größen, die für rechenintensive Workloads konzipiert sind. Virtuelle Computer vom Typ „H16r“ und „H16mr“ können beispielsweise eine Verbindung mit einem Back-End-RDMA-Netzwerk mit hohem Durchsatz herstellen. Dieses Cloudnetzwerk kann die Leistung eng gekoppelter paralleler Anwendungen unter [Microsoft MPI](https://msdn.microsoft.com/library/bb524831.aspx) oder Intel MPI verbessern. 

Virtuelle Computer der N-Serie verfügen über NVIDIA-GPUs für rechen- oder grafikintensive Anwendungen wie KI-Lernen und Visualisierung. 

Weitere Informationen:

* HPC-Größen für virtuelle Computer unter [Linux](../articles/virtual-machines/linux/sizes-hpc.md) und [Windows](../articles/virtual-machines/windows/sizes-hpc.md) 
* Größen für virtuelle Computer mit GPU unter [Linux](../articles/virtual-machines/linux/sizes-gpu.md) und [Windows](../articles/virtual-machines/windows/sizes-gpu.md) 

## <a name="azure-cyclecloud"></a>Azure CycleCloud

Verwalten Sie häufige Workloads effizient und mühelos beim Erstellen und Optimieren von HPC-Clustern auf virtuellen Azure-Computern mit [Azure CycleCloud](https://docs.microsoft.com/azure/cyclecloud/overview).

In diesem Artikel werden folgende Themen erläutert:

* [Installieren und Einrichten von CycleCloud mit einer Resource Manager-Vorlage](https://docs.microsoft.com/azure/cyclecloud/quickstart-install-cyclecloud)

* [Manuelles Einrichten von CycleCloud](https://docs.microsoft.com/azure/cyclecloud/installation)

## <a name="azure-batch"></a>Azure Batch

Bei [Batch](../articles/batch/batch-technical-overview.md) handelt es sich um eine Plattform zum Ausführen umfangreicher paralleler Anwendungen und HPC-Anwendungen (High Performance Computing) in der Cloud. Azure Batch plant die Ausführung rechenintensiver Aufgaben mit einem verwalteten Pool virtueller Computer und kann Computeressourcen automatisch skalieren, um den Anforderungen Ihrer Aufträge gerecht zu werden. 

SaaS-Anbieter oder Entwickler können die Batch-SDKs und -Tools verwenden, um HPC-Anwendungen oder Containerworkloads in Azure zu integrieren, Daten in Azure bereitzustellen und Pipelines für die Auftragsausführung zu erstellen. 

In diesem Artikel werden folgende Themen erläutert:

* [Erste Schritte beim Entwickeln mit Batch](../articles/batch/quick-run-dotnet.md)
* [Verwenden von Codebeispielen für Azure Batch](https://github.com/Azure/azure-batch-samples)
* [Verwenden von VMs mit niedriger Priorität mit Batch](../articles/batch/batch-low-pri-vms.md)
* [Ausführen von HPC-Workloads in Containern mit Batch Shipyard](https://github.com/Azure/batch-shipyard)
* [Ausführen gleichzeitiger R-Workloads in Batch](https://github.com/Azure/doAzureParallel)
* [Ausführen bedarfsorientierter Spark-Aufträge in Batch](https://github.com/Azure/aztk)

## <a name="workload-managers"></a>Workload-Manager

Unten sind Beispiele für Cluster- und Workload-Manager angegeben, die in der Azure-Infrastruktur ausgeführt werden können. Erstellen Sie eigenständige Cluster auf Azure-VMs, oder führen Sie aus einem lokalen Cluster einen Burst-Vorgang auf Azure-VMs durch. 
* [Alces Flight Compute](https://azuremarketplace.microsoft.com/marketplace/apps/alces-flight-limited.alces-flight-compute-solo?tab=Overview)
* [TIBCO DataSynapse GridServer](https://azure.microsoft.com/blog/tibco-datasynapse-comes-to-the-azure-marketplace/) 
* [Bright Cluster Manager](http://www.brightcomputing.com/technology-partners/microsoft)
* [IBM Spectrum Symphony und Symphony LSF](https://azure.microsoft.com/blog/ibm-and-microsoft-azure-support-spectrum-symphony-and-spectrum-lsf/)
* [PBS Pro](http://pbspro.org)
* [Microsoft HPC Pack](https://docs.microsoft.com/powershell/high-performance-computing/overview) 

## <a name="hpc-storage"></a>HPC-Speicher

Herkömmliche Clouddateisysteme sind den Anforderungen, die umfangreiche Batch- und HPC-Workloads in puncto Datenspeicherung und -zugriff haben, nicht gewachsen. 

Weitere Informationen:

* [Avere vFXT für Azure](../articles/avere-vfxt/avere-vfxt-overview.md) 
* [Parallele virtuelle Dateisysteme in Azure](https://azure.microsoft.com/resources/parallel-virtual-file-systems-on-microsoft-azure/), einschließlich [Lustre](http://lustre.org/) und [BeeGFS](http://www.beegfs.com/content/)

## <a name="related-azure-services"></a>Verwandte Azure-Dienste

Die meisten Azure-HPC-Lösungen basieren auf Azure Virtual Machines, VM-Skalierungsgruppen, Batch und ähnlichen Computediensten. Ihre Lösung kann jedoch von zahlreichen verwandten Azure-Diensten profitieren. Im Anschluss finden Sie eine unvollständige Liste:

### <a name="storage"></a>Storage

* [Blob, Table und Queue Storage](../articles/storage/storage-introduction.md)
* [File Storage](../articles/storage/storage-files-introduction.md)

### <a name="data-and-analytics"></a>Daten und Analysen

* [HDInsight](../articles/hdinsight/hadoop/apache-hadoop-introduction.md)
* [Data Factory](../articles/data-factory/introduction.md)
* [Data Lake Storage Gen1](../articles/data-lake-store/data-lake-store-overview.md)
* [Databricks](../articles/azure-databricks/what-is-azure-databricks.md)
* [SQL-Datenbank](../articles/sql-database/sql-database-technical-overview.md)

### <a name="ai-and-machine-learning"></a>KI und Machine Learning

* [Machine Learning-Dienst](../articles/machine-learning/service/overview-what-is-azure-ml.md)
* [Genomics](../articles/genomics/overview-what-is-genomics.md)

### <a name="networking"></a>Netzwerk

* [Virtual Network](../articles/virtual-network/virtual-networks-overview.md)
* [ExpressRoute](../articles/expressroute/expressroute-introduction.md)

### <a name="containers"></a>Container

* [Azure Kubernetes Service (AKS)](../articles/aks/intro-kubernetes.md)
* [Containerregistrierung](../articles/container-registry/container-registry-intro.md)
* [Containerinstanzen](../articles/container-instances/container-instances-overview.md)

## <a name="customer-stories"></a>Kundenstimmen

Beispiele für Kunden, die mithilfe von Azure-HPC-Lösungen geschäftliche Probleme gelöst haben:

* [ANEO](https://customers.microsoft.com/story/it-provider-finds-highly-scalable-cloud-based-hpc-redu) 
* [AXA Global P&amp;C](https://customers.microsoft.com/story/axa-global-p-and-c)
* [Axioma](https://customers.microsoft.com/story/axioma-delivers-fintechs-first-born-in-the-cloud-multi-asset-class-enterprise-risk-solution)
* [d3View](https://customers.microsoft.com/story/big-data-solution-provider-adopts-new-cloud-gains-thou)
* [EFS](https://customers.microsoft.com/story/efs-professionalservices-azure)
* [Hymans Robertson](https://customers.microsoft.com/story/hymans-robertson)
* [MetLife](https://customers.microsoft.com/story/metlife-insurance-azure-cloud-services-windows-server-analytics-platform-server-en)
* [Microsoft Research](https://customers.microsoft.com/doclink/fast-lmm-and-windows-azure-put-genetics-research-on-fa)
* [Milliman](https://customers.microsoft.com/story/actuarial-firm-works-to-transform-insurance-industry-w)
* [Mitsubishi UFJ Securities International](https://customers.microsoft.com/story/powering-risk-compute-grids-in-the-cloud)
* [NeuroInitiative](https://customers.microsoft.com/story/neuroinitiative-health-provider-azure)
* [Schlumberger](https://azure.microsoft.com/blog/big-compute-for-large-engineering-simulations)
* [Towers Watson](https://customers.microsoft.com/story/insurance-tech-provider-delivers-disruptive-solutions)

## <a name="next-steps"></a>Nächste Schritte

* Erfahren Sie mehr über Azure-Lösungen für [High-Performance Computing](https://azure.microsoft.com/solutions/high-performance-computing/), [Rendering](https://azure.microsoft.com/solutions/big-compute/rendering/), [Bankwesen und Kapitalmärkte](https://finance.azure.com/) und [Genomik](https://enterprise.microsoft.com/industries/health/genomics/).

* Erfahren Sie mehr über [Big Compute-Lösungsarchitekturen](https://azure.microsoft.com/solutions/architecture/?solution=high-performance-computing) in Azure.
