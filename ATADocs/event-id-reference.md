---
title: ATA 事件識別碼參考 | Microsoft Docs
description: 提供 ATA 事件識別碼的清單及其描述。
keywords: ''
author: mlottner
ms.author: mlottner
manager: barbkess
ms.date: 12/20/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 5d639e84-2e37-43a9-9667-49be6c4fa8b7
ms.reviewer: arzinger
ms.suite: ems
ms.openlocfilehash: 09ba4967cdb7b4b142c3102ca2e9f708cefe9dd5
ms.sourcegitcommit: 62b631f64a639f5df04bf805755f26c69b40e8e4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/29/2019
ms.locfileid: "58639131"
---
# <a name="ata-event-id-reference"></a>ATA 事件識別碼參考


適用對象：*Advanced Threat Analytics 1.9 版*

ATA 中心事件檢視器會記錄 ATA 的事件。 這篇文章會提供事件識別碼的清單以及每個識別碼的描述。

以下可找到事件：

![事件識別碼位置](./media/event-id-location.png)

## <a name="ata-health-events"></a>ATA 健康情況事件

|監視事件識別碼| 監視警示名稱|
|---------|---------------|
|1001|中心磁碟空間用盡|
|1003|中心超載|
|1004|中心憑證即將到期/中心憑證已到期|
|1005|MongoDB 已關閉|
|1006|唯讀使用者密碼即將到期/唯讀使用者密碼已到期|
|1007|未指派網域同步器|
|1008|閘道上的部分或所有擷取網路介面卡無法使用|
|1009|閘道上的擷取網路介面卡已不存在|
|1010|閘道無法連線到部分網域控制站/閘道無法連線到所有網域控制站|
|1011|閘道已停止通訊|
|1012|某些轉送的事件不會被分析|
|1013|某些網路流量不會被分析|
|1014|傳送郵件失敗|
|1015|無法連線到使用 Syslog 的 SIEM 伺服器|
|1016|閘道版本已過期|
|1017|未從網域控制站收到任何流量|
|1018|閘道服務無法啟動|
|1019|輕量型閘道已達到記憶體資源限制|
|1020|閘道未處理 RADIUS 事件|
|1021|閘道未處理 Syslog 事件|
|1022|無法使用地理位置服務|
 
## <a name="ata-security-alert-events"></a>ATA 安全性警訊事件

|警示名稱|警示事件識別碼|
|---------|---------------|
|2001|基於異常行為懷疑身分遭竊|
|2002|不尋常的通訊協定實作|
|2003|使用帳戶列舉偵查|
|2004|使用 LDAP 簡單繫結的暴力密碼破解攻擊|
|2006|惡意的目錄服務複寫|
|2007|使用 DNS 探查|
|2008|加密降級活動|
|2009|加密降級活動 (可能為黃金票證)|
|2010|加密降級活動 (可能為 Overpass-the-Hash)|
|2011|加密降級活動 (可能為萬能金鑰)|
|2012|使用 SMB 工作階段列舉的偵察|
|2013|使用偽造授權資料提升權限|
|2014|Honeytoken 活動|
|2016|大量物件刪除|
|2017 年|使用傳遞雜湊攻擊竊取身分|
|2018 年|使用傳遞票證攻擊竊取身分|
|2019|偵測到遠端執行嘗試|
|2020|惡意的資料保護私人資訊要求|
|2021|使用目錄服務查詢的偵察|
|2022|Kerberos 黃金票證活動|
|2023|可疑的驗證失敗|
|2024|敏感性群組的異常修改|
|2026|可疑的服務建立|

## <a name="ata-auditing-events"></a>ATA 稽核事件

|警示名稱|警示事件識別碼|
|---------|---------------|
|3001|變更為 ATA 設定|
|3002|已新增 ATA 閘道|
|3003|已刪除 ATA 閘道|
|3004|已啟用 ATA 授權|
|3005|登入 ATA 主控台|
|3006|手動變更為健康情況活動狀態|
|3007|手動變更為可疑活動狀態|

## <a name="see-also"></a>另請參閱
- [ATA 必要條件](ata-prerequisites.md)
- [ATA 容量規劃](ata-capacity-planning.md)
- [設定事件收集](configure-event-collection.md)
- [設定 Windows 事件轉送](configure-event-collection.md)
- [查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
