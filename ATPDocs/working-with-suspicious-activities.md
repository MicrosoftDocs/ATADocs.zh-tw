---
title: 在適用於身分識別的 Microsoft Defender 中使用安全性警示
description: 描述如何檢閱適用於身分識別的 Microsoft Defender 所發出的安全性警示
ms.date: 10/27/2020
ms.topic: how-to
ms.openlocfilehash: cb589442143bfd78f13360c076d9f5205c0a21af
ms.sourcegitcommit: a892419a5cb95412e4643c35a9a72092421628ec
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/16/2021
ms.locfileid: "100534424"
---
# <a name="working-with-security-alerts"></a>使用安全性警訊

> [!NOTE]
> 此頁面所述的[!INCLUDE [Product long](includes/product-long.md)] 功能也可使用新的[入口網站](https://portal.cloudappsecurity.com)來存取。

此文章說明使用[!INCLUDE [Product long](includes/product-long.md)] 安全性警示的基本概念。

<a name="review-suspicious-activities-on-the-attack-time-line"></a>

## <a name="review-security-alerts-on-the-attack-timeline"></a>檢閱攻擊時間軸上的安全性警訊 

登入[!INCLUDE [Product short](includes/product-short.md)] 入口網站後，系統會自動帶您前往開啟的 **安全性警示時間表**。 安全性警訊會依時間順序列出，最新的警訊會位於時間軸頂端。

每個安全性警訊具有下列資訊：

- 涉及的實體，包括使用者、電腦、伺服器、網域控制站以及資源。

- 起始安全性警訊的可疑活動時間和時間範圍。
- 警訊的嚴重性：高、中或低。
- 狀態：開啟、已關閉或已隱藏。
- 能力：
  - 透過電子郵件將安全性警訊分享給組織中的其他人員。
  - 以 Excel 格式下載安全性警訊。

> [!NOTE]
>
> - 當您將滑鼠暫留在使用者或電腦上時，就會顯示迷你實體設定檔。 迷你設定檔可提供實體的額外資訊，並包含與實體連結的安全性警訊數目。
> - 按一下實體，您便會前往使用者或電腦的實體設定檔。

![[!INCLUDE [Product short](includes/product-short.md)] 安全性警示時間表影像](media/sa-timeline.png)

## <a name="security-alert-categories"></a>安全性警訊類別

[!INCLUDE [Product short](includes/product-short.md)] 安全性警示分為下列類別或階段，如同在典型網路攻擊狙殺鏈中會看到的階段。

- [偵察警訊](reconnaissance-alerts.md)
- [遭入侵的認證警訊](compromised-credentials-alerts.md)
- [橫向移動警訊](lateral-movement-alerts.md)
- [網域支配警訊](domain-dominance-alerts.md)
- [外流警訊](exfiltration-alerts.md)

## <a name="preview-detections"></a>預覽偵測 

[!INCLUDE [Product short](includes/product-short.md)] 研究小組會持續致力於針對新探索到的攻擊實作新的偵測。 由於[!INCLUDE [Product short](includes/product-short.md)] 是雲端服務，所以能快速推出新的偵測，讓[!INCLUDE [Product short](includes/product-short.md)] 客戶能盡快受益於新的偵測。

這些偵測會標上預覽徽章，協助您找出新偵測，並知道它們是產品的新偵測。 如果您關閉預覽偵測，其將不會顯示在[!INCLUDE [Product short](includes/product-short.md)] 主控台中 (不在時間表或實體設定檔中)，而且不會開啟新警示。

![時間表中的預覽偵測](media/preview-detection-in-timeline.png)

根據預設，[!INCLUDE [Product short](includes/product-short.md)] 中會啟用預覽偵測。

停用預覽偵測：

1. 在[!INCLUDE [Product short](includes/product-short.md)] 主控台中，選取 [設定]。
1. 在左功能表中，於 [預覽] 底下，按一下 [偵測]。
1. 使用滑桿開啟和關閉預覽偵測。

![預覽偵測](media/preview-detections.png)

## <a name="filter-security-alerts-list"></a>篩選安全性警訊清單

若要篩選安全性警訊清單：

1. 在畫面左側的 [篩選依據]  窗格中，選取以下其中一個選項︰[所有]  、[開啟]  、[已關閉]  或 [已隱藏]  。

1. 若要進一步篩選清單，請選取 [高]  、[中]  或 [低]  。

**可疑活動嚴重性**

- **低**

    表示可能會導致攻擊的活動；惡意使用者或軟體會透過這些攻擊來存取組織的資料。

- **中**

    表示可能會讓特定身分識別陷入更嚴重攻擊風險的活動，這些攻擊可能會導致身分識別盜用或特殊權限的提升。

- **高**

    表示可能會導致身分識別盜用、權限提升或其他重大影響攻擊的活動

## <a name="managing-security-alerts"></a>管理安全性警訊

您可以按一下安全性警訊的目前狀態，然後選取下列其中一項來變更安全性警訊的狀態：[開啟]  、[已隱藏]  、[已關閉]  或 [已刪除]  。
若要這樣做，請按一下特定警訊右上角的三個點，以顯示可用的動作清單。

![適用於安全性警示的[!INCLUDE [Product short](includes/product-short.md)] 動作](media/sa-actions.png)

**安全性警訊狀態**

- **開啟**：所有新的安全性警訊都會顯示在這份清單中。

- **關閉**：用於追蹤您已識別、研究並修正以緩解的安全性警訊。

- **隱藏**：隱藏警訊表示您想要暫時忽略它，只有出現新的執行個體時，才會再次收到通知。 這表示如果有類似的警示，[!INCLUDE [Product short](includes/product-short.md)] 不會加以重新開啟。 但如果此警示在停止七天後再次出現，便會開啟新的警示。

- **刪除**：如果您刪除警示，即會將其從系統和資料庫中刪除，且您將「無法」予以還原。 按一下 [刪除] 之後，您即可刪除相同類型的所有安全性警訊。

- **排除**：排除實體使其不會引發更多特定類型警示的功能。 例如，您可以將[!INCLUDE [Product short](includes/product-short.md)] 設定為排除特定實體 (使用者或電腦)，使其不會再次引發特定活動類型的警示，例如會執行遠端程式碼的特定管理員，或是會執行 DNS 偵察的安全性掃描器。 除了能夠直接在安全性警訊上新增排除項目之外 (因為已在時間軸中偵測到此警訊)，您也可以移至 [設定] 頁面，再移至 [排除]  ，並針對每個安全性警訊，手動新增及移除排除的實體或子網路 (例如針對傳遞票證的情況)。

> [!NOTE]
> 只有[!INCLUDE [Product short](includes/product-short.md)] 管理員才能修改設定頁面。

## <a name="see-also"></a>另請參閱

- [使用[!INCLUDE [Product short](includes/product-short.md)] 入口網站](workspace-portal.md)
- [查看[!INCLUDE [Product short](includes/product-short.md)] 論壇！](https://aka.ms/MDIcommunity)\(英文\)
