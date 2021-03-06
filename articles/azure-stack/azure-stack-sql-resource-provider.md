---
title: Verwenden von SQL-Datenbanken in Azure Stack | Microsoft-Dokumentation
description: Erfahren Sie, wie Sie in wenigen Schritten SQL-Datenbanken als Dienst in Azure Stack und den SQL Server-Ressourcenanbieteradapter bereitstellen können.
services: azure-stack
documentationCenter: ''
author: jeffgilb
manager: femila
editor: ''
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 10/25/2018
ms.author: jeffgilb
ms.reviewer: quying
ms.lastreviewed: 10/25/2018
ms.openlocfilehash: 7183cae491287042c778c2e56be8a1451c8c71a2
ms.sourcegitcommit: 898b2936e3d6d3a8366cfcccc0fccfdb0fc781b4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/30/2019
ms.locfileid: "55247764"
---
# <a name="use-sql-databases-on-microsoft-azure-stack"></a>Verwenden von SQL-Datenbanken in Microsoft Azure Stack

Verwenden Sie den SQL Server-Ressourcenanbieteradapter, um SQL-Datenbanken als Dienst in [Azure Stack](azure-stack-poc.md) anzubieten. Nachdem Sie den Ressourcenanbieter installiert und mit mindestens einer SQL Server-Instanz verbunden haben, können Sie und Ihre Benutzer damit Folgendes erstellen:

- Datenbanken für native Cloud-Apps.
- Websites, die SQL verwenden.
- Workloads, die SQL verwenden.

Der Ressourcenanbieter bietet nicht alle Datenbankverwaltungsfunktionen von [Azure SQL-Datenbank](https://azure.microsoft.com/services/sql-database/). Zum Beispiel werden Pools für elastische Datenbanken, die automatisch Ressourcen zuordnen, nicht unterstützt. Der Ressourcenanbieter unterstützt jedoch ähnliche Vorgänge für das Erstellen, Lesen, Aktualisieren und Löschen in einer SQL Server-Datenbank. 

## <a name="sql-resource-provider-adapter-architecture"></a>Architektur des SQL-Ressourcenanbieteradapters

Der Ressourcenanbieter besteht aus den folgenden Komponenten:

- **Dem virtuellen Computer des SQL-Ressourcenanbieteradapters**, einem virtuellen Windows Server-Computer, der die Anbieterdienste ausführt.
- **Dem Ressourcenanbieter selbst**, der Anforderungen der und Zugriffe auf Datenbankressourcen verarbeitet.
- **Servern, die SQL Server hosten**, die Kapazität für Datenbanken bereitstellen und als „Hostserver“ bezeichnet werden.

Sie müssen mindestens eine SQL Server-Instanz erstellen bzw. den Zugriff auf externe SQL Server-Instanzen bereitstellen.

> [!NOTE]
> Hostserver, die auf integrierten Azure Stack-Systemen installiert werden, müssen mit einem Mandantenabonnement erstellt werden. Sie können nicht mit dem Standardabonnement des Anbieters erstellt werden. Sie müssen im Mandantenportal oder mit PowerShell mit einer geeigneten Anmeldung erstellt werden. Alle Hostserver sind abrechenbare virtuelle Computer, die Lizenzen benötigen. Der Dienstadministrator kann Besitzer des Mandantenabonnements sein.

## <a name="next-steps"></a>Nächste Schritte

[Bereitstellen des SQL Server-Ressourcenanbieters](azure-stack-sql-resource-provider-deploy.md)
