---
title: Verwalten von Programmen und Steuerelementen für Azure AD-Zugriffsüberprüfungen | Microsoft Docs
description: Sie können zusätzliche Programme für jede Governance-, Risikomanagement- und Konformitätsinitiative in Ihrer Organisation erstellen, um Azure Active Directory-Zugriffsüberprüfungen als Steuerelemente zu erfassen und zu organisieren.
services: active-directory
documentationcenter: ''
author: rolyon
manager: mtillman
editor: markwahl-msft
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.subservice: compliance
ms.date: 06/21/2018
ms.author: rolyon
ms.reviewer: mwahl
ms.openlocfilehash: 0a20f1bf53a42487e3ce6b347cde8be9a343bc2e
ms.sourcegitcommit: d3200828266321847643f06c65a0698c4d6234da
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/29/2019
ms.locfileid: "55166695"
---
# <a name="manage-programs-and-their-controls"></a>Verwalten von Programmen und ihren Steuerelementen 

Azure Active Directory (Azure AD) enthält Zugriffsüberprüfungen von Gruppenmitgliedern und Anwendungszugriff. Diese Beispiele für Steuerelemente sichern den Überblick, wer auf Gruppenmitgliedschaften und Anwendungen Ihrer Organisation zugreifen kann. Diese Steuerelemente ermöglichen Organisationen das effiziente Verwalten ihrer Governance-, Risikomanagement- und Konformitätsanforderungen.

## <a name="create-and-manage-programs-and-their-controls"></a>Erstellen und Verwalten von Programmen und ihren Steuerelementen
Sie können die Nachverfolgung und das Erfassen von Zugriffsüberprüfungen für verschiedene Zwecke vereinfachen, indem Sie diese Aufgaben in Programmen organisieren. Jede Zugriffsüberprüfung kann mit einem Programm verknüpft werden. Wenn Sie dann Berichte für einen Auditor vorbereiten, können Sie sich auf die Zugriffsüberprüfungen im Bereich einer bestimmten Initiative konzentrieren.  Programme und Ergebnisse der Zugriffsüberprüfung werden Benutzern mit der Rolle „Globaler Administrator“, „Benutzerkontoadministrator“, „Sicherheitsadministrator“ oder „Benutzer mit Leseberechtigung für Sicherheitsfunktionen“ angezeigt.

Um eine Liste der Programme anzuzeigen, navigieren Sie zur Seite [Zugriffsüberprüfungen](https://portal.azure.com/#blade/Microsoft_AAD_ERM/DashboardBlade/), und wählen Sie **Programme**.

**Standardprogramm** ist immer vorhanden. Globale Administratoren und Benutzerkontoadministratoren können weitere Programme erstellen. Sie können z.B. ein Programm für jede Konformitätsinitiative oder für jedes Geschäftsziel verwenden.

Wenn ein Programm nicht mehr benötigt wird und keine Steuerelemente mit ihm verknüpft sind, können Sie es löschen.

## <a name="next-steps"></a>Nächste Schritte

- [Erstellen einer Zugriffsüberprüfung für Mitglieder einer Gruppe oder den Zugriff auf eine Anwendung](create-access-review.md)
- [Abrufen der Ergebnisse einer Zugriffsüberprüfung](retrieve-access-review.md)
