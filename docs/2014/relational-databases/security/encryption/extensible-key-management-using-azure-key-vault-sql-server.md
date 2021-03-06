---
title: Erweiterbare Schlüsselverwaltung mit Azure Key Vault (SQL Server) | Microsoft-Dokumentation
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: security
ms.topic: conceptual
helpviewer_keywords:
- EKM, with key vault
- TDE, EKM and key vault
- Extensible Key Management with key vault
- Key Management with key vault
- Transparent Data Encryption, using EKM and key vault
ms.assetid: 3efdc48a-8064-4ea6-a828-3fbf758ef97c
author: aliceku
ms.author: aliceku
manager: craigg
ms.openlocfilehash: 677da53a1bc27c4e64a91f04d242635fe2df4471
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 10/02/2018
ms.locfileid: "48192160"
---
# <a name="extensible-key-management-using-azure-key-vault-sql-server"></a>Erweiterbare Schlüsselverwaltung mit Azure Key Vault (SQL Server)
  Die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Connector für [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Azure Key Vault ermöglicht [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Verschlüsselung zu nutzen, den Azure Key Vault-Dienst als eine [Extensible Key Management &#40;EKM&#41; ](extensible-key-management-ekm.md) Anbieter zum Schutz der Verschlüsselungsschlüssel.  
  
 In diesem Thema:  
  
-   [Verwendungsmöglichkeiten für erweiterbare Schlüsselverwaltung](#Uses)  
  
-   [Schritt 1: Einrichten von Key Vault für die Verwendung durch SQL Server](#Step1)  
  
-   [Schritt 2: Installieren des SQL Server-Connectors](#Step2)  
  
-   [Schritt 3: Konfigurieren von SQL Server zur Verwendung von EKM-Anbieter für den Schlüsseltresor](#Step3)  
  
-   [Beispiel A: Transparente datenverschlüsselung mit einem asymmetrischen Schlüssel aus dem Schlüsseltresor](#ExampleA)  
  
-   [Beispiel B: Verschlüsseln von Sicherungen mit einem asymmetrischen Schlüssel aus dem Schlüsseltresor](#ExampleB)  
  
-   [Beispiel C: Verschlüsselung auf Spaltenebene mit einem asymmetrischen Schlüssel aus dem Schlüsseltresor](#ExampleC)  
  
##  <a name="Uses"></a> Verwendungsmöglichkeiten für erweiterbare Schlüsselverwaltung  
 Organisationen können die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Verschlüsselung zum Schutz sensibler Daten verwenden. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Verschlüsselung umfasst [Transparent Data Encryption &#40;TDE&#41;](transparent-data-encryption.md), [Verschlüsselung auf Spaltenebene](/sql/t-sql/functions/cryptographic-functions-transact-sql) (CLE) und [Sicherungsverschlüsselung](../../backup-restore/backup-encryption.md). In all diesen Fällen werden die Daten mit einem symmetrischen Datenverschlüsselungsschlüssel verschlüsselt. Der symmetrische Datenverschlüsselungsschlüssel wird außerdem geschützt durch Verschlüsselung mit einer Hierarchie von Schlüsseln, die in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]gespeichert sind. Sie können auch die EKM-Anbieterarchitektur ermöglicht [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , die Schlüssel zur Verschlüsselung von Daten zu schützen, indem Sie mit einem asymmetrischen Schlüssel, die außerhalb des [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in einem externen Kryptografieanbieter. Die Verwendung der Architektur des Anbieters für erweiterbare Schlüsselverwaltung stellt eine zusätzliche Sicherheitsebene dar und ermöglicht Unternehmen die getrennte Verwaltung von Schlüsseln und Daten.  
  
 Die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Connector für Azure Key Vault können [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] skalierbaren, leistungsfähigen und hochverfügbaren Key Vault-Dienst nutzen, als EKM-Anbieter für den Schutz des Verschlüsselungsschlüssels. Der schlüsseltresordienst kann verwendet werden, mit [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Installationen auf [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Azure Virtual Machines und auf lokalen Servern. Der Schlüsseltresordienst bietet auch die Option, genau gesteuerte und stark überwachte Hardwaresicherheitsmodule (HSMs) für ein höheres Maß an Schutz für asymmetrische Schlüssel zu verwenden. Weitere Informationen zum Schlüsseltresor finden Sie unter [Azure Key Vault](http://go.microsoft.com/fwlink/?LinkId=521401).  
  
 Die folgende Grafik enthält eine Zusammenfassung des Prozessablaufs der erweiterbaren Schlüsselverwaltung mit Schlüsseltresor. Die Nummern der Prozessschritte in der Grafik stimmen nicht mit den Nummern der Einrichtungsschritte, die auf die Grafik folgen, überein.  
  
 ![SQL Server-EKM mit Azure Key Vault](../../../database-engine/media/ekm-using-azure-key-vault.png "SQL Server EKM using the Azure Key Vault")  
  
##  <a name="Step1"></a> Schritt 1: Einrichten von Key Vault für die Verwendung durch SQL Server  
 Führen Sie die folgenden Schritte aus, um einen Schlüsseltresor für die Verwendung mit der [!INCLUDE[ssDEnoversion](../../../includes/ssdenoversion-md.md)] für den Schutz des Verschlüsselungsschlüssels einzurichten. Für die Organisation wird möglicherweise bereits ein Tresor verwendet. Bei ein Tresor nicht vorhanden ist, der Azure-Administrator in Ihrer Organisation, die vorgesehen ist, um die Verwaltung von kryptoschlüsseln können erstellen Sie einen Tresor einen asymmetrischen Schlüssel im Tresor generieren und anschließend autorisieren [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] zum Verwenden des Schlüssels. Machen Sie sich unter [Erste Schritte mit Azure Key Vault](http://go.microsoft.com/fwlink/?LinkId=521402)und der Referenz zu PowerShell- [Azure Key Vault-Cmdlets](http://go.microsoft.com/fwlink/?LinkId=521403) mit dem Schlüsseltresordienst vertraut.  
  
> [!IMPORTANT]  
>  Wenn Sie mehrere Azure-Abonnements verfügen, müssen Sie das Abonnement mit verwenden [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
1.  **Erstellen Sie einen Tresor:** Erstellen Sie einen Tresor nach der Anweisungen im Abschnitt **Erstellen eines Schlüsseltresors** in [Erste Schritte mit Azure Key Vault](http://go.microsoft.com/fwlink/?LinkId=521402). Notieren Sie den Namen des Tresors. In diesem Thema wird **ContosoKeyVault** als Schlüsseltresorname verwendet.  
  
2.  **Generieren Sie einen asymmetrischen Schlüssel im Tresor:** der asymmetrische Schlüssel im schlüsseltresor dient zum Schutz [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Verschlüsselungsschlüssel. Nur der öffentliche Teil des asymmetrischen Schlüssels verlässt jemals den Tresor, der private Teil wird nie vom Tresor exportiert. Alle kryptografischen Vorgänge mit dem asymmetrischen Schlüssel werden an den Azure-Schlüsseltresor delegiert und durch die Schlüsseltresorsicherheit geschützt.  
  
     Es gibt mehrere Möglichkeiten, wie Sie einen asymmetrischen Schlüssel generieren und im Tresor speichern können. Sie können einen Schlüssel extern generieren und den Schlüssel als PFX-Datei in den Tresor importieren. Oder Sie erstellen den Schlüssel mit den Schlüsseltresor-APIs direkt im Tresor.  
  
     Die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Connector erfordert asymmetrische Schlüssel nach 2048-Bit-RSA, und den Namen des Schlüssels können Sie nur die Zeichen "a – Z", "A – Z", "0-9", und "-". In diesem Dokument wird als Name des asymmetrischen Schlüssels **ContosoMasterKey**verwendet. Ersetzen Sie dies durch den eindeutigen Namen, den Sie für den Schlüssel verwenden.  
  
    > [!IMPORTANT]  
    >  Das Importieren des asymmetrischen Schlüssels wird für Produktionsszenarien dringend empfohlen, da der Administrator dann den Schlüssel in einem Schlüsselhinterlegungssystem hinterlegen kann. Wenn der asymmetrische Schlüssel im Tresor erstellt wird, kann er nicht hinterlegt werden, da der private Schlüssel nie den Tresor verlassen kann. Schlüssel zum Schützen wichtiger Daten sollten hinterlegt werden. Der Verlust eines asymmetrischen Schlüssels führt dazu, dass Daten dauerhaft nicht wiederhergestellt werden können.  
  
    > [!IMPORTANT]  
    >  Der Schlüsseltresor unterstützt mehrere Versionen desselben benannten Schlüssels. Schlüssel vom zu verwendende [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Connector sollte nicht Versionierung noch Rollover ausgeführt. Wenn der Administrator den Schlüssel für die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Verschlüsselung wieder verwenden möchte, sollte ein neuer Schlüssel mit einem anderen Namen im Tresor erstellt und zum Verschlüsseln des Datenverschlüsselungsschlüssels verwendet werden.  
  
     Weitere Informationen zum Importieren eines Schlüssels in den Tresor oder zum Erstellen eines Schlüssels im Schlüsseltresor (nicht empfohlen für Produktionsumgebungen) finden Sie im Abschnitt **Hinzufügen eines Schlüssels oder eines geheimen Schlüssels zum Schlüsseltresor** in [Erste Schritte mit Azure Key Vault](http://go.microsoft.com/fwlink/?LinkId=521402).  
  
3.  **Rufen Sie Azure Active Directory-Dienstprinzipale für SQL Server ab:** Wenn sich die Organisation für einen Microsoft Cloud-Dienst registriert, erhält sie ein Azure Active Directory. Erstellen Sie **Dienstprinzipale** in Azure Active Directory für [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] (zur Authentifizierung gegenüber Azure Active Directory) beim Zugriff auf den schlüsseltresor verwenden.  
  
    -   Eine **Dienstprinzipal** benötigt werden, indem eine [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Administrator während der Konfiguration auf den Tresor zugreifen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] , Verschlüsselung zu verwenden.  
  
    -   Eine andere **Dienstprinzipal** benötigt werden, indem die [!INCLUDE[ssDEnoversion](../../../includes/ssdenoversion-md.md)] zum Zugreifen auf den Tresor zum Entpacken verwendeten Schlüsseln [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Verschlüsselung.  
  
     Weitere Informationen zum Registrieren einer Anwendung und Generieren eines Dienstprinzipals finden Sie im Abschnitt **Registrieren einer Anwendung in Azure Active Directory** in [Erste Schritte mit Azure Key Vault](http://go.microsoft.com/fwlink/?LinkId=521402). Der Registrierungsprozess gibt eine **Anwendungs-ID** (auch bekannt als **CLIENT-ID**) und einen **Authentifizierungsschlüssel** (auch bekannt als **geheimer Schlüssel**) für jeden Azure Active Directory- **Dienstprinzipal**zurück. Bei der Verwendung in der `CREATE CREDENTIAL` -Anweisung wird der Bindestrich muss entfernt werden aus der **CLIENT-ID**. Notieren Sie diese für die Verwendung in den unten stehenden Skripts:  
  
    -   **Dienstprinzipal** für eine **sysadmin** -Anmeldung: **CLIENTID_sysadmin_login** und **SECRET_sysadmin_login**  
  
    -   **Dienstprinzipal** für die [!INCLUDE[ssDEnoversion](../../../includes/ssdenoversion-md.md)]: **CLIENTID_DBEngine** und **SECRET_DBEngine**.  
  
4.  **GRANT-Berechtigung für die Dienstprinzipale zum Zugriff auf den Schlüsseltresor:** sowohl die **CLIENTID_sysadmin_login** und **CLIENTID_DBEngineService Prinzipale** erfordern die **abrufen** , **Liste**, **WrapKey**, und **UnwrapKey** Berechtigungen im schlüsseltresor. Wenn Sie, zum Erstellen von Schlüsseln über beabsichtigen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] müssen Sie auch gewähren der **erstellen** -Berechtigung für Key Vault-Instanz.  
  
    > [!IMPORTANT]  
    >  Benutzer müssen mindestens über die Vorgänge **wrapKey** und **unwrapKey** für den Schlüsseltresor verfügen.  
  
     Weitere Informationen zum Erteilen von Berechtigungen für den Tresor finden Sie im Abschnitt **Autorisieren der Anwendung zum Verwenden des Schlüssels oder des geheimen Schlüssels** in [Erste Schritte mit Azure Key Vault](http://go.microsoft.com/fwlink/?LinkId=521402).  
  
     Links zur Dokumentation für Azure Key Vault  
  
    -   [Was ist Azure Key Vault?](http://go.microsoft.com/fwlink/?LinkId=521401)  
  
    -   [Erste Schritte mit Azure Key Vault](http://go.microsoft.com/fwlink/?LinkId=521402)  
  
    -   Referenz der PowerShell- [Azure Key Vault-Cmdlets](http://go.microsoft.com/fwlink/?LinkId=521403)  
  
##  <a name="Step2"></a> Schritt 2: Installieren des SQL Server-Connectors  
 Die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Connector heruntergeladen und installiert, indem Sie der Administrator die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Computer. Die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Connector steht als Download unter dem [Microsoft Download Center](http://go.microsoft.com/fwlink/p/?LinkId=521700).  Suchen Sie nach **SQL Server-Connector für Microsoft Azure Key Vault**. Überprüfen Sie die Details, Systemanforderungen und Installationsanweisungen, wählen Sie den Download des Connectors, und starten Sie die Installation mit **Ausführen**. Lesen Sie die Lizenzbedingungen, stimmen Sie ihnen zu, und setzen Sie den Vorgang fort.  
  
 In der Standardeinstellung der Connector installiert ist, auf **C:\Program Files\SQL Server Connector for Microsoft Azure Key Vault**. Dieser Speicherort kann während des Setups geändert werden. (Wenn Sie ihn ändern, passen Sie die unten angegebenen Skripts entsprechend an.)  
  
 Nach Abschluss der Installation ist Folgendes auf dem Computer installiert:  
  
-   **Microsoft.AzureKeyVaultService.EKM.dll**: Dies ist die EKM-Kryptografieanbieters DLL, die registriert werden muss [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] mithilfe der CREATE CRYPTOGRAPHIC PROVIDER-Anweisung.  
  
-   **Azure Key Vault SQL Server-Connector**: Dies ist ein Windows-Dienst, der dem kryptografischen Anbieter für erweiterbare Schlüsselverwaltung die Kommunikation mit dem Schlüsseltresor ermöglicht.  
  
 Die [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Connectorinstallation ermöglicht außerdem, optional auch Beispielskripts zum Herunterladen [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Verschlüsselung.  
  
##  <a name="Step3"></a> Schritt 3: Konfigurieren von SQL Server zur Verwendung von EKM-Anbieter für den Schlüsseltresor  
  
###  <a name="Permissions"></a> Berechtigungen  
 Das gesamte Verfahren erfordert die CONTROL SERVER-Berechtigung oder die Mitgliedschaft in der festen Serverrolle **sysadmin** . Bestimmte Aktionen erfordern die folgenden Berechtigungen:  
  
-   Zum Erstellen eines Kryptografieanbieters ist die CONTROL SERVER-Berechtigung oder die Mitgliedschaft in der festen Serverrolle **sysadmin** erforderlich.  
  
-   Zum Ändern einer Konfigurationsoption und Ausführen der RECONFIGURE-Anweisung muss Ihnen die ALTER SETTINGS-Berechtigung auf Serverebene erteilt worden sein. Die ALTER SETTINGS-Berechtigung ist in den festen Serverrollen **sysadmin** und **serveradmin** eingeschlossen.  
  
-   Zum Erstellen von Anmeldeinformationen ist die ALTER ANY CREDENTIAL-Berechtigung erforderlich.  
  
-   Zum Hinzufügen von Anmeldeinformationen zu einem Anmeldenamen ist die ALTER ANY LOGIN-Berechtigung erforderlich.  
  
-   Zum Erstellen eines asymmetrischen Schlüssels ist die CREATE ASYMMETRIC KEY-Berechtigung erforderlich.  
  
###  <a name="TsqlProcedure"></a> So konfigurieren Sie SQL Server zur Verwendung eines Kryptografieanbieters  
  
1.  Konfigurieren Sie die [!INCLUDE[ssDE](../../../includes/ssde-md.md)] für die Verwendung der erweiterbaren Schlüsselverwaltung, und registrieren (erstellen) Sie den Kryptografieanbieter in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
    ```  
    -- Enable advanced options.  
    USE master;  
    GO  
  
    sp_configure 'show advanced options', 1 ;  
    GO  
    RECONFIGURE ;  
    GO  
    -- Enable EKM provider  
    sp_configure 'EKM provider enabled', 1 ;  
    GO  
    RECONFIGURE ;  
    GO  
  
    -- Create a cryptographic provider, using the SQL Server Connector  
    -- which is an EKM provider for the Azure Key Vault. This example uses   
    -- the name AzureKeyVault_EKM_Prov.  
  
    CREATE CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov   
    FROM FILE = 'C:\Program Files\SQL Server Connector for Microsoft Azure Key Vault\Microsoft.AzureKeyVaultService.EKM.dll';  
    GO   
    ```  
  
2.  Setup einer [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -Anmeldeinformation für eine [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] -administratoranmeldung zum Einrichten und Verwalten von Key Vault [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Szenarios für die Verschlüsselung.  
  
    > [!IMPORTANT]  
    >  Die **Identität** Argument `CREATE CREDENTIAL` erfordert den schlüsseltresornamen. Die **GEHEIMNIS** Argument `CREATE CREDENTIAL` erfordert die  *\<Client-ID >* (ohne Bindestriche) und  *\<Geheimnis >* übergeben werden ohne ein Leerzeichen dazwischen.  
  
     Im folgenden Beispiel wird die **Client-ID** (`EF5C8E09-4D2A-4A76-9998-D93440D8115D`) von den Bindestrichen bereinigt und als Zeichenfolge `EF5C8E094D2A4A769998D93440D8115D` eingegeben. Der **geheime Schlüssel** wird durch die Zeichenfolge *SECRET_sysadmin_login*dargestellt.  
  
    ```  
    USE master;  
    CREATE CREDENTIAL sysadmin_ekm_cred   
        WITH IDENTITY = 'ContosoKeyVault',   
        SECRET = 'EF5C8E094D2A4A769998D93440D8115DSECRET_sysadmin_login'   
    FOR CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov ;  
  
    -- Add the credential to the SQL Server administrators domain login   
    ALTER LOGIN [<domain>/<login>]  
    ADD CREDENTIAL sysadmin_ekm_cred;  
    ```  
  
     Ein Beispiel für die Verwendung von Variablen für die `CREATE CREDENTIAL` Argumente und die programmgesteuerte Entfernung der Bindestriche aus der Client-ID finden Sie unter [CREATE CREDENTIAL &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-credential-transact-sql).  
  
3.  Wenn Sie einen asymmetrischen Schlüssel importiert haben, wie zuvor in Schritt 1, Abschnitt 3, beschrieben, öffnen Sie den Schlüssel, indem Sie im folgenden Beispiel Ihren Schlüsselnamen angeben.  
  
    ```  
    CREATE ASYMMETRIC KEY CONTOSO_KEY   
    FROM PROVIDER [AzureKeyVault_EKM_Prov]  
    WITH PROVIDER_KEY_NAME = 'ContosoMasterKey',  
    CREATION_DISPOSITION = OPEN_EXISTING;  
    ```  
  
     Obwohl dies für die Produktionsumgebung nicht empfohlen wird (da der Schlüssel nicht exportiert werden kann), ist es möglich, von [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] aus einen asymmetrischen Schlüssel direkt im Tresor zu erstellen. Wenn Sie zuvor keinen Schlüssel importiert haben, erstellen Sie mit dem folgenden Skript zu Testzwecken einen asymmetrischen Schlüssel im Schlüsseltresor. Führen Sie das Skript mithilfe einer mit den Anmeldeinformationen **sysadmin_ekm_cred** bereitgestellten Anmeldung aus.  
  
    ```  
    CREATE ASYMMETRIC KEY CONTOSO_KEY   
    FROM PROVIDER [AzureKeyVault_EKM_Prov]  
    WITH ALGORITHM = RSA_2048,  
    PROVIDER_KEY_NAME = 'ContosoMasterKey';  
    ```  
  
> [!TIP]  
>  Benutzer, die den Fehler **kann nicht öffentlichen Schlüssel vom Anbieter exportiert. Anbieterfehlercode: 2053.** sollten ihre **get**, **list**, **wrapKey**- und **unwrapKey** -Berechtigungen im Schlüsseltresor prüfen.  
  
 Weitere Informationen finden Sie unter den folgenden Links:  
  
-   [sp_configure &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-configure-transact-sql)  
  
-   [CREATE CRYPTOGRAPHIC PROVIDER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-cryptographic-provider-transact-sql)  
  
-   [CREATE CREDENTIAL &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-credential-transact-sql)  
  
-   [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-asymmetric-key-transact-sql)  
  
-   [CREATE LOGIN &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-login-transact-sql)  
  
-   [ALTER LOGIN &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-login-transact-sql)  
  
## <a name="examples"></a>Beispiele  
  
###  <a name="ExampleA"></a> Beispiel A: Transparente datenverschlüsselung mit einem asymmetrischen Schlüssel aus dem Schlüsseltresor  
 Erstellen Sie nach Abschluss der obigen Schritte Anmeldeinformationen und eine Anmeldung, und erstellen Sie einen Datenbank-Verschlüsselungsschlüssel, der durch den asymmetrischen Schlüssel im Schlüsseltresor geschützt wird. Verwenden Sie den Datenbank-Verschlüsselungsschlüssel zum Verschlüsseln einer Datenbank mit transparenter Datenverschlüsselung.  
  
 Zum Verschlüsseln einer Datenbank ist die CONTROL-Berechtigung für die Datenbank erforderlich.  
  
##### <a name="to-enable-tde-using-ekm-and-the-key-vault"></a>So aktivieren Sie die transparente Datenverschlüsselung mit erweiterbarer Schlüsselverwaltung und dem Schlüsseltresor  
  
1.  Erstellen Sie [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Anmeldeinformationen für die [!INCLUDE[ssDE](../../../includes/ssde-md.md)], die beim Laden der Datenbank für den Zugriff auf die erweiterbare Schlüsselverwaltung mit Schlüsseltresor verwendet werden.  
  
    > [!IMPORTANT]  
    >  Die **Identität** Argument `CREATE CREDENTIAL` erfordert den schlüsseltresornamen. Die **GEHEIMNIS** Argument `CREATE CREDENTIAL` erfordert die  *\<Client-ID >* (ohne Bindestriche) und  *\<Geheimnis >* übergeben werden ohne ein Leerzeichen dazwischen.  
  
     Im folgenden Beispiel wird die **Client-ID** (`EF5C8E09-4D2A-4A76-9998-D93440D8115D`) von den Bindestrichen bereinigt und als Zeichenfolge `EF5C8E094D2A4A769998D93440D8115D` eingegeben. Der **geheime Schlüssel** wird durch die Zeichenfolge *SECRET_DBEngine*dargestellt.  
  
    ```  
    USE master;  
    CREATE CREDENTIAL Azure_EKM_TDE_cred   
        WITH IDENTITY = 'ContosoKeyVault',   
        SECRET = 'EF5C8E094D2A4A769998D93440D8115DSECRET_DBEngine'   
        FOR CRYPTOGRAPHIC PROVIDER AzureKeyVault_EKM_Prov ;  
    ```  
  
2.  Erstellen Sie eine [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]-Anmeldung, die von der [!INCLUDE[ssDE](../../../includes/ssde-md.md)] für die transparente Datenverschlüsselung verwendet wird, und fügen Sie die Anmeldeinformationen hinzu. In diesem Beispiel wird der asymmetrische Schlüssel CONTOSO_KEY aus dem Schlüsseltresor verwendet, der importiert oder zuvor für die Masterdatenbank erstellt wurde, wie oben in [Schritt 3, Abschnitt 3](#Step3) beschrieben.  
  
    ```  
    USE master;  
    -- Create a SQL Server login associated with the asymmetric key   
    -- for the Database engine to use when it loads a database   
    -- encrypted by TDE.  
    CREATE LOGIN TDE_Login   
    FROM ASYMMETRIC KEY CONTOSO_KEY;  
    GO   
  
    -- Alter the TDE Login to add the credential for use by the   
    -- Database Engine to access the key vault  
    ALTER LOGIN TDE_Login   
    ADD CREDENTIAL Azure_EKM_TDE_cred ;  
    GO  
    ```  
  
3.  Erstellen Sie den Datenbank-Verschlüsselungsschlüssel (Database Encryption Key, DEK), der für die transparente Datenverschlüsselung verwendet wird. Der DEK kann mit jedem von SQL Server unterstützten Algorithmus und jeder unterstützten Schlüssellänge erstellt werden. Der DEK wird durch den asymmetrischen Schlüssel im Schlüsseltresor geschützt.  
  
     In diesem Beispiel wird der asymmetrische Schlüssel CONTOSO_KEY aus dem Schlüsseltresor verwendet, der importiert oder zuvor erstellt wurde, wie oben in [Schritt 3, Abschnitt 3](#Step3) beschrieben.  
  
    ```  
    USE ContosoDatabase;  
    GO  
  
    CREATE DATABASE ENCRYPTION KEY   
    WITH ALGORITHM = AES_128   
    ENCRYPTION BY SERVER ASYMMETRIC KEY CONTOSO_KEY;  
    GO  
  
    -- Alter the database to enable transparent data encryption.  
    ALTER DATABASE ContosoDatabase   
    SET ENCRYPTION ON ;  
    GO  
    ```  
  
     Weitere Informationen finden Sie unter den folgenden Links:  
  
    -   [CREATE DATABASE ENCRYPTION KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-database-encryption-key-transact-sql)  
  
    -   [ALTER DATABASE &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-database-transact-sql)  
  
###  <a name="ExampleB"></a> Beispiel B: Verschlüsseln von Sicherungen mit einem asymmetrischen Schlüssel aus dem Schlüsseltresor  
 Verschlüsselte Sicherungen werden ab [!INCLUDE[ssSQL14](../../../includes/sssql14-md.md)]unterstützt. Im folgenden Beispiel wird eine Sicherung erstellt und wiederhergestellt, die mit einem Verschlüsselungsschlüssel verschlüsselt wurde, der durch den asymmetrischen Schlüssel im Schlüsseltresor geschützt wird.  
  
```  
USE master;  
BACKUP DATABASE [DATABASE_TO_BACKUP]  
TO DISK = N'[PATH TO BACKUP FILE]'   
WITH FORMAT, INIT, SKIP, NOREWIND, NOUNLOAD,   
ENCRYPTION(ALGORITHM = AES_256, SERVER ASYMMETRIC KEY = [CONTOSO_KEY]);  
GO  
```  
  
 Beispiel für Wiederherstellungscode.  
  
```  
RESTORE DATABASE [DATABASE_TO_BACKUP]  
FROM DISK = N'[PATH TO BACKUP FILE]' WITH FILE = 1, NOUNLOAD, REPLACE;  
GO  
```  
  
 Weitere Informationen zu Sicherungsoptionen finden Sie unter [BACKUP &#40;Transact-SQL&#41;](/sql/t-sql/statements/backup-transact-sql).  
  
###  <a name="ExampleC"></a> Beispiel C: Verschlüsselung auf Spaltenebene mit einem asymmetrischen Schlüssel aus dem Schlüsseltresor  
 Das folgende Beispiel erstellt einen symmetrischen Schlüssel, der durch den asymmetrischen Schlüssel im Schlüsseltresor geschützt wird. Anschließend wird der symmetrische Schlüssel zum Verschlüsseln von Daten in der Datenbank verwendet.  
  
 In diesem Beispiel wird der asymmetrische Schlüssel CONTOSO_KEY aus dem Schlüsseltresor verwendet, der importiert oder zuvor erstellt wurde, wie oben in [Schritt 3, Abschnitt 3](#Step3) beschrieben. Um diesen asymmetrischen Schlüssel in der `ContosoDatabase` -Datenbank zu verwenden, müssen Sie die CREATE ASYMMETRIC KEY-Anweisung erneut ausführen, um der `ContosoDatabase` -Datenbank einen Verweis auf den Schlüssel zur Verfügung zu stellen.  
  
```  
USE [ContosoDatabase];  
GO  
  
-- Create a reference to the key in the key vault  
CREATE ASYMMETRIC KEY CONTOSO_KEY   
FROM PROVIDER [AzureKeyVault_EKM_Prov]  
WITH PROVIDER_KEY_NAME = 'ContosoMasterKey',  
CREATION_DISPOSITION = OPEN_EXISTING;  
  
-- Create the data encryption key.  
-- The data encryption key can be created using any SQL Server   
-- supported algorithm or key length.  
-- The DEK will be protected by the asymmetric key in the key vault  
  
CREATE SYMMETRIC KEY DATA_ENCRYPTION_KEY  
    WITH ALGORITHM=AES_256  
    ENCRYPTION BY ASYMMETRIC KEY CONTOSO_KEY;  
  
DECLARE @DATA VARBINARY(MAX);  
  
--Open the symmetric key for use in this session  
OPEN SYMMETRIC KEY DATA_ENCRYPTION_KEY   
DECRYPTION BY ASYMMETRIC KEY CONTOSO_KEY;  
  
--Encrypt syntax  
SELECT @DATA = ENCRYPTBYKEY(KEY_GUID('DATA_ENCRYPTION_KEY'), CONVERT(VARBINARY,'Plain text data to encrypt'));  
  
-- Decrypt syntax  
SELECT CONVERT(VARCHAR, DECRYPTBYKEY(@DATA));  
  
--Close the symmetric key  
CLOSE SYMMETRIC KEY DATA_ENCRYPTION_KEY;  
```  
  
## <a name="see-also"></a>Siehe auch  
 [CREATE CRYPTOGRAPHIC PROVIDER &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-cryptographic-provider-transact-sql)   
 [CREATE CREDENTIAL &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-credential-transact-sql)   
 [CREATE ASYMMETRIC KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-asymmetric-key-transact-sql)   
 [CREATE SYMMETRIC KEY &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-symmetric-key-transact-sql)   
 [Erweiterbare Schlüsselverwaltung &#40;EKM&#41;](extensible-key-management-ekm.md)   
 [Aktivieren von TDE unter Verwendung von EKM](enable-tde-on-sql-server-using-ekm.md)   
 [Verschlüsseln von Sicherungen](../../backup-restore/backup-encryption.md)   
 [Erstellen einer verschlüsselten Sicherung](../../backup-restore/create-an-encrypted-backup.md)  
  
  
