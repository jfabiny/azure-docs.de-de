---
title: Erste Schritte mit den Azure Stack-Speicherentwicklungstools | Microsoft-Dokumentation
description: Anleitung für die ersten Schritte mit Azure Stack-Speicher-Entwicklungstools
services: azure-stack
author: mattbriggs
ms.author: mabrigg
ms.date: 12/03/2018
ms.topic: get-started-article
ms.service: azure-stack
manager: femila
ms.reviewer: xiaofmao
ms.lastreviewed: 12/03/2018
ms.openlocfilehash: 857e12664defb1fc0106dd0d3012b77a89f826c2
ms.sourcegitcommit: 5978d82c619762ac05b19668379a37a40ba5755b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/31/2019
ms.locfileid: "55495104"
---
# <a name="get-started-with-azure-stack-storage-development-tools"></a>Erste Schritte mit den Azure Stack-Speicherentwicklungstools

*Anwendungsbereich: Integrierte Azure Stack-Systeme und Azure Stack Development Kit*

Microsoft Azure Stack bietet eine Reihe von Speicherdiensten einschließlich Blob-, Tabellen- und Warteschlangenspeicher.

Nutzen Sie diesen Artikel als Leitfaden für die ersten Schritte mit den Azure Stack-Speicherentwicklungstools. Ausführlichere Informationen und Beispielcode finden Sie in den entsprechenden Azure-Speichertutorials.

> [!NOTE]
> Es gibt bestimmte Unterschiede zwischen Azure Stack-Speicher und Azure-Speicher sowie besondere Anforderungen für die jeweilige Plattform. Beispielsweise gelten bestimmte Clientbibliotheken- und Endpunktsuffix-Anforderungen für Azure Stack. Weitere Informationen finden Sie unter [Azure Stack-Speicher: Unterschiede und Überlegungen](azure-stack-acs-differences.md).

## <a name="azure-client-libraries"></a>Azure-Clientbibliotheken

Bei den Speicherclientbibliotheken müssen Sie auf die Version achten, die mit der REST-API kompatibel ist. Sie müssen auch den Azure Stack-Endpunkt in Ihrem Code angeben.

### <a name="1811-update-or-newer-versions"></a>Update 1811 oder neuere Versionen

| Clientbibliothek | Von Azure Stack unterstützte Version | Link | Endpunktspezifikation |
|----------------|-------------------------------|-----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------|
| .NET | 8.7.0 | NuGet-Paket:<br>https://www.nuget.org/packages/WindowsAzure.Storage/8.7.0<br> <br>GitHub-Release:<br>https://github.com/Azure/azure-storage-net/releases/tag/v8.7.0 | app.config-Datei |
| Java | 6.1.0 | Maven-Paket:<br>http://mvnrepository.com/artifact/com.microsoft.azure/azure-storage/6.1.0<br> <br>GitHub-Release:<br>https://github.com/Azure/azure-storage-java/releases/tag/v6.1.0 | Verbindungszeichenfolgen-Setup |
| Node.js | 2.7.0 | NPM-Link:<br>https://www.npmjs.com/package/azure-storage<br>(Ausführung: `npm install azure-storage@2.7.0`)<br> <br>GitHub-Release:<br>https://github.com/Azure/azure-storage-node/releases/tag/v2.7.0 | Dienstinstanzdeklaration |
| C++ | 3.1.0 | NuGet-Paket:<br>https://www.nuget.org/packages/wastorage.v140/3.1.0<br> <br>GitHub-Release:<br>https://github.com/Azure/azure-storage-cpp/releases/tag/v3.1.0 | Verbindungszeichenfolgen-Setup |
| PHP | 1.0.0 | GitHub-Release:<br>Allgemein: https://github.com/Azure/azure-storage-php/releases/tag/v1.0.0-common<br>Blob: https://github.com/Azure/azure-storage-php/releases/tag/v1.0.0-blob<br>Queue:<br>https://github.com/Azure/azure-storage-php/releases/tag/v1.0.0-queue<br>Table: https://github.com/Azure/azure-storage-php/releases/tag/v1.0.0-table<br> <br>Installation per Composer (siehe [Details weiter unten](#install-php-client-via-composer---current).) | Verbindungszeichenfolgen-Setup |
| Python | 1.0.0 | GitHub-Release:<br>Allgemein:<br>https://github.com/Azure/azure-storage-python/releases/tag/v1.0.0-common<br>Blob:<br>https://github.com/Azure/azure-storage-python/releases/tag/v1.0.0-blob<br>Queue:<br>https://github.com/Azure/azure-storage-python/releases/tag/v1.0.0-queue | Dienstinstanzdeklaration |
| Ruby | 1.0.1 | RubyGems-Paket:<br>Allgemein:<br>https://rubygems.org/gems/azure-storage-common/versions/1.0.1<br>Blob: https://rubygems.org/gems/azure-storage-blob/versions/1.0.1<br>Queue: https://rubygems.org/gems/azure-storage-queue/versions/1.0.1<br>Table: https://rubygems.org/gems/azure-storage-table/versions/1.0.1<br> <br>GitHub-Release:<br>Allgemein: https://github.com/Azure/azure-storage-ruby/releases/tag/v1.0.1-common<br>Blob: https://github.com/Azure/azure-storage-ruby/releases/tag/v1.0.1-blob<br>Queue: https://github.com/Azure/azure-storage-ruby/releases/tag/v1.0.1-queue<br>Table: https://github.com/Azure/azure-storage-ruby/releases/tag/v1.0.1-table | Verbindungszeichenfolgen-Setup |

