---
title: "ATA 事件識別碼參考 | Microsoft Docs"
description: "提供 ATA 事件識別碼的清單及其描述。"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 10/25/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 5d639e84-2e37-43a9-9667-49be6c4fa8b7
ms.reviewer: arzinger
ms.suite: ems
ms.openlocfilehash: 7bd0f90acbb6a2d8eb84fd09bc4d859fff082273
ms.sourcegitcommit: 5563c6861bb5db5cb73e058e5a51b4938b9a7d46
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/30/2017
---
適用於︰Advanced Threat Analytics 1.8 版


# <a name="ata-event-id-reference"></a>ATA 事件識別碼參考

ATA 中心事件檢視器會記錄 ATA 的事件。 這篇文章會提供事件識別碼的清單以及每個識別碼的描述。

以下可找到事件：

![事件識別碼位置](./media/event-id-location.png)

## <a name="ata-health-events"></a>ATA 健康情況事件

1001 – ATA 中心資料庫資料磁碟機可用空間健康情況警示 

1003 – ATA 中心已超載健康情況警示 

1004 – 憑證到期健康情況警示 

1005 – 中心資料庫已中斷連線健康情況警示 

1006 – ATA 閘道目錄服務用戶端帳戶密碼到期健康情況警示 

1007 – ATA 閘道網域同步器未指派健康情況警示 

1008 – ATA 閘道擷取網路介面卡發生錯誤健康情況警示 

1009 – ATA 閘道擷取網路介面卡遺失健康情況警示 

1010 – ATA 閘道目錄服務用戶端連線健康情況警示 

1011 – ATA 閘道已中斷連線健康情況警示 

1012 – ATA 閘道已超載事件活動健康情況警示 

1013 – ATA 閘道已超載網路活動健康情況警示 

1014 – 中心郵件健康情況警示 

1015 – 中心 Syslog 健康情況警示 

1016 – ATA 閘道已過期健康情況警示 

1017 – 中心未接收流量健康情況警示 

1018 – ATA 閘道啟動失敗健康情況警示 

1019 – ATA 閘道記憶體不足健康情況警示 

1020 – ATA 閘道 RADIUS 事件接聽程式健康情況警示 

1021 – ATA 閘道 Syslog 事件接聽程式健康情況警示 

1022 – ATA 中心外部 IP 位址解析失敗健康情況警示 
 
## <a name="ata-suspicious-ctivity-events"></a>ATA 可疑活動事件

2001 – 異常行為可疑活動 

2002 – 異常通訊協定可疑活動 

2003 – 帳戶列舉可疑活動 

2004 – LDAP 暴力密碼破解可疑活動 

2005 – 電腦預先驗證失敗可疑活動 

2006 – 目錄服務複寫可疑活動 

2007 – DNS 探察可疑活動 

2008 – 加密降級可疑活動 

2012 – 列舉工作階段可疑活動 

2013 – 偽造的 PAC 可疑活動 

2014 – Honeytoken 活動的可疑活動 

2015 – LDAP 純文字密碼可疑活動 

2016 – 大量物件刪除可疑活動 

2017 – 傳遞雜湊可疑活動 

2018 – 傳遞票證可疑活動 

2019 – 遠端執行可疑活動 

2020 – 擷取資料保護備份金鑰可疑活動 

2021 – SAMR 探察可疑活動 

2022 – 黃金票證可疑活動 

2023 – 異常敏感性群組成員資格變更可疑活動 

2023 – 暴力密碼破解可疑活動 

## <a name="ata-auditing-events"></a>ATA 稽核事件

3001 – 變更為 ATA 設定 

3002 – ATA 閘道已新增

3003 – ATA 閘道已刪除

3004 - ATA 授權已啟用

3005 – 登入 ATA 主控台

3006 – 手動變更為健康情況活動狀態 

3007 – 手動變更為可疑活動狀態 


## <a name="see-also"></a>另請參閱
- [ATA 必要條件](ata-prerequisites.md)
- [ATA 容量規劃](ata-capacity-planning.md)
- [設定事件收集](configure-event-collection.md)
- [設定 Windows 事件轉送](configure-event-collection.md#configuring-windows-event-forwarding)
- [查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
