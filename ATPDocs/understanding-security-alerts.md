---
title: 適用於身分識別的 Microsoft Defender 安全性警示教學課程
description: 此文章說明如何使用及了解適用於身分識別的 Microsoft Defender 安全性警示。
ms.date: 10/27/2020
ms.topic: how-to
ms.openlocfilehash: bec99de6189e51fa86cfd96dc219de3fe54538fa
ms.sourcegitcommit: a892419a5cb95412e4643c35a9a72092421628ec
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/16/2021
ms.locfileid: "100534526"
---
# <a name="understanding-security-alerts"></a>了解安全性警訊

[!INCLUDE [Product long](includes/product-long.md)] 安全性警示會以清晰的語言與圖片說明在您網路上找到的可疑活動，以及涉及威脅的執行者與電腦。 警訊會以嚴重性進行分級，以色彩劃分使其更輕易地以視覺方式篩選，且依威脅階段整理。 所有警訊的設計目的都是為了讓您更快了解網路的當前情形。 包含涉及使用者和電腦直接連結的警示辨識項清單，可協助您輕易且直接地進行調查。

在此教學課程中，了解[!INCLUDE [Product short](includes/product-short.md)] 安全性警示的結構，以及其使用方式：

> [!div class="checklist"]
>
> - 安全性警訊結構
> - 安全性警訊分類
> - 安全性警訊類別
> - 進階的安全性警訊調查
> - 相關的實體
> - [!INCLUDE [Product short](includes/product-short.md)] 與 NNR (網路名稱解析)

## <a name="security-alert-structure"></a>安全性警訊結構

每個[!INCLUDE [Product short](includes/product-short.md)] 安全性警示都包含：

- **警訊標題**  
警示的正式[!INCLUDE [Product short](includes/product-short.md)] 名稱。
- **描述**  
提供發生事件的簡短說明。
- **辨識項**  
提供發生事件的其他相關資訊及資料，以在調查程序中給予協助。
- **Excel 下載**  
提供有助於分析的詳細 Excel 下載報表

![[!INCLUDE [Product short](includes/product-short.md)] 安全性警示結構](media/security-alert-structure.png)

## <a name="security-alert-classifications"></a>安全性警訊分類

在適當的調查之後，所有[!INCLUDE [Product short](includes/product-short.md)] 安全性警示都可以分類為下列其中一種活動類型：

- **確判 (TP)** ：由[!INCLUDE [Product short](includes/product-short.md)] 偵測到的惡意動作。

- **良性確判 (B-TP)** ：由[!INCLUDE [Product short](includes/product-short.md)] 偵測到實際存在但不具惡意的動作，例如滲透測試，或由已核准應用程式產生的已知活動。

- **誤判 (FP)** ：假警示，表示活動並未發生。

### <a name="is-the-security-alert-a-tp-b-tp-or-fp"></a>安全性警訊為 TP、B-TP 或 FP

針對各警訊，詢問以下問題以判斷警訊的分類，並協助您決定下一步動作：

1. 特定安全性警訊在您環境中出現的頻率為何？
1. 該警訊是否都是由相同類型的電腦或使用者觸發？
   例如，具有相同角色的伺服器，或來自相同群組/部門的使用者？ 若電腦或使用者相似，您可決定是否要予以排除，以避免往後出現其他 FP 警訊。

附註：完全相同類型警訊的增加，通常會降低警訊的可疑/重要性等級。 對於重複的警訊，請驗證設定，並使用安全性警訊詳細資料及定義，了解重複觸發警訊的實際緣由。

## <a name="security-alert-categories"></a>安全性警訊類別

[!INCLUDE [Product short](includes/product-short.md)] 安全性警示分為下列類別或階段，如同在典型網路攻擊狙殺鏈中會看到的階段。 請使用以下連結，深入了解設計來偵測每個攻擊的各階段及警訊：

- [偵察警訊](reconnaissance-alerts.md)
- [遭入侵的認證警訊](compromised-credentials-alerts.md)
- [橫向移動警訊](lateral-movement-alerts.md)
- [網域支配警訊](domain-dominance-alerts.md)
- [外流警訊](exfiltration-alerts.md)

## <a name="advanced-security-alert-investigation"></a>進階的安全性警訊調查

若要取得更多安全性警訊的詳細資料，請下載詳細的 Excel 警訊報表。

1. 按一下任何警訊右上角的三個點，然後選取 [下載詳細資料]。

每個[!INCLUDE [Product short](includes/product-short.md)] 警示 Excel 下載項目都會提供下列資訊：

- 摘要 - 包含警訊重點的第一個索引標籤
  - Title
  - 說明
  - 開始時間 (UTC)
  - 結束時間 (UTC)
  - 嚴重性 - 低/中/高
  - 狀態 - 開啟/關閉
  - 狀態更新時間 (UTC)
  - 在瀏覽器中檢視
- 所有涉及的實體 (帳戶、電腦及資源) 都會列出，且由他們的角色來區分。
  - 取決於警訊，可分為來源、目的地或受攻擊。
