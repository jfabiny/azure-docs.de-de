---
title: Erstellen und Konfigurieren von Azure Kubernetes Service-Clustern in Azure mithilfe von Ansible
description: Erfahren Sie, wie Sie mithilfe von Ansible einen Azure Kubernetes Service-Cluster in Azure erstellen und verwalten können
ms.service: ansible
keywords: Ansible, Azure, DevOps, Bash, CloudShell, Playbook, Aks, Container, Kubernetes
author: tomarchermsft
manager: jeconnoc
ms.author: tarcher
ms.topic: tutorial
ms.date: 08/23/2018
ms.openlocfilehash: df1efc1506fbbe51ba5afb03f147c51a57d9bbdb
ms.sourcegitcommit: 3aa0fbfdde618656d66edf7e469e543c2aa29a57
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 02/05/2019
ms.locfileid: "55727057"
---
# <a name="create-and-configure-azure-kubernetes-service-clusters-in-azure-using-ansible"></a>Erstellen und Konfigurieren von Azure Kubernetes Service-Clustern in Azure mithilfe von Ansible
Ansible ermöglicht die Automatisierung der Bereitstellung und Konfiguration von Ressourcen in Ihrer Umgebung. Sie können Ansible verwenden, um Ihren Azure Kubernetes Service (AKS) zu verwalten. Dieser Artikel beschreibt, wie Sie mithilfe von Ansible einen Azure Kubernetes Service-Cluster erstellen und verwalten können.

