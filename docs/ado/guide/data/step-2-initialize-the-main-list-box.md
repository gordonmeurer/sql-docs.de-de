---
title: 'Schritt 2: Initialisieren der wichtigsten Listenfelder | Microsoft-Dokumentation'
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
ms.assetid: a1454493-1c86-46c2-ada8-d3c6fcdaf3c1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 629ba98b4b30f5000cac7366f5b558e925cf20cf
ms.sourcegitcommit: 63b4f62c13ccdc2c097570fe8ed07263b4dc4df0
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/13/2018
ms.locfileid: "51600010"
---
# <a name="step-2-initialize-the-main-list-box"></a>Schritt 2: Initialisieren des Listenfelds „Main“
Um globale Datensatz und Recordset-Objekte zu deklarieren, fügen Sie den folgenden Code in die (Allgemein) (Deklarationen) für Form1 aus:  
  
```  
Option Explicit  
Dim grec As Record  
Dim grs As Recordset  
```  
  
 Dieser Code deklariert die globale Objektverweise für Datensatz und Recordset-Objekte, die weiter unten in diesem Szenario verwendet werden.  
  
## <a name="to-connect-to-a-url-and-populate-lstmain"></a>Eine Verbindung mit einer URL, und füllen IstMain  
 Fügen Sie den folgenden Code in den Formular-Ereignishandler für Form1:  
  
```  
Private Sub Form_Load()  
    Set grec = New Record  
    Set grs = New Recordset  
    grec.Open "", "URL=https://servername/foldername/", , _  
        adOpenIfExists Or adCreateCollection  
    Set grs = grec.GetChildren  
    While Not grs.EOF  
        lstMain.AddItem grs(0)  
        grs.MoveNext  
    Wend  
End Sub  
```  
  
 Dieser Code instanziiert die globalen Datensatz und Recordset-Objekte. Das Datensatzobjekt `grec`, mit einer URL, die als ActiveConnection angegeben geöffnet wird. Wenn die URL vorhanden ist, wird sie geöffnet. Wenn sie nicht bereits vorhanden ist, wird es erstellt. Beachten Sie, die Sie ersetzen soll "https://servername/foldername/" mit einer gültigen URL aus Ihrer Umgebung.  
  
 Das Recordset-Objekt, `grs`, wird geöffnet, auf die untergeordneten Elemente des Datensatzes, `grec`. Klicken Sie dann `lstMain` wird aufgefüllt, die Dateinamen der Ressourcen in der URL veröffentlicht.  
  
## <a name="see-also"></a>Siehe auch  
 [Internet Publishing-Szenario](../../../ado/guide/data/internet-publishing-scenario.md)   
 [Schritt 1: Einrichten von Visual Basic-Projekt](../../../ado/guide/data/step-1-set-up-the-visual-basic-project.md)   
 [Schritt 3: Auffüllen des Listenfelds „Fields“](../../../ado/guide/data/step-3-populate-the-fields-list-box.md)
