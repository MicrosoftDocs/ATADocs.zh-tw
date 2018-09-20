---
title: 安裝 Advanced Threat Analytics - 步驟 8 | Microsoft Docs
description: 在安裝 ATA 的最後一個步驟裡，您可以設定 Honeytoken 使用者。
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 6/14/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: 8980e724-06a6-40b0-8477-27d4cc29fd2b
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: eacc3c2449e6fd7771c43b97b8ed08276ab130d2
ms.sourcegitcommit: 959b1f7753b9a8ad94870d2014376d55296fbbd4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/18/2018
ms.locfileid: "46133529"
---
*適用於：Advanced Threat Analytics 1.9 版*



# <a name="install-ata---step-8"></a>安裝 ATA - 步驟 8

>[!div class="step-by-step"]
[« 步驟 7](vpn-integration-install-step.md)
[步驟 9 »](install-ata-step9-samr.md)

## <a name="step-8-configure-ip-address-exclusions-and-honeytoken-user"></a>步驟 8： 設定 IP 位址排除項目和 Honeytoken 使用者
ATA 可從一些偵測排除特定 IP 位址或使用者。 

例如，**DNS 探查排除項目**可以是一個使用 DNS 做為掃描機制的安全性掃描程式。 排除項目可協助 ATA 忽略這類掃描器。 「傳遞票證」排除項目的一個範例是 NAT 裝置。    

ATA 也能讓您設定 Honeytoken 使用者，用來作為針對惡意執行者的陷阱。所有與此 (通常是休眠的) 帳戶相關聯的驗證都會觸發警示。

若要設定此帳戶，請遵循下列步驟︰

1.  從 ATA 主控台按一下設定圖示，然後選取 [設定]。

    ![ATA 組態設定](media/ATA-config-icon.png)

2.  在 [偵測] 下，按一下 [實體標記]。

2. 在 [Honeytoken 帳戶] 下，輸入 Honeytoken 帳戶名稱。 [Honeytoken 帳戶] 欄位是可搜尋的，而且會自動顯示您網路中的實體。

   ![Honeytoken](media/honeytoken.png)

3. 按一下 [排除]。 針對每個威脅類型，輸入要從這些威脅偵測排除的使用者帳戶或 IP 位址，然後按一下「加號」符號。 [加入實體] \(使用者或電腦\) 欄位是可搜尋的，而且會自動填入您網路中的實體。 如需詳細資訊，請參閱[從偵測中排除實體](excluding-entities-from-detections.md)

   ![排除](media/exclusions.png)

4.  按一下 **[儲存]**。


恭喜，您已成功部署 Microsoft Advanced Threat Analytics！

檢查受攻擊的時間線以便檢視偵測到的可疑活動，並搜尋使用者或電腦並檢視其設定檔。

ATA 會立即開始掃描是否有可疑的活動。 某些活動 (例如某些可疑行為的活動) 需等到 ATA 有時間建置行為設定檔之後 (至少需三週的時間) 才會提供。

若要確定 ATA 已啟動並執行，以及攔截網路中的漏洞，您可以查看 [ATA 攻擊模擬腳本](https://docs.microsoft.com/enterprise-mobility-security/solutions/ata-attack-simulation-playbook)。


>[!div class="step-by-step"]
[« 步驟 7](vpn-integration-install-step.md)
[步驟 9 »](install-ata-step9-samr.md)


## <a name="related-videos"></a>相關影片
- [ATA 部署概觀](https://channel9.msdn.com/Shows/Microsoft-Security/Overview-of-ATA-Deployment-in-10-Minutes)
- [選擇正確的 ATA 閘道類型](https://channel9.msdn.com/Shows/Microsoft-Security/ATA-Deployment-Choose-the-Right-Gateway-Type)


## <a name="see-also"></a>另請參閱
- [ATA POC 部署指南](http://aka.ms/atapoc)
- [ATA 調整大小工具](http://aka.ms/atasizingtool)
- [查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [設定事件收集](configure-event-collection.md)
- [ATA 必要條件](ata-prerequisites.md)

