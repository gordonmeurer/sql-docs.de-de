---
title: Sys.dm_os_buffer_pool_extension_configuration (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 09/08/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- dm_os_buffer_pool_extension_configuration
- sys.dm_os_buffer_pool_extension_configuration_TSQL
- dm_os_buffer_pool_extension_configuration_TSQL
- sys.dm_os_buffer_pool_extension_configuration
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_os_buffer_pool_extension_configuration dynamic management view
ms.assetid: d52cc481-4d29-4f33-b63d-231ec35d092f
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ef0eea139b491c565b8635daf69cefff61492688
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/01/2018
ms.locfileid: "47755838"
---
# <a name="sysdmosbufferpoolextensionconfiguration-transact-sql"></a>sys.dm_os_buffer_pool_extension_configuration (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

  Gibt die Konfigurationsinformationen zur Pufferpoolerweiterung in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]zurück. Gibt eine Zeile für jede Pufferpoolerweiterungsdatei zurück.  
  

  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|path|**Nvarchar**(256)|Pfad und Dateiname des Pufferpoolerweiterungscaches. NULL-Werte sind zulässig.|  
|file_id|**int**|ID der Pufferpoolerweiterungsdatei. Lässt keine NULL-Werte zu.|  
|state|**int**|Der Status der Pufferpoolerweiterungsfunktion. Lässt keine NULL-Werte zu.<br /><br /> 0 – Die Pufferpoolerweiterung ist deaktiviert<br /><br /> 1 – Die Pufferpoolerweiterung wird deaktiviert<br /><br /> 2 – wird für die zukünftige Verwendung reserviert.<br /><br /> 3 – Die Pufferpoolerweiterung wird aktiviert<br /><br /> 4 – Für die zukünftige Verwendung reserviert<br /><br /> 5 – Die Pufferpoolerweiterung ist aktiviert|  
|state_description|**Nvarchar**(60)|Beschreibt den Status der Pufferpoolerweiterungsfunktion. Lässt NULL-Werte zu.<br /><br /> 0 = BUFFER POOL EXTENSION DISABLED<br /><br /> 1 = BUFFER POOL EXTENSION ENABLED|  
|current_size_in_kb|**bigint**|Aktuelle Größe der Pufferpoolerweiterungsdatei. Lässt keine NULL-Werte zu.|  
  
## <a name="permissions"></a>Berechtigungen  
 Erfordert die VIEW SERVER STATE-Berechtigung auf dem Server.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-returning-configuration-buffer-pool-extension-information"></a>A. Gibt Konfigurationsinformationen zur Pufferpoolerweiterungsdatei zurück.  
 Im folgenden Beispiel werden alle Spalten aus der sys.dm_os_buffer_pool_extension_configruations-DMV zurückgegeben.  
  
```sql  
SELECT path, file_id, state, state_description, current_size_in_kb  
FROM sys.dm_os_buffer_pool_extension_configuration;  
```  
  
### <a name="b-returning-the-number-of-cached-pages-in-the-buffer-pool-extension-file"></a>B. Gibt die Anzahl der zwischengespeicherten Seiten in der Pufferpoolerweiterungsdatei zurück.  
 Im folgenden Beispiel wird die Anzahl der zwischengespeicherten Seiten in jeder Pufferpoolerweiterungsdatei zurückgegeben.  
  
```sql  
SELECT COUNT(*) AS cached_pages_count  
FROM sys.dm_os_buffer_descriptors  
WHERE is_in_bpool_extension <> 0  
;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Pufferpoolerweiterung](../../database-engine/configure-windows/buffer-pool-extension.md)   
 [sys.dm_os_buffer_descriptors &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-os-buffer-descriptors-transact-sql.md)  
  
  
