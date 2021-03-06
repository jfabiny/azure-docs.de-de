---
title: Status von Datenbankmigrationsszenarios | Microsoft-Dokumentation
description: Lernen Sie den Status von Migrationsszenarios kennen, die von Azure Database Migration Service unterstützt werden.
services: database-migration
author: pochiraju
ms.author: rajpo
manager: craigg
ms.reviewer: douglasl
ms.service: dms
ms.workload: data-services
ms.custom: mvc
ms.topic: article
ms.date: 01/15/2019
ms.openlocfilehash: edc6e651c3ec352115e360e50f98a3e36cd287c0
ms.sourcegitcommit: 644de9305293600faf9c7dad951bfeee334f0ba3
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/25/2019
ms.locfileid: "54904079"
---
# <a name="status-of-migration-scenarios-supported-by-the-azure-database-migration-service"></a>Status von Migrationsszenarios, die von Azure Database Migration Service unterstützt werden
Azure Database Migration Service wurde zur Unterstützung einer Vielzahl von Migrationsszenarios (Quelle/Ziel-Paare) und sowohl für die Offline- (einmalig) als auch die Onlinemigration (fortlaufende Synchronisierung) konzipiert. Der von Azure Database Migration Service bereitgestellte Szenarioumfang wird im Laufe der Zeit erweitert. In regelmäßigen Abständen werden neue Szenarios hinzugefügt. Dieser Artikel beschreibt die Migrationsszenarien, die derzeit von Azure Database Migration Service unterstützt werden, sowie die Status der einzelnen Szenarien (private [eingeschränkte] Vorschau, öffentliche Vorschau oder allgemein verfügbar).

## <a name="offline-versus-online-migrations"></a>Offline- und Onlinemigrationen
Beim Migrieren von Datenbanken zu Azure mit dem Azure Database Migration Service können Sie eine Migration des Typs „Offline“ oder „Online“ durchführen. Bei Migrationen des Typs *Offline* beginnt die Ausfallzeit der Anwendung mit dem Start der Migration. Bei Migrationen des Typs *Online* ist die Ausfallzeit auf die Zeit begrenzt, die bei Abschluss der Migration für die Umstellung auf die neue Umgebung erforderlich ist. Es empfiehlt sich, eine Offlinemigration zu testen, um zu ermitteln, ob die Ausfallzeit akzeptabel ist. Wenn dies nicht der Fall ist, sollten Sie eine Onlinemigration durchführen.

## <a name="migration-scenario-status"></a>Status von Migrationsszenarios
Der Status der einzelnen Migrationsszenarios, die von Azure Database Migration Service unterstützt werden, verändert sich mit der Zeit. Szenarios werden im Allgemeinen zuerst als **Private Vorschau** veröffentlicht und nutzen die Nominierungsfunktion, d. h. ein Kunde muss über die [DMS Preview-Website](https://aka.ms/dms-preview) eine Nominierung übermitteln. Wenn die Private Vorschau abgeschlossen ist, ändert sich der Szenariostatus in **Öffentliche Vorschau**. Alle Benutzer von Azure Database Migration Service können die in der öffentlichen Vorschau verfügbaren Migrationsszenarios nutzen. Allerdings ist das Migrationsszenario möglicherweise nicht in allen Regionen verfügbar, und vor der endgültigen Veröffentlichung werden ggf. noch weitere Änderungen an der Funktionalität vorgenommen. Wenn ein Migrationsszenario den Status **Allgemein verfügbar**, den endgültigen Veröffentlichungsstatus, erreicht, ist die Funktionalität fertiggestellt und für alle Azure Database Migration Service-Benutzer zugänglich. 

## <a name="migration-scenario-support"></a>Unterstützung von Migrationsszenarios

Die folgenden Tabellen zeigen, welche Migrationsszenarios bei Verwendung des Azure Database Migration Service unterstützt werden.

> [!NOTE]
> Wenn ein Szenario, das im Folgenden als unterstützt aufgeführt, auf der Benutzeroberfläche aber nicht angezeigt wird, wenden Sie sich an das [Data Migration-Team](mailto:datamigrationteam@microsoft.com), um weitere Informationen zu erhalten.

### <a name="offline-one-time-migration-support"></a>Unterstützung der Offlinemigration (einmalig)
Die folgende Tabelle enthält die Azure Database Migration Service-Unterstützung für Offlinemigrationen.

| Ziel  | Quelle | Support |
| ------------- | ------------- | :-------------: |
| **Azure SQL-Datenbank**  | SQL Server | ✔ |
|   | RDS SQL  |  ✔ |
|   | Oracle  |   |
| **Azure SQL-Datenbank MI**  | SQL Server  | ✔ |
|   | RDS SQL  | ✔ |
|   | Oracle  | ✔  |
| **Virtueller Azure SQL-Computer**  | SQL Server | ✔ |
|   | Oracle  |   |
| **Azure Cosmos DB**  | MongoDB | ✔ |
| **Azure-Datenbank für MySQL**  | MySQL |  |
|   | RDS MySQL  |  |
| **Azure-Datenbank für PostgreSQL**  | PostgreSQL |  |
|  | RDS PostgreSQL  |  |

### <a name="online-continuous-sync-migration-support"></a>Unterstützung der Onlinemigration (fortlaufende Synchronisierung)
Die folgende Tabelle enthält die Azure Database Migration Service-Unterstützung für Onlinemigrationen.

| Ziel  | Quelle | Support |
| ------------- | ------------- | :-------------: |
| **Azure SQL-Datenbank**  | SQL Server | ✔ |
|   | RDS SQL  |   |
|   | Oracle  |  ✔ |
| **Azure SQL-Datenbank MI**  | SQL Server  | ✔ |
|   | RDS SQL  |  |
|   | Oracle  | ✔  |
| **Virtueller Azure SQL-Computer**  | SQL Server  |   |
|   | Oracle  | ✔  |
| **Azure Cosmos DB**  | MongoDB  | ✔ |
| **Azure-Datenbank für MySQL**  | MySQL | ✔ |
|   | RDS MySQL  | ✔ |
| **Azure-Datenbank für PostgreSQL**  | PostgreSQL | ✔ |
|  | RDS PostgreSQL  | ✔ |

## <a name="next-steps"></a>Nächste Schritte
Eine Übersicht über Azure Database Migration Service und Informationen zur regionalen Verfügbarkeit finden Sie im Artikel [Was ist Azure Database Migration Service?](dms-overview.md). 
