---
title: 安裝 Azure 進階威脅防護 - 步驟 4 | Microsoft Docs
description: 安裝 Azure ATP 的步驟四可協助您安裝 Azure ATP 獨立感應器。
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/25/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 51911e39-76c7-4dcd-bc0b-ec6235d0403f
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 9eaa6b37d56c3d8b18c3f5d015581cf7975d6e93
ms.sourcegitcommit: 7f3ded32af35a433d4b407009f87cfa6099f8edf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/07/2018
ms.locfileid: "44126315"
---
適用於：Azure 進階威脅防護



# <a name="install-azure-atp---step-4"></a>安裝 Azure ATP - 步驟 4

>[!div class="step-by-step"]
[« 步驟 3](install-atp-step3.md)
[步驟 5 »](install-atp-step5.md)

## <a name="step-4-install-the-azure-atp-sensor"></a>步驟 4： 安裝 Azure ATP 感應器

在專用伺服器上安裝 Azure ATP 獨立感應器之前，請驗證連接埠鏡像已正確設定，且 Azure ATP 獨立感應器可以查看進出網域控制站的流量。 


> [!IMPORTANT]
>請確定電腦上已安裝 .Net Framework 4.7。 如果尚未安裝 .Net Framework 4.7，Azure ATP 感應器安裝套件便會加以安裝，如此將需要伺服器重新開機。

在 Azure ATP 感應器伺服器或網域控制站上執行下列步驟。

1. 檢查機器是否可以連線到相關的 Azure ATP 雲端服務端點：
  - https://triprd1wceuw1sensorapi.atp.azure.com (適用於歐洲)  
  - https://triprd1wcuse1sensorapi.atp.azure.com (適用於美國)
  - https://triprd1wcasse1sensorapi.atp.azure.com (適用於亞洲)

2. 將安裝檔案從 zip 檔案解壓縮。 
> [!NOTE] 
> 從 ZIP 檔案直接安裝會失敗。

3.  執行 **Azure ATP sensor setup.exe** 並按照安裝精靈的指示操作。

4.  在 [歡迎] 頁面中，選取您的語言，然後按一下 [下一步]。

     ![Azure ATP 獨立感應器安裝語言](media/sensor-install-language.png)


5.  安裝精靈會自動檢查伺服器為網域控制站或專用伺服器。 如果是網域控制站，則其中已安裝 Azure ATP 感應器。如果是專用伺服器，則其中已安裝 Azure ATP 獨立感應器。 
    
    例如，針對 Azure ATP 獨立感應器，會顯示下列畫面，讓您知道您的專用伺服器上已安裝 Azure ATP 獨立感應器：
    
    ![Azure ATP 獨立感應器安裝](media/sensor-install-deployment-type.png)

    按一下 [下一步] 。

    > [!NOTE] 
    > 如果網域控制站或專用伺服器不符合安裝的最低硬體需求，您會收到一則警告。 但這並不會阻止您按 [下一步] 和繼續進行安裝。 在不需要這麼多資料儲存空間的小型實驗室測試環境中，這可能會是安裝 Azure ATP 的正確選項。 針對生產環境，強烈建議使用 Azure ATP 的 [容量規劃](atp-capacity-planning.md)指南，確保您的網域控制站或專用伺服器符合必要需求。

6.  在 [設定感應器] 下，輸入從上一個步驟複製的安裝路徑和存取金鑰 (視您的環境而定)：

    ![Azure ATP 獨立感應器設定的影像](media/sensor-install-config.png)

      - 安裝路徑：這是安裝 Azure ATP 獨立感應器的位置。 根據預設，這是 %programfiles%\Azure Advanced Threat Protection sensor。 保留預設值。

      - 存取金鑰：這是擷取自上一個步驟中的工作區入口網站。
    
7. 按一下 [安裝]。 安裝 Azure ATP 感應器期間將安裝及設定下列元件︰

    -   KB 3047154 (僅適用於 Windows Server 2012 R2)

        > [!IMPORTANT]
        > -   請勿將 KB 3047154 安裝於虛擬主機 (執行虛擬化的主機；可在虛擬機器上執行)。 這可能會導致連接埠鏡像無法正常運作。 
        > -   如果 ATP 感應器電腦上已安裝 Wireshark，您將需要重新啟動 ATP 感應器，因為它使用相同的驅動程式。

    -   Azure ATP 感應器服務和 Azure ATP 感應器更新程式服務
    -   Microsoft Visual C++ 2013 可轉散發元件

8.  安裝完成後，請按一下 [啟動] 以開啟瀏覽器，並登入 Azure ATP 工作區入口網站。


>[!div class="step-by-step"]
[« 步驟 3](install-atp-step3.md)
[步驟 5 »](install-atp-step5.md)


## <a name="see-also"></a>另請參閱

- [Azure ATP 調整大小工具](http://aka.ms/aatpsizingtool) \(英文\)

- [設定事件收集](configure-event-collection.md)

- [Azure ATP 必要條件](atp-prerequisites.md)

- [查看 ATP 論壇！](https://aka.ms/azureatpcommunity)\(英文\)
