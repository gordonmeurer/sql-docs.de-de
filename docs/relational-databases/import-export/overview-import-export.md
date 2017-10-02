---
title: Importieren und Exportieren von Daten von SQL Server und Azure SQL-Datenbank | Microsoft-Dokumentation
ms.custom: 
ms.date: 09/12/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.translationtype: HT
ms.sourcegitcommit: 6e754198cf82a7ba0752fe8f20c3780a8ac551d7
ms.openlocfilehash: 3c41be0642b13b63367c5601b716b506808472e7
ms.contentlocale: de-de
ms.lasthandoff: 09/14/2017

---
# <a name="import-and-export-data-from-sql-server-and-azure-sql-database"></a>Importieren und Exportieren von Daten von SQL Server und Azure SQL-Datenbank
Sie können eine Vielzahl von Methoden zum Importieren und Exportieren von Daten von SQL Server und Azure SQL-Datenbank verwenden. Zu diesen Methoden zählen Transact-SQL-Anweisungen, Befehlszeilentools und Assistenten.

Sie können Daten ebenfalls in einer Vielzahl von Dateiformaten importieren und exportieren. Zu diesen Formaten zählen Flatfiles, Excel, gängige relationale Datenbanken und verschiedene Clouddienste.

## <a name="methods-for-importing-and-exporting-data"></a>Methoden für den das Importieren und Exportieren von Daten

### <a name="use-transact-sql-statements"></a>Verwenden von Transact-SQL-Anweisungen
Sie können Daten mit den `BULK INSERT`- oder `OPENROWSET(BULK...)`-Befehlen importieren. In der Regel führen Sie diese Befehle in SQL Server Management Studio (SSMS) aus. Weitere Informationen finden Sie unter [Importieren von Massendaten mithilfe von BULK INSERT oder OPENROWSET(BULK...)](import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md).

### <a name="use-bcp-from-the-command-prompt"></a>Verwenden von BCP über die Eingabeaufforderung
Sie können Daten mit dem Hilfsprogramm für BCP-Befehlszeilen importieren und exportieren. Weitere Informationen finden Sie unter [Importieren und Exportieren von Massendaten mithilfe des Hilfsprogramms BCP](import-bulk-data-by-using-bulk-insert-or-openrowset-bulk-sql-server.md).

### <a name="use-the-sql-server-import-and-export-wizard"></a>Verwenden des SQL Server-Import/Export-Assistenten
Mit dem SQL Server-Import/Export-Assistenten können Sie Daten von einer Vielzahl von Quellen und Zielen importieren und exportieren. SQL Server Integration Services (SSIS) oder SQL Server Data Tools (SSDT) muss installiert sein, damit Sie den Assistenten verwenden können. Weitere Informationen finden Sie unter [Importieren und Exportieren von Daten mit dem SQL Server-Import/Export-Assistenten](../../integration-services/import-export-data/import-and-export-data-with-the-sql-server-import-and-export-wizard.md).

### <a name="design-your-own-import-or-export"></a>Entwerfen von eigenen Importen und Exporten
Wenn Sie einen benutzerdefinierten Datenimport entwerfen möchten, können Sie eine der folgenden Funktionen oder Dienste verwenden:
-   SQL Server Integration Services Weitere Informationen finden Sie unter [SQL Server Integration Services](../../integration-services/sql-server-integration-services.md).
-   Azure Data Factory Weitere Informationen finden Sie unter [Einführung in Azure Data Factory](https://docs.microsoft.com/azure/data-factory/data-factory-introduction).

## <a name="data-formats-for-import-and-export"></a>Dateiformate für den Import und Export

### <a name="supported-formats"></a>Unterstützte Formate

Sie können Daten von Flatfiles oder einer Vielzahl von anderen Dateiformaten, relationalen Datenbanken und Clouddiensten importieren und exportieren. Weitere Informationen zu diesen Optionen für bestimmte Tools finden Sie in den folgenden Themen:
-   Informationen zum SQL Server-Import/Export-Assistenten finden Sie unter [Connect to Data Sources with the SQL Server Import and Export Wizard (Herstellen einer Verbindung zu Datenquellen mit dem SQL Server-Import/Export-Assistenten)](../../integration-services/import-export-data/connect-to-data-sources-with-the-sql-server-import-and-export-wizard.md).
-   Informationen zu SQL Server Integration Services finden Sie unter [Integration Services-Verbindungen (SSIS)](../../integration-services/connection-manager/integration-services-ssis-connections.md).
-   Informationen zu Azure Data Factory finden Sie unter [Azure Data Factory-Connectors](https://docs.microsoft.com/en-us/azure/data-factory/data-factory-amazon-redshift-connector).

### <a name="commonly-used-data-formats"></a>Häufig verwendete Dateiformate

Für häufig verwendete Dateiformate sind spezielle Überlegungen und Beispiele verfügbar. Weitere Informationen zu diesen Dateiformaten finden Sie in den folgenden Themen:
-   Weitere Informationen zu Excel finden Sie unter [Import from Excel (Importieren von Excel)](import-data-from-excel-to-sql.md).
-   Weitere Informationen zu JSON finden Sie unter [Importieren von JSON-Dokumenten](../json/import-json-documents-into-sql-server.md).
-   Weitere Informationen zu XML finden Sie unter [Importieren und Exportieren von XML-Dokumenten](examples-of-bulk-import-and-export-of-xml-documents-sql-server.md).
-   Weitere Informationen zu Azure Blob Storage finden Sie unter [Importieren und Exportieren von Azure Blob Storage](examples-of-bulk-access-to-data-in-azure-blob-storage.md).

## <a name="next-steps"></a>Nächste Schritte
Verwenden Sie den SQL Server-Import/Export-Assistenten, wenn Sie nicht sicher sind, welche Schritte Sie beim Importieren oder Exportieren zuerst durchführen sollen. Eine kurze Einführung finden Sie unter [Erste Schritte mit diesem einfachen Beispiel des Import/Export-Assistenten](../../integration-services/import-export-data/get-started-with-this-simple-example-of-the-import-and-export-wizard.md).
