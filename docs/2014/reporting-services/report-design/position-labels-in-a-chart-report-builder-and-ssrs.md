---
title: Positionieren von Bezeichnungen in einem Diagramm (Berichts-Generator und SSRS) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 5db74e0b-8be8-4b47-b386-faab56dffa9b
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: 77a4a9b2749eefbe43cac04351fd1d2bd2c9300e
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/02/2018
ms.locfileid: "48138737"
---
# <a name="position-labels-in-a-chart-report-builder-and-ssrs"></a>Positionieren von Bezeichnungen in einem Diagramm (Berichts-Generator und SSRS)
  Da jeder Diagrammtyp über eine andere Form verfügt, werden Datenpunktbezeichnungen so platziert, dass sie sich im Diagramm nicht überlappen. Die Standardposition der Bezeichnungen ist vom Diagrammtyp abhängig:  
  
-   Bei gestapelten Diagrammen können Bezeichnungen nur innerhalb der Reihe positioniert werden.  
  
-   Bei Trichter- und Pyramidendiagrammen werden Bezeichnungen an der Außenseite in einer Spalte eingefügt.  
  
-   Bei Kreisdiagrammen werden Bezeichnungen innerhalb der einzelnen Kreissegmente platziert.  
  
-   Bei Balkendiagrammen werden Bezeichnungen außerhalb der Balken platziert, die Datenpunkte darstellen.  
  
-   Bei Polardiagrammen werden Bezeichnungen außerhalb der Kreisbereiche platziert, die Datenpunkte darstellen.  
  
> [!NOTE]  
>  [!INCLUDE[ssRBRDDup](../../includes/ssrbrddup-md.md)]  
  
### <a name="to-change-the-position-of-point-labels-in-a-pie-chart"></a>So ändern Sie die Position von Punktbezeichnungen in einem Kreisdiagramm  
  
1.  Erstellen Sie ein Kreisdiagramm.  
  
2.  Klicken Sie auf der Entwurfsoberfläche mit der rechten Maustaste auf das Diagramm, und wählen Sie **Datenbezeichnungen anzeigen**aus.  
  
3.  Öffnen Sie den Bereich Eigenschaften. Klicken Sie auf der Registerkarte **Ansicht** auf **Eigenschaften**.  
  
4.  Klicken Sie auf der Entwurfsoberfläche auf das Diagramm. Die Eigenschaften für das Diagramm werden im Bereich "Eigenschaften" angezeigt.  
  
5.  Erweitern Sie im Abschnitt **Allgemein** den Knoten **CustomAttributes** . Eine Liste der Attribute für das Kreisdiagramm wird angezeigt.  
  
6.  Wählen Sie einen Wert für die Eigenschaft PieLabelStyle aus.  
  
### <a name="to-change-the-position-of-point-labels-in-a-funnel-or-pyramid-chart"></a>So ändern Sie die Position von Punktbezeichnungen in einem Trichter- oder Pyramidendiagramm  
  
1.  Erstellen Sie ein Trichter- oder ein Pyramidendiagramm.  
  
2.  Klicken Sie auf der Entwurfsoberfläche mit der rechten Maustaste auf das Diagramm, und wählen Sie **Datenbezeichnungen anzeigen**aus.  
  
3.  Öffnen Sie den Bereich Eigenschaften. Klicken Sie auf der Registerkarte **Ansicht** auf **Eigenschaften**.  
  
4.  Klicken Sie auf der Entwurfsoberfläche auf das Diagramm. Die Eigenschaften für das Diagramm werden im Bereich "Eigenschaften" angezeigt.  
  
5.  Erweitern Sie im Abschnitt **Allgemein** den Knoten **CustomAttributes** . Eine Liste der Attribute für das Trichterdiagramm wird angezeigt.  
  
6.  Wählen Sie bei Trichterdiagrammen einen Wert für die Eigenschaft FunnelLabelStyle aus. Wählen Sie bei Pyramidendiagrammen einen Wert für die Eigenschaft PyramidLabelStyle aus.  
  
    > [!NOTE]  
    >  Wenn diese Eigenschaft auf einen Wert festgelegt ist `OutsideInColumn`, werden die Bezeichnungen in einer vertikalen Spalte gezeichnet. Die Position der Spalte kann nicht geändert werden.  
  
