---
title: Advanced Threat Analytics 資料庫管理 |Microsoft Docs
description: 這些程序可協助您移動、備份或還原 ATA 資料庫。
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: 05e49e23-6e0a-4ec0-9a63-a2093173c8a1
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 3dde0df4c0ddcf69a17b103d0a60bbb04ffe0d67
ms.sourcegitcommit: f37127601166216e57e56611f85dd783c291114c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/24/2019
ms.locfileid: "54840415"
---
# <a name="ata-database-management"></a>ATA 資料庫管理

適用對象：*Advanced Threat Analytics 1.9 版*

如果您要移動、備份或還原 ATA 資料庫，請使用這些程序以使用 MongoDB。

## <a name="backing-up-the-ata-database"></a>備份 ATA 資料庫
請參閱[相關 MongoDB 文件](http://docs.mongodb.org/manual/administration/backup/)。

## <a name="restoring-the-ata-database"></a>還原 ATA 資料庫
請參閱[相關 MongoDB 文件](http://docs.mongodb.org/manual/administration/backup/)。

## <a name="moving-the-ata-database-to-another-drive"></a>將 ATA 資料庫移至其他磁碟機

1. 停止 **Microsoft Advanced Threat Analytics 中心**服務。
   > [!Important] 
   > 繼續下一步之前，請確定 ATA 中心服務已經停止。

2. 停止 **MongoDB** 服務。

3. 開啟 Mongo 設定檔，其預設位置為：C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\mongod.cfg。

   找出參數 `storage: dbPath`

4. 將列於 `dbPath` 參數中的資料夾移至新的位置。

5. 將 mongo 組態檔內的 `dbPath` 參數變更為新的資料夾路徑，然後儲存並關閉檔案。

   ![修改 MongoDB 組態影像](media/ATA-mongoDB-moveDB.png)

6. 啟動 **MongoDB** 服務。

7. 啟動 **Microsoft Advanced Threat Analytics 中心**服務。

## <a name="see-also"></a>另請參閱
- [ATA 架構](ata-architecture.md)
- [ATA 必要條件](ata-prerequisites.md)
- [查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

