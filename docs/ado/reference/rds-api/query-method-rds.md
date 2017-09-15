---
title: Query-Methode (RDS) | Microsoft Docs
ms.prod: sql-non-specified
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: 
ms.tgt_pltfrm: 
ms.topic: article
apitype: COM
helpviewer_keywords:
- Query method [ADO]
ms.assetid: 20f2480f-3758-405d-a379-05a0dce74796
caps.latest.revision: 16
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 53647d80b2e6110e5af084e6a3f983381ced1690
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="query-method-rds"></a>Query-Methode (RDS)
Eine gültige SQL-Abfragezeichenfolge zurückzugebenden verwendet eine [Recordset](../../../ado/reference/ado-api/recordset-object-ado.md).  
  
> [!IMPORTANT]
>  Ab Windows 8 und Windows Server 2012, sind nicht mehr RDS-Server-Komponenten in Windows-Betriebssystems enthalten (finden Sie unter Windows 8 und [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/en-us/download/details.aspx?id=27416) detailliertere). RDS-Clientkomponenten werden in einer zukünftigen Version von Windows entfernt werden. Verwenden Sie diese Funktion beim Entwickeln neuer Anwendungen nicht, und planen Sie das Ändern von Anwendungen, in denen es zurzeit verwendet wird. Anwendungen, die RDS verwenden sollten migrieren [WCF Data Service](http://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Syntax  
  
```  
  
Set Recordset = DataFactory.Query(Connection, Query)  
```  
  
#### <a name="parameters"></a>Parameter  
 *Recordset*  
 Objektvariable stellt eine **Recordset** Objekt.  
  
 *DataFactory*  
 Objektvariable stellt eine [RDSServer.DataFactory](../../../ado/reference/rds-api/datafactory-object-rdsserver.md) Objekt.  
  
 *Verbindung*  
 Ein **Zeichenfolge** Wert, der die Server-Verbindungsinformationen enthält. Dies ist vergleichbar mit der [verbinden](../../../ado/reference/rds-api/connect-property-rds.md) Eigenschaft.  
  
 *Abfrage*  
 Ein **Zeichenfolge** , die die SQL-Abfrage enthält.  
  
## <a name="remarks"></a>Hinweise  
 Die Abfrage sollte den SQL-Dialekt, der den Datenbankserver verwenden. Ein Ergebnisstatus wird zurückgegeben, wenn ein Fehler mit der Abfrage, die ausgeführt wurde. Die **Abfrage** Methode führt syntaxüberprüfung auf keine der **Abfrage** Zeichenfolge.  
  
## <a name="applies-to"></a>Gilt für  
 [DataFactory-Objekt (RDSServer)](../../../ado/reference/rds-api/datafactory-object-rdsserver.md)  
  
## <a name="see-also"></a>Siehe auch  
 [DataFactory-Objekt, Abfragemethode und CreateObject-Methode (Beispiel (VBScript)](../../../ado/reference/rds-api/datafactory-object-query-method-and-createobject-method-example-vbscript.md)


