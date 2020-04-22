---
title: 什麼是 Azure 進階威脅防護 (Azure ATP)？
description: 說明何謂 Azure 進階威脅防護 (Azure ATP)，以及它可以偵測到哪些可疑活動種類
keywords: ''
author: shsagir
ms.author: shsagir
manager: rkarlin
ms.date: 04/05/2020
ms.topic: article
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 2d14d0e9-1b03-4bcc-ae97-8fd41526ffc5
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: a421fdb784bd0e180921048951f73c94382ea733
ms.sourcegitcommit: 63be53de5b84eabdeb8c006438dab45bd35a4ab7
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "80669973"
---
# <a name="what-is-azure-advanced-threat-protection"></a>什麼是 Azure 進階威脅防護？

Azure 進階威脅防護 (ATP) 是雲端式安全性解決方案，其可運用您的內部部署 Active Directory 訊號來識別、偵測及調查針對您組織的進階威脅、身分識別盜用，以及惡意的內部人員動作。

Azure ATP 可讓為了偵測出混合式環境中的進階攻擊而心力交瘁的 SecOp 分析師和安全性專業人員完成以下作業：

- 透過學習式分析，監視使用者、實體行為及活動
- 保護儲存在 Active Directory 中的使用者身分識別與認證
- 識別及調查整個狙殺鏈中的可疑使用者活動與進階攻擊
- 在簡單的時間軸上提供明確的事件資訊，以快速分級

## <a name="monitor-and-profile-user-behavior-and-activities"></a>監視和分析使用者行為和活動

Azure ATP 會監視並分析整個網路的使用者活動和資訊，例如權限和群組成員資格，並為每個使用者建立行為基準。 接著，Azure ATP 會使用調適型內建智慧功能識別出異常項目，提供您可疑活動和事件的見解，揭露進階威脅、遭入侵的使用者和組織所面臨的內部威脅。 Azure ATP 專屬感應器可監視組織的網域控制站，並提供每部裝置所有使用者活動的完整檢視。

## <a name="protect-user-identities-and-reduce-the-attack-surface"></a>保護使用者的身分識別，並減少受攻擊面

Azure ATP 可提供您身分識別設定的寶貴見解以及安全性最佳實務的建議。 透過安全性報告和使用者設定檔分析，Azure ATP 可協助大幅減少組織的受攻擊面，提高入侵使用者認證與發動攻擊的難度。 Azure ATP 的視覺化橫向移動路徑可協助您對攻擊者如何在組織內部橫向移動以入侵機密帳戶的過程一目了然，並事先防止這些風險。 Azure ATP 安全性報告可協助您找出使用純文字密碼進行驗證的使用者和裝置，並提供額外的見解，以提升組織的安全性狀態與原則。

## <a name="identify-suspicious-activities-and-advanced-attacks-across-the-cyber-attack-kill-chain"></a>識別整個網路攻擊狙殺鏈的可疑活動與進階攻擊

一般來說，攻擊者會針對任何可存取的實體 (例如低權限使用者) 發動攻擊，再快速橫向移動直到獲得寶貴資產的存取權為止 – 例如敏感性帳戶、網域系統管理員和高敏感性資料。 Azure ATP 會從整個網路攻擊狙殺鏈來源識別這些進階威脅：

### <a name="reconnaissance"></a>探查

識別流氓使用者和攻擊者取得資訊的嘗試。 攻擊者會使用各種方法尋找使用者名稱、使用者群組成員資格、指派給裝置的 IP 位址、資源等相關資訊。

### <a name="compromised-credentials"></a>遭洩漏的認證

識別透過暴力密碼破解攻擊、失敗的驗證、使用者群組成員資格變更等其他方法入侵使用者認證的嘗試。

### <a name="lateral-movements"></a>橫向移動

偵測利用傳遞票證、傳遞雜湊、侵犯雜湊等方式在網路內部橫向移動，以進一步控制機密使用者的不良意圖。

### <a name="domain-dominance"></a>網域支配

如果有人透過在網域控制站上遠端執行程式碼及 DC Shadow、惡意網域控制站複寫、Golden Ticket 活動等方法達成網域支配，即醒目提示攻擊者的行為。

## <a name="investigate-alerts-and-user-activities"></a>調查警示和使用者活動

Azure ATP 的設計目的是減少一般警示干擾，只在簡單的即時組織攻擊時間軸中提供相關的重要安全性警訊。 Azure ATP 的攻擊時間軸檢視，可讓您運用智慧分析的情報，安心專注於重要工作。 使用 Azure ATP 來快速調查威脅，並取得整個組織中使用者、裝置和網路資源的見解。 與 Microsoft Defender ATP 緊密整合，透過可抵禦作業系統上進階持續威脅的額外偵測和防護，提供另一道增強的安全性保障。

## <a name="additional-resources-for-azure-atp"></a>Azure ATP 的其他資源

### <a name="start-a-free-trial"></a>開始使用免費試用版

