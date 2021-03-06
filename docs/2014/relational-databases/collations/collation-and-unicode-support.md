---
title: Sortierung und Unicode-Unterstützung | Microsoft-Dokumentation
ms.custom: ''
ms.date: 07/17/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- binary collations [SQL Server]
- expression-level collations [SQL Server]
- Windows collations [SQL Server]
- globalization [SQL Server], about globalization
- supplementary character support
- code pages [SQL Server], about code pages
- collations [SQL Server], about collations
- Unicode [SQL Server], collations
- database-level collations [SQL Server]
- reading order
- column-level collations
- locales [SQL Server], about locales
- locales [SQL Server]
- code pages [SQL Server]
- SQL Server collations
- server-level collations [SQL Server]
ms.assetid: 92d34f48-fa2b-47c5-89d3-a4c39b0f39eb
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7f313854119094b4407dc8bf4f6e62fdf7a31677
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/02/2018
ms.locfileid: "48126530"
---
# <a name="collation-and-unicode-support"></a>Collation and Unicode Support
  Sortierungen in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bieten Sortierregeln und die Berücksichtigung von Groß-/Kleinschreibung und Akzenten für die Daten. Sortierungen, mit denen, Zeichen-Datentypen wie z. B. `char` und `varchar` geben die Codeseite und die entsprechenden Zeichen, die für diesen Datentyp dargestellt werden können. Bei der Installation einer neuen Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], bei der Wiederherstellung einer Datenbanksicherung oder bei der Verbindung von Servern mit Clientdatenbanken ist es wichtig, dass Sie die Gebietsschemaanforderungen, die Sortierreihenfolge und das Verhalten in Bezug auf die Groß-/Kleinschreibung und Akzente der Daten kennen, mit denen Sie arbeiten. Informationen zum Auflisten von Sortierungen, die in Ihrer [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Instanz verfügbar sind, finden Sie unter [sys.fn_helpcollations &#40;Transact-SQL&#41;](/sql/relational-databases/system-functions/sys-fn-helpcollations-transact-sql).  
  
 Wenn Sie eine Sortierung für den Server, die Datenbank, die Spalte oder den Ausdruck auswählen, weisen Sie den Daten bestimmte Merkmale zu, die Auswirkungen auf die Ergebnisse vieler Datenbankvorgänge haben. Wenn Sie beispielsweise eine Abfrage mit ORDER BY erstellen, kann die Sortierreihenfolge des Resultsets von der Sortierung abhängen, die für die Datenbank gilt oder die in einer COLLATE-Klausel auf Ausdrucksebene der Abfrage vorgegeben ist.  
  
 Zur optimalen Verwendung der Sortierungsunterstützung in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ist es erforderlich, die in diesem Thema beschriebenen Begriffe zu verstehen und zu wissen, wie sie mit den Eigenschaften der Daten in Zusammenhang stehen.  
  
  
###  <a name="Collation_Defn"></a> Sortierung  
 Eine Sortierung gibt die Bitmuster an, die die jeweiligen Zeichen in einem Datensatz darstellen. Sortierungen legen außerdem die Regeln fest, nach denen Daten sortiert und verglichen werden. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützt das Speichern von Objekten mit verschiedenen Sortierungen in einer Datenbank. Bei Nicht-Unicode-Spalten gibt die Sortierungseinstellung die Codepage für die Daten und die Zeichen an, die dargestellt werden können. Daten, die zwischen Nicht-Unicode-Spalten verschoben werden, müssen jedoch von der Quellcodepage in die Zielcodepage konvertiert werden.  
  
 [!INCLUDE[tsql](../../includes/tsql-md.md)] -Anweisungsergebnisse können unterschiedlich sein, wenn die Anweisung im Kontext verschiedener Datenbanken ausgeführt wird, die jeweils andere Sortierungseinstellungen haben. Wenn möglich, sollte in Unternehmen eine standardisierte Sortierung verwendet werden. Auf diese Weise müssen Sie die Sortierung nicht explizit für jedes Zeichen oder jeden Unicode-Ausdruck angeben. Bei Objekten mit abweichenden Sortierungs- oder Codepageeinstellungen codieren Sie Ihre Abfragen so, dass diese den Regeln der Sortierungspriorität entsprechen. Weitere Informationen finden Sie unter [Rangfolge der Sortierungen (Transact-SQL)](/sql/t-sql/statements/collation-precedence-transact-sql).  
  
 Die einer Sortierung zugeordneten Optionen sind die Berücksichtigung von Groß-/Kleinschreibung, Akzenten, Kana und Breite. Diese Optionen werden angegeben, indem sie an den Sortierungsnamen angefügt werden. Beispiel: Bei der Sortierung `Japanese_Bushu_Kakusu_100_CS_AS_KS_WS` wird nach Groß-/Kleinschreibung, nach Akzent, Kana und Breite unterschieden. In der folgenden Tabelle wird das diesen Optionen zugeordnete Verhalten beschrieben.  
  
|Option|Description|  
|------------|-----------------|  
|Unterscheidung nach Groß-/Kleinschreibung (_CS)|Unterscheidet zwischen Groß- und Kleinbuchstaben. Wenn diese Option ausgewählt ist, stehen Kleinbuchstaben in der Sortierreihenfolge vor ihren entsprechenden Großbuchstaben. Wenn diese Option nicht aktiviert wird, wird bei der Sortierung die Groß-/Kleinschreibung nicht beachtet. D. h. SQL Server betrachtet die groß- und die kleingeschriebenen Versionen von Buchstaben für Sortierzwecke als identisch. Sie können die Nichtunterscheidung nach Groß-/Kleinbuchstaben durch Angeben von "_CI" explizit auswählen.|  
|Unterscheidung nach Akzent (_AS)|Unterscheidet zwischen Zeichen mit Akzent und Zeichen ohne Akzent. Beispielsweise ist 'a' nicht mit 'ấ' identisch. Wenn diese Option nicht aktiviert wird, werden bei der Sortierung Akzente nicht beachtet. D. h. SQL Server betrachtet die Versionen von Buchstaben mit und ohne Akzent für Sortierzwecke als identisch. Sie können die Nichtunterscheidung nach Akzent durch Angeben von "_AI" explizit auswählen.|  
|Unterscheidung nach Kana (_KS)|Unterscheidet zwischen den zwei Arten japanischer Kana-Zeichen: Hiragana und Katakana. Wenn diese Option nicht aktiviert wird, wird bei der Sortierung Kana nicht beachtet. D. h. SQL Server unterscheidet bei der Sortierung nicht zwischen Hiragana- und Katakana-Zeichen. Das Weglassen dieser Option ist die einzige Möglichkeit, die Nichtbeachtung von Kana anzugeben.|  
|Unterscheidung nach Breite (_WS)|Unterscheidet zwischen Zeichen halber Breite und Zeichen normaler Breite. Wenn diese Option nicht ausgewählt ist, betrachtet SQL Server die Darstellung in halber Breite und in normaler Breite desselben Zeichens für Sortierzwecke als identisch. Das Weglassen dieser Option ist die einzige Möglichkeit, die Nichtbeachtung der Breite anzugeben.|  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] unterstützt die folgenden Sortierungssätze:  
  
 Windows-Sortierungen  
 Windows-Sortierungen definieren Regeln zum Speichern von Zeichendaten, die auf dem zugehörigen Windows-Systemgebietsschema basieren. Bei einer Windows-Sortierung wird der Vergleich der Nicht-Unicode-Daten implementiert, indem derselbe Algorithmus wie bei Unicode-Daten verwendet wird. Die grundlegenden Regeln für Windows-Sortierreihenfolgen geben an, welches Alphabet oder welche Sprache verwendet wird, wenn Wörterbuchsortierung angewendet wird. Zudem geben die Regeln die Codepage an, die zum Speichern von Nicht-Unicode-Zeichendaten verwendet wird. Sowohl die Unicode- als auch die Nicht-Unicode-Sortierung sind kompatibel mit Zeichenfolgenvergleichen in einer bestimmten Version von Windows. Dadurch wird die Konsistenz der Datentypen in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ermöglicht. Außerdem erhalten Entwickler so die Möglichkeit, Zeichenfolgen in ihren Anwendungen mithilfe der gleichen Regeln zu sortieren, die auch in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] verwendet werden. Weitere Informationen finden Sie unter [Name der Windows-Sortierung &#40;Transact-SQL&#41;](/sql/t-sql/statements/windows-collation-name-transact-sql).  
  
 Binäre Sortierungen  
 Binäre Sortierungen sortieren Daten basierend auf der Reihenfolge codierter Werte, die vom Gebietsschema und Datentyp definiert werden. Dabei wird die Groß- und Kleinschreibung beachtet. Eine binäre Sortierung in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] definiert das zu verwendende Gebietsschema sowie die zu verwendende ANSI-Codepage. Dies erzwingt eine binäre Sortierreihenfolge. Da binäre Sortierungen relativ einfach sind, tragen sie dazu bei, die Anwendungsleistung zu verbessern. Bei Nicht-Unicode-Datentypen basieren Datenvergleiche auf den in der ANSI-Codepage definierten Codepunkten. Bei Unicode-Datentypen basieren Datenvergleiche auf den Unicode-Codepunkten. Bei binären Sortierungen von Unicode-Datentypen wird das Gebietsschema bei Datensortierungen nicht berücksichtigt. Beispielsweise führen Latin_1_General_BIN und Japanese_BIN bei Unicode-Daten zu den gleichen Sortierergebnissen.  
  
 Es gibt zwei Arten von binären Sortierungen in [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]; die älteren `BIN`-Sortierungen und die neueren `BIN2`-Sortierungen. In einer `BIN2`-Sortierung werden alle Zeichen entsprechend ihren Codepunkten sortiert. In einer `BIN`-Sortierung wird nur der erste Buchstabe nach Codepunkt sortiert, die verbleibenden Zeichen werden entsprechend ihren Bytewerten sortiert. (Da die Intel Plattform eine Little-Endian-Architektur aufweist, werden Unicode-Zeichen immer mit vertauschten Bytes gespeichert.)  
  
 SQL Server-Sortierungen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Sortierungen (SQL_*) sind hinsichtlich der Sortierreihenfolge mit älteren Versionen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]kompatibel. Die Wörterbuch-Sortierungsregeln für Nicht-Unicode-Daten sind nicht kompatibel mit den vom Betriebssystem Windows bereitgestellten Sortierroutinen. Das Sortieren von Unicode-Daten ist jedoch kompatibel mit einer bestimmten Version der Windows-Sortierregeln. Da [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Sortierungen unterschiedliche Vergleichsregeln für Nicht-Unicode- und Unicode-Daten verwenden, werden bei Vergleichen derselben Daten, je nach dem zugrunde liegenden Datentyp, unterschiedliche Ergebnisse angezeigt. Weitere Informationen finden Sie unter [Name der SQL Server-Sortierung &#40;Transact-SQL&#41;](/sql/t-sql/statements/sql-server-collation-name-transact-sql).  
  
> [!NOTE]  
>  Wenn Sie eine englischsprachige Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aktualisieren, können Sie [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]-Sortierungen (SQL_*) angeben, die mit vorhandenen Instanzen von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] kompatibel sein sollen. Da die Standardsortierung einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] während des Setups festgelegt wird, geben Sie unbedingt die Sortierungseinstellungen in den folgenden Fällen sorgfältig an:  
>   
>  -   Der Anwendungscode ist abhängig vom Verhalten der vorherigen [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Sortierungen.  
> -   Sie müssen Zeichendaten speichern, die mehrere Sprachen wiedergeben.  
  
 Das Festlegen von Sortierungen wird bei einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]für die folgenden Ebenen unterstützt:  
  
 Sortierungen auf Serverebene  
 Die Standardserversortierung wird während des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Setups festgelegt und außerdem als Standardsortierung der Systemdatenbanken und aller Benutzerdatenbanken vorgegeben. Beachten Sie, dass Nur-Unicode-Sortierungen während des [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Setups nicht ausgewählt werden können, da sie nicht als Sortierungen auf Serverebene unterstützt werden.  
  
 Nach dem Zuordnen einer Sortierung zum Server können Sie die Sortierung nur ändern, indem Sie alle Datenbankobjekte und -daten exportieren, die `master`-Datenbank erneut erstellen und alle Datenbankobjekte und -daten importieren. Statt die Standardsortierung einer Instanz von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]zu ändern, können Sie die gewünschte Sortierung auch beim Erstellen einer neuen Datenbank oder Datenbankspalte angeben.  
  
 Sortierungen auf Datenbankebene  
 Beim Anlegen oder Ändern einer Datenbank können Sie die Standardsortierung der Datenbank mithilfe der COLLATE-Klausel der CREATE DATABASE- oder ALTER DATABASE-Anweisung angeben. Wenn keine Sortierung angegeben wird, wird die Datenbank der Serversortierung zugeordnet.  
  
 Sie können die Sortierung von Systemdatenbanken nur ändern, indem Sie die Sortierung für den Server ändern.  
  
 Die Datenbanksortierung wird für alle Metadaten in der Datenbank verwendet und ist der Standard für alle Zeichenfolgenspalten, temporären Objekte, Variablennamen und anderen in der Datenbank verwendeten Zeichenfolgen. Wenn Sie die Sortierung einer Benutzerdatenbank ändern, treten möglicherweise Sortierungskonflikte auf, wenn Abfragen in der Datenbank auf temporäre Tabellen zugreifen. Temporäre Tabellen werden immer gespeichert, der `tempdb` Systemdatenbank, die die Sortierung für die Instanz verwendet wird. Abfragen, die Zeichendaten aus der Benutzerdatenbank und `tempdb` vergleichen, schlagen möglicherweise fehl, wenn die Sortierungen einen Konflikt beim Auswerten der Zeichendaten verursachen. Sie können dieses Problem umgehen, wenn Sie die COLLATE-Klausel in der Abfrage angeben. Weitere Informationen finden Sie unter [COLLATE &#40;Transact-SQL&#41;](/sql/t-sql/statements/collations).  
  
 Sortierungen auf Spaltenebene  
 Beim Erstellen oder Ändern einer Tabelle können Sie mithilfe der COLLATE-Klausel Sortierungen für alle Zeichenfolgenspalten angeben. Wenn keine Sortierung angegeben ist, wird der Spalte die Standardsortierung der Datenbank zugewiesen.  
  
 Sortierungen auf Ausdrucksebene  
 Sortierungen auf Ausdrucksebene werden zum Zeitpunkt der Ausführung einer Anweisung festgelegt. Sie haben Auswirkungen auf die Art und Weise, wie ein Resultset zurückgegeben wird. Somit können die ORDER BY-Sortierergebnisse gebietsschemaspezifisch sein. Implementieren Sie mithilfe einer COLLATE-Klausel, die folgendermaßen aussehen kann, Sortierungen auf Ausdrucksebene:  
  
```  
SELECT name FROM customer ORDER BY name COLLATE Latin1_General_CS_AI;  
```  
  
  
###  <a name="Locale_Defn"></a> Gebietsschema  
 Ein Gebietsschema ist ein Satz von Informationen, die einem Ort oder einer Kultur zugeordnet sind. Es kann Name und Bezeichner der gesprochenen Sprache, die Schrift, die zum Schreiben dieser Sprache verwendet wird, sowie kulturelle Konventionen enthalten. Sortierungen können einem oder mehreren Gebietsschemas zugeordnet sein. Weitere Informationen finden Sie unter [Von Microsoft zugewiesene Gebietsschemabezeichner (LCIDs)](http://msdn.microsoft.com/goglobal/bb964664.aspx).  
  
  
###  <a name="Code_Page_Defn"></a> Code Page  
 Eine Codepage ist ein geordneter Satz von Zeichen in einem vorgegebenen Skript, in dem ein numerischer Index, oder Codepunktwert, mit jedem Zeichen verbunden ist. Eine Codepage in Windows wird in der Regal als *Zeichensatz* oder *charset*bezeichnet. Codepages werden zur Unterstützung der Zeichensätze und Tastaturlayouts verschiedener Windows-Systemgebietsschemas verwendet.  
  
  
###  <a name="Sort_Order_Defn"></a> Sort Order  
 Die Sortierreihenfolge gibt an, wie Datenwerte sortiert werden. Dies wirkt sich auf die Ergebnisse des Datenvergleichs aus. Daten werden mithilfe von Sortierungen sortiert, die mit Indizes optimiert werden können.  
  
  
##  <a name="Unicode_Defn"></a> Unicode-Unterstützung  
 Unicode ist ein Standard zum Zuordnen von Codepunkten zu Zeichen. Da dieser Standard entwickelt wurde, um alle Zeichen aus allen Sprachen der Welt zu unterstützen, besteht keine Notwendigkeit für unterschiedliche Codepages zur Handhabung der verschiedenen Zeichensätze. Wenn Sie Zeichendaten, die mehrere Sprachen darstellen speichern, verwenden Sie immer Unicode-Datentypen (`nchar`, `nvarchar`, und `ntext`) anstelle der nicht-Unicode-Datentypen (`char`, `varchar`, und `text`).  
  
 Nicht-Unicode-Datentypen verfügen über umfassende Einschränkungen. Das liegt daran, dass ein Nicht-Unicode-Computer auf die Verwendung einer einzelnen Codepage beschränkt ist. Es kann sein, dass Sie mit Unicode eine bessere Systemleistung erzielen, da weniger Codepagekonvertierungen erforderlich sind. Unicode-Sortierungen müssen auf der Datenbank-, Spalten- oder Ausdrucksebene einzeln ausgewählt werden, weil sie auf Serverebene nicht unterstützt werden.  
  
 Die Codepages, die ein Client verwendet, werden durch die Einstellungen des Betriebssystems bestimmt. Verwenden Sie zum Festlegen von Clientcodepages unter Windows die Option **Ländereinstellungen** in der Systemsteuerung.  
  
 Wenn Sie Daten von einem Server auf einen Client verschieben, wird die Serversortierung von älteren Clienttreibern möglicherweise nicht erkannt. Dies kann passieren, wenn Sie Daten von einem Unicode-Server auf einen Nicht-Unicode-Client verschieben. Die beste Möglichkeit, dieses Problem zu beheben, besteht in einem Update des Clientbetriebssystems, wobei die zugrunde liegenden Systemsortierungen aktualisiert werden. Wenn auf dem Client Datenbankclient-Software installiert ist, sollten Sie ein Serviceupdate der Datenbankclient-Software in Erwägung ziehen.  
  
 Sie können auch versuchen, eine andere Sortierung für die Daten auf dem Server zu verwenden. Wählen Sie eine Sortierung aus, die einer Codepage auf dem Client zugeordnet werden kann.  
  
 Um die verfügbaren UTF-16-Sortierungen in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]zu verwenden und das Suchen und Sortieren einiger Unicode-Zeichen zu verbessern, können Sie eine der `_SC` -Sortierungen mit ergänzenden Zeichen (nur Windows-Sortierungen) auswählen.  
  
 Zum Abwägen der Vor- und Nachteile von Unicode- und Nicht-Unicode-Datentypen müssen Sie das Szenario testen und die Leistungsunterschiede in Ihrer Umgebung messen. Es ist ratsam, die Sortierung zu standardisieren, die für die Systeme in Ihrem Unternehmen verwendet wird, und so weit wie möglich Unicode-Server und -Clients bereitzustellen.  
  
 In vielen Fällen interagiert [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mit anderen Servern oder Clients, und Ihr Unternehmen verwendet möglicherweise mehrere Standards für den Datenzugriff zwischen Anwendungen und Serverinstanzen. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] -Clients stellen einen der beiden Haupttypen dar:  
  
-   **Unicode-Clients** , die OLE DB und Open Database Connectivity (ODBC) Version 3.7 oder höher verwenden.  
  
-   **Nicht-Unicode-Clients** , die DB Library und ODBC Version 3.6 oder früher verwenden.  
  
 Die folgende Tabelle enthält Informationen zur Verwendung mehrsprachiger Daten mit verschiedenen Kombinationen von Unicode- und Nicht-Unicode-Servern.  
  
|Server|Client|Vorteile oder Beschränkungen|  
|------------|------------|-----------------------------|  
|Unicode|Unicode|Da Unicode-Daten im gesamten System verwendet werden, verfügt dieses Szenario über die beste Systemleistung und den besten Schutz vor Beschädigung der abgerufenen Daten. Dies ist der Fall bei ActiveX Data Objects (ADO), OLE DB und ODBC Version 3.7 oder höher.|  
|Unicode|Nicht-Unicode|In diesem Szenario sind Einschränkungen oder Fehler beim Verschieben von Daten auf einen Clientcomputer möglich. Dies gilt besonders für Verbindungen zwischen einem Server, auf dem ein neueres Betriebssystem ausgeführt wird, und einem Client, auf dem eine ältere Version von [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]oder ein älteres Betriebssystem installiert ist. Die Unicode-Daten auf dem Server versuchen, eine Zuordnung zu einer entsprechenden Codeseite auf dem Nicht-Unicode-Client zu erstellen, um die Daten zu konvertieren.|  
|Nicht-Unicode|Unicode|Dies ist keine günstige Konfiguration bei der Verwendung mehrsprachiger Daten Sie sind nicht in der Lage, Unicode-Daten auf den Nicht-Unicode-Server zu schreiben. Es ist wahrscheinlich, dass Probleme auftreten, wenn Daten an Server gesendet werden, die von der Codepage des Servers nicht erfasst werden.|  
|Nicht-Unicode|Nicht-Unicode|Dieses Szenario ist bei mehrsprachigen Daten mit zahlreichen Beschränkungen verbunden. Sie können nur eine Codepage verwenden.|  
  
  
##  <a name="Supplementary_Characters"></a> Ergänzende Zeichen  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Stellt Datentypen bereit, z. B. `nchar` und `nvarchar` zum Speichern von Unicode-Daten. Bei diesen Datentypen wird Text im Format *UTF-16*codiert. Das Unicode Consortium hat jedem Zeichen einen eindeutigen Codepunkt zugeordnet, der einem Wert im Bereich 0x0000 bis 0x10FFFF entspricht. Die am häufigsten verwendeten Zeichen weisen Codepunktwerte auf, die im Arbeitsspeicher und auf dem Datenträger in ein 16-Bit-Wort passen. Zeichen mit Codepunktwerten, die größer als 0xFFFF sind, erfordern jedoch zwei aufeinanderfolgende 16-Bit-Wörter. Diese Zeichen werden als *ergänzende Zeichen*bezeichnet, und die beiden aufeinanderfolgenden 16-Bit-Wörter werden als *Ersatzpaare*bezeichnet.  
  
 Bei Verwendung ergänzender Zeichen:  
  
-   Ergänzende Zeichen können bei Sortier- und Vergleichsvorgängen für Sortierungsversionen ab 90 verwendet werden.  
  
-   Alle _100-Ebenen-Sortierungen unterstützen die linguistische Sortierung mit ergänzenden Zeichen.  
  
-   Ergänzende Zeichen werden für die Verwendung in Metadaten, beispielsweise in Namen von Datenbankobjekten, nicht unterstützt.  
  
-   Für die Datentypen `nchar`, `nvarchar` und `sql_variant` kann jetzt eine neue Familie von SC (Supplementary Characters)-Sortierungen verwendet werden, die in [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] eingeführt wurde. Beispiel: `Latin1_General_100_CI_AS_SC`, oder bei Verwenden einer japanischen Sortierung `Japanese_Bushu_Kakusu_100_CI_AS_SC`.  
  
     Das SC-Flag kann in folgenden Versionen angewendet werden:  
  
    -   Windows-Sortierungen der Version 90  
  
    -   Windows-Sortierungen der Version 100  
  
     Das SC-Flag kann nicht auf folgende Versionen angewendet werden:  
  
    -   Nicht versionierte Windows-Sortierungen der Version 80  
  
    -   Die binären Sortierungen BIN und BIN2  
  
    -   Die SQL*-Sortierungen  
  
 In der folgenden Tabelle wird das Verhalten einiger Zeichenfolgenfunktionen und Zeichenfolgenoperatoren verglichen, wenn diese ergänzende Zeichen mit und ohne SC-Sortierung verwenden.  
  
|Zeichenfolgenfunktion oder Operator|Mit SC-Sortierung|Ohne SC-Sortierung|  
|---------------------------------|--------------------------|-----------------------------|  
|[CHARINDEX](/sql/t-sql/functions/charindex-transact-sql)<br /><br /> [LEN](/sql/t-sql/functions/len-transact-sql)<br /><br /> [PATINDEX](/sql/t-sql/functions/patindex-transact-sql)|Das UTF-16-Ersatzzeichenpaar wird als einzelner Codepunkt betrachtet.|Das UTF-16-Ersatzzeichenpaar wird als zwei Codepunkte betrachtet.|  
|[LEFT](/sql/t-sql/functions/left-transact-sql)<br /><br /> [REPLACE](/sql/t-sql/functions/replace-transact-sql)<br /><br /> [REVERSE](/sql/t-sql/functions/reverse-transact-sql)<br /><br /> [RIGHT](/sql/t-sql/functions/right-transact-sql)<br /><br /> [SUBSTRING](/sql/t-sql/functions/substring-transact-sql)<br /><br /> [STUFF](/sql/t-sql/functions/stuff-transact-sql)|Diese Funktionen behandeln jedes Ersatzzeichenpaar als einzelnen Codepunkt und funktionieren wie erwartet.|Diese Funktionen können Ersatzzeichenpaare möglicherweise aufteilen und zu unerwarteten Ergebnissen führen.|  
|[NCHAR](/sql/t-sql/functions/nchar-transact-sql)|Gibt das Zeichen zurück, das dem angegebenen Unicode-Codepunktwert im Bereich 0 zu 0x10FFFF entspricht. Wenn der angegebene Wert im Bereich 0 bis 0xFFFF liegt, wird nur ein Zeichen zurückgegeben. Bei höheren Werten wird das entsprechende Ersatzzeichenpaar zurückgegeben.|Ein Wert größer als 0xFFFF gibt anstelle des entsprechenden Ersatzzeichens NULL zurück.|  
|[UNICODE](/sql/t-sql/functions/unicode-transact-sql)|Gibt einen UTF-16-Codepunkt im Bereich 0 bis 0x10FFFF zurück.|Gibt einen UCS-2-Codepunkt im Bereich 0 bis 0xFFFF zurück.|  
|[Einzelnes zu suchendes Zeichen](/sql/t-sql/language-elements/wildcard-match-one-character-transact-sql)<br /><br /> [Platzhalterzeichen - nicht zu suchende(s) Zeichen](/sql/t-sql/language-elements/wildcard-character-s-not-to-match-transact-sql)|Ergänzende Zeichen werden für alle Platzhaltervorgänge unterstützt.|Ergänzende Zeichen werden für diese Platzhaltervorgänge nicht unterstützt. Andere Platzhalteroperatoren werden unterstützt.|  
  
  
##  <a name="GB18030"></a> GB18030-Unterstützung  
 GB18030 ist ein separater Standard, der in der Volksrepublik China zur Codierung von chinesischen Schriftzeichen verwendet wird. In GB18030 können Zeichen 1, 2 oder 4 Bytes lang sein. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] bietet Unterstützung für GB18030-codierte Zeichen, indem diese erkannt werden, wenn Sie den Server von einer clientseitigen Anwendung erreichen, und in systemeigene Unicode-Zeichen konvertiert und als solche gespeichert werden. Nach ihrer Speicherung im Server werden diese Zeichen in allen nachfolgenden Operationen als Unicode-Zeichen behandelt. Sie können eine beliebige chinesische Sortierung verwenden. Empfohlen wird die aktuelle Version 100. Alle _100-Ebenen-Sortierungen unterstützen die linguistische Sortierung mit GB18030-Zeichen. Wenn die Daten ergänzende Zeichen (Ersatzpaare) enthalten, können Sie Such- und Sortiervorgänge mithilfe der in [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] verfügbaren SC-Sortierungen optimieren.  
  
  
