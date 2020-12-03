---
title: 適用于身分識別的 Microsoft Defender 常見問題
description: 提供有關 Microsoft Defender 身分識別和相關解答的常見問題清單
ms.date: 10/27/2020
ms.topic: conceptual
ms.openlocfilehash: 6b8ac890f60a283f5749cd262a8b7f65819e3231
ms.sourcegitcommit: cdb7ae4580851e25aae24d07e7d66a750aa54405
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2020
ms.locfileid: "96544295"
---
# <a name="product-long-frequently-asked-questions"></a>[!INCLUDE [Product long](includes/product-long.md)] 常見問題

本文提供有關分為下列類別的常見問題和解答清單 [!INCLUDE [Product long](includes/product-long.md)] ：

- [什麼 [!INCLUDE [Product short](includes/product-short.md)]](#what-is-azure-atp)
- [授權和隱私權](#licensing-and-privacy)
- [部署](#deployment)
- [作業](#operation)
- [疑難排解](#troubleshooting)

<a name="what-is-azure-atp"></a>

## <a name="what-is-product-short"></a>什麼是 [!INCLUDE [Product short](includes/product-short.md)]？

### <a name="what-can-product-short-detect"></a>可以偵測 [!INCLUDE [Product short](includes/product-short.md)] 到什麼？

[!INCLUDE [Product short](includes/product-short.md)] 偵測已知的惡意攻擊和技術、安全性問題，以及對您的網路的風險。
如需偵測的完整清單 [!INCLUDE [Product short](includes/product-short.md)] ，請參閱偵測 [執行的作業為何 [!INCLUDE [Product short](includes/product-short.md)] ？](suspicious-activity-guide.md)。

### <a name="what-data-does-product-short-collect"></a>收集哪些資料 [!INCLUDE [Product short](includes/product-short.md)] ？

[!INCLUDE [Product short](includes/product-short.md)] 會從您設定的伺服器收集並儲存資訊 (網域控制站、成員伺服器等 ) 在服務特定的資料庫中進行管理、追蹤和報告等用途。 收集的資訊包括針對網域控制站的雙向網路流量 (例如 Kerberos 驗證、NTLM 驗證、DNS 查詢)、安全性記錄 (例如 Windows 安全性事件)、Active Directory 資訊 (結構、子網路、網站)，以及實體資訊 (例如名稱、電子郵件地址及電話號碼)。

Microsoft 會使用這份資料：

- 主動識別您組織中的攻擊指標 (IOA)
- 在偵測到可能的攻擊時產生警示
- 為您的安全性作業提供與來自您網路的威脅訊號相關聯之實體的檢視，使您可以調查並探索存在於網路上的安全性威脅。

Microsoft 並不會將您的資料用於廣告用途，或是任何其他與為您提供服務無關的用途之上。

### <a name="how-many-directory-service-credentials-does-product-short-support"></a>有多少目錄服務認證 [!INCLUDE [Product short](includes/product-short.md)] 支援？

[!INCLUDE [Product short](includes/product-short.md)] 目前支援新增最多10個不同的目錄服務認證，以支援具有不受信任之樹系的 Active Directory 環境。 如果您需要更多帳戶，請建立支援票證。

### <a name="does-product-short-only-leverage-traffic-from-active-directory"></a>[!INCLUDE [Product short](includes/product-short.md)]只會利用來自 Active Directory 的流量？

除了使用深度封包檢查技術來分析 Active Directory 流量之外， [!INCLUDE [Product short](includes/product-short.md)] 也會從您的網域控制站收集相關的 Windows 事件，並根據 Active Directory Domain Services 的資訊建立實體設定檔。 [!INCLUDE [Product short](includes/product-short.md)] 也支援接收來自不同廠商的 VPN 記錄的 RADIUS 帳戶處理 (Microsoft、Cisco、F5 和檢查點) 。

### <a name="does-product-short-monitor-only-domain-joined-devices"></a>是否 [!INCLUDE [Product short](includes/product-short.md)] 只會監視已加入網域的裝置？

否。 [!INCLUDE [Product short](includes/product-short.md)] 監視網路中針對 Active Directory 執行驗證和授權要求的所有裝置，包括非 Windows 和行動裝置。

### <a name="does-product-short-monitor-computer-accounts-as-well-as-user-accounts"></a>是否會 [!INCLUDE [Product short](includes/product-short.md)] 監視電腦帳戶以及使用者帳戶？

是。 因為電腦帳戶 (以及任何其他實體) 可用來執行惡意活動，所以會 [!INCLUDE [Product short](includes/product-short.md)] 監視所有電腦帳戶的行為以及環境中的所有其他實體。

### <a name="what-is-the-difference-between-advanced-threat-analytics-ata-and-product-short"></a>Advanced 威脅分析 (ATA) 和之間有何差異 [!INCLUDE [Product short](includes/product-short.md)] ？

ATA 是獨立的內部部署解決方案，具有多個元件，例如需要內部部署專用硬體的 ATA 中心。

[!INCLUDE [Product short](includes/product-short.md)] 是以雲端為基礎的安全性解決方案，可利用內部部署 Active Directory (Azure AD) 信號。 這個解決方案有很高的調整能力，且經常更新。

ATA 的最終發行版本已 [正式推出](https://support.microsoft.com/help/4568997/update-3-for-microsoft-advanced-threat-analytics-1-9)。 ATA 將于2021年1月12日結束主流支援。 延伸支援將繼續進行，直到2026年1月為止。 如需詳細資訊，請閱讀 [我們的 blog](https://techcommunity.microsoft.com/t5/microsoft-security-and/end-of-mainstream-support-for-advanced-threat-analytics-january/ba-p/1539181)。

相較于 ATA 感應器， [!INCLUDE [Product short](includes/product-short.md)] 感應器也會使用資料來源，例如 Windows 的事件追蹤 (ETW) 啟用 [!INCLUDE [Product short](includes/product-short.md)] 以傳遞額外的偵測。

[!INCLUDE [Product short](includes/product-short.md)]經常更新包含下列特性和功能：

- **支援 [多樹系環境](multi-forest.md)** ：可在多個 AD 樹系間查看組織。

- **[身分識別安全性態勢評定](isp-overview.md)** ：找出常見的錯誤設定及易受惡意探索的元件，並提供補救路徑以縮小受攻擊面。

- **[UEBA 功能](/cloud-app-security/tutorial-ueba)** ：透過使用者調查優先順序評分，提供個別使用者風險的見解。 分數可協助 SecOps 調查，並協助分析師了解使用者和組織的異常活動。

- **原生整合**：與 Microsoft Cloud App Security 及 Azure AD Identity Protection 整合，以透過混合檢視，同時了解內部部署與混合式環境的情況。

- **參與 Microsoft 365 defender**：將警示和威脅資料貢獻給 Microsoft 365 Defender。 Microsoft 365 Defender 利用 Microsoft 365 的安全性組合 (身分識別、端點、資料和應用程式) 自動分析跨網域的威脅資料，在單一儀表板中建立每個攻擊的完整圖片。 有了這項廣度和深度的清楚，防禦者可以專注于嚴重的威脅，並尋找複雜的缺口，信任 Microsoft 365 Defender 強大的自動化會在終止鏈中的任何位置停止攻擊，並讓組織回到安全的狀態。

## <a name="licensing-and-privacy"></a>授權和隱私權

### <a name="where-can-i-get-a-license-for-product-long"></a>我可以在哪裡取得授權 [!INCLUDE [Product long](includes/product-long.md)] ？

[!INCLUDE [Product short](includes/product-short.md)] 可作為 Enterprise Mobility + Security 5 suite (EMS E5) 的一部分，並以獨立授權的形式提供。 您可以直接透過 [Microsoft 365 入口網站](https://www.microsoft.com/cloud-platform/enterprise-mobility-security-pricing)，或雲端解決方案合作夥伴 (CSP) 授權模型取得授權。

### <a name="does-product-short-need-only-a-single-license-or-does-it-require-a-license-for-every-user-i-want-to-protect"></a>[!INCLUDE [Product short](includes/product-short.md)]只需要單一授權，還是需要授權給我想要保護的每個使用者？

如需授權需求的詳細資訊 [!INCLUDE [Product short](includes/product-short.md)] ，請參閱[ [!INCLUDE [Product short](includes/product-short.md)] 授權指引](/office365/servicedescriptions/microsoft-365-service-descriptions/microsoft-365-tenantlevel-services-licensing-guidance/microsoft-365-security-compliance-licensing-guidance#azure-advanced-threat-protection)。

### <a name="is-my-data-isolated-from-other-customer-data"></a>我的資料是否會與其他客戶的資料隔離？

是，您的資料會透過以客戶識別碼為基礎的存取驗證和邏輯隔離進行隔離。 每個客戶皆只能存取收集自其組織的資料，以及由 Microsoft 提供的泛用資料。

### <a name="do-i-have-the-flexibility-to-select-where-to-store-my-data"></a>我是否能選擇資料的儲存位置？

否。 當您 [!INCLUDE [Product short](includes/product-short.md)] 建立實例時，系統會自動將其儲存在最接近 AAD 租使用者地理位置的國家/地區資料中心。 [!INCLUDE [Product short](includes/product-short.md)] 一旦您的 [!INCLUDE [Product short](includes/product-short.md)] 實例建立至不同的資料中心，就無法移動資料。

### <a name="how-does-microsoft-prevent-malicious-insider-activities-and-abuse-of-high-privilege-roles"></a>Microsoft 如何防止惡意內部人士活動及針對高權限角色的濫用行為？

我們刻意使 Microsoft 開發人員和系統管理員在運作及開發服務時，都只具有足以完成其受指派工作的最少權限。 Microsoft 會搭配部署預防性、偵測性及反應性的控制 (包括下列機制)，以協助保護使用者不受未經授權的開發人員和/或系統管理活動的危害：

- 針對機密資料的嚴格存取控制
- 搭配使用各種控制，以大幅強化對惡意活動的獨立偵測能力
- 多階層的監視、記錄及報告

除此之外，Microsoft 會針對特定作業人員進行背景驗證檢查，並根據背景驗證的層級，在對應用程式、系統及網路基礎結構的存取上實施相對應的限制。 當作業人員因自身業務而需要存取客戶的帳戶或相關資訊時，將需要遵循正式的程序。

## <a name="deployment"></a>部署

### <a name="how-many-product-short-sensors-do-i-need"></a>[!INCLUDE [Product short](includes/product-short.md)]我需要多少感應器？

環境中的每個網域控制站都應由 [!INCLUDE [Product short](includes/product-short.md)] 感應器或獨立感應器所涵蓋。 如需詳細資訊，請參閱感應器重設[ [!INCLUDE [Product short](includes/product-short.md)] 大小](capacity-planning.md#sizing)。

### <a name="does-product-short-work-with-encrypted-traffic"></a>是否可 [!INCLUDE [Product short](includes/product-short.md)] 使用加密的流量？

系統不會將具有加密流量的網路通訊協定 (例如 AtSvc 和 WMI) 解密，但感應器會對其進行分析。

### <a name="does-product-short-work-with-kerberos-armoring"></a>是否 [!INCLUDE [Product short](includes/product-short.md)] 適用于 Kerberos 防護？

支援啟用 Kerberos 防護（也稱為彈性驗證安全通道 (FAST) ） [!INCLUDE [Product short](includes/product-short.md)] ，除了過度傳遞雜湊偵測之外，無法使用 Kerberos 防護。

### <a name="how-do-i-monitor-a-virtual-domain-controller-using-product-short"></a>如何? 使用來監視虛擬網域控制站 [!INCLUDE [Product short](includes/product-short.md)] ？

感應器可以涵蓋大部分的虛擬網域控制站 [!INCLUDE [Product short](includes/product-short.md)] ，以判斷 [!INCLUDE [Product short](includes/product-short.md)] 感應器是否適用于您的環境，請參閱[ [!INCLUDE [Product short](includes/product-short.md)] 容量規劃](capacity-planning.md)。

如果感應器無法涵蓋某個虛擬網域控制站 [!INCLUDE [Product short](includes/product-short.md)] ，您可以有虛擬或實體的 [!INCLUDE [Product short](includes/product-short.md)] 獨立感應器，如 [設定埠鏡像](configure-port-mirroring.md)中所述。  
最簡單的方法是 [!INCLUDE [Product short](includes/product-short.md)] 在虛擬網域控制站所在的每一部主機上擁有虛擬的獨立感應器。  
如果您的虛擬網域控制站要在主機之間移動，您需要執行下列其中一項步驟︰

- 當虛擬網域控制站移至另一部主機時，請預先設定 [!INCLUDE [Product short](includes/product-short.md)] 該主機中的獨立感應器，以接收最近移動的虛擬網域控制站的流量。
- 確定您已將虛擬 [!INCLUDE [Product short](includes/product-short.md)] 獨立感應器與虛擬網域控制站建立關聯，如此一來，在移動時， [!INCLUDE [Product short](includes/product-short.md)] 獨立感應器會隨之移動。
- 有一些可以在主機之間傳送流量的虛擬交換器。

### <a name="how-do-i-configure-the-product-short-sensors-to-communicate-with-product-short-cloud-service-when-i-have-a-proxy"></a>[!INCLUDE [Product short](includes/product-short.md)]當我有 proxy 時，如何? 將感應器設定為與 [!INCLUDE [Product short](includes/product-short.md)] 雲端服務通訊嗎？

若要讓網域控制站與雲端服務通訊，您必須在防火牆/ Proxy 中開啟：*.atp.azure.com 連接埠 443。 如需如何進行此動作的指示，請參閱 [設定您的 proxy 或防火牆，以啟用與 [!INCLUDE [Product short](includes/product-short.md)] 感應器的通訊](configure-proxy.md)。

### <a name="can-product-short-monitored-domain-controllers-be-virtualized-on-your-iaas-solution"></a>[!INCLUDE [Product short](includes/product-short.md)]受監視的網域控制站可以在您的 IaaS 解決方案上虛擬化嗎？

是的，您可以使用 [!INCLUDE [Product short](includes/product-short.md)] 感應器來監視任何 IaaS 解決方案中的網域控制站。

### <a name="can-product-short-support-multi-domain-and-multi-forest"></a>可以 [!INCLUDE [Product short](includes/product-short.md)] 支援多網域和多樹系嗎？

[!INCLUDE [Product short](includes/product-short.md)] 支援多網域環境和多個樹系。 如需詳細資訊與信任需求，請參閱[多樹系支援](multi-forest.md)。

### <a name="can-you-see-the-overall-health-of-the-deployment"></a>可以看到部署的整體健全狀況嗎？

是，您可以查看部署的整體健全狀況，以及與設定、連線能力等相關的特定問題，並在健康情況警示發生時收到警示 [!INCLUDE [Product short](includes/product-short.md)] 。

## <a name="operation"></a>作業

### <a name="what-kind-of-integration-does-product-short-have-with-siems"></a>Siem 有何種整合 [!INCLUDE [Product short](includes/product-short.md)] ？

[!INCLUDE [Product short](includes/product-short.md)] 可以設定為將 Syslog 警示傳送至任何使用 CEF 格式的 SIEM 伺服器，以取得健康情況警示以及偵測到安全性警示的時間。 如需詳細資訊，請參閱 [SIEM 記錄檔參考](cef-format-sa.md)。

### <a name="why-are-certain-accounts-considered-sensitive"></a>為何將某些帳戶視為機密？

當帳戶為被指定為機密之群組的成員時，便會發生這種情況 (例如「網域系統管理員」)。

若要了解為何是機密帳戶，您可以檢閱其群組成員資格，以了解它所屬的機密群組 (其所屬的群組也可以是因為另一個群組而機密，因此您應該執行相同的程序，直到找出最高層級的機密群組)。 您也可以手動[將帳戶標記為敏感性](sensitive-accounts.md)。

### <a name="do-you-have-to-write-your-own-rules-and-create-a-thresholdbaseline"></a>必須撰寫自己的規則，並建立臨界值/基準嗎？

使用 [!INCLUDE [Product short](includes/product-short.md)] 時，不需要建立規則、臨界值或基準，然後微調。 [!INCLUDE [Product short](includes/product-short.md)] 分析使用者、裝置和資源之間的行為，以及彼此之間的關聯性，並且可以快速偵測可疑的活動和已知的攻擊。 部署後的三周 [!INCLUDE [Product short](includes/product-short.md)] 開始偵測行為可疑的活動。 另一方面，在 [!INCLUDE [Product short](includes/product-short.md)] 部署之後，將會立即開始偵測已知的惡意攻擊和安全性問題。

### <a name="which-traffic-does-product-short-generate-in-the-network-from-domain-controllers-and-why"></a>哪些流量會 [!INCLUDE [Product short](includes/product-short.md)] 在網路中從網域控制站產生，原因為何？

[!INCLUDE [Product short](includes/product-short.md)] 在下列三種情況下，從網域控制站產生流量到組織中的電腦：

1. **網路名稱解析**  
[!INCLUDE [Product short](includes/product-short.md)] 在網路中捕獲流量和事件、學習和分析使用者和電腦活動。 若要根據組織中的電腦來學習及分析活動， [!INCLUDE [Product short](includes/product-short.md)] 必須將 ip 解析為電腦帳戶。 若要將 ip 解析為電腦名稱稱， [!INCLUDE [Product short](includes/product-short.md)] 感應器會要求 ip 位址 *後方* 電腦名稱稱的 ip 位址。

    要求是使用下列其中一種方法提出的：
    - 透過 RPC 的 NTLM (TCP 連接埠 135)
    - NetBIOS (UDP 連接埠 137)
    - RDP (TCP 連接埠 3389)
    - 使用 IP 位址的反向 DNS 查閱來查詢 DNS 伺服器 (UDP 53)

    取得電腦名稱稱之後，  [!INCLUDE [Product short](includes/product-short.md)] 感應器會交叉檢查 Active Directory 中的詳細資料，以查看是否有相關聯的電腦物件具有相同的電腦名稱稱。 如果找到相符項目，則會在 IP 位址和比對的電腦物件之間建立關聯。
2. **橫向移動路徑 (LMP)**  
若要建立敏感性使用者的潛在 Lmp， [!INCLUDE [Product short](includes/product-short.md)] 需要電腦上本機系統管理員的相關資訊。 在此案例中， [!INCLUDE [Product short](includes/product-short.md)] 感應器會使用 (TCP 445) 的 SAM 來查詢網路流量中識別的 IP 位址，以便判斷電腦的本機系統管理員。 若要深入瞭解 [!INCLUDE [Product short](includes/product-short.md)] 和 sam-r，請參閱 [設定 Sam-r 所需的許可權](install-step8-samr.md)。

3. 針對實體資料 **使用 LDAP 查詢 Active Directory**  
[!INCLUDE [Product short](includes/product-short.md)] 感應器會從實體所屬的網域查詢網域控制站。 它可以是相同的感應器，或是來自該網域的其他網域控制站。

|通訊協定|Service|Port|來源| 方向|
|---------|---------|---------|---------|--------|
|LDAP|TCP 和 UDP|389|網域控制站|輸出|
|安全的 LDAP (LDAPS)|TCP|636|網域控制站|輸出|
|LDAP 至通用類別|TCP|3268|網域控制站|輸出|
|LDAPS 至通用類別|TCP|3269|網域控制站|輸出|

### <a name="why-dont-activities-always-show-both-the-source-user-and-computer"></a>為什麼活動不會一律顯示來源使用者與電腦？

[!INCLUDE [Product short](includes/product-short.md)] 透過許多不同的通訊協定來捕捉活動。 在某些情況下， [!INCLUDE [Product short](includes/product-short.md)] 不會接收流量中來源使用者的資料。 [!INCLUDE [Product short](includes/product-short.md)] 嘗試將使用者的會話與活動相互關聯，並在嘗試成功時，顯示活動的來源使用者。 當使用者相互關聯嘗試失敗時，則只會顯示來源電腦。

## <a name="troubleshooting"></a>疑難排解

### <a name="what-should-i-do-if-the-product-short-sensor-or-standalone-sensor-doesnt-start"></a>如果 [!INCLUDE [Product short](includes/product-short.md)] 感應器或獨立感應器無法啟動，該怎麼辦？

查看目前錯誤 [記錄](troubleshooting-using-logs.md) 檔中最新的錯誤 (在 [ [!INCLUDE [Product short](includes/product-short.md)] 記錄檔] 資料夾下安裝) 。

## <a name="see-also"></a>另請參閱

- [[!INCLUDE [Product short](includes/product-short.md)] 先決條件](prerequisites.md)
- [[!INCLUDE [Product short](includes/product-short.md)] 容量規畫](capacity-planning.md)
- [設定事件收集](configure-event-collection.md)
- [設定 Windows 事件轉送](configure-event-forwarding.md)
- [疑難排解](troubleshooting-known-issues.md)
- [查看[!INCLUDE [Product short](includes/product-short.md)] 論壇！](https://aka.ms/MDIcommunity)\(英文\)
