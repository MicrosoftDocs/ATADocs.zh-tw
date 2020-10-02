---
title: 設定 Azure 進階威脅防護通知
description: 描述如何設定 Azure ATP 安全性警訊，以在偵測到可疑的活動時收到通知。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 09/29/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 4308f03e-b2a7-4e38-a750-540ff94faa81
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: b60044cbc2ccf05ff1802ecce6e3e11d42543f97
ms.sourcegitcommit: dd8435ba20f76a6fc4590980c040c6fc7ec6c62b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/29/2020
ms.locfileid: "91451727"
---
# <a name="set-azure-atp-notifications"></a>設定 Azure ATP 通知

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

Azure ATP 會在偵測到可疑的活動並引發安全性警訊或健康狀態警訊時，透過電子郵件通知您。

若要接收特定電子郵件地址的通知，請設定下列參數：

1. 在 Azure ATP 入口網站中，選取工具列上的 [設定] 選項，然後選取 [設定]****。

    ![Azure ATP 組態設定圖示](media/atp-config-menu.png)

1. 按一下 [通知]****。
1. 在 [郵件通知] 下，新增您想收到通知的電子郵件地址 - 可針對新的警示 (可疑的活動) 和新的健康狀態問題傳送。

    > [!NOTE]
    >
    > - 只有定義的電子郵件地址才能接收電子郵件通知。
    > - 只有在建立可疑活動時，才會傳送可疑活動的電子郵件警示。

1. 按一下 [儲存]。

    ![Azure ATP 通知](media/atp-notifications.png)

## <a name="see-also"></a>另請參閱

- [設定事件收集](configure-event-collection.md)

- [設定 Syslog 設定](setting-syslog.md)
- [查看 Azure ATP 論壇！](https://aka.ms/azureatpcommunity)
