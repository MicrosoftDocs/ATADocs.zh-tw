---
# required metadata

title: ATA 資料庫管理 |Microsoft Advanced Threat Analytics
description: 這些程序可協助您移動、備份或還原 ATA 資料庫。
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 1d27dba8-fb30-4cce-a68a-f0b1df02b977

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# ATA 資料庫管理
如果您要移動、備份或還原 ATA 資料庫，請使用這些程序以使用 MongoDB。

## 備份 ATA 資料庫
請參閱 [relevant MongoDB documentation](http://docs.mongodb.org/manual/administration/backup/) (相關 MongoDB 文件).

## 還原 ATA 資料庫
請參閱 [relevant MongoDB documentation](http://docs.mongodb.org/manual/administration/backup/) (相關 MongoDB 文件).

## 將 ATA 資料庫移至其他磁碟機

1.  停止 **Microsoft Advanced Threat Analytics 中心**服務。

2.  停止 **MongoDB** 服務。

3.  開啟 Mongo 組態檔，其預設位置為︰C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\mongod.cfg。

    找出參數 `storage: dbPath`

4.  將列於 `dbPath` 參數中的資料夾移至新的位置。

5.  將 mongo 組態檔內的 `dbPath` 參數變更為新的資料夾路徑，然後儲存並關閉檔案。

    ![修改 MongoDB 組態影像](media/ATA-mongoDB-moveDB.png)

6.  啟動 **MongoDB** 服務。

7.  開啟命令提示字元，並執行 Mongo 殼層，執行方式為 `mongo.exe ATA` .

    根據預設，mongo.exe 位於︰C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin

8.  執行下列命令︰`db.SystemProfiles.update( {_t: "CenterSystemProfile"} , {$set:{"Configuration.CenterDatabaseClientConfiguration.DataPath" : "<New DB Location>"}}) Instead of <New DB Location>` 其中 &lt;新的 DB 位置&gt; 為新的資料夾路徑。

9.  將 HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Advanced Threat Analytics\Center\DatabaseDataPath 更新至新的資料夾路徑。

9. 啟動 **Microsoft Advanced Threat Analytics 中心**服務。

## 另請參閱
- [ATA 架構](/advanced-threat-analytics/plan-design/ata-architecture)
- [ATA 必要條件](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)



<!--HONumber=May16_HO1-->


