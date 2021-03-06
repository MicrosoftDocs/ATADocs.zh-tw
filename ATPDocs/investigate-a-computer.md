---
title: 適用於身分識別的 Microsoft Defender 電腦調查教學課程
description: 此文章說明如何使用適用於身分識別的 Microsoft Defender 安全性警示來調查可疑電腦。
ms.date: 10/26/2020
ms.topic: tutorial
ms.openlocfilehash: dac0630eda6ef81b0af3125fcd05d1d91b43c906
ms.sourcegitcommit: cdb7ae4580851e25aae24d07e7d66a750aa54405
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2020
ms.locfileid: "96543913"
---
# <a name="tutorial-investigate-a-computer"></a>教學課程：調查電腦

> [!NOTE]
> 此頁面所述的[!INCLUDE [Product long](includes/product-long.md)] 功能也可使用新的[入口網站](https://portal.cloudappsecurity.com)來存取。

[!INCLUDE [Product long](includes/product-long.md)] 警示辨識項清楚指出電腦何時涉及可疑活動，或何時存在電腦已遭入侵的跡象。 在此教學課程中，您將使用調查建議來協助判斷組織的風險、決定如何進行補救，並判斷最能防止日後遭受類似攻擊的方式。  

> [!div class="checklist"]
>
> - 檢查已登入使用者的電腦。
> - 驗證使用者是否是以正常方式存取電腦。
> - 調查電腦的可疑活動。
> - 同一時間是否有其他警訊？

## <a name="investigation-steps-for-suspicious-computers"></a>針對可疑電腦的調查步驟

若要存取電腦設定檔頁面，請按一下您想要調查警示中所提及的特定電腦。 為了協助您進行調查，警示辨識項會列出與每個可疑活動相關的所有電腦 (及[使用者](investigate-a-user.md))。

檢查並調查電腦設定檔中的下列詳細資料和活動：

- 在可疑活動期間發生什麼事？  
    1. 哪位[使用者](investigate-a-user.md)已登入電腦？
    1. 該使用者是否正常登入或存取來源或目的地電腦？
    1. 在何處存取了哪些資源？ 哪些使用者進行了存取？
      - 如果資源已遭存取，那些資源是否為高價值資源？
    1. 使用者是否應該存取這些資源？
    1. 存取電腦的[使用者](investigate-a-user.md)是否執行其他可疑活動？

- 要調查的其他可疑活動：
    1. 在此警示期間，是否有其他警示在[!INCLUDE [Product short](includes/product-short.md)] 或其他安全性工具 (例如適用於端點的 Microsoft Defender、Azure 資訊安全中心和/或 Microsoft CAS) 中開啟？
    1. 是否有失敗的登入？

- 如果已啟用適用於端點的 Microsoft Defender 整合，請按一下適用於端點的 Microsoft Defender 徽章進一步調查電腦。 在適用於端點的 Microsoft Defender 中，您可以查看在警示期間所發生的處理序與警示。
    - 是否已部署或安裝任何新程式？

## <a name="next-steps"></a>後續步驟

- [調查使用者](investigate-a-user.md)
- [使用安全性警訊](working-with-suspicious-activities.md)
- [使用橫向移動路徑](use-case-lateral-movement-path.md)
- [偵察警訊](reconnaissance-alerts.md)
- [遭入侵的認證警訊](compromised-credentials-alerts.md)
- [橫向移動警訊](lateral-movement-alerts.md)
- [網域支配警訊](domain-dominance-alerts.md)
- [外流警訊](exfiltration-alerts.md)
- [查看[!INCLUDE [Product short](includes/product-short.md)] 論壇！](https://aka.ms/MDIcommunity)\(英文\)
