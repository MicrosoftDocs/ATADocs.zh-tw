---
title: 什麼是適用於身分識別的 Microsoft Defender？
description: 說明什麼是適用於身分識別的 Microsoft Defender，以及其可以偵測哪種類型的可疑活動
ms.date: 12/23/2020
ms.topic: overview
ms.openlocfilehash: 2893567b6aca307c4a99148804544aa7da8863ea
ms.sourcegitcommit: a892419a5cb95412e4643c35a9a72092421628ec
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/16/2021
ms.locfileid: "100534465"
---
# <a name="what-is-microsoft-defender-for-identity"></a>什麼是適用於身分識別的 Microsoft Defender？

[!INCLUDE [Product long](includes/product-long.md)] (先前是 Azure 進階威脅防護 (ATP)，亦稱為 Azure ATP) 是雲端式安全性解決方案，其可運用您的內部部署 Active Directory 訊號來識別、偵測及調查針對您組織的進階威脅、身分識別盜用，以及惡意的內部人員動作。

[!INCLUDE [Product short](includes/product-short.md)] 讓 SecOp 分析師及安全性專業人員可以在努力偵測混合式環境中的進階攻擊時，能夠：

- 透過學習式分析，監視使用者、實體行為及活動
- 保護儲存在 Active Directory 中的使用者身分識別與認證
- 識別及調查整個狙殺鏈中的可疑使用者活動與進階攻擊
- 在簡單的時間軸上提供明確的事件資訊，以快速分級

## <a name="monitor-and-profile-user-behavior-and-activities"></a>監視和分析使用者行為和活動

[!INCLUDE [Product short](includes/product-short.md)] 會監視並分析整個網路的使用者活動與資訊，例如權限與群組成員資格，並為每個使用者建立行為基準。 接著，[!INCLUDE [Product short](includes/product-short.md)] 會使用調適型內建智慧功能識別出異常項目，提供您可疑活動與事件的見解，揭露進階威脅、遭入侵的使用者與組織所面臨的內部威脅。 [!INCLUDE [Product short](includes/product-short.md)] 專屬感應器可監視組織的網域控制站，並提供每部裝置所有使用者活動的完整檢視。

## <a name="protect-user-identities-and-reduce-the-attack-surface"></a>保護使用者的身分識別，並減少受攻擊面

[!INCLUDE [Product short](includes/product-short.md)] 可提供您身分識別設定的寶貴見解以及安全性最佳實務的建議。 透過安全性報告與使用者設定檔分析，[!INCLUDE [Product short](includes/product-short.md)] 有助於大幅減少組織的受攻擊面，提高入侵使用者認證與發動攻擊的難度。 [!INCLUDE [Product short](includes/product-short.md)] 的視覺化橫向移動路徑可協助您對攻擊者如何在組織內部橫向移動以入侵機密帳戶的過程一目了然，並事先防止這些風險。 [!INCLUDE [Product short](includes/product-short.md)] 安全性報告可協助您找出使用純文字密碼進行驗證的使用者與裝置，並提供額外的見解，以提升組織的安全性狀態與原則。

## <a name="protecting-the-ad-fs-in-hybrid-environments"></a>保護混合式環境中的 AD FS

在混合式環境中的驗證方面，Active Directory 同盟服務 (AD FS) 於現今的基礎結構中扮演重要的角色。 [!INCLUDE [Product short](includes/product-short.md)] 透過在 AD FS 偵測內部部署攻擊並讓您了解由 AD 產生的驗證事件，來保護您環境中的 AD FS。

## <a name="identify-suspicious-activities-and-advanced-attacks-across-the-cyber-attack-kill-chain"></a>識別整個網路攻擊狙殺鏈的可疑活動與進階攻擊

一般來說，攻擊者會針對任何可存取的實體 (例如低權限使用者) 發動攻擊，再快速橫向移動直到獲得寶貴資產的存取權為止 – 例如敏感性帳戶、網域系統管理員和高敏感性資料。 [!INCLUDE [Product short](includes/product-short.md)] 會從整個網路攻擊狙殺鏈來源識別這些進階威脅：

### <a name="reconnaissance"></a>探查

識別流氓使用者和攻擊者取得資訊的嘗試。 攻擊者會使用各種方法尋找使用者名稱、使用者群組成員資格、指派給裝置的 IP 位址、資源等相關資訊。

### <a name="compromised-credentials"></a>遭洩漏的認證

識別透過暴力密碼破解攻擊、失敗的驗證、使用者群組成員資格變更等其他方法入侵使用者認證的嘗試。

### <a name="lateral-movements"></a>橫向移動

偵測利用傳遞票證、傳遞雜湊、侵犯雜湊等方式在網路內部橫向移動，以進一步控制機密使用者的不良意圖。

### <a name="domain-dominance"></a>網域支配

如果有人透過在網域控制站上遠端執行程式碼及 DC Shadow、惡意網域控制站複寫、Golden Ticket 活動等方法達成網域支配，即醒目提示攻擊者的行為。

## <a name="investigate-alerts-and-user-activities"></a>調查警示和使用者活動

