---
title: Problembehandlung | Microsoft-Dokumentation
titleSuffix: Azure Dev Spaces
services: azure-dev-spaces
ms.service: azure-dev-spaces
ms.subservice: azds-kubernetes
author: zr-msft
ms.author: zarhoads
ms.date: 09/11/2018
ms.topic: article
description: Schnelle Kubernetes-Entwicklung mit Containern und Microservices in Azure
keywords: Docker, Kubernetes, Azure, AKS, Azure Kubernetes Service, Container
ms.openlocfilehash: 37ee9fec8940231a01b0014b020ca3f0dffb53bf
ms.sourcegitcommit: 698a3d3c7e0cc48f784a7e8f081928888712f34b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/31/2019
ms.locfileid: "55467100"
---
# <a name="troubleshooting-guide"></a>Handbuch zur Problembehandlung

Dieses Handbuch enthält Informationen über allgemeine Probleme, die bei Verwendung von Azure Dev Spaces auftreten können.

## <a name="enabling-detailed-logging"></a>Aktivieren der ausführlichen Protokollierung

Um Probleme effektiver zu behandeln, kann es hilfreich sein, ausführlichere Protokolle zur Überprüfung zu erstellen.

Bei der Visual Studio-Erweiterung erreichen Sie dies durch Festlegen der Umgebungsvariable `MS_VS_AZUREDEVSPACES_TOOLS_LOGGING_ENABLED` auf 1. Achten Sie darauf, Visual Studio neu zu starten, damit die Umgebungsvariable übernommen wird. Nach der Aktivierung werden detaillierte Protokolle in das Verzeichnis `%TEMP%\Microsoft.VisualStudio.Azure.DevSpaces.Tools` geschrieben.

An der Befehlzeilenschnittstelle (CLI) können Sie während der Befehlsausführung weitere Informationen ausgeben. Verwenden Sie dazu den Schalter `--verbose`. Sie können `%TEMP%\Azure Dev Spaces` auch nach ausführlicheren Protokollen durchsuchen. Auf einem Mac finden Sie das TEMP-Verzeichnis, indem Sie `echo $TMPDIR` in einem Terminalfenster ausführen. Auf einem Linux-Computer finden Sie das TEMP-Verzeichnis für gewöhnlich unter `/tmp`.

## <a name="debugging-services-with-multiple-instances"></a>Debuggen von Diensten mit mehreren Instanzen

Derzeit funktioniert Azure Dev Spaces am besten, wenn eine einzelne Instanz (Pod) gedebuggt wird. Die Datei „azds.yaml“ enthält die Einstellung „replicaCount“, die die Anzahl der Pods angibt, die für Ihren Dienst ausgeführt werden. Wenn Sie die Einstellung „replicaCount“ ändern, um Ihre App so zu konfigurieren, dass mehrere Pods für einen bestimmten Dienst ausgeführt werden, fügt sich der Debugger dem ersten Pod an (wenn alphabetisch aufgeführt). Falls dieser Pod aus irgendeinem Grund wiederverwendet wird, fügt sich der Debugger einem anderen Pod an, was möglicherweise zu einem unerwarteten Verhalten führt.

## <a name="error-failed-to-create-azure-dev-spaces-controller"></a>Fehler „Azure Dev Spaces-Controller kann nicht erstellt werden“

Dieser Fehler kann angezeigt werden, wenn beim Erstellen des Controllers ein Fehler auftritt. Wenn es sich um einen vorübergehenden Fehler handelt, löschen Sie den Controller und erstellen Sie ihn dann erneut.

### <a name="try"></a>Versuchen Sie Folgendes:

Löschen Sie den Controller über die CLI von Azure Dev Spaces (AZDS CLI). Sie können diesen Vorgang nicht in Visual Studio oder Cloud Shell ausführen. Um die AZDS CLI zu installieren, installieren Sie zuerst die Azure CLI, und führen Sie diesen Befehl aus:

```cmd
az aks use-dev-spaces -g <resource group name> -n <cluster name>
```

Führen Sie dann diesen Befehl aus, um den Controller zu löschen:

```cmd
azds remove -g <resource group name> -n <cluster name>
```

Sie können den Controller über die CLI oder in Visual Studio erneut erstellen. Folgen Sie den Anweisungen in den Tutorials wie beim ersten Start.


