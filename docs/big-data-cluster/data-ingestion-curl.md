---
title: Verwenden Sie Curl zum Laden von Daten in HDFS auf SQL Server 2019 CTP 2.1 | Microsoft-Dokumentation
description: ''
author: rothja
ms.author: jroth
manager: craigg
ms.date: 11/06/2018
ms.topic: conceptual
ms.prod: sql
ms.openlocfilehash: a5f580ab39ef7338f424975d9667745131ee748f
ms.sourcegitcommit: cb73d60db8df15bf929ca17c1576cf1c4dca1780
ms.translationtype: MT
ms.contentlocale: de-DE
ms.lasthandoff: 11/07/2018
ms.locfileid: "51221626"
---
# <a name="use-curl-to-load-data-into-hdfs-on-sql-server-2019-ctp-21"></a>Mithilfe von Curl zum Laden von Daten in HDFS auf SQL Server 2019 CTP 2.1

In diesem Artikel wird erläutert, wie Sie mit **curl** zum Laden von Daten in HDFS auf SQL Server 2019 CTP-Version 2.1.

## <a name="obtain-the-service-external-ip"></a>Dienst für die externe IP-Adresse abrufen

WebHDFS wird gestartet, wenn die Bereitstellung abgeschlossen ist, und der Zugriff von Knox durchläuft. Der Knox-Endpunkt wird über einen Kubernetes-Dienst verfügbar gemacht (für den Moment) namens **Service-Sicherheit-lb**.  Um die WebHDFS-URL zu erstellen, die Sie benötigen, verwenden Sie CURL, um Dateien hoch-und herunterladen Sie müssen die **Service-Sicherheit-lb** -externe IP-Adresse und den Namen Ihres Clusters. Sie können die Dienst-Security-lb-Dienst externe IP-Adresse abrufen, mit dem folgenden Befehl:

```bash
kubectl get service service-security-lb -n <cluster name> -o json | jq -r .status.loadBalancer.ingress[0].ip
```

> [!NOTE]
> Die `<cluster name>` hier ist der Name des Clusters, den Sie angegeben, bei der Ausführung Mssqlctl erstellen Clusters `<cluster name>`.

## <a name="construct-the-url-to-access-webhdfs"></a>Erstellen Sie die URL für den Zugriff auf WebHDFS

Sie können nun die URL, um die WebHDFS zugreifen, wie folgt erstellen:

`https://<service-security-lb service external IP address>:30433/gateway/default/webhdfs/v1/`

Zum Beispiel:

`https://13.66.190.205:30443/gateway/default/webhdfs/v1/`

## <a name="list-a-file"></a>Auflisten einer Datei

Um die Datei unter **Hdfs: / / / Airlinedata** verwenden Sie den folgenden Curl-Befehl:

```bash
curl -i -k -u root:root-password -X GET 'https://<service-security-lb IP external address>:30443/gateway/default/webhdfs/v1/airlinedata/?op=liststatus'
```

## <a name="put-a-local-file-into-hdfs"></a>Speichern Sie eine lokale Datei in HDFS

Stellen Sie eine neue Datei **test.csv** aus lokalen Verzeichnis Airlinedata Verzeichnis (**Content-Type** -Parameter ist erforderlich) den folgenden Curl-Befehl verwenden:

```bash
curl -i -L -k -u root:root-password -X PUT 'https://<service-security-lb IP external address>:30443/gateway/default/webhdfs/v1/airlinedata/test.csv?op=create' -H 'Content-Type: application/octet-stream' -T 'test.csv'
```

## <a name="create-a-directory"></a>Erstellen Sie ein Verzeichnis

Zum Erstellen eines Verzeichnisses **testen** unter `hdfs:///` mithilfe des folgenden Befehls:

```bash
curl -i -L -k -u root:root-password -X PUT 'https://<service-security-lb IP external address>:30443/gateway/default/webhdfs/v1/test?op=MKDIRS'
```

## <a name="next-steps"></a>Nächste Schritte

Weitere Informationen zu SQL Server-big Data-Cluster, finden Sie unter [neuerungen von SQL Server-big Data-Cluster?](big-data-cluster-overview.md).