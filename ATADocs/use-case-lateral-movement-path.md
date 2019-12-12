---
title: 使用 ATA 調查橫向移動路徑攻擊 |Microsoft Docs
description: 本文說明如何使用 Advanced Threat Analytics (ATA) 偵測橫向移動路徑攻擊。
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 06/14/2019
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 710f01bd-c878-4406-a7b2-ce13f98736ea
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 2f020838d182b99b1f5f42455330b2b0ce5aa88f
ms.sourcegitcommit: 6dd002b5a34f230aaada55a6f6178c2f9e1584d9
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2019
ms.locfileid: "66500649"
---
# <a name="investigate-lateral-movement-paths-with-ata"></a>使用 ATA 調查橫向移動路徑


*適用於：Advanced Threat Analytics 1.9 版*

即便您盡了全力保護敏感性使用者，且管理員也設定了複雜的密碼並經常變更、強化了電腦，而資料也存放在安全的位置，但攻擊者仍可使用橫向移動路徑來存取敏感性帳戶。 在橫向移動攻擊中，攻擊者會利用實例，而敏感性使用者必須登入非敏感性使用者具有本機許可權的電腦。 攻擊者隨後便可進行橫向移動，存取較不敏感的使用者，然後越過電腦來取得敏感性使用者的認證。 

## <a name="what-is-a-lateral-movement-path"></a>橫向移動路徑是什麼？

橫向移動是攻擊者使用非敏感性帳戶來取得敏感性帳戶存取權的方式。 此攻擊可利用[可疑活動指南](suspicious-activity-guide.md)中描述的方法達成。 攻擊者會使用橫向移動來識別網路中的系統管理員，並瞭解他們可以存取的機器。 有了這項資訊並進一步移動之後，攻擊者就可以利用網域控制站上的資料。 

ATA 可讓您在網路上採取防範動作，以防止攻擊者成功進行橫向移動。

## <a name="discovery-your-at-risk-sensitive-accounts"></a>探索具有風險的敏感性帳戶

若要探索網路中有哪些敏感性帳戶因其與非敏感性帳戶或資源的連線而受到影響，請在特定時間範圍內執行下列步驟： 

1. 在 ATA 主控台功能表中，按一下報表圖示 ![[報表] 圖示](./media/ata-report-icon.png).

2. 在 [**對敏感性帳戶的橫向移動路徑**] 下，如果找不到橫向移動路徑，報表就會呈現灰色。如果有橫向移動路徑，則報表的日期會自動選取具有相關資料的第一個日期。 

   ![報告](./media/reports.png)

3. 按一下 [下載]。

4. 所建立的 Excel 檔案會提供您有風險之敏感性帳戶的詳細資料。 [摘要] 索引標籤能提供詳述敏感性帳戶及電腦的數目，以及處於風險資源之平均值的圖表。 [詳細資料] 索引標籤能提供您應注意之敏感性帳戶的清單。 請注意，路徑是先前存在的路徑，目前可能不可用。


## <a name="investigate"></a>調查

現在您已知道有哪些敏感性帳戶處於風險中，便可以深入鑽研 ATA 以了解更多資訊並採取預防性措施。

1. 若實體位於橫向移動路徑，請在 ATA 主控台中，搜尋新增至實體設定檔的橫向移動徽章 ![橫向圖示](./media/lateral-movement-icon.png) 或 ![路徑圖示](./media/paths-icon.png). 這會在過去兩天內有出現橫向移動路徑的情況下提供。

2. 在隨即開啟的使用者設定檔頁面中，按一下 [橫向移動路徑] 索引標籤。

3. 顯示的圖表能提供針對敏感性使用者之可能路徑的地圖。 該圖表能顯示於過去兩天內所做出的連線。

4. 檢閱報表以查看並了解敏感性使用者認證的暴露程度。 例如，在此地圖中，您可以遵循 [**登入者**] 灰色箭號來查看 Samira 使用其特殊許可權認證登入的位置。 在此案例中，Samira 的敏感性認證已儲存在 REDMOND-WA-DEV 這部電腦上。 然後，查看哪些其他使用者已登入哪些電腦建立最大的曝光和弱點。 您可以查看 [身為系統管理員] 黑色箭頭，以了解誰在該資源上具有系統管理權限。 在此範例中，所有 [Contoso All] 群組中的使用者都能從該資源存取使用者認證。  

   ![使用者設定檔橫向移動路徑](media/user-profile-lateral-movement-paths.png)


## <a name="preventative-best-practices"></a>預防性最佳做法

- 防止橫向移動的最佳方式，是確保敏感性使用者只在登入強化的電腦時才使用其系統管理員認證，而在同一部電腦上沒有任何具有管理員許可權的非敏感性使用者。 在此範例中，請確定如果 Samira 需要存取 REDMOND-WA-DEV，他們會使用其系統管理員認證以外的使用者名稱和密碼來登入，或從 REDMOND-WA-DEV 的本機 administrators 群組中移除 Contoso All 群組。

- 也建議您確保沒有人具有非必要的本機系統管理權限。 在此範例中，檢查 Contoso 中的所有人是否都真的需要 REDMOND-WA-DEV 的系統管理許可權。

- 確保人員只擁有必要資源的存取權。 在上述範例中，Oscar Posada 會大幅提高 Samira 的暴露程度。 是否需要將它們包含在 [ **Contoso All**] 群組中？ 是否可以建立子群組來將暴露程度降至最低？

> [!TIP]
> 如果在過去兩天內未偵測到活動，則圖表不會出現，但橫向移動路徑報表仍然可以提供過去60天橫向移動路徑的相關資訊。

> [!TIP]
> 如需有關如何將伺服器設定為允許 ATA 執行橫向移動路徑偵測所需之 SAM-R 作業的指示，請設定[SAM-R](install-ata-step9-samr.md)。




## <a name="see-also"></a>請參閱
- [使用可疑活動](working-with-suspicious-activities.md)
- [查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
