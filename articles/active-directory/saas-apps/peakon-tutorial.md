---
title: 'Tutorial: Azure Active Directory-Integration mit Peakon | Microsoft-Dokumentation'
description: Erfahren Sie, wie Sie das einmalige Anmelden zwischen Azure Active Directory und Peakon konfigurieren.
services: active-directory
documentationCenter: na
author: jeevansd
manager: femila
ms.reviewer: joflore
ms.assetid: a944c397-ed3f-4d45-b9b2-6d4bcb6b0a09
ms.service: active-directory
ms.subservice: saas-app-tutorial
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 11/13/2018
ms.author: jeedes
ms.openlocfilehash: 637988179228fbf0a6000de74a1185af98277e3c
ms.sourcegitcommit: d3200828266321847643f06c65a0698c4d6234da
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/29/2019
ms.locfileid: "55178952"
---
# <a name="tutorial-azure-active-directory-integration-with-peakon"></a>Tutorial: Azure Active Directory-Integration mit Peakon

In diesem Tutorial erfahren Sie, wie Sie Peakon in Azure Active Directory (Azure AD) integrieren.

Die Integration von Peakon in Azure AD bietet die folgenden Vorteile:

- Sie können in Azure AD steuern, wer auf Peakon zugreifen kann.
- Sie können es Benutzern ermöglichen, sich mit ihren Azure AD-Konten automatisch bei Peakon anzumelden (einmaliges Anmelden, Single Sign-On, SSO).
- Sie können Ihre Konten über das Azure-Portal an einem zentralen Ort verwalten.

Weitere Informationen zur Integration von SaaS-Apps in Azure AD finden Sie unter [Was bedeuten Anwendungszugriff und einmaliges Anmelden mit Azure Active Directory?](../manage-apps/what-is-single-sign-on.md).

## <a name="prerequisites"></a>Voraussetzungen

Um die Azure AD-Integration von Peakon konfigurieren zu können, benötigen Sie Folgendes:

- Ein Azure AD-Abonnement
- Ein Peakon-Abonnement, für das einmaliges Anmelden aktiviert ist

> [!NOTE]
> Um die Schritte in diesem Tutorial zu testen, wird empfohlen, keine Produktionsumgebung zu verwenden.

Um die Schritte in diesem Tutorial zu testen, sollten Sie folgende Empfehlungen beachten:

