---
title: "C, um SQL: binäre | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- binary data type [ODBC]
- data conversions from C to SQL types [ODBC], binary
- binary data transfers [ODBC]
- converting data from c to SQL types [ODBC], binary
ms.assetid: 3e9083f3-357b-41aa-833c-2c8aac2226cd
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: e85e57206c6bf963e3b97039224d37f512961f86
ms.contentlocale: de-de
ms.lasthandoff: 09/09/2017

---
# <a name="c-to-sql-binary"></a>C, um SQL: binär
Der Bezeichner für die binäre ODBC C-Datentyp ist:  
  
 SQL_C_BINARY  
  
 In der folgenden Tabelle zeigt die ODBC-SQL-Datentypen, die in die C-Binärdaten konvertiert werden können. Eine Erläuterung der Begriffe in der Tabelle und Spalten, finden Sie unter [Daten von C-in SQL-Datentypen konvertieren](../../../odbc/reference/appendixes/converting-data-from-c-to-sql-data-types.md).  
  
|SQL-Typ-ID|Test|SQLSTATE|  
|-------------------------|----------|--------------|  
|SQL_CHAR<br /><br /> SQL_VARCHAR<br /><br /> SQL_LONGVARCHAR|Die Bytelänge der Daten < = Byte Spaltenlänge<br /><br /> Die Bytelänge der Daten > Byte Spaltenlänge|–<br /><br /> 22001|  
|SQL_WCHAR<br /><br /> SQL_WVARCHAR<br /><br /> SQL_WLONGVARCHAR|Zeichenlänge von Daten < = Spalte Zeichenlänge<br /><br /> Zeichenlänge von Daten > Spalte Zeichenlänge|–<br /><br /> 22001|  
|SQL_DECIMAL<br /><br /> SQL_NUMERIC<br /><br /> SQL_TINYINT<br /><br /> SQL_SMALLINT<br /><br /> SQL_INTEGER<br /><br /> SQL_BIGINT<br /><br /> SQL_REAL<br /><br /> SQL_FLOAT<br /><br /> SQL_DOUBLE<br /><br /> SQL_BIT SQL_TYPE_DATE<br /><br /> SQL_TYPE_TIME<br /><br /> SQL_TYPE_TIMESTAMP|Die Bytelänge der Daten = SQL-Länge<br /><br /> Die Bytelänge der Daten <> SQL Datenlänge|–<br /><br /> 22003|  
|SQL_BINARY<br /><br /> SQL_VARBINARY<br /><br /> SQL_LONGVARBINARY|Länge der Daten < = Spaltenlänge<br /><br /> Länge der Daten > Spaltenlänge|–<br /><br /> 22001|