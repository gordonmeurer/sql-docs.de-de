---
title: Erstellen den Server Connection Files (AccessToSQL) | Microsoft-Dokumentation
ms.prod: sql
ms.custom: ''
ms.date: 08/17/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 829153be-aa8e-4162-87e8-69882feecf19
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: c3c31e4c815ac3c52f029ec474e53488b8202c8e
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/15/2018
ms.locfileid: "51664296"
---
# <a name="creating-the-server-connection-files-accesstosql"></a>Erstellen des Servers Connection-Dateien (AccessToSQL)
Informationen zum Server möglich. entweder in den Bereich "Server", der Skriptdatei angegeben. Informationen zum Server kann auch in einer separaten Server Connection-Datei angegeben werden. Die Befehlszeilenparameter für die Server-Verbindungsdatei ist `-c <serverconnectionfile>`. Wenn die gleiche Id in das Skript und die Server-Connection-Dateien vorhanden ist, wird die Definition des Servers in der Skriptdatei als betrachtet.  
  
```xml  
<!--Sample of server connection file commands -->  
<!--Connection to SQL Server-->  
  
<sql-server name="target_3">  
  
  <sql-server-authentication>  
  
    <server value="$TargetServerName$"/>  
  
    <database value="$TargetDB$"/>  
  
    <user-id value="$TargetUserName$"/>  
  
    <password value="$TargetPassword$"/>  
  
    <encrypt value="true"/>  
  
    <trust-server-certificate value="true"/>  
  
  </sql-server-authentication>  
  
</sql-server>  
```  
  
```xml  
<!--Connection to SQL Azure-->  
  
<sql-azure name="target_azure">  
  
  <server value="$TargetAzureServerName$"/>  
  
  <database value="$TargetAzureDB$"/>  
  
  <user-id value="$TargetAzureUserName$"/>  
  
  <password value="$TargetAzurePassword$"/>  
  
</sql-azure>  
```  
  
## <a name="server-connection-file-validation"></a>Datei-Überprüfung von Server-Verbindung  
Benutzer kann ganz einfach überprüfen, seine Verbindung-Serverdatei anhand der Schemadefinitionsdatei **"A2SSConsoleScriptServersSchema.xsd"** in den Ordner "Schemas" verfügbar.  
  
## <a name="next-step"></a>Nächster Schritt  
Der nächste Schritt in der Konsole ausgeführt wird [Executing the SSMA Console ausführen &#40;AccessToSQL&#41;](../../ssma/access/executing-the-ssma-console-accesstosql.md)  
  
## <a name="see-also"></a>Siehe auch  
[Ausführen der SSMA-Konsole (Datenzugriff)](https://msdn.microsoft.com/aa1bf665-8dc0-4259-b36f-46ae67197a43)  
  
