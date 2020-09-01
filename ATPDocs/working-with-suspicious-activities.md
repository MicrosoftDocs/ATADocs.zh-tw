---
title: 使用 Azure 進階威脅防護中的安全性警訊
description: 描述如何檢閱 Azure ATP 發出的安全性警訊
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 01/26/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: a06004bd-9f77-4e8e-a0e5-4727d6651a0f
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 331f709c19008e1f11aacc50678893158528042d
ms.sourcegitcommit: 2be59f0bd4c9fd0d3827e9312ba20aa8eb43c6b5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88955559"
---
# <a name="working-with-security-alerts"></a>使用安全性警訊

> [!NOTE]
> 此頁面所述的 Azure ATP 功能也可使用新的[入口網站](https://portal.cloudappsecurity.com)來存取。

本文說明使用 Azure ATP 安全性警訊的基本概念。

## <a name="review-security-alerts-on-the-attack-timeline"></a>檢閱攻擊時間軸上的安全性警訊 <a name="review-suspicious-activities-on-the-attack-time-line"></a>

登入 Azure ATP 入口網站後，系統會自動帶您前往開啟的**安全性警訊時間軸**。 安全性警訊會依時間順序列出，最新的警訊會位於時間軸頂端。

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

![Azure ATP 安全性警訊時間軸影像](media/atp-sa-timeline.png)

## <a name="security-alert-categories"></a>安全性警訊類別

Azure ATP 安全性警訊分為下列類別或階段，如同在典型網路攻擊終止鏈結中會看到的階段。

- [偵察警訊](atp-reconnaissance-alerts.md)
- [遭入侵的認證警訊](atp-compromised-credentials-alerts.md)
- [橫向移動警訊](atp-lateral-movement-alerts.md)
- [網域支配警訊](atp-domain-dominance-alerts.md)
- [外流警訊](atp-exfiltration-alerts.md)

## <a name="preview-detections"></a>預覽偵測 <a name="preview-detections"></a>

Azure ATP 研究小組會持續致力於實作新偵測攻擊的新探索。 由於 Azure ATP 是雲端服務，所以新偵測能快速推出，讓 Azure ATP 客戶盡快享受到新偵測的優點。

這些偵測會標上預覽徽章，協助您找出新偵測，並知道它們是產品的新偵測。 如果您關閉預覽偵測，則它們不會顯示在 Azure ATP 主控台中 (不在時間軸或實體設定檔中)，而且不會開啟新警示。

![預覽偵測 VPN](media/preview-detection-vpn.png)

預設會在 Azure ATP 中啟用預覽偵測。

停用預覽偵測：

1. 在 Azure ATP 主控台中，按一下設定 cog。
1. 在左功能表中，按一下 [偵測]  。
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

![Azure ATP 的安全性警訊動作](media/atp-sa-actions.png)

**安全性警訊狀態**

- **開啟**：所有新的安全性警訊都會顯示在這份清單中。

- **關閉**：用於追蹤您已識別、研究並修正以緩解的安全性警訊。

- **隱藏**：隱藏警訊表示您想要暫時忽略它，只有出現新的執行個體時，才會再次收到通知。 這表示如果有類似的警示，Azure ATP 將不會重新開啟它。 但如果此警示在停止七天後再次出現，便會開啟新的警示。

- **刪除**：如果您刪除警示，即會將其從系統和資料庫中刪除，且您將「無法」予以還原。 按一下 [刪除] 之後，您即可刪除相同類型的所有安全性警訊。

- **排除**：排除實體使其不會引發更多特定類型警示的功能。 例如，您可以將 Azure ATP 設定為排除特定實體 (使用者或電腦)，使其不會再引發特定類型的活動警訊，例如執行遠端程式碼的特定系統管理員，或執行 DNS 探查的安全性掃描程式。 除了能夠直接在安全性警訊上新增排除項目之外 (因為已在時間軸中偵測到此警訊)，您也可以移至 [設定] 頁面，再移至 [排除]  ，並針對每個安全性警訊，手動新增及移除排除的實體或子網路 (例如針對傳遞票證的情況)。

> [!NOTE]
> 只有 Azure ATP 系統管理員才能修改設定頁面。

## <a name="see-also"></a>另請參閱

- [使用 Azure ATP 入口網站](workspace-portal.md)
- [查看 Azure ATP 論壇！](https://aka.ms/azureatpcommunity)
