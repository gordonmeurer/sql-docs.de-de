---
title: Entfernen von Renderingerweiterungen | Microsoft Docs
ms.custom: 
ms.date: 03/18/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- deleting rendering extensions
- removing rendering extensions
- rendering extensions [Reporting Services], removing
ms.assetid: 2abfebfb-065f-45cc-a904-c914394cf900
caps.latest.revision: 38
author: sabotta
ms.author: carlasab
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 58e9d46c17b300cda365e8b42d6442e00ffab0b9
ms.contentlocale: de-de
ms.lasthandoff: 06/13/2017

---
# <a name="removing-a-rendering-extension"></a>Entfernen von Renderingerweiterungen
  So entfernen Sie eine [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] Renderingerweiterung, entfernen Sie einfach die **Erweiterung** -Element für Ihre Renderingerweiterung aus der Datei "rsreportserver.config" in **%ProgramFiles%\Microsoft SQL Server\MSRS10_50.\< Instanzname > \reporting** Ordner. Wenn Sie Einträge für einen Berichts-Designer als auch auf einem Berichtsserver vorgenommen haben, entfernen Sie die **Erweiterung** Element aus der [RSReportDesigner-Konfigurationsdatei](../../../reporting-services/report-server/rsreportdesigner-configuration-file.md) ebenfalls. Nachdem Sie die Konfigurationsdaten entfernt haben, steht die Renderingerweiterung nicht mehr für die Komponente zur Verfügung.  
  
## <a name="see-also"></a>Siehe auch  
 [Reporting Services-Konfigurationsdateien](../../../reporting-services/report-server/reporting-services-configuration-files.md)   
 [Implementieren von Renderingerweiterungen](../../../reporting-services/extensions/rendering-extension/implementing-a-rendering-extension.md)   
 [Übersicht über Renderingerweiterungen](../../../reporting-services/extensions/rendering-extension/rendering-extensions-overview.md)   
 [Implementieren der IRenderingExtension-Schnittstelle](../../../reporting-services/extensions/rendering-extension/implementing-the-irenderingextension-interface.md)   
 [Überlegungen zur Sicherheit bei Erweiterungen](../../../reporting-services/extensions/security-considerations-for-extensions.md)   
 [Bereitstellen von Renderingerweiterungen](../../../reporting-services/extensions/rendering-extension/deploying-a-rendering-extension.md)  
  
  