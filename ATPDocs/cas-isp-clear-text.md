---
title: Azure 進階威脅防護純文字暴露評估
description: 本文提供 Azure ATP 的「純文字公開身分識別」安全性狀態評估報告的總覽。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 08/25/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 124957bb-5882-4fcf-bab2-b74b0c69571d
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 413e7482900f34428056401085f04195ccb4e720
ms.sourcegitcommit: c7c0a4c9f7507f3e8e0f219798ed7d347c03e792
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/22/2020
ms.locfileid: "90913227"
---
# <a name="security-assessment-entities-exposing-credentials-in-clear-text"></a>安全性評估：實體以純文字公開認證

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

![防止純文字認證暴露](media/atp-cas-isp-clear-text-1.png)

## <a name="what-information-does-the-prevent-clear-text-security-assessment-provide"></a>防止純文字安全性評估提供哪些資訊？

此安全性評估會針對以純文字公開認證的任何實體監視您的流量，並使用建議的補救功能向您的組織中目前的暴露風險 (最受影響的實體) 發出警示。

## <a name="why-is-clear-text-credential-exposure-risky"></a>為什麼純文字認證暴露具有風險？

以純文字公開認證的實體，不僅對有問題的公開實體有風險，也會威脅到整個組織。

增加的風險是因為不安全的流量 (例如 LDAP 簡單繫結) 很容易遭到攻擊者攔截攻擊。 這些類型的攻擊會導致惡意活動，包括認證暴露，攻擊者可以利用認證來因應惡意用途。

## <a name="how-do-i-use-this-security-assessment-to-improve-my-organizational-security-posture"></a>如何使用此安全性評估來改善我的組織安全性狀態？

1. 檢閱受影響實體的安全性評估。
    ![查看熱門的受影響實體並建立動作計畫](media/atp-cas-isp-clear-text-2.png)
1. 研究為何那些實體會以純文字使用 LDAP。
1. 修復問題並停止暴露。
1. 確認補救之後，建議您要求網域控制站層級 LDAP 簽署。 若要深入了解 LDAP 伺服器簽署, 請[參閱網域控制站 LDAP 伺服器簽署 ](/windows/security/threat-protection/security-policy-settings/domain-controller-ldap-server-signing-requirements)需求。

> [!NOTE]
> 此評定會以近乎即時的方式更新。

## <a name="next-steps"></a>後續步驟

- [Cloud App Security 中的 Azure ATP 活動篩選](activities-filtering-mcas.md)
- [查看 Azure ATP 論壇！](https://aka.ms/azureatpcommunity)