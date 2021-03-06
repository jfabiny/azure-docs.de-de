---
title: 'Tutorial: Azure Active Directory-Integration mit Hightail | Microsoft-Dokumentation'
description: Erfahren Sie, wie Sie das einmalige Anmelden für Azure Active Directory und Hightail konfigurieren.
services: active-directory
documentationCenter: na
author: jeevansd
manager: daveba
ms.assetid: e15206ac-74b0-46e4-9329-892c7d242ec0
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/15/2018
ms.author: jeedes
ms.openlocfilehash: 59342aa95e50b29e58035892967be6d0407aae91
ms.sourcegitcommit: 98645e63f657ffa2cc42f52fea911b1cdcd56453
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/23/2019
ms.locfileid: "54812963"
---
# <a name="tutorial-azure-active-directory-integration-with-hightail"></a>Tutorial: Azure Active Directory-Integration in Hightail

In diesem Tutorial erfahren Sie, wie Sie Hightail in Azure Active Directory (Azure AD) integrieren.

Die Integration von Hightail in Azure AD bietet die folgenden Vorteile:

- Sie können in Azure AD steuern, wer Zugriff auf Hightail hat
- Sie können es Benutzern ermöglichen, sich mit ihren Azure AD-Konten automatisch bei Hightail anzumelden (einmaliges Anmelden).
- Sie können Ihre Konten an einem zentralen Ort verwalten – im Azure-Portal.

