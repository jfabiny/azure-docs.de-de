---
title: Includedatei
description: Includedatei
services: container-registry
author: dlepow
ms.service: container-registry
ms.topic: include
ms.date: 01/23/2019
ms.author: danlep
ms.custom: include file
ms.openlocfilehash: a97bcf371efc42ff6ff12ba5921eba53abf519bc
ms.sourcegitcommit: a7331d0cc53805a7d3170c4368862cad0d4f3144
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/30/2019
ms.locfileid: "55302258"
---
## <a name="run-image-from-registry"></a>Ausführen des Images aus der Registrierung

Als Nächstes können Sie das Containerimage `hello-world:v1` per Pull abrufen und mithilfe von [docker run][docker-run] aus Ihrer Containerregistrierung ausführen:

```Docker
docker run <acrLoginServer>/hello-world:v1  
```

Beispielausgabe: 

```
Unable to find image 'mycontainerregistry007.azurecr.io/hello-world:v1' locally
v1: Pulling from hello-world
Digest: sha256:662dd8e65ef7ccf13f417962c2f77567d3b132f12c95909de6c85ac3c326a345
Status: Downloaded newer image for mycontainerregistry007.azurecr.io/hello-world:v1

Hello from Docker!
This message shows that your installation appears to be working correctly.

[...]
```

<!-- LINKS - External -->
[docker-run]: https://docs.docker.com/engine/reference/commandline/run/
