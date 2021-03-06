---
title: Verwenden von Multiple Active Resultsets (MARS) | Microsoft-Dokumentation
description: Verwenden von Multiple Active Result Sets (MARS)
ms.custom: ''
ms.date: 06/12/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: connectivity
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, MARS
- MSOLEDBSQL, MARS
- data access [OLE DB Driver for SQL Server], MARS
- Multiple Active Result Sets
- OLE DB Driver for SQL Server, MARS
- MARS [SQL Server]
author: pmasl
ms.author: pelopes
manager: craigg
ms.openlocfilehash: 7f0c8c9d13eca087db3d7202d57c058527e2c073
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MTE75
ms.contentlocale: de-DE
ms.lasthandoff: 10/01/2018
ms.locfileid: "47610318"
---
# <a name="using-multiple-active-result-sets-mars"></a>Verwenden von Multiple Active Result Sets (MARS)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Seit [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] werden Multiple Active Result Sets (MARS) in Anwendungen unterstützt, die auf [!INCLUDE[ssDE](../../../includes/ssde-md.md)] zugreifen. In früheren Versionen von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] konnten Datenbankanwendungen nicht mehrere aktive Anweisungen über eine Verbindung verwalten. Beim Verwenden von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Standardresultsets musste die Anwendung alle Resultsets aus einem Batch verarbeiten oder abbrechen, bevor ein anderer Batch auf dieser Verbindung ausgeführt werden konnte. In [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] wurde ein neues Verbindungsattribut eingeführt, das es Anwendungen ermöglicht, mehr als eine ausstehende Anforderung pro Verbindung und mehr als ein aktives Standardresultset pro Verbindung anzugeben.  
  
 MARS vereinfacht den Anwendungsentwurf mit den folgenden neuen Fähigkeiten:  
  
-   Anwendungen können mehrere Standardresultsets geöffnet haben und die Lesevorgänge daraus verschachteln.  
  
-   Anwendungen können bei geöffneten Standardresultsets andere Anweisungen ausführen (z. B. INSERT, UPDATE, DELETE und Aufrufe gespeicherter Prozeduren).  
  
 Für Anwendungen, die MARS verwenden, gelten die folgenden nützlichen Richtlinien:  
  
-   Standardresultsets sollten für kurzlebige oder kurze Resultsets verwendet werden, die durch einzelne SQL-Anweisungen generiert werden (SELECT, DML mit OUTPUT, RECEIVE, READ TEXT usw.).  
  
-   Servercursor sollten für längerlebige oder große Resultsets verwendet werden, die durch einzelne SQL-Anweisungen generierte werden.  
  
-   Lesen Sie bei Batches, die mehrere Ergebnisse zurückgeben, und bei Prozeduranforderungen immer bis zum Ende der Results, unabhängig davon, ob Ergebnisse zurückgeben werden oder nicht.  
  
-   Wo möglich, verwenden Sie anstelle von [!INCLUDE[tsql](../../../includes/tsql-md.md)]-Anweisungen API-Aufrufe, um Verbindungseigenschaften zu ändern und Transaktionen zu verwalten.  
  
-   In MARS wird ein Identitätswechsel im Bereich einer Sitzung verhindert, solange gleichzeitige Batches ausgeführt werden.  
  
