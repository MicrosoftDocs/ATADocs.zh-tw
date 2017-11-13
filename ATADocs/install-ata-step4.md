---
title: "安裝 Advanced Threat Analytics - 步驟 4 | Microsoft Docs"
description: "安裝 ATA 的步驟 4 協助您安裝 ATA 閘道。"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 11/7/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 6bbc50c3-bfa8-41db-a2f9-56eed68ef5d2
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 4abeda5a54de771c6e6d3c73d9217113dfe88b8e
ms.sourcegitcommit: 4d2ac5b02c682840703edb0661be09055d57d728
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/07/2017
---
適用於︰Advanced Threat Analytics 1.8 版



# <a name="install-ata---step-4"></a>安裝 ATA - 步驟 4

>[!div class="step-by-step"]
[« 步驟 3](install-ata-step3.md)
[步驟 5 »](install-ata-step5.md)

## <a name="step-4-install-the-ata-gateway"></a>步驟 4： 安裝 ATA 閘道

在專用伺服器上安裝 ATA 閘道之前，請先驗證連接埠鏡像都已正確設定，而且 ATA 閘道可以查看往來網域控制站的流量。 如需詳細資訊，請參閱[驗證連接埠鏡像](validate-port-mirroring.md)。


> [!IMPORTANT]
> 請確定 [KB2919355](http://support.microsoft.com/kb/2919355/) 已安裝。  執行以下 PowerShell Cmdlet 來檢查是否已安裝 hotfix：
>
> `Get-HotFix -Id kb2919355`

在 ATA 閘道伺服器上執行下列步驟。

1.  解壓縮 Zip 檔案。 
> [!NOTE] 
> 從 ZIP 檔案直接安裝會失敗。

2.  執行 **Microsoft ATA Gateway Setup.exe**，然後依照安裝精靈的步驟。

3.  在 [歡迎] 頁面中，選取您的語言，然後按一下 [下一步]。

4.  安裝精靈會自動檢查伺服器為網域控制站或專用伺服器。 如果是網域控制站，系統會安裝 ATA 輕量型閘道；如果是專用伺服器，系統會安裝 ATA 閘道。 
    
    例如，針對 ATA 閘道，系統會顯示下列畫面以通知將會在您的專用伺服器上安裝 ATA 閘道：
    
    ![ATA 閘道安裝](media/ata-gw-install.png) 按一下 [下一步]。

    > [!NOTE] 
    > 如果網域控制站或專用伺服器不符合安裝的最低硬體需求，您會收到一則警告。 但這並不會阻止您按 [下一步] 和繼續進行安裝。 在不需要這麼多資料儲存空間的小型實驗室測試環境中，這可能會是安裝 ATA 的正確選項。 如果是生產環境，強烈建議使用 ATA 的 [容量規劃](ata-capacity-planning.md)指南，確保您的網域控制站或專用伺服器符合必要需求。

4.  在 [Configure the Gateway (設定閘道)] 下，根據您的環境輸入下列資訊：

    ![ATA 閘道組態設定影像](media/ata-gw-configure.png)

    > [!NOTE]
    > 當您部署 ATA 閘道時，您不必提供認證。 如果 ATA 閘道安裝無法使用單一登入擷取您的認證 (例如，如果 ATA 中心或 ATA 閘道不在網域中，或是您沒有 ATA 系統管理員認證，就會發生此情況)，系統會提示您提供認證，如下列畫面所示： 

  ![提供 ATA 閘道認證](media/ata-install-credentials.png)

   - 安裝路徑：這是安裝 ATA 閘道的位置。 位置預設為 %programfiles%\Microsoft Advanced Threat Analytics\Gateway。 保留預設值。
    
5. 按一下 [安裝]。 安裝 ATA 閘道期間將安裝及設定下列元件︰

    -   KB 3047154 (僅適用於 Windows Server 2012 R2)

        > [!IMPORTANT]
        > -   請勿將 KB 3047154 安裝於虛擬主機 (執行虛擬化的主機；可在虛擬機器上執行)。 這可能會導致連接埠鏡像無法正常運作。 
        > -   請勿在 ATA 閘道上安裝 Message Analyzer、Wireshark 或其他網路擷取軟體。 如果您需要擷取網路流量，請安裝並使用 Microsoft Network Monitor 3.4。

    -   ATA 閘道服務
    -   Microsoft Visual C++ 2013 可轉散發元件
    -   自訂的效能監視資料收集組

5.  安裝完成之後，若是 ATA 閘道，請按一下 [啟動] 開啟瀏覽器，然後登入 ATA 主控台；若是 ATA 輕量型閘道，請按一下 [完成]。


>[!div class="step-by-step"]
[« 步驟 3](install-ata-step3.md)
[步驟 5 »](install-ata-step5.md)


## <a name="related-videos"></a>相關影片
- [ATA 部署概觀](https://channel9.msdn.com/Shows/Microsoft-Security/Overview-of-ATA-Deployment-in-10-Minutes)
- [選擇正確的 ATA 閘道類型](https://channel9.msdn.com/Shows/Microsoft-Security/ATA-Deployment-Choose-the-Right-Gateway-Type)

## <a name="see-also"></a>另請參閱
- [ATA POC 部署指南](http://aka.ms/atapoc)
- [ATA 調整大小工具](http://aka.ms/atasizingtool)
- [查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [設定事件收集](configure-event-collection.md)
- [ATA 必要條件](ata-prerequisites.md)

