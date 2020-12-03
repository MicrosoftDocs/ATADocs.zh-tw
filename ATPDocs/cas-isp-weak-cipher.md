---
title: 適用于身分識別弱式加密身分識別安全性狀態評估報告的 Microsoft Defender
description: 本文概述 Microsoft Defender 身分識別的弱式加密身分識別安全性狀態評估報告。
ms.date: 10/26/2020
ms.topic: how-to
ms.openlocfilehash: 9001fcc0aa871c14924fdd5c913e488e00104f3b
ms.sourcegitcommit: cdb7ae4580851e25aae24d07e7d66a750aa54405
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2020
ms.locfileid: "96543496"
---
# <a name="security-assessment-weak-cipher-usage"></a>安全性評估：弱式加密使用方式

## <a name="what-are-weak-ciphers"></a>什麼是弱式加密？

密碼編譯會依賴加密來加密我們的資料。 例如 RC4 (Rivest Cipher 4，亦稱為 ARC4 或 ARCFOUR，代表有意義的 RC4) 就是其中一種。 雖然 RC4 的以其簡單性和速度聞名，但自從 RC4 的原始版本推出，就有人發現了許多弱點，因此並不安全。 當輸出金鑰資料流程的開頭不會被捨棄，或使用非隨機或相關的索引鍵時，RC4 特別容易受到攻擊。

## <a name="how-do-i-use-this-security-assessment-to-improve-my-organizational-security-posture"></a>如何使用此安全性評估來改善我的組織安全性狀態？

1. 檢閱安全性評估中的弱式加密使用方式。
    ![檢閱防止弱式加密使用方式評估](media/cas-isp-weak-cipher-2.png)
1. 理解已識別用戶端和伺服器使用弱式加密的原因。
1. 補救問題，並停用 RC4 和 (或) 其他弱式加密 (例如 DES/3DES) 的使用。
1. 若要深入了解如何停用 RC4，請參閱 [Microsoft 資訊安全諮詢](https://support.microsoft.com/help/2868725/microsoft-security-advisory-update-for-disabling-rc4)。

> [!NOTE]
> 此評定會以近乎即時的方式更新。

## <a name="remediation"></a>修復

藉由設定下列登錄機碼，停用您想要停止使用 RC4 加密套件的用戶端和伺服器。 停用之後，所有和另一個需要使用 RC4 之用戶端/伺服器通訊的伺服器或用戶端，都能防止連線發生。 部署此設定的用戶端將無法連線到需要 RC4 的網站，而部署此設定的伺服器將無法服務需要使用 RC4 的用戶端。

> [!NOTE]
> 請務必先在受控制的環境中測試下列設定，再於生產環境中啟用它們。
>
> - [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 128/128]   "Enabled"=dword:00000000
> - [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 40/128]   "Enabled"=dword:00000000
> - [HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\SecurityProviders\SCHANNEL\Ciphers\RC4 56/128]   "Enabled"=dword:00000000

若要深入了解如何下載和更新登錄編輯，請參閱 [Microsoft 資訊安全諮詢](/security-updates/SecurityAdvisories/2013/2868725)。

## <a name="next-steps"></a>後續步驟

- [[!INCLUDE [Product short](includes/product-short.md)] Cloud App Security 中的活動篩選](activities-filtering-mcas.md)
- [查看[!INCLUDE [Product short](includes/product-short.md)] 論壇！](https://aka.ms/MDIcommunity)\(英文\)