Weitere Informationen zur Integration von SaaS-Apps in Azure AD finden Sie unter [Was bedeuten Anwendungszugriff und einmaliges Anmelden mit Azure Active Directory?](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Voraussetzungen

Um die Azure AD-Integration mit Hightail konfigurieren zu können, benötigen Sie Folgendes:

- Ein Azure AD-Abonnement
- Ein Hightail-Abonnement, für das einmaliges Anmelden aktiviert ist

> [!NOTE]
> Um die Schritte in diesem Tutorial zu testen, wird empfohlen, keine Produktionsumgebung zu verwenden.

Um die Schritte in diesem Tutorial zu testen, sollten Sie folgende Empfehlungen beachten:

- Verwenden Sie die Produktionsumgebung nur, wenn dies unbedingt erforderlich ist.
- Wenn Sie keine Azure AD-Testumgebung haben, können Sie [hier](https://azure.microsoft.com/pricing/free-trial/)eine einmonatige Testversion anfordern.

## <a name="scenario-description"></a>Beschreibung des Szenarios
In diesem Tutorial testen Sie das einmalige Anmelden für Azure AD in einer Testumgebung. Das in diesem Tutorial beschriebene Szenario besteht aus zwei Hauptbestandteilen:

1. Hinzufügen von Hightail aus dem Katalog
1. Konfigurieren und Testen der einmaligen Anmeldung von Azure AD

## <a name="adding-hightail-from-the-gallery"></a>Hinzufügen von Hightail aus dem Katalog
Zum Konfigurieren der Integration von Hightail in Azure AD müssen Sie Hightail aus dem Katalog der Liste mit den verwalteten SaaS-Apps hinzufügen.

**Um Hightail aus dem Katalog hinzuzufügen, führen Sie die folgenden Schritte aus:**

1. Klicken Sie im linken Navigationsbereich des **[Azure-Portals](https://portal.azure.com)** auf das Symbol für **Azure Active Directory**. 

    ![Active Directory][1]

1. Navigieren Sie zu **Unternehmensanwendungen**. Wechseln Sie dann zu **Alle Anwendungen**.

    ![ANWENDUNGEN][2]
    
1. Klicken Sie oben im Dialogfeld auf die Schaltfläche **Neue Anwendung**, um eine neue Anwendung hinzuzufügen.

    ![ANWENDUNGEN][3]

1. Geben Sie im Suchfeld als Suchbegriff **Hightail**ein.

    ![Erstellen eines Azure AD-Testbenutzers](./media/hightail-tutorial/tutorial_hightail_search.png)

1. Wählen Sie im Ergebnisbereich die Option **Hightail** aus, und klicken Sie dann auf die Schaltfläche **Hinzufügen**, um die Anwendung hinzuzufügen.

    ![Erstellen eines Azure AD-Testbenutzers](./media/hightail-tutorial/tutorial_hightail_addfromgallery.png)

##  <a name="configuring-and-testing-azure-ad-single-sign-on"></a>Konfigurieren und Testen der einmaligen Anmeldung von Azure AD
Dieser Abschnitt veranschaulicht anhand einer Testbenutzerin namens Britta Simon, wie das einmalige Anmelden von Azure AD in Hightail konfiguriert und getestet wird.

Damit einmaliges Anmelden funktioniert, muss Azure AD wissen, welcher Benutzer in Hightail als Pendant zu einem Benutzer in Azure AD fungiert. Anders ausgedrückt: Zwischen einem Azure AD-Benutzer und dem entsprechenden Benutzer in Hightail muss eine Linkbeziehung eingerichtet werden.

Weisen Sie in Hightail den Wert für **Benutzername** in Azure AD als Wert für **Benutzername** zu, um eine Linkbeziehung herzustellen.

Zum Konfigurieren und Testen des einmaligen Anmeldens in Azure AD mit Hightail müssen Sie die folgenden Schritte ausführen:

1. **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**, um Ihren Benutzern das Verwenden dieser Funktion zu ermöglichen.
1. **[Erstellen eines Azure AD-Testbenutzers](#creating-an-azure-ad-test-user)** , um das einmalige Anmelden von Azure AD mit der Testbenutzerin Britta Simon zu testen.
1. **[Erstellen eines Hightail-Testbenutzers](#creating-a-hightail-test-user)**, um ein Pendant von Britta Simon in Hightail zu erhalten, das mit ihrer Darstellung in Azure AD verknüpft ist.
1. **[Zuweisen des Azure AD-Testbenutzers](#assigning-the-azure-ad-test-user)**, um Britta Simon für das einmalige Anmelden von Azure AD zu aktivieren.
1. **[Testing Single Sign-On](#testing-single-sign-on)** , um zu überprüfen, ob die Konfiguration funktioniert.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfigurieren des einmaligen Anmeldens von Azure AD

In diesem Abschnitt aktivieren Sie das einmalige Anmelden von Azure AD im Azure-Portal und konfigurieren das einmalige Anmelden in Ihrer Hightail Software-Anwendung.

**Führen Sie zum Konfigurieren des einmaligen Anmeldens von Azure AD bei Hightail die folgenden Schritte aus:**

1. Klicken Sie im Azure-Portal auf der Anwendungsintegrationsseite für **Hightail** auf **Einmaliges Anmelden**.

    ![Configure single sign-on][4]

1. Wählen Sie im Dialogfeld **Einmaliges Anmelden** als **Modus** die Option **SAML-basierte Anmeldung** aus, um einmaliges Anmelden zu aktivieren.

    ![Configure single sign-on](./media/hightail-tutorial/tutorial_hightail_samlbase.png)

1. Führen Sie im Abschnitt **Domäne und URLs für Hightail** die folgenden Schritte aus, wenn Sie die Anwendung im **IdP**-initiierten Modus konfigurieren möchten:

    ![Configure single sign-on](./media/hightail-tutorial/tutorial_hightail_url.png)

    Geben Sie im Textfeld **Antwort-URL** folgende URL ein: `https://www.hightail.com/samlLogin?phi_action=app/samlLogin&subAction=handleSamlResponse`

    > [!NOTE]
    > Der Wert der Antwort-URL entspricht nicht dem tatsächlichen Wert. Sie aktualisieren den Wert der Antwort-URL mit der tatsächlichen Antwort-URL. Dies wird später in diesem Tutorial beschrieben.

1. Aktivieren Sie **Erweiterte URL-Einstellungen anzeigen**, und führen Sie die folgenden Schritte aus, wenn Sie die Anwendung im **SP-initiierten Modus** konfigurieren möchten:

    ![Configure single sign-on](./media/hightail-tutorial/tutorial_hightail_url1.png)

    Geben Sie im Textfeld **Anmelde-URL** die URL ein: `https://www.hightail.com/loginSSO`.

1. Klicken Sie im Abschnitt **SAML-Signaturzertifikat** auf **Zertifikat (Base64)**, und speichern Sie die Zertifikatdatei auf Ihrem Computer.

    ![Configure single sign-on](./media/hightail-tutorial/tutorial_hightail_certificate.png) 

1. Die Hightail-Anwendung erwartet die SAML-Assertionen in einem bestimmten Format. Konfigurieren Sie für diese Anwendung die folgenden Ansprüche. Sie können die Werte dieser Attribute auf der Registerkarte **Attributes** (Attribute) der Anwendung verwalten. Der folgende Screenshot zeigt ein Beispiel für diese Attributzuordnungen: 

    ![Configure single sign-on](./media/hightail-tutorial/tutorial_hightail_attribute.png) 

1. Konfigurieren Sie das SAML-Tokenattribut im Abschnitt **Benutzerattribute** im Dialogfeld **Einmaliges Anmelden**, wie in der Abbildung gezeigt, und führen Sie die folgenden Schritte aus:
    
    | Attributname | Attributwert |
    | ------------------- | -------------------- |
    | FirstName | user.givenname |
    | Nachname | user.surname |
    | E-Mail | user.mail |    
    | UserIdentity | user.mail |
    
    a. Klicken Sie auf **Attribut hinzufügen**, um das Dialogfeld **Benutzerattribut hinzufügen** zu öffnen.

    ![Configure single sign-on](./media/hightail-tutorial/tutorial_officespace_04.png)

    ![Configure single sign-on](./media/hightail-tutorial/tutorial_officespace_05.png)

    b. Geben Sie im Textfeld **Name** den für die Zeile angezeigten Attributnamen ein.

    c. Geben Sie in der Liste **Wert** den für diese Zeile angezeigten Wert ein.

    d. Lassen Sie den **Namespace** leer.

    e. Klicken Sie auf **OK**.

1. Klicken Sie auf die Schaltfläche **Save** .

    ![Configure single sign-on](./media/hightail-tutorial/tutorial_general_400.png)

1. Klicken Sie im Abschnitt **Hightail-Konfiguration** auf **Hightail konfigurieren**, um das Fenster **Anmeldung konfigurieren** zu öffnen. Kopieren Sie die **URL für den SAML-SSO-Dienst** aus dem Abschnitt **Kurzübersicht**.

    ![Configure single sign-on](./media/hightail-tutorial/tutorial_hightail_configure.png)

    >[!NOTE]
    >Bevor Sie das einmalige Anmelden für die Hightail-App konfigurieren, lassen Sie Ihre E-Mail-Domäne über das Hightail-Team zur Whitelist hinzufügen, damit alle Benutzer, die diese Domäne verwenden, das einmalige Anmelden nutzen können.

1. Öffnen Sie in einem anderen Browserfenster das Administratorportal **Hightail**.

1. Klicken Sie in der oberen rechten Ecke der Seite auf das **Benutzersymbol**. 

    ![Configure single sign-on](./media/hightail-tutorial/configure1.png)

1. Klicken Sie auf die Registerkarte **Administratorkonsole anzeigen**.

    ![Configure single sign-on](./media/hightail-tutorial/configure2.png)

1. Klicken Sie im oberen Menü auf die Registerkarte **SAML**, und führen Sie die folgenden Schritte aus:

    ![Configure single sign-on](./media/hightail-tutorial/configure3.png)

    a. Fügen Sie in das Textfeld **Anmelde-URL** den aus dem Azure-Portal kopierten Wert der **SAML-Dienst-URL für einmaliges Anmelden** ein.

    b. Öffnen Sie im Editor das Base64-codierte Zertifikat, das Sie aus dem Azure-Portal heruntergeladen haben, kopieren Sie den Inhalt des Zertifikats in die Zwischenablage, und fügen Sie ihn anschließend in das Textfeld **SAML-Zertifikat** ein.

    c. Klicken Sie zum Kopieren der SAML-Verbraucher-URL für Ihre Instanz auf **KOPIEREN**, und fügen Sie sie im Azure-Portal in das Textfeld **Antwort-URL** im Abschnitt **Domäne und URLs für Hightail** ein.

    d. Klicken Sie auf **Konfigurationen speichern**.

### <a name="creating-an-azure-ad-test-user"></a>Erstellen eines Azure AD-Testbenutzers
Das Ziel dieses Abschnitts ist das Erstellen eines Testbenutzers namens Britta Simon im Azure-Portal.

![Azure AD-Benutzer erstellen][100]

**Um einen Testbenutzer in Azure AD zu erstellen, führen Sie die folgenden Schritte aus:**

1. Klicken Sie im linken Navigationsbereich des **Azure-Portals** auf das Symbol für **Azure Active Directory**.

    ![Erstellen eines Azure AD-Testbenutzers](./media/hightail-tutorial/create_aaduser_01.png) 

1. Wechseln Sie zu **Benutzer und Gruppen**, und klicken Sie auf **Alle Benutzer**, um die Liste der Benutzer anzuzeigen.
    
    ![Erstellen eines Azure AD-Testbenutzers](./media/hightail-tutorial/create_aaduser_02.png) 

1. Klicken Sie oben im Dialogfeld auf **Hinzufügen**, um das Dialogfeld **Benutzer** zu öffnen.
 
    ![Erstellen eines Azure AD-Testbenutzers](./media/hightail-tutorial/create_aaduser_03.png) 

1. Führen Sie auf der Dialogfeldseite **Benutzer** die folgenden Schritte aus:
 
    ![Erstellen eines Azure AD-Testbenutzers](./media/hightail-tutorial/create_aaduser_04.png) 

    a. Geben Sie in das Textfeld **Name** den Namen **BrittaSimon** ein.

    b. Geben Sie in das Textfeld **Benutzername** die **E-Mail-Adresse** von Britta Simon ein.

    c. Wählen Sie **Kennwort anzeigen** aus, und notieren Sie sich den Wert des **Kennworts**.

    d. Klicken Sie auf **Create**.
 
### <a name="creating-a-hightail-test-user"></a>Erstellen eines Hightail-Testbenutzers

Das Ziel dieses Abschnitts ist das Erstellen eines Benutzers namens Britta Simon in Hightail. 

Für Sie steht in diesem Abschnitt kein Aktionselement zur Verfügung. Hightail unterstützt die Just-In-Time-Benutzerbereitstellung auf Grundlage der benutzerdefinierten Ansprüche. Wenn Sie die benutzerdefinierten Ansprüche wie im Abschnitt **[Konfigurieren des einmaligen Anmeldens von Azure AD](#configuring-azure-ad-single-sign-on)** oben konfiguriert haben, wird automatisch ein Benutzer in der Anwendung erstellt, wenn dieser noch nicht vorhanden ist. 

>[!NOTE]
>Wenn Sie einen Benutzer manuell erstellen müssen, müssen Sie sich an das [Hightail-Supportteam](mailto:support@hightail.com) wenden. 

### <a name="assigning-the-azure-ad-test-user"></a>Zuweisen des Azure AD-Testbenutzers

In diesem Abschnitt ermöglichen Sie Britta Simon die Verwendung des einmaligen Anmeldens von Azure, indem Sie ihr Zugriff auf Hightail gewähren.

![Benutzer zuweisen][200] 

**Zur Zuweisung von Britta Simon zu Hightail führen Sie die folgenden Schritte aus:**

1. Öffnen Sie im Azure-Portal die Anwendungsansicht, navigieren Sie zur Verzeichnisansicht, wechseln Sie dann zu **Unternehmensanwendungen**, und klicken Sie auf **Alle Anwendungen**.

    ![Benutzer zuweisen][201] 

1. Wählen Sie in der Anwendungsliste **Hightail**aus.

    ![Configure single sign-on](./media/hightail-tutorial/tutorial_hightail_app.png) 

1. Klicken Sie im Menü auf der linken Seite auf **Benutzer und Gruppen**.

    ![Benutzer zuweisen][202]

1. Klicken Sie auf die Schaltfläche **Hinzufügen**. Wählen Sie dann im Dialogfeld **Zuweisung hinzufügen** die Option **Benutzer und Gruppen** aus.

    ![Benutzer zuweisen][203]

1. Wählen Sie im Dialogfeld **Benutzer und Gruppen** in der Benutzerliste **Britta Simon** aus.

1. Klicken Sie im Dialogfeld **Benutzer und Gruppen** auf die Schaltfläche **Auswählen**.

1. Klicken Sie im Dialogfeld **Zuweisung hinzufügen** auf **Zuweisen**.

### <a name="testing-single-sign-on"></a>Testen der einmaligen Anmeldung

In diesem Abschnitt soll Ihre Azure AD-Konfiguration für das einmalige Anmelden mithilfe des Zugriffsbereichs getestet werden.

Wenn Sie im Zugriffsbereich auf die Kachel „Hightail“ klicken, sollten Sie automatisch bei Ihrer Hightail-Anwendung angemeldet werden.


## <a name="additional-resources"></a>Zusätzliche Ressourcen

* [Liste der Tutorials zur Integration von SaaS-Apps in Azure Active Directory](tutorial-list.md)
* [Was bedeuten Anwendungszugriff und einmaliges Anmelden mit Azure Active Directory?](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/hightail-tutorial/tutorial_general_01.png
[2]: ./media/hightail-tutorial/tutorial_general_02.png
[3]: ./media/hightail-tutorial/tutorial_general_03.png
[4]: ./media/hightail-tutorial/tutorial_general_04.png

[100]: ./media/hightail-tutorial/tutorial_general_100.png

[200]: ./media/hightail-tutorial/tutorial_general_200.png
[201]: ./media/hightail-tutorial/tutorial_general_201.png
[202]: ./media/hightail-tutorial/tutorial_general_202.png
[203]: ./media/hightail-tutorial/tutorial_general_203.png

