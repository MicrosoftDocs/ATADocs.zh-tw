---
title: 監視 Azure 進階威脅防護系統健康狀態和事件 | Microsoft Docs
description: 使用 Azure ATP 工作區健康狀態中心來查看 Azure ATP 服務的運作情況、收看潛在問題的警示，以及在事件檢視器中檢視系統事件。
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 1b7e72c3-a538-443f-981c-398ffafa5ab8
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 86eb90f452d5aee2504e525e64bfc62c22207880
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/21/2018
ms.locfileid: "29444904"
---
適用於：Azure 進階威脅防護


# <a name="working-with-azure-atp-workspace-health-and-events"></a>使用 Azure ATP 工作區健康狀態和事件

## <a name="azure-atp-workspace-health-center"></a>Azure ATP 工作區健康狀態中心 

Azure ATP 工作區健康狀態中心可讓您知道 Azure ATP 工作區的運作情況，並在發生問題時通知您。

## <a name="working-with-the-azure-atp-workspace-health-center"></a>使用 Azure ATP 工作區健康狀態中心

當功能表列中的健康狀態中心圖示上方出現警示 (一個紅點)，就是 Azure ATP 工作區健康狀態中心在告訴您有問題發生。

![Azure ATP 健康狀態中心紅點工具列](media/atp-health-bar.png)

### <a name="managing-azure-atp-workspace-health"></a>管理 Azure ATP 工作區的健康狀態
若要檢查工作區的整體健全狀況，按一下功能表列中的健全狀況中心圖示 ![Azure ATP 工作區健康狀態中心圖示](media/atp-red-dot.png)

-   按一下警示角落的三個點並選擇所要的選項，將開啟的問題設定為 [關閉] 或 [隱藏]，便能管理所有開啟的警示。

-   **開啟**：所有新的可疑活動都出現在此清單中。

-   **關閉**：用於追蹤您已識別、研究與修正以緩解的可疑活動。

    > [!NOTE]
    > 如果在短時間內偵測到相同的活動，Azure ATP 可能會重新開啟已經關閉的活動。
    > 每個工作區都有它自己的健康狀態中心。

-   **隱藏**：隱藏活動表示您想要暫時將它忽略，只有出現新的執行個體時才會再次收到警示。 如果有類似的警示，Azure ATP 不會將它重新開啟。 但如果此警示在停止七天後再次出現，您便會再次收到警示。

-   **重新開啟**：如果您關閉或隱藏問題，您可以重新開啟它，使它重新在時間軸中顯示為「開啟」。
- 
- **刪除**：從可疑的活動時間軸內，您也有刪除健康狀態問題的選項。 如果您刪除警示，則會將它從工作區中刪除，而且您將「無法」予以還原。 按一下 [刪除] 之後，您將可以刪除相同類型的所有可疑活動。



![Azure ATP 工作區健全狀況中心問題影像](media/atp-health-issue.png)






## <a name="see-also"></a>另請參閱

- [處理可疑活動](working-with-suspicious-activities.md)
- [查看 ATP 論壇！](https://aka.ms/azureatpcommunity)\(英文\)
