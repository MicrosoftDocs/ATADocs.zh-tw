---
title: 適用于身分識別的 Microsoft Defender 設定偵測排除專案和 honeytoken 帳戶
description: 設定偵測排除範圍和 Honeytoken 使用者。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 10/26/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: fb4aa3b26c9026a62aac81bd1a88b50b95141ecd
ms.sourcegitcommit: e2227c0b0e5aaa5163dc56d4131ca82f8dca8fb0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2020
ms.locfileid: "94848477"
---
# <a name="configure-detection-exclusions-and-honeytoken-accounts"></a>設定偵測排除範圍和 Honeytoken 帳戶

[!INCLUDE [Product long](includes/product-long.md)] 可從一些偵測中排除特定 IP 位址或使用者。

例如，**DNS 探查排除項目** 可以是一個使用 DNS 做為掃描機制的安全性掃描程式。 排除有助於 [!INCLUDE [Product short](includes/product-short.md)] 忽略這類掃描器。

[!INCLUDE [Product short](includes/product-short.md)] 也可讓您設定 honeytoken 帳戶，以做為惡意執行者的陷阱-與這些 honeytoken 帳戶相關聯的任何驗證 (正常休眠) ，會觸發警示。

若要設定，請依照下列步驟執行︰

1. 從[!INCLUDE [Product short](includes/product-short.md)] 入口網站，按一下設定圖示，然後選取 [設定]。

    ![[!包含 [Product short] (include/product-short. md) ] configuration settings](media/config-menu.png)

1. 在 [偵測]  下，按一下 [實體標記]  。

1. 在 [Honeytoken 帳戶] 下，輸入 Honeytoken 帳戶名稱並按一下 [+] 符號。 [Honeytoken 帳戶] 欄位是可搜尋的，而且會自動顯示您網路中的實體。 按一下 **[儲存]** 。

    ![Honeytoken](media/honeytoken-sensitive.png)

1. 按一下 [排除]  。 針對每個威脅類型，輸入要排除而不予偵測的使用者帳戶或 IP 位址。
1. 按一下加號  。 [加入實體]  \(使用者或電腦\) 欄位是可搜尋的，而且會自動填入您網路中的實體。 如需詳細資訊，請參閱[從偵測中排除實體](excluding-entities-from-detections.md)和[安全性警訊指南](suspicious-activity-guide.md)。

    ![從偵測中排除實體](media/exclusions.png)

1. 按一下 **[儲存]** 。

恭喜，您已成功部署 [!INCLUDE [Product long](includes/product-long.md)] ！

檢查攻擊時間表以檢視從所偵測到之活動產生的安全性警示，並搜尋使用者或電腦並檢視其設定檔。

[!INCLUDE [Product short](includes/product-short.md)] 掃描立即開始。 某些偵測（例如 [敏感性群組的可疑新增](domain-dominance-alerts.md#suspicious-additions-to-sensitive-groups-external-id-2024)專案）需要學習期間，因此無法在部署後立即使用 [!INCLUDE [Product short](includes/product-short.md)] 。每個警示的學習期間會列在詳細的 [安全性警示指南](suspicious-activity-guide.md)中。

## <a name="see-also"></a>另請參閱

- [[!INCLUDE [Product short](includes/product-short.md)] 大小調整工具](https://aka.ms/aatpsizingtool) \(英文\)
- [設定事件收集](configure-event-collection.md)
- [[!INCLUDE [Product short](includes/product-short.md)] 先決條件](prerequisites.md)
- [查看[!INCLUDE [Product short](includes/product-short.md)] 論壇！](https://aka.ms/MDIcommunity)\(英文\)
