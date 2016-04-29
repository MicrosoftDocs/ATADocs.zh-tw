---
# required metadata

title: ATA 常見技術問題集 | Microsoft Advanced Threat Analytics
description: 提供關於 ATA 的常見問題清單以及相關解答
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: a7d378ec-68ed-4a7b-a0db-f5e439c3e852

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# ATA 常見技術問題集
本文章提供關於 ATA 的常見問題清單，並提供見解和解答。

## ATA 常見問題集

|問題|解答|
|------------|-----------------------------------|
|ATA 閘道無法啟動，我該怎麼做？|在目前的錯誤記錄檔中尋找最新的錯誤 (ATA 安裝在 Logs 資料夾下)。|
|如何測試 ATA？|您可以模擬可疑的活動，也就是進行下列作業之一執行端對端測試︰<br /><br />1.使用 Nslookup.exe 進行 DNS 探查<br />2.使用 psexec.exe 進行遠端執行<br /><br />這需要針對受監視的網域控制站執行，而不是從 ATA 閘道執行。|
|如何確認 Windows 事件轉送？|您可以在 **\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin** 目錄中從命令提示字元執行︰<br /><br />mongo ATA --eval "printjson(db.getCollectionNames())" &#124; find /C "NtlmEvents"`|
|ATA 會處理加密的流量嗎？|不會分析加密的流量 (例如︰LDAPS、IPSEC ESP)。|
|ATA 會處理 Kerberos 防護嗎？|Kerberos 防護又稱為彈性驗證安全通道 (FAST)，ATA 支援 Kerberos 防護，但過度傳遞雜湊偵測時除外 (將無法運作)。|
|我需要多少 ATA 閘道？|找出您需要多少閘道時，需要考慮兩件事︰<br /><br />-   從效能觀點來看，為了能夠處理您的 Active Directory 環境，您的網域控制站產生的總流量，決定了您需要的 ATA 閘道的最低數目。<br />    若要進一步了解如何判斷網域控制站產生多少流量，請參閱 [ATA 容量規劃](/advanced-threat-analytics/PlanDesign/ata-capacity-planning)。<br />-   連接埠鏡像的操作限制也會決定您需要多少 ATA 閘道來支援所有網域控制站，例如︰每個交換器、每個資料中心，每個區域 – 每個環境有它自己的考量。|
|我需要為 ATA 準備多少儲存空間？|以平均每秒 1000 個封包一整天為例，您需要 1.5 GB 的儲存空間。<br /><br />如需詳細資訊，請參閱 [ATA 容量規劃](/advanced-threat-analytics/PlanDesign/ata-capacity-planning)。|
|為何某些帳戶特別機密？|當帳戶屬於我們指定為機密的特定群組時 (例如，「網域系統管理員」)，會發生這種情況。<br />若要了解為何是機密帳戶，您可以檢閱其群組成員資格，以了解它所屬的機密群組 (其所屬的群組也可以是因為另一個群組而機密，因此您應該執行相同的程序，直到找出最高層級的機密群組)。|
|如何監視虛擬網域控制站？|您可以有虛擬或實體的 ATA 閘道，如[設定連接埠鏡像](/advanced-threat-analytics/PlanDesign/configure-port-mirroring)中所述。  <br />最簡單的方式是在每一個有虛擬網域控制站的主機上有一個虛擬 ATA 閘道。<br />如果您的虛擬網域控制站要在主機之間移動，您需要執行下列其中一項作業︰<br /><br />-   當虛擬網域控制站移至另一部主機，請預先將該主機中的 ATA 閘道設定為可以從最近移動的虛擬網域控制站接收流量。<br />-   請務必將虛擬 ATA 閘道與虛擬網域控制站緊密聯結，這樣當它移動時，ATA 閘道才會隨之移動。<br />-   有一些可以在主機之間傳送流量的虛擬交換器。|
|如何備份 ATA？|有 2 個東西要備份︰<br /><br />-   ATA 的設定，這儲存在資料庫中，且每個小時會自動備份。 <br />-   ATA儲存的流量和事件，可以使用任何支援的資料庫備份程序加以備份，如需詳細資訊請參閱 [ATA 資料庫管理](/advanced-threat-analytics/DeployUse/ata-database-management)。|
|ATA 可以偵測什麼？|如需 ATA 偵測的完整清單，請參閱[什麼是 Microsoft Advanced Threat Analytics？](/advanced-threat-analytics/Understand/what-is-ata)。|
|我需要為 ATA 準備何種儲存體？|建議使用低延遲數 (小於 10 毫秒) 的快速儲存體 (不是 7200 RPM 磁碟)，以及支援大量寫入負載的 RAID 設定 (不是 RAID-5/6 及其衍生項目)。|
|ATA 閘道需要多少 NIC？|ATA 閘道需要至少兩張網路介面卡︰<br>1.一個 NIC 連線到內部網路和 ATA 中心。<br>2.一個 NIC 透過連接埠鏡像擷取網域控制站的網路流量。<br>* 這不適用於輕量型閘道。|
|ATA 與 SIEM 有何種整合？|ATA 與 SIEM 已經雙向整合，如下所示︰<br>
1.可將 ATA 設定為在可疑活動發生時傳送 Syslog 警示至任何支援 CEF 格式的 SIEM 伺服器。<br>2.可將 ATA 設定為接收來自[這些 SIEM](/advanced-threat-analytics/PlanDesign/configure-event-collection#SIEMsupport) 的每個 Windows 事件識別碼 4776 的 Syslog 訊息。|


<!--HONumber=Apr16_HO2-->


