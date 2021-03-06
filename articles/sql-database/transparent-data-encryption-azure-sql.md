---
title: Transparente Datenverschlüsselung für Azure SQL-Datenbank und Data Warehouse | Microsoft-Dokumentation
description: Eine Übersicht über transparente Datenverschlüsselung für SQL-Datenbank und Data Warehouse Das Dokument behandelt die Vorteile dieser Verschlüsselung sowie die Konfigurationsoptionen. Diese umfassen die von einem Dienst verwaltete transparente Datenverschlüsselung und Bring Your Own Key.
services: sql-database
ms.service: sql-database
ms.subservice: security
ms.custom: ''
ms.devlang: ''
ms.topic: conceptual
author: aliceku
ms.author: aliceku
ms.reviewer: vanto
manager: craigg
ms.date: 01/22/2019
ms.openlocfilehash: 7b1d58b82f2ccc99ecacb6099f6063fba5899421
ms.sourcegitcommit: 698a3d3c7e0cc48f784a7e8f081928888712f34b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/31/2019
ms.locfileid: "55478456"
---
# <a name="transparent-data-encryption-for-sql-database-and-data-warehouse"></a>Transparente Datenverschlüsselung für SQL-Datenbank und Data Warehouse

Transparente Datenverschlüsselung (Transparent Data Encryption, TDE) trägt zum Schutz von Azure SQL-Datenbank, einer verwalteten Azure SQL-Instanz und Azure Data Warehouse vor der Bedrohung durch schädliche Aktivitäten bei. TDE ver- und entschlüsselt die Datenbank, die zugehörigen Sicherungen und die Transaktionsprotokolldateien im Ruhezustand in Echtzeit, ohne dass Änderungen an der Anwendung erforderlich sind. TDE ist standardmäßig für alle neu bereitgestellten Azure SQL-Datenbanken aktiviert. TDE kann nicht zum Verschlüsseln der **master**-Datenbank in SQL-Datenbank verwendet werden.  Die **master**-Datenbank enthält Objekte, die zum Ausführen der TDE-Vorgänge für die Benutzerdatenbanken erforderlich sind.

TDE muss für eine verwaltete Azure SQL-Instanz, ältere Datenbanken von Azure SQL-Datenbank oder Azure SQL Data Warehouse manuell aktiviert werden.  

Die transparente Datenverschlüsselung verschlüsselt den Speicher einer gesamten Datenbank mithilfe eines symmetrischen Schlüssels, der als Datenbankverschlüsselungsschlüssel bezeichnet wird. Dieser Verschlüsselungsschlüssel für die Datenbank wird durch die Schutzvorrichtung der transparenten Datenverschlüsselung geschützt. Bei dieser Schutzvorrichtung handelt es sich entweder um ein von einem Dienst verwaltetes Zertifikat (von einem Dienst verwaltete transparente Datenverschlüsselung) oder um einen asymmetrischen Schlüssel, der in Azure Key Vault gespeichert ist (Bring Your Own Key). Die Schutzvorrichtung der transparenten Datenverschlüsselung ist für Azure SQL-Datenbank und Data Warehouse auf Serverebene und für eine verwaltete Azure SQL-Instanz auf Instanzebene festgelegt. In diesem Dokument bezieht sich der Begriff *Server* sowohl auf den Server als auch die Instanz (sofern nicht anders angegeben).

