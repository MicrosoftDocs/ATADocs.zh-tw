---
title: 適用于身分識別個人資料原則的 Microsoft Defender
description: 提供如何從 Microsoft Defender for Identity 刪除私人資訊和個人資料的相關資訊連結。
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 10/26/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: ophir
ms.suite: ems
ms.openlocfilehash: 648d12d6135e5ab09319580142807f930e595eda
ms.sourcegitcommit: 07a855b87931875bdeca14b152b13a36db79bfa8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "94846964"
---
# <a name="product-long-data-security-and-privacy"></a>[!INCLUDE [Product long](includes/product-long.md)] 資料安全性和隱私權

[!INCLUDE [Handle personal data](../includes/gdpr-intro-sentence.md)]

## <a name="search-for-and-identify-personal-data"></a>搜尋和識別個人資料

在中 [!INCLUDE [Product short](includes/product-short.md)] ，您可以使用 [[搜尋](workspace-portal.md#search-bar)] 列從[ [!INCLUDE [Product long](includes/product-long.md)] 入口網站](workspace-portal.md)中查看可識別的個人資料。

您可以搜尋特定使用者或電腦，然後按一下實體以顯示使用者或電腦的[設定檔頁面](entity-profiles.md)。 設定檔提供您來自 Active Directory 實體的完整詳細資料，包括與該實體相關的網路活動與其歷史記錄。

[!INCLUDE [Product short](includes/product-short.md)] 個人資料是從 Active Directory 透過感應器收集 [!INCLUDE [Product short](includes/product-short.md)] ，並儲存在後端資料庫中。

## <a name="update-personal-data"></a>更新個人資料

[!INCLUDE [Product short](includes/product-short.md)]的個人使用者資料是衍生自組織 Active Directory 中的使用者物件。 因此，對組織 AD 中的使用者設定檔所做的變更會反映在中 [!INCLUDE [Product short](includes/product-short.md)] 。

## <a name="delete-personal-data"></a>刪除個人資料

- 從組織的 Active Directory 中刪除使用者之後， [!INCLUDE [Product short](includes/product-short.md)] 會自動刪除一年內的使用者設定檔和任何相關的網路活動。 您也可以[刪除](working-with-suspicious-activities.md#review-suspicious-activities-on-the-attack-time-line)包含個人資料的任何安全性警示。

- 建議在 **Deleted Objects** 容器使用 **唯讀** 權限。 若要深入瞭解服務如何使用 [已刪除的物件] 容器許可權 [!INCLUDE [Product short](includes/product-short.md)] ，請參閱[ [!INCLUDE [Product short](includes/product-short.md)] 必要條件](prerequisites.md#before-you-start)中已刪除的物件容器建議。

## <a name="export-personal-data"></a>匯出個人資料

在中 [!INCLUDE [Product short](includes/product-short.md)] ，您可以將安全性警示資訊 [匯出](working-with-suspicious-activities.md#review-suspicious-activities-on-the-attack-time-line) 到 Excel。 此功能也會匯出個人資料。

## <a name="audit-personal-data"></a>稽核個人資料

[!INCLUDE [Product short](includes/product-short.md)] 實行個人資料變更的審核，包括刪除和匯出個人資料記錄。 稽核記錄的保留時間為 90 天。 中的審核 [!INCLUDE [Product short](includes/product-short.md)] 是後端功能，無法供客戶存取。

## <a name="additional-resources"></a>其他資源

- 如需 [!INCLUDE [Product short](includes/product-short.md)] 信任和合規性的相關資訊，請參閱 [服務信任入口](https://servicetrust.microsoft.com/ViewPage/GDPRGetStarted) 網站和 [Microsoft 365 企業版 GDPR 合規性網站](/microsoft-365/compliance/gdpr?view=o365-worldwide&preserve-view=true)。

## <a name="security-and-privacy-for-product-short-us-government-gcc-high-customers"></a>[!INCLUDE [Product short](includes/product-short.md)]美國政府 GCC High 客戶的安全性和隱私權

如需適用于 [!INCLUDE [Product short](includes/product-short.md)] 美國政府 GCC High 客戶之合規性標準和客戶資料位置的詳細資訊，請參閱 [美國政府服務描述的 Enterprise Mobility + Security](/enterprise-mobility-security/solutions/ems-govt-service-description)。
