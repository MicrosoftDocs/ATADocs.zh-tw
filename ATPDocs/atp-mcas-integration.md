---
title: Microsoft Cloud App Security 中的 Azure 進階威脅防護 | Microsoft Docs
description: Microsoft Cloud App Security 中的 Azure ATP 功能概觀。
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 07/01/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 5169dffc-75c4-4eb0-b997-b5359cecda97
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: b66b2f0a087bbaacc09eda54958824da693209b3
ms.sourcegitcommit: 6dd002b5a34f230aaada55a6f6178c2f9e1584d9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2019
ms.locfileid: "67506502"
---
# <a name="using-azure-atp-with-microsoft-cloud-app-security"></a>搭配 Microsoft Cloud App Security 使用 Azure ATP 


本文旨在協助您了解並瀏覽搭配 Azure ATP 使用 Microsoft Cloud App Security 入口網站時的增強調查體驗。 

利用現有的內部部署偵測與異常行為分析，使用 Microsoft Cloud App Security 入口網站存取 Azure ATP 會提供新增的功能，來偵測並警示整個企業中的機密資料外洩，以及篩選活動並建立可採取動作的原則。 這個混合式供應項目會根據使用者與實體行為分析 (UEBA) 來分析活動和警示以判斷具風險的行為，並提供調查優先順序分數來簡化對於遭入侵之身分識別的事件回應。 

在本文中，您將了解：

> [!div class="checklist"]
> * 服務概觀
> * 存取 Azure ATP 的新方法
> * 授權必要條件
> * 可在 Cloud App Security 中的何處找到 Azure ATP 追蹤的活動

## <a name="service-overview"></a>服務概觀

Cloud App Security 入口網站會與 Azure ATP 整合，以提供來自下列各項的警示與深入解析：
- Microsoft Cloud App Security (識別雲端工作階段中的攻擊) 不僅涵蓋 Microsoft 產品，還包括協力廠商應用程式
- Azure 進階威脅防護，其會使用機器學習和行為分析，來識別您整個內部部署網路上的攻擊
- Azure Active Directory Identity Protection 會偵測和主動防止使用者與雲端中身分識別的登入風險

## <a name="access-azure-atp"></a>存取 Azure ATP

選擇繼續在 Azure ATP 入口網站中使用 Azure ATP，或者，您可以使用 Microsoft Cloud App Security 入口網站來存取 Azure ATP 警示與身分識別評分。 在任一個工作流程中，Azure ATP 設定和組態工作會繼續在 Azure ATP 入口網站中進行處理。 

 

## <a name="prerequisites"></a>必要條件

如需跨混合式環境的完整使用者調查功能，您必須具備：
- 適用於 Microsoft Cloud App Security 的有效授權
- 有 Azure ATP 的有效授權連線到您的 Active Directory 執行個體
 
>[!NOTE]
>如果您沒有 Cloud App Security 的訂用帳戶，您仍能使用 Cloud App Security 入口網站來調查 Azure ATP 警示，並深入了解使用者及其內部部署的受控活動，但您將不會收到來自您雲端應用程式的相關深入解析。

請參閱 [Azure ATP 整合](https://docs.microsoft.com/cloud-app-security/aatp-integration) \(部分機器翻譯\)，以了解如何快速啟用 Cloud App Security 中的 Azure ATP。  
 
## <a name="azure-atp-in-cloud-app-security"></a>Cloud App Security 中的 Azure ATP 

請參閱 [Cloud App Security 快速入門](https://docs.microsoft.com/cloud-app-security/getting-started-with-cloud-app-security)以熟悉使用 Cloud App Security 入口網站的基本概念。 

存取您的 Azure ATP 資料以及 Cloud App Security 警示、活動及使用者頁面內的新混合式功能。 

## <a name="alerts"></a>警示

Azure ATP 警示會顯示於 Cloud App Security 的 [警示]  佇列內。 只有在使用 Cloud App Security 檢視警示時，才能使用其他警示篩選選項。 針對 **Active Directory** 使用應用程式篩選來篩選 Azure ATP 警示。 

## <a name="alert-management"></a>警示管理
搭配 Cloud App Security 使用 Azure ATP 時，關閉一個服務中的警示不會自動關閉其他服務中的警示。 決定在何處管理和補救警示，以避免執行重複的作業。 

## <a name="siem-notification"></a>SIEM 通知

如果這兩個服務 (Azure ATP 與 Cloud App Security) 目前都設定為傳送警示通知到 SIEM，在啟用 Cloud App Security 中的 Azure ATP 整合之後，您將開始接收到相同警示的重複 SIEM 通知。 每個服務都會發出一個警示，且每個警示會有不同的警示識別碼。 若要避免重複和混淆，請決定您想要執行警示管理的位置，然後停止從其他服務傳送 SIEM 通知。  

## <a name="activities"></a>活動

Azure ATP 警示會顯示於 Cloud App Security 的 [活動記錄]  內。 只有在使用 Cloud App Security 檢視警示時，才能使用其他活動篩選選項和功能。 請參閱[使用 Microsoft Cloud App Security 的 Azure ATP 活動](https://docs.microsoft.com/azure-advanced-threat-protection/atp-activities-filtering-mcas)以了解如何篩選及建立新的活動原則。  

## <a name="user-pages"></a>使用者頁面 

使用者頁面包含每位使用者的[調查優先順序分數](https://docs.microsoft.com/cloud-app-security/tutorial-ueba)與所有動作的活動記錄。 

存取系統使用者的使用者頁面：
1. 從主功能表中開啟 [警示]  。
1. 使用 [使用者名稱]  欄位來選取和篩選特定使用者的警示佇列。

 或

1. 從 [調查]  功能表中，選取 [活動記錄]  。 
1. 依使用者篩選 [活動記錄] 佇列。 

    ![活動記錄](media/atp-mcas-activity-filter.png)

## <a name="next-steps"></a>後續步驟

請參閱[使用 Microsoft Cloud App Security 的 Azure ATP 活動](https://docs.microsoft.com/azure-advanced-threat-protection/atp-activities-filtering-mcas)以了解如何篩選及建立新的活動原則。 
  
## <a name="join-the-community"></a>加入社群

是否有更多問題，或是想與其他人討論 Azure ATP 及相關的安全性？ 現在就加入 [Azure ATP 社群](https://techcommunity.microsoft.com/t5/Azure-Advanced-Threat-Protection/bd-p/AzureAdvancedThreatProtection)！




