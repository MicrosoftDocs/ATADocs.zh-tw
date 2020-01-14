---
title: 如何利用 Azure ATP 來調查使用者與電腦 | Microsoft Docs
description: 描述如何使用 Azure 進階威脅防護 (ATP) 來調查使用者、實體、電腦或裝置執行的可疑活動
keywords: ''
author: shsagir
ms.author: shsagir
manager: rkarlin
ms.date: 09/15/2019
ms.topic: tutorial
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 43e57f87-ca85-4922-8ed0-9830139fe7cb
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: e4102f40c2440357798fa3d079d51380da0b2cde
ms.sourcegitcommit: 9673eb49729a06d3a25d52c0f43c76ac61b9cf89
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/12/2020
ms.locfileid: "75906303"
---
# <a name="tutorial-investigate-an-entity"></a>教學課程：調查實體

> [!NOTE]
> 此頁面所述的 Azure ATP 功能也可使用新的[入口網站](https://portal.cloudappsecurity.com)來存取。

在本教學課程中，您將了解如何針對 Azure 進階威脅防護 (ATP) 偵測到已連線至可疑活動的實體進行調查。 檢視時間軸中的安全性警訊後，您將了解如何向下切入至警訊涉及的實體，並使用下列參數與詳細資料來了解發生的問題，以及降低風險所需採取的動作。

> [!div class="checklist"]
> * 檢查實體設定檔
> * 查看實體標籤
> * 檢查使用者帳戶控制旗標
> * 利用 Windows Defender 進行交叉檢查
> * 留意敏感性使用者與群組
> * 檢閱潛在橫向移動路徑
> * 檢查 honeytoken 狀態

## <a name="check-the-entity-profile"></a>檢查實體設定檔

實體設定檔提供您專為完整深入調查使用者、電腦、裝置，以及他們有權存取的資源及其歷程記錄所設計的全方位實體頁面。 設定檔頁面會利用新的 Azure ATP 邏輯活動轉譯程式，此轉譯程式可查看一組發生的活動 (彙總最多一分鐘)，並將它們組成單一邏輯活動，以讓您更深入了解您使用者的實際活動。

若要存取實體設定檔頁面，請按一下安全性警訊時間軸中的實體名稱 (例如使用者名稱)。 您也可以將滑鼠移至實體名稱上，在安全性警訊頁面中查看迷你版本的實體設定檔。

實體設定檔可讓您檢視實體活動、檢視目錄資料，以及檢視實體的[橫向移動路徑](use-case-lateral-movement-path.md)。 如需實體的詳細資訊，請參閱[了解實體設定檔](entity-profiles.md)。

## <a name="check-entity-tags"></a>查看實體標籤

Azure ATP 會從 Active Directory 中提出標籤，以為您提供可監視 Active Directory 使用者與實體的單一介面。 這些標籤會為您提供 Active Directory 實體的資訊，包含：
- 部分：這個使用者、電腦或群組未從網域同步，而且透過通用類別目錄進行部份解析。 部分屬性無法使用。
- 未解決：這部電腦在 Active Directory 樹系中未解析為有效實體。 沒有任何目錄資訊可用。
- 已刪除：實體已從 Active Directory 刪除。
- 已停用：實體已在 Active Directory 中停用。
- 已鎖定：實體輸入錯誤密碼的次數過多，因此已鎖定。
- 已過期：實體在 Active Directory 中已過期。
- 新增：實體建立時間不到 30 天。

## <a name="check-user-account-control-flags"></a>檢查使用者帳戶控制旗標

使用者帳戶控制旗標也會從 Active Directory 匯入。 Azure ATP 實體目錄資料包含 10 個有助於調查的旗標： 
- 密碼永久有效
- 具信任可委派
- 需要智慧卡
- 密碼過期
- 允許空白密碼
- 已儲存純文字密碼
- 無法委派
- 僅限 DES 加密
- 不需要 Kerberos 預先驗證
- 帳戶已停用 

Azure ATP 能夠讓您得知這些旗標在 Active Directory 中的開啟/關閉狀態。 彩色圖示與對應的切換開關指出每個旗標的狀態。 在下面的範例中，Active Directory 只有**密碼永久有效**是開啟的。

 ![使用者帳戶控制旗標](./media/user-access-flags.png)

## <a name="cross-check-with-windows-defender"></a>利用 Windows Defender 進行交叉檢查

為提供您跨產品見解，您的實體設定檔會為在 Windows Defender 中具未解決警示的實體提供徽章。 此徽章可讓您得知該實體在 Windows Defender 中有多少未解決的警示，以及這些警示的嚴重性等級。 按一下徽章就能直接前往 Windows Defender 中與此實體相關的警示。


## <a name="keep-an-eye-on-sensitive-users-and-groups"></a>留意敏感性使用者與群組

Azure ATP 會從 Azure Active Directory 匯入使用者與群組資訊，以便您識別有哪些使用者因為在以下 Active Directory 群組中具成員身分，所以會自動視為具敏感性：

-   Administrators
-   Power Users
-   Account Operators
-   Server Operators
-   Print Operators
-   Backup Operators
-   Replicators
-   Remote Desktop Users 
-   Network Configuration Operators 
-   Incoming Forest Trust Builders
-   Domain Admins
-   網域控制站
-   Group Policy Creator Owners 
-   唯讀網域控制站 
-   企業唯讀網域控制站 
-   Schema Admins 
-   Enterprise Admins

此外，您可在 Azure ATP 中**手動標記**實體為具敏感性。 這一點很重要，因為部分 Azure ATP 偵測 (例如敏感性群組修改偵測與橫向移動路徑) 會仰賴於實體的敏感度狀態。 若您將其他使用者或群組手動標記為具敏感性 (例如董事會成員、公司主管、業務總監等)，Azure ATP 會將其視為具敏感性。 如需詳細資訊，請參閱[使用敏感性帳戶](sensitive-accounts.md)。

## <a name="review-lateral-movement-paths"></a>檢閱橫向移動路徑

Azure ATP 可協助您預防使用橫向移動路徑的攻擊。 橫向移動是攻擊者主動使用非敏感性帳戶來取得敏感性帳戶存取權的方式。

若實體存在橫向移動路徑，您便可在實體設定檔頁面中按一下 [橫向移動路徑]  索引標籤。顯示的圖表能提供您針對敏感性使用者之可能路徑的地圖。 

如需詳細資訊，請參閱[使用 Azure ATP 調查橫向移動路徑](use-case-lateral-movement-path.md)。

## <a name="check-honeytoken-status"></a>檢查 honeytoken 狀態

在您開始調查前，必須先了解實體是否為 honeytoken。 您可以將帳戶與實體標示為 Azure ATP 中的 honeytoken。 當您開啟您已標示為 honeytoken 之帳戶或實體的實體設定檔或迷你設定檔時，您會看到 honeytoken 徽章。 調查時，honeytoken 徽章可警示您正在檢閱的活動是由您標示為 honeytoken 的帳戶所執行的。

## <a name="see-also"></a>另請參閱

- [使用安全性警訊](working-with-suspicious-activities.md)
- [查看 Azure ATP 論壇！](https://aka.ms/azureatpcommunity)
