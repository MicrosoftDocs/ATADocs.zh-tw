---
title: 使用 Azure ATP 調查橫向移動路徑攻擊 | Microsoft Docs
description: 本文說明如何使用 Azure 進階威脅防護 (ATP) 偵測橫向移動路徑攻擊。
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 8/05/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: de15c920-8904-4124-8bdc-03abd9f667cf
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 270b84c24ef8b52565ee97c2c15374645eb54a2c
ms.sourcegitcommit: 93a133430ac85d6db7afad5f6f2583b3a39c423a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/02/2018
ms.locfileid: "43469646"
---
適用於：Azure 進階威脅防護

# <a name="investigating-lateral-movement-paths-with-azure-atp"></a>使用 Azure ATP 調查橫向移動路徑


橫向移動是攻擊者使用非敏感性帳戶來取得敏感性帳戶存取權的方式。 此攻擊可利用[可疑活動指南](suspicious-activity-guide.md)中描述的方法達成。 橫向移動是攻擊者利用共用帳戶、群組與電腦中儲存之登入認證的非敏感性帳戶，來識別並取得您網路中敏感性帳戶和電腦存取權限的手段。 一旦攻擊者取得存取權限，攻擊者還能利用您網域控制站上的資料。


## <a name="discover-your-at-risk-sensitive-accounts"></a>探索具風險的敏感性帳戶

若要探索網路中有哪些敏感性帳戶因和非敏感性的帳戶、群組與電腦之間具有連線而處於公開的狀態，請遵循這些步驟。 

1. 在 Azure ATP 工作區入口網站功能表列中，按一下 [報表] 圖示 ![[報表] 圖示](./media/atp-report-icon.png)。

2. 在 [針對敏感性帳戶的橫向移動路徑] 底下，若找不到潛在的橫向移動路徑，報表將會呈現灰色。若有潛在的橫向移動路徑，則報表會自動預先選取有相關資料的第一個日期。 橫向移動路徑報表會提供最多 60 天的資料。

 ![報告](./media/reports.png)

3. 按一下 [下載]。

4. 隨即會建立 Excel 檔案，其中提供您所選日期的潛在橫向移動路徑以及敏感性帳戶暴露的詳細資料。 [摘要] 索引標籤提供詳述敏感性帳戶及電腦的數目，以及風險性存取之平均值的圖表。 [詳細資料] 索引標籤提供您應進一步調查之敏感性帳戶的清單。 請注意，可下載之報表中詳述的路徑可能無法再使用，因為其偵測期間已超過 60 天，可能已經遭到變更或修改。


## <a name="investigate"></a>調查



1. 在 Azure ATP 工作區入口網站中，在實體位於橫向移動路徑 ![橫向圖示](./media/lateral-movement-icon.png) 或 ![路徑圖示](./media/paths-icon.png)。 請注意，只有在過去 48 小時內有橫向移動時，才會顯示該徽章。 

2. 在隨即開啟的使用者設定檔頁面中，按一下 [橫向移動路徑] 索引標籤。 

3. 顯示的圖表能提供針對敏感性使用者之可能路徑的地圖。 圖表會顯示過去 48 小時內觀察到的可能連線。 如果過去兩天內沒有偵測到任何活動，就不會顯示圖表。 

4. 檢閱報表以查看並了解敏感性使用者認證的暴露程度。 例如，在此地圖中，您可以依照 [登入者] 灰色箭頭來查看 Samira 使用其特殊權限認證登入的位置。 在此案例中，Samira 的敏感性認證是儲存在 REDMOND-WA-DEV 這部電腦上。 現在，請注意有哪些其他使用者登入哪部電腦並產生最大程度的暴露與弱點。 您可以查看 [身為系統管理員] 黑色箭頭，以了解誰在該資源上具有系統管理權限。 在此範例中，所有屬於 [Contoso All] 的使用者都能從該資源存取使用者認證。  

 ![使用者設定檔橫向移動路徑](media/user-profile-lateral-movement-paths.png)


## <a name="preventative-best-practices"></a>預防性最佳做法

- 預防橫向移動的最佳做法，是確保敏感性使用者只有在登入強化電腦時才使用其系統管理員認證。 在上述範例中，請確保系統管理員 Samira 在需要存取 REDMOND-WA-DEV 時，以使用者名稱與密碼來登入，而非使用其系統管理員認證。

- 也建議您確保沒有人具有非必要的系統管理權限。 在上述範例中，您應該檢查 [Contoso All] 中的所有成員在 REDMOND-WA-DEV 上是否確實需要系統管理權限。

- 確保人員只擁有必要資源的存取權。 在上述範例中，Oscar Posada 會大幅提高 Samira 的暴露程度。 是否有必要將該使用者包含在 [Contoso All] 群組中？ 是否可以建立子群組來將暴露程度降至最低？

**祕訣**：若過去 48 小時並未偵測到任何活動，且圖表無法使用，橫向移動路徑報告仍然可供使用，而且會提供過去 60 天偵測到的潛在橫向移動路徑資訊。 

**祕訣**：如需設定用戶端與伺服器以允許 Azure ATP 執行橫向移動路徑偵測所需之 SAM-R 作業的指示，請參閱[設定 SAM-R](install-atp-step8-samr.md)。


## <a name="see-also"></a>另請參閱

- [設定 SAM-R 所需的權限](install-atp-step8-samr.md)
- [處理可疑活動](working-with-suspicious-activities.md)
- [查看 ATP 論壇！](https://aka.ms/azureatpcommunity)\(英文\)