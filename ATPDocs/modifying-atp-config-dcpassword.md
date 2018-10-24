---
title: 變更 Azure 進階威脅防護設定 - 網域連線密碼 | Microsoft Docs
description: 描述如何變更 Azure ATP 獨立式感應器上的「網域連線密碼」。
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 10/04/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: e7f065fa-1ad1-4e87-bd80-99cc695efbf5
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: a175a23a087b11d481dbcf055bff4fe5577b4f8e
ms.sourcegitcommit: 27cf312b8ebb04995e4d06d3a63bc75d8ad7dacb
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/04/2018
ms.locfileid: "48783112"
---
適用於：Azure 進階威脅防護



# <a name="change-azure-atp-workspace-portal-configuration---domain-connectivity-password"></a>變更 Azure ATP 工作區入口網站設定 - 網域連線密碼



## <a name="change-the-domain-connectivity-password"></a>變更網域連線密碼
如果您需要修改網域連線密碼，請確定輸入的密碼正確。 如果密碼不正確，所有已部署的感應器都會停止 Azure ATP 感應器服務。

如果您懷疑此情況已發生，請於 Azure ATP 獨立式感應器上的 Microsoft.Tri.sensor-Errors.log 檔案查看下列錯誤︰`The supplied credential is invalid.`

請遵循此程序來更新 Azure ATP 入口網站上的網域連線密碼︰

> [!NOTE]
> 這是來自 Active Directory 內部部署的使用者名稱與密碼，而不是來自 Azure AD。

1.  存取工作區 URL，以開啟 Azure ATP 入口網站。

2.  選取工具列上的 [設定] 選項並選取 [組態]。

    ![Azure ATP 組態設定圖示](media/atp-config-menu.png)

3.  選取 [目錄服務]。

    ![Azure ATP 獨立式感應器變更密碼影像](media/directory-services.png)

4.  在 [密碼] 下，變更密碼。

 > [!NOTE]
 > 在此處輸入 Active Directory 使用者和密碼，而非 Azure Active Directory。

5.  按一下 **[儲存]**。

6.  變更密碼之後，手動檢查 Azure ATP 獨立式感應器服務已在 Azure ATP 獨立式感應器伺服器上執行。

7. 在 Azure ATP 入口網站中，移至 [設定] 下方的 [感應器] 頁面，並檢查感應器狀態。

## <a name="see-also"></a>另請參閱

- [與 Windows Defender ATP 整合](integrate-wd-atp.md)
- [查看 Azure ATP 論壇！](https://aka.ms/azureatpcommunity)