---
title: Aktive Georeplikation – Azure SQL-Datenbank | Microsoft-Dokumentation
description: Mit aktiver Georeplikation können Sie lesbare sekundäre Datenbanken für einzelne Datenbanken im gleichen oder einem anderen Rechenzentrum (Region) erstellen.
services: sql-database
ms.service: sql-database
ms.subservice: high-availability
ms.custom: ''
ms.devlang: ''
ms.topic: conceptual
author: anosov1960
ms.author: sashan
ms.reviewer: mathoma, carlrab
manager: craigg
ms.date: 01/25/2019
ms.openlocfilehash: ae57605b0fb2cba8cdb0c2f9ecfbab8eef7a5197
ms.sourcegitcommit: 698a3d3c7e0cc48f784a7e8f081928888712f34b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/31/2019
ms.locfileid: "55468273"
---
# <a name="create-readable-secondary-databases-using-active-geo-replication"></a>Erstellen lesbarer sekundärer Datenbanken mithilfe aktiver Georeplikation

Die aktive Georeplikation ist eine Funktion in Azure SQL-Datenbank, mit der Sie lesbare sekundäre Datenbanken für einzelne Datenbanken auf einem SQL-Datenbank-Server im selben oder in einem anderen Rechenzentrum (Region) erstellen können.

> [!NOTE]
> Die aktive Georeplikation wird von der verwalteten Instanz nicht unterstützt. Für ein geografisches Failover verwalteter Datenbanken verwenden Sie [Autofailover-Gruppen](sql-database-auto-failover-group.md).

Aktive Georeplikation ist als Geschäftskontinuitätslösung konzipiert, die der Anwendung im Falle eines regionalen Notfalls oder größeren Ausfalls eine schnelle Notfallwiederherstellung einzelner Datenbanken ermöglicht. Wenn Georeplikation aktiviert ist, kann die Anwendung ein Failover auf eine sekundäre Datenbank in einer anderen Azure-Region initiieren. Bis zu vier sekundäre Datenbanken werden in derselben oder verschiedenen Regionen unterstützt, und die sekundären Datenbanken können auch für schreibgeschützten Abfragezugriff verwendet werden. Das Failover muss durch die Anwendung oder den Benutzer manuell eingeleitet werden. Nach einem Failover hat die neue primäre Datenbank einen anderen Verbindungsendpunkt. Das folgende Diagramm zeigt eine typische Konfiguration einer georedundanten Cloudanwendung mit aktiver Georeplikation.

![Aktive Georeplikation](./media/sql-database-active-geo-replication/geo-replication.png )

> [!IMPORTANT]
> SQL-Datenbank unterstützt auch Autofailover-Gruppen. Weitere Informationen finden Sie unter [Autofailover-Gruppen](sql-database-auto-failover-group.md). Aktive Georeplikation wird für Datenbanken, die innerhalb einer verwalteten Instanz erstellt wurden, nicht unterstützt. Ziehen Sie bei verwalteten Instanzen die Verwendung von [Failovergruppen](sql-database-auto-failover-group.md) in Betracht.

Falls Ihre primäre Datenbank aus irgendeinem Grund ausfällt oder einfach offline geschaltet werden muss, können Sie ein Failover auf eine der sekundären Datenbanken initiieren. Wenn das Failover auf eine sekundäre Datenbank aktiviert ist, werden alle anderen sekundären Datenbanken automatisch mit der neuen primären Datenbank verknüpft.

Sie können Replikation und Failover für eine einzelne Datenbank oder eine Gruppe von Datenbanken auf einem Server oder in einem Pool für elastische Datenbanken mithilfe der aktiven Georeplikation verwalten. Verwenden Sie hierfür Folgendes:

- Das [Azure-Portal](sql-database-geo-replication-portal.md)
- [PowerShell: Einzelne Datenbank](scripts/sql-database-setup-geodr-and-failover-database-powershell.md)
- [PowerShell: Pool für elastische Datenbanken](scripts/sql-database-setup-geodr-and-failover-pool-powershell.md)
- [Transact-SQL: Einzelne Datenbank oder Pool für elastische Datenbanken](/sql/t-sql/statements/alter-database-azure-sql-database)
- [REST-API: Einzelne Datenbank](https://docs.microsoft.com/rest/api/sql/replicationlinks)

Stellen Sie nach dem Failover sicher, dass die Authentifizierungsanforderungen für Ihren Server und Ihre Datenbank auf der neuen primären konfiguriert sind. Weitere Informationen finden Sie unter [Verwalten der Sicherheit der Azure SQL-Datenbank nach der Notfallwiederherstellung](sql-database-geo-replication-security-config.md).

Aktive Georeplikation nutzt die [Always On](https://docs.microsoft.com/sql/database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server)-Technologie von SQL Server, um Transaktionen mit ausgeführtem Commit in der primären Datenbank asynchron mit Momentaufnahmeisolation in eine sekundäre Datenbank zu replizieren. Gruppen für automatisches Failover stellen die Gruppensemantik über der aktiven Georeplikation bereit, es wird aber der gleiche asynchrone Replikationsmechanismus verwendet. Wenngleich die sekundäre Datenbank stets ein wenig hinter der primären Datenbank zurückliegt, sind unvollständige Transaktionen bei sekundären Daten garantiert ausgeschlossen. Regionsübergreifende Redundanz ermöglicht Anwendungen die schnelle Wiederherstellung nach einem dauerhaften Ausfall eines gesamten Rechenzentrums oder von Teilen eines Rechenzentrums aufgrund von Naturkatastrophen, schwerwiegendem menschlichen Versagen oder böswilligen Handlungen. Die spezifischen RPO-Daten finden Sie unter [Übersicht über die Geschäftskontinuität mit Azure SQL-Datenbank](sql-database-business-continuity.md).

Die folgende Abbildung zeigt ein Beispiel für die Konfiguration der aktiven Georeplikation, wobei sich die primäre Datenbank in der Region „USA, Norden-Mitte“ und die sekundäre Datenbank in der Region „USA, Süden-Mitte“ befindet.

![Georeplikationsbeziehung](./media/sql-database-active-geo-replication/geo-replication-relationship.png)

Weil die sekundären Datenbanken lesbar sind, können sie zum Auslagern schreibgeschützter Workloads wie Berichtsaufträge verwendet werden. Bei Verwendung der aktiven Georeplikation können Sie die sekundäre Datenbank in der gleichen Region wie die primäre erstellen, aber dies steigert nicht die Stabilität der Anwendung gegenüber schwerwiegenden Ausfällen. Wenn Sie Gruppen für automatisches Failover verwenden, werden die sekundären Datenbanken immer in einer anderen Region erstellt.

Zusätzlich zur Wiederherstellung im Notfall kann aktive Georeplikation in den folgenden Szenarien verwendet werden:

- **Datenbankmigration**: Sie können die aktive Georeplikation zur Onlinemigration einer Datenbank von einem Server auf einen anderen mit minimalen Ausfallzeiten nutzen.
- **Anwendungsupgrades**: Sie können bei Anwendungsupgrades eine zusätzliche sekundäre Datenbank als Failbackkopie erstellen.

Wenn Sie echte Geschäftskontinuität erreichen möchten, ist das Bereitstellen von Datenbankredundanz zwischen Rechenzentren jedoch nur ein Teil der Lösung. Für die komplette Wiederherstellung einer Anwendung bzw. eines Diensts nach einem schwerwiegenden Fehler ist das Wiederherstellen aller Komponenten erforderlich, aus denen sich der Dienst und alle abhängigen Dienste zusammensetzen. Beispiele dieser Komponenten sind die Clientsoftware (z. B. ein Browser mit benutzerdefiniertem JavaScript), Web-Front-Ends, Speicher und DNS. Es ist wichtig, dass alle Komponenten hinsichtlich derselben Fehler gegen Ausfälle geschützt und innerhalb des RTO (Recovery Time Objective) der Anwendung wieder verfügbar sind. Daher müssen Sie alle abhängigen Dienste bestimmen und mit dem Leistungsumfang und den Funktionen vertraut sein, die sie bieten. Dann müssen Sie entsprechende Maßnahmen ergreifen, um sicherzustellen, dass Ihr Dienst während des Failovers der Dienste funktioniert, von denen er abhängig ist. Weitere Informationen zum Entwerfen von Lösungen für die Notfallwiederherstellung finden Sie unter [Entwerfen von Cloudlösungen für die Notfallwiederherstellung mithilfe der aktiven Georeplikation](sql-database-designing-cloud-solutions-for-disaster-recovery.md).

## <a name="active-geo-replication-terminology-and-capabilities"></a>Aktive Georeplikation – Terminologie und Funktionen

- **Automatische asynchrone Replikation**

 Sie können eine sekundäre Datenbank nur erstellen, indem Sie diese einer vorhandenen Datenbank hinzufügen. Die sekundäre Datenbank kann auf einem anderen Azure SQL-Datenbank-Server erstellt werden. Nach der Erstellung wird die sekundäre Datenbank mit den Daten aufgefüllt, die aus der primären Datenbank kopiert wurden. Dieser Prozess wird als Seeding bezeichnet. Nachdem eine sekundäre Datenbank erstellt wurde und das Seeding erfolgt ist, werden Aktualisierungen der primären Datenbank automatisch asynchron in die sekundäre Datenbank repliziert. Asynchrone Replikation bedeutet, dass für Transaktionen in der primären Datenbank ein Commit erfolgt, ehe sie in die sekundäre Datenbank repliziert werden.

- **Lesbare sekundäre Datenbanken**

  Eine Anwendung kann für schreibgeschützte Vorgänge auf eine sekundäre Datenbank zugreifen, indem sie die Sicherheitsprinzipale für den Zugriff auf die primäre Datenbank oder andere Sicherheitsprinzipale verwendet. Die sekundären Datenbanken werden im Momentaufnahme-Isolationsmodus betrieben. Auf diese Weise wird sichergestellt, dass die Replikation von Aktualisierungen der primären Datenbank (Protokollwiedergabe) nicht durch Abfragen verzögert wird, die für die sekundäre Datenbank ausgeführt werden.

  > [!NOTE]
  > Die Protokollwiedergabe wird in der sekundären Datenbank verzögert, wenn Schemaupdates für die primäre Datenbank vorhanden sind. In diesem Fall ist eine Schemasperre für die sekundäre Datenbank erforderlich.

- **Geplantes Failover**

  Beim geplanten Failover wird eine vollständige Synchronisierung zwischen primärer und sekundärer Datenbank ausgeführt, bevor die sekundäre Datenbank die Rolle der primären Datenbank übernimmt. Dadurch ist sichergestellt, dass keine Daten verloren gehen. Ein geplantes Failover wird in folgenden Szenarien verwendet: (a) zum Ausführen von DR-Drills in der Produktion, wenn ein Datenverlust nicht akzeptabel ist, (b) zum Verschieben der Datenbank in eine andere Region, (c) für die Rückkehr der Datenbank in die primäre Region, nachdem der Ausfall behoben wurde (Failback).

- **Nicht geplantes Failover**

  Beim ungeplanten oder erzwungenen Failover übernimmt die sekundäre Datenbank sofort die Rolle der primären Datenbank, ohne dass eine Synchronisierung mit der primären Datenbank stattfindet. Bei diesem Vorgang gehen Daten verloren. Ein ungeplantes Failover wird als Wiederherstellungsmethode bei Ausfällen verwendet, wenn auf die primäre Datenbank nicht zugegriffen werden kann. Wenn die ursprüngliche primäre Datenbank wieder online ist, stellt sie automatisch wieder eine Verbindung ohne Synchronisierung her und wird zur neuen sekundären Datenbank.

- **Mehrere lesbare sekundäre Datenbanken**

  Es können bis zu vier sekundäre Datenbanken für eine primäre Datenbank erstellt werden. Wenn es nur eine sekundäre Datenbank gibt und diese ausfällt, ist die Anwendung bis zum Erstellen einer neuen sekundären Datenbank einem höheren Risiko ausgesetzt. Wenn mehrere sekundäre Datenbanken vorhanden sind, bleibt die Anwendung auch bei Ausfall einer der sekundären Datenbanken geschützt. Die zusätzlichen sekundären Datenbanken können auch zum horizontalen Skalieren der schreibgeschützten Workloads verwendet werden.

  > [!NOTE]
  > Wenn Sie mit der aktiven Georeplikation eine global verteilte Anwendung erstellen und schreibgeschützten Zugriff auf Daten in mehr als vier Regionen bereitstellen müssen, können Sie eine sekundäre Datenbank einer sekundären Datenbank erstellen (dieser Prozess wird als Verkettung bezeichnet). Auf diese Weise können Sie die Datenbankreplikation praktisch unbegrenzt skalieren. Darüber hinaus verkürzt die Verkettung den Mehraufwand der Replikation von der primären Datenbank. Der Nachteil besteht in der erhöhten Replikationsverzögerung in den äußersten sekundären Datenbanken.

- **Georeplikation von Datenbanken in einem Pool für elastische Datenbanken**

  Jede sekundäre Datenbank kann einzeln in einem Pool für elastische Datenbanken enthalten sein oder sich in keinem Pool befinden. Die Auswahl des Pools für jede sekundäre Datenbank erfolgt einzeln und ist nicht von der Konfiguration einer anderen sekundären Datenbank abhängig (ob primär oder sekundär). Jeder Pool für elastische Datenbanken befindet sich innerhalb einer einzelnen Region, daher können mehrere sekundäre Datenbanken in derselben Topologie einen Pool für elastische Datenbanken nie gemeinsam verwenden.

- **Konfigurierbare Computegröße der sekundären Datenbank**

  Sowohl die primäre als auch die sekundäre Datenbank müssen die gleiche Dienstebene aufweisen. Darüber hinaus wird dringend empfohlen, eine sekundäre Datenbank mit der gleichen Computegröße (DTUs oder virtuelle Kerne) wie die primäre Datenbank zu erstellen. Bei einer sekundären Datenbank mit einer niedrigeren Computegröße besteht das Risiko, dass eine größere Replikationsverzögerung auftritt und die sekundäre Datenbank nicht verfügbar ist. Dies kann nach einem Failover erhebliche Datenverluste zur Folge haben. Daher kann die veröffentlichte RPO von 5 Sekunden nicht garantiert werden. Ein weiteres Risiko besteht darin, dass die Leistung der Anwendung nach einem Failover beeinträchtigt ist, da die neue primäre Datenbank über zu geringe Computekapazität verfügt, bis sie auf eine höhere Computegröße aktualisiert wird. Der Zeitpunkt des Upgrades hängt von der Größe der Datenbank ab. Darüber hinaus erfordert ein solches Upgrade derzeit, dass sowohl primäre als auch sekundäre Datenbanken online sind. Daher kann ein Update erst abgeschlossen werden, wenn der Ausfall behoben ist. Wenn Sie die sekundäre Datenbank mit einer niedrigeren Computegröße erstellen, können Sie anhand des Diagramms mit dem Protokoll-E/A-Prozentsatz im Azure-Portal gut abschätzen, welche Computegröße für die sekundäre Datenbank mindestens erforderlich ist, um die Replikationslast zu bewältigen. Wenn die Leistungsstufe der primären Datenbank beispielsweise P6 (1.000 DTU) ist und ihr Protokoll-E/A-Prozentsatz 50 % beträgt, muss die Leistungsstufe der sekundären Datenbank mindestens P4 (500 DTU) sein. Sie können die Protokoll-E/A-Daten auch mithilfe der Datenbanksicht [sys.resource_stats](/sql/relational-databases/system-catalog-views/sys-resource-stats-azure-sql-database) oder [sys.dm_db_resource_stats](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-resource-stats-azure-sql-database) abrufen.  Weitere Informationen zu SQL-Datenbank-Computegrößen finden Sie im Artikel über die [SQL-Datenbank-Dienstebenen](sql-database-service-tiers.md).

- **Benutzergesteuertes Failover und Failback**

  Eine sekundäre Datenbank kann jederzeit durch die Anwendung oder den Benutzer explizit die primäre Rolle erhalten. Bei einem echten Ausfall sollte die Option „Nicht geplant“ verwendet werden, die eine sekundäre Datenbank umgehend zu einer primären Datenbank heraufstuft. Wenn die ausgefallene primäre Datenbank wiederhergestellt ist und wieder zur Verfügung steht, kennzeichnet das System diese wiederhergestellte primäre Datenbank automatisch als sekundäre Datenbank und bringt sie auf den aktuellen Stand der neuen primären Datenbank. Aufgrund der asynchronen Natur der Replikation kann eine kleine Menge von Daten bei einem nicht geplanten Failover verloren gehen, wenn eine primäre Datenbank ausfällt, bevor die aktuellen Änderungen in die sekundäre Datenbank repliziert wurden. Wenn für eine primäre Datenbank mit mehreren sekundären Datenbanken ein Failover durchgeführt wird, konfiguriert das System automatisch die Replikationsbeziehungen neu und verknüpft die verbleibenden sekundären Datenbanken mit der soeben heraufgestuften primären Datenbank, ohne dass ein Benutzereingriff erforderlich ist. Wenn der Ausfall behoben ist, durch den das Failover verursacht wurde, kann es wünschenswert sein, die Anwendung wieder in die primäre Region zurückzuführen. Zu diesem Zweck sollte der Failoverbefehl mit der Option „Geplant“ aufgerufen werden.

- **Synchronisieren von Anmeldeinformationen und Firewallregeln**

  Wir empfehlen die Verwendung von [Datenbank-Firewallregeln](sql-database-firewall-configure.md) für georeplizierte Datenbanken, damit diese Regeln mit der Datenbank repliziert werden können. So wird sichergestellt, dass alle sekundären Datenbanken die gleichen Firewallregeln wie die primäre Datenbank besitzen. Mit diesem Ansatz müssen Kunden auf Servern, auf denen sowohl die primäre als auch die sekundäre Datenbank gehostet wird, keine Firewallregeln mehr manuell konfigurieren und verwalten. Analog dazu wird durch die Verwendung von [eigenständigen Datenbankbenutzern](sql-database-manage-logins.md) für den Datenzugriff sichergestellt, dass für primäre und sekundäre Datenbanken immer die gleichen Benutzeranmeldeinformationen gelten, damit bei einem Failover keine Unterbrechungen durch Benutzernamen- und Kennwortkonflikte auftreten. Durch Hinzufügen von [Azure Active Directory](../active-directory/fundamentals/active-directory-whatis.md) können Kunden den Benutzerzugriff sowohl für primäre als auch für sekundäre Datenbanken verwalten, sodass die Notwendigkeit der Verwaltung von Anmeldeinformationen in Datenbanken vollständig entfällt.

## <a name="upgrading-or-downgrading-a-primary-database"></a>Upgrade oder Downgrade einer primären Datenbank

Sie können für eine primäre Datenbank ein Upgrade oder Downgrade auf eine andere Computegröße (innerhalb der gleichen Dienstebene; nicht zwischen „Universell“ und „Unternehmenskritisch“) ausführen, ohne die Verbindung mit sekundären Datenbanken zu trennen. Bei einem Upgrade wird empfohlen, zuerst das Upgrade für die sekundäre Datenbank und anschließend das Upgrade für die primäre Datenbank auszuführen. Drehen Sie bei einem Downgrade die Reihenfolge um: Führen Sie zuerst das Downgrade für die primäre und anschließend das Downgrade für die sekundäre Datenbank aus. Wenn Sie ein Upgrade oder Downgrade der Datenbank auf eine andere Dienstebene durchführen, wird diese Empfehlung erzwungen.

> [!NOTE]
> Wenn Sie eine sekundäre Datenbank als Teil der Konfiguration der Failovergruppe erstellt haben, sollten Sie kein Downgrade der sekundären Datenbank durchführen. So wird sichergestellt, dass Ihre Datenebene nach dem Aktivieren des Failovers ausreichende Kapazität zum Verarbeiten des normalen Workloads hat.

## <a name="preventing-the-loss-of-critical-data"></a>Verhindern des Verlusts wichtiger Daten

Aufgrund der hohen Latenz von WANs wird für die fortlaufende Kopie ein asynchroner Replikationsmechanismus verwendet. Asynchrone Replikation macht Datenverlust unvermeidlich, sobald ein Ausfall auftritt. Bei einigen Anwendung dürfen jedoch ggf. keine Daten verloren gehen. Um diese kritischen Aktualisierungen zu schützen, kann ein Anwendungsentwickler die Systemprozedur [sp_wait_for_database_copy_sync](/sql/relational-databases/system-stored-procedures/active-geo-replication-sp-wait-for-database-copy-sync) aufrufen, unmittelbar nachdem der Commit für die Transaktion erfolgt ist. Das Aufrufen von **sp_wait_for_database_copy_sync** blockiert den aufrufenden Thread so lange, bis die letzte Transaktion mit erfolgtem Commit in die sekundäre Datenbank übertragen wurde. Es wird jedoch nicht abgewartet, bis die übertragenen Transaktionen wiedergegeben und in der sekundären Datenbank committet werden. **sp_wait_for_database_copy_sync** ist auf eine bestimmte fortlaufende Kopierverknüpfung begrenzt. Jeder Benutzer mit den Rechten zum Herstellen der Verbindung mit der primären Datenbank kann diese Prozedur aufrufen.

> [!NOTE]
> **sp_wait_for_database_copy_sync** verhindert Datenverlust nach einem Failover, garantiert aber nicht die vollständige Synchronisierung für den Lesezugriff. Die vom Aufruf der Prozedur **sp_wait_for_database_copy_sync** verursachte Verzögerung kann signifikant sein und hängt von der Größe des Transaktionsprotokolls zum Zeitpunkt des Aufrufs ab.

## <a name="programmatically-managing-active-geo-replication"></a>Programmgesteuertes Verwalten der aktiven Georeplikation

Wie bereits zuvor erwähnt, kann die aktive Georeplikation auch programmgesteuert mit Azure PowerShell und der REST-API verwaltet werden. Die folgenden Tabellen beschreiben den verfügbaren Satz von Befehlen. Die aktive Georeplikation umfasst eine Reihe von Azure Resource Manager-APIs für die Verwaltung. Hierzu zählen unter anderem die [Azure SQL-Datenbank-REST-API](https://docs.microsoft.com/rest/api/sql/) und [Azure PowerShell-Cmdlets](https://docs.microsoft.com/powershell/azure/overview). Diese APIs erfordern die Verwendung von Ressourcengruppen und unterstützen rollenbasierte Sicherheit (RBAC). Weitere Informationen zur Implementierung von Zugriffsrollen finden Sie unter [Rollenbasierte Zugriffssteuerung in Azure](../role-based-access-control/overview.md).

### <a name="t-sql-manage-failover-of-standalone-and-pooled-databases"></a>T-SQL: Verwalten des Failovers von eigenständigen und in einem Pool zusammengefassten Datenbanken

> [!IMPORTANT]
> Diese Transact-SQL-Befehle gelten nur für die aktive Georeplikation und nicht für Failovergruppen. Daher gelten sie auch nicht für verwaltete Instanzen, da diese nur Failovergruppen unterstützen.

| Get-Help | Beschreibung |
| --- | --- |
| [ALTER DATABASE](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql?view=azuresqldb-current) |Verwenden Sie das Argument ADD SECONDARY ON SERVER, um eine sekundäre Datenbank für eine vorhandene Datenbank zu erstellen und die Datenreplikation zu starten. |
| [ALTER DATABASE](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql?view=azuresqldb-current) |Verwenden Sie FAILOVER oder FORCE_FAILOVER_ALLOW_DATA_LOSS, um die sekundäre Datenbank zur primären zu erklären und zu ihr zu wechseln – damit starten Sie das Failover. |
| [ALTER DATABASE](https://docs.microsoft.com/sql/t-sql/statements/alter-database-transact-sql?view=azuresqldb-current) |Verwenden Sie REMOVE SECONDARY ON SERVER, um die Datenreplikation zwischen einer SQL-Datenbank und der angegebenen sekundären Datenbank zu beenden. |
| [sys.geo_replication_links](/sql/relational-databases/system-dynamic-management-views/sys-geo-replication-links-azure-sql-database) |Gibt Informationen über alle vorhandenen Replikationsverknüpfungen für alle Datenbanken auf dem Azure SQL-Datenbank-Server zurück. |
| [sys.dm_geo_replication_link_status](/sql/relational-databases/system-dynamic-management-views/sys-dm-geo-replication-link-status-azure-sql-database) |Ruft den Zeitpunkt der letzten Replikation, die Verzögerung der letzten Replikation und andere Informationen über die Replikationsverknüpfung für eine angegebene SQL-Datenbank ab. |
| [sys.dm_operation_status](/sql/relational-databases/system-dynamic-management-views/sys-dm-operation-status-azure-sql-database) |Zeigt den Status für alle Datenbankvorgänge an, einschließlich des Status der Replikationsverknüpfungen. |
| [sp_wait_for_database_copy_sync](/sql/relational-databases/system-stored-procedures/active-geo-replication-sp-wait-for-database-copy-sync) |Bewirkt, dass die Anwendung wartet, bis alle Transaktionen mit erfolgtem Commit repliziert und von der aktiven sekundären Datenbank bestätigt wurden. |
|  | |

### <a name="powershell-manage-failover-of-standalone-and-pooled-databases"></a>PowerShell: Verwalten des Failovers von eigenständigen und in einem Pool zusammengefassten Datenbanken

| Cmdlet | Beschreibung |
| --- | --- |
| [Get-AzureRmSqlDatabase](https://docs.microsoft.com/powershell/module/azurerm.sql/get-azurermsqldatabase) |Ruft mindestens eine Datenbank ab. |
| [New-AzureRmSqlDatabaseSecondary](https://docs.microsoft.com/powershell/module/azurerm.sql/new-azurermsqldatabasesecondary) |Erstellt eine sekundäre Datenbank für eine vorhandene Datenbank und startet die Datenreplikation. |
| [Set-AzureRmSqlDatabaseSecondary](https://docs.microsoft.com/powershell/module/azurerm.sql/set-azurermsqldatabasesecondary) |Erklärt die sekundäre Datenbank zur primären und wechselt zu ihr – dadurch wird das Failover gestartet. |
| [Remove-AzureRmSqlDatabaseSecondary](https://docs.microsoft.com/powershell/module/azurerm.sql/remove-azurermsqldatabasesecondary) |Beendet die Datenreplikation zwischen einer SQL-Datenbank und der angegebenen sekundären Datenbank. |
| [Get-AzureRmSqlDatabaseReplicationLink](https://docs.microsoft.com/powershell/module/azurerm.sql/get-azurermsqldatabasereplicationlink) |Ruft die Georeplikationsverknüpfungen zwischen einer Azure SQL-Datenbank und einer Ressourcengruppe oder einer SQL Server-Instanz ab. |
|  | |

> [!IMPORTANT]
> Beispielskripts finden Sie unter [Verwenden von PowerShell zum Konfigurieren der aktiven Georeplikation für eine einzelne Azure SQL-Datenbank](scripts/sql-database-setup-geodr-and-failover-database-powershell.md) und [Verwenden von PowerShell zum Konfigurieren der aktiven Georeplikation für eine in einem Pool enthaltene Azure SQL-Datenbank](scripts/sql-database-setup-geodr-and-failover-pool-powershell.md).

### <a name="rest-api-manage-failover-of-standalone-and-pooled-databases"></a>REST-API: Verwalten des Failovers von eigenständigen und in einem Pool zusammengefassten Datenbanken

| API | Beschreibung |
| --- | --- |
| [Create or Update Database (createMode=Restore)](https://docs.microsoft.com/rest/api/sql/databases/createorupdate) |Erstellt oder aktualisiert eine primäre oder sekundäre Datenbank oder stellt diese wieder her. |
| [Get Create or Update Database Status](https://docs.microsoft.com/rest/api/sql/databases/createorupdate) |Ruft den Status während eines Erstellungsvorgangs ab. |
| [Set Secondary Database as Primary (Planned Failover)](https://docs.microsoft.com/rest/api/sql/replicationlinks/failover) |Legt fest, welche sekundäre Datenbank als primäre Datenbank verwendet wird, indem ein Failover von der aktuellen primären Datenbank durchgeführt wird. **Diese Option wird bei einer verwalteten Instanz nicht unterstützt.**|
| [Set Secondary Database as Primary (Unplanned Failover)](https://docs.microsoft.com/rest/api/sql/replicationlinks/failoverallowdataloss) |Legt fest, welche sekundäre Datenbank als primäre Datenbank verwendet wird, indem ein Failover von der aktuellen primären Datenbank durchgeführt wird. Bei diesem Vorgang können Daten verloren gehen. **Diese Option wird bei einer verwalteten Instanz nicht unterstützt.**|
| [Get Replication Link](https://docs.microsoft.com/rest/api/sql/replicationlinks/get) |Ruft eine spezifische Replikationsverknüpfung für eine angegebene SQL-Datenbank in einer Georeplikationspartnerschaft ab. Es werden die Informationen abgerufen, die in der Katalogsicht „sys.geo_replication_links“ sichtbar sind. **Diese Option wird bei einer verwalteten Instanz nicht unterstützt.**|
| [Replication Links - List By Database](https://docs.microsoft.com/rest/api/sql/replicationlinks/listbydatabase) | Ruft alle Replikationsverknüpfungen für eine angegebene SQL-Datenbank in einer Georeplikationspartnerschaft ab. Es werden die Informationen abgerufen, die in der Katalogsicht „sys.geo_replication_links“ sichtbar sind. |
| [Delete Replication Link](https://docs.microsoft.com/rest/api/sql/replicationlinks/delete) | Löscht einen Datenbankreplikationslink. Kann nicht während eines Failovers verwendet werden. |
|  | |

## <a name="next-steps"></a>Nächste Schritte

- Beispielskripts:
  - [Configure and failover a single database using active geo-replication](scripts/sql-database-setup-geodr-and-failover-database-powershell.md) (Konfiguration und Failover einer einzelnen Datenbank mithilfe von aktiver Georeplikation)
  - [Configure and failover a pooled database using active geo-replication](scripts/sql-database-setup-geodr-and-failover-pool-powershell.md) (Konfiguration und Failover einer gepoolten Datenbank mithilfe von aktiver Georeplikation)
- SQL-Datenbank unterstützt auch Autofailover-Gruppen. Weitere Informationen finden Sie unter [Autofailover-Gruppen](sql-database-auto-failover-group.md).
- Eine Übersicht und verschiedene Szenarien zum Thema Geschäftskontinuität finden Sie unter [Übersicht über die Geschäftskontinuität](sql-database-business-continuity.md)
- Informationen über automatisierte Sicherungen von Azure SQL-Datenbanken finden Sie unter [Übersicht: Automatisierte SQL-Datenbanksicherungen](sql-database-automated-backups.md).
- Informationen zum Verwenden automatisierter Sicherungen für die Wiederherstellung finden Sie unter [Wiederherstellen einer Datenbank aus vom Dienst initiierten Sicherungen](sql-database-recovery-using-backups.md).
- Weitere Informationen zu Authentifizierungsanforderungen für einen neuen primären Server und die Datenbank finden Sie unter [Verwalten der Sicherheit der Azure SQL-Datenbank nach der Notfallwiederherstellung](sql-database-geo-replication-security-config.md).
