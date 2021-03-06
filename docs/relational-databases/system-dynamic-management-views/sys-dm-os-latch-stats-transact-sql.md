---
title: Sys. dm_os_latch_stats (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 08/18/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_os_latch_stats_TSQL
- dm_os_latch_stats_TSQL
- dm_os_latch_stats
- sys.dm_os_latch_stats
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_latch_stats dynamic management view
ms.assetid: 2085d9fc-828c-453e-82ec-b54ed8347ae5
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1fe8a78047be763aecb898a48a882b8f08d3bfb6
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/01/2018
ms.locfileid: "47734030"
---
# <a name="sysdmoslatchstats-transact-sql"></a>sys.dm_os_latch_stats (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt Informationen zu allen nach Klassen sortierten Latchwartevorgängen zurück.  
  
> [!NOTE]  
>  Aufrufen von [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)] oder [!INCLUDE[ssPDW](../../includes/sspdw-md.md)], verwenden Sie den Namen **sys.dm_pdw_nodes_os_latch_stats**.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|latch_class|**nvarchar(120)**|Name der Latchklasse.|  
|waiting_requests_count|**bigint**|Anzahl der Wartevorgänge auf Latches in dieser Klasse. Dieser Leistungsindikator wird beim Starten eines Latchwartevorgangs erhöht.|  
|wait_time_ms|**bigint**|Gesamtwartezeit auf Latches in dieser Klasse (in Millisekunden).<br /><br /> **Hinweis:** in dieser Spalte wird alle fünf Minuten während eines latchwartevorgangs und am Ende eines latchwartevorgangs aktualisiert.|  
|max_wait_time_ms|**bigint**|Maximale Zeitdauer, die ein Speicherobjekt auf diesen Latch gewartet hat. Wenn dieser Wert ungewöhnlich hoch ist, kann dies ein Hinweis auf einen internen Deadlock sein.|  
|pdw_node_id|**int**|**Gilt für**: [!INCLUDE[ssSDWfull](../../includes/sssdwfull-md.md)], [!INCLUDE[ssPDW](../../includes/sspdw-md.md)]<br /><br /> Der Bezeichner für den Knoten, dem auf diesem Verteilungspunkt befindet.|  
  
## <a name="permissions"></a>Berechtigungen  

Auf [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)], erfordert `VIEW SERVER STATE` Berechtigung.   
Auf [!INCLUDE[ssSDS_md](../../includes/sssds-md.md)], erfordert die `VIEW DATABASE STATE` Berechtigung in der Datenbank.   
  
## <a name="remarks"></a>Hinweise  
 Sys. dm_os_latch_stats kann verwendet werden, zum Identifizieren der Quelle von latchkonflikten anhand die relative Anzahl und der Wartezeiten für die verschiedenen latchklassen. In einigen Fällen können Sie Latchkonflikte möglicherweise lösen oder reduzieren. Es kann jedoch Situationen geben, in denen Sie sich mit [!INCLUDE[msCoName](../../includes/msconame-md.md)] Support Services in Verbindung setzen müssen.  
  
 Sie können den Inhalt der Sys. dm_os_latch_stats zurücksetzen, indem Sie mithilfe von `DBCC SQLPERF` wie folgt:  
  
```  
DBCC SQLPERF ('sys.dm_os_latch_stats', CLEAR);  
GO  
```  
  
 Dadurch werden alle Leistungsindikatoren auf 0 zurückgesetzt.  
  
> [!NOTE]  
>  Diese Statistiken werden nicht persistent gespeichert, wenn [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] neu gestartet wird. Alle Daten stellen einen Gesamtwert seit dem letzten Zurücksetzen der Statistiken oder dem Starten von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dar.  
  
