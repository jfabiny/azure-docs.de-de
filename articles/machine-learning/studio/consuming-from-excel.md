---
Titel: Nutzen des Webdiensts in Excel titleSuffix: Azure Machine Learning Studio – Beschreibung: Mit Azure Machine Learning Studio können Webdienste auf einfache Weise direkt von Excel aus aufgerufen werden, ohne einen Code schreiben zu müssen.
Dienste: machine-learning ms.service: machine-learning ms.subservice: studio ms.topic: Artikel

Autor: ericlicoding ms.author: amlstudiodocs ms.custom: seodec18 ms.date: 01.02.2018
---
# <a name="consuming-an-azure-machine-learning-studio-web-service-from-excel"></a>Nutzen ein Azure Machine Learning Studio-Webdiensts aus Excel

 Mit Azure Machine Learning Studio können Webdienste auf einfache Weise direkt von Excel aus aufgerufen werden, ohne einen Code schreiben zu müssen.

Wenn Sie Excel 2013 (oder höher) oder Excel Online verwenden, empfehlen wir die Verwendung des [Excel-Add-Ins](excel-add-in-for-web-services.md).



## <a name="steps"></a>Schritte
Veröffentlichen eines Webdiensts. Auf [dieser Seite](walkthrough-5-publish-web-service.md) wird dies erläutert. Die Excel-Arbeitsmappenfunktion wird derzeit nur für Antwort-/Anfrage-Dienste unterstützt, die eine einzelne Ausgabe aufweisen (d. h. eine einzelne Bewertungsbezeichnung). 

Wenn Sie einen Webdienst haben, klicken Sie auf den Bereich **WEB SERVICES** der linken Seite in Studio und wählen Sie den aus Excel zu verwendenden Webdienst aus.

**Klassischer Webdienst**

1. Auf der Registerkarte **DASHBOARD** für den Webdienst befindet sich die Zeile **REQUEST/RESPONSE** für den Antwort-/Anfrage-Dienst. Wenn dieser Dienst eine einzelne Ausgabe hat, sollte sich in dieser Zeile der Link **Download Excel Workbook** befinden.
   
    ![][1]
2. Klicken Sie auf **Download Excel Workbook**.

**Neuer Webdienst**

1. Wählen Sie im Azure Machine Learning Web Service-Portal **Consume**aus.
2. Klicken Sie auf der Seite „Consume“ im Abschnitt **Web service consumption options** auf das Excel-Symbol.

**Verwenden der Arbeitsmappe**

1. Öffnen Sie die Arbeitsmappe.
2. Es wird eine Sicherheitswarnung angezeigt. Klicken Sie auf die Schaltfläche **Bearbeitung aktivieren**.
   
    ![][2]
3. Es wird eine Sicherheitswarnung angezeigt. Klicken Sie auf die Schaltfläche **Inhalt aktivieren** zum Ausführen von Makros im Arbeitsblatt.
   
    ![][3]
4. Sobald Makros aktiviert sind, wird eine Tabelle generiert. Spalten in Blau sind als Eingabe für den RRS-Webdienst oder als **PARAMETER**erforderlich. Beachten Sie die Ausgaben des RRS-Diensts **PREDICTED VALUES** in Grün. Wenn alle Spalten für eine bestimmte Zeile gefüllt wurden, ruft die Arbeitsmappe automatisch die Bewertungs-API auf und zeigt die bewerteten Ergebnisse an.
   
    ![][4]
5. Um mehr als eine Zeile zu bewerten, geben Sie in der zweiten Zeile Daten ein. Daraufhin werden die Vorhersagewerte erzeugt. Sie können auch gleichzeitig mehrere Zeilen einfügen.

Sie können beliebige Excel-Funktionen (Diagramme, Power Map, bedingte Formatierungen usw.) mit den Vorhersagewerten verwenden, um die Daten zu visualisieren.    

## <a name="sharing-your-workbook"></a>Freigeben Ihrer Arbeitsmappe
Damit die Makros funktionieren, muss der API-Schlüssel Teil des Arbeitsblatts sein. Das bedeutet, dass Sie die Arbeitsmappe nur für Entitäten und Personen freigeben sollten, denen Sie vertrauen.

## <a name="automatic-updates"></a>Automatische Aktualisierungen
RRS-Aufrufe werden in diesen beiden Situationen ausgeführt:

1. Beim ersten Mal, wenn in einer Zeile in jedem **PARAMETER**
2. Jedes Mal, wenn einer der **PARAMETER** in einer Zeile, in der alle **PARAMETER** vorhanden sind, geändert wird.

[1]: ./media/consuming-from-excel/excellink.png
[2]: ./media/consuming-from-excel/enableeditting.png
[3]: ./media/consuming-from-excel/enablecontent.png
[4]: ./media/consuming-from-excel/sampletable.png
