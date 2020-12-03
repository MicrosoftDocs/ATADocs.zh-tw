---
title: Microsoft Defender for Identity Microsoft LAPS 使用量評定
description: 本文概要說明 Microsoft Defender 身分識別的 Microsoft LAPS 使用身分識別安全性狀態評估報告。
ms.date: 10/26/2020
ms.topic: how-to
ms.openlocfilehash: d829636ac9659a19453db6f4cadfba54d129593d
ms.sourcegitcommit: cdb7ae4580851e25aae24d07e7d66a750aa54405
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2020
ms.locfileid: "96543618"
---
# <a name="security-assessment-microsoft-laps-usage"></a>安全性評估：Microsoft LAPS 使用情況

## <a name="what-is-microsoft-laps"></a>什麼是 Microsoft LAPS？

Microsoft 的「區域系統管理員密碼解決方案」(LAPS) 提供已加入網域的電腦本機系統管理員帳戶密碼管理。 隨機化的密碼儲存在由 ACL 保護的 Active Directory (AD) 中，因此只有合格的使用者可以讀取或要求重設。

## <a name="what-risk-does-not-implementing-laps-pose-to-an-organization"></a>實作 LAPS 不會對組織造成哪些風險？

LAPS 為網域中每部電腦之常用本機帳戶使用相同密碼的問題，提供了解決方案。 LAPS 解決此問題的方法，是為網域中每部電腦的常用本機系統管理員帳戶設定不同的輪換隨機密碼。

LAPS 能在簡化密碼管理的同時，協助客戶針對網路攻擊實作其他建議的防禦措施。 此解決方案特別能夠降低因客戶在電腦上使用同一組本機系統管理帳戶與密碼而橫向擴展的風險。 LAPS 會將每部電腦的本機系統管理員帳戶密碼儲存在 AD 中，以電腦對應 AD 物件的機密屬性加以保護。 電腦可以在 AD 中更新自己的密碼資料，而網域系統管理員可將讀取存取權授與已授權的使用者或群組，例如工作站服務台管理員。

## <a name="how-do-i-use-this-security-assessment"></a>我該如何使用這項安全性評估？

1. 您可使用報告資料表來探索哪些網域有部分 (或全部) 相容的 Windows 裝置尚未受到 LAPS 保護，或在過去 60 天內未變更其 LAPS 受控密碼。
1. 若為僅受部分保護的網域，請選取相關的資料列，以檢視該網域中未受 LAPS 保護的裝置清單。
    ![選取具有 LAPS 裝置的網域](media/cas-isp-laps-1.png)
1. 使用下載中提供的文件，下載、安裝及設定或疑難排解 [Microsoft LAPS](https://go.microsoft.com/fwlink/?linkid=2104282)，對這些裝置採取適當的動作。
    ![修復 LAPS 裝置](media/cas-isp-laps-2.png)

> [!NOTE]
> 此評定會每隔 24 小時更新一次。

## <a name="see-also"></a>另請參閱

- [查看[!INCLUDE [Product short](includes/product-short.md)] 論壇！](https://aka.ms/MDIcommunity)\(英文\)
