---
title: Konvertieren von URNs in SQL Server-Anbieterpfade | Microsoft-Dokumentation
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: c9b1b8f1-b117-4e87-9704-2170f62c5c8b
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e75581756f0464197e05b78083b7e90d7d3dfb3a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/02/2018
ms.locfileid: "48061290"
---
# <a name="convert-urns-to-sql-server-provider-paths"></a>Konvertieren von URNs in SQL Server-Anbieterpfade
  Das [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] Management Object-Modell (SMO-Modell) erstellt einheitliche Ressourcennamen (Uniform Resource Names, URN) für seine Objekte. Jeder URN identifiziert eindeutig ein SMO-Objekt, und in einen SQL Server PowerShell-anbieterpfad konvertiert werden kann, um mithilfe der `Convert-UrnToPath` Cmdlet.  
  
## <a name="converting-urns-to-paths"></a>Konvertieren von URNs in Pfade  
 Jeder URN weist die gleichen Informationen wie einen Pfad zum Objekt auf, aber in einer anderen Form. Dies ist beispielsweise der Pfad zu einer Tabelle:  
  
 SQLSERVER:\SQL\MyComputer\DEFAULT\Databases\AdventureWorks2012\Tables\Person.Address  
  
 Und dies ist die URN zum gleichen Objekt:  
  
 Server [@Name='MyComputer']\Database[@Name='AdventureWorks2012']\Table[@Name='Address' und @Schema='Person']  
  
 Wenn Sie ein SMO-Objekt in einem Powershellskript erstellt haben, können Sie verweisen die `Urn` Eigenschaft, um den URN für das Objekt abzurufen, und verwenden Sie dann die `Convert-UrnToPath` Cmdlet, um die SMO-URN-Zeichenfolge in eine Windows PowerShell-Pfad zu konvertieren. Sie können dann mithilfe des Anbieters zu anderen Positionen im Pfad navigieren.  
  
 Wenn Knotennamen erweiterte Zeichen enthalten, die in Windows PowerShell-Pfadnamen nicht unterstützt werden, codiert `Convert-UrnToPath` sie in ihrer hexadezimalen Darstellung. Zum Beispiel wird "Meine:Tabelle" als "Meine%3ATabelle" zurückgegeben.  
  
 Führen Sie Folgendes aus, um Beispiele für die Verwendung des Cmdlet in Windows PowerShell zu erhalten:  
  
```  
Get-Help Convert-UrnToPath -Examples  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Abfrageausdrücke und eindeutige Ressourcennamen](../powershell/query-expressions-and-uniform-resource-names.md)   
 [SQL Server PowerShell-Anbieter](../powershell/sql-server-powershell-provider.md)   
 [SQL Server-PowerShell](../powershell/sql-server-powershell.md)  
  
  
