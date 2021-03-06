---
title: Anforderungsprotokoll | Microsoft-Dokumentation
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
ms.assetid: 165d3833-0493-490c-9f63-8a134a7fafb8
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 55ac9eaaaa2313536c27df4c96723e96b70fada5
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/02/2018
ms.locfileid: "48060860"
---
# <a name="request-log"></a>Anforderungsprotokoll
  Verwenden Sie das Dialogfeld **Anforderungsprotokoll** , um die Ereignisse anzuzeigen, die protokolliert werden, während Beispieldaten vom SAP NetWeaver BW-System angefordert werden. Diese Informationen können hilfreich sein, um Konfigurationsprobleme mit der SAP BW-Quelle zu beheben.  
  
 Weitere Informationen zur SAP BW-Quellkomponente von [!INCLUDE[msCoName](../../includes/msconame-md.md)] Connector 1.1 for SAP BW finden Sie unter [SAP BW-Quelle](sap-bw-source.md).  
  
> [!IMPORTANT]  
>  Die Dokumentation für Microsoft Connector 1.1 for SAP BW setzt Kenntnisse der SAP NetWeaver BW-Umgebung voraus. Weitere Informationen zu SAP NetWeaver BW oder Informationen zur Konfiguration von SAP NetWeaver BW-Objekten und -Prozessen finden Sie in der SAP-Dokumentation.  
  
> [!IMPORTANT]  
>  Das Extrahieren von Daten aus SAP NetWeaver BW erfordert zusätzliche SAP-Lizenzen. Stimmen Sie diese Anforderungen mit SAP ab.  
  
 **So öffnen Sie das Dialogfeld "Anforderungsprotokoll"**  
  
1.  Öffnen Sie in [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]das [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] -Paket, in dem die SAP BW-Quelle enthalten ist.  
  
2.  Doppelklicken Sie auf der Registerkarte **Datenfluss** auf die SAP BW-Quelle.  
  
3.  Klicken Sie im **Quellen-Editor für SAP BW**auf **Verbindungs-Manager** , um die Seite **Verbindungs-Manager** des Editors zu öffnen.  
  
4.  Nachdem Sie die SAP BW-Quelle konfiguriert haben, klicken Sie auf **Vorschau** , um die Ereignisse im Dialogfeld **Anforderungsprotokoll** in der Vorschau anzuzeigen.  
  
    > [!NOTE]  
    >  Wenn Sie auf **Vorschau** klicken, wird auch das Dialogfeld **Vorschau** geöffnet. Weitere Informationen zu diesem Dialogfeld finden Sie unter [Preview](preview.md).  
  
## <a name="options"></a>Tastatur  
 **Zeit**  
 Zeigt die Uhrzeit an, zu der das Ereignis protokolliert wurde.  
  
 **Typ**  
 Zeigt den Typ des protokollierten Ereignisses an. In der folgenden Tabelle sind die möglichen Ereignistypen aufgelistet.  
  
|value|Description|  
|-----------|-----------------|  
|S|Eine Erfolgsmeldung.|  
|E|Fehlermeldung|  
|W|Warnmeldung.|  
|I|Informationsmeldung.|  
|A|Der Vorgang wurde abgebrochen.|  
  
 **MessageBox**  
 Zeigt den Meldungstext an, der dem protokollierten Ereignis zugeordnet ist.  
  
## <a name="see-also"></a>Siehe auch  
 [Quellen-Editor für SAP BW &#40;Seite Verbindungs-Manager&#41;](sap-bw-source-editor-connection-manager-page.md)   
 [F1-Hilfe zu Microsoft Connector 1.1 für SAP BW](../microsoft-connector-for-sap-bw-f1-help.md)  
  
  