##  <a name="Complex_script"></a> Unterstützung komplexer Skripts  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] kann das Eingeben, Speichern, Ändern und Anzeigen komplexer Skripts unterstützen. Zu komplexen Skripts gehören Folgende:  
  
-   Skripts, die sowohl die Kombination von Text von rechts nach links und Text von links nach rechts enthalten, als auch die Kombination von arabischem und englischem Text.  
  
-   Skripts, deren Zeichen die Form abhängig von ihrer Position ändern, oder abhängig davon, ob sie mit anderen Zeichen kombiniert werden, wie beispielsweise arabische, indische und thailändische Zeichen.  
  
-   Sprachen, wie beispielsweise Thailändisch, die ein internes Wörterbuch zum Erkennen von Wörtern erfordern, da keine Abstände zwischen den Wörtern vorhanden sind.  
  
 Datenbankanwendungen, die mit [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] interagieren, müssen über Steuerelemente verfügen, die komplexe Skripts unterstützen. Standardmäßige Windows-Formularsteuerelemente, die in verwaltetem Code erstellt werden, sind für komplexe Skripts aktiviert.  
  
  
##  <a name="Related_Tasks"></a> Verwandte Aufgaben  
  
|Task|Thema|  
|----------|-----------|  
|Beschreibt, wie die Sortierung der Instanz von SQL Server festgelegt oder geändert wird.|[Festlegen oder Ändern der Serversortierung](set-or-change-the-server-collation.md)|  
|Beschreibt, wie die Sortierung einer Benutzerdatenbank festgelegt oder geändert wird.|[Festlegen oder Ändern der Datenbanksortierung](set-or-change-the-database-collation.md)|  
|Beschreibt, wie die Sortierung einer Spalte in der Datenbank festgelegt oder geändert wird.|[Festlegen oder Ändern der Spaltensortierung](set-or-change-the-column-collation.md)|  
|Beschreibt, wie Sortierungsinformationen auf Server-, Datenbank- oder Spaltenebene zurückgegeben werden.|[Anzeigen von Sortierungsinformationen](view-collation-information.md)|  
|Beschreibt, wie Transact-SQL-Anweisungen geschrieben werden, die die Übertragung von einer Sprache in eine andere verbessern, oder wie mehrere Sprachen einfacher unterstützt werden.|[Schreiben internationaler Transact-SQL-Anweisungen](write-international-transact-sql-statements.md)|  
|Beschreibt, wie die Sprache von Fehlermeldungen und die bevorzugte Verwendungs- und Anzeigeweise von Datums-, Zeit-, und Währungsdaten geändert werden.|[Festlegen einer Sitzungssprache](set-a-session-language.md)|  
  
  
##  <a name="Related_Content"></a> Verwandte Inhalte  
 [Bewährte Vorgehensweisen zur Sortierungsänderung bei SQL Server](http://go.microsoft.com/fwlink/?LinkId=113891)  
  
 ["Bewährte Vorgehensweise zur Unicode-Migration bei SQL Server"](http://go.microsoft.com/fwlink/?LinkId=113890)  
  
 [Website des Unicode Consortium](http://go.microsoft.com/fwlink/?LinkId=48619)  
  
## <a name="see-also"></a>Weitere Informationen enthält auch die  
 [Contained Database Collations](../databases/contained-database-collations.md)   
 [Auswählen einer Sprache beim Erstellen eines Volltextindex](../search/choose-a-language-when-creating-a-full-text-index.md)   
 [fn_helpcollations (Transact-SQL)](https://msdn.microsoft.com/library/ms187963(SQL.130).aspx)  
  
  
