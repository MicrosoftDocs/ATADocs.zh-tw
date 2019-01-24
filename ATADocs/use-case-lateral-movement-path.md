---
title: 使用 ATA 調查橫向移動路徑攻擊 | Microsoft Docs
description: 本文說明如何使用 Advanced Threat Analytics (ATA) 偵測橫向移動路徑攻擊。
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 6/14/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: 710f01bd-c878-4406-a7b2-ce13f98736ea
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: b6aaaf1a93fe635f4e159f88e7d55a110bcef0d2
ms.sourcegitcommit: f37127601166216e57e56611f85dd783c291114c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/24/2019
ms.locfileid: "54840483"
---
# <a name="investigating-lateral-movement-paths-with-ata"></a>使用 ATA 調查橫向移動路徑


適用對象：*Advanced Threat Analytics 1.9 版*

即便您盡了全力保護敏感性使用者，且管理員也設定了複雜的密碼並經常變更、強化了電腦，而資料也存放在安全的位置，但攻擊者仍可使用橫向移動路徑來存取敏感性帳戶。 在橫向移動攻擊中，當敏感性使用者登入非敏感性使用者具有本機權限的電腦時，攻擊者會利用執行個體。 攻擊者隨後便可進行橫向移動，存取較不敏感的使用者，然後越過電腦來取得敏感性使用者的認證。 

## <a name="what-is-a-lateral-movement-path"></a>橫向移動路徑是什麼？

橫向移動是攻擊者使用非敏感性帳戶來取得敏感性帳戶存取權的方式。 此攻擊可使用[可疑活動指南](suspicious-activity-guide.md)中描述的方法達成。 了解您網路中系統管理員是誰和攻擊者可以存取的機器，攻擊者就可以利用網域控制器上的資料。 

ATA 可讓您在網路上採取防範動作，以防止攻擊者成功進行橫向移動。

## <a name="discovery-your-at-risk-sensitive-accounts"></a>探索具有風險的敏感性帳戶

若要在特定時間範圍內，探索網路中有哪些敏感性帳戶因為和非敏感性的帳戶或資源之間具有連線，而處於易受攻擊的狀態，請遵循這些步驟。 

1. 在 ATA 主控台功能表中，按一下報表圖示 ![[報表] 圖示](./media/ata-report-icon.png)。

2. 在 [針對敏感性帳戶的橫向移動路徑] 底下，若找不到橫向移動路徑，報表將會呈現灰色。若有橫向移動路徑，則報表的日期將會自動選取為具有相關資料的第一個日期。 

   ![報告](./media/reports.png)

3. 按一下 [下載]。

4. 所建立的 Excel 檔案能為您提供處於風險之敏感性帳戶的詳細資料。 [摘要] 索引標籤能提供詳述敏感性帳戶及電腦的數目，以及處於風險資源之平均值的圖表。 [詳細資料] 索引標籤能提供您應注意之敏感性帳戶的清單。 請注意，路徑是先前存在的路徑，目前可能不可用。


## <a name="investigate"></a>調查

現在您已知道有哪些敏感性帳戶處於風險中，便可以深入鑽研 ATA 以了解更多資訊並採取預防性措施。

1. 若實體位於橫向移動路徑，請在 ATA 主控台中，搜尋新增至實體設定檔的橫向移動徽章 ![橫向圖示](./media/lateral-movement-icon.png) 或 ![路徑圖示](./media/paths-icon.png)。 這會在過去兩天內有出現橫向移動路徑的情況下提供。

2. 在隨即開啟的使用者設定檔頁面中，按一下 [橫向移動路徑] 索引標籤。

3. 顯示的圖表能提供針對敏感性使用者之可能路徑的地圖。 該圖表能顯示於過去兩天內所做出的連線。

4. 檢閱報表以查看並了解敏感性使用者認證的暴露程度。 例如，在此地圖中，您可以遵循 [登入者] 灰色箭頭來查看 Samira 使用其特殊權限認證登入的位置。 在此案例中，Samira 的敏感性認證已儲存在 REDMOND-WA-DEV 這部電腦上。 接著，查看有哪些其他使用者登入哪部電腦並產生最大程度的暴露及漏洞。 您可以查看 [身為系統管理員] 黑色箭頭，以了解誰在該資源上具有系統管理權限。 在此範例中，所有 [Contoso All] 群組中的使用者都能從該資源存取使用者認證。  

   ![使用者設定檔橫向移動路徑](media/user-profile-lateral-movement-paths.png)


## <a name="preventative-best-practices"></a>預防性最佳做法

- 預防橫向移動的最佳做法，是確保敏感性使用者只會在登入沒有任何非敏感性使用者在同一部電腦上具有管理權限的強化電腦時，才使用其系統管理員認證。 在此範例中，請確認 Samira 是否需要 REDMOND-WA-DEV 的存取權、是否使用其管理員認證以外的使用者名稱與密碼登入，或是在 REDMOND-WA-DEV 上的本機系統管理員群組移除 Contoso All 群組。

- 也建議您確保沒有人具有非必要的本機系統管理權限。 在上述範例中，您應該檢查 [Contoso All] 中的所有成員在 REDMOND-WA-DEV 上是否都需要有系統管理權限。

- 確保人員只擁有必要資源的存取權。 在上述範例中，Oscar Posada 會大幅提高 Samira 的暴露程度。 是否有必要將其包含在 [Contoso All] 群組中？ 是否可以建立子群組來將暴露程度降至最低？

**提示** - 若在過去兩天內都沒有偵測到活動，該圖表便不會出現，不過系統仍然會提供橫向移動路徑報表，以提供您過去 60 天的橫向移動路徑相關資訊。

**提示** - 如需設定伺服器以允許 ATA 執行橫向移動路徑偵測所需之 SAM-R 作業的指示，請參閱[設定 SAM-R](install-ata-step9-samr.md)。




## <a name="see-also"></a>另請參閱
- [處理可疑活動](working-with-suspicious-activities.md)
- [查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
