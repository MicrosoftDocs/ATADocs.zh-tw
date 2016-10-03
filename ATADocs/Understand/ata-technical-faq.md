---
title: "ATA 常見問題 | Microsoft ATA"
description: "提供關於 ATA 的常見問題清單以及相關解答"
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 08/24/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: a7d378ec-68ed-4a7b-a0db-f5e439c3e852
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 7d081a6e14adffc675de203001074c3435cce6b2
ms.openlocfilehash: 8896df26157f9da903e68ac7a1d21f7f80f95026


---
*適用於︰Advanced Threat Analytics 1.7 版*

# ATA 常見問題集
本文章提供關於 ATA 的常見問題清單，並提供見解和解答。


## ATA 如何授權？
如需授權資訊，請參閱[如何購買 Advanced Threat Analytics](https://www.microsoft.com/cloud-platform/advanced-threat-analytics-pricing)


## 如果 ATA 閘道無法啟動，該怎麼辦？
在目前的錯誤記錄檔中尋找最新的錯誤 (ATA 安裝在 Logs 資料夾下)。
## 如何測試 ATA？
您可以模擬可疑的活動，也就是進行下列作業之一執行端對端測試︰

1.  使用 Nslookup.exe 進行 DNS 探查
2.  使用 psexec.exe 進行遠端執行


這需要針對受監視的網域控制站從遠端執行，而不是從 ATA 閘道執行。

## 如何確認 Windows 事件轉送？
您可以將下列程式碼放入一個檔案，然後在 **\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin** 目錄中從命令提示字元執行，如下所示︰

mongo.exe ATA 檔案名稱

        db.getCollectionNames().forEach(function(collection) {
        if (collection.substring(0,10)=="NtlmEvent_") {
                if (db[collection].count() > 0) {
                                  print ("Found "+db[collection].count()+" NTLM events") 
                                }
                }
        });

## ATA 會處理加密的流量嗎？
ATA 會分析多個網路通訊協定，以及從 SIEM 或透過 Windows 事件轉送收集的事件，因此即使不分析加密的流量 (例如 LDAPS 和 IPSEC ESP)，ATA 仍然可以運作，大多數偵測也不會受到影響

## ATA 會處理 Kerberos 防護嗎？
Kerberos 保護又稱為彈性驗證安全通道 (FAST)，ATA 支援啟用 Kerberos 保護，但過度傳遞雜湊偵測時除外 (將無法運作)。
## 我需要多少 ATA 閘道？

ATA 閘道數目取決於您的網路配置、封包的數量和 ATA 所擷取的事件數量。 若要得知確切的數字，請參閱 [ATA 輕量型閘道大小](/advanced-threat-analytics/plan-design/ata-capacity-planning#ata-lightweight-gateway-sizing)。 

## 我需要為 ATA 準備多少儲存空間？
以一整天平均每秒 1000 個封包為例，您需要 0.3 GB 的儲存空間。<br /><br />如需 ATA 中心大小的詳細資訊，請參閱 [ATA Capacity Planning](/advanced-threat-analytics/plan-design/ata-capacity-planning) (ATA 容量規劃)。


## 為何將某些帳戶視為機密？
當帳戶屬於我們指定為機密的特定群組時 (例如，「網域系統管理員」)，會發生這種情況。

若要了解為何是機密帳戶，您可以檢閱其群組成員資格，以了解它所屬的機密群組 (其所屬的群組也可以是因為另一個群組而機密，因此您應該執行相同的程序，直到找出最高層級的機密群組)。

## 如何使用 ATA 監視虛擬網域控制站？
ATA 輕量型閘道可以涵蓋大多數虛擬網域控制站；如需判斷 ATA 輕量型閘道是否適合您的環境，請參閱 [ATA Capacity Planning](/advanced-threat-analytics/plan-design/ata-capacity-planning) (ATA 容量規劃)。

如果 ATA 輕量型閘道無法涵蓋某個虛擬網域控制站，您可以有虛擬或實體的 ATA 閘道，如 [Configure port mirroring](/advanced-threat-analytics/deploy-use/configure-port-mirroring) (設定連接埠鏡像) 中所述。  <br />最簡單的方式是在每一個有虛擬網域控制站的主機上有一個虛擬 ATA 閘道。<br />如果您的虛擬網域控制站要在主機之間移動，您需要執行下列其中一項作業︰

-   當虛擬網域控制站移至另一部主機時，請預先將該主機中的 ATA 閘道設定為可以從最近移動的虛擬網域控制站接收流量。
-   請務必將虛擬 ATA 閘道與虛擬網域控制站緊密聯結，這樣當它移動時，ATA 閘道才會隨之移動。
-   有一些可以在主機之間傳送流量的虛擬交換器。

## 如何備份 ATA？
有 2 個東西要備份︰

-   ATA 儲存的流量和事件，可以使用任何支援的資料庫備份程序加以備份；如需詳細資訊，請參閱 [ATA database management](/advanced-threat-analytics/deploy-use/ata-database-management) (ATA 資料庫管理)。 
-   ATA 的設定。 這儲存在資料庫中，每小時自動備份在 ATA 中心部署位置中的 [Backup] 資料夾。  請參閱 [ATA 資料庫管理](https://docs.microsoft.com/advanced-threat-analytics/deploy-use/ata-database-management)了解詳細資訊。
## ATA 可以偵測什麼？
ATA 可以偵測已知的惡意攻擊和技術、安全性問題和風險。
如需 ATA 偵測的完整清單，請參閱 [ATA 會執行哪些偵測？](ata-threats.md)。

## 我需要為 ATA 準備何種儲存體？
建議使用具有低延遲磁碟存取 (不到 10 毫秒) 的快速存放裝置 (不建議使用 7200 RPM 磁碟)。 RAID 設定應該能夠支援大量寫入負載 (不建議使用 RAID 5/6 及其衍生項目)。

## ATA 閘道需要多少 NIC？
ATA 閘道需要至少兩張網路介面卡︰<br>1.一個 NIC 連線到內部網路和 ATA 中心。<br>2.NIC，將用來透過連接埠鏡像擷取網域控制站的網路流量。<br>* 這不適用於 ATA 輕量型閘道，該閘道原本就會使用網域控制站所使用的所有網路介面卡。

## ATA 與 SIEM 有何種整合？
ATA 與 SIEM 已經雙向整合，如下所示︰

1. 可將 ATA 設定為在可疑活動發生時將 Syslog 警示傳送至任何使用 CEF 格式的 SIEM 伺服器。
2. 可將 ATA 設定為接收來自[這些 SIEM](/advanced-threat-analytics/deploy-use/configure-event-collection#siem-support)，每個 Windows 事件識別碼為 4776 的 Syslog 訊息。

## ATA 是否可以監視在 IaaS 解決方案上虛擬的網域控制站？

是，您可以使用 ATA 輕量型閘道來監視任何 IaaS 解決方案中的網域控制站。

## 這是內部部署或雲端產品？
Microsoft Advanced Threat Analytics 是內部部署的產品。

## 它會成為 Azure Active Directory 或內部部署 Active Directory 的一部分嗎？
此解決方案目前是獨立產品，不屬於 Azure Active Directory 或內部部署 Active Directory。

## 必須撰寫自己的規則，並建立臨界值/基準嗎？
使用 Microsoft Advanced Threat Analytics 不需要建立規則、臨界值或基準然後調整。 ATA 會分析使用者、裝置、資源的行為 — 以及它們之間的關聯性 — 可以快速偵測可疑的活動和已知的攻擊。 在部署三個星期之後，ATA 開始偵測行為的可疑活動。 另外，在部署之後，ATA 會立即啟動偵測已知的惡意攻擊和安全性問題。

## 如果已經被滲透，Microsoft Advanced Threat Analytics 能夠識別異常行為嗎？
可以，即使在您被滲透後才安裝 ATA，ATA 仍然可以偵測到駭客的可疑活動。 ATA 不只針對使用者的行為，也會查看組織安全圖中的其他使用者。 初始分析期間，如果攻擊者的行為異常，便會被視為「極端值」，ATA 會持續報告其異常行為。 此外，如果駭客嘗試竊取其他使用者認證 (例如，傳遞票證)，或嘗試在其中一個網域控制站上執行遠端執行，ATA 會偵測到可疑的活動。

## 這些只需要利用 Active Directory 的流量？
除了使用深度封包檢查技術來分析 Active Directory 流量，ATA 也可以從您的安全性資訊和事件管理 (SIEM) 收集相關的事件，並根據 Active Directory 網域服務的資訊建立實體設定檔。 如果組織有設定 Windows 事件記錄檔轉送，ATA 也可以從事件記錄檔收集事件。

## 什麼是連接埠鏡像？
連接埠鏡像又稱為「交換器連接埠分析器」(SPAN)，是監視網路流量的方法。 啟用連接埠鏡像，交換器會將一個連接埠 (或整個 VLAN) 上的所有網路封包的複本，傳送至另一個可分析封包的連接埠。

## ATA 是否只監視加入網域的裝置？
否。 ATA 會監視對 Active Directory 執行驗證和授權要求的網路中的所有裝置，包括非 Windows 和行動裝置。

## ATA 會監視電腦帳戶以及使用者帳戶嗎？
是。 因為電腦帳戶 (以及任何其他實體) 可以用來執行惡意活動，ATA 會監視所有電腦帳戶的行為以及環境中的所有其他實體。

## ATA 支援多網域和多樹系嗎？
Microsoft Advanced Threat Analytics 支援在相同樹系邊界內的多網域環境。 多樹系則需要為每個樹系部署 ATA。
## 可以看到部署的整體健全狀況嗎？
是，您可以檢視部署的整體健全狀況以及與組態、連線等相關的特定問題，而且系統會在問題發生時警示您。


## 另請參閱
- [ATA 必要條件](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [ATA 容量規劃](/advanced-threat-analytics/plan-design/ata-capacity-planning)
- [設定事件收集](/advanced-threat-analytics/deploy-use/configure-event-collection)
- [設定 Windows 事件轉送](/advanced-threat-analytics/deploy-use/configure-event-collection#Configuring-Windows-Event-Forwarding)
- [查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/home?forum=mata)




<!--HONumber=Sep16_HO4-->


