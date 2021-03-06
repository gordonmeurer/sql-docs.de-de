---
title: SQL Server-XTP Garbage Collection | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance-monitor
ms.topic: conceptual
ms.assetid: 64ae91e5-b420-44b4-af1a-f8bca83d7f41
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 3721cceb9ff66ec3d971ea35d2c49aaaf7dc6730
ms.sourcegitcommit: af1d9fc4a50baf3df60488b4c630ce68f7e75ed1
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2018
ms.locfileid: "51029735"
---
# <a name="sql-server-xtp-garbage-collection"></a>SQL Server-XTP Garbage Collection
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]

  Das SQL Server-XTP-Leistungsobjekt für die Garbage Collection enthält Leistungsindikatoren für die Garbage Collection der In-Memory-OLTP-Engine.  
  
 In dieser Tabelle werden die Leistungsindikatoren für die **SQL Server XTP Garbage Collection** beschrieben.  
  
|Leistungsindikator|und Beschreibung|  
|-------------|-----------------|  
|**Dusty-Corner-Scanwiederholungen/s (durch GC ausgegeben)**|Die durchschnittliche Anzahl von Scanwiederholungen aufgrund von Schreibkonflikten während Dusty-Corner-Sweep-Vorgängen, die pro Sekunde durch die Garbage Collection ausgegeben werden. Dieser Leistungsindikator befindet sich auf einer sehr niedrigen Ebene und dient nicht der Verwendung durch Kunden.|  
|**Arbeitselemente des GC-Hauptthreads/s**|Die Anzahl an Arbeitselementen, die vom GC-Hauptthread verarbeitet werden.|  
|**Parallele GC-Arbeitselemente/s**|Die Häufigkeit, mit der ein paralleler Thread ein GC-Arbeitselement ausgeführt hat.|  
|**Verarbeitete Zeilen/s**|Die durchschnittliche Anzahl von Zeilen, die pro Sekunde von der Garbage Collection verarbeitet werden.|  
|**Verarbeitete Zeilen/s (erste in Bucket und entfernt)**|Die durchschnittliche Anzahl der pro Sekunde von der Garbage Collection verarbeiteten Zeilen, die sich zuerst im entsprechenden Hashbucket befanden und sofort entfernt werden konnten.|  
|**Verarbeitete Zeilen/s (erste in Bucket)**|Die durchschnittliche Anzahl der pro Sekunde verarbeiteten Zeilen, die sich zuerst im entsprechenden Hashbucket befanden.|  
|**Verarbeitete Zeilen/s (zum Aufheben der Verknüpfung markiert)**|Die durchschnittliche Anzahl der pro Sekunde von der Garbage Collection verarbeiteten Zeilen, die bereits für das Aufheben der Verknüpfung markiert waren.|  
|**Verarbeitete Zeilen/s (kein Sweep erforderlich)**|Die durchschnittliche Anzahl der pro Sekunde von der Garbage Collection verarbeiteten Zeilen, für die kein Dusty-Corner-Sweep-Vorgang erforderlich ist.|  
|**Entfernte nach Sweep abgelaufene Zeilen/s**|Die durchschnittliche Anzahl der pro Sekunde abgelaufenen Zeilen, die bei Dusty-Corner-Sweep-Vorgängen entfernt werden.|  
|**Berührte nach Sweep abgelaufene Zeilen/s**|Die durchschnittliche Anzahl der abgelaufenen Zeilen, die pro Sekunde bei Dusty-Corner-Sweep-Vorgängen berührt werden.|  
|**Berührte nach Sweep ablaufende Zeilen/s**|Die durchschnittliche Anzahl ablaufender Zeilen, die pro Sekunde bei Dusty-Corner-Sweep-Vorgängen berührt werden.|  
|**Berührte Sweepzeilen/s**|Die durchschnittliche Anzahl der Zeilen, die pro Sekunde bei Dusty-Corner-Sweep-Vorgängen berührt werden.|  
|**Gestartete Sweep-Scans/s**|Die durchschnittliche Anzahl der pro Sekunde gestarteten Dusty-Corner-Sweep-Scans.|  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Leistungsindikatoren für SQL Server XTP &#40;In-Memory OLTP&#41;](../../relational-databases/performance-monitor/sql-server-xtp-in-memory-oltp-performance-counters.md)  
  
  
