---
title: dm_db_mirroring_auto_page_repair (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/15/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_db_mirroring_auto_page_repair_TSQL
- sys.dm_db_mirroring_auto_page_repair_TSQL
- sys.dm_db_mirroring_auto_page_repair
- dm_db_mirroring_auto_page_repair
dev_langs:
- TSQL
helpviewer_keywords:
- automatic page repair
- database mirroring [SQL Server], automatic page repair
- sys.dm_db_mirroring_auto_page_repair dynamic management view
ms.assetid: 49f0fc2a-e25e-47e1-a135-563adb509af1
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 976992cfe5d68659b95a62cc0b4e839f19f8cdd4
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/01/2018
ms.locfileid: "47638428"
---
# <a name="database-mirroring---sysdmdbmirroringautopagerepair"></a>Datenbankspiegelung – dm_db_mirroring_auto_page_repair
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt eine Zeile für jede automatische Seitenreparatur für jede gespiegelte Datenbank der Serverinstanz zurück. Diese Sicht enthält Zeilen für die letzte automatische Seitenreparatur einer bestimmten gespiegelten Datenbank. Pro Datenbank können maximal 100 Zeilen angezeigt werden. Sobald das Maximum in der Datenbank erreicht ist, ersetzt die Zeile bei der nächsten automatischen Seitenreparatur einen der bereits vorhandenen Einträge. In der folgenden Tabelle wird die Bedeutung der einzelnen Spalten definiert.  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|ID der Datenbank, der diese Zeile entspricht.|  
|**file_id**|**int**|ID der Datei, in der sich diese Seite befindet.|  
|**page_id**|**bigint**|ID der Seite in der Datei.|  
|**error_type**|**int**|Typ des Fehlers. Folgende Werte sind möglich:<br /><br /> **-** 1 = alle Hardwarefehler 823<br /><br /> 1 = 824 Fehler außer einer fehlerhaften Prüfsumme oder einer zerrissenen Seite (z. B. eine fehlerhafte Seiten-ID)<br /><br /> 2 = Fehlerhafte Prüfsumme<br /><br /> 3 = Zerrissene Seite|  
|**page_status**|**int**|Status einer Seitenreparatur:<br /><br /> 2 = In der Warteschlange für Partneranforderung.<br /><br /> 3 = Anforderung an Partner gesendet.<br /><br /> 4 = In der Warteschlange für automatische Seitenreparatur (Antwort von Partner empfangen).<br /><br /> 5 = Automatische Seitenreparatur erfolgreich ausgeführt. Die Seite sollte verwendbar sein.<br /><br /> 6 = Nicht zu reparieren. Dies weist darauf hin, dass bei der Seitenreparatur ein Fehler aufgetreten ist, weil beispielsweise die Partnerseite ebenfalls beschädigt ist, der Partner nicht verbunden ist oder ein Netzwerkproblem aufgetreten ist. Dieser Status ist nicht abschließend; wenn auf der Seite erneut eine Beschädigung festgestellt wird, wird sie nochmals vom Partner angefordert.|  
|**modification_time**|**datetime**|Zeitpunkt der letzten Seitenstatusänderung.|  
  
## <a name="security"></a>Security  
  
### <a name="permissions"></a>Berechtigungen  
 Erfordert die VIEW SERVER STATE-Berechtigung auf dem Server.  
  
## <a name="see-also"></a>Siehe auch  
 [Automatische Seitenreparatur (Verfügbarkeitsgruppen: Datenbankspiegelung)](../../sql-server/failover-clusters/automatic-page-repair-availability-groups-database-mirroring.md)   
 [Dynamische Verwaltungssichten und -funktionen &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Suspect_pages &#40;Transact-SQL&#41;](../../relational-databases/system-tables/suspect-pages-transact-sql.md)   
 [Verwalten der suspect_pages-Tabelle &#40;SQL Server&#41;](../../relational-databases/backup-restore/manage-the-suspect-pages-table-sql-server.md)  
  
  


