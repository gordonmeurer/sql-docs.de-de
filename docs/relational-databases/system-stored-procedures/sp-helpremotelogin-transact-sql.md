---
title: Sp_helpremotelogin (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_helpremotelogin_TSQL
- sp_helpremotelogin
dev_langs:
- TSQL
helpviewer_keywords:
- sp_helpremotelogin
ms.assetid: 93f50869-2627-4642-899f-8f626f8833f4
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 1181ab030078b0f7ba61a72448991ed677e22d76
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/01/2018
ms.locfileid: "47704803"
---
# <a name="sphelpremotelogin-transact-sql"></a>sp_helpremotelogin (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Gibt Informationen zu Remoteanmeldenamen für einen bestimmten Remoteserver oder für alle Remoteserver zurück, die auf dem lokalen Server definiert sind.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepNextDontUse](../../includes/ssnotedepnextdontuse-md.md)] Verwenden Sie stattdessen Verbindungsserver und gespeicherte Prozeduren, die über Verbindungsserver ausgeführt werden.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
sp_helpremotelogin [ [ @remoteserver = ] 'remoteserver' ]   
     [ , [ @remotename = ] 'remote_name' ]  
```  
  
## <a name="arguments"></a>Argumente  
 [ @remoteserver **=** ] **"***Remoteserver***"**  
 Der Remoteserver, für den Informationen zu Remoteanmeldenamen zurückgegeben werden. *Remoteserver* ist **Sysname**, hat den Standardwert NULL. Wenn *Remoteserver* ist nicht angegeben ist, werden Informationen zu allen Remoteservern, auf dem lokalen Server definierten zurückgegeben.  
  
 [ @remotename **=** ] **"***Remote_name***"**  
 Ein bestimmter Remoteanmeldename auf dem Remoteserver. *remote_name* ist vom Datentyp **sysname**und hat den Standardwert NULL. Wenn *Remote_name* nicht angegeben ist, Informationen zu allen Remotebenutzern für definierten *Remoteserver* zurückgegeben wird.  
  
## <a name="return-code-values"></a>Rückgabecodewerte  
 0 (Erfolg) oder 1 (Fehler)  
  
## <a name="result-sets"></a>Resultsets  
  
|Spaltenname|Datentyp|Description|  
|-----------------|---------------|-----------------|  
|server|**sysname**|Name des Remoteservers, der auf dem lokalen Server definiert ist.|  
|local_user_name|**sysname**|Anmeldename auf dem lokalen Server, dem Remoteanmeldenamen vom Server zugeordnet werden.|  
|remote_user_name|**sysname**|Melden Sie sich auf dem Remoteserver, der Local_user_name zugeordnet wird.|  
|Optionen|**sysname**|Vertrauenswürdig = Der Remoteanmeldename muss beim Herstellen der Verbindung zum lokalen Server vom Remoteserver aus kein Kennwort angeben.<br /><br /> Nicht vertrauenswürdig (oder leer) = Der Remoteanmeldename wird beim Herstellen der Verbindung zum lokalen Server vom Remoteserver aus zur Eingabe eines Kennworts aufgefordert.|  
  
## <a name="remarks"></a>Hinweise  
 Verwenden Sie Sp_helpserver, um die Namen der auf dem lokalen Server definierten Remoteserver anzuzeigen.  
  
## <a name="permissions"></a>Berechtigungen  
 Es werden keine Berechtigungen geprüft.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-reporting-help-on-a-single-server"></a>A. Anzeigen der Hilfe zu einem einzelnen Server  
 Im folgenden Beispiel werden Informationen zu allen Remotebenutzern auf dem Remoteserver `Accounts` angezeigt.  
  
```  
EXEC sp_helpremotelogin 'Accounts';  
```  
  
### <a name="b-reporting-help-on-all-remote-users"></a>B. Anzeigen der Hilfe zu allen Remotebenutzern  
 Im folgenden Beispiel werden Informationen zu allen Remotebenutzern auf allen Remoteservern angezeigt, die dem lokalen Server bekannt sind.  
  
```  
EXEC sp_helpremotelogin;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Sp_addremotelogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-addremotelogin-transact-sql.md)   
 [sp_dropremotelogin &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dropremotelogin-transact-sql.md)   
 [sp_helpserver (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-helpserver-transact-sql.md)   
 [Sp_remoteoption &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-remoteoption-transact-sql.md)   
 [Gespeicherte Systemprozeduren &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
