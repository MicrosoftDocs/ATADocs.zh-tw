---
title: "使用記錄檔針對 Advanced Threat Analytics 進行疑難排解 | Microsoft Docs"
description: "描述如何使用 ATA 記錄檔來疑難排解問題"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 06/26/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 5a65285c-d1de-4025-9bb4-ef9c20b13cfa
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 1291281273188a21b61b29f06a5220eee589767c
ms.sourcegitcommit: 470675730967e0c36ebc90fc399baa64e7901f6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/30/2017
---
適用於︰Advanced Threat Analytics 1.8 版



<a id="troubleshooting-ata-center-service-startup" class="xliff"></a>

# 針對 ATA 中心服務啟動進行疑難排解

如果您的 ATA 中心未啟動，請執行下列疑難排解程序：

1.  執行下列 Windows PowerShell 命令：Get-Service Pla | Select Status，確定效能計數器服務正在執行。 如果未執行，則是平台問題，而您必須確定讓此服務再次執行。
2.  如果正在執行，請嘗試將它重新啟動，看看是否會解決此問題：Restart-Service Pla
3.  嘗試手動建立新的資料收集器 (任何收集器都可以，即使只收集電腦 CPU 也可以)。
如果可以啟動，平台可能沒問題；如果無法啟動，則仍然是平台問題。

4.  嘗試手動重新建立 ATA 資料收集器，使用提升權限的提示字元並執行下列命令：sc stop ATACenter logman stop "Microsoft ATA Center" logman export "Microsoft ATA Center" -xml c:\center.xml logman delete "Microsoft ATA Center" logman import "Microsoft ATA Center" -xml c:\center.xml logman start "Microsoft ATA Center" sc start ATACenter



<a id="see-also" class="xliff"></a>

## 另請參閱
- [ATA 必要條件](ata-prerequisites.md)
- [ATA 容量規劃](ata-capacity-planning.md)
- [設定事件收集](configure-event-collection.md)
- [設定 Windows 事件轉送](configure-event-collection.md#configuring-windows-event-forwarding)
- [查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
