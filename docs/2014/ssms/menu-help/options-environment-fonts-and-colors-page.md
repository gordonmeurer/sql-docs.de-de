---
title: 'Optionen (Umgebung: Schriftarten und Farben-Seite) | Microsoft-Dokumentation'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
ms.assetid: ea3aa222-538d-485f-99dc-01eb02cdcfea
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: f2a73bd30ab72cc293f8cbd0dcebc2b123d6538e
ms.sourcegitcommit: af1d9fc4a50baf3df60488b4c630ce68f7e75ed1
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/06/2018
ms.locfileid: "51031808"
---
# <a name="options-environment-fonts-and-colors-page"></a>Optionen (Umgebung: Seite „Schriftarten und Farben“)
  Im Dialogfeld **Optionen** können Sie ein benutzerdefiniertes Schriftart- und Farbschema für verschiedene Elemente der Benutzeroberfläche in [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] erstellen. Klicken Sie im Menü **Extras** auf **Optionen** , erweitern Sie den Ordner **Umgebung** , und klicken Sie anschließend auf **Schriftarten und Farben**.  
  
 Änderungen am Farbschema werden nicht in der Sitzung wirksam, in der Sie sie vornehmen. Sie können Farbänderungen auswerten, indem Sie eine andere Instanz von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] öffnen und die Bedingungen erstellen, unter denen Sie die Anwendung Ihrer Änderungen erwarten.  
  
## <a name="uielement-list"></a>Liste der Benutzeroberflächenelemente  
 **Einstellungen anzeigen für**  
 Führt alle Elemente der Benutzeroberfläche auf, für die Sie das Schriftart- und Farbschema ändern können. Nach dem Auswählen eines Elements aus der Liste können Sie die Farbeinstellungen für das ausgewählten Element unter **Elemente anzeigen**anpassen.  
  
