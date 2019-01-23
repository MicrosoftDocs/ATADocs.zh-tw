---
title: 安裝 Advanced Threat Analytics - 步驟 1 | Microsoft Docs
description: 安裝 ATA 的第一步驟是下載並安裝 ATA 中心到您所選的伺服器。
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 1/10/2019
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: b3cceb18-0f3c-42ac-8630-bdc6b310f1d6
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 00bce1b381b32e1fe3fe9a2bb2c11016b33699f7
ms.sourcegitcommit: 6a0ac21f59e72db8615811da2c886f54cf3727f5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/13/2019
ms.locfileid: "54249924"
---
適用對象：*Advanced Threat Analytics 1.9 版*


# <a name="install-ata---step-1"></a>安裝 ATA - 步驟 1

> [!div class="step-by-step"]
> [步驟 2 »](install-ata-step2.md)

此安裝程序提供執行 ATA 1.9 全新安裝的指示。 如需從舊版更新現有 ATA 部署的資訊，請參閱 [1.9 版 ATA 移轉指南](ata-update-1.9-migration-guide.md)。

> [!IMPORTANT] 
> 如果使用 Windows 2012 R2，開始安裝之前，您可以先在 ATA 中心伺服器和 ATA 閘道伺服器上安裝 KB2934520；若沒有這麼做，ATA 安裝會安裝此更新，並需要在 ATA 安裝期間重新啟動。

## <a name="step-1-download-and-install-the-ata-center"></a>步驟 1： 下載並安裝 ATA 中心
確認伺服器符合需求之後，您可以繼續 ATA 中心的安裝。
    
> [!NOTE]
>如果您直接透過 Office 365 入口網站或透過雲端解決方案提供者 (CSP) 授權模型取得 Enterprise Mobility + Security (EMS) 的授權，而且無法透過 Microsoft 大量授權服務中心 (VLSC) 存取 ATA，請連絡 Microsoft 客戶支援服務以取得啟動 Advanced Threat Analytics (ATA) 的程序。

在 ATA 中心伺服器上執行下列步驟。

