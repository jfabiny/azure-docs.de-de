---
title: Hinzufügen öffentlicher IP-Adressen in Azure Stack | Microsoft Docs
description: Erfahren Sie, wie Sie Azure Stack weitere öffentliche IP-Adressen hinzufügen können.
services: azure-stack
documentationcenter: ''
author: jeffgilb
manager: femila
editor: ''
ms.assetid: ''
ms.service: azure-stack
ms.workload: na
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 09/17/2018
ms.author: jeffgilb
ms.reviewer: scottnap
ms.lastreviewed: 09/17/2018
ms.openlocfilehash: d81374b110523e48e06725d3d3153e61135471cc
ms.sourcegitcommit: 898b2936e3d6d3a8366cfcccc0fccfdb0fc781b4
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/30/2019
ms.locfileid: "55251621"
---
# <a name="add-public-ip-addresses"></a>Hinzufügen öffentlicher IP-Adressen
*Anwendungsbereich: Integrierte Azure Stack-Systeme und Azure Stack Development Kit*  

Erfahren Sie, wie Sie Azure Stack weitere öffentliche IP-Adressen hinzufügen können.  In diesem Artikel beziehen wir uns auf die externen Adressen als öffentliche IP-Adressen, aber in Azure Stack soll dies das Hinzufügen von IP-Adressblöcken zu Ihrem externen Netzwerk bedeuten.  Ob dieses externe Netzwerk öffentlich internetroutingfähig ist oder sich in einem Intranet befindet und einen privaten Adressraum verwendet, spielt für die Zwecke dieses Artikels keine Rolle.  Die Schritte sind identisch. 

## <a name="add-a-public-ip-address-pool"></a>Hinzufügen eines öffentlichen IP-Adresspools
Sie können Ihrem Azure Stack-System jederzeit nach der erstmaligen Bereitstellung des Azure Stack-Systems öffentliche IP-Adressen hinzufügen. Schauen Sie sich an, wie Sie die [Nutzung öffentlicher IP-Adressen anzeigen](azure-stack-viewing-public-ip-address-consumption.md) können, um zu sehen, welche aktuelle Nutzung und Verfügbarkeit öffentlicher IP-Adressen in Ihrem Azure Stack vorliegt.

Auf Übersichtsebene sieht der Vorgang des Hinzufügens eines neuen öffentlichen IP-Adressblocks zu Azure Stack folgendermaßen aus:

 ![Hinzufügen eines IP-Datenflusses](media/azure-stack-add-ips/flow.PNG)

## <a name="obtain-the-address-block-from-your-provider"></a>Abrufen des Adressblocks von Ihrem Anbieter
Zunächst müssen Sie den Adressblock abrufen, den Sie Azure Stack hinzufügen möchten.  Je nachdem, woher Sie Ihren Adressblock beziehen, müssen Sie die Vorlaufzeit berücksichtigen und diese mit der Rate abgleichen, mit der Sie öffentliche IP-Adressen in Azure Stack nutzen.  

> [!IMPORTANT]
> Azure Stack akzeptiert jeden von Ihnen bereitgestellten Adressblock, sofern es sich um einen gültigen Adressblock handelt und er sich nicht mit einem vorhandenen Adressbereich in Azure Stack überschneidet.  Stellen Sie sicher, dass Sie einen gültigen Adressblock erhalten, der routingfähig ist und nicht mit dem externen Netzwerk überlappt, mit dem Azure Stack verbunden ist.  Nachdem Sie den Bereich Azure Stack hinzugefügt haben, können Sie ihn nicht mehr entfernen.

## <a name="add-the-ip-address-range-to-azure-stack"></a>Hinzufügen des IP-Adressbereichs zu Azure Stack

1. Navigieren Sie in einem Internetbrowser zu Ihrem Verwaltungsportaldashboard.  In diesem Beispiel verwenden wir https://adminportal.local.azurestack.external.  
2.  Melden Sie sich als Cloudoperator am Azure Stack-Verwaltungsportal an.
3.  Suchen Sie im Standarddashboard nach der Liste „Regionsverwaltung“, und wählen Sie die Region aus, die Sie verwalten möchten (beispielsweise „lokal“).
4.  Suchen Sie nach der Kachel „Ressourcenanbieter“, und klicken Sie auf den Netzwerkressourcenanbieter.
5.  Klicken Sie auf die Kachel für die Nutzung öffentlicher IP-Pools.
6.  Klicken Sie auf die Schaltfläche „IP-Pool hinzufügen“.
7.  Geben Sie einen Namen für den IP-Pool an.  Der von Ihnen ausgewählte Name dient nur dazu, den IP-Pool leicht zu identifizieren, sodass Sie einen beliebigen Namen verwenden können.  Es hat sich als bewährte Methode herausgestellt, den gleichen Namen wie der Adressbereich zu verwenden, aber das ist nicht erforderlich.
8.   Geben Sie den Adressblock in CIDR-Notation ein, den Sie hinzufügen möchten.  Beispiel:  192.168.203.0/24
9.  Wenn Sie einen gültigen CIDR-Bereich im Feld „Adressbereich“ (CIDR-Block) angeben, werden die Felder „IP-Startadresse“, „IP-Endadresse“ und „Verfügbare IP-Adressen“ automatisch mit Daten aufgefüllt.  Sie sind schreibgeschützt und werden automatisch generiert, sodass Sie diese Angaben nicht ändern können, ohne den Wert im Feld „Adressbereich“ zu ändern.
10. Nach dem Überprüfen der Informationen auf dem Blatt und dem Bestätigen, dass alle Angaben richtig sind, klicken Sie auf „OK“, um die Änderung zu übernehmen und den Adressbereich Azure Stack hinzuzufügen.

## <a name="update-the-acls-on-your-top-of-rack-switches"></a>Aktualisieren der ACLs für Ihre ToR-Switches
Die letzte Aktion, die Sie ausführen müssen, damit der neu hinzugefügte IP-Bereich funktioniert, ist die Aktualisierung der Zugriffssteuerungslisten (ACLs) für Ihre ToR-Switches (Top-of-Rack).  Die ACLs für die ToR-Switches sind so gesperrt, dass die Konnektivität außerhalb von Azure Stack mit dem neu hinzugefügten IP-Bereich erst funktioniert, wenn der neue Bereich den ACLs für den Switch hinzugefügt wird.  

Sie müssen sich mit Ihrem OEM in Verbindung setzen und mit ihm zusammenarbeiten, um die ACLs für ToR-Switches zu aktualisieren.  OEMs verfügen über die erforderlichen Tools, um dies auf unterstützte Weise auszuführen.


## <a name="next-steps"></a>Nächste Schritte 
[Überprüfen von Knotenaktionen für Skalierungseinheiten](azure-stack-node-actions.md) 
