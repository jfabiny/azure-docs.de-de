---
title: 'Azure AD Connect: Funktionen in der Vorschau | Microsoft-Dokumentation'
description: In diesem Thema werden Funktionen detaillierter beschrieben, die sich in Azure AD Connect in der Preview befinden.
services: active-directory
documentationcenter: ''
author: billmath
manager: daveba
editor: ''
ms.assetid: c75cd8cf-3eff-4619-bbca-66276757cc07
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: conceptual
ms.date: 07/13/2017
ms.subservice: hybrid
ms.author: billmath
ms.openlocfilehash: afbd48b8793e8b16597efb1e3996058b7450e03e
ms.sourcegitcommit: 5978d82c619762ac05b19668379a37a40ba5755b
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/31/2019
ms.locfileid: "55497094"
---
# <a name="more-details-about-features-in-preview"></a>Weitere Informationen zu den Funktionen in der Vorschau
In diesem Thema wird beschrieben, wie Sie Funktionen verwenden, die sich derzeit in der Vorschau befinden.

## <a name="group-writeback"></a>Gruppenrückschreiben
Mit der Option zum Gruppenrückschreiben, die unter den optionalen Features aufgeführt ist, können Sie **Office 365-Gruppen** in eine Gesamtstruktur zurückschreiben, in der Exchange installiert ist. Dies ist eine Gruppe, die immer in der Cloud verwaltet wird. Wenn Sie über lokales Exchange verfügen, können Sie diese Gruppen in die lokale Installation zurückschreiben, damit Benutzer mit einem lokalen Exchange-Postfach E-Mails von diesen Gruppen empfangen und an sie senden können.

Weitere Informationen zu Office 365-Gruppen und zu deren Verwendung finden Sie [hier](https://aka.ms/O365g).

Eine Office 365-Gruppe wird im lokalen AD DS als Verteilergruppe dargestellt. Auf dem lokalen Exchange-Server muss das kumulative Update 8 für Exchange Server 2013 (vom März 2015) oder Exchange 2016 installiert sein, damit dieser neue Gruppentyp erkannt wird.

**Hinweise während der Vorschau**

* Das Adressbuchattribut ist in der Vorschau derzeit nicht aufgefüllt. Ohne dieses Attribut ist diese Gruppe in der globalen Adressliste nicht sichtbar. Am einfachsten können Sie dieses Attribut mit dem Exchange PowerShell-Cmdlet `update-recipient`auffüllen.
* Nur Gesamtstrukturen mit dem Exchange-Schema sind gültige Ziele für Gruppen. Wenn kein Exchange erkannt wurde, kann das Gruppenrückschreiben nicht aktiviert werden.
* Derzeit werden nur Bereitstellungen unterstützt, bei der eine Exchange-Organisation eine einzelne Gesamtstruktur darstellt. Wenn Sie lokal über mehrere Exchange-Organisationen verfügen, benötigen Sie eine lokale Lösung für die Synchronisierung der globalen Adressliste, damit diese Gruppen in Ihren anderen Gesamtstrukturen angezeigt werden können.
* Das Feature „Gruppenrückschreiben“ verarbeitet keine Sicherheitsgruppen oder Verteilergruppen.

> [!NOTE]
> Für das Gruppenrückschreiben ist ein Azure AD Premium-Abonnement erforderlich.
> 
>

## <a name="user-writeback"></a>Rückschreiben von Benutzern
> [!IMPORTANT]
> Die Vorschaufunktion „Rückschreiben von Benutzern“ wurde im Azure AD Connect-Update vom August 2015 entfernt. Wenn Sie diese Funktion aktiviert haben, sollten Sie sie deaktivieren.
>
>

## <a name="next-steps"></a>Nächste Schritte
Fahren Sie mit Ihrer [benutzerdefinierten Installation von Azure AD Connect](how-to-connect-install-custom.md)fort.

Weitere Informationen zum [Integrieren lokaler Identitäten in Azure Active Directory](whatis-hybrid-identity.md).
