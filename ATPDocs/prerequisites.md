---
title: 適用於身分識別的 Microsoft Defender 先決條件
description: 描述適用於身分識別的 Microsoft Defender 在環境中成功部署的需求
ms.date: 12/23/2020
ms.topic: overview
ms.openlocfilehash: cb925a0b2bc2767367b6d3adabd5cb7dabcffa00
ms.sourcegitcommit: 57dd3e4663346db3542cf9e755dac135c5e75125
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/11/2021
ms.locfileid: "98062547"
---
# <a name="product-long-prerequisites"></a>[!INCLUDE [Product long](includes/product-long.md)] 先決條件

本文描述在環境中成功部署 [!INCLUDE [Product long](includes/product-long.md)] 的條件需求。

>[!NOTE]
> 如需如何規劃資源和容量的資訊，請參閱 [[!INCLUDE [Product short](includes/product-short.md)] 容量規劃](capacity-planning.md)。

[!INCLUDE [Product short](includes/product-short.md)] 是由 [!INCLUDE [Product short](includes/product-short.md)] 雲端服務所組成，其中包含 [!INCLUDE [Product short](includes/product-short.md)] 入口網站與 [!INCLUDE [Product short](includes/product-short.md)] 感應器。 如需每個 [!INCLUDE [Product short](includes/product-short.md)] 元件的詳細資訊，請參閱 [[!INCLUDE [Product short](includes/product-short.md)] 架構](architecture.md)。

[!INCLUDE [Product short](includes/product-short.md)] 能保護內部部署 Active Directory 使用者及/或同步至 Azure Active Directory 的使用者。 若要保護僅包含 AAD 使用者的環境，請參閱 [AAD 身分識別保護](/azure/active-directory/identity-protection/overview) \(部分機器翻譯\)。

若要建立 [!INCLUDE [Product short](includes/product-short.md)] 執行個體，您必須使用具有至少一位全域/安全性系統管理員的 AAD 租用戶。 每個 [!INCLUDE [Product short](includes/product-short.md)] 執行個體都支援多 Active Directory 樹系邊界，以及 Windows 2003 和更新版本的樹系功能等級 (FFL)。

此先決條件指南分成下列各節，以確保您了解成功部署 [!INCLUDE [Product short](includes/product-short.md)] 所需的一切項目。

