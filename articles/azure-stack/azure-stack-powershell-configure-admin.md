---
title: Herstellen einer Verbindung mit Azure Stack über PowerShell als Operator | Microsoft-Dokumentation
description: Informationen zum Herstellen einer Verbindung mit Azure Stack über PowerShell als Operator
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
ms.date: 01/30/2019
ms.author: mabrigg
ms.reviewer: thoroet
ms.lastreviewed: 01/24/2019
ms.openlocfilehash: 47d6b336a031f4233bebb7af0b0c57dd8f643dac
ms.sourcegitcommit: 698a3d3c7e0cc48f784a7e8f081928888712f34b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/31/2019
ms.locfileid: "55452481"
---
# <a name="connect-to-azure-stack-with-powershell-as-an-operator"></a>Herstellen einer Verbindung mit Azure Stack über PowerShell als Operator

*Anwendungsbereich: Integrierte Azure Stack-Systeme und Azure Stack Development Kit*

Sie können Azure Stack für die Verwendung von PowerShell zum Verwalten von Ressourcen konfigurieren, z.B. die Erstellung von Angeboten, Plänen, Kontingenten und Warnungen. In diesem Thema können Sie die Betreiberumgebung konfigurieren.

## <a name="prerequisites"></a>Voraussetzungen

Führen Sie die folgenden erforderlichen Schritte entweder über das [Development Kit](./asdk/asdk-connect.md#connect-with-rdp) oder auf einem Windows-basierten externen Client aus, sofern [eine VPN-Verbindung mit dem ASDK](./asdk/asdk-connect.md#connect-with-vpn) besteht. 

 - Installieren Sie [mit Azure Stack kompatible Azure PowerShell-Module](azure-stack-powershell-install.md).  
 - Laden Sie die [Tools herunter, die für die Arbeit mit Azure Stack benötigt werden](azure-stack-powershell-download.md).  

## <a name="connect-with-azure-ad"></a>Herstellen einer Verbindung mit Azure AD

Konfigurieren Sie die Azure Stack-Betreiberumgebung mit PowerShell. Führen Sie eines der folgenden Skripts aus: Ersetzen Sie darin den Azure Active Directory (Azure AD) tenantName und die Endpunktwerte von Azure Resource Manager durch ihre eigene Umgebungskonfiguration. <!-- GraphAudience endpoint -->

```PowerShell  
    # Register an Azure Resource Manager environment that targets your Azure Stack instance. Get your Azure Resource Manager endpoint value from your service provider.
Add-AzureRMEnvironment -Name "AzureStackAdmin" -ArmEndpoint "https://adminmanagement.local.azurestack.external"

    # Set your tenant name
    $AuthEndpoint = (Get-AzureRmEnvironment -Name "AzureStackAdmin").ActiveDirectoryAuthority.TrimEnd('/')
    $AADTenantName = "<myDirectoryTenantName>.onmicrosoft.com"
    $TenantId = (invoke-restmethod "$($AuthEndpoint)/$($AADTenantName)/.well-known/openid-configuration").issuer.TrimEnd('/').Split('/')[-1]

    # After signing in to your environment, Azure Stack cmdlets
    # can be easily targeted at your Azure Stack instance.
    Add-AzureRmAccount -EnvironmentName "AzureStackAdmin" -TenantId $TenantId
```

## <a name="connect-with-ad-fs"></a>Herstellen einer Verbindung mit AD FS

Verbinden Sie die Azure Stack-Betreiberumgebung mit PowerShell mit Azure Active Directory-Verbunddiensten (Azure AD FS). Beim Azure Stack Development Kit wird dieser Azure Resource Manager-Endpunkt auf `https://adminmanagement.local.azurestack.external` festgelegt. Um den Azure Resource Manager-Endpunkt für integrierte Azure Stack-Systeme zu erhalten, wenden Sie sich an Ihren Dienstanbieter.

<!-- GraphAudience endpoint -->

  ```PowerShell  
  # Register an Azure Resource Manager environment that targets your Azure Stack instance. Get your Azure Resource Manager endpoint value from your service provider.
  Add-AzureRMEnvironment -Name "AzureStackAdmin" -ArmEndpoint "https://adminmanagement.local.azurestack.external"

  # Sign in to your environment

  $cred = get-credential

  Login-AzureRmAccount `
    -EnvironmentName "AzureStackAdmin" `
    -Credential $cred
  ```

> [!Note]  
> AD FS unterstützt nur die interaktive Authentifizierung mit Benutzeridentitäten. Wenn ein Objekt mit Anmeldeinformationen erforderlich ist, müssen Sie einen Dienstprinzipalnamen (SPN) verwenden. Weitere Informationen zum Einrichten eines Dienstprinzipals mit Azure Stack und AD FS als Identitätsverwaltungsdienst finden Sie unter [Verwalten eines Dienstprinzipals für AD FS](azure-stack-create-service-principals.md#manage-service-principal-for-ad-fs).

## <a name="test-the-connectivity"></a>Testen der Konnektivität

Nachdem Sie nun alles eingerichtet haben, können Sie mit PowerShell Ressourcen in Azure Stack erstellen. Sie können beispielsweise eine Ressourcengruppe für eine Anwendung erstellen und einen virtuellen Computer hinzufügen. Verwenden Sie den folgenden Befehl, um eine Ressourcengruppe mit dem Namen **MyResourceGroup** zu erstellen.

```PowerShell  
New-AzureRmResourceGroup -Name "MyResourceGroup" -Location "Local"
```

## <a name="next-steps"></a>Nächste Schritte

 - [Entwickeln von Vorlagen für Azure Stack](user/azure-stack-develop-templates.md)
 - [Bereitstellen von Vorlagen mit PowerShell](user/azure-stack-deploy-template-powershell.md)
