---
title: 為 Advanced Threat Analytics 服務啟動進行疑難排解 | Microsoft Docs
description: 本文描述如何為 ATA 啟動問題進行疑難排解
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: 5a65285c-d1de-4025-9bb4-ef9c20b13cfa
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 21afd487fbf15b3fc1f5d618e0e6b98d50d07cae
ms.sourcegitcommit: f37127601166216e57e56611f85dd783c291114c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/24/2019
ms.locfileid: "54839558"
---
# <a name="troubleshooting-service-startup"></a>為服務啟動進行疑難排解

適用對象：*Advanced Threat Analytics 1.9 版*

## <a name="troubleshooting-ata-center-service-startup"></a>針對 ATA 中心服務啟動進行疑難排解

如果您的 ATA 中心未啟動，請執行下列疑難排解程序：

1.  執行下列 Windows PowerShell 命令：`Get-Service Pla | Select Status`
    確定效能計數器服務正在執行。 如果未執行，則是平台問題，而您必須確定讓此服務再次執行。
2.  如果正在執行，請嘗試將它重新啟動，看看是否會解決此問題：`Restart-Service Pla`
3.  嘗試手動建立新的資料收集器 (任何收集器都可以，即使只收集電腦 CPU 也可以)。
如果可以啟動，代表平台應該沒問題。 如果無法啟動，則可能仍是平台問題。

4.  嘗試使用已提升權限的提示字元執行下列命令，以手動重新建立 ATA 資料收集器：

        sc stop ATACenter
        logman stop "Microsoft ATA Center"
        logman export "Microsoft ATA Center" -xml c:\center.xml
        logman delete "Microsoft ATA Center"
        logman import "Microsoft ATA Center" -xml c:\center.xml
        logman start "Microsoft ATA Center"
        sc start ATACenter

## <a name="troubleshooting-ata-lightweight-gateway-startup"></a>為 ATA 輕量型閘道啟動進行疑難排解

**徵兆**

您的 ATA 閘道未啟動且您收到此錯誤：<br></br>
*System.Net.Http.HttpRequestException:回應狀態碼未指出成功：500 (內部伺服器錯誤)*

**描述**

在輕量型閘道安裝程序中，ATA 會配置 CPU 閾值，使輕量型閘道能夠以 15% 的緩衝區來利用 CPU，從而導致此問題發生。 若您使用了登錄機碼個別設定閾值：這項衝突會造成輕量型閘道無法啟動。 

**解決方法**

1. 在登錄機碼下，如果有稱為 **Disable Performance Counters** 的 DWORD 值，請確認其設為 **0**：`HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\PerfOS\Performance\`
    `HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Services\PerfProc\Performance`
 
2. 然後重新啟動效能記錄檔及警示 (PLA) 服務。 ATA 輕量型閘道會自動偵測變更並重新啟動服務。


## <a name="see-also"></a>另請參閱
- [ATA 必要條件](ata-prerequisites.md)
- [ATA 容量規劃](ata-capacity-planning.md)
- [設定事件收集](configure-event-collection.md)
- [設定 Windows 事件轉送](configure-event-collection.md)
- [查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
