---
title: 監視 Azure 進階威脅防護系統健康情況和事件
description: 使用 Azure ATP 健康情況中心來查看 Azure ATP 服務的運作情況、收到潛在問題的警示，以及在事件檢視器中檢視系統事件。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 1/3/2019
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 1b7e72c3-a538-443f-981c-398ffafa5ab8
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: fc192856a247ca4ee47e5e73ddc366bb7592a0c0
ms.sourcegitcommit: c7c0a4c9f7507f3e8e0f219798ed7d347c03e792
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/22/2020
ms.locfileid: "90910396"
---
# <a name="work-with-azure-atp-health-and-events"></a>使用 Azure ATP 健康情況和事件

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

## <a name="azure-atp-health-center"></a>Azure ATP 健康情況中心 

Azure ATP 健康情況中心可讓您知道 Azure ATP 執行個體的執行情況，並在發生問題時通知您。

## <a name="working-with-the-azure-atp-health-center"></a>使用 Azure ATP 健康情況中心

當功能表列中的健康情況中心圖示上方出現警示 (一個紅點)，就是 Azure ATP 健康情況中心在告訴您有問題發生。

![Azure ATP 健康情況中心紅點工具列](media/atp-health-bar.png)

### <a name="managing-azure-atp-health"></a>管理 Azure ATP 健康情況
若要檢查 Azure ATP 執行個體的整體健康情況，請按一下功能表列中的健康情況中心圖示 ![Azure ATP 健康情況中心圖示](media/atp-red-dot.png)

- 按一下警示角落的三個點並選擇所要的選項，將開啟的問題設定為 [關閉]**** 或 [隱藏]****，便能管理所有開啟的警示。

-   **開啟**：所有新的可疑活動都出現在此清單中。

-   **關閉**：用於追蹤您已識別、研究與修正以緩解的可疑活動。

    > [!NOTE]
    > 如果在短時間內偵測到相同的活動，Azure ATP 可能會重新開啟已經關閉的活動。
    
-   **隱藏**：隱藏活動表示您想要暫時將它忽略，只有出現新的執行個體時才會再次收到警示。 如果有類似的警示，Azure ATP 不會將它重新開啟。 但如果此警示在停止七天後再次出現，您便會再次收到警示。

-   **重新開啟**：您可以重新開啟關閉或隱藏的警示，使它重新在時間表中顯示為**開啟**。

-   **刪除**：從安全性警訊時間表內，您也有刪除健全狀況問題的選項。 如果您刪除警示，則會將它從執行個體中刪除，而且您將「無法」予以還原。 按一下 [刪除] 之後，您即可刪除相同類型的所有安全性警訊。



![Azure ATP 健康狀態中心問題的圖片](media/atp-health-issue.png)






## <a name="see-also"></a>另請參閱

- [處理可疑活動](working-with-suspicious-activities.md)
- [查看 Azure ATP 論壇！](https://aka.ms/azureatpcommunity)