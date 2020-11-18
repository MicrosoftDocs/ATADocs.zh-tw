---
title: Microsoft Cloud App Security 中的 Microsoft Defender 身分識別
description: Microsoft Cloud App Security 中的身分識別功能的 Microsoft Defender 總覽。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 01/05/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 70a316deaafec0c251c91defbc47ec5281eba617
ms.sourcegitcommit: e2227c0b0e5aaa5163dc56d4131ca82f8dca8fb0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2020
ms.locfileid: "94848868"
---
# <a name="using-product-long-with-microsoft-cloud-app-security"></a>使用 [!INCLUDE [Product long](includes/product-long.md)] with Microsoft Cloud App Security

本文旨在協助您瞭解並在搭配使用 Microsoft Cloud App Security 入口網站時，流覽增強的調查體驗 [!INCLUDE [Product long](includes/product-long.md)] 。

運用現有的內部部署偵測和異常行為分析， [!INCLUDE [Product short](includes/product-short.md)] 使用 Microsoft Cloud App Security 入口網站進行存取，可讓您在整個企業中偵測及警示機密資料遭到外泄，以及篩選活動並建立可採取動作的原則。 這個混合式供應項目會根據使用者與實體行為分析 (UEBA) 來分析活動和警示以判斷具風險的行為，並提供調查優先順序分數來簡化對於遭入侵之身分識別的事件回應。

在本文中，您將了解：

> [!div class="checklist"]
>
> - 服務概觀
> - 新的存取方式 [!INCLUDE [Product short](includes/product-short.md)]
> - 授權必要條件
> - [!INCLUDE [Product short](includes/product-short.md)]在 Cloud App Security 中尋找追蹤活動的位置

## <a name="service-overview"></a>服務概觀

與整合之後 [!INCLUDE [Product short](includes/product-short.md)] ，Cloud App Security 入口網站提供下列警示和見解：

- Microsoft Cloud App Security (識別雲端工作階段中的攻擊) 不僅涵蓋 Microsoft 產品，還包括協力廠商應用程式
- [!INCLUDE [Product long](includes/product-long.md)]，其使用機器學習和行為分析來識別內部部署網路之間的攻擊
- Azure Active Directory Identity Protection 會偵測和主動防止使用者與雲端中身分識別的登入風險

## <a name="access-product-short"></a>訪問 [!INCLUDE [Product short](includes/product-short.md)]

選擇繼續在 [!INCLUDE [Product short](includes/product-short.md)] 入口網站中使用 [!INCLUDE [Product short](includes/product-short.md)] ，或者，您可以 [!INCLUDE [Product short](includes/product-short.md)] 使用 Microsoft Cloud App Security 入口網站來存取警示和身分識別評分。 在任一工作流程中， [!INCLUDE [Product short](includes/product-short.md)] 設定和設定工作會繼續在 [!INCLUDE [Product short](includes/product-short.md)] 入口網站中處理。

## <a name="prerequisites"></a>必要條件

如需跨混合式環境的完整使用者調查功能，您必須具備：

- Microsoft Cloud App Security 的有效授權
- [!INCLUDE [Product long](includes/product-long.md)]連接到您的 Active Directory 實例的有效授權

>[!NOTE]
>
> - 如果您沒有 Cloud App Security 的訂用帳戶，您仍然能夠使用 Cloud App Security 入口網站來調查 [!INCLUDE [Product short](includes/product-short.md)] 警示，並深入瞭解使用者及其內部部署的受控活動，但您不會收到來自雲端應用程式的相關深入解析。
> - [!INCLUDE [Product short](includes/product-short.md)] 系統管理員可能需要新的許可權才能存取 Cloud App Security。 若要了解如何指派 Cloud App Security 的授權，請參閱[管理管理員存取權](/cloud-app-security/manage-admins) \(部分機器翻譯\)。

請參閱[ [!INCLUDE [Product short](includes/product-short.md)] 整合](/cloud-app-security/mdi-integration)，以瞭解如何 [!INCLUDE [Product short](includes/product-short.md)] 在 Cloud App Security 中快速啟用。

## <a name="product-short-in-cloud-app-security"></a>[!INCLUDE [Product short](includes/product-short.md)] 在 Cloud App Security

請參閱 [Cloud App Security 快速入門](/cloud-app-security/getting-started-with-cloud-app-security)以熟悉使用 Cloud App Security 入口網站的基本概念。

存取 [!INCLUDE [Product short](includes/product-short.md)] Cloud App Security 警示、活動和使用者頁面內的資料和新的混合式功能。

## <a name="alerts"></a>警示

[!INCLUDE [Product short](includes/product-short.md)] 警示會顯示在 Cloud App Security **警示** 佇列內。 只有在使用 Cloud App Security 檢視警示時，才能使用其他警示篩選選項。 [!INCLUDE [Product short](includes/product-short.md)] 警示會使用應用程式篩選器進行篩選以 **Active Directory**。

## <a name="alert-management"></a>警示管理

搭配 [!INCLUDE [Product short](includes/product-short.md)] Cloud app security 使用時，在某個服務中關閉警示將不會在其他服務中自動關閉警示。 決定在何處管理和補救警示，以避免執行重複的作業。

## <a name="siem-notification"></a>SIEM 通知

如果您的服務 ([!INCLUDE [Product short](includes/product-short.md)] 和 Cloud App Security) 目前設定為傳送警示通知至 SIEM，在啟用 [!INCLUDE [Product short](includes/product-short.md)] Cloud App Security 中的整合之後，您就會開始收到相同警示的重複 SIEM 通知。 每個服務都會發出一個警示，且每個警示會有不同的警示識別碼。 若要避免重複和混淆，請決定您想要執行警示管理的位置，然後停止從其他服務傳送 SIEM 通知。

## <a name="activities"></a>活動

[!INCLUDE [Product short](includes/product-short.md)] 警示會顯示在 Cloud App Security **活動記錄** 檔中。 只有在使用 Cloud App Security 檢視警示時，才能使用其他活動篩選選項和功能。 請參閱[ [!INCLUDE [Product short](includes/product-short.md)] 使用 Microsoft Cloud App Security 的活動](activities-filtering-mcas.md)，以瞭解如何篩選和建立新的活動原則。

## <a name="user-pages"></a>使用者頁面

使用者頁面包含每位使用者的[調查優先順序分數](/cloud-app-security/tutorial-ueba)與所有動作的活動記錄。

存取系統使用者的使用者頁面：

1. 從主功能表中開啟 [警示]。
1. 使用 [使用者名稱] 欄位來選取和篩選特定使用者的警示佇列。

 或

1. 從 [調查] 功能表中，選取 [活動記錄]。
1. 依使用者篩選 [活動記錄] 佇列。

    ![活動記錄檔](media/mcas-activity-filter.png)

## <a name="next-steps"></a>後續步驟

請參閱[ [!INCLUDE [Product short](includes/product-short.md)] 使用 Microsoft Cloud App Security 的活動](activities-filtering-mcas.md)，以瞭解如何篩選和建立新的活動原則。

## <a name="join-the-community"></a>加入社群

是否有更多問題或想與其他人討論[!INCLUDE [Product short](includes/product-short.md)] 與相關的安全性？ 立即加入[[!INCLUDE [Product short](includes/product-short.md)] 社群](https://techcommunity.microsoft.com/t5/Azure-Advanced-Threat-Protection/bd-p/AzureAdvancedThreatProtection) \(英文\)！