## <a name="error-service-cannot-be-started"></a>Fehler „Dienst kann nicht gestartet werden.“

Dieser Fehler kann angezeigt werden, wenn der Dienstcode nicht gestartet wird. Die Ursache liegt häufig im Benutzercode. Um weitere Diagnoseinformationen zu erhalten, nehmen Sie die folgenden Änderungen Ihrer Befehle und Einstellungen vor:

### <a name="try"></a>Versuchen Sie Folgendes:

In der Befehlszeile:

Verwenden Sie bei Verwendung von _azds.exe_ die Befehlszeilenoption „--verbose“, und verwenden Sie die Befehlszeilenoption „--output“ zur Angabe des Ausgabeformats.
 
```cmd
azds up --verbose --output json
```

In Visual Studio:

1. Öffnen Sie **Tools > Optionen**, und wählen Sie unter **Projekte und Projektmappen** die Option **Erstellen und ausführen** aus.
2. Ändern Sie die Einstellungen für **Ausführlichkeit der MSBuild-Projektbuildausgabe:** zu **Detailliert** oder **Diagnose**.

    ![Screenshot des Dialogfelds „Tools > Optionen“](media/common/VerbositySetting.PNG)
    
### <a name="multi-stage-dockerfiles"></a>Mehrstufige Dockerfiles:
Dieser Fehler tritt möglicherweise auf, wenn Sie versuchen, eine mehrstufige Dockerfile zu verwenden. Die ausführliche Ausgabe sieht dann wie folgt aus:

```cmd
$ azds up
Using dev space 'default' with target 'AksClusterName'
Synchronizing files...6s
Installing Helm chart...2s
Waiting for container image build...10s
Building container image...
Step 1/12 : FROM [imagename:tag] AS base
Error parsing reference: "[imagename:tag] AS base" is not a valid repository/tag: invalid reference format
Failed to build container image.
Service cannot be started.
```

Dies liegt daran, dass AKS-Knoten eine ältere Version von Docker ausführen, die mehrstufige Builds nicht unterstützt. Sie müssen Ihre Dockerfile neu schreiben, um mehrstufige Builds zu vermeiden.

### <a name="re-running-a-service-after-controller-re-creation"></a>Erneutes Ausführen eines Diensts nach der Neuerstellung des Controllers
Dieser Fehler wird eventuell angezeigt, wenn Sie versuchen, einen Dienst erneut auszuführen, nachdem Sie den Azure Dev Spaces-Controller entfernt und dann neu erstellt haben, der diesem Cluster zugeordnet ist. Die ausführliche Ausgabe sieht dann wie folgt aus:

```cmd
Installing Helm chart...
Release "azds-33d46b-default-webapp1" does not exist. Installing it now.
Error: release azds-33d46b-default-webapp1 failed: services "webapp1" already exists
Helm install failed with exit code '1': Release "azds-33d46b-default-webapp1" does not exist. Installing it now.
Error: release azds-33d46b-default-webapp1 failed: services "webapp1" already exists
```

Das liegt daran, dass durch das Entfernen des Dev Spaces-Controllers keine zuvor von diesem Controller installierten Dienste entfernt werden. Die Neuerstellung des Controllers und der anschließende Versuch, die Dienste mithilfe des neuen Controllers auszuführen, schlagen fehl, da die alten Diensten immer noch vorhanden sind.

Um dies zu beheben, verwenden Sie den Befehl `kubectl delete`, um die alten Diensten manuell aus Ihrem Cluster zu entfernen, und führen Sie dann Dev Spaces erneut aus, um die neuen Dienste zu installieren.

## <a name="dns-name-resolution-fails-for-a-public-url-associated-with-a-dev-spaces-service"></a>Bei der DNS-Namensauflösung tritt für eine öffentliche URL, die einem Dev Spaces-Dienst zugeordnet ist, ein Fehler auf.

Wenn die DNS-Namensauflösung fehlschlägt, wird Ihnen unter Umständen der Fehler „Page cannot be displayed“ (Die Seite kann nicht angezeigt werden.) oder „This site cannot be reached“ (Diese Website ist nicht erreichbar.) im Webbrowser angezeigt, wenn Sie versuchen, eine Verbindung mit einer URL herzustellen, die einem Dev Spaces-Dienst zugeordnet ist.

