---
title: Erstellen eines benutzerdefinierten Aktivierungsworts – Speech Services
titleSuffix: Azure Cognitive Services
description: Ihr Gerät lauscht immer auf ein Aktivierungswort (oder einen Aktivierungsausdruck). Wenn der Benutzer das Aktivierungswort nennt, sendet das Gerät sämtliche nachfolgende Audioaufnahmen an die Cloud, bis der Benutzer aufhört zu sprechen. Durch das Anpassen Ihres Aktivierungsworts können Sie Ihr Gerät auf effektive Weise differenzieren und Ihr Branding stärken.
services: cognitive-services
author: erhopf
manager: cgronlun
ms.service: cognitive-services
ms.subservice: speech-service
ms.topic: conceptual
ms.date: 12/06/2018
ms.author: erhopf
ms.custom: seodec18
ms.openlocfilehash: 8a736d6dcdac5fe6d4eec4f2ef5e4387ebdcdc80
ms.sourcegitcommit: 95822822bfe8da01ffb061fe229fbcc3ef7c2c19
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 01/29/2019
ms.locfileid: "55219089"
---
# <a name="create-a-custom-wake-word-by-using-the-speech-service"></a>Erstellen eines benutzerdefinierten Aktivierungsworts mit dem Spracherkennungsdienst

Ihr Gerät lauscht immer auf ein Aktivierungswort (oder einen Aktivierungsausdruck). „Hey Cortana“ ist beispielsweise ein Aktivierungswort für den Cortana-Assistenten. Wenn der Benutzer das Aktivierungswort nennt, sendet das Gerät sämtliche nachfolgende Audioaufnahmen an die Cloud, bis der Benutzer aufhört zu sprechen. Durch das Anpassen Ihres Aktivierungsworts können Sie Ihr Gerät auf effektive Weise differenzieren und Ihr Branding stärken.

In diesem Artikel erfahren Sie, wie Sie für Ihr Gerät ein benutzerdefiniertes Aktivierungswort erstellen.

## <a name="choose-an-effective-wake-word"></a>Auswählen eines effektiven Aktivierungsworts

Berücksichtigen Sie bei der Auswahl eines Aktivierungsworts die folgenden Richtlinien:

* Ihr Aktivierungswort sollte ein englisches Wort oder ein englischer Ausdruck sein. Es sollte nicht länger als zwei Sekunden dauern, es auszusprechen.

* Wörter mit 4 bis 7 Silben eignen sich am besten. So ist „Hey, Computer“ beispielsweise ein gutes Aktivierungswort. Nur „Hey“ ist ein schlechtes Aktivierungswort.

* Bei Aktivierungswörtern sollten englische Ausspracheregeln befolgt werden.

* Durch ein einzigartiges Wort oder ein Kunstwort, das die allgemeinen englischen Ausspracheregeln befolgt, könnten Ergebnisse mit falsch positiven Werten verringert werden. „Computerama“ würde sich beispielsweise gut als Aktivierungswort eignen.

* Wählen Sie kein gängiges Wort aus. Die Wörter „eat“ und „go“ werden beispielsweise häufig in gewöhnlichen Konversationen gesagt. Sie könnten falsche Auslöser für Ihr Gerät sein.

* Vermeiden Sie die Verwendung eines Aktivierungsworts, das verschiedene Aussprachevarianten haben könnte. Benutzern müsste die „richtige“ Aussprache bekannt sein, um eine Antwort von ihrem Gerät erhalten zu können. „509“ kann beispielsweise als „five zero nine“, „five oh nine“ oder als „five hundred and nine“ ausgesprochen werden. „R.E.I.“ kann als „r-e-i“ oder als „ray“ ausgesprochen werden. „Live“ kann „/līv/“ oder „/liv/“ ausgesprochen werden.

* Verwenden Sie keine Sonderzeichen, Symbole oder Ziffern. „Go#“ und „20 + cats“ wären beispielsweise keine guten Aktivierungswörter. „Go sharp“ oder „twenty plus cats“ kann jedoch funktionieren. Sie können weiterhin die Symbole in Ihrem Branding sowie Marketing und Dokumentation zur Untermauerung der richtigen Aussprache verwenden.

