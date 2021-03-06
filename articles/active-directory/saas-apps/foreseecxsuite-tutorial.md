---
title: 'Tutorial: Azure Active Directory-Integration in ForeSee CX Suite | Microsoft-Dokumentation'
description: Erfahren Sie, wie Sie das einmalige Anmelden für Azure Active Directory und ForeSee CX Suite konfigurieren.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: 5f4b7830-6186-4d17-b77b-504d4192bfde
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 05/24/2018
ms.author: jeedes
ms.openlocfilehash: 54dd577e3e3cc1650e4384e3b7f4eda581fe0fa1
ms.sourcegitcommit: d3200828266321847643f06c65a0698c4d6234da
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/29/2019
ms.locfileid: "55191141"
---
# <a name="tutorial-azure-active-directory-integration-with-foresee-cx-suite"></a>Tutorial: Azure Active Directory-Integration in ForeSee CX Suite

In diesem Tutorial erfahren Sie, wie Sie ForeSee CX Suite in Azure Active Directory (Azure AD) integrieren.

Die Integration von ForeSee CX Suite in Azure AD bietet die folgenden Vorteile:

- Sie können in Azure AD steuern, wer Zugriff auf ForeSee CX Suite hat.
- Sie können Benutzern ermöglichen, sich mit ihren Azure AD-Konten automatisch bei ForeSee CX Suite anzumelden (einmaliges Anmelden, SSO).
- Sie können Ihre Konten über das Azure-Portal an einem zentralen Ort verwalten.

