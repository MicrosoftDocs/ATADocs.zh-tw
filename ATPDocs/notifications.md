---
title: 設定 Azure 進階威脅防護通知 | Microsoft Docs
description: 描述如何設定 Azure ATP 警示，讓您在偵測到可疑的活動時會收到通知。
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 4308f03e-b2a7-4e38-a750-540ff94faa81
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: c3fc5adbb700c4b8df66c243a655cf98aacc79af
ms.sourcegitcommit: 9f02f0f6669b25f39b616bb0885bb55b8c4f050b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/19/2018
ms.locfileid: "46362420"
---
適用於：Azure 進階威脅防護


# <a name="set-azure-atp-notifications"></a>設定 Azure ATP 通知

Azure ATP 可以在偵測到可疑的活動或健康狀態警示時，透過電子郵件通知您。 

若要接收特定電子郵件地址的通知，請設定下列參數：


1. 在 Azure ATP 工作區入口網站中，選取工具列上的 [設定] 選項，然後選取 [組態]。

![Azure ATP 組態設定圖示](media/atp-config-menu.png)

2. 按一下 [通知]。
3. 在 [郵件通知] 下，指定要透過電子郵件傳送的通知 - 可針對新的警示 (可疑的活動) 和新的健康狀態問題傳送。 
 
 >  [!NOTE]
 >   只有在建立可疑活動時，才會傳送可疑活動的電子郵件警示。
 
4. 按一下 **[儲存]**。

 ![Azure ATP 通知](media/atp-notifications.png)



## <a name="see-also"></a>另請參閱

- [設定事件收集](configure-event-collection.md)

- [設定 Syslog 設定](setting-syslog.md)
- [查看 ATP 論壇！](https://aka.ms/azureatpcommunity)\(英文\)
