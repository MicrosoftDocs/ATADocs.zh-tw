---
title: 使用適用於身分識別的 Microsoft Defender 標記敏感性帳戶
description: 描述如何使用適用於身分識別的 Microsoft Defender 標記敏感性帳戶
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 10/27/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 74e97750d25f48522d38246337682e0399d24c4d
ms.sourcegitcommit: f434dbff577d9944df18ca7533d026acdab0bb42
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/03/2020
ms.locfileid: "93274472"
---
# <a name="working-with-sensitive-accounts"></a>使用機密帳戶

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

## <a name="sensitive-entities"></a>機密實體

[!INCLUDE [Product long](includes/product-long.md)] 將下列群組清單視為 **敏感性** 。 屬於任一這些群組的任何實體都會被視為機密：

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
- 唯讀網域控制站
- 企業唯讀網域控制站
- Schema Admins
- Enterprise Admins
- Microsoft Exchange Servers

  > [!NOTE]
  > 在 2018 年 9 月之前，[!INCLUDE [Product short](includes/product-short.md)] 也會自動將遠端桌面使用者視為敏感性。 在此日期之後新增的遠端桌面實體或群組即不會再自動標示為機密，但此日期之前新增的遠端桌面實體或群組，可能仍會維持機密標示。 您現在可以手動變更這項機密設定。

除了這些群組之外，[!INCLUDE [Product short](includes/product-short.md)] 還會識別下列高價值資產伺服器，並自動將其標記為 **敏感性** ：

- 憑證授權單位伺服器
- DHCP 伺服器
- DNS 伺服器
- Microsoft Exchange Server

## <a name="tagging-sensitive-accounts"></a>標記機密帳戶

除了這些群組，您可以手動將群組或帳戶標記為機密，以增強偵測。 這一點很重要，因為某些[!INCLUDE [Product short](includes/product-short.md)] 偵測 (例如敏感性群組修改偵測與橫向移動路徑) 仰賴於哪些群組和帳戶被視為敏感性。 您可以手動將其他使用者或群組標記為敏感性，例如董事會成員、公司主管、業務總監等，而[!INCLUDE [Product short](includes/product-short.md)] 會將他們視為敏感性。

1. 在[!INCLUDE [Product short](includes/product-short.md)] 中，選取 [設定]。

1. 在 [偵測]  下，按一下 [實體標記]  。

    ![[!INCLUDE [Product short](includes/product-short.md)] 實體標記](media/entity-tags.png)

1. 在 [機密]  區段中，輸入 [機密帳戶]  和 [機密群組]  的名稱，然後按一下 **+** 符號將它們加入。

    ![[!INCLUDE [Product short](includes/product-short.md)] 敏感性帳戶範例](media/sensitive-account-sample.png)

1. 按一下 **[儲存]** 。

## <a name="see-also"></a>請參閱

- [處理可疑活動](working-with-suspicious-activities.md)
- [查看[!INCLUDE [Product short](includes/product-short.md)] 論壇！](https://aka.ms/MDIcommunity)\(英文\)