Beim Datenbankstart wird der Verschlüsselungsschlüssel der verschlüsselten Datenbank entschlüsselt und dann für die Entschlüsselung und erneute Verschlüsselung der Datenbankdateien im Prozess der SQL Server-Datenbank-Engine verwendet. Die transparente Datenverschlüsselung führt die E/A-Verschlüsselung und -Entschlüsselung der Daten auf Seitenebene in Echtzeit durch. Jede Seite wird entschlüsselt, wenn sie in den Speicher gelesen wird, und dann verschlüsselt, bevor sie auf den Datenträger geschrieben wird. Eine allgemeine Beschreibung der transparenten Datenverschlüsselung finden Sie unter [Transparente Datenverschlüsselung](https://docs.microsoft.com/sql/relational-databases/security/encryption/transparent-data-encryption).

SQL Server kann bei der Ausführung auf einem virtuellen Azure-Computer auch einen asymmetrischen Schlüssel aus Key Vault verwenden. Die Konfigurationsschritte unterscheiden sich von der Verwendung eines asymmetrischen Schlüssels in SQL-Datenbank und einer verwalteten SQL-Instanz. Weitere Informationen finden Sie unter [Erweiterbare Schlüsselverwaltung mit Azure Key Vault (SQL Server)](https://docs.microsoft.com/sql/relational-databases/security/encryption/extensible-key-management-using-azure-key-vault-sql-server).

## <a name="service-managed-transparent-data-encryption"></a>Von einem Dienst verwaltete transparente Datenverschlüsselung

In Azure ist bei der Standardeinstellung für die transparente Datenverschlüsselung der Verschlüsselungsschlüssel der Datenbank durch ein integriertes Serverzertifikat geschützt. Das integrierte Serverzertifikat ist für jeden Server eindeutig. Wenn sich eine Datenbank in einer Georeplikationsbeziehung befindet, werden die primäre und die sekundäre Geodatenbank vom übergeordneten Serverschlüssel der primären Datenbank geschützt. Sind zwei Datenbanken mit dem gleichen Server verbunden, verwenden sie auch das gleiche integrierte Zertifikat. Microsoft führt für diese Zertifikate nach spätestens 90 Tagen automatisch eine Rotation durch.

Microsoft verschiebt und verwaltet auch die Schlüssel nahtlos, die für die Georeplikation und Wiederherstellung benötigt werden.

> [!IMPORTANT]
> Alle neu erstellten SQL-Datenbanken werden standardmäßig mithilfe der von einem Dienst verwalteten transparenten Datenverschlüsselung verschlüsselt. Datenbanken einer verwalteten Azure SQL-Instanz, vorhandene SQL-Datenbanken, die vor Mai 2017 erstellt wurden, und SQL-Datenbanken, die durch Wiederherstellung, Georeplikation und Datenbankkopie erstellt wurden, sind standardmäßig nicht verschlüsselt.

## <a name="bring-your-own-key"></a>Bring Your Own Key

Durch die Bring Your Own Key-Unterstützung können Sie Ihre Schlüssel für die transparente Datenverschlüsselung verwalten und steuern, wer zu welchem Zeitpunkt auf diese zugreifen kann. Key Vault, das cloudbasierte externe Schlüsselverwaltungssystem von Azure, ist der erste Schlüsselverwaltungsdienst, der in die transparente Datenverschlüsselung mit Bring Your Own Key-Unterstützung integriert ist. Durch die Bring Your Own Key-Unterstützung ist der Verschlüsselungsschlüssel der Datenbank durch einen asymmetrischen Schlüssel geschützt, der in Key Vault gespeichert ist. Der asymmetrische Schlüssel verlässt Key Vault nie. Sobald der Server Berechtigungen für einen Schlüsseltresor besitzt, sendet er grundlegende Anforderungen für Schlüsselvorgänge über Key Vault an den Schlüsseltresor. Der asymmetrische Schlüssel ist auf Serverebene festgelegt und wird von allen *verschlüsselten* Datenbanken unter diesem Server geerbt.

Mithilfe der Bring Your Own Key-Unterstützung steuern Sie die Aufgaben der Schlüsselverwaltung, z.B. Schlüsselrotationen und Schlüsseltresorberechtigungen. Außerdem können Sie Schlüssel löschen sowie die Überwachung und Berichterstellung für alle Verschlüsselungsschlüssel aktivieren. Key Vault bietet eine zentrale Schlüsselverwaltung und verwendet streng überwachte Hardwaresicherheitsmodule. Key Vault unterstützt die Trennung der Verwaltung von Schlüsseln und Daten, um gesetzliche Bestimmungen zu erfüllen. Weitere Informationen zu Key Vault finden Sie in der [Dokumentation zu Key Vault](https://docs.microsoft.com/azure/key-vault/key-vault-secure-your-key-vault).

Weitere Informationen zur transparenten Datenverschlüsselung mit Bring Your Own Key-Unterstützung für Azure SQL-Datenbank, verwaltete SQL-Instanz und Data Warehouse finden Sie unter [Transparente Datenverschlüsselung mit Bring Your Own Key-Unterstützung](transparent-data-encryption-byok-azure-sql.md).

Weitere Informationen zur Verwendung der transparenten Datenverschlüsselung mit Bring Your Own Key-Unterstützung finden Sie in der Anleitung [Aktivieren der transparenten Datenverschlüsselung mithilfe Ihres eigenen Schlüssels aus Key Vault mit PowerShell](transparent-data-encryption-byok-azure-sql-configure.md).

## <a name="move-a-transparent-data-encryption-protected-database"></a>Verschieben einer durch die transparente Datenverschlüsselung gesicherte Datenbank

Für Vorgänge in Azure müssen Datenbanken nicht entschlüsselt werden. Die Einstellungen der transparenten Datenverschlüsselung für die Quelldatenbank oder die primäre Datenbank werden transparent an das Ziel vererbt. Dies gilt für folgende Vorgänge:

- Geografische Wiederherstellung
- Self-Service-Point-in-Time-Wiederherstellung
- Wiederherstellung einer gelöschten Datenbank
- Aktive Georeplikation
- Erstellung einer Datenbankkopie
- Wiederherstellen einer Sicherungsdatei in der verwalteten Azure SQL-Instanz

> [!IMPORTANT]
> Die Verwendung einer manuellen Kopiesicherung einer Datenbank, die über einen vom Dienst verwalteten TDE-Vorgang verschlüsselt wurde, ist auf einer verwalteten Azure SQL-Instanz nicht zulässig, da nicht auf das für die Verschlüsselung genutzte Zertifikat zugegriffen werden kann. Verwenden Sie die Point-in-Time-Wiederherstellung, um diese Art von Datenbank auf eine andere verwaltete Instanz zu verschieben.

Wenn Sie eine Datenbank exportieren, die mit der transparenten Datenverschlüsselung gesichert ist, werden die exportierten Inhalte der Datenbank nicht verschlüsselt. Diese exportierten Inhalte werden in unverschlüsselten BACPAC-Dateien gespeichert. Achten Sie darauf, die BACPAC-Dateien entsprechend zu schützen, und aktivieren Sie die transparente Datenverschlüsselung, nachdem der Import der neuen Datenbank abgeschlossen ist.

Wenn die BACPAC-Datei z.B. von einer lokalen Instanz von SQL Server exportiert wird, erfolgt keine automatische Verschlüsselung des importierten Inhalts der neuen Datenbank. Wenn die BACPAC-Datei auf eine lokale Instanz von SQL Server exportiert wird, erfolgt ebenfalls keine automatische Verschlüsselung der neuen Datenbank.

Eine Ausnahme besteht im Exportieren nach und aus SQL-Datenbank. Die transparente Datenverschlüsselung ist in der neuen Datenbank aktiviert, die BACPAC-Datei ist jedoch nicht verschlüsselt.

## <a name="manage-transparent-data-encryption-in-the-azure-portal"></a>Verwalten der transparenten Datenverschlüsselung im Azure-Portal

Sie müssen eine Verbindung als Azure-Besitzer, -Mitwirkender oder SQL-Sicherheitsmanager herstellen, um die transparente Datenverschlüsselung über das Azure-Portal zu konfigurieren.

Die transparente Datenverschlüsselung wird auf Datenbankebene aktiviert und deaktiviert. Rufen Sie das [Azure-Portal](https://portal.azure.com) auf, und melden Sie sich mit Ihrem Azure-Administrator- oder Mitwirkendenkonto an, um die transparente Datenverschlüsselung für eine Datenbank zu aktivieren. Suchen Sie die Einstellungen für die transparente Datenverschlüsselung in Ihrer Benutzerdatenbank. Standardmäßig wird die von einem Dienst verwaltete transparente Datenverschlüsselung verwendet. Für den Server, der die Datenbank enthält, wird automatisch ein Zertifikat für die transparente Datenverschlüsselung generiert. Bei einer verwalteten Azure SQL-Instanz verwenden Sie T-SQL, um die transparente Datenverschlüsselung für eine Datenbank zu aktivieren oder deaktivieren.

![Von einem Dienst verwaltete transparente Datenverschlüsselung](./media/transparent-data-encryption-azure-sql/service-managed-tde.png)  

Der Hauptschlüssel für die transparente Datenverschlüsselung, der auch als Schutzvorrichtung für die transparente Datenverschlüsselung bezeichnet wird, wird auf Serverebene festgelegt. Öffnen Sie die Einstellungen für die transparente Datenverschlüsselung auf Ihrem Server, um diese mit Bring Your Own Key-Unterstützung zu verwenden und Ihre Datenbank mit einem Schlüssel von Key Vault zu schützen.

![Transparente Datenverschlüsselung mit Bring Your Own Key-Unterstützung](./media/transparent-data-encryption-azure-sql/tde-byok-support.png)

## <a name="manage-transparent-data-encryption-by-using-powershell"></a>Verwalten der transparenten Datenverschlüsselung mithilfe von PowerShell

Sie müssen eine Verbindung als Azure-Besitzer, -Mitwirkender oder SQL-Sicherheitsmanager herstellen, um die transparente Datenverschlüsselung über PowerShell zu konfigurieren.

### <a name="cmdlets-for-azure-sql-database-and-data-warehouse"></a>Cmdlets für Azure SQL-Datenbank und Data Warehouse

Verwenden Sie die folgenden Cmdlets für Azure SQL-Datenbank und Data Warehouse:

| Cmdlet | BESCHREIBUNG |
| --- | --- |
| [Set-AzureRmSqlDatabaseTransparentDataEncryption](https://docs.microsoft.com/powershell/module/azurerm.sql/set-azurermsqldatabasetransparentdataencryption) |Aktiviert oder deaktiviert die transparente Datenverschlüsselung für eine Datenbank|
| [Get-AzureRmSqlDatabaseTransparentDataEncryption](https://docs.microsoft.com/powershell/module/azurerm.sql/get-azurermsqldatabasetransparentdataencryption) |Ruft den Status der transparenten Datenverschlüsselung für eine Datenbank ab |
| [Get-AzureRmSqlDatabaseTransparentDataEncryptionActivity](https://docs.microsoft.com/powershell/module/azurerm.sql/get-azurermsqldatabasetransparentdataencryptionactivity) |Überprüft den Verschlüsselungsfortschritt für eine Datenbank |
| [Add-AzureRmSqlServerKeyVaultKey](https://docs.microsoft.com/powershell/module/azurerm.sql/add-azurermsqlserverkeyvaultkey) |Fügt einer SQL Server-Instanz einen Key Vault-Schlüssel hinzu |
| [Get-AzureRmSqlServerKeyVaultKey](https://docs.microsoft.com/powershell/module/azurerm.sql/get-azurermsqlserverkeyvaultkey) |Ruft die Key Vault-Schlüssel für einen Azure SQL-Datenbankserver ab  |
| [Set-AzureRmSqlServerTransparentDataEncryptionProtector](https://docs.microsoft.com/powershell/module/azurerm.sql/set-azurermsqlservertransparentdataencryptionprotector) |Legt die Schutzvorrichtung der transparenten Datenverschlüsselung für eine SQL Server-Instanz fest |
| [Get-AzureRmSqlServerTransparentDataEncryptionProtector](https://docs.microsoft.com/powershell/module/azurerm.sql/get-azurermsqlservertransparentdataencryptionprotector) |Ruft die Schutzvorrichtung für die transparente Datenverschlüsselung ab |
| [Remove-AzureRmSqlServerKeyVaultKey](https://docs.microsoft.com/powershell/module/azurerm.sql/remove-azurermsqlserverkeyvaultkey) |Entfernt einen Key Vault-Schlüssel aus einer SQL Server-Instanz |
|  | |

> [!IMPORTANT]
> Verwenden Sie bei einer verwalteten Azure SQL-Instanz den T-SQL-Befehl [ALTER DATABASE](https://docs.microsoft.com/sql/t-sql/statements/alter-database-azure-sql-database), um die transparente Datenverschlüsselung auf Datenbankebene zu aktivieren oder deaktivieren, und prüfen Sie das [PowerShell-Beispielskript](transparent-data-encryption-byok-azure-sql-configure.md), um die transparente Datenverschlüsselung auf Instanzebene zu verwalten.

## <a name="manage-transparent-data-encryption-by-using-transact-sql"></a>Verwalten der transparenten Datenverschlüsselung mithilfe von Transact-SQL

Stellen Sie mit einem Konto, das ein Administratorkonto oder ein Mitglied der Rolle **dbmanager** in der Masterdatenbank ist, eine Verbindung mit der Datenbank her.

| Get-Help | BESCHREIBUNG |
| --- | --- |
| [ALTER DATABASE (Azure SQL-Datenbank)](https://docs.microsoft.com/sql/t-sql/statements/alter-database-azure-sql-database) | Mit SET ENCRYPTION ON/OFF wird eine Datenbank verschlüsselt oder entschlüsselt. |
| [sys.dm_database_encryption_keys](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-database-encryption-keys-transact-sql) |Gibt Informationen über den Verschlüsselungsstatus einer Datenbank und die ihr zugeordneten Verschlüsselungsschlüssel zurück. |
| [sys.dm_pdw_nodes_database_encryption_keys](https://docs.microsoft.com/sql/relational-databases/system-dynamic-management-views/sys-dm-pdw-nodes-database-encryption-keys-transact-sql) |Gibt Informationen über den Verschlüsselungsstatus jedes Data Warehouse-Knotens und die ihm zugeordneten Verschlüsselungsschlüssel der Datenbank zurück. |
|  | |

Sie können die Schutzvorrichtung der transparenten Datenverschlüsselung mithilfe von Transact-SQL nicht durch einen Schlüssel von Key Vault ersetzen. Verwenden Sie PowerShell oder das Azure-Portal.

## <a name="manage-transparent-data-encryption-by-using-the-rest-api"></a>Verwalten der transparenten Datenverschlüsselung mithilfe der REST-API

Sie müssen eine Verbindung als Azure-Besitzer, -Mitwirkender oder SQL-Sicherheitsmanager herstellen, um die transparente Datenverschlüsselung über die REST-API zu konfigurieren.
Verwenden Sie den folgenden Satz von Befehlen für Azure SQL-Datenbank und Data Warehouse:

| Get-Help | BESCHREIBUNG |
| --- | --- |
|[Server erstellen oder aktualisieren](https://docs.microsoft.com/rest/api/sql/servers/createorupdate)|Fügt einer SQL Server-Instanz, die für den Zugriff auf Key Vault verwendet wird, Azure Active Directory-Identität hinzu.|
|[Serverschlüssel erstellen oder aktualisieren](https://docs.microsoft.com/rest/api/sql/serverkeys/createorupdate)|Fügt einer SQL Server-Instanz einen Key Vault-Schlüssel hinzu|
|[Serverschlüssel entfernen](https://docs.microsoft.com/rest/api/sql/serverkeys/delete)|Entfernt einen Key Vault-Schlüssel aus einer SQL Server-Instanz|
|[Serverschlüssel abrufen](https://docs.microsoft.com/rest/api/sql/serverkeys/get)|Ruft einen bestimmten Key Vault-Schlüssel aus einer SQL Server-Instanz ab|
|[Serverschlüssel nach Server auflisten](https://docs.microsoft.com/rest/api/sql/serverkeys/listbyserver)|Ruft die Key Vault-Schlüssel für eine SQL Server-Instanz ab |
|[Verschlüsselungsschutzvorrichtung erstellen oder aktualisieren](https://docs.microsoft.com/rest/api/sql/encryptionprotectors/createorupdate)|Legt die Schutzvorrichtung der transparenten Datenverschlüsselung für eine SQL Server-Instanz fest|
|[Verschlüsselungsschutzvorrichtung abrufen](https://docs.microsoft.com/rest/api/sql/encryptionprotectors/get)|Ruft Schutzvorrichtung der transparenten Datenverschlüsselung für eine SQL Server-Instanz ab|
|[Verschlüsselungsschutzvorrichtungen nach Server auflisten](https://docs.microsoft.com/rest/api/sql/encryptionprotectors/listbyserver)|Ruft die Schutzvorrichtungen der transparenten Datenverschlüsselung für eine SQL Server-Instanz ab |
|[Transparent Data Encryption-Konfiguration erstellen oder aktualisieren](https://docs.microsoft.com/rest/api/sql/transparentdataencryptions/createorupdate)|Aktiviert oder deaktiviert die transparente Datenverschlüsselung für eine Datenbank|
|[Transparent Data Encryption-Konfiguration abrufen](https://docs.microsoft.com/rest/api/sql/transparentdataencryptions/get)|Ruft die Konfiguration der transparenten Datenverschlüsselung für eine Datenbank ab|
|[Ergebnisse der Transparent Data Encryption-Konfiguration auflisten](https://docs.microsoft.com/rest/api/sql/transparentdataencryptionactivities/listbyconfiguration)|Ruft das Verschlüsselungsergebnis für eine Datenbank ab|

## <a name="next-steps"></a>Nächste Schritte

- Eine allgemeine Beschreibung der transparenten Datenverschlüsselung finden Sie unter [Transparente Datenverschlüsselung](https://docs.microsoft.com/sql/relational-databases/security/encryption/transparent-data-encryption).
- Weitere Informationen zur transparenten Datenverschlüsselung mit Bring Your Own Key-Unterstützung für Azure SQL-Datenbank, verwaltete Azure SQL-Instanz und Data Warehouse finden Sie unter [Transparente Datenverschlüsselung mit Bring Your Own Key-Unterstützung](transparent-data-encryption-byok-azure-sql.md).
- Weitere Informationen zur Verwendung der transparenten Datenverschlüsselung mit Bring Your Own Key-Unterstützung finden Sie in der Anleitung [Aktivieren der transparenten Datenverschlüsselung mithilfe Ihres eigenen Schlüssels aus Key Vault mit PowerShell](transparent-data-encryption-byok-azure-sql-configure.md).
- Weitere Informationen zu Key Vault finden Sie in der [Dokumentation zu Key Vault](https://docs.microsoft.com/azure/key-vault/key-vault-secure-your-key-vault).
