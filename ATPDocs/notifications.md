---
title: 設定適用於身分識別的 Microsoft Defender 通知
description: 描述如何設定適用於身分識別的 Microsoft Defender 安全性警示，以在偵測到可疑活動時收到通知。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 10/26/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 3eb687b716ce69bb4be0aabc2b128b1cf46242ff
ms.sourcegitcommit: 07a855b87931875bdeca14b152b13a36db79bfa8
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/26/2020
ms.locfileid: "94847134"
---
# <a name="set-product-long-notifications"></a>設定[!INCLUDE [Product long](includes/product-long.md)] 通知

[!INCLUDE [Product long](includes/product-long.md)] 可在偵測到可疑活動時通知您，並透過電子郵件發出安全性警示或健康情況警示。

若要接收特定電子郵件地址的通知，請設定下列參數：

1. 在[!INCLUDE [Product short](includes/product-short.md)] 入口網站中，選取工具列上的 [設定] 選項，然後選取 [設定]。

    ![[!INCLUDE [Product short](includes/product-short.md)] 組態設定圖示](media/config-menu.png)

1. 按一下 [通知]。
1. 在 [郵件通知] 下，新增您想收到通知的電子郵件地址 - 可針對新的警示 (可疑的活動) 和新的健康狀態問題傳送。

    > [!NOTE]
    >
    > - 只有定義的電子郵件地址才能接收電子郵件通知。
    > - 只有在建立可疑活動時，才會傳送可疑活動的電子郵件警示。

1. 按一下 [儲存]。

    ![[!INCLUDE [Product short](includes/product-short.md)] 通知](media/notifications.png)

## <a name="see-also"></a>另請參閱

- [設定事件收集](configure-event-collection.md)

- [設定 Syslog 設定](setting-syslog.md)
- [查看[!INCLUDE [Product short](includes/product-short.md)] 論壇！](https://aka.ms/MDIcommunity)\(英文\)
