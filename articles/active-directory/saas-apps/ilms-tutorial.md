---
title: 'Tutorial: Azure Active Directory-Integration mit iLMS | Microsoft-Dokumentation'
description: Erfahren Sie, wie Sie das einmalige Anmelden zwischen Azure Active Directory und iLMS konfigurieren.
services: active-directory
documentationCenter: na
author: jeevansd
manager: daveba
ms.assetid: d6e11639-6cea-48c9-b008-246cf686e726
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/13/2017
ms.author: jeedes
ms.openlocfilehash: 0a1de782b3b4502107c14282bdd4ce5ef2caa871
ms.sourcegitcommit: d3200828266321847643f06c65a0698c4d6234da
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/29/2019
ms.locfileid: "55165913"
---
# <a name="tutorial-azure-active-directory-integration-with-ilms"></a>Tutorial: Azure Active Directory-Integration in iLMS

In diesem Tutorial erfahren Sie, wie Sie iLMS in Azure Active Directory (Azure AD) integrieren.

Die Integration von iLMS in Azure AD bietet die folgenden Vorteile:

- Sie können in Azure AD steuern, wer Zugriff auf iLMS hat.
- Sie können es Benutzern ermöglichen, sich mit ihren Azure AD-Konten automatisch bei iLMS anzumelden (einmaliges Anmelden, Single Sign-On).
- Sie können Ihre Konten an einem zentralen Ort verwalten – im Azure-Portal.

