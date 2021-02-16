---
title: 適用于身分識別與 Microsoft Defender for Endpoint 整合的 microsoft Defender
description: 如何將 Microsoft Defender for Identity 與 Microsoft Defender for Endpoint 整合，以取得完整的威脅偵測涵蓋範圍
ms.date: 10/26/2020
ms.topic: how-to
ms.openlocfilehash: 356f97509fe3af81a4d1c896e7b64b2779e6028a
ms.sourcegitcommit: a892419a5cb95412e4643c35a9a72092421628ec
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/16/2021
ms.locfileid: "100533863"
---
# <a name="integrate-microsoft-defender-for-identity-with-microsoft-defender-for-endpoint"></a>將 Microsoft Defender for Identity 與 Microsoft Defender for Endpoint 整合

[!INCLUDE [Product long](includes/product-long.md)] 可讓您 [!INCLUDE [Product long](includes/product-long.md)] 與 Defender For Endpoint 整合，以取得更完整的威脅防護解決方案。 在 [!INCLUDE [Product short](includes/product-short.md)] 監視您網域控制站上的流量時，Defender For Endpoint 會監視您的端點，同時提供單一介面讓您可以保護您的環境。

藉由將 Defender for Endpoint 整合到 [!INCLUDE [Product short](includes/product-short.md)] ，您可以充分利用這兩項服務的完整功能，並保護您的環境，包括：

- 端點行為感應器：內嵌于 Windows 10 中，這些感應器會收集和處理作業系統 (的行為信號，例如，程式、登錄、檔案和網路通訊) ，並將此感應器資料傳送至您私人獨立的 Defender for Endpoint 雲端實例。

- 雲端安全性分析：利用巨量資料、機器學習及整個 Windows 生態系統的獨特 Microsoft 檢視 (例如 [Microsoft 惡意軟體移除工具](https://www.microsoft.com/download/malicious-software-removal-tool-details.aspx))、企業雲端產品 (例如 Microsoft 365) 與線上資產 (例如 Bing 及 SmartScreen URL 信譽)，行為訊號會轉譯為針對進階威脅的見解、偵測及建議回應。

- 威脅情報：由合作夥伴提供的威脅情報所產生的 Microsoft 獵人及、安全性小組和增強功能，威脅情報可讓 Defender for Endpoint 識別攻擊者工具、技術、程式，並在收集到的感應器資料中觀察到這些活動時產生警示。

[!INCLUDE [Product short](includes/product-short.md)] 技術會偵測到多個可疑的活動，著重在網路攻擊的幾個階段，包括：

- 「偵查」階段，此時攻擊者會收集有關環境的建構方式、有哪些不同的資產，以及存在何種實體等資訊。 他們通常會在此著手規劃下一階段的攻擊。

- 橫向移動週期，此時攻擊者會將時間與精力放在在網路內部分散攻擊面。

- 「網域支配 (持續性)」階段，此時攻擊者會擷取資訊，以便使用各種進入點、認證和技術繼續進行攻擊活動。

同時，Defender for Endpoint 會利用 Microsoft 技術和專業知識來偵測複雜的網路攻擊，提供：

- 以行為為基礎、運用雲端技術的進階攻擊偵測  
找出所有其他防禦 (入侵後偵測) 的攻擊，並針對嘗試在端點上隱藏其活動的已知和未知敵人提供可採取動作的相關警示。

- 可供進行鑑識調查及緩解問題的豐富時間表  
透過豐富的電腦時間表，輕鬆地調查任何電腦上的入侵範圍或可疑的行為。 範圍遍布整個網路的檔案、URL 和網路連線清查。 針對任何檔案或 URL 使用深層收集及分析 (「引爆」) 來取得額外的見解。

- 內建的獨特威脅情報知識庫  
絕佳的威脅視野能結合第一方和第三方情報來源，針對每個威脅情報偵測提供執行者詳細資料和意圖內容。

## <a name="prerequisites"></a>先決條件

若要啟用這項功能，您需要 [!INCLUDE [Product short](includes/product-short.md)] 和 Defender For Endpoint 的授權。

<a name="how-to-integrate-azure-atp-with-microsoft-defender-atp"></a>

## <a name="how-to-integrate-defender-for-identity-with-defender-for-endpoint"></a>如何整合 Defender for Identity 與 Defender for Endpoint

1. 在[!INCLUDE [Product short](includes/product-short.md)] 中，選取 [設定]。

    ![[!包含 [Product short] (include/product-short. md) ] 設定功能表](media/msde-configuration.png)
1. 在 [設定] 清單中，選取 [ **Microsoft Defender For Endpoint** ]，並將 [整合切換] 設定為 [ **開啟**]。

    ![啟用 Windows Defender 整合](media/msde-enable-integration.png)

1. 在 [Defender For Endpoint 入口網站](https://securitycenter.windows.com/preferences/advanced)中，移至 [**設定**]、[ **Advanced features** ]，並將 **[!INCLUDE [Product long](includes/product-long.md)] 整合** 設定為 [**開啟**]。

    ![Defender for Endpoint 啟用整合](media/msde-enable.png)

1. 若要檢查整合狀態，請在 [!INCLUDE [Product short](includes/product-short.md)] 入口網站中，移至 [**設定**  >  **Microsoft Defender 以進行端點整合**]。 您可以查看整合狀態，若發生問題，您將會看到錯誤。

## <a name="how-it-works"></a>運作方式

當 [!INCLUDE [Product short](includes/product-short.md)] 端點和 defender For endpoint 完全整合之後，在 [!INCLUDE [Product short](includes/product-short.md)] 入口網站中，在迷你設定檔快顯視窗和實體設定檔頁面面中，每個存在於端點之 defender 中的實體都會包含徽章，以顯示它已與 Defender for endpoint 整合。

 ![Defender for Endpoint alerts 設定檔](media/profile-alerts-msde.png)

如果實體包含 Defender for Endpoint 的警示，徽章旁邊會有一個數位，讓您知道引發了多少警示。

 ![[!包含 [Product short] (include/product-short. md) ] 警示](media/msde-icon-alerts.png)

如果您按一下徽章，則會帶您前往 Defender for Endpoint 入口網站，您可以在其中查看和緩和警示。 如果 Defender 無法辨識該實體的端點，徽章會呈現灰色。

 ![Defender for Endpoint 灰色](media/msde-grey.png)

從 Defender for Endpoint 入口網站中，按一下端點以查看 [!INCLUDE [Product short](includes/product-short.md)] 警示。 如果您在 Defender 中針對端點按一下此實體的警示，則會在中開啟實體的設定檔頁面面 [!INCLUDE [Product short](includes/product-short.md)] 。

 > [!NOTE]
 > 目前， [!INCLUDE [Product short](includes/product-short.md)] 與 Defender For Endpoint 的整合僅支援來自內部部署 AD 的使用者和電腦。 來自 Azure AD 以及在 Azure 中管理之虛擬機器的使用者不會在整合中出現

![Defender for Endpoint 警示](media/msde-alerts.png)

## <a name="see-also"></a>另請參閱

- [調查橫向移動路徑 [!INCLUDE [Product short](includes/product-short.md)]](use-case-lateral-movement-path.md)
- [[!INCLUDE [Product short](includes/product-short.md)] 大小調整工具](https://aka.ms/aatpsizingtool) \(英文\)
- [[!INCLUDE [Product short](includes/product-short.md)] 架構](architecture.md)
- [安裝[!INCLUDE [Product short](includes/product-short.md)]](install-step1.md)
- [查看[!INCLUDE [Product short](includes/product-short.md)] 論壇！](https://aka.ms/MDIcommunity)\(英文\)