[!INCLUDE [Product short](includes/product-short.md)] 的設計目的是減少一般警示干擾，只在簡單的即時組織攻擊時間軸中提供相關的重要安全性警示。 [!INCLUDE [Product short](includes/product-short.md)] 的攻擊時間軸檢視可讓您運用智慧分析的情報，安心專注於重要工作。 使用[!INCLUDE [Product short](includes/product-short.md)] 來快速調查威脅，並取得整個組織中使用者、裝置與網路資源的見解。 與適用於端點的 Microsoft Defender 緊密整合，透過可抵禦作業系統上進階持續威脅的額外偵測和防護，提供另一道增強的安全性保障。

## <a name="additional-resources-for-defender-for-identity"></a>適用于 Defender 身分識別的其他資源

### <a name="start-a-free-trial"></a>開始使用免費試用版

[https://signup.microsoft.com/Signup?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7&ali=1](https://signup.microsoft.com/Signup?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7&ali=1 "Enterprise Mobility + Security E5")

### <a name="follow-defender-for-identity-on-microsoft-tech-community"></a>在 Microsoft Tech 團體上追蹤適用于身分識別的 Defender

[https://aka.ms/MDIcommunity](https://aka.ms/MDIcommunity "[!INCLUDE [Product short](includes/product-short.md)] on Microsoft Tech Community")

### <a name="join-the-defender-for-identity-yammer-community"></a>加入適用于 Identity Yammer 的 Defender 社區

[https://www.yammer.com/azureadvisors/#/threads/inGroup?type=in_group&feedId=9386893](https://www.yammer.com/azureadvisors/#/threads/inGroup?type=in_group&feedId=9386893 "[!INCLUDE [Product short](includes/product-short.md)] Yammer community")

### <a name="visit-the-defender-for-identity-product-page"></a>造訪適用于身分識別的 Defender 產品頁面

[https://www.microsoft.com/microsoft-365/security/identity-defender](https://www.microsoft.com/microsoft-365/security/identity-defender "[!INCLUDE [Product short](includes/product-short.md)] product page")

### <a name="learn-more-about-defender-for-identity-architecture"></a>深入瞭解適用于身分識別架構的 Defender

[[!INCLUDE [Product short](includes/product-short.md)] 架構](architecture.md)

### <a name="watch-our-videos"></a>觀看我們的影片

[使用 [!INCLUDE [Product short](includes/product-short.md)]](https://techcommunity.microsoft.com/t5/video-hub/bolster-your-security-posture-with-microsoft-defender-for/m-p/1698841) 維持您的安全性狀態 - 識別及主動解決已知不良做法，讓您的環境維持較健康的狀態，以及加強抵禦惡意執行者的能力 - 觀看 [YouTube 影片](https://youtu.be/nx5rrxVuRTk)

[使用 [!INCLUDE [Product short](includes/product-short.md)]](https://techcommunity.microsoft.com/t5/video-hub/incident-investigation-with-microsoft-defender-for-identity/m-p/1698840) 進行事件調查 - 了解如何使用[!INCLUDE [Product short](includes/product-short.md)] 來偵測、調查及回應以身分識別與網域控制站為目標的進階威脅。 從[!INCLUDE [Product short](includes/product-short.md)] 中的警示開始，我們將示範如何將該資訊與事件相互關聯、如何使用[!INCLUDE [Product short](includes/product-short.md)] 所擷取的資訊來搜捕威脅，以及如何起始自動事件回應以在事件發展為更大的問題之前進行補救 - 觀看 [YouTube 影片](https://youtu.be/geWU4It6S48)

## <a name="whats-next"></a>接下來要做什麼？

建議您分三個階段來部署[!INCLUDE [Product short](includes/product-short.md)]：

### <a name="phase-1"></a>階段 1

1. 設定[!INCLUDE [Product short](includes/product-short.md)] 以保護您的主要環境。 [!INCLUDE [Product short](includes/product-short.md)] 的快速部署模型可讓您立即開始保護組織。 [安裝[!INCLUDE [Product short](includes/product-short.md)]](install-step1.md)
1. 設定[機密帳戶](sensitive-accounts.md)與 [honeytoken 帳戶](install-step7.md)。
1. 檢閱報告和[橫向移動路徑](use-case-lateral-movement-path.md)。

### <a name="phase-2"></a>階段 2

1. 保護組織中的所有網域控制站和[樹系](multi-forest.md)。
1. 監視所有[警示](working-with-suspicious-activities.md) – 調查橫向移動和網域支配的警示。
1. 使用[安全性警訊指南](suspicious-activity-guide.md)，以了解威脅並對潛在攻擊進行分級。

### <a name="phase-3"></a>階段 3

1. 將[!INCLUDE [Product short](includes/product-short.md)] 警示整合到您的 SecOp 工作流程。

## <a name="see-also"></a>另請參閱

- [[!INCLUDE [Product short](includes/product-short.md)] 常見問題集](technical-faq.yml)
- [使用安全性警訊](working-with-suspicious-activities.md)
- [查看[!INCLUDE [Product short](includes/product-short.md)] 論壇！](https://aka.ms/MDIcommunity)\(英文\)
