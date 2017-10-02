---
title: "Erfassen einer Liste für die foreach-Schleife mit dem Skripttask | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- Foreach Loop containers
- Script task [Integration Services], Foreach loops
- Script task [Integration Services], examples
- SSIS Script task, Foreach loops
ms.assetid: 694f0462-d0c5-4191-b64e-821b1bdef055
caps.latest.revision: 34
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: b1bd133c2fdc8c500db9c07df9c54e954db327bf
ms.contentlocale: de-de
ms.lasthandoff: 09/26/2017

---
# <a name="gathering-a-list-for-the-foreach-loop-with-the-script-task"></a>Erfassen einer Liste für die ForEach-Schleife mit dem Skripttask
  Der Foreach-Enumerator für Daten aus Variable führt die Elemente in einer Liste auf, die ihm in einer Variablen übergeben wird, und führt für alle Elemente dieselben Aufgaben aus. Sie können benutzerdefinierten Code in einem Skripttask verwenden, um eine Liste für diesen Zweck zu erstellen. Weitere Informationen zum Enumerator finden Sie unter [ForEach-Schleifencontainer](../../integration-services/control-flow/foreach-loop-container.md).  
  
> [!NOTE]  
>  Wenn Sie einen Task erstellen möchten, den Sie einfacher in mehreren Paketen wiederverwenden können, empfiehlt es sich, den Code in diesem Skripttaskbeispiel als Ausgangspunkt für einen benutzerdefinierten Task zu verwenden. Weitere Informationen finden Sie unter [Entwickeln eines benutzerdefinierten Tasks](../../integration-services/extending-packages-custom-objects/task/developing-a-custom-task.md).  
  
## <a name="description"></a>Description  
 Im folgenden Beispiel wird die Methoden aus der **System.IO** Namespace zum Sammeln einer Liste von Excel-Arbeitsmappen auf dem Computer, die älter sind als eine Anzahl von Tagen angegeben, die vom Benutzer in einer Variablen oder neuer sind. Verzeichnisse des Laufwerks C werden rekursiv nach Dateien durchsucht, die eine .xls-Erweiterung aufweisen. Anschließend wird das Datum der letzten Änderung der Datei überprüft, um festzustellen, ob die Datei in die Liste gehört. Es fügt geeignete Dateien werden ein **ArrayList** und speichert die **ArrayList** in einer Variablen zur späteren Verwendung in einem ForEach-Schleifencontainer. Der Foreach-Schleifencontainer wird für die Verwendung des Foreach-Enumerators für Daten aus Variable konfiguriert.  
  
> [!NOTE]  
>  Die Variable, die mit den Foreach from-Variablenenumerator muss vom Typ **Objekt**. Das Objekt, das Sie in der Variablen platzieren muss eine der folgenden Schnittstellen implementieren: **"System.Collections.IEnumerable"**, **System.Runtime.InteropServices.ComTypes.IEnumVARIANT**, **System.ComponentModel IListSource**, oder **Microsoft.SqlServer.Dts.Runtime.Wrapper.ForEachEnumeratorHost**. Ein **Array** oder **ArrayList** wird häufig verwendet. Die **ArrayList** erfordert einen Verweis und ein **Importe** -Anweisung für die **System.Collections** Namespace.  
  
 Sie können mit diesem Task experimentieren, indem Sie verschiedene positive und negative Werte für die Paketvariable `FileAge` einsetzen. Sie können z. B. den Wert 5 eingeben, um nach Dateien zu suchen, die in den letzten fünf Tagen erstellt wurden, oder den Wert -3 für Dateien, die vor mehr als drei Tagen angelegt wurden. Diese Aufgabe kann bei Laufwerken, die viele zu durchsuchende Ordner enthalten, ein bis zwei Minuten in Anspruch nehmen.  
  
#### <a name="to-configure-this-script-task-example"></a>So konfigurieren Sie dieses Skripttaskbeispiel  
  
1.  Erstellen Sie eine Paketvariable vom Typ integer mit dem Namen `FileAge`, und geben Sie einen positiven oder negativen ganzzahligen Wert ein. Ist der Wert positiv, sucht der Code nach Dateien, die neuer als die angegebene Anzahl von Tagen ist. Bei negativen Werten wird nach Dateien gesucht, die älter als die genannte Anzahl von Tagen sind.  
  
2.  Erstellen Sie eine Paketvariable, die mit dem Namen `FileList` des Typs **Objekt** erhalten Sie die Liste der Dateien, die vom Skripttask für die spätere Verwendung durch den Foreach from-Variablenenumerator erfasst.  
  
3.  Hinzufügen der `FileAge` Variable an des Skripttasks **ReadOnlyVariables** -Eigenschaft, und fügen die `FileList` Variable auf die **ReadWriteVariables** Eigenschaft.  
  
4.  Importieren Sie in Ihrem Code die **System.Collections** und **System.IO** Namespaces.  
  
### <a name="code"></a>Code  
  
