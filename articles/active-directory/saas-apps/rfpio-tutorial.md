---
title: 'Tutorial: Azure Active Directory-Integration mit RFPIO | Microsoft-Dokumentation'
description: Erfahren Sie, wie Sie das einmalige Anmelden zwischen Azure Active Directory und RFPIO konfigurieren.
services: active-directory
documentationCenter: na
author: jeevansd
manager: daveba
ms.assetid: 87187076-7b50-4247-814f-f217b052703f
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 06/16/2017
ms.author: jeedes
ms.openlocfilehash: 0b216d8a8a2c6e1ab7c7b71eedfca9cbd6dbd5cf
ms.sourcegitcommit: d3200828266321847643f06c65a0698c4d6234da
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/29/2019
ms.locfileid: "55197346"
---
# <a name="tutorial-azure-active-directory-integration-with-rfpio"></a>Tutorial: Azure Active Directory-Integration mit RFPIO

In diesem Tutorial erfahren Sie, wie Sie RFPIO in Azure Active Directory (Azure AD) integrieren.

Die Integration von RFPIO in Azure AD bietet die folgenden Vorteile:

- Sie können in Azure AD steuern, wer Zugriff auf RFPIO hat.
- Sie können Benutzern ermöglichen, sich mit ihrem Azure AD-Konto automatisch bei RFPIO anzumelden (einmaliges Anmelden).
- Sie können Ihre Konten an einem zentralen Ort verwalten – im Azure-Portal.

