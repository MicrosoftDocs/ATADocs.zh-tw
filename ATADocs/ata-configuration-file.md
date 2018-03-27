---
title: 匯出和匯入 Advanced Threat Analytics 組態 | Microsoft Docs
description: 如何匯出和匯入 ATA 組態。
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: article
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: 1d27dba8-fb30-4cce-a68a-f0b1df02b977
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: edbf553bf48d984f4864264643d197362c3d6042
ms.sourcegitcommit: 49c3e41714a5a46ff2607cbced50a31ec90fc90c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/22/2018
---
*適用於：Advanced Threat Analytics 1.9 版*



# <a name="export-and-import-the-ata-configuration"></a>匯出和匯入 ATA 組態
ATA 組態會儲存在資料庫的「SystemProfile 」集合中。
ATA 中心服務每小時會將此集合備份成名為 **SystemProfile_*timestamp*.json** 的檔案。 會儲存 10 個最新的版本。
此檔案位於名為 **Backup** 的子資料夾中。 在預設的 ATA 安裝位置中，可以在這裡找到︰*C:\Program Files\Microsoft Advanced Threat Analytics\Center\Backup\SystemProfile_*timestamp*.json*。 

**注意**：建議在針對 ATA 進行重大變更時，在某處備份此檔案。

可執行下列命令來還原所有設定︰

`mongoimport.exe --db ATA --collection SystemProfile --file "<SystemProfile.json backup file>" --upsert`

## <a name="see-also"></a>另請參閱
- [ATA 架構](ata-architecture.md)
- [ATA 必要條件](ata-prerequisites.md)
- [查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