> [!NOTE]  
>  Standardmäßig ist die MARS-Funktionalität nicht aktiviert. Um MARS bei Herstellen einer Verbindung mit [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] mit OLE DB-Treiber für SQL Server, Sie müssen explizit aktivieren sie in einer Verbindungszeichenfolge. Weitere Informationen finden Sie in der OLE DB-Treiber für SQL Server-Abschnitte, weiter unten in diesem Thema.  
  
 OLE DB-Treiber für SQL Server beschränkt nicht die Anzahl aktiver Anweisungen über eine Verbindung.  
  
 Traditionelle Anwendungen, bei denen kein Bedarf an mehreren Batches oder gespeicherten Prozeduren aus mehreren gleichzeitig ausgeführten Anweisungen besteht, profitieren von MARS, ohne die Implementierung von MARS verstehen zu müssen. Anwendungen mit komplexeren Anforderungen müssen diese jedoch berücksichtigen.  
  
 MARS ermöglicht die verschachtelte Ausführung mehrerer Anforderungen innerhalb einer einzelnen Verbindung. Das bedeutet, dass innerhalb der Ausführung eines Batches eine weitere Anforderung ausgeführt werden kann. Beachten Sie jedoch, dass MARS mit Blick auf Interleaving, nicht die parallele Ausführung definiert ist.  
  
 Die MARS-Infrastruktur ermöglicht die verschachtelte Ausführung mehrerer Batches, die Ausführung kann jedoch nur an genau definierten Punkten gewechselt werden. Außerdem müssen die meisten Anweisungen innerhalb eines Batches atomar ausgeführt werden. Anweisungen, die Zeilen an den Client zurückgeben (gelegentlich bezeichnet als *Zwischenergebnispunkte*) dürfen die Ausführung vor Abschluss verschachteln, während noch Zeilen an den Client gesendet werden. Beispiel:  
  
-   SELECT  
  
-   FETCH  
  
-   RECEIVE  
  
 Alle anderen Anweisungen, die im Rahmen einer gespeicherten Prozedur oder eines Batches ausgeführt werden, müssen zunächst abgeschlossen werden, ehe die Ausführung zu anderen MARS-Anforderungen umgeschaltet werden kann.  
  
 Wie Batches die Ausführung genau verschachteln, hängt von zahlreichen Faktoren ab, und die exakte Ausführungsfolge von Befehlen aus mehreren Batches mit Zwischenergebnispunkten lässt sich nur schwer vorhersagen. Achten Sie darauf, unerwünschte Nebeneffekte aufgrund der verschachtelten Ausführung solcher komplexer Batches zu vermeiden.  
  
 Sie vermeiden Probleme, indem Sie den Verbindungsstatus (SET, USE) und Transaktionen (BEGIN TRAN, COMMIT, ROLLBACK) an Stelle von [!INCLUDE[tsql](../../../includes/tsql-md.md)]-Anweisungen mit API-Aufrufen verwalten. Schließen Sie diese Anweisungen zudem nicht in Batches mit mehreren Anweisungen ein, die auch Zwischenergebnispunkte enthalten, und serialisieren Sie die Ausführung solcher Batches durch Verarbeitung oder Abbruch aller Ergebnisse.  
  
