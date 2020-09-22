---
title: Azure 進階威脅防護個人資料原則
description: 提供如何從 Azure ATP 刪除私人資訊和個人資料的相關資訊連結。
keywords: ''
author: shsagir
ms.author: shsagir
manager: rkarlin
ms.date: 06/21/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 224e629a-0e82-458c-bb03-b67070a9241d
ms.reviewer: ophirp
ms.suite: ems
ms.openlocfilehash: 8cfd442e05827811c929f5d6e89ab03dad8a3367
ms.sourcegitcommit: c7c0a4c9f7507f3e8e0f219798ed7d347c03e792
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/22/2020
ms.locfileid: "90912394"
---
# <a name="azure-atp-data-security-and-privacy"></a>Azure ATP 資料安全性和隱私權

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

[!INCLUDE [Handle personal data](../includes/gdpr-intro-sentence.md)]

## <a name="search-for-and-identify-personal-data"></a>搜尋和識別個人資料

在 Azure 進階威脅防護中，您可以使用[搜尋列](workspace-portal.md#search-bar)，透過 [Azure ATP 入口網站](workspace-portal.md)檢視可識別的個人資料。

您可以搜尋特定使用者或電腦，然後按一下實體以顯示使用者或電腦的[設定檔頁面](entity-profiles.md)。 設定檔提供您來自 Active Directory 實體的完整詳細資料，包括與該實體相關的網路活動與其歷史記錄。

Azure ATP 個人資料是透過 Azure ATP 感應器從 Active Directory 收集的，並且會儲存在後端資料庫中。

## <a name="update-personal-data"></a>更新個人資料

Azure ATP 個人使用者資料是擷取自組織 Active Directory 中的使用者物件。 因此，對組織 AD 中使用者設定檔所做的變更會反映在 Azure ATP 中。


## <a name="delete-personal-data"></a>刪除個人資料

- 從組織的 Active Directory 刪除使用者之後，Azure ATP 會自動刪除使用者設定檔和一年當中任何相關的網路活動。 您也可以[刪除](working-with-suspicious-activities.md#review-suspicious-activities-on-the-attack-time-line)包含個人資料的任何安全性警示。

- 建議在 **Deleted Objects** 容器使用**唯讀**權限。 若要深入了解 Azure ATP 服務如何使用 **Deleted Objects 容器權限，請參閱 [Azure ATP prerequisites](prerequisites.md#before-you-start) (Azure ATP 必要條件) 中的 Deleted Objects 容器建議。

## <a name="export-personal-data"></a>匯出個人資料

在 Azure ATP 中，您可以將安全性警示資訊[匯出](working-with-suspicious-activities.md#review-suspicious-activities-on-the-attack-time-line)到 Excel。 此功能也會匯出個人資料。

## <a name="audit-personal-data"></a>稽核個人資料

Azure ATP 有實作個人資料變更的稽核，包括個人資料的刪除和匯出。 稽核記錄的保留時間為 90 天。 Azure ATP 中的稽核是後端功能，客戶無法存取。

## <a name="additional-resources"></a>其他資源

- 如需 Azure ATP 信任與合規性的相關資訊，請參閱[服務信任入口網站](https://servicetrust.microsoft.com/ViewPage/GDPRGetStarted) \(英文\) 與 [Microsoft 365 企業版 GDPR 合規性網站](/microsoft-365/compliance/gdpr?view=o365-worldwide&preserve-view=true)。

## <a name="security-and-privacy-for-azure-atp-us-government-gcc-high-customers"></a>Azure ATP 美國政府 GCC High 客戶的安全性及隱私權
如需 Azure ATP 合規性標準的其他資訊，以及美國政府 GCC High 客戶之客戶資料位置的其他資訊，請參閱[適用於美國政府的 Enterprise Mobility + Security 服務描述](/enterprise-mobility-security/solutions/ems-govt-service-description)。