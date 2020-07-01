---
title: Azure 進階威脅防護風險最高的橫向移動路徑評定
description: 本文概述 Azure ATP 敏感性實體具有風險最高橫向移動路徑的身分識別安全性態勢評定報告。
keywords: ''
author: shsagir
ms.author: shsagir
manager: rkarlin
ms.date: 06/23/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 2fe62047-75ef-4b2e-b4aa-72860e39b4e4
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 85e14135fed9a36279fbf615618f614e71ef9c18
ms.sourcegitcommit: 2b8b727b11227aa6b665ba9e02ffa700a2dc33c6
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/29/2020
ms.locfileid: "85516905"
---
# <a name="security-assessment-riskiest-lateral-movement-paths-lmp"></a>安全性評估：風險最高的橫向移動路徑 (LMP)

## <a name="what-are-risky-lateral-movement-paths"></a>有風險的橫向移動路徑是指什麼？

Azure ATP 會持續監視您的環境，辨識橫向移動路徑風險最高而造成安全性風險的**敏感性**帳戶，並針對這些帳戶提出報告，以協助您管理環境。 若路徑有三個以上的非敏感性帳戶，可能讓惡意行動者對**敏感性**帳戶進行認證竊取，該路徑即視為有風險的路徑。

深入了解 LMP：

- [Azure ATP 橫向移動路徑 (LMP)](use-case-lateral-movement-path.md)
- [MITRE ATT&CK Lateral Movement](https://attack.mitre.org/tactics/TA0008/) (橫向移動)

## <a name="what-risk-do-risky-lateral-movement-paths-pose"></a>有風險的橫向移動路徑會造成什麼風險？

無法保護**敏感性**帳戶的組織，會對惡意行動者毫無防備。

惡意執行者 (如竊賊) 通常會試圖以最輕鬆且不容易被發現的方式進入環境。 橫向移動路徑有風險的敏感性帳戶，會讓攻擊者有機可乘，因而暴露在風險中。

例如，攻擊者較容易發現風險最高的路徑，若入侵成功，就可以存取貴組織最敏感的實體。

## <a name="how-do-i-use-this-security-assessment"></a>我該如何使用這項安全性評估？

1. 使用報告資料表找出哪些**敏感性**帳戶有具風險的 LMP。
    ![查看熱門的受影響實體並建立動作計畫](media/atp-cas-isp-riskiest-lmp-1.png)
1. 採取適當的動作：
    - 依建議從群組中移除實體。
    - 依建議移除實體在裝置上的本機系統管理員權限。

    > [!NOTE]
    > 請等候 24 小時，然後檢查建議是否已從清單中消失。

## <a name="see-also"></a>另請參閱

- [Cloud App Security 中的 Azure ATP 活動篩選](atp-activities-filtering-mcas.md)
- [查看 Azure ATP 論壇！](https://aka.ms/azureatpcommunity)
