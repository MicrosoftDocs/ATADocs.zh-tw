---
title: 適用于身分識別活動篩選和原則的 Microsoft Defender Microsoft Cloud App Security
description: 使用 Microsoft Cloud App Security 的身分識別活動篩選和原則的 Microsoft Defender 總覽。
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
ms.openlocfilehash: 0f6a359745ae03ce0b982e00b7f4c06d556eb702
ms.sourcegitcommit: e2227c0b0e5aaa5163dc56d4131ca82f8dca8fb0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2020
ms.locfileid: "94848817"
---
# <a name="use-activity-filters-and-create-action-policies-with-product-long-in-microsoft-cloud-app-security"></a>在 Microsoft Cloud App Security 中使用活動篩選和建立動作原則 [!INCLUDE [Product long](includes/product-long.md)]

本文旨在協助您瞭解如何使用 Microsoft Cloud App Security 來篩選和建立活動的動作原則 [!INCLUDE [Product short](includes/product-short.md)] 。

如需如何完成整合的詳細資訊，請參閱[ [!INCLUDE [Product short](includes/product-short.md)] 與 Cloud App Security 整合](/cloud-app-security/aatp-integration)。

使用 [!INCLUDE [Product short](includes/product-short.md)] with Microsoft Cloud App Security 可提供以使用者和實體行為分析為基礎的活動分析和警示 (UEBA) 、識別企業中的風險最高行為、提供完整的調查優先順序分數，以及活動篩選和可自訂的活動原則。

## <a name="prerequisites"></a>必要條件

如需跨混合式環境的完整使用者調查功能，您必須具備：

- Microsoft Cloud App Security 的有效授權
- [!INCLUDE [Product long](includes/product-long.md)]連接到您的 Active Directory 實例的有效授權

>[!NOTE]
>如果您沒有 Cloud App Security 的訂用帳戶，您可以使用 Cloud App Security 入口網站來調查 [!INCLUDE [Product short](includes/product-short.md)] 警示，並深入瞭解使用者及其內部部署的受控活動，但與您的雲端應用程式相關的見解仍無法使用。

## <a name="filter-product-short-activities-in-cloud-app-security"></a>[!INCLUDE [Product short](includes/product-short.md)]Cloud App Security 中的篩選活動

[!INCLUDE [Product short](includes/product-short.md)]您可以透過選取 [**活動記錄**] 子功能表，或從 [**警示**] 功能表依狀態、類別、嚴重性、應用程式、使用者名稱或原則，從主要 Cloud App Security **調查**] 功能表存取活動。

若要 [!INCLUDE [Product short](includes/product-short.md)] 依使用者存取活動：

1. 使用 [使用者名稱] 欄位來篩選 [警示]  佇列。
    ![依使用者名稱篩選警示](media/mcas-alerts-queue.png)
1. 在結果清單中，按一下任意警示上的使用者名稱，以開啟您想要調查之使用者的 [使用者]  頁面。

1. 使用可用欄位來篩選使用者的活動，或使用 [+] 按鈕來加入新的篩選規則。
    ![篩選使用者的活動](media/mcas-activity-filter.png)

## <a name="create-activity-policies-in-cloud-app-security"></a>在 Cloud App Security 中建立活動原則

篩選活動並識別組織內您想要實作或不符合規範的活動原則之後，使用 [篩選] 功能表的 [建立新的活動原則]  選項，立即為每個使用者、裝置或租用戶建立新的自訂原則。

建立新的活動原則：

1. 從任何 [活動記錄]  頁面中，套用篩選 (例如應用程式、使用者名稱、活動類型) 等。
    - 若要從 [!INCLUDE [Product short](includes/product-short.md)] [應用程式篩選器] 中選取 [ **Active Directory** ] 選項來篩選活動。
    ![建立新的活動原則](media/mcas-create-new-policy.png)
1. 按一下 [從搜尋新增原則]  按鈕。
1. 新增 **原則名稱**。
    ![建立新的活動原則 - 步驟 2](media/mcas-create-policy.png)
1. 新增原則 **描述**。
1. 指派原則的 [嚴重性]  。
1. 選取原則的 [類別]  。
1. 選擇或修改要針對原則建立並指派的篩選。
1. 精簡或新增更多篩選。
1. 儲存並套用新的原則。

## <a name="next-steps"></a>後續步驟

深入了解調查優先順序評分及 [Microsoft Cloud App Security](/cloud-app-security/) \(部分機器翻譯\) 功能的其他功能。

## <a name="join-the-community"></a>加入社群

是否有更多問題或想與其他人討論[!INCLUDE [Product short](includes/product-short.md)] 與相關的安全性？ 立即加入[[!INCLUDE [Product short](includes/product-short.md)] 社群](https://techcommunity.microsoft.com/t5/Azure-Advanced-Threat-Protection/bd-p/AzureAdvancedThreatProtection) \(英文\)！