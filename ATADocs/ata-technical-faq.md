---
title: Advanced Threat Analytics 常見問題集 | Microsoft Docs
description: 提供關於 ATA 的常見問題清單以及相關解答
keywords: ''
author: shsagir
ms.author: shsagir
manager: rkarlin
ms.date: 03/07/2019
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: a7d378ec-68ed-4a7b-a0db-f5e439c3e852
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 9c8a16cbd49f653425b27fe50d18d7de155dab12
ms.sourcegitcommit: 9673eb49729a06d3a25d52c0f43c76ac61b9cf89
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/12/2020
ms.locfileid: "75905701"
---
# <a name="ata-frequently-asked-questions"></a>ATA 常見問題集

*適用於：Advanced Threat Analytics 1.9 版*

本文章提供關於 ATA 的常見問題清單，並提供見解和解答。


## <a name="where-can-i-get-a-license-for-advanced-threat-analytics-ata"></a>哪裡可以取得 Advanced Threat Analytics (ATA) 的授權？

如果您有使用中的 Enterprise 合約，您可以從 Microsoft 大量授權服務中心 (VLSC) 下載軟體。

如果您直接透過 Microsoft 365 入口網站或雲端解決方案合作夥伴 (CSP) 授權模型取得 Enterprise Mobility + Security (EMS) 的授權，而且無法透過 Microsoft 大量授權服務中心 (VLSC) 存取 ATA，請連絡 Microsoft 客戶支援服務，以取得啟用 Advanced Threat Analytics (ATA) 的程序。

## <a name="what-should-i-do-if-the-ata-gateway-wont-start"></a>如果 ATA 閘道無法啟動，該怎麼辦？
在目前的錯誤記錄檔中尋找最新的錯誤 (ATA 安裝在 Logs 資料夾下)。

## <a name="how-can-i-test-ata"></a>如何測試 ATA？
您可以模擬可疑的活動，也就是進行下列作業之一執行端對端測試︰

1.  使用 Nslookup.exe 進行 DNS 探查
2.  使用 psexec.exe 進行遠端執行


這需要針對受監視的網域控制站從遠端執行，而不是從 ATA 閘道執行。

## <a name="which-ata-build-corresponds-to-each-version"></a>每個版本所對應的 ATA 組建為何？

如需版本升級資訊，請參閱 [ATA 升級路徑](upgrade-path.md)。

## <a name="what-version-should-i-use-to-upgrade-my-current-ata-deployment-to-the-latest-version"></a>我應該使用哪一個版本來將目前的 ATA 部署升級至最新版本？

如需 ATA 版本升級矩陣，請參閱 [ATA 升級路徑](upgrade-path.md)。


## <a name="how-does-the-ata-center-update-its-latest-signatures"></a>ATA 中心如何更新其最新的特徵標記？

ATA 中心上安裝較新的版本時，會加強 ATA 偵測機制。 您可透過使用 Microsoft Update (MU) 或從下載中心或大量授權網站下載新版本，來升級中心。

## <a name="how-do-i-verify-windows-event-forwarding"></a>如何確認 Windows 事件轉送？
您可以將下列程式碼放入一個檔案，然後在 **\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin** 目錄中從命令提示字元執行，如下所示︰

mongo.exe ATA 檔案名稱

        db.getCollectionNames().forEach(function(collection) {
        if (collection.substring(0,10)=="NtlmEvent_") {
                if (db[collection].count() > 0) {
                                  print ("Found "+db[collection].count()+" NTLM events") 
                                }
                }
        });

## <a name="does-ata-work-with-encrypted-traffic"></a>ATA 會處理加密的流量嗎？
ATA 需要分析多個網路通訊協定，以及從 SIEM 或透過 Windows 事件轉送收集到的事件。 若偵測以流量經過加密的網路通訊協定 (例如 LDAPS 及IPSEC) 為基礎，就不會進行分析。


## <a name="does-ata-work-with-kerberos-armoring"></a>ATA 會處理 Kerberos 防護嗎？
Kerberos 保護又稱為彈性驗證安全通道 (FAST)，ATA 支援啟用 Kerberos 保護，但過度傳遞雜湊偵測時除外 (將無法運作)。

## <a name="how-many-ata-gateways-do-i-need"></a>我需要多少 ATA 閘道？

