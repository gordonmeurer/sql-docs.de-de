---
title: Target-Element (XMLA) | Microsoft Docs
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
apiname:
- Target Element
apilocation:
- http://schemas.microsoft.com/analysisservices/2003/engine
apitype: Schema
applies_to:
- SQL Server 2016 Preview
f1_keywords:
- microsoft.xml.analysis.target
- http://schemas.microsoft.com/analysisservices/2003/engine#Target
- urn:schemas-microsoft-com:xml-analysis#Target
helpviewer_keywords:
- Target element
ms.assetid: 9a69a777-5f34-4e94-b470-6bab2a98df8b
caps.latest.revision: 14
author: jeannt
ms.author: jeannt
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 6b9a30b4b16ee56479e594cf71c79e963e55ed77
ms.contentlocale: de-de
ms.lasthandoff: 09/01/2017

---
# <a name="target-element-xmla"></a>Target-Element (XMLA)
  Stellt die Zielpartition dar, die während der zusammengeführt werden eine [MergePartitions](../../../analysis-services/xmla/xml-elements-commands/mergepartitions-element-xmla.md) Befehl.  
  
## <a name="syntax"></a>Syntax  
  
```xml  
  
<MergePartitions>  
   <Target>  
      <DatabaseID>...</DatabaseID>  
      <CubeID>...</CubeID>  
      <MeasureGroupID>...</MeasureGroupID>  
      <PartitionID>...</PartitionID>  
   </Target>  
</MergePartitions>  
```  
  
## <a name="element-characteristics"></a>Elementmerkmale  
  
|Merkmal|Beschreibung|  
|--------------------|-----------------|  
|Datentyp und -länge|Keine|  
|Standardwert|Keine|  
|Kardinalität|1-n: Erforderliches Element, das mehr als einmal auftreten kann.|  
  
## <a name="element-relationships"></a>Elementbeziehungen  
  
|Beziehung|Element|  
|------------------|-------------|  
|Übergeordnete Elemente|[MergePartitions](../../../analysis-services/xmla/xml-elements-commands/mergepartitions-element-xmla.md)|  
|Untergeordnete Elemente|[CubeID](../../../analysis-services/xmla/xml-elements-properties/cubeid-element-xmla.md), [DatabaseID](../../../analysis-services/xmla/xml-elements-properties/databaseid-element-xmla.md), [MeasureGroupID](../../../analysis-services/xmla/xml-elements-properties/measuregroupid-element-xmla.md), [PartitionID](../../../analysis-services/xmla/xml-elements-properties/partitionid-element-xmla.md)|  
  
## <a name="remarks"></a>Hinweise  
 Die **Ziel** Element ist ein Objektverweis auf eine einzelne Partition, in dem die Inhalte der Quellpartitionen, gemäß, der [Quellen](../../../analysis-services/xmla/xml-elements-properties/sources-element-xmla.md) Element des übergeordneten Elements **MergePartitions** Element zusammengeführt werden sollen.  
  
## <a name="example"></a>Beispiel  
 Im folgenden Beispiel werden alle vier Partitionen der Internet Sales-Measuregruppe mit der `Internet_Sales_2004` -Zielpartition kombiniert. Das Beispiel verweist auf den [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)]-Cube der [!INCLUDE[ssSampleDBnormal](../../../includes/sssampledbnormal-md.md)]-Beispiel-[!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]-Datenbank.  
  
```  
<MergePartitions xmlns="http://schemas.microsoft.com/analysisservices/2003/engine">  
  <Sources>  
     <Source>  
        <DatabaseID>database</DatabaseID>  
        <CubeID>Adventure Works DW</CubeID>  
        <MeasureGroupID>Fact Internet Sales 1</MeasureGroupID>  
        <PartitionID>Internet_Sales_2001</PartitionID>  
     </Source>  
     <Source>  
      <DatabaseID>database</DatabaseID>  
      <CubeID>Adventure Works DW</CubeID>  
      <MeasureGroupID>Fact Internet Sales 1</MeasureGroupID>  
      <PartitionID>Internet_Sales_2002</PartitionID>  
    </Source>  
    <Source>  
      <DatabaseID>database</DatabaseID>  
      <CubeID>Adventure Works DW</CubeID>  
      <MeasureGroupID>Fact Internet Sales 1</MeasureGroupID>  
      <PartitionID>Internet_Sales_2003</PartitionID>  
    </Source>  
  </Sources>  
  <Target>    <DatabaseID>database</DatabaseID>    <CubeID>Adventure Works DW</CubeID>    <MeasureGroupID>Fact Internet Sales 1</MeasureGroupID>    <PartitionID>Internet_Sales_2004</PartitionID>  </Target>  
</MergePartitions>  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Source-Element &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/source-element-xmla.md)   
 [Datenbankeigenschaften &#40; XMLA &#41;](../../../analysis-services/xmla/xml-elements-properties/xml-elements-properties.md)  
  
  