- 大多數的索引標籤都包含以下各實體的資料：
  - 名稱
  - 詳細資料
  - 類型
  - SamName
  - 來源電腦
  - 來源使用者 (如果有的話)
  - 網域控制站
  - 存取的資源：時間、電腦、名稱、詳細資料、類型、服務。
  - 各警訊的其他索引標籤：
    - 當有可疑的攻擊使用暴力密碼破解時，受攻擊帳戶上出現的索引標籤。
    - 當疑似受攻擊的目標涉及網路對應偵察 (DNS) 時，網域名稱系統 (DNS) 上出現的索引標籤。
  - 相關實體：識別碼、類型、名稱、唯一實體 JSON、唯一實體設定檔 JSON
- 由[!INCLUDE [Product short](includes/product-short.md)] 感應器所擷取到與警示 (網路或事件活動) 相關的所有原始活動包含：
  - 網路活動
  - 事件活動

![涉及的實體](media/involved-entities.png)

### <a name="related-entities"></a>相關的實體

在各警訊中，最後一個索引標籤會提供 **相關的實體**。 相關的實體為涉及可疑活動的所有實體，且與他們在警訊中扮演的「角色」一致。 每個實體都有兩個 JSON 檔案，分別為唯一的實體 JSON 及唯一的實體設定檔 JSON。 若要深入了解實體及取得調查警訊的協助，請使用這兩個 JSON 檔案。

**唯一的實體 JSON**

包含[!INCLUDE [Product short](includes/product-short.md)] 從 Active Directory 了解到的帳戶相關資料。 其中包含「辨別名稱」、*SID*、*LockoutTime* 與 *PasswordExpiryTime* 等所有屬性。 若為使用者帳戶，其中會包含 *Department*、*Mail* 及 *PhoneNumber* 等資料。 針對電腦帳戶，其中會包含 *OperatingSystem*、*IsDomainController* 與 *DnsName* 等資料。

**唯一的實體設定檔 JSON**

包含[!INCLUDE [Product short](includes/product-short.md)] 已在實體上分析的所有資料。 [!INCLUDE [Product short](includes/product-short.md)] 會使用擷取到的網路與事件活動，了解環境的使用者與電腦。 [!INCLUDE [Product short](includes/product-short.md)] 會分析每個實體的相關資訊。 此資訊會供[!INCLUDE [Product short](includes/product-short.md)] 的威脅識別功能利用。

![相關的實體](media/related-entities.png)

### <a name="how-can-i-use-defender-for-identity-information-in-an-investigation"></a>如何在調查中使用 Defender 進行身分識別資訊？

調查的詳細程度可完全符合您的需求。 以下為使用[!INCLUDE [Product short](includes/product-short.md)] 所提供的資料進行調查的一些方向。

- 檢查所有相關的使用者否都屬於相同的群組或部門？
- 相關的使用者會共用資源、應用程式或電腦嗎？
- 帳戶在經過 PasswordExpiryTime 後仍然會有效嗎？

## <a name="defender-for-identity-and-nnr-network-name-resolution"></a>適用于身分識別和 NNR 的 Defender (網路名稱解析) 

[!INCLUDE [Product short](includes/product-short.md)] 偵測功能需要使用中的網路名稱解析 (NNR)，才能對您組織中的電腦 IP 進行解析。 透過使用 NNR，[!INCLUDE [Product short](includes/product-short.md)] 就能在原始活動 (包含 IP 位址)，以及涉及各活動的相關電腦間建立相互關聯。 根據原始活動，[!INCLUDE [Product short](includes/product-short.md)] 會分析電腦等實體，並產生警示。

如果要偵測以下警訊，NNR 資料可說是不可或缺：

- 可疑的身分識別竊取 (票證傳遞)
- 可疑的 DCSync 攻擊 (目錄服務的複寫)
- 網路對應偵察 (DNS)

使用警訊下載報表中 [網路活動] 索引標籤中提供的 NNR 資訊，來判斷警訊是否為 **FP**。 一旦出現 **FP** 警訊，獲得的 NNR 確定性結果通常會具有低可信度。

下載兩個資料行中出現的報表資料：

- **來源/目的地電腦**

  - 確定性 - 低解析確定性可能代表名稱解析有誤。
- **來源/目的地電腦**
  - 解決方法 - 可提供用以解析組織中電腦 IP 的 NNR 方法。

![網路活動](media/network-activities.png)

如需如何使用[!INCLUDE [Product short](includes/product-short.md)] 安全性警示的詳細資訊，請參閱[使用安全性警示](working-with-suspicious-activities.md)。

## <a name="see-also"></a>另請參閱

- [調查使用者](investigate-a-user.md)
- [調查電腦](investigate-a-computer.md)
- [使用橫向移動路徑](use-case-lateral-movement-path.md)
- [查看[!INCLUDE [Product short](includes/product-short.md)] 論壇！](https://aka.ms/MDIcommunity)\(英文\)
