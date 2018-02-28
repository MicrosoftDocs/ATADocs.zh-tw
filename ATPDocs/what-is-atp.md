---
title: "什麼是 Azure 進階威脅防護 (ATP)？ | Microsoft Docs"
description: "說明何謂 Azure 進階威脅防護 (ATP)，以及它可以偵測到的可疑活動種類"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2018
ms.topic: article
ms.prod: 
ms.service: azure-advanced-threat-protection
ms.technology: 
ms.assetid: 2d14d0e9-1b03-4bcc-ae97-8fd41526ffc5
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 5ccac90a171c895ee8b4d5336a125ccd7fa66239
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/21/2018
---
適用於：Azure 進階威脅防護


# <a name="what-is-azure-advanced-threat-protection"></a>什麼是 Azure 進階威脅防護？
Azure 進階威脅防護 (ATP) 為雲端服務，可保護您的企業混合式環境，以防止多種進階目標式網路攻擊及內部威脅。

## <a name="how-azure-atp-works"></a>Azure ATP 的運作方式

Azure ATP 會利用專用的網路剖析引擎來擷取和剖析多個通訊協定 (例如 Kerberos、DNS、RPC、NTLM 和其他) 的網路流量，以進行驗證、授權和資訊收集。 Azure ATP 會透過下列方式收集此資訊：

-   直接在您的網域控制站上部署 Azure ATP 感應器
-   從網域控制站和 DNS 伺服器將連接埠鏡像設定至 Azure ATP 獨立式感應器

Azure ATP 會從多個資料來源 (例如網路中的記錄檔和事件) 取得資訊，以了解組織中使用者和其他實體的行為，並建立其相關行為的設定檔。
Azure ATP 可以從下列項目接收事件和記錄檔︰

-   SIEM 整合
-   Windows 事件轉送 (WEF)
-   直接從 Windows Event Collector (適用於感應器)
-   從 VPN 進行 RADIUS 帳戶處理


如需 Azure ATP 架構的詳細資訊，請參閱 [Azure ATP 架構](atp-architecture.md)。

## <a name="what-does-azure-atp-do"></a>Azure ATP 有何功能？

Azure ATP 技術可偵測多種可疑的活動，專注於網路攻擊狙殺鏈的數個階段，包括︰

-   「偵查」階段，此時攻擊者會收集有關環境的建構方式、有哪些不同的資產，以及存在何種實體等資訊。 他們通常會著手規劃下一階段的攻擊。
-   橫向移動週期，此時攻擊者會將時間與精力放在在網路內部分散攻擊面。
-   「網域支配 (持續性)」階段，此時攻擊者會擷取資訊，以便使用各種進入點、認證和技術繼續進行攻擊活動。 

無論何種公司受到攻擊，或者何種資訊遭到鎖定，這些網路攻擊階段都非常類似而且可預測。
Azure ATP 會搜尋三種主要的攻擊︰惡意攻擊、異常行為和安全性問題與風險。

**惡意的攻擊**會藉由確定的條件來偵測，也可透過異常行為分析來偵測。 已知攻擊類型的完整清單包括：

-   傳遞票證 (PtT)
-   傳遞雜湊 (PtH)
-   越過雜湊
-   偽造的 PAC (MS14-068)
-   黃金票證
-   惡意的複寫
-   目錄服務列舉
-   SMB 工作階段列舉
-   DNS 探查
-   水平暴力密碼破解 
-   垂直暴力密碼破解
-   基本架構金鑰
-   異常通訊協定
-   加密降級
-   遠端執行
-   惡意的服務建立


Azure ATP 會偵測這些可疑的活動，並且在 Azure ATP 工作區入口網站中呈現各項資訊，包括人員、內容、時間和方式的清楚檢視。 透過監視此簡單且方便使用的儀表板，您就會警覺到 Azure ATP 懷疑網路中的用戶端 1 和用戶端 2 電腦上有傳遞票證攻擊。

 ![傳遞票證 Azure ATP 畫面範例](media/pass-the-ticket-sa.png)


Azure ATP 也會偵測**安全性問題與風險**，包括︰

-   弱式通訊協定
-   已知的通訊協定弱點
-   [機密帳戶的橫向移動路徑](use-case-lateral-movement-path.md)

# <a name="what-threats-does-azure-atp-look-for"></a>Azure ATP 會尋找哪些威脅？

Azure ATP 提供下列進階攻擊各階段的偵測︰探查、認證入侵、橫向移動、權限提升、網域支配等等。 這些偵測的目標是在造成組織危害之前偵測到進階攻擊和內部威脅。

每個階段的偵測會產生與問題階段相關的數個可疑活動，而每個可疑活動各與不同類別的可能攻擊相互關聯。
下列影像標示了 Azure ATP 目前可偵測的狙殺鏈階段：

![Azure ATP 著重在攻擊狙殺鏈中的橫向活動](media/attack-kill-chain-small.jpg)


如需詳細資訊，請參閱[處理可疑活動](working-with-suspicious-activities.md)和 [Azure ATP 可疑活動指南](suspicious-activity-guide.md)。

## <a name="whats-next"></a>新功能

-   如需 Azure ATP 如何融入網路的詳細資訊︰[Azure ATP 架構](atp-architecture.md)

-   開始部署 ATP：[安裝ATP](install-atp-step1.md)


## <a name="see-also"></a>另請參閱
- [Azure ATP 常見問題集](atp-technical-faq.md)
- [查看 ATP 論壇！](https://aka.ms/azureatpcommunity)\(英文\)