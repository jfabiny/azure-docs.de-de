---
title: 'Tutorial: Konfigurieren von Cornerstone OnDemand für die automatische Benutzerbereitstellung in Azure Active Directory | Microsoft-Dokumentation'
description: Erfahren Sie, wie Sie Azure Active Directory für das automatische Bereitstellen und Aufheben der Bereitstellung von Benutzerkonten in Cornerstone OnDemand konfigurieren.
services: active-directory
documentationcenter: ''
author: zhchia
writer: zhchia
manager: beatrizd
ms.assetid: d4ca2365-6729-48f7-bb7f-c0f5ffe740a3
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 01/31/2018
ms.author: v-ant
ms.openlocfilehash: 9f18fcb38e6e0855a00ffb454211273dfb2041a6
ms.sourcegitcommit: d3200828266321847643f06c65a0698c4d6234da
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/29/2019
ms.locfileid: "55168497"
---
# <a name="tutorial-configure-cornerstone-ondemand-for-automatic-user-provisioning"></a>Tutorial: Konfigurieren von Cornerstone OnDemand für die automatische Benutzerbereitstellung


In diesem Tutorial werden die Schritte erläutert, die in Cornerstone OnDemand und Azure Active Directory (Azure AD) ausgeführt werden müssen, um Azure AD für das automatische Bereitstellen und Aufheben der Bereitstellung von Benutzern und/oder Gruppen in Cornerstone OnDemand zu konfigurieren.


> [!NOTE]
> In diesem Tutorial wird ein Connector beschrieben, der auf dem Benutzerbereitstellungsdienst von Azure AD basiert. Wichtige Details zum Zweck und zur Funktionsweise dieses Diensts sowie häufig gestellte Fragen finden Sie unter [Automatisieren der Bereitstellung und Bereitstellungsaufhebung von Benutzern für SaaS-Anwendungen mit Azure Active Directory](../manage-apps/user-provisioning.md).

## <a name="prerequisites"></a>Voraussetzungen

Das diesem Tutorial zu Grunde liegende Szenario setzt voraus, dass Sie bereits über die folgenden Voraussetzungen verfügen:

*   Einen Azure AD-Mandanten
*   Einen Cornerstone OnDemand-Mandanten
*   Ein Benutzerkonto in Cornerstone OnDemand mit Administratorrechten


