---
title: 規劃 Azure 進階威脅防護部署 | Microsoft Docs
description: 協助您規劃部署並決定支援您的網路需要多少 Azure ATP 伺服器
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 5/22/2018
ms.topic: conceptual
ms.service: azure-advanced-threat-protection
ms.prod: ''
ms.assetid: da0ee438-35f8-4097-b3a1-1354ad59eb32
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 3426829c0c3b9b52ec1c0fb2c7f19e5a0944bfdf
ms.sourcegitcommit: 7f3ded32af35a433d4b407009f87cfa6099f8edf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/07/2018
ms.locfileid: "44126360"
---
適用於：Azure 進階威脅防護



# <a name="azure-atp-capacity-planning"></a>Azure ATP 容量規劃
此文章可協助您判斷您需要多少 Azure ATP 感應器和獨立感應器。

> [!NOTE] 
> 調整大小工具有兩個工作表 - 一個用於 ATA，另一個則用於 Azure ATP。 請確定您使用正確的工作表。

## <a name="using-the-sizing-tool"></a>使用調整大小工具
若要判斷 Azure ATP 部署容量，建議且最容易的方法是使用 [Azure ATP 調整大小工具](http://aka.ms/aatpsizingtool)。 執行 Azure ATP 調整大小工具，並從 Excel 檔案結果中，使用下列欄位判斷感應器所使用的記憶體和 CPU︰

- Azure ATP 感應器：根據[您選擇的感應器類型](#choosing-the-right-sensor-type-for-your-deployment)，比對結果檔案內 Azure ATP 感應器表格中的 **Busy Packets/sec** 欄位與 [Azure ATP 獨立感應器表格](#azure-atp-sensor-sizing)或 [Azure ATP 感應器表格](#azure-atp-standalone-sensor-sizing)中的 **PACKETS PER SECOND** 欄位。


![範例容量規劃工具](media/capacity-tool.png)


若基於某些原因而無法使用 Azure ATP 調整大小工具，請以極短的收集間隔 (大約 5 秒) 手動收集所有網域控制站 24 小時內的 packet/sec 計數器資訊。 然後，對於每個網域控制站，您必須計算每日平均和最繁忙期間的 (15 分鐘) 平均。
下列章節將說明如何從一個網域控制站收集 packets/sec 計數器的指示。

## 為您的部署選擇正確的感應器類型<a name="choosing-the-right-sensor-type-for-your-deployment"></a>
在 Azure ATP 部署中，支援任何 Azure ATP 獨立感應器類型的組合：

- 僅限 Azure ATP 獨立感應器
- 僅限 Azure ATP 感應器
- 上列兩者的組合

當您決定感應器部署類型時，請考慮下列優點：

|感應器類型|優點|成本|部署拓撲|網域控制站|
|----|----|----|----|-----|
|Azure ATP 獨立感應器|頻外部署會讓攻擊者更難發現 Azure ATP|更高|與網域控制站 (頻外) 一起安裝|支援每秒最多 100,000 個封包|
|Azure ATP 感應器|不需要專用的伺服器及連接埠鏡像設定|較低|安裝在網域控制站上|支援每秒最多 100,000 個封包|

決定要部署多少個 Azure ATP 獨立感應器時，請考慮下列問題。

-   **Active Directory 樹系和網域**<br>
    Azure ATP 可以針對您所建立的每個工作區，監視單一 Active Directory 樹系內多個網域的流量。 若要監視多個樹系，您需要建立多個工作區。 

-   **連接埠鏡像**<br>
連接埠鏡像考量可能需要您在每個資料中心或分支網站部署多個 Azure ATP 獨立感應器。

-   **容量**<br>
    Azure ATP 獨立感應器可以支援監視多個網域控制站，依受監視的網域控制站的網路流量而定。 


## Azure ATP 感應器和獨立感應器大小調整 <a name="sizing"></a>

Azure ATP 感應器可以支援監視一個網域控制站，依網域控制站產生的網路流量而定。 下表只是估計值，感應器最後剖析的數量取決於流量的數量和流量的分配。 
> [!NOTE]
> 下列的 CPU 和記憶體容量是指感應器自己的耗用量 – 不是網域控制站容量。

|每秒封包數*|CPU (核心)|記憶體 (GB)|
|----|----|-----|
|0-1k|0.25|2.50|
|1k-5k|0.75|6.00|
|5k-10k|1.00|6.50|
|10k-20k|2.00|9.00|
|20k-50k|3.50|9.50|
|50k-75k |3.50|9.50|
|75k-100k|3.50 |9.50|

> [!NOTE]
> - 感應器服務會使用的核心數總計。<br>建議您不要使用超執行緒核心。
> - 感應器服務會使用的記憶體數量總計。
> -   如果網域控制站沒有 Azure ATP 感應器所需的資源，網域控制站效能不會受到影響，但 Azure ATP 感應器可能無法如預期般運作。
> -   作為虛擬機器執行時不支援動態記憶體或任何其他記憶體佔用功能。
> -   為了達到最佳效能，請將 Azure ATP 感應器的 [電源選項] 設定為 [高效能]。
> -   至少需要 2 個核心和 6 GB 的空間，建議使用 10 GB，其中包括 Azure ATP 二進位檔和記錄所需的空間。


## <a name="domain-controller-traffic-estimation"></a>網域控制站流量估計

您可以使用各種工具來探索網域控制站的每秒平均封包數。 如果您沒有任何工具可追蹤此計數器，您可以使用效能監視器來收集所需的資訊。

若要判斷每秒封包數，請對每個網域控制站執行下列步驟：

1.  開啟效能監視器。

    ![效能監視器影像](media/atp-traffic-estimation-1.png)

2.  展開**資料收集器集合工具**。

    ![資料收集器集合工具影像](media/atp-traffic-estimation-2.png)

3.  以滑鼠右鍵按一下 [使用者定義]，然後選取 [新增] &gt;[資料收集器集合工具]。

    ![新資料收集器集合工具影像](media/atp-traffic-estimation-3.png)

4.  輸入資料收集器集合工具的名稱，然後選取 [手動建立 (進階)]。

5.  在 [要包含哪些資料類型?] 下，選取 [Create data logs, and Performance counter (建立資料記錄檔和效能計數器)]。

    ![新資料收集器集合工具的資料類型影像](media/atp-traffic-estimation-5.png)

6.  在 [要記錄哪些效能計數器 ] 下，按一下 [新增]。

7.  展開**網路介面卡**，然後選取 [封包/秒] 並選取適當的執行個體。 如果您不確定，您可以選取 [&lt;所有執行個體&gt;]，然後按一下 [新增] 和 [確定]。

    > [!NOTE]
    > 若要在命令列中執行這項作業，請執行 `ipconfig /all` 以查看介面卡和設定的名稱。

    ![新增效能計數器影像](media/atp-traffic-estimation-7.png)

8.  將 [取樣間隔] 變更為**五秒**。

9. 設定您想要儲存資料的位置。

10. 在 [建立資料收集器集合工具] 下，選取 [立即啟動這個資料收集器集合工具] 並按一下 [完成]。

    您現在應該會看到您所建立的資料收集器集合工具，以綠色三角形表示它正在運作。

11. 24 小時之後，以滑鼠右鍵按一下資料收集器集合工具並選取 [停止]，以停止資料收集器集合工具。

    ![停止資料收集器集合工具影像](media/atp-traffic-estimation-12.png)

12. 在檔案總管中，瀏覽至儲存 .blg 檔案的資料夾，然後按兩下以在效能監視器中將其開啟。

13. 選取封包/秒計數器，並記錄平均值和最大值。

    ![每秒封包數計數器影像](media/atp-traffic-estimation-14.png)



## <a name="see-also"></a>另請參閱
- [Azure ATP 調整大小工具](http://aka.ms/aatpsizingtool) \(英文\)
- [Azure ATP 必要條件](atp-prerequisites.md)
- [Azure ATP 架構](atp-architecture.md)
- [查看 ATP 論壇！](https://aka.ms/azureatpcommunity)\(英文\)
