---
title: Verwalten des Zugriffs auf Azure-Ressourcen mit Privileged Identity Management (PIM)
description: Hier erfahren Sie mehr über das Verwalten des Zugriffs auf Azure-Ressourcen mithilfe von Privileged Identity Management (PIM) und rollenbasierter Zugriffskontrolle (RBAC).
services: active-directory
documentationcenter: ''
author: rolyon
manager: mtillman
editor: skwan
ms.assetid: ba06b8dd-4a74-4bda-87c7-8a8583e6fd14
ms.service: role-based-access-control
ms.devlang: na
ms.topic: conceptual
ms.tgt_pltfrm: na
ms.workload: identity
ms.date: 03/30/2018
ms.author: rolyon
ms.reviewer: skwan
ms.openlocfilehash: 141cba29f5027ce092775d97c1abe9ecf11badf5
ms.sourcegitcommit: e0834ad0bad38f4fb007053a472bde918d69f6cb
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 07/03/2018
ms.locfileid: "37436044"
---
# <a name="manage-access-to-azure-resources-with-privileged-identity-management"></a>Verwalten des Zugriffs auf Azure-Ressourcen mit Privileged Identity Management

Um privilegierte Konten vor bösartigen Cyberangriffen zu schützen, können Sie mit Azure Active Directory Privileged Identity Management (PIM) die Dauer der Aktivierung von Berechtigungen verkürzen und sich mittels Berichten und Warnungen einen besseren Überblick über deren Verwendung verschaffen. Hierfür werden Benutzern von PIM mit Beschränkungen auferlegt, indem ihnen Berechtigungen nur gemäß des Just-in-Time-Prinzips (JIT) zugeteilt oder nur für eine kurze Dauer zugewiesen und danach automatisch widerrufen werden. 

Sie können PIM nun mit der rollenbasierten Zugriffssteuerung in Azure (Role-Based Access Control, RBAC) verwenden, um den Zugriff auf Azure-Ressourcen zu verwalten, zu steuern und zu überwachen. PIM kann die Mitgliedschaft von integrierten und benutzerdefinierten Rollen verwalten, um Sie bei Folgendem zu unterstützen: 

- Bedarfsgesteuertes Aktivieren des Just-in-Time-Zugriffs auf Azure-Ressourcen
- Automatisches Ablaufen des Ressourcenzugriffs für zugewiesene Benutzer und Gruppen
- Zuweisen des temporären Zugriffs auf Azure-Ressourcen für kurze Aufgaben oder Bereitschaftszeitpläne
- Empfangen von Benachrichtigungen, wenn neuen Benutzern oder Gruppen Ressourcenzugriff zugewiesen wird und sie geeignete Zuweisungen aktivieren

Weitere Informationen finden Sie in der [Übersicht über die rollenbasierte Zugriffssteuerung in Azure PIM](../active-directory/privileged-identity-management/azure-pim-resource-rbac.md).