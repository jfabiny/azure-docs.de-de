---
title: 'Beispiele für die Azure CLI: Installieren von Apps | Microsoft-Dokumentation'
description: Azure CLI-Beispiele
services: virtual-machine-scale-sets
documentationcenter: ''
author: cynthn
manager: jeconnoc
editor: ''
tags: azure-resource-manager
ms.assetid: ''
ms.service: virtual-machine-scale-sets
ms.devlang: azurecli
ms.topic: sample
ms.tgt_pltfrm: na
ms.workload: na
ms.date: 03/27/2018
ms.author: cynthn
ms.custom: mvc
ms.openlocfilehash: b63a4ed26688b73b9a8b1568433c7ae7606e6c6a
ms.sourcegitcommit: a65b424bdfa019a42f36f1ce7eee9844e493f293
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/04/2019
ms.locfileid: "55698958"
---
# <a name="install-applications-into-a-virtual-machine-scale-set-with-the-azure-cli"></a>Installieren von Anwendungen in einer VM-Skalierungsgruppe mit der Azure CLI
Dieses Skript erstellt eine VM-Skalierungsgruppe unter Ubuntu und installiert eine einfache Webanwendung unter Verwendung der benutzerdefinierten Skripterweiterung. Nach dem Ausführen des Skripts können Sie über einen Webbrowser auf die Web-App zugreifen.

[!INCLUDE [sample-cli-install](../../../includes/sample-cli-install.md)]

[!INCLUDE [quickstarts-free-trial-note](../../../includes/quickstarts-free-trial-note.md)]

## <a name="sample-script"></a>Beispielskript
[!code-azurecli-interactive[main](../../../cli_scripts/virtual-machine-scale-sets/install-apps/install-apps.sh "Install apps into a scale set")]

## <a name="clean-up-deployment"></a>Bereinigen der Bereitstellung
Führen Sie den folgenden Befehl aus, um die Ressourcengruppe, die Skalierungsgruppe und alle dazugehörigen Ressourcen zu entfernen.

```azurecli-interactive
az group delete --name myResourceGroup
```

## <a name="script-explanation"></a>Erläuterung des Skripts
In diesem Skript werden die folgenden Befehle verwendet, um eine Ressourcengruppe, eine VM-Skalierungsgruppe und alle dazugehörigen Ressourcen zu erstellen. Jeder Befehl in der Tabelle ist mit der zugehörigen Dokumentation verknüpft.

| Get-Help | Notizen |
|---|---|
| [az group create](/cli/azure/ad/group) | Erstellt eine Ressourcengruppe, in der alle Ressourcen gespeichert sind. |
| [az vmss create](/cli/azure/vmss#az_vmss_create) | Erstellt die VM-Skalierungsgruppe und verbindet sie mit dem virtuellen Netzwerk, dem Subnetz und der Netzwerksicherheitsgruppe. Des Weiteren wird ein Lastenausgleich erstellt, um Datenverkehr auf mehrere VM-Instanzen zu verteilen. Dieser Befehl gibt auch das zu verwendende VM-Image und die Administratoranmeldeinformationen an.  |
| [az vmss extension set](/cli/azure/vmss/extension) | Installiert die benutzerdefinierte Skripterweiterung von Azure, um ein Skript auszuführen, das die Datenträger auf den einzelnen VM-Instanzen vorbereitet. |
| [az network lb rule create](/cli/azure/network/lb/rule) | Erstellt eine Lastenausgleichsregel, um den Datenverkehr am TCP-Port 80 auf die VM-Instanzen in der Skalierungsgruppe zu verteilen. |
| [az network public-ip show](/cli/azure/network/public-ip) | Ruft Informationen zur zugewiesenen öffentlichen IP-Adresse ab, die vom Load Balancer verwendet wird. |
| [az group delete](/cli/azure/ad/group) | Löscht eine Ressourcengruppe einschließlich aller geschachtelten Ressourcen. |

## <a name="next-steps"></a>Nächste Schritte
Weitere Informationen zur Azure CLI finden Sie in der [Azure CLI-Dokumentation](https://docs.microsoft.com/cli/azure/overview).

Weitere Azure CLI-Skriptbeispiele für VM-Skalierungsgruppen finden Sie in der [Dokumentation zu Azure-VM-Skalierungsgruppen](../cli-samples.md).
