---
title: "Azure 進階威脅防護常見問題集 | Microsoft Docs"
description: "提供關於 Azure ATP 的常見問題清單以及相關解答"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/27/2018
ms.topic: article
ms.prod: 
ms.service: azure-advanced-threat-protection
ms.technology: 
ms.assetid: 6a9b5273-eb26-414e-9cdd-f64406e24ed8
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 6a6a34b9a2aae0e507fe18872a31368cf3f3e9d0
ms.sourcegitcommit: 21d8f9abf909fc5f0e0da03cd100fa8fb950baa4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/27/2018
---
適用於：Azure 進階威脅防護

# <a name="azure-atp-frequently-asked-questions"></a>Azure ATP 常見問題集
本文章提供關於 Azure ATP 的常見問題清單，並提供見解和解答。


## <a name="where-can-i-get-a-license-for-azure-advanced-threat-protection-atp"></a>哪裡可以取得 Azure 進階威脅防護 (ATP) 的授權？

如果您直接透過 Office 365 入口網站或透過雲端解決方案提供者 (CSP) 授權模型取得 Enterprise Mobility + Security 5 (EMS E5) 的授權，而且無法透過 Microsoft 大量授權服務中心 (VLSC) 存取 Azure ATP，請連絡 Microsoft 客戶支援服務以取得啟動 Azure 進階威脅防護 (ATP) 的程序。

## <a name="what-should-i-do-if-the-azure-atp-sensor-or-standalone-sensor-doesnt-start"></a>如果 Azure ATP 感應器或獨立感應器無法啟動該怎麼辦？
在目前的錯誤記錄檔中尋找最新的錯誤 (在 Azure ATP 安裝位置的 "Logs" 資料夾下)。

## <a name="how-can-i-test-azure-atp"></a>如何測試 Azure ATP？
透過執行下列命令，您能以端對端測試的方式模擬可疑的活動：

-  使用 Nslookup.exe 進行 DNS 探查


這需要針對受監視的網域控制站從遠端執行，而不是從 Azure ATP 獨立感應器執行。


## <a name="does-azure-atp-work-with-encrypted-traffic"></a>Azure ATP 是否能搭配加密的流量使用？
Azure ATP 需要分析多個網路通訊協定，以及從 SIEM 或透過 Windows 事件轉寄收集到的事件。 系統並不會分析以搭配加密流量的網路通訊協定 (例如 LDAPS 及IPSEC) 為基礎的偵測。


## <a name="does-azure-atp-work-with-kerberos-armoring"></a>Azure ATP 是否能搭配 Kerberos 保護使用？
ATP 支援啟用 Kerberos 保護 (又稱為彈性驗證安全通道 (FAST))，唯一的例外是過度傳遞雜湊偵測，其無法搭配 Kerberos 保護使用。

## <a name="how-many-azure-atp-sensors-do-i-need"></a>我需要多少 Azure ATP 感應器？

