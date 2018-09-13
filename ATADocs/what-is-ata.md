---
title: 什麼是 Microsoft Advanced Threat Analytics (ATA)？ | Microsoft Docs
description: 說明何謂 Microsoft Advanced Threat Analytics (ATA)，以及它可以偵測到的可疑活動種類
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 7/24/2018
ms.topic: conceptual
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: 283e7b4e-996a-4491-b7f6-ff06e73790d2
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 518e248c013c781a86fa8a4d212ff7079be2175f
ms.sourcegitcommit: 5ad28d7b0607c7ea36d795b72928769c629fb80a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/07/2018
ms.locfileid: "44166199"
---
*適用於：Advanced Threat Analytics 1.9 版*


# <a name="what-is-advanced-threat-analytics"></a>什麼是 Advanced Threat Analytics？
Advanced Threat Analytics (ATA) 是內部部署平台，可協助保護您的企業免於受到多種進階鎖定目標類型的網路攻擊和內部威脅。

## <a name="how-ata-works"></a>ATA 的運作方式

ATA 會利用專用的網路剖析引擎來擷取和剖析多個通訊協定 (例如 Kerberos、DNS、RPC、NTLM 和其他) 的網路流量，以進行驗證、授權和資訊的收集。 ATA 會透過下列項目收集此資訊：

-   從網域控制站和 DNS 伺服器將連接埠鏡像設定至 ATA 閘道，及/或
-   在網域控制站上直接部署 ATA 輕量型閘道 (LGW)

ATA 會從多個資料來源 (例如網路中的記錄檔和事件) 取得資訊，以了解組織中使用者和其他實體的行為，並建立有關他們的行為設定檔。
ATA 可以從下列項目接收事件和記錄檔︰

-   SIEM 整合
-   Windows 事件轉送 (WEF)
-   直接從 Windows Event Collector (適用於輕量型閘道)


如需 ATA 架構的詳細資訊，請參閱 [ATA 架構](ata-architecture.md)。

## <a name="what-does-ata-do"></a>ATA 有何作用？

ATA 技術會偵測多個可疑的活動，將焦點放在網路攻擊狙殺鏈的幾個階段，包括︰

-   「偵查」階段，此時攻擊者會收集有關環境的建構方式、有哪些不同的資產，以及存在何種實體等資訊。 一般而言，攻擊者在此階段建立其下一個攻擊階段的計畫。
-   橫向移動週期，此時攻擊者會將時間與精力放在在網路內部分散攻擊面。
-   「網域支配 (持續性)」階段，此時攻擊者會擷取資訊，以便能使用各種進入點、認證和技術來繼續進行攻擊活動。 

無論何種公司受到攻擊，或者何種資訊遭到鎖定，這些網路攻擊階段都非常類似而且可預測。
ATA 會搜尋三種主要的攻擊︰惡意攻擊、異常行為和安全性問題與風險。

**惡意攻擊**可以透過尋找已知攻擊類型的完整清單很容易偵測到，包括︰

-   傳遞票證 (PtT)
-   傳遞雜湊 (PtH)
-   越過雜湊
-   偽造的 PAC (MS14-068)
-   黃金票證
-   惡意的複寫
-   探查
-   暴力密碼破解
-   遠端執行

如需偵測的完整清單及其描述，請參閱 [ATA 可以偵測哪些可疑的活動？](ata-threats.md)。 

ATA 會偵測這些可疑的活動，並且在 ATA 主控台中呈現各項資訊，包括人員、內容、時間和方式的清楚檢視。 透過監視此簡單且方便使用的儀表板，就可以看到警示，指出 ATA 懷疑網路中的用戶端 1 和用戶端 2 電腦上有傳遞票證攻擊。

 ![ATA 傳遞票證畫面範例](media/pass_the_ticket_sa.png)

**異常行為** - ATA 使用行為分析並運用機器學習，發現網路的使用者和裝置中有可疑的活動和異常行為，包括︰

-   異常的登入
-   不明的威脅
-   共用密碼
-   橫向移動
-   敏感性群組的修改


您可以在 ATA 儀表板中檢視此類型的可疑活動。 在下列範例中，ATA 會在某位使用者存取四台他平常不會存取的電腦時警示您，因為這可能是您應該警覺的情況。

 ![範例 ATA 螢幕異常行為](media/abnormal-behavior-sa.png) 

ATA 也會偵測**安全性問題與風險**，包括︰

-   信任中斷
-   弱式通訊協定
-   已知的通訊協定弱點

您可以在 ATA 儀表板中檢視此類型的可疑活動。 在下列範例中，ATA 讓您知道網路中的電腦和網域之間的信任關係已中斷。

  ![範例 ATA 螢幕信任中斷](media/broken-trust-sa.png)


## <a name="known-issues"></a>已知問題

- 更新至 ATA 1.7 後，如果您沒有更新 ATA 閘道就立即更新至 ATA 1.8，您會無法移轉至 ATA 1.8。 您必須先將所有閘道更新至 1.7.1 或 1.7.2 版，才能將 ATA 中心更新至 1.8 版。

- 如果您選取執行完整移轉的選項，視資料庫大小而定，可能需要很長的時間。 當您選取移轉選項時，系統會顯示估計時間；請記下此時間，再決定要選取哪個選項。 


## <a name="whats-next"></a>新功能

-   如需 ATA 如何融入網路的詳細資訊︰[ATA 架構](ata-architecture.md)

-   若要開始部署 ATA：[安裝 ATA](install-ata-step1.md)

## <a name="related-videos"></a>相關影片
- [加入安全性社群](https://channel9.msdn.com/Shows/Microsoft-Security/Join-the-Security-Community)
- [ATA 部署概觀](https://channel9.msdn.com/Shows/Microsoft-Security/Overview-of-ATA-Deployment-in-10-Minutes)


## <a name="see-also"></a>另請參閱
[ATA 可疑活動腳本](http://aka.ms/ataplaybook)
[查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
