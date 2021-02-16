---
title: 變更身分識別設定的 Microsoft Defender-網域連線能力密碼
description: 說明如何針對身分識別獨立感應器變更 Microsoft Defender 的網域連線密碼。
ms.date: 10/26/2020
ms.topic: how-to
ms.openlocfilehash: 2a82226a4eda3a7db762df4e04728848f7e1958e
ms.sourcegitcommit: a892419a5cb95412e4643c35a9a72092421628ec
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/16/2021
ms.locfileid: "100533812"
---
# <a name="change-microsoft-defender-for-identity-portal-configuration---domain-connectivity-password"></a>變更適用于身分識別入口網站設定的 Microsoft Defender-網域連線能力密碼

## <a name="change-the-domain-connectivity-password"></a>變更網域連線密碼

如果您需要修改網域連線密碼，請確定輸入的密碼正確。 如果不是，就會 [!INCLUDE [Product long](includes/product-long.md)] 停止所有已部署感應器的感應器服務。

如果您懷疑發生這種情況，請查看 Microsoft.tri.sensor-errors.log 記錄檔以取得下列錯誤： `The supplied credential is invalid.`

請遵循此程式來更新入口網站上的網域連線密碼 [!INCLUDE [Product short](includes/product-short.md)] ：

> [!NOTE]
> 這是來自 Active Directory 內部部署的使用者名稱與密碼，而不是來自 Azure AD。

1. [!INCLUDE [Product short](includes/product-short.md)]存取入口網站 URL 以開啟入口網站。

1. 選取工具列上的 [設定] 選項並選取 [組態]。

    ![[!INCLUDE [Product short](includes/product-short.md)] 組態設定圖示](media/config-menu.png)

1. 選取 [目錄服務]。

    ![[!包含 [產品簡短] (包含/產品簡短的 md) ] 獨立感應器變更密碼影像](media/directory-services.png)

1. 在 [密碼] 下，變更密碼。

    > [!NOTE]
    > 在此處輸入 Active Directory 使用者和密碼，而非 Azure Active Directory。

1. 按一下 [儲存]。

1. 在[!INCLUDE [Product short](includes/product-short.md)] 中，選取 [設定]。
1. 在 [ **系統**] 下，選取 [ **感應器** ] 頁面，並檢查感應器的狀態。

## <a name="see-also"></a>另請參閱

- [與端點的 Microsoft Defender 整合](integrate-mde.md)
- [查看[!INCLUDE [Product short](includes/product-short.md)] 論壇！](https://aka.ms/MDIcommunity)\(英文\)