## <a name="latches"></a>Latches  
 Ein Latch ist ein Lightweight-Synchronisierungsobjekt, das von verschiedenen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Komponenten verwendet wird. Ein Latch wird in erster Linie zum Synchronisieren von Datenbankseiten verwendet. Jedem Latch wird eine einzelne Zuordnungseinheit zugeordnet.  
  
 Ein Latchwartevorgang findet dann statt, wenn der Latch nicht sofort erteilt werden kann, da er von einem anderen Thread in einem in Konflikt stehenden Modus beansprucht wird. Im Gegensatz zu Sperren wird ein Latch unmittelbar nach dem Vorgang freigegeben, selbst bei Schreibvorgängen.  
  
 Latches werden nach Klassen gruppiert, die auf Komponenten und der Verwendung basieren. 0 oder mehr Latches einer bestimmten Klasse können zu jeder Zeit in einer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz vorhanden sein.  
  
> [!NOTE]  
>  Sys. dm_os_latch_stats verfolgt Latchanforderungen nicht nach, die sofort erteilt werden soll, oder die ohne warten einen Fehler.  
  
 Die folgende Tabelle enthält kurze Beschreibungen der verschiedenen Latchklassen.  
  
|Latchklasse|Description|  
|-----------------|-----------------|  
|ALLOC_CREATE_RINGBUF|Wird intern von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] zum Initialisieren der Synchronisierung beim Erstellen eines Zuordnungsringpuffers verwendet.|  
|ALLOC_CREATE_FREESPACE_CACHE|Wird zum Initialisieren der Synchronisierung interner Caches für freien Speicher für Heaps verwendet.|  
|ALLOC_CACHE_MANAGER|Wird zum Synchronisieren interner Kohärenztests verwendet.|  
|ALLOC_FREESPACE_CACHE|Wird zum Synchronisieren des Zugriffs auf einen Seitencache mit verfügbarem Speicher für Heaps und BLOBs (Binary Large Objects) verwendet. Konflikte bei Latches dieser Klasse können auftreten, wenn mehrere Verbindungen versuchen, gleichzeitig Zeilen in einen Heap oder ein BLOB einzufügen. Durch Partitionieren des Objekts sinkt das Konfliktrisiko. Jede Partition verfügt über einen eigenen Latch. Durch das Partitionieren werden die Einfügevorgänge auf mehrere Latches verteilt.|  
|ALLOC_EXTENT_CACHE|Wird zum Synchronisieren des Zugriffs auf einen Cache mit Blöcken verwendet, die nicht zugeordnete Seiten enthalten. Konflikte bei Latches dieser Klasse können auftreten, wenn mehrere Verbindungen versuchen, gleichzeitig in derselben Zuordnungseinheit Datenseiten zuzuordnen. Das Konfliktrisiko kann durch Partitionieren des Objekts, zu dem diese Zuordnungseinheit gehört, gesenkt werden.|  
|ACCESS_METHODS_DATASET_PARENT|Wird zum Synchronisieren des Zugriffs des untergeordneten Datasets auf das übergeordnete Dataset während paralleler Vorgänge verwendet.|  
|ACCESS_METHODS_HOBT_FACTORY|Wird zum Synchronisieren des Zugriffs auf eine interne Hashtabelle verwendet.|  
|ACCESS_METHODS_HOBT|Wird zum Synchronisieren des Zugriffs auf die speicherinterne Darstellung eines HoBts verwendet.|  
|ACCESS_METHODS_HOBT_COUNT|Wird zum Synchronisieren des Zugriffs auf HoBt-Seiten- und Zeilenleistungsindikatoren verwendet.|  
|ACCESS_METHODS_HOBT_VIRTUAL_ROOT|Wird zum Synchronisieren des Zugriffs auf die Stammseitenabstraktion einer internen B-Struktur verwendet.|  
|ACCESS_METHODS_CACHE_ONLY_HOBT_ALLOC|Wird zum Synchronisieren des Zugriffs auf Arbeitstabellen verwendet.|  
|ACCESS_METHODS_BULK_ALLOC|Wird zum Synchronisieren des Zugriffs innerhalb von Massenzuordnungen verwendet.|  
|ACCESS_METHODS_SCAN_RANGE_GENERATOR|Wird zum Synchronisieren des Zugriffs auf einen Bereichgenerator während paralleler Scans verwendet.|  
|ACCESS_METHODS_KEY_RANGE_GENERATOR|Wird zum Synchronisieren des Zugriffs auf Read-Ahead-Vorgänge während paralleler Scans in Schlüsselbereichen verwendet.|  
|APPEND_ONLY_STORAGE_INSERT_POINT|Wird zum Synchronisieren von Einfügungen in schnellen Nur anhängen-Speichereinheiten verwendet.|  
|APPEND_ONLY_STORAGE_FIRST_ALLOC|Wird zum Synchronisieren der ersten Zuordnung für eine Nur anhängen-Speichereinheit verwendet.|  
|APPEND_ONLY_STORAGE_UNIT_MANAGER|Wird zum Synchronisieren des Zugriffs auf die interne Datenstruktur innerhalb der Verwaltung schneller Nur anhängen-Speichereinheiten verwendet.|  
|APPEND_ONLY_STORAGE_MANAGER|Wird zum Synchronisieren von Verkleinerungsvorgängen bei der Verwaltung schneller Nur anhängen-Speichereinheiten verwendet.|  
|BACKUP_RESULT_SET|Wird zum Synchronisieren paralleler Sicherungsresultsets verwendet.|  
|BACKUP_TAPE_POOL|Wird zum Synchronisieren von Pools mit Sicherungsbändern verwendet.|  
|BACKUP_LOG_REDO|Wird zum Synchronisieren von Wiederholungsvorgängen für Sicherungsprotokolle verwendet.|  
|BACKUP_INSTANCE_ID|Wird zum Synchronisieren der Generierung von Instanz-IDs für Sicherungsleistungsindikatoren verwendet.|  
|BACKUP_MANAGER|Wird zum Synchronisieren des internen Sicherungs-Managers verwendet.|  
|BACKUP_MANAGER_DIFFERENTIAL|Wird zum Synchronisieren differenzieller Sicherungsvorgänge mit DBCC verwendet.|  
|BACKUP_OPERATION|Wird für die interne Datenstruktursynchronisierung in einem Sicherungsvorgang verwendet, wie z. B. in einer Datenbank-, Protokoll- oder Dateisicherung.|  
|BACKUP_FILE_HANDLE|Wird zum Synchronisieren von Vorgängen zum Öffnen von Dateien während einer Wiederherstellung verwendet.|  
|BUFFER|Wird zum Synchronisieren des kurzfristigen Zugriffs auf Datenbankseiten verwendet. Vor dem Lesen oder Ändern von Datenbankseiten ist ein Pufferlatch erforderlich. Pufferlatchkonflikte können ein Hinweis auf unterschiedliche Probleme sein, darunter Hotpages und langsame E/A-Vorgänge.<br /><br /> Diese Latchklasse umfasst alle möglichen Verwendungen von Seitenlatches. Sys. dm_os_wait_stats macht einen Unterschied zwischen Seitenlatch-Wartevorgängen, die entstehen durch e/a-Vorgänge und Lese- und Schreibvorgänge auf der Seite.|  
|BUFFER_POOL_GROW|Wird für die Synchronisierung des internen Puffer-Managers während Erweiterungen des Pufferpools verwendet.|  
|DATABASE_CHECKPOINT|Wird für die Serialisierung von Prüfpunkten in einer Datenbank verwendet.|  
|CLR_PROCEDURE_HASHTABLE|Nur interne Verwendung.|  
|CLR_UDX_STORE|Nur interne Verwendung.|  
|CLR_DATAT_ACCESS|Nur interne Verwendung.|  
|CLR_XVAR_PROXY_LIST|Nur interne Verwendung.|  
|DBCC_CHECK_AGGREGATE|Nur interne Verwendung.|  
|DBCC_CHECK_RESULTSET|Nur interne Verwendung.|  
|DBCC_CHECK_TABLE|Nur interne Verwendung.|  
|DBCC_CHECK_TABLE_INIT|Nur interne Verwendung.|  
|DBCC_CHECK_TRACE_LIST|Nur interne Verwendung.|  
|DBCC_FILE_CHECK_OBJECT|Nur interne Verwendung.|  
|DBCC_PERF|Wird zum Synchronisieren interner Leistungsindikatoren verwendet.|  
|DBCC_PFS_STATUS|Nur interne Verwendung.|  
|DBCC_OBJECT_METADATA|Nur interne Verwendung.|  
|DBCC_HASH_DLL|Nur interne Verwendung.|  
|EVENTING_CACHE|Nur interne Verwendung.|  
|FCB|Wird zum Synchronisieren des Zugriffs auf den Dateikontrollblock verwendet.|  
|FCB_REPLICA|Nur interne Verwendung.|  
|FGCB_ALLOC|Wird zum Synchronisieren des Zugriffs auf Roundrobin-Zuordnungsinformationen in einer Dateigruppe verwendet.|  
|FGCB_ADD_REMOVE|Verwenden Sie zum Synchronisieren des Zugriffs auf Dateigruppen für hinzufügen, löschen, Größe und Position Dateivorgänge.|  
|FILEGROUP_MANAGER|Nur interne Verwendung.|  
|FILE_MANAGER|Nur interne Verwendung.|  
|FILESTREAM_FCB|Nur interne Verwendung.|  
|FILESTREAM_FILE_MANAGER|Nur interne Verwendung.|  
|FILESTREAM_GHOST_FILES|Nur interne Verwendung.|  
|FILESTREAM_DFS_ROOT|Nur interne Verwendung.|  
|LOG_MANAGER|Nur interne Verwendung.|  
|FULLTEXT_DOCUMENT_ID|Nur interne Verwendung.|  
|FULLTEXT_DOCUMENT_ID_TRANSACTION|Nur interne Verwendung.|  
|FULLTEXT_DOCUMENT_ID_NOTIFY|Nur interne Verwendung.|  
|FULLTEXT_LOGS|Nur interne Verwendung.|  
|FULLTEXT_CRAWL_LOG|Nur interne Verwendung.|  
|FULLTEXT_ADMIN|Nur interne Verwendung.|  
|FULLTEXT_AMDIN_COMMAND_CACHE|Nur interne Verwendung.|  
|FULLTEXT_LANGUAGE_TABLE|Nur interne Verwendung.|  
|FULLTEXT_CRAWL_DM_LIST|Nur interne Verwendung.|  
|FULLTEXT_CRAWL_CATALOG|Nur interne Verwendung.|  
|FULLTEXT_FILE_MANAGER|Nur interne Verwendung.|  
|DATABASE_MIRRORING_REDO|Nur interne Verwendung.|  
|DATABASE_MIRRORING_SERVER|Nur interne Verwendung.|  
|DATABASE_MIRRORING_CONNECTION|Nur interne Verwendung.|  
|DATABASE_MIRRORING_STREAM|Nur interne Verwendung.|  
|QUERY_OPTIMIZER_VD_MANAGER|Nur interne Verwendung.|  
|QUERY_OPTIMIZER_ID_MANAGER|Nur interne Verwendung.|  
|QUERY_OPTIMIZER_VIEW_REP|Nur interne Verwendung.|  
|RECOVERY_BAD_PAGE_TABLE|Nur interne Verwendung.|  
|RECOVERY_MANAGER|Nur interne Verwendung.|  
|SECURITY_OPERATION_RULE_TABLE|Nur interne Verwendung.|  
|SECURITY_OBJPERM_CACHE|Nur interne Verwendung.|  
|SECURITY_CRYPTO|Nur interne Verwendung.|  
|SECURITY_KEY_RING|Nur interne Verwendung.|  
|SECURITY_KEY_LIST|Nur interne Verwendung.|  
|SERVICE_BROKER_CONNECTION_RECEIVE|Nur interne Verwendung.|  
|SERVICE_BROKER_TRANSMISSION|Nur interne Verwendung.|  
|SERVICE_BROKER_TRANSMISSION_UPDATE|Nur interne Verwendung.|  
|SERVICE_BROKER_TRANSMISSION_STATE|Nur interne Verwendung.|  
|SERVICE_BROKER_TRANSMISSION_ERRORS|Nur interne Verwendung.|  
|SSBXmitWork|Nur interne Verwendung.|  
|SERVICE_BROKER_MESSAGE_TRANSMISSION|Nur interne Verwendung.|  
|SERVICE_BROKER_MAP_MANAGER|Nur interne Verwendung.|  
|SERVICE_BROKER_HOST_NAME|Nur interne Verwendung.|  
|SERVICE_BROKER_READ_CACHE|Nur interne Verwendung.|  
|SERVICE_BROKER_WAITFOR_MANAGER| Verwendet, um eine Ebene instanzzuordnung Waiter Warteschlangen zu synchronisieren. Pro Datenbank-ID, die Version der Datenbank und die Warteschlangen-ID-Tupel ist eine Warteschlange vorhanden. Konflikte bei Latches dieser Klasse kann auftreten, wenn viele Verbindungen sind: In einer WAITFOR(RECEIVE) warten Zustand Aufrufen von WAITFOR(RECEIVE); mehr als das Timeout WAITFOR; Empfangen einer Nachricht an; ein Commit oder Rollback der Transaktion, die die WAITFOR(RECEIVE) enthält; Sie können die Anzahl von Konflikten reduzieren, durch Verringern der Anzahl der Threads im Wartezustand WAITFOR(RECEIVE). |  
|SERVICE_BROKER_WAITFOR_TRANSACTION_DATA|Nur interne Verwendung.|  
|SERVICE_BROKER_TRANSMISSION_TRANSACTION_DATA|Nur interne Verwendung.|  
|SERVICE_BROKER_TRANSPORT|Nur interne Verwendung.|  
|SERVICE_BROKER_MIRROR_ROUTE|Nur interne Verwendung.|  
|TRACE_ID|Nur interne Verwendung.|  
|TRACE_AUDIT_ID|Nur interne Verwendung.|  
|TRACE|Nur interne Verwendung.|  
|TRACE_CONTROLLER|Nur interne Verwendung.|  
|TRACE_EVENT_QUEUE|Nur interne Verwendung.|  
|TRANSACTION_DISTRIBUTED_MARK|Nur interne Verwendung.|  
|TRANSACTION_OUTCOME|Nur interne Verwendung.|  
|NESTING_TRANSACTION_READONLY|Nur interne Verwendung.|  
|NESTING_TRANSACTION_FULL|Nur interne Verwendung.|  
|MSQL_TRANSACTION_MANAGER|Nur interne Verwendung.|  
|DATABASE_AUTONAME_MANAGER|Nur interne Verwendung.|  
|UTILITY_DYNAMIC_VECTOR|Nur interne Verwendung.|  
|UTILITY_SPARSE_BITMAP|Nur interne Verwendung.|  
|UTILITY_DATABASE_DROP|Nur interne Verwendung.|  
|UTILITY_DYNAMIC_MANAGER_VIEW|Nur interne Verwendung.|  
|UTILITY_DEBUG_FILESTREAM|Nur interne Verwendung.|  
|UTILITY_LOCK_INFORMATION|Nur interne Verwendung.|  
|VERSIONING_TRANSACTION|Nur interne Verwendung.|  
|VERSIONING_TRANSACTION_LIST|Nur interne Verwendung.|  
|VERSIONING_TRANSACTION_CHAIN|Nur interne Verwendung.|  
|VERSIONING_STATE|Nur interne Verwendung.|  
|VERSIONING_STATE_CHANGE|Nur interne Verwendung.|  
|KTM_VIRTUAL_CLOCK|Nur interne Verwendung.|  
  
## <a name="see-also"></a>Siehe auch  
 
 [DBCC SQLPERF &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-sqlperf-transact-sql.md)   
 
 [Dynamische Verwaltungssichten in Verbindung mit SQL Server-Betriebssystem &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sql-server-operating-system-related-dynamic-management-views-transact-sql.md)  
  
  


