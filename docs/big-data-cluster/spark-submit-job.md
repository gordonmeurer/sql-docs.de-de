---
title: Übermitteln von Spark-Auftrag in SQL Server-big Data-Clustern in Azure Data Studio
description: Übermitteln von Spark-Auftrag in SQL Server-big Data-Clustern in Azure Data Studio
services: SQL Server 2019 big data cluster spark
ms.service: SQL Server 2019 big data cluster spark
author: jejiang
ms.author: jejiang
ms.reviewer: jroth
ms.custom: ''
ms.topic: conceptual
ms.date: 11/06/2018
ms.openlocfilehash: 4ff29460ade2a3e32f3650d2c2701f22548bdb60
ms.sourcegitcommit: cb73d60db8df15bf929ca17c1576cf1c4dca1780
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/07/2018
ms.locfileid: "51221606"
---
# <a name="submit-spark-job-on-sql-server-big-data-clusters-in-azure-data-studio"></a>Übermitteln von Spark-Auftrag in SQL Server-big Data-Clustern in Azure Data Studio

Einer der wichtigsten Szenarios ist die Möglichkeit zum Übermitteln von Spark-Auftrags für SQL Server 2019 CTP-Version 2.1. Die Spark Job Submission-Funktion können Sie eine lokale JAR- oder Py-Dateien mit Verweisen auf SQL Server-2019 big Data-Cluster zu übermitteln. Darüber hinaus können Sie zum Ausführen von einer JAR-Datei oder Py-Dateien, die sich bereits in das HDFS-Dateisystem befinden. 

## <a name="prerequisite"></a>Voraussetzung 
Installieren von big Data-Tools für SQL Server und eine Verbindung mit einem big Data-Cluster herstellen, bevor Sie die Spark-Auftrag übermitteln können. Für ausführliche Informationen zur Installation finden Sie in den link [Bereitstellen von big Data-Tools](deploy-big-data-tools.md).

## <a name="open-spark-job-submission-dialog"></a>Öffnen des Dialogfelds "Senden" der Spark-Auftrag
Es gibt mehrere Methoden zum Öffnen des Dialogfelds "Senden" der Spark-Auftrag. Die Methoden enthalten Dashboards, wählen Sie im Objekt-Explorer, und die Palette der Befehl im Kontextmenü.

+ Klicken Sie auf **neue Spark-Auftrag** im Dashboard, um das Dialogfeld "Spark Job Submission" zu öffnen.

    ![Übermitteln Sie im Menü durch Klicken auf dashboard ](./media/submit-spark-job/new-spark-job.png)
 
+ Mit der rechten Maustaste auf den Cluster im Objekt-Explorer, und wählen Sie **Submit Spark Job** aus dem Kontextmenü. Spark-Auftrag-Dialogfelds "Senden" wird geöffnet.  
 
    ![Menü mit der rechten Maustaste-Cluster übermitteln](./media/submit-spark-job/submit-spark-job.png)

+ Mit der rechten Maustaste auf eine JAR-Datei/Py-Datei im Objekt-Explorer, und wählen Sie **Submit Spark Job** aus dem Kontextmenü. Spark Job Submission Dialog durch die JAR-Datei/Py-Feld, das ausgefüllt wird geöffnet. 
 
    ![Übermitteln Sie im Menü mit der rechten Maustaste-Datei](./media/submit-spark-job/submit-spark-job-2.png)

+ Verwenden Sie Befehl **Submit Spark Job** über die befehlspalette, indem Sie STRG + UMSCHALT + P (in Windows) und Cmd + UMSCHALT + P (in Mac) eingeben.

    ![Übermitteln Sie die befehlspalette den Befehl im Menü in windows](./media/submit-spark-job/submit-spark-job-3.png)

    ![Übermitteln Sie die befehlspalette den Befehl im Menü unter mac](./media/submit-spark-job/submit-spark-job-4.png)
  
 
## <a name="submit-spark-job"></a>Übermitteln von Spark-Auftrag 
Das Dialogfeld "Spark Job Submission" wird wie folgt angezeigt. Geben Sie ein Auftragsname, Pfad der JAR-Datei/Py-Datei, main-Klasse und anderen Feldern. Die JAR-Datei / der Quelle der Py-Datei ist möglicherweise aus lokalen oder aus einem HDFS. Wenn die Spark-Auftrags JAR-Dateien, Py-Dateien oder zusätzliche Dateien verweisen, klicken Sie auf **erweitert** Registerkarte, und geben Sie die entsprechenden Dateipfade. Klicken Sie auf **senden** zum Übermitteln von Spark-Auftrag.
 
![Dialogfeld "neue Spark-Auftrag"](./media/submit-spark-job/submit-spark-job-section.png)

![Dialogfeld "Erweitert"](./media/submit-spark-job/submit-spark-job-section-1.png)

## <a name="monitor-spark-job-submission"></a>Überwachen von Spark-Auftragsübermittlung
Nachdem der Spark-Auftrag übermittelt wurde, werden Statusinformationen für den Spark-Auftrag Übermittlung und die Ausführung im Task-Verlauf auf der linken Seite angezeigt. Und Informationen zu den Fortschritt und die Protokolle werden ebenfalls angezeigt, der **Ausgabe** Fenster am unteren Rand.
+ Bei der Spark-Auftrag ausgeführt wird, wird die **Taskverlauf** Bereich und **Ausgabe** Fenster werden mit dem Status aktualisiert.

![Überwachen von Spark-Auftrags in Bearbeitung](./media/submit-spark-job/monitor-spark-job-submission.png)

+ Wenn Spark-Auftrag wird erfolgreich abgeschlossen ist, sehen Sie Links von Spark-Benutzeroberfläche und die Yarn-Benutzeroberfläche in der **Ausgabe** Fenster. Sie können die Links, um weitere Informationen klicken.

![Spark-Auftrag-Link in der Ausgabe](./media/submit-spark-job/monitor-spark-job-submission-2.png)

## <a name="next-steps"></a>Nächste Schritte
Weitere Informationen zu SQL Server-big Data-Cluster und die zugehörigen Szenarien, finden Sie unter [neuerungen von SQL Server-big Data-Cluster](big-data-cluster-overview.md)?

