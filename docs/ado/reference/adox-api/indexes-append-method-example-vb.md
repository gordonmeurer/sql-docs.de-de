---
title: Indizes Append-Methode – Beispiel (VB) | Microsoft-Dokumentation
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
dev_langs:
- VB
helpviewer_keywords:
- Append method [ADOX]
ms.assetid: 50f87e27-1bf9-427c-9b1d-704a672434d2
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9e8f0d245da2bde9763a1b940f8253d4c81fe903
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/01/2018
ms.locfileid: "47705524"
---
# <a name="indexes-append-method-example-vb"></a>Append-Methode für Indizes – Beispiel (VB)
Der folgende Code veranschaulicht, wie ein neuer Index erstellt wird. Der Index ist für zwei Spalten in der Tabelle.  
  
```  
Attribute VB_Name = "IndexesAppend"  
Option Explicit  
  
' BeginCreateIndexVB  
Sub Main()  
    On Error GoTo CreateIndexError  
  
    Dim tbl As New Table  
    Dim idx As New ADOX.Index  
    Dim cat As New ADOX.Catalog  
  
    'Open the catalog.  
    cat.ActiveConnection = "Provider='Microsoft.Jet.OLEDB.4.0';" & _  
        "Data Source='Northwind.mdb';"  
  
    ' Define the table and append it to the catalog.  
    tbl.Name = "MyTable"  
    tbl.Columns.Append "Column1", adInteger  
    tbl.Columns.Append "Column2", adInteger  
    tbl.Columns.Append "Column3", adVarWChar, 50  
    cat.Tables.Append tbl  
    Debug.Print "Table 'MyTable' is added."  
  
    ' Define a multi-column index.  
    idx.Name = "multicolidx"  
    idx.Columns.Append "Column1"  
    idx.Columns.Append "Column2"  
  
    ' Append the index to the table.  
    tbl.Indexes.Append idx  
    Debug.Print "The index is appended to table 'MyTable'."  
  
    'Delete the table as this is a demonstration.  
    cat.Tables.Delete tbl.Name  
    Debug.Print "Table 'MyTable' is deleted."  
  
    'Clean up.  
    Set cat.ActiveConnection = Nothing  
    Set cat = Nothing  
    Set tbl = Nothing  
    Set idx = Nothing  
    Exit Sub  
  
CreateIndexError:  
    Set cat = Nothing  
    Set tbl = Nothing  
    Set idx = Nothing  
  
    If Err <> 0 Then  
        MsgBox Err.Source & "-->" & Err.Description, , "Error"  
    End If  
End Sub  
' EndCreateIndexVB  
```  
  
## <a name="see-also"></a>Siehe auch  
 [Append-Methode (ADOX Indizes)](../../../ado/reference/adox-api/append-method-adox-indexes.md)   
 [Index-Objekt (ADOX)](../../../ado/reference/adox-api/index-object-adox.md)   
 [Auflistung von Indizes (ADOX)](../../../ado/reference/adox-api/indexes-collection-adox.md)
