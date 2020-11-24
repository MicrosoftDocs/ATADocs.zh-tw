---
title: 適用於身分識別的 AzMicrosoft Defender：使用者調查教學課程
description: 本文說明如何使用適用於身分識別的 Microsoft Defender 安全性警訊來調查可疑使用者。
keywords: ''
author: shsagir
ms.author: shsagir
ms.date: 10/26/2020
ms.topic: tutorial
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: f92e8ffc2ed30e858c5bb0e7728f8f4c76309a2a
ms.sourcegitcommit: e2227c0b0e5aaa5163dc56d4131ca82f8dca8fb0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2020
ms.locfileid: "94848460"
---
# <a name="tutorial-investigate-a-user"></a>教學課程：調查使用者

> [!NOTE]
> 此頁面所述的[!INCLUDE [Product long](includes/product-long.md)] 功能也可使用新的[入口網站](https://portal.cloudappsecurity.com)來存取。

[!INCLUDE [Product long](includes/product-long.md)] 警訊辨識項和橫向移動路徑清楚指出使用者何時執行可疑活動，或何時存在其帳戶已遭入侵的跡象。 在此教學課程中，您將使用調查建議來協助判斷組織的風險、決定如何進行補救，並判斷最能防止日後遭受類似攻擊的方式。

> [!div class="checklist"]
>
> - 收集使用者的相關資訊。
> - 調查使用者執行的活動。
> - 調查使用者存取的資源。
> - 調查橫向移動路徑。

## <a name="recommended-investigation-steps-for-suspicious-users"></a>針對可疑使用者的建議調查步驟

檢查並調查使用者設定檔中的下列詳細資料和活動：

1. 誰是[使用者](entity-profiles.md)？
    1. 使用者是否為[敏感性使用者](sensitive-accounts.md) (例如系統管理員或關注清單等)？
    1. 他們在組織中扮演什麼角色？
    1. 他們在組織樹狀目錄中是否重要？

1. 要[調查](investigate-entity.md)的可疑活動：
    1. 使用者在 [!INCLUDE [Product short](includes/product-short.md)] 或其他安全性工具 (例如適用於端點的 Microsoft Defender、Azure 資訊安全中心及/或 Microsoft CAS) 中，是否有其他已開啟的警訊？
    1. 使用者是否有失敗的登入？
    1. 使用者存取了哪些資源？
    1. 使用者是否存取了高價值的資源？
    1. 使用者是否應該具有所存取資源的存取權？
    1. 使用者登入了哪些電腦？
    1. 使用者是否應該登入這些電腦？
    1. 使用者與敏感性使用者之間是否有[橫向移動路徑](use-case-lateral-movement-path.md) (LMP)？

## <a name="see-also"></a>另請參閱

- [調查電腦](investigate-a-computer.md)
- [使用安全性警訊](working-with-suspicious-activities.md)
- [使用橫向移動路徑](use-case-lateral-movement-path.md)
- [偵察警訊](reconnaissance-alerts.md)
- [遭入侵的認證警訊](compromised-credentials-alerts.md)
- [橫向移動警訊](lateral-movement-alerts.md)
- [網域支配警訊](domain-dominance-alerts.md)
- [外流警訊](exfiltration-alerts.md)
- [查看[!INCLUDE [Product short](includes/product-short.md)] 論壇！](https://aka.ms/MDIcommunity)\(英文\)
