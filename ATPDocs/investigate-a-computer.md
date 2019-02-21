---
title: Azure ATP 電腦調查教學課程 | Microsoft Docs
d|Description: This article explains how to use Azure ATP security alerts to investigate a suspicious computer.
keywords: ''
author: mlottner
ms.author: mlottner
ms.date: 02/07/2019
ms.topic: tutorial
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 547fcb9173d8e51687124bac3f555a4eedc3634d
ms.sourcegitcommit: c48db18274edb2284e281960c6262d97f96e01d2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/14/2019
ms.locfileid: "56263500"
---
# <a name="tutorial-investigate-a-computer"></a>教學課程：調查電腦

Azure ATP 警示辨識項清楚指出電腦何時涉及可疑活動，或何時存在電腦已遭入侵的跡象。 在此教學課程中，您將使用調查建議來協助判斷組織的風險、決定如何進行補救，並判斷最能防止日後遭受類似攻擊的方式。  

> [!div class="checklist"]
> * 檢查已登入使用者的電腦。
> * 驗證使用者是否是以正常方式存取電腦。
> * 調查電腦的可疑活動。
> * 同一時間是否有其他警訊？


## <a name="investigation-steps-for-suspicious-computers"></a>針對可疑電腦的調查步驟

若要存取電腦設定檔頁面，請按一下您想要調查警示中所提及的特定電腦。 為了協助您進行調查，警示辨識項會列出與每個可疑活動相關的所有電腦 (及[使用者](investigate-a-user.md))。

檢查並調查電腦設定檔中的下列詳細資料和活動：

- 在可疑活動期間發生什麼事？  
  1. 哪位[使用者](investigate-a-user.md)已登入電腦？
  2. 該使用者是否正常登入或存取來源或目的地電腦？
  3. 在何處存取了哪些資源？ 哪些使用者進行了存取？
      - 如果資源已被存取，那些資源是否價值很高？
  4. 使用者是否應該存取這些資源？
  5. 存取電腦的[使用者](investigate-a-user.md)是否執行其他可疑活動？

- 要調查的其他可疑活動：
    1. 在此警示期間，是否有其他警示在 Azure ATP 或其他安全性工具 (例如 Windows Defender ATP、Azure 資訊安全中心及/或 Microsoft CAS) 中開啟？
    2. 是否有失敗的登入？


- 如果已啟用 Windows Defender ATP 整合，請按一下 Windows Defender ATP 徽章進一步調查電腦。 在 Windows Defender ATP 中，您可以查看在警示期間所發生的處理序與警示。
    1. 是否已部署或安裝任何新程式？

## <a name="next-steps"></a>後續步驟

- [調查使用者](investigate-a-user.md)
- [使用安全性警訊](working-with-suspicious-activities.md)
- [使用橫向移動路徑](use-case-lateral-movement-path.md)
- [偵察警訊](atp-reconnaissance-alerts.md)
- [遭入侵的認證警訊](atp-compromised-credentials-alerts.md)
- [橫向移動警訊](atp-lateral-movement-alerts.md)
- [網域支配警訊](atp-domain-dominance-alerts.md)
- [外流警訊](atp-exfiltration-alerts.md)
- [查看 Azure ATP 論壇！](https://aka.ms/azureatpcommunity)