```vb  
Imports System  
Imports System.Data  
Imports System.Math  
Imports Microsoft.SqlServer.Dts.Runtime  
Imports System.Collections  
Imports System.IO  
  
Public Class ScriptMain  
  
  Private Const FILE_AGE As Integer = -50  
  
  Private Const FILE_ROOT As String = "C:\"  
  Private Const FILE_FILTER As String = "*.xls"  
  
  Private isCheckForNewer As Boolean = True  
  Dim fileAgeLimit As Integer  
  Private listForEnumerator As ArrayList  
  
  Public Sub Main()  
  
    fileAgeLimit = DirectCast(Dts.Variables("FileAge").Value, Integer)  
  
    ' If value provided is positive, we want files NEWER THAN n days.  
    '  If negative, we want files OLDER THAN n days.  
    If fileAgeLimit < 0 Then  
      isCheckForNewer = False  
    End If  
    ' Extract number of days as positive integer.  
    fileAgeLimit = Math.Abs(fileAgeLimit)  
  
    listForEnumerator = New ArrayList  
  
    GetFilesInFolder(FILE_ROOT)  
  
    ' Return the list of files to the variable  
    '  for later use by the Foreach from Variable enumerator.  
    System.Windows.Forms.MessageBox.Show("Matching files: " & listForEnumerator.Count.ToString, "Results", Windows.Forms.MessageBoxButtons.OK, Windows.Forms.MessageBoxIcon.Information)  
    Dts.Variables("FileList").Value = listForEnumerator  
  
    Dts.TaskResult = ScriptResults.Success  
  
  End Sub  
  
  Private Sub GetFilesInFolder(ByVal folderPath As String)  
  
    Dim localFiles() As String  
    Dim localFile As String  
    Dim fileChangeDate As Date  
    Dim fileAge As TimeSpan  
    Dim fileAgeInDays As Integer  
    Dim childFolder As String  
  
    Try  
      localFiles = Directory.GetFiles(folderPath, FILE_FILTER)  
      For Each localFile In localFiles  
        fileChangeDate = File.GetLastWriteTime(localFile)  
        fileAge = DateTime.Now.Subtract(fileChangeDate)  
        fileAgeInDays = fileAge.Days  
        CheckAgeOfFile(localFile, fileAgeInDays)  
      Next  
  
      If Directory.GetDirectories(folderPath).Length > 0 Then  
        For Each childFolder In Directory.GetDirectories(folderPath)  
          GetFilesInFolder(childFolder)  
        Next  
      End If  
  
    Catch  
      ' Ignore exceptions on special folders such as System Volume Information.  
    End Try  
  
  End Sub  
  
  Private Sub CheckAgeOfFile(ByVal localFile As String, ByVal fileAgeInDays As Integer)  
  
    If isCheckForNewer Then  
      If fileAgeInDays <= fileAgeLimit Then  
        listForEnumerator.Add(localFile)  
      End If  
    Else  
      If fileAgeInDays > fileAgeLimit Then  
        listForEnumerator.Add(localFile)  
      End If  
    End If  
  
  End Sub  
  
End Class  
```  
  
```csharp  
using System;  
using System.Data;  
using System.Math;  
using Microsoft.SqlServer.Dts.Runtime;  
using System.Collections;  
using System.IO;  
  
public partial class ScriptMain : Microsoft.SqlServer.Dts.Tasks.ScriptTask.VSTARTScriptObjectModelBase  
    {  
  
        private const int FILE_AGE = -50;  
  
        private const string FILE_ROOT = "C:\\";  
        private const string FILE_FILTER = "*.xls";  
  
        private bool isCheckForNewer = true;  
        int fileAgeLimit;  
        private ArrayList listForEnumerator;  
  
        public void Main()  
  {  
  
    fileAgeLimit = (int)(Dts.Variables["FileAge"].Value);  
  
    // If value provided is positive, we want files NEWER THAN n days.  
    // If negative, we want files OLDER THAN n days.  
    if (fileAgeLimit<0)  
    {  
      isCheckForNewer = false;  
    }  
    // Extract number of days as positive integer.  
    fileAgeLimit = Math.Abs(fileAgeLimit);  
  
    ArrayList listForEnumerator = new ArrayList();  
  
    GetFilesInFolder(FILE_ROOT);  
  
    // Return the list of files to the variable  
    // for later use by the Foreach from Variable enumerator.  
    System.Windows.Forms.MessageBox.Show("Matching files: "+ listForEnumerator.Count, "Results",   
MessageBoxButtons.OK, MessageBoxIcon.Information);  
    Dts.Variables["FileList"].Value = listForEnumerator;  
  
    Dts.TaskResult = (int)ScriptResults.Success;  
  
  }  
  
        private void GetFilesInFolder(string folderPath)  
        {  
  
            string[] localFiles;  
            DateTime fileChangeDate;  
            TimeSpan fileAge;  
            int fileAgeInDays;  
  
            try  
            {  
                localFiles = Directory.GetFiles(folderPath, FILE_FILTER);  
                foreach (string localFile in localFiles)  
                {  
                    fileChangeDate = File.GetLastWriteTime(localFile);  
                    fileAge = DateTime.Now.Subtract(fileChangeDate);  
                    fileAgeInDays = fileAge.Days;  
                    CheckAgeOfFile(localFile, fileAgeInDays);  
                }  
  
                if (Directory.GetDirectories(folderPath).Length > 0)  
                {  
                    foreach (string childFolder in Directory.GetDirectories(folderPath))  
                    {  
                        GetFilesInFolder(childFolder);  
                    }  
                }  
  
            }  
            catch  
            {  
                // Ignore exceptions on special folders, such as System Volume Information.  
            }  
  
        }  
  
        private void CheckAgeOfFile(string localFile, int fileAgeInDays)  
        {  
  
            if (isCheckForNewer)  
            {  
                if (fileAgeInDays <= fileAgeLimit)  
                {  
                    listForEnumerator.Add(localFile);  
                }  
            }  
            else  
            {  
                if (fileAgeInDays > fileAgeLimit)  
                {  
                    listForEnumerator.Add(localFile);  
                }  
            }  
  
        }  
  
    }  
```  
  
## <a name="see-also"></a>Siehe auch  
 [ForEach-Schleifencontainer](../../integration-services/control-flow/foreach-loop-container.md)   
 [Konfigurieren eines Foreach-Schleifencontainers](http://msdn.microsoft.com/library/519c6f96-5e1f-47d2-b96a-d49946948c25)  
  
  