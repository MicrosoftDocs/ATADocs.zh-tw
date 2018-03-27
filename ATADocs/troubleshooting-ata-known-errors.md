---
title: 針對 ATA 已知問題進行疑難排解 | Microsoft Docs
description: 描述如何針對 Advanced Threat Analytics 中的已知問題進行疑難排解
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: article
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: d89e7aff-a6ef-48a3-ae87-6ac2e39f3bdb
ms.reviewer: arzinger
ms.suite: ems
ms.openlocfilehash: a7172447de5b4d4088da2d8d687a7bec47a01551
ms.sourcegitcommit: 49c3e41714a5a46ff2607cbced50a31ec90fc90c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/22/2018
---
*適用於：Advanced Threat Analytics 1.9 版*



# <a name="troubleshooting-ata-known-issues"></a>針對 ATA 已知問題進行疑難排解

本節詳細說明 ATA 部署中可能發生的錯誤，以及對其進行疑難排解所需的步驟。

## <a name="ata-gateway-and-lightweight-gateway-errors"></a>ATA 閘道和輕量型閘道錯誤

> [!div class="mx-tableFixed"]
|錯誤|說明|解決方案|
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
|無法啟動即時消費者 ---> Microsoft.Opn.Runtime.Monitoring.MessageSessionException: PEFNDIS 事件提供者尚未就緒|未正確安裝 PEF (郵件分析器)。|若是使用 HYPER-V，請嘗試升級 Hyper-V 整合服務，否則請連絡支援人員詢問其因應措施。|
|安裝失敗，錯誤為：0x80070652|電腦上有其他擱置的安裝。|請等候其他安裝完成，如有必要，請重新啟動電腦。|
|System.InvalidOperationException︰指定的分類中不存在執行個體 'Microsoft.Tri.Gateway'。|ATA 閘道中的程序名稱已啟用 PID|使用 [KB281884](https://support.microsoft.com/kb/281884) 停用程序名稱中的 PID|
|System.InvalidOperationException︰類別不存在。|登錄中的計數器可能已停用|使用 [KB2554336](https://support.microsoft.com/kb/2554336) 重建效能計數器|
|System.ApplicationException︰無法啟動 ETW 工作階段 MMA-ETW-Livecapture-a4f595bd-f567-49a7-b963-20fa4e370329|HOSTS 檔案中有一個主機項目指向電腦的簡短名稱|從 C:\Windows\System32\drivers\etc\HOSTS 檔案移除主機項目，或將它變更為 FQDN。|
|System.IO.IOException：驗證失敗，因為遠端群體已經關閉傳輸資料流。|ATA 閘道上已停用 TLS 1.0，但是 .Net 設定為使用 TLS 1.2|使用下列其中一個選項： </br> 在 ATA 閘道上啟用 TLS 1.0 </br>將登錄機碼設定為使用 SSL 和 TLS 的作業系統預設，以在 .Net 上啟用 TLS 1.2，方式如下： </br>`[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319] "SystemDefaultTlsVersions"=dword:00000001` </br>`[HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\v4.0.30319] "SystemDefaultTlsVersions"=dword:00000001`</br>`[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319] "SchUseStrongCrypto"=dword:00000001 `</br>`[HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\v4.0.30319] " SchUseStrongCrypto"=dword:00000001`|
|System.TypeLoadException：無法從組件 'Microsoft.Opn.Runtime, Version=4.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35' 載入類型 'Microsoft.Opn.Runtime.Values.BinaryValueBufferManager'|ATA 閘道無法載入必要的剖析檔案。|請檢查目前是否已安裝 Microsoft 郵件分析器。 不支援郵件分析器與 ATA 閘道/輕量型閘道一起安裝。 請解除安裝郵件分析器，然後重新啟動閘道服務。|
|System.Net.WebException: 遠端伺服器傳回錯誤: (407) 要求 Proxy 驗證|Proxy 伺服器中斷 ATA 閘道與 ATA 中心的通訊。|停用 ATA 閘道機器上的 Proxy。 <br></br>請注意，Proxy 設定可能依各帳戶為依據。|
|System.IO.DirectoryNotFoundException: 系統找不到指定的路徑。 (來自 HRESULT 的例外狀況: 0x80070003)|一或多個操作 ATA 所需的服務未啟動。|啟動下列服務： <br></br>效能記錄檔及警示 (PLA)、工作排程器 (排程)。|
|System.Net.WebException: 遠端伺服器傳回錯誤: (403) 禁止|ATA 閘道或輕量型閘道可能會因為 ATA 中心未受信任，而遭禁止建立 HTTP 連線。|將 ATA 中心的 NetBIOS 名稱和 FQDN 新增到受信任的網站清單，並清除 Interne Explorer 上的快取 (或者，如果不是設定 NetBIOS/FQDN，則是以設定中指定的 ATA 中心名稱)。|
|System.Net.Http.HttpRequestException：PostAsync 失敗 [requestTypeName=StopNetEventSessionRequest]|由於 WMI 的問題，ATA 閘道或 ATA 輕量型閘道無法停止並啟動收集網路流量的 ETW 工作階段|請依照 [WMI：重建 WMI 存放庫](https://blogs.technet.microsoft.com/askperf/2009/04/13/wmi-rebuilding-the-wmi-repository/) \(英文\) 中的指示來修正 WMI 問題|
|System.Net.Sockets.SocketException：嘗試採行其存取權限所禁止的方式存取通訊端|另一個應用程式正於 ATA 閘道上使用連接埠 514|使用 `netstat -o` 建立哪個處理序正在使用該連接埠。|
 
## <a name="deployment-errors"></a>部署錯誤
> [!div class="mx-tableFixed"]
|錯誤|說明|解決方案|
|-------------|----------|---------|
|.Net Framework 4.6.1 安裝失敗，並發生錯誤 0x800713ec|.Net Framework 4.6.1 的必要條件尚未安裝於伺服器。 |安裝 ATA 之前，請驗證伺服器上已安裝 Windows Update [KB2919442](https://www.microsoft.com/download/details.aspx?id=42135) 和 [KB2919355](https://support.microsoft.com/kb/2919355)。|
|System.Threading.Tasks.TaskCanceledException：工作已取消|因為無法連線到 ATA 中心，所以部署程序已逾時。|1.  藉由使用 ATA 中心的 IP 位址瀏覽至 ATA 中心，來檢查與其的網路連線。 <br></br>2.  檢查 Proxy 或防火牆設定。|
|System.Net.Http.HttpRequestException：傳送要求時發生錯誤。 ---> System.Net.WebException：遠端伺服器傳回一個錯誤：(407) 要求 Proxy 驗證。|因為 Proxy 設定錯誤而無法連線到 ATA 中心，所以部署程序已逾時。|請先停用 Proxy 設定再進行部署，然後再次啟用 Proxy 設定。 或者，您可以在 Proxy 中設定例外狀況。|
|System.Net.Sockets.SocketException：遠端主機已強制關閉現有的連線||使用下列其中一個選項： </br>在 ATA 閘道上啟用 TLS 1.0 </br>將登錄機碼設定為使用 SSL 和 TLS 的作業系統預設，以在 .Net 上啟用 TLS 1.2，方式如下：</br> `[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319] "SystemDefaultTlsVersions"=dword:00000001`</br> `[HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\v4.0.30319] "SystemDefaultTlsVersions"=dword:00000001`</br>`[HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\.NETFramework\v4.0.30319] "SchUseStrongCrypto"=dword:00000001` </br>`[HKEY_LOCAL_MACHINE\SOFTWARE\Wow6432Node\Microsoft\.NETFramework\v4.0.30319] " SchUseStrongCrypto"=dword:00000001`|
|錯誤 [\[]DeploymentModel[\]] 失敗的管理驗證 [\[]CurrentlyLoggedOnUser=<domain>\<username>Status=FailedAuthentication Exception=[\]]|ATA 閘道或 ATA 輕量型閘道的部署程序無法順利向 ATA 中心驗證|請從部署程序失敗所在的電腦開啟瀏覽器，並試試看能否連線到 ATA 主控台。 </br>若無法連線，請開始進行疑難排解，以了解瀏覽器為何無法向 ATA 中心驗證。 </br>可以檢查的事項： </br>Proxy 組態</br>網路問題</br>電腦上驗證的群組原則設定不同於 ATA 中心的設定。|





## <a name="ata-gateway-and-lightweight-gateway-issues"></a>ATA 閘道和輕量型閘道問題

> [!div class="mx-tableFixed"]
|問題|說明|解決方案|
|-------------|----------|---------|
|未從網域控制站收到流量，但觀察到監視警示|    未從透過 ATA 閘道使用連接埠鏡像的網域控制站收到流量|在 ATA 閘道擷取 NIC 上，停用 [進階設定] 中的這些功能：<br></br>接收區段聯合 (IPv4)<br></br>接收區段聯合 (IPv6)|
|系統會顯示此監視警示：**未分析部分網路流量**|如果您在 VMware 虛擬機器上有 ATA 閘道或輕量型閘道，就可能會收到此監視警示。 當 VMware 中的設定不相符時，就會發生此狀況。|請在 NIC 設定中將以下設定設為 **0** 或 [停用]：TsoEnable、LargeSendOffload、TSO Offload、Giant TSO Offload|ATA 閘道上已停用 TLS 1.0，但是 .Net 設定為使用 TLS 1.2|




## <a name="see-also"></a>另請參閱
- [ATA 必要條件](ata-prerequisites.md)
- [ATA 容量規劃](ata-capacity-planning.md)
- [設定事件收集](configure-event-collection.md)
- [設定 Windows 事件轉送](configure-event-collection.md#configuring-windows-event-forwarding)
- [查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
