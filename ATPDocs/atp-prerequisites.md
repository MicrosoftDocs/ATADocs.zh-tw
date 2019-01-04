---
title: Azure 進階威脅防護必要條件 | Microsoft Docs
description: 描述在環境中成功部署 Azure ATP 的需求
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 12/13/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 62c99622-2fe9-4035-9839-38fec0a353da
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 1fc3930fc4b38b396bda2c3ff50795d835910439
ms.sourcegitcommit: 1c657f269aaece71b2126df55a37f8c43851539a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/13/2018
ms.locfileid: "53335416"
---
適用對象：*Azure 進階威脅防護*



# <a name="azure-atp-prerequisites"></a>Azure ATP 必要條件
本文描述在您的環境中成功部署 Azure ATP 的需求。

>[!NOTE]
> 如需如何規劃資源和容量的相關資訊，請參閱 [Azure ATP 容量規劃](atp-capacity-planning.md)。


Azure ATP 是由 Azure ATP 雲端服務組成，其包含 Azure ATP 入口網站、Azure ATP 感應器和/或 Azure ATP 獨立感應器。 如需每種 Azure ATP 元件的詳細資訊，請參閱 [Azure ATP 架構](atp-architecture.md)。

若要建立 Azure ATP 執行個體，您必須使用具有至少一位全域/安全性系統管理員的 AAD 租用戶。 每個 Azure ATP 執行個體都支援多 Active Directory 樹系邊界，以及 Windows 2003 和更新版本的樹系功能等級 (FFL)。 

此必要條件指南分成下列各節，以確保您了解成功部署 Azure ATP 所需的一切項目。 

