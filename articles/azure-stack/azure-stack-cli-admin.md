---
title: Aktivieren der Azure CLI für Azure Stack-Benutzer | Microsoft-Dokumentation
description: Es wird beschrieben, wie Sie die plattformübergreifende Befehlszeilenschnittstelle (Command-Line Interface, CLI) verwenden, um Ressourcen in Azure Stack zu verwalten und bereitzustellen.
services: azure-stack
documentationcenter: ''
author: mattbriggs
manager: femila
editor: ''
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: CLI
ms.topic: article
ms.date: 01/15/2019
ms.author: mabrigg
ms.lastreviewed: 01/15/2019
ms.openlocfilehash: 0d6a93b396e90f3bc27a1eb879556d774075c86f
ms.sourcegitcommit: 898b2936e3d6d3a8366cfcccc0fccfdb0fc781b4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/30/2019
ms.locfileid: "55243299"
---
# <a name="enable-azure-cli-for-azure-stack-users"></a>Aktivieren der Azure CLI für Azure Stack-Benutzer

*Anwendungsbereich: Integrierte Azure Stack-Systeme und Azure Stack Development Kit*

Sie können das CA-Stammzertifikat Benutzern in Azure Stack zur Verfügung stellen, damit sie die Azure CLI auf ihren Entwicklungscomputern verwenden können. Ihre Benutzer benötigen das Zertifikat, um Ressourcen über die CLI zu verwalten.

 - Das **Azure Stack-Zertifizierungsstellen-Stammzertifikat** ist erforderlich, wenn Benutzer die CLI auf einer Arbeitsstation außerhalb von Azure Stack Development Kit verwenden.  

 - Der **Endpunkt der VM-Aliase** stellt einen Alias (z.B. „UbuntuLTS“ oder „Win2012Datacenter“) bereit, der beim Bereitstellen von VMs als einzelner Parameter auf einen Herausgeber, ein Angebot, eine SKU und die Version eines Image verweist.  

In den folgenden Abschnitten wird beschrieben, wie Sie diese Werte abrufen.

## <a name="export-the-azure-stack-ca-root-certificate"></a>Exportieren des Azure Stack-Zertifizierungsstellen-Stammzertifikats

Wenn Sie ein integriertes System verwenden, müssen Sie das Stammzertifikat der Zertifizierungsstelle nicht exportieren. Bei einem Azure Stack Development Kit (ASDK) müssen Sie das Stammzertifikat der Zertifizierungsstelle exportieren.

Um das ASDK-Stammzertifikat im PEM-Format zu exportieren, melden Sie sich an, und führen Sie das folgende Skript aus:

```powershell
$label = "<Your Azure Stack CA root certificate name>"
Write-Host "Getting certificate from the current user trusted store with subject CN=$label"
$root = Get-ChildItem Cert:\CurrentUser\Root | Where-Object Subject -eq "CN=$label" | select -First 1
if (-not $root)
{
    Log-Error "Certificate with subject CN=$label not found"
    return
}

Write-Host "Exporting certificate"
Export-Certificate -Type CERT -FilePath root.cer -Cert $root

Write-Host "Converting certificate to PEM format"
certutil -encode root.cer root.pem
```

## <a name="set-up-the-virtual-machine-aliases-endpoint"></a>Einrichten des Endpunkts der VM-Aliase

Azure Stack-Betreiber sollten einen öffentlich zugänglichen Endpunkt einrichten, der eine VM-Aliasdatei hostet. Bei der VM-Aliasdatei handelt es sich um eine JSON-Datei, die einen allgemeinen Namen für ein Image bereitstellt. Sie verwenden den Namen, wenn Sie eine VM bereitstellen, als Azure CLI-Parameter.  

Stellen Sie vor dem Hinzufügen eines Eintrags zu einer Aliasdatei sicher, dass Sie [Images aus dem Azure Marketplace heruntergeladen](azure-stack-download-azure-marketplace-item.md) oder [ein eigenes benutzerdefiniertes Image veröffentlicht](azure-stack-add-vm-image.md) haben. Wenn Sie ein benutzerdefiniertes Image veröffentlichen, notieren Sie sich die während der Veröffentlichung angegebenen Informationen zu Herausgeber, Angebot, SKU und Version. Wenn es sich um ein Image aus dem Marketplace handelt, können Sie die Informationen mithilfe des ```Get-AzureVMImage```-Cmdlets anzeigen.  

Eine [Aliasbeispieldatei](https://raw.githubusercontent.com/Azure/azure-rest-api-specs/master/arm-compute/quickstart-templates/aliases.json) mit zahlreichen allgemeinen Imagealiasen ist verfügbar. Sie können diese als Ausgangspunkt verwenden. Hosten Sie diese Datei an einem Ort, auf den die CLI-Clients zugreifen können. Eine Möglichkeit besteht darin, die Datei in einem Blob Storage-Konto zu hosten und die URL für Ihre Benutzer freizugeben:

1. Laden Sie die [Beispieldatei](https://raw.githubusercontent.com/Azure/azure-rest-api-specs/master/arm-compute/quickstart-templates/aliases.json) von GitHub herunter.
2. Erstellen Sie ein Speicherkonto in Azure Stack. Erstellen Sie anschließend einen Blobcontainer. Legen Sie die Zugriffsrichtlinie auf „Öffentlich“ fest.  
3. Laden Sie die JSON-Datei in den neuen Container hoch. Wenn das erledigt ist, können Sie die URL des Blobs anzeigen. Wählen Sie den Blobnamen aus, und wählen Sie dann die URL in den „Blob-Eigenschaften“ aus.

## <a name="next-steps"></a>Nächste Schritte

- [Bereitstellen von Vorlagen mit der Azure CLI](azure-stack-deploy-template-command-line.md)
- [Verbinden mit PowerShell](azure-stack-connect-powershell.md)
- [Verwalten von Benutzerberechtigungen](azure-stack-manage-permissions.md)
