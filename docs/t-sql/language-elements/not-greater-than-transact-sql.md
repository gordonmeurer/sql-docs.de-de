---
title: '!&gt; > (nicht größer als) (Transact-SQL) | Microsoft-Dokumentation'
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- Not Greater
- Greater
- '!>_TSQL'
- '!>'
- Not Greater Than
dev_langs:
- TSQL
helpviewer_keywords:
- '!> (not greater than)'
- not greater than operator (!>)
ms.assetid: 71a413ed-64f1-4ab9-9c52-c5959a77d00f
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 013c620609b5f8d3fc603df993eda1af377c1a26
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 10/01/2018
ms.locfileid: "47686786"
---
# <a name="gt-not-greater-than-transact-sql"></a>!&gt; > (nicht größer als) (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Vergleicht zwei Ausdrücke (ein Vergleichsoperator). Beim Vergleich von Ausdrücken, die ungleich NULL sind, ist das Ergebnis TRUE, wenn der linke Operand keinen höheren Wert als der rechte Operand besitzt; andernfalls ist das Ergebnis FALSE. Im Gegensatz zum Vergleichsoperator = (gleich) ist das Ergebnis des Vergleichs zweier NULL-Werte mit dem Operator !> nicht von der ANSI_NULLS-Einstellung abhängig.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
  
expression !> expression  
```  
  
## <a name="arguments"></a>Argumente  
 *expression*  
 Ein beliebiger gültiger [Ausdruck](../../t-sql/language-elements/expressions-transact-sql.md). Beide Ausdrücke müssen implizit konvertierbare Datentypen besitzen. Die Konvertierung hängt von den [Rangfolgeregeln für Datentypen](../../t-sql/data-types/data-type-precedence-transact-sql.md) ab.  
  
## <a name="result-types"></a>Ergebnistypen  
 **Boolean**  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Datentypen &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)   
 [Operatoren &#40;Transact-SQL&#41;](../../t-sql/language-elements/operators-transact-sql.md)  
  
  