Weitere Informationen zur Integration von SaaS-Apps in Azure AD finden Sie unter [Was bedeuten Anwendungszugriff und einmaliges Anmelden mit Azure Active Directory?](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Voraussetzungen

Um die Azure AD-Integration mit iLMS konfigurieren zu können, benötigen Sie Folgendes:

- Ein Azure AD-Abonnement
- Ein iLMS-Abonnement, das für das einmalige Anmelden aktiviert ist

> [!NOTE]
> Um die Schritte in diesem Tutorial zu testen, wird empfohlen, keine Produktionsumgebung zu verwenden.

Um die Schritte in diesem Tutorial zu testen, sollten Sie folgende Empfehlungen beachten:

- Sie sollten keine Produktionsumgebung verwenden, sofern dies nicht erforderlich ist.
- Wenn Sie keine Azure AD-Testumgebung haben, können Sie [hier](https://azure.microsoft.com/pricing/free-trial/)eine einmonatige Testversion anfordern.

## <a name="scenario-description"></a>Beschreibung des Szenarios
In diesem Tutorial testen Sie das einmalige Anmelden für Azure AD in einer Testumgebung. Das in diesem Tutorial beschriebene Szenario besteht aus zwei Hauptbestandteilen:

1. Hinzufügen von iLMS aus dem Katalog
1. Konfigurieren und Testen der einmaligen Anmeldung von Azure AD

## <a name="adding-ilms-from-the-gallery"></a>Hinzufügen von iLMS aus dem Katalog
Zum Konfigurieren der Integration von iLMS in Azure AD müssen Sie iLMS aus dem Katalog zur Liste mit den verwalteten SaaS-Apps hinzufügen.

**Um iLMS aus dem Katalog hinzuzufügen, führen Sie die folgenden Schritte aus:**

1. Klicken Sie im linken Navigationsbereich des **[Azure-Portals](https://portal.azure.com)** auf das Symbol für **Azure Active Directory**. 

    ![Active Directory][1]

1. Navigieren Sie zu **Unternehmensanwendungen**. Wechseln Sie dann zu **Alle Anwendungen**.

    ![ANWENDUNGEN][2]
    
1. Klicken Sie oben im Dialogfeld auf die Schaltfläche **Neue Anwendung**, um eine neue Anwendung hinzuzufügen.

    ![ANWENDUNGEN][3]

1. Geben Sie im Suchfeld den Suchbegriff **iLMS** ein.

    ![Erstellen eines Azure AD-Testbenutzers](./media/ilms-tutorial/tutorial_ilms_search.png)

1. Wählen Sie im Ergebnisbereich die Option **iLMS** aus, und klicken Sie dann auf die Schaltfläche **Hinzufügen**, um die Anwendung hinzuzufügen.

    ![Erstellen eines Azure AD-Testbenutzers](./media/ilms-tutorial/tutorial_ilms_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurieren und Testen der einmaligen Anmeldung von Azure AD
In diesem Abschnitt konfigurieren und testen Sie das einmalige Anmelden von Azure AD bei iLMS basierend auf einer Testbenutzerin mit dem Namen Britta Simon.

Damit das einmalige Anmelden funktioniert, muss Azure AD wissen, welcher Benutzer in iLMS als Gegenstück zu einem Benutzer in Azure AD fungiert. Anders ausgedrückt: Zwischen einem Azure AD-Benutzer und dem entsprechenden Benutzer in iLMS muss eine Linkbeziehung eingerichtet werden.

Diese Linkbeziehung wird hergestellt, indem Sie den Wert für den **Benutzernamen** in Azure AD als Wert für den **Benutzernamen** in iLMS zuweisen.

Zum Konfigurieren und Testen des einmaligen Anmeldens von Azure AD bei iLMS müssen Sie die folgenden Bausteine ausführen:

1. **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**, um Ihren Benutzern das Verwenden dieser Funktion zu ermöglichen.
1. **[Erstellen eines Azure AD-Testbenutzers](#creating-an-azure-ad-test-user)** , um das einmalige Anmelden von Azure AD mit der Testbenutzerin Britta Simon zu testen.
1. **[Erstellen eines iLMS-Testbenutzers](#creating-an-ilms-test-user)**, um eine Entsprechung von Britta Simon in iLMS zu erhalten, die mit ihrer Darstellung in Azure AD verknüpft ist.
1. **[Zuweisen des Azure AD-Testbenutzers](#assigning-the-azure-ad-test-user)**, um Britta Simon für das einmalige Anmelden von Azure AD zu aktivieren.
1. **[Testing Single Sign-On](#testing-single-sign-on)** , um zu überprüfen, ob die Konfiguration funktioniert.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfigurieren des einmaligen Anmeldens von Azure AD

In diesem Abschnitt aktivieren Sie das einmalige Anmelden von Azure AD im Azure-Portal und konfigurieren das einmalige Anmelden in Ihrer iLMS-Anwendung.

**Führen Sie zum Konfigurieren des einmaligen Anmeldens von Azure AD in iLMS die folgenden Schritte aus:**

1. Klicken Sie im Azure-Portal auf der Anwendungsintegrationsseite für **iLMS** auf **Einmaliges Anmelden**.

    ![Configure single sign-on][4]

1. Wählen Sie im Dialogfeld **Einmaliges Anmelden** als **Modus** die Option **SAML-basierte Anmeldung** aus, um einmaliges Anmelden zu aktivieren.
 
    ![Configure single sign-on](./media/ilms-tutorial/tutorial_ilms_samlbase.png)

1. Führen Sie im Abschnitt **Domäne und URLs für iLMS** die folgenden Schritte aus, wenn Sie die Anwendung im **IDP-initiierten Modus** konfigurieren möchten:

    ![Configure single sign-on](./media/ilms-tutorial/tutorial_ilms_url.png)

    a. Fügen Sie im Textfeld**Bezeichner** den Wert ein, den Sie im iLMS-Verwaltungsportal im Abschnitt **Service Provider** der SAML-Einstellungen aus dem Feld **Identifier** kopieren.

    b. Fügen Sie im Textfeld **Antwort-URL** den Wert ein, den Sie im iLMS-Verwaltungsportal im Abschnitt **Service Provider** der SAML-Einstellungen aus dem Feld **Endpoint (URL)** kopieren. Der Wert weist folgendes Muster auf: `https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`.

    >[!Note]
    >Hinweis: Der Wert „123456“ ist nur ein Beispiel für einen Bezeichner.

1. Aktivieren Sie **Erweiterte URL-Einstellungen anzeigen**, wenn Sie die Anwendung im **SP-initiierten Modus** konfigurieren möchten:

    ![Configure single sign-on](./media/ilms-tutorial/tutorial_ilms_url1.png)

    Fügen Sie im Textfeld **Anmelde-URL** den Wert ein, den Sie im iLMS-Verwaltungsportal im Abschnitt **Service Provider** der SAML-Einstellungen aus dem Feld **Endpoint (URL)** kopieren. Der Wert weist folgendes Muster auf: `https://www.inspiredlms.com/Login/<instanceName>/consumer.aspx`.     

1. Um die JIT-Bereitstellung zu aktivieren, erwartet Ihre iLMS-Anwendung die SAML-Assertions in einem bestimmten Format. Konfigurieren Sie die folgenden Ansprüche für diese Anwendung. Sie können die Werte dieser Attribute im Abschnitt **Benutzerattribute** auf der Anwendungsintegrationsseite verwalten. Der folgende Screenshot zeigt ein Beispiel für diese Attributzuordnungen:
    
    ![Configure single sign-on](./media/ilms-tutorial/4.png)
    
    Erstellen Sie die Attribute **department, region** und **division**, und fügen Sie die Namen dieser Attribute in iLMS hinzu. Alle oben gezeigten Attribute sind erforderlich.  

    > [!NOTE] 
    > Sie müssen die Option **Create Un-recognized User Account** in iLMS aktivieren, um diese Attribute zuzuordnen. Befolgen Sie die Anweisungen [hier](http://support.inspiredelearning.com/customer/portal/articles/2204526), um eine Vorstellung von der Konfiguration der Attribute zu erhalten.

1. Konfigurieren Sie das SAML-Tokenattribut im Dialogfeld **Einmaliges Anmelden** im Abschnitt **Benutzerattribute**, wie im obigen Bild gezeigt, und führen Sie die folgenden Schritte aus:
    
    | Attributname | Attributwert |
    | ---------------| --------------- |    
    | division | user.department |
    | region | user.state |
    | department | user.jobtitle |

    a. Klicken Sie auf **Attribut hinzufügen**, um das Dialogfeld **Benutzerattribut hinzufügen** zu öffnen.

    ![Configure single sign-on](./media/ilms-tutorial/tutorial_ilms_04.png)

    ![Configure single sign-on](./media/ilms-tutorial/tutorial_ilms_05.png)
    
    b. Geben Sie im Textfeld **Name** den für die Zeile angezeigten Attributnamen ein.
    
    c. Geben Sie in der Liste **Wert** den für diese Zeile angezeigten Wert ein.
    
    d. Klicken Sie auf **OK**.

1. Klicken Sie im Abschnitt **SAML-Signaturzertifikat** auf **Metadaten-XML**, und speichern Sie die XML-Datei dann auf Ihrem Computer.

    ![Configure single sign-on](./media/ilms-tutorial/tutorial_ilms_certificate.png) 

1. Klicken Sie auf die Schaltfläche **Save** .

    ![Configure single sign-on](./media/ilms-tutorial/tutorial_general_400.png)

1. Melden Sie sich in einem anderen Webbrowserfenster im **iLMS-Verwaltungsportal** als Administrator an.

1. Klicken Sie auf der Registerkarte **Settings** auf **SSO:SAML**, um die SAML-Einstellungen zu öffnen, und führen Sie die folgenden Schritte aus:
    
    ![Configure single sign-on](./media/ilms-tutorial/1.png) 

    a. Erweitern Sie den Abschnitt **Service Provider**, und kopieren Sie die Werte für **Identifier** und **Endpoint (URL)**.

    ![Configure single sign-on](./media/ilms-tutorial/2.png) 

    b. Klicken Sie im Abschnitt **Identity Provider** auf **Import Metadata**.
    
    c. Wählen Sie die Datei mit **Metadaten**, die Sie aus dem Abschnitt **SAML-Signaturzertifikat** des Azure-Portals heruntergeladen haben.

    ![Configure single sign-on](./media/ilms-tutorial/tutorial_ilms_ssoconfig1.png) 

    d. Wenn Sie die JIT-Bereitstellung aktivieren möchten, um iLMS-Konten für unbekannte Benutzer zu erstellen, führen Sie die folgenden Schritte aus:
        
       - Aktivieren Sie das Kontrollkästchen **Create Un-recognized User Account**.
       
       ![Configure Single Sign-On](./media/ilms-tutorial/tutorial_ilms_ssoconfig2.png)

       -  Ordnen Sie die Attribute in Azure AD den Attributen in iLMS zu. Geben Sie in der Spalte mit den Attributen den Attributnamen oder den Standardwert an.

    e. Wechseln Sie zur Registerkarte **Business Rules**, und führen Sie die folgenden Schritte aus: 
        
       ![Configure Single Sign-On](./media/ilms-tutorial/5.png)

       - Aktivieren Sie das Kontrollkästchen **Create Un-recognized Regions, Divisions and Departments**, um Regionen, Sparten und Abteilungen zu erstellen, die zum Zeitpunkt des einmaligen Anmeldens noch nicht vorhanden waren.
        
       - Aktivieren Sie das Kontrollkästchen **Update User Profile During Sign-in**, um anzugeben, ob das Benutzerprofil bei jedem einmaligen Anmelden aktualisiert werden soll. 
        
       - Wenn das Kontrollkästchen **Update Blank Values for Non Mandatory Fields in User Profile** aktiviert ist, führen optionale Felder im Profil, die während des Anmeldevorgangs leer sind, dazu, dass das iLMS-Profil für diese Felder ebenfalls leere Werte enthält.
        
       - Aktivieren Sie das Kontrollkästchen **Send Error Notification Email**, und geben Sie die E-Mail-Adresse des Benutzers ein, der bei Fehlern Benachrichtigungs-E-Mails erhalten soll.

1. Klicken Sie auf die Schaltfläche **Save**, um die Änderungen zu speichern.

    ![Configure single sign-on](./media/ilms-tutorial/save.png)

> [!TIP]
> Während der Einrichtung der App können Sie im [Azure-Portal](https://portal.azure.com) nun eine Kurzfassung dieser Anweisungen lesen.  Nachdem Sie diese App aus dem Abschnitt **Active Directory > Unternehmensanwendungen** heruntergeladen haben, klicken Sie einfach auf die Registerkarte **Einmaliges Anmelden**, und rufen Sie die eingebettete Dokumentation über den Abschnitt **Konfiguration** um unteren Rand der Registerkarte auf. Weitere Informationen zur eingebetteten Dokumentation finden Sie hier: [Dokumentation zu eingebettetem Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
    
### <a name="creating-an-azure-ad-test-user"></a>Erstellen eines Azure AD-Testbenutzers
Das Ziel dieses Abschnitts ist das Erstellen eines Testbenutzers namens Britta Simon im Azure-Portal.

![Azure AD-Benutzer erstellen][100]

**Um einen Testbenutzer in Azure AD zu erstellen, führen Sie die folgenden Schritte aus:**

1. Klicken Sie im linken Navigationsbereich des **Azure-Portals** auf das Symbol für **Azure Active Directory**.

    ![Erstellen eines Azure AD-Testbenutzers](./media/ilms-tutorial/create_aaduser_01.png) 

1. Wechseln Sie zu **Benutzer und Gruppen**, und klicken Sie auf **Alle Benutzer**, um die Liste der Benutzer anzuzeigen.
    
    ![Erstellen eines Azure AD-Testbenutzers](./media/ilms-tutorial/create_aaduser_02.png) 

1. Klicken Sie oben im Dialogfeld auf **Hinzufügen**, um das Dialogfeld **Benutzer** zu öffnen.
 
    ![Erstellen eines Azure AD-Testbenutzers](./media/ilms-tutorial/create_aaduser_03.png) 

1. Führen Sie auf der Dialogfeldseite **Benutzer** die folgenden Schritte aus:
 
    ![Erstellen eines Azure AD-Testbenutzers](./media/ilms-tutorial/create_aaduser_04.png) 

    a. Geben Sie in das Textfeld **Name** den Namen **BrittaSimon** ein.

    b. Geben Sie in das Textfeld **Benutzername** die **E-Mail-Adresse** von Britta Simon ein.

    c. Wählen Sie **Kennwort anzeigen** aus, und notieren Sie sich den Wert des **Kennworts**.

    d. Klicken Sie auf **Create**.
 
### <a name="creating-an-ilms-test-user"></a>Erstellen eines iLMS-Testbenutzers

Die Anwendung unterstützt die Just-in-Time-Benutzerbereitstellung (JIT). Nach der Authentifizierung werden Benutzer in der Anwendung automatisch erstellt. JIT funktioniert, wenn Sie während der Konfiguration der SAML-Einstellungen im iLMS-Verwaltungsportal das Kontrollkästchen **Create Un-recognized User Account** aktiviert haben.

Wenn Sie manuell einen Benutzer erstellen müssen, führen Sie die folgenden Schritte aus:

1. Melden Sie sich bei der iLMS-Unternehmenswebsite als Administrator an.

1. Klicken Sie auf der Registerkarte **Users** auf **Register User**, um die Seite **Register User** zu öffnen. 
   
   ![Mitarbeiter hinzufügen](./media/ilms-tutorial/3.png)

1. Führen Sie auf der Seite **Register User** die folgenden Schritte aus.

    ![Mitarbeiter hinzufügen](./media/ilms-tutorial/create_testuser_add.png)

    a. Geben Sie im Textfeld **First Name** den Vornamen ein, z.B. Britta.
   
    b. Geben Sie im Textfeld **Last Name** den Nachnamen ein, z.B. Simon.

    c. Geben Sie im Textfeld **Email ID** die E-Mail-Adresse des Kontos von Britta Simon ein.

    d. Wählen Sie in der Dropdownliste **Region** den Wert für die Region aus.

    e. Wählen Sie in der Dropdownliste **Division** den Wert für die Sparte aus.

    f. Wählen Sie in der Dropdownliste **Department** den Wert für die Abteilung aus.

    g. Klicken Sie auf **Speichern**.

    > [!NOTE] 
    > Sie können eine Registrierungs-E-Mail an den Benutzer senden, indem Sie das Kontrollkästchen **Send Registration Mail** aktivieren.

### <a name="assigning-the-azure-ad-test-user"></a>Zuweisen des Azure AD-Testbenutzers

In diesem Abschnitt ermöglichen Sie Britta Simon die Verwendung des einmaligen Anmeldens von Azure, indem Sie ihr Zugriff auf iLMS gewähren.

![Benutzer zuweisen][200] 

**Um Britta Simon zu iLMS zuzuweisen, führen Sie die folgenden Schritte aus:**

1. Öffnen Sie im Azure-Portal die Anwendungsansicht, navigieren Sie zur Verzeichnisansicht, wechseln Sie dann zu **Unternehmensanwendungen**, und klicken Sie auf **Alle Anwendungen**.

    ![Benutzer zuweisen][201] 

1. Wählen Sie in der Anwendungsliste **iLMS** aus.

    ![Configure single sign-on](./media/ilms-tutorial/tutorial_ilms_app.png) 

1. Klicken Sie im Menü auf der linken Seite auf **Benutzer und Gruppen**.

    ![Benutzer zuweisen][202] 

1. Klicken Sie auf die Schaltfläche **Hinzufügen**. Wählen Sie dann im Dialogfeld **Zuweisung hinzufügen** die Option **Benutzer und Gruppen** aus.

    ![Benutzer zuweisen][203]

1. Wählen Sie im Dialogfeld **Benutzer und Gruppen** in der Benutzerliste **Britta Simon** aus.

1. Klicken Sie im Dialogfeld **Benutzer und Gruppen** auf die Schaltfläche **Auswählen**.

1. Klicken Sie im Dialogfeld **Zuweisung hinzufügen** auf **Zuweisen**.
    
### <a name="testing-single-sign-on"></a>Testen der einmaligen Anmeldung

In diesem Abschnitt testen Sie die Azure AD-Konfiguration für einmaliges Anmelden über den Zugriffsbereich.

Wenn Sie im Zugriffsbereich auf die Kachel „iLMS“ klicken, sollten Sie automatisch bei Ihrer iLMS-Anwendung angemeldet werden.

## <a name="additional-resources"></a>Zusätzliche Ressourcen

* [Liste der Tutorials zur Integration von SaaS-Apps in Azure Active Directory](tutorial-list.md)
* [Was bedeuten Anwendungszugriff und einmaliges Anmelden mit Azure Active Directory?](../manage-apps/what-is-single-sign-on.md)



<!--Image references-->

[1]: ./media/ilms-tutorial/tutorial_general_01.png
[2]: ./media/ilms-tutorial/tutorial_general_02.png
[3]: ./media/ilms-tutorial/tutorial_general_03.png
[4]: ./media/ilms-tutorial/tutorial_general_04.png

[100]: ./media/ilms-tutorial/tutorial_general_100.png

[200]: ./media/ilms-tutorial/tutorial_general_200.png
[201]: ./media/ilms-tutorial/tutorial_general_201.png
[202]: ./media/ilms-tutorial/tutorial_general_202.png
[203]: ./media/ilms-tutorial/tutorial_general_203.png

