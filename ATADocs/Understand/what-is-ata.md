---
title: "什麼是 Microsoft Advanced Threat Analytics (ATA)？ | Microsoft Docs"
description: "說明何謂 Microsoft Advanced Threat Analytics (ATA)，以及它可以偵測到的可疑活動種類"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 09/28/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 283e7b4e-996a-4491-b7f6-ff06e73790d2
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 85e285c5d88e5916e0bf0eb7dd327cb4cb45b4cb
ms.openlocfilehash: 70d66bccfda484722afa63a7f85dc8f85013f54f


---

適用於︰Advanced Threat Analytics 1.7 版


## <a name="what-is-advanced-threat-analytics"></a>什麼是 Advanced Threat Analytics？
Advanced Threat Analytics (ATA) 是內部部署平台，可協助保護您的企業免於受到多種進階鎖定目標類型的網路攻擊和內部威脅。

## <a name="how-ata-works"></a>ATA 的運作方式
ATA 會從網路中的記錄檔和事件取得多個資料來源的資訊，了解組織中使用者和其他實體的行為，並建立其相關行為的設定檔。
ATA 可以從下列項目接收事件和記錄檔︰

-   SIEM 整合
-   Windows 事件轉送 (WEF)

此外，ATA 還會利用專用的網路剖析引擎擷取和剖析多個通訊協定 (例如 Kerberos、DNS、RPC、NTLM 和其他) 的網路流量，進行驗證、授權和資訊的收集。 ATA 會透過下列項目收集此資訊：

-   從網域控制站和 DNS 伺服器將連接埠鏡像設定至 ATA 閘道
-   在網域控制站上直接部署 ATA 輕量型閘道 (LGW)

如需 ATA 架構的詳細資訊，請參閱 [ATA 架構](/advanced-threat-analytics/plan-design/ata-architecture)。

## <a name="what-does-ata-do"></a>ATA 有何作用？

ATA 技術會偵測多個可疑的活動，將焦點放在網路攻擊狙殺鏈的幾個階段，包括︰

-   探查，此時攻擊者會收集有關環境的建置方式、不同資產和實體存在的差異為何，而且通常會建置下一個攻擊階段的計畫。
-   橫向移動週期，此時攻擊者會將時間與精力放在在網路內部分散攻擊面。
-   網域支配 (持續性)，此時攻擊者會擷取資訊以便使用各種進入點、認證和技術繼續進行活動。 

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

如需偵測的完整清單及其描述，請參閱 [ATA 可以偵測哪些可疑的活動？](ata-threats.md)
ATA 會偵測這些可疑的活動，並且在 ATA 主控台中呈現各項資訊，包括人員、內容、時間和方式的清楚檢視。 透過監視此簡單、方便使用的儀表板，您就可以看到 ATA 懷疑網路中的用戶端 1 和用戶端 2 電腦上有傳遞雜湊攻擊的警示。

 ![範例 ATA 螢幕傳遞雜湊](media/sample screen pth.png)

**異常行為** - ATA 使用行為分析並運用機器學習，發現網路的使用者和裝置中有可疑的活動和異常行為，包括︰

-   異常的登入
-   不明的威脅
-   共用密碼
-   橫向移動


您可以在 ATA 儀表板中檢視此類型的可疑活動。 在下列範例中，ATA 會在某位使用者存取 4 台平常不會存取的電腦時警示您，這可能是造成警示的原因。

 ![範例 ATA 螢幕異常行為](media/sample screen abnormal behavior.png) 

ATA 也會偵測**安全性問題與風險**，包括︰

-   信任中斷
-   弱式通訊協定
-   已知的通訊協定弱點

您可以在 ATA 儀表板中檢視此類型的可疑活動。 在下列範例中，ATA 讓您知道網路中的電腦和網域之間的信任關係已中斷。

  ![範例 ATA 螢幕信任中斷](media/sample screen broken trust.png)


## <a name="whats-next"></a>新功能

-   如需 ATA 如何融入網路的詳細資訊︰[ATA 架構](/advanced-threat-analytics/plan-design/ata-architecture)

-   若要開始部署 ATA：[安裝 ATA](/advanced-threat-analytics/deploy-use/install-ata)

## <a name="see-also"></a>另請參閱
[查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Jan17_HO1-->