ATA 閘道數目取決於您的網路配置、封包的數量和 ATA 所擷取的事件數量。 若要得知確切的數字，請參閱 [ATA 輕量型閘道大小](ata-capacity-planning.md#ata-lightweight-gateway-sizing)。 

## <a name="how-much-storage-do-i-need-for-ata"></a>我需要為 ATA 準備多少儲存空間？
以一整天平均每秒 1000 個封包為例，您需要 0.3 GB 的儲存空間。<br /><br />如需 ATA 中心大小的詳細資訊，請參閱 [ATA Capacity Planning](ata-capacity-planning.md) (ATA 容量規劃)。


## <a name="why-are-certain-accounts-considered-sensitive"></a>為何將某些帳戶視為機密？
當帳戶屬於我們指定為機密的特定群組時 (例如，「網域系統管理員」)，會發生這種情況。

若要了解為何是機密帳戶，您可以檢閱其群組成員資格，以了解它所屬的機密群組 (其所屬的群組也可以是因為另一個群組而機密，因此您應該執行相同的程序，直到找出最高層級的機密群組)。 

此外，您可以手動將使用者、群組或電腦標記為敏感性。 如需詳細資訊，請參閱[標記敏感性帳戶](tag-sensitive-accounts.md)。

## <a name="how-do-i-monitor-a-virtual-domain-controller-using-ata"></a>如何使用 ATA 監視虛擬網域控制站？
ATA 輕量型閘道可以涵蓋大多數虛擬網域控制站；如需判斷 ATA 輕量型閘道是否適合您的環境，請參閱 [ATA Capacity Planning](ata-capacity-planning.md) (ATA 容量規劃)。

如果 ATA 輕量型閘道無法涵蓋某個虛擬網域控制站，您可以有虛擬或實體的 ATA 閘道，如[設定連接埠鏡像](configure-port-mirroring.md)中所述。  <br />最簡單的方式是在每一個有虛擬網域控制站的主機上有一個虛擬 ATA 閘道。<br />如果您的虛擬網域控制站要在主機之間移動，您需要執行下列其中一項步驟︰

-   當虛擬網域控制站移至另一部主機時，請預先將該主機中的 ATA 閘道設定為可以從最近移動的虛擬網域控制站接收流量。
-   請務必將虛擬 ATA 閘道與虛擬網域控制站緊密聯結，這樣當它移動時，ATA 閘道才會隨之移動。
-   有一些可以在主機之間傳送流量的虛擬交換器。

## <a name="how-do-i-back-up-ata"></a>如何備份 ATA？

請參閱 [ATA 災害復原](disaster-recovery.md)



## <a name="what-can-ata-detect"></a>ATA 可以偵測什麼？

ATA 可以偵測已知的惡意攻擊和技術、安全性問題和風險。
如需 ATA 偵測的完整清單，請參閱 [ATA 會執行哪些偵測？](ata-threats.md)。

## <a name="what-kind-of-storage-do-i-need-for-ata"></a>我需要為 ATA 準備何種儲存體？
建議使用具有低延遲磁碟存取 (不到 10 毫秒) 的快速存放裝置 (不建議使用 7200-RPM 磁碟)。 RAID 設定應該能夠支援大量寫入負載 (不建議使用 RAID 5/6 及其衍生項目)。

## <a name="how-many-nics-does-the-ata-gateway-require"></a>ATA 閘道需要多少 NIC？
ATA 閘道需要至少兩張網路介面卡︰<br>1. 用來連線到內部網路和 ATA 中心的 NIC<br>2. 用來透過埠鏡像來捕獲網域控制站網路流量的 NIC。<br>* 這不適用於 ATA 輕量型閘道，該閘道原本就會使用網域控制站所使用的所有網路介面卡。

## <a name="what-kind-of-integration-does-ata-have-with-siems"></a>ATA 與 SIEM 有何種整合？
ATA 與 SIEM 已經雙向整合，如下所示︰

1. 可將 ATA 設定為在偵測到可疑活動時，將 Syslog 警示傳送至任何使用 CEF 格式的 SIEM 伺服器。
2. 可將 ATA 設定為從[這些 SIEM](install-ata-step6.md) 接收 Windows 事件的 Syslog 訊息。

## <a name="can-ata-monitor-domain-controllers-virtualized-on-your-iaas-solution"></a>ATA 是否可以監視在 IaaS 解決方案上虛擬的網域控制站？
是，您可以使用 ATA 輕量型閘道來監視任何 IaaS 解決方案中的網域控制站。

## <a name="is-this-an-on-premises-or-in-cloud-offering"></a>這是內部部署或雲端供應項目？
Microsoft Advanced Threat Analytics 是內部部署的產品。

## <a name="is-this-going-to-be-a-part-of-azure-active-directory-or-on-premises-active-directory"></a>它會成為 Azure Active Directory 或內部部署 Active Directory 的一部分嗎？
此解決方案目前是獨立供應項目，不屬於 Azure Active Directory 或內部部署 Active Directory。

## <a name="do-you-have-to-write-your-own-rules-and-create-a-thresholdbaseline"></a>必須撰寫自己的規則，並建立臨界值/基準嗎？
使用 Microsoft Advanced Threat Analytics 不需要建立規則、臨界值或基準然後調整。 ATA 會分析使用者、裝置、資源的行為 — 以及它們之間的關聯性 — 可以快速偵測可疑的活動和已知的攻擊。 在部署三個星期之後，ATA 開始偵測行為的可疑活動。 另外，在部署之後，ATA 會立即啟動偵測已知的惡意攻擊和安全性問題。

## <a name="if-you-are-already-breached-can-microsoft-advanced-threat-analytics-identify-abnormal-behavior"></a>如果已經被滲透，Microsoft Advanced Threat Analytics 是否可以識別異常行為？
可以，即使在您被滲透後才安裝 ATA，ATA 仍然可以偵測到駭客的可疑活動。 ATA 不只針對使用者的行為，也會查看組織安全圖中的其他使用者。 初始分析期間，如果攻擊者的行為異常，便會被視為「極端值」，ATA 會持續報告其異常行為。 此外，如果駭客嘗試竊取其他使用者認證 (例如，傳遞票證)，或嘗試在其中一個網域控制站上執行遠端執行，ATA 會偵測到可疑的活動。

## <a name="does-this-only-leverage-traffic-from-active-directory"></a>這些只需要利用 Active Directory 的流量？
除了使用深度封包檢查技術來分析 Active Directory 流量，ATA 也可以從您的安全性資訊和事件管理 (SIEM) 收集相關的事件，並根據 Active Directory 網域服務的資訊建立實體設定檔。 如果組織有設定 Windows 事件記錄檔轉送，ATA 也可以從事件記錄檔收集事件。

## <a name="what-is-port-mirroring"></a>什麼是連接埠鏡像？
連接埠鏡像又稱為「交換器連接埠分析器」(SPAN)，是監視網路流量的方法。 啟用連接埠鏡像，交換器會將一個連接埠 (或整個 VLAN) 上的所有網路封包的複本，傳送至另一個可分析封包的連接埠。

## <a name="does-ata-monitor-only-domain-joined-devices"></a>ATA 是否只監視加入網域的裝置？
不可以。 ATA 會監視對 Active Directory 執行驗證和授權要求的網路中的所有裝置，包括非 Windows 和行動裝置。

## <a name="does-ata-monitor-computer-accounts-as-well-as-user-accounts"></a>ATA 會監視電腦帳戶以及使用者帳戶嗎？
可以。 因為電腦帳戶 (以及任何其他實體) 可以用來執行惡意活動，ATA 會監視所有電腦帳戶的行為，以及環境中的所有其他實體。

## <a name="can-ata-support-multi-domain-and-multi-forest"></a>ATA 支援多網域和多樹系嗎？
Microsoft Advanced Threat Analytics 支援在相同樹系邊界內的多網域環境。 多樹系則需要為每個樹系部署 ATA。

## <a name="can-you-see-the-overall-health-of-the-deployment"></a>可以看到部署的整體健全狀況嗎？
是，您可以檢視部署的整體健全狀況，以及與設定、連線等相關的特定問題，而且系統會在問題發生時警示您。


## <a name="see-also"></a>另請參閱
- [ATA 必要條件](ata-prerequisites.md)
- [ATA 容量規劃](ata-capacity-planning.md)
- [設定事件收集](configure-event-collection.md)
- [設定 Windows 事件轉送](configure-event-collection.md)
- [查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

