---
title: Ausführen des SQL-Skripts in Adressbuch | Microsoft-Dokumentation
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- address book application scenario [ADO]
- RDS scenarios [ADO]
ms.assetid: 409b3f8b-0ced-4867-acbe-b245dcdf6702
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 6c77bece1b2ab67cc361f7445240e1a2b1190587
ms.sourcegitcommit: 1a5448747ccb2e13e8f3d9f04012ba5ae04bb0a3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/12/2018
ms.locfileid: "51557797"
---
# <a name="running-the-address-book-sql-script"></a>Ausführen des Adress Book-SQL-Skripts
> [!IMPORTANT]
>  Ab Windows 8 und Windows Server 2012, sind nicht mehr RDS-Server-Komponenten in das Windows-Betriebssystem enthalten (finden Sie unter Windows 8 und [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) Einzelheiten). RDS-Client-Komponenten werden in einer zukünftigen Version von Windows entfernt werden. Nutzen Sie diese Funktionen bei Neuentwicklungen nicht mehr, und planen Sie die Änderung von Anwendungen, die diese Funktion zurzeit verwenden. Anwendungen, die RDS zu migrieren sollten [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
 Verwenden Sie entweder das ISQL/Query Analyzer-Befehlszeilen-Hilfsprogramm oder SQL Server Enterprise Manager auf dem enthaltene SQL-Skript (Sampleemp.sql) ausführen, die:  
  
-   Erstellt eine neue Datenbank AddrBookDB, auf dem Standardgerät an.  
  
-   Eine Verbindung mit der Datenbank AddrBookDB.  
  
-   Erstellt eine Employee-Tabelle.  
  
-   Füllt die Tabelle mit Beispieldaten.  
  
-   Führt eine einfache SELECT-Anweisung, um zu überprüfen, ob die Auffüllung der Datenbanktabelle an.  
  
-   Richtet ein Benutzerkonto namens "Adcdemo" mit dem Kennwort "Adcdemo."  
  
#### <a name="to-run-the-sampleempsql-script-in-microsoft-sql-server-65"></a>Zum Ausführen des Sampleemp.sql-Skripts in Microsoft SQL Server 6.5  
  
1.  Klicken Sie auf **starten**, zeigen Sie auf **Programme**, und zeigen Sie dann auf **Microsoft SQL Server 6.5**. Klicken Sie auf **SQL Enterprise Manager**.  
  
2.  Von der **Tools** Menü klicken Sie auf **SQL-Abfragetool**.  
  
3.  Klicken Sie auf **SQL-Skript laden** und navigieren Sie zu c:\Platform SDK\Samples\DataAccess\RDS\AddressBook.  
  
4.  Wählen Sie die Datei Sampleemp.sql. Klicken Sie auf **Öffnen**.  
  
5.  Klicken Sie auf die **Abfrage ausführen** Schaltfläche (der grüne Pfeil auf der Symbolleiste).  
  
6.  Nachdem sie ausgeführt wird, schließen die **Abfrage** und **Enterprise Manager** Windows.  
  
#### <a name="to-run-the-sampleempsql-script-in-microsoft-sql-server-70"></a>Zum Ausführen des Sampleemp.sql-Skripts in Microsoft SQL Server 7.0  
  
1.  Klicken Sie auf **starten**, zeigen Sie auf **Programme**, und zeigen Sie dann auf **Microsoft SQL Server 7.0**. Klicken Sie auf **Enterprise Manager**.  
  
2.  Achten Sie darauf, dass die SQL-Server, die Sie verwenden möchten, aus der Liste der registrierten Server in Enterprise Manager ausgewählt ist.  
  
3.  Von der **Tools** Menü klicken Sie auf **SQL Server Query Analyzer**.  
  
4.  Klicken Sie auf die **SQL-Skript laden** Schaltfläche (im geöffneten Ordner auf der Symbolleiste), und navigieren Sie zu c:\Platform SDK\Samples\DataAccess\RDS\AddressBook.  
  
5.  Wählen Sie die Datei Sampleemp.sql. Klicken Sie auf **Öffnen**.  
  
6.  Klicken Sie auf die **Abfrage ausführen** Schaltfläche (der grüne Pfeil auf der Symbolleiste) oder **F5**.  
  
7.  Nachdem sie ausgeführt wird, schließen die **Abfrage**, **Query Analyzer**, und **Enterprise Manager** Windows.  
  
## <a name="see-also"></a>Siehe auch  
 [Ausführen der Adress Book-Beispielanwendung](../../../ado/guide/remote-data-service/running-the-address-book-sample-application.md)


