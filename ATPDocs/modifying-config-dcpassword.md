---
title: 變更身分識別設定的 Microsoft Defender-網域連線能力密碼
description: 說明如何針對身分識別獨立感應器變更 Microsoft Defender 的網域連線密碼。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 10/26/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: b9dcd871fecd855a35a530f57c020fba5f3d1347
ms.sourcegitcommit: f434dbff577d9944df18ca7533d026acdab0bb42
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/03/2020
ms.locfileid: "93275870"
---
# <a name="change-product-long-portal-configuration---domain-connectivity-password"></a>變更 [!INCLUDE [Product long](includes/product-long.md)] 入口網站設定-網域連線密碼

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

## <a name="change-the-domain-connectivity-password"></a>變更網域連線密碼

如果您需要修改網域連線密碼，請確定輸入的密碼正確。 如果不是，就會 [!INCLUDE [Product long](includes/product-long.md)] 停止所有已部署感應器的感應器服務。

如果您懷疑發生這種情況，請查看 Microsoft.tri.sensor-errors.log 記錄檔以取得下列錯誤： `The supplied credential is invalid.`

請遵循此程式來更新入口網站上的網域連線密碼 [!INCLUDE [Product short](includes/product-short.md)] ：

> [!NOTE]
> 這是來自 Active Directory 內部部署的使用者名稱與密碼，而不是來自 Azure AD。

1. [!INCLUDE [Product short](includes/product-short.md)]存取入口網站 URL 以開啟入口網站。

1. 選取工具列上的 [設定] 選項並選取 [組態]。

    ![[!包含 [Product short] (include/product-short. md) ] configuration settings 圖示](media/config-menu.png)

1. 選取 [目錄服務]。

    ![[!包含 [產品簡短] (包含/產品簡短的 md) ] 獨立感應器變更密碼影像](media/directory-services.png)

1. 在 [密碼] 下，變更密碼。

    > [!NOTE]
    > 在此處輸入 Active Directory 使用者和密碼，而非 Azure Active Directory。

1. 按一下 [檔案]  。

1. 在 [!INCLUDE [Product short](includes/product-short.md)] 入口網站中， **Configuration** 選取 [設定]。
1. 在 [ **系統** ] 下，選取 [ **感應器** ] 頁面，並檢查感應器的狀態。

## <a name="see-also"></a>另請參閱

- [與 Microsoft Defender for Endpoint 整合](integrate-mde.md)
- [查看 [!INCLUDE [Product short](includes/product-short.md)] 論壇！](https://aka.ms/MDIcommunity)
