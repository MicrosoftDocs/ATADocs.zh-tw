---
title: Azure ATP 使用者調查教學課程 | Microsoft Docs
d|Description: This article explains how to user Azure ATP security alerts to investigate a suspicious user.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 1/14/2019
ms.topic: tutorial
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: e9cf68d2-36bd-4b0d-b36e-7cf7ded2618e
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 126653dd2831e0e3dbd9c777d84d32b1c2e74bd9
ms.sourcegitcommit: 1ee052c4c6b04b290e2d5384c24b65a108b1f1f3
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/14/2019
ms.locfileid: "54253396"
---
# <a name="tutorial-investigate-a-user"></a>教學課程：調查使用者

Azure ATP 警示辨識項和橫向移動路徑清楚指出使用者何時執行可疑活動，或何時存在其帳戶已遭入侵的跡象。 您可以使用調查建議來協助判斷組織的風險、決定如何進行修復，並判斷防止類似未來攻擊的最佳方式。  

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
