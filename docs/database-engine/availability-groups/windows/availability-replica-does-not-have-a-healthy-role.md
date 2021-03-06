---
title: Verfügbarkeitsreplikat hat keine fehlerfreie Rolle | Microsoft-Dokumentation
ms.custom: ''
ms.date: 05/17/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: high-availability
ms.topic: conceptual
f1_keywords:
- sql13.swb.agdashboard.arp1rolehealthy.issues.f1
helpviewer_keywords:
- Availability Groups [SQL Server], policies
ms.assetid: ebb2c9f4-2097-4688-b4fb-8f0571047317
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: aec1a0cc2b6a5f12dce1d8c49c7d2c1b26771e00
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: HT
ms.contentlocale: de-DE
ms.lasthandoff: 11/13/2018
ms.locfileid: "51602820"
---
# <a name="availability-replica-does-not-have-a-healthy-role"></a>Verfügbarkeitsreplikat hat keine fehlerfreie Rolle
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
    
## <a name="introduction"></a>Einführung  
  
|||  
|-|-|  
|**Richtlinienname**|Verfügbarkeitsreplikat-Rollenstatus|  
|**Problem**|Das Verfügbarkeitsreplikat hat keine fehlerfreie Rolle.|  
|**Kategorie**|**Kritisch**|  
|**Facet**|Verfügbarkeitsreplikat|  
  
## <a name="description"></a>und Beschreibung  
 Diese Richtlinie überprüft den Status der Verfügbarkeitsreplikatrolle. Die Richtlinie befindet sich in einem fehlerhaften Zustand, wenn die Rolle des Verfügbarkeitsreplikats weder primär noch sekundär ist. Die Richtlinie befindet sich andernfalls in einem ordnungsgemäßen Zustand.  
  
> [!NOTE]  
>  Für diese Version von [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]finden Sie Informationen zu möglichen Ursachen und Lösungen im TechNet Wiki unter [Verfügbarkeitsreplikat hat keine fehlerfreie Rolle](https://go.microsoft.com/fwlink/p/?LinkId=220856) .  
  
## <a name="possible-causes"></a>Mögliche Ursachen  
 Die Rolle dieses Verfügbarkeitsreplikats ist fehlerhaft. Das Replikat hat nicht entweder die primäre oder sekundäre Rolle inne.  
  
## <a name="possible-solution-informationstilltocome"></a>Mögliche Lösung: Informationen_werden_noch_bereitgestellt  
  
## <a name="see-also"></a>Weitere Informationen finden Sie unter  
 [Übersicht über AlwaysOn-Verfügbarkeitsgruppen &#40;SQL Server&#41;](../../../database-engine/availability-groups/windows/overview-of-always-on-availability-groups-sql-server.md)   
 [Verwenden des AlwaysOn-Dashboards &#40;SQL Server Management Studio&#41;](../../../database-engine/availability-groups/windows/use-the-always-on-dashboard-sql-server-management-studio.md)  
  
  
