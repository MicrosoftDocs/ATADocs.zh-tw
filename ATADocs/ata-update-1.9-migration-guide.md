---
title: 1.9 遷移指南的 Advanced 威脅分析更新
description: 將 ATA 更新至 1.9 版的程序
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 03/25/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 2946310a-8e4e-48fc-9450-fc9647efeb22
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 2277e8eb6cbfb9c61dd0e814d6f2170599ff9c86
ms.sourcegitcommit: c7c0a4c9f7507f3e8e0f219798ed7d347c03e792
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/22/2020
ms.locfileid: "90911823"
---
# <a name="updating-ata-to-version-19"></a>將 ATA 更新至 1.9 版

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

> [!NOTE] 
> 如果您的環境中未安裝 ATA，請下載包括 1.9 版的 ATA 完整版本，並遵循[安裝 ATA](install-ata-step1.md) 中所述的標準安裝程序。

如果您已經部署 ATA 1.8 版，此程序會逐步引導您進行更新部署所需的步驟。

> [!NOTE] 
>  只有 ATA 1.8 (1.8.6645) 與 ATA 1.8 Update 1 (1.8.6765) 可以更新至 ATA 1.9 版，任何舊版的 ATA 都不能直接更新至 ATA 1.9 版。

請遵循下列步驟將 ATA 更新至 1.9 版：

1.  [從下載中心下載 ATA 1.9 版的更新](https://www.microsoft.com/download/details.aspx?id=56725)，或從 [評估中心](https://www.microsoft.com/evalcenter/evaluate-microsoft-advanced-threat-analytics)下載完整版本。<br>
在移轉版本中，檔案只能用於從 ATA 1.8 版更新。 在評估中心的版本中，會使用相同的安裝檔案 (Microsoft ATA Center Setup.exe) 來安裝新的 ATA 部署及升級現有的部署。

1. 更新 ATA 中心

1. 更新 ATA 閘道

    > [!IMPORTANT]
    > 更新所有 ATA 閘道以確保 ATA 正常運作。

### <a name="step-1-update-the-ata-center"></a>步驟 1︰更新 ATA 中心

1. 備份您的資料庫：(選擇性)

   - 如果 ATA 中心是作為虛擬機器執行，而您想要取得一個檢查點，請先關閉虛擬機器。

   - 如果 ATA 中心正在實體伺服器上執行，請參閱[災害復原](disaster-recovery.md)一文以取得備份資料庫的相關資訊。

1. 執行安裝檔案 **Microsoft ATA Center Setup.exe**，並依照螢幕上的指示安裝更新。

   - 在 [歡迎]**** 頁面中，選擇您的語言，然後按一下 [下一步]****。

   - 如果您未在 1.8 版中啟用自動更新，系統會提示您設定 ATA，以使用 Microsoft Update 讓 ATA 保持最新狀態。  在 [Microsoft Update] 頁面中，選取 [ **當我檢查更新時使用 Microsoft Update] (建議的) **。
     ![保持 ATA 最新狀態影像](media/ata_ms_update.png)
     
     這會調整 Windows 設定，以針對 ATA 啟用更新。 
    
   - **部分資料移轉**畫面可讓您得知先前擷取的網路流量、事件、實體，以及偵測相關的資料已刪除。 除了異常行為偵測、異常群組修改、使用目錄服務的偵察 (SAM-R)，以及加密降級偵測 (在必要的學習時間後，需要最多三個禮拜的時間才能建置完整設定檔) 以外，所有偵測皆會立即生效。 
     
     ![ATA 部分移轉](media/partial-migration.png)

   - 按一下 [更新]。 按一下 [更新] 之後，ATA 會離線直到更新程序完成。

1. ATA 中心更新順利完成之後，按一下 [啟動]**** 開啟 ATA 閘道之 ATA 主控台中的 [更新]**** 畫面。

    ![更新成功畫面](media/migration-center-success.png)

1. 在 [更新]**** 畫面中，如果您已經設定 ATA 閘道自動更新，它們就會現在更新。如果未設定自動更新，請按一下每個 ATA 閘道旁邊的 [更新]****。
  
    ![更新閘道影像](media/migration-update-gw.png)

  
> [!IMPORTANT] 
> 更新所有 ATA 閘道以確保 ATA 正常運作。
 
> [!NOTE] 
> 若要安裝新的 ATA 閘道，請移至 [ **網** 關] 畫面，然後按一下 [ **下載閘道安裝程式** ] 以取得 ATA 1.9 閘道安裝套件，並遵循步驟4中所述的新閘道安裝指示 [。安裝 ATA 閘道](install-ata-step4.md)。


## <a name="see-also"></a>另請參閱

- [查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