Weitere Informationen zur Integration von SaaS-Apps in Azure AD finden Sie unter [Was bedeuten Anwendungszugriff und einmaliges Anmelden mit Azure Active Directory?](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Voraussetzungen

Um die Azure AD-Integration in ForeSee CX Suite konfigurieren zu können, benötigen Sie Folgendes:

- Ein Azure AD-Abonnement
- Ein ForeSee CX Suite-Abonnement, für das einmaliges Anmelden aktiviert ist

> [!NOTE]
> Um die Schritte in diesem Tutorial zu testen, wird empfohlen, keine Produktionsumgebung zu verwenden.

Um die Schritte in diesem Tutorial zu testen, sollten Sie folgende Empfehlungen beachten:

- Verwenden Sie die Produktionsumgebung nur, wenn dies unbedingt erforderlich ist.
- Wenn Sie keine Azure AD-Testumgebung haben, können Sie eine [einmonatige Testversion anfordern](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Beschreibung des Szenarios
In diesem Tutorial testen Sie das einmalige Anmelden für Azure AD in einer Testumgebung.
Das in diesem Tutorial beschriebene Szenario besteht aus zwei Hauptbestandteilen:

1. Hinzufügen von ForeSee CX Suite aus dem Katalog
1. Konfigurieren und Testen der einmaligen Anmeldung von Azure AD

## <a name="adding-foresee-cx-suite-from-the-gallery"></a>Hinzufügen von ForeSee CX Suite aus dem Katalog
Zum Konfigurieren der Integration von ForeSee CX Suite in Azure AD müssen Sie ForeSee CX Suite aus dem Katalog der Liste mit den verwalteten SaaS-Apps hinzufügen.

**So fügen Sie ForeSee CX Suite aus dem Katalog hinzu**

1. Klicken Sie im linken Navigationsbereich des **[Azure-Portals](https://portal.azure.com)** auf das Symbol für **Azure Active Directory**.

    ![Schaltfläche „Azure Active Directory“][1]

1. Navigieren Sie zu **Unternehmensanwendungen**. Wechseln Sie dann zu **Alle Anwendungen**.

    ![Blatt „Unternehmensanwendungen“][2]

1. Klicken Sie oben im Dialogfeld auf die Schaltfläche **Neue Anwendung**, um eine neue Anwendung hinzuzufügen.

    ![Schaltfläche „Neue Anwendung“][3]

1. Geben Sie im Suchfeld **ForeSee CX Suite** ein, wählen Sie im Ergebnisbereich **ForeSee CX Suite** aus, und klicken Sie dann auf die Schaltfläche **Hinzufügen**, um die Anwendung hinzuzufügen.

    ![ForeSee CX Suite in der Ergebnisliste](./media/foreseecxsuite-tutorial/tutorial_foreseecxsuite_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Konfigurieren und Testen des einmaligen Anmeldens in Azure AD

In diesem Abschnitt konfigurieren und testen Sie das einmalige Anmelden von Azure AD bei ForeSee CX Suite anhand einer Testbenutzerin namens Britta Simon.

Damit das einmalige Anmelden funktioniert, muss Azure AD wissen, welcher Benutzer in ForeSee CX Suite als Entsprechung für einen Benutzer in Azure AD fungiert. Anders ausgedrückt: Zwischen einem Azure AD-Benutzer und dem entsprechenden ForeSee CX Suite-Benutzer muss eine Linkbeziehung eingerichtet werden.

Führen Sie die folgenden Schritte aus, um das einmalige Anmelden von Azure AD mit ForeSee CX Suite zu konfigurieren und zu testen:

1. **[Konfigurieren des einmaligen Anmeldens von Azure AD](#configure-azure-ad-single-sign-on)**, um Ihren Benutzern das Verwenden dieses Features zu ermöglichen.
1. **[Erstellen eines Azure AD-Testbenutzers](#create-an-azure-ad-test-user)**, um das einmalige Anmelden mit Azure AD mit dem Testbenutzer Britta Simon zu testen.
1. **[Erstellen eines ForeSee CX Suite-Testbenutzers](#create-a-foresee-cx-suite-test-user)**, um eine Entsprechung für Britta Simon in ForeSee CX Suite zu haben, die mit ihrer Darstellung in Azure AD verknüpft ist.
1. **[Zuweisen des Azure AD-Testbenutzers](#assign-the-azure-ad-test-user)**, um Britta Simon für das einmalige Anmelden von Azure AD zu aktivieren.
1. **[Testen der einmaligen Anmeldung](#test-single-sign-on)**, um zu überprüfen, ob die Konfiguration funktioniert.

### <a name="configure-azure-ad-single-sign-on"></a>Konfigurieren des einmaligen Anmeldens in Azure AD

In diesem Abschnitt aktivieren Sie das einmalige Anmelden von Azure AD im Azure-Portal und konfigurieren das einmalige Anmelden in Ihrer ForeSee CX Suite-Anwendung.

**So konfigurieren Sie das einmalige Anmelden von Azure AD mit ForeSee CX Suite**

1. Klicken Sie im Azure-Portal auf der Anwendungsintegrationsseite für **ForeSee CX Suite** auf **Einmaliges Anmelden**.

    ![Konfigurieren des Links für einmaliges Anmelden][4]

1. Wählen Sie im Dialogfeld **Einmaliges Anmelden** als **Modus** die Option **SAML-basierte Anmeldung** aus, um einmaliges Anmelden zu aktivieren.

    ![Dialogfeld „Einmaliges Anmelden“](./media/foreseecxsuite-tutorial/tutorial_foreseecxsuite_samlbase.png)

1. Führen Sie im Abschnitt **Domäne und URLs für ForeSee CX Suite** die folgenden Schritte aus, wenn Sie eine **Dienstanbieter-Metadatendatei** haben:

    ![SSO-Informationen zur Domäne und zu den URLs für ForeSee CX Suite](./media/foreseecxsuite-tutorial/upload.png)

    a. Klicken Sie auf **Metadatendatei hochladen**.

    ![SSO-Informationen zur Domäne und zu den URLs für ForeSee CX Suite](./media/foreseecxsuite-tutorial/tutorial_foreseen_uploadconfig.png)

    b. Klicken Sie auf das **Ordnerlogo**, wählen Sie die Metadatendatei aus, und klicken Sie auf **Hochladen**.

    c. Nachdem die **Dienstanbieter-Metadatendatei** hochgeladen wurde, wird im Abschnitt **Domäne und URLs für ForeSee CX Suite** der Wert für **Bezeichner** automatisch ausgefüllt, wie unten dargestellt:

    ![SSO-Informationen zur Domäne und zu den URLs für ForeSee CX Suite](./media/foreseecxsuite-tutorial/urlupload.png)

1. Führen Sie die folgenden Schritte aus, wenn Sie keine **Dienstanbieter-Metadatendatei** haben:

    ![SSO-Informationen zur Domäne und zu den URLs für ForeSee CX Suite](./media/foreseecxsuite-tutorial/tutorial_foreseecxsuite_url.png)

    a. Geben Sie im Textfeld **Anmelde-URL** diese URL ein: `https://cxsuite.foresee.com/`

    b. Geben Sie im Textfeld **Bezeichner** eine URL nach folgendem Muster ein: `https://www.okta.com/saml2/service-provider/<UniqueID>`

    > [!NOTE]
    > Der ID-Wert ist nicht der tatsächliche Wert. Aktualisieren Sie den Wert mit dem tatsächlichen Bezeichner. Wenden Sie sich an das [Supportteam von ForeSee CX Suite](mailto:support@foresee.com), um diesen Wert zu erhalten.

1. Klicken Sie im Abschnitt **SAML-Signaturzertifikat** auf **Metadaten-XML**, und speichern Sie die Metadatendatei dann auf Ihrem Computer.

    ![Downloadlink für das Zertifikat](./media/foreseecxsuite-tutorial/tutorial_foreseecxsuite_certificate.png)

1. Klicken Sie auf die Schaltfläche **Save** .

    ![Schaltfläche „Speichern“ beim Konfigurieren des einmaligen Anmeldens](./media/foreseecxsuite-tutorial/tutorial_general_400.png)

1. Senden Sie die heruntergeladene **Metadaten-XML**-Datei an das [ForeSee CX Suite-Supportteam](mailto:support@foresee.com), um das einmalige Anmelden bei **ForeSee CX Suite** zu konfigurieren. Es führt die Einrichtung durch, damit die SAML-SSO-Verbindung auf beiden Seiten richtig festgelegt ist.

### <a name="create-an-azure-ad-test-user"></a>Erstellen eines Azure AD-Testbenutzers

Das Ziel dieses Abschnitts ist das Erstellen eines Testbenutzers namens Britta Simon im Azure-Portal.

   ![Erstellen eines Azure AD-Testbenutzers][100]

**Um einen Testbenutzer in Azure AD zu erstellen, führen Sie die folgenden Schritte aus:**

1. Klicken Sie im linken Bereich des Azure-Portals auf die Schaltfläche **Azure Active Directory**.

    ![Schaltfläche „Azure Active Directory“](./media/foreseecxsuite-tutorial/create_aaduser_01.png)

1. Navigieren Sie zu **Benutzer und Gruppen**, und klicken Sie dann auf **Alle Benutzer**, um die Liste mit den Benutzern anzuzeigen.

    ![Links „Benutzer und Gruppen“ und „Alle Benutzer“](./media/foreseecxsuite-tutorial/create_aaduser_02.png)

1. Klicken Sie oben im Dialogfeld **Alle Benutzer** auf **Hinzufügen**, um das Dialogfeld **Benutzer** zu öffnen.

    ![Schaltfläche „Hinzufügen“](./media/foreseecxsuite-tutorial/create_aaduser_03.png)

1. Führen Sie im Dialogfeld **Neuer Benutzer** die folgenden Schritte aus:

    ![Dialogfeld „Benutzer“](./media/foreseecxsuite-tutorial/create_aaduser_04.png)

    a. Geben Sie in das Feld **Name** den Namen **BrittaSimon** ein.

    b. Geben Sie im Feld **Benutzername** die E-Mail-Adresse des Benutzers Britta Simon ein.

    c. Aktivieren Sie das Kontrollkästchen **Kennwort anzeigen**, und notieren Sie sich den Wert, der im Feld **Kennwort** angezeigt wird.

    d. Klicken Sie auf **Create**.

### <a name="create-a-foresee-cx-suite-test-user"></a>Erstellen eines ForeSee CX Suite-Testbenutzers

In diesem Abschnitt erstellen Sie in ForeSee CX Suite eine Benutzerin namens Britta Simon. Das [ForeSee CX Suite-Supportteam](mailto:support@foresee.com) kann Sie beim Hinzufügen von Benutzern oder Domänen unterstützen, die auf der ForeSee CX Suite-Plattform auf die Whitelist gesetzt werden sollen. Wird die Domäne vom Team hinzugefügt, werden Benutzer automatisch auf der ForeSee CX Suite-Plattform bereitgestellt. Benutzer müssen erstellt und aktiviert werden, damit Sie einmaliges Anmelden verwenden können.

### <a name="assign-the-azure-ad-test-user"></a>Zuweisen des Azure AD-Testbenutzers

In diesem Abschnitt gewähren Sie Britta Simon Zugriff auf ForeSee CX Suite, damit sie das einmalige Anmelden von Azure verwenden kann.

![Zuweisen der Benutzerrolle][200]

**So weisen Sie Britta Simon ForeSee CX Suite zu**

1. Öffnen Sie im Azure-Portal die Anwendungsansicht, navigieren Sie zur Verzeichnisansicht, wechseln Sie dann zu **Unternehmensanwendungen**, und klicken Sie auf **Alle Anwendungen**.

    ![Benutzer zuweisen][201]

1. Wählen Sie in der Anwendungsliste **ForeSee CX Suite** aus.

    ![ForeSee CX Suite-Link in der Anwendungsliste](./media/foreseecxsuite-tutorial/tutorial_foreseecxsuite_app.png)

1. Klicken Sie im Menü auf der linken Seite auf **Benutzer und Gruppen**.

    ![Link „Benutzer und Gruppen“][202]

1. Klicken Sie auf die Schaltfläche **Hinzufügen**. Wählen Sie dann im Dialogfeld **Zuweisung hinzufügen** die Option **Benutzer und Gruppen** aus.

    ![Bereich „Zuweisung hinzufügen“][203]

1. Wählen Sie im Dialogfeld **Benutzer und Gruppen** in der Benutzerliste **Britta Simon** aus.

1. Klicken Sie im Dialogfeld **Benutzer und Gruppen** auf die Schaltfläche **Auswählen**.

1. Klicken Sie im Dialogfeld **Zuweisung hinzufügen** auf **Zuweisen**.

### <a name="test-single-sign-on"></a>Testen des einmaligen Anmeldens

In diesem Abschnitt testen Sie die Azure AD-Konfiguration für einmaliges Anmelden über den Zugriffsbereich.

Wenn Sie im Zugriffsbereich auf die Kachel „ForeSee CX Suite“ klicken, werden Sie automatisch bei Ihrer ForeSee CX Suite-Anwendung angemeldet.
Weitere Informationen zum Zugriffsbereich finden Sie unter [Einführung in den Zugriffsbereich](../user-help/active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Zusätzliche Ressourcen

* [Liste der Tutorials zur Integration von SaaS-Apps in Azure Active Directory](tutorial-list.md)
* [Was bedeuten Anwendungszugriff und einmaliges Anmelden mit Azure Active Directory?](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: ./media/foreseecxsuite-tutorial/tutorial_general_01.png
[2]: ./media/foreseecxsuite-tutorial/tutorial_general_02.png
[3]: ./media/foreseecxsuite-tutorial/tutorial_general_03.png
[4]: ./media/foreseecxsuite-tutorial/tutorial_general_04.png

[100]: ./media/foreseecxsuite-tutorial/tutorial_general_100.png

[200]: ./media/foreseecxsuite-tutorial/tutorial_general_200.png
[201]: ./media/foreseecxsuite-tutorial/tutorial_general_201.png
[202]: ./media/foreseecxsuite-tutorial/tutorial_general_202.png
[203]: ./media/foreseecxsuite-tutorial/tutorial_general_203.png

