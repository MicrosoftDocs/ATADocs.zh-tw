---
title: 安裝 Advanced 威脅分析-步驟1
description: 安裝 ATA 的第一步驟是下載並安裝 ATA 中心到您所選的伺服器。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 01/12/2021
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: b3cceb18-0f3c-42ac-8630-bdc6b310f1d6
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: bef73309e71acd067c02a5ff597f0b5397a09fc7
ms.sourcegitcommit: 5bf0c6a204b71126306a0c64108eaf9cb7fc042f
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/18/2021
ms.locfileid: "101097550"
---
# <a name="install-ata---step-1"></a>安裝 ATA - 步驟 1

[!INCLUDE [Banner for top of topics](includes/banner.md)]

> [!NOTE]
> **支援週期**
>
> ATA 的最終發行版本已 [正式推出](https://support.microsoft.com/help/4568997/update-3-for-microsoft-advanced-threat-analytics-1-9)。 ATA 主流支援于2021年1月12日結束。 延伸支援將繼續進行，直到2026年1月為止。 如需詳細資訊，請閱讀 [我們的 blog](https://techcommunity.microsoft.com/t5/microsoft-security-and/end-of-mainstream-support-for-advanced-threat-analytics-january/ba-p/1539181)。

> [!div class="step-by-step"]
> [步驟2»](install-ata-step2.md)

此安裝程序提供執行 ATA 1.9 全新安裝的指示。 如需從舊版更新現有 ATA 部署的資訊，請參閱 [1.9 版 ATA 移轉指南](ata-update-1.9-migration-guide.md)。

> [!IMPORTANT]
> 如果使用 Windows 2012 R2，開始安裝之前，您可以先在 ATA 中心伺服器和 ATA 閘道伺服器上安裝 KB2934520；若沒有這麼做，ATA 安裝會安裝此更新，並需要在 ATA 安裝期間重新啟動。

## <a name="step-1-download-and-install-the-ata-center"></a>步驟 1： 下載並安裝 ATA 中心

確認伺服器符合需求之後，您可以繼續 ATA 中心的安裝。

> [!NOTE]
> 如果您直接透過 Microsoft 365 入口網站或雲端解決方案合作夥伴 (CSP) 授權模型取得 Enterprise Mobility + Security (EMS) 的授權，而且無法透過 Microsoft 大量授權服務中心 (VLSC) 存取 ATA，請連絡 Microsoft 客戶支援服務，以取得啟用 Advanced Threat Analytics (ATA) 的程序。

在 ATA 中心伺服器上執行下列步驟。

1. 從 [Microsoft 大量授權服務中心](https://www.microsoft.com/Licensing/servicecenter/default.aspx) 或從 [TechNet 評估中心](https://www.microsoft.com/evalcenter/) 或 [MSDN](/powerapps/developer/common-data-service/org-service/subscribe-sdk-assembly-updates-using-nuget)下載 ATA。

1. 請以本機系統管理員群組成員的使用者身分，登入要安裝 ATA 中心的電腦。

1. 以較高的許可權執行 **MICROSOFT ATA 中心 Setup.EXE** ([以 **系統管理員身分執行** ]) ，然後遵循安裝程式。

    > [!NOTE]
    > 請務必從本機磁碟機執行安裝檔案，而不是從掛接的 ISO 檔案執行，以避免安裝過程中必須重新開機的問題。

1. 如果未安裝 Microsoft .NET Framework，當您開始安裝時，系統會提示您安裝它。 安裝 .NET Framework 之後，可能會出現重新開機的提示。
1. 在 [ **歡迎使用** ] 頁面上，選取要用於 ATA 安裝畫面的語言，然後按 **[下一步]**。

1. 閱讀 Microsoft 軟體授權條款。在您接受條款之後，請按一下接受核取方塊，然後按一下 [下一步]。

1. 我們建議將 ATA 設定為自動更新。 如果您未在電腦上將 Windows 設定為自動更新，您將會看到 [使用 Microsoft Update 協助您的電腦保持在安全和最新的狀態] 畫面。
    ![保持 ATA 最新狀態影像](media/ata_ms_update.png)

1. 選取 [當我檢查更新時使用 Microsoft Update (建議選項)]。 這可調整 Windows 設定，以允許其他 Microsoft 產品 (包括 ATA) 的更新。

    ![Windows 自動更新影像](media/ata_installupdatesautomatically.png)

1. 在 [Configure the Center (設定中心)] 頁面中，根據您的環境輸入下列資訊：

    |欄位|描述|註解|
    |---------|---------------|------------|
    |安裝路徑|這是要安裝 ATA 中心的位置。 位置預設為 %programfiles%\Microsoft Advanced Threat Analytics\Center|保留預設值|
    |資料庫資料路徑|這是 MongoDB 資料庫檔案的所在位置。 位置預設為 %programfiles%\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\data|變更位置至有空間可隨著您的規模成長的位置。 **注意：** <ul><li>在生產環境中，您應該根據容量規劃使用具有足夠空間的磁碟機。</li><li>大規模部署的資料庫應該放在個別的實體磁碟上。</li></ul>如需大小資訊，請參閱 [ATA 容量規劃](ata-capacity-planning.md)。|
    |中心服務 SSL 憑證|這是 ATA 主控台與 ATA 中心服務所使用的憑證。|按一下鑰匙圖示以選取已安裝的憑證，或使用核取方塊來建立自我簽署憑證。|

    ![ATA 中心設定映像](media/ATA-Center-Configuration.png)

    > [!NOTE]
    > 請務必留意有關中心服務 SSL 憑證狀態和到期警告的健康情況警示。 如果憑證過期，您必須完全重新部署 ATA。

1. 按一下 [安裝] 來安裝 ATA 中心及其元件。  
安裝 ATA 中心時將安裝及設定下列元件︰

    - ATA 中心服務

    - MongoDB

    - 自訂的效能監視資料收集組

    - 自我簽署的憑證 (如果在安裝期間有選取)

1. 安裝完成時，請按一下 [啟動] 開啟 ATA 主控台，然後從 [設定] 頁面完成設定。
    [一般] 設定頁面隨即開啟，以繼續進行 ATA 閘道的設定和部署。
    由於您使用 IP 位址登入網站，因此會收到與憑證相關的警告，這是正常現象，且您應該按一下 [繼續瀏覽此網站]。

### <a name="validate-installation"></a>驗證安裝

1. 檢查名為 **Microsoft Advanced Threat Analytics 中心** 的服務是否正在執行。
1. 按一下桌面上的 [Microsoft Advanced Threat Analytics] 捷徑以連線到 ATA 主控台。 以您用來安裝 ATA 中心的使用者認證登入。

### <a name="set-anti-virus-exclusions"></a>設定防毒程式排除項目

在安裝 ATA 中心後，請排除 MongoDB 資料庫目錄，使防毒應用程式不持續對其進行掃描。 在資料庫中的預設路徑為︰**C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin\data**。

請確定您也將下列資料夾和處理序排除在 AV 掃描之外：

**資料夾**  
C:\Program Files\Microsoft Advanced Threat Analytics\Center\ParentKerberosAsBloomFilters  
C:\Program Files\Microsoft Advanced Threat Analytics\Center\ParentKerberosTgsBloomFilters  
C:\Program Files\Microsoft Advanced Threat Analytics\Center\Backup  
C:\Program Files\Microsoft Advanced Threat Analytics\Center\Logs

**處理序**  
mongod.exe  
Microsoft.Tri.Center.exe

如果您將 ATA 安裝在不同的目錄，請務必依照您安裝的位置變更資料夾路徑。

> [!div class="step-by-step"]
> [«預先安裝](configure-port-mirroring.md) 
> [步驟2»](install-ata-step2.md)

## <a name="related-videos"></a>相關影片

- [選擇正確的 ATA 閘道類型](https://channel9.msdn.com/Shows/Microsoft-Security/ATA-Deployment-Choose-the-Right-Gateway-Type)
- [ATA 部署概觀](https://channel9.msdn.com/Shows/Microsoft-Security/Overview-of-ATA-Deployment-in-10-Minutes)

## <a name="see-also"></a>另請參閱

- [ATA POC 部署指南](/samples/browse/?redirectedfrom=TechNet-Gallery)
- [ATA 調整大小工具](https://aka.ms/atasizingtool)
- [查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [設定事件收集](configure-event-collection.md)
- [ATA 必要條件](ata-prerequisites.md)