---
title: srv_paramdata (API für erweiterte gespeicherte Prozeduren) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: stored-procedures
ms.topic: reference
apiname:
- srv_paramdata
apilocation:
- opends60.dll
apitype: DLLExport
dev_langs:
- C++
helpviewer_keywords:
- srv_paramdata
ms.assetid: 3104514d-b404-47c9-b6d7-928106384874
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 8740e97d1c12cc0fc9198048ea58c12e01e6771c
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/15/2018
ms.locfileid: "51666799"
---
# <a name="srvparamdata-extended-stored-procedure-api"></a>srv_paramdata (API für erweiterte gespeicherte Prozeduren)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Verwenden Sie stattdessen die CLR-Integration.  
  
 Gibt den Wert eines Aufrufparameters für eine remote gespeicherte Prozedur zurück. Diese Funktion wurde durch die **srv_paraminfo**-Funktion ersetzt.  
  
## <a name="syntax"></a>Syntax  
  
```  
  
void * srv_paramdata (  
SRV_PROC *  
srvproc  
,  
int  
n   
);  
```  
  
## <a name="arguments"></a>Argumente  
 *srvproc *  
 Ist ein Zeiger auf die SRV_PROC-Struktur, die das Handle für eine bestimmte Clientverbindung ist (in diesem Fall das Handle, das den Aufruf der remote gespeicherten Prozedur erhalten hat). Die Struktur enthält Informationen, mit der die Bibliothek für erweiterte gespeicherte Prozeduren die Daten und Kommunikation zwischen der Anwendung und dem Client verwaltet.  
  
 *n*  
 Entspricht der Nummer des Parameters. Die erste Parameternummer ist 1.  
  
## <a name="returns"></a>Rückgabewert  
 Ein Zeiger auf den Parameterwert. Ist der *n*-te Parameter NULL, ist kein *n*-ter Parameter vorhanden, oder ist keine remote gespeicherte Prozedur vorhanden, wird NULL zurückgegeben. Wenn der Parameterwert eine Zeichenfolge ist, kann er nicht NULL-terminiert sein. Verwenden Sie **srv_paramlen**, um die Länge der Zeichenfolge zu bestimmen.  
  
 Diese Funktion gibt die folgenden Werte zurück, wenn der Parameter einem der Datentypen von [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] entspricht. Zeigerdaten umfassen, ob der Zeiger für den Datentyp gültig (VP), NULL oder nicht anwendbar (N/V) ist, sowie den Inhalt der Daten, auf die der Zeiger verweist.  
  
|Neue Datentypen|Länge der Eingabedaten|  
|--------------------|-----------------------|  
|BITN|**NULL**: VP, NULL<br /><br /> **ZERO**: VP, NULL<br /><br /> **>=255:** NICHT ZUTREFFEND<br /><br /> **<255:** NICHT ZUTREFFEND|  
|BIGVARCHAR|**NULL**: NULL, NICHT ZUTREFFEND<br /><br /> **ZERO**: VP, NULL<br /><br /> **>=255:** VP, 255 Zeichen<br /><br /> **<255:** VP, tatsächliche Daten|  
|BIGCHAR|**NULL**: NULL, NICHT ZUTREFFEND<br /><br /> **ZERO:** VP, 255 Leerräume<br /><br /> **>=255:** VP, 255 Zeichen<br /><br /> **<255:** VP, tatsächliche Daten und Auffüllung (bis 255)|  
|BIGBINARY|**NULL**: NULL, NICHT ZUTREFFEND<br /><br /> **ZERO:** VP, 255 0x00<br /><br /> **>=255:** VP, 255 Byte<br /><br /> **<255:** VP, tatsächliche Daten und Auffüllung (bis 255)|  
|BIGVARBINARY|**NULL**: NULL, NICHT ZUTREFFEND<br /><br /> **ZERO**: VP, 0x00<br /><br /> **>=255:** VP, 255 Byte<br /><br /> **<255:** VP, tatsächliche Daten|  
|NCHAR|**NULL**: NULL, NICHT ZUTREFFEND<br /><br /> **ZERO:** VP, 255 Leerräume<br /><br /> **>=255:** VP, 255 Zeichen<br /><br /> **<255:** VP, tatsächliche Daten und Auffüllung (bis 255)|  
|NVARCHAR|**NULL**: NULL, NICHT ZUTREFFEND<br /><br /> **ZERO**: VP, NULL<br /><br /> **>=255:** VP, 255 Zeichen<br /><br /> **<255:** VP, tatsächliche Daten|  
|NTEXT|**NULL**: NICHT ZUTREFFEND<br /><br /> **ZERO**: NICHT ZUTREFFEND<br /><br /> **>=255:** NICHT ZUTREFFEND<br /><br /> **\<255:** NICHT ZUTREFFEND|  
  
 \* Daten enden nicht auf NULL. Es wird keine Warnung für abgeschnittene Daten, die größer als 255 Zeichen sind, ausgegeben.  
  
## <a name="remarks"></a>Remarks  
 Wenn Sie den Parameternamen wissen, können Sie **srv_paramnumber** verwenden, um die Parameternummer abzurufen. Verwenden Sie **srv_paramlen**, um zu bestimmen, ob ein Parameter NULL ist.  
  
 Wenn eine remote gespeicherte Prozedur mit Parametern aufgerufen wird, werden die Parameter mit ihrem Namen oder mit ihrer Position übergeben (unbenannt). Werden beim Aufruf einer remote gespeicherten Prozedur einige Parameter über ihren Namen und andere über ihre Position übergeben, so tritt ein Fehler auf. Bei Auftreten eines Fehlers wird der SRV_RPC-Handler trotzdem aufgerufen, doch es sind scheinbar keine Parameter vorhanden und **srv_rpcparams** gibt 0 zurück.  
  
> [!IMPORTANT]  
>  Sie sollten den Quellcode der erweiterten gespeicherten Prozeduren sorgfältig prüfen, und Sie sollten die kompilierten DLL-Dateien testen, bevor Sie sie auf einem Produktionsserver installieren. Weitere Informationen zum Überprüfen und Testen der Sicherheit finden Sie auf dieser [Microsoft-Website](https://go.microsoft.com/fwlink/?LinkID=54761&amp;clcid=0x409https://msdn.microsoft.com/security/).  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [srv_rpcparams (API für erweiterte gespeicherte Prozeduren)](../../relational-databases/extended-stored-procedures-reference/srv-rpcparams-extended-stored-procedure-api.md)  
  
  
