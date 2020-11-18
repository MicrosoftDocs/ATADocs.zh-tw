---
title: 適用于身分識別風險最高的 Microsoft Defender 橫向移動路徑評量
description: 本文概述使用風險最高橫向移動路徑身分識別安全性狀態評估報告的身分識別敏感性實體 Microsoft Defender。
keywords: ''
author: shsagir
ms.author: shsagir
manager: rkarlin
ms.date: 10/26/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 40175ace8046ae7b0edb77f4cac6e036eed997e7
ms.sourcegitcommit: e2227c0b0e5aaa5163dc56d4131ca82f8dca8fb0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2020
ms.locfileid: "94848341"
---
# <a name="security-assessment-riskiest-lateral-movement-paths-lmp"></a>安全性評估：風險最高的橫向移動路徑 (LMP)

## <a name="what-are-risky-lateral-movement-paths"></a>有風險的橫向移動路徑是指什麼？

[!INCLUDE [Product long](includes/product-long.md)] 持續監視您的環境，以使用公開安全性風險的風險最高橫向移動路徑來識別 **敏感性** 帳戶，並報告這些帳戶以協助您管理環境。 若路徑有三個以上的非敏感性帳戶，可能讓惡意行動者對 **敏感性** 帳戶進行認證竊取，該路徑即視為有風險的路徑。

深入了解 LMP：

- [[!INCLUDE [Product short](includes/product-short.md)] 橫向移動路徑 (Lmp) ](use-case-lateral-movement-path.md)
- [MITRE ATT&CK Lateral Movement](https://attack.mitre.org/tactics/TA0008/) (橫向移動)

## <a name="what-risk-do-risky-lateral-movement-paths-pose"></a>有風險的橫向移動路徑會造成什麼風險？

無法保護 **敏感性** 帳戶的組織，會對惡意行動者毫無防備。

惡意執行者 (如竊賊) 通常會試圖以最輕鬆且不容易被發現的方式進入環境。 橫向移動路徑有風險的敏感性帳戶，會讓攻擊者有機可乘，因而暴露在風險中。

例如，攻擊者較容易發現風險最高的路徑，若入侵成功，就可以存取貴組織最敏感的實體。

## <a name="how-do-i-use-this-security-assessment"></a>我該如何使用這項安全性評估？

1. 使用報告資料表找出哪些 **敏感性** 帳戶有具風險的 LMP。
    ![查看熱門的受影響實體並建立動作計畫](media/cas-isp-riskiest-lmp-1.png)
1. 採取適當的動作：
    - 依建議從群組中移除實體。
    - 依建議移除實體在裝置上的本機系統管理員權限。

    > [!NOTE]
    > 請等候 24 小時，然後檢查建議是否已從清單中消失。

> [!NOTE]
> 此評定會每隔 24 小時更新一次。

## <a name="see-also"></a>另請參閱

- [[!INCLUDE [Product short](includes/product-short.md)] Cloud App Security 中的活動篩選](activities-filtering-mcas.md)
- [查看[!INCLUDE [Product short](includes/product-short.md)] 論壇！](https://aka.ms/MDIcommunity)\(英文\)
