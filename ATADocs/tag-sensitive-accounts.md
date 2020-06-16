---
title: 使用 ATA 標記敏感性帳戶
description: 說明如何使用 Advanced Threat Analytics (ATA) 標記敏感性帳戶
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 6/14/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 40a1c5c4-b8d6-477c-8ae5-562b37661624
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 81924146012b02464f435904593c930eda9f77b9
ms.sourcegitcommit: fbb0768c392f9bccdd7e4adf0e9a0303c8d1922c
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2020
ms.locfileid: "84774990"
---
# <a name="tag-sensitive-accounts"></a>標記敏感性帳戶


*適用於：Advanced Threat Analytics 1.9 版*

您可以手動將群組或帳戶標記為敏感性，以增強偵測。 確實更新此項目對部分 ATA 偵測很重要，例如敏感性群組修改偵測與橫向移動路徑，這將取決於那些群組與帳戶視為具敏感性而定。 在此之前，若實體是特定群組清單的成員，則 ATA 會自動將其標記為敏感性**。 您現在可以手動將其他使用者或群組標記為敏感性，例如董事會成員、公司主管、業務總監等，而 ATA 會將其視為敏感性。

1.  在 ATA 主控台中按一下功能表列上的 [設定]**** 齒輪。

2.  按一下 [偵測]**** 下的 [實體標籤]****。

    ![ATA 實體標籤](media/entity-tags.png)

3.  在 [機密]**** 區段中，輸入 [機密帳戶]**** 和 [機密群組]**** 的名稱，然後按一下 **+** 符號將它們加入。

    ![ATA 敏感性帳戶範例](media/sensitive-account-sample.png)

4. 按一下 [檔案] 。

5. 按一下實體名稱即可前往 [實體設定檔] 頁面。 您在這裡可以看到將實體視為敏感性的原因，原因可能是群組中的成員資格或手動標記為敏感性。


## <a name="sensitive-groups"></a>敏感性群組

ATA 將下列群組清單視為敏感性。 屬於這些群組的任何實體都視為具有敏感性：

-   Administrators
-   進階使用者
-   Account Operators
-   Server Operators
-   Print Operators
-   Backup Operators
-   複寫者
-   Remote Desktop Users 
-   Network Configuration Operators 
-   Incoming Forest Trust Builders
-   Domain Admins
-   網域控制站
-   Group Policy Creator Owners 
-   唯讀網域控制站 
-   企業唯讀網域控制站 
-   Schema Admins 
-   Enterprise Admins
     
## <a name="see-also"></a>另請參閱
[查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
