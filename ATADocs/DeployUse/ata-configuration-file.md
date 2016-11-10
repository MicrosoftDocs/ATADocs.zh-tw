---
title: "ATA 設定檔 | Microsoft ATA"
description: "備份 ATA 設定。"
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 10/31/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 1d27dba8-fb30-4cce-a68a-f0b1df02b977
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: f334f9c8440e4bb0202579de220f6530d0aabad8
ms.openlocfilehash: 542bdf983e26fa98c036de55860b482d0b1d734d


---

*適用於︰Advanced Threat Analytics 1.7 版*



# <a name="ata-configuration-file"></a>ATA 設定檔
ATA 組態會儲存在資料庫的「SystemProfile 」集合中。
ATA 中心服務每小時會將此集合備份到名為 "SystemProfile_*timestamp*.json" 的檔案。 會儲存 10 個最新的版本。
這位於名為「Backup」的子資料夾中。 在預設的 ATA 安裝位置中，可以在這裡找到︰*C:\Program Files\Microsoft Advanced Threat Analytics\Center\Backup\SystemProfile_*timestamp*.json*。 

**注意**：建議在針對 ATA 進行重大變更時，在某處備份此檔案。

可執行下列命令來還原所有設定︰

`mongoimport.exe --db ATA --collection SystemProfile --file "<SystemProfile.json backup file>" --upsert`

## <a name="see-also"></a>另請參閱
- [ATA 架構](/advanced-threat-analytics/plan-design/ata-architecture)
- [ATA 必要條件](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/home?forum=mata)




<!--HONumber=Oct16_HO5-->


