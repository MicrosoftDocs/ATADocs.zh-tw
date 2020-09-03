---
title: Microsoft Cloud App Security 中的 Azure 進階威脅防護活動篩選與原則
description: 使用 Microsoft Cloud App Security 進行的 Azure ATP 活動篩選和原則概觀。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 07/01/2019
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 397e5a77-2bc7-454c-9fe5-649ebaab16b3
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: fc3032c9964a4e4e887dfedf01e57649d3bf2358
ms.sourcegitcommit: 2be59f0bd4c9fd0d3827e9312ba20aa8eb43c6b5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88955967"
---
# <a name="use-activity-filters-and-create-action-policies-with-azure-atp-in-microsoft-cloud-app-security"></a>在 Microsoft Cloud App Security 中使用活動篩選以及使用 Azure ATP 建立動作原則

本文旨在協助您了解如何使用 Microsoft Cloud App Security 來篩選及建立 Azure ATP 活動的動作原則。

如需如何完成整合的詳細資訊，請參閱 [Azure ATP Cloud App Security 整合](/cloud-app-security/aatp-integration)。

搭配 Microsoft Cloud App Security 使用 Azure ATP 可根據使用者與實體行為分析 (UEBA) 來提供活動分析和警示，以識別貴企業中風險最高的行為、提供完整的調查優先順序分數，以及活動篩選和可自訂的活動原則。

## <a name="prerequisites"></a>必要條件

如需跨混合式環境的完整使用者調查功能，您必須具備：

- Microsoft Cloud App Security 的有效授權
- 有 Azure ATP 的有效授權連線到您的 Active Directory 執行個體

>[!NOTE]
>如果您沒有 Cloud App Security 的訂用帳戶，您可以使用 Cloud App Security 入口網站來調查 Azure ATP 警示，並深入了解使用者及其內部部署的受控活動，但與您的雲端應用程式相關的深入解析仍無法使用。

## <a name="filter-azure-atp-activities-in-cloud-app-security"></a>篩選 Cloud App Security 中的 Azure ATP 活動

您可以從主要的 Cloud App Security [調查]  功能表中選取 [活動記錄]  子功能表，或從 [警示]  功能表中依狀態、類別、嚴重性、應用程式、使用者名稱或原則，來存取 Azure ATP 活動。

依使用者存取 Azure ATP 活動：

1. 使用 [使用者名稱] 欄位來篩選 [警示]  佇列。
    ![依使用者名稱篩選警示](media/atp-mcas-alerts-queue.png)
1. 在結果清單中，按一下任意警示上的使用者名稱，以開啟您想要調查之使用者的 [使用者]  頁面。

1. 使用可用欄位來篩選使用者的活動，或使用 [+] 按鈕來加入新的篩選規則。
    ![篩選使用者的活動](media/atp-mcas-activity-filter.png)

## <a name="create-activity-policies-in-cloud-app-security"></a>在 Cloud App Security 中建立活動原則

篩選活動並識別組織內您想要實作或不符合規範的活動原則之後，使用 [篩選] 功能表的 [建立新的活動原則]  選項，立即為每個使用者、裝置或租用戶建立新的自訂原則。

建立新的活動原則：

1. 從任何 [活動記錄]  頁面中，套用篩選 (例如應用程式、使用者名稱、活動類型) 等。
    - 若要針對 Azure ATP 中的活動進行篩選，請在 [應用程式] 篩選中選取 [Active Directory]  選項。
    ![建立新的活動原則](media/atp-mcas-create-new-policy.png)
1. 按一下 [從搜尋新增原則]  按鈕。
1. 新增**原則名稱**。
    ![建立新的活動原則 - 步驟 2](media/atp-mcas-create-policy.png)
1. 新增原則**描述**。
1. 指派原則的 [嚴重性]  。
1. 選取原則的 [類別]  。
1. 選擇或修改要針對原則建立並指派的篩選。
1. 精簡或新增更多篩選。
1. 儲存並套用新的原則。

## <a name="next-steps"></a>後續步驟

深入了解調查優先順序評分及 [Microsoft Cloud App Security](/cloud-app-security/) \(部分機器翻譯\) 功能的其他功能。

## <a name="join-the-community"></a>加入社群

是否有更多問題，或是想與其他人討論 Azure ATP 及相關的安全性？ 現在就加入 [Azure ATP 社群](https://techcommunity.microsoft.com/t5/Azure-Advanced-Threat-Protection/bd-p/AzureAdvancedThreatProtection)！