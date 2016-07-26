---
title: "安裝 ATA - 步驟 1 | Microsoft ATA"
description: "安裝 ATA 的第一步驟是下載並安裝 ATA 中心到您所選的伺服器。"
keywords: 
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: b3cceb18-0f3c-42ac-8630-bdc6b310f1d6
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: c512fd20f913c53ac936f7de288eb024d91cf9f1
ms.openlocfilehash: 756c01d4fc4fbe7950cbbfc66fd65cf32b3bc44a


---

# 安裝 ATA - 步驟 1

>[!div class="step-by-step"]

[步驟 2 »](install-ata-step2.md)

此安裝程序提供執行 ATA 1.6 全新安裝的指示。 如需從舊版更新現有 ATA 部署的相關資訊，請參閱 [1.6 版 ATA 移轉指南](/advanced-threat-analytics/understand-explore/ata-update-1.6-migration-guide)。

> [!IMPORTANT] 
> 開始安裝之前，先在 ATA Center 伺服器和 ATA 閘道伺服器上安裝 KB2934520；若沒有這麼做，ATA 安裝將會安裝此更新，且您需要在 ATA 安裝期間重新啟動機器。

## 步驟 1： 下載並安裝 ATA 中心
確認伺服器符合需求之後，您可以繼續 ATA 中心的安裝。

在 ATA 中心伺服器上執行下列步驟。

1.  從 [Microsoft 大量授權服務中心](https://www.microsoft.com/Licensing/servicecenter/default.aspx)、[TechNet Evaluation Center](http://www.microsoft.com/evalcenter/) 或 [MSDN](https://msdn.microsoft.com/subscriptions/downloads) 下載 ATA。

2.  請以本機系統管理員群組成員的使用者身分，登入 ATA 中心安裝所在的電腦。

3.  執行 **Microsoft ATA Center Setup.EXE**，然後遵循安裝精靈的步驟。

4.  如果未安裝 Microsoft .Net Framework，當您開始安裝時，系統會提示您進行安裝。 安裝 .NET Framework 之後，可能會出現重新開機的提示。
5.  在**歡迎**頁面上選取要用於 ATA 安裝畫面的語言，然後按 **[下一步]**。

6.  閱讀 Microsoft 軟體授權條款，如果您接受條款，請按一下核取方塊，然後按 **[下一步]**。

7.  建議您將 ATA 設為自動更新。 如果您未在電腦上設定 Windows 使其執行此動作，就會看到 [使用 Microsoft Update 協助您的電腦保持在安全和最新的狀態] 畫面。 
    ![保持 ATA 最新狀態影像](media/ata_ms_update.png)

8. 選取 [當我檢查更新時使用 Microsoft Update (建議選項)]。 如此會調整 Windows 設定，以允許其他 Microsoft 產品 (包括 ATA) 更新，如下所示。 
    ![Windows 自動更新影像](media/ata_installupdatesautomatically.png)

8.  在 [ATA 中心設定] 頁面中，根據您的環境輸入下列資訊︰

    |欄位|說明|註解|
    |---------|---------------|------------|
    |安裝路徑|這是將安裝 ATA 中心的位置。 位置預設為 %programfiles%\Microsoft Advanced Threat Analytics\Center|保留預設值|
    |資料庫資料路徑|這將會是 MongoDB 資料庫檔案的所在位置。 位置預設為 %programfiles%\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\data|變更位置至有空間可隨著您的規模成長的位置。 **注意：** <ul><li>在實際執行環境中，您應該根據容量規劃使用具有足夠空間的磁碟機。</li><li>大規模部署的資料庫應該放在個別的實體磁碟上。</li></ul>如需大小資訊，請參閱 [ATA 容量規劃](/advanced-threat-analytics/plan-design/ata-capacity-planning)。|
    |ATA 中心服務 IP 位址：連接埠|這是 ATA 中心服務會接聽 ATA 閘道通訊的 IP 位址。<br /><br />**預設連接埠：**443|按一下向下箭頭選取 ATA 中心服務要使用的 IP 位址。<br /><br />此 IP 位址與 ATA 中心服務的連接埠不能和 ATA 主控台的 IP 位址與連接埠相同。 請務必變更 ATA 主控台的連接埠。|
    |ATA 中心服務 SSL 憑證|這是 ATA 中心服務將使用的憑證。|按一下鑰匙圖示以選取安裝的憑證，或者，在實驗室環境中部署時可選取自我簽署的憑證。|
    |ATA 主控台 IP 位址|這是 ATA 主控台的 IIS 將使用的 IP 位址。|按一下向下箭頭選取 ATA 主控台要使用的 IP 位址。 **注意︰** 記下此 IP 位址，可讓您更輕鬆地從 ATA 閘道存取 ATA 主控台。|
    |ATA 主控台 SSL 憑證|這是IIS 將使用的憑證。|按一下鑰匙圖示以選取安裝的憑證，或者，在實驗室環境中部署時可選取自我簽署的憑證。|

    ![ATA 中心設定映像](media/ATA-Center-Configuration.JPG)

10.  按一下 [安裝] 來安裝 ATA 中心及其元件。
    安裝 ATA 中心時將安裝及設定下列元件︰

    -   Internet Information Services (IIS)

    -   ATA 中心服務和 ATA 主控台 IIS 站台

    -   MongoDB

    -   自訂的效能監視資料收集組

    -   自我簽署的憑證 (如果在安裝期間有選取)

11.  安裝完成後，按一下 [啟動] 連線至 ATA 主控台。
此時，系統會自動將您帶到 [一般] 設定頁面，以繼續進行 ATA 閘道的設定和部署。
由於您使用 IP 位址登入網站，因此會收到與憑證相關的警告，這是正常現象，而您應該要按一下 **[繼續瀏覽此網站]**。

### 驗證安裝

1.  檢查名為 **Microsoft Advanced Threat Analytics 中心**的服務是否正在執行。
2.  按一下桌面上的 [Microsoft Advanced Threat Analytics] 捷徑以連線到 ATA 主控台。 以您安裝 ATA 中心的相同使用者認證登入。



>[!div class="step-by-step"]
[«前置安裝](preinstall-ata.md)
[步驟 2»](install-ata-step2.md)

## 另請參閱

- [查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [設定事件收集](configure-event-collection.md)
- [ATA 必要條件](/advanced-threat-analytics/plan-design/ata-prerequisites)




<!--HONumber=Jul16_HO3-->


