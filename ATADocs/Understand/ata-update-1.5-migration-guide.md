---
# required metadata

title: ATA 更新至 1.5 移轉指南 | Microsoft Advanced Threat Analytics
description: 更新 ATA 至 1.5 版的程序
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: fb65eb41-b215-4530-93a2-0b8991f4e980

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# ATA 更新至 1.5 移轉指南
更新至 ATA 1.5 提供下列各方面的改良︰

-   更快速的偵測時間

-   增強對 NAT (網路位址轉譯) 裝置的自動偵測演算法

-   增強對未加入網域裝置的名稱解析程序

-   支援在產品更新期間的資料移轉

-   針對涉及上千個實體的可疑活動提供更好的 UI 回應性

-   改良監視警示的自動解析

-   增強的監視和疑難排解有更多的效能計數器

## 更新 ATA 至 1.5 版
> [!NOTE]
> 如果您的環境中沒有安裝 ATA，請下載包括 1.5 版的完整版本 ATA，並遵循 [Install ATA](/advanced-threat-analytics/deploy-use/install-ata) (安裝 ATA) 所述的標準安裝程序.

如果您已經部署 ATA 1.4 版，此程序將逐步引導您進行更新安裝所需的步驟。

依照下列步驟將 ATA 更新至 1.5 版：

1.  [下載更新 1.5](http://aka.ms/ata1_5update)
      > [!NOTE]
         您也可以使用更新的完整版 ATA 來執行更新至 1.5 版。


2.  更新 ATA 中心

3.  下載更新的 ATA 閘道套件

4.  更新 ATA 閘道

    > [!IMPORTANT]
    > 更新所有 ATA 閘道以確保 ATA 正常運作。

### 步驟 1︰更新 ATA 中心

1.  備份您的資料庫：(選擇性)

    -   如果 ATA 中心是做為虛擬機器執行，而您想要取一個檢查點，請先關閉虛擬機器。

    -   如果 ATA 中心是在實體伺服器上執行，請遵循建議的程序[back up MongoDB](https://docs.mongodb.org/manual/core/backups/) (備份 MongoDB).

2.  執行更新的檔案 Microsoft ATA Center Update.exe，遵循螢幕上的指示安裝更新。

    1.  在 [歡迎] 頁面中選取您的語言，然後按一下 [下一步].

    2.  閱讀使用者授權合約，如果您接受條款，請按一下核取方塊，然後按一下 [下一步].

    3.  選取您要執行完整 (預設值) 或部分移轉。

        ![選擇完整或部分移轉](media/ATA-center-fullpartial.png)

        -   如果選取**部分**移轉，ATA 分析過的所有收集和轉送的 Windows 事件的網路流量，都將被刪除，使用者行為設定檔將必須重新學習；這需要至少三週。 如果您執行的磁碟空間很小，則執行**部分**移轉較有益。

        -   如果您執行**完整**移轉，您需要額外的磁碟空間 (如升級頁面中為您計算出來的大小)，且移轉可能需要較長時間，取決於網路流量。 完整移轉會保留所有先前收集的資料和維護的使用者行為設定檔，這表示 ATA 不需要再花時間學習行為設定檔，更新之後可以立即偵測到異常行為。

3.  按一下 [更新]。 一旦按下 [更新]，ATA 會離線直到更新程序完成。

4.  在更新 ATA 中心之後，ATA 閘道會報告它們現在已經過期。

    ![閘道過期的圖片](media/ATA-center-outdated.png)

> [!IMPORTANT]
> - 更新所有 ATA 閘道以確保 ATA 正常運作。

### 步驟 2： 下載 ATA 閘道安裝套件
設定網域連線設定後，您可以下載 ATA 閘道安裝套件。

若要下載 ATA 閘道安裝套件：

1.  刪除先前下載的舊版 ATA 閘道套件。

2.  在 ATA 閘道的電腦上，開啟瀏覽器，並輸入您之前在 ATA 中心為 ATA 主控台設定的 IP 位址。 ATA 主控台開啟時，按一下設定圖示，然後選取 [設定].

    ![組態設定圖示](media/ATA-config-icon.JPG)

3.  在 [ATA 閘道] 索引標籤中，按一下 [下載 ATA 閘道安裝程式].

4.  將封裝儲存在本機。

ZIP 檔案包含下列項目：

-   ATA 閘道安裝程式

-   包含連線至 ATA 中心所需資訊的組態設定檔

### 步驟 3：更新 ATA 閘道

1.  在每個 ATA 閘道上，解壓縮 ATA 閘道套件的檔案，執行 Microsoft ATA Gateway Setup 檔案。

    > [!NOTE]
    > 您也可以使用這個 ATA 閘道套件來安裝新的 ATA 閘道。

2.  系統會保留您先前的設定，但是可能需要幾分鐘讓服務重新啟動。

3.  對部署的其他 ATA 閘道重複此步驟。

> [!NOTE]
> 成功更新 ATA 閘道之後，特定 ATA 閘道的過期通知就會消失。

當所有 ATA 閘道都報告已成功同步，且不再顯示有更新的 ATA 閘道套件的訊息時，即表示所有 ATA 閘道皆已更新成功。

![閘道已更新的圖片](media/ATA-gw-updated.png)

## 另請參閱

- [查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO1-->


