---
title: Grundlegendes zum WMI-Anbieter für Serverereignisse | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- architecture [WMI]
- SQL Server Agent [WMI]
- WMI Provider for Server Events, about WMI Provider for Server Events
ms.assetid: 8fd7bd18-76d0-4b28-8fee-8ad861441ab2
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 6f761e07822c0db14e47e6709d704a4555dd6221
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/02/2018
ms.locfileid: "48132480"
---
# <a name="understanding-the-wmi-provider-for-server-events"></a>Grundlegendes zum WMI-Anbieter für Serverereignisse
  Über den WMI-Anbieter für Serverereignisse können Sie Ereignisse in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]mithilfe von WMI (Windows Management Instrumentation) überwachen. Der Anbieter funktioniert durch das Aktivieren der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] in ein verwaltetes WMI-Objekt. Jedes Ereignis, das eine ereignisbenachrichtigung in generieren kann [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mithilfe dieses Anbieters von WMI genutzt werden kann. Darüber hinaus kann der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agent als eine mit WMI interagierende Verwaltungsanwendung auf diese Ereignisse reagieren. Dadurch wird der durch den [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Agent abgedeckte Ereignisbereich im Gegensatz zu früheren Versionen erweitert.  
  
 Verwaltungsanwendungen wie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Agent zugreifen kann [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Ereignisse, die mit dem WMI-Anbieter für Serverereignisse von Windows-Verwaltungsinstrumentation (WMI Query Language, WQL)-Anweisungen ausgeben. WQL ist eine vereinfachte Teilmenge von Structured Query Language (SQL) mit einigen WMI-spezifischen Erweiterungen. Bei Verwendung von WQL ruft eine Anwendung einen Ereignistyp für eine bestimmte Datenbank oder ein bestimmtes Datenbankobjekt ab. Der WMI-Anbieter für Serverereignisse übersetzt die Abfrage in eine Ereignisbenachrichtigung und erstellt dadurch auf effektive Weise eine Ereignisbenachrichtigung in der Zieldatenbank. Weitere Informationen zur Funktionsweise von ereignisbenachrichtigungen in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], finden Sie unter [WMI-Anbieter für Ereignisse Serverkonzepte](http://technet.microsoft.com/library/ms180560.aspx). Die Ereignisse, die abgefragt werden können, finden Sie in [WMI-Anbieter für Server Ereignisklassen und Eigenschaften](../../relational-databases/wmi-provider-server-events/wmi-provider-for-server-events-classes-and-properties.md).  
  
 Wenn ein Ereignis auftritt, das die Ereignisbenachrichtigungsfunktion zum Senden einer Meldung veranlasst, wird die Benachrichtigung an einen vordefinierten Zieldienst in **msdb** mit dem Namen **SQL/Notifications/ProcessWMIEventProviderNotification/v1.0**übermittelt. Der Zieldienst fügt das Ereignis in eine vordefinierte Warteschlange in **msdb** ein. Ihr Name ist **WMIEventProviderNotificationQueue**. (Sowohl der Dienst als auch die Warteschlange werden vom Anbieter beim Herstellen der ersten Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dynamisch erstellt.) Der Anbieter liest die Ereignisdaten aus dieser Warteschlange, wandelt sie in MOF-Daten (Managed Object Format) um und gibt sie dann an die Anwendung zurück. Die folgende Abbildung veranschaulicht diesen Prozess:  
  
 ![Flussdiagramm des WMI-Anbieters für Serverereignisse](../../../2014/database-engine/dev-guide/media/wmi-provider-functional-spec.gif "Flussdiagramm des WMI-Anbieters für Serverereignisse")  
  
 Betrachten Sie beispielsweise folgende WQL-Abfrage:  
  
```  
SELECT * FROM DDL_DATABASE_LEVEL_EVENTS  
WHERE DatabaseName = 'AdventureWorks'  
```  
  
 Als Reaktion auf diese Abfrage erstellt der WMI-Anbieter für Serverereignisse die entsprechende Ereignisbenachrichtigung in der Zieldatenbank:  
  
```  
USE AdventureWorks ;  
GO  
CREATE EVENT NOTIFICATION SQLWEP_76CF38C1_18BB_42DD_A7DC_C8820155B0E9  
    ON DATABASE  
    WITH FAN_IN  
    FOR DDL_DATABASE_LEVEL_EVENTS  
    TO SERVICE  
        'SQL/Notifications/ProcessWMIEventProviderNotification/v1.0',   
        'A7E5521A-1CA6-4741-865D-826F804E5135';  
GO  
```  
  
 In diesem Beispiel ist `SQLWEP_76CF38C1_18BB_42DD_A7DC_C8820155B0E9` ein [!INCLUDE[tsql](../../includes/tsql-md.md)]-Bezeichner, der aus dem Präfix `SQLWEP_` und einer GUID besteht. `SQLWEP` erstellt eine neue GUID für jeden Bezeichner. Der Wert `A7E5521A-1CA6-4741-865D-826F804E5135` in der `TO SERVICE` -Klausel ist der GUID, der die Broker-Instanz in der **msdb** -Datenbank identifiziert.  
  
 Weitere Informationen zur Arbeit mit WQL finden Sie unter [Verwenden von WQL mit dem WMI-Anbieter für Serverereignisse](http://technet.microsoft.com/library/ms180524\(v=sql.105\).aspx).  
  
 Verwaltungsanwendungen verweisen den WMI-Anbieter für Serverereignisse an eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] durch das Verbinden mit einem WMI-Namespace, die vom Anbieter definiert ist. Der WMI-Dienst ordnet der Anbieter-DLL Sqlwep.dll diesen Namespace zu und lädt sie in den Arbeitsspeicher. Der Anbieter verwaltet einen WMI-Namespace für Serverereignisse für jede Instanz der [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], und das Format ist: \\ \\.\\ *Stamm*\Microsoft\SqlServer\ServerEvents\\*Instance_name*, wobei *Instance_name* lautet standardmäßig MSSQLSERVER. Weitere Informationen zum Herstellen einer Verbindung mit einem WMI-Namespace für eine Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], finden Sie unter [Verwenden von WQL mit dem WMI-Anbieter für Serverereignisse](http://technet.microsoft.com/library/ms180524\(v=sql.105\).aspx).  
  
 Die Anbieter-DLL Sqlwep.dll geladen wird nur ein Mal in der WMI-Hostdienst des Betriebssystems des Servers an, unabhängig davon, wie viele Instanzen des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sind auf dem Server.  
  
 Ein Beispiel für eine [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent-verwaltungsanwendung, die den WMI-Anbieter für Serverereignisse verwendet, finden Sie unter [Beispiel: Erstellen einer SQL Server-Agent Warnungen mithilfe der WMI-Anbieter für Serverereignisse](http://technet.microsoft.com/library/ms186385.aspx). Ein Beispiel für eine Verwaltungsanwendung, die den WMI-Anbieter für Serverereignisse in verwaltetem Code verwendet, finden Sie unter [Beispiel: Verwenden des WMI-Ereignisanbieters in verwaltetem Code](http://technet.microsoft.com/library/ms179315.aspx). Weitere Informationen finden Sie auch zu WMI in der [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] SDK.  
  
## <a name="see-also"></a>Siehe auch  
 [Konzepte des WMI-Anbieters für Serverereignisse](http://technet.microsoft.com/library/ms180560.aspx)  
  
  
