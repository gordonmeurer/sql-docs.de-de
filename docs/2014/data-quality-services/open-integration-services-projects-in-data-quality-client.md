---
title: Öffnen von Integration Services-Projekten im Data Quality-Client | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: a8bad2f1-8fb0-4d14-a978-11a5720e62d6
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: dc1899dd230908c8dae87dc5004355c8f56c7d0d
ms.sourcegitcommit: af1d9fc4a50baf3df60488b4c630ce68f7e75ed1
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2018
ms.locfileid: "51031308"
---
# <a name="open-integration-services-projects-in-data-quality-client"></a>Öffnen von Integration Services-Projekten im Data Quality-Client
  [!INCLUDE[ssDQSCleansingLong](../includes/ssdqscleansinglong-md.md)] ermöglicht es Ihnen, im Batchmodus ein Bereinigungsprojekt auszuführen. Manchmal möchten Sie allerdings die Bereinigungsergebnisse vielleicht in einem Integration Services-Paket überprüfen, wie Sie auch die Bereinigungsergebnisse auf der Registerkarte **Ergebnisse verwalten und anzeigen** einer Bereinigungsaktivität in einem Data Quality-Projekt in DQS überprüfen können. DQS ermöglicht es Ihnen, Integration Services-Projekte nur in [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] wie ein beliebiges anderes Data Quality-Projekt im Bildschirm **Projekt öffnen** zu öffnen und eine interaktive Bereinigung der Bereinigungsergebnisse in einem Integration Services-Projekt durchzuführen.  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungen  
  
###  <a name="LimitationsRestrictions"></a> Einschränkungen  
  
-   Nur abgeschlossene Integration Services-Projekte sind im Bildschirm **Projekt öffnen** in [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]verfügbar. Fehlgeschlagene und aktuell ausgeführte Projekte sind im Bildschirm **Projekt öffnen** nicht verfügbar.  
  
-   Integration Services-Projekte werden in der interaktiven Bereinigungsphase in (Registerkarte**Ergebnisse verwalten und anzeigen** ) in [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]geöffnet. Sie können nicht auf die Registerkarte **Bereinigen** oder **Struktur** wechseln. Sie können nur zur Registerkarte **Exportieren** wechseln, indem Sie auf **Weiter**klicken.  
  
-   Sie können ein gesperrtes Integration Services-Projekt nicht aus [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]löschen. Zum Löschen müssen Sie es zunächst entsperren.  
  
###  <a name="Prerequisites"></a> Erforderliche Komponenten  
 Sie müssen das Ausführen eines Integration Services-Projekts, das ein Paket mit einer DQS-Bereinigungskomponente enthält, erfolgreich abgeschlossen haben, um es in [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]anzuzeigen und zu öffnen.  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Sie müssen die Rolle „dqs_kb_editor“ oder „dqs_kb_operator“ in der Datenbank DQS_MAIN haben, um ein Integration Services-Projekt zu öffnen.  
  
 ![Pfeilsymbol mit Rückverweis auf den obersten](../2014-toc/media/uparrow16x16.gif "Pfeilsymbol mit Rückverweis auf den obersten") [In diesem Thema](#Intro)  
  
##  <a name="Open"></a> Öffnen eines Integration Services-Projekts  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Ausführen der Data Quality-Clientanwendung](../../2014/data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Klicken Sie im [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] -Startbildschirm auf **Data Quality-Projekt öffnen**. Der Bildschirm **Projekt öffnen** wird angezeigt.  
  
3.  Im Bildschirm **Projekt öffnen** können Sie ein Integration Services-Projekt auf eine der folgenden Weisen identifizieren:  
  
    1.  **Projektname**: Die Auflistung von Integration Services-Projekten erfolgt anhand der folgenden Namensterminologie: „Package.DQS Cleansing_*\<DATUM>**\<ZEIT>*_{GUID}“. Bei jeder erfolgreichen Ausführung des gleichen Pakets in [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]wird ein neues Projekt auf dem Bildschirm **Projekt öffnen** aufgelistet.  
  
    2.  **Projekttyp**: Integration Services-Projekte haben **SSIS** als Projekttyp im Bildschirm **Projekt öffnen** .  
  
     Wählen Sie ein Projekt aus, und klicken Sie auf **Weiter**.  
  
4.  Das Integration Services-Projekt wird in der interaktiven Bereinigungsphase (Registerkarte**Ergebnisse verwalten und anzeigen** ) geöffnet. Sie können eine interaktive Bereinigung für die Daten im Integration Services-Projekt ausführen. Ausführliche Informationen zur Registerkarte **Ergebnisse verwalten und anzeigen** finden Sie unter [Interaktive Bereinigungsphase](../../2014/data-quality-services/cleanse-data-using-dqs-internal-knowledge.md#Interactive) in [Bereinigen von Daten mit &#40;internem&#41; DQS-Wissen](../../2014/data-quality-services/cleanse-data-using-dqs-internal-knowledge.md).  
  
5.  Klicken Sie auf **Weiter** , um zur Registerkarte **Exportieren** zu wechseln, wo Sie die verarbeiteten Daten in eine neue Tabelle in der SQL Server-Datenbank, eine CSV-Datei oder eine Excel-Datei exportieren können. Ausführliche Informationen zur Registerkarte **Exportieren** finden Sie unter [Exportphase](../../2014/data-quality-services/cleanse-data-using-dqs-internal-knowledge.md#Export) in [Bereinigen von Daten mit &#40;internem&#41; DQS-Wissen](../../2014/data-quality-services/cleanse-data-using-dqs-internal-knowledge.md).  
  
6.  Klicken Sie nach dem Exportieren der Daten auf **Fertig stellen** , um das Integration Services-Projekt zu schließen.  
  
 ![Pfeilsymbol mit Rückverweis auf den obersten](../2014-toc/media/uparrow16x16.gif "Pfeilsymbol mit Rückverweis auf den obersten") [In diesem Thema](#Intro)  
  
## <a name="see-also"></a>Siehe auch  
 [DQS-Bereinigungstransformation](../integration-services/data-flow/transformations/dqs-cleansing-transformation.md)   
 [Integration Services-Projekte &#40;SSIS&#41;](../integration-services/integration-services-ssis-projects-and-solutions.md)  
  
  
