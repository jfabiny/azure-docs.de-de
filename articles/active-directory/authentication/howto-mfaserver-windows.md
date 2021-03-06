---
title: Windows-Authentifizierung und Azure MFA-Server | Microsoft-Dokumentation
description: Bereitstellen von Windows-Authentifizierung und Azure Multi-Factor Authentication-Server
services: multi-factor-authentication
ms.service: active-directory
ms.subservice: authentication
ms.topic: conceptual
ms.date: 07/11/2018
ms.author: joflore
author: MicrosoftGuyJFlo
manager: daveba
ms.reviewer: michmcla
ms.openlocfilehash: e2f6c8986ec5ea21a0c12dfa3f7c0aec9b30ef49
ms.sourcegitcommit: 58dc0d48ab4403eb64201ff231af3ddfa8412331
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/26/2019
ms.locfileid: "55080713"
---
# <a name="windows-authentication-and-azure-multi-factor-authentication-server"></a>Windows-Authentifizierung und Azure Multi-Factor Authentication-Server

Die Windows-Authentifizierung für Anwendungen können Sie mithilfe des Windows-Authentifizierungsabschnitts des Azure Multi-Factor Authentication-Servers aktivieren und konfigurieren. Bedenken Sie vor dem Einrichten der Windows-Authentifizierung Folgendes:

* Nach der Einrichtung muss Azure Multi-Factor Authentication für Terminaldienste neu gestartet werden.
* Wenn "Multi-Factor Authentication-Benutzerabgleich erforderlich" aktiviert ist und Sie nicht in der Benutzerliste aufgeführt sind, können Sie sich nach dem Neustart des Computers nicht anmelden.
* Vertrauenswürdige IPs hängen davon ab, ob die Anwendung der Client-IP die Authentifizierung bereitstellen kann. Derzeit werden nur Terminaldienste unterstützt.  

> [!NOTE]
> Dieses Feature wird nicht unterstützt, um Terminaldienste unter Windows Server 2012 R2 zu sichern.

## <a name="to-secure-an-application-with-windows-authentication-use-the-following-procedure"></a>Um eine Anwendung mit der Windows-Authentifizierung zu sichern, verwenden Sie das folgende Verfahren.
1. Klicken Sie im Azure Multi-Factor Authentication-Server auf das Symbol "Windows-Authentifizierung".
   ![Windows-Authentifizierung](./media/howto-mfaserver-windows/windowsauth.png)
2. Aktivieren Sie das Kontrollkästchen **Windows-Authentifizierung aktivieren**. Standardmäßig ist dieses Kontrollkästchen deaktiviert.
3. Die Registerkarte "Anwendungen" gibt dem Administrator die Möglichkeit, eine oder mehrere Anwendungen für die Windows-Authentifizierung zu konfigurieren.
4. Wählen Sie einen Server oder eine Anwendung, und geben Sie an, ob der Server/die Anwendung aktiviert ist. Klicken Sie auf **OK**.
5. Klicken Sie auf **Hinzufügen...**.
6. Auf der Registerkarte "Vertrauenswürdige IP-Adressen" können Sie Azure Multi-Factor Authentication für Windows-Sitzungen überspringen, die aus bestimmten IPs stammen. Wenn Mitarbeiter die Anwendung im Büro und zu Hause verwenden, können Sie z. B. entscheiden, dass deren Telefone für Azure Multi-Factor Authentication im Büro nicht klingeln sollen. Dazu geben Sie das Bürosubnetz als Eintrag "Vertrauenswürdige IPs" an.
7. Klicken Sie auf **Hinzufügen...**.
8. Wählen Sie **Einzelne IP-Adresse** aus, wenn Sie eine einzelne IP-Adresse überspringen möchten.
9. Wählen Sie **IP-Bereich** aus, wenn Sie einen ganzen IP-Bereich überspringen möchten. Beispiel 10.63.193.1-10.63.193.100.
10. Wählen Sie **Subnetz** aus, wenn Sie einen IP-Bereich mithilfe der Subnetznotation angeben möchten. Geben Sie die Start-IP des Subnetzes an, und wählen Sie die entsprechende Netzmaske aus der Dropdown-Liste.
11. Klicken Sie auf **OK**.

## <a name="next-steps"></a>Nächste Schritte

- [Konfigurieren von Drittanbieter-VPN-Appliances für Azure MFA-Server](howto-mfaserver-nps-vpn.md)

- [Verbessern der vorhandenen Authentifizierungsinfrastruktur mit der NPS-Erweiterung für Azure MFA](howto-mfa-nps-extension.md)
