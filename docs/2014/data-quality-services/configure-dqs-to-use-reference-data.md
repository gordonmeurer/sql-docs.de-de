---
title: Konfigurieren von DQS zum Verwenden von Verweisdaten | Microsoft-Dokumentation
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
f1_keywords:
- sql12.dqs.admin.config.rds.f1
- sql12.dqs.administration.rdsconfiguration.f1
- sql12.dqs.administration.configuration.createDirectRDS.f1
ms.assetid: fae745e7-57a7-4cbc-8979-56ea8e392e4e
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ff622236100399f43b8420bb71a7ae4d5a915013
ms.sourcegitcommit: af1d9fc4a50baf3df60488b4c630ce68f7e75ed1
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2018
ms.locfileid: "51030108"
---
# <a name="configure-dqs-to-use-reference-data"></a>Konfigurieren von DQS zum Verwenden von Verweisdaten
  In diesem Thema wird beschrieben, wie [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) zum Verwenden von Verweisdaten zum Bereinigen der Daten konfiguriert wird. Sie können Verweisdaten von Windows Azure Marketplace oder von direkten Onlineverweisdatendrittanbietern verwenden.  
  
## <a name="before-you-begin"></a>Vorbereitungen  
  
###  <a name="Prerequisites"></a> Erforderliche Komponenten  
 Um Verweisdaten vom Marketplace zu verwenden, müssen Sie über einen gültigen Marketplace-Kontoschlüssel verfügen. Weitere Informationen zum Erstellen eines Marketplace-Kontoschlüssels finden Sie unter [Erstellen eines Marketplace-Kontos](http://go.microsoft.com/fwlink/?LinkId=212936) (http://go.microsoft.com/fwlink/?LinkId=212936). Sie können auch innerhalb von [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] einen Marketplace-Kontoschlüssel erstellen, indem Sie auf **Konfiguration** unter **Verwaltung** im [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] -Startbildschirm und dann auf **ID für DataMarket-Konto erstellen** auf der Registerkarte **Verweisdaten** klicken.  
  
###  <a name="Security"></a> Sicherheit  
  
####  <a name="Permissions"></a> Berechtigungen  
 Sie müssen über die Rolle „dqs_administrator“ in der DQS_MAIN-Datenbank verfügen, um Verweisdaten-Diensteinstellungen in DQS zu konfigurieren.  
  
##  <a name="Marketplace"></a> Konfigurieren von DQS zum Verwenden von Verweisdaten vom Marketplace  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Ausführen der Data Quality-Clientanwendung](../../2014/data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Klicken Sie im [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] -Startbildschirm unter **Verwaltung**auf **Konfiguration**.  
  
3.  Geben Sie auf der Registerkarte **Verweisdaten** unter dem Bereich **Netzwerkeinstellungen** entsprechende Werte in den Feldern **Proxyserver** und **Port** ein, wenn Sie oder Ihre Organisation mithilfe des Proxyservers eine Verbindung zum Internet herstellt.  
  
4.  Geben Sie den Marketplace-Kontoschlüssel im Feld **ID des DataMarket-Kontos** ein, und klicken Sie auf das Symbol **DataMarket-Konto-ID überprüfen** , um den Kontoschlüssel zu überprüfen. Eine Meldung zeigt an, ob der angegebene Marketplace-Kontoschlüssel gültig ist.  
  
 Jetzt können Sie die Verweisdatendienste, die für den angegebenen Marketplace-Kontoschlüssel abonniert wurden, vom Marketplace in DQS verwenden.  
  
##  <a name="ThirdParty"></a> Konfigurieren von DQS zum Verwenden von Verweisdaten von direkten Onlineverweisdatendrittanbietern  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Ausführen der Data Quality-Clientanwendung](../../2014/data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Klicken Sie im [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] -Startbildschirm unter **Verwaltung**auf **Konfiguration**.  
  
3.  Geben Sie auf der Registerkarte **Verweisdaten** unter dem Bereich **Netzwerkeinstellungen** entsprechende Werte in den Feldern **Proxyserver** und **Port** ein, wenn Sie oder Ihre Organisation mithilfe des Proxyservers eine Verbindung zum Internet herstellt.  
  
4.  Klicken Sie im Bereich **Einstellungen für direkten Reference Data Service-Onlinedrittanbieter** auf das Symbol **Neuen Reference Data Service-Anbieter hinzufügen** .  
  
5.  Geben Sie im Dialogfeld **Neuen direkten Reference Data Service-Onlinedrittanbieter erstellen** die folgenden Details an:  
  
    1.  Geben Sie im Feld **Name** einen Namen für den neuen direkten Reference Data Service-Anbieter ein.  
  
    2.  (Optional) Geben Sie im Feld **Beschreibung** eine Beschreibung für den neuen direkten Reference Data Service-Anbieter ein.  
  
    3.  Geben Sie im Feld **Kategorie** die Kategorie der Daten ein, die vom neuen direkten Reference Data Service-Anbieter bereitgestellt werden.  
  
    4.  Geben Sie im Feld Schema das Schema an, das die Zeichenfolge von Feldern (Spaltennamen) definiert, die vom direkten Reference Data Service-Anbieter verwendet werden soll. Ein Feldname sollte kein Leerzeichen enthalten, und die Felder sollten durch Trennzeichen getrennt sein. Beispiel: `FirstName, LastName, City, State`  
  
    5.  Geben Sie im Feld **URI** die URI für den direkten Reference Data Service-Anbieter ein. Nur sichere URIs (Adresse, die mit „https://“ beginnen) sind in DQS zulässig.  
  
    6.  Geben Sie im Feld **Max. Batchgröße** die maximale Anzahl von Datensätzen pro Batch ein, die an den Reference Data Service-Anbieter zum Bereinigen gesendet werden. Maximal 100 Datensätze pro Batch können für die Bereinigungsaktivität angegeben werden.  
  
    7.  Geben Sie im Feld **Konto-ID** die Konto-ID des Abonnenten des Reference Data Service-Anbieters ein.  
  
6.  Klicken Sie auf **OK** , um die Daten zu speichern, und schließen Sie das Dialogfeld **Neuen direkten Reference Data Service-Onlinedrittanbieter erstellen** . Der neu hinzugefügte direkte Reference Data Service-Onlinedrittanbieter wird im **Raster des direkten Reference Data Service-Anbieters** in DQS verfügbar.  
  
 Jetzt können Sie die Reference Data Services des neu konfigurierten direkten Reference Data Service-Onlinedrittanbieters in DQS verwenden.  
  
##  <a name="FollowUp"></a> Nachverfolgung: Nach dem Konfigurieren von DQS zum Verwenden von Verweisdaten  
 Sie müssen die erforderlichen Wissensdatenbankdomänen jetzt den Verweisdaten zuordnen, die bei den gerade konfigurierten Datenanbietern verfügbar sind. Zu diesem Zweck finden Sie unter [Anfügen einer Domäne oder Verbunddomäne an Verweisdaten](../../2014/data-quality-services/attach-a-domain-or-composite-domain-to-reference-data.md).  
  
  
