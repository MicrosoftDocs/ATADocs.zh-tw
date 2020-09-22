---
title: 變更 Azure 進階威脅防護設定-網域連線密碼
description: 描述如何變更 Azure ATP 獨立式感應器上的「網域連線密碼」。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 02/19/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: e7f065fa-1ad1-4e87-bd80-99cc695efbf5
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 810268ea0661bac47ee7735f0508ed4295d2cc3b
ms.sourcegitcommit: c7c0a4c9f7507f3e8e0f219798ed7d347c03e792
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/22/2020
ms.locfileid: "90912065"
---
# <a name="change-azure-atp-portal-configuration---domain-connectivity-password"></a>變更 Azure ATP 入口網站設定 - 網域連線能力密碼

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

## <a name="change-the-domain-connectivity-password"></a>變更網域連線密碼

如果您需要修改網域連線密碼，請確定輸入的密碼正確。 如果密碼不正確，所有已部署的感應器都會停止 Azure ATP 感應器服務。

如果您懷疑發生這種情況，請查看 Microsoft.tri.sensor-errors.log 記錄檔以取得下列錯誤： `The supplied credential is invalid.`

請遵循此程序來更新 Azure ATP 入口網站上的網域連線密碼︰

> [!NOTE]
> 這是來自 Active Directory 內部部署的使用者名稱與密碼，而不是來自 Azure AD。

1. 存取入口網站 URL，以開啟 Azure ATP 入口網站。

1. 選取工具列上的 [設定] 選項並選取 [組態]****。

    ![Azure ATP 組態設定圖示](media/atp-config-menu.png)

1. 選取 [目錄服務]****。

    ![Azure ATP 獨立式感應器變更密碼影像](media/directory-services.png)

1. 在 [密碼]**** 下，變更密碼。

    > [!NOTE]
    > 在此處輸入 Active Directory 使用者和密碼，而非 Azure Active Directory。

1. 按一下 [檔案]  。

1. 在 Azure ATP 入口網站中，移至 [設定]**** 下方的 [感應器]**** 頁面，並檢查感應器狀態。

## <a name="see-also"></a>另請參閱

- [與 Microsoft Defender ATP 整合](integrate-msde.md)
- [查看 Azure ATP 論壇！](https://aka.ms/azureatpcommunity)