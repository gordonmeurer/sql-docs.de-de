---
title: SMALLDATETIMEFROMPARTS (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SMALLDATETIMEFROMPARTS
- SMALLDATETIMEFROMPARTS_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- SMALLDATETIMEFROMPARTS function
ms.assetid: 7467fdab-e588-419c-9e29-42caec34a9ea
author: MashaMSFT
ms.author: mathoma
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7a07c71a03d396843c57c82a1e4944f82d976185
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/01/2018
ms.locfileid: "47681848"
---
# <a name="smalldatetimefromparts-transact-sql"></a>SMALLDATETIMEFROMPARTS (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-all-md](../../includes/tsql-appliesto-ss2012-all-md.md)]

  Gibt einen **smalldatetime**-Wert für das angegebene Datum und die Uhrzeit zurück.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
SMALLDATETIMEFROMPARTS ( year, month, day, hour, minute )  
```  
  
## <a name="arguments"></a>Argumente  
 *year*  
 Ganzzahliger Ausdruck, der ein Jahr angibt.  
  
 *month*  
 Ganzzahliger Ausdruck, der einen Monat angibt.  
  
 *day*  
 Ganzzahliger Ausdruck, der einen Tag angibt.  
  
 *hour*  
 Ganzzahliger Ausdruck, der die Stunden angibt.  
  
 *minute*  
 Ganzzahliger Ausdruck, der die Minuten angibt.  
  
## <a name="return-types"></a>Rückgabetypen  
 **smalldatetime**  
  
## <a name="remarks"></a>Remarks  
 Diese Funktion dient als Konstruktor für einen vollständig initialisierten **smalldatetime**-Wert. Wenn die Argumente nicht gültig sind, wird ein Fehler ausgegeben. Wenn erforderliche Argumente den Wert NULL haben, wird NULL zurückgegeben.  
  
 Diese Funktion kann remote auf [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)]-Servern oder höher ausgeführt werden. Eine Remoteausführung auf Servern mit einer Version vor [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] ist nicht möglich.  
  
## <a name="examples"></a>Beispiele  
  
```  
SELECT SMALLDATETIMEFROMPARTS ( 2010, 12, 31, 23, 59 ) AS Result  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
```  
Result  
---------------------------  
2011-01-01 00:00:00  
  
(1 row(s) affected)  
```  
  

