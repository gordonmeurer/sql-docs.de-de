---
title: Platzhalterkomponenten und Inhaltsüberprüfung | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- wildcard components [XML]
- content validation [XML]
ms.assetid: ffa7d974-3645-446c-8425-f0b22b6b060a
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: dbb4ecd59362c016536aed6731d5418cbe88d616
ms.sourcegitcommit: 9c6a37175296144464ffea815f371c024fce7032
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/15/2018
ms.locfileid: "51674413"
---
# <a name="wildcard-components-and-content-validation"></a>Platzhalterkomponenten und Inhaltsüberprüfung
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Platzhalterkomponenten werden verwendet, um die Flexibilität der zulässigen Inhalte in einem Inhaltsmodell zu erhöhen. Diese Komponenten werden in der XSD-Sprache auf folgende Weise unterstützt:  
  
-   Elementplatzhalterkomponenten. Diese werden durch das **\<xsd:any>**-Element dargestellt.  
  
-   Attributplatzhalterkomponenten. Diese werden durch das **\<xsd:anyAttribute>**-Element dargestellt.  
  
 Beide Platzhalterzeichenelemente **\<xsd:any>** und **\<xsd: anyAttribute >** unterstützen die Verwendung eines **processContents** Attributs. Auf diese Weise können Sie einen Wert angeben, der angibt, wie XML-Anwendungen die Überprüfung des Dokumentinhalts durchführen, der diesen Platzhalterzeichenelementen zugeordnet ist. Die folgenden Werte und Auswirkungen werden bereitgestellt:  
  
-   Der **strict** -Wert gibt an, dass der Inhalt vollständig überprüft wird.  
  
-   Der **skip** -Wert gibt an, dass der Inhalt nicht überprüft wird.  
  
-   Der **lax** -Wert gibt an, dass nur Elemente und Attribute überprüft werden, für die Schemadefinitionen verfügbar sind.  
  
## <a name="lax-validation-and-xsanytype-elements"></a>Lax-Überprüfung und xs:anyType-Elemente  
 Die XML-Schemaspezifikation verwendet die **lax** -Überprüfung für Elemente des **anyType** -Datentyps. Da [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] die "lax"-Überprüfung nicht unterstützte, wurde die strict-Überprüfung für Elemente des **anyType**-Datentyps verwendet. Ab [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)]wird die lax-Überprüfung unterstützt. Inhalt der Elemente des Typs **anyType** wird mit lax-Überprüfung überprüft.  
  
 Das folgende Beispiel veranschaulicht die laxÜberprüfung. Das Schemaelement `e` weist den Typ **anyType** auf. Im Beispiel werden typisierte **xml** -Variablen erstellt und die **strict** -Überprüfung des Elements vom Typ anyType veranschaulicht.  
  
```  
CREATE XML SCHEMA COLLECTION SC AS '  
<schema xmlns="https://www.w3.org/2001/XMLSchema"   
        targetNamespace="https://ns">  
   <element name="e" type="anyType"/>  
   <element name="a" type="byte"/>  
   <element name="b" type="string"/>  
 </schema>'  
GO  
```  
  
 Das folgende Beispiel ist erfolgreich, weil die Überprüfung von `<e>` erfolgreich ist:  
  
```  
DECLARE @var XML(SC)  
SET @var = '<e xmlns="https://ns"><a>1</a><b>data</b></e>'  
GO  
```  
  
 Das folgende Beispiel ist erfolgreich. Die Instanz wird akzeptiert, obwohl kein `<c>` -Element im Schema definiert wird:  
  
```  
DECLARE @var XML(SC)  
SET @var = '<e xmlns="https://ns"><a>1</a><c>Wrong</c><b>data</b></e>'  
GO  
```  
  
 Die XML-Instanz im folgenden Beispiel wird abgelehnt, weil die Definition des `<a>` -Elements keinen Zeichenfolgenwert zulässt.  
  
```  
DECLARE @var XML(SC)  
SET @var = '<e xmlns="https://ns"><a>Wrong</a><b>data</b></e>'  
SELECT @var  
GO  
```  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Anforderungen und Einschränkungen für XML-Schemaauflistungen auf dem Server](../../relational-databases/xml/requirements-and-limitations-for-xml-schema-collections-on-the-server.md)  
  
  
