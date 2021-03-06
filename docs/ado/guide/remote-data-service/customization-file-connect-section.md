---
title: Connect-Abschnitt der Anpassungsdatei | Microsoft-Dokumentation
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 11/09/2018
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- connect section in RDS [ADO]
- customization file in RDS [ADO]
ms.assetid: d50eb3cc-a822-486f-b80b-65bb50547ecd
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: bb493378240f8c536b0af1c1b0ff5cf3bc93c042
ms.sourcegitcommit: 1a5448747ccb2e13e8f3d9f04012ba5ae04bb0a3
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/12/2018
ms.locfileid: "51558537"
---
# <a name="customization-file-connect-section"></a>Connect-Abschnitt der Anpassungsdatei
Das Standardverhalten des ereignishandlers ist, alle Verbindungen zu verweigern. Die **verbinden** Abschnitt gibt Ausnahmen, um dieses Verhalten. Z. B., wenn alle der **verbinden** Abschnitte wurden, fehlt oder ist leer, und dann in der Standardeinstellung keine Verbindungen hergestellt werden konnte.  
  
 Die **verbinden** Abschnitt enthalten kann:  
  
-   Ein Zugriffseintrag, der angibt, der Standardwert Lese- und Schreibvorgänge, die für diese Verbindung zulässig. Bei wird kein Standard-Access-Eintrag im Abschnitt wird der Abschnitt ignoriert werden.  
  
-   Eine neue Verbindungszeichenfolge, die die Client-Verbindungszeichenfolge ersetzt.  
  
> [!IMPORTANT]
>  Ab Windows 8 und Windows Server 2012, sind nicht mehr RDS-Server-Komponenten in das Windows-Betriebssystem enthalten (finden Sie unter Windows 8 und [Windows Server 2012 Compatibility Cookbook](https://www.microsoft.com/download/details.aspx?id=27416) Einzelheiten). RDS-Client-Komponenten werden in einer zukünftigen Version von Windows entfernt werden. Nutzen Sie diese Funktionen bei Neuentwicklungen nicht mehr, und planen Sie die Änderung von Anwendungen, die diese Funktion zurzeit verwenden. Anwendungen, die RDS zu migrieren sollten [WCF Data Service](https://go.microsoft.com/fwlink/?LinkId=199565).  
  
## <a name="syntax"></a>Syntax  
 Ein Zugriffseintrag hat das Format:  
  
```console
  
Access=  
accessRight  
  
```  
  
 Ein Ersatz-Verbindungszeichenfolgeneintrag hat folgendes Format:  
  
```console
  
Connect=  
connectionString  
  
```  
  
## <a name="remarks"></a>Hinweise  
  
|Teil|Description|  
|----------|-----------------|  
|**Verbinden**|Eine Literalzeichenfolge, die dies weist darauf hin, ist ein Eintrag der Verbindungszeichenfolge.|  
|***connectionString***|Eine Zeichenfolge, die die gesamte Client-Verbindungszeichenfolge ersetzt.|  
|**Zugriff**|Eine Literalzeichenfolge, die dies weist darauf hin ist ein Zugriffseintrag.|  
|***accessRight***|Eine der folgenden Zugriffsrechte:<br /><br /> -   **NoAccess** – Benutzer kann nicht auf die Datenquelle zugreifen.<br />-   **ReadOnly** – der Benutzer kann die Datenquelle lesen.<br />-   **"ReadWrite"** – Benutzer Lese- oder Schreibzugriff auf Daten in die Datenquelle.|  
  
 Wenn Sie eine Verbindung (in "Auswirkung", "das Deaktivieren des Standardverhaltens von Handler") zulassen möchten, legen Sie den Zugriffseintrag in der **standardmäßig verbinden** Abschnitt `Access=ReadWrite`, und löschen, oder kommentieren Sie alle anderen **Verbinden** *Bezeichner* Abschnitt.  
  
## <a name="see-also"></a>Siehe auch  
 [Logs-Abschnitt der Anpassungsdatei](../../../ado/guide/remote-data-service/customization-file-logs-section.md)   
 [SQL-Abschnitt der Anpassungsdatei](../../../ado/guide/remote-data-service/customization-file-sql-section.md)   
 [UserList-Abschnitt der Anpassungsdatei](../../../ado/guide/remote-data-service/customization-file-userlist-section.md)   
 [DataFactory-Anpassung](../../../ado/guide/remote-data-service/datafactory-customization.md)   
 [Erforderliche Clienteinstellungen](../../../ado/guide/remote-data-service/required-client-settings.md)   
 [Grundlegendes zu der Anpassungsdatei](../../../ado/guide/remote-data-service/understanding-the-customization-file.md)   
 [Schreiben Ihres eigenen benutzerdefinierten Handlers](../../../ado/guide/remote-data-service/writing-your-own-customized-handler.md)



