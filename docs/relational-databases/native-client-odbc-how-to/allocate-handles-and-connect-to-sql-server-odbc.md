---
title: Zuordnen von Handles und Verbinden mit SQLServer (ODBC) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- handles [ODBC]
- handles [ODBC], connection
- handles [ODBC], about handles
ms.assetid: 6172cd52-9c9a-467d-992f-def07f3f3bb1
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 2144513a5f5de453c93215edcc2bb416d53781bc
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/15/2018
ms.locfileid: "51677379"
---
# <a name="allocate-handles-and-connect-to-sql-server-odbc"></a>Zuordnen von Handles und Herstellen einer Verbindung mit SQL Server (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

    
### <a name="to-allocate-handles-and-connect-to-sql-server"></a>So ordnen Sie Handles zu und stellen eine Verbindung mit SQL Server her  
  
1.  Schließen Sie die ODBC-Headerdateien Sql.h, Sqlext.h und Sqltypes.h ein.  
  
2.  Schließen Sie die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-treiberspezifische Headerdatei Odbcss.h ein.  
  
3.  Rufen Sie [SQLAllocHandle](https://go.microsoft.com/fwlink/?LinkId=58396) mit einem **HandleType** SQL_HANDLE_ENV auf, um ODBC zu initialisieren und ein Umgebungshandle zuzuordnen.  
  
4.  Rufen Sie [SQLSetEnvAttr](../../relational-databases/native-client-odbc-api/sqlsetenvattr.md) mit **Attribut** festgelegt auf SQL_ATTR_ODBC_VERSION und **ValuePtr** auf SQL_OV_ODBC3 festgelegt ist, um anzugeben, die Anwendung verwendet ODBC 3.x-Format-Funktion wird aufgerufen.  
  
5.  Rufen Sie optional [SQLSetEnvAttr](../../relational-databases/native-client-odbc-api/sqlsetenvattr.md) anderen Umgebungen festgelegt, oder rufen [SQLGetEnvAttr](https://go.microsoft.com/fwlink/?LinkId=58403) um Umgebungsoptionen abzurufen.  
  
6.  Rufen Sie [SQLAllocHandle](https://go.microsoft.com/fwlink/?LinkId=58396) mit einem **HandleType** SQL_HANDLE_DBC auf, um ein Verbindungshandle zuzuordnen.  
  
7.  Rufen Sie optional [SQLSetConnectAttr](../../relational-databases/native-client-odbc-api/sqlsetconnectattr.md) um Verbindungsoptionen festzulegen, oder rufen [SQLGetConnectAttr](../../relational-databases/native-client-odbc-api/sqlgetconnectattr.md) um Optionen zu erhalten.  
  
8.  SQLConnect auf, um eine vorhandene Datenquelle zu verwenden, um das Herstellen einer Verbindung mit Aufrufen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
     oder  
  
     Rufen Sie [SQLDriverConnect](../../relational-databases/native-client-odbc-api/sqldriverconnect.md) verwenden Sie eine Verbindungszeichenfolge zum Herstellen einer Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
     Eine minimale vollständige [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Verbindungszeichenfolge weist eine der beiden folgenden Formen auf:  
  
    ```  
    DSN=dsn_name;Trusted_connection=yes;  
    DRIVER={SQL Server Native Client 10.0};SERVER=server;Trusted_connection=yes;  
    ```  
  
     Wenn die Verbindungszeichenfolge nicht abgeschlossen ist, ist **SQLDriverConnect** kann für die erforderlichen Informationen auffordern. Dies wird gesteuert, indem der angegebene Wert für die *DriverCompletion* Parameter.  
  
     \- oder –  
  
     Rufen Sie [SQLBrowseConnect](../../relational-databases/native-client-odbc-api/sqlbrowseconnect.md) mehrere Male in einer iterativen Weise auf die Verbindungszeichenfolge erstellen und eine Verbindung mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
9. Rufen Sie optional [SQLGetInfo](../../relational-databases/native-client-odbc-api/sqlgetinfo.md) abzurufenden Treiberattribute und-Verhalten für die [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Datenquelle.  
  
10. Ordnen Sie Anweisungen zu und verwenden Sie sie.  
  
11. Rufen Sie SQLDisconnect beim Trennen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] und das Verbindungshandle für eine neue Verbindung verfügbar zu machen.  
  
12. Rufen Sie [SQLFreeHandle](../../relational-databases/native-client-odbc-api/sqlfreehandle.md) mit einem **HandleType** SQL_HANDLE_DBC auf, um das Verbindungshandle freizugeben.  
  
13. Rufen Sie **SQLFreeHandle** mit einem **HandleType** SQL_HANDLE_ENV auf, um das Umgebungshandle freizugeben.  
  
> [!IMPORTANT]  
>  Verwenden Sie nach Möglichkeit die Windows-Authentifizierung. Wenn die Windows-Authentifizierung nicht verfügbar ist, fordern Sie die Benutzer auf, ihre Anmeldeinformationen zur Laufzeit einzugeben. Die Anmeldeinformationen sollten nicht in einer Datei gespeichert werden. Wenn Sie die Anmeldeinformationen permanent speichern müssen, verschlüsseln Sie sie mit der [Win32 Crypto-API](https://go.microsoft.com/fwlink/?LinkId=64532).  
  
## <a name="example"></a>Beispiel  
 Dieses Beispiel zeigt einen Aufruf von **SQLDriverConnect** für die Verbindung mit einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ohne eine vorhandene ODBC-Datenquelle. Durch Übergabe einer unvollständigen Verbindungszeichenfolge an **SQLDriverConnect**, wird der ODBC-Treiber den Benutzer auffordern, die fehlenden Informationen einzugeben.  
  
```  
#define MAXBUFLEN   255  
  
SQLHENV      henv = SQL_NULL_HENV;  
SQLHDBC      hdbc1 = SQL_NULL_HDBC;  
SQLHSTMT      hstmt1 = SQL_NULL_HSTMT;  
  
SQLCHAR      ConnStrIn[MAXBUFLEN] =  
         "DRIVER={SQL Server Native Client 10.0};SERVER=MyServer";  
  
SQLCHAR      ConnStrOut[MAXBUFLEN];  
SQLSMALLINT   cbConnStrOut = 0;  
  
// Make connection without data source. Ask that driver   
// prompt if insufficient information. Driver returns  
// SQL_ERROR and application prompts user  
// for missing information. Window handle not needed for  
// SQL_DRIVER_NOPROMPT.  
retcode = SQLDriverConnect(hdbc1,      // Connection handle  
                  NULL,         // Window handle  
                  ConnStrIn,      // Input connect string  
                  SQL_NTS,         // Null-terminated string  
                  ConnStrOut,      // Address of output buffer  
                  MAXBUFLEN,      // Size of output buffer  
                  &cbConnStrOut,   // Address of output length  
                  SQL_DRIVER_PROMPT);  
```  
  
  
