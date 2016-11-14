---
title: "為 ATA 錯誤記錄檔疑難排解 | Microsoft ATA"
description: "說明如何針對 ATA 中的常見錯誤進行疑難排解"
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 10/25/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: d89e7aff-a6ef-48a3-ae87-6ac2e39f3bdb
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: f334f9c8440e4bb0202579de220f6530d0aabad8
ms.openlocfilehash: aa16eeb45272ffcf28bbb28ed9a02f30f52b15d0


---

*適用於︰Advanced Threat Analytics 1.7 版*



# <a name="troubleshooting-the-ata-error-log"></a>為 ATA 錯誤記錄檔進行疑難排解
本節詳細說明 ATA 部署中可能發生的錯誤，以及對其進行疑難排解所需的步驟。
## <a name="ata-gateway-errors"></a>ATA 閘道錯誤
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
|無法啟動即時消費者 ---> Microsoft.Opn.Runtime.Monitoring.MessageSessionException: PEFNDIS 事件提供者尚未就緒|未正確安裝 PEF (郵件分析器)。|如果使用 HYPER-V，請嘗試升級 Hyper-V 整合服務，否則請連絡支援人員取得因應措施。|
|安裝失敗，錯誤為：0x80070652|電腦上有其他擱置的安裝。|請等候其他安裝完成，如有必要，請重新啟動電腦。|
|System.InvalidOperationException︰指定的分類中不存在執行個體 'Microsoft.Tri.Gateway'。|ATA 閘道中的程序名稱已啟用 PID|使用 [KB281884](https://support.microsoft.com/en-us/kb/281884) 停用程序名稱中的 PID|
|System.InvalidOperationException︰類別不存在。|登錄中的計數器可能已停用|使用 [KB2554336](https://support.microsoft.com/en-us/kb/2554336) 重建效能計數器|
|System.ApplicationException︰無法啟動 ETW 工作階段 MMA-ETW-Livecapture-a4f595bd-f567-49a7-b963-20fa4e370329|HOSTS 檔案中有一個主機項目指向電腦的簡短名稱|從 C:\Windows\System32\drivers\etc\HOSTS 檔案移除主機項目，或將它變更為 FQDN。|



## <a name="ata-lightweight-gateway-errors"></a>ATA 輕量型閘道錯誤

**錯誤**：在 VMware 上使用輕量閘道時的「已丟棄連接埠鏡像流量」警示

**描述**：若在 VMware 虛擬機器上使用 DC，可能會收到有關於**已丟棄連接埠鏡像流量**的警示。 這可能是 VMware 中的設定不相符所致。 
**解決方法**：若要避免這些警示，可檢查是否已將下列設定設為 [0] 或 [已停用]：TsoEnable、LargeSendOffload、IPv4、TSO Offload。 此外也請考慮停用 [IPv4 Giant TSO Offload]。 如需詳細資訊，請參閱 VMware 文件。


## <a name="ata-iis-errors-not-applicable-for-ata-v17-and-above"></a>ATA IIS 錯誤 (不適用於 ATA v1.7 和更新版本)
|錯誤|說明|解決方法|
|-------------|----------|---------|
|HTTP 錯誤 500.19 - 內部伺服器錯誤|IIS URL Rewrite Module 無法正確安裝。|請解除安裝，再重新安裝 IIS URL Rewrite Module。<br>[下載 IIS URL Rewrite Module](http://go.microsoft.com/fwlink/?LinkID=615137)|

## <a name="deployment-errors"></a>部署錯誤
|錯誤|說明|解決方法|
|-------------|----------|---------|
|.Net Framework 4.6.1 安裝失敗，並發生錯誤 0x800713ec|.Net Framework 4.6.1 的必要條件尚未安裝於伺服器。 |安裝 ATA 之前，請驗證伺服器上已安裝 Windows Update [KB2919442](https://www.microsoft.com/download/details.aspx?id=42135) 和 [KB2919355](https://support.microsoft.com/kb/2919355)。|

![ATA .NET 安裝錯誤影像](media/netinstallerror.png)


## <a name="see-also"></a>另請參閱
- [ATA 必要條件](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [ATA 容量規劃](/advanced-threat-analytics/plan-design/ata-capacity-planning)
- [設定事件收集](/advanced-threat-analytics/deploy-use/configure-event-collection)
- [設定 Windows 事件轉送](/advanced-threat-analytics/deploy-use/configure-event-collection#configuring-windows-event-forwarding)
- [查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Oct16_HO5-->