> [!NOTE]
> Wenn Sie als Aktivierungswort ein markenrechtlich geschütztes Wort auswählen, sollten Sie sicherstellen, dass Sie Eigentümer dieser Marke sind oder über eine Berechtigung vom Eigentümer der Marke zur Verwendung des Worts verfügen. Microsoft haftet nicht für rechtliche Probleme, die möglicherweise durch Ihre Auswahl eines Aktivierungsworts auftreten.

## <a name="create-your-wake-word"></a>Erstellen Ihres Aktivierungsworts

Bevor Sie auf Ihrem Gerät ein benutzerdefiniertes Aktivierungswort verwenden können, müssen Sie das Aktivierungswort mithilfe des Microsoft-Diensts für die benutzerdefinierte Generierung eines Aktivierungsworts erstellen. Nachdem Sie ein Aktivierungswort angegeben haben, erstellt der Dienst eine Datei, die Sie anschließend zur Aktivierung Ihres Aktivierungsworts auf Ihrem Gerät in Ihrem Development Kit bereitstellen.

1. Navigieren Sie zum [Portal des Custom Speech Service](https://cris.ai/).

1. Erstellen Sie ein neues Konto. Verwenden Sie dabei die E-Mail-Adresse, an die Ihre Einladung für Azure Active Directory gesendet wurde.

    ![Erstellen eines neuen Kontos](media/speech-devices-sdk/wake-word-1.png)

1. Die Seite **Custom Wake Word** (Benutzerdefiniertes Aktivierungswort) ist nicht für die Öffentlichkeit verfügbar. Folglich ist kein direkter Link vorhanden, über den Sie zu der Seite gelangen. Das Custom Speech-Feature erfordert ein Azure-Abonnement, das Feature „Benutzerdefiniertes Aktivierungswort“ hingegen nicht. Wenn die Fehlerseite **Keine Abonnements gefunden** angezeigt wird, ersetzen Sie einfach **"Subscriptions?errorMessage=No%20Subscriptions%20found"** durch "**customkws**" in der URL, und drücken Sie die EINGABETASTE. Die URL muss eine der folgenden URLs sein: https://westus.cris.ai/customkws, https://eastasia.cris.ai/customkws oder https://northeurope.cris.ai/customkws abhängig von Ihrer Region.

    ![Die Seite „Benutzerdefiniertes Aktivierungswort“ ist ausgeblendet.](media/speech-devices-sdk/wake-word-4.png)

1. Geben Sie das gewünschte Aktivierungswort ein, und wählen Sie dann **Wort übermitteln** aus.

    ![Eingeben Ihres Aktivierungsworts](media/speech-devices-sdk/wake-word-5.png)

1. Es kann einige Minuten dauern, bis die Dateien generiert werden. Im Fenster Ihres Browsers müsste ein sich drehender Kreis angezeigt werden. Danach wird eine Informationsleiste angezeigt, in der Sie aufgefordert werden, eine ZIP-Datei herunterzuladen.

    ![Empfangen der ZIP-Datei](media/speech-devices-sdk/wake-word-6.png)

1. Speichern Sie die ZIP-Datei auf Ihrem Computer. Sie benötigen diese Datei, um das benutzerdefinierte Aktivierungswort im Development Kit bereitzustellen. Um das benutzerdefinierte Aktivierungswort bereitzustellen, befolgen Sie die Anweisungen unter [Erste Schritte mit dem SDK für sprachaktivierte Geräte](speech-devices-sdk-qsg.md).

1. Wählen Sie **Abmelden** aus.

## <a name="next-steps"></a>Nächste Schritte

Richten Sie zunächst ein [kostenloses Azure-Konto](https://azure.microsoft.com/free/) ein, und registrieren Sie sich für das Speech-Geräte-SDK.

> [!div class="nextstepaction"]
> [Registrieren für das Speech-Geräte-SDK](get-speech-devices-sdk.md)
