---
title: 適用于身分識別休眠實體安全性評定的 Microsoft Defender
description: 本文概述 Microsoft Defender 身分識別在敏感性群組中的休眠實體身分識別安全性狀態評估報告。
ms.date: 10/26/2020
ms.topic: how-to
ms.openlocfilehash: e96b7af917f898c7ef9f701b7e7ffda1cf001598
ms.sourcegitcommit: cdb7ae4580851e25aae24d07e7d66a750aa54405
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2020
ms.locfileid: "96544193"
---
# <a name="security-assessment-dormant-entities-in-sensitive-groups"></a>安全性評估：**從敏感性群組中移除休眠實體**

## <a name="what-are-sensitive-dormant-entities"></a>什麼是 **敏感性** 休眠實體？

[!INCLUDE [Product long](includes/product-long.md)] 探索特定使用者是否 **敏感性** ，以及提供屬性以呈現非使用中、已停用或已過期。

不過，如果 **敏感性** 帳戶超過 180 天無人使用。也可能會變成 *休眠* 狀態。 休眠的[敏感性](sensitive-accounts.md)實體是讓惡意執行者取得貴組織敏感存取的機會目標。

## <a name="what-risk-do-dormant-entities-create-in-sensitive-groups"></a>休眠實體在 **敏感性** 群組中建立的風險為何？

無法保護其休眠使用者帳戶的組織，會使敏感性資料的安全暴露在外。

惡意執行者 (如竊賊) 通常會試圖以最輕鬆且不容易被發現的方式進入環境。 您組織的簡單且無訊息的路徑，是透過不再使用的 **敏感性** 使用者和服務帳戶。

不管原因是由於員工流失還是資源管理疏失，略過此步驟都會讓貴組織最敏感的實體受到易受攻擊和公開的影響。

## <a name="how-do-i-use-this-security-assessment"></a>我該如何使用這項安全性評估？

1. 使用報告資料表來找出您有哪些敏感性帳戶處於休眠狀態。
    ![修復休眠實體 ini 敏感性群組](media/cas-isp-dormant-entities-sensitive-groups-1.png)
1. 對這些使用者帳戶採取合適的動作，例如移除他們的特殊存取權限，或是刪除帳戶。

> [!NOTE]
> 此評定會以近乎即時的方式更新。

## <a name="see-also"></a>另請參閱

- [[!INCLUDE [Product short](includes/product-short.md)] Cloud App Security 中的活動篩選](activities-filtering-mcas.md)
- [查看[!INCLUDE [Product short](includes/product-short.md)] 論壇！](https://aka.ms/MDIcommunity)\(英文\)
