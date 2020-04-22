---
title: Azure 進階威脅防護先決條件
description: 描述在環境中成功部署 Azure ATP 的需求
keywords: ''
author: shsagir
ms.author: shsagir
manager: rkarlin
ms.date: 03/15/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 62c99622-2fe9-4035-9839-38fec0a353da
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 185d3e8c70c11e06d1125a634c3cd9c12e2076c8
ms.sourcegitcommit: 63be53de5b84eabdeb8c006438dab45bd35a4ab7
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "79414262"
---
# <a name="azure-atp-prerequisites"></a>Azure ATP 必要條件

本文描述在您的環境中成功部署 Azure ATP 的需求。

>[!NOTE]
> 如需如何規劃資源和容量的相關資訊，請參閱 [Azure ATP 容量規劃](atp-capacity-planning.md)。

Azure ATP 是由 Azure ATP 雲端服務組成，其包含 Azure ATP 入口網站與 Azure ATP 感應器。 如需每種 Azure ATP 元件的詳細資訊，請參閱 [Azure ATP 架構](atp-architecture.md)。

Azure ATP 能保護您的內部部署 Active Directory 使用者及 (或) 同步至您 Azure Active Directory 的使用者。 若要保護僅包含 AAD 使用者的環境，請參閱 [AAD 身分識別保護](https://docs.microsoft.com/azure/active-directory/identity-protection/overview) \(部分機器翻譯\)。

若要建立 Azure ATP 執行個體，您必須使用具有至少一位全域/安全性系統管理員的 AAD 租用戶。 每個 Azure ATP 執行個體都支援多 Active Directory 樹系邊界，以及 Windows 2003 和更新版本的樹系功能等級 (FFL)。

此必要條件指南分成下列各節，以確保您了解成功部署 Azure ATP 所需的一切項目。

[開始之前](#before-you-start)：列出開始安裝之前應收集的資訊，以及您應具備的帳戶和網路實體。

[Azure ATP 入口網站](#azure-atp-portal-requirements)：描述 Azure ATP 入口網站的瀏覽器需求。

[Azure ATP 感應器](#azure-atp-sensor-requirements)：列出 Azure ATP 感應器的硬體及軟體需求。

[Azure ATP 獨立感應器](#azure-atp-standalone-sensor-requirements)：Azure ATP 獨立感應器會安裝在專用伺服器上，而且要求必須在網域控制站上設定連接埠鏡像以接收網路流量。

> [!NOTE]
> Azure ATP 獨立感應器無法支援所有資料來源類型，因而會導致遺漏偵測。 若要完整涵蓋您的環境，建議您部署 Azure ATP 感應器。

## <a name="before-you-start"></a>在您開始使用 Intune 之前

本節列出在開始安裝 Azure ATP 前，您應收集的資訊及您應擁有的帳戶與網路實體資訊。

- 直接透過 [Microsoft 365 入口網站](https://www.microsoft.com/cloud-platform/enterprise-mobility-security-pricing)取得 Enterprise Mobility + Security 5 (EMS E5) 的授權，或使用雲端解決方案合作夥伴 (CSP) 授權模型。 另外也提供獨立 Azure ATP 授權。

- 驗證您要在其中安裝 Azure ATP 感應器的網域控制站可網際網路連線至 Azure ATP 雲端服務。 Azure ATP 感應器支援使用 Proxy。 如需 Proxy 設定的詳細資訊，請參閱[為 Azure ATP 設定 Proxy](configure-proxy.md)。

- 至少下列其中一個目錄服務帳戶，該帳戶必須有所提及網域中所有物件的讀取權限：
  - **標準** AD 使用者帳戶與密碼。 為執行 Windows Server 2008 R2 SP1 的感應器所需。
  - **群組受管理的服務帳戶** (gMSA)。 需要 Windows Server 2012 或更新版本。  
  所有感應器都必須有可擷取 gMSA 帳戶密碼的權限。  
  若要了解 gMSA 帳戶，請參閱[開始使用群組受管理的服務帳戶](/windows-server/security/group-managed-service-accounts/getting-started-with-group-managed-service-accounts#BKMK_CreateGMSA)。

    下表顯示哪些 AD 使用者帳戶可以搭配哪些伺服器版本使用：

    |帳戶類型|Windows Server 2008 R2 SP1|Windows Server 2012 或更新版本|
    |---|---|---|
    |**標準** AD 使用者帳戶|是|是|
    |**gMSA** 帳戶|否|是|

    > [!NOTE]
    >
    > - 針對執行 Windows Server 2012 與更新版本的感應器電腦，我們建議使用 **gMSA** 帳戶，以獲得改善的安全性與自動密碼管理。
    > - 若您有多個感應器，其中有些執行 Windows Server 2008，而其他執行 Windows Server 2012 或更新版本，則除了使用 **gMSA** 帳戶的建議之外，您也必須使用至少一個**標準** AD 使用者帳戶。
    > - 如果您已經在網域中設定不同組織單位 (OU) 的自訂 ACL，請確定選取的使用者具有讀取這些 OU 的權限。

- 如果您在 Azure ATP 獨立感應器上執行 Wireshark，在停止 Wireshark 擷取後，重新啟動 Azure 進階威脅防護感應器服務。 如果您未重新啟動感應器服務，感應器會停止擷取流量。

- 如果您嘗試在設定了 NIC 小組介面卡的電腦上安裝 Azure ATP 感應器，則會收到安裝錯誤。 如果您想要在已設定 NIC 小組的電腦上安裝 Azure ATP 感應器，請參閱 [Azure ATP 感應器 NIC 小組問題](troubleshooting-atp-known-issues.md#nic-teaming)。

- **Deleted Objects** 容器建議：使用者應該擁有「刪除的物件」容器的唯讀權限。 這個容器的唯讀權限可讓 Azure ATP 偵測從 Active Directory 中刪除使用者的情形。 如需在 Deleted Objects 容器設定唯讀權限的相關資訊，請參閱 [View or Set Permissions on a Directory Object](https://technet.microsoft.com/library/cc816824%28v=ws.10%29.aspx) (檢視或設定目錄物件的權限) 文章中的 **Changing permissions on a deleted object container** (變更已刪除物件的容器權限) 一節。

- 選擇性的 **Honeytoken**：沒有任何網路活動之使用者的使用者帳戶。 此帳戶設定為 Azure ATP Honeytoken 使用者。 如需使用 Honeytoken 的詳細資訊，請參閱[設定排除專案和 Honeytoken 使用者](install-atp-step7.md)。

- 選用：在部署獨立感應器時，必須將 Windows 事件 4726、4728、4729、4730、4732、4733、4743、4753、4756、4757、4758、4763、4776、7045 與 8004 轉送給 Azure ATP，以在對敏感性群組與可疑服務建立偵測能力之外進一步增強 Azure ATP 驗證型偵測能力。  Azure ATP 感應器自動支援這些事件。 在 Azure ATP 獨立感應器中，這些事件可從您的 SIEM 接收，或在網域控制站上設定 Windows 事件轉送來接收。 所收集的事件可提供 Azure ATP 透過網域控制站網路流量無法取得的額外資訊。

## <a name="azure-atp-portal-requirements"></a>Azure ATP 入口網站需求

您可透過瀏覽器來存取 Azure ATP 入口網站，其支援下列瀏覽器和設定︰

- 支援 TLS 1.2 的瀏覽器，例如：
  - Microsoft Edge
  - Internet Explorer 11 版與更新版本
  - Google Chrome 30.0 與更新版本
- 螢幕解析度最低需求為 1700 像素
- 防火牆/Proxy 開啟 - 若要與 Azure ATP 雲端服務通訊，您必須在防火牆/Proxy 中開啟 *.atp.azure.com 連接埠 443。

    > [!NOTE]
    > 您也可以使用 Azure 服務標籤 (**AzureAdvancedThreatProtection**) 來啟用對 Azure ATP 的存取權。 如需服務標籤的詳細資訊，請參閱[虛擬網路服務標籤](https://docs.microsoft.com/azure/virtual-network/service-tags-overview)或[下載服務標籤](https://www.microsoft.com/download/details.aspx?id=56519)檔案。

 ![Azure ATP 架構圖表](media/azure-atp-architecture.png)

> [!NOTE]
> 根據預設值，Azure ATP 最多支援 200 個感應器。 如果您想要安裝更多感應器，請連絡 Azure ATP 支援。

## <a name="azure-atp-network-name-resolution-nnr-requirements"></a>Azure ATP 網路名稱解析 (NNR) 需求

網路名稱解析 (NNR) 是 Azure ATP 功能的主要元件。 若要讓 Azure ATP 服務正常運作，Azure ATP 感應器必須至少能存取下列其中一個 NNR 方法：

1. **透過 RPC 的 NTLM** (TCP 連接埠 135)
2. **NetBIOS** (UDP 連接埠 137)
3. **RDP** (TCP 連接埠 3389) - 只有 Client hello 的第一個封包
4. **使用 IP 位址的反向 DNS 查閱來查詢 DNS 伺服器** (UDP 53)

若要讓方法 1、2 與 3 正常運作，必須開啟從從 Azure ATP 感應器到網路上裝置的相關連入連接埠。 若要深入了解 Azure ATP 與 NNR，請參閱 [Azure ATP NNR 原則](atp-nnr-policy.md)。

## <a name="azure-atp-sensor-requirements"></a>Azure ATP 感應器需求

本節列出 Azure ATP 感應器的需求。

### <a name="general"></a>一般

> [!NOTE]
> 使用 Server 2019 時，請確定已安裝 [KB4487044](https://support.microsoft.com/help/4487044/windows-10-update-kb4487044)。 系統將會自動停止安裝在未安裝此更新之 2019 伺服器上的 Azure ATP 感應器。

Azure ATP 感應器可在執行 Windows Server 2008 R2 SP1 (不含 Server Core)、Windows Server 2012、Windows Server 2012 R2、Windows Server 2016 (包含 Windows Server Core 但不含 Windows Nano 伺服器)、Windows Server 2019 (包含 Windows Core 但不含 Windows Nano 伺服器) 的網域控制站上安裝。

網域控制站可以是唯讀網域控制站 (RODC)。

若要讓網域控制站與雲端服務通訊，您必須在防火牆和 Proxy 中針對 *.atp.azure.com 開啟連接埠 443。

安裝期間會安裝 .Net Framework 4.7，並可能會要求網域控制站重新開機 (如果重新啟動已暫止)。

> [!NOTE]
> 至少需要 5 GB 的磁碟空間，建議要有 10 GB。 這包括 Azure ATP 二進位檔、Azure ATP 記錄檔和效能記錄檔所需的空間。

### <a name="server-specifications"></a>伺服器規格

Azure ATP 感應器在網域控制站上需要安裝至少 2 個核心和 6 GB 的 RAM。
為了達到最佳效能，請將 Azure ATP 感應器的 [電源選項]  設定為 [高效能]  。

Azure ATP 感應器可以部署在各種負載和大小的網域控制站上，依進出網域控制站的網路流量，以及安裝的資源數量而定。

針對 Windows 作業系統 2008 R2 與 2012，[多處理器群組](https://docs.microsoft.com/windows/win32/procthread/processor-groups)模式中不支援 Azure ATP 感應器。 如需有關多處理器群組模式的詳細資訊，請參閱[疑難排解](troubleshooting-atp-known-issues.md#multi-processor-group-mode)。

>[!NOTE]
> 作為虛擬機器執行時，將不支援動態記憶體或任何其他記憶體佔用功能。

如需 Azure ATP 感應器硬體需求的詳細資訊，請參閱 [Azure ATP 容量規劃](atp-capacity-planning.md)。

### <a name="time-synchronization"></a>時間同步

安裝感應器之伺服器和網域控制站的時間，必須同步到相差五分鐘內。

### <a name="network-adapters"></a>網路介面卡

Azure ATP 感應器可為所有網域控制站的網路介面卡監視其上的本機流量。  
部署後，可以使用 Azure ATP 入口網站來修改監視的網路介面卡。

執行 Windows 2008 R2 且啟用 Broadcom 網路介面卡小組的網域控制站不支援感應器。

### <a name="ports"></a>連接埠

下表列出 Azure ATP 感應器至少需要的連接埠：

|通訊協定|傳輸|Port|去/從|方向|
|------------|-------------|--------|-----------|-------------|
|**內部連接埠**|||||
|SSL (*.atp.azure.com)|TCP|443|Azure ATP 雲端服務|輸出|
|SSL (本機主機)|TCP|444|本機主機|兩者|
|**內部連接埠**|||||
|DNS|TCP 和 UDP|53|DNS 伺服器|輸出|
|Netlogon (SMB、CIFS、SAM-R)|TCP/UDP|445|網路上的所有裝置|輸出|
|Syslog (選擇性)|TCP/UDP|514，取決於設定|SIEM 伺服器|輸入|
|RADIUS|UDP|1813|RADIUS|輸入|

### <a name="windows-event-logs"></a>Windows 事件記錄檔

Azure ATP 偵測仰賴下列特定 Windows 事件記錄檔，這些記錄檔可由感應器從您的網域控制站剖析。4726、4728、4729、4730、4732、4733、4743、4753、4756、4757、4758、4763、4776、7045 與 8004。 若要正確稽核事件並將其包含在 Windows 事件記錄檔中，網域控制站需要精確的進階稽核原則設定。 如需有關設定正確原則的詳細資訊，請參閱[進階稽核原則檢查](atp-advanced-audit-policy.md)。 若要確定已依服務所需[稽核 Windows 事件 8004](configure-windows-event-collection.md#ntlm-authentication-using-windows-event-8004)，請檢閱您的 [NTLM 稽核設定](https://blogs.technet.microsoft.com/askds/2009/10/08/ntlm-blocking-and-you-application-analysis-and-auditing-methodologies-in-windows-7/) \(英文\)。

> [!NOTE]
>
> - 使用 Directory 服務使用者帳戶，感應器會查詢您組織中的端點以尋找使用 SAM-R (網路登入) 的本機系統管理員，以建置[橫向移動路徑圖表](use-case-lateral-movement-path.md)。 如需詳細資訊，請參閱[設定 SAM-R 必要權限](install-atp-step8-samr.md)。

## <a name="azure-atp-standalone-sensor-requirements"></a>Azure ATP 獨立感應器需求

本節列出 Azure ATP 獨立感應器的需求。

> [!NOTE]
> Azure ATP 獨立感應器無法支援所有資料來源類型，因而會導致遺漏偵測。 若要完整涵蓋您的環境，建議您部署 Azure ATP 感應器。

### <a name="general"></a>一般

Azure ATP 獨立感應器可安裝在執行 Windows Server 2012 R2 或 Windows Server 2016 (包括 Server Core) 的伺服器上。
Azure ATP 獨立感應器可以安裝在屬於網域或工作群組之成員的伺服器上。
Azure ATP 獨立感應器可以用來監視具 Windows Server 2003 或更新版本之網域功能等級的網域控制站。

若要讓獨立感應器與雲端服務通訊，您必須在防火牆和 Proxy 中針對 *.atp.azure.com 開啟連接埠 443。

如需使用虛擬機器與 Azure ATP 獨立感應器的相關資訊，請參閱[設定連接埠鏡像](configure-port-mirroring.md)。

> [!NOTE]
> 至少需要 5 GB 的磁碟空間，建議要有 10 GB。 這包括 Azure ATP 二進位檔、Azure ATP 記錄檔和效能記錄檔所需的空間。

### <a name="server-specifications"></a>伺服器規格

為了達到最佳效能，將 Azure ATP 獨立感應器的 [電源選項]  設定為 [高效能]  。<br>
Azure ATP 獨立感應器可以支援監視多個網域控制站，依進出網域控制站的網路傳輸量而定。

>[!NOTE]
> 作為虛擬機器執行時，將不支援動態記憶體或任何其他記憶體佔用功能。

如需 Azure ATP 獨立感應器硬體需求的詳細資訊，請參閱 [Azure ATP 容量規劃](atp-capacity-planning.md)。

### <a name="time-synchronization"></a>時間同步

安裝感應器之伺服器和網域控制站的時間，必須同步到相差五分鐘內。

### <a name="network-adapters"></a>網路介面卡

Azure ATP 獨立感應器需要至少一個管理介面卡和至少一個擷取介面卡︰

- **管理介面卡** - 用於您公司網路上的通訊。 感應器會使用此配接器來查詢其正在保護的 DC，並對電腦帳戶執行解析。 <br>此介面卡應進行下列設定：

    - 靜態 IP 位址，包含預設閘道

    - 慣用和替代的 DNS 伺服器

    - **此連線的 DNS 尾碼**應該是受監視之每個網域的網域 DNS 名稱。

        ![在進階 TCP/IP 設定中設定 DNS 尾碼](media/ATP-DNS-Suffix.png)

        > [!NOTE]
        > 如果 Azure ATP 獨立感應器是網域的成員，這可能會自動設定。

- **擷取介面卡** - 用來擷取進出網域控制站的流量。

    > [!IMPORTANT]
    >
    > - 設定擷取介面卡的連接埠鏡像做為網域控制站網路流量的目的地。 如需詳細資訊，請參閱[設定連接埠鏡像](configure-port-mirroring.md)。 一般而言，設定通訊埠鏡像必須與網路或虛擬化團隊合作。
    > - 為您的環境設定靜態、無法路由傳送的 IP 位址 (使用 /32 遮罩)，沒有預設感應器閘道也沒有 DNS 伺服器位址。 例如，10.10.0.10/32。 這會確保擷取網路介面卡可以擷取最大的流量，而且管理網路介面卡會用於傳送和接收必要的網路流量。

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
|Syslog (選擇性)|TCP/UDP|514，取決於設定|SIEM 伺服器|輸入|
|RADIUS|UDP|1813|RADIUS|輸入|

> [!NOTE]
>
> - 使用 Directory 服務使用者帳戶，感應器會查詢您組織中的端點以尋找使用 SAM-R (網路登入) 的本機系統管理員，以建置[橫向移動路徑圖表](use-case-lateral-movement-path.md)。 如需詳細資訊，請參閱[設定 SAM-R 必要權限](install-atp-step8-samr.md)。

## <a name="see-also"></a>另請參閱

- [Azure ATP 調整大小工具](https://aka.ms/aatpsizingtool) \(英文\)
- [Azure ATP 架構](atp-architecture.md)
- [安裝 Azure ATP](install-atp-step1.md)
- [網路名稱解析 (NNR)](atp-nnr-policy.md)
- [查看 Azure ATP 論壇！](https://aka.ms/azureatpcommunity)
