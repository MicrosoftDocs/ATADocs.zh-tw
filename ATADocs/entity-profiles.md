---
title: 使用 Advanced Threat Analytics 主控台中的實體設定檔 | Microsoft Docs
description: 說明如何從 ATA 主控台的使用者設定檔畫面調查實體
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: rkarlin
ms.date: 3/25/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 581a3257-32dc-453f-b84e-b9f99186f5d3
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 1f8f2c507ea45ddb422868f8b86a973c8454509e
ms.sourcegitcommit: ae9db212f268f067b217d33b0c3f991b6531c975
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/07/2019
ms.locfileid: "65195829"
---
# <a name="investigating-entity-profiles"></a>調查實體設定檔


適用對象：*Advanced Threat Analytics 1.9 版*

實體設定檔提供您專為完整深入調查使用者、電腦、裝置，以及上述項目有權存取的資源及其歷程記錄所設計的儀表板。 設定檔頁面會利用新的 Azure ATA 邏輯活動轉譯程式，此轉譯程式可查看一組發生的活動 (彙總最多一分鐘)，並將其組成單一邏輯活動，以讓您更深入了解使用者的實際活動。

若要存取實體設定檔頁面，請按一下可疑活動時間軸中的實體名稱 (例如使用者名稱)。

左側窗格會提供您有關實體的所有可用 Active Directory 資訊 - 電子郵件地址、網域、首見日期。 若實體具敏感性性質，則會告訴您原因。 例如，使用者是否標記為機密或者為機密群組的成員？
若其為敏感性使用者，您會在該使用者名稱的下方看見圖示。

## <a name="view-entity-activities"></a>檢視實體活動

若要檢視使用者所執行 (或在實體上執行) 的所有活動，請按一下 [活動] 索引標籤。 

 ![使用者設定檔活動](media/user-profile-activities.png)

根據預設，實體設定檔的主窗格會顯示實體活動的時間軸，包含最多 6 個月的歷程記錄，您也可以從中向下鑽研到由使用者存取的實體 (或者針對實體而言，存取實體的使用者)。

您可在頂端檢視提供您快速概觀的摘要磚，使您對實體相關的須知一目瞭然。 這些磚會根據實體的類型變更，對於使用者，您可以看到：
- 使用者有多少開啟的可疑活動
- 使用者登入的電腦數
- 使用者存取的資源數
- 使用者從哪個位置登入 VPN

  ![實體功能表](media/entity-menu.png)

對於電腦，您可以看到：
- 電腦有多少開啟的可疑活動
- 登入電腦的使用者數
- 電腦存取的資源數
- 從電腦存取 VPN 的位置數
- 電腦所使用的 IP 位址清單

  ![實體功能表電腦](media/entity-computer.png)

使用活動時間軸上的 [篩選依據] 按鈕，您可以依活動類型篩選活動。 您也可以篩選掉特定的 (雜訊) 活動類型。 當您想要了解實體在網路中之行為的基本概念時，這對調查相當實用。 您也可以移至特定日期，並將篩選的活動匯出到 Excel。 匯出的檔案提供目錄服務變更 (針對帳戶在 Active Directory 中變更的項目) 的頁面，以及適用於活動的個別頁面。 

## <a name="view-directory-data"></a>檢視目錄資料

[目錄資料] 索引標籤提供可從 Active Directory 取得的靜態資訊，包含使用者存取控制安全性旗標。 ATA 也會顯示使用者的群組成員資格，如此您就可以分辨使用者是否有直接成員資格或遞迴成員資格。 針對群組，ATA 會列出群組的成員。

 ![使用者設定檔目錄資料](media/user-profile-dir-data.png)

在 [使用者存取控制] 區段中，ATA 會顯示可能需要您注意的安全性設定。 您可以看到有關使用者的重要旗標，例如使用者是否可以按 Enter 略過密碼、使用者是否擁有永不過期的密碼等。 

## <a name="view-lateral-movement-paths"></a>檢視橫向移動路徑

透過按一下 [橫向移動路徑] 索引標籤，您可以檢視完整動態和可按式影像地圖，其中提供可用來滲透您的網路，來回於此使用者之橫向移動路徑的視覺表示法。

該影像地圖所提供的清單可讓您知道攻擊者在電腦和使用者之間必須有多少來回於此使用者的躍點才能入侵機密帳戶，且如果使用者本身擁有機密帳戶，您可以查看有多少直接連線的資源和帳戶。 如需詳細資訊，請參閱[橫向移動路徑](use-case-lateral-movement-path.md)。 

 ![使用者設定檔橫向移動路徑](media/user-profile-lateral-movement-paths.png)


## <a name="see-also"></a>另請參閱
[查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
