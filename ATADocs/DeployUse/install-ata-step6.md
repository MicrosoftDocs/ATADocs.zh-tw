---
title: "安裝 Advanced Threat Analytics - 步驟 6 | Microsoft Docs"
description: "在安裝 ATA 的最後一個步驟裡，您可以設定 Honeytoken 使用者。"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 01/23/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 8980e724-06a6-40b0-8477-27d4cc29fd2b
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 70b8c4886f1c7459412eafc0646abfe1cc5d37d3
ms.sourcegitcommit: 49e892a82275efa5146998764e850959f20d3216
translationtype: HT
---
適用於︰Advanced Threat Analytics 1.7 版



# <a name="install-ata---step-6"></a>安裝 ATA - 步驟 6

>[!div class="step-by-step"]
[« 步驟 5](install-ata-step5.md)

## <a name="step-6-configure--ip-address-exclusions-and-honeytoken-user"></a>步驟 6： 設定 IP 位址排除項目和 Honeytoken 使用者
ATA 可從兩種類型的偵測排除特定的 IP 位址︰**DNS 探查**和**傳遞票證**。 

例如，**DNS 探查排除項目**可以是一個使用 DNS 做為掃描機制的安全性掃描程式。 排除項目可協助 ATA 忽略這類掃描器。 「傳遞票證」排除項目的一個範例是 NAT 裝置。    

ATA 也可以用來設定 Honeytoken 使用者，用來當做惡意執行者的設陷 - 與此 (通常是休眠) 帳戶相關聯的任何驗證將會觸發警示。

若要設定上述項目，請依照下列步驟進行：

1.  從 ATA 主控台按一下設定圖示，然後選取 [設定]。

    ![ATA 組態設定](media/ATA-config-icon.JPG)

2.  在 [偵測排除項目] 下，針對 [DNS 探查] 或 [傳遞票證] 輸入 IP 位址，然後按一下*加號*。

    ![儲存變更](media/ATA-exclusions.png)

3.  在 [偵測設定] 下輸入 Honeytoken 帳戶的 SID，然後按一下加號。 例如：`S-1-5-21-72081277-1610778489-2625714895-10511`。

    ![ATA 組態設定](media/ATA-honeytoken.png)

    > [!NOTE]
    > 若要尋找使用者的 SID，請在 ATA 主控台中搜尋使用者，然後按一下 [帳戶資訊] 索引標籤。 

4.  按一下 [儲存]。


恭喜，您已成功部署 Microsoft Advanced Threat Analytics！

檢查受攻擊的時間線以便檢視偵測到的可疑活動，並搜尋使用者或電腦並檢視其設定檔。

ATA 將立即開始掃描是否有可疑的活動。 某些活動 (例如某些可疑行為的活動) 會等到 ATA 有時間建立行為設定檔之後 (至少三週) 才可以使用。


>[!div class="step-by-step"]
[« 步驟 5](install-ata-step5.md)


## <a name="see-also"></a>另請參閱

- [查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [設定事件收集](configure-event-collection.md)
- [ATA 必要條件](/advanced-threat-analytics/plan-design/ata-prerequisites)