> [!NOTE]  
>  Ein Batch oder eine gespeicherte Prozedur, die bei Aktivierung von MARS eine manuelle oder implizite Transaktion startet, muss diese Transaktion vor Ausführung des Batchs abschließen. Andernfalls führt [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] nach Abschluss des Batchs einen Rollback für alle von der Transaktion vorgenommenen Änderungen aus. Eine derartige Transaktion wird von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] als Transaktion im Bereich des Batchs verwaltet. Dieser Transaktionstyp wurde in [!INCLUDE[ssVersion2005](../../../includes/ssversion2005-md.md)] neu eingeführt, um vorhandene, gut konzipierte gespeicherte Prozeduren verwenden zu können, wenn MARS aktiviert ist. Weitere Informationen zu Transaktionen mit batchbereich, finden Sie unter [Transaction-Anweisungen &#40;Transact-SQL&#41;](../../../t-sql/statements/statements.md).  
  
 Ein Beispiel der Verwendung von MARS aus ADO finden Sie unter [mithilfe von ADO mit OLE DB-Treiber für SQL Server](../../oledb/applications/using-ado-with-oledb-driver-for-sql-server.md).  
  
## <a name="in-memory-oltp"></a>In-Memory OLTP  
 In-Memory-OLTP unterstützt MARS mithilfe von Abfragen und systemintern kompilierte gespeicherte Prozeduren. MARS ermöglicht die anfordernde Daten aus mehreren Abfragen ohne die einzelnen Resultsets, die vor dem Senden einer Anforderung zum Abrufen von Zeilen aus einem neuen Resultset vollständig abrufen. Um mehrere geöffneten Resultsets erfolgreich gelesen werden, müssen Sie eine aktivierter MARS-Verbindung verwenden.  
  
 MARS ist standardmäßig deaktiviert, sodass Sie es explizit durch das Hinzufügen aktivieren müssen `MultipleActiveResultSets=True` auf eine Verbindungszeichenfolge. Im folgende Beispiel wird veranschaulicht, wie eine Verbindung mit einer Instanz von SQL Server, und geben an, dass MARS aktiviert ist:  
  
```  
Data Source=MSSQL; Initial Catalog=AdventureWorks; Integrated Security=SSPI; MultipleActiveResultSets=True  
```  
  
 MARS mit In-Memory-OLTP ist im Grunde identisch mit MARS im weiteren Verlauf der SQL-Engine. Im folgenden werden die Unterschiede beim Verwenden von MARS in speicheroptimierten Tabellen und systemintern gespeicherten Prozeduren kompilierten aufgeführt.  
  
 **MARS und Speicheroptimierte Tabellen**  
  
 Im folgenden sind die Unterschiede zwischen datenträgerbasierte und Speicheroptimierte Tabellen bei der Verbindung mit einem MARS aktiviert werden:  
  
-   Zwei Anweisungen können Daten in dem gleichen Zielobjekt ändern, wenn beide versuchen, denselben Datensatz zu ändern ein Write-Write-Konflikt führt aber zu den neuen Vorgang fehlschlägt. Wenn beide Vorgänge auf unterschiedliche Datensätze ändern, werden jedoch die Vorgänge erfolgreich.  
  
-   Jede Anweisung unter momentaufnahmeisolation ausgeführt wird, sodass neue Vorgänge nicht von den vorhandenen Anweisungen vorgenommene Änderungen sehen können. Auch wenn die gleichzeitigen Anweisungen unter der gleichen Transaktion ausgeführt werden erstellt die SQL-Engine mit batchbereich Transaktionen für jede Anweisung, die voneinander isoliert sind. Transaktionen mit batchbereich sind daher ein Rollback für eine Transaktion mit batchbereich anderen Formeln in demselben Batch wirkt sich jedoch immer noch miteinander verbunden.  
  
-   DDL-Vorgänge sind in Transaktionen nicht zulässig, sodass sie sofort fehl.  
  
 **MARS und nativ kompilierte gespeicherte Prozeduren**  
  
 Systemintern kompilierte gespeicherte Prozeduren können in Verbindungen mit aktivierter MARS-Funktion ausgeführt und können die Ausführung an eine andere Anweisung ergibt, nur, wenn ein Yield-Punkt gefunden wird. Ein Yield-Punkt erfordert eine SELECT-Anweisung die einzige Anweisung in einer systemintern kompilierten gespeicherten Prozedur handelt, die Ausführung einer anderen Anweisung ergeben können. Wenn eine SELECT-Anweisung nicht in die Prozedur vorhanden, die sie nicht liefert ist, wird es bis zum Abschluss ausgeführt, bevor andere Anweisungen beginnen.  
  
 **MARS und In-Memory-OLTP-Transaktionen**  
  
 Von Anweisungen und atomic-Blöcke, die sich überlappen vorgenommenen Änderungen sind voneinander isoliert. Z. B. wenn eine Anweisung oder atomic-Block nimmt einige Änderungen vor, und klicken Sie dann setzt die Ausführung auf einer anderen Anweisung aus, sehen die neue Anweisung nicht durch die erste Anweisung vorgenommene Änderungen. Darüber hinaus bei der ersten Anweisung die Ausführung fortgesetzt wird, wird sie keine Änderungen, die von allen anderen Anweisungen angezeigt. Anweisungen werden nur Änderungen angezeigt, die abgeschlossen und ein Commit ausgeführt, bevor die Anweisung beginnt.  
  
 Eine neue Benutzertransaktion in der aktuellen Benutzertransaktion, die mit der BEGIN TRANSACTION-Anweisung gestartet werden – dies ist nur im interop-Modus unterstützt werden, damit der BEGIN TRANSACTION kann nur von einer T-SQL-Anweisung aufgerufen werden und nicht aus innerhalb einer systemintern kompilierten gespeicherten die Prozedur. Sie können einen erstellen, zeigen Sie mit der Transaktion zu speichern oder einen API-Aufruf zu Transaktion in einer Transaktion. Save(save_point_name), ein Rollback zum Sicherungspunkt auszuführen. Dieses Feature ist auch nur von T-SQL-Anweisungen aktiviert und nicht in systemintern kompilierten gespeicherten Prozeduren.  
  
 **MARS und columnstore-Indizes**  
  
 SQL Server (ab 2016) unterstützt MARS mit columnstore-Indizes. SQL Server 2014 verwendet MARS für schreibgeschützte Verbindungen mit Tabellen mit einem Columnstore-Index.    SQL Server 2014 unterstützt MARS jedoch nicht für gleichzeitige DML-Vorgänge (Data Manipulation Language, Datenbearbeitungssprache) für eine Tabelle mit einem Columnstore-Index. In diesem Fall beendet SQL Server die Verbindung und bricht die Transaktionen ab.   SQL Server 2012 bietet nur-Lese columnstore-Indizes und MARS gilt nicht für sie.  
  
## <a name="ole-db-driver-for-sql-server"></a>OLE DB-Treiber für SQL Server  
 Der OLE DB-Treiber für SQL Server unterstützt MARS durch Hinzufügen der SSPROP_INIT_MARSCONNECTION-Eigenschaft zur Datenquelleninitialisierung, die in der Eigenschaftengruppe DBPROPSET_SQLSERVERDBINIT implementiert wird. Außerdem wurde ein neues Verbindungszeichenfolgen-Schlüsselwort, **MarsConn**, aufgenommen. Er akzeptiert **"true"** oder **"false"** Werte **"false"** ist die Standardeinstellung.  
  
 Die Datenquelleneigenschaft DBPROP_MULTIPLECONNECTIONS ist standardmäßig auf VARIANT_TRUE festgelegt. Das bedeutet, der Anbieter erzeugt mehrere Verbindungen, um mehrere gleichzeitige Befehls- und Rowsetobjekte zu unterstützen. Ist MARS aktiviert, kann der OLE DB-Treiber für SQL Server mehrere Befehls- und Rowsetobjekte in einer einzelnen Verbindung unterstützen. Daher ist MULTIPLE_CONNECTIONS standardmäßig auf VARIANT_FALSE festgelegt.  
  
 Weitere Informationen zu Verbesserungen der DBPROPSET_SQLSERVERDBINIT-Eigenschaftensatz finden Sie unter [Initialisierungs- und Autorisierungseigenschaften](../../oledb/ole-db-data-source-objects/initialization-and-authorization-properties.md).  
  
### <a name="ole-db-driver-for-sql-server-example"></a>OLE DB-Treiber für SQL Server: Beispiel  
 In diesem Beispiel wird mit dem OLE DB-Treiber für SQL Server ein Datenquellenobjekt erstellt. Vor der Erstellung des Sitzungsobjekts wird MARS mithilfe der DBPROPSET_SQLSERVERDBINIT-Eigenschaftengruppe aktiviert.  
  
```  
#include <msoledbsql.h>  
  
IDBInitialize *pIDBInitialize = NULL;  
IDBCreateSession *pIDBCreateSession = NULL;  
IDBProperties *pIDBProperties = NULL;  
  
// Create the data source object.  
hr = CoCreateInstance(CLSID_MSOLEDBSQL, NULL,  
   CLSCTX_INPROC_SERVER,  
   IID_IDBInitialize,   
    (void**)&pIDBInitialize);  
  
hr = pIDBInitialize->QueryInterface(IID_IDBProperties, (void**)&pIDBProperties);  
  
// Set the MARS property.  
DBPROP rgPropMARS;  
  
// The following is necessary since MARS is off by default.  
rgPropMARS.dwPropertyID = SSPROP_INIT_MARSCONNECTION;  
rgPropMARS.dwOptions = DBPROPOPTIONS_REQUIRED;  
rgPropMARS.dwStatus = DBPROPSTATUS_OK;  
rgPropMARS.colid = DB_NULLID;  
V_VT(&(rgPropMARS.vValue)) = VT_BOOL;  
V_BOOL(&(rgPropMARS.vValue)) = VARIANT_TRUE;  
  
// Create the structure containing the properties.  
DBPROPSET PropSet;  
PropSet.rgProperties = &rgPropMARS;  
PropSet.cProperties = 1;  
PropSet.guidPropertySet = DBPROPSET_SQLSERVERDBINIT;  
  
// Get an IDBProperties pointer and set the initialization properties.  
pIDBProperties->SetProperties(1, &PropSet);  
pIDBProperties->Release();  
  
// Initialize the data source object.  
hr = pIDBInitialize->Initialize();  
  
//Create a session object from a data source object.  
IOpenRowset * pIOpenRowset = NULL;  
hr = IDBInitialize->QueryInterface(IID_IDBCreateSession, (void**)&pIDBCreateSession));  
hr = pIDBCreateSession->CreateSession(  
   NULL,             // pUnkOuter  
   IID_IOpenRowset,  // riid  
  &pIOpenRowset ));  // ppSession  
  
// Create a rowset with a firehose mode cursor.  
IRowset *pIRowset = NULL;  
DBPROP rgRowsetProperties[2];  
  
// To get a firehose mode cursor request a   
// forward only read only rowset.  
rgRowsetProperties[0].dwPropertyID = DBPROP_IRowsetLocate;  
rgRowsetProperties[0].dwOptions = DBPROPOPTIONS_REQUIRED;  
rgRowsetProperties[0].dwStatus = DBPROPSTATUS_OK;  
rgRowsetProperties[0].colid = DB_NULLID;  
VariantInit(&(rgRowsetProperties[0].vValue));  
rgRowsetProperties[0].vValue.vt = VARIANT_BOOL;  
rgRowsetProperties[0].vValue.boolVal = VARIANT_FALSE;  
  
rgRowsetProperties[1].dwPropertyID = DBPROP_IRowsetChange;  
rgRowsetProperties[1].dwOptions = DBPROPOPTIONS_REQUIRED;  
rgRowsetProperties[1].dwStatus = DBPROPSTATUS_OK;  
rgRowsetProperties[1].colid = DB_NULLID;  
VariantInit(&(rgRowsetProperties[1].vValue));  
rgRowsetProperties[1].vValue.vt = VARIANT_BOOL;  
rgRowsetProperties[1].vValue.boolVal = VARIANT_FALSE;  
  
DBPROPSET rgRowsetPropSet[1];  
rgRowsetPropSet[0].rgProperties = rgRowsetProperties  
rgRowsetPropSet[0].cProperties = 2  
rgRowsetPropSet[0].guidPropertySet = DBPROPSET_ROWSET;  
  
hr = pIOpenRowset->OpenRowset (NULL,  
   &TableID,  
   NULL,  
   IID_IRowset,  
   1,  
   rgRowsetPropSet  
   (IUnknown**)&pIRowset);  
```  

  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [OLE DB-Treiber für SQL Server-Features](../../oledb/features/oledb-driver-for-sql-server-features.md)   
 
  
  
