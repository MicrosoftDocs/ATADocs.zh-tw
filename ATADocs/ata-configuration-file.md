---
title: 匯出和匯入 Advanced Threat Analytics 組態 | Microsoft Docs
description: 如何匯出和匯入 ATA 組態。
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 9/04/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 1d27dba8-fb30-4cce-a68a-f0b1df02b977
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 06c225b26c43d48aeba6c032434af08231106dad
ms.sourcegitcommit: ae9db212f268f067b217d33b0c3f991b6531c975
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/07/2019
ms.locfileid: "65196466"
---
# <a name="export-and-import-the-ata-configuration"></a>匯出和匯入 ATA 組態

適用對象：*Advanced Threat Analytics 1.9 版*

ATA 組態會儲存在資料庫的「SystemProfile 」集合中。
ATA 中心服務每 4 小時會將此集合備份至下列名稱的檔案：**SystemProfile_*timestamp*.json**。 並會儲存 300 個最新版本。
此檔案位於名為 **Backup** 的子資料夾中。 在預設 ATA 安裝位置中，可以在此處找到它：<em>C:\Program Files\Microsoft Advanced Threat Analytics\Center\Backup\SystemProfile_</em>timestamp<em>.json</em>。 

**注意**：建議在針對 ATA 進行重大變更時，在某處備份此檔案。

可執行下列命令來還原所有設定︰

`mongoimport.exe --db ATA --collection SystemProfile --file "<SystemProfile.json backup file>" --upsert`

## <a name="see-also"></a>另請參閱
- [ATA 架構](ata-architecture.md)
- [ATA 必要條件](ata-prerequisites.md)
- [查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

