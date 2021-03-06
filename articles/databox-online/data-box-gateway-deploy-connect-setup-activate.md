---
title: Verbinden mit und Konfigurieren und Aktivieren von Azure Data Box Gateway im Azure-Portal | Microsoft-Dokumentation
description: Im dritten Tutorial zur Bereitstellung von Data Box Gateway erfahren Sie, wie Sie Ihr virtuelles Gerät verbinden, einrichten und aktivieren können.
services: databox
author: alkohli
ms.service: databox
ms.subservice: gateway
ms.topic: article
ms.date: 01/09/2019
ms.author: alkohli
ms.openlocfilehash: 887c1d554cd5bd2b935178a77a2de19e687ca3f2
ms.sourcegitcommit: 9b6492fdcac18aa872ed771192a420d1d9551a33
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/22/2019
ms.locfileid: "54450403"
---
# <a name="tutorial-connect-set-up-activate-azure-data-box-gateway-preview"></a>Tutorial: Verbinden, Einrichten und Aktivieren von Azure Data Box Gateway (Vorschauversion) 

## <a name="introduction"></a>Einführung

In diesem Tutorial wird beschrieben, wie Sie sich mit Ihrem Data Box Gateway-Gerät über die lokale Webbenutzeroberfläche verbinden und wie Sie es einrichten und aktivieren. 

Der Einrichtungs- und Aktivierungsvorgang kann ca. 10 Minuten dauern. 

In diesem Tutorial lernen Sie Folgendes:

> [!div class="checklist"]
> * Herstellen einer Verbindung mit dem virtuellen Gerät
> * Einrichten und Aktivieren des virtuellen Geräts