[https://signup.microsoft.com/Signup?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7&ali=1](https://signup.microsoft.com/Signup?OfferId=87dd2714-d452-48a0-a809-d2f58c4f68b7&ali=1 "Enterprise Mobility + Security E5")

### <a name="follow-azure-atp-on-microsoft-tech-community"></a>追蹤 Microsoft 技術社群的 Azure ATP 專區

[https://techcommunity.microsoft.com/t5/Azure-Advanced-Threat-Protection/bd-p/AzureAdvancedThreatProtection](https://techcommunity.microsoft.com/t5/Azure-Advanced-Threat-Protection/bd-p/AzureAdvancedThreatProtection "Azure ATP on Microsoft Tech Community")

### <a name="join-the-azure-atp-yammer-community"></a>加入 Azure ATP Yammer 社群

[https://www.yammer.com/azureadvisors/#/threads/inGroup?type=in_group&feedId=9386893](https://www.yammer.com/azureadvisors/#/threads/inGroup?type=in_group&feedId=9386893 "Azure ATP Yammer community")

### <a name="visit-the-azure-atp-product-page"></a>瀏覽 Azure ATP 產品頁面

[https://azure.microsoft.com/features/azure-advanced-threat-protection/](https://azure.microsoft.com/features/azure-advanced-threat-protection/ "Azure ATP product page")

### <a name="learn-more-about-azure-atp-architecture"></a>深入了解 Azure ATP 架構

 [Azure ATP 架構](atp-architecture.md)

## <a name="microsoft-ignite"></a>Microsoft Ignite

Microsoft Ignite 2018 會舉辦多場會議，著重探討 [Azure 進階威脅防護](https://myignite.techcommunity.microsoft.com/sessions?q=Azure%2520Advanced%2520Threat%2520Protection&t=%257B%2522from%2522%253A%25222018-09-23T08%253A00%253A00-04%253A00%2522%252C%2522to%2522%253A%25222018-09-28T19%253A00%253A00-04%253A00%2522%257D)。 我們已為會議錄影，因此若您錯過活動，建議您在此觀看：

### <a name="azure-atp"></a>Azure ATP

[BRK3117](https://myignite.techcommunity.microsoft.com/videos/65780) - SecOp and incident response with Azure ATP (使用 Azure ATP 的 SecOp 和事件回應) - 觀看 [YouTube 影片](https://www.youtube.com/watch?v=QXZIfH0wP3Q)

### <a name="azure-atp-and-azure-ad-ip-active-directory-identity-protection"></a>Azure ATP 和 Azure AD IP (Active Directory Identity Protection)

[BRK3237](https://myignite.techcommunity.microsoft.com/videos/64523) - Securing your hybrid cloud environment with Azure AD Identity Protection and Azure ATP (使用 Azure AD Identity Protection 和 Azure ATP 保護您混合式雲端環境的安全) - 觀看 [YouTube 影片](https://www.youtube.com/watch?v=X7CXaok6GbM)

[BRK2157](https://myignite.techcommunity.microsoft.com/videos/65776) - Accelerate deployment and adoption of Microsoft Information Protection solutions (加速 Microsoft 資訊保護解決方案的部署及採用) - 觀看 [YouTube 影片](https://www.youtube.com/watch?v=Foh-XDVbPog)

如需 Ignite 2018 中進行的 Azure ATP 公告摘要，請參閱部落格文章 - [Azure 進階威脅防護擴展整合、偵測及鑑識功能](https://techcommunity.microsoft.com/t5/Enterprise-Mobility-Security/Azure-Advanced-Threat-Protection-Expands-Integrations-Detections/ba-p/262409) \(英文\)

## <a name="whats-next"></a>新功能

建議您分三個階段來部署 Azure ATP：

### <a name="phase-1"></a>階段 1

1. 設定 Azure ATP 以保護您的主要環境。 Azure ATP 的快速部署模型可讓您立即開始保護組織。 [安裝 Azure ATP](install-atp-step1.md)
2. 設定[機密帳戶](sensitive-accounts.md)與 [honeytoken 帳戶](install-atp-step7.md)。
3. 檢閱報告和[橫向移動路徑](use-case-lateral-movement-path.md)。

### <a name="phase-2"></a>階段 2

1. 保護組織中的所有網域控制站和[樹系](atp-multi-forest.md)。
2. 監視所有[警示](working-with-suspicious-activities.md) – 調查橫向移動和網域支配的警示。
3. 使用[安全性警訊指南](suspicious-activity-guide.md)，以了解威脅並對潛在攻擊進行分級。

### <a name="phase-3"></a>階段 3

1. 將 Azure ATP 警示整合至您的 SecOp 工作流程中。

## <a name="see-also"></a>另請參閱

- [Azure ATP 常見問題集](atp-technical-faq.md)
- [使用安全性警訊](working-with-suspicious-activities.md)
- [查看 Azure ATP 論壇！](https://aka.ms/azureatpcommunity)
