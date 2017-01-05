---
title: "安裝 ATA - 步驟 4 | Microsoft Docs"
description: "安裝 ATA 的步驟 4 協助您安裝 ATA 閘道。"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 08/24/2016
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 6bbc50c3-bfa8-41db-a2f9-56eed68ef5d2
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 85e285c5d88e5916e0bf0eb7dd327cb4cb45b4cb
ms.openlocfilehash: ebaab5e8768d6b78c6d9ff93fa1430673827e483


---

適用於︰Advanced Threat Analytics 1.7 版



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
> 從 ZIP 檔案直接安裝將會失敗。

2.  執行 **Microsoft ATA Gateway Setup.exe**，然後依照安裝精靈的步驟。

3.  在 [歡迎] 頁面中，選取您的語言，然後按一下 [下一步]。

4.  安裝精靈會自動檢查伺服器為網域控制站或專用伺服器。 如果是網域控制站，將會安裝 ATA 輕量型閘道，如果是專用伺服器，將會安裝 ATA 閘道。 
    
    例如，如果是 ATA 輕量型閘道，則顯示下列畫面讓您知道將會在您的網域控制站上安裝 ATA 輕量型閘道︰
    
    ![ATA 輕量型閘道安裝](media/ATA-lightweight-gateway-install-selected.png) 按 [下一步]。

    > [!NOTE] 
    > 如果網域控制站或專用伺服器不符合安裝的最低硬體需求，您會收到一則警告。 但這並不會阻止您按 [下一步] 和繼續進行安裝。 在不需要這麼多資料儲存空間的小型實驗室測試環境中，則需要使用此選項安裝 ATA。 如果是生產環境，強烈建議使用 ATA 的 [容量規劃](/advanced-threat-analytics/plan-design/ata-capacity-planning)指南，確保您的網域控制站或專用伺服器符合必要需求。

4.  在 [ATA 閘道設定] 下，根據您的環境輸入下列資訊︰

    ![ATA 閘道組態設定影像](media/ATA-Gateway-Configuration.png)

    |欄位|說明|註解|
    |---------|---------------|------------|
    |安裝路徑|這是將安裝 ATA 閘道的位置。 位置預設為 %programfiles%\Microsoft Advanced Threat Analytics\Gateway|保留預設值|
    |閘道服務 SSL 憑證|這是 ATA 閘道將使用的憑證。|自我簽署憑證僅適合使用在實驗室環境中。|
    |閘道註冊|輸入 ATA 系統管理員的使用者名稱和密碼。|要使 ATA 閘道器向 ATA 中心登錄，請輸入已安裝 ATA 中心的使用者名稱和密碼。 此使用者必須是 ATA 中心下列其中一個本機群組的成員。<br /><br />-   系統管理員<br />-   Microsoft Advanced Threat Analytics 管理員 **注意︰**這些認證只用於登錄而不會儲存在 ATA 上。|
    
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

## <a name="see-also"></a>另請參閱

- [查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [設定事件收集](configure-event-collection.md)
- [ATA 必要條件](/advanced-threat-analytics/plan-design/ata-prerequisites)




<!--HONumber=Jan17_HO1-->


