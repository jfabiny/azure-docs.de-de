---
title: Herunterladen von Azure Stack-Tools von GitHub | Microsoft-Dokumentation
description: Erfahren Sie, wie Sie Tools herunterladen, die für die Arbeit mit Azure Stack benötigt werden.
services: azure-stack
documentationcenter: ''
author: mattbriggs
manager: femila
editor: ''
ms.service: azure-stack
ms.workload: na
pms.tgt_pltfrm: na
ms.devlang: PowerShell
ms.topic: article
ms.date: 01/14/2019
ms.author: mabrigg
ms.reviewer: thoroet
ms.lastreviewed: 01/14/2019
ms.openlocfilehash: 05dd3b292f90964c6af21890aaeafab9849a09ed
ms.sourcegitcommit: 898b2936e3d6d3a8366cfcccc0fccfdb0fc781b4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/30/2019
ms.locfileid: "55242976"
---
# <a name="download-azure-stack-tools-from-github"></a>Herunterladen von Azure Stack-Tools von GitHub

*Anwendungsbereich: Integrierte Azure Stack-Systeme und Azure Stack Development Kit*

**AzureStack-Tools** ist ein [GitHub-Repository](https://github.com/Azure/AzureStack-Tools), das PowerShell-Module zum Verwalten und Bereitstellen von Ressourcen für Azure Stack hostet. Sie können diese PowerShell-Module in das Azure Stack Development Kit oder in einen Windows-basierten externen Client herunterladen und verwenden, wenn Sie planen, VPN-Konnektivität einzurichten. Um diese Tools zu erhalten, klonen Sie das GitHub-Repository, oder laden Sie den Ordner **AzureStack-Tools** herunter. Führen Sie dazu das folgende Skript aus:

```PowerShell
# Change directory to the root directory. 
cd \

# Download the tools archive.
[Net.ServicePointManager]::SecurityProtocol = [Net.SecurityProtocolType]::Tls12 
invoke-webrequest `
  https://github.com/Azure/AzureStack-Tools/archive/master.zip `
  -OutFile master.zip

# Expand the downloaded files.
expand-archive master.zip `
  -DestinationPath . `
  -Force

# Change to the tools directory.
cd AzureStack-Tools-master

```

## <a name="functionality-provided-by-the-modules"></a>Von den Modulen bereitgestellte Funktionen

Das Repository **AzureStack-Tools** umfasst PowerShell-Module, die die folgenden Funktionen für Azure Stack unterstützen:  

| Funktionalität | BESCHREIBUNG | Wer kann dieses Modul verwenden? |
| --- | --- | --- |
| [Cloudfunktionen](user/azure-stack-validate-templates.md) | Verwenden Sie dieses Modul, um die Cloudfunktionen einer Cloud zu nutzen. Mithilfe dieses Moduls können Sie z.B. Cloudfunktionen wie die API-Version und Azure Resource Manager-Ressourcen abrufen. Mithilfe dieses Moduls können Sie auch die VM-Erweiterungen für Azure Stack und Azure-Clouds abrufen. | Cloudoperatoren und Benutzer |
| [Resource Manager-Richtlinie für Azure Stack](user/azure-stack-policy-module.md) | Verwenden Sie dieses Modul zum Konfigurieren eines Azure-Abonnements oder einer Azure-Ressourcengruppe mit der gleichen Versionsverwaltung und Dienstverfügbarkeit wie Azure Stack. | Cloudoperatoren und Benutzer |
| [Registrieren bei Azure](azure-stack-register.md) | Verwenden Sie dieses Modul zum Registrieren Ihrer Development Kit-Instanz bei Azure. Nach der Registrierung können Sie die Marketplace-Elemente von Azure herunterladen und in Azure Stack verwenden. | Cloudoperatoren |
| [Azure Stack-Bereitstellung](azure-stack-run-powershell-script.md) | Verwenden Sie dieses Modul zum Vorbereiten des Azure Stack-Hostcomputers auf die Bereitstellung und die erneute Bereitstellung mithilfe des Azure Stack-VHD-Images (virtuelle Festplatte). | Cloudoperatoren|
| [Herstellen einer Verbindung mit Azure Stack](azure-stack-connect-powershell.md) | Verwenden Sie dieses Modul, um die VPN-Konnektivität für Azure Stack zu konfigurieren. | Cloudoperatoren und Benutzer |
| [Validierungssteuerelement für Vorlagen](user/azure-stack-validate-templates.md) | Verwenden Sie dieses Modul, um zu überprüfen, ob eine vorhandene oder eine neue Vorlage für Azure Stack bereitgestellt werden kann. | Cloudoperatoren und Benutzer|


## <a name="next-steps"></a>Nächste Schritte
* [Konfigurieren der PowerShell-Umgebung des Azure Stack-Benutzers](user/azure-stack-powershell-configure-user.md)   
* [Connect to Azure Stack Development Kit over a VPN (Herstellen einer Verbindung mit dem Azure Stack Development Kit über VPN)](azure-stack-connect-azure-stack.md)  
