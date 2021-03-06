---
title: Einfügen, aktualisieren und Löschen von Elementen (XMLA) | Microsoft-Dokumentation
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: xmla
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 3a409e21e925b3912aee5ec751747f61bce05276
ms.sourcegitcommit: 7fe14c61083684dc576d88377e32e2fc315b7107
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/26/2018
ms.locfileid: "50147325"
---
# <a name="inserting-updating-and-dropping-members-xmla"></a>Einfügen, Aktualisieren und Löschen von Elementen (XMLA)
  Können Sie die [einfügen](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/insert-element-xmla), [aktualisieren](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/update-element-xmla), und [löschen](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/drop-element-xmla) -Befehle in XML for Analysis (XMLA) bzw. einfügen, aktualisieren oder Löschen von Mitgliedern aus einer Dimension mit aktiviertem Schreibzugriff. Weitere Informationen zu Dimensionen mit aktiviertem Schreibzugriff, finden Sie unter [Dimensionen mit aktiviertem Schreibzugriff](../../analysis-services/multidimensional-models-olap-logical-dimension-objects/write-enabled-dimensions.md).  
  
## <a name="inserting-new-members"></a>Einfügen von neuen Elementen  
 Die **einfügen** -Befehl fügt festgelegten Attributen in einer Dimension mit aktiviertem Schreibzugriff neue Elemente hinzu.  
  
 Vor der Erstellung der **einfügen** Befehls müssen Sie die folgende Informationen für die neuen Elemente eingefügt werden soll:  
  
-   Die Dimension, in die die neuen Elemente eingefügt werden sollen.  
  
-   Das Dimensionsattribut, in die die neuen Elemente eingefügt werden sollen.  
  
-   Die Namen der neuen Elemente, einschließlich alle entsprechenden Übersetzungen für den Namen.  
  
-   Die Schlüssel der neuen Elemente. Wenn ein Attribut einen zusammengesetzten Schlüssel verwendet, erfordert der Schlüssel möglicherweise mehrere Werte.  
  
-   Werte für alle entsprechenden Attributeigenschaften, die nicht als andere Attribute innerhalb der Dimension implementiert wurden. Derartige Attributeigenschaften umfassen unäre Operationen, Übersetzungen, benutzerdefinierte Rollups, benutzerdefinierte Rollupeigenschaften und übersprungene Ebenen.  
  
 Die **einfügen** -Befehl unterstützt nur zwei Eigenschaften:  
  
-   Die [Objekt](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/object-element-xmla) -Eigenschaft, die einen Objektverweis für die Dimension enthält, in dem die Elemente eingefügt werden soll. Der Objektverweis enthält den Datenbankbezeichner, den Cubebezeichner sowie den Dimensionsbezeichner für die Dimension.  
  
-   Die [Attribute](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/attributes-element-xmla) Eigenschaft, die eine oder mehrere enthält [Attribut](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/attribute-element-xmla) Elemente die Attribute zu identifizieren, in dem Elemente eingefügt werden soll. Jede **Attribut** -Element identifiziert ein Attribut enthält, Name, Wert, Übersetzungen, unäroperator, benutzerdefinierte Rollups, Benutzerdefinierte Rollupeigenschaften und übersprungene Ebenen für ein einzelnes Element, das dem identifizierten Attribut hinzugefügt werden.  
  
    > [!NOTE]  
    >  Alle Eigenschaften für die **Attribut** -Element müssen eingefügt werden. Andernfalls tritt möglicherweise ein Fehler auf.  
  
## <a name="updating-existing-members"></a>Aktualisieren von vorhandenen Elementen  
 Die **Update** Befehl aktualisiert vorhandene Elemente in festgelegten Attributen, die auf der Grundlage der Beziehungen mit anderen Mitgliedern in anderen Attributen in einer Dimension mit aktiviertem Schreibzugriff. Die **Update** Befehl Elemente auf andere Ebenen in Hierarchien der Dimension enthalten und können verwendet werden, um die über-/ unterordnungshierarchien, die von übergeordneten Attributen definierte umstrukturieren verschieben.  
  
 Vor der Erstellung der **Update** Befehls müssen Sie die folgende Informationen für die Elemente aktualisiert werden:  
  
