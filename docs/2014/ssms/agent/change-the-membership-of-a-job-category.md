---
title: Ändern der Mitgliedschaft einer Auftragskategorie | Microsoft-Dokumentation
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL Server Agent jobs, categories
- jobs [SQL Server Agent], categories
- categories [SQL Server Agent jobs]
- members [SQL Server], job categories
ms.assetid: 6a18f7f0-eb50-485f-a9c7-df31ae0f994e
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f956a6f87142a9b9bae2d8398d69e3fd3ae08c9c
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/02/2018
ms.locfileid: "48106170"
---
# <a name="change-the-membership-of-a-job-category"></a>Change the Membership of a Job Category
  In diesem Thema wird beschrieben, wie Sie die Mitgliedschaft der Auftragskategorie in [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] mithilfe von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], [!INCLUDE[tsql](../../includes/tsql-md.md)]oder SQL Server Management Objects ändern können.  
  
 Auftragskategorien helfen Ihnen dabei, Ihre Aufträge zum einfachen Filtern und Gruppieren zu organisieren. Sie können eigene Auftragskategorien erstellen. Zudem können Sie die Mitgliedschaft von Microsoft SQL Server-Agent-Aufträgen in Auftragskategorien ändern.  
  
 **In diesem Thema**  
  
-   **Vorbereitungen:**  
  
     [Security](#Security)  
  
-   **So ändern Sie die Mitgliedschaft einer Auftragskategorie mit**  
  
     [SQL Server Management Studio](#SSMS)  
  
     [Transact-SQL](#TSQL)  
  
     [SQL Server Management Objects](#SMO)  
  
##  <a name="BeforeYouBegin"></a> Vorbereitungsmaßnahmen  
  
###  <a name="Security"></a> Sicherheit  
 Ausführliche Informationen finden Sie unter [Implement SQL Server Agent Security](implement-sql-server-agent-security.md).  
  
##  <a name="SSMS"></a> Verwenden von SQL Server Management Studio  
  
#### <a name="to-change-the-membership-of-a-job-category"></a>So ändern Sie die Mitgliedschaft einer Auftragskategorie  
  
1.  Klicken Sie im **Objekt-Explorer** auf das Pluszeichen, um den Server zu erweitern, auf dem Sie eine Auftragskategorie bearbeiten möchten.  
  
2.  Klicken Sie auf das Pluszeichen, um **SQL Server-Agent**zu erweitern.  
  
3.  Klicken Sie mit der rechten Maustaste auf den Ordner **Aufträge** , und wählen Sie **Auftragskategorien verwalten**aus.  
  
4.  Wählen Sie im Dialogfeld **Auftragskategorien verwalten***Servername* die Auftragskategorie aus, die Sie bearbeiten möchten, und klicken Sie dann auf **Aufträge anzeigen**.  
  
5.  Aktivieren Sie das Kontrollkästchen **Alle Aufträge anzeigen** .  
  
6.  Um der Kategorie einen Auftrag hinzuzufügen, aktivieren Sie im Hauptraster in der **Select** -Spalte das Kontrollkästchen, das dem Auftrag entspricht. Um einen Auftrag aus der Kategorie zu entfernen, deaktivieren Sie das Kontrollkästchen. Wenn Sie fertig sind, klicken Sie auf **OK**.  
  
7.  Schließen Sie das Dialogfeld **Auftragskategorien verwalten***Servername*.  
  
##  <a name="TSQL"></a> Verwenden von Transact-SQL  
  
#### <a name="to-change-the-membership-of-a-job-category"></a>So ändern Sie die Mitgliedschaft einer Auftragskategorie  
  
1.  Stellen Sie im **Objekt-Explorer**eine Verbindung mit einer [!INCLUDE[ssDE](../../includes/ssde-md.md)]-Instanz her.  
  
2.  Klicken Sie in der Standardleiste auf **Neue Abfrage**.  
  
3.  Kopieren Sie das folgende Beispiel, fügen Sie es in das Abfragefenster ein, und klicken Sie auf **Ausführen**.  
  
    ```  
    -- adding a new job category to the "NightlyBackups" job  
    USE msdb ;  
    GO  
    EXEC dbo.sp_update_job  
        @job_name = N'NightlyBackups',  
        @category_name = N'[Uncategorized (Local)]';  
    GO  
    ```  
  
 Weitere Informationen finden Sie unter [Sp_update_job &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-update-job-transact-sql).  
  
##  <a name="SMO"></a> Verwendung von SQL Server Management Objects  
 **So ändern Sie die Mitgliedschaft einer Auftragskategorie**  
  
 Verwenden der `JobCategory` Klasse, indem Sie eine Programmiersprache, die Sie, wie z. B. Visual Basic, Visual c# oder PowerShell auswählen.  
  
  
