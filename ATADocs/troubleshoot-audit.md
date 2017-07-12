---
title: "使用 ATA 稽核記錄檔 | Microsoft Docs"
description: "本文說明如何使用 Windows 事件記錄檔的 ATA 稽核記錄檔。"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 7/5/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 1d186a96-ef70-4787-aa64-c03d1db94ce0
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 54f17bc4775868e380586822456330dfc2d45c29
ms.sourcegitcommit: 53b56220fa761671442da273364bdb3d21269c9e
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/05/2017
---
*適用於︰Advanced Threat Analytics 1.8 版*

<a id="working-with-ata-audit-logs" class="xliff"></a>

# 使用 ATA 稽核記錄檔

ATA 稽核記錄檔會先保留在 [應用程式及服務] 下的 Windows 事件記錄檔，然後再放在 ATA 中心和 ATA 閘道電腦的 **Microsoft ATA**。

ATA 中心的稽核記錄檔包含：
-   可疑的活動資訊
-   監視警示 (健康狀態頁面)
-   ATA 主控台登入
-   所有設定變更*

ATA 閘道的稽核記錄檔包含：
-   閘道設定變更* 

(所有 ATA 閘道設定變更都是在 ATA 中心設定，但仍在閘道電腦上進行稽核。)

*設定變更稽核記錄檔會包含先前的設定和新的設定。


<a id="see-also" class="xliff"></a>

## 另請參閱
- [處理可疑活動](working-with-suspicious-activities.md)
- [查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