環境中的每個網域控制站都應該由一個 ATP 感應器或獨立感應器所涵蓋。 如需詳細資訊，請參閱 [Azure ATP 感應器調整大小](atp-capacity-planning.md#sizing)。 


## <a name="why-are-certain-accounts-considered-sensitive"></a>為何將某些帳戶視為機密？
當帳戶為被指定為機密之群組的成員 (例如「網域系統管理員」) 時，便會發生這種情況。

若要了解為何是機密帳戶，您可以檢閱其群組成員資格，以了解它所屬的機密群組 (其所屬的群組也可以是因為另一個群組而機密，因此您應該執行相同的程序，直到找出最高層級的機密群組)。 您也可以[手動將帳戶標記為機密](sensitive-accounts.md)。

## <a name="how-do-i-monitor-a-virtual-domain-controller-using-azure-atp"></a>如何使用 Azure ATP 監視虛擬網域控制站？
Azure ATP 感應器可以涵蓋大多數虛擬網域控制站；如需判斷 Azure ATP 感應器是否適合您的環境，請參閱 [Azure ATP 容量規劃](atp-capacity-planning.md)。

如果 Azure ATP 感應器無法涵蓋某個虛擬網域控制站，您可以取得虛擬或實體的 Azure ATP 獨立感應器，如[設定連接埠鏡像](configure-port-mirroring.md)中所述。  <br />最簡單的方式是在每一個存在虛擬網域控制站的主機上有一個虛擬 Azure ATP 獨立感應器。<br />如果您的虛擬網域控制站要在主機之間移動，您需要執行下列其中一項步驟︰

-   當虛擬網域控制站移至另一部主機時，請預先設定該主機中的 Azure ATP 獨立感應器，以從最近移動的虛擬網域控制站接收流量。
-   請務必將虛擬 Azure ATP 獨立感應器與虛擬網域控制站緊密聯結，這樣當它移動時，Azure ATP 獨立感應器才會隨之移動。
-   有一些可以在主機之間傳送流量的虛擬交換器。


## <a name="what-can-azure-atp-detect"></a>Azure ATP 可以偵測什麼？

Azure ATP 可以偵測已知的惡意攻擊和技術、安全性問題和風險。
如需 Azure ATP 偵測的完整清單，請參閱 [Azure ATP 會執行哪些偵測？](suspicious-activity-guide.md)。

## <a name="how-many-nics-does-the-azure-atp-standalone-sensor-require"></a>Azure ATP 獨立感應器需要多少 NIC？
Azure ATP 獨立感應器至少需要兩個網路介面卡：<br>1.連線到內部網路和 Azure ATP 雲端服務的 NIC<br>2.用來透過連接埠鏡像擷取網域控制站網路流量的 NIC。<br>* 這不適用於 Azure ATP 感應器，因為它原本就會使用網域控制站所使用的所有網路介面卡。

## <a name="what-kind-of-integration-does-azure-atp-have-with-siems"></a>Azure ATP 與 SIEM 的整合方式為何？
Azure ATP 與 SIEM 具有雙向整合，如下所示︰

1. 可設定 Azure ATP 針對健康情況警示及在偵測到可疑活動時，將 Syslog 警示傳送至任何使用 CEF 格式的 SIEM 伺服器。
2. 可設定 Azure ATP 以接收來自[這些 SIEM](configure-event-collection.md) 之 Windows 事件的 Syslog 訊息。

## <a name="how-do-i-configure-the-azure-atp-sensors-to-communicate-with-azure-atp-cloud-service-when-i-have-a-proxy"></a>在有 Proxy 的情況下，我要如何設定 Azure ATP 感應器以和 Azure ATP 雲端服務通訊？

若要讓網域控制站與雲端服務通訊，您必須在防火牆/ Proxy 中開啟：*.atp.azure.com 連接埠 443。 如需執行此操作的相關指示，請參閱[設定 Proxy 或防火牆以啟用與 Azure ATP 感應器的通訊](configure-proxy.md)。
 

## <a name="can-azure-atp-monitor-domain-controllers-virtualized-on-your-iaas-solution"></a>Azure ATP 是否可以監視在 IaaS 解決方案上虛擬化的網域控制站？
是，您可以使用 Azure ATP 感應器來監視位於任何 IaaS 解決方案中的網域控制站。

## <a name="is-this-going-to-be-a-part-of-azure-active-directory-or-on-premises-active-directory"></a>它會成為 Azure Active Directory 或內部部署 Active Directory 的一部分嗎？
此解決方案目前為獨立的供應項目。 它不是 Azure Active Directory 或內部部署 Active Directory 的一部分。

## <a name="do-you-have-to-write-your-own-rules-and-create-a-thresholdbaseline"></a>必須撰寫自己的規則，並建立臨界值/基準嗎？
使用 Azure 進階威脅防護時，將不需要建立規則、臨界值或基準然後再進行調整。 Azure ATP 會分析使用者、裝置、資源的行為 (以及它們之間的關聯性)，並可以快速偵測可疑的活動和已知的攻擊。 在部署三個星期之後，Azure ATP 便會開始偵測行為上的可疑活動。 另外，Azure ATP 會在部署之後立即開始偵測已知的惡意攻擊和安全性問題。

## <a name="does-this-only-leverage-traffic-from-active-directory"></a>這些只需要利用 Active Directory 的流量？
除了使用深度封包檢查技術來分析 Active Directory 流量之外，Azure ATP 也可以從您的安全性資訊和事件管理 (SIEM) 收集相關的事件，並根據 Active Directory 網域服務的資訊建立實體設定檔。 如果您使用 Azure ATP 感應器，它將會自動擷取這些事件。 您可以使用 Windows 事件轉寄來將這些事件傳送至 Azure ATP 獨立感應器。 Azure ATP 也支援接收來自不同廠商 (Microsoft、Cisco、F5 及 Checkpoint) 之 VPN 記錄的 RADIUS 帳戶處理。

## <a name="what-is-port-mirroring"></a>什麼是連接埠鏡像？
連接埠鏡像又稱為「交換器連接埠分析器」(SPAN)，是監視網路流量的方法。 啟用連接埠鏡像，交換器會將一個連接埠 (或整個 VLAN) 上的所有網路封包的複本，傳送至另一個可分析封包的連接埠。

## <a name="does-azure-atp-monitor-only-domain-joined-devices"></a>Azure ATP 是否只會監視已加入網域的裝置？
否。 Azure ATP 會監視網路中針對 Active Directory 執行驗證和授權要求的所有裝置，包括非 Windows 的裝置和行動裝置。

## <a name="does-azure-atp-monitor-computer-accounts-as-well-as-user-accounts"></a>Azure ATP 是否會監視電腦帳戶及使用者帳戶？
是。 因為電腦帳戶 (以及任何其他實體) 可以用來執行惡意活動，所以 Azure ATP 會監視所有電腦帳戶的行為，以及環境中的所有其他實體。

## <a name="can-azure-atp-support-multi-domain-and-multi-forest"></a>Azure ATP 是否能支援多網域和多樹系？
Azure 進階威脅防護支援在相同樹系邊界內的多網域環境。 多樹系針對每個樹系皆需要一個 Azure ATP 工作區。

## <a name="can-you-see-the-overall-health-of-the-deployment"></a>可以看到部署的整體健全狀況嗎？
是，您可以檢視部署的整體健全狀況，以及與設定、連線等相關的特定問題，而且系統會在問題發生時警示您。

## <a name="what-data-does-azure-atp-collect"></a>Azure ATP 會收集什麼資料？ 
Azure ATP 會將來自您已設定伺服器 (網域控制站、成員伺服器等) 的資訊，收集並儲存至特別針對系統管理、追蹤及報告用途的資料庫中。 收集的資訊包括針對網域控制站的雙向網路流量 (例如 Kerberos 驗證、NTLM 驗證、DNS 查詢)、安全性記錄 (例如 Windows 安全性事件)、Active Directory 資訊 (結構、子網路、網站)，以及實體資訊 (例如名稱、電子郵件地址及電話號碼)。 

Microsoft 會使用這份資料： 

-   主動識別您組織中的攻擊指標 (IOA) 
-   在偵測到可能的攻擊時產生警示 
-   為您的安全性作業提供與來自您網路的威脅訊號相關聯之實體的檢視，使您可以調查並探索存在於網路上的安全性威脅。 

Microsoft 並不會將您的資料用於廣告用途，或是任何其他與為您提供服務無關的用途之上。 

## <a name="do-i-have-the-flexibility-to-select-where-to-store-my-data"></a>我是否能選擇資料的儲存位置？ 

建立 Azure ATP 工作區時，您可以選擇要將資料儲存在位於美國或歐洲的 Microsoft Azure 資料中心。 設定好之後，您便無法變更資料的儲存位置。 Microsoft 將不會把資料從該指定位置傳輸到其他位置。 

## <a name="is-my-data-isolated-from-other-customer-data"></a>我的資料是否會與其他客戶的資料隔離？ 

是，您的資料會透過以客戶識別碼為基礎的存取驗證和邏輯隔離進行隔離。 每個客戶皆只能存取收集自其組織的資料，以及由 Microsoft 提供的泛用資料。 

## <a name="how-does-microsoft-prevent-malicious-insider-activities-and-abuse-of-high-privilege-roles"></a>Microsoft 如何防止惡意內部人士活動及針對高權限角色的濫用行為？ 

我們刻意使 Microsoft 開發人員和系統管理員在運作及開發服務時，都只具有足以完成其受指派工作的最少權限。 Microsoft 會搭配部署預防性、偵測性及反應性的控制 (包括下列機制)，以協助保護使用者不受未經授權的開發人員和/或系統管理活動的危害： 

-   針對機密資料的嚴格存取控制 
-   搭配使用各種控制，以大幅強化對惡意活動的獨立偵測能力 
-   多階層的監視、記錄及報告 

除此之外，Microsoft 會針對特定作業人員進行背景驗證檢查，並根據背景驗證的層級，在對應用程式、系統及網路基礎結構的存取上實施相對應的限制。 當作業人員因自身業務而需要存取客戶的帳戶或相關資訊時，將需要遵循正式的程序。 

## <a name="see-also"></a>另請參閱
- [Azure ATP 必要條件](atp-prerequisites.md)
- [Azure ATP 容量規劃](atp-capacity-planning.md)
- [設定事件收集](configure-event-collection.md)
- [設定 Windows 事件轉送](configure-event-forwarding.md#configuring-windows-event-forwarding)
- [查看 ATP 論壇！](https://aka.ms/azureatpcommunity)\(英文\)