Weitere Informationen zur Integration von SaaS-Apps in Azure AD finden Sie unter [Was bedeuten Anwendungszugriff und einmaliges Anmelden mit Azure Active Directory?](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Voraussetzungen

Um die Azure AD-Integration mit RFPIO konfigurieren zu können, benötigen Sie Folgendes:

- Ein Azure AD-Abonnement
- Ein RFPIO-Abonnement, für das einmaliges Anmelden aktiviert ist

> [!NOTE]
> Es wird nicht empfohlen, zum Testen der Schritte in diesem Tutorial eine Produktionsumgebung zu verwenden.

Beachten Sie beim Testen der Schritte in diesem Tutorial die folgenden Empfehlungen:

- Verwenden Sie die Produktionsumgebung nur, wenn dies unbedingt erforderlich ist.
- Wenn Sie keine Azure AD-Testumgebung haben, können Sie eine [einmonatige Testversion anfordern](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Beschreibung des Szenarios
In diesem Tutorial testen Sie das einmalige Anmelden für Azure AD in einer Testumgebung. Das in diesem Tutorial beschriebene Szenario besteht aus zwei Hauptelementen:

1. Hinzufügen von RFPIO aus dem Katalog
1. Konfigurieren und Testen der einmaligen Anmeldung von Azure AD

## <a name="add-rfpio-from-the-gallery"></a>Hinzufügen von RFPIO aus dem Katalog
Zum Konfigurieren der Integration von RFPIO in Azure AD müssen Sie RFPIO aus dem Katalog der Liste der verwalteten SaaS-Apps hinzufügen.

### <a name="to-add-rfpio-from-the-gallery"></a>So fügen Sie RFPIO aus dem Katalog hinzu

1. Wählen Sie im linken Navigationsbereich des **[Azure-Portals](https://portal.azure.com)** das Symbol für **Azure Active Directory** aus. 

    ![Active Directory][1]

1. Wählen Sie **Unternehmensanwendungen** und dann **Alle Anwendungen** aus.

    ![ANWENDUNGEN][2]
    
1. Wählen Sie oben im Dialogfeld die Schaltfläche **Neue Anwendung** aus, um eine neue Anwendung hinzuzufügen.

    ![ANWENDUNGEN][3]

1. Geben Sie im Suchfeld als Suchbegriff **RFPIO** ein.

    ![Erstellen eines Azure AD-Testbenutzers](./media/rfpio-tutorial/tutorial_rfpio_search.png)

1. Wählen Sie im Ergebnisbereich **RFPIO** aus, und klicken Sie dann auf die Schaltfläche **Hinzufügen**, um die Anwendung hinzuzufügen.

    ![Erstellen eines Azure AD-Testbenutzers](./media/rfpio-tutorial/tutorial_rfpio_addfromgallery.png)

##  <a name="configure-and-test-azure-ad-single-sign-on"></a>Konfigurieren und Testen des einmaligen Anmeldens in Azure AD
In diesem Abschnitt konfigurieren und testen Sie das einmalige Anmelden mit Azure AD bei RFPIO mithilfe einer Testbenutzerin namens Britta Simon.

Damit das einmalige Anmelden funktioniert, muss Azure AD wissen, welcher Benutzer in RFPIO als Entsprechung für einen Benutzer in Azure AD fungiert. Anders ausgedrückt: Zwischen einem Azure AD-Benutzer und dem entsprechenden Benutzer in RFPIO muss eine Linkbeziehung eingerichtet werden.

Weisen Sie in RFPIO den Wert für **Benutzername** in Azure AD als Wert für **Benutzername** zu, um eine Linkbeziehung herzustellen.

Zum Konfigurieren und Testen des einmaligen Anmeldens in Azure AD bei RFPIO müssen Sie die folgenden Bausteine ausführen:

1. **[Konfigurieren des einmaligen Anmeldens von Azure AD](#configuring-azure-ad-single-sign-on)**, um Ihren Benutzern das Verwenden dieses Features zu ermöglichen.
1. **[Erstellen eines Azure AD-Testbenutzers](#creating-an-azure-ad-test-user)**, um das einmalige Anmelden mit Azure AD mit der Testbenutzerin Britta Simon zu testen.
1. **[Erstellen eines RFPIO-Testbenutzers](#creating-a-rfpio-test-user)**, um eine Entsprechung von Britta Simon in RFPIO zu erhalten, die mit ihrer Darstellung in Azure AD verknüpft ist.
1. **[Zuweisen des Azure AD-Testbenutzers](#assigning-the-azure-ad-test-user)**, um Britta Simon für das einmalige Anmelden von Azure AD zu aktivieren.
1. **[Testen des einmaligen Anmeldens](#testing-single-sign-on)**, um sicherzustellen, dass die Konfiguration funktioniert.

### <a name="configure-azure-ad-single-sign-on"></a>Konfigurieren des einmaligen Anmeldens in Azure AD

In diesem Abschnitt aktivieren Sie das einmalige Anmelden mit Azure AD im Azure-Portal und konfigurieren das einmalige Anmelden in Ihrer RFPIO-Anwendung.

**Führen Sie zum Konfigurieren des einmaligen Anmeldens von Azure AD in RFPIO die folgenden Schritte aus:**

1. Klicken Sie im Azure-Portal auf der Anwendungsintegrationsseite für **RFPIO** auf **Einmaliges Anmelden**.

    ![Configure single sign-on][4]

1. Wählen Sie im Dialogfeld **Einmaliges Anmelden** als **Modus** die Option **SAML-basierte Anmeldung** aus, um einmaliges Anmelden zu aktivieren.
 
    ![Configure single sign-on](./media/rfpio-tutorial/tutorial_rfpio_samlbase.png)

1. Führen Sie im Abschnitt **Domäne und URLs für RFPIO** die folgenden Schritte aus, wenn Sie die Anwendung im **IDP-initiierten Modus** konfigurieren möchten:

    ![Configure single sign-on](./media/rfpio-tutorial/tutorial_rfpio_url.png)

    a. Geben Sie im Textfeld **Bezeichner** die folgende URL ein: `https://www.rfpio.com`.

    ![Configure single sign-on](./media/rfpio-tutorial/tutorial_rfpio_url1.png)

    b. Aktivieren Sie **Erweiterte URL-Einstellungen anzeigen**.

    c. Geben Sie im Textfeld **Relayzustand** einen Zeichenfolgenwert ein. Wenden Sie sich an das [Supportteam von RFPIO](https://www.rfpio.com/contact/), um diesen Wert zu erhalten. 

1. Aktivieren Sie **Erweiterte URL-Einstellungen anzeigen**. Wenn Sie die Anwendung im **SP-initiierten Modus** konfigurieren möchten: 

    ![Configure single sign-on](./media/rfpio-tutorial/tutorial_rfpio_url2.png)

    Geben Sie im Textfeld **Anmelde-URL** die URL ein: `https://www.app.rfpio.com`.

1. Klicken Sie im Abschnitt **SAML-Signaturzertifikat** auf **Metadaten-XML**, und speichern Sie die Metadatendatei dann auf Ihrem Computer.

    ![Configure single sign-on](./media/rfpio-tutorial/tutorial_rfpio_certificate.png) 

1. Klicken Sie auf die Schaltfläche **Save** .

    ![Configure single sign-on](./media/rfpio-tutorial/tutorial_general_400.png)

1. Melden Sie sich in einem anderen Webbrowserfenster bei der **RFPIO**-Website als Administrator an.

1. Klicken Sie in der linken unteren Ecke auf die Dropdownliste.

    ![Configure single sign-on](./media/rfpio-tutorial/app1.png)

1. Klicken Sie auf **Organization Settings** (Organisationseinstellungen). 

    ![Configure single sign-on](./media/rfpio-tutorial/app2.png)

1. Klicken Sie auf **FEATURES & INTEGRATION**.

    ![Configure single sign-on](./media/rfpio-tutorial/app4.png)

1. Klicken Sie unter **SAML SSO Configuration** (SAML-SSO-Konfiguration) auf **Edit** (Bearbeiten).

    ![Configure single sign-on](./media/rfpio-tutorial/app3.png)

1. Führen Sie in diesem Abschnitt folgende Aktionen durch:

    ![Configure single sign-on](./media/rfpio-tutorial/app5.png)
    
    a. Kopieren Sie den Inhalt der heruntergeladenen **XML-Metadatendatei**, und fügen Sie ihn in das Feld **identity configuration** (Identitätskonfiguration) ein.

    > [!NOTE]
    >Verwenden Sie zum Kopieren des Inhalts der heruntergeladenen **Metadata-XML** das Programm **Notepad++** oder einen geeigneten **XML-Editor**. 

    b. Klicken Sie auf **Überprüfen**.

    c. Schalten Sie nach dem Klicken auf **Überprüfen** die Einstellung **SAML(Enabled)** (SAML – aktiviert) auf „Ein“.

    d. Klicken Sie auf **Submit**.

> [!TIP]
> Während der Einrichtung der App können Sie im [Azure-Portal](https://portal.azure.com) nun eine Kurzfassung dieser Anweisungen lesen.  Nachdem Sie diese App aus dem Abschnitt **Active Directory > Unternehmensanwendungen** heruntergeladen haben, klicken Sie einfach auf die Registerkarte **Einmaliges Anmelden**, und rufen Sie die eingebettete Dokumentation über den Abschnitt **Konfiguration** um unteren Rand der Registerkarte auf. Weitere Informationen zur eingebetteten Dokumentation finden Sie hier: [Dokumentation zu eingebettetem Azure AD]( https://go.microsoft.com/fwlink/?linkid=845985)
> 

### <a name="create-an-azure-ad-test-user"></a>Erstellen eines Azure AD-Testbenutzers
Das Ziel dieses Abschnitts ist das Erstellen eines Testbenutzers namens Britta Simon im Azure-Portal.

![Azure AD-Benutzer erstellen][100]

**Um einen Testbenutzer in Azure AD zu erstellen, führen Sie die folgenden Schritte aus:**

1. Klicken Sie im linken Navigationsbereich des **Azure-Portals** auf das Symbol für **Azure Active Directory**.

    ![Erstellen eines Azure AD-Testbenutzers](./media/rfpio-tutorial/create_aaduser_01.png) 

1. Wechseln Sie zu **Benutzer und Gruppen**, und klicken Sie auf **Alle Benutzer**, um die Liste der Benutzer anzuzeigen.
    
    ![Erstellen eines Azure AD-Testbenutzers](./media/rfpio-tutorial/create_aaduser_02.png) 

1. Klicken Sie oben im Dialogfeld auf **Hinzufügen**, um das Dialogfeld **Benutzer** zu öffnen.
 
    ![Erstellen eines Azure AD-Testbenutzers](./media/rfpio-tutorial/create_aaduser_03.png) 

1. Führen Sie auf der Dialogfeldseite **Benutzer** die folgenden Schritte aus:
 
    ![Erstellen eines Azure AD-Testbenutzers](./media/rfpio-tutorial/create_aaduser_04.png) 

    a. Geben Sie in das Textfeld **Name** den Namen **BrittaSimon** ein.

    b. Geben Sie in das Textfeld **Benutzername** die **E-Mail-Adresse** von Britta Simon ein.

    c. Wählen Sie **Kennwort anzeigen** aus, und notieren Sie sich den Wert des **Kennworts**.

    d. Klicken Sie auf **Create**.
 
### <a name="create-a-rfpio-test-user"></a>Erstellen eines RFPIO-Testbenutzers

Damit sich Azure AD-Benutzer bei RFPIO anmelden können, müssen sie in RFPIO bereitgestellt werden.  
Im Fall von RFPIO ist die Bereitstellung eine manuelle Aufgabe.

**Führen Sie zum Bereitstellen eines Benutzerkontos die folgenden Schritte aus:**

1. Melden Sie sich bei der RFPIO-Unternehmenswebsite als Administrator an.

1. Klicken Sie in der linken unteren Ecke auf die Dropdownliste.

    ![Configure single sign-on](./media/rfpio-tutorial/app1.png)

1. Klicken Sie auf **Organization Settings** (Organisationseinstellungen). 

    ![Configure single sign-on](./media/rfpio-tutorial/app2.png)

1. Klicken Sie auf **TEAM MEMBERS** (TEAMMITGLIEDER).

    ![Configure single sign-on](./media/rfpio-tutorial/app6.png)

1. Klicken Sie auf **ADD MEMBERS** (MITGLIEDER HINZUFÜGEN).

    ![Configure single sign-on](./media/rfpio-tutorial/app7.png)

1. Im Abschnitt **Add New Members** (Neue Mitglieder hinzufügen) Führen Sie folgende Aktionen aus:

    ![Configure single sign-on](./media/rfpio-tutorial/app8.png)

    a. Geben Sie die **E-Mail-Adresse** in das Feld **Enter one email per line** (eine E-Mail-Adresse pro Zeile eingeben) ein.

    b. Wählen Sie die **Rolle** entsprechend Ihren Anforderungen aus.

    c. Klicken Sie auf **ADD MEMBERS** (MITGLIEDER HINZUFÜGEN).
        
    > [!NOTE]
    > Der Besitzer des Azure Active Directory-Kontos erhält eine E-Mail und folgt einem Link zur Bestätigung des Kontos, bevor es aktiv wird.

### <a name="assign-the-azure-ad-test-user"></a>Zuweisen des Azure AD-Testbenutzers

In diesem Abschnitt ermöglichen Sie Britta Simon die Verwendung des einmaligen Anmeldens von Azure, indem Sie ihr Zugriff auf RFPIO gewähren.

![Benutzer zuweisen][200] 

**Um Britta Simon RFPIO zuzuweisen, führen Sie die folgenden Schritte aus:**

1. Öffnen Sie im Azure-Portal die Anwendungsansicht, navigieren Sie zur Verzeichnisansicht, wechseln Sie dann zu **Unternehmensanwendungen**, und klicken Sie auf **Alle Anwendungen**.

    ![Benutzer zuweisen][201] 

1. Wählen Sie in der Anwendungsliste **RFPIO** aus.

    ![Configure single sign-on](./media/rfpio-tutorial/tutorial_rfpio_app.png) 

1. Klicken Sie im Menü auf der linken Seite auf **Benutzer und Gruppen**.

    ![Benutzer zuweisen][202] 

1. Klicken Sie auf die Schaltfläche **Hinzufügen**. Wählen Sie dann im Dialogfeld **Zuweisung hinzufügen** die Option **Benutzer und Gruppen** aus.

    ![Benutzer zuweisen][203]

1. Wählen Sie im Dialogfeld **Benutzer und Gruppen** in der Benutzerliste **Britta Simon** aus.

1. Klicken Sie im Dialogfeld **Benutzer und Gruppen** auf die Schaltfläche **Auswählen**.

1. Klicken Sie im Dialogfeld **Zuweisung hinzufügen** auf **Zuweisen**.
    
### <a name="test-single-sign-on"></a>Testen des einmaligen Anmeldens

In diesem Abschnitt testen Sie die Azure AD-Konfiguration für einmaliges Anmelden über den Zugriffsbereich.

Wenn Sie im Zugriffsbereich auf die Kachel „RFPIO“ klicken, sollten Sie automatisch bei Ihrer RFPIO-Anwendung angemeldet werden.
Weitere Informationen zum Zugriffspanel finden Sie unter [Einführung in das Zugriffspanel](../user-help/active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Zusätzliche Ressourcen

* [Liste der Tutorials zur Integration von SaaS-Apps in Azure Active Directory](tutorial-list.md)
* [Was bedeuten Anwendungszugriff und einmaliges Anmelden mit Azure Active Directory?](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/rfpio-tutorial/tutorial_general_01.png
[2]: ./media/rfpio-tutorial/tutorial_general_02.png
[3]: ./media/rfpio-tutorial/tutorial_general_03.png
[4]: ./media/rfpio-tutorial/tutorial_general_04.png

[100]: ./media/rfpio-tutorial/tutorial_general_100.png

[200]: ./media/rfpio-tutorial/tutorial_general_200.png
[201]: ./media/rfpio-tutorial/tutorial_general_201.png
[202]: ./media/rfpio-tutorial/tutorial_general_202.png
[203]: ./media/rfpio-tutorial/tutorial_general_203.png

