---
title: "安裝 Advanced Threat Analytics - 步驟 2 | Microsoft Docs"
description: "安裝 ATA 的步驟 2 協助您設定 ATA 中心伺服器網域連線設定"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 07/2/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: e1c5ff41-d989-46cb-aa38-5a3938f03c0f
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: aa5e752fa10644165cb70d2cd8c08a1145261edb
ms.sourcegitcommit: fa50f37b134d7579d7c310852dff60e5f1996eaa
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/03/2017
---
適用於︰Advanced Threat Analytics 1.8 版



# <a name="install-ata---step-2"></a>安裝 ATA - 步驟 2

>[!div class="step-by-step"]
[« 步驟 1](install-ata-step1.md)
[步驟 3 »](install-ata-step3.md)

## <a name="step-2-provide-a-username-and-password-to-connect-to-your-active-directory-forest"></a>步驟 2： 提供使用者名稱和密碼來連線到您的 Active Directory 樹系

第一次開啟 ATA 主控台時會出現下列畫面︰

![ATA 歡迎階段 1](media/ATA_1.7-welcome-provide-username.png)

1.  輸入下列資訊，然後按一下 [儲存]：

    |欄位|註解|
    |---------|------------|
    |**使用者名稱** (必填)|輸入唯讀使用者名稱，例如︰**ATAuser**。|
    |**密碼** (必填)|輸入唯讀使用者的密碼，例如︰**Pencil1**。|
    |**網域** (必填)|輸入唯讀使用者的網域，例如︰**contoso.com**。 **注意︰**您務必輸入使用者所在網域的完整 FQDN。 例如，如果使用者的帳戶是在 corp.contoso.com 網域中，您需要輸入 `corp.contoso.com`，而非 contoso.com|

2. 您可以按一下 [測試連線]，以測試網域的連線，並檢查提供的認證有提供存取權。 這只在 ATA 中心具有網域連線時有效。   

    儲存之後，主控台中的歡迎訊息會變更如下︰![ATA 歡迎階段 1 完成](media/ATA_1.7-welcome-provide-username-finished.png)

3. 在主控台中，按一下 [下載閘道安裝程式並安裝第一個閘道] 繼續。


>[!div class="step-by-step"]
[« 步驟 1](install-ata-step1.md)
[步驟 3 »](install-ata-step3.md)


## <a name="see-also"></a>另請參閱

- [查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [設定事件收集](configure-event-collection.md)
- [ATA 必要條件](ata-prerequisites.md)
