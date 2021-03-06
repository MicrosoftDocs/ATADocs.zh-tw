---
title: 適用于身分識別不安全帳戶屬性評估的 Microsoft Defender
description: 本文概述 Microsoft Defender 身分識別的實體，其具有不安全的屬性身分識別安全性狀態評估報告。
ms.date: 01/18/2021
ms.topic: how-to
ms.openlocfilehash: 64aa95a423d0c8fc0bb210c2c10bc63f8c33bca4
ms.sourcegitcommit: 14f7228dbe6af353e81f20d2047dad24043840b4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/31/2021
ms.locfileid: "99217697"
---
# <a name="security-assessment-unsecure-account-attributes"></a>安全性評估：不安全的帳戶屬性

## <a name="what-are-unsecure-account-attributes"></a>不安全的帳戶屬性是指什麼？

[!INCLUDE [Product long](includes/product-long.md)] 持續監視您的環境，以識別具有可公開安全性風險之屬性值的帳戶，並報告這些帳戶以協助保護您的環境。

## <a name="what-risk-do-unsecure-account-attributes-pose"></a>不安全的帳戶屬性會造成什麼風險？

無法保護其帳戶屬性的組織對惡意源起方毫無防備。

惡意執行者 (如竊賊) 通常會試圖以最輕鬆且不容易被發現的方式進入環境。 以不安全的屬性設定的帳戶是攻擊者的機會，而且可能會暴露風險。

例如，若啟用了 *PasswordNotRequired* 屬性，攻擊者就可以輕易存取帳戶。 而若帳戶具有其他資源的特殊權限，風險就會特別高。

## <a name="how-do-i-use-this-security-assessment"></a>我該如何使用這項安全性評估？

1. 使用報告資料表找出哪些帳戶具有不安全的屬性。
    ![查看熱門的受影響實體並建立動作計畫](media/cas-isp-unsecure-account-attributes-1.png)
1. 請對這些使用者帳戶採取行動，即修改或移除相關的屬性。

> [!NOTE]
>
> - 此評定會以近乎即時的方式更新。
> - 如果不符合的 [必要條件](prerequisites.md#before-you-start) ，此評量可能包含先前刪除的實體 [!INCLUDE [Product long](includes/product-long.md)] 。

## <a name="remediation"></a>修復

請對相關屬性採取適用的補救措施，如下表所述。

| 建議的動作 | 修復 | 原因 |
| --- | --- | --- |
| 移除不需要 Kerberos 預先驗證| 從 Active Directory (AD) 中的帳戶屬性移除此設定 | 若要移除此設定，帳戶必須經過 Kerberos 預先驗證，以提升安全性。 |
| 移除 [使用可還原的加密來存放密碼] | 從 AD 中的帳戶屬性移除此設定 | 移除此設定可防止帳戶密碼遭輕易解密。 |
| 移除 [不需要密碼] | 從 AD 中的帳戶屬性移除此設定 | 若要移除此設定，帳戶必須使用密碼，而這有助於防止有人未經授權即存取資源。 |
| 移除 [以低度加密存放密碼] | 重設帳戶密碼 | 變更帳戶密碼，即可使用較強的加密演算法加以保護。 |
| 啟用 Kerberos AES 加密支援 | 在 AD 中的帳戶屬性上啟用 AES 功能 | 在帳戶上啟用 AES128_CTS_HMAC_SHA1_96 或 AES256_CTS_HMAC_SHA1_96 有助於防止使用較弱的加密密碼進行 Kerberos 驗證。 |
| 移除 [這個帳戶需要使用 Kerberos DES 加密類型] | 從 AD 中的帳戶屬性移除此設定 | 移除此設定，即可對帳戶密碼使用較強的加密演算法。 |

## <a name="see-also"></a>另請參閱

- [[!INCLUDE [Product short](includes/product-short.md)] Cloud App Security 中的活動篩選](activities-filtering-mcas.md)
- [查看[!INCLUDE [Product short](includes/product-short.md)] 論壇！](https://aka.ms/MDIcommunity)\(英文\)