|Begriff|Definition|  
|----------|----------------|  
|Text-Editor|Änderungen an den Anzeigeeinstellungen für Schriftart, Größe und Farbe für den Text-Editor wirken sich auf die Darstellung von Text in Ihrem Standard-Text-Editor aus. In einem Text-Editor außerhalb von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] geöffnete Dokumente sind von diesen Einstellungen nicht betroffen.|  
|Drucker|Änderungen an den Anzeigeeinstellungen für Schriftart, Größe und Farbe für den Drucker wirken sich auf die Darstellung von Text in gedruckten Dokumenten aus.<br /><br /> Tipp: Bei Bedarf können Sie eine andere Standardschriftart für den Druck als für die Anzeige im Text-Editor auswählen. Das kann sehr hilfreich sein, wenn Sie Code ausdrucken, der Ein-Byte- und Doppelbyte-Zeichen enthält.|  
|[Alle Texttoolfenster **]**|Änderungen an den Anzeigeeinstellungen für Schriftart, Größe und Farbe für dieses Element wirken sich auf die Darstellung von Text in Toolfenstern aus, die in [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]über Ausgabebereiche verfügen. Zum Beispiel Ausgabefenster, TextResults-Fenster usw.<br /><br /> Hinweis: Änderungen am Text von [Alle Texttoolfenster]-Elementen werden nicht in der Sitzung wirksam, in der Sie sie vornehmen. Solche Änderungen können Sie auswerten, indem Sie eine andere Instanz von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]öffnen.|  
|Fenster "Suchergebnisse"|Änderungen an den Anzeigeeinstellungen für Schriftart, Größe und Farbe für dieses Element wirken sich auf die Darstellung von Text im Fenster „Suchergebnisse“ (FindResults) aus.|  
|Ausgabefenster|Änderungen an den Anzeigeeinstellungen für Schriftart, Größe und Farbe für dieses Element wirken sich auf die Darstellung von Text im Ausgabefenster aus.|  
|Rasterergebnisse|Änderungen an den Anzeigeeinstellungen für Schriftart, Größe und Farbe für dieses Element wirken sich auf die Darstellung von Text im Bereich **Rasterergebnisse** des Fensters „Abfrage“ aus.|  
|Ausführungsplan|Änderungen an den Anzeigeeinstellungen für Schriftart, Größe und Farbe für dieses Element wirken sich auf die Darstellung von Text im Ausführungsplan von [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Abfragen sowie Abfragen von [!INCLUDE[ssEW](../../includes/ssew-md.md)] aus.|  
|Textergebnis|Änderungen an den Anzeigeeinstellungen für Schriftart, Größe und Farbe für dieses Element wirken sich auf die Darstellung von Text im Bereich **Textergebnisse** des Fensters „Abfrage“ aus.|  
|Business Intelligence-Designer|Änderungen an den Anzeigeeinstellungen für Schriftart, Größe und Farbe für dieses Element wirken sich auf die Darstellung von Text im Fenster „Business Intelligence-Designer“ aus.|  
  
 **Standard verwenden**  
 Die Schaltfläche **Standard verwenden** setzt den Wert für die Standardschriftart- und -farbwerte des Listenelements zurück, das Sie aus der Liste **Einstellungen anzeigen für** ausgewählt haben.  
  
 **Schriftart (Fett bedeutet mit fester Breite formatiert)**  
 Führt alle Schriftarten auf, die auf Ihrem System installiert sind. Wenn diese Dropdownliste erstmalig geöffnet wird, ist die aktuelle Schriftart für das Element ausgewählt, das Sie aus der Liste **Einstellungen anzeigen für** ausgewählt haben. Feste Schriftarten – die im Editor einfacher auszurichten sind - werden in Fettschrift angezeigt.  
  
 **Größe**  
 Führt die verfügbaren Schriftgrade für die ausgewählte Schriftart auf. Die Änderung des Schriftgrades der Schriftart wirkt sich auf alle Einträge in der Liste **Elemente anzeigen** für ein unter **Einstellungen anzeigen für** ausgewähltes Element aus.  
  
 **Elemente anzeigen**  
 Führt die Elemente auf, für die Sie die Vordergrund- und Hintergrundfarbe ändern können.  
  
> [!NOTE]  
>  Das Standardelement für die Anzeige ist Text. Anzeigeelementen des Typs Text zugewiesene Eigenschaften werden von Eigenschaften, die anderen Anzeigeelementen zugewiesen wurden, überschrieben. Wenn Sie **Text** beispielsweise die Farbe Blau und Bezeichnern die Farbe Grün zuweisen, werden alle Bezeichner in grüner Farbe angezeigt. In diesem Beispiel überschreiben die Eigenschaften für Bezeichner die Eigenschaften für Text.  
  
 Zu den Anzeigeelementen gehören unter anderem:  
  
-   Indikatorrand: Der Rand auf der linken Seite des Code-Editors, auf dem Breakpoints und Lesezeichensymbole angezeigt werden.  
  
-   Reduzierbarer Text: Ein Block mit Text oder Code, der innerhalb des Code-Editors (nur XML) ein- bzw. ausgeblendet werden kann.  
  
 **Elementvordergrund**  
 Führt die verfügbaren Farben auf, die Sie für den Vordergrund des unter **Elemente anzeigen**ausgewählten Elements auswählen können. Weil einige Elemente in Beziehung zueinander stehen, sollte ein einheitliches Anzeigeschema beibehalten werden. Beispielsweise wird bei Änderung der Vordergrundfarbe von Text auch die Vordergrundfarbe für Elemente des Typs Zeichenfolge geändert.  
  
 **Custom**  
 Zeigt das Dialogfeld **Farbe** an, in dem Sie für das in der Liste **Elemente anzeigen** ausgewählte Element eine benutzerdefinierte Farbe festlegen können.  
  
> [!NOTE]  
>  Ihre Möglichkeiten, benutzerdefinierte Farben zu definieren, werden möglicherweise durch die Farbeinstellungen für Ihr Computerdisplay eingeschränkt. Wenn für Ihren Computer beispielsweise die Anzeige von 256 Farben festgelegt ist und Sie im Dialogfeld **Farbe** eine benutzerdefinierte Farbe auswählen, wird von [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] aus der Liste **Grundfarben** als Standardwert die Farbe ausgewählt, die der benutzerdefinierten Farbe am nächsten kommt. Außerdem wird im Dialogfeld **Farbe** die Farbe Schwarz angezeigt.  
  
 **Elementhintergrund**  
 Stellt eine Farbpalette bereit, aus der Sie für das in der Liste **Elemente anzeigen**ausgewählte Element eine Hintergrundfarbe auswählen können. Weil einige Elemente in Beziehung zueinander stehen, sollte ein einheitliches Anzeigeschema beibehalten werden. Beispielsweise wird bei Änderung der Hintergrundfarbe von Text auch die Hintergrundfarbe für Elemente des Typs SQL-Zeichenfolge geändert.  
  
 **Benutzerdefiniert**  
 Zeigt das Dialogfeld **Farbe** an, in dem Sie für das in der Liste **Elemente anzeigen** ausgewählte Element eine benutzerdefinierte Farbe festlegen können.  
  
 **Fett**  
 Aktivieren Sie dieses Kontrollkästchen, wenn der Text ausgewählter Anzeigeelemente in Fettschrift angezeigt werden soll. Text in Fettschrift ist in einem Editor einfacher zu identifizieren.  
  
 **Beispiel**  
 Zeigt ein Beispiel für den Schriftschnitt, den Schriftgrad und das Farbschema für die unter **Einstellungen anzeigen für** und **Elemente anzeigen**ausgewählten Werte an. In diesem Textfeld können Sie beim Ausprobieren der verschiedenen Formatierungsoptionen eine Vorschau der Ergebnisse anzeigen.  
  
## <a name="see-also"></a>Siehe auch  
 [Farbcodierung im Abfrage-Editor](../../relational-databases/scripting/color-coding-in-query-editors.md)   
 [Optionen &#40;Text-Editor: Registerkarte ' Editor ' und Statusleiste&#41;](../../database-engine/options-text-editor-editor-tab-and-status-bar-page.md)  
  
  
