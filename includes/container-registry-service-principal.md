---
title: Includedatei
description: Includedatei
services: container-registry
author: dlepow
ms.service: container-registry
ms.topic: include
ms.date: 12/14/2018
ms.author: danlep
ms.custom: include file
ms.openlocfilehash: 1a8a31b34981b0e2b68caf3f5c4952d0ee59ac8e
ms.sourcegitcommit: 7862449050a220133e5316f0030a259b1c6e3004
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/22/2018
ms.locfileid: "53784453"
---
## <a name="create-a-service-principal"></a>Erstellen eines Dienstprinzipals

Führen Sie zum Erstellen eines Dienstprinzipals mit Zugriff auf die Containerregistrierung das folgende Skript in [Azure Cloud Shell](../articles/cloud-shell/overview.md) oder in einer lokalen Installation der [Azure CLI](/cli/azure/install-azure-cli) aus. Das Skript ist für die Bash-Shell formatiert.

Aktualisieren Sie vor dem Ausführen des Skripts die Variable `ACR_NAME` mit dem Namen Ihrer Containerregistrierung. Der Wert `SERVICE_PRINCIPAL_NAME` muss in Ihrem Azure Active Directory-Mandanten eindeutig sein. Wird der Fehler `'http://acr-service-principal' already exists.` angezeigt, geben Sie einen anderen Namen für den Dienstprinzipal an.

Optional können Sie den Wert `--role` im Befehl [az ad sp create-for-rbac][az-ad-sp-create-for-rbac] ändern, falls Sie andere Berechtigungen gewähren möchten. Eine vollständige Liste der Rollen finden Sie unter [ACR-Rollen und -Berechtigungen](https://github.com/Azure/acr/blob/master/docs/roles-and-permissions.md).

Nachdem Sie das Skript ausgeführt haben, notieren Sie die **ID** und das **Kennwort** des Dienstprinzipals. Sobald Sie über dessen Anmeldeinformationen verfügen, können Sie Ihre Anwendungen und Dienste so konfigurieren, dass diese bei Ihrer Containerregistrierung als Dienstprinzipal authentifiziert werden.

<!-- https://github.com/Azure-Samples/azure-cli-samples/blob/master/container-registry/service-principal-create/service-principal-create.sh --> [!code-azurecli-interactive[acr-sp-create](~/cli_scripts/container-registry/service-principal-create/service-principal-create.sh)]

## <a name="use-an-existing-service-principal"></a>Verwenden eines vorhandenen Dienstprinzipals

Damit Sie einem vorhandenen Dienstprinzipal den Zugriff auf die Registrierung gewähren können, müssen Sie dem Dienstprinzipal eine neue Rolle zuweisen. Wie bei der Erstellung eines neuen Dienstprinzipals können Sie unter anderem Pull-, Push- und Pull- sowie Besitzerzugriff gewähren.

Das folgende Skript verwendet den Befehl [az role assignment create][az-role-assignment-create], um einem Dienstprinzipal *Pull*-Berechtigungen zuzuweisen, den Sie in der Variablen `SERVICE_PRINCIPAL_ID` festlegen. Passen Sie den Wert `--role` an, wenn Sie eine andere Zugriffsebene zuweisen möchten.


<!-- https://github.com/Azure-Samples/azure-cli-samples/blob/master/container-registry/service-principal-assign-role/service-principal-assign-role.sh --> [!code-azurecli-interactive[acr-sp-role-assign](~/cli_scripts/container-registry/service-principal-assign-role/service-principal-assign-role.sh)]

<!-- LINKS - Internal -->
[az-ad-sp-create-for-rbac]: /cli/azure/ad/sp#az_ad_sp_create_for_rbac
[az-role-assignment-create]: /cli/azure/role/assignment#az_role_assignment_create
