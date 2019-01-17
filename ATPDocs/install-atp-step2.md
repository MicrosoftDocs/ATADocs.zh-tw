---
title: 安裝 Azure 進階威脅防護 | Microsoft Docs
description: 安裝 Azure ATP 的步驟 2 可協助您設定 Azure ATP 雲端服務上的網域連線設定
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 12/30/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: ae8a95f0-278c-4a12-ae69-14282364fba1
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 6ee7bbe48181b55ba93e24e9ac4dd5c9f7d0b59f
ms.sourcegitcommit: 1bdaccbddf2896be517885fbcee1c2bc47f4de8d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/30/2018
ms.locfileid: "53815068"
---
適用對象：*Azure 進階威脅防護*



# <a name="install-azure-atp---step-2"></a>安裝 Azure ATP - 步驟 2

> [!div class="step-by-step"]
> [« 步驟 1](install-atp-step1.md)
> [步驟 3 »](install-atp-step3.md)

## <a name="step-2-provide-a-username-and-password-to-connect-to-your-active-directory-forest"></a>步驟 2： 提供使用者名稱和密碼來連線到您的 Active Directory 樹系

當您第一次開啟 Azure ATP 入口網站時，會出現下列畫面：

![Azure ATP 歡迎使用階段 1](media/directory-services.png)

> [!IMPORTANT]
> 這裡的使用者認證必須是在內部部署 Active Directory 中的使用者帳戶。 


1.  輸入下列資訊，然後按一下 [儲存]：

    |欄位|註解|
    |---------|------------|
    |**使用者名稱** (必填)|輸入唯讀 Active Directory 使用者名稱，例如：**ATPuser**。 **注意︰** **請勿**使用 UPN 作為使用者名稱的格式。|
    |**密碼** (必填)|輸入唯讀使用者的密碼，例如︰**Pencil1**。|
    |**網域** (必填)|輸入唯讀使用者的網域，例如︰**contoso.com**。 **注意︰** 請務必輸入使用者所在網域的完整 FQDN。 例如，如果使用者的帳戶是在 corp.contoso.com 網域中，您需要輸入 `corp.contoso.com`，而非 contoso.com|

3. 在 Azure ATP 入口網站中，按一下 [下載感應器安裝程式並安裝第一個感應器] 以繼續。


> [!div class="step-by-step"]
> [« 步驟 1](install-atp-step1.md)
> [步驟 3 »](install-atp-step3.md)


## <a name="see-also"></a>另請參閱
- [Azure ATP 調整大小工具](http://aka.ms/aatpsizingtool) \(英文\)
- [設定事件收集](configure-event-collection.md)
- [Azure ATP 必要條件](atp-prerequisites.md)
- [查看 Azure ATP 論壇！](https://aka.ms/azureatpcommunity)