> [!NOTE]
> Die Azure AD-Bereitstellungsintegration basiert auf dem [Cornerstone OnDemand-Webdienst](https://help.csod.com/help/csod_0/Content/Resources/Documents/WebServices/CSOD_-_Summary_of_Web_Services_v20151106.pdf), der für Cornerstone OnDemand-Teams verfügbar ist.

## <a name="adding-cornerstone-ondemand-from-the-gallery"></a>Hinzufügen von Cornerstone OnDemand aus dem Katalog
Bevor Sie Cornerstone OnDemand für die automatische Benutzerbereitstellung mit Azure AD konfigurieren, müssen Sie Cornerstone OnDemand aus dem Azure AD-Anwendungskatalog zur Liste der verwalteten SaaS-Anwendungen hinzufügen.

**Führen Sie zum Hinzufügen von Cornerstone OnDemand aus dem Azure AD-Anwendungskatalog die folgenden Schritte aus:**

1. Klicken Sie im linken Navigationsbereich des **[Azure-Portals](https://portal.azure.com)** auf das Symbol für **Azure Active Directory**. 

    ![Schaltfläche „Azure Active Directory“][1]

2. Navigieren Sie zu **Unternehmensanwendungen** > **Alle Anwendungen**.

    ![Der Abschnitt „Unternehmensanwendungen“][2]
    
3. Klicken Sie im oberen Bereich des Dialogfelds auf die Schaltfläche **Neue Anwendung**, um Cornerstone OnDemand hinzuzufügen.

    ![Schaltfläche „Neue Anwendung“][3]

4. Geben Sie im Suchfeld als Suchbegriff **Cornerstone OnDemand** ein.

    ![Cornerstone OnDemand-Bereitstellung](./media/cornerstone-ondemand-provisioning-tutorial/AppSearch.png)

5. Wählen Sie im Ergebnisbereich **Cornerstone OnDemand** aus, und klicken Sie dann auf die Schaltfläche **Hinzufügen**, um Cornerstone OnDemand zur Liste der SaaS-Anwendungen hinzuzufügen.

    ![Cornerstone OnDemand-Bereitstellung](./media/cornerstone-ondemand-provisioning-tutorial/AppSearchResults.png)

    ![Cornerstone OnDemand-Bereitstellung](./media/cornerstone-ondemand-provisioning-tutorial/AppCreation.png)

## <a name="assigning-users-to-cornerstone-ondemand"></a>Zuweisen von Benutzern zu Cornerstone OnDemand

Azure Active Directory ermittelt anhand von Zuweisungen, welche Benutzer Zugriff auf bestimmte Apps erhalten sollen. Im Kontext der automatischen Benutzerbereitstellung werden nur die Benutzer und/oder Gruppen synchronisiert, die einer Anwendung in Azure AD zugewiesen wurden. 

Vor dem Konfigurieren und Aktivieren der automatischen Benutzerbereitstellung müssen Sie entscheiden, welche Benutzer und/oder Gruppen in Azure AD Zugriff auf Cornerstone OnDemand benötigen. Anschließend können Sie diese Benutzer und/oder Gruppen Cornerstone OnDemand anhand der folgenden Anweisungen zuweisen:

*   [Zuweisen eines Benutzers oder einer Gruppe zu einer Unternehmens-App](../manage-apps/assign-user-or-group-access-portal.md)

### <a name="important-tips-for-assigning-users-to-cornerstone-ondemand"></a>Wichtige Tipps zum Zuweisen von Benutzern zu Cornerstone OnDemand

*   Es wird empfohlen, Cornerstone OnDemand einen einzelnen Azure AD-Benutzer zuzuweisen, um die Konfiguration der automatischen Benutzerbereitstellung zu testen. Später können weitere Benutzer und/oder Gruppen zugewiesen werden.

*   Beim Zuweisen eines Benutzers zu Cornerstone OnDemand müssen Sie eine gültige anwendungsspezifische Rolle (sofern verfügbar) im Dialogfeld für die Zuweisung auswählen. Benutzer mit der Rolle **Standardzugriff** werden von der Bereitstellung ausgeschlossen.

## <a name="configuring-automatic-user-provisioning-to-cornerstone-ondemand"></a>Konfigurieren der automatischen Benutzerbereitstellung für Cornerstone OnDemand

In diesem Abschnitt werden die Schritte zum Konfigurieren des Azure AD-Bereitstellungsdiensts zum Erstellen, Aktualisieren und Deaktivieren von Benutzern und/oder Gruppen in Cornerstone OnDemand auf der Grundlage von Benutzer- und/oder Gruppenzuweisungen in Azure AD erläutert.


### <a name="to-configure-automatic-user-provisioning-for-cornerstone-ondemand-in-azure-ad"></a>So konfigurieren Sie die automatische Benutzerbereitstellung für Cornerstone OnDemand in Azure AD


1. Melden Sie sich beim [Azure-Portal](https://portal.azure.com) an, und navigieren Sie zu **Azure Active Directory > Unternehmensanwendungen > Alle Anwendungen**.

2. Wählen Sie Cornerstone OnDemand in der Liste der SaaS-Anwendungen aus.
 
    ![Cornerstone OnDemand-Bereitstellung](./media/cornerstone-ondemand-provisioning-tutorial/Successcenter2.png)

3. Wählen Sie die Registerkarte **Bereitstellung**.

    ![Cornerstone OnDemand-Bereitstellung](./media/cornerstone-ondemand-provisioning-tutorial/ProvisioningTab.png)

4. Legen Sie den **Bereitstellungsmodus** auf **Automatisch** fest.

    ![Cornerstone OnDemand-Bereitstellung](./media/cornerstone-ondemand-provisioning-tutorial/ProvisioningCredentials.png)

5. Geben Sie im Abschnitt **Administratoranmeldeinformationen** die Werte für **Administratorbenutzername**, **Administratorkennwort** und **Domäne** Ihres Cornerstone OnDemand-Kontos ein.

    *   Geben Sie im Feld **Administratorbenutzername** den Domänen-/Benutzernamen des Administratorkontos im Cornerstone OnDemand-Mandanten ein. Beispiel: contoso\admin.

    *   Geben Sie im Feld **Administratorkennwort** das Kennwort für den Administratorbenutzernamen ein.

    *   Füllen Sie im Feld **Domäne** die Webdienst-URL des Cornerstone OnDemand-Mandanten auf. Beispiel: Der Dienst befindet sich unter `https://ws-[corpname].csod.com/feed30/clientdataservice.asmx`. Für Contoso lautet die Domäne `https://ws-contoso.csod.com/feed30/clientdataservice.asmx`. Weitere Informationen zum Abrufen der Webdienst-URL finden Sie [hier](https://help.csod.com/help/csod_0/Content/Resources/Documents/WebServices/CSOD_Web_Services_-_User-OU_Technical_Specification_v20160222.pdf).

6. Klicken Sie nach dem Auffüllen der in Schritt 5 gezeigten Felder auf **Verbindung testen**, um sicherzustellen, dass Azure AD eine Verbindung mit Cornerstone OnDemand herstellen kann. Wenn die Verbindung nicht möglich ist, stellen Sie sicher, dass Ihr Cornerstone OnDemand-Konto über Administratorberechtigungen verfügt, und wiederholen Sie den Vorgang.

    ![Cornerstone OnDemand-Bereitstellung](./media/cornerstone-ondemand-provisioning-tutorial/TestConnection.png)

7. Geben Sie im Feld **Benachrichtigungs-E-Mail** die E-Mail-Adresse einer Person oder einer Gruppe ein, die Benachrichtigungen zu Bereitstellungsfehlern erhalten soll, und aktivieren Sie das Kontrollkästchen **Bei Fehler E-Mail-Benachrichtigung senden**.

    ![Cornerstone OnDemand-Bereitstellung](./media/cornerstone-ondemand-provisioning-tutorial/EmailNotification.png)

8. Klicken Sie auf **Speichern**.

9. Wählen Sie im Abschnitt **Zuordnungen** die Option **Azure Active Directory-Benutzer mit Cornerstone OnDemand synchronisieren**.

    ![Cornerstone OnDemand-Bereitstellung](./media/cornerstone-ondemand-provisioning-tutorial/UserMapping.png)

10. Überprüfen Sie im Abschnitt **Attributzuordnungen** die Benutzerattribute, die von Azure AD mit Cornerstone OnDemand synchronisiert werden. Beachten Sie, dass die als **übereinstimmende** Eigenschaften ausgewählten Attribute für den Abgleich der Benutzerkonten in Cornerstone OnDemand für Updatevorgänge verwendet werden. Wählen Sie die Schaltfläche **Speichern**, um alle Änderungen zu übernehmen.

    ![Cornerstone OnDemand-Bereitstellung](./media/cornerstone-ondemand-provisioning-tutorial/UserMappingAttributes.png)

11. Wenn Sie Bereichsfilter konfigurieren möchten, lesen Sie die Anweisungen unter [Attributbasierte Anwendungsbereitstellung mit Bereichsfiltern](../manage-apps/define-conditional-rules-for-provisioning-user-accounts.md).

12. Um den Azure AD-Bereitstellungsdienst für Cornerstone OnDemand zu aktivieren, ändern Sie den **Bereitstellungsstatus** im Abschnitt **Einstellungen** in **Ein**.

    ![Cornerstone OnDemand-Bereitstellung](./media/cornerstone-ondemand-provisioning-tutorial/ProvisioningStatus.png)

13. Legen Sie die Benutzer und/oder Gruppen fest, die in Cornerstone OnDemand bereitgestellt werden sollen. Wählen Sie dazu im Abschnitt **Einstellungen** unter **Bereich** die gewünschten Werte aus.

    ![Cornerstone OnDemand-Bereitstellung](./media/cornerstone-ondemand-provisioning-tutorial/SyncScope.png)

14. Wenn Sie fertig sind, klicken Sie auf **Speichern**.

    ![Cornerstone OnDemand-Bereitstellung](./media/cornerstone-ondemand-provisioning-tutorial/Save.png)


Dadurch wird die Erstsynchronisierung aller Benutzer und/oder Gruppen gestartet, die im Abschnitt **Einstellungen** unter **Bereich** definiert sind. Die Erstsynchronisierung dauert länger als nachfolgende Synchronisierungen, die ungefähr alle 40 Minuten erfolgen, solange der Azure AD-Bereitstellungsdienst ausgeführt wird. Im Abschnitt **Synchronisierungsdetails** können Sie den Fortschritt überwachen und Links zu Berichten zur Bereitstellungsaktivität aufrufen. Darin sind alle Aktionen aufgeführt, die vom Azure AD-Bereitstellungsdienst in Cornerstone OnDemand ausgeführt werden.

Weitere Informationen zum Lesen von Azure AD-Bereitstellungsprotokollen finden Sie unter [Tutorial: Meldung zur automatischen Benutzerkontobereitstellung](../manage-apps/check-status-user-account-provisioning.md).
## <a name="connector-limitations"></a>Connector-Einschränkungen

* Das Cornerstone OnDemand-Attribut **Position** erwartet einen Wert, der den Rollen im Cornerstone OnDemand-Portal entspricht. Die Liste der gültigen **Position**-Werte kann abgerufen werden, indem Sie im Cornerstone OnDemand-Portal zu **Benutzerdatensatz bearbeiten > Organisationsstruktur > Position** navigieren.
    ![Cornerstone OnDemand-Bereitstellung: Benutzer bearbeiten](./media/cornerstone-ondemand-provisioning-tutorial/UserEdit.png) ![Cornerstone OnDemand-Bereitstellung: Position](./media/cornerstone-ondemand-provisioning-tutorial/UserPosition.png) ![Cornerstone OnDemand-Bereitstellung: Positionsliste](./media/cornerstone-ondemand-provisioning-tutorial/PostionId.png)
    
## <a name="additional-resources"></a>Zusätzliche Ressourcen

* [Verwalten der Benutzerkontobereitstellung für Unternehmens-Apps](../manage-apps/configure-automatic-user-provisioning-portal.md)
* [Was bedeuten Anwendungszugriff und einmaliges Anmelden mit Azure Active Directory?](../manage-apps/what-is-single-sign-on.md)



## <a name="next-steps"></a>Nächste Schritte

* [Erfahren Sie, wie Sie Protokolle überprüfen und Berichte zu Bereitstellungsaktivitäten abrufen.](../manage-apps/check-status-user-account-provisioning.md)

<!--Image references-->
[1]: ./media/cornerstone-ondemand-provisioning-tutorial/tutorial_general_01.png
[2]: ./media/cornerstone-ondemand-provisioning-tutorial/tutorial_general_02.png
[3]: ./media/cornerstone-ondemand-provisioning-tutorial/tutorial_general_03.png
