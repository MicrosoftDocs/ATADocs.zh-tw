---
title: 調查使用 ATA 的橫向移動路徑攻擊 |Microsoft Docs
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
ms.sourcegitcommit: 37b572e0e9e4bb874c7965f66de0ee8b6fbe5416
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/04/2019
ms.locfileid: "66500649"
---
# <a name="investigate-lateral-movement-paths-with-ata"></a>調查使用 ATA 的橫向移動路徑


*適用於：Advanced Threat Analytics 1.9 版*

即便您盡了全力保護敏感性使用者，且管理員也設定了複雜的密碼並經常變更、強化了電腦，而資料也存放在安全的位置，但攻擊者仍可使用橫向移動路徑來存取敏感性帳戶。 在橫向移動攻擊中，攻擊者會利用執行個體當敏感性使用者登入電腦時，非敏感性使用者具有本機權限。 攻擊者隨後便可進行橫向移動，存取較不敏感的使用者，然後越過電腦來取得敏感性使用者的認證。 

## <a name="what-is-a-lateral-movement-path"></a>橫向移動路徑是什麼？

橫向移動是攻擊者使用非敏感性帳戶來取得敏感性帳戶存取權的方式。 此攻擊可利用[可疑活動指南](suspicious-activity-guide.md)中描述的方法達成。 攻擊者會使用橫向移動，找出您的網路中的系統管理員，並了解他們可以存取哪些機器。 使用此資訊，以及進一步的移動，攻擊者可以利用資料的網域控制站上。 

ATA 可讓您在網路上採取防範動作，以防止攻擊者成功進行橫向移動。

## <a name="discovery-your-at-risk-sensitive-accounts"></a>探索具有風險的敏感性帳戶

若要探索您網路中的敏感性帳戶受到其連線到非敏感性帳戶或資源，在特定時間範圍內，請遵循下列步驟： 

1. 在 ATA 主控台功能表中，按一下報表圖示 ![[報表] 圖示](./media/ata-report-icon.png).

2. 在 [針對敏感性帳戶的橫向移動路徑]  底下，若找不到橫向移動路徑，報表將會呈現灰色。若有橫向移動路徑，則報表的日期將會自動選取為具有相關資料的第一個日期。 

   ![報告](./media/reports.png)

3. 按一下 **下載**。

4. Excel 檔案建立為您提供有關您面臨風險的敏感性帳戶的詳細資料。 [摘要]  索引標籤能提供詳述敏感性帳戶及電腦的數目，以及處於風險資源之平均值的圖表。 [詳細資料]  索引標籤能提供您應注意之敏感性帳戶的清單。 請注意，路徑是先前存在的路徑，目前可能不可用。


## <a name="investigate"></a>調查

現在您已知道有哪些敏感性帳戶處於風險中，便可以深入鑽研 ATA 以了解更多資訊並採取預防性措施。

1. 若實體位於橫向移動路徑，請在 ATA 主控台中，搜尋新增至實體設定檔的橫向移動徽章 ![橫向圖示](./media/lateral-movement-icon.png) 或 ![路徑圖示](./media/paths-icon.png). 這會在過去兩天內有出現橫向移動路徑的情況下提供。

2. 在隨即開啟的使用者設定檔頁面中，按一下 [橫向移動路徑]  索引標籤。

3. 顯示的圖表能提供針對敏感性使用者之可能路徑的地圖。 該圖表能顯示於過去兩天內所做出的連線。

4. 檢閱報表以查看並了解敏感性使用者認證的暴露程度。 例如，在此圖中，您可以依照**登入者**灰色箭頭來查看 Samira 使用其特殊權限的認證已簽署的位置。 在此案例中，Samira 的敏感性認證已儲存在 REDMOND-WA-DEV 這部電腦上。 然後，查看其他使用者登入到最大的風險和弱點可能會建立哪些電腦。 您可以查看 [身為系統管理員]  黑色箭頭，以了解誰在該資源上具有系統管理權限。 在此範例中，所有 [Contoso All]  群組中的使用者都能從該資源存取使用者認證。  

   ![使用者設定檔橫向移動路徑](media/user-profile-lateral-movement-paths.png)


## <a name="preventative-best-practices"></a>預防性最佳做法

- 預防橫向移動的最佳方式是確保敏感性使用者使用其系統管理員認證，僅當他們登入強化電腦沒有任何非敏感性使用者可在相同電腦上的系統管理員權限的人員。 在範例中，可確保當 Samira 需要 REDMOND-WA-開發人員，他們使用的使用者名稱和密碼不是其系統管理員認證，登入存取，或從 REDMOND-WA-DEV 上的本機 administrators 群組移除 Contoso All 群組。

- 也建議您確保沒有人具有非必要的本機系統管理權限。 在範例中，檢查看看 Contoso All 中的所有人真的需要 REDMOND-WA-DEV 上的系統管理員權限

- 確保人員只擁有必要資源的存取權。 在上述範例中，Oscar Posada 會大幅提高 Samira 的暴露程度。 一定會包含在群組**Contoso All**嗎？ 是否可以建立子群組來將暴露程度降至最低？

> [!TIP]
> 如果在過去兩天內沒有偵測到活動，圖形不會出現，但橫向移動路徑報表仍可提供過去 60 天的橫向移動路徑相關資訊。

> [!TIP]
> 如需如何設定您的伺服器以允許執行 SAM R 作業所需的橫向移動路徑偵測，ATA 中的指示[設定 SAM-R](install-ata-step9-samr.md)。




## <a name="see-also"></a>另請參閱
- [處理可疑活動](working-with-suspicious-activities.md)
- [查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
