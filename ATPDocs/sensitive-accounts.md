---
title: 使用 Azure ATP 標記機密帳戶
description: 描述如何使用 Azure 進階威脅防護 (ATP) 標記機密帳戶
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 02/16/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 43e57f87-ca85-4922-8ed0-9830139fe7cb
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: e033e2b3b99664513fcaac04059dbbb27c380665
ms.sourcegitcommit: c7c0a4c9f7507f3e8e0f219798ed7d347c03e792
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/22/2020
ms.locfileid: "90912594"
---
# <a name="working-with-sensitive-accounts"></a>使用機密帳戶

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

## <a name="sensitive-entities"></a>機密實體

Azure ATP 將下列群組清單視為**機密**。 屬於任一這些群組的任何實體都會被視為機密：

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
  > 在 2018 年 9 月之前，Azure ATP 也會自動將遠端桌面使用者視為機密。 在此日期之後新增的遠端桌面實體或群組即不會再自動標示為機密，但此日期之前新增的遠端桌面實體或群組，可能仍會維持機密標示。 您現在可以手動變更這項機密設定。

除了這些群組之外，Azure ATP 還會識別下列高價值資產伺服器，並自動將其標記為**機密**：

- 憑證授權單位伺服器
- DHCP 伺服器
- DNS 伺服器
- Microsoft Exchange Server

## <a name="tagging-sensitive-accounts"></a>標記機密帳戶

除了這些群組，您可以手動將群組或帳戶標記為機密，以增強偵測。 這一點很重要，因為部分 Azure ATP 偵測 (例如機密群組修改偵測和橫向移動路徑) 仰賴於哪些群組和帳戶被視為機密。 您可以手動將其他使用者或群組標記為機密，例如董事會成員、公司主管、業務總監等，而 Azure ATP 會將他們視為機密。

1. 在 Azure ATP 入口網站中，按一下功能表列的 [設定]  齒輪。

1. 在 [偵測]  下，按一下 [實體標記]  。

    ![Azure ATP 實體標記](media/entity-tags.png)

1. 在 [機密]  區段中，輸入 [機密帳戶]  和 [機密群組]  的名稱，然後按一下 **+** 符號將它們加入。

    ![Azure ATP 機密帳戶範例](media/sensitive-account-sample.png)

1. 按一下 **[儲存]** 。

## <a name="see-also"></a>請參閱

- [處理可疑活動](working-with-suspicious-activities.md)
- [查看 Azure ATP 論壇！](https://aka.ms/azureatpcommunity)
