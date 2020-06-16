---
title: 使用 ATA 稽核記錄檔
description: 本文說明如何使用 Windows 事件記錄檔的 ATA 稽核記錄檔。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 1d186a96-ef70-4787-aa64-c03d1db94ce0
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 4fed6cc6eddfd33606c1811e0a1e861b5bf8a108
ms.sourcegitcommit: fbb0768c392f9bccdd7e4adf0e9a0303c8d1922c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2020
ms.locfileid: "84774956"
---
# <a name="working-with-ata-audit-logs"></a>使用 ATA 稽核記錄檔


*適用於：Advanced Threat Analytics 1.9 版*

ATA 稽核記錄檔會先保留在 [應用程式及服務]**** 下的 Windows 事件記錄檔，然後再放在 ATA 中心和 ATA 閘道電腦的 **Microsoft ATA**。

ATA 中心的稽核記錄檔包含：
-   可疑的活動資訊
-   健康情況警示（健康情況頁面）
-   ATA 主控台登入
-   所有設定變更*

ATA 閘道的稽核記錄檔包含：
-   閘道設定變更* 

(所有 ATA 閘道設定變更都是在 ATA 中心設定，但仍在閘道電腦上進行稽核。)

*設定變更稽核記錄檔會包含先前的設定和新的設定。


## <a name="see-also"></a>另請參閱
- [處理可疑活動](working-with-suspicious-activities.md)
- [查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
