---
title: 適用于存取管理的身分識別角色群組的 Microsoft Defender
description: 引導您使用 Microsoft Defender 作為身分識別角色群組。
ms.date: 02/27/2020
ms.topic: conceptual
ms.openlocfilehash: 9ff271c8f417d3f2c15e3e6809b62986a7825db4
ms.sourcegitcommit: a892419a5cb95412e4643c35a9a72092421628ec
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/16/2021
ms.locfileid: "100533353"
---
# <a name="microsoft-defender-for-identity-role-groups"></a>適用于身分識別角色群組的 Microsoft Defender

[!INCLUDE [Product long](includes/product-long.md)] 提供以角色為基礎的安全性，根據組織的特定安全性和合規性需求來保護資料。 [!INCLUDE [Product short](includes/product-short.md)] 支援三種不同的角色：系統管理員、使用者和檢視器。

[!INCLUDE [Handle personal data](../includes/gdpr-intro-sentence.md)]

角色群組可啟用的存取管理 [!INCLUDE [Product short](includes/product-short.md)] 。 使用角色群組可以隔離安全性小組內的責任，並授與使用者執行工作所需的存取權。 本文說明存取管理、 [!INCLUDE [Product short](includes/product-short.md)] 角色授權，並協助您在中啟動並執行角色群組 [!INCLUDE [Product short](includes/product-short.md)] 。

> [!NOTE]
> 租使用者 Azure Active Directory 上的任何全域管理員或安全性系統管理員都會自動成為 [!INCLUDE [Product short](includes/product-short.md)] 系統管理員。

## <a name="accessing-the-defender-for-identity-portal"></a>存取身分識別入口網站的 Defender

[!INCLUDE [Product short](includes/product-short.md)]只有具有全域管理員或安全性系統管理員目錄角色的 Azure AD 使用者才能完成入口網站 (portal.atp.azure.com) 的存取權。 使用必要的角色進入入口網站之後，您可以建立 [!INCLUDE [Product short](includes/product-short.md)] 實例。 [!INCLUDE [Product short](includes/product-short.md)] 服務會在您的 Azure Active Directory 租使用者中建立三個安全性群組：系統管理員、使用者、檢視器。

> [!NOTE]
> 入口網站的存取權 [!INCLUDE [Product short](includes/product-short.md)] 只會授與安全性群組中的使用者 [!INCLUDE [Product short](includes/product-short.md)] 、您的 Azure Active Directory 內的使用者，以及租使用者的全域和安全性系統管理員。

## <a name="types-of-defender-for-identity-security-groups"></a>身分識別安全性群組的 Defender 類型

[!INCLUDE [Product short](includes/product-short.md)] 提供三種類型的安全性群組： Azure ATP *(實例名稱)* 系統管理員、Azure ATP (使用者) *實例* 名稱，以及 Azure ATP 檢視器 (*實例名稱*) 檢視器。 下表說明 [!INCLUDE [Product short](includes/product-short.md)] 入口網站中每個角色可用的存取類型。 根據您指派的角色而定，入口網站中的各種畫面與功能表選項 [!INCLUDE [Product short](includes/product-short.md)] 無法供這些使用者使用，如下所示：

|活動 |) 系統管理員 Azure ATP *(實例名稱*|Azure ATP *(實例名稱)* 使用者|) 檢視器 Azure ATP *(實例名稱*|
|----|----|----|----|
|變更健康情況警示的狀態|可用|無法使用|無法使用|
|變更安全性警訊的狀態 (重新開啟、關閉、排除、隱藏)|可用|可用|無法使用|
|刪除實例|可用|無法使用|無法使用|
|下載報表|可用|可用|可用|
|登入|可用|可用|可用|
|共用/匯出安全性警訊 (透過電子郵件、取得連結、下載詳細資料)|可用|可用|可用|
|更新設定 [!INCLUDE [Product short](includes/product-short.md)] -更新|可用|無法使用|無法使用|
|更新設定 [!INCLUDE [Product short](includes/product-short.md)] - (敏感性和 honeytoken) 的實體標記|可用|可用|無法使用|
|更新設定 [!INCLUDE [Product short](includes/product-short.md)] -排除|可用|可用|無法使用|
|更新設定 [!INCLUDE [Product short](includes/product-short.md)] -語言|可用|可用|無法使用|
|更新設定 [!INCLUDE [Product short](includes/product-short.md)] - (電子郵件和 syslog) 的通知|可用|可用|無法使用|
|更新設定 [!INCLUDE [Product short](includes/product-short.md)] -預覽偵測|可用|可用|無法使用|
|更新 [!INCLUDE [Product short](includes/product-short.md)] 設定-排程的報表|可用|可用|無法使用|
|更新設定 [!INCLUDE [Product short](includes/product-short.md)] -資料來源 (目錄服務、SIEM、VPN WD-ATP) |可用|無法使用|無法使用|
|更新設定 [!INCLUDE [Product short](includes/product-short.md)] -感應器 (下載、重新產生金鑰、設定、刪除) |可用|無法使用|無法使用|
|檢視實體設定檔和安全性警訊|可用|可用|可用|

當使用者嘗試存取不適用於其角色群組的頁面時，系統會將他們重新導向至 [!INCLUDE [Product short](includes/product-short.md)] 未授權的頁面。

## <a name="add-and-remove-users"></a>新增及移除使用者

[!INCLUDE [Product short](includes/product-short.md)] 使用 Azure AD 安全性群組作為角色群組的基礎。 角色群組可以從 [ [群組管理] 頁面](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/GroupsManagementMenuBlade/All%20groups)進行管理。 只可以將 Azure AD 使用者加入或移除自安全性群組。

## <a name="see-also"></a>另請參閱

- [[!INCLUDE [Product short](includes/product-short.md)] 大小調整工具](https://aka.ms/aatpsizingtool) \(英文\)
- [[!INCLUDE [Product short](includes/product-short.md)] 架構](architecture.md)
- [安裝[!INCLUDE [Product short](includes/product-short.md)]](install-step1.md)
- [查看[!INCLUDE [Product short](includes/product-short.md)] 論壇！](https://aka.ms/MDIcommunity)\(英文\)
