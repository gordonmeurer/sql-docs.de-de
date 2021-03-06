---
title: Tools und Anwendungen, die in Analysis Services verwendete | Microsoft Docs
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: ''
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: e2ff1808739eff4aed9ad34bef5d512f7539b7a6
ms.sourcegitcommit: c12a7416d1996a3bcce3ebf4a3c9abe61b02fb9e
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 05/10/2018
ms.locfileid: "34041791"
---
# <a name="tools-and-applications-used-in-analysis-services"></a>In Analysis Services verwendete Tools und Anwendungen
[!INCLUDE[ssas-appliesto-sqlas-aas](../includes/ssas-appliesto-sqlas-aas.md)]

  Suchen die Tools und Anwendungen, die Sie zum Erstellen von Analysis Services-Modellen benötigen und Verwalten von Datenbanken bereitgestellt.  
  
## <a name="analysis-services-model-designers"></a>Analysis Services-Modell-Designer  
 Modelle werden mithilfe von Projektvorlagen in SQL Server Data Tools (SSDT), einer Visual Studio-Shell erstellt. Projektvorlagen enthalten die Modell-Designer zum Erstellen der Model-Objekte, die eine Analysis Services-Lösung bilden. SSDT ist ein kostenloser Webdownload monatlich aktualisiert.

 **[Herunterladen von SQL Server Data Tools (SSDT)](https://docs.microsoft.com/sql/ssdt/download-sql-server-data-tools-ssdt)** 
  
 Modelle verfügen über eine Einstellung des Kompatibilitätsgrades, der die Funktionsverfügbarkeit bestimmt und welches Release von Analysis Services das Modell ausführt.  Ob Sie angeben können, dass es sich bei ein bestimmten Kompatibilitätsgrad ist der Teil der Modell-Designer bestimmt.  
  
 Tabellarische Modelle, die die neueste Funktionen verwenden, z. B. BIM-Dateien im JSON-Tabellenformat und bidirektionales kreuzfilterrichtung, müssen erstellt oder mit dem Kompatibilitätsgrad 1200 oder höher aktualisiert werden.  
  
 Wenn Sie einen niedrigeren Kompatibilitätsgrad benötigen, vielleicht können weil ein Modell mit einer früheren Version von Analysis Services, bereitgestellt werden soll weiterhin im Modell-Designer in SSDT. Neuere Versionen des Tools wird das Erstellen von jedem Modelltyp (tabellarisch oder mehrdimensional) mit jedem Kompatibilitätsgrad unterstützt.   

## <a name="administrative-tools"></a>Verwaltungstools  
  
 SQL Server Management Studio (SSMS) ist das primäre Verwaltungstool für alle SQL Server-Funktionen, einschließlich Analysis Services. SSMS ist ein kostenloser Webdownload monatlich aktualisiert. 
  
**[Herunterladen von SQL Server Management Studio](../ssms/download-sql-server-management-studio-ssms.md)** 
  
 SSMS bietet erweiterte Ereignisse (xEvents), mit einem eine einfache Alternative zu SQL Server Profiler-ablaufverfolgungen zum Überwachen der Aktivität und Diagnostizieren von Problemen auf SQL Server 2016 und Azure Analysis Services-Server. Weitere Informationen finden Sie unter [Überwachen von Analysis Services mit den erweiterten Ereignissen von SQL Server](../analysis-services/instances/monitor-analysis-services-with-sql-server-extended-events.md) .  
  
### <a name="sql-server-profiler"></a>SQL Server Profiler  
 Auch wenn er zugunsten von xEvents offiziell als veraltet eingestuft ist, bietet SQL Server Profiler ein vertrautes Konzept zum Überwachen von Verbindungen, der MDX-Abfrageausführung und anderer Servervorgänge. SQL Server Profiler wird standardmäßig installiert. Sie können es mit SQL Server-Anwendungen für Apps in Windows finden.  
  
### <a name="powershell"></a>PowerShell  
 Mithilfe von PowerShell-Befehlen können Sie viele Verwaltungsaufgaben durchführen. Finden Sie unter [PowerShell-Referenz](../analysis-services/powershell/analysis-services-powershell-reference.md) für Weitere Informationen.  
  
### <a name="community-and-third-party-tools"></a>Community- und Drittanbietertools  
 Community-Codebeispiele finden Sie auf der [Analysis Services-Codeplex-Seite](http://sqlsrvanalysissrvcs.codeplex.com/) . [Foren](http://social.msdn.microsoft.com/Forums/sqlserver/home?forum=sqlanalysisservices) können hilfreich sein, wenn Sie Empfehlungen für Drittanbietertools suchen, die Analysis Services unterstützen.  
  
## <a name="see-also"></a>Siehe auch  
 [Kompatibilitätsgrad einer mehrdimensionalen Datenbank](../analysis-services/multidimensional-models/compatibility-level-of-a-multidimensional-database-analysis-services.md)   
 [Kompatibilitätsgrad für tabellarische Modelle](../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md)  
  
  
