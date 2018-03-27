---
title: 使用 ATA 調查橫向移動路徑攻擊 | Microsoft Docs
description: 本文說明如何使用 Advanced Threat Analytics (ATA) 偵測橫向移動路徑攻擊。
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: article
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: 710f01bd-c878-4406-a7b2-ce13f98736ea
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: dc03cfe1719541dac0f8509c0f8f22987ecb96bb
ms.sourcegitcommit: 49c3e41714a5a46ff2607cbced50a31ec90fc90c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/22/2018
---
*適用於：Advanced Threat Analytics 1.9 版*

# <a name="investigating-lateral-movement-paths-with-ata"></a>使用 ATA 調查橫向移動路徑

即便您盡了全力保護敏感性使用者，且管理員也設定了複雜的密碼並經常變更、強化了電腦，而資料也存放在安全的位置，但攻擊者仍可使用橫向移動路徑來存取敏感性帳戶。 在橫向移動攻擊中，當敏感性使用者登入非敏感性使用者具有本機權限的電腦時，攻擊者會利用執行個體。 攻擊者隨後便可進行橫向移動，存取較不敏感的使用者，然後越過電腦來取得敏感性使用者的認證。 

## <a name="what-is-a-lateral-movement-path"></a>橫向移動路徑是什麼？

橫向移動是攻擊者主動使用非敏感性帳戶來取得敏感性帳戶存取權的方式。 他們可以使用[可疑活動指南](suspicious-activity-guide.md)中所述的任何一種方法，來取得初步的非敏感性密碼，然後使用如 Bloodhound 等工具來了解您網路中的系統管理員身分，以及該系統管理員所能存取的電腦。 攻擊者隨後便可存取網域控制站上的資料，來了解帳戶擁有者的身分，以及其可存取的資源與檔案，並能從其已存取的電腦上竊取其他使用者 (有時還是敏感性使用者) 儲存的認證，然後在使用者與資源間進行橫向移動，直到攻擊者取得您網路的系統管理權限為止。 

ATA 可讓您在網路上採取防範動作，以防止攻擊者成功進行橫向移動。

## <a name="discovery-your-at-risk-sensitive-accounts"></a>探索具有風險的敏感性帳戶

若要探索網路中有哪些敏感性帳戶因和非敏感性的帳戶或資源之間具有連線而處於易受攻擊的狀態，請遵循這些步驟。 為了保護網路不受橫向移動攻擊的危害，ATA 會從末端反向運作，這代表 ATA 會提供您一幅以特殊權限帳戶為起點的地圖，然後為您顯示處於這些使用者及其認證的橫向路徑有哪些使用者及裝置。

1. 在 ATA 主控台功能表中，按一下報表圖示 ![[報表] 圖示](./media/ata-report-icon.png)。

2. 在 [針對敏感性帳戶的橫向移動路徑] 底下，若找不到橫向移動路徑，報表將會呈現灰色。若有橫向移動路徑，則報表的日期將會自動選取為具有相關資料的第一個日期。 

 ![報告](./media/reports.png)

3. 按一下 [下載]。

3. 所建立的 Excel 檔案能為您提供處於風險之敏感性帳戶的詳細資料。 [摘要] 索引標籤能提供詳述敏感性帳戶及電腦的數目，以及處於風險資源之平均值的圖表。 [詳細資料] 索引標籤能提供您應注意之敏感性帳戶的清單。


## <a name="investigate"></a>調查

現在您已知道有哪些敏感性帳戶處於風險中，便可以深入鑽研 ATA 以了解更多資訊並採取預防性措施。

1. 在 ATA 主控台中，在 [針對敏感性帳戶的橫向移動路徑] 報表中查看帳戶被列為易受攻擊的使用者，例如 Samira Abbasi。 在實體位於橫向移動路徑![橫向圖示](./media/lateral-movement-icon.png)或![路徑圖示](./media/paths-icon.png)時，您也可以搜尋新增至實體設定檔的橫向移動徽章。

2. 在隨即開啟的使用者設定檔頁面中，按一下 [橫向移動路徑] 索引標籤。

3. 顯示的圖表能提供您針對敏感性使用者之可能路徑的地圖。 該圖表能顯示於過去兩天內所做出的連線，以提供最新的暴露程度。

4. 檢閱報表以查看並了解敏感性使用者認證的暴露程度。 例如，在此地圖中，您可跟隨 [登入者] 灰色箭頭找到 Samira Abbasi，來查看 Samira 使用其特殊權限登入的位置。 在此案例中，Samira 的敏感性認證已儲存在 REDMOND-WA-DEV 這部電腦上。 接著，查看有哪些其他使用者登入哪部電腦並產生最大程度的暴露及漏洞。 您可以查看 [身為系統管理員] 黑色箭頭，以了解誰在該資源上具有系統管理權限。 在此範例中，所有屬於 [Contoso All] 的使用者都能從該資源存取使用者認證。  

 ![使用者設定檔橫向移動路徑](media/user-profile-lateral-movement-paths.png)


## <a name="preventative-best-practices"></a>預防性最佳做法

- 預防橫向移動的最佳做法，是確保敏感性使用者只會在登入沒有任何非敏感性使用者在同一部電腦上具有管理權限的強化電腦時，才使用其系統管理員認證。 在此範例中，請確認 Samira 是否需要 REDMOND-WA-DEV 的存取權、是否使用其管理員認證以外的使用者名稱與密碼登入，或是在 REDMOND-WA-DEV 上的本機系統管理員群組移除 Contoso All 群組。

- 也建議您確保沒有人具有非必要的本機系統管理權限。 在上述範例中，您應該檢查 [Contoso All] 中的所有成員在 REDMOND-WA-DEV 上是否都需要有系統管理權限。

- 確保人員只具有必要資源的存取權，一向都是個良好的做法。 如您在上述範例中所見，Oscar Posada 會大幅提高 Samira 的暴露程度。 是否有必要在 Contoso All 中包含 Oscar Posada 呢？ 是否可以建立子群組來將暴露程度降至最低？


## <a name="see-also"></a>另請參閱
- [處理可疑活動](working-with-suspicious-activities.md)
- [查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