- Verwenden Sie die Produktionsumgebung nur, wenn dies unbedingt erforderlich ist.
- Wenn Sie keine Azure AD-Testumgebung haben, können Sie eine [einmonatige Testversion anfordern](https://azure.microsoft.com/pricing/free-trial/).

## <a name="scenario-description"></a>Beschreibung des Szenarios

In diesem Tutorial testen Sie das einmalige Anmelden für Azure AD in einer Testumgebung. Das in diesem Tutorial beschriebene Szenario besteht aus zwei Hauptbestandteilen:

1. Hinzufügen von Peakon aus dem Katalog
2. Konfigurieren und Testen der einmaligen Anmeldung von Azure AD

## <a name="adding-peakon-from-the-gallery"></a>Hinzufügen von Peakon aus dem Katalog

Um die Integration von Peakon in Azure AD konfigurieren zu können, müssen Sie Ihrer Liste der verwalteten SaaS-Apps Peakon aus dem Katalog hinzufügen.

**Führen Sie die folgenden Schritte aus, um Peakon aus dem Katalog hinzuzufügen:**

1. Klicken Sie im linken Navigationsbereich des **[Azure-Portals](https://portal.azure.com)** auf das Symbol für **Azure Active Directory**. 

    ![Schaltfläche „Azure Active Directory“][1]

2. Navigieren Sie zu **Unternehmensanwendungen**. Wechseln Sie dann zu **Alle Anwendungen**.

    ![Blatt „Unternehmensanwendungen“][2]

3. Klicken Sie oben im Dialogfeld auf die Schaltfläche **Neue Anwendung**, um eine neue Anwendung hinzuzufügen.

    ![Schaltfläche „Neue Anwendung“][3]

4. Geben Sie im Suchfeld den Namen **Peakon** ein, wählen Sie im Ergebnisbereich den Eintrag **Peakon** aus, und klicken Sie dann auf die Schaltfläche **Hinzufügen**, um die Anwendung hinzuzufügen.

    ![Peakon in der Ergebnisliste](./media/peakon-tutorial/tutorial_peakon_addfromgallery.png)

## <a name="configure-and-test-azure-ad-single-sign-on"></a>Konfigurieren und Testen des einmaligen Anmeldens in Azure AD

In diesem Abschnitt konfigurieren und testen Sie das einmalige Anmelden über Azure AD bei Peakon mithilfe eines Testbenutzers namens Britta Simon.

Damit das einmalige Anmelden funktioniert, muss Azure AD wissen, welcher Benutzer in Peakon als Entsprechung für einen Benutzer in Azure AD fungiert. Anders ausgedrückt: Zwischen einem Azure AD-Benutzer und dem entsprechenden Benutzer in Peakon muss eine Linkbeziehung eingerichtet werden.

Zum Konfigurieren und Testen des einmaligen Anmeldens über Azure AD bei Peakon müssen Sie die folgenden Bausteine ausführen:

1. **[Configuring Azure AD Single Sign-On](#configuring-azure-ad-single-sign-on)**, um Ihren Benutzern das Verwenden dieser Funktion zu ermöglichen.
2. **[Erstellen eines Azure AD-Testbenutzers](#creating-an-azure-ad-test-user)** , um das einmalige Anmelden von Azure AD mit der Testbenutzerin Britta Simon zu testen.
3. **[Erstellen eines Peakon-Testbenutzers](#creating-a-peakon-test-user)**, um eine Entsprechung von Britta Simon in Peakon zu erhalten, die mit ihrer Darstellung in Azure AD verknüpft ist.
4. **[Zuweisen des Azure AD-Testbenutzers](#assigning-the-azure-ad-test-user)**, um Britta Simon für das einmalige Anmelden von Azure AD zu aktivieren.
5. **[Testen der einmaligen Anmeldung](#testing-single-sign-on)**, um zu überprüfen, ob die Konfiguration funktioniert.

### <a name="configuring-azure-ad-single-sign-on"></a>Konfigurieren des einmaligen Anmeldens von Azure AD

In diesem Abschnitt aktivieren Sie das einmalige Anmelden von Azure AD im Azure-Portal und konfigurieren das einmalige Anmelden in Ihrer Peakon-Anwendung.

**Führen Sie zum Konfigurieren des einmaligen Anmeldens über Azure AD bei Peakon die folgenden Schritte aus:**

1. Klicken Sie im Azure-Portal auf der Anwendungsintegrationsseite für **Peakon** auf **Einmaliges Anmelden**.

    ![Konfigurieren des Links für einmaliges Anmelden][4]

2. Klicken Sie im Dialogfeld **SSO-Methode auswählen** für den Modus **SAML** auf **Auswählen**, um einmaliges Anmelden zu aktivieren.

    ![Configure single sign-on](common/tutorial_general_301.png)

3. Klicken Sie auf der Seite **Einmaliges Anmelden (SSO) mit SAML einrichten** auf das Symbol **Bearbeiten**, um das Dialogfeld **Grundlegende SAML-Konfiguration** zu öffnen.

    ![Configure single sign-on](common/editconfigure.png)

4. Führen Sie im Abschnitt **Grundlegende SAML-Konfiguration** die folgenden Schritte aus, wenn Sie die Anwendung im **IDP**-initiierten Modus konfigurieren möchten:

    ![SSO-Informationen zur Domäne und zu den URLs für Peakon](./media/peakon-tutorial/tutorial_peakon_url.png)

    a. Geben Sie im Textfeld **Bezeichner** eine URL nach folgendem Muster ein: `https://app.peakon.com/saml/<companyid>/metadata`

    b. Geben Sie im Textfeld **Antwort-URL** eine URL nach folgendem Muster ein: `https://app.peakon.com/saml/<companyid>/assert`

5. Klicken Sie auf **Zusätzliche URLs festlegen**, und führen Sie den folgenden Schritt aus, wenn Sie die Anwendung im **SP-initiierten Modus** konfigurieren möchten:

    ![SSO-Informationen zur Domäne und zu den URLs für Peakon](./media/peakon-tutorial/tutorial_peakon_url1.png)

    Geben Sie im Textfeld **Anmelde-URL** eine URL wie die Folgende ein: `https://app.peakon.com/login`.

    > [!NOTE]
    > Hierbei handelt es sich um Beispielwerte. Ersetzen Sie diese Werte durch den tatsächlichen Bezeichner und die tatsächliche Antwort-URL. Darauf wird später im Tutorial eingegangen.

6. Klicken Sie im Abschnitt **SAML-Signaturzertifikat** auf **Herunterladen**, um das **Zertifikat (Rohdaten)** herunterzuladen, und speichern Sie dann die Zertifikatsdatei auf Ihrem Computer.

    ![Downloadlink für das Zertifikat](./media/peakon-tutorial/tutorial_peakon_certificate.png) 

7. Kopieren Sie im Abschnitt **Peakon einrichten** die entsprechenden URLs gemäß Ihren Anforderungen.

    a. Anmelde-URL

    b. Azure AD-Bezeichner

    c. Abmelde-URL

    ![Peakon-Konfiguration](common/configuresection.png)

8. Melden Sie sich in einem anderen Webbrowserfenster als Administrator bei Peakon an.

9. Klicken Sie auf der Menüleiste auf der linken Seite auf **Konfiguration**, und navigieren Sie dann zu **Integrationen**.

    ![Die Konfiguration](./media/peakon-tutorial/tutorial_peakon_config.png)

10. Klicken Sie auf der Seite **Integrationen** auf **Einmaliges Anmelden**.

    ![Einmaliges Anmelden](./media/peakon-tutorial/tutorial_peakon_single.png)

11. Klicken Sie unter dem Abschnitt **Einmaliges Anmelden** auf **Aktivieren**.

    ![Aktivieren](./media/peakon-tutorial/tutorial_peakon_enable.png)

12. Führen Sie im Abschnitt **Einmaliges Anmelden für Mitarbeiter mit SAML** die folgenden Schritte aus:

    ![SAML](./media/peakon-tutorial/tutorial_peakon_saml.png)

    a. Fügen Sie in das Textfeld **SSO-Anmelde-URL** den Wert der **Anmelde-URL** ein, den Sie aus dem Azure-Portal kopiert haben.

    b. Fügen Sie in das Textfeld **SSO-Abmelde-URL** den Wert der **Abmelde-URL** ein, den Sie aus dem Azure-Portal kopiert haben.

    c. Klicken Sie auf **Datei auswählen**, um das aus dem Azure-Portal heruntergeladene Zertifikat in das Feld „Zertifikat“ hochzuladen.

    d. Klicken Sie auf das **Symbol**, um die **Entitäts-ID** zu kopieren und im Azure-Portal im Abschnitt **Grundlegende SAML-Konfiguration** in das Textfeld **Bezeichner** einzufügen.

    e. Klicken Sie auf das **Symbol**, um die **Antwort-URL (ACS)** zu kopieren und im Azure-Portal im Abschnitt **Grundlegende SAML-Konfiguration** in das Textfeld **Antwort-URL** einzufügen.

    f. Klicken Sie unten auf der Seite auf **Speichern**.

### <a name="creating-an-azure-ad-test-user"></a>Erstellen eines Azure AD-Testbenutzers

Das Ziel dieses Abschnitts ist das Erstellen eines Testbenutzers namens Britta Simon im Azure-Portal.

1. Wählen Sie im Azure-Portal im linken Bereich die Option **Azure Active Directory**, **Benutzer** und dann **Alle Benutzer** aus.

    ![Azure AD-Benutzer erstellen][100]

2. Wählen Sie oben im Bildschirm die Option **Neuer Benutzer** aus.

    ![Erstellen eines Azure AD-Testbenutzers](common/create_aaduser_01.png) 

3. Führen Sie in den Benutzereigenschaften die folgenden Schritte aus.

    ![Erstellen eines Azure AD-Testbenutzers](common/create_aaduser_02.png)

    a. Geben Sie im Feld **Name** den Namen **BrittaSimon** ein.
  
    b. Geben Sie im Feld **Benutzername** den Namen **brittasimon@yourcompanydomain.extension** ein.  
    Zum Beispiel, BrittaSimon@contoso.com

    c. Wählen Sie **Eigenschaften** aus, aktivieren Sie das Kontrollkästchen **Kennwort anzeigen**, und notieren Sie sich dann den Wert, der im Feld „Kennwort“ angezeigt wird.

    d. Klicken Sie auf **Erstellen**.

### <a name="creating-a-peakon-test-user"></a>Erstellen eines Peakon-Testbenutzers

Damit sich Azure AD-Benutzer bei Peakon anmelden können, müssen sie in Peakon bereitgestellt werden.  
Im Fall von Peakon ist die Bereitstellung eine manuelle Aufgabe.

**Führen Sie zum Bereitstellen eines Benutzerkontos die folgenden Schritte aus:**

1. Melden Sie sich bei der Peakon-Unternehmenswebsite als Administrator an.

2. Klicken Sie auf der Menüleiste auf der linken Seite auf **Konfiguration**, und navigieren Sie dann zu **Mitarbeiter**.

    ![Mitarbeiter](./media/peakon-tutorial/tutorial_peakon_employee.png)

3. Klicken Sie oben rechts auf der Seite auf **Mitarbeiter hinzufügen**.

      ![Mitarbeiter hinzufügen](./media/peakon-tutorial/tutorial_peakon_addemployee.png)

3. Führen Sie auf der Dialogfeldseite **Neuer Mitarbeiter** die folgenden Schritte aus:

     ![Neuer Mitarbeiter](./media/peakon-tutorial/tutorial_peakon_create.png)

    a. Geben Sie im Textfeld **Name** den Vornamen **Britta** und den Nachnamen **simon** ein.

    b. Geben Sie im Textfeld **E-Mail-Adresse** die E-Mail-Adresse (z. B. **Brittasimon@contoso.com**) ein.

    c. Klicken Sie auf **Mitarbeiter erstellen**.

### <a name="assigning-the-azure-ad-test-user"></a>Zuweisen des Azure AD-Testbenutzers

In diesem Abschnitt ermöglichen Sie Britta Simon die Verwendung des einmaligen Anmeldens von Azure, indem Sie ihr Zugriff auf Peakon gewähren.

1. Wählen Sie im Azure-Portal die Option **Unternehmensanwendungen** und dann **Alle Anwendungen** aus.

    ![Benutzer zuweisen][201]

2. Wählen Sie in der Anwendungsliste den Eintrag **Peakon** aus.

    ![Configure single sign-on](./media/peakon-tutorial/tutorial_peakon_app.png) 

3. Klicken Sie im Menü auf der linken Seite auf **Benutzer und Gruppen**.

    ![Benutzer zuweisen][202]

4. Klicken Sie auf die Schaltfläche **Hinzufügen**. Wählen Sie dann im Dialogfeld **Zuweisung hinzufügen** die Option **Benutzer und Gruppen** aus.

    ![Benutzer zuweisen][203]

5. Wählen Sie im Dialogfeld **Benutzer und Gruppen** in der Liste „Benutzer“ den Eintrag **Britta Simon** aus, und klicken Sie dann unten im Bildschirm auf die Schaltfläche **Auswählen**.

6. Wählen Sie im Dialogfeld **Zuweisung hinzufügen** die Schaltfläche **Zuweisen** aus.

### <a name="testing-single-sign-on"></a>Testen der einmaligen Anmeldung

In diesem Abschnitt testen Sie die Azure AD-Konfiguration für einmaliges Anmelden über den Zugriffsbereich.

Wenn Sie im Zugriffsbereich auf die Kachel „Peakon“ klicken, sollten Sie automatisch bei Ihrer Peakon-Anwendung angemeldet werden.
Weitere Informationen zum Zugriffsbereich finden Sie unter [Einführung in den Zugriffsbereich](../user-help/active-directory-saas-access-panel-introduction.md).

## <a name="additional-resources"></a>Zusätzliche Ressourcen

* [Liste der Tutorials zur Integration von SaaS-Apps in Azure Active Directory](tutorial-list.md)
* [Was bedeuten Anwendungszugriff und einmaliges Anmelden mit Azure Active Directory?](../manage-apps/what-is-single-sign-on.md)

<!--Image references-->

[1]: common/tutorial_general_01.png
[2]: common/tutorial_general_02.png
[3]: common/tutorial_general_03.png
[4]: common/tutorial_general_04.png

[100]: common/tutorial_general_100.png

[201]: common/tutorial_general_201.png
[202]: common/tutorial_general_202.png
[203]: common/tutorial_general_203.png
