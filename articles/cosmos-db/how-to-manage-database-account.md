---
title: Verwalten von Datenbankkonten in Azure Cosmos DB
description: Verwalten von Datenbankkonten in Azure Cosmos DB
author: christopheranderson
ms.service: cosmos-db
ms.topic: sample
ms.date: 10/17/2018
ms.author: chrande
ms.openlocfilehash: 1486ab3240036abedea2cbb3cbe93e5c061691d8
ms.sourcegitcommit: 698a3d3c7e0cc48f784a7e8f081928888712f34b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/31/2019
ms.locfileid: "55467406"
---
# <a name="manage-an-azure-cosmos-account"></a>Verwalten eines Azure Cosmos-Kontos

In diesem Artikel wird die Verwaltung Ihres Azure Cosmos DB-Kontos beschrieben. Sie erfahren, wie Sie Multi-Homing einrichten, eine Region hinzufügen oder entfernen, mehrere Schreibregionen konfigurieren und Failoverprioritäten einrichten. 

## <a name="create-a-database-account"></a>Erstellen eines Datenbankkontos

### <a id="create-database-account-via-portal"></a>Azure-Portal

[!INCLUDE [cosmos-db-create-dbaccount](../../includes/cosmos-db-create-dbaccount.md)]

### <a id="create-database-account-via-cli"></a>Azure-Befehlszeilenschnittstelle

```bash
# Create an account
az cosmosdb create --name <Azure Cosmos account name> --resource-group <Resource Group Name>
```

## <a name="configure-clients-for-multi-homing"></a>Konfigurieren von Clients für Multihoming

### <a id="configure-clients-multi-homing-dotnet"></a>.NET SDK

```csharp
// Create a new connection policy.
ConnectionPolicy policy = new ConnectionPolicy
    {
        // Note: These aren't required settings for multi-homing,
        // just suggested defaults.
        ConnectionMode = ConnectionMode.Direct,
        ConnectionProtocol = Protocol.Tcp,
        UseMultipleWriteLocations = true,
    };
// Add regions to preferred locations.
// The name of the location will match what you see in the portal, etc.
policy.PreferredLocations.Add("East US");
policy.PreferredLocations.Add("North Europe");

// Pass the connection policy with the preferred locations on it to the client.
DocumentClient client = new DocumentClient(new Uri(this.accountEndpoint), this.accountKey, policy);
```

### <a id="configure-clients-multi-homing-java-async"></a>Java Async SDK

```java
ConnectionPolicy policy = new ConnectionPolicy();
policy.setPreferredLocations(Collections.singleton("West US"));
AsyncDocumentClient client =
        new AsyncDocumentClient.Builder()
                .withMasterKey(this.accountKey)
                .withServiceEndpoint(this.accountEndpoint)
                .withConnectionPolicy(policy).build();
```

### <a id="configure-clients-multi-homing-java-sync"></a>Java Sync SDK

```java
ConnectionPolicy connectionPolicy = new ConnectionPolicy();
Collection<String> preferredLocations = new ArrayList<String>();
preferredLocations.add("Australia East");
connectionPolicy.setPreferredLocations(preferredLocations);
DocumentClient client = new DocumentClient(accountEndpoint, accountKey, connectionPolicy);
```

### <a id="configure-clients-multi-homing-javascript"></a>Node.js/JavaScript/TypeScript SDK

```javascript
// Set up the connection policy with your preferred regions.
const connectionPolicy: ConnectionPolicy = new ConnectionPolicy();
connectionPolicy.PreferredLocations = ["West US", "Australia East"];

// Pass that connection policy to the client.
const client = new CosmosClient({
  endpoint: config.endpoint,
  auth: { masterKey: config.key },
  connectionPolicy
});
```

### <a id="configure-clients-multi-homing-python"></a>Python SDK

```python
connection_policy = documents.ConnectionPolicy()
connection_policy.PreferredLocations = ['West US', 'Japan West']
client = cosmos_client.CosmosClient(self.account_endpoint, {'masterKey': self.account_key}, connection_policy)

```

## <a name="addremove-regions-from-your-database-account"></a>Hinzufügen/Entfernen von Regionen für Ihr Datenbankkonto

### <a id="add-remove-regions-via-portal"></a>Azure-Portal

1. Navigieren Sie zu Ihrem Azure Cosmos DB-Konto, und öffnen Sie das Menü **Daten global replizieren**.

2. Wenn Sie Regionen hinzufügen möchten, wählen Sie auf der Karte die Sechsecke mit der Beschriftung **+** aus, die der gewünschten Region entsprechen. Wenn Sie eine Region hinzufügen möchten, wählen Sie die Option **+ Region hinzufügen** und anschließend eine Region aus dem Dropdownmenü aus.

