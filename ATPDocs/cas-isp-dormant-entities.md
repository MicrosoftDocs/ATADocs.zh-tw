---
title: Azure 進階威脅防護休眠實體安全性評量
description: 本文概述敏感性群組身分識別安全性狀態評估報告中 Azure ATP 的休眠實體。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 08/25/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 2fe62047-75ef-4b2e-b4aa-72860e39b4e4
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: db289191d8520a478867c3a2ff3c1b47267e82f1
ms.sourcegitcommit: c7c0a4c9f7507f3e8e0f219798ed7d347c03e792
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/22/2020
ms.locfileid: "90913178"
---
# <a name="security-assessment-dormant-entities-in-sensitive-groups"></a>安全性評估：**從敏感性群組中移除休眠實體**

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

## <a name="what-are-sensitive-dormant-entities"></a>什麼是**敏感性**休眠實體？

Azure ATP 會探索特定使用者是否具**敏感性**，以及提供會呈現為非使用中、已停用或已過期的屬性。

不過，如果**敏感性**帳戶超過 180 天無人使用。也可能會變成*休眠*狀態。 休眠的[敏感性](sensitive-accounts.md)實體是讓惡意執行者取得貴組織敏感存取的機會目標。

## <a name="what-risk-do-dormant-entities-create-in-sensitive-groups"></a>休眠實體在**敏感性**群組中建立的風險為何？

無法保護其休眠使用者帳戶的組織，會使敏感性資料的安全暴露在外。

惡意執行者 (如竊賊) 通常會試圖以最輕鬆且不容易被發現的方式進入環境。 如果要輕鬆且悄悄地進入您的組織，透過不再使用的**敏感性**使用者和服務帳戶是最佳方式。

不管原因是由於員工流失還是資源管理疏失，略過此步驟都會讓貴組織最敏感的實體受到易受攻擊和公開的影響。

## <a name="how-do-i-use-this-security-assessment"></a>我該如何使用這項安全性評估？

1. 使用報告資料表來找出您有哪些敏感性帳戶處於休眠狀態。
1. 對這些使用者帳戶採取合適的動作，例如移除他們的特殊存取權限，或是刪除帳戶。

> [!NOTE]
> 此評定會以近乎即時的方式更新。

## <a name="see-also"></a>另請參閱

- [Cloud App Security 中的 Azure ATP 活動篩選](activities-filtering-mcas.md)
- [查看 Azure ATP 論壇！](https://aka.ms/azureatpcommunity)
