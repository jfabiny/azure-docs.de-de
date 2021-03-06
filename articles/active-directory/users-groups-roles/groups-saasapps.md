---
title: Verwenden einer Gruppe zum Verwalten des Zugriffs auf SaaS-Anwendungen | Microsoft-Dokumentation
description: Erfahren Sie, wie Sie Gruppen in Azure Active Directory Premium oder Basic den Zugriff auf SaaS-Anwendungen zuweisen, die in Azure Active Directory integriert sind.
services: active-directory
documentationcenter: ''
author: curtand
manager: mtillman
editor: ''
ms.service: active-directory
ms.workload: identity
ms.subservice: users-groups-roles
ms.topic: article
ms.date: 03/14/2017
ms.author: curtand
ms.reviewer: krbain
ms.custom: it-pro
ms.openlocfilehash: a7e4a20905b390945c22557af044cf739bc17ce8
ms.sourcegitcommit: d3200828266321847643f06c65a0698c4d6234da
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/29/2019
ms.locfileid: "55197210"
---
# <a name="using-a-group-to-manage-access-to-saas-applications"></a>Verwenden einer Gruppe zum Verwalten des Zugriffs auf SaaS-Anwendungen
Mit Azure Active Directory (Azure AD) mit einer Azure AD Premium- oder Azure AD-Basic-Lizenz können Sie Gruppen verwenden, um Zugriff auf eine SaaS-Anwendung zu gewähren, die in Azure AD integriert ist. Wenn Sie beispielsweise der Marketingabteilung Zugriff auf fünf verschiedene SaaS-Anwendungen erteilen möchten, können Sie eine Gruppe erstellen, die die Benutzer der Marketingabteilung enthält, und diese Gruppe dann diesen fünf SaaS-Anwendungen zuweisen, die von der Marketingabteilung benötigt werden. Auf diese Weise sparen Sie Zeit, da Sie die Mitgliedschaft für die Marketingabteilung zentral verwalten können. Benutzer werden der Anwendung zugewiesen, wenn sie als Mitglieder der Marketinggruppe hinzugefügt werden. Ebenso wird die Zuweisung der Benutzer zur Anwendung entfernt, wenn sie als Mitglieder aus der Marketinggruppe entfernt werden. Diese Funktion kann für Hunderte von Anwendungen verwendet werden, die Sie aus dem Azure AD-Anwendungskatalog hinzufügen können.

> [!IMPORTANT]
> Sie können diese Funktionen nur verwenden, nachdem Sie eine Azure AD Premium-Testversion gestartet oder Azure AD Premium- bzw. Azure AD Basic-Lizenzen erworben haben. Die gruppenbasierte Zuweisung wird nur für Sicherheitsgruppen unterstützt. Geschachtelte Gruppenmitgliedschaften werden für die gruppenbasierte Zuordnung zu Anwendungen derzeit nicht unterstützt.

**So weisen Sie einem Benutzer oder einer Gruppe den Zugriff auf eine SaaS-Anwendung zu**

1. Wählen Sie im [Azure AD Admin Center](https://aad.portal.azure.com) die Option **Unternehmensanwendungen**.
2. Wählen Sie eine der aus dem Anwendungskatalog hinzugefügten Anwendungen aus, um diese zu öffnen.
3. Wählen Sie **Benutzer und Gruppen** und dann **Alle Benutzer**.
4. Wählen Sie unter **Zuweisung hinzufügen** die Option **Benutzer und Gruppen**, um die Auswahlliste **Benutzer und Gruppen** zu öffnen.
6. Wählen Sie beliebig viele Gruppen oder Benutzer aus, und klicken oder tippen Sie dann auf **Auswählen**, um diese der Liste **Zuweisung hinzufügen** hinzuzufügen. An dieser Stelle können Sie auch einem Benutzer eine Rolle zuweisen.
7. Wählen Sie **Zuweisen**, um die Benutzer oder Gruppen der ausgewählten Unternehmensanwendung zuzuweisen.

### <a name="next-steps"></a>Nächste Schritte
Diese Artikel enthalten zusätzliche Informationen zu Azure Active Directory.

* [Verwalten des Zugriffs auf Ressourcen mit Azure Active Directory-Gruppen](../fundamentals/active-directory-manage-groups.md)
* [Anwendungsverwaltung in Azure Active Directory](../manage-apps/what-is-application-management.md)
* [Azure Active Directory-Cmdlets zum Konfigurieren von Gruppeneinstellungen](groups-settings-cmdlets.md)
* [Was ist Azure Active Directory?](../fundamentals/active-directory-whatis.md)
* [Integrieren lokaler Identitäten in Azure Active Directory](../hybrid/whatis-hybrid-identity.md)
