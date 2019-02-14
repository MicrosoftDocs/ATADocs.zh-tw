---
title: 使用 Azure ATP 標記機密帳戶 | Microsoft Docs
description: 描述如何使用 Azure 進階威脅防護 (ATP) 標記機密帳戶
keywords: ''
author: mlottner
ms.author: mlottner
manager: barbkess
ms.date: 10/04/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 43e57f87-ca85-4922-8ed0-9830139fe7cb
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: d5d7cc89303adf1113811d525f6f0f0a4711ffde
ms.sourcegitcommit: 78748bfd75ae68230d72ad11010ead37d96b0c58
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/12/2019
ms.locfileid: "56075615"
---
# <a name="working-with-sensitive-accounts"></a>使用機密帳戶

## <a name="sensitive-groups"></a>敏感性群組

Azure ATP 將下列群組清單視為「機密」。 屬於這些群組的任何實體都視為具有敏感性：

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

  > [!NOTE]
  > 在 2018 年 9 月之前，Azure ATP 也會自動將遠端桌面使用者視為機密。 在此日期之後新增的遠端桌面實體或群組即不會再自動標示為機密，但此日期之前新增的遠端桌面實體或群組，可能仍會維持機密標示。 您現在可以手動變更這項機密設定。  

## <a name="tagging-sensitive-accounts"></a>標記機密帳戶

除了這些群組，您可以手動將群組或帳戶標記為機密，以增強偵測。 這一點很重要，因為部分 Azure ATP 偵測 (例如機密群組修改偵測和橫向移動路徑) 會仰賴於哪些群組和帳戶被視為機密。 您可以手動將其他使用者或群組標記為機密，例如董事會成員、公司主管、業務總監等，而 Azure ATP 會將他們視為機密。

1.  在 Azure ATP 入口網站中，按一下功能表列的 [設定] 齒輪。

2.  在 [偵測] 下，按一下 [實體標記]。

    ![Azure ATP 實體標記](media/entity-tags.png)

3.  在 [機密] 區段中，輸入 [機密帳戶] 和 [機密群組] 的名稱，然後按一下 **+** 符號將它們加入。

    ![Azure ATP 機密帳戶範例](media/sensitive-account-sample.png)

4. 按一下 **[儲存]**。

    
## <a name="see-also"></a>請參閱

- [處理可疑活動](working-with-suspicious-activities.md)
- [查看 Azure ATP 論壇！](https://aka.ms/azureatpcommunity)