### <a name="try"></a>Versuchen Sie Folgendes:

Mit dem folgenden Befehl können Sie alle Ihren Dev Spaces-Diensten zugeordneten URLs auflisten:

```cmd
azds list-uris
```

Der Status *Ausstehend* für eine URL bedeutet, dass Dev Spaces auf den Abschluss der DNS-Registrierung wartet. Manchmal dauert es einige Minuten, bis die Registrierung abgeschlossen ist. Dev Spaces öffnet zudem für die einzelnen Dienste einen localhost-Tunnel, den Sie beim Warten auf die DNS-Registrierung verwenden können.

Wird für eine URL länger als fünf Minuten der Status *Ausstehend* angezeigt, deutet dies unter Umständen auf ein Problem mit dem externen DNS-Pod hin, der den öffentlichen Endpunkt erstellt, und/oder mit dem Pod des Eingangscontrollers, der den öffentlichen Endpunkt abruft. Mit den folgenden Befehlen können Sie diese Pods löschen. Sie werden automatisch neu erstellt.

```cmd
kubectl delete pod -n kube-system -l app=addon-http-application-routing-external-dns
kubectl delete pod -n kube-system -l app=addon-http-application-routing-nginx-ingress
```

## <a name="error-required-tools-and-configurations-are-missing"></a>Fehler „Erforderliche Tools und Konfigurationen fehlen“

Dieser Fehler kann beim Starten von Visual Studio Code auftreten: „[Azure Dev Spaces] Erforderliche Tools und Konfigurationen zum Erstellen und Debuggen von ‚[Projektname]‘ fehlen.“
Der Fehler weist darauf hin, dass „azds.exe“ nicht in der PATH-Umgebungsvariablen angegeben ist, wie in Visual Studio Code zu sehen ist.

### <a name="try"></a>Versuchen Sie Folgendes:

Starten Sie Visual Studio Code über eine Eingabeaufforderung, wo die PATH-Umgebungsvariable ordnungsgemäß eingerichtet ist.

## <a name="error-required-tools-to-build-and-debug-projectname-are-out-of-date"></a>Fehler „Erforderliche Tools zum Erstellen und Debuggen von ‚Projektname‘ sind veraltet.“

Dieser Fehler wird in Visual Studio Code angezeigt, wenn Sie über eine neuere Version der Visual Studio Code-Erweiterung für Azure Dev Spaces verfügen, aber eine ältere Version der Azure Dev Spaces-Befehlszeilenschnittstelle (CLI).

### <a name="try"></a>Testen

Laden Sie die neueste Version der Azure Dev Spaces-CLI herunter, und installieren Sie sie:

* [Windows](http://aka.ms/get-azds-windows)
* [Mac](http://aka.ms/get-azds-mac)
* [Linux](https://aka.ms/get-azds-linux)

## <a name="error-azds-is-not-recognized-as-an-internal-or-external-command-operable-program-or-batch-file"></a>Fehler: „azds“ wird nicht als interner oder externer Befehl, ausführbares Programm oder Batchdatei erkannt.
 
Dieser Fehler kann angezeigt werden, wenn „azds.exe“ nicht installiert oder nicht ordnungsgemäß konfiguriert ist.

### <a name="try"></a>Versuchen Sie Folgendes:

1. Überprüfen Sie, ob „azds.exe“ in „%ProgramFiles%/Microsoft SDKs\Azure\Azure Dev Spaces CLI (Preview)“ vorhanden ist. Wenn ja, fügen Sie diesen Speicherort der PATH-Umgebungsvariablen hinzu.
2. Wenn „azds.exe“ nicht installiert ist, führen Sie den folgenden Befehl aus:

    ```cmd
    az aks use-dev-spaces -n <cluster-name> -g <resource-group>
    ```

## <a name="warning-dockerfile-could-not-be-generated-due-to-unsupported-language"></a>Warnung „Aufgrund einer nicht unterstützten Sprache konnte keine Dockerfile generiert werden“
Azure Dev Spaces bietet systeminternen Support für C# und Node.js. Wenn Sie *azds prep* in einem Verzeichnis ausführen, das in einer dieser Sprachen geschriebenen Code enthält, erstellt Azure Dev Spaces automatisch eine entsprechende Dockerfile-Datei.

Sie können Azure Dev Spaces auch mit Code verwenden, der in anderen Sprachen geschrieben ist. Dann müssen Sie jedoch vor der erstmaligen Ausführung von *azds up* die Dockerfile-Datei selbst erstellen.

### <a name="try"></a>Versuchen Sie Folgendes:
Wenn Ihre Anwendung in einer Sprache geschrieben ist, die Azure Dev Spaces systemintern nicht unterstützt, müssen Sie zum Erstellen eines Containerimages zum Ausführen des Codes eine entsprechende Dockerfile-Datei bereitstellen. Docker stellt eine [Liste der bewährten Methoden für das Schreiben von Dockerfile-Dateien](https://docs.docker.com/develop/develop-images/dockerfile_best-practices/) sowie eine [Dockerfile-Referenz](https://docs.docker.com/engine/reference/builder/) bereit, die Ihnen beim Schreiben einer für Ihre Bedürfnisse geeigneten Dockerfile-Datei behilflich sein können.

Wenn Sie eine entsprechende Dockerfile-Datei haben, können Sie die Ausführung von *azds up* fortsetzen, um Ihre Anwendung in Azure Dev Spaces auszuführen.

## <a name="error-upstream-connect-error-or-disconnectreset-before-headers"></a>Fehler „Upstream-Verbindungsfehler oder Trennung/Reset vor Headern“
Dieser Fehler kann angezeigt werden, wenn Sie versuchen, auf den Dienst zuzugreifen, beispielsweise, wenn Sie in einem Browser zur URL des Diensts wechseln. 

### <a name="reason"></a>Grund 
Der Containerport ist nicht verfügbar. Dieses Problem kann auftreten, weil: 
* Erstellung und Bereitstellung des Containers sind noch nicht abgeschlossen. Das Problem kann vorkommen, wenn Sie `azds up` ausführen oder den Debugger starten, und dann versuchen, auf den Container zuzugreifen, bevor er erfolgreich bereitgestellt wurde.
* Die Portkonfiguration ist nicht konsistent über _Dockerfile_, Helm-Diagramm und sämtlichen Servercode hinweg, durch den ein Port geöffnet wird.

### <a name="try"></a>Versuchen Sie Folgendes:
1. Wenn der Container gerade erstellt/bereitgestellt wird, können Sie 2 bis 3 Sekunden warten und dann erneut versuchen, auf den Dienst zuzugreifen. 
1. Überprüfen Sie Ihre Portkonfiguration. Die angegebenen Portnummern müssen in den folgenden Ressourcen **identisch** sein:
    * **Dockerfile:** Angegeben durch die `EXPOSE`-Anweisung.
    * **[Helm-Chart](https://docs.helm.sh):** Angegeben durch die `externalPort`- und `internalPort`-Werte für einen Dienst (oft in einer `values.yml`-Datei).
    * Alle Ports, die im Anwendungscode geöffnet werden (z. B. in Node.js): `var server = app.listen(80, function () {...}`


## <a name="config-file-not-found"></a>Config-Datei nicht gefunden
Sie führen `azds up` aus und erhalten den folgenden Fehler: `Config file not found: .../azds.yaml`

### <a name="reason"></a>Grund
Führen Sie `azds up` aus dem Stammverzeichnis des auszuführenden Codes aus, und initialisieren Sie den Codeordner für die Ausführung mit Azure Dev Spaces.

### <a name="try"></a>Versuchen Sie Folgendes:
1. Ändern Sie das aktuelle Verzeichnis in den Stammordner, der Dienstcode enthält. 
1. Wenn im Codeordner keine _azds.yaml_-Datei vorhanden ist, führen Sie `azds prep` aus, um Docker-, Kubernetes- und Azure Dev Spaces-Objekte zu generieren.

## <a name="error-the-pipe-program-azds-exited-unexpectedly-with-code-126"></a>Fehler „Das Pipe-Programm ‚azds‘ wurde unerwartet mit Code 126 beendet.“
Das Starten des VS Code-Debuggers kann in einigen Fällen zu diesem Fehler führen.

### <a name="try"></a>Versuchen Sie Folgendes:
1. Schließen Sie VS Code, und öffnen Sie es erneut.
2. Drücken Sie erneut F5.

## <a name="debugging-error-failed-to-find-debugger-extension-for-typecoreclr"></a>Debuggen des Fehlers „Debugger-Erweiterung für coreclr-Typ wurde nicht gefunden“
Beim Ausführen des VS Code-Debuggers wird der folgende Fehler gemeldet: `Failed to find debugger extension for type:coreclr.`

### <a name="reason"></a>Grund
Auf Ihrem Entwicklungscomputer ist die VS Code-Erweiterung für C# nicht installiert. Die Erweiterung für C# enthält Debug-Unterstützung für .Net Core (CoreCLR).

### <a name="try"></a>Versuchen Sie Folgendes:
Installieren Sie die [VS Code-Erweiterung für C#](https://marketplace.visualstudio.com/items?itemName=ms-vscode.csharp).

## <a name="debugging-error-configured-debug-type-coreclr-is-not-supported"></a>Debuggen des Fehlers „Der konfigurierte Debugtyp ‚coreclr‘ wird nicht unterstützt.“
Beim Ausführen des VS Code-Debuggers wird der folgende Fehler gemeldet: `Configured debug type 'coreclr' is not supported.`

### <a name="reason"></a>Grund
Auf Ihrem Entwicklungscomputer ist die VS Code-Erweiterung für Azure Dev Spaces nicht installiert.

### <a name="try"></a>Versuchen Sie Folgendes:
Installieren Sie die [VS Code-Erweiterung für Azure Dev Spaces](get-started-netcore.md).

## <a name="debugging-error-invalid-cwd-value-src-the-system-cannot-find-the-file-specified-or-launch-program-srcpath-to-project-binary-does-not-exist"></a>Debugfehler „Ungültiger ‚cwd‘-Wert ‚/src‘. Das System kann die angegebene Datei nicht finden.“ oder „launch: program ‚/src/[Pfad zur Projektbinärdatei]‘ ist nicht vorhanden“.
Bei der Ausführung des VS Code-Debuggers wird der folgende Fehler gemeldet: `Invalid 'cwd' value '/src'. The system cannot find the file specified.` und/oder `launch: program '/src/[path to project executable]' does not exist`.

### <a name="reason"></a>Grund
Standardmäßig verwendet die VS Code-Erweiterung `src` als Arbeitsverzeichnis für das Projekt im Container. Wenn Sie Ihre `Dockerfile` aktualisiert haben, um ein anderes Arbeitsverzeichnis anzugeben, kann dieser Fehler angezeigt werden.

### <a name="try"></a>Versuchen Sie Folgendes:
Aktualisieren Sie die Datei `launch.json` unter dem Unterverzeichnis `.vscode` Ihres Projektordners. Ändern Sie die `configurations->cwd`-Anweisung so, dass sie auf das selbe Verzeichnis verweist, wie die `WORKDIR`-Variable, die in der `Dockerfile` Ihres Projekts definiert ist. Möglicherweise müssen Sie auch die `configurations->program`-Anweisung aktualisieren.

## <a name="the-type-or-namespace-name-mylibrary-could-not-be-found"></a>Der Typ- oder Namespacename „MyLibrary“ konnte nicht gefunden werden

### <a name="reason"></a>Grund 
Der Buildkontext befindet sich standardmäßig auf Projekt-/Dienstebene, aus diesem Grund kann ein verwendetes Bibliotheksprojekt nicht gefunden werden.

### <a name="try"></a>Versuchen Sie Folgendes:
Erforderliche Maßnahmen:
1. Ändern Sie die _azds.yaml_-Datei, um den Buildkontext auf Projektmappenebene festzulegen.
2. Ändern Sie die _Dockerfile_- und _Dockerfile.develop_-Dateien so, dass sie relativ zum neuen Buildkontext ordnungsgemäß auf die _csproj_-Dateien verweisen.
3. Platzieren Sie neben der SLN-Datei eine _DOCKERIGNORE_-Datei, und ändern Sie sie nach Bedarf.

Ein Beispiel finden Sie unter https://github.com/sgreenmsft/buildcontextsample

## <a name="microsoftdevspacesregisteraction-authorization-error"></a>Autorisierungsfehler „Microsoft.DevSpaces/register/action“
Der folgende Fehler wird möglicherweise angezeigt, wenn Sie einen Azure Dev Space verwalten und in einem Azure-Abonnement arbeiten, für das Sie nicht über Zugriff als Besitzer oder Mitwirkender verfügen.
`The client '<User email/Id>' with object id '<Guid>' does not have authorization to perform action 'Microsoft.DevSpaces/register/action' over scope '/subscriptions/<Subscription Id>'.`

### <a name="reason"></a>Grund
Für das ausgewählte Azure-Abonnement ist der `Microsoft.DevSpaces`-Namespace nicht registriert.

### <a name="try"></a>Versuchen Sie Folgendes:
Jemand, der als Besitzer oder Mitwirkender Zugriff auf das Azure-Abonnement hat, kann den folgenden Azure CLI-Befehl ausführen, um den `Microsoft.DevSpaces`-Namespace manuell zu registrieren:

```cmd
az provider register --namespace Microsoft.DevSpaces
```

## <a name="error-could-not-find-a-ready-tiller-pod-when-launching-dev-spaces"></a>„Fehler: Bereiter Tiller-Pod konnte nicht gefunden werden“ beim Starten von Dev Spaces

### <a name="reason"></a>Grund
Dieser Fehler tritt auf, wenn der Helm-Client nicht mehr mit dem im Cluster ausgeführten Tiller-Pod kommunizieren kann.

### <a name="try"></a>Versuchen Sie Folgendes:
Ein Neustart der Agent-Knoten in Ihrem Cluster behebt in der Regel dieses Problem.

## <a name="azure-dev-spaces-proxy-can-interfere-with-other-pods-running-in-a-dev-space"></a>Azure Dev Spaces-Proxy beeinträchtigt ggf. andere Pods, die in einer Dev Space-Instanz ausgeführt werden

### <a name="reason"></a>Grund
Wenn Sie Dev Spaces auf einem Namespace in Ihrem AKS-Cluster aktivieren, wird ein zusätzlicher Container namens _mindaro-proxy_ in jedem Pod installiert, der in diesem Namespace ausgeführt wird. Dieser Container fängt Aufrufe an die Dienste im Pod ab. Dies ist eine wesentliche Entwicklungsfunktion des Dev Spaces-Teams.

Leider kann dieser Vorgang bestimmte Dienste beeinträchtigen, die in diesen Pods ausgeführt werden. Insbesondere betrifft dies Pods, in denen Azure Cache for Redis ausgeführt wird. Es treten Verbindungsfehler und Fehler bei der Kommunikation zwischen Primär- und Sekundärgerät auf.

### <a name="try"></a>Versuchen Sie Folgendes:
Sie können die betroffenen Pods in einen Namespace im Cluster verschieben, für das Dev Spaces _nicht_ aktiviert ist, während Sie den Rest Ihrer Anwendung weiterhin in einem Namespace ausführen, für das Dev Spaces aktiviert ist. Dev Spaces installiert den Container _mindaro-proxy_ nicht in Namespaces, für die Dev Spaces nicht aktiviert ist.

## <a name="azure-dev-spaces-doesnt-seem-to-use-my-existing-dockerfile-to-build-a-container"></a>Azure Dev Spaces scheint meine vorhandene Dockerfile nicht zum Erstellen eines Containers zu verwenden 

### <a name="reason"></a>Grund
Azure Dev Spaces kann so konfiguriert werden, dass es auf eine bestimmte _Dockerfile_ in Ihrem Projekt verweist. Wenn es den Anschein hat, dass Azure Dev Spaces zum Erstellen Ihrer Container nicht die erwartete _Dockerfile_ verwendet, müssen Sie Azure Dev Spaces möglicherweise explizit mitteilen, wo sich die gewünschte Dockerfile befindet. 

### <a name="try"></a>Versuchen Sie Folgendes:
Öffnen Sie die _azds.yaml_-Datei, die von Azure Dev Spaces in Ihrem Projekt generiert wurde. Verwenden Sie die `configurations->develop->build->dockerfile`-Direktive, um auf die Dockerfile zu verweisen, die Sie verwenden möchten:

```
...
configurations:
  develop:
    build:
      dockerfile: Dockerfile.develop
```
