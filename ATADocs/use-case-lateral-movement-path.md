---
title: 使用 ATA 調查橫向移動路徑攻擊
description: 本文說明如何使用 Advanced Threat Analytics (ATA) 偵測橫向移動路徑攻擊。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 06/14/2019
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 710f01bd-c878-4406-a7b2-ce13f98736ea
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: c5836b1086806b848560c0c99893d7a6fafeea1c
ms.sourcegitcommit: c7c0a4c9f7507f3e8e0f219798ed7d347c03e792
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/22/2020
ms.locfileid: "90910847"
---
# <a name="investigate-lateral-movement-paths-with-ata"></a>使用 ATA 調查橫向移動路徑

[!INCLUDE [Banner for top of topics](includes/banner.md)]

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

即便您盡了全力保護敏感性使用者，且管理員也設定了複雜的密碼並經常變更、強化了電腦，而資料也存放在安全的位置，但攻擊者仍可使用橫向移動路徑來存取敏感性帳戶。 在橫向移動攻擊中，攻擊者會在敏感性使用者登入不具敏感性使用者具有本機許可權的電腦時，利用這些實例。 攻擊者隨後便可進行橫向移動，存取較不敏感的使用者，然後越過電腦來取得敏感性使用者的認證。

## <a name="what-is-a-lateral-movement-path"></a>橫向移動路徑是什麼？

橫向移動是攻擊者使用非敏感性帳戶來取得敏感性帳戶存取權的方式。 此攻擊可利用[可疑活動指南](suspicious-activity-guide.md)中描述的方法達成。 攻擊者會使用橫向移動來識別網路中的系統管理員，並瞭解他們可以存取的電腦。 利用這項資訊及進一步的移動，攻擊者可以利用網域控制站上的資料。

ATA 可讓您在網路上採取防範動作，以防止攻擊者成功進行橫向移動。

## <a name="discovery-your-at-risk-sensitive-accounts"></a>探索具有風險的敏感性帳戶

若要探索網路中有哪些敏感性帳戶因連線到非敏感性帳戶或資源而受到影響，請在特定時間範圍內遵循下列步驟：

1. 在 ATA 主控台功能表中，按一下報表圖示 ![[報表] 圖示](media/ata-report-icon.png).

1. 如果找不到橫向移動路徑，則 **為敏感性帳戶的橫向移動路徑**，報表會呈現灰色。如果有橫向移動路徑，則報表的日期會自動選取有相關資料的第一個日期。

    ![顯示選取報表日期的螢幕擷取畫面](media/reports.png)

1. 按一下 [下載]  。

1. 所建立的 Excel 檔案可提供您敏感性帳戶有風險的詳細資料。 [摘要]**** 索引標籤能提供詳述敏感性帳戶及電腦的數目，以及處於風險資源之平均值的圖表。 [詳細資料]**** 索引標籤能提供您應注意之敏感性帳戶的清單。 請注意，路徑是先前存在的路徑，目前可能不可用。

## <a name="investigate"></a>調查

現在您已知道有哪些敏感性帳戶處於風險中，便可以深入鑽研 ATA 以了解更多資訊並採取預防性措施。

1. 若實體位於橫向移動路徑，請在 ATA 主控台中，搜尋新增至實體設定檔的橫向移動徽章 ![橫向圖示](media/lateral-movement-icon.png) 或 ![路徑圖示](media/paths-icon.png). 這會在過去兩天內有出現橫向移動路徑的情況下提供。

1. 在隨即開啟的使用者設定檔頁面中，按一下 [橫向移動路徑]  索引標籤。

1. 顯示的圖表能提供針對敏感性使用者之可能路徑的地圖。 該圖表能顯示於過去兩天內所做出的連線。

1. 檢閱報表以查看並了解敏感性使用者認證的暴露程度。 例如，在此地圖中，您可以遵循以灰色箭號 **登入** ，以查看 Samira 使用其特殊許可權認證登入的位置。 在此案例中，Samira 的敏感性認證已儲存在 REDMOND-WA-DEV 這部電腦上。 然後，查看哪些其他使用者登入了哪些電腦建立最多暴露和弱點。 您可以查看 [身為系統管理員]  黑色箭頭，以了解誰在該資源上具有系統管理權限。 在此範例中， **Contoso** 群組中的每個人都能夠從該資源存取使用者認證。

    ![使用者設定檔橫向移動路徑](media/user-profile-lateral-movement-paths.png)

## <a name="preventative-best-practices"></a>預防性最佳做法

- 預防橫向移動的最佳方式，是確保敏感性使用者只會在登入的電腦上，只有在同一部電腦上具有系統管理員許可權的非敏感性使用者登入時才會使用其系統管理員認證。 在此範例中，確定 Samira 需要存取 REDMOND-WA-開發人員，他們使用其系統管理員認證以外的使用者名稱和密碼登入，或從 REDMOND-WA-DEV 的本機系統管理員群組中移除 Contoso All 群組。

- 也建議您確保沒有人具有非必要的本機系統管理權限。 在此範例中，請查看 Contoso 中的所有人都真的需要在 REDMOND-WA-開發人員上的系統管理員許可權。

- 確保人員只擁有必要資源的存取權。 在上述範例中，Oscar Posada 會大幅提高 Samira 的暴露程度。 是否需要將它們包含在 **Contoso 全部**群組中？ 是否可以建立子群組來將暴露程度降至最低？

> [!TIP]
> 如果未在過去兩天內偵測到活動，就不會顯示圖表，但橫向移動路徑報表仍可提供過去60天的橫向移動路徑相關資訊。

> [!TIP]
> 如需有關如何設定伺服器以允許 ATA 執行橫向移動路徑偵測所需的 SAM-R 作業的指示，請設定 [SAM-r](install-ata-step9-samr.md)。

## <a name="see-also"></a>另請參閱

- [使用可疑活動](working-with-suspicious-activities.md)
- [查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
