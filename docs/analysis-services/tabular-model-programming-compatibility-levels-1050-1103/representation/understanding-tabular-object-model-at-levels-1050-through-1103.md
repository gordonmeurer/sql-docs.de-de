---
title: Grundlegendes zum tabellarischen Objektmodell auf Ebenen 1050 bis 1103 | Microsoft-Dokumentation
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 16808ae1ceccd64a109a78c33d861ab45076b98d
ms.sourcegitcommit: 7fe14c61083684dc576d88377e32e2fc315b7107
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/26/2018
ms.locfileid: "50146415"
---
# <a name="understanding-tabular-object-model-at-levels-1050-through-1103"></a>Grundlegendes zum tabellarischen Objektmodell auf Ebenen 1050 bis 1103
[!INCLUDE[ssas-appliesto-sqlas](../../../includes/ssas-appliesto-sqlas.md)]

  Ein tabellarisches Modell ist eine logische Darstellung von Tabellen, Beziehungen, Hierarchien, Perspektiven, Measures und der Schlüsselleistung. In diesem Abschnitt wird die interne Implementierung mithilfe von AMO eingeführt. Finden Sie unter [Entwickeln mit Analysis Management Objects &#40;AMO&#41; ](https://docs.microsoft.com/bi-reference/amo/developing-with-analysis-management-objects-amo) , wenn Sie AMO bisher nicht verwendet haben.  
  
 Es wird ein Top-Down-Ansatz verwendet. Alle relevanten Objekte im tabellarischen Modell werden den AMO-Objekten logisch zugeordnet, und die erforderliche Interaktion oder der erforderliche Workflow werden erläutert. Ein Quellcodebeispiel, das Erstellen eines tabellarischen Modells mit AMO, AMO2TABULAR, zum Beispiel ist unter Codeplex verfügbar. Ein wichtiger Hinweis zum Code im Beispiel: Dieser wird nur zur Verdeutlichung der hier erläuterten logischen Konzepte bereitgestellt und sollte nicht in einer Produktionsumgebung verwendet werden. Das Beispiel wird ohne Support oder Garantie bereitgestellt.  
  
## <a name="database-representation"></a>Datenbankdarstellung  
 Eine Datenbank stellt das Containerobjekt für das tabellarische Modell bereit. Alle Objekte in einem tabellarischen Modell sind in der Datenbank enthalten. Im Hinblick auf AMO-Objekte verfügt eine Datenbankdarstellung über eine 1:1-Zuordnungsbeziehung zu `xref:Microsoft.AnalysisServices.Database`, und es sind keine weiteren AMO-Hauptobjekte erforderlich. Beachten Sie, dass dies nicht bedeutet, dass beim Erstellen von Modellen alle im AMO-Datenbankobjekt enthaltenen Objekte verwendet werden können.  
  
 Finden Sie unter [Datenbankdarstellung&#40;tabellarische&#41; ](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/representation/database-representation-tabular.md) eine ausführliche Erläuterung zum Erstellen und Bearbeiten der datenbankdarstellung.  
  
## <a name="connection-representation"></a>Verbindungsdarstellung  
 Durch eine Verbindung wird die Beziehung zwischen den Daten, die in eine Projektmappe für tabellarische Modelle aufgenommen werden sollen, und dem Modell selbst hergestellt. Im Hinblick auf AMO-Objekte verfügt eine Verbindung über eine 1:1-Zuordnungsbeziehung zu `xref:Microsoft.AnalysisServices.DataSource`, und es sind keine weiteren AMO-Hauptobjekte erforderlich. Beachten Sie, dass dies nicht bedeutet, dass beim Erstellen von Modellen alle im AMO-Datenquellenobjekt enthaltenen Objekte verwendet werden können.  
  
 Finden Sie unter [Verbindungsdarstellung &#40;tabellarische&#41; ](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/representation/connection-representation-tabular.md) für eine ausführliche Erläuterung zum Erstellen und Bearbeiten der datenquellendarstellung.  
  
## <a name="table-representation"></a>Tabellendarstellung  
 Tabellen sind Datenbankobjekte, die die Daten in der Datenbank enthalten. Im Hinblick auf AMO-Objekte hat eine Tabelle eine 1:n-Zuordnungsbeziehung. Eine Tabelle wird durch die Verwendung der folgenden AMO-Objekte dargestellt: `xref:Microsoft.AnalysisServices.DataSourceView`, `xref:Microsoft.AnalysisServices.Dimension`, `xref:Microsoft.AnalysisServices.Cube`, `xref:Microsoft.AnalysisServices.CubeDimension`, `xref:Microsoft.AnalysisServices.MeasureGroup` und `xref:Microsoft.AnalysisServices.Partition` sind die erforderlichen Hauptobjekte. Allerdings ist es wichtig zu beachten, dass dies nicht bedeutet, dass alle in den zuvor erwähnten AMO-Objekten enthaltenen Objekte verwendet werden können, bei der Modellierung.  
  
 Finden Sie unter [Tabellendarstellung &#40;tabellarische&#41; ](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/representation/tables-representation-tabular.md) eine ausführliche Erläuterung zum Erstellen und Bearbeiten der tabellendarstellung.  
  
### <a name="calculated-column-representation"></a>Darstellung einer berechneten Spalte  
 Berechnete Spalten sind ausgewertete Ausdrücke, die eine Spalte in einer Tabelle generieren, wo ein neuer Wert berechnet wird und für jede Zeile in der Tabelle gespeichert wird. Im Hinblick auf AMO-Objekte verfügt eine berechnete Spalte eine 1: n zuordnungsbeziehung. Eine berechnete Spalte wird durch die Verwendung der folgenden AMO-Objekte dargestellt: `xref:Microsoft.AnalysisServices.Dimension` und `xref:Microsoft.AnalysisServices.MeasureGroup` sind die erforderlichen Hauptobjekte. Beachten Sie, dass dies nicht bedeutet, dass beim Modellieren alle in den zuvor erwähnten AMO-Objekten enthaltenen Objekte verwendet werden können.  
  
 Finden Sie unter [Darstellung einer berechneten Spalte &#40;tabellarische&#41; ](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/representation/tables-calculated-column-representation.md) für eine ausführliche Erläuterung zum Erstellen und bearbeiten die Darstellung einer berechneten Spalte.  
  
### <a name="calculated-measure-representation"></a>Darstellung eines berechneten Measures  
 Berechnete Measures sind gespeicherte Ausdrücke, die auf Anfrage ausgewertet werden, sobald das Modell bereitgestellt wird. Im Hinblick auf AMO-Objekte verfügt ein berechnetes Measure über eine 1:n-Zuordnungsbeziehung. Eine berechnete Spalte wird durch die Verwendung der folgenden AMO-Objekte dargestellt: `xref:Microsoft.AnalysisServices.MdxScript.Commands%2A` und `xref:Microsoft.AnalysisServices.MdxScript.CalculationProperties%2A` sind die erforderlichen Hauptobjekte. Beachten Sie, dass dies nicht bedeutet, dass beim Modellieren alle in den zuvor erwähnten AMO-Objekten enthaltenen Objekte verwendet werden können.  
  
> [!NOTE]  
>  Die `xref:Microsoft.AnalysisServices.Measure`-Objekte weisen keine Beziehung zu den berechneten Measures in tabellarischen Modellen auf und werden in tabellarischen Modellen nicht unterstützt.  
  
 Finden Sie unter [Darstellung eines berechneten Measures &#40;tabellarische&#41; ](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/representation/tables-calculated-measure-representation.md) eine ausführliche Erläuterung dazu, wie die Darstellung eines berechneten Measures zu erstellen.  
  
### <a name="hierarchy-representation"></a>Hierarchiedarstellung  
 Hierarchien sind ein Mechanismus, dem Endbenutzer umfangreichere Drillup- und Drilldownfunktionen bereitzustellen. Im Hinblick auf AMO-Objekte verfügt eine Hierarchiedarstellung über eine 1:1-Zuordnungsbeziehung zu `xref:Microsoft.AnalysisServices.Hierarchy`, und es sind keine weiteren AMO-Hauptobjekte erforderlich. Beachten Sie, dass dies nicht bedeutet, dass beim Erstellen tabellarischer Modelle alle im AMO-Datenbankobjekt enthaltenen Objekte verwendet werden können.  
  
 Finden Sie unter [Hierarchiedarstellung &#40;tabellarische&#41; ](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/representation/tables-hierarchy-representation.md) eine ausführliche Erläuterung zum Erstellen und Bearbeiten der hierarchiedarstellung.  
  
### <a name="key-performance-indicator-kpi--representation"></a>Key Performance Indicator (KPI)-Darstellung  
 Ein KPI misst die Leistung eines Werts, der durch ein Basismeasure definiert wird, anhand eines Zielwerts. Im Hinblick auf AMO-Objekte verfügt eine KPI-Darstellung über eine 1:n-Zuordnungsbeziehung. Ein KPI wird durch die Verwendung der folgenden AMO-Objekte dargestellt: `xref:Microsoft.AnalysisServices.MdxScript.Commands%2A` und `xref:Microsoft.AnalysisServices.MdxScript.CalculationProperties%2A` sind die erforderlichen Hauptobjekte.  Beachten Sie, dass dies nicht bedeutet, dass beim Modellieren alle in den zuvor erwähnten AMO-Objekten enthaltenen Objekte verwendet werden können.  
  
> [!NOTE]  
>  Ein weiterer wichtiger Unterschied besteht darin, dass die `xref:Microsoft.AnalysisServices.Kpi`-Objekte keine Beziehung zu den KPIs in tabellarischen Modellen aufweisen. Außerdem werden sie in tabellarischen Modellen nicht unterstützt.  
  
 Finden Sie unter [Key Performance Indicator-Darstellung &#40;tabellarische&#41; ](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/representation/tables-key-performance-indicator-representation.md) für eine ausführliche Erläuterung zum Erstellen und Bearbeiten der KPI-Darstellung.  
  
### <a name="partition-representation"></a>Partitionsdarstellung  
 Zu eine Tabelle unterteilt werden kann, in verschiedene Teilmengen von Zeilen, die, wenn die Tabelle kombiniert. Jede dieser Teilmengen ist eine Partition der Tabelle. Im Hinblick auf AMO-Objekte verfügt eine Partitionsdarstellung über eine 1:1-Zuordnungsbeziehung zu `xref:Microsoft.AnalysisServices.Partition`, und es sind keine weiteren AMO-Hauptobjekte erforderlich. Beachten Sie, dass dies nicht bedeutet, dass beim Erstellen von Modellen alle im AMO-Datenbankobjekt enthaltenen Objekte verwendet werden können.  
  
 Finden Sie unter [Partitionsdarstellung &#40;tabellarische&#41; ](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/representation/tables-partition-representation.md) eine ausführliche Erläuterung zum Erstellen und Bearbeiten der partitionsdarstellung.  
  
## <a name="relationship-representation"></a>Beziehungsdarstellung  
 Eine Beziehung ist eine Verbindung zwischen zwei Tabellen mit Daten. Die Beziehung legt fest, wie die Daten in den beiden Tabellen korreliert werden sollen.  
  
 In tabellarischen Modellen können mehrere Beziehungen zwischen zwei Tabellen definiert werden. Wenn mehrere Beziehungen zwischen zwei Tabellen definiert werden, kann nur eine als aktive Standardbeziehung definiert werden. Alle anderen Beziehungen sind inaktiv.  
  
 Im Hinblick auf AMO-Objekte verfügen alle inaktiven Beziehungen über eine Darstellung einer 1:1-Zuordnungsbeziehung zu `xref:Microsoft.AnalysisServices.Relationship`, und es sind keine weiteren AMO-Hauptobjekte erforderlich. Für die aktive Beziehung gelten andere Anforderungen, und es ist zusätzlich eine Zuordnung zu `xref:Microsoft.AnalysisServices.ReferenceMeasureGroupDimension` erforderlich. Beachten Sie, dass dies nicht bedeutet, dass beim Modellieren alle in der AMO-Beziehung oder dem referenceMeasureGroupDimension-Objekt enthaltenen Objekte verwendet werden können.  
  
 Finden Sie unter [Beziehungsdarstellung &#40;tabellarische&#41; ](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/representation/relationship-representation-tabular.md) eine ausführliche Erläuterung zum Erstellen und Bearbeiten der beziehungsdarstellung.  
  
## <a name="perspective-representation"></a>Perspektivendarstellung  
 Eine Perspektive ist ein Mechanismus, um den Modus zu vereinfachen oder zu fokussieren. Im Hinblick auf AMO-Objekte verfügt eine Beziehungsdarstellung über eine 1:1-Zuordnungsbeziehung zu `xref:Microsoft.AnalysisServices.Perspective`, und es sind keine weiteren AMO-Hauptobjekte erforderlich. Es ist wichtig zu beachten, dass dies nicht bedeutet, dass alle im AMO-Perspective-Objekt enthaltenen Objekte verwendet werden können, bei der tabellarischen Modellierung.  
  
 Finden Sie unter [Perspektivendarstellung &#40;tabellarische&#41; ](../../../analysis-services/tabular-model-programming-compatibility-levels-1050-1103/representation/perspective-representation-tabular.md) eine ausführliche Erläuterung zum Erstellen und Bearbeiten der perspektivendarstellung.  
  
> [!WARNING]  
>  Perspektiven sind kein Sicherheitsmechanismus; auf Objekte außerhalb der Perspektive kann immer noch vom Benutzer über andere Schnittstellen zugegriffen werden.  
  
  