[開始之前](#before-you-start)：列出開始安裝之前應收集的資訊，以及您應具備的帳戶和網路實體。

[[!INCLUDE [Product short](includes/product-short.md)] 入口網站](#azure-atp-portal-requirements)：描述 [!INCLUDE [Product short](includes/product-short.md)] 入口網站的瀏覽器需求。

[[!INCLUDE [Product short](includes/product-short.md)] 感應器](#azure-atp-sensor-requirements)：列出 [!INCLUDE [Product short](includes/product-short.md)] 感應器的硬體及軟體需求。

[[!INCLUDE [Product short](includes/product-short.md)] 獨立感應器](#azure-atp-standalone-sensor-requirements)：[!INCLUDE [Product short](includes/product-short.md)] 獨立感應器會安裝在專用伺服器上，且要求必須在網域控制站上設定連接埠鏡像以接收網路流量。

> [!NOTE]
> [!INCLUDE [Product short](includes/product-short.md)] 獨立感應器不會收集 Windows 事件追蹤 (ETW) 的記錄項目，無法提供多種偵測的資料。 若要完整涵蓋您的環境，建議您部署[!INCLUDE [Product short](includes/product-short.md)] 感應器。

## <a name="before-you-start"></a>在您開始使用 Intune 之前

本節列出在開始安裝 [!INCLUDE [Product short](includes/product-short.md)] 前，所應收集資訊及應擁有的帳戶與網路實體資訊。

- 直接透過 [Microsoft 365 入口網站](https://www.microsoft.com/cloud-platform/enterprise-mobility-security-pricing)取得 Enterprise Mobility + Security 5 (EMS E5) 的授權，或使用雲端解決方案合作夥伴 (CSP) 授權模型。 另外也提供獨立 [!INCLUDE [Product short](includes/product-short.md)] 授權。

- 驗證您要在其中安裝 [!INCLUDE [Product short](includes/product-short.md)] 感應器的網域控制站可網際網路連線至 [!INCLUDE [Product short](includes/product-short.md)] 雲端服務。 [!INCLUDE [Product short](includes/product-short.md)] 感應器支援使用 Proxy。 如需 Proxy 設定的詳細資訊，請參閱[為 [!INCLUDE [Product short](includes/product-short.md)] 設定 Proxy](configure-proxy.md)。

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
    > - 若您有多個感應器，其中有些執行 Windows Server 2008，而其他執行 Windows Server 2012 或更新版本，則除了使用 **gMSA** 帳戶的建議之外，您也必須使用至少一個 **標準** AD 使用者帳戶。
    > - 如果您已經在網域中設定不同組織單位 (OU) 的自訂 ACL，請確定選取的使用者具有讀取這些 OU 的權限。

- 如果在 [!INCLUDE [Product short](includes/product-short.md)] 獨立感應器上執行 Wireshark，在停止 Wireshark 擷取後，請重新啟動 [!INCLUDE [Product short](includes/product-short.md)] 感應器服務。 如果您未重新啟動感應器服務，感應器會停止擷取流量。

- 如果嘗試在具備 NIC 小組介面卡的電腦上安裝 [!INCLUDE [Product short](includes/product-short.md)] 感應器，您將會接收到安裝錯誤。 如果想要在具備 NIC 小組的電腦上安裝 [!INCLUDE [Product short](includes/product-short.md)] 感應器，請參閱 [[!INCLUDE [Product short](includes/product-short.md)] 感應器 NIC 小組問題](troubleshooting-known-issues.md#nic-teaming)。

- **Deleted Objects** 容器建議：使用者應該擁有「刪除的物件」容器的唯讀權限。 這個容器的唯讀權限可讓 [!INCLUDE [Product short](includes/product-short.md)] 偵測從 Active Directory 中刪除使用者的情形。 如需在 Deleted Objects 容器設定唯讀權限的相關資訊，請參閱 [View or Set Permissions on a Directory Object](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc816824(v=ws.10)) (檢視或設定目錄物件的權限) 文章中的 **Changing permissions on a deleted object container** (變更已刪除物件的容器權限) 一節。

- 選擇性的 **Honeytoken**：沒有任何網路活動之使用者的使用者帳戶。 此帳戶設定為 [!INCLUDE [Product short](includes/product-short.md)] Honeytoken 使用者。 如需使用 Honeytoken 的詳細資訊，請參閱[設定排除專案和 Honeytoken 使用者](install-step7.md)。

- 選用：在部署獨立感應器時，必須將 [Windows 事件](configure-windows-event-collection.md#configure-event-collection)轉送給 [!INCLUDE [Product short](includes/product-short.md)]，以在敏感性群組與可疑服務建立偵測能力之外，進一步增強 [!INCLUDE [Product short](includes/product-short.md)] 驗證型偵測能力。  [!INCLUDE [Product short](includes/product-short.md)] 感應器會自動收到這些事件。 在 [!INCLUDE [Product short](includes/product-short.md)] 獨立感應器中，這些事件可從 SIEM 接收，或在網域控制站上設定 Windows 事件轉送來接收。 所收集的事件可為[!INCLUDE [Product short](includes/product-short.md)] 提供透過網域控制站網路流量無法取得的額外資訊。

<a name="azure-atp-portal-requirements"></a>

## <a name="product-short-portal-requirements"></a>[!INCLUDE [Product short](includes/product-short.md)] 入口網站需求

您可透過瀏覽器來存取 [!INCLUDE [Product short](includes/product-short.md)] 入口網站，其支援下列瀏覽器和設定︰

- 支援 TLS 1.2 的瀏覽器，例如：
  - Microsoft Edge
  - Internet Explorer 11 版與更新版本
  - Google Chrome 30.0 與更新版本
- 螢幕解析度最低需求為 1700 像素
- 防火牆/Proxy 開啟 - 若要與 [!INCLUDE [Product short](includes/product-short.md)] 雲端服務通訊，則必須在防火牆/Proxy 中開啟 *.atp.azure.com 連接埠 443。

    > [!NOTE]
    > 您也可以使用 Azure 服務標籤 (**AzureAdvancedThreatProtection**) 來啟用對 [!INCLUDE [Product short](includes/product-short.md)] 的存取權。 如需服務標籤的詳細資訊，請參閱[虛擬網路服務標籤](/azure/virtual-network/service-tags-overview)或[下載服務標籤](https://www.microsoft.com/download/details.aspx?id=56519)檔案。

 ![[!INCLUDE [Product short](includes/product-short.md)] 架構圖表](media/architecture-topology.png)

> [!NOTE]
> 根據預設，[!INCLUDE [Product short](includes/product-short.md)] 最多支援 200 個感應器。 如果想要安裝更多感應器，請連絡 [!INCLUDE [Product short](includes/product-short.md)] 支援。

## <a name="product-short-network-name-resolution-nnr-requirements"></a>[!INCLUDE [Product short](includes/product-short.md)] 網路名稱解析 (NNR) 需求

網路名稱解析 (NNR) 是 [!INCLUDE [Product short](includes/product-short.md)] 功能的主要元件。 為將 IP 位址解析成電腦名稱，[!INCLUDE [Product short](includes/product-short.md)] 感應器會使用下列方法來查閱 IP 位址：

- 透過 RPC 的 NTLM (TCP 連接埠 135)
- NetBIOS (UDP 連接埠 137)
- RDP (TCP 連接埠 3389) - 只有 **Client hello** 的第一個封包
- 使用 IP 位址的反向 DNS 查閱來查詢 DNS 伺服器 (UDP 53)

若要讓前三個方法正常運作，必須開啟從 [!INCLUDE [Product short](includes/product-short.md)] 感應器到網路上裝置的相關連入連接埠。 若要深入了解 [!INCLUDE [Product short](includes/product-short.md)] 和 NNR，請參閱 [[!INCLUDE [Product short](includes/product-short.md)] NNR 原則](nnr-policy.md)。

為獲得最佳結果，建議使用所有方法。 如果無法這麼做，您應該使用 DNS 查閱方法與至少一個其他方法。

<a name="azure-atp-sensor-requirements"></a>

## <a name="product-short-sensor-requirements"></a>[!INCLUDE [Product short](includes/product-short.md)] 感應器需求

本節會列出 [!INCLUDE [Product short](includes/product-short.md)] 感應器的需求。

### <a name="general"></a>一般

[!INCLUDE [Product short](includes/product-short.md)] 感應器支援在執行 Windows Server 2008 R2 SP1 (不含 Server Core)、Windows Server 2012、Windows Server 2012 R2、Windows Server 2016 (包含 Server Core 但不含 Nano 伺服器)、Windows Server 2019\* (包含 Server Core 但不含 Nano 伺服器) 的網域控制站與 Active Directory 同盟服務 (AD FS) 上安裝，如下表所示。

| 作業系統版本   | 具備桌面體驗的伺服器 | Server Core | Nano Server    | 支援的安裝  |
| -------------------------- | ------------------------------ | ----------- | -------------- | ------------------------ |
| Windows Server 2008 R2 SP1 | &#10004;                       | &#10060;    | 不適用 | 網域控制站        |
| Windows Server 2012        | &#10004;                       | &#10004;    | 不適用 | 網域控制站        |
| Windows Server 2012 R2     | &#10004;                       | &#10004;    | 不適用 | 網域控制站        |
| Windows Server 2016        | &#10004;                       | &#10004;    | &#10060;       | 網域控制站、AD FS |
| Windows Server 2019\*      | &#10004;                       | &#10004;    | &#10060;       | 網域控制站、AD FS |

\* 需要 [KB4487044](https://support.microsoft.com/help/4487044/windows-10-update-kb4487044) 或更新的累積更新。 如果系統目錄中 *ntdsai* 檔案的檔案版本早於 *10.0.17763.316*，則在沒有此更新之 Server 2019 上安裝的感應器會自動停止。

網域控制站可以是唯讀網域控制站 (RODC)。

若要讓網域控制站與 AD FS 上執行的感應器與雲端服務通訊，您必須在防火牆和 Proxy 中針對 \*.atp.azure.com 開啟連接埠 443。

在安裝期間，如果未安裝 .Net Framework 4.7 或更新版本，則會安裝 .Net Framework 4.7，而且可能需要將伺服器重新開機。 如果有擱置中的重新啟動，可能也需要重新開機。

> [!NOTE]
> 至少需要 5 GB 的磁碟空間，建議要有 10 GB。 這包括 [!INCLUDE [Product short](includes/product-short.md)] 二進位檔、[!INCLUDE [Product short](includes/product-short.md)] 記錄檔以及效能記錄檔所需的空間。

### <a name="server-specifications"></a>伺服器規格

[!INCLUDE [Product short](includes/product-short.md)] 感應器在網域控制站上需要安裝至少 2 個核心和 6 GB 的 RAM。
為取得最佳化效能，請將執行 [!INCLUDE [Product short](includes/product-short.md)] 感應器的電腦其 [電源選項] 設定為 [高效能]。

[!INCLUDE [Product short](includes/product-short.md)] 感應器可部署在具有各種負載和大小的網域控制站或 AD FS 伺服器上，依進出伺服器的網路流量，以及已安裝的資源數量而定。

針對 Windows 作業系統 2008 R2 與 2012，[多處理器群組](/windows/win32/procthread/processor-groups)模式中不支援[!INCLUDE [Product short](includes/product-short.md)] 感應器。 如需有關多處理器群組模式的詳細資訊，請參閱[疑難排解](troubleshooting-known-issues.md#multi-processor-group-mode)。

>[!NOTE]
> 作為虛擬機器執行時，將不支援動態記憶體或任何其他記憶體佔用功能。

如需 [!INCLUDE [Product short](includes/product-short.md)] 感應器硬體需求的詳細資訊，請參閱 [[!INCLUDE [Product short](includes/product-short.md)] 容量規劃](capacity-planning.md)。

### <a name="time-synchronization"></a>時間同步

安裝感應器之伺服器和網域控制站的時間，必須同步到相差五分鐘內。

### <a name="network-adapters"></a>網路介面卡

[!INCLUDE [Product short](includes/product-short.md)] 感應器可為所有網域控制站的網路介面卡監視其上本機流量。  
部署後，可使用 [!INCLUDE [Product short](includes/product-short.md)] 入口網站來修改監視的網路介面卡。

執行 Windows 2008 R2 且啟用 Broadcom 網路介面卡小組的網域控制站不支援感應器。

### <a name="ports"></a>連接埠

下表列出 [!INCLUDE [Product short](includes/product-short.md)] 感應器至少需要的連接埠：

|通訊協定|傳輸|Port|寄件者|收件者|
|------------|-------------|--------|-----------|---|
|**內部連接埠**|||||
|SSL (\*.atp.azure.com)|TCP|443|[!INCLUDE [Product short](includes/product-short.md)] 感應器|[!INCLUDE [Product short](includes/product-short.md)] 雲端服務|
|SSL (localhost)|TCP|444|[!INCLUDE [Product short](includes/product-short.md)] 感應器|本機主機|
|**內部連接埠**|||||
|DNS|TCP 和 UDP|53|[!INCLUDE [Product short](includes/product-short.md)] 感應器|DNS 伺服器|
|Netlogon (SMB、CIFS、SAM-R)|TCP/UDP|445|[!INCLUDE [Product short](includes/product-short.md)] 感應器|網路上的所有裝置|
|RADIUS|UDP|1813|RADIUS|[!INCLUDE [Product short](includes/product-short.md)] 感應器|
|**NNR 連接埠**\*|||||
|透過 RPC 的 NTLM|TCP|連接埠 135|[!INCLUDE [Product short](includes/product-short.md)]|網路上的所有裝置|
|NetBIOS|UDP|137|[!INCLUDE [Product short](includes/product-short.md)]|網路上的所有裝置|
|RDP|TCP|3389，只有 Client hello 的第一個封包|[!INCLUDE [Product short](includes/product-short.md)]|網路上的所有裝置|

\*其中一個連接埠是必要的，但我們建議全部開啟。

### <a name="windows-event-logs"></a>Windows 事件記錄檔

[!INCLUDE [Product short](includes/product-short.md)] 偵測仰賴特定的 [Windows 事件記錄檔](configure-windows-event-collection.md#configure-event-collection)，這些記錄檔由感應器從網域控制站剖析而來。 若要正確稽核事件並將其包含在 Windows 事件記錄檔中，網域控制站需要精確的進階稽核原則設定。 如需有關設定正確原則的詳細資訊，請參閱[進階稽核原則檢查](configure-windows-event-collection.md)。 若要確定已依服務所需[稽核 Windows 事件 8004](configure-windows-event-collection.md#configure-audit-policies)，請檢閱您的 [NTLM 稽核設定](/archive/blogs/askds/ntlm-blocking-and-you-application-analysis-and-auditing-methodologies-in-windows-7) \(英文\)。

針對在 AD FS 伺服器上執行的感應器，請將稽核等級設定為 [詳細資訊]。 如需如何設定稽核等級的相關資訊，請參閱 [AD FS 的事件稽核資訊](/windows-server/identity/ad-fs/troubleshooting/ad-fs-tshoot-logging#event-auditing-information-for-ad-fs-on-windows-server-2016)。

> [!NOTE]
> 使用 Directory 服務使用者帳戶，感應器會查詢您組織中的端點以尋找使用 SAM-R (網路登入) 的本機系統管理員，以建置[橫向移動路徑圖表](use-case-lateral-movement-path.md)。 如需詳細資訊，請參閱[設定 SAM-R 必要權限](install-step8-samr.md)。

<a name="azure-atp-standalone-sensor-requirements"></a>

## <a name="product-short-standalone-sensor-requirements"></a>[!INCLUDE [Product short](includes/product-short.md)] 獨立感應器需求

本節列出 [!INCLUDE [Product short](includes/product-short.md)] 獨立感應器的需求。

> [!NOTE]
> [!INCLUDE [Product short](includes/product-short.md)] 獨立感應器不會收集 Windows 事件追蹤 (ETW) 的記錄項目，無法提供多種偵測的資料。 若要完整涵蓋您的環境，建議您部署[!INCLUDE [Product short](includes/product-short.md)] 感應器。

### <a name="general"></a>一般

[!INCLUDE [Product short](includes/product-short.md)] 獨立感應器可安裝在執行 Windows Server 2012 R2 或 Windows Server 2016 (包括 Server Core) 的伺服器上。
[!INCLUDE [Product short](includes/product-short.md)] 獨立感應器可以安裝在屬於網域或工作群組之成員的伺服器上。
[!INCLUDE [Product short](includes/product-short.md)] 獨立感應器可用來監視具 Windows Server 2003 或更新版本網域功能等級的網域控制站。

若要讓獨立感應器與雲端服務通訊，您必須在防火牆和 Proxy 中針對 *.atp.azure.com 開啟連接埠 443。

如需使用虛擬機器與 [!INCLUDE [Product short](includes/product-short.md)] 獨立感應器的相關資訊，請參閱[設定連接埠鏡像](configure-port-mirroring.md)。

> [!NOTE]
> 至少需要 5 GB 的磁碟空間，建議要有 10 GB。 這包括 [!INCLUDE [Product short](includes/product-short.md)] 二進位檔、[!INCLUDE [Product short](includes/product-short.md)] 記錄檔以及效能記錄檔所需的空間。

### <a name="server-specifications"></a>伺服器規格

為取得最佳化效能，請將執行 [!INCLUDE [Product short](includes/product-short.md)] 獨立感應器的電腦其 [電源選項] 設定為 [高效能]。

[!INCLUDE [Product short](includes/product-short.md)] 獨立感應器可支援監視多個網域控制站，依進出網域控制站的網路傳輸量而定。

>[!NOTE]
> 作為虛擬機器執行時，將不支援動態記憶體或任何其他記憶體佔用功能。

如需 [!INCLUDE [Product short](includes/product-short.md)] 獨立感應器硬體需求的詳細資訊，請參閱 [[!INCLUDE [Product short](includes/product-short.md)] 容量規劃](capacity-planning.md)。

### <a name="time-synchronization"></a>時間同步

安裝感應器之伺服器和網域控制站的時間，必須同步到相差五分鐘內。

### <a name="network-adapters"></a>網路介面卡

[!INCLUDE [Product short](includes/product-short.md)] 獨立感應器需要各至少一個管理介面卡和擷取介面卡︰

- **管理介面卡** - 用於您公司網路上的通訊。 感應器會使用此配接器來查詢其正在保護的 DC，並對電腦帳戶執行解析。

    此介面卡應進行下列設定：

    - 靜態 IP 位址，包含預設閘道

    - 慣用和替代的 DNS 伺服器

    - **此連線的 DNS 尾碼** 應該是受監視之每個網域的網域 DNS 名稱。

        ![在進階 TCP/IP 設定中設定 DNS 尾碼](media/dns-suffix.png)

        > [!NOTE]
        > 如果 [!INCLUDE [Product short](includes/product-short.md)] 獨立感應器是網域的成員，這可能會自動設定。

- **擷取介面卡** - 用來擷取進出網域控制站的流量。

    > [!IMPORTANT]
    >
    > - 設定擷取介面卡的連接埠鏡像做為網域控制站網路流量的目的地。 如需詳細資訊，請參閱[設定連接埠鏡像](configure-port-mirroring.md)。 一般而言，設定通訊埠鏡像必須與網路或虛擬化團隊合作。
    > - 為您的環境設定靜態、無法路由傳送的 IP 位址 (使用 /32 遮罩)，沒有預設感應器閘道也沒有 DNS 伺服器位址。 例如，10.10.0.10/32。 這會確保擷取網路介面卡可以擷取最大的流量，而且管理網路介面卡會用於傳送和接收必要的網路流量。

### <a name="ports"></a>連接埠

下表列出 [!INCLUDE [Product short](includes/product-short.md)] 獨立感應器在管理介面卡上至少需要設定的連接埠：

|通訊協定|傳輸|Port|寄件者|收件者|
|------------|-------------|--------|-----------|---|
|**內部連接埠**||||
|SSL (\*.atp.azure.com)|TCP|443|[!INCLUDE [Product short](includes/product-short.md)] 感應器|[!INCLUDE [Product short](includes/product-short.md)] 雲端服務|
|SSL (localhost)|TCP|444|[!INCLUDE [Product short](includes/product-short.md)] 感應器|本機主機|
|**內部連接埠**||||
|LDAP|TCP 和 UDP|389|[!INCLUDE [Product short](includes/product-short.md)] 感應器|網域控制站|
|安全的 LDAP (LDAPS)|TCP|636|[!INCLUDE [Product short](includes/product-short.md)] 感應器|網域控制站|
|LDAP 至通用類別|TCP|3268|[!INCLUDE [Product short](includes/product-short.md)] 感應器|網域控制站|
|LDAPS 至通用類別|TCP|3269|[!INCLUDE [Product short](includes/product-short.md)] 感應器|網域控制站|
|Kerberos|TCP 和 UDP|88|[!INCLUDE [Product short](includes/product-short.md)] 感應器|網域控制站|
|Netlogon (SMB、CIFS、SAM-R)|TCP 和 UDP|445|[!INCLUDE [Product short](includes/product-short.md)] 感應器|網路上的所有裝置|
|Windows Time|UDP|123|[!INCLUDE [Product short](includes/product-short.md)] 感應器|網域控制站|
|DNS|TCP 和 UDP|53|[!INCLUDE [Product short](includes/product-short.md)] 感應器|DNS 伺服器|
|Syslog (選擇性)|TCP/UDP|514，取決於設定|SIEM 伺服器|[!INCLUDE [Product short](includes/product-short.md)] 感應器|
|RADIUS|UDP|1813|RADIUS|[!INCLUDE [Product short](includes/product-short.md)] 感應器|
|**NNR 連接埠** \*|||||
|透過 RPC 的 NTLM|TCP|135|[!INCLUDE [Product short](includes/product-short.md)]|網路上的所有裝置|
|NetBIOS|UDP|137|[!INCLUDE [Product short](includes/product-short.md)]|網路上的所有裝置|
|RDP|TCP|3389，只有 Client hello 的第一個封包|[!INCLUDE [Product short](includes/product-short.md)]|網路上的所有裝置|

\*其中一個連接埠是必要的，但我們建議全部開啟。

> [!NOTE]
>
> - 使用 Directory 服務使用者帳戶，感應器會查詢您組織中的端點以尋找使用 SAM-R (網路登入) 的本機系統管理員，以建置[橫向移動路徑圖表](use-case-lateral-movement-path.md)。 如需詳細資訊，請參閱[設定 SAM-R 必要權限](install-step8-samr.md)。

## <a name="see-also"></a>另請參閱

- [[!INCLUDE [Product short](includes/product-short.md)] 大小調整工具](https://aka.ms/aatpsizingtool) \(英文\)
- [[!INCLUDE [Product short](includes/product-short.md)] 架構](architecture.md)
- [安裝[!INCLUDE [Product short](includes/product-short.md)]](install-step1.md)
- [網路名稱解析 (NNR)](nnr-policy.md)
- [查看[!INCLUDE [Product short](includes/product-short.md)] 論壇！](https://aka.ms/MDIcommunity)\(英文\)