#### <a name="install-php-client-via-composer---current"></a>Installation des PHP-Clients per Composer – Aktuell

Installation über Composer: (Verwenden Sie das Blob als Beispiel).

1. Erstellen Sie eine Datei mit dem Namen **composer.json** im Stammverzeichnis des Projekts mit folgendem Code:

    ```json
    {
      "require": {
      "Microsoft/azure-storage-blob":"1.2.0"
      }
    }
    ```

2. Laden Sie [composer.phar](http://getcomposer.org/composer.phar) in das Stammverzeichnis des Projekts herunter.
3. Führen Sie `php composer.phar install` aus.

### <a name="previous-versions-1802-to-1809-update"></a>Vorherige Versionen (1802 bis Update 1809)

|Clientbibliothek|Von Azure Stack unterstützte Version|Link|Endpunktspezifikation|
|---------|---------|---------|---------|
|.NET     |6.2.0|NuGet-Paket:<br>[https://www.nuget.org/packages/WindowsAzure.Storage/6.2.0](https://www.nuget.org/packages/WindowsAzure.Storage/6.2.0)<br><br>GitHub-Release:<br>[https://github.com/Azure/azure-storage-net/releases/tag/v6.2.1](https://github.com/Azure/azure-storage-net/releases/tag/v6.2.1)|app.config-Datei|
|Java|4.1.0|Maven-Paket:<br>[http://mvnrepository.com/artifact/com.microsoft.azure/azure-storage/4.1.0](http://mvnrepository.com/artifact/com.microsoft.azure/azure-storage/4.1.0)<br><br>GitHub-Release:<br> [https://github.com/Azure/azure-storage-java/releases/tag/v4.1.0](https://github.com/Azure/azure-storage-java/releases/tag/v4.1.0)|Verbindungszeichenfolgen-Setup|
|Node.js     |1.1.0|NPM-Link:<br>[https://www.npmjs.com/package/azure-storage](https://www.npmjs.com/package/azure-storage)<br>(Ausführen: `npm install azure-storage@1.1.0)`<br><br>GitHub-Release:<br>[https://github.com/Azure/azure-storage-node/releases/tag/1.1.0](https://github.com/Azure/azure-storage-node/releases/tag/1.1.0)|Dienstinstanzdeklaration||C++|2.4.0|NuGet-Paket:<br>[https://www.nuget.org/packages/wastorage.v140/2.4.0](https://www.nuget.org/packages/wastorage.v140/2.4.0)<br><br>GitHub-Release:<br>[https://github.com/Azure/azure-storage-cpp/releases/tag/v2.4.0](https://github.com/Azure/azure-storage-cpp/releases/tag/v2.4.0)|Verbindungszeichenfolgen-Setup|
|C++|2.4.0|NuGet-Paket:<br>[https://www.nuget.org/packages/wastorage.v140/2.4.0](https://www.nuget.org/packages/wastorage.v140/2.4.0)<br><br>GitHub-Release:<br>[https://github.com/Azure/azure-storage-cpp/releases/tag/v2.4.0](https://github.com/Azure/azure-storage-cpp/releases/tag/v2.4.0)|Verbindungszeichenfolgen-Setup|
|PHP|0.15.0|GitHub-Release:<br>[https://github.com/Azure/azure-storage-php/releases/tag/v0.15.0](https://github.com/Azure/azure-storage-php/releases/tag/v0.15.0)<br><br>Installation über Composer (Details siehe unten)|Verbindungszeichenfolgen-Setup|
|Python     |0.30.0|PIP-Paket:<br> [https://pypi.python.org/pypi/azure-storage/0.30.0](https://pypi.python.org/pypi/azure-storage/0.30.0)<br>(Ausführen: `pip install -v azure-storage==0.30.0)`<br><br>GitHub-Release:<br> [https://github.com/Azure/azure-storage-python/releases/tag/v0.30.0](https://github.com/Azure/azure-storage-python/releases/tag/v0.30.0)|Dienstinstanzdeklaration|
|Ruby|0.12.1<br>Vorschau|RubyGems-Paket:<br> [https://rubygems.org/gems/azure-storage/versions/0.12.1.preview](https://rubygems.org/gems/azure-storage/versions/0.12.1.preview)<br><br>GitHub-Release:<br> [https://github.com/Azure/azure-storage-ruby/releases/tag/v0.12.1](https://github.com/Azure/azure-storage-ruby/releases/tag/v0.12.1)|Verbindungszeichenfolgen-Setup|

#### <a name="install-php-client-via-composer---previous"></a>Installation des PHP-Clients per Composer – Vorherige

Installation per Composer: (Blob als Beispiel verwenden).

1. Erstellen Sie eine Datei mit dem Namen **composer.json** im Stammverzeichnis des Projekts mit folgendem Code:

  ```json
    {
      "require": {
      "Microsoft/azure-storage-blob":"1.0.0"
      }
    }
  ```

2. Laden Sie [composer.phar](http://getcomposer.org/composer.phar) in das Stammverzeichnis des Projekts herunter.
3. Führen Sie `php composer.phar install` aus.

## <a name="endpoint-declaration"></a>Endpunktdeklaration

Ein Azure Stack-Endpunkt besteht aus zwei Teilen: dem Namen einer Region und der Azure Stack-Domäne.
Im Azure Stack Development Kit ist der Standardendpunkt **local.azurestack.external**.
Wenn Sie sich über Ihren Endpunkt nicht sicher sind, wenden Sie sich an den Cloudadministrator.

## <a name="examples"></a>Beispiele

### <a name="net"></a>.NET

Für Azure Stack ist das Endpunktsuffix in der Datei „app.config“ angegeben:

```xml
<add key="StorageConnectionString"
value="DefaultEndpointsProtocol=https;AccountName=myaccount;AccountKey=mykey;
EndpointSuffix=local.azurestack.external;" />
```

### <a name="java"></a>Java

Für Azure Stack ist das Endpunktsuffix im Setup der Verbindungszeichenfolge angegeben:

```java
public static final String storageConnectionString =
    "DefaultEndpointsProtocol=http;" +
    "AccountName=your_storage_account;" +
    "AccountKey=your_storage_account_key;" +
    "EndpointSuffix=local.azurestack.external";
```

### <a name="nodejs"></a>Node.js

Für Azure Stack ist das Endpunktsuffix in der Deklarationsinstanz angegeben:

```javascript
var blobSvc = azure.createBlobService('myaccount', 'mykey',
'myaccount.blob.local.azurestack.external');
```

### <a name="c"></a>C++

Für Azure Stack ist das Endpunktsuffix im Setup der Verbindungszeichenfolge angegeben:

```cpp
const utility::string_t storage_connection_string(U("DefaultEndpointsProtocol=https;
AccountName=your_storage_account;
AccountKey=your_storage_account_key;
EndpointSuffix=local.azurestack.external"));
```

### <a name="php"></a>PHP

Für Azure Stack ist das Endpunktsuffix im Setup der Verbindungszeichenfolge angegeben:

```php
$connectionString = 'BlobEndpoint=http://<storage account name>.blob.local.azurestack.external/;
QueueEndpoint=http:// <storage account name>.queue.local.azurestack.external/;
TableEndpoint=http:// <storage account name>.table.local.azurestack.external/;
AccountName=<storage account name>;AccountKey=<storage account key>'
```

### <a name="python"></a>Python

Für Azure Stack ist das Endpunktsuffix in der Deklarationsinstanz angegeben:

```python
block_blob_service = BlockBlobService(account_name='myaccount',
account_key='mykey',
endpoint_suffix='local.azurestack.external')
```

### <a name="ruby"></a>Ruby

Für Azure Stack ist das Endpunktsuffix im Setup der Verbindungszeichenfolge angegeben:

```ruby
set
AZURE_STORAGE_CONNECTION_STRING=DefaultEndpointsProtocol=https;
AccountName=myaccount;
AccountKey=mykey;
EndpointSuffix=local.azurestack.external
```

## <a name="blob-storage"></a>Blob Storage

Die folgenden Tutorials zu Azure Blob Storage gelten für Azure Stack. Beachten Sie die im vorherigen Abschnitt [Beispiele](#examples) beschriebene bestimmte Endpunktsuffix-Voraussetzung für Azure Stack.

* [Erste Schritte mit Azure Blob Storage mit .NET](../../storage/blobs/storage-dotnet-how-to-use-blobs.md)
* [Gewusst wie: Verwenden von Blob Storage mit Java](../../storage/blobs/storage-java-how-to-use-blob-storage.md)
* [Gewusst wie: Verwenden von Blob Storage mit Node.js](../../storage/blobs/storage-nodejs-how-to-use-blob-storage.md)
* [Verwenden des BLOB-Speichers mit C++](../../storage/blobs/storage-c-plus-plus-how-to-use-blobs.md)
* [Gewusst wie: Verwenden von Blob Storage mit PHP](../../storage/blobs/storage-php-how-to-use-blobs.md)
* [Verwenden von Azure Blob Storage mit Python](../../storage/blobs/storage-python-how-to-use-blob-storage.md)
* [Gewusst wie: Verwenden von Blob Storage mit Ruby](../../storage/blobs/storage-ruby-how-to-use-blob-storage.md)

## <a name="queue-storage"></a>Queue Storage

Die folgenden Tutorials zu Azure Queue Storage gelten für Azure Stack. Beachten Sie die im vorherigen Abschnitt [Beispiele](#examples) beschriebene bestimmte Endpunktsuffix-Voraussetzung für Azure Stack.

* [Erste Schritte mit Azure Queue Storage mit .NET](../../storage/queues/storage-dotnet-how-to-use-queues.md)
* [Gewusst wie: Verwenden von Queue Storage mit Java](../../storage/queues/storage-java-how-to-use-queue-storage.md)
* [Gewusst wie: Verwenden von Queue Storage mit Node.js](../../storage/queues/storage-nodejs-how-to-use-queues.md)
* [Verwenden des Warteschlangenspeichers mit C++](../../storage/queues/storage-c-plus-plus-how-to-use-queues.md)
* [Gewusst wie: Verwenden von Queue Storage mit PHP](../../storage/queues/storage-php-how-to-use-queues.md)
* [Gewusst wie: Verwenden von Queue Storage mit Python](../../storage/queues/storage-python-how-to-use-queue-storage.md)
* [Gewusst wie: Verwenden von Queue Storage mit Ruby](../../storage/queues/storage-ruby-how-to-use-queue-storage.md)

## <a name="table-storage"></a>Table Storage

Die folgenden Tutorials zu Azure Table Storage gelten für Azure Stack. Beachten Sie die im vorherigen Abschnitt [Beispiele](#examples) beschriebene bestimmte Endpunktsuffix-Voraussetzung für Azure Stack.

* [Erste Schritte mit Azure Table Storage mit .NET](../../cosmos-db/table-storage-how-to-use-dotnet.md)
* [Gewusst wie: Verwenden von Table Storage mit Java](../../cosmos-db/table-storage-how-to-use-java.md)
* [Verwenden des Azure-Tabellenspeichers mit Node.js](../../cosmos-db/table-storage-how-to-use-nodejs.md)
* [Verwenden des Tabellenspeichers mit C++](../../cosmos-db/table-storage-how-to-use-c-plus.md)
* [Gewusst wie: Verwenden von Table Storage mit PHP](../../cosmos-db/table-storage-how-to-use-php.md)
* [Verwenden von Table Storage in Python](../../cosmos-db/table-storage-how-to-use-python.md)
* [Gewusst wie: Verwenden von Table Storage mit Ruby](../../cosmos-db/table-storage-how-to-use-ruby.md)

## <a name="next-steps"></a>Nächste Schritte

* [Einführung in Azure Storage](../../storage/common/storage-introduction.md)
