---
title: Azure 進階威脅防護受監視活動的篩選與搜尋 | Microsoft Docs
description: 本文提供如何使用 Azure ATP 篩選及搜尋受監視活動的概觀。
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 10/28/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: a546703b-d5a9-404d-9e87-125523bb8421
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 4f065b299f499b28368fd43fe03d2e7c38741f67
ms.sourcegitcommit: a0ebb0b6f140d4abf091ebd9d756b975b3d96b9d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/23/2019
ms.locfileid: "54458422"
---
# <a name="azure-atp-monitored-activities-search-and-filter"></a>Azure ATP 受監視活動的搜尋與篩選 

Azure ATP 在您網路上偵測到的活動，可以經過搜尋與篩選，讓您在研究與調查安全性警訊時，能夠輕鬆向下鑽研及整理這些活動。  

從 Azure ATP 時間軸選取網路中的任何實體 (DC、電腦或使用者) 當作篩選存取點。 接下來，選取要依 [安全性警訊]、[活動] 類型或任意組合來篩選。 套用篩選之後，實體的威脅時間軸就會以篩選的資訊更新。 您也可下載篩選出的警示與活動，以在其他工具中繼續進行調查或追蹤。 

![篩選警示與活動](./media/activities-filter.png)

若要篩選警示與活動：
 1. 從 Azure ATP 時間軸選取要調查的實體。 
 2. 按一下 [篩選依據]，然後選取要篩選的警示及 (或) 活動。 
 3. 按一下 [套用] 。 實體時間軸會根據您選取的篩選來更新。 
 4. 若要下載篩選出的活動，請按一下 [下載活動]，然後選取下載報表的日期範圍。 
 5. 若要重設實體時間軸，以顯示所有警示及活動，請按一下 [重設] 或關閉篩選。 


## <a name="see-also"></a>另請參閱
- [調查實體](investigate-entity.md)
- [監視警示](monitoring-alerts.md)
- [使用安全性警訊](working-with-suspicious-activities.md)
- [查看 ATP 論壇！](https://aka.ms/azureatpcommunity)\(英文\)
