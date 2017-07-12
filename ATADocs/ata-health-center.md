---
title: "監視 Advanced Threat Analytics 系統健康狀態和事件 | Microsoft Docs"
description: "使用 ATA 健康狀態中心來查看 ATA 服務的運作情況、收看潛在問題的警示，以及在事件檢視器中檢視系統事件。"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 07/2/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: d6c783b2-46c5-4211-b21a-d6b17f08d03d
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 7e396cddb818c0e80f8b7d78764a58d6abd560e5
ms.sourcegitcommit: fa50f37b134d7579d7c310852dff60e5f1996eaa
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/03/2017
---
適用於︰Advanced Threat Analytics 1.8 版


<a id="working-with-ata-system-health-and-events" class="xliff"></a>

# 使用 ATA 系統健康狀態和事件

<a id="ata-health-center" class="xliff"></a>

## ATA 健全狀況中心
ATA 健全狀況中心可讓您知道 ATA 服務的運作情況，並向您警示問題。

<a id="working-with-the-ata-health-center" class="xliff"></a>

## 使用 ATA 健全狀況中心
當功能表列中的健全狀況中心圖示上方出現警示 (一個紅點)，就是 ATA 健全狀況中心在告訴您有問題發生。

![ATA 健全狀況中心紅點工具列](media/ATA-Health-Center-Alert-red-dot.png)

<a id="managing-ata-health" class="xliff"></a>

### 管理 ATA 健全狀況
若要檢查系統的整體健全狀況，按一下功能表列中的健全狀況中心圖示 ![ATA 健全狀況中心圖示](media/ATA-red-dot.png)

-   可將所有未解決的警示設定為**已解決**或**已解除**。 在 [警示] 中，按一下 [未解決] 並捲動到 [已解決] 或 [已解除]。

-   如果解決了問題，而 ATA 偵測到此問題仍然發生，此問題將會自動移回 [未解決] 問題清單。 如果 ATA 偵測到未解決的問題已解決，便會自動將它移至 [已解決] 問題清單。

-   **已解除**問題是您不想要 ATA 繼續檢查的問題 - 例如，您收到您已知存在問題的警示，而您不打算解決這個問題，但不想繼續收到有關它的通知，也不想在 [未解決] 問題清單中看到它，您可以將它設定為**已解除**。

![ATA 健全狀況中心問題的圖片](media/ATA-Health-Issue.JPG)






<a id="see-also" class="xliff"></a>

## 另請參閱
- [使用 ATA 偵測設定](working-with-detection-settings.md)
- [處理可疑活動](working-with-suspicious-activities.md)
- [查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
