---
title: "Anzeigen oder Ändern der Standardspeicherorte für Daten- und Protokolldateien (SQL Server Management Studio) | Microsoft-Dokumentation"
ms.custom: 
ms.date: 06/13/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- log files [SQL Server], changing default location
- data files [SQL Server], changing default location
ms.assetid: 70a57fda-fcfe-490f-9cf6-5df620e32b2a
caps.latest.revision: 16
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 1419847dd47435cef775a2c55c0578ff4406cddc
ms.openlocfilehash: 7e206ce6bf55a2180d19878797f79502ced3a3d4
ms.contentlocale: de-de
ms.lasthandoff: 08/02/2017

---
# <a name="view-or-change-the-default-locations-for-data-and-log-files"></a>Anzeigen oder Ändern der Standardspeicherorte für Datenbankdateien
  
 Als bewährte Methode zum Schutz der Datendateien und Protokolldateien sollten Sie sicherstellen, dass diese durch Zugriffssteuerungslisten (ACLs) geschützt sind. Einrichten der ACLs für den Verzeichnisstamm, unter dem die Dateien erstellt werden.  
 
  
## <a name="view-or-change-the-default-locations-for-database-files"></a>Anzeigen oder Ändern der Standardspeicherorte für Datenbankdateien  
  
1.  Klicken Sie im Objekt-Explorer mit der rechten Maustaste auf Ihren Server, und klicken Sie auf **Eigenschaften**.  
  
2.  Klicken Sie im linken Bedienfeld auf der betreffenden Eigenschaftenseite auf die Registerkarte **Datenbankeinstellungen** .  
  
3.  Im Bereich **Standardspeicherorte für Datenbank**können Sie die aktuellen Standardspeicherorte für neue Datendateien und neue Protokolldateien anzeigen. Um einen Standardspeicherort zu ändern, geben Sie einen neuen Standardpfadnamen in das Feld **Daten** oder **Protokoll** ein, oder klicken Sie auf die Schaltfläche zum Durchsuchen, um einen Pfadnamen zu suchen und auszuwählen.  
  
>**HINWEIS:** Nach dem Ändern der Standardspeicherorte müssen Sie den SQL Server-Dienst beenden und wieder starten, um die Änderung abzuschließen.  
  
## <a name="see-also"></a>Siehe auch  
 [CREATE DATABASE &#40;SQL Server Transact-SQL&#41;](../../t-sql/statements/create-database-sql-server-transact-sql.md)   
 [Erstellen einer Datenbank](../../relational-databases/databases/create-a-database.md)  
  
  