[開始之前](#before-you-start)：列出開始安裝之前應收集的資訊，以及您應具備的帳戶和網路實體。

[Azure ATP 入口網站](#azure-atp-workspace-management-portal-and-workspace-portal-requirements)：描述 Azure ATP 入口網站的瀏覽器需求。

[Azure ATP 感應器](#azure-atp-lightweight-sensor-requirements)：列出 Azure ATP 感應器的硬體及軟體需求。

[Azure ATP 獨立感應器](#azure-atp-sensor-requirements)：列出 Azure ATP 獨立感應器的硬體和軟體需求，以及必須在 Azure ATP 獨立感應器伺服器上進行的設定。

## <a name="before-you-start"></a>開始之前
本節列出在開始安裝 Azure ATP 前，您應收集的資訊及您應擁有的帳戶與網路實體資訊。

- 直接透過 [Office 365 入口網站](https://www.microsoft.com/cloud-platform/enterprise-mobility-security-pricing)或雲端解決方案提供者 (CSP) 授權模型，取得 Enterprise Mobility + Security 5 (EMS E5) 的授權。  

- 驗證您要在其中安裝 Azure ATP 感應器的網域控制站可網際網路連線至 Azure ATP 雲端服務。 Azure ATP 感應器支援使用 Proxy。 如需 Proxy 設定的詳細資訊，請參閱[為 Azure ATP 設定 Proxy](configure-proxy.md)。  

-   針對監視網域中的所有物件具有讀取存取權的**內部部署** AD 使用者帳戶和密碼。

    > [!NOTE]
    > 如果您已經在網域中設定不同組織單位 (OU) 的自訂 ACL，請確定選取的使用者具有讀取這些 OU 的權限。

-   如果您在 Azure ATP 獨立感應器上執行 Wireshark，在停止 Wireshark 擷取後，將需要重新啟動 Azure 進階威脅防護感應器服務。 否則，感應器會停止擷取流量。

- 如果您嘗試在設定了 NIC 小組介面卡的電腦上安裝 Azure ATP 感應器，則會收到安裝錯誤。 如果您想要在已設定 NIC 小組的電腦上安裝 Azure ATP 感應器，請參閱 [Azure ATP 感應器 NIC 小組問題](troubleshooting-atp-known-issues.md#nic-teaming)。

-    建議：使用者應該擁有「刪除的物件」容器的唯讀權限。 這可讓 Azure ATP 偵測到透過 Active Directory 進行的使用者刪除作業。 如需設定「已刪除物件」容器的唯讀權限相關資訊，請參閱[檢視或設定目錄物件的權限](https://technet.microsoft.com/library/cc816824%28v=ws.10%29.aspx) \(英文\) 文章中的＜變更刪除的物件容器的權限＞。

-   選擇性：沒有任何網路活動之使用者的使用者帳戶。 此帳戶設定為 Azure ATP Honeytoken 使用者。 如需詳細資訊，請參閱[設定排除項目和 Honeytoken 使用者](install-atp-step7.md)。

-   選擇性：在部署獨立感應器時，必須將 Windows 事件 4776、4732、4733、4728、4729、4756、4757 與 7045 轉送給 Azure ATP，以進一步增強 Azure ATP 對雜湊傳遞、暴力密碼破解、修改敏感性群組、Honey Token 偵測與建立惡意服務的抵禦能力。 Azure ATP 感應器自動支援這些事件。 在 Azure ATP 獨立感應器中，這些事件可從您的 SIEM 接收，或在網域控制站上設定 Windows 事件轉送來接收。 所收集的事件可提供 Azure ATP 透過網域控制站網路流量無法取得的額外資訊。

## <a name="azure-atp-portal-requirements"></a>Azure ATP 入口網站需求
您可透過瀏覽器來存取 Azure ATP 入口網站，其支援下列瀏覽器和設定︰
-   Microsoft Edge
-   Internet Explorer 第 10 版及更新版本
-   Google Chrome 4.0 和更新版本
-   螢幕解析度最低需求為 1700 像素
-   防火牆/Proxy 開啟 - 若要與 Azure ATP 雲端服務通訊，您必須在防火牆/Proxy 中針對 *.atp.azure.com 開啟連接埠 443。

 ![Azure ATP 架構圖表](media/ATP-architecture-topology.png)


> [!NOTE]
> 根據預設值，Azure ATP 最多支援 100 個感應器。 如果您想要安裝更多，請連絡 Azure ATP 支援。

## <a name="azure-atp-sensor-requirements"></a>Azure ATP 感應器需求
本節列出 Azure ATP 感應器的需求。
### <a name="general"></a>一般
Azure ATP 感應器可在執行 Windows Server 2008 R2 SP1 (不含 Server Core)、Windows Server 2012、Windows Server 2012 R2、Windows Server 2016 (包含 Core 但不含 Nano) 的網域控制站上安裝。

網域控制站可以是唯讀網域控制站 (RODC)。

若要讓網域控制站與雲端服務通訊，您必須在防火牆和 Proxy 中針對 *.atp.azure.com 開啟連接埠 443。

安裝期間會安裝 .Net Framework 4.7，並可能會要求網域控制站重新開機 (如果重新啟動已暫止)。


> [!NOTE]
> 至少需要 5 GB 的磁碟空間，建議要有 10 GB。 這包括 Azure ATP 二進位檔、Azure ATP 記錄檔和效能記錄檔所需的空間。

### <a name="server-specifications"></a>伺服器規格

Azure ATP 感應器在網域控制站上需要安裝至少兩個核心和 6 GB 的 RAM。
為了達到最佳效能，請將 Azure ATP 感應器的 [電源選項] 設定為 [高效能]。
Azure ATP 感應器可以部署在各種負載和大小的網域控制站上，依進出網域控制站的網路流量，以及安裝在該網域控制站上的資源數量而定。

>[!NOTE] 
> 作為虛擬機器執行時，將不支援動態記憶體或任何其他記憶體佔用功能。

如需 Azure ATP 感應器硬體需求的詳細資訊，請參閱 [Azure ATP 容量規劃](atp-capacity-planning.md)。

### <a name="time-synchronization"></a>時間同步

安裝感應器之伺服器和網域控制站的時間，必須同步到相差五分鐘內。

### <a name="network-adapters"></a>網路介面卡

Azure ATP 感應器可為所有網域控制站的網路介面卡監視其上的本機流量。 <br>
部署後，如果您想要修改監視的網路介面卡，可以使用 Azure ATP 入口網站。

執行 Windows 2008 R2 且啟用 Broadcom 網路介面卡小組的網域控制站不支援感應器。

### <a name="ports"></a>連接埠
下表列出 Azure ATP 感應器至少需要的連接埠：

|通訊協定|傳輸|Port|去/從|方向|
|------------|-------------|--------|-----------|-------------|
|**內部連接埠**|||||
|SSL (*.atp.azure.com)|TCP|443|Azure ATP 雲端服務|輸出|
|**內部連接埠**|||||
|DNS|TCP 和 UDP|53|DNS 伺服器|輸出|
|Netlogon (SMB、CIFS、SAM-R)|TCP/UDP|445|網路上的所有裝置|輸出|
|透過 RPC 的 NTLM|TCP|135|網路上的所有裝置|兩者|
|NetBIOS|UDP|137|網路上的所有裝置|兩者|
|Syslog (選擇性)|TCP/UDP|514，取決於設定|SIEM 伺服器|輸入|
|RADIUS|UDP|1813|RADIUS|輸入|
|TLS 至 RDP 連接埠|TCP|3389|網路上的所有裝置|兩者|

### <a name="windows-event-logs"></a>Windows 事件記錄檔
Azure ATP 偵測依賴特定的 Windows 事件記錄檔，其可由感應器從網域控制站剖析。 若要稽核正確的事件並將其包含在 Windows 事件記錄檔中，則網域控制站需要精確的進階稽核原則設定。 如需詳細資訊，請參閱[進階稽核原則檢查](atp-advanced-audit-policy.md)。


> [!NOTE]
> - 使用 Directory 服務使用者帳戶，感應器會查詢您組織中的端點以尋找使用 SAM-R (網路登入) 的本機系統管理員，以建置[橫向移動路徑圖表](use-case-lateral-movement-path.md)。 如需詳細資訊，請參閱[設定 SAM-R 必要權限](install-atp-step8-samr.md)。
> - 下列連接埠需要為 Azure ATP 獨立感應器在網路上的裝置上針對傳入開啟：
>   -   透過 RPC 的 NTLM (TCP 連接埠 135) (針對解析目的)
>   -   NetBIOS (UDP 連接埠 137) (針對解析目的)
>   -   RDP (TCP 連接埠 3389)，只提供 *Client hello* 的第一個套件作解析之用<br> 請注意，不會在任何連接埠上執行任何驗證。

## <a name="azure-atp-standalone-sensor-requirements"></a>Azure ATP 獨立感應器需求
本節列出 Azure ATP 獨立感應器的需求。
### <a name="general"></a>一般
Azure ATP 獨立感應器可安裝在執行 Windows Server 2012 R2 或 Windows Server 2016 (包括 Server Core) 的伺服器上。
Azure ATP 獨立感應器可以安裝在屬於網域或工作群組之成員的伺服器上。
Azure ATP 獨立感應器可以用來監視具 Windows Server 2003 或更新版本之網域功能等級的網域控制站。

若要讓獨立感應器與雲端服務通訊，您必須在防火牆和 Proxy 中針對 *.atp.azure.com 開啟連接埠 443。


如需使用虛擬機器與 Azure ATP 獨立感應器的相關資訊，請參閱[設定連接埠鏡像](configure-port-mirroring.md)。

> [!NOTE]
> 至少需要 5 GB 的磁碟空間，建議要有 10 GB。 這包括 Azure ATP 二進位檔、Azure ATP 記錄檔和效能記錄檔所需的空間。

### <a name="server-specifications"></a>伺服器規格
為了達到最佳效能，將 Azure ATP 獨立感應器的 [電源選項] 設定為 [高效能]。<br>
Azure ATP 獨立感應器可以支援監視多個網域控制站，依進出網域控制站的網路傳輸量而定。

>[!NOTE] 
> 作為虛擬機器執行時，將不支援動態記憶體或任何其他記憶體佔用功能。

如需 Azure ATP 獨立感應器硬體需求的詳細資訊，請參閱 [Azure ATP 容量規劃](atp-capacity-planning.md)。

### <a name="time-synchronization"></a>時間同步

安裝感應器之伺服器和網域控制站的時間，必須同步到相差五分鐘內。


### <a name="network-adapters"></a>網路介面卡
Azure ATP 獨立感應器需要至少一個管理介面卡和至少一個擷取介面卡︰

-   **管理介面卡** - 用於您公司網路上的通訊。 感應器會使用此配接器來查詢它正在保護的 DC，並對電腦帳戶執行解析。 <br>此介面卡應進行下列設定：

    -   靜態 IP 位址，包含預設閘道

    -   慣用和替代的 DNS 伺服器

    -   **此連線的 DNS 尾碼**應該是受監視之每個網域的網域 DNS 名稱。

        ![在進階 TCP/IP 設定中設定 DNS 尾碼](media/ATP-DNS-Suffix.png)

        > [!NOTE]
        > 如果 Azure ATP 獨立感應器是網域的成員，這可能會自動設定。

-   **擷取介面卡** - 用來擷取進出網域控制站的流量。

    > [!IMPORTANT]
    > -   設定擷取介面卡的連接埠鏡像做為網域控制站網路流量的目的地。 如需詳細資訊，請參閱[設定連接埠鏡像](configure-port-mirroring.md)。 一般而言，設定通訊埠鏡像必須與網路或虛擬化團隊合作。
    > -   為您的環境設定靜態、無法路由傳送的 IP 位址 (使用 /32 遮罩)，沒有預設感應器閘道也沒有 DNS 伺服器位址。 例如，10.10.0.10/32。 這會確保擷取網路介面卡可以擷取最大的流量，而且管理網路介面卡會用於傳送和接收必要的網路流量。

### <a name="ports"></a>連接埠
下表列出 Azure ATP 獨立感應器在管理介面卡上至少需要設定的連接埠：

|通訊協定|傳輸|Port|去/從|方向|
|------------|-------------|--------|-----------|-------------|
|**內部連接埠**|||||
|SSL (*.atp.azure.com)|TCP|443|Azure ATP 雲端服務|輸出|
|**內部連接埠**|||||
|LDAP|TCP 和 UDP|389|網域控制站|輸出|
|安全的 LDAP (LDAPS)|TCP|636|網域控制站|輸出|
|LDAP 至通用類別|TCP|3268|網域控制站|輸出|
|LDAPS 至通用類別|TCP|3269|網域控制站|輸出|
|Kerberos|TCP 和 UDP|88|網域控制站|輸出|
|Netlogon (SMB、CIFS、SAM-R)|TCP 和 UDP|445|網路上的所有裝置|輸出|
|Windows Time|UDP|123|網域控制站|輸出|
|DNS|TCP 和 UDP|53|DNS 伺服器|輸出|
|透過 RPC 的 NTLM|TCP|135|網路上的所有裝置|兩者|
|NetBIOS|UDP|137|網路上的所有裝置|兩者|
|Syslog (選擇性)|TCP/UDP|514，取決於設定|SIEM 伺服器|輸入|
|RADIUS|UDP|1813|RADIUS|輸入|
|TLS 至 RDP|TCP|3389|網路上的所有裝置|兩者|

> [!NOTE]
> - 使用 Directory 服務使用者帳戶，感應器會查詢您組織中的端點以尋找使用 SAM-R (網路登入) 的本機系統管理員，以建置[橫向移動路徑圖表](use-case-lateral-movement-path.md)。 如需詳細資訊，請參閱[設定 SAM-R 必要權限](install-atp-step8-samr.md)。
> - 下列連接埠需要為 Azure ATP 獨立感應器在網路上的裝置上針對傳入開啟：
>   -   透過 RPC 的 NTLM (TCP 連接埠 135) (針對解析目的)
>   -   NetBIOS (UDP 連接埠 137) (針對解析目的)
>   -   RDP (TCP 連接埠 3389)，只提供 *Client hello* 的第一個套件作解析之用<br> 請注意，不會在任何連接埠上執行任何驗證。



## <a name="see-also"></a>另請參閱
- [Azure ATP 調整大小工具](http://aka.ms/aatpsizingtool) \(英文\)
- [Azure ATP 架構](atp-architecture.md)
- [安裝 Azure ATP](install-atp-step1.md)
- [查看 Azure ATP 論壇！](https://aka.ms/azureatpcommunity)

