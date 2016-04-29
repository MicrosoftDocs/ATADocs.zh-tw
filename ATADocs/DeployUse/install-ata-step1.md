---
# required metadata

title: 安裝 ATA - 步驟 1 | Microsoft Advanced Threat Analytics
description: 安裝 ATA 的第一步驟是下載並安裝 ATA 中心到您所選的伺服器。
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: b3cceb18-0f3c-42ac-8630-bdc6b310f1d6

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 安裝 ATA - 步驟 1

>[!div class="step-by-step"]
[« 預先安裝](install-ata-preinstall.md)
[步驟 2 »](install-ata-step2.md)

## 步驟 1： 下載並安裝 ATA 中心
確認伺服器符合需求之後，您可以繼續 ATA 中心的安裝。

在 ATA 中心伺服器上執行下列步驟。

1.  從 [TechNet 評估中心](http://www.microsoft.com/en-us/evalcenter/)下載 ATA。

2.  使用身為本機 Administrators 群組成員的使用者帳戶登入。

3.  從提高權限的命令提示字元中，執行 Microsoft ATA 中心 Setup.EXE，然後遵循安裝精靈的指示。

4.  在 [歡迎]**** 頁面中，選取您的語言，然後按一下 [下一步]****。

5.  閱讀使用者授權合約，如果您接受條款，請按 [下一步]****。

6.  在 [中心設定]**** 頁面中，根據您的環境輸入下列資訊︰

    |欄位|說明|註解|
    |---------|---------------|------------|
    |安裝路徑|這是將安裝 ATA 中心的位置。 位置預設為 %programfiles%\Microsoft Advanced Threat Analytics\Center|保留預設值|
    |資料庫資料路徑|這將會是 MongoDB 資料庫檔案的所在位置。 位置預設為 %programfiles%\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\data|變更位置至有空間可隨著您的規模成長的位置。 **注意：** <ul><li>在實際執行環境中，您應該根據容量規劃使用具有足夠空間的磁碟機。</li><li>大規模部署的資料庫應該放在個別的實體磁碟上。</li></ul>如需規模大小的詳細資訊，請參閱 [ATA 容量規劃](/advanced-threat-analytics/PlanDesign/ata-capacity-planning)。|
    |資料庫日誌路徑|這將會是資料庫日誌檔案的所在位置。 位置預設為 %programfiles%\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\data\journal|在大型部署中，資料庫日誌應該放在和資料庫及系統磁碟機不同的實體磁碟上。 變更位置至有空間可容納資料庫日誌的位置。|
    |ATA 中心服務 IP 位址：連接埠|這是 ATA 中心服務會接聽 ATA 閘道通訊的 IP 位址。<br /><br />**預設連接埠：**443|按一下向下箭頭選取 ATA 中心服務要使用的 IP 位址。<br /><br />此 IP 位址與 ATA 中心服務的連接埠不能和 ATA 主控台的 IP 位址與連接埠相同。 請務必變更 ATA 主控台的連接埠。|
    |ATA 中心服務 SSL 憑證|這是 ATA 中心服務將使用的憑證。|按一下鑰匙圖示以選取安裝的憑證，或者，在實驗室環境中部署時可選取自我簽署的憑證。|
    |ATA 主控台 IP 位址|這是 ATA 主控台的 IIS 將使用的 IP 位址。|按一下向下箭頭選取 ATA 主控台要使用的 IP 位址。 **注意︰** 記下此 IP 位址，可讓您更輕鬆地從 ATA 閘道存取 ATA 主控台。|
    |ATA 主控台 SSL 憑證|這是IIS 將使用的憑證。|按一下鑰匙圖示以選取安裝的憑證，或者，在實驗室環境中部署時可選取自我簽署的憑證。|
    ![ATA 中心設定映像](media/ATA-Center-Configuration.JPG)

7.  按一下 [安裝]**** 安裝 ATA 及其元件，並建立 ATA 中心與 ATA 主控台之間的連線。

8.  安裝完成後，按一下 [啟動]**** 連線至 ATA 主控台。

    安裝 ATA 中心時將安裝及設定下列元件︰

    -   Internet Information Services (IIS)

    -   MongoDB

    -   ATA 中心服務和 ATA 主控台 IIS 站台

    -   自訂的效能監視資料收集組

    -   自我簽署的憑證 (如果在安裝期間有選取)

> [!NOTE]
> 為了有助於進行疑難排解和產品增強功能，建議您安裝 MongoVue 和任何其他 MongoDB 增益集，或您選擇的任何其他協力廠商工具。 需有 .Net Framework 3.5 才能安裝 MongoVue。

### 驗證安裝

1.  檢查 Microsoft Advanced Threat Analytics 中心服務是否正在執行。

2.  按一下桌面上的 Microsoft Advanced Threat Analytics 捷徑，連線到 ATA 主控台。 以您安裝 ATA 中心的相同使用者認證登入。 初次登入 ATA 主控台時，系統會自動將您帶到 [網域連線設定]**** 頁面，以繼續進行 ATA 閘道的設定和部署。

3.  檢閱 **Microsoft.Tri.Center-Errors.log** 檔案中的錯誤檔案，此檔案可以在此預設位置中找到：%programfiles%\Microsoft Advanced Threat Analytics\Center\Logs。

>[!div class="step-by-step"]
[« 預先安裝](install-ata-preinstall.md)
[步驟 2 »](install-ata-step2.md)

## 另請參閱

- [如需支援，請查看我們的論壇！](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)
- [設定事件收集](/advanced-threat-analytics/plandesign/configure-event-collection)
- [ATA 必要條件](/advanced-threat-analytics/plandesign/ata-prerequisites)


<!--HONumber=Apr16_HO2-->


