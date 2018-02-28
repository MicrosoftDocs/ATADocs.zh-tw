---
title: "使用 Azure ATP 調查橫向移動路徑攻擊 | Microsoft Docs"
description: "本文說明如何使用 Azure 進階威脅防護 (ATP) 偵測橫向移動路徑攻擊。"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2018
ms.topic: article
ms.prod: 
ms.service: azure-advanced-threat-protection
ms.technology: 
ms.assetid: de15c920-8904-4124-8bdc-03abd9f667cf
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 7deeec2c2ee2c2d964b6495921eba0fa378bd8ee
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/21/2018
---
適用於：Azure 進階威脅防護 1.9 版

# <a name="investigating-lateral-movement-paths-with-azure-atp"></a>使用 Azure ATP 調查橫向移動路徑

Azure ATP 可協助您預防使用橫向移動路徑的攻擊。 就算您盡最大努力保護敏感性使用者，且您的系統管理員經常變更其複雜密碼、強化其電腦並將資料儲存在安全的位置，攻擊者仍然可以使用橫向移動路徑在您網路上的使用者及電腦之間移動，直到他們成功找出虛擬安全性的寶庫，也就是您敏感的管理帳戶認證。

## <a name="what-is-a-lateral-movement-path"></a>橫向移動路徑是什麼？

橫向移動是攻擊者主動使用非敏感性帳戶來取得敏感性帳戶存取權的方式。 他們可以使用[可疑活動指南](suspicious-activity-guide.md)中所述的任何一種方法，來取得初步的非敏感性密碼，然後使用如 Bloodhound 等工具來了解您網路中的系統管理員身分，以及該系統管理員所能存取的電腦。 攻擊者能利用其可從您的網域控制站上取得的資料，來了解帳戶擁有者的身分，以及該使用者能夠存取的資源及檔案，並能竊取儲存在已成功存取之電腦上的其他使用者 (有時還是敏感性使用者) 認證，然後以橫向方式移至更多的使用者及資源，直到他們取得您網路的系統管理權限為止。 

Azure ATP 可讓您在網路上採取先佔式動作，以防止攻擊者成功進行橫向移動。

## <a name="discovery-your-at-risk-sensitive-accounts"></a>探索具有風險的敏感性帳戶

若要探索網路中有哪些敏感性帳戶因和非敏感性的帳戶或資源之間具有連線而處於易受攻擊的狀態，請遵循這些步驟。 為了保護網路不受橫向移動攻擊的危害，Azure ATP 會從末端反向運作，這代表 Azure ATP 會給您一幅以特殊權限帳戶為起點的地圖，然後為您顯示處於這些使用者及其認證之橫向路徑的使用者及裝置有哪些。

1. 在 Azure ATP 工作區入口網站功能表列中，按一下 [報表] 圖示 ![[報表] 圖示](./media/atp-report-icon.png)。

2. 在 [針對敏感性帳戶的橫向移動路徑] 底下，若找不到橫向移動路徑，報表將會呈現灰色。若有橫向移動路徑，則報表的日期將會自動選取為具有相關資料的第一個日期。 橫向移動路徑報表會提供過去 60 天的資料。

 ![報告](./media/reports.png)

3. 按一下 [下載]。

3. 所建立的 Excel 檔案能為您提供處於風險之敏感性帳戶的詳細資料。 [摘要] 索引標籤能提供詳述敏感性帳戶及電腦的數目，以及處於風險資源之平均值的圖表。 [詳細資料] 索引標籤能提供您應注意之敏感性帳戶的清單。

4. 如需設定伺服器以允許 Azure ATP 執行橫向移動路徑偵測所需之 SAM-R 作業的指示，請參閱[設定 SAM-R](install-atp-step8-samr.md)。

## <a name="investigate"></a>調查

現在您已知道有哪些敏感性帳戶處於風險中，便可以深入鑽研 Azure ATP 以了解更多資訊並採取預防性措施。

1. 在 Azure ATP 工作區入口網站中，在 [針對敏感性帳戶的橫向移動路徑] 報表中查看帳戶被列為易受攻擊的使用者，例如 Samira Abbasi。 在實體位於橫向移動路徑 ![橫向圖示](./media/lateral-movement-icon.png) 或 ![路徑圖示](./media/paths-icon.png) 時，您也可以搜尋實體設定檔中新增有這些橫向移動徽章的實體。 這會在過去兩天內有出現橫向移動的情況下提供。 

2. 在隨即開啟的使用者設定檔頁面中，按一下 [橫向移動路徑] 索引標籤。 

3. 顯示的圖表能提供您針對敏感性使用者之可能路徑的地圖。 該圖表能顯示於過去兩天內所做出的連線，以提供最新的暴露程度。 若在過去兩天內都沒有偵測到活動，該圖表便不會出現，不過系統仍然會提供[橫向移動路徑報表](reports.md)，以提供您過去 60 天的橫向移動路徑相關資訊。

4. 檢閱報表以查看並了解敏感性使用者認證的暴露程度。 例如，在此針對 Samira Abbasi 的地圖中，您可以依照 [登入者] 灰色箭頭來查看 Samira 使用其特殊權限認證登入的位置。 在此案例中，Samira 的敏感性認證已儲存在 REDMOND-WA-DEV 這部電腦上。 接著，查看有哪些其他使用者登入哪部電腦並產生最大程度的暴露及漏洞。 您可以查看 [身為系統管理員] 黑色箭頭，以了解誰在該資源上具有系統管理權限。 在此範例中，所有屬於 [Contoso All] 的使用者都能從該資源存取使用者認證。  

 ![使用者設定檔橫向移動路徑](media/user-profile-lateral-movement-paths.png)


## <a name="preventative-best-practices"></a>預防性最佳做法

- 預防橫向移動的最佳做法，是確保敏感性使用者只有在登入強化電腦時才使用其系統管理員認證。 在上述範例中，請確保系統管理員 Samira 在需要存取 REDMOND-WA-DEV 時，所使用的使用者名稱及密碼不是其系統管理員認證。

- 也建議您確保沒有人具有非必要的系統管理權限。 在上述範例中，您應該檢查 [Contoso All] 中的所有成員在 REDMOND-WA-DEV 上是否都需要有系統管理權限。

- 確保人員只具有必要資源的存取權，一向都是個良好的做法。 如您在上述範例中所見，Oscar Posada 會大幅提高 Samira 的暴露程度。 是否有必要將該使用者包含在 [Contoso All] 中？ 是否可以建立子群組來將暴露程度降至最低？


## <a name="see-also"></a>另請參閱

- [設定 SAM-R 所需的權限](install-atp-step8-samr.md)
- [處理可疑活動](working-with-suspicious-activities.md)
- [查看 ATP 論壇！](https://aka.ms/azureatpcommunity)\(英文\)