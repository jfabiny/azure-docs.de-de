---
title: Verwalten von Instanzen in Durable Functions – Azure
description: Es wird beschrieben, wie Instanzen in der Erweiterung Durable Functions für Azure Functions verwaltet werden.
services: functions
author: cgillum
manager: jeconnoc
keywords: ''
ms.service: azure-functions
ms.devlang: multiple
ms.topic: conceptual
ms.date: 12/07/2018
ms.author: azfuncdf
ms.openlocfilehash: dba5518df34fa4fb6c403a72aa40405bcde5c426
ms.sourcegitcommit: eecd816953c55df1671ffcf716cf975ba1b12e6b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/28/2019
ms.locfileid: "55104676"
---
# <a name="manage-instances-in-durable-functions-in-azure"></a>Verwalten von Instanzen in Durable Functions in Azure

In [Durable Functions](durable-functions-overview.md) können Orchestrierungsinstanzen gestartet, beendet und abgefragt sowie Benachrichtigungsereignisse gesendet werden. Die gesamte Instanzenverwaltung erfolgt mithilfe der [Orchestrierungsclientbindung](durable-functions-bindings.md). In diesem Artikel wird jeder Instanzenverwaltungsvorgang im Detail erläutert.

## <a name="starting-instances"></a>Starten von Instanzen

