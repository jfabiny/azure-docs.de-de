---
title: Includedatei
description: Includedatei
services: iot-accelerators
author: dominicbetts
ms.service: iot-accelerators
ms.topic: include
ms.date: 07/26/2018
ms.author: dobett
ms.custom: include file
ms.openlocfilehash: 0b2b6814ad0b55d8f56998f6d4c9b6bb88663e04
ms.sourcegitcommit: c2e61b62f218830dd9076d9abc1bbcb42180b3a8
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 12/15/2018
ms.locfileid: "53444132"
---
## <a name="state-behavior"></a>Statusverhalten

Der Abschnitt [Simulation](../articles/iot-accelerators/iot-accelerators-remote-monitoring-device-schema.md#simulation) des Gerätemodellschemas definiert den internen Status eines simulierten Geräts:

- `InitialState` definiert Anfangswerte für alle Eigenschaften des Gerätestatusobjekts.
- `Script` identifiziert eine JavaScript-Datei, die nach einem Zeitplan zum Aktualisieren des Gerätestatus ausgeführt wird.

Das folgende Beispiel zeigt die Definition des Gerätestatusobjekts für eine simulierte Kühlanlage:

```json
"Simulation": {
  "InitialState": {
    "online": true,
    "temperature": 75.0,
    "temperature_unit": "F",
    "humidity": 70.0,
    "humidity_unit": "%",
    "pressure": 150.0,
    "pressure_unit": "psig",
    "simulation_state": "normal_pressure"
  },
  "Interval": "00:00:05",
  "Scripts": {
    "Type": "javascript",
    "Path": "chiller-01-state.js"
  }
}
```

Der Status des simulierten Geräts, wie im Abschnitt `InitialState` definiert, wird im Arbeitsspeicher des Simulationsdiensts festgehalten. Die Statusinformationen werden als Eingabe an die `main`-Funktion übergeben, die in **chiller-01-state.js** definiert ist. In diesem Beispiel führt der Simulationsdienst die Datei **chiller-01-state.js** alle fünf Sekunden aus. Das Skript kann den Status des simulierten Geräts ändern.

Nachstehend sehen Sie das Konzept einer typischen `main`-Funktion:

```javascript
function main(context, previousState, previousProperties) {

  // Use the previous device state to
  // generate the new device state
  // returned by the function.

  return state;
}
```

Der `context`-Parameter hat folgende Eigenschaften:

- `currentTime` als Zeichenfolge mit dem Format `yyyy-MM-dd'T'HH:mm:sszzz`
- `deviceId`, z.B. `Simulated.Chiller.123`
- `deviceModel`, z.B. `Chiller`

Der `state`-Parameter enthält den Status des Geräts, wie er vom Gerätesimulationsdienst verwaltet wird. Dieser Wert ist das vom vorherigen Aufruf an `main` zurückgegebene `state`-Objekt.

Das folgende Beispiel zeigt eine typische Implementierung der `main`-Methode zum Behandeln des vom Simulationsdienst verwalteten Gerätestatus:

```javascript
// Default state
var state = {
  online: true,
  temperature: 75.0,
  temperature_unit: "F",
  humidity: 70.0,
  humidity_unit: "%",
  pressure: 150.0,
  pressure_unit: "psig",
  simulation_state: "normal_pressure"
};

function restoreState(previousState) {
  // If the previous state is null, force a default state
  if (previousState !== undefined && previousState !== null) {
      state = previousState;
  } else {
      log("Using default state");
  }
}

function main(context, previousState, previousProperties) {

  restoreState(previousState);

  // Update state

  return state;
}
```

Das folgende Beispiel zeigt, wie die `main`-Methode Telemetriewerte simulieren kann, die mit der Zeit variieren:

```javascript
/**
 * Simple formula generating a random value
 * around the average and between min and max
 */
function vary(avg, percentage, min, max) {
  var value = avg * (1 + ((percentage / 100) * (2 * Math.random() - 1)));
  value = Math.max(value, min);
  value = Math.min(value, max);
  return value;
}


function main(context, previousState, previousProperties) {

    restoreState(previousState);

    // 75F +/- 5%,  Min 25F, Max 100F
    state.temperature = vary(75, 5, 25, 100);

    // 70% +/- 5%,  Min 2%, Max 99%
    state.humidity = vary(70, 5, 2, 99);

    log("Simulation state: " + state.simulation_state);
    if (state.simulation_state === "high_pressure") {
        // 250 psig +/- 25%,  Min 50 psig, Max 300 psig
        state.pressure = vary(250, 25, 50, 300);
    } else {
        // 150 psig +/- 10%,  Min 50 psig, Max 300 psig
        state.pressure = vary(150, 10, 50, 300);
    }

    return state;
}
```

Sie können die vollständige Datei [chiller-01-state.js](https://github.com/Azure/device-simulation-dotnet/blob/master/Services/data/devicemodels/scripts/chiller-01-state.js) auf GitHub anzeigen.

## <a name="method-behavior"></a>Methodenverhalten

Der Abschnitt [CloudToDeviceMethods](../articles/iot-accelerators/iot-accelerators-remote-monitoring-device-schema.md#cloudtodevicemethods) des Gerätemodellschemas definiert die Methoden, auf die ein simuliertes Gerät reagiert.

Das folgende Beispiel zeigt die Liste der Methoden, die von einer simulierten Kühlanlage unterstützt werden:

```json
"CloudToDeviceMethods": {
  "Reboot": {
    "Type": "javascript",
    "Path": "Reboot-method.js"
  },
  "FirmwareUpdate": {
    "Type": "javascript",
    "Path": "FirmwareUpdate-method.js"
  },
  "EmergencyValveRelease": {
    "Type": "javascript",
    "Path": "EmergencyValveRelease-method.js"
  },
  "IncreasePressure": {
    "Type": "javascript",
    "Path": "IncreasePressure-method.js"
  }
}
```

Jeder Methode ist eine JavaScript-Datei zugeordnet, die das Verhalten der Methode implementiert.

Der Status des simulierten Geräts, wie im Abschnitt `InitialState` des Schemas definiert, wird im Arbeitsspeicher des Simulationsdiensts festgehalten. Die Statusinformationen werden als Eingabe an die `main`-Funktion übergeben, die in der JavaScript-Datei definiert ist, wenn die Methode aufgerufen wird. Das Skript kann den Status des simulierten Geräts ändern.

Nachstehend sehen Sie das Konzept einer typischen `main`-Funktion:

```javascript
function main(context, previousState, previousProperties) {

}
```

Der `context`-Parameter hat folgende Eigenschaften:

- `currentTime` als Zeichenfolge mit dem Format `yyyy-MM-dd'T'HH:mm:sszzz`
- `deviceId`, z.B. `Simulated.Chiller.123`
- `deviceModel`, z.B. `Chiller`

Der `state`-Parameter enthält den Status des Geräts, wie er vom Gerätesimulationsdienst verwaltet wird.

Der `properties`-Parameter enthält die Eigenschaften des Geräts, die als gemeldete Eigenschaften in den IoT Hub-Gerätezwilling geschrieben sind.

Es gibt drei globalen Funktionen, die Sie verwenden können, um das Verhalten der Methode zu implementieren:

- `updateState`, um den vom Simulationsdienst festgehaltenen Status zu aktualisieren.
- `updateProperty`, um eine einzelne Geräteeigenschaft zu aktualisieren.
- `sleep`, um die Ausführung zum Simulieren einer lange ausgeführten Aufgabe anzuhalten.

Das folgende Beispiel zeigt eine verkürzte Version des **IncreasePressure method.js**-Skripts, das von der simulierten Kühlanlage verwendet wird:

```javascript
function main(context, previousState, previousProperties) {

    log("Starting 'Increase Pressure' method simulation (5 seconds)");

    // Pause the simulation and change the simulation mode so that the
    // temperature will fluctuate at ~250 when it resumes
    var state = {
        simulation_state: "high_pressure",
        CalculateRandomizedTelemetry: false
    };
    updateState(state);

    // Increase
    state.pressure = 210;
    updateState(state);
    log("Pressure increased to " + state.pressure);
    sleep(1000);

    // Increase
    state.pressure = 250;
    updateState(state);
    log("Pressure increased to " + state.pressure);
    sleep(1000);

    // Resume the simulation
    state.CalculateRandomizedTelemetry = true;
    updateState(state);

    log("'Increase Pressure' method simulation completed");
}
```

## <a name="debugging-script-files"></a>Debuggen von Skriptdateien

Es ist nicht möglich, dem Javascript-Interpreter, der vom Gerätesimulationsdienst zum Ausführen von Status- und Methodenskripts verwendet wird, einen Debugger anzufügen. Allerdings können Sie Informationen im Dienstprotokoll protokollieren. Die integrierte `log()`-Funktion ermöglicht Ihnen das Speichern von Informationen zum Nachverfolgen und Debuggen der Funktionsausführung.

Wenn ein Syntaxfehler vorliegt, tritt beim Interpreter ein Fehler auf, und es wird ein `Jint.Runtime.JavaScriptException`-Eintrag in das Protokoll des Diensts geschrieben.

Im Artikel [Ausführen des Gerätesimulationsdiensts](https://github.com/Azure/device-simulation-dotnet#running-the-service-locally-eg-for-development-tasks) auf GitHub erfahren Sie, wie Sie den Gerätesimulationsdienst lokal ausführen. Die lokale Ausführung des Diensts erleichtert das Debuggen Ihrer simulierten Geräte, bevor Sie sie in der Cloud bereitstellen.