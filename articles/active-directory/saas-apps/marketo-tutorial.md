---
title: 'Tutorial: Azure Active Directory-Integration mit Marketo | Microsoft-Dokumentation'
description: Erfahren Sie, wie Sie das einmalige Anmelden zwischen Azure Active Directory und Marketo konfigurieren.
services: active-directory
documentationCenter: na
author: jeevansd
manager: daveba
ms.assetid: b88c45f5-d288-4717-835c-ca965add8735
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/09/2017
ms.author: jeedes
ms.openlocfilehash: dbdf66c71bf007b27751191d3818f8002a8c2614
ms.sourcegitcommit: d3200828266321847643f06c65a0698c4d6234da
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/29/2019
ms.locfileid: "55172560"
---
# <a name="tutorial-azure-active-directory-integration-with-marketo"></a>Tutorial: Azure Active Directory-Integration mit Marketo

In diesem Tutorial erfahren Sie, wie Sie Marketo in Azure Active Directory (Azure AD) integrieren.

Die Integration von Marketo in Azure AD bietet die folgenden Vorteile:

- Sie können in Azure AD steuern, wer Zugriff auf Marketo hat.
- Sie können es Benutzern ermöglichen, sich mit ihren Azure AD-Konten automatisch bei Marketo anzumelden (einmaliges Anmelden).
- Sie können Ihre Konten an einem zentralen Ort verwalten – im Azure-Portal.

