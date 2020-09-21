---
title: Azure 進階威脅防護 Microsoft LAPS 使用情況評定
description: 本文提供 Azure ATP Microsoft LAPS 使用情況身分識別安全性狀態評估報告的概觀。
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
ms.openlocfilehash: f9e322e831b2c5e7b9852ce0889aafff6dffde8f
ms.sourcegitcommit: 0c356b0860ae8663254e0cf6f04001bcc91ce207
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/21/2020
ms.locfileid: "90828088"
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
    ![選取具有 LAPS 裝置的網域](media/atp-cas-isp-laps-1.png)
1. 使用下載中提供的文件，下載、安裝及設定或疑難排解 [Microsoft LAPS](https://go.microsoft.com/fwlink/?linkid=2104282)，對這些裝置採取適當的動作。
    ![修復 LAPS 裝置](media/atp-cas-isp-laps-2.png)

> [!NOTE]
> 此評定會每隔 24 小時更新一次。

## <a name="see-also"></a>另請參閱

- [查看 Azure ATP 論壇！](https://aka.ms/azureatpcommunity)