-   Die Dimension, in der die vorhandenen Elemente aktualisiert werden sollen.  
  
-   Die Dimensionsattribute, in denen die vorhandenen Elemente aktualisiert werden sollen.  
  
-   Die Schlüssel der vorhandenen Elemente. Wenn ein Attribut einen zusammengesetzten Schlüssel verwendet, erfordert der Schlüssel möglicherweise mehrere Werte.  
  
-   Werte für alle entsprechenden Attributeigenschaften, die nicht als andere Attribute innerhalb der Dimension implementiert wurden. Derartige Attributeigenschaften umfassen unäre Operationen, Übersetzungen, benutzerdefinierte Rollups, benutzerdefinierte Rollupeigenschaften und übersprungene Ebenen.  
  
 Die **Update** -Befehl unterstützt nur drei erforderliche Eigenschaften:  
  
-   Die **Objekt** -Eigenschaft, die einen Objektverweis für die Dimension enthält, in dem die Elemente aktualisiert werden. Der Objektverweis enthält den Datenbankbezeichner, den Cubebezeichner sowie den Dimensionsbezeichner für die Dimension.  
  
-   Die **Attribute** Eigenschaft, die eine oder mehrere enthält **Attribut** Elemente, Attribute zu identifizieren, in dem Mitglieder sind, aktualisiert werden. Die **Attribut** -Element identifiziert ein Attribut enthält, Name, Wert, Übersetzungen, unäroperator, benutzerdefinierte Rollups, Benutzerdefinierte Rollupeigenschaften und übersprungene Ebenen für ein einzelnes Element, das für das identifizierte Attribut aktualisiert.  
  
    > [!NOTE]  
    >  Alle Eigenschaften für die **Attribut** -Element müssen eingefügt werden. Andernfalls tritt möglicherweise ein Fehler auf.  
  
-   Die [, in denen](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/where-element-xmla) Eigenschaft, die eine oder mehrere enthält **Attribut** Elemente, die die Attribute zu beschränken, in dem Mitglieder sind, aktualisiert werden. Die **, in denen** Eigenschaft ist wichtig für die Beschränkung einer **Update** -Befehls auf bestimmte Instanzen eines Elements. Wenn die **, in denen** nicht angegeben wird, werden alle Instanzen eines bestimmten Elements aktualisiert. Angenommen, Sie möchten den Stadtnamen für drei Kunden von Redmond zu Bellevue ändern. Um den Stadtnamen zu ändern, müssen Sie angeben einer **, in denen** , identifiziert die drei Elemente im Customer-Attribut für die die Elemente im City-Attribut geändert werden soll. Wenn Sie keinen dieser **, in denen** -Eigenschaft, würde jeder Kunde, dessen Stadtname zurzeit Redmond ist. Name der Stadt Bellevue nach haben die **Update** -Befehl ausgeführt wird.  
  
    > [!NOTE]  
    >  Mit Ausnahme von neuen Membern die **aktualisieren** Befehl kann nur attributschlüsselwerte für Attribute, die nicht im enthalten aktualisieren die **, in denen** Klausel. Der Stadtname kann beispielsweise nicht aktualisiert werden, wenn ein Kunde aktualisiert wird, andernfalls wird der Stadtname für alle Kunden geändert.  
  
### <a name="updating-members-in-parent-attributes"></a>Aktualisieren von Elementen in übergeordneten Attributen  
 Zur Unterstützung von übergeordneten Attributen, die **Update** -Befehl die optionalen [MoveWithDescendants](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/movewithdescendants-element-xmla)sollte Eigenschaften. Festlegen der **MoveWithDescendants** Eigenschaft auf "true" gibt an, dass die Nachfolger des übergeordneten Elements auch mit dem übergeordneten Element verschoben werden soll, wenn der Bezeichner des übergeordneten Elements ändert. Wenn dieser Wert auf „False“ festgelegt wird, werden die unmittelbaren Nachfolger eines übergeordneten Elements zu der Ebene höhergestuft, auf der sich das übergeordnete Element zuvor befand, wenn dieses übergeordnete Element verschoben wird.  
  
 Beim Aktualisieren von Elementen in ein übergeordnetes Attribut, die **aktualisieren** Befehl Elemente in anderen Attributen kann nicht aktualisiert werden.  
  
