---
title: "為 ATA 錯誤記錄檔疑難排解 | Microsoft ATA"
description: "說明如何針對 ATA 中的常見錯誤進行疑難排解"
keywords: 
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: d89e7aff-a6ef-48a3-ae87-6ac2e39f3bdb
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: a5c7163bc7b1989672e587bfb4fa6a65cd4e3751
ms.openlocfilehash: cf2e1ab1fec4906e0bf2df8e0407b1951081e62f


---

# 為 ATA 錯誤記錄檔進行疑難排解
本節詳細說明 ATA 部署中可能發生的錯誤，以及對其進行疑難排解所需的步驟。
## ATA 閘道錯誤
|錯誤|說明|解決方法|
|-------------|----------|---------|
|System.DirectoryServices.Protocols.LdapException：發生本機錯誤|ATA 閘道無法對網域控制站進行驗證。|1.確認網域控制站的 DNS 記錄在 DNS 伺服器中正確設定。 <br>2.驗證 ATA 閘道的時間與網域控制站的時間同步。|
|System.IdentityModel.Tokens.SecurityTokenValidationException︰無法驗證憑證鏈結|ATA 閘道無法驗證 ATA 中心的憑證。|1.驗證已將根 CA 憑證安裝在 ATA 閘道上受信任的憑證授權單位憑證存放區中。 <br>2.驗證憑證撤銷清單 (CRL) 可供使用，而且可以執行憑證撤銷驗證。|
|Microsoft.Common.ExtendedException︰無法剖析產生的時間|ATA 閘道無法剖析從 SIEM 轉寄的 syslog 訊息。|驗證已將 SIEM 設定為以 ATA 支援的其中一個格式來轉寄訊息。|
|System.ServiceModel.FaultException：確認訊息安全性時發生錯誤|ATA 閘道無法對 ATA 中心進行驗證。|驗證 ATA 閘道的時間與 ATA 中心的時間同步。|
|System.ServiceModel.EndpointNotFoundException：無法連線到 net.tcp://center.ip.addr:443/IEntityReceiver|ATA 閘道無法建立與 ATA 中心的連線。|確定網路設定正確，而且 ATA 閘道 ATA 中心之間的網路連線使用中。|
|System.DirectoryServices.Protocols.LdapException：LDAP 伺服器無法使用。|ATA 閘道無法使用 LDAP 通訊協定查詢網域控制站。|1. 驗證 ATA 用來連線到 Active Directory 網域的使用者帳戶，具有 Active Directory 樹狀目錄中所有物件的讀取存取。 <br>2. 確定網域控制站未經強化，不會防止 ATA 使用的使用者帳戶進行 LDAP 查詢。|
|Microsoft.Tri.Infrastructure.ContractException：合約例外狀況|ATA 閘道無法同步處理 ATA 中心的設定。|請在 ATA 主控台中完成 ATA 閘道的設定。|
|System.Reflection.ReflectionTypeLoadException: 無法載入一或多個要求的類型。 如需詳細資訊，請擷取 LoaderExceptions 屬性。|郵件分析器已安裝於 ATA 閘道。| 請將郵件分析器解除安裝。|
|Error [配置] System.OutOfMemoryException: 擲回 'System.OutOfMemoryException' 類型的例外狀況。|ATA 閘道的記憶體不足。|請增加網域控制站上的記憶體數量。|
|無法啟動即時消費者 ---> Microsoft.Opn.Runtime.Monitoring.MessageSessionException: PEFNDIS 事件提供者尚未就緒|未正確安裝 PEF (郵件分析器)。|如需因應措施，請連絡支援人員。|
|安裝失敗，錯誤為：0x80070652|電腦上有其他擱置的安裝。|請等候其他安裝完成，如有必要，請重新啟動電腦。|

## ATA 主控台錯誤
|錯誤|說明|解決方法|
|-------------|----------|---------|
|HTTP 錯誤 500.19 - 內部伺服器錯誤|IIS URL Rewrite Module 無法正確安裝。|請解除安裝，再重新安裝 IIS URL Rewrite Module。<br>[下載 IIS URL Rewrite Module](http://go.microsoft.com/fwlink/?LinkID=615137)|

## 部署錯誤
|錯誤|說明|解決方法|
|-------------|----------|---------|
|.Net Framework 4.6.1 安裝失敗，並發生錯誤 0x800713ec|.Net Framework 4.6.1 的必要條件尚未安裝於伺服器。 |安裝 ATA 之前，請驗證伺服器上已安裝 Windows Update [KB2919442](https://www.microsoft.com/download/details.aspx?id=42135) 和 [KB2919355](https://support.microsoft.com/kb/2919355)。|

![ATA .NET 安裝錯誤影像](media/netinstallerror.png)


## 另請參閱
- [ATA 必要條件](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [ATA 容量規劃](/advanced-threat-analytics/plan-design/ata-capacity-planning)
- [設定事件收集](/advanced-threat-analytics/deploy-use/configure-event-collection)
- [設定 Windows 事件轉送](/advanced-threat-analytics/deploy-use/configure-event-collection#configuring-windows-event-forwarding)
- [查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Jul16_HO3-->


