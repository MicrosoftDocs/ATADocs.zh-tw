---
title: 安裝 Advanced 威脅分析-步驟2
description: 安裝 ATA 的步驟 2 協助您設定 ATA 中心伺服器網域連線設定
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 12/30/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: e1c5ff41-d989-46cb-aa38-5a3938f03c0f
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: fe99921e1193f79f7031c04156a79fd8fa55dc9e
ms.sourcegitcommit: 2be59f0bd4c9fd0d3827e9312ba20aa8eb43c6b5
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88954556"
---
# <a name="install-ata---step-2"></a>安裝 ATA - 步驟 2

*適用於：Advanced Threat Analytics 1.9 版*

> [!div class="step-by-step"]
> [«步驟 1](install-ata-step1.md) 
> [步驟3»](install-ata-step3.md)

## <a name="step-2-provide-a-username-and-password-to-connect-to-your-active-directory-forest"></a>步驟 2： 提供使用者名稱和密碼來連線到您的 Active Directory 樹系

第一次開啟 ATA 主控台時會出現下列畫面︰

![ATA 歡迎階段 1](media/ATA_1.7-welcome-provide-username.png)

1. 輸入下列資訊，然後按一下 [儲存]****：

    |欄位|註解|
    |---------|------------|
    |需要 (使用者**名稱**) |輸入唯讀使用者名稱，例如︰**ATAuser**。 **注意：** 請勿 **將 UPN 格式用於您** 的使用者名稱。|
    |需要**密碼** () |輸入唯讀使用者的密碼，例如︰**Pencil1**。|
    |**網域** (必填)|輸入唯讀使用者的網域，例如︰**contoso.com**。 **注意︰** 您務必輸入使用者所在網域的完整 FQDN。 例如，如果使用者的帳戶位於網域 corp.contoso.com，您就必須輸入 `corp.contoso.com` not contoso.com|

1. 您可以按一下 [測試連線]****，以測試網域的連線，並檢查提供的認證有提供存取權。 這在 ATA 中心具有網域連線時有效。

    儲存之後，主控台中的歡迎訊息會變更成下列訊息︰![ATA 歡迎階段 1 完成](media/ATA_1.7-welcome-provide-username-finished.png)

1. 在主控台中，按一下 [下載閘道安裝程式並安裝第一個閘道]**** 繼續。

> [!div class="step-by-step"]
> [«步驟 1](install-ata-step1.md) 
> [步驟3»](install-ata-step3.md)

## <a name="related-videos"></a>相關影片

- [ATA 部署概觀](https://channel9.msdn.com/Shows/Microsoft-Security/Overview-of-ATA-Deployment-in-10-Minutes)
- [選擇正確的 ATA 閘道類型](https://channel9.msdn.com/Shows/Microsoft-Security/ATA-Deployment-Choose-the-Right-Gateway-Type)

## <a name="see-also"></a>另請參閱

- [ATA POC 部署指南](https://aka.ms/atapoc)
- [ATA 調整大小工具](https://aka.ms/atasizingtool)
- [查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [設定事件收集](configure-event-collection.md)
- [ATA 必要條件](ata-prerequisites.md)