3. Wenn Sie Regionen entfernen möchten, entfernen Sie sie von der Karte, indem Sie die blauen, mit einem Häkchen versehenen Sechsecke auswählen. Alternativ können Sie auch neben der Region auf der rechten Seite das Papierkorbsymbol (🗑) auswählen.

4. Wählen Sie zum Speichern der Änderungen **OK** aus.

   ![Menü zum Hinzufügen oder Entfernen von Regionen](./media/how-to-manage-database-account/add-region.png)

Im Schreibmodus mit einer einzelnen Region kann die Schreibregion nicht entfernt werden. In diesem Fall muss erst ein Failover auf eine andere Region durchgeführt werden, um die aktuelle Schreibregion löschen zu können.

Im Schreibmodus mit mehreren Regionen können Sie beliebige Regionen hinzufügen oder entfernen, solange noch mindestens eine Region vorhanden ist.

### <a id="add-remove-regions-via-cli"></a>Azure-Befehlszeilenschnittstelle

```bash
# Given an account created with 1 region like so
az cosmosdb create --name <Azure Cosmos account name> --resource-group <Resource Group name> --locations 'eastus=0'

# Add a new region by adding another region to the list
az cosmosdb update --name <Azure Cosmos account name> --resource-group <Resource Group name> --locations 'eastus=0 westus=1'

# Remove a region by removing a region from the list
az cosmosdb update --name <Azure Cosmos account name> --resource-group <Resource Group name> --locations 'westus=0'
```

## <a name="configure-multiple-write-regions"></a>Konfigurieren mehrerer Schreibregionen

### <a id="configure-multiple-write-regions-portal"></a>Azure-Portal

Achten Sie beim Erstellen eines Datenbankkontos darauf, dass die Einstellung **Multi-region Writes** (Schreibvorgänge in mehreren Regionen) aktiviert ist.

![Screenshot: Azure Cosmos-Kontoerstellung](./media/how-to-manage-database-account/account-create.png)

### <a id="configure-multiple-write-regions-cli"></a>Azure-Befehlszeilenschnittstelle

```bash
az cosmosdb create --name <Azure Cosmos account name> --resource-group <Resource Group name> --enable-multiple-write-locations true
```

### <a id="configure-multiple-write-regions-arm"></a>Resource Manager-Vorlage

Der folgende JSON-Code ist ein Beispiel für eine Azure Resource Manager-Vorlage. Damit können Sie ein Azure Cosmos DB-Konto mit einer Konsistenzrichtlinie für begrenzte Veraltung bereitstellen. Das maximale Veraltungsintervall ist auf fünf Sekunden festgelegt. Die maximale Anzahl tolerierter veralteter Anforderungen ist auf 100 festgelegt. Weitere Informationen zum Resource Manager-Vorlagenformat sowie zur Syntax finden Sie unter [Resource Manager](../azure-resource-manager/resource-group-authoring-templates.md).

```json
{
    "$schema": "https://schema.management.azure.com/schemas/2015-01-01/deploymentTemplate.json#",
    "contentVersion": "1.0.0.0",
    "parameters": {
        "name": {
            "type": "String"
        },
        "location": {
            "type": "String"
        },
        "locationName": {
            "type": "String"
        },
        "defaultExperience": {
            "type": "String"
        }
    },
    "resources": [
        {
            "type": "Microsoft.DocumentDb/databaseAccounts",
            "kind": "GlobalDocumentDB",
            "name": "[parameters('name')]",
            "apiVersion": "2015-04-08",
            "location": "[parameters('location')]",
            "tags": {
                "defaultExperience": "[parameters('defaultExperience')]"
            },
            "properties": {
                "databaseAccountOfferType": "Standard",
                "consistencyPolicy": {
                    "defaultConsistencyLevel": "BoundedStaleness",
                    "maxIntervalInSeconds": 5,
                    "maxStalenessPrefix": 100
                },
                "locations": [
                    {
                        "id": "[concat(parameters('name'), '-', parameters('location'))]",
                        "failoverPriority": 0,
                        "locationName": "[parameters('locationName')]"
                    }
                ],
                "isVirtualNetworkFilterEnabled": false,
                "enableMultipleWriteLocations": true,
                "virtualNetworkRules": [],
                "dependsOn": []
            }
        }
    ]
}
```


## <a id="manual-failover"></a>Aktivieren des manuellen Failovers für Ihr Azure Cosmos DB-Konto

### <a id="enable-manual-failover-via-portal"></a>Azure-Portal

