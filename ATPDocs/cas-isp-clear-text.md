---
title: 適用于身分識別純文字曝光評定的 Microsoft Defender
description: 本文概述 Microsoft Defender 身分識別的純文字公開身分識別安全性狀態評估報告。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 08/25/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 6a5d110d35ad3b49205d4c0b7b03412fe26626ae
ms.sourcegitcommit: e2227c0b0e5aaa5163dc56d4131ca82f8dca8fb0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2020
ms.locfileid: "94848783"
---
# <a name="security-assessment-entities-exposing-credentials-in-clear-text"></a>安全性評估：實體以純文字公開認證

![防止純文字認證暴露](media/cas-isp-clear-text-1.png)

## <a name="what-information-does-the-prevent-clear-text-security-assessment-provide"></a>防止純文字安全性評估提供哪些資訊？

此安全性評估會針對以純文字公開認證的任何實體監視您的流量，並使用建議的補救功能向您的組織中目前的暴露風險 (最受影響的實體) 發出警示。

## <a name="why-is-clear-text-credential-exposure-risky"></a>為什麼純文字認證暴露具有風險？

以純文字公開認證的實體，不僅對有問題的公開實體有風險，也會威脅到整個組織。

增加的風險是因為不安全的流量 (例如 LDAP 簡單繫結) 很容易遭到攻擊者攔截攻擊。 這些類型的攻擊會導致惡意活動，包括認證暴露，攻擊者可以利用認證來因應惡意用途。

## <a name="how-do-i-use-this-security-assessment-to-improve-my-organizational-security-posture"></a>如何使用此安全性評估來改善我的組織安全性狀態？

1. 檢閱受影響實體的安全性評估。
    ![查看熱門的受影響實體並建立動作計畫](media/cas-isp-clear-text-2.png)
1. 研究為何那些實體會以純文字使用 LDAP。
1. 修復問題並停止暴露。
1. 確認補救之後，建議您要求網域控制站層級 LDAP 簽署。 若要深入了解 LDAP 伺服器簽署, 請[參閱網域控制站 LDAP 伺服器簽署 ](/windows/security/threat-protection/security-policy-settings/domain-controller-ldap-server-signing-requirements)需求。

> [!NOTE]
> 此評定會以近乎即時的方式更新。

## <a name="next-steps"></a>後續步驟

- [[!INCLUDE [Product short](includes/product-short.md)] Cloud App Security 中的活動篩選](activities-filtering-mcas.md)
- [查看[!INCLUDE [Product short](includes/product-short.md)] 論壇！](https://aka.ms/MDIcommunity)\(英文\)