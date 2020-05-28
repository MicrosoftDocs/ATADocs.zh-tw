---
title: 規劃 Azure 進階威脅防護部署快速入門
description: 協助您規劃部署並決定支援您的網路需要多少 Azure ATP 伺服器
author: shsagir
ms.author: shsagir
ms.date: 05/20/2020
ms.topic: quickstart
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.openlocfilehash: 7bcebf2142980990bb71fb1c09faa986b4315fa7
ms.sourcegitcommit: c3949c8f0332198753c14e3bcd7cb4ca6d288e25
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/20/2020
ms.locfileid: "83696027"
---
# <a name="quickstart-plan-capacity-for-azure-atp"></a>快速入門：規劃 Azure ATP 容量

在此快速入門中，您會判斷需要多少 Azure ATP 感應器。

## <a name="prerequisites"></a>先決條件

- 下載 [Azure ATP 調整大小工具](https://aka.ms/aatpsizingtool)。
- 檢閱 [Azure ATP 架構](atp-architecture.md)文章。
- 檢閱 [Azure ATP 必要條件](atp-prerequisites.md)文章。

## <a name="use-the-sizing-tool"></a>使用調整大小工具

若要判斷 Azure ATP 部署容量，建議且最容易的方法是使用 Azure ATP 調整大小工具。 如果您無法使用此工具，您可以手動收集流量資訊。 如需手動方法的詳細資訊，請參閱本文章底部的[網域控制站流量估算](#manual-sizing)一節。

1. 從您下載的 zip 檔案執行 Azure ATP 調整大小工具 **TriSizingTool.exe**。
1. 當此工具完成執行時，開啟 Excel 檔案結果。
1. 在 Excel 檔案中，找出然後按一下 **Azure ATP 摘要**工作表。 因為是用於 ATA 規劃，所以不需要其他工作表。
   ![範例容量規劃工具](media/capacity-tool.png)

1. 在結果 Excel 檔案的 Azure ATP 感應器表格中找出 **Busy Packets/sec** 欄位，並且記下它。
1. 比對您的 **Busy Packets/sec** 欄位與本文中 [Azure ATP 感應器表格](#sizing)一節中的 **PACKETS PER SECOND** 欄位。 使用此欄位來判斷感應器所使用的記憶體和 CPU。

## <a name="azure-atp-sensor-sizing"></a><a name="sizing"></a> Azure ATP 感應器大小調整

Azure ATP 感應器可以支援監視一個網域控制站，依網域控制站產生的網路流量而定。 下表是估計值。 感應器最後剖析的數量取決於流量的數量和流量的分配。

下列的 CPU 與隨機存取記憶體 (RAM) 容量是指**感應器自己的耗用量**，不是網域控制站容量。

|每秒封包數|CPU (核心) \*|記憶體 \*\* (GB)|
|----|----|-----|
|0-1k|0.25|2.50|
|1k-5k|0.75|6.00|
|5k-10k|1.00|6.50|
|10k-20k|2.00|9.00|
|20k-50k|3.50|9.50|
|50k-75k |3.50|9.50|
|75k-100k|3.50|9.50|

\*這包括實體核心，不包括超執行緒核心。  
\*\*隨機存取記憶體 (RAM)

在決定調整大小，請注意下列項目：

- 感應器服務會使用的核心數總計。  
建議您不要使用超執行緒核心。 搭配超執行緒核心使用，可能會產生 Azure ATP 感應器健康情況問題。
- 感應器服務會使用的記憶體數量總計。
- 如果網域控制站沒有 Azure ATP 感應器所需的資源，網域控制站效能不會受到影響。 但 Azure ATP 感應器可能無法如預期般運作。
- 作為虛擬機器執行時，所有記憶體在任何時候都必須配置到虛擬機器。
- 為了達到最佳效能，請將 Azure ATP 感應器的 [電源選項] 設定為 [高效能]。
- 需要最少 2 個核心。
- 至少需要 6 GB 的硬碟空間，建議 10 GB，因為包括 Azure ATP 二進位檔與記錄檔所需的空間。

### <a name="dynamic-memory"></a>動態記憶體

> [!NOTE]
> 作為虛擬機器 (VM) 執行時，所有記憶體在任何時候都必須配置到 VM。

|VM 執行位置|說明|
|------------|-------------|
|Hyper-V|確保未為 VM **啟用動態記憶體**。|
|VMWare|確保設定的記憶體量和保留的記憶體量相同，或是在 VM 設定中選取以下選項 - **保留所有客體記憶體 (全部鎖定)** 。|
|其他虛擬化主機|請參閱廠商提供的文件，以了解如何確保記憶體能在任何時候均向 VM 配置。 |

## <a name="domain-controller-traffic-estimation"></a><a name="manual-sizing"></a>網域控制站流量估計

若基於某些原因而無法使用 Azure ATP 調整大小工具，請以極短的收集間隔 (大約 5 秒)， 手動收集所有網域控制站 24 小時內的每秒封包計數器資訊。 然後，針對每個網域控制站，計算每日平均和最繁忙期間的 (15 分鐘) 平均。 下列各節將說明如何從一個網域控制站收集每秒封包計數器的指示。

您可以使用各種工具來探索網域控制站的每秒平均封包數。 如果您沒有任何工具可追蹤此計數器，您可以使用效能監視器來收集所需的資訊。

若要判斷每秒封包數，請對每個網域控制站執行下列步驟：

1. 開啟效能監視器。

    ![效能監視器影像](media/atp-traffic-estimation-1.png)

1. 展開**資料收集器集合工具**。

    ![資料收集器集合工具影像](media/atp-traffic-estimation-2.png)

1. 以滑鼠右鍵按一下 [使用者定義]，然後選取 [新增] &gt; [資料收集器集合工具]。

    ![新資料收集器集合工具影像](media/atp-traffic-estimation-3.png)

1. 輸入資料收集器集合工具的名稱，然後選取 [手動建立 (進階)]。

1. 在 [要包含哪些資料類型?] 下，選取 [Create data logs, and Performance counter (建立資料記錄檔和效能計數器)]。

    ![新資料收集器集合工具的資料類型影像](media/atp-traffic-estimation-5.png)

1. 在 [要記錄哪些效能計數器 ] 下，按一下 [新增]。

1. 展開**網路介面卡**，然後選取 [封包/秒] 並選取適當的執行個體。 如果您不確定，您可以選取 [&lt;所有執行個體&gt;]，然後按一下 [新增] 和 [確定]。

    > [!NOTE]
    > 若要在命令列中執行這項作業，請執行 `ipconfig /all` 以查看介面卡和設定的名稱。

    ![新增效能計數器影像](media/atp-traffic-estimation-7.png)

1. 將 [取樣間隔] 變更為**五秒**。

1. 設定您想要儲存資料的位置。

1. 在 [建立資料收集器集合工具] 下，選取 [立即啟動這個資料收集器集合工具] 並按一下 [完成]。

    您現在應該會看到您所建立的資料收集器集合工具，以綠色三角形表示它正在運作。

1. 24 小時之後，以滑鼠右鍵按一下資料收集器集合工具並選取 [停止]，以停止資料收集器集合工具。

    ![停止資料收集器集合工具影像](media/atp-traffic-estimation-12.png)

1. 在檔案總管中，瀏覽至儲存 .blg 檔案的資料夾，然後按兩下以在效能監視器中將其開啟。

1. 選取封包/秒計數器，並記錄平均值和最大值。

    ![每秒封包數計數器影像](media/atp-traffic-estimation-14.png)

## <a name="next-steps"></a>後續步驟

在此快速入門中，您已判斷需要多少 Azure ATP 感應器。 您也會判斷感應器的大小。 繼續到下一個快速入門建立 Azure ATP 執行個體。

> [!div class="nextstepaction"]
> [建立您的 Azure ATP 執行個體](install-atp-step1.md)

## <a name="join-the-community"></a>加入社群

有更多問題嗎，或是想與其他人討論 Azure ATP 與相關的安全性？ 現在就加入 [Azure ATP 社群](https://aka.ms/azureatpcommunity)！
