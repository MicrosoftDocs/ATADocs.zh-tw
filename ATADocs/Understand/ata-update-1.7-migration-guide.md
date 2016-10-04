---
title: "ATA 更新至 1.7 移轉指南 | Microsoft ATA"
description: "將 ATA 更新至 1.7 版的程序"
keywords: 
author: rkarlin
manager: mbaldwin
ms.date: 08/24/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: fb65eb41-b215-4530-93a2-0b8991f4e980
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: e3b690767e5c6f5561a97a73eccfbf50ddb04148
ms.openlocfilehash: 5c20c41c3fe587f18087d64f4f84c1df65072fde


---

# ATA 更新至 1.7 移轉指南
ATA 1.7 的更新提供下列各方面的改良︰

-   新增偵測

-   改進現有偵測
  

## 將 ATA 更新至 1.7 版
> [!NOTE] 
> 如果您的環境中未安裝 ATA，請下載包括 1.7 版的 ATA 完整版本，並依照[安裝 ATA](/advanced-threat-analytics/deploy-use/install-ata) 所描述的標準安裝程序。

如果您已經部署 ATA 1.6 版，此程序將逐步引導您進行更新部署所需的步驟。

> [!NOTE] 
> 您無法在 ATA 1.4 或 1.5 版上直接安裝 ATA 1.7 版。 您必須先安裝 ATA 1.6 版。 

依照下列步驟將 ATA 更新至 1.7 版：

1.  [下載更新 1.7](http://www.microsoft.com/evalcenter/evaluate-microsoft-advanced-threat-analytics)<br>
在此版本中，會使用相同的安裝檔案 (Microsoft ATA Center Setup.exe) 來安裝新的 ATA 部署及升級現有的部署。

2.  更新 ATA 中心

4.  更新 ATA 閘道

    > [!IMPORTANT]
    > 更新所有 ATA 閘道以確保 ATA 正常運作。

### 步驟 1︰更新 ATA 中心

1.  備份您的資料庫：(選擇性)

    -   如果 ATA 中心是做為虛擬機器執行，而您想要取一個檢查點，請先關閉虛擬機器。

    -   如果 ATA 中心是在實體伺服器上執行，請遵循建議的程序[備份 MongoDB](https://docs.mongodb.org/manual/core/backups/)。

2.  執行安裝檔案 **Microsoft ATA Center Setup.exe**，並依照螢幕上的指示安裝更新。

    -  在 [歡迎] 頁面中，選取您的語言，然後按一下 [下一步]。

    -  如果您未在 1.6 版中啟用自動更新，系統會提示您設定 ATA 使用 Microsoft Update 讓 ATA 保持最新狀態。  在 [Microsoft Update] 頁面中，選取 **[當我檢查更新時使用 Microsoft Update (建議選項)]**。
    ![保持 ATA 最新狀態影像](media/ata_ms_update.png) 如此會調整 Windows 設定，以允許其他 Microsoft 產品 (包括 ATA) 更新，如下所示。 
     ![Windows 自動更新影像](media/ata_installupdatesautomatically.png)

    -  在 [資料移轉] 畫面中，選取您要移轉所有或部分資料。 如果您選擇只移轉部分資料，將不會移轉先前擷取的網路流量和行為設定檔。 這表示要花費三週的時間，異常行為偵測才會有完整的設定檔可進行異常的活動偵測。 在這三週期間，所有其他的 ATA 偵測都將會正常運作。 **部分**資料移轉花費的時間比安裝還短得多。 如果您選取 [完整] 資料移轉，可能需要很長一段時間才能完成安裝。 估計的時間量和所需的磁碟空間，會列在 [資料移轉] 畫面上，視您在舊版 ATA 中儲存先前擷取的網路流量的量而定。 選取 [部分] 或 [完整] 之前，請先務必查看這些需求。  
    
    ![ATA 資料移轉](media/migration data migration.png)

    -  按一下 [更新]。 按一下 [更新] 之後，ATA 會離線直到更新程序完成。

4.  ATA 中心更新順利完成之後，按一下 [啟動] 開啟 ATA 閘道之 ATA 主控台中的 [更新] 畫面。
    ![更新成功畫面](media/migration center success.png)

5.  在 [更新] 畫面中，如果您已經設定 ATA 閘道自動更新，它們將會現在更新，如果沒有，請按一下每個 ATA 閘道旁邊的 [更新]。
  ![更新閘道影像](media/migration update gw.png)

  
> [!IMPORTANT] 
> 更新所有 ATA 閘道以確保 ATA 正常運作。
> 在所有閘道上設定的 Syslog 接聽程式連接埠將會變更為 514。
 
    > [!NOTE] 
    > To install new ATA Gateways, go the **Gateways** screen and click **Download Gateway Setup** to get the ATA 1.7 installation package and follow the instructions for new Gateway installation as described in [Step 4. Install the ATA Gateway](/advanced-threat-analytics/deploy-use/install-ata-step4) .



## 另請參閱

- [查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Oct16_HO1-->


