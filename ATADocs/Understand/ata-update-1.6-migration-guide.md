---
title: "ATA 更新至 1.6 移轉指南 | Microsoft ATA"
description: "將 ATA 更新至 1.6 版的程序"
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 04/28/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: fb65eb41-b215-4530-93a2-0b8991f4e980
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: f13750f9cdff98aadcd59346bfbbb73c2f3a26f0
ms.openlocfilehash: 87cb9534a45d3a8ca29d6a803ca399a33a3d3ea6


---

# 將 ATA 更新至 1.6 移轉指南
ATA 1.6 的更新提供下列各方面的改良︰

-   新增偵測

-   改進現有偵測

-   ATA 輕量型閘道

-   自動更新

-   提升的 ATA 中心效能

-   降低儲存體需求

-   支援 IBM QRadar

## 將 ATA 更新至 1.6 版
> [!NOTE] 
> 如果您的環境中未安裝 ATA，請下載包括 1.6 版的 ATA 完整版本，並遵循[安裝 ATA](/advanced-threat-analytics/deploy-use/install-ata) 所述的標準安裝程序。

如果您已經部署 ATA 1.5 版，此程序將逐步引導您進行更新部署所需的步驟。

> [!NOTE] 
> 您無法在 ATA 1.4 版上直接安裝 ATA 1.6 版。 您必須先安裝 ATA 1.5 版。 如果您不小心在尚未安裝 ATA 1.5 的情況下嘗試安裝 ATA 1.6，會收到錯誤，告知**您的電腦上已安裝更新的版本**。 您必須先將留在電腦上的其餘 ATA 1.6 解除安裝 (即使安裝失敗也是一樣)，再安裝 ATA 1.5 版。

依照下列步驟將 ATA 更新至 1.6 版：

1. 若要避免升級問題，請確定您遵循 [ATA 1.6 版新功能](whats-new-version-1.6.md)中所述之**將 ATA 更新 1.6 版時移轉失敗**的步驟 8 到 10。
2. 確定您有需要的可用空間可完成升級。 您可以執行安裝到整備檢查的步驟，以估計所需的可用空間，然後在配置所需的磁碟空間之後重新開始升級。
1.  [下載更新 1.6](http://www.microsoft.com/evalcenter/evaluate-microsoft-advanced-threat-analytics)<br>
在此版本中，會使用相同的安裝檔案 (Microsoft ATA Center Setup.exe) 來安裝新的 ATA 部署及升級現有的部署。

2.  更新 ATA 中心

3.  下載更新的 ATA 閘道套件

4.  更新 ATA 閘道

    > [!IMPORTANT]
    > 更新所有 ATA 閘道以確保 ATA 正常運作。

### 步驟 1︰更新 ATA 中心

1.  備份您的資料庫：(選擇性)

    -   如果 ATA 中心是做為虛擬機器執行，而您想要取一個檢查點，請先關閉虛擬機器。

    -   如果 ATA 中心是在實體伺服器上執行，請遵循建議的程序[備份 MongoDB](https://docs.mongodb.org/manual/core/backups/)。

2.  執行安裝檔案 Microsoft ATA Center Setup.exe，並遵循螢幕上的指示安裝更新。

    1.  ATA 1.6 需要安裝 .Net Framework 4.6.1。 如果尚未安裝，ATA 安裝會在安裝過程中安裝 .Net Framework 4.6.1<br>
    > [!NOTE]
    > .Net Framework 4.6.1 安裝可能需要重新啟動伺服器。 只有在重新啟動伺服器之後，才會繼續進行 ATA 安裝。
5.  在 [歡迎] 頁面中，選取您的語言，然後按一下 [下一步]。

    6.  閱讀使用者授權合約，如果您接受條款，請按 [下一步]。

    7.  您現在可以使用 Microsoft Update 讓 ATA 保持最新狀態。  在 [Microsoft Update] 頁面中，選取 **[當我檢查更新時使用 Microsoft Update (建議選項)]**。
    ![保持 ATA 最新狀態影像](media/ata_ms_update.png) 如此會調整 Windows 設定，以允許其他 Microsoft 產品 (包括 ATA) 更新，如下所示。 
     ![Windows 自動更新影像](media/ata_installupdatesautomatically.png)

    8.  開始安裝之前，ATA 會執行整備檢查。 檢閱檢查的結果，確保已成功設定必要條件，且至少具有磁碟空間下限。 
    ![ATA 整備檢查影像](media/ata_install_readinesschecks.png)

    3.  按一下 [更新]。 按一下 [更新] 之後，ATA 會離線直到更新程序完成。

4.  在更新 ATA 中心之後，ATA 閘道會報告它們現在已經過期。

    ![閘道過期的圖片](media/ATA-center-outdated.png)

> [!IMPORTANT] 
> 更新所有 ATA 閘道以確保 ATA 正常運作。

### 步驟 2： 下載 ATA 閘道安裝套件
設定網域連線設定後，您可以下載 ATA 閘道安裝套件。

若要下載 ATA 閘道安裝套件：

1.  刪除先前下載的舊版 ATA 閘道套件。

2.  在 ATA 閘道的電腦上，開啟瀏覽器，並輸入您之前在 ATA 中心為 ATA 主控台設定的 IP 位址。 ATA 主控台開啟時，按一下 [設定] 圖示，然後選取 [組態]。

    ![組態設定圖示](media/ATA-config-icon.JPG)

3.  在 [ATA 閘道] 索引標籤上，按一下 [下載 ATA 閘道安裝程式]。

4.  將封裝儲存在本機。

ZIP 檔案包含下列項目：

-   ATA 閘道安裝程式

-   包含連線至 ATA 中心所需資訊的組態設定檔

### 步驟 3：更新 ATA 閘道

1.  在每個 ATA 閘道上，將檔案從 ATA 閘道套件解壓縮，然後執行 **Microsoft ATA Gateway Setup.exe** 檔案。

    > [!NOTE] 
    > 您也可以使用這個 ATA 閘道套件來安裝新的 ATA 閘道。

2.  系統會保留您先前的設定，但是可能需要幾分鐘的時間讓服務重新啟動。

3.  對部署的其他 ATA 閘道重複此步驟。

> [!NOTE] 
> 成功更新 ATA 閘道之後，就會解決特定 ATA 閘道的過期通知。

當所有 ATA 閘道都報告已成功同步，且不再顯示有更新的 ATA 閘道套件的訊息時，即表示所有 ATA 閘道皆已更新成功。

![閘道已更新的圖片](media/ATA-gw-updated.png)


## 另請參閱

- [查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Sep16_HO4-->


