---
title: 使用 Microsoft Defender for Identity 管理敏感性或 honeytoken 帳戶
description: 說明如何使用 Microsoft Defender 身分識別管理敏感性或 honeytoken 帳戶
ms.date: 02/17/2021
ms.topic: how-to
ms.openlocfilehash: 7078e93ad384d81d59a13ff4b527ca59bc678ad2
ms.sourcegitcommit: f92dca4dc3d8a25b1a06f68ac7a9f8318105bcd8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/17/2021
ms.locfileid: "100630763"
---
# <a name="manage-sensitive-or-honeytoken-accounts"></a>管理敏感性或 honeytoken 帳戶

本文說明如何將實體標記套用至敏感性帳戶。 這點很重要，因為某些 [!INCLUDE [Short long](includes/product-short.md)] 偵測（例如敏感性群組修改偵測和橫向移動路徑）會依賴實體的敏感度狀態。

[!INCLUDE [Product short](includes/product-short.md)] 也可讓您設定 honeytoken 帳戶，以做為惡意執行者的陷阱-與這些 honeytoken 帳戶相關聯的任何驗證 (正常休眠) ，會觸發警示。

## <a name="sensitive-entities"></a>機密實體

[!INCLUDE [Short long](includes/product-short.md)] 將下列群組清單視為 **敏感性**。 屬於其中一個 Azure Active Directory 群組成員的任何實體都會被視為機密：

- Administrators
- Power Users
- Account Operators
- Server Operators
- Print Operators
- Backup Operators
- Replicators
- Network Configuration Operators
- Incoming Forest Trust Builders
- Domain Admins
- 網域控制站
- Group Policy Creator Owners
- Read-only Domain Controllers
- 企業唯讀網域控制站
- Schema Admins
- Enterprise Admins
- Microsoft Exchange Servers

  > [!NOTE]
  > 在 2018 年 9 月之前，[!INCLUDE [Product short](includes/product-short.md)] 也會自動將遠端桌面使用者視為敏感性。 在此日期之後新增的遠端桌面實體或群組即不會再自動標示為機密，但此日期之前新增的遠端桌面實體或群組，可能仍會維持機密標示。 您現在可以手動變更這項機密設定。

除了這些群組之外，[!INCLUDE [Product short](includes/product-short.md)] 還會識別下列高價值資產伺服器，並自動將其標記為 **敏感性**：

- 憑證授權單位伺服器
- DHCP 伺服器
- DNS 伺服器
- Microsoft Exchange Server

## <a name="manually-tagging-entities"></a>手動標記實體

您也可以手動將實體標記為敏感性或 honeytoken 帳戶。 如果您手動標記額外的使用者或群組，例如董事會成員、公司主管和銷售主管， [!INCLUDE [Product short](includes/product-short.md)] 則會將其視為機密。

### <a name="to-manually-tag-entities"></a>手動標記實體

若要標記實體，請執行下列動作：

1. 在[!INCLUDE [Product short](includes/product-short.md)] 中，選取 [設定]。

    ![[!包含 [Product short] (include/product-short. md) ] configuration settings](media/config-menu.png)

1. 在 [ **偵測**] 下，選取 [ **實體標記**]。

    ![[!INCLUDE [Product short](includes/product-short.md)] 實體標記](media/entity-tags.png)

1. 針對您想要設定的每個帳戶，執行下列步驟：
    1. 在 [ **Honeytoken 帳戶** 或 **機密**] 下，輸入帳戶名稱。
    1. 按一下加號圖示 **(+)**。

    > [!TIP]
    > [敏感性或 honeytoken 帳戶] 欄位是可搜尋的，而且會自動填入您網路中的實體。

    ![[!INCLUDE [Product short](includes/product-short.md)] 敏感性帳戶範例](media/sensitive-account-sample.png)

1. 按一下 **[儲存]** 。

## <a name="see-also"></a>請參閱

- [處理可疑活動](working-with-suspicious-activities.md)
- [查看[!INCLUDE [Product short](includes/product-short.md)] 論壇！](https://aka.ms/MDIcommunity)\(英文\)
