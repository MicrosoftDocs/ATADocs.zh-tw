---
title: 適用于身分識別設定偵測排除專案的 Microsoft Defender
description: 偵測排除專案的設定。
ms.date: 02/17/2021
ms.topic: how-to
ms.openlocfilehash: 6e771e2a2755845fe4f02fb9d21750720bbbe37d
ms.sourcegitcommit: f92dca4dc3d8a25b1a06f68ac7a9f8318105bcd8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/17/2021
ms.locfileid: "100630767"
---
# <a name="configure-detection-exclusions"></a>設定偵測排除專案

[!INCLUDE [Product long](includes/product-long.md)] 可從一些偵測中排除特定的 IP 位址、電腦或使用者。

例如，**DNS 探查排除項目** 可以是一個使用 DNS 做為掃描機制的安全性掃描程式。 排除有助於 [!INCLUDE [Product short](includes/product-short.md)] 忽略這類掃描器。

## <a name="how-to-add-detection-exclusions"></a>如何新增偵測排除專案

您可以透過兩種方式，手動排除使用者、電腦或 IP 位址以進行偵測。 您可以在 [設定] 頁面的 [**排除**]**或 [直接** 從安全性警示] 中進行這項操作。

### <a name="from-the-configuration-page"></a>從 [設定] 頁面

若要從 [設定] 頁面設定排除專案，請執行下列動作：

1. 在[!INCLUDE [Product short](includes/product-short.md)] 中，選取 [設定]。

    ![[!包含 [Product short] (include/product-short. md) ] configuration settings](media/config-menu.png)

1. 在 [ **偵測**] 下，選取 [ **排除**]。
1. 針對您想要設定的每個偵測，請執行下列動作：
    1. 輸入要從偵測中排除的 IP 位址、電腦或使用者帳戶
    1. 按一下加號圖示 **(+)**。

    > [!TIP]
    > 使用者或電腦欄位是可搜尋的，而且會自動填入您網路中的實體。 如需詳細資訊，請參閱[從偵測中排除實體](excluding-entities-from-detections.md)和[安全性警訊指南](suspicious-activity-guide.md)。

    ![從偵測中排除實體](media/exclusions.png)

1. 按一下 **[儲存]** 。

### <a name="from-a-security-alert"></a>從安全性警示

若要從安全性警示設定排除專案，請執行下列動作：

1. 在 [!INCLUDE [Product short](includes/product-short.md)] 入口網站中，選取 [ **時程表**]。
1. 識別允許執行特定活動之使用者、電腦或 IP **位址的活動** 警示。

1. 在警示的右邊，選取 **[...]**  > **關閉和排除**。 此動作會關閉警示，而不會再列于 **警示時間軸** 的 [**開啟** 事件] 清單中。 此動作也會將使用者、電腦或 IP 位址新增至該警示的排除清單。

    ![排除實體](media/exclude-in-sa.png)

[!INCLUDE [Product short](includes/product-short.md)] 掃描立即開始。 某些偵測（例如 [敏感性群組的可疑新增](domain-dominance-alerts.md#suspicious-additions-to-sensitive-groups-external-id-2024)專案）需要學習期間，因此無法在部署後立即使用 [!INCLUDE [Product short](includes/product-short.md)] 。 每個警示的學習期間會列在詳細的 [安全性警示指南](suspicious-activity-guide.md)中。

## <a name="see-also"></a>另請參閱

- [設定事件收集](configure-event-collection.md)
- [查看[!INCLUDE [Product short](includes/product-short.md)] 論壇！](https://aka.ms/MDIcommunity)\(英文\)
