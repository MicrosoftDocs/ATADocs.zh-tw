---
title: 規劃 Azure 進階威脅防護部署快速入門 | Microsoft Docs
description: 協助您規劃部署並決定支援您的網路需要多少 Azure ATP 伺服器
author: mlottner
ms.author: mlottner
ms.date: 12/26/2019
ms.topic: quickstart
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.openlocfilehash: 5edb88ebc9db10abec7e8064be4af37f66111afc
ms.sourcegitcommit: 0f3ee3241895359d5cecd845827cfba1fdca9317
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/29/2019
ms.locfileid: "75543900"
---
# <a name="quickstart-plan-capacity-for-azure-atp"></a>快速入門：規劃 Azure ATP 容量

在本快速入門中，您判斷您需要多少 Azure ATP 感應器和獨立感應器。

## <a name="prerequisites"></a>先決條件

- 下載 [Azure ATP 調整大小工具](https://aka.ms/aatpsizingtool)。
- 檢閱 [Azure ATP 架構](atp-architecture.md)文章。
- 檢閱 [Azure ATP 必要條件](atp-prerequisites.md)文章。 


## <a name="use-the-sizing-tool"></a>使用調整大小工具

若要判斷 Azure ATP 部署容量，建議且最容易的方法是使用 Azure ATP 調整大小工具。 如果您無法使用此工具，您可以手動收集流量資訊。 如需手動方法的詳細資訊，請參閱本文章底部的[網域控制站流量估算](#manual-sizing)一節。

1. 從您下載的 zip 檔案執行 Azure ATP 調整大小工具 **TriSizingTool.exe**。 
2. 當此工具完成執行時，開啟 Excel 檔案結果。
3. 在 Excel 檔案中，找出然後按一下 **Azure ATP 摘要**工作表。 因為是用於 ATA 規劃，所以不需要其他工作表。
   ![範例容量規劃工具](media/capacity-tool.png)

4. 在結果 Excel 檔案的 Azure ATP 感應器表格中找出 **Busy Packets/sec** 欄位，並且記下它。
5. 選擇您的感應器類型。 使用[選擇正確的感應器類型](#choosing-the-right-sensor-type-for-your-deployment)一節中的資訊，判斷您要使用哪個感應器。 選擇感應器類型時請留意 **Busy Packets/sec**。
6. 比對您的 **Busy Packets/sec** 欄位與本文中 [Azure ATP 感應器表格](#sizing)一節中的 **PACKETS PER SECOND** 欄位。 使用此欄位來判斷感應器所使用的記憶體和 CPU。


## 為您的部署選擇正確的感應器類型<a name="choosing-the-right-sensor-type-for-your-deployment"></a>

在 Azure ATP 部署中，支援任何 Azure ATP 感應器類型的組合：

- 僅限 Azure ATP 感應器
- 僅限 Azure ATP 獨立感應器
- 上列兩者的組合

當您決定感應器部署類型時，請考慮下列優點：

|感應器類型|優點|成本|部署拓撲|網域控制站|
|----|----|----|----|-----|
|Azure ATP 感應器|不需要專用的伺服器及連接埠鏡像設定|較低|安裝在網域控制站上|支援每秒最多 100,000 個封包|
|Azure ATP 獨立感應器|頻外部署會讓攻擊者更難發現 Azure ATP|更高|與網域控制站 (頻外) 一起安裝|支援每秒最多 100,000 個封包|


決定要部署多少個 Azure ATP 獨立感應器時，請考慮下列問題：

- **Active Directory 樹系和網域** - Azure ATP 可以針對您所建立的每個 Azure ATP 執行個體，監視多個 Active Directory 樹系內多個網域的流量。

- **連接埠鏡像** - 連接埠鏡像考量可能需要您在每個資料中心或分支網站部署多個 Azure ATP 獨立感應器。

- **容量** - Azure ATP 獨立感應器可以支援監視多個網域控制站，依受監視的網域控制站的網路流量而定。

## <a name="sizing"></a>Azure ATP 感應器和獨立感應器大小調整 

Azure ATP 感應器可以支援監視一個網域控制站，依網域控制站產生的網路流量而定。 下表是估計值。 感應器最後剖析的數量取決於流量的數量和流量的分配。

下列的 CPU 和記憶體容量是指**感應器自己的耗用量**，不是網域控制站容量。

|每秒封包數*|CPU (核心)**|記憶體 (GB)|
|----|----|-----|
|0-1k|0.25|2.50|
|1k-5k|0.75|6.00|
|5k-10k|1.00|6.50|
|10k-20k|2.00|9.00|
|20k-50k|3.50|9.50|
|50k-75k |3.50|9.50|
|75k-100k|3.50|9.50|
|

這包括實體核心，不包括超執行緒核心。 

在決定調整大小，請注意下列項目： 

- 感應器服務會使用的核心數總計。<br>建議您不要使用超執行緒核心。 搭配超執行緒核心使用，可能會產生 Azure ATP 感應器健康情況問題。 
- 感應器服務會使用的記憶體數量總計。
- 如果網域控制站沒有 Azure ATP 感應器所需的資源，網域控制站效能不會受到影響。 但 Azure ATP 感應器可能無法如預期般運作。
- 作為虛擬機器執行時，所有記憶體在任何時候都必須配置到虛擬機器。
- 為了達到最佳效能，請將 Azure ATP 感應器的 [電源選項]  設定為 [高效能]  。
- 需要最少 2 個核心。 至少需要 6 GB 的空間，建議使用 10 GB，其中包括 Azure ATP 二進位檔和記錄所需的空間。

### <a name="dynamic-memory"></a>動態記憶體

> [!NOTE] 
> 作為虛擬機器 (VM) 執行時，所有記憶體在任何時候都必須配置到 VM。 

|VM 執行位置|說明|
|------------|-------------|
|Hyper-V|確保未為 VM **啟用動態記憶體**。|
|VMWare|確保設定的記憶體量和保留的記憶體量相同，或是在 VM 設定中選取以下選項 - **保留所有客體記憶體 (全部鎖定)** 。|
|其他虛擬化主機|請參閱廠商提供的文件，以了解如何確保記憶體能在任何時候均向 VM 配置。 |
|

## <a name="manual-sizing"></a>網域控制站流量估計

若基於某些原因而無法使用 Azure ATP 調整大小工具，請以極短的收集間隔 (大約 5 秒)， 手動收集所有網域控制站 24 小時內的每秒封包計數器資訊。 然後，針對每個網域控制站，計算每日平均和最繁忙期間的 (15 分鐘) 平均。 下列各節將說明如何從一個網域控制站收集每秒封包計數器的指示。

您可以使用各種工具來探索網域控制站的每秒平均封包數。 如果您沒有任何工具可追蹤此計數器，您可以使用效能監視器來收集所需的資訊。

若要判斷每秒封包數，請對每個網域控制站執行下列步驟：

1.  開啟效能監視器。

    ![效能監視器影像](media/atp-traffic-estimation-1.png)

2.  展開**資料收集器集合工具**。

    ![資料收集器集合工具影像](media/atp-traffic-estimation-2.png)

3.  以滑鼠右鍵按一下 [使用者定義]  ，然後選取 [新增]  &gt; [資料收集器集合工具]  。

    ![新資料收集器集合工具影像](media/atp-traffic-estimation-3.png)

4.  輸入資料收集器集合工具的名稱，然後選取 [手動建立 (進階)]  。

5.  在 [要包含哪些資料類型?]  下，選取 [Create data logs, and Performance counter (建立資料記錄檔和效能計數器)]  。

    ![新資料收集器集合工具的資料類型影像](media/atp-traffic-estimation-5.png)

6.  在 [要記錄哪些效能計數器 ]  下，按一下 [新增]  。

7.  展開**網路介面卡**，然後選取 [封包/秒]  並選取適當的執行個體。 如果您不確定，您可以選取 [&lt;所有執行個體&gt;]  ，然後按一下 [新增]  和 [確定]  。

    > [!NOTE]
    > 若要在命令列中執行這項作業，請執行 `ipconfig /all` 以查看介面卡和設定的名稱。

    ![新增效能計數器影像](media/atp-traffic-estimation-7.png)

8.  將 [取樣間隔]  變更為**五秒**。

9. 設定您想要儲存資料的位置。

10. 在 [建立資料收集器集合工具]  下，選取 [立即啟動這個資料收集器集合工具]  並按一下 [完成]  。

    您現在應該會看到您所建立的資料收集器集合工具，以綠色三角形表示它正在運作。

11. 24 小時之後，以滑鼠右鍵按一下資料收集器集合工具並選取 [停止]  ，以停止資料收集器集合工具。

    ![停止資料收集器集合工具影像](media/atp-traffic-estimation-12.png)

12. 在檔案總管中，瀏覽至儲存 .blg 檔案的資料夾，然後按兩下以在效能監視器中將其開啟。

13. 選取封包/秒計數器，並記錄平均值和最大值。

    ![每秒封包數計數器影像](media/atp-traffic-estimation-14.png)



## <a name="next-steps"></a>後續步驟

此文章可協助您判斷您需要多少 Azure ATP 感應器和獨立感應器。 您也會判斷感應器的大小。 繼續到下一個快速入門建立 Azure ATP 執行個體。

> [!div class="nextstepaction"]
> [建立您的 Azure ATP 執行個體](install-atp-step1.md)


## <a name="join-the-community"></a>加入社群

有更多問題嗎，或是想與其他人討論 Azure ATP 與相關的安全性？ 現在就加入 [Azure ATP 社群](https://aka.ms/azureatpcommunity)！