1. Navigieren Sie zu Ihrem Azure Cosmos DB-Konto, und öffnen Sie das Menü **Daten global replizieren**.

2. Wählen Sie im oberen Bereich des Menüs die Option **Manuelles Failover** aus.

   ![Menü „Daten global replizieren“](./media/how-to-manage-database-account/replicate-data-globally.png)

3. Wählen Sie im Menü **Manuelles Failover** Ihre neue Schreibregion aus. Aktivieren Sie das Kontrollkästchen, um anzugeben, dass Sie wissen, dass diese Option Ihre Schreibregion ändert.

4. Wählen Sie **OK** aus, um das Failover zu starten.

   ![Portalmenü für manuelles Failover](./media/how-to-manage-database-account/manual-failover.png)

### <a id="enable-manual-failover-via-cli"></a>Azure-Befehlszeilenschnittstelle

```bash
# Given your account currently has regions with priority like so: 'eastus=0 westus=1'
# Change the priority order to trigger a failover of the write region
az cosmosdb update --name <Azure Cosmos account name> --resource-group <Resource Group name> --locations 'eastus=1 westus=0'
```

## <a id="automatic-failover"></a>Aktivieren des automatischen Failovers für Ihr Azure Cosmos DB-Konto

### <a id="enable-automatic-failover-via-portal"></a>Azure-Portal

1. Öffnen Sie in Ihrem Azure Cosmos DB-Konto den Bereich **Daten global replizieren**. 

2. Wählen Sie im oberen Bereich die Option **Automatisches Failover** aus.

   ![Menü „Daten global replizieren“](./media/how-to-manage-database-account/replicate-data-globally.png)

3. Vergewissern Sie sich im Bereich **Automatisches Failover**, dass **Automatisches Failover aktivieren** auf **EIN** festgelegt ist. 

4. Wählen Sie **Speichern** aus.

   ![Portalmenü für automatisches Failover](./media/how-to-manage-database-account/automatic-failover.png)

In diesem Menü können Sie auch Ihre Failoverprioritäten festlegen.

### <a id="enable-automatic-failover-via-cli"></a>Azure-Befehlszeilenschnittstelle

```bash
# Enable automatic failover on account creation
az cosmosdb create --name <Azure Cosmos account name> --resource-group <Resource Group name> --enable-automatic-failover true

# Enable automatic failover on an existing account
az cosmosdb update --name <Azure Cosmos account name> --resource-group <Resource Group name> --enable-automatic-failover true

# Disable automatic failover on an existing account
az cosmosdb update --name <Azure Cosmos account name> --resource-group <Resource Group name> --enable-automatic-failover false
```

## <a name="set-failover-priorities-for-your-azure-cosmos-db-account"></a>Festlegen von Failoverprioritäten für Ihr Azure Cosmos DB-Konto

### <a id="set-failover-priorities-via-portal"></a>Azure-Portal

1. Öffnen Sie in Ihrem Azure Cosmos DB-Konto den Bereich **Daten global replizieren**. 

2. Wählen Sie im oberen Bereich die Option **Automatisches Failover** aus.

   ![Menü „Daten global replizieren“](./media/how-to-manage-database-account/replicate-data-globally.png)

3. Vergewissern Sie sich im Bereich **Automatisches Failover**, dass **Automatisches Failover aktivieren** auf **EIN** festgelegt ist. 

4. Ziehen Sie zum Ändern der Failoverpriorität die Leseregionen mithilfe der drei Punkte, die auf der linken Seite der Zeile angezeigt werden, wenn Sie darauf zeigen. 

5. Wählen Sie **Speichern** aus.

   ![Portalmenü für automatisches Failover](./media/how-to-manage-database-account/automatic-failover.png)

Die Schreibregion kann in diesem Menü nicht geändert werden. Sie müssen ein manuelles Failover durchführen, um die Schreibregion manuell zu ändern.

### <a id="set-failover-priorities-via-cli"></a>Azure-Befehlszeilenschnittstelle

```bash
az cosmosdb failover-priority-change --name <Azure Cosmos account name> --resource-group <Resource Group name> --failover-policies 'eastus=0 westus=2 southcentralus=1'
```

## <a name="next-steps"></a>Nächste Schritte

Informieren Sie sich über den Umgang mit Konsistenzebenen und Datenkonflikten in Azure Cosmos DB. Entsprechende Informationen finden Sie in den folgenden Artikeln:

* [Verwalten der Konsistenz](how-to-manage-consistency.md)
* [Behandeln von Konflikten zwischen Regionen](how-to-manage-conflicts.md)