Weitere Informationen zur Integration von SaaS-Apps in Azure AD finden Sie unter [Was bedeuten Anwendungszugriff und einmaliges Anmelden mit Azure Active Directory?](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Voraussetzungen

Um die Azure AD-Integration mit Marketo konfigurieren zu können, benötigen Sie Folgendes:

- Ein Azure AD-Abonnement
- Ein Marketo-Abonnement, für das einmaliges Anmelden aktiviert ist

> [!NOTE]
> Um die Schritte in diesem Tutorial zu testen, wird empfohlen, keine Produktionsumgebung zu verwenden.

Um die Schritte in diesem Tutorial zu testen, sollten Sie folgende Empfehlungen beachten:

- Verwenden Sie die Produktionsumgebung nur, wenn dies unbedingt erforderlich ist.
- Wenn Sie keine Azure AD-Testumgebung haben, können Sie [hier](https://azure.microsoft.com/pricing/free-trial/)eine einmonatige Testversion anfordern.

## <a name="scenario-description"></a>Beschreibung des Szenarios
In diesem Tutorial testen Sie das einmalige Anmelden für Azure AD in einer Testumgebung. Das in diesem Tutorial beschriebene Szenario besteht aus zwei Hauptbestandteilen:

1. Hinzufügen von Marketo aus dem Katalog
1. Konfigurieren und Testen der einmaligen Anmeldung von Azure AD

## <a name="adding-marketo-from-the-gallery"></a>Hinzufügen von Marketo aus dem Katalog
Zum Konfigurieren der Integration von Marketo in Azure AD müssen Sie Marketo aus dem Katalog der Liste der verwalteten SaaS-Apps hinzufügen.

**Um Marketo aus dem Katalog hinzuzufügen, führen Sie die folgenden Schritte aus:**

1. Klicken Sie im linken Navigationsbereich des **[Azure-Portals](https://portal.azure.com)** auf das Symbol für **Azure Active Directory**. 

    ![Active Directory][1]

1. Navigieren Sie zu **Unternehmensanwendungen**. Wechseln Sie dann zu **Alle Anwendungen**.

    ![ANWENDUNGEN][2]
    
1. Klicken Sie oben im Dialogfeld auf die Schaltfläche **Neue Anwendung**, um eine neue Anwendung hinzuzufügen.

    ![ANWENDUNGEN][3]

1. Geben Sie im Suchfeld **Marketo**ein.

    ![Erstellen eines Azure AD-Testbenutzers](./media/marketo-tutorial/tutorial_marketo_search.png)

1. Wählen Sie im Ergebnisbereich die Option **Marketo** aus, und klicken Sie dann auf die Schaltfläche **Hinzufügen**, um die Anwendung hinzuzufügen.

    ![Erstellen eines Azure AD-Testbenutzers](./media/marketo-tutorial/tutorial_marketo_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurieren und Testen der einmaligen Anmeldung von Azure AD
In diesem Abschnitt konfigurieren und testen Sie anhand eines Testbenutzers namens Britta Simon das einmalige Anmelden von Azure AD mit Marketo.

Für das einmalige Anmelden muss Azure AD wissen, welcher Benutzer in Marketo als Gegenstück für einen Benutzer in Azure AD fungiert. Anders ausgedrückt: Zwischen einem Azure AD-Benutzer und dem entsprechenden Benutzer in Marketo muss eine Linkbeziehung eingerichtet werden.

Weisen Sie in Marketo den Wert für **Benutzername** in Azure AD als Wert für **Benutzername** zu, um eine Linkbeziehung herzustellen.

Zum Konfigurieren und Testen des einmaligen Anmeldens in Azure AD bei Marketo müssen Sie die folgenden Bausteine ausführen:

1. **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**, um Ihren Benutzern das Verwenden dieser Funktion zu ermöglichen.
1. **[Erstellen eines Azure AD-Testbenutzers](#creating-an-azure-ad-test-user)** , um das einmalige Anmelden von Azure AD mit der Testbenutzerin Britta Simon zu testen.
1. **[Erstellen eines Marketo-Testbenutzers](#creating-a-marketo-test-user)**, um eine Entsprechung von Britta Simon in Marketo zu erhalten, die mit ihrer Darstellung in Azure AD verknüpft ist.
1. **[Zuweisen des Azure AD-Testbenutzers](#assigning-the-azure-ad-test-user)**, um Britta Simon für das einmalige Anmelden von Azure AD zu aktivieren.
1. **[Testing Single Sign-On](#testing-single-sign-on)** , um zu überprüfen, ob die Konfiguration funktioniert.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfigurieren des einmaligen Anmeldens von Azure AD

In diesem Abschnitt ermöglichen Sie das einmalige Anmelden von Azure AD im Azure-Portal und konfigurieren das einmalige Anmelden in Ihrer Marketo-Anwendung.

**Führen Sie zum Konfigurieren des einmaligen Anmeldens von Azure AD bei Marketo die folgenden Schritte aus:**

1. Klicken Sie im Azure-Portal auf der Anwendungsintegrationsseite für **Marketo** auf **Einmaliges Anmelden**.

    ![Configure single sign-on][4]

1. Wählen Sie im Dialogfeld **Einmaliges Anmelden** als **Modus** die Option **SAML-basierte Anmeldung** aus, um einmaliges Anmelden zu aktivieren.
 
    ![Configure single sign-on](./media/marketo-tutorial/tutorial_marketo_samlbase.png)

1. Führen Sie auf der Seite **Domäne und URLs für Marketo** die folgenden Schritte aus:

    ![Configure single sign-on](./media/marketo-tutorial/tutorial_marketo_url.png)

    a. Geben Sie im Textfeld **Bezeichner** eine URL nach folgendem Muster ein: `https://saml.marketo.com/sp`

    b. Geben Sie im Textfeld **Antwort-URL** eine URL nach folgendem Muster ein: `https://login.marketo.com/saml/assertion/\<munchkinid\>`

    > [!NOTE] 
    > Hierbei handelt es sich um Beispielwerte. Aktualisieren Sie diese Werte mit dem eigentlichen Bezeichner und der Antwort-URL. Wenden Sie sich an das [Supportteam von Marketo](http://investors.marketo.com/contactus.cfm), um diese Werte zu erhalten.
 
1. Klicken Sie im Abschnitt **SAML-Signaturzertifikat** auf **Zertifikat (Base64)**, und speichern Sie die Zertifikatdatei auf Ihrem Computer.

    ![Configure single sign-on](./media/marketo-tutorial/tutorial_marketo_certificate.png) 

1. Klicken Sie auf die Schaltfläche **Save** .

    ![Configure single sign-on](./media/marketo-tutorial/tutorial_general_400.png)

1. Klicken Sie im Abschnitt **Marketo-Konfiguration** auf **Marketo konfigurieren**, um das Fenster **Anmeldung konfigurieren** zu öffnen. Kopieren Sie die **Abmelde-URL, die SAML-Entitäts-ID und die URL für den SAML-SSO-Dienst** aus dem Abschnitt **Kurzübersicht**.

    ![Configure single sign-on](./media/marketo-tutorial/tutorial_marketo_configure.png) 

1. Um die Munchkin-ID Ihrer Anwendung zu erhalten, melden Sie sich mit Ihren Administratoranmeldeinformationen bei Marketo an und führen Sie folgende Aktionen aus:
   
    a. Melden Sie sich mit Ihren Administratoranmeldeinformationen bei der Marketo-App an.
   
    b. Klicken Sie auf die Schaltfläche **Admin** im oberen Navigationsbereich.
   
    ![Configure single sign-on](./media/marketo-tutorial/tutorial_marketo_06.png) 
   
    c. Navigieren Sie zum Menü „Integration“, und klicken Sie auf den **Munchkin-Link**.
   
    ![Configure single sign-on](./media/marketo-tutorial/tutorial_marketo_11.png)
   
    d. Kopieren Sie die Munchkin-ID, die auf dem Bildschirm angezeigt wird, und schließen Sie Ihre Antwort-URL im Azure AD-Konfigurations-Assistenten ab.
   
    ![Configure single sign-on](./media/marketo-tutorial/tutorial_marketo_12.png) 

1. Führen Sie die unten beschriebenen Schritte aus, um SSO in der Anwendung zu konfigurieren:
   
    a. Melden Sie sich mit Ihren Administratoranmeldeinformationen bei der Marketo-App an.
   
    b. Klicken Sie auf die Schaltfläche **Admin** im oberen Navigationsbereich.
   
    ![Configure single sign-on](./media/marketo-tutorial/tutorial_marketo_06.png) 
   
    c. Navigieren Sie zum Menü „Integration“, und klicken Sie auf **Einmaliges Anmelden**.
   
    ![Configure single sign-on](./media/marketo-tutorial/tutorial_marketo_07.png) 
   
    d. Klicken zum Aktivieren der SAML-Einstellungen auf die Schaltfläche **Bearbeiten**.
   
    ![Configure single sign-on](./media/marketo-tutorial/tutorial_marketo_08.png) 
   
    e. **Aktivieren** Sie die Einstellungen für einmaliges Anmelden.
   
    f. Fügen Sie die **SAML-Entitäts-ID** in das Textfeld **Entitäts-ID** ein.
   
    g. Geben Sie die URL als `http://saml.marketo.com/sp` in das Textfeld **Entitäts-ID** ein.
   
    h. Wählen Sie den Speicherort der Benutzer-ID als **Namensbezeichnerelement** aus.
   
    ![Configure single sign-on](./media/marketo-tutorial/tutorial_marketo_09.png)
   
    > [!NOTE]
    > Wenn Ihre Benutzer-ID kein UPN-Wert ist, ändern Sie den Wert in der Registerkarte „Attribut“.
   
    i. Laden Sie das Zertifikat hoch, das Sie aus dem Azure AD-Konfigurations-Assistenten heruntergeladen haben. **Speichern** Sie die Einstellungen.
   
    j. Bearbeiten Sie die Einstellungen für Seitenumleitungen.
   
    k. Fügen Sie die **URL für den SAML-SSO-Dienst** in das Textfeld **Anmelde-URL** ein.
   
    l. Fügen Sie die **Abmelde-URL** in das Textfeld **Abmelde-URL** ein.
   
    m. Kopieren Sie in der **Fehler-URL** die **URL Ihrer Marketo-Instanz**, und klicken Sie auf die Schaltfläche **Speichern**, um die Einstellungen zu speichern.
   
    ![Configure single sign-on](./media/marketo-tutorial/tutorial_marketo_10.png)

1. Um SSO für Benutzer zu aktivieren, führen Sie die folgenden Aktionen aus:
   
    a. Melden Sie sich mit Ihren Administratoranmeldeinformationen bei der Marketo-App an.
   
    b. Klicken Sie auf die Schaltfläche **Admin** im oberen Navigationsbereich.
   
    ![Configure single sign-on](./media/marketo-tutorial/tutorial_marketo_06.png) 
   
    c. Navigieren Sie zum Menü **Sicherheit**, und klicken Sie auf **Anmeldeeinstellungen**.
   
    ![Configure single sign-on](./media/marketo-tutorial/tutorial_marketo_13.png)
   
    d. Aktivieren Sie die Option **SSO erfordern**, und **speichern** Sie die Einstellungen.
   
    ![Configure single sign-on](./media/marketo-tutorial/tutorial_marketo_14.png)

> [!TIP]
> Während der Einrichtung der App können Sie im [Azure-Portal](https://portal.azure.com) nun eine Kurzfassung dieser Anweisungen lesen.  Nachdem Sie diese App aus dem Abschnitt **Active Directory > Unternehmensanwendungen** heruntergeladen haben, klicken Sie einfach auf die Registerkarte **Einmaliges Anmelden**, und rufen Sie die eingebettete Dokumentation über den Abschnitt **Konfiguration** um unteren Rand der Registerkarte auf. Weitere Informationen zur eingebetteten Dokumentation finden Sie hier: [Dokumentation zu eingebettetem Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="creating-an-azure-ad-test-user"></a>Erstellen eines Azure AD-Testbenutzers
Das Ziel dieses Abschnitts ist das Erstellen eines Testbenutzers namens Britta Simon im Azure-Portal.

![Azure AD-Benutzer erstellen][100]

**Um einen Testbenutzer in Azure AD zu erstellen, führen Sie die folgenden Schritte aus:**

1. Klicken Sie im linken Navigationsbereich des **Azure-Portals** auf das Symbol für **Azure Active Directory**.

    ![Erstellen eines Azure AD-Testbenutzers](./media/marketo-tutorial/create_aaduser_01.png) 

1. Wechseln Sie zu **Benutzer und Gruppen**, und klicken Sie auf **Alle Benutzer**, um die Liste der Benutzer anzuzeigen.
    
    ![Erstellen eines Azure AD-Testbenutzers](./media/marketo-tutorial/create_aaduser_02.png) 

1. Klicken Sie oben im Dialogfeld auf **Hinzufügen**, um das Dialogfeld **Benutzer** zu öffnen.
 
    ![Erstellen eines Azure AD-Testbenutzers](./media/marketo-tutorial/create_aaduser_03.png) 

1. Führen Sie auf der Dialogfeldseite **Benutzer** die folgenden Schritte aus:
 
    ![Erstellen eines Azure AD-Testbenutzers](./media/marketo-tutorial/create_aaduser_04.png) 

    a. Geben Sie in das Textfeld **Name** den Namen **BrittaSimon** ein.

    b. Geben Sie in das Textfeld **Benutzername** die **E-Mail-Adresse** von Britta Simon ein.

    c. Wählen Sie **Kennwort anzeigen** aus, und notieren Sie sich den Wert des **Kennworts**.

    d. Klicken Sie auf **Create**.
 
### <a name="creating-a-marketo-test-user"></a>Erstellen eines Marketo-Testbenutzers

In diesem Abschnitt erstellen Sie in Marketo einen Benutzer namens Britta Simon. Befolgen Sie diese Schritte, um einen Benutzer in der Marketo-Plattform zu erstellen.

1. Melden Sie sich mit Ihren Administratoranmeldeinformationen bei der Marketo-App an.

1. Klicken Sie auf die Schaltfläche **Admin** im oberen Navigationsbereich.
   
    ![Configure single sign-on](./media/marketo-tutorial/tutorial_marketo_06.png) 

1. Navigieren Sie zum Menü **Sicherheit**, und klicken Sie auf **Benutzer und Rollen**
   
    ![Configure single sign-on](./media/marketo-tutorial/tutorial_marketo_19.png)  

1. Klicken Sie auf der Registerkarte „Benutzer“ auf den Link **Neuen Benutzer einladen**.
   
    ![Configure single sign-on](./media/marketo-tutorial/tutorial_marketo_15.png) 

1. Geben Sie die folgenden Informationen im Assistenten zum Einladen neuer Benutzer ein.
   
    a. Geben Sie die **E-Mail** -Adresse des Benutzers in das Textfeld ein.
   
    ![Configure single sign-on](./media/marketo-tutorial/tutorial_marketo_16.png)
   
    b. Geben Sie den **Vornamen** in das Textfeld ein.
   
    c. Geben Sie den **Nachnamen** in das Textfeld ein.
   
    d. Klicken Sie unten auf der Seite auf **Weiter**

1. Wählen Sie auf der Registerkarte **Berechtigungen** die Option **userRoles** aus, und klicken Sie auf **Weiter**.
   
    ![Configure single sign-on](./media/marketo-tutorial/tutorial_marketo_17.png)
1. Klicken Sie auf die Schaltfläche **Senden**, um die Benutzereinladung zu senden.
   
    ![Configure single sign-on](./media/marketo-tutorial/tutorial_marketo_18.png)

1. Der Benutzer erhält die E-Mail-Benachrichtigung und muss auf den Link klicken sowie das Kennwort ändern, um das Konto zu aktivieren. 

### <a name="assigning-the-azure-ad-test-user"></a>Zuweisen des Azure AD-Testbenutzers

In diesem Abschnitt ermöglichen Sie Britta Simon das einmalige Anmelden bei Azure, indem Sie Zugriff auf Marketo gewähren.

![Benutzer zuweisen][200] 

**Um Britta Simon Marketo zuzuweisen, führen Sie die folgenden Schritte aus:**

1. Öffnen Sie im Azure-Portal die Anwendungsansicht, navigieren Sie zur Verzeichnisansicht, wechseln Sie dann zu **Unternehmensanwendungen**, und klicken Sie auf **Alle Anwendungen**.

    ![Benutzer zuweisen][201] 

1. Wählen Sie in der Anwendungsliste **Marketo**aus.

    ![Configure single sign-on](./media/marketo-tutorial/tutorial_marketo_app.png) 

1. Klicken Sie im Menü auf der linken Seite auf **Benutzer und Gruppen**.

    ![Benutzer zuweisen][202] 

1. Klicken Sie auf die Schaltfläche **Hinzufügen**. Wählen Sie dann im Dialogfeld **Zuweisung hinzufügen** die Option **Benutzer und Gruppen** aus.

    ![Benutzer zuweisen][203]

1. Wählen Sie im Dialogfeld **Benutzer und Gruppen** in der Benutzerliste **Britta Simon** aus.

1. Klicken Sie im Dialogfeld **Benutzer und Gruppen** auf die Schaltfläche **Auswählen**.

1. Klicken Sie im Dialogfeld **Zuweisung hinzufügen** auf **Zuweisen**.
    
### <a name="testing-single-sign-on"></a>Testen der einmaligen Anmeldung

In diesem Abschnitt testen Sie die Azure AD-Konfiguration für einmaliges Anmelden über den Zugriffsbereich.

Wenn Sie im Zugriffsbereich auf die Kachel „Marketo“ klicken, sollten Sie automatisch bei Ihrer Marketo-Anwendung angemeldet werden.

## <a name="additional-resources"></a>Zusätzliche Ressourcen

* [Liste der Tutorials zur Integration von SaaS-Apps in Azure Active Directory](tutorial-list.md)
* [Was bedeuten Anwendungszugriff und einmaliges Anmelden mit Azure Active Directory?](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/marketo-tutorial/tutorial_general_01.png
[2]: ./media/marketo-tutorial/tutorial_general_02.png
[3]: ./media/marketo-tutorial/tutorial_general_03.png
[4]: ./media/marketo-tutorial/tutorial_general_04.png

[100]: ./media/marketo-tutorial/tutorial_general_100.png

[200]: ./media/marketo-tutorial/tutorial_general_200.png
[201]: ./media/marketo-tutorial/tutorial_general_201.png
[202]: ./media/marketo-tutorial/tutorial_general_202.png
[203]: ./media/marketo-tutorial/tutorial_general_203.png

