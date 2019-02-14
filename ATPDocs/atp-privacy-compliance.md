---
title: Azure 進階威脅防護個人資料原則 | Microsoft Docs
description: 提供如何從 Azure ATP 刪除私人資訊和個人資料的相關資訊連結。
keywords: ''
author: mlottner
ms.author: mlottner
manager: barbkess
ms.date: 10/04/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 224e629a-0e82-458c-bb03-b67070a9241d
ms.reviewer: ophirp
ms.suite: ems
ms.openlocfilehash: cc6085158366e94be8c9572d2aedff37db9c5769
ms.sourcegitcommit: 78748bfd75ae68230d72ad11010ead37d96b0c58
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/12/2019
ms.locfileid: "56076958"
---
# <a name="azure-atp-data-security-and-privacy"></a>Azure ATP 資料安全性和隱私權

[!INCLUDE [Handle personal data](../includes/gdpr-intro-sentence.md)]

## <a name="search-for-and-identify-personal-data"></a>搜尋和識別個人資料 

在 Azure 進階威脅防護中，您可以使用[搜尋列](workspace-portal.md#search-bar)，透過 [Azure ATP 入口網站](workspace-portal.md)檢視可識別的個人資料。 

您可以搜尋特定使用者或電腦，然後按一下實體以顯示使用者或電腦的[設定檔頁面](entity-profiles.md)。 設定檔提供您來自 Active Directory 實體的完整詳細資料，包括與該實體相關的網路活動與其歷史記錄。

Azure ATP 個人資料是透過 Azure ATP 感應器從 Active Directory 收集的，並且會儲存在後端資料庫中。

## <a name="update-personal-data"></a>更新個人資料 

Azure ATP 的個人使用者資料是從組織 Active Directory 中的使用者物件所衍生。 因此，對組織 AD 中使用者設定檔所做的變更會反映在 Azure ATP 中。


## <a name="delete-personal-data"></a>刪除個人資料 

從組織的 Active Directory 刪除使用者之後，Azure ATP 會自動刪除使用者設定檔和一年當中任何相關的網路活動。 您也可以[刪除](working-with-suspicious-activities.md#review-suspicious-activities-on-the-attack-time-line)包含個人資料的任何安全性警示。 

## <a name="export-personal-data"></a>匯出個人資料 

在 Azure ATP 中，您可以將安全性警示資訊[匯出](working-with-suspicious-activities.md#review-suspicious-activities-on-the-attack-time-line)到 Excel。 此功能也會匯出個人資料。 
 
## <a name="audit-personal-data"></a>稽核個人資料

Azure ATP 有實作個人資料變更的稽核，包括個人資料的刪除和匯出。 稽核記錄的保留時間為 90 天。 Azure ATP 中的稽核是後端功能，客戶無法存取。
 
## <a name="additional-resources"></a>其他資源

- 如需 Azure ATP 信任與合規性的相關資訊，請參閱[服務信任入口網站](https://servicetrust.microsoft.com/ViewPage/GDPRGetStarted) \(英文\) 與 [Microsoft 365 企業版 GDPR 合規性網站](https://docs.microsoft.com/microsoft-365/compliance/compliance-solutions-overview)。
