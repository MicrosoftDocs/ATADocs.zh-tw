---
title: Azure ATP 使用者調查教學課程 | Microsoft Docs
d|Description: This article explains how to user Azure ATP security alerts to investigate a suspicious user.
keywords: ''
author: mlottner
ms.author: mlottner
ms.date: 09/15/2019
ms.topic: tutorial
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: fdf0c4cc32137b23f7c2170a2c8dd0132b3b6462
ms.sourcegitcommit: 6dd002b5a34f230aaada55a6f6178c2f9e1584d9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2019
ms.locfileid: "71004768"
---
# <a name="tutorial-investigate-a-user"></a>教學課程：調查使用者

> [!NOTE]
> 此頁面所述的 Azure ATP 功能也可使用新的[入口網站](https://portal.cloudappsecurity.com)來存取。

Azure ATP 警示辨識項和橫向移動路徑清楚指出使用者何時執行可疑活動，或何時存在其帳戶已遭入侵的跡象。 在此教學課程中，您將使用調查建議來協助判斷組織的風險、決定如何進行補救，並判斷最能防止日後遭受類似攻擊的方式。  

> [!div class="checklist"]
> * 收集使用者的相關資訊。
> * 調查使用者執行的活動。
> * 調查使用者存取的資源。
> * 調查橫向移動路徑。

## <a name="recommended-investigation-steps-for-suspicious-users"></a>針對可疑使用者的建議調查步驟

檢查並調查使用者設定檔中的下列詳細資料和活動：

1. 誰是[使用者](entity-profiles.md)？
     1. 使用者是否為[敏感性使用者](sensitive-accounts.md) (例如系統管理員或關注清單等)？  
     2. 他們在組織中扮演什麼角色？
     3. 他們在組織樹狀目錄中是否重要？

2. 要[調查](investigate-entity.md)的可疑活動：
     1. 使用者在 Azure ATP 或其他安全性工具 (例如 Windows Defender-ATP、Azure 資訊安全中心及/或 Microsoft CAS) 中，是否有其他已開啟的警示？
     2. 使用者是否有失敗的登入？
     3. 使用者存取了哪些資源？  
     4. 使用者是否存取了高價值的資源？  
     5. 使用者是否應該具有所存取資源的存取權？  
     6. 使用者登入了哪些電腦？ 
     7. 使用者是否應該登入這些電腦？
     8. 使用者與敏感性使用者之間是否有[橫向移動路徑](use-case-lateral-movement-path.md) (LMP)？


## <a name="see-also"></a>另請參閱

- [調查電腦](investigate-a-computer.md)
- [使用安全性警訊](working-with-suspicious-activities.md)
- [使用橫向移動路徑](use-case-lateral-movement-path.md)
- [偵察警訊](atp-reconnaissance-alerts.md)
- [遭入侵的認證警訊](atp-compromised-credentials-alerts.md)
- [橫向移動警訊](atp-lateral-movement-alerts.md)
- [網域支配警訊](atp-domain-dominance-alerts.md)
- [外流警訊](atp-exfiltration-alerts.md)
- [查看 Azure ATP 論壇！](https://aka.ms/azureatpcommunity)
