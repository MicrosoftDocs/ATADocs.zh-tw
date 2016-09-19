---
title: "ATA 資料庫管理 | Microsoft ATA"
description: "這些程序可協助您移動、備份或還原 ATA 資料庫。"
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 1d27dba8-fb30-4cce-a68a-f0b1df02b977
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 5cd030f3b952d08c6617a6cda121c344a9c36f51
ms.openlocfilehash: b4e68e9e8dbd94075a34a8e3e8f42d4f534caf50


---

*適用於︰Advanced Threat Analytics 1.7 版*



# ATA 資料庫管理
如果您要移動、備份或還原 ATA 資料庫，請使用這些程序以使用 MongoDB。

## 備份 ATA 資料庫
請參閱[相關 MongoDB 文件](http://docs.mongodb.org/manual/administration/backup/)。

## 還原 ATA 資料庫
請參閱[相關 MongoDB 文件](http://docs.mongodb.org/manual/administration/backup/)。

## 將 ATA 資料庫移至其他磁碟機

1.  停止 **Microsoft Advanced Threat Analytics 中心**服務。

2.  停止 **MongoDB** 服務。

3.  開啟 Mongo 組態檔，其預設位置為︰C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\mongod.cfg。

    找出參數 `storage: dbPath`

4.  將列於 `dbPath` 參數中的資料夾移至新的位置。

5.  將 mongo 組態檔內的 `dbPath` 參數變更為新的資料夾路徑，然後儲存並關閉檔案。

    ![修改 MongoDB 組態影像](media/ATA-mongoDB-moveDB.png)

6.  啟動 **MongoDB** 服務。

7. 啟動 **Microsoft Advanced Threat Analytics 中心**服務。

## ATA 設定檔
ATA 組態會儲存在資料庫的「SystemProfile 」集合中。
ATA 中心服務每小時會將此集合備份到名為 "SystemProfile_*timestamp*.json" 的檔案。 會儲存 10 個最新的版本。
這位於名為「Backup」的子資料夾中。 在預設的 ATA 安裝位置中，可以在這裡找到︰*C:\Program Files\Microsoft Advanced Threat Analytics\Center\Backup\SystemProfile_*timestamp*.json*。 

**注意**：建議在針對 ATA 進行重大變更時，在某處備份此檔案。

可執行下列命令來還原所有設定︰

`mongoimport.exe --db ATA --collection SystemProfile --file "<SystemProfile.json backup file>" --upsert`

## 另請參閱
- [ATA 架構](/advanced-threat-analytics/plan-design/ata-architecture)
- [ATA 必要條件](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/home?forum=mata)




<!--HONumber=Aug16_HO5-->


