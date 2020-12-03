---
title: 適用于身分識別舊版通訊協定身分識別安全性狀態評估的 Microsoft Defender
description: 本文概述 Microsoft Defender 身分識別的舊版通訊協定識別安全性狀態評估報告。
ms.date: 10/26/2020
ms.topic: how-to
ms.openlocfilehash: 54bc0aeca86acf30101cb3200c1c5c8a3d5041bd
ms.sourcegitcommit: cdb7ae4580851e25aae24d07e7d66a750aa54405
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2020
ms.locfileid: "96544176"
---
# <a name="security-assessment-legacy-protocols-usage"></a>安全性評估：使用舊版通訊協定

## <a name="what-are-legacy-protocols"></a>什麼是舊版通訊協定？

企業雖然會使用修補和伺服器強化來保護其基礎結構所執行的所有標準工作，卻常忽略淘汰舊版通訊協定的需求。 因為舊版通訊協定的暴露機率並沒有降低，所以認證仍然相對地容易竊取。

大部分的舊版通訊協定都是在現今的安全性需求出現前草擬建立的，而其建立背景則在現代企業安全性需求仍不明朗的時期。 不過，舊版通訊協定至今仍保持原樣，使得它們在所有現代組織中都很容易成為易受攻擊的存取點。

## <a name="what-risks-do-retained-legacy-protocols-introduce"></a>保留的舊版通訊協定會帶來哪些風險？

新式網路攻擊方法通常會在其攻擊中使用舊版的通訊協定，並經常利用它們來鎖定尚未採取適當因應措施的組織。

針對不安全舊版通訊協定停用支援，即可縮減受攻擊面，例如：

- TLS 1.0 & 1.1 (以及所有版本的 SSL)
- 伺服器訊息區 v1 (SMBv1)
- LanMan (LM) / NTLMv1
- 摘要式驗證

若要淘汰舊版通訊協定的使用，您的組織必須先探索有哪些內部實體和應用程式依賴它們。 **舊版通訊協定使用方式** 評估報告資料表，會使用舊版通訊協定 (現在為 NTLMv1) 來呈現最常探索到的實體。 您可以使用報表立即查看所有受到最大影響的實體，並對其採取動作、停止使用這些通訊協定，最終將它們全部停用。 若要深入了解使用舊版通訊協定的危險，請參閱[停止使用 LAN 管理員和 NTLMv1！](/archive/blogs/miriamxyra/stop-using-lan-manager-and-ntlmv1) (英文) 和 [Drop The MIC 2 & Exploiting LMv2 Clients](https://www.preempt.com/blog/active-directory-ntlm-attacks/) (卸除 MIC 2 與惡意探索 LMv2 用戶端)。

## <a name="how-do-i-use-this-security-assessment"></a>我該如何使用這項安全性評估？

1. 使用報表資料表來知道有哪幾個前幾大已探索實體在使用舊版通訊協定。

    ![防止使用舊版通訊協定](media/cas-isp-legacy-protocols-2.png)
1. 對這些實體採取適當的動作，進而探索相依性。
1. 停止使用舊版通訊協定，並於之後[完全停用通訊協定](/archive/blogs/miriamxyra/stop-using-lan-manager-and-ntlmv1)。
1. [卸除 MIC 2 並停止使用 LMv2 用戶端](https://www.preempt.com/blog/active-directory-ntlm-attacks/)。

> [!NOTE]
> 此評定會以近乎即時的方式更新。

## <a name="next-steps"></a>後續步驟

- [[!INCLUDE [Product short](includes/product-short.md)] Cloud App Security 中的活動篩選](activities-filtering-mcas.md)
- [查看[!INCLUDE [Product short](includes/product-short.md)] 論壇！](https://aka.ms/MDIcommunity)\(英文\)