---
title: 了解及使用搭配適用於身分識別的 Microsoft Defender 的橫向移動路徑
description: 此文章描述適用於身分識別的 Microsoft Defender 的潛在橫向移動路徑 (LMP)
ms.date: 10/27/2020
ms.topic: conceptual
ms.openlocfilehash: 60fac487690d5ff71eb2df5d6ee52c15c336941e
ms.sourcegitcommit: a892419a5cb95412e4643c35a9a72092421628ec
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/16/2021
ms.locfileid: "100533438"
---
# <a name="microsoft-defender-for-identity-lateral-movement-paths-lmps"></a>適用于身分識別橫向移動路徑的 Microsoft Defender (Lmp) 

> [!NOTE]
> 此頁面所述的[!INCLUDE [Product long](includes/product-long.md)] 功能也可使用新的[入口網站](https://portal.cloudappsecurity.com)來存取。

橫向移動是攻擊者使用非敏感性帳戶存取您整個網路中的敏感性帳戶。 攻擊者使用橫向移動來識別並存取您網路中共用帳戶、群組與電腦內已儲存登入認證的敏感性帳戶和電腦。 一旦攻擊者成功橫向移動到您的關鍵目標，攻擊者也可以利用和存取您的網域控制站。 橫向移動攻擊使用[可疑活動指南](suspicious-activity-guide.md)中說明的許多方法來達成。

[!INCLUDE [Product long](includes/product-long.md)] 安全性見解的一個主要要素為橫向移動路徑 (LMP)。 [!INCLUDE [Product short](includes/product-short.md)] LMP 是以圖像呈現的指南，可協助您快速了解並確實識別攻擊者如何在您的網路中橫向移動。 在網路攻擊狙殺鏈 (cyber-attack kill chain) 中橫向移動的目的在於讓攻擊者使用非敏感性帳戶，取得並入侵您的敏感性帳戶。 入侵您的敏感性帳戶讓攻擊者可以更靠近他們的最終目標，也就是支配網域。 為防止這些攻擊，[!INCLUDE [Product short](includes/product-short.md)] LMP 針對您最易受攻擊的敏感性帳戶為您提供以圖像呈現而且直接易懂的指南。 LMP 可協助您降低風險並防範未來發生那些風險，以及在攻擊者達成網域支配前，關閉他們的存取權。

![[!INCLUDE [Product short](includes/product-short.md)] 橫向移動路徑 (LMP)](media/lmp.png)

橫向移動攻擊通常使用許多不同的技術來達成。 攻擊者最常用的某些方法為認證竊取和票證傳遞。 在這兩種方法中，攻擊者會使用您的非敏感性帳戶，透過入侵帳戶、群組及擁有敏感性帳戶之電腦中，共用已儲存登入認證的非敏感性電腦來進行橫向移動。

## <a name="where-can-i-find-defender-for-identity-lmps"></a>哪裡可以找到 Defender 以進行身分識別 Lmp？

[!INCLUDE [Product short](includes/product-short.md)] 探索到位於 LMP 中的每個電腦或使用者設定檔都有 [橫向移動路徑] 索引標籤。在潛在 LMP 中永遠不會探索到沒有索引標籤的電腦及設定檔。

![[!INCLUDE [Product short](includes/product-short.md)] [橫向移動路徑 (LMP)] 索引標籤](media/lateral-movement-path-tab.png)

每個實體的 LMP 都會依據實體的敏感度提供不同的資訊：

- 敏感性使用者 - 顯示通往此使用者的潛在 LMP。
- 非敏感性使用者及電腦 - 顯示與實體相關的潛在 LMP。

每次按一下該索引標籤時，[!INCLUDE [Product short](includes/product-short.md)] 都會顯示最近探索到的 LMP。 每個潛在 LMP 都會在探索到之後儲存 48 小時。 並有 LMP 歷程記錄。 按一下 [檢視其他日期]  ，即可檢視過去探索到的較舊 LMP。

![[!INCLUDE [Product short](includes/product-short.md)] [橫向移動路徑 (LMP)] 顯示](media/lmp-complete.png)

探索識別出潛在 LMP 的時間，和可能涉及的相關實體。

## <a name="lmp-discovery"></a>LMP 探索

在 [活動] 索引標籤中，當識別到新的潛在 LMP 時，就會予以指示：

- 敏感性使用者 - 當識別到通往敏感性使用者的新路徑時

![[!INCLUDE [Product short](includes/product-short.md)] 橫向移動路徑 (LMP) 敏感性已識別](media/lmp-activities.png)

- 非敏感性使用者和電腦 - 當在通往敏感性使用者的潛在 LMP 中識別到此實體時。

![[!INCLUDE [Product short](includes/product-short.md)] 橫向移動路徑 (LMP) 非敏感性已識別](media/lateral-non-sensitive.png)

## <a name="lmp-related-entities"></a>LMP 相關實體

LMP 現在可直接協助您進行調查流程。 [!INCLUDE [Product short](includes/product-short.md)] 安全性警示辨識項清單提供涉及各個潛在橫向移動路徑的相關實體。 辨識項清單可直接地協助安全性回應小組增加或減少安全性警訊，及 (或) 相關實體調查的重要性。 例如，當發出票證傳遞警示時，竊取票證的來源來源電腦、遭入侵使用者及目的地電腦，都屬於通往敏感性使用者的潛在橫向移動路徑。 存在偵測到的 LMP 讓調查警示和觀看可疑使用者更為重要，以防止敵人又橫向移動。 LMP 中提供可追蹤的辨識項，讓您更快且更輕鬆地防止攻擊者繼續入侵您的網域。

## <a name="lateral-movement-paths-to-sensitive-accounts-report"></a>通往敏感性帳戶的橫向移動路徑報告

[通往敏感性帳戶的橫向移動路徑報告](investigate-lateral-movement-path.md)中也會提供 LMP 資料。 此報告列出透過橫向移動路徑暴露的敏感性帳戶，並包含特定期間或排程報告期間內手動選取的路徑。  使用行事曆選取範圍自訂包含的日期範圍。

## <a name="preventative-best-practices"></a>預防性最佳做法

安全性見解永遠能夠及時防止下一次的攻擊和修補損害。 因此，即使在網域支配階段內調查攻擊仍可提供不同但重要的範例。 通常當調查像是遠端程式碼執行等安全性警訊時，若警示為確判，您的網域控制站可能已經遭入侵。 但 LMP 會通知您攻擊者取得權限的位置，和他們進入您網路所使用的路徑。 如此一來，LMP 也可提供如何補救的重要見解。

- 防止組織受橫向移動攻擊的最佳做法，是確保敏感性使用者只在登入強化的電腦時使用其系統管理員認證。 在此範例中，檢查路徑中的系統管理員是否真的需要共用電腦的存取權。 若他們真的需要存取權，請確定使用使用者名稱與密碼，而非其系統管理員認證登入共用電腦。

- 請驗證您的使用者沒有不必要的系統管理權限。 在範例中，請檢查共用群組的每個人是否都真的需要已暴露電腦上的系統管理員權限。

- 確保人員只擁有必要資源的存取權。 在範例中，Ron Harper 大幅提高了 Nick Cowley 暴露度。 Ron Harper 需要包含在群組中嗎？ 可建立子群組來降低受橫向移動攻擊的風險嗎？

**提示** - 若過去 48 小時內針對實體未偵測出潛在橫向移動路徑活動，請選擇 [檢視其他日期]  ，並檢查先前的潛在橫向移動路徑。 當探索到 LMP 時，[通往敏感性使用者的 LMP 報告]  將會一律可用，並會為您提供偵測到通往敏感性使用者的潛在橫向移動路徑相關資訊。

**祕訣**：如需設定用戶端與伺服器以允許 [!INCLUDE [Product short](includes/product-short.md)] 執行橫向移動路徑偵測所需之 SAM-R 作業的指示，請參閱 [設定 SAM-R](install-step8-samr.md)。

## <a name="investigating-lmps"></a>調查 LMP

如需如何使用[!INCLUDE [Product short](includes/product-short.md)] 橫向移動路徑來識別並調查的指示，請參閱[調查橫向移動路徑](investigate-lateral-movement-path.md)。

## <a name="see-also"></a>另請參閱

- [調查[!INCLUDE [Product short](includes/product-short.md)] LMP](investigate-lateral-movement-path.md)
- [設定[!INCLUDE [Product short](includes/product-short.md)] 以對 SAM 發出遠端呼叫](install-step8-samr.md)
- [使用安全性警訊](working-with-suspicious-activities.md)
- [查看[!INCLUDE [Product short](includes/product-short.md)] 論壇！](https://aka.ms/MDIcommunity)\(英文\)
