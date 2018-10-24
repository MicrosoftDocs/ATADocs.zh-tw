---
title: Azure 進階威脅防護的偵測排除範圍和 Honeytoken 帳戶設定 | Microsoft Docs
description: 設定偵測排除範圍和 Honeytoken 使用者。
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 10/04/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 1ad5e923-9bbd-4f56-839a-b11a9f387d4b
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: a538ce4596da106d11646e27aa65131bb47380d2
ms.sourcegitcommit: 27cf312b8ebb04995e4d06d3a63bc75d8ad7dacb
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/04/2018
ms.locfileid: "48782976"
---
適用於：Azure 進階威脅防護


<<<<<<< HEAD
# <a name="configure-detection-exclusions-and-honeytoken-accounts"></a>設定偵測排除範圍和 Honeytoken 帳戶
=======

# <a name="install-azure-atp---step-7"></a>安裝 Azure ATP - 步驟 7

> [!div class="step-by-step"]
> [« 步驟 6](install-atp-step6-vpn.md)
> [步驟 8 »](install-atp-step8-samr.md)

## <a name="step-7-configure-detection-exclusions-and-honeytoken-accounts"></a>步驟 ７： 設定偵測排除範圍和 Honeytoken 帳戶
>>>>>>> 209d7e7162816a4c9e6e0ec0ff8d02f771e12d04

Azure ATP 可從一些偵測排除特定 IP 位址或使用者。 

例如，**DNS 探查排除項目**可以是一個使用 DNS 做為掃描機制的安全性掃描程式。 排除能協助 Azure ATP 略過這類掃描程式。  

Azure ATP 也能讓您設定 honeytoken 帳戶，用來做為針對惡意執行者的陷阱。與這些 honeytoken 帳戶 (通常是休眠的) 關聯的任何驗證都會觸發警示。

若要設定，請依照下列步驟執行︰

1.  從 Azure ATP 入口網站中，按一下設定圖示，然後選取 [設定]。

    ![Azure ATP 組態設定](media/atp-config-menu.png)

2.  在 [偵測] 下，按一下 [實體標記]。

3. 在 [Honeytoken 帳戶] 下，輸入 Honeytoken 帳戶名稱並按一下 [+] 符號。 [Honeytoken 帳戶] 欄位是可搜尋的，而且會自動顯示您網路中的實體。 按一下 **[儲存]**。

   ![Honeytoken](media/honeytoken-sensitive.png)

4. 按一下 [排除]。 針對每個威脅類型，輸入要排除而不予偵測的使用者帳戶或 IP 位址。 
5. 按一下加號。 [加入實體] \(使用者或電腦\) 欄位是可搜尋的，而且會自動填入您網路中的實體。 如需詳細資訊，請參閱[從偵測中排除實體](excluding-entities-from-detections.md)和[可疑活動指南](suspicious-activity-guide.md)。

   ![排除](media/exclusions.png)

6.  按一下 **[儲存]**。


恭喜，您已成功部署 Azure 進階威脅防護！

檢查受攻擊的時間線以便檢視偵測到的可疑活動，並搜尋使用者或電腦並檢視其設定檔。

Azure ATP 會立即開始掃描是否有可疑的活動。 某些偵測 (例如異常群組修改) 需要學習期間，因此無法在 Azure ATP 部署後立即供使用。


<a name="-head"></a><<<<<<< HEAD
=======

> [!div class="step-by-step"]
> [« 步驟 6](install-atp-step6-vpn.md)
> [步驟 8 »](install-atp-step8-samr.md)

>>>>>>> 209d7e7162816a4c9e6e0ec0ff8d02f771e12d04
## <a name="see-also"></a>另請參閱
- [Azure ATP 調整大小工具](http://aka.ms/aatpsizingtool) \(英文\)
- [設定事件收集](configure-event-collection.md)
- [Azure ATP 必要條件](atp-prerequisites.md)
- [查看 Azure ATP 論壇！](https://aka.ms/azureatpcommunity)