Wenn Sie kein Azure-Abonnement besitzen, können Sie ein [kostenloses Konto](https://azure.microsoft.com/free/?WT.mc_id=A261C142F) erstellen, bevor Sie beginnen.


> [!IMPORTANT]
> - Data Box Gateway ist in der Vorschauphase. Lesen Sie die [Azure-Vertragsbedingungen für Vorschauversionen](https://azure.microsoft.com/support/legal/preview-supplemental-terms/), bevor Sie diese Lösung bestellen und bereitstellen. 


## <a name="prerequisites"></a>Voraussetzungen

Überprüfen Sie Folgendes, bevor Sie Data Box Gateway konfigurieren und einrichten:

* Sie haben ein virtuelles Gerät bereitgestellt und eine damit verbundene URL abgerufen, wie unter [Bereitstellen eines Data Box Gateways in Hyper-V](data-box-gateway-deploy-provision-hyperv.md) bzw. [Bereitstellen eines Data Box Gateways in VMware](data-box-gateway-deploy-provision-vmware.md) beschrieben.
* Sie haben den Aktivierungsschlüssel vom Data Box Gateway-Dienst erhalten, den Sie zur Verwaltung von Data Box Gateway-Geräten erstellt haben. Weitere Informationen finden Sie unter [Vorbereiten der Bereitstellung von Azure Data Box Gateway](data-box-gateway-deploy-prep.md)

<!--* If this is the second or subsequent virtual device that you are registering with an existing StorSimple Device Manager service, you should have the service data encryption key. This key was generated when the first device was successfully registered with this service. If you have lost this key, see [Get the service data encryption key](storsimple-ova-web-ui-admin.md#get-the-service-data-encryption-key) for your Data Box Gateway.-->

## <a name="connect-to-the-local-web-ui-setup"></a>Herstellen einer Verbindung mit der lokalen Webbenutzeroberfläche 

1. Öffnen Sie ein Browserfenster, und stellen Sie eine Verbindung mit der lokalen Webbenutzeroberfläche her. Geben Sie Folgendes ein: 
   
   [https://ip-address-of-network-interface](https://ip-address-of-network-interface)
   
   Verwenden Sie die Verbindungs-URL aus dem vorherigen Tutorial. Es wird eine Fehlermeldung mit dem Hinweis angezeigt, dass ein Problem mit dem Sicherheitszertifikat der Website aufgetreten ist. Klicken Sie auf **Mit dieser Webseite fortfahren**. (Diese Schritte können je nach Browser unterschiedlich sein.)
   
    ![](./media/data-box-gateway-deploy-connect-setup-activate/image2.png)

2. Melden Sie sich bei der Webbenutzeroberfläche des virtuellen Geräts an. Das Standardkennwort lautet *Password1*. 
   
    ![](./media/data-box-gateway-deploy-connect-setup-activate/image3.png)

3. Sie werden aufgefordert, das Geräteadministratorkennwort zu ändern. Geben Sie ein neues Kennwort mit 8 bis 16 Zeichen ein. Das Kennwort muss drei der folgenden Elemente enthalten: Großbuchstaben, Kleinbuchstaben, Zahlen und Sonderzeichen.

    ![](./media/data-box-gateway-deploy-connect-setup-activate/image4.png)

Sie befinden sich jetzt im **Dashboard** Ihres Geräts.

## <a name="set-up-and-activate-the-virtual-device"></a>Einrichten und Aktivieren des virtuellen Geräts
 
1. Im Dashboard können Sie zu den verschiedenen Einstellungen wechseln, die zum Konfigurieren und Registrieren des virtuellen Geräts beim Data Box Gateway-Dienst erforderlich sind. Die **Netzwerkeinstellungen**, **Webproxyeinstellungen** und **Uhrzeiteinstellungen** sind optional. Die einzigen erforderlichen Einstellungen sind **Gerätename** und **Cloudeinstellungen**.
   
    ![](./media/data-box-gateway-deploy-connect-setup-activate/image5.png)

2. Geben Sie auf der Seite **Gerätename** einen Anzeigenamen für Ihr Gerät an. Der Anzeigename kann 1 bis 15 Zeichen lang sein und Buchstaben, Zahlen und Bindestriche enthalten.

    ![](./media/data-box-gateway-deploy-connect-setup-activate/image6.png)

3. (Optional) Konfigurieren Sie Ihre **Netzwerkeinstellungen**. Es werden eine oder mehrere Netzwerkschnittstellen angezeigt, je nachdem, wie viele Sie in dem zugrunde liegenden virtuellen Computer konfiguriert haben. Die Seite **Netzwerkeinstellungen** für ein virtuelles Gerät mit aktivierter Netzwerkschnittstelle ist nachstehend abgebildet.
    
    ![](./media/data-box-gateway-deploy-connect-setup-activate/image7.png)
   
    Wenn Sie Netzwerkeinstellungen konfigurieren, berücksichtigen Sie Folgendes:

    - Falls DHCP in Ihrer Umgebung aktiviert ist, werden Netzwerkschnittstellen automatisch konfiguriert. Daher werden IP-Adresse, Subnetz, Gateway und DNS automatisch zugewiesen.
    - Wenn DHCP nicht aktiviert ist, weisen Sie bei Bedarf statische IP-Adressen zu.
    - Sie können die Netzwerkschnittstelle als IPv4 konfigurieren.

    >[!NOTE] 
    > Wir empfehlen, die lokale IP-Adresse der Netzwerkschnittstelle nicht von statisch auf DHCP umzustellen, es sei denn, Sie haben eine andere IP-Adresse für die Verbindung zum Gerät. Wenn Sie eine Netzwerkschnittstelle verwenden und zu DHCP wechseln, gibt es keine Möglichkeit, die DHCP-Adresse zu bestimmen. Wenn Sie zu einer DHCP-Adresse wechseln möchten, warten Sie, bis sich das Gerät beim Dienst registriert hat, und ändern Sie dann. Sie können dann die IPs aller Adapter im Azure-Portal in den **Geräteeigenschaften** für Ihren Dienst anzeigen.

4. Optional: Konfigurieren Sie Ihren Webproxyserver. Die Webproxykonfiguration ist optional. Achten Sie jedoch bei Verwendung eines Webproxys darauf, dass dieser nur hier konfiguriert werden kann.
   
   ![](./media/data-box-gateway-deploy-connect-setup-activate/image8.png)
   
   Auf der Seite **Webproxy** :
   
   1. Geben Sie die **Webproxy-URL** in diesem Format an: *http://&lt;Host-IP-Adresse oder FQDN&gt;:Portnummer*. Beachten Sie, dass HTTPS-URLs nicht unterstützt werden.
   2. Geben Sie unter **Authentifizierung** die Option **Einfach** oder **Keine** an.
   3. Wenn Sie die Authentifizierung verwenden, müssen Sie auch einen **Benutzernamen** und ein **Kennwort** angeben.
   4. Klicken Sie auf **Anwenden**. Die konfigurierten Webproxyeinstellungen werden überprüft und angewendet.

5. Optional: Konfigurieren Sie die Zeiteinstellungen für Ihr Gerät, z. B. die Zeitzone und die primären und sekundären NTP-Server. NTP-Server sind für die Zeitsynchronisierung erforderlich, damit Ihr Gerät bei den Clouddienstanbietern authentifiziert werden kann.
    
    ![](./media/data-box-gateway-deploy-connect-setup-activate/image9.png)
    
    Auf der Seite **Uhrzeiteinstellungen** :
    
    1. Legen Sie über die Dropdownliste die **Zeitzone** basierend auf dem geografischen Standort fest, an dem das Gerät bereitgestellt wird. Die Standardzeitzone für Ihr Gerät ist „PST“. Ihr Gerät verwendet diese Zeitzone für alle geplanten Vorgänge.
    2. Geben Sie einen **primären NTP-Server** für das Gerät an, oder übernehmen Sie den Standardwert „time.windows.com“. Stellen Sie sicher, dass Ihr Netzwerk NTP-Datenverkehr vom Rechenzentrum ins Internet zulässt.
    3. Geben Sie optional einen **sekundären NTP-Server** für Ihr Gerät an.
    4. Klicken Sie auf **Übernehmen**. Die konfigurierten Uhrzeiteinstellungen werden überprüft und angewendet.

6. Aktivieren Sie Ihr Gerät im Azure-Portal auf der Seite **Cloudeinstellungen** für den Data Box Gateway-Dienst.
    
    1. Geben Sie den **Aktivierungsschlüssel** ein, den Sie in [Aktivierungsschlüssel abrufen](data-box-gateway-deploy-prep.md#get-the-activation-key) für Data Box Gateway abgerufen haben.

    2. Klicken Sie auf **Aktivieren**. 
       
         ![](./media/data-box-gateway-deploy-connect-setup-activate/image10.png)
    
    3. Sie müssen ggf. eine Minute warten, bis das Gerät erfolgreich aktiviert wurde. Nach der Aktivierung wird die Seite mit der Angabe aktualisiert, dass das Gerät erfolgreich aktiviert wurde.


## <a name="next-steps"></a>Nächste Schritte

In diesem Tutorial haben Sie sich mit den folgenden Themen zu Data Box Gateway befasst:

> [!div class="checklist"]
> * Herstellen einer Verbindung mit dem virtuellen Gerät
> * Einrichten und Aktivieren des virtuellen Geräts


Fahren Sie mit dem nächsten Tutorial fort, um zu erfahren, wie Sie Daten mit Data Box Gateway übertragen.

> [!div class="nextstepaction"]
> [Übertragen von Daten mit Data Box Gateway](./data-box-gateway-deploy-add-shares.md)
