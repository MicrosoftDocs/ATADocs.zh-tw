---
title: Azure 進階威脅防護設定偵測排除範圍和 Honeytoken 帳戶
description: 設定偵測排除範圍和 Honeytoken 使用者。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 10/22/2019
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 1ad5e923-9bbd-4f56-839a-b11a9f387d4b
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 95f3408468a2e1d78a04772673612c3335030f00
ms.sourcegitcommit: 2be59f0bd4c9fd0d3827e9312ba20aa8eb43c6b5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88956188"
---
# <a name="configure-detection-exclusions-and-honeytoken-accounts"></a>設定偵測排除範圍和 Honeytoken 帳戶

Azure ATP 可從一些偵測排除特定 IP 位址或使用者。

例如，**DNS 探查排除項目**可以是一個使用 DNS 做為掃描機制的安全性掃描程式。 排除能協助 Azure ATP 略過這類掃描程式。

Azure ATP 也能讓您設定 honeytoken 帳戶，用來做為針對惡意執行者的陷阱。與這些 honeytoken 帳戶 (通常是休眠的) 關聯的任何驗證都會觸發警示。

若要設定，請依照下列步驟執行︰

1. 從 Azure ATP 入口網站中，按一下設定圖示，然後選取 [設定]  。

    ![Azure ATP 組態設定](media/atp-config-menu.png)

1. 在 [偵測]  下，按一下 [實體標記]  。

1. 在 [Honeytoken 帳戶] 下，輸入 Honeytoken 帳戶名稱並按一下 [+] 符號。 [Honeytoken 帳戶] 欄位是可搜尋的，而且會自動顯示您網路中的實體。 按一下 **[儲存]** 。

    ![Honeytoken](media/honeytoken-sensitive.png)

1. 按一下 [排除]  。 針對每個威脅類型，輸入要排除而不予偵測的使用者帳戶或 IP 位址。
1. 按一下加號  。 [加入實體]  \(使用者或電腦\) 欄位是可搜尋的，而且會自動填入您網路中的實體。 如需詳細資訊，請參閱[從偵測中排除實體](excluding-entities-from-detections.md)和[安全性警訊指南](suspicious-activity-guide.md)。

    ![從偵測中排除實體](media/exclusions.png)

1. 按一下 **[儲存]** 。

恭喜，您已成功部署 Azure 進階威脅防護！

檢查攻擊時間表以檢視從所偵測到之活動產生的安全性警示，並搜尋使用者或電腦並檢視其設定檔。

Azure ATP 掃描會立即開始。 某些偵測 (例如[敏感性群組的可疑新增項目](atp-domain-dominance-alerts.md#suspicious-additions-to-sensitive-groups-external-id-2024)) 需要學習期間，而且在 Azure ATP 部署之後不會立即可用。每個警示的學習期間列在詳細的[安全性警示指南](suspicious-activity-guide.md)中。

## <a name="see-also"></a>另請參閱

- [Azure ATP 調整大小工具](https://aka.ms/aatpsizingtool) \(英文\)
- [設定事件收集](configure-event-collection.md)
- [Azure ATP 必要條件](atp-prerequisites.md)
- [查看 Azure ATP 論壇！](https://aka.ms/azureatpcommunity)