## <a name="dropping-existing-members"></a>Löschen von vorhandenen Elementen  
 Vor der Erstellung der **löschen** Befehls müssen Sie die folgende Informationen für die zu löschenden Mitglieder:  
  
-   Die Dimension, in der die vorhandenen Elemente gelöscht werden sollen.  
  
-   Die Dimensionsattribute, in denen die vorhandenen Elemente gelöscht werden sollen.  
  
-   Die Schlüssel der zu löschenden vorhandenen Elemente. Wenn ein Attribut einen zusammengesetzten Schlüssel verwendet, erfordert der Schlüssel möglicherweise mehrere Werte.  
  
 Die **löschen** -Befehl unterstützt nur zwei erforderliche Eigenschaften:  
  
-   Die **Objekt** -Eigenschaft, die einen Objektverweis für die Dimension enthält, in dem die Elemente gelöscht werden soll. Der Objektverweis enthält den Datenbankbezeichner, den Cubebezeichner sowie den Dimensionsbezeichner für die Dimension.  
  
-   Die **, in denen** Eigenschaft, die eine oder mehrere enthält **Attribut** Elementen, die die Attribute zu beschränken, in dem Mitglieder sind, gelöscht werden soll. Die **, in denen** Eigenschaft ist wichtig für die Beschränkung einer **löschen** -Befehls auf bestimmte Instanzen eines Elements. Wenn die **, in denen** Befehl nicht angegeben ist, werden alle Instanzen eines bestimmten Elements gelöscht. Angenommen, Sie möchten in Redmond drei Kunden löschen. Um diese Kunden zu löschen, müssen Sie angeben einer **, in denen** Eigenschaft identifiziert, die die drei Elemente im Customer-Attribut entfernt werden soll und das Element "Redmond" des City-Attributs aus dem sind die drei Kunden entfernt werden soll. Wenn die **, in denen** Eigenschaft gibt nur das Element "Redmond" des City-Attributs, jeder Kunde von Redmond zugeordnet würde gelöscht werden, die **löschen** Befehl. Wenn die **, in denen** Eigenschaft gibt nur die drei Elemente im Customer-Attribut, das die drei Kunden gelöscht werden vollständig über die **löschen** Befehl.  
  
    > [!NOTE]  
    >  Die **Attribut** Elemente in einem **löschen** Befehl darf nur die **AttributeName** und **Schlüssel** Eigenschaften. Andernfalls tritt möglicherweise ein Fehler auf.  
  
### <a name="dropping-members-in-parent-attributes"></a>Löschen von Elementen in übergeordneten Attributen  
 Festlegen der [DeleteWithDescendants](https://docs.microsoft.com/bi-reference/xmla/xml-elements-properties/deletewithdescendants-element-xmla) Eigenschaft gibt an, dass die Nachfolger eines übergeordneten Elements mit dem übergeordneten Element ebenfalls gelöscht werden soll. Wenn dieser Wert auf „False“ festgelegt wird, werden die unmittelbaren Nachfolger eines übergeordneten Elements zu der Ebene höhergestuft, auf der sich das übergeordnete Element zuvor befand.  
  
> [!IMPORTANT]  
>  Ein Benutzer muss lediglich über Löschberechtigungen für das übergeordnete Element verfügen, um sowohl das übergeordnete Element als auch die Nachfolger zu löschen. Ein Benutzer benötigt keine Löschberechtigungen für die Nachfolger.  
  
## <a name="see-also"></a>Siehe auch  
 [Drop-Element &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/drop-element-xmla)   
 [INSERT-Element &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/insert-element-xmla)   
 [Update-Element &#40;XMLA&#41;](https://docs.microsoft.com/bi-reference/xmla/xml-elements-commands/update-element-xmla)   
 [Definieren und Identifizieren von Objekten &#40;XMLA&#41;](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/defining-and-identifying-objects-xmla.md)   
 [Entwickeln mit XMLA in Analysis Services](../../analysis-services/multidimensional-models-scripting-language-assl-xmla/developing-with-xmla-in-analysis-services.md)  
  
  
