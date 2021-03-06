---
title: Bezeichner in Anführungszeichen | Microsoft-Dokumentation
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL statements [ODBC], interoperability
- interoperability of SQL statements [ODBC], quoted identifiers
- quoted identifiers [ODBC]
ms.assetid: 729ba55f-743b-4a04-8c39-ac0a9914211d
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b0a81237eddd4836394cc9797a79690ba4b49a35
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/01/2018
ms.locfileid: "47769048"
---
# <a name="quoted-identifiers"></a>Bezeichner in Anführungszeichen
In einer SQL­Anweisung müssen in Bezeichnern, die Sonderzeichen oder Übereinstimmung Schlüsselwörter eingeschlossen werden *Anführungszeichen für Bezeichner*; Bezeichner eingeschlossen in solche Zeichen werden als bezeichnet *Anführungszeichen eingeschlossenen Bezeichnern*(auch bekannt als *aus voneinander getrennten Bezeichnern* in SQL-92). Beispielsweise wird der Accounts Payable Bezeichner in Anführungszeichen in der folgenden **wählen** Anweisung:  
  
```  
SELECT * FROM "Accounts Payable"  
```  
  
 Der Grund für Bezeichner ist, die Anweisung analysiert. Wenn Accounts Payable nicht in der vorherigen Anweisung in Anführungszeichen eingeschlossen ist, würde der Parser z. B. davon aus, dass zwei Tabellen, Konten und zu Zahlen wurden und zurückgeben, ein Syntaxfehler, die sie nicht durch ein Komma getrennt. Der Bezeichner, die Anführungszeichen ist treiberspezifisch und wird abgerufen, mit der Option SQL_IDENTIFIER_QUOTE_CHAR **SQLGetInfo**. Die Listen von Sonderzeichen und Schlüsselwörter werden abgerufen, mit dem SQL_SPECIAL_CHARACTERS und SQL_KEYWORDS in **SQLGetInfo**.  
  
 Merken Sie sich zitieren interoperable Anwendungen häufig alle Bezeichner, mit Ausnahme derjenigen für Pseudo-Spalten, z. B. die ROWID-Spalte in Oracle. **SQLSpecialColumns** gibt eine Liste der Pseudospalten zurück. Darüber hinaus treten anwendungsspezifischen Einschränkungen auf, in dem Sonderzeichen in Objektnamen angezeigt werden können, ist es am besten für interoperable Anwendungen nicht, für die Verwendung von Sonderzeichen in diese Positionen.
