---
title: Serverseitige XML-Formatierung (SQLXML 4.0) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
helpviewer_keywords:
- FOR XML clause, formatting
- server-side XML formatting
ms.assetid: ae9ea068-0857-4505-a3b2-f53d256b644c
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 2d9e23528a7732d3974902c24ca777fc2d19dae9
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/02/2018
ms.locfileid: "48222205"
---
# <a name="server-side-xml-formatting-sqlxml-40"></a>Serverseitige XML-Formatierung (SQLXML 4.0)
  Dieses Thema enthält Informationen über das serverseitige Formatieren von XML-Dokumenten aus den Rowsets, die von Abfragen generiert werden, die in einer Datenbank in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] ausgeführt werden.  
  
 In [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] können Sie XML-Dokumente in Datenbanktabellen speichern und aus Datenbanktabellen abrufen. Um ein XML-Dokument abzurufen, verwenden Sie die FOR XML-Abfrageerweiterung in einer SELECT-Abfrage.  
  
 Nehmen wir beispielsweise an eine Clientanwendung führt einen Befehl für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] besteht aus folgenden [!INCLUDE[tsql](../../../includes/tsql-md.md)] Abfrage:  
  
```  
SELECT FirstName, LastName  
FROM   Person.Contact  
FOR XML AUTO  
```  
  
 Der Server führt die Abfrage in zwei Schritten aus. Zuerst führt der Server diese SELECT-Anweisung aus:  
  
```  
SELECT FirstName, LastName  
FROM   Person.Contact  
```  
  
 Dann wendet der Server die FOR XML-Transformation auf das generierte Rowset an. Der resultierende XML-Code wird dann an den Client als ein einspaltiges Rowset gesendet. In dieser Dokumentation wird dieser Prozess als serverseitige XML-Formatierung bezeichnet.  
  
 Auf der Serverseite können Sie die folgenden Modi mit einer FOR XML-Klausel angeben:  
  
-   RAW  
  
-   AUTO  
  
-   EXPLICIT  
  
 Weitere Informationen zur FOR XML-Klausel finden Sie unter [Erstellen von XML mit FOR XML](../../xml/for-xml-sql-server.md).  
  
## <a name="see-also"></a>Siehe auch  
 [Architektur der Client- und serverseitigen XML-Formatierung &#40;SQLXML 4.0&#41;](architecture-of-client-side-and-server-side-xml-formatting-sqlxml-4-0.md)   
 [Die clientseitige XML-Formatierung &#40;SQLXML 4.0&#41;](client-side-xml-formatting-sqlxml-4-0.md)   
 [FOR XML &#40;SQL Server&#41;](../../xml/for-xml-sql-server.md)  
  
  