1.  從 [Microsoft 大量授權服務中心](https://www.microsoft.com/Licensing/servicecenter/default.aspx)、[TechNet Evaluation Center](http://www.microsoft.com/evalcenter/) 或 [MSDN](https://msdn.microsoft.com/subscriptions/downloads) 下載 ATA。

2.  請以本機系統管理員群組成員的使用者身分，登入要安裝 ATA 中心的電腦。

3.  執行 **Microsoft ATA Center Setup.EXE**，然後遵循安裝精靈的步驟。

> [!NOTE]   
> 請務必從本機磁碟機執行安裝檔案，而不是從掛接的 ISO 檔案執行，以避免安裝過程中必須重新開機的問題。   

4.  當您開始安裝時，如果未安裝 Microsoft .Net Framework，系統會提示您安裝它。 安裝 .NET Framework 之後，可能會出現重新開機的提示。
5.  在**歡迎**頁面上選取要用於 ATA 安裝畫面的語言，然後按 **[下一步]**。

6.  閱讀 Microsoft 軟體授權條款，如果您接受條款，請按一下核取方塊，然後按一下 [下一步]。

7.  建議您將 ATA 設為自動更新。 如果您未在電腦上設定 Windows 使其執行此動作，您會看到 [使用 Microsoft Update 協助您的電腦保持在安全和最新的狀態] 畫面。 
    ![保持 ATA 最新狀態影像](media/ata_ms_update.png)

8. 選取 [當我檢查更新時使用 Microsoft Update (建議選項)]。 如下所示，如此可調整 Windows 設定，以允許其他 Microsoft 產品 (包括 ATA) 的更新。 

    ![Windows 自動更新影像](media/ata_installupdatesautomatically.png)

8.  在 [Configure the Center (設定中心)] 頁面中，根據您的環境輸入下列資訊：

    |欄位|說明|註解|
    |---------|---------------|------------|
    |安裝路徑|這是要安裝 ATA 中心的位置。 位置預設為 %programfiles%\Microsoft Advanced Threat Analytics\Center|保留預設值|
    |資料庫資料路徑|這是 MongoDB 資料庫檔案的所在位置。 位置預設為 %programfiles%\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\data|變更位置至有空間可隨著您的規模成長的位置。 **注意︰** <ul><li>在生產環境中，您應該根據容量規劃使用具有足夠空間的磁碟機。</li><li>大規模部署的資料庫應該放在個別的實體磁碟上。</li></ul>如需大小資訊，請參閱 [ATA 容量規劃](ata-capacity-planning.md)。|
    |中心服務 SSL 憑證|這是 ATA 主控台與 ATA 中心服務所使用的憑證。|按一下鑰匙圖示以選取安裝的憑證，或者，在實驗室環境中部署時可選取自我簽署的憑證。 您可以選擇建立自我簽署憑證。|
        
    ![ATA 中心設定映像](media/ATA-Center-Configuration.png)

10.  按一下 [安裝] 來安裝 ATA 中心及其元件。
    安裝 ATA 中心時將安裝及設定下列元件︰

    -   ATA 中心服務

    -   MongoDB

    -   自訂的效能監視資料收集組

    -   自我簽署的憑證 (如果在安裝期間有選取)

11.  安裝完成時，請按一下 [啟動] 開啟 ATA 主控台，然後在 [設定] 頁面上完成設定。
此時，系統會自動將您帶到 [一般] 設定頁面，以繼續進行 ATA 閘道的設定和部署。
由於您使用 IP 位址登入網站，因此會收到與憑證相關的警告，這是正常現象，且您應該按一下 [繼續瀏覽此網站]。

### <a name="validate-installation"></a>驗證安裝

1.  檢查名為 **Microsoft Advanced Threat Analytics 中心**的服務是否正在執行。
2.  按一下桌面上的 [Microsoft Advanced Threat Analytics] 捷徑以連線到 ATA 主控台。 以您安裝 ATA 中心的相同使用者認證登入。

### <a name="set-anti-virus-exclusions"></a>設定防毒程式排除項目

在安裝 ATA 中心後，您應排除 MongoDB 資料庫目錄，使防毒應用程式不持續對其進行掃描。 資料庫中的預設位置為：**C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\data**。

請確定您也將下列資料夾和處理序排除在 AV 掃描之外：

**Folders** C:\Program Files\Microsoft Advanced Threat Analytics\Center\ParentKerberosAsBloomFilters
<br>C:\Program Files\Microsoft Advanced Threat Analytics\Center\ParentKerberosTgsBloomFilters
<br>C:\Program Files\Microsoft Advanced Threat Analytics\Center\Backup
<br>C:\Program Files\Microsoft Advanced Threat Analytics\Center\Logs

**處理序**
<br>mongod.exe
<br>Microsoft.Tri.Center.exe


如果您將 ATA 安裝在不同的目錄，務必要依照您安裝的位置變更資料夾路徑。 

> [!div class="step-by-step"]
> [«前置安裝](configure-port-mirroring.md)
> [步驟 2»](install-ata-step2.md)

## <a name="related-videos"></a>相關影片
- [選擇正確的 ATA 閘道類型](https://channel9.msdn.com/Shows/Microsoft-Security/ATA-Deployment-Choose-the-Right-Gateway-Type)
- [ATA 部署概觀](https://channel9.msdn.com/Shows/Microsoft-Security/Overview-of-ATA-Deployment-in-10-Minutes)


## <a name="see-also"></a>另請參閱
- [ATA POC 部署指南](http://aka.ms/atapoc)
- [ATA 調整大小工具](http://aka.ms/atasizingtool)
- [查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [設定事件收集](configure-event-collection.md)
- [ATA 必要條件](ata-prerequisites.md)

