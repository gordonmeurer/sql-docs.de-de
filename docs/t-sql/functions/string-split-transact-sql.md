---
title: STRING_SPLIT (Transact-SQL) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 11/15/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- STRING_SPLIT
- STRING_SPLIT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- STRING_SPLIT function
ms.assetid: 3273dbf3-0b4f-41e1-b97e-b4f67ad370b9
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: daad1b738030efa48d5a85f91b70ebf747d4702c
ms.sourcegitcommit: 9ece10c2970a4f0812647149d3de2c6b75713e14
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/16/2018
ms.locfileid: "51812525"
---
# <a name="stringsplit-transact-sql"></a>STRING_SPLIT (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

> [!div class="nextstepaction"]
> [Unterstützen Sie uns bei der Verbesserung der Dokumentation für SQL Server.](https://80s3ignv.optimalworkshop.com/optimalsort/36yyw5kq-0)

Teilt den Zeichenausdruck mit einem angegebenen Trennzeichen.  
  
> [!NOTE]  
> Die **STRING_SPLIT**-Funktion steht nur für den Kompatibilitätsgrad 130 und höher zur Verfügung. Wenn der Datenbank-Kompatibilitätsgrad kleiner als 130 ist, wird [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] nicht in der Lage sein, die **STRING_SPLIT**-Funktion zu suchen und auszuführen. Unter [Anzeigen oder Ändern des Kompatibilitätsgrads einer Datenbank](../../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md) finden Sie Informationen zum Ändern des Datenbank-Kompatibilitätsgrads.
> Beachten Sie, dass der Kompatibilitätsgrad 120 auch in einer neuen [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] die Standardeinstellung sein kann.  
  
 ![Themenlinksymbol](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Transact-SQL Syntax Conventions (Transact-SQL-Syntaxkonventionen)](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Syntax  
  
```  
STRING_SPLIT ( string , separator )  
```  
  
## <a name="arguments"></a>Argumente  
 *Zeichenfolge*  
 Ist ein [Ausdruck](../../t-sql/language-elements/expressions-transact-sql.md) eines beliebigen Zeichentyps (z.B. **nvarchar**, **varchar**, **nchar** oder **char**).  
  
 *Trennzeichen*  
 Ein [Ausdruck](../../t-sql/language-elements/expressions-transact-sql.md) mit einem einzelnen Zeichen jedes beliebigen Zeichentyps (z.B. **nvarchar(1)**, **varchar(1)**, **nchar(1)** oder **char(1)**), der als Trennzeichen für verkettete Zeichenfolgen verwendet wird.  
  
## <a name="return-types"></a>Rückgabetypen  
 Gibt eine einspaltige Tabelle mit Fragmenten zurück. Der Name der Spalte ist **value**. Gibt **nvarchar** zurück, wenn eines der Eingabeargumente entweder **nvarchar** oder **nchar** ist, andernfalls wird **varchar** zurückgegeben. Die Länge des Rückgabetyps unterscheidet sich nicht von der Länge des Zeichenfolgenarguments.  
  
## <a name="remarks"></a>Remarks  
**STRING_SPLIT** akzeptiert eine Zeichenfolge, die getrennt werden soll, sowie das Trennzeichen, das zum Trennen von Zeichenfolgen verwendet wird. Gibt eine einspaltige Tabelle mit Teilzeichenfolgen zurück. Beispielsweise gibt die folgende Anweisung, `SELECT value FROM STRING_SPLIT('Lorem ipsum dolor sit amet.', ' ');`, die das Leerzeichen als Trennzeichen verwendet, die folgende Ergebnistabelle zurück:  
  
|Wert|  
|-----------|  
|Lorem|  
|ipsum|  
|dolor|  
|sit|  
|amet.|  
  
Wenn die Eingabezeichenfolge **NULL** ist, gibt die Tabellenwertfunktion **STRING_SPLIT** eine leere Tabelle zurück.  
  
Für **STRING_SPLIT** ist mindestens der Kompatibilitätsmodus 130 erforderlich.  
  
## <a name="examples"></a>Beispiele  
  
### <a name="a-split-comma-separated-value-string"></a>A. Teilen einer Zeichenfolge mit durch Trennzeichen getrennten Werten (CSV)  
Analysieren einer durch Komma getrennte Liste von Werten und Zurückgeben aller nicht leeren Token:  
  
```sql  
DECLARE @tags NVARCHAR(400) = 'clothing,road,,touring,bike'  
  
SELECT value  
FROM STRING_SPLIT(@tags, ',')  
WHERE RTRIM(value) <> '';  
```  
  
STRING_SPLIT gibt eine leere Zeichenfolge zurück, wenn zwischen dem Trennzeichen nichts vorhanden ist. Die Bedingung RTRIM(value) <> '' entfernt leere Token.  
  
### <a name="b-split-comma-separated-value-string-in-a-column"></a>B. Teilen einer Zeichenfolge mit durch Trennzeichen getrennten Werten in einer Spalte  
Die Produkttabelle verfügt über eine Spalte mit einer durch Komma getrennte Liste von Tags, wie in diesem Beispiel dargestellt wird:  
  
|ProductId|Name|Tags|  
|---------------|----------|----------|  
|1|Full-Finger Gloves|clothing,road,touring,bike|  
|2|LL Headset|bike|  
|3|HL Mountain Frame|bike,mountain|  
  
Die folgende Abfrage wandelt jede Tagliste um und verknüpft sie mit der ursprünglichen Zeile:  
  
```sql  
SELECT ProductId, Name, value  
FROM Product  
    CROSS APPLY STRING_SPLIT(Tags, ',');  
```  
  
 [!INCLUDE[ssResult](../../includes/ssresult-md.md)]  
  
|ProductId|Name|Wert|  
|---------------|----------|-----------|  
|1|Full-Finger Gloves|clothing|  
|1|Full-Finger Gloves|Straße|  
|1|Full-Finger Gloves|touring|  
|1|Full-Finger Gloves|bike|  
|2|LL Headset|bike|  
|3|HL Mountain Frame|bike|  
|3|HL Mountain Frame|mountain|  
  
### <a name="c-aggregation-by-values"></a>C. Aggregation nach Werten  
Benutzer müssen einen Bericht erstellen, der die Anzahl der Produkte pro Tag anzeigt, die nach der Anzahl der Produkte geordnet ist, und sie dürfen nur die Tags mit mehr als zwei Produkten filtern.  
  
```sql  
SELECT value as tag, COUNT(*) AS [Number of articles]  
FROM Product  
    CROSS APPLY STRING_SPLIT(Tags, ',')  
GROUP BY value  
HAVING COUNT(*) > 2  
ORDER BY COUNT(*) DESC;  
```  
  
### <a name="d-search-by-tag-value"></a>D. Nach Tagwert suchen  
Entwickler müssen Abfragen erstellen, die Artikel nach Schlüsselwörtern finden. Sie können folgende Abfragen verwenden:  
  
Um Produkte mit einem einzelnen Tag zu finden (clothing):  
  
```sql  
SELECT ProductId, Name, Tags  
FROM Product  
WHERE 'clothing' IN (SELECT value FROM STRING_SPLIT(Tags, ','));  
```  
  
Produkte mit zwei angegebenen Tags finden (clothing und road):  
  
```sql  
  
SELECT ProductId, Name, Tags  
FROM Product  
WHERE EXISTS (SELECT *  
    FROM STRING_SPLIT(Tags, ',')  
    WHERE value IN ('clothing', 'road');  
```  
  
### <a name="e-find-rows-by-list-of-values"></a>E. Suchen nach Zeilen nach einer Liste von Werten  
Entwickler müssen eine Abfrage erstellen, die Artikel nach einer Liste von IDs sucht. Sie können die folgende Abfrage verwenden:  
  
```sql  
SELECT ProductId, Name, Tags  
FROM Product  
JOIN STRING_SPLIT('1,2,3',',')   
    ON value = ProductId;  
```  
  
Dies ist ein Ersatz für häufige Antimuster, z.B. das Erstellen einer dynamischen SQL-Zeichenfolge in der Anwendungsschicht oder [!INCLUDE[tsql](../../includes/tsql-md.md)] oder mithilfe des LIKE-Operators:  
  
```sql  
SELECT ProductId, Name, Tags  
FROM Product  
WHERE ',1,2,3,' LIKE '%,' + CAST(ProductId AS VARCHAR(20)) + ',%';  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
[LEFT &#40;Transact-SQL&#41;](../../t-sql/functions/left-transact-sql.md)     
[LTRIM &#40;Transact-SQL&#41;](../../t-sql/functions/ltrim-transact-sql.md)     
[RIGHT &#40;Transact-SQL&#41;](../../t-sql/functions/right-transact-sql.md)    
[RTRIM &#40;Transact-SQL&#41;](../../t-sql/functions/rtrim-transact-sql.md)     
[SUBSTRING &#40;Transact-SQL&#41;](../../t-sql/functions/substring-transact-sql.md)     
[TRIM &#40;Transact-SQL&#41;](../../t-sql/functions/trim-transact-sql.md)     
[String Functions &#40;Transact-SQL&#41; (Zeichenfolgenfunktionen &#40;Transact-SQL&#41;)](../../t-sql/functions/string-functions-transact-sql.md)      
  
  
