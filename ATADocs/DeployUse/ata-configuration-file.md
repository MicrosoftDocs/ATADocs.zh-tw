---
title: "匯出和匯入 Advanced Threat Analytics 組態 | Microsoft Docs"
description: "如何匯出和匯入 ATA 組態。"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 1/23/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 1d27dba8-fb30-4cce-a68a-f0b1df02b977
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: b28cb3a0da844b7c460c03726222bc775a9e47da
ms.openlocfilehash: 5ea29a5b64fd1f786200d3bbb62cd3964f8802e2


---

適用於︰Advanced Threat Analytics 1.7 版



# <a name="export-and-import-the-ata-configuration"></a>匯出和匯入 ATA 組態
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




<!--HONumber=Feb17_HO1-->


