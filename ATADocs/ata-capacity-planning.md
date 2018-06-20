---
title: 規劃 Advanced Threat Analytics 部署 | Microsoft Docs
description: 協助您規劃部署並決定支援您的網路需要多少 ATA 伺服器
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: get-started-article
ms.service: advanced-threat-analytics
ms.prod: ''
ms.assetid: 279d79f2-962c-4c6f-9702-29744a5d50e2
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: e58fe62fc655fed8f17ae800dda20e022e198a26
ms.sourcegitcommit: 49c3e41714a5a46ff2607cbced50a31ec90fc90c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/22/2018
ms.locfileid: "30010018"
---
*適用於：Advanced Threat Analytics 1.9 版*



# <a name="ata-capacity-planning"></a>ATA 容量規劃
本文將協助您決定監視您的網路需要多少部 ATA 伺服器。 文章的內容可協助您了解需要多少 ATA 閘道及/或 ATA 輕量型閘道，以及 ATA 中心和 ATA 閘道的伺服器容量。

> [!NOTE] 
> 所有效能需求符合本文所述條件的 IaaS 廠商，都能部署 ATA 中心。

## <a name="using-the-sizing-tool"></a>使用調整大小工具
若要判斷 ATA 部署容量，建議且最容易的方法是使用 [ATA 調整大小工具](http://aka.ms/atasizingtool)。 執行 ATA 調整大小工具，並從 Excel 檔案結果中，使用下列欄位判斷您需要的 ATA 容量︰

- ATA 中心 CPU 及記憶體：比對 ATA 中心資料表結果檔案中的 [Busy Packets/sec] 欄位與 [ATA 中心資料表](#ata-center-sizing)中的 [每秒封包數] 欄位。

- ATA 中心儲存體：比對 ATA 中心資料表結果檔案中的 [Avg Packets/sec] 欄位與 [ATA 中心資料表](#ata-center-sizing)中的 [每秒封包數] 欄位。
- ATA 閘道︰比對結果檔案中 ATA 閘道資料表的 **Busy Packets/sec** 欄位與 [ATA 閘道資料表](#ata-gateway-sizing)或 [ATA 輕量型閘道資料表](#ata-lightweight-gateway-sizing)中的**每秒封包數**欄位，依據[您所選擇的閘道類型](#choosing-the-right-gateway-type-for-your-deployment)而定。


![範例容量規劃工具](media/capacity tool.png)


> [!NOTE]
> 由於不同的環境會有差異，而且存在著多項特殊且無法預期的網路流量特性，因此在您一開始部署及 ATA 及執行縮放工具之後，可能必須調整及微調您的容量部署。


若基於某些原因而無法使用 ATA 調整大小工具，請以極短的收集間隔 (大約 5 秒)，手動收集 24 小時內所有網域控制站的 packet/sec 計數器資訊。 然後，對於每個網域控制站，您必須計算每日平均和最繁忙期間的 (15 分鐘) 平均。
下列章節將說明如何從一個網域控制站收集 packets/sec 計數器的指示。


> [!NOTE]
> 由於不同的環境會有差異，而且存在著多項特殊且無法預期的網路流量特性，因此在您一開始部署及 ATA 及執行縮放工具之後，可能必須調整及微調您的容量部署。


### <a name="ata-center-sizing"></a>ATA 中心大小
ATA 中心建議最少需要 30 天的資料來進行使用者行為分析。
 

|來自所有 DC 的每秒封包數|CPU (核心&#42;)|記憶體 (GB)|每日資料庫儲存體 (GB)|每月資料庫儲存體 (GB)|IOPS&#42;&#42;|
|---------------------------|-------------------------|-------------------|---------------------------------|-----------------------------------|-----------------------------------|
|1,000|2|32|0.3|9|30 (100)
|40,000|4|48|12|360|500 (750)
|200,000|8|64|60|1,800|1,000 (1,500)
|400,000|12|96|120|3,600|2,000 (2,500)
|750,000|24|112|225|6,750|2,500 (3,000)
|1,000,000|40|128|300|9,000|4,000 (5,000)

&#42;這包括實體核心，不包括超執行緒核心。

&#42;&#42;平均數目 (尖峰數目)
> [!NOTE]
> -   針對來自所有受監視的網域控制站，ATA 中心每秒彙總最多可以處理 1 百萬個封包。 在某些環境中，相同的 ATA 中心可以處理超過 1M 的整體流量。 請連絡 askcesec@microsoft.com 以取得這類環境的協助。
> -   如果您的可用空間達到最小值 (20% 或 200 GB)，則會刪除最舊的資料集合。 如果無法成功地將資料集合減少至此等級，將會記錄警示。  ATA 會繼續運作，直到達到 5% 或 50 GB 可用空間的閾值。  此時，ATA 將會停止填入資料庫，並會發出其他警示。
> - 所有效能需求符合本文所述條件的 IaaS 廠商，都能部署 ATA 中心。
> -   讀取和寫入活動的儲存體延遲應少於 10 毫秒。
> -   讀取和寫入活動之間的比率在每秒 100,000 個封包以下時大約為 1:3，在每秒 100,000 個封包以上時大約為 1:6。
> -   作為虛擬機器執行時不支援動態記憶體或任何其他記憶體佔用功能。
> -   為了達到最佳效能，將 ATA 中心的 [電源選項] 設定為 [高效能]。<br>
> -   當於實體伺服器上執行工作時，ATA 資料庫需要您**停用** BIOS 中的非統一記憶體存取 (NUMA)。 您的系統可能會將 NUMA 作為節點交錯參考，在此情況下您必須**啟用**節點交錯以停用 NUMA。 如需詳細資訊，請參閱您的 BIOS 文件。 當 ATA 中心在虛擬伺服器上執行時，這並不相關。


## <a name="choosing-the-right-gateway-type-for-your-deployment"></a>為您的部署選擇正確的閘道類型
ATA 部署中能夠支援任何 ATA 閘道類型的組合︰

- 僅限 ATA 閘道
- 僅限 ATA 輕量型閘道
- 上列兩者的組合

當您決定閘道部署類型時，請考慮下列優點：

|閘道類型|優點|成本|部署拓撲|網域控制站|
|----|----|----|----|-----|
|ATA 閘道|頻外部署會讓攻擊者更難發現 ATA|更高|與網域控制站 (頻外) 一起安裝|每秒支援最多 50,000 個封包|
|ATA 輕量型閘道|不需要專用的伺服器及連接埠鏡像設定|較低|安裝在網域控制站上|每秒支援最多 10,000 個封包|

在下列案例範例中，ATA 輕量型閘道應該涵蓋下列網域控制站︰


- 分支網站

- 部署在雲端 (IaaS) 中的虛擬網域控制站


在下列案例範例中，ATA 閘道應該涵蓋下列網域控制站︰


- 總部資料中心 (具有每秒超過 10,000 個封包的網域控制站)


### <a name="ata-lightweight-gateway-sizing"></a>ATA 輕量型閘道大小

ATA 輕量型閘道可以支援監視一個網域控制站，依網域控制站產生的網路流量而定。 


|每秒封包數&#42;|CPU (核心&#42;&#42;)|記憶體 (GB)&#42;&#42;&#42;|
|---------------------------|-------------------------|---------------|
|1,000|2|6|
|5,000|6|16|
    |10,000|10|24|

&#42;由特定 ATA 輕量型閘道監視的網域控制站上，每秒封包的總數。

&#42;&#42;此網域控制站已安裝的非超執行緒核心總數。<br>雖然 ATA 輕量型閘道可接受超執行緒，但規劃容量時，您應該計算實際核心數，而不是超執行緒核心數。

&#42;&#42;&#42;此網域控制站已安裝的記憶體總數。

> [!NOTE]   
> -   如果網域控制站沒有 ATA 輕量型閘道所需的資源，網域控制站的效能不會受到影響，但 ATA 輕量型閘道可能無法如預期般運作。
> -   作為虛擬機器執行時不支援動態記憶體或任何其他記憶體佔用功能。
> -   為了達到最佳效能，將 ATA 輕量型閘道的 **[電源選項]** 設定為 [高效能]。
> -   至少需要 5 GB 的空間，建議使用 10 GB，其中包括 ATA 二進位檔、[ATA 記錄檔](troubleshooting-ata-using-logs.md)和[效能記錄檔](troubleshooting-ata-using-perf-counters.md)所需的空間。


### <a name="ata-gateway-sizing"></a>ATA 閘道大小

決定要部署多少個 ATA 閘道時，請考慮下列問題。

-   **Active Directory 樹系和網域**<br>
    ATA 可以為來自單一 Active Directory 樹系的多個網域監視其流量。 監視多個 Active Directory 樹系需要個別 ATA 部署。 請勿將單一 ATA 部署設定為監視來自不同樹系之網域控制站的網路流量。

-   **連接埠鏡像**<br>
連接埠鏡像考量可能需要您在每個資料中心或分支網站部署多個 ATA 閘道。

-   **容量**<br>
    ATA 閘道可以支援監視多個網域控制站，依受監視的網域控制站網路流量而定。 
<br>



|每秒封包數&#42;|CPU (核心&#42;&#42;)|記憶體 (GB)|
|---------------------------|-------------------------|---------------|
|1,000|1|6|
|5,000|2|10|
|10,000|3|12|
|20,000|6|24|
|50,000|16|48|
&#42;由特定 ATA 閘道在當天最忙碌的時段監視的所有網域控制站上，每秒封包的平均總數。

&#42;網域控制站的連接埠鏡像總流量不能超過 ATA 閘道上的擷取 NIC 容量。

&#42;&#42;必須停用超執行緒。

> [!NOTE] 
> -   不支援動態記憶體。
> -   為了達到最佳效能，將 ATA 閘道的 [電源選項] 設定為 [高效能]。
> -   至少需要 5 GB 的空間，建議使用 10 GB，其中包括 ATA 二進位檔、[ATA 記錄檔](troubleshooting-ata-using-logs.md)和[效能記錄檔](troubleshooting-ata-using-perf-counters.md)所需的空間。



## <a name="related-videos"></a>相關影片
- [選擇正確的 ATA 閘道類型](https://channel9.msdn.com/Shows/Microsoft-Security/ATA-Deployment-Choose-the-Right-Gateway-Type)


## <a name="see-also"></a>另請參閱
- [ATA 調整大小工具](http://aka.ms/atasizingtool)
- [ATA 必要條件](ata-prerequisites.md)
- [ATA 架構](ata-architecture.md)
- [查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