Die [StartNewAsync](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClient.html#Microsoft_Azure_WebJobs_DurableOrchestrationClient_StartNewAsync_)-Methode der [DurableOrchestrationClient](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClient.html)-Klasse (.NET) oder die `startNew`-Methode der `DurableOrchestrationClient`-Klasse (JavaScript) startet eine neue Instanz einer Orchestratorfunktion. Instanzen dieser Klasse können mithilfe der `orchestrationClient`-Bindung abgerufen werden. Intern stellt diese Methode eine Nachricht in die Steuerwarteschlange, die dann den Start einer Funktion mit dem angegebenen Namen auslöst, der die `orchestrationTrigger`-Bindung verwendet.

Dieser asynchrone Vorgang wird abgeschlossen, wenn der Orchestrierungsprozess erfolgreich geplant wurde. Der Orchestrierungsprozess sollte innerhalb von 30 Sekunden gestartet werden. Wenn es länger dauert, wird eine `TimeoutException` ausgelöst.

> [!WARNING]
> Wenn Sie lokal in JavaScript entwickeln, müssen Sie die Umgebungsvariable `WEBSITE_HOSTNAME` auf `localhost:<port>` festlegen, z. B. `localhost:7071`, um Methoden mit `DurableOrchestrationClient` zu verwenden. Weitere Informationen zu dieser Anforderung finden Sie in der [Beschreibung des Problems auf GitHub](https://github.com/Azure/azure-functions-durable-js/issues/28).

### <a name="net"></a>.NET

Die Parameter für [StartNewAsync](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClient.html#Microsoft_Azure_WebJobs_DurableOrchestrationClient_StartNewAsync_) lauten wie folgt:

* **Name**: Der Name der zu planenden Orchestratorfunktion.
* **Eingabe**: Alle JSON-serialisierbaren Daten, die als Eingabe an die Orchestratorfunktion übergeben werden sollen.
* **InstanceId**: (Optional) Die eindeutige ID der Instanz. Wenn nicht angegeben, wird eine zufällige Instanz-ID generiert.

Hier ist ein einfaches Beispiel für C#:

```csharp
[FunctionName("HelloWorldManualStart")]
public static async Task Run(
    [ManualTrigger] string input,
    [OrchestrationClient] DurableOrchestrationClient starter,
    ILogger log)
{
    string instanceId = await starter.StartNewAsync("HelloWorld", input);
    log.LogInformation($"Started orchestration with ID = '{instanceId}'.");
}
```

### <a name="javascript-functions-2x-only"></a>JavaScript (nur Functions 2.x)

Die Parameter für `startNew` lauten wie folgt:

* **Name**: Der Name der zu planenden Orchestratorfunktion.
* **InstanceId**: (Optional) Die eindeutige ID der Instanz. Wenn nicht angegeben, wird eine zufällige Instanz-ID generiert.
* **Eingabe**: (Optional) Alle JSON-serialisierbaren Daten, die als Eingabe an die Orchestratorfunktion übergeben werden sollen.

Hier sehen Sie ein einfaches JavaScript-Beispiel:

```javascript
const df = require("durable-functions");

module.exports = async function(context, input) {
    const client = df.getClient(context);

    const instanceId = await client.startNew("HelloWorld", undefined, input);
    context.log(`Started orchestration with ID = ${instanceId}.`);
};
```

> [!NOTE]
> Verwenden Sie einen zufälligen Bezeichner für die Instanz-ID. Dies gewährleistet eine gleichmäßige Lastenverteilung, wenn Orchestratorfunktionen mehrere virtuelle Computer übergreifend skaliert werden. Wenn die ID aus einer externen Quelle stammen muss oder bei der Implementierung des [Singleton-Orchestrator](durable-functions-singletons.md)-Musters sollten nicht zufällige Instanz-IDs verwendet werden.

### <a name="using-core-tools"></a>Verwenden von Core Tools

Es ist auch möglich, eine Instanz direkt über den Befehl `durable start-new` von [Azure Functions Core Tools](../functions-run-local.md) zu starten. Hierfür werden die folgenden Parameter verwendet:

* **`function-name` (erforderlich)**: Der Name der zu startenden Funktion.
* **`input` (optional)**: Die Eingabe für die Funktion, entweder inline oder über eine JSON-Datei. Bei Dateien muss dem Pfad zur Datei das Präfix `@` vorangestellt werden, z.B. `@path/to/file.json`.
* **`id` (optional)**: Die ID der Orchestrierungsinstanz. Wenn diese nicht angegeben ist, wird eine zufällige GUID generiert.
* **`connection-string-setting` (optional)**: Der Name der Anwendungseinstellung mit der zu verwendenden Speicherverbindungszeichenfolge. Der Standardwert ist AzureWebJobsStorage.
* **`task-hub-name` (optional)**: Der Name des zu verwendenden Durable-Aufgabenhubs. Der Standardwert ist DurableFunctionsHub. Dieser Wert kann auch in [host.json](durable-functions-bindings.md#host-json) über durableTask:HubName festgelegt werden.

> [!NOTE]
> Bei Core Tools-Befehlen wird davon ausgegangen, dass sie im Stammverzeichnis einer Funktions-App ausgeführt werden. Wenn `connection-string-setting` und `task-hub-name` explizit angegeben werden, können die Befehle in einem beliebigen Verzeichnis ausgeführt werden. Diese Befehle können zwar ohne ausgeführten Funktions-App-Host ausgeführt werden, einige Auswirkungen können jedoch nur beobachtet werden, wenn der Host ausgeführt wird. Beispielsweise reiht der Befehl `start-new` eine Startmeldung in die Warteschlange für den Ziel-Aufgabenhub ein, die Orchestrierung wird jedoch nicht ausgeführt, bis ein Funktions-App-Hostprozess ausgeführt wird, der die Nachricht verarbeiten kann.

Der folgende Befehl startet die Funktion HelloWorld und übergibt dieser den Inhalt der Datei „counter-data.json“:

```bash
func durable start-new --function-name HelloWorld --input @counter-data.json --task-hub-name TestTaskHub
```

## <a name="querying-instances"></a>Abfragen von Instanzen

Die [GetStatusAsync](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClient.html#Microsoft_Azure_WebJobs_DurableOrchestrationClient_GetStatusAsync_)-Methode der [DurableOrchestrationClient](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClient.html)-Klasse (.NET) oder `getStatus`-Methode der `DurableOrchestrationClient`-Klasse (JavaScript) fragt den Status einer Orchestrierungsinstanz ab.

Die Methode akzeptiert die Parameter `instanceId` (erforderlich), `showHistory` (optional), `showHistoryOutput` (optional) und `showInput` (optional, nur .NET).

* **`showHistory`**: Bei Festlegung auf `true` enthält die Antwort den Ausführungsverlauf.
* **`showHistoryOutput`**: Bei Festlegung auf `true` enthält der Ausführungsverlauf Aktivitätsausgaben.
* **`showInput`**: Bei Festlegung auf `false` enthält die Antwort nicht die Eingabe der Funktion. Standardwert: `true`. (Nur .NET)

Die Methode gibt ein JSON-Objekt mit den folgenden Eigenschaften zurück:

* **Name**: Der Name der Orchestratorfunktion.
* **InstanceId**: Die Instanz-ID der Orchestrierung (muss mit der Eingabe `instanceId` identisch sein).
* **CreatedTime**: Der Zeitpunkt, zu dem die Ausführung der Orchestratorfunktion gestartet wurde.
* **LastUpdatedTime**: Der Zeitpunkt, zu dem der letzte Prüfpunkt für die Orchestrierung erstellt wurde.
* **Eingabe**: Die Eingabe der Funktion als JSON-Wert. Dieses Feld wird nicht aufgefüllt, wenn `showInput` FALSE ist.
* **CustomStatus**: Der benutzerdefinierter Orchestrierungsstatus im JSON-Format.
* **Ausgabe**: Die Ausgabe der Funktion als JSON-Wert (wenn die Funktion abgeschlossen wurde). Wenn ein Fehler bei der Orchestratorfunktion auftritt, enthält diese Eigenschaft die Fehlerdetails. Wenn die Orchestratorfunktion beendet wurde, enthält diese Eigenschaft den angegebenen Grund für die Beendigung (sofern vorhanden).
* **RuntimeStatus**: Einer der folgenden Werte:
  * **Pending**: Die Instanz wurde geplant, ihre Ausführung aber noch nicht gestartet.
  * **Running**: Die Instanz wurde gestartet.
  * **Completed**: Die Instanz wurde normal abgeschlossen.
  * **ContinuedAsNew**: Die Instanz hat sich selbst mit einem neuen Verlauf neu gestartet. Dies ist ein vorübergehender Status.
  * **Failed**: Bei der Instanz ist ein Fehler aufgetreten.
  * **Terminated**: Die Instanz wurde plötzlich beendet.
* **History**: Der Ausführungsverlauf der Orchestrierung. Dieses Feld wird nur gefüllt, wenn `showHistory` auf `true` festgelegt ist.

Diese Methode gibt `null` zurück, wenn die Instanz nicht vorhanden ist, oder ihre Ausführung noch nicht gestartet wurde.

### <a name="c"></a>C#

```csharp
[FunctionName("GetStatus")]
public static async Task Run(
    [OrchestrationClient] DurableOrchestrationClient client,
    [ManualTrigger] string instanceId)
{
    var status = await client.GetStatusAsync(instanceId);
    // do something based on the current status.
}
```

### <a name="javascript-functions-2x-only"></a>JavaScript (nur Functions 2.x)

```javascript
const df = require("durable-functions");

module.exports = async function(context, instanceId) {
    const client = df.getClient(context);

    const status = await client.getStatus(instanceId);
    // do something based on the current status.
}
```

### <a name="using-core-tools"></a>Verwenden von Core Tools

Es ist auch möglich, den Status der Orchestrierung direkt über den Befehl `durable get-runtime-status` von [Azure Functions Core Tools](../functions-run-local.md) abzurufen. Hierfür werden die folgenden Parameter verwendet:

* **`id` (erforderlich)**: Die ID der Orchestrierungsinstanz.
* **`show-input` (optional)**: Bei Festlegung auf `true` enthält die Antwort die Eingabe der Funktion. Standardwert: `false`.
* **`show-output` (optional)**: Bei Festlegung auf `true` enthält die Antwort die Ausgabe der Funktion. Standardwert: `false`.
* **`connection-string-setting` (optional)**: Der Name der Anwendungseinstellung mit der zu verwendenden Speicherverbindungszeichenfolge. Der Standardwert ist AzureWebJobsStorage.
* **`task-hub-name` (optional)**: Der Name des zu verwendenden Durable-Aufgabenhubs. Der Standardwert ist DurableFunctionsHub. Dieser Wert kann auch in [host.json](durable-functions-bindings.md#host-json) über durableTask:HubName festgelegt werden.

Der folgende Befehl ruft den Status (einschließlich Ein- und Ausgaben) einer Instanz mit der Orchestrierungsinstanz-ID 0ab8c55a66644d68a3a8b220b12d209c ab. Dabei wird vorausgesetzt, dass der Befehl `func` im Stammverzeichnis der Funktions-App ausgeführt wird:

```bash
func durable get-runtime-status --id 0ab8c55a66644d68a3a8b220b12d209c --show-input true --show-output true
```

Der Befehl `durable get-history` kann zum Abrufen des Ausführungsverlaufs einer Orchestrierungsinstanz verwendet werden. Hierfür werden die folgenden Parameter verwendet:

* **`id` (erforderlich)**: Die ID der Orchestrierungsinstanz.
* **`connection-string-setting` (optional)**: Der Name der Anwendungseinstellung mit der zu verwendenden Speicherverbindungszeichenfolge. Der Standardwert ist AzureWebJobsStorage.
* **`task-hub-name` (optional)**: Der Name des zu verwendenden Durable-Aufgabenhubs. Der Standardwert ist DurableFunctionsHub. Der Wert kann auch in „host.json“ über durableTask:HubName festgelegt werden.

```bash
func durable get-history --id 0ab8c55a66644d68a3a8b220b12d209c
```

## <a name="querying-all-instances"></a>Abfragen aller Instanzen

Sie können die `GetStatusAsync`-Methode (.NET) oder `getStatusAll`-Methode (JavaScript) verwenden, um die Status aller Orchestrierungsinstanzen abzufragen. In .NET können Sie ein `CancellationToken`-Objekt übergeben, falls Sie die Methode abbrechen möchten. Die Methode gibt Objekte mit denselben Eigenschaften wie die `GetStatusAsync`-Methode mit Parametern zurück.

### <a name="c"></a>C#

```csharp
[FunctionName("GetAllStatus")]
public static async Task Run(
    [HttpTrigger(AuthorizationLevel.Anonymous, "get", "post")]HttpRequestMessage req,
    [OrchestrationClient] DurableOrchestrationClient client,
    ILogger log)
{
    IList<DurableOrchestrationStatus> instances = await client.GetStatusAsync(); // You can pass CancellationToken as a parameter.
    foreach (var instance in instances)
    {
        log.LogInformation(JsonConvert.SerializeObject(instance));
    };
}
```

### <a name="javascript-functions-2x-only"></a>JavaScript (nur Functions 2.x)

```javascript
const df = require("durable-functions");

module.exports = async function(context, req) {
    const client = df.getClient(context);

    const instances = await client.getStatusAll();
    instances.forEach((instance) => {
        context.log(JSON.stringify(instance));
    });
};
```

### <a name="using-core-tools"></a>Verwenden von Core Tools

Es ist auch möglich, eine Abfrage direkt über den Befehl `durable get-instances` von [Azure Functions Core Tools](../functions-run-local.md) zu starten. Hierfür werden die folgenden Parameter verwendet:

* **`top` (optional)**: Dieser Befehl unterstützt Paging. Dieser Parameter entspricht der Anzahl der pro Anforderung abgerufenen Instanzen. Der Standardwert ist 10.
* **`continuation-token` (optional)**: Ein Token, das angibt, welche Seite oder welcher Abschnitt der Instanzen abgerufen werden soll. Jede Ausführung von `get-instances` gibt ein Token an den nächsten Satz von Instanzen zurück.
* **`connection-string-setting` (optional)**: Der Name der Anwendungseinstellung mit der zu verwendenden Speicherverbindungszeichenfolge. Der Standardwert ist AzureWebJobsStorage.
* **`task-hub-name` (optional)**: Der Name des zu verwendenden Durable-Aufgabenhubs. Der Standardwert ist DurableFunctionsHub. Dieser Wert kann auch in [host.json](durable-functions-bindings.md#host-json) über durableTask:HubName festgelegt werden.

```bash
func durable get-instances
```

## <a name="querying-instances-with-filters"></a>Abfragen von Instanzen mit Filtern

Mit der `GetStatusAsync`-Methode (.NET) oder `getStatusBy`-Methode (JavaScript) kann auch eine Liste von Orchestrierungsinstanzen abgerufen werden, die einer Gruppe von vordefinierten Filtern entsprechen. Zu den möglichen Filteroptionen gehören der Erstellungszeitpunkt der Orchestrierung und ihr Laufzeitstatus.

### <a name="c"></a>C#

```csharp
[FunctionName("QueryStatus")]
public static async Task Run(
    [HttpTrigger(AuthorizationLevel.Anonymous, "get", "post")]HttpRequestMessage req,
    [OrchestrationClient] DurableOrchestrationClient client,
    ILogger log)
{
    IEnumerable<OrchestrationRuntimeStatus> runtimeStatus = new List<OrchestrationRuntimeStatus> {
        OrchestrationRuntimeStatus.Completed,
        OrchestrationRuntimeStatus.Running
    };
    IList<DurableOrchestrationStatus> instances = await starter.GetStatusAsync(
        new DateTime(2018, 3, 10, 10, 1, 0),
        new DateTime(2018, 3, 10, 10, 23, 59),
        runtimeStatus
    ); // You can pass CancellationToken as a parameter.
    foreach (var instance in instances)
    {
        log.LogInformation(JsonConvert.SerializeObject(instance));
    };
}
```

### <a name="javascript-functions-2x-only"></a>JavaScript (nur Functions 2.x)

```javascript
const df = require("durable-functions");

module.exports = async function(context, req) {
    const client = df.getClient(context);

    const runtimeStatus = [
        df.OrchestrationRuntimeStatus.Completed,
        df.OrchestrationRuntimeStatus.Running,
    ];
    const instances = await client.getStatusBy(
        new Date(2018, 3, 10, 10, 1, 0),
        new Date(2018, 3, 10, 10, 23, 59),
        runtimeStatus
    );
    instances.forEach((instance) => {
        context.log(JSON.stringify(instance));
    });
};
```

### <a name="using-the-functions-core-tools"></a>Verwenden von Functions Core Tools

Der Befehl `durable get-instances` kann auch mit Filtern verwendet werden. Zusätzlich zu den oben genannten Parametern `top`, `continuation-token`, `connection-string-setting` und `task-hub-name` können drei Filterparameter (`created-after`, `created-before` und `runtime-status`) verwendet werden.

* **`created-after` (optional)**: Ruft die nach diesem Datum/dieser Uhrzeit (UTC) erstellten Instanzen ab. Es werden nach ISO 8601 formatierte datetime-Werte akzeptiert.
* **`created-before` (optional)**: Ruft die vor diesem Datum/dieser Uhrzeit (UTC) erstellten Instanzen ab. Es werden nach ISO 8601 formatierte datetime-Werte akzeptiert.
* **`runtime-status` (optional)**: Ruft die Instanzen ab, deren Status den angegebenen Werten entspricht („running“, „completed“ usw.). Es können mehrere Status angegeben werden (Leerzeichen als Trennzeichen).
* **`top` (optional)**: Die Anzahl pro Anforderung abgerufener Instanzen. Der Standardwert ist 10.
* **`continuation-token` (optional)**: Ein Token, das angibt, welche Seite oder welcher Abschnitt der Instanzen abgerufen werden soll. Jede Ausführung von `get-instances` gibt ein Token an den nächsten Satz von Instanzen zurück.
* **`connection-string-setting` (optional)**: Der Name der Anwendungseinstellung mit der zu verwendenden Speicherverbindungszeichenfolge. Der Standardwert ist AzureWebJobsStorage.
* **`task-hub-name` (optional)**: Der Name des zu verwendenden Durable-Aufgabenhubs. Der Standardwert ist DurableFunctionsHub. Dieser Wert kann auch in [host.json](durable-functions-bindings.md#host-json) über durableTask:HubName festgelegt werden.

Wenn keine Filter (`created-after`, `created-before` oder `runtime-status`) angegeben sind, werden `top` Instanzen abgerufen, unabhängig von Laufzeitstatus und der Erstellungszeit.

```bash
func durable get-instances --created-after 2018-03-10T13:57:31Z --created-before  2018-03-10T23:59Z --top 15
```

## <a name="terminating-instances"></a>Beenden von Instanzen

Eine aktive Orchestrierungsinstanz kann mithilfe der [TerminateAsync](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClient.html#Microsoft_Azure_WebJobs_DurableOrchestrationClient_TerminateAsync_)-Methode der [DurableOrchestrationClient](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClient.html)-Klasse (.NET) oder `terminate`-Methode der `DurableOrchestrationClient`-Klasse (JavaScript) beendet werden. Die beiden Parameter sind eine `instanceId` und eine `reason`-Zeichenfolge, die in Protokolle und den Instanzenstatus geschrieben werden. Die Ausführung einer beendeten Instanz endet, sobald sie den nächsten `await`-Punkt (.NET) oder `yield`-Punkt (JavaScript) erreicht, oder sofort, wenn sie sich bereits an einem `await`-Punkt (.NET) oder `yield`-Punkt (JavaScript) befindet.

### <a name="c"></a>C#

```csharp
[FunctionName("TerminateInstance")]
public static Task Run(
    [OrchestrationClient] DurableOrchestrationClient client,
    [ManualTrigger] string instanceId)
{
    string reason = "It was time to be done.";
    return client.TerminateAsync(instanceId, reason);
}
```

### <a name="javascript-functions-2x-only"></a>JavaScript (nur Functions 2.x)

```javascript
const df = require("durable-functions");

module.exports = async function(context, instanceId) {
    const client = df.getClient(context);

    const reason = "It was time to be done.";
    return client.terminate(instanceId, reason);
};
```

> [!NOTE]
> Die Instanzbeendigung wird momentan nicht weitergegeben. Aktivitätsfunktionen und untergeordnete Orchestrierungen werden bis zum Ende ausgeführt, auch wenn die Orchestrierungsinstanz, durch die sie aufgerufen wurden, beendet wurde.

### <a name="using-core-tools"></a>Verwenden von Core Tools

Es ist auch möglich, eine Orchestrierungsinstanz direkt über den Befehl `durable terminate` von [Core Tools](../functions-run-local.md) zu beenden. Hierfür werden die folgenden Parameter verwendet:

* **`id` (erforderlich)**: Die ID der zu beendenden Orchestrierungsinstanz.
* **`reason` (optional)**: Der Grund für die Beendigung.
* **`connection-string-setting` (optional)**: Der Name der Anwendungseinstellung mit der zu verwendenden Speicherverbindungszeichenfolge. Der Standardwert ist AzureWebJobsStorage.
* **`task-hub-name` (optional)**: Der Name des zu verwendenden Durable-Aufgabenhubs. Der Standardwert ist DurableFunctionsHub. Dieser Wert kann auch in [host.json](durable-functions-bindings.md#host-json) über durableTask:HubName festgelegt werden.

Der folgende Befehl beendet die Orchestrierungsinstanz mit der ID 0ab8c55a66644d68a3a8b220b12d209c:

```bash
func durable terminate --id 0ab8c55a66644d68a3a8b220b12d209c --reason "It was time to be done."
```

## <a name="sending-events-to-instances"></a>Senden von Ereignissen an Instanzen

Ereignisbenachrichtigungen können mit der [RaiseEventAsync](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClient.html#Microsoft_Azure_WebJobs_DurableOrchestrationClient_RaiseEventAsync_)-Methode der [DurableOrchestrationClient](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClient.html)-Klasse (.NET) oder `raiseEvent`-Methode der `DurableOrchestrationClient`-Klasse (JavaScript) an aktive Instanzen gesendet werden. Instanzen, die auf einen Aufruf von [WaitForExternalEvent](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationContext.html#Microsoft_Azure_WebJobs_DurableOrchestrationContext_WaitForExternalEvent_) (.NET) oder `waitForExternalEvent` (JavaScript) warten, können diese Ereignisse verarbeiten.

Die Parameter für [RaiseEventAsync](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClient.html#Microsoft_Azure_WebJobs_DurableOrchestrationClient_RaiseEventAsync_) (.NET) und `raiseEvent` (JavaScript) lauten wie folgt:

* **InstanceId**: Die eindeutige ID der Instanz.
* **EventName**: Der Name des zu sendenden Ereignisses.
* **EventData**: Eine JSON-serialisierbare Nutzlast, die an die Instanz gesendet werden soll.

### <a name="c"></a>C#

```csharp
[FunctionName("RaiseEvent")]
public static Task Run(
    [OrchestrationClient] DurableOrchestrationClient client,
    [ManualTrigger] string instanceId)
{
    int[] eventData = new int[] { 1, 2, 3 };
    return client.RaiseEventAsync(instanceId, "MyEvent", eventData);
}
```

### <a name="javascript-functions-2x-only"></a>JavaScript (nur Functions 2.x)

```javascript
const df = require("durable-functions");

module.exports = async function(context, instanceId) {
    const client = df.getClient(context);

    const eventData = [ 1, 2, 3 ];
    return client.raiseEvent(instanceId, "MyEvent", eventData);
};
```

> [!WARNING]
> Wenn keine Orchestrierungsinstanz mit der angegebenen *Instanz-ID* vorhanden ist, oder die Instanz nicht auf den angegebenen *Ereignisnamen* wartet, wird die Ereignisnachricht verworfen. Weitere Informationen zu diesem Verhalten finden Sie unter [Expected behavior when unexpected event is received?](https://github.com/Azure/azure-functions-durable-extension/issues/29) (Erwartetes Verhalten, wenn ein unerwartetes Ereignis empfangen wird?).

### <a name="using-core-tools"></a>Verwenden von Core Tools

Es ist auch möglich, ein Ereignis an eine Orchestrierungsinstanz direkt über den Befehl `durable raise-event` von [Core Tools](../functions-run-local.md) auszulösen. Hierfür werden die folgenden Parameter verwendet:

* **`id` (erforderlich)**: Die ID der Orchestrierungsinstanz.
* **`event-name` (optional)**: Der Name des auszulösenden Ereignisses. Der Standardwert ist `$"Event_{RandomGUID}"`.
* **`event-data` (optional)**: Die an die Orchestrierungsinstanz zu sendenden Daten. Dies kann den Pfad zu einer JSON-Datei sein, oder die Daten können direkt in der Befehlszeile angegeben werden.
* **`connection-string-setting` (optional)**: Der Name der Anwendungseinstellung mit der zu verwendenden Speicherverbindungszeichenfolge. Der Standardwert ist AzureWebJobsStorage.
* **`task-hub-name` (optional)**: Der Name des zu verwendenden Durable-Aufgabenhubs. Der Standardwert ist DurableFunctionsHub. Dieser Wert kann auch in [host.json](durable-functions-bindings.md#host-json) über durableTask:HubName festgelegt werden.

```bash
func durable raise-event --id 0ab8c55a66644d68a3a8b220b12d209c --event-name MyEvent --event-data @eventdata.json
```

```bash
func durable raise-event --id 1234567 --event-name MyOtherEvent --event-data 3
```

## <a name="wait-for-orchestration-completion"></a>Warten auf den Abschluss der Orchestrierung

Die [DurableOrchestrationClient](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClient.html)-Klasse macht eine [WaitForCompletionOrCreateCheckStatusResponseAsync](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClient.html#Microsoft_Azure_WebJobs_DurableOrchestrationClient_WaitForCompletionOrCreateCheckStatusResponseAsync_)-API in .NET verfügbar, mit der die tatsächliche Ausgabe einer Orchestrierungsinstanz synchron abgerufen werden kann. In JavaScript macht die `DurableOrchestrationClient`-Klasse eine `waitForCompletionOrCreateCheckStatusResponse`-API für den gleichen Zweck verfügbar. Für die Methoden wird ein Standardwert von 10 Sekunden für `timeout` und von 1 Sekunde für `retryInterval` verwendet, wenn keine Werte festgelegt werden.  

Hier ist ein Beispiel für eine HTTP-Triggerfunktion angegeben, mit dem die Nutzung dieser API veranschaulicht wird:

[!code-csharp[Main](~/samples-durable-functions/samples/precompiled/HttpSyncStart.cs)]

[!code-javascript[Main](~/samples-durable-functions/samples/javascript/HttpSyncStart/index.js)]

Die Funktion kann mit der folgenden Zeile aufgerufen werden, indem eine Zeitlimit von 2 Sekunden und ein Wiederholungsintervall von 0,5 Sekunden verwendet wird:

```bash
    http POST http://localhost:7071/orchestrators/E1_HelloSequence/wait?timeout=2&retryInterval=0.5
```

Je nach Zeitraum, der zum Abrufen der Antwort aus der Orchestrierungsinstanz erforderlich ist, gibt es zwei Fälle:

* Die Orchestrierungsinstanzen werden innerhalb des definierten Zeitraums (hier: 2 Sekunden) abgeschlossen, und die Antwort ist die tatsächliche Orchestrierungsinstanzausgabe, die synchron bereitgestellt wird:

    ```http
        HTTP/1.1 200 OK
        Content-Type: application/json; charset=utf-8
        Date: Thu, 14 Dec 2017 06:14:29 GMT
        Server: Microsoft-HTTPAPI/2.0
        Transfer-Encoding: chunked

        [
            "Hello Tokyo!",
            "Hello Seattle!",
            "Hello London!"
        ]
    ```

* Die Orchestrierungsinstanzen können nicht innerhalb des definierten Zeitraums (hier: 2 Sekunden) abgeschlossen werden, und die Antwort ist die Standardantwort, die unter **Ermittlung der HTTP-API-URL** beschrieben ist:

    ```http
        HTTP/1.1 202 Accepted
        Content-Type: application/json; charset=utf-8
        Date: Thu, 14 Dec 2017 06:13:51 GMT
        Location: http://localhost:7071/admin/extensions/DurableTaskExtension/instances/d3b72dddefce4e758d92f4d411567177?taskHub={taskHub}&connection={connection}&code={systemKey}
        Retry-After: 10
        Server: Microsoft-HTTPAPI/2.0
        Transfer-Encoding: chunked

        {
            "id": "d3b72dddefce4e758d92f4d411567177",
            "sendEventPostUri": "http://localhost:7071/admin/extensions/DurableTaskExtension/instances/d3b72dddefce4e758d92f4d411567177/raiseEvent/{eventName}?taskHub={taskHub}&connection={connection}&code={systemKey}",
            "statusQueryGetUri": "http://localhost:7071/admin/extensions/DurableTaskExtension/instances/d3b72dddefce4e758d92f4d411567177?taskHub={taskHub}&connection={connection}&code={systemKey}",
            "terminatePostUri": "http://localhost:7071/admin/extensions/DurableTaskExtension/instances/d3b72dddefce4e758d92f4d411567177/terminate?reason={text}&taskHub={taskHub}&connection={connection}&code={systemKey}",
            "rewindPostUri": "https://localhost:7071/admin/extensions/DurableTaskExtension/instances/d3b72dddefce4e758d92f4d411567177/rewind?reason={text}&taskHub={taskHub}&connection={connection}&code={systemKey}"
        }
    ```

> [!NOTE]
> Das Format der Webhook-URLs kann in Abhängigkeit davon variieren, welche Version des Azure Functions-Hosts Sie ausführen. Das obige Beispiel gilt für den Azure Functions 2.x-Host.

## <a name="retrieving-http-management-webhook-urls"></a>Abrufen von HTTP-Management-Webhook-URLs

Externe Systeme können mit robusten Funktionen über die Webhook-URLs kommunizieren, die Teil der in [HTTP-APIs in Durable Functions (Azure Functions)](durable-functions-http-api.md) beschriebenen Standardantwort sind. Allerdings kann auch im Orchestrierungsclient oder in einer Aktivitätsfunktion über die [CreateHttpManagementPayload](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClient.html#Microsoft_Azure_WebJobs_DurableOrchestrationClient_CreateHttpManagementPayload_)-Methode der [DurableOrchestrationClient](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClient.html)-Klasse (.NET) oder `createHttpManagementPayload`-Methode der `DurableOrchestrationClient`-Klasse (JavaScript) programmgesteuert auf die Webhook-URLs zugegriffen werden.

[CreateHttpManagementPayload](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClient.html#Microsoft_Azure_WebJobs_DurableOrchestrationClient_CreateHttpManagementPayload_) und `createHttpManagementPayload` verfügen über einen Parameter:

* **instanceId**: Die eindeutige ID der Instanz.

Die Methoden geben eine Instanz von [HttpManagementPayload](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.Extensions.DurableTask.HttpManagementPayload.html#Microsoft_Azure_WebJobs_Extensions_DurableTask_HttpManagementPayload_) (.NET) bzw. ein Objekt (JavaScript) mit den folgenden Zeichenfolgeneigenschaften zurück:

* **Id**: Die Instanz-ID der Orchestrierung (muss mit der Eingabe `InstanceId` identisch sein).
* **StatusQueryGetUri**: Status-URL der Orchestrierungsinstanz
* **SendEventPostUri**: URL der Orchestrierungsinstanz für die „Ereignisauslösung“
* **TerminatePostUri**: URL der Orchestrierungsinstanz für die „Beendigung“
* **RewindPostUri**: URL der Orchestrierungsinstanz für den „Rücklauf“

Aktivitätsfunktionen können zum Überwachen oder Auslösen von Ereignissen in einer Orchestrierung eine Instanz dieser Objekte an externe Systeme senden:

### <a name="c"></a>C#

```csharp
[FunctionName("SendInstanceInfo")]
public static void SendInstanceInfo(
    [ActivityTrigger] DurableActivityContext ctx,
    [OrchestrationClient] DurableOrchestrationClient client,
    [DocumentDB(
        databaseName: "MonitorDB",
        collectionName: "HttpManagementPayloads",
        ConnectionStringSetting = "CosmosDBConnection")]out dynamic document)
{
    HttpManagementPayload payload = client.CreateHttpManagementPayload(ctx.InstanceId);

    // send the payload to Cosmos DB
    document = new { Payload = payload, id = ctx.InstanceId };
}
```

### <a name="javascript-functions-2x-only"></a>JavaScript (nur Functions 2.x)

```javascript
const df = require("durable-functions");

modules.exports = async function(context, ctx) {
    const client = df.getClient(context);

    const payload = client.createHttpManagementPayload(ctx.instanceId);

    // send the payload to Cosmos DB
    context.bindings.document = JSON.stringify({
        id: ctx.instanceId,
        payload,
    });
};
```

## <a name="rewinding-instances-preview"></a>Zurückspulen-Instanzen (Vorschau)

Eine fehlerhafte Orchestrierungsinstanz kann mithilfe der [RewindAsync](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClient.html#Microsoft_Azure_WebJobs_DurableOrchestrationClient_RewindAsync_System_String_System_String_)-API (.NET) oder `rewindAsync`-API (JavaScript) zu einem vorherigen fehlerfreien Zustand *zurückgespult* werden. Dies funktioniert durch Zurückversetzen der Orchestrierung in den Status *Ausgeführt* und erneutes Ausführen der Ausführungsfehler der Aktivität und/oder Unterorchestrierung, die zum Fehler bei der Orchestrierung geführt haben.

> [!NOTE]
> Diese API ist nicht als Ersatz für ordnungsgemäße Richtlinien zur Fehlerbehandlung und Wiederholung gedacht. Sie soll nur in Fällen verwendet werden, in denen Orchestrierungsinstanzen aus unerwarteten Gründen ausfallen. Weitere Informationen zur Richtlinien für Fehlerbehandlung und Wiederholung finden Sie im Thema [Fehlerbehandlung](durable-functions-error-handling.md).

Ein Beispiel-Anwendungsfall für *Zurückspulen* ist ein Workflow, der eine Reihe von [menschlichen Genehmigungen](durable-functions-concepts.md#human) umfasst. Angenommen, eine Reihe von Aktivitätsfunktionen benachrichtigt jemanden, dass seine Genehmigung erforderlich ist und wartet in Echtzeit auf die Antwort. Nachdem alle Genehmigungsaktivitäten Antworten erhalten haben oder abgelaufen sind, tritt aufgrund einer Fehlkonfiguration einer Anwendung, z.B. eine ungültige Datenbank-Verbindungszeichenfolge, ein Fehler bei einer anderen Aktivität auf. Das Ergebnis ist ein Orchestrierungsfehler tief im Workflow. Mit der `RewindAsync`-API (.NET) oder `rewindAsync`-API (JavaScript) kann ein Anwendungsadministrator den Konfigurationsfehler beheben und die fehlerhafte Orchestrierung zum Zustand unmittelbar vor dem Fehler *zurückspulen*. Keiner der Schritte, die menschliche Interaktion erforderten, muss erneut genehmigt werden, und die Orchestrierung kann jetzt erfolgreich abgeschlossen werden.

> [!NOTE]
> Die Funktion *Zurückspulen* unterstützt kein Zurückspulen von Orchestrierungsinstanzen, die permanente Timer verwenden.

### <a name="c"></a>C#

```csharp
[FunctionName("RewindInstance")]
public static Task Run(
    [OrchestrationClient] DurableOrchestrationClient client,
    [ManualTrigger] string instanceId)
{
    string reason = "Orchestrator failed and needs to be revived.";
    return client.RewindAsync(instanceId, reason);
}
```

### <a name="javascript-functions-2x-only"></a>JavaScript (nur Functions 2.x)

```javascript
const df = require("durable-functions");

module.exports = async function(context, instanceId) {
    const client = df.getClient(context);

    const reason = "Orchestrator failed and needs to be revived.";
    return client.rewind(instanceId, reason);
};
```

### <a name="using-core-tools"></a>Verwenden von Core Tools

Es ist auch möglich, eine Orchestrierungsinstanz direkt über den Befehl `durable rewind` von [Core Tools](../functions-run-local.md) zurückzuspulen. Hierfür werden die folgenden Parameter verwendet:

* **`id` (erforderlich)**: Die ID der Orchestrierungsinstanz.
* **`reason` (optional)**: Der Grund für das Zurückspulen der Orchestrierungsinstanz.
* **`connection-string-setting` (optional)**: Der Name der Anwendungseinstellung mit der zu verwendenden Speicherverbindungszeichenfolge. Der Standardwert ist AzureWebJobsStorage.
* **`task-hub-name` (optional)**: Der Name des zu verwendenden Durable-Aufgabenhubs. Der Standardwert ist DurableFunctionsHub. Dieser Wert kann auch in [host.json](durable-functions-bindings.md#host-json) über durableTask:HubName festgelegt werden.

```bash
func durable rewind --id 0ab8c55a66644d68a3a8b220b12d209c --reason "Orchestrator failed and needs to be revived."
```

## <a name="purge-instance-history"></a>Löschen des Instanzverlaufs

> [!NOTE]
> Die `PurgeInstanceHistoryAsync`-API ist derzeit nur für C# verfügbar. Sie wird in einer zukünftigen Version zu JavaScript hinzugefügt.

Der Orchestrierungsverlauf kann mithilfe von [PurgeInstanceHistoryAsync](https://azure.github.io/azure-functions-durable-extension/api/Microsoft.Azure.WebJobs.DurableOrchestrationClient.html#Microsoft_Azure_WebJobs_DurableOrchestrationClient_PurgeInstanceHistoryAsync_) gelöscht werden. Mit der Funktion werden alle Daten im Zusammenhang mit einer Orchestrierung entfernt – Azure-Tabellenzeilen und große Nachrichtenblobs, sofern diese vorhanden sind. Diese Methode weist zwei Überladungen auf. Bei der ersten wird der Verlauf durch die ID der Orchestrierungsinstanz gelöscht:

```csharp
[FunctionName("PurgeInstanceHistory")]
public static Task Run(
    [OrchestrationClient] DurableOrchestrationClient client,
    [ManualTrigger] string instanceId)
{
    return client.PurgeInstanceHistoryAsync(instanceId);
}
```

Das zweite Beispiel zeigt eine per Timer ausgelöste Funktion, die den Verlauf für alle Orchestrierungsinstanzen löscht, die nach Ablauf der angegebenen Zeitspanne abgeschlossen wurden. In diesem Fall werden die Daten für alle Instanzen entfernt, die vor mindestens 30 Tagen abgeschlossen wurden. Die Ausführung der Funktion ist einmal pro Tag um 12 Uhr geplant:

```csharp
[FunctionName("PurgeInstanceHistory")]
public static Task Run(
    [OrchestrationClient] DurableOrchestrationClient client,
    [TimerTrigger("0 0 12 * * *")]TimerInfo myTimer)
{
    return client.PurgeInstanceHistoryAsync(
                    DateTime.MinValue,
                    DateTime.UtcNow.AddDays(-30),  
                    new List<OrchestrationStatus>
                    {
                        OrchestrationStatus.Completed
                    });
}
```

> [!NOTE]
> Die Überladung *PurgeInstanceHistory* nimmt den Zeitraum als Parameter an und verarbeitet nur Orchestrierungsinstanzen mit einem der Laufzeitstatus „Abgeschlossen“, „Beendet“ oder „Fehler“.

### <a name="using-core-tools"></a>Verwenden von Core Tools

Es ist möglich, den Verlauf einer Orchestrierungsinstanz mithilfe des Befehls `durable purge-history` von [Core Tools](../functions-run-local.md) zu löschen. Ähnlich wie im zweiten C#-Beispiel oben wird der Verlauf für alle Orchestrierungsinstanzen gelöscht, die während eines angegebenen Zeitintervalls erstellt wurden. Die gelöschten Instanzen können weiter nach Laufzeitstatus gefiltert werden. Der Befehl verfügt über mehrere Parameter:

* **`created-after` (optional)**: Löscht den Verlauf der nach diesem Datum/dieser Uhrzeit (UTC) erstellten Instanzen. Es werden nach ISO 8601 formatierte datetime-Werte akzeptiert.
* **`created-before` (optional)**: Löscht den Verlauf der vor diesem Datum/dieser Uhrzeit (UTC) erstellten Instanzen. Es werden nach ISO 8601 formatierte datetime-Werte akzeptiert.
* **`runtime-status` (optional)**: Löscht den Verlauf der Instanzen, deren Status den angegebenen Werten entspricht („running“, „completed“ usw.). Es können mehrere Status angegeben werden (Leerzeichen als Trennzeichen).
* **`connection-string-setting` (optional)**: Der Name der Anwendungseinstellung mit der zu verwendenden Speicherverbindungszeichenfolge. Der Standardwert ist AzureWebJobsStorage.
* **`task-hub-name` (optional)**: Der Name des zu verwendenden Durable-Aufgabenhubs. Der Standardwert ist DurableFunctionsHub. Dieser Wert kann auch in [host.json](durable-functions-bindings.md#host-json) über durableTask:HubName festgelegt werden.

Der folgende Befehl löscht den Verlauf aller fehlerhaften Instanzen, die vor dem 14. November 2018 um 19:35 Uhr (UTC) erstellt wurden.

```bash
func durable purge-history --created-before 2018-11-14T19:35:00.0000000Z --runtime-status failed
```

## <a name="deleting-a-task-hub"></a>Löschen eines Aufgabenhubs

Mithilfe des Befehls `durable delete-task-hub` von [Core Tools](../functions-run-local.md) können alle Speicherartefakte, die einem bestimmten Aufgabenhub zugeordnet sind, gelöscht werden. Dies schließt Azure Storage-Tabellen, Warteschlangen und Blobs ein. Der Befehl verfügt über zwei Parameter:

* **`connection-string-setting` (optional)**: Der Name der Anwendungseinstellung mit der zu verwendenden Speicherverbindungszeichenfolge. Der Standardwert ist AzureWebJobsStorage.
* **`task-hub-name` (optional)**: Der Name des zu verwendenden Durable-Aufgabenhubs. Der Standardwert ist DurableFunctionsHub. Dieser Wert kann auch in [host.json](durable-functions-bindings.md#host-json) über durableTask:HubName festgelegt werden.

Der folgende Befehl löscht alle Azure Storage-Daten, die dem Aufgabenhub „UserTest“ zugeordnet sind.

```bash
func durable delete-task-hub --task-hub-name UserTest
```

## <a name="next-steps"></a>Nächste Schritte

> [!div class="nextstepaction"]
> [HTTP APIs in Durable Functions (Azure Functions)](durable-functions-http-api.md) (HTTP-APIs in Durable Functions [Azure Functions])
