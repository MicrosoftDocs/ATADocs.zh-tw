---
title: Azure 進階威脅防護常見問題集
description: 提供關於 Azure ATP 的常見問題清單以及相關解答
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 06/15/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 6a9b5273-eb26-414e-9cdd-f64406e24ed8
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 524fec2722bb31aaffe1629bece5b0381ec98566
ms.sourcegitcommit: 0c356b0860ae8663254e0cf6f04001bcc91ce207
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/21/2020
ms.locfileid: "90828148"
---
# <a name="azure-atp-frequently-asked-questions"></a>Azure ATP 常見問題集

此文章提供關於 Azure ATP 的常見問題與解答清單，並分成下列類別：

- [什麼是 Azure ATP](#what-is-azure-atp)
- [授權和隱私權](#licensing-and-privacy)
- [部署](#deployment)
- [作業](#operation)
- [疑難排解](#troubleshooting)

## <a name="what-is-azure-atp"></a>什麼是 Azure ATP？

### <a name="what-can-azure-atp-detect"></a>Azure ATP 可以偵測什麼？

Azure ATP 可以偵測對您網路所進行的已知惡意攻擊和技術、安全性問題及風險。
如需 Azure ATP 偵測的完整清單，請參閱 [Azure ATP 會執行哪些偵測？](suspicious-activity-guide.md)。

### <a name="what-data-does-azure-atp-collect"></a>Azure ATP 會收集什麼資料？

Azure ATP 會將來自您已設定伺服器 (網域控制站、成員伺服器等) 的資訊，收集並儲存至特別針對系統管理、追蹤及報告用途的資料庫中。 收集的資訊包括針對網域控制站的雙向網路流量 (例如 Kerberos 驗證、NTLM 驗證、DNS 查詢)、安全性記錄 (例如 Windows 安全性事件)、Active Directory 資訊 (結構、子網路、網站)，以及實體資訊 (例如名稱、電子郵件地址及電話號碼)。

Microsoft 會使用這份資料：

- 主動識別您組織中的攻擊指標 (IOA)
- 在偵測到可能的攻擊時產生警示
- 為您的安全性作業提供與來自您網路的威脅訊號相關聯之實體的檢視，使您可以調查並探索存在於網路上的安全性威脅。

Microsoft 並不會將您的資料用於廣告用途，或是任何其他與為您提供服務無關的用途之上。

### <a name="how-many-directory-service-credentials-does-azure-atp-support"></a>Azure ATP 支援多少個目錄服務認證？

Azure ATP 目前支援最多 10 個不同的目錄服務認證，以支援具有不受信任樹系的 Active Directory 環境。 如果您需要更多帳戶，請建立支援票證。

### <a name="does-azure-atp-only-leverage-traffic-from-active-directory"></a>Azure ATP 只會利用 Active Directory 的流量嗎？

除了使用深度封包檢查技術來分析 Active Directory 流量之外，Azure ATP 也可以從您的網域控制站收集相關的 Windows 事件，並根據 Active Directory 網域服務的資訊建立實體設定檔。 Azure ATP 也支援接收來自不同廠商 (Microsoft、Cisco、F5 及 Checkpoint) 之 VPN 記錄的 RADIUS 帳戶處理。

### <a name="does-azure-atp-monitor-only-domain-joined-devices"></a>Azure ATP 是否只會監視已加入網域的裝置？

否。 Azure ATP 會監視網路中針對 Active Directory 執行驗證和授權要求的所有裝置，包括非 Windows 的裝置和行動裝置。

### <a name="does-azure-atp-monitor-computer-accounts-as-well-as-user-accounts"></a>Azure ATP 是否會監視電腦帳戶及使用者帳戶？

是。 因為電腦帳戶 (以及任何其他實體) 可以用來執行惡意活動，所以 Azure ATP 會監視所有電腦帳戶的行為，以及環境中的所有其他實體。

### <a name="what-is-the-difference-between-advanced-threat-analytics-ata-and-azure-atp"></a>Advanced Threat Analytics (ATA) 與 Azure ATP 之間的差異為何？

ATA 是獨立的內部部署解決方案，具有多個元件，例如需要內部部署專用硬體的 ATA 中心。

Azure ATP 是雲端式的安全性解決方案，會利用您的內部部署 Active Directory (Azure AD) 訊號。 這個解決方案有很高的調整能力，且經常更新。

相較於 ATA 感應器，Azure ATP 感應器也會使用資料來源 (例如 Windows 事件追蹤，ETW)，讓 Azure ATP 能夠提供額外的偵測。

Azure ATP 的頻繁更新包括下列功能：

- **支援[多樹系環境](multi-forest.md)** ：可在多個 AD 樹系間查看組織。

- **[身分識別安全性態勢評定](isp-overview.md)** ：找出常見的錯誤設定及易受惡意探索的元件，並提供補救路徑以縮小受攻擊面。

- **[UEBA 功能](/cloud-app-security/tutorial-ueba)** ：透過使用者調查優先順序評分，提供個別使用者風險的見解。 分數可協助 SecOps 調查，並協助分析師了解使用者和組織的異常活動。

- **原生整合**：與 Microsoft Cloud App Security 及 Azure AD Identity Protection 整合，以透過混合檢視，同時了解內部部署與混合式環境的情況。

- **提供給 Microsoft 威脅防護 (MTP)** ：將警示及威脅資料提供給 MTP。 MTP 利用 Microsoft 365 安全性組合 (身分識別、端點、資料及應用程式) 來自動分析跨網域威脅資料，並在單一儀表板中提供各個攻擊的完整樣貌。 有了這樣清楚的廣度與深度，防禦者就能聚焦於重大威脅，以及搜捕複雜的缺口，相信 MTP 強大的自動化能夠扼殺處於任一階段的攻擊，讓組織回復到安全狀態。

## <a name="licensing-and-privacy"></a>授權和隱私權

### <a name="where-can-i-get-a-license-for-azure-advanced-threat-protection-atp"></a>哪裡可以取得 Azure 進階威脅防護 (ATP) 的授權？

Azure ATP 隨附於 Enterprise Mobility + Security 5 套件 (EMS E5) 中，也可以獨立授權。 您可以直接透過 [Microsoft 365 入口網站](https://www.microsoft.com/cloud-platform/enterprise-mobility-security-pricing)，或雲端解決方案合作夥伴 (CSP) 授權模型取得授權。

### <a name="does-azure-atp-need-only-a-single-license-or-does-it-require-a-license-for-every-user-i-want-to-protect"></a>Azure ATP 是否僅需要單一授權，還是針對我想要保護的每個使用者都需要授權？

Azure ATP 要求 Azure AD 中的所有使用者都必須獲得授權

### <a name="is-my-data-isolated-from-other-customer-data"></a>我的資料是否會與其他客戶的資料隔離？

是，您的資料會透過以客戶識別碼為基礎的存取驗證和邏輯隔離進行隔離。 每個客戶皆只能存取收集自其組織的資料，以及由 Microsoft 提供的泛用資料。

### <a name="do-i-have-the-flexibility-to-select-where-to-store-my-data"></a>我是否能選擇資料的儲存位置？

否。 建立您的 Azure ATP 執行個體時，它會自動儲存在與您 AAD 租用戶地理位置最接近的國家/地區資料中心內。 一旦建立您的 Azure ATP 執行個體，便無法將它移動到不同的資料中心。

### <a name="how-does-microsoft-prevent-malicious-insider-activities-and-abuse-of-high-privilege-roles"></a>Microsoft 如何防止惡意內部人士活動及針對高權限角色的濫用行為？

我們刻意使 Microsoft 開發人員和系統管理員在運作及開發服務時，都只具有足以完成其受指派工作的最少權限。 Microsoft 會搭配部署預防性、偵測性及反應性的控制 (包括下列機制)，以協助保護使用者不受未經授權的開發人員和/或系統管理活動的危害：

- 針對機密資料的嚴格存取控制
- 搭配使用各種控制，以大幅強化對惡意活動的獨立偵測能力
- 多階層的監視、記錄及報告

除此之外，Microsoft 會針對特定作業人員進行背景驗證檢查，並根據背景驗證的層級，在對應用程式、系統及網路基礎結構的存取上實施相對應的限制。 當作業人員因自身業務而需要存取客戶的帳戶或相關資訊時，將需要遵循正式的程序。

## <a name="deployment"></a>部署

### <a name="how-many-azure-atp-sensors-do-i-need"></a>我需要多少 Azure ATP 感應器？

環境中的每個網域控制站都應該由一個 ATP 感應器或獨立感應器所涵蓋。 如需詳細資訊，請參閱 [Azure ATP 感應器調整大小](capacity-planning.md#sizing)。

### <a name="does-azure-atp-work-with-encrypted-traffic"></a>Azure ATP 是否能搭配加密的流量使用？

系統不會將具有加密流量的網路通訊協定 (例如 AtSvc 和 WMI) 解密，但感應器會對其進行分析。

### <a name="does-azure-atp-work-with-kerberos-armoring"></a>Azure ATP 是否能搭配 Kerberos 保護使用？

Azure ATP 支援啟用 Kerberos 保護 (又稱為彈性驗證安全通道 (FAST))，唯一的例外是過度傳遞雜湊偵測，他它無法與 Kerberos 保護搭配使用。

### <a name="how-do-i-monitor-a-virtual-domain-controller-using-azure-atp"></a>如何使用 Azure ATP 監視虛擬網域控制站？

Azure ATP 感應器可以涵蓋大多數虛擬網域控制站；如需判斷 Azure ATP 感應器是否適合您的環境，請參閱 [Azure ATP 容量規劃](capacity-planning.md)。

如果 Azure ATP 感應器無法涵蓋某個虛擬網域控制站，您可以取得虛擬或實體的 Azure ATP 獨立感應器，如[設定連接埠鏡像](configure-port-mirroring.md)中所述。  
最簡單的方式是在每一個存在虛擬網域控制站的主機上有一個虛擬 Azure ATP 獨立感應器。  
如果您的虛擬網域控制站要在主機之間移動，您需要執行下列其中一項步驟︰

- 當虛擬網域控制站移至另一部主機時，請預先設定該主機中的 Azure ATP 獨立感應器，以從最近移動的虛擬網域控制站接收流量。
- 請務必將虛擬 Azure ATP 獨立感應器與虛擬網域控制站緊密聯結，這樣當它移動時，Azure ATP 獨立感應器才會隨之移動。
- 有一些可以在主機之間傳送流量的虛擬交換器。

### <a name="how-do-i-configure-the-azure-atp-sensors-to-communicate-with-azure-atp-cloud-service-when-i-have-a-proxy"></a>在有 Proxy 的情況下，我要如何設定 Azure ATP 感應器以和 Azure ATP 雲端服務通訊？

若要讓網域控制站與雲端服務通訊，您必須在防火牆/ Proxy 中開啟：*.atp.azure.com 連接埠 443。 如需執行此操作的相關指示，請參閱[設定 Proxy 或防火牆以啟用與 Azure ATP 感應器的通訊](configure-proxy.md)。

### <a name="can-azure-atp-monitored-domain-controllers-be-virtualized-on-your-iaas-solution"></a>受 Azure ATP 監視的網域控制站是否可以在 IaaS 解決方案上虛擬化？

是，您可以使用 Azure ATP 感應器來監視位於任何 IaaS 解決方案中的網域控制站。

### <a name="can-azure-atp-support-multi-domain-and-multi-forest"></a>Azure ATP 是否能支援多網域和多樹系？

Azure 進階威脅防護支援多網域環境與多樹系。 如需詳細資訊與信任需求，請參閱[多樹系支援](multi-forest.md)。

### <a name="can-you-see-the-overall-health-of-the-deployment"></a>可以看到部署的整體健全狀況嗎？

是，您可以檢視部署的整體健全狀況，以及與設定、連線能力等相關的特定問題，而且系統會在問題發生時透過 Azure ATP 健全狀況警示來警示您。

## <a name="operation"></a>操作

### <a name="what-kind-of-integration-does-azure-atp-have-with-siems"></a>Azure ATP 與 SIEM 的整合方式為何？

您可以將 Azure ATP 設定為針對健康狀態警示和偵測到可疑活動時，使用 CEF 格式傳送 Syslog 警示至任何 SIEM 伺服器。 如需詳細資訊，請參閱 [SIEM 記錄檔參考](cef-format-sa.md)。

### <a name="why-are-certain-accounts-considered-sensitive"></a>為何將某些帳戶視為機密？

當帳戶為被指定為機密之群組的成員時，便會發生這種情況 (例如「網域系統管理員」)。

若要了解為何是機密帳戶，您可以檢閱其群組成員資格，以了解它所屬的機密群組 (其所屬的群組也可以是因為另一個群組而機密，因此您應該執行相同的程序，直到找出最高層級的機密群組)。 您也可以手動[將帳戶標記為敏感性](sensitive-accounts.md)。

### <a name="do-you-have-to-write-your-own-rules-and-create-a-thresholdbaseline"></a>必須撰寫自己的規則，並建立臨界值/基準嗎？

使用 Azure 進階威脅防護時，將不需要建立規則、臨界值或基準然後再進行調整。 Azure ATP 會分析使用者、裝置、資源的行為 (以及它們之間的關聯性)，並可以快速偵測可疑活動和已知的攻擊。 在部署三個星期之後，Azure ATP 便會開始偵測行為上的可疑活動。 另外，Azure ATP 會在部署之後立即開始偵測已知的惡意攻擊和安全性問題。

### <a name="which-traffic-does-azure-atp-generate-in-the-network-from-domain-controllers-and-why"></a>在網路中，Azure ATP 會從網域控制站產生哪些流量？為什麼？

Azure ATP 會在下列其中一個案例中，產生網域控制站到組織中電腦的流量：

1. **網路名稱解析**  
Azure ATP 會擷取流量和事件，進而了解並分析網路中的使用者和電腦活動。 為根據組織中的電腦了解並分析活動，Azure ATP 需要將 IP 解析為電腦帳戶。 為將 IP 解析為電腦名稱，Azure ATP 感應器會要求 IP 位址*後方*之電腦名稱的 IP 位址。

    要求是使用下列其中一種方法提出的：
    - 透過 RPC 的 NTLM (TCP 連接埠 135)
    - NetBIOS (UDP 連接埠 137)
    - RDP (TCP 連接埠 3389)
    - 使用 IP 位址的反向 DNS 查閱來查詢 DNS 伺服器 (UDP 53)

    取得電腦名稱之後，Azure ATP 感應器會在 Active Directory 中交互檢查詳細資料，以了解是否有與該相同電腦名稱相關的電腦物件。 如果找到相符項目，則會在 IP 位址和比對的電腦物件之間建立關聯。
2. **橫向移動路徑 (LMP)**  
若要為敏感性使用者建置潛在的 LMP，Azure ATP 會需要電腦上的本機系統管理員相關資訊。 在此案例中，Azure ATP 感應器會使用 SAM-R (TCP 445) 查詢網路流量中識別到的 IP 位址，以確定電腦的本機系統管理員。 若要深入了解 Azure ATP 與 SAM-R，請參閱[設定 SAM-R 所需的權限](install-step8-samr.md)。

3. 針對實體資料**使用 LDAP 查詢 Active Directory**  
Azure ATP 感應器會從實體所屬的網域查詢網域控制站。 它可以是相同的感應器，或是來自該網域的其他網域控制站。

|通訊協定|Service|Port|來源| 方向|
|---------|---------|---------|---------|--------|
|LDAP|TCP 和 UDP|389|網域控制站|輸出|
|安全的 LDAP (LDAPS)|TCP|636|網域控制站|輸出|
|LDAP 至通用類別|TCP|3268|網域控制站|輸出|
|LDAPS 至通用類別|TCP|3269|網域控制站|輸出|

### <a name="why-dont-activities-always-show-both-the-source-user-and-computer"></a>為什麼活動不會一律顯示來源使用者與電腦？

Azure ATP 會透過許多不同的通訊協定擷取活動。 在某些情況下，Azure ATP 不會收到量中來源使用者的資料。 Azure ATP 會嘗試將使用者的工作階段與活動相互關聯，並在嘗試成功時，顯示活動的來源使用者。 當使用者相互關聯嘗試失敗時，則只會顯示來源電腦。

## <a name="troubleshooting"></a>疑難排解

### <a name="what-should-i-do-if-the-azure-atp-sensor-or-standalone-sensor-doesnt-start"></a>如果 Azure ATP 感應器或獨立感應器無法啟動該怎麼辦？

在目前的錯誤[記錄檔](troubleshooting-using-logs.md)中尋找最新的錯誤 (在 Azure ATP 安裝位置的 "Logs" 資料夾下)。

## <a name="see-also"></a>另請參閱

- [Azure ATP 必要條件](prerequisites.md)
- [Azure ATP 容量規劃](capacity-planning.md)
- [設定事件收集](configure-event-collection.md)
- [設定 Windows 事件轉送](configure-event-forwarding.md)
- [疑難排解](troubleshooting-known-issues.md)
- [查看 Azure ATP 論壇！](https://aka.ms/azureatpcommunity)
