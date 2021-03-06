---
title: 監視 Microsoft Defender 的身分識別系統健康情況和事件
description: 使用健康情況中心來檢查 Microsoft Defender for Identity service 的運作情況，並在事件檢視器中查看潛在問題的警示，並查看系統事件。
ms.date: 10/26/2020
ms.topic: how-to
ms.openlocfilehash: ac03020c559a860fded89a496bc927da06fce3d9
ms.sourcegitcommit: a892419a5cb95412e4643c35a9a72092421628ec
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/16/2021
ms.locfileid: "100534288"
---
# <a name="work-with-microsoft-defender-for-identity-health-and-events"></a>使用 Microsoft Defender 進行身分識別健康情況和事件

## <a name="microsoft-defender-for-identity-health-center"></a>適用于身分識別健康狀態中心的 Microsoft Defender

[!INCLUDE [Product long](includes/product-long.md)]健全狀況中心可讓您知道 [!INCLUDE [Product short](includes/product-short.md)] 實例的執行情況，並在發生問題時發出警示。

## <a name="working-with-the-defender-for-identity-health-center"></a>使用 Defender 進行身分識別健康情況中心

[!INCLUDE [Product short](includes/product-short.md)]健康情況中心會在導覽列中的健康情況中心圖示上方) 的紅色點 (發出警示，讓您知道有問題發生。

![[!包含 [Product short] (include/product-short. md) ] 健全狀況中心紅點工具列](media/health-bar.png)

### <a name="managing-defender-for-identity-health"></a>管理適用于身分識別健康情況的 Defender

若要檢查實例的整體健全狀況 [!INCLUDE [Product short](includes/product-short.md)] ，請選取 [ **健全狀況** ![ [！包含 [產品簡短] (包含/產品簡短的 md) ] 健康情況中心圖示](media/red-dot.png)

- 按一下警示角落的三個點並選擇所要的選項，將開啟的問題設定為 [關閉] 或 [隱藏]，便能管理所有開啟的警示。

- **開啟**：所有新的可疑活動都出現在此清單中。

- **關閉**：用於追蹤您已識別、研究與修正以緩解的可疑活動。

    > [!NOTE]
    > [!INCLUDE [Product short](includes/product-short.md)] 如果在短時間內再次偵測到相同的活動，可能會重新開啟已關閉的活動。

- **隱藏**：隱藏活動表示您想要暫時將它忽略，只有出現新的執行個體時才會再次收到警示。 如果有類似的警示， [!INCLUDE [Product short](includes/product-short.md)] 則不會將它重新開啟。 但如果此警示在停止七天後再次出現，您便會再次收到警示。

- **重新開啟**：您可以重新開啟關閉或隱藏的警示，使它重新在時間表中顯示為 **開啟**。

- **刪除**：從安全性警訊時間表內，您也有刪除健全狀況問題的選項。 如果您刪除警示，則會將它從執行個體中刪除，而且您將「無法」予以還原。 按一下 [刪除] 之後，您即可刪除相同類型的所有安全性警訊。

![[!包含 [產品簡短] (包含/產品簡短的 md) ] 健康情況中心問題影像](media/health-issue.png)

## <a name="see-also"></a>另請參閱

- [處理可疑活動](working-with-suspicious-activities.md)
- [查看[!INCLUDE [Product short](includes/product-short.md)] 論壇！](https://aka.ms/MDIcommunity)\(英文\)