## <a name="prerequisites"></a>Voraussetzungen
- **Azure-Abonnement:** Falls Sie über kein Azure-Abonnement verfügen, können Sie ein [kostenloses Konto](https://azure.microsoft.com/free/?ref=microsoft.com&utm_source=microsoft.com&utm_medium=docs&utm_campaign=visualstudio) erstellen, bevor Sie beginnen.
- **Azure-Dienstprinzipal**: Notieren Sie [beim Erstellen des Dienstprinzipals](/cli/azure/create-an-azure-service-principal-azure-cli?view=azure-cli-latest#create-the-service-principal) die folgenden Werte: **App-ID**, **Anzeigename**, **Kennwort**  und **Mandant**.

- [!INCLUDE [ansible-prereqs-for-cloudshell-use-or-vm-creation1.md](../../includes/ansible-prereqs-for-cloudshell-use-or-vm-creation1.md)][!INCLUDE [ansible-prereqs-for-cloudshell-use-or-vm-creation2.md](../../includes/ansible-prereqs-for-cloudshell-use-or-vm-creation2.md)]

> [!Note]
> Für die Ausführung der folgenden Beispielplaybooks in diesem Tutorial ist Ansible 2.6 erforderlich.

## <a name="create-a-managed-aks-cluster"></a>Erstellen eines verwalteten AKS-Clusters
Der Code in diesem Abschnitt stellt ein Ansible-Beispielplaybook dar, das eine Ressourcengruppe und einen AKS-Cluster erstellt, der sich in der Ressourcengruppe befindet.

> [!Tip]
> Geben Sie für den Platzhalter `your_ssh_key` Ihren öffentlichen RSA-Schlüssel im einzeiligen Format beginnend mit „ssh-rsa“ (ohne Anführungszeichen) ein.

  ```yaml
  - name: Create Azure Kubernetes Service
    hosts: localhost
    connection: local
    vars:
      resource_group: myResourceGroup
      location: eastus
      aks_name: myAKSCluster
      username: azureuser
      ssh_key: "your_ssh_key"
      client_id: "your_client_id"
      client_secret: "your_client_secret"
    tasks:
    - name: Create resource group
      azure_rm_resourcegroup:
        name: "{{ resource_group }}"
        location: "{{ location }}"
    - name: Create a managed Azure Container Services (AKS) cluster
      azure_rm_aks:
        name: "{{ aks_name }}"
        location: "{{ location }}"
        resource_group: "{{ resource_group }}"
        dns_prefix: "{{ aks_name }}"
        linux_profile:
          admin_username: "{{ username }}"
          ssh_key: "{{ ssh_key }}"
        service_principal:
          client_id: "{{ client_id }}"
          client_secret: "{{ client_secret }}"
        agent_pool_profiles:
          - name: default
            count: 2
            vm_size: Standard_D2_v2
        tags:
          Environment: Production
  ```

In der folgenden Aufzählung werden die vorangehenden Ansible-Playbookcodes erläutert:
- Der erste Abschnitt in **Tasks** definiert eine Ressourcengruppe namens **myResourceGroup** im Speicherort **eastus**.
- Der zweite Abschnitt in **Tasks** definiert einen AKS-Cluster mit dem Namen **myAKSCluster** in der Ressourcengruppe **myResourceGroup**.

Um den AKS-Cluster mit Ansible zu erstellen, speichern Sie das vorherige Beispielplaybook als `azure_create_aks.yml`, und führen Sie das Playbook mit dem folgenden Befehl aus:

  ```bash
  ansible-playbook azure_create_aks.yml
  ```

Die Ausgabe des Befehls **ansible-playbook* sieht in etwa folgendermaßen aus und zeigt, dass der AKS-Cluster erfolgreich erstellt wurde:

  ```Output
  PLAY [Create AKS] ****************************************************************************************

  TASK [Gathering Facts] ********************************************************************************************
  ok: [localhost]

  TASK [Create resource group] **************************************************************************************
  changed: [localhost]

  TASK [Create a Azure Container Services (AKS) cluster] ***************************************************
  changed: [localhost]

  PLAY RECAP *********************************************************************************************************
  localhost                  : ok=3    changed=2    unreachable=0    failed=0
  ```

## <a name="scale-aks-nodes"></a>Skalieren der AKS-Knoten

Das Beispielplaybook aus dem vorherigen Abschnitt definiert zwei Knoten. Wenn Sie größere oder kleinere Containerworkloads in Ihrem Cluster benötigen, können Sie die Anzahl der Knoten auf einfache Weise anpassen. Im Beispielplaybook in diesem Abschnitt wird die Anzahl von Knoten von 2 auf 3 Knoten erhöht. Die Knotenanzahl wird geändert, indem der Wert **count** im Block **agent_pool_profiles** geändert wird.

> [!Tip]
> Geben Sie für den Platzhalter `your_ssh_key` Ihren öffentlichen RSA-Schlüssel im einzeiligen Format beginnend mit „ssh-rsa“ (ohne Anführungszeichen) ein.

```yaml
- name: Scale AKS cluster
  hosts: localhost
  connection: local
  vars:
    resource_group: myResourceGroup
    location: eastus
    aks_name: myAKSCluster
    username: azureuser
    ssh_key: "your_ssh_key"
    client_id: "your_client_id"
    client_secret: "your_client_secret"
  tasks:
  - name: Scaling an existed AKS cluster
    azure_rm_aks:
        name: "{{ aks_name }}"
        location: "{{ location }}"
        resource_group: "{{ resource_group }}"
        dns_prefix: "{{ aks_name }}"
        linux_profile:
          admin_username: "{{ username }}"
          ssh_key: "{{ ssh_key }}"
        service_principal:
          client_id: "{{ client_id }}"
          client_secret: "{{ client_secret }}"
        agent_pool_profiles:
          - name: default
            count: 3
            vm_size: Standard_D2_v2
```

Um den Azure Kubernetes Service-Cluster mit Ansible zu skalieren, speichern Sie das vorherige Playbook als *azure_configure_aks.yml*, und führen Sie das Playbook wie folgt aus:

  ```bash
  ansible-playbook azure_configure_aks.yml
  ```

Die folgende Ausgabe zeigt, dass der AKS-Cluster erfolgreich erstellt wurde:

  ```Output
  PLAY [Scale AKS cluster] ***************************************************************

  TASK [Gathering Facts] ******************************************************************
  ok: [localhost]

  TASK [Scaling an existed AKS cluster] **************************************************
  changed: [localhost]

  PLAY RECAP ******************************************************************************
  localhost                  : ok=2    changed=1    unreachable=0    failed=0
  ```
## <a name="delete-a-managed-aks-cluster"></a>Löschen eines verwalteten AKS-Clusters

Der folgende Abschnitt im Ansible-Beispielplaybook veranschaulicht das Löschen eines AKS-Clusters:

  ```yaml
  - name: Delete a managed Azure Container Services (AKS) cluster
    hosts: localhost
    connection: local
    vars:
      resource_group: myResourceGroup
      aks_name: myAKSCluster
    tasks:
    - name:
      azure_rm_aks:
        name: "{{ aks_name }}"
        resource_group: "{{ resource_group }}"
        state: absent
   ```

Zum Löschen des Azure Kubernetes Service-Clusters mit Ansible speichern Sie das vorherige Playbook als *azure_delete_aks.yml*, und führen Sie das Playbook wie folgt aus:

  ```bash
  ansible-playbook azure_delete_aks.yml
  ```

Die folgende Ausgabe zeigt, dass der AKS-Cluster erfolgreich gelöscht wurde:
  ```Output
PLAY [Delete a managed Azure Container Services (AKS) cluster] ****************************

TASK [Gathering Facts] ********************************************************************
ok: [localhost]

TASK [azure_rm_aks] *********************************************************************

PLAY RECAP *********************************************************************
localhost                  : ok=2    changed=1    unreachable=0    failed=0
  ```

## <a name="next-steps"></a>Nächste Schritte
> [!div class="nextstepaction"]
> [Tutorial: Skalieren einer Anwendung in Azure Kubernetes Service (AKS)](https://docs.microsoft.com/azure/aks/tutorial-kubernetes-scale)
