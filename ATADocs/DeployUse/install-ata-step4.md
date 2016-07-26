---
title: "安裝 ATA - 步驟 4 | Microsoft ATA"
description: "安裝 ATA 的步驟 4 協助您安裝 ATA 閘道。"
keywords: 
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: get-started-article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 6bbc50c3-bfa8-41db-a2f9-56eed68ef5d2
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: a5c7163bc7b1989672e587bfb4fa6a65cd4e3751
ms.openlocfilehash: 1cd9bafa0bfcd00e9801e252553382d98d3905f8


---

# 安裝 ATA - 步驟 4

>[!div class="step-by-step"]
[« 步驟 3](install-ata-step3.md)
[步驟 5 »](install-ata-step5.md)

## 步驟 4： 安裝 ATA 閘道

在專用伺服器上安裝 ATA 閘道之前，請先驗證連接埠鏡像都已正確設定，而且 ATA 閘道可以查看往來網域控制站的流量。 如需詳細資訊，請參閱[驗證連接埠鏡像](validate-port-mirroring.md)。


> [!IMPORTANT]
> 請確定 [KB2919355](http://support.microsoft.com/kb/2919355/) 已安裝。  執行以下 PowerShell Cmdlet 來檢查是否已安裝 hotfix：
>
> `Get-HotFix -Id kb2919355`

在 ATA 閘道伺服器上執行下列步驟。

1.  解壓縮 Zip 檔案。 
> [!NOTE] 
> 從 ZIP 檔案直接安裝將會失敗。

2.  從提升權限的命令提示字元執行 **Microsoft ATA Gateway Setup.exe**，然後遵循安裝精靈的步驟。

3.  在 [歡迎] 頁面中，選取您的語言，然後按一下 [下一步]。

4.  在 [ATA 閘道設定] 下，根據您的環境輸入下列資訊︰

    ![ATA 閘道組態設定影像](media/ATA-Gateway-Configuration.JPG)

    |欄位|說明|註解|
    |---------|---------------|------------|
    |安裝路徑|這是將安裝 ATA 閘道的位置。 位置預設為 %programfiles%\Microsoft Advanced Threat Analytics\Gateway|保留預設值|
    |ATA 閘道服務 SSL 憑證|這是 ATA 閘道將使用的憑證。|自我簽署憑證僅適合使用在實驗室環境中。|
    |ATA 閘道註冊|輸入 ATA 系統管理員的使用者名稱和密碼。|要使 ATA 閘道器向 ATA 中心登錄，請輸入已安裝 ATA 中心的使用者名稱和密碼。 此使用者必須是 ATA 中心下列其中一個本機群組的成員。<br /><br />-   系統管理員<br />-   Microsoft Advanced Threat Analytics 管理員 **注意︰**這些認證只用於登錄而不會儲存在 ATA 上。|
    安裝 ATA 閘道期間將安裝及設定下列元件︰

    -   KB 3047154

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

## 另請參閱

- [查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [設定事件收集](configure-event-collection.md)
- [ATA 必要條件](/advanced-threat-analytics/plan-design/ata-prerequisites)




<!--HONumber=Jul16_HO3-->


