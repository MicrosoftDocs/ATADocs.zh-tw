---
title: 設定適用於身分識別的 Microsoft Defender 通知
description: 描述如何設定適用於身分識別的 Microsoft Defender 安全性警示，以在偵測到可疑活動時收到通知。
ms.date: 10/26/2020
ms.topic: how-to
ms.openlocfilehash: ad02fab44b76fc9d30af59a331ec5243796224d5
ms.sourcegitcommit: a892419a5cb95412e4643c35a9a72092421628ec
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/16/2021
ms.locfileid: "100533642"
---
# <a name="set-microsoft-defender-for-identity-notifications"></a>設定適用於身分識別的 Microsoft Defender 通知

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
