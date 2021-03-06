---
title: Ändern und Verarbeiten der Market Basket-Modells (mittleres Datamining Tutorial) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: b6019413-aebd-4ff7-831a-644572ad88b1
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 9c99945ad1e1d8c5027f7dfc63dcb725b0f0dac7
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/02/2018
ms.locfileid: "48204380"
---
# <a name="modifying-and-processing-the-market-basket-model-intermediate-data-mining-tutorial"></a>Ändern und Verarbeiten des Market Basket-Modells (Data Mining-Lernprogramm für Fortgeschrittene)
  Bevor Sie das von Ihnen erstellte Association-Miningmodell verarbeiten, müssen Sie die Standardwerte von zwei der Parameter ändern: *Support* und *Probability*.  
  
-   *Support* definiert den Prozentsatz von Fällen, in denen eine Regel vorhanden sein muss, um als gültig betrachtet zu werden. Geben Sie an, dass bei mindestens 1 Prozent der Fälle eine Regel vorhanden sein muss.  
  
-   *Probability* definiert, wie wahrscheinlich eine Zuordnung sein muss, um als gültig betrachtet zu werden. Berücksichtigen Sie alle Zuordnungen mit einer Wahrscheinlichkeit von mindestens 10 Prozent.  
  
 Weitere Informationen zu den Auswirkungen der Erhöhung bzw. Verringerung von Support und Probability finden Sie unter [Microsoft Association Algorithm Technical Reference](../../2014/analysis-services/data-mining/microsoft-association-algorithm-technical-reference.md).  
  
 Nachdem Sie Struktur und Parameter für das **Association** -Miningmodell definiert haben, können Sie das Modell verarbeiten.  
  
### <a name="to-adjust-the-parameters-of-the-association-model"></a>So passen Sie die Parameter für das Modell Association an  
  
1.  Öffnen Sie im Data Mining-Designer die Registerkarte **Miningmodelle** .  
  
2.  Klicken Sie im Designer mit der rechten Maustaste auf die Spalte **Association** , und wählen Sie **Algorithmusparameter festlegen** , um das Dialogfeld Algorithmusparameter zu öffnen.  
  
3.  Legen Sie in der Spalte **Wert** des Dialogfelds **Algorithmusparameter** folgende Parameter fest:  
  
     MINIMUM_PROBABILITY = 0.1  
  
     MINIMUM_SUPPORT = 0.01  
  
4.  [!INCLUDE[clickOK](../includes/clickok-md.md)]  
  
### <a name="to-process-the-mining-model"></a>So wird das Miningmodell verarbeitet  
  
1.  Auf der **Miningmodell** Menü [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]Option **Miningstruktur verarbeiten und alle Modelle.**  
  
2.  Klicken Sie in der Meldung mit der Frage, ob Sie das Projekt erstellen und bereitstellen möchten, auf **Ja**.  
  
     Das Dialogfeld **Miningstruktur verarbeiten - Association** wird angezeigt.  
  
3.  Klicken Sie auf **Ausführen**.  
  
     Das Dialogfeld **Verarbeitungsstatus** wird geöffnet und zeigt Informationen zur Verarbeitung des Modells an. Das Verarbeiten der neuen Struktur und des Modells kann eine Weile dauern.  
  
4.  Nachdem die Verarbeitung abgeschlossen ist, klicken Sie auf **Schließen** , um das Dialogfeld **Verarbeitungsstatus** zu schließen.  
  
5.  Klicken Sie auf **Schließen** , um das Dialogfeld **Miningstruktur verarbeiten - Association** wieder zu schließen.  
  
## <a name="next-task-in-lesson"></a>Nächste Aufgabe in dieser Lektion  
 [Durchsuchen der Market Basket-Modellen &#40;Datamining-Lernprogramm für fortgeschrittene&#41;](../../2014/tutorials/exploring-the-market-basket-models-intermediate-data-mining-tutorial.md)  
  
## <a name="see-also"></a>Siehe auch  
 [Anforderungen und Überlegungen zur Verarbeitung &#40;Datamining&#41;](../../2014/analysis-services/data-mining/processing-requirements-and-considerations-data-mining.md)  
  
  