### <a name="to-change-the-position-of-point-labels-in-a-bar-chart"></a>So ändern Sie die Position von Punktbezeichnungen in einem Balkendiagramm  
  
1.  Erstellen Sie ein Balkendiagramm.  
  
2.  Klicken Sie auf der Entwurfsoberfläche mit der rechten Maustaste auf das Diagramm, und wählen Sie **Datenbezeichnungen anzeigen**aus.  
  
3.  Öffnen Sie den Bereich Eigenschaften. Klicken Sie auf der Registerkarte **Ansicht** auf **Eigenschaften**.  
  
4.  Klicken Sie auf der Entwurfsoberfläche auf das Diagramm. Die Eigenschaften für das Diagramm werden im Bereich "Eigenschaften" angezeigt.  
  
5.  Erweitern Sie im Abschnitt **Allgemein** den Knoten **CustomAttributes** . Eine Liste mit Attributen für das Balkendiagramm wird angezeigt.  
  
6.  Wählen Sie einen Wert für die Eigenschaft BarLabelStyle aus.  
  
 Wenn die balkenbezeichnungsart nastaven NA hodnotu `Outside`, die Bezeichnungen werden außerhalb des Balkens, platziert werden, solange sie in den Diagrammbereich passen. Falls die Bezeichnung nicht außerhalb des Balkens positioniert werden kann, sondern im Diagrammbereich platziert werden muss, wird sie im Balken an der dem Ende des Balkens am nächsten gelegenen Stelle eingefügt.  
  
### <a name="to-change-the-position-of-point-labels-in-an-area-column-line-or-scatter-chart"></a>So ändern Sie die Position von Punktbezeichnungen in einem Flächen-, Säulen-, Linien- oder Punktdiagramm  
  
1.  Erstellen Sie ein Flächen-, Säulen-, Linien- oder Punktdiagramm.  
  
2.  Klicken Sie auf der Entwurfsoberfläche mit der rechten Maustaste auf das Diagramm, und wählen Sie **Datenbezeichnungen anzeigen**aus.  
  
3.  Öffnen Sie den Bereich Eigenschaften. Klicken Sie auf der Registerkarte **Ansicht** auf **Eigenschaften**.  
  
4.  Klicken Sie auf der Entwurfsoberfläche auf die Reihe. Die Eigenschaften für die Reihe werden im Bereich "Eigenschaften" angezeigt.  
  
5.  Erweitern Sie im Abschnitt **Daten** den Knoten **DataPoint** und dann den Knoten **Label**.  
  
6.  Wählen Sie einen Wert für die Eigenschaft „Position“ aus.  
  
## <a name="see-also"></a>Siehe auch  
 [Kreisdiagramme &#40;Berichts-Generator und SSRS&#41;](charts-report-builder-and-ssrs.md)   
 [Balkendiagramme &#40;Berichts-Generator und SSRS&#41;](bar-charts-report-builder-and-ssrs.md)   
 [Formatieren von Achsenbezeichnungen in einem Diagramm &#40;Berichts-Generator und SSRS&#41;](formatting-axis-labels-on-a-chart-report-builder-and-ssrs.md)   
 [Formatieren von Achsenbezeichnungen als Datumsangabe oder Währung (Berichts-Generator und SSRS)](format-axis-labels-as-dates-or-currencies-report-builder-and-ssrs.md)   
 [Anzeigen von Datenpunktbezeichnungen außerhalb eines Kreisdiagramms &#40;Berichts-Generator und SSRS&#41;](display-data-point-labels-outside-a-pie-chart-report-builder-and-ssrs.md)   
 [Formatieren von Datenpunkten in einem Diagramm &#40;Berichts-Generator und SSRS&#41;](formatting-data-points-on-a-chart-report-builder-and-ssrs.md)  
  
  
