---
title: 使用 Azure 進階威脅防護入口網站中的使用者設定檔 | Microsoft Docs
description: 描述如何從 Azure ATP 入口網站的使用者設定檔畫面調查使用者
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 09/15/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 17458706-79fb-4c23-aa42-66979164a45f
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 0bff9c9081951c234d2d0076d154a984898a0a31
ms.sourcegitcommit: 939c098dd02a1f4191c528d10d69d059a62042b2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/15/2019
ms.locfileid: "71004490"
---
# <a name="understanding-entity-profiles"></a>了解實體設定檔

> [!NOTE]
> 此頁面所述的 Azure ATP 功能也可使用新的[入口網站](https://portal.cloudappsecurity.com)來存取。

實體設定檔提供您專為完整深入調查使用者、電腦、裝置，以及其有權存取資源及其歷程記錄所設計的全方位實體頁面。 設定檔頁面會利用新的 Azure ATP 邏輯活動轉譯程式，此轉譯程式可查看一組發生的活動 (彙總最多一分鐘)，並將它們組成單一邏輯活動，以讓您更深入了解您使用者的實際活動。

若要存取實體設定檔頁面，請按一下可疑活動時間軸中的實體名稱 (例如使用者名稱)。

左側窗格會提供您有關實體的所有可用 Active Directory 資訊 - 電子郵件地址、網域、首見日期。 如果為機密實體，則會告訴您原因。 例如，使用者是否標記為機密或者為機密群組的成員？
如果是機密使用者，您會在使用者的名稱下看見圖示。

## <a name="view-entity-activities"></a>檢視實體活動

若要檢視使用者所執行 (或在實體上執行) 的所有活動，請按一下 [活動]  索引標籤。 

 ![使用者設定檔活動](media/user-profile-activities.png)

根據預設，實體設定檔的主窗格會顯示實體活動的時間軸，包含最多六個月的歷程記錄，您也可以從中向下鑽研到由使用者存取的實體 (或者針對實體而言，存取實體的使用者)。

在頂端，您可以檢視摘要圖格，其中提供關於您的實體所需要清楚了解的快速概觀 - 使用者登入多少部電腦、存取多少資源，以及使用者登入 VPN (若有設定) 的位置。 

使用活動時間軸上的 [篩選依據]  按鈕，您可以依活動類型篩選活動。 您也可以篩選掉特定的 (雜訊) 活動類型。 當您想要了解實體在網路中之行為的基本概念時，這可以協助調查。 您也可以移至特定日期，並將篩選的活動匯出到 Excel。 匯出的檔案提供目錄服務變更 (針對帳戶在 Active Directory 中變更的項目) 的頁面，以及適用於活動的個別頁面。 

## <a name="view-directory-data"></a>檢視目錄資料

[目錄資料]  索引標籤提供可從 Active Directory 取得的靜態資訊，包含使用者存取控制安全性旗標。 Azure ATP 也會顯示使用者的群組成員資格，如此您就可以分辨使用者是否有直接成員資格或遞迴成員資格。 針對群組，Azure ATP 會列出群組的成員。

 ![使用者設定檔目錄資料](media/user-profile-dir-data.png)

在 [使用者存取控制]  區段中，Azure ATP 會顯示可能需要您注意的安全性設定。 您可以看到使用者的相關重要旗標，例如使用者是否可以按 Enter 略過密碼、使用者是否擁有永不過期的密碼等。 

## <a name="view-lateral-movement-paths"></a>檢視橫向移動路徑

透過按一下 [橫向移動路徑] 索引標籤，您可以檢視完整動態和可按式影像地圖，其中提供可用來滲透您的網路，來回於此使用者之橫向移動路徑的視覺表示法。

該影像地圖所提供的清單可讓您知道攻擊者在電腦和使用者之間必須有多少來回於此使用者的躍點才能入侵機密帳戶，且如果使用者擁有機密帳戶，您可以查看有多少直接連線的資源和帳戶。

若在過去兩天期間未針對實體偵測到潛在 LMP，便不會顯示圖表。 使用 [檢視不同日期]  選取不同日期，來檢視先前針對此實體所探索到的橫向移動路徑圖表。 [橫向移動路徑報表](reports.md)一律可供您使用，提供所探索到潛在橫向移動路徑的相關資訊，並可隨時間自訂。  

如需詳細資訊，請參閱[橫向移動路徑](use-case-lateral-movement-path.md)。 

 ![使用者設定檔橫向移動路徑](media/user-profile-lateral-movement-paths.png)


## <a name="see-also"></a>另請參閱

- [使用 Azure ATP 調查橫向移動路徑](use-case-lateral-movement-path.md)
- [查看 Azure ATP 論壇！](https://aka.ms/azureatpcommunity)
