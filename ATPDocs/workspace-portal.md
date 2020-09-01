---
title: 了解 Azure 進階威脅防護入口網站
description: 描述如何登入 Azure ATP 入口網站和入口網站的元件
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 11/05/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 4ba46d60-3a74-480e-8f0f-9a082d62f343
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: fa19723ec0193a7a933eef292505a62b3d3b9961
ms.sourcegitcommit: 2be59f0bd4c9fd0d3827e9312ba20aa8eb43c6b5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88955593"
---
# <a name="working-with-the-azure-atp-portal"></a>使用 Azure ATP 入口網站

> [!NOTE]
> 您也可以使用新的 [Cloud App Security 入口網站](https://portal.cloudappsecurity.com)來存取此頁面所述的所有 Azure ATP 功能。

使用 Azure ATP 入口網站來監視及回應由 ATP 偵測到的可疑活動。

鍵入 `?` 鍵可提供 Azure ATP 入口網站協助工具的鍵盤快速鍵。

Azure ATP 入口網站可讓您依時間順序快速檢視所有可疑的活動。 不但讓您能夠深入了解任何活動，還能根據這些活動執行動作。 Azure ATP 入口網站也會顯示警訊和通知，以醒目提示 Azure ATP 所發現的問題，或是被系統視為可疑的新活動。

本文描述如何使用 Azure ATP 入口網站的關鍵項目。

## <a name="enabling-access-to-the-azure-atp-portal"></a>啟用 Azure ATP 入口網站的存取

若要成功登入 Azure ATP 入口網站，您必須使用已指派給 Azure Active Directory 安全性群組並具備 Azure ATP 入口網站存取權的使用者來登入。
如需 Azure ATP 中有關角色型存取控制 (RBAC) 的詳細資訊，請參閱[使用 Azure ATP 角色群組](atp-role-groups.md)。

## <a name="logging-into-the-azure-atp-portal"></a>登入 Azure ATP 入口網站

1. 進入 Azure ATP 入口網站的方法包括登入入口網站 [https://portal.atp.azure.com](https://portal.atp.azure.com) 並選取執行個體，或瀏覽到執行個體 URL：`https://*instancename*.atp.azure.com` 。

1. Azure ATP 支援與 Windows 驗證整合的單一登入；如果您已登入電腦，Azure ATP 會使用該權杖將您登入 Azure ATP 入口網站。 您也可以使用智慧卡進行登入。 您在 Azure ATP 中的權限會與您的[系統管理員角色](atp-role-groups.md)對應。

   > [!NOTE]
   > 請務必使用您的 Azure ATP 系統管理員使用者名稱和密碼，登入您要從中存取 Azure ATP 入口網站的電腦。 或者，您可以使用不同的使用者身分執行瀏覽器，或登出 Windows 並使用 Azure ATP 系統管理員使用者身分登入。 [Cloud App Security 入口網站](https://portal.cloudappsecurity.com)與 Azure ATP 入口網站不同，能夠提供多使用者登入，不需要額外授權就能搭配 Azure ATP 使用。

### <a name="attack-time-line"></a>攻擊時間表

攻擊時間表是您登入 Azure ATP 入口網站時會前往的預設登陸頁面。 根據預設，所有開啟的可疑活動都會顯示在攻擊時間表上。 您可以篩選攻擊時間軸，以顯示 [所有]、[開啟]、[已解除] 或 [已隱藏] 的可疑活動。 您也可以查看指派給每個活動的嚴重性。

![Azure ATP 攻擊時間表影像](media/atp-sa-timeline.png)

如需詳細資訊，請參閱[使用安全性警訊](working-with-suspicious-activities.md)。

### <a name="whats-new"></a>新增功能

Azure ATP 的新版本發行之後，[最新消息] 視窗會出現在右上角，讓您知道最新版本中新增了哪些功能。 它也會提供您可下載該版本的連結。

### <a name="filtering-panel"></a>篩選窗格

您可以根據狀態和嚴重性，篩選要顯示在攻擊時間表的可疑活動，或者要顯示在實體設定檔可疑活動索引標籤中的可疑活動。

### <a name="search-bar"></a>搜尋列 <a name="search-bar"></a>

您可以在上層功能表找到搜尋列。 您可以搜尋 Azure ATP 中的特定使用者、電腦或群組。 若要試試看，請開始輸入。 在搜尋列底部，會顯示找到的搜尋結果數目。

![Azure ATP 入口網站搜尋影像](media/atp-workspace-portal-search.png)

如果您按一下數字，就可進入搜尋結果頁面，在其中您可依實體類型篩選結果，以進一步調查。

![搜尋結果](media/search-results.png)

### <a name="health-center"></a>健康情況中心

健全狀況中心會在 Azure ATP 執行個體未正常運作時向您提出警示。

![Azure ATP 健康情況中心影像](media/atp-health-issue.png)

每當系統發生問題時 (例如連線錯誤或與 Azure ATP 獨立感應器的連線中斷)，健康情況中心圖示就會顯示一個紅點來告知您。

![Azure ATP 健康情況中心紅點影像](media/atp-health-bar.png)

### <a name="sensitive-groups"></a>敏感性群組

如需了解 Azure ATP 中敏感性群組的資訊，請參閱[使用敏感性群組](sensitive-accounts.md)。

### <a name="mini-profile"></a>小型設定檔

如果您將滑鼠暫留在 Azure ATP 入口網站中任何顯示單一實體 (例如使用者或電腦) 位置的實體上方，就會自動開啟迷你設定檔並顯示下列資訊 (如果有且相關的話)︰

![Azure ATP 小型設定檔影像](media/atp-mini-profile.png)

- Name
- 標題
- 部門
- AD 標記
- 電子郵件
- Office
- 電話號碼
- Domain
- SAM 名稱
- 建立時間：在 Active Directory 中建立實體的時間。 如果是在 Azure ATP 開始監視之前建立，則不會顯示此資訊。
- 第一次出現時間：Azure ATP 第一次從此實體觀察到活動的時間。
- 上次出現時間：Azure ATP 上次從此實體觀察到活動的時間。
- SA 徽章：如果有與此實體相關聯的可疑活動，就會顯示此徽章。
- WD ATP 徽章：如果在 Microsoft Defender ATP 中有與此實體相關聯的可疑活動，就會顯示此徽章。
- 橫向移動路徑徽章：如果在過去兩天內於此實體內偵測到橫向移動路徑，就會顯示此徽章。

## <a name="see-also"></a>另請參閱

- [建立 Azure ATP 執行個體](install-atp-step1.md)
- [查看 Azure ATP 論壇！](https://aka.ms/azureatpcommunity)
