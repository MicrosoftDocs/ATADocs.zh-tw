---
title: 使用適用於身分識別的 Microsoft Defender 來調查橫向移動路徑
description: 此文章描述如何使用適用於身分識別的 Microsoft Defender 來偵測及調查潛在橫向移動路徑攻擊。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 10/26/2020
ms.topic: tutorial
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: de9f13a5f29e90ad27a5b07f6b6a92952db6f70d
ms.sourcegitcommit: e2227c0b0e5aaa5163dc56d4131ca82f8dca8fb0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2020
ms.locfileid: "94848528"
---
# <a name="tutorial-use-lateral-movement-paths-lmps"></a>教學課程：使用橫向移動路徑 (LMP)

> [!NOTE]
> 此頁面所述的[!INCLUDE [Product long](includes/product-long.md)] 功能也可使用新的[入口網站](https://portal.cloudappsecurity.com)來存取。

橫向移動攻擊通常使用許多不同的技術來達成。 攻擊者最常用的某些方法為[認證竊取](suspicious-activity-guide.md#)和[票證傳遞](suspicious-activity-guide.md)攻擊。 在這兩種方法中，攻擊者會使用非敏感性帳戶，透過入侵帳戶、群組及擁有敏感性帳戶之電腦中，共用已儲存登入認證的非敏感性電腦來進行橫向移動。

在這個教學課程中，您將了解如何使用[!INCLUDE [Product long](includes/product-long.md)] LMP 來[調查](#investigate)潛在橫向移動路徑，並透過[!INCLUDE [Product short](includes/product-short.md)] 安全性警示，更清楚理解網路發生什麼問題，以及發生原因。 此外，您也將了解如何使用[通往敏感性帳戶的 LMP 報告](#discover-your-at-risk-sensitive-accounts)，依時段探索具有在網路中探索到之潛在橫向移動路徑的所有敏感性帳戶。

> [!div class="checklist"]
>
> - 調查 LMP
> - 探索具風險的敏感性帳戶
> - 存取 **通往敏感性帳戶的橫向移動路徑** 報告

## <a name="investigate"></a>調查

使用和調查 LMP 的方式有許多種。 在[!INCLUDE [Product short](includes/product-short.md)] 入口網站中，依實體搜尋，然後依路徑或活動探索。

1. 從入口網站搜尋使用者或電腦。 請注意橫向移動徽章是否已新增至實體設定檔。 徽章只有在過去 48 小時內於潛在 LMP 中發現實體時才會顯示。

    ![橫向圖示](media/lateral-movement-icon.png) 或 ![路徑圖示](media/paths-icon.png)。

1. 在隨即開啟的使用者設定檔頁面中，按一下 [橫向移動路徑]  索引標籤。

    ![[!INCLUDE [Product short](includes/product-short.md)] [橫向移動路徑 (LMP)] 索引標籤](media/lateral-movement-path-tab.png)

1. 顯示的圖表提供了 48 小時內敏感性使用者潛在路徑的地圖。 如果過去兩天內沒有偵測到任何活動，就不會顯示圖表。 使用 [檢視不同日期]  選項，可顯示先前針對實體偵測橫向移動路徑的圖表。

    ![LMP 可檢視不同的日期](media/view-different-date.png)

1. 檢閱報表以查看並了解敏感性使用者認證的暴露程度。 例如，在路徑中，您可以遵循 [登入者]  灰色箭頭來查看 Nick 使用其特殊權限認證登入的位置。 在此案例中，Nick 的敏感性認證儲存在 SHAREPOINT-SRV 電腦上。 現在，請注意有哪些其他使用者登入哪部電腦並產生最大程度的暴露與弱點。 您可以查看 [身為系統管理員]  黑色箭頭，以了解誰在該資源上具有系統管理權限。 在此範例中，[HelpDesk] 群組中的所有成員都能從該資源存取使用者認證。

    ![[!INCLUDE [Product short](includes/product-short.md)] 橫向移動路徑 (LMP)](media/lmp.png)

## <a name="discover-your-at-risk-sensitive-accounts"></a>探索具風險的敏感性帳戶

若要探索網路中，所有因為連線至橫向移動路徑中非敏感性帳戶、群組及電腦而暴露的敏感性帳戶，請遵循以下步驟。

1. 在[!INCLUDE [Product short](includes/product-short.md)] 入口網站功能表中，按一下報表圖示 ![報表圖示](media/report-icon.png)。

1. 在 [針對敏感性帳戶的橫向移動路徑]  底下，若找不到潛在的橫向移動路徑，報表將會呈現灰色。若有潛在的橫向移動路徑，則報表會自動預先選取有相關資料的第一個日期。 橫向移動路徑報表會提供最多 60 天的資料。

    ![顯示選取報表日期的螢幕擷取畫面](media/reports.png)

1. 按一下 [下載]  。

1. 隨即會建立 Excel 檔案，其中提供您所選日期的潛在橫向移動路徑以及敏感性帳戶暴露的詳細資料。 [摘要]  索引標籤提供詳述敏感性帳戶及電腦的數目，以及風險性存取之平均值的圖表。 [詳細資料]  索引標籤提供您應進一步調查之敏感性帳戶的清單。

## <a name="schedule-report"></a>為報告進行排程

也可以使用設定排程報告功能，為敏感性帳戶的橫向移動報告排程。

請注意，由於過去已偵測到實際的 LMP，而且可能因為被偵測到，而已變更、修改或修正，所以可下載報告中詳述的實際 LMP 可能已無法使用。

若要檢閱歷史 LMP，請於建立報告時，選取行事曆選取項目中其他可用的日期。

## <a name="next-steps"></a>後續步驟

在這個教學課程中，您已經了解如何使用 LMP 調查可疑的活動。 如需深入了解涉及 LMP 的實體，請繼續瀏覽調查實體教學課程。

> [!div class="nextstepaction"]
> [調查實體](investigate-entity.md)

## <a name="see-also"></a>另請參閱

- [了解[!INCLUDE [Product short](includes/product-short.md)] 橫向移動路徑](use-case-lateral-movement-path.md)
- [設定[!INCLUDE [Product short](includes/product-short.md)] 以對 SAM 發出遠端呼叫](install-step8-samr.md)
- [使用安全性警訊](working-with-suspicious-activities.md)
- [查看[!INCLUDE [Product short](includes/product-short.md)] 論壇！](https://aka.ms/MDIcommunity)\(英文\)
