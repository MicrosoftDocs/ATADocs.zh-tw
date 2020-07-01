---
title: Azure 進階威脅防護的不安全 SID History 屬性評定
description: 本文概述不安全 SID History 屬性身分識別安全性狀態評定報表中的 Azure ATP 實體。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 04/30/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 2fe62047-75ef-4b2e-b4aa-72860e39b4e4
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: f10756f3b5fc009e2bd37fff9eff04d1c5c41585
ms.sourcegitcommit: 073154998f5fdfbefe276888ffb034dfce368662
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/23/2020
ms.locfileid: "85256264"
---
# <a name="security-assessment-unsecure-sid-history-attributes"></a>安全性評估：不安全的 SID History 屬性

## <a name="what-is-an-unsecure-sid-history-attribute"></a>什麼是不安全的 SID History 屬性？

SID History 是支援[移轉案例](/previous-versions/windows/it-pro/windows-server-2003/cc779590(v=ws.10))的屬性。 每個使用者帳戶都有相關聯的[安全性識別碼 (SID)](/windows/win32/secauthz/security-identifiers)，可在連線到資源時，用於追蹤其安全性主體及該帳戶所擁有的存取權。 SID History 可將另一個帳戶的存取權有效複製到其他帳戶，非常適合使用者在網域間移動 (移轉) 時以確保保留存取權。

評定會檢查帳戶是否有 Azure ATP 分析後認為有風險的 SID History 屬性。

## <a name="what-risk-does-unsecure-sid-history-attribute-pose"></a>不安全的 SID History 屬性會造成什麼風險？

無法保護其帳戶屬性的組織對惡意源起方毫無防備。

惡意執行者 (如竊賊) 通常會試圖以最輕鬆且不容易被發現的方式進入環境。 帳戶若設定了不安全的 SID History 屬性，就會讓攻擊者有機可趁，而且會暴露在風險中。

例如，網域中的非敏感性帳戶可以在其 SID History 中，包含來自 Active Directory 樹系中另一個網域的企業系統管理員 SID，藉此將使用者帳戶的存取權「提升」至樹系中所有網域的有效網域系統管理員權限。 此外，如有未啟用 SID 篩選 (也稱為隔離) 的信任樹系，則可以從另一個樹系插入 SID，這樣在接受驗證與用於評估存取權時，該 SID 就會新增到使用者權杖。

## <a name="how-do-i-use-this-security-assessment"></a>我該如何使用這項安全性評估？

1. 使用報告資料表來探索哪些帳戶具有不安全的 SID History 屬性。
    ![查看熱門的受影響實體並建立動作計畫](media/atp-cas-isp-unsecure-sid-history-attribute-1.png)
1. 請使用下列步驟，使用 PowerShell 採取適當的動作，從帳戶中移除 SID History 屬性：

    1. 識別帳戶之 SIDHistory 屬性中的 SID。

        ```powershell
        Get-ADUser -Identity <account> -Properties SidHistory | Select-Object -ExpandProperty SIDHistory
        ```

    2. 使用剛剛識別的 SID 來移除 SIDHistory 屬性。

        ```powershell
        Set-ADUser -Identity <account> -Remove @{SIDHistory='S-1-5-21-...'}
        ```

## <a name="see-also"></a>另請參閱

- [Cloud App Security 中的 Azure ATP 活動篩選](atp-activities-filtering-mcas.md)
- [查看 Azure ATP 論壇！](https://aka.ms/azureatpcommunity)
