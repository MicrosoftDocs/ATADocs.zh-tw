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
ms.sourcegitcommit: 6dd002b5a34f230aaada55a6f6178c2f9e1584d9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2019
ms.locfileid: "65196466"
---
# <a name="export-and-import-the-ata-configuration"></a>匯出和匯入 ATA 組態

*適用於：Advanced Threat Analytics 1.9 版*

ATA 組態會儲存在資料庫的「SystemProfile 」集合中。
ATA 中心服務每 4 小時會將此集合備份至名為 **SystemProfile_*timestamp*.json** 的檔案。 並會儲存 300 個最新版本。
這個檔案位於名為**Backup**的子資料夾中。 在預設的 ATA 安裝位置中，可以在這裡找到︰<em>C:\Program Files\Microsoft Advanced Threat Analytics\Center\Backup\SystemProfile_</em>timestamp<em>.json</em>。 

**注意**：建議在針對 ATA 進行重大變更時，在某處備份此檔案。

可執行下列命令來還原所有設定︰

`mongoimport.exe --db ATA --collection SystemProfile --file "<SystemProfile.json backup file>" --upsert`

## <a name="see-also"></a>另請參閱
- [ATA 架構](ata-architecture.md)
- [ATA 必要條件](ata-prerequisites.md)
- [查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

