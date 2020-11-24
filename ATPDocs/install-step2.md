---
title: 快速入門：將適用於身分識別的 Microsoft Defender 連線至 Active Directory
description: 在安裝適用於身分識別的 Microsoft Defender 中，其步驟 2 可協助您為適用於身分識別的 Defender 雲端服務進行網域連線設定
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 10/26/2020
ms.topic: quickstart
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 58a5f6c37a5b5bc4e224393aac5ad9771d6a1f6b
ms.sourcegitcommit: e2227c0b0e5aaa5163dc56d4131ca82f8dca8fb0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2020
ms.locfileid: "94847865"
---
# <a name="quickstart-connect-to-your-active-directory-forest"></a>快速入門：連線到您的 Active Directory 樹系

在此快速入門中，您會將 [!INCLUDE [Product long](includes/product-long.md)] 連線到 Active Directory (AD)，以擷取使用者和電腦的相關資料。 若您要連線多個樹系，請參閱[多樹系支援](multi-forest.md)一文。

## <a name="prerequisites"></a>Prerequisites

- [[!INCLUDE [Product short](includes/product-short.md)] 執行個體](install-step1.md)。
- 請檢閱 [[!INCLUDE [Product short](includes/product-short.md)] 先決條件](prerequisites.md)一文。
- 至少下列其中一個目錄服務帳戶，該帳戶必須有所提及網域中所有物件的讀取權限：
  - **標準** AD 使用者帳戶與密碼。 為執行 Windows Server 2008 R2 SP1 的感應器所需。
  - **群組受管理的服務帳戶** (gMSA)。 需要 Windows Server 2012 或更新版本。  
  所有感應器都必須有可擷取 gMSA 帳戶密碼的權限。 如需建立 gMSA 帳戶的相關資訊，請參閱[設定 gMSA 帳戶](#how-to-set-up-a-gmsa-account)。

    > [!NOTE]
    >
    > - 針對執行 Windows Server 2012 與更新版本的感應器電腦，我們建議使用 **gMSA** 帳戶，以獲得改善的安全性與自動密碼管理。
    > - 若您有多個感應器，其中有些執行 Windows Server 2008，而其他執行 Windows Server 2012 或更新版本，則除了使用 **gMSA** 帳戶的建議之外，您也必須使用至少一個 **標準** AD 使用者帳戶。

### <a name="how-to-set-up-a-gmsa-account"></a>如何設定 gMSA 帳戶

1. 建立 [gMSA 帳戶](/windows-server/security/group-managed-service-accounts/getting-started-with-group-managed-service-accounts#BKMK_CreateGMSA)。
1. 建立新的[安全性群組，其中包含具有感應器的所有網域控制站 (執行 Windows Server 2012 或更新版本)](/windows-server/security/group-managed-service-accounts/getting-started-with-group-managed-service-accounts#BKMK_AddMemberHosts)，該群組必須具有可擷取 gMSA 帳戶密碼的權限。 (建議使用)

## <a name="provide-a-username-and-password-to-connect-to-your-active-directory-forest"></a>提供使用者名稱和密碼來連線到您的 Active Directory 樹系

當第一次開啟 [!INCLUDE [Product short](includes/product-short.md)] 入口網站時，會出現下列畫面：

![[!INCLUDE [Product short](includes/product-short.md)] 歡迎階段 1](media/directory-services.png)

1. 輸入下列資訊，然後按一下 [儲存]：

    |欄位|註解|
    |---|---|
    |**使用者名稱** (必填)|輸入唯讀 AD 使用者名稱。 例如：**DefenderForIdentityUser**。 您必須使用 **標準** AD 使用者或 gMSA 帳戶。 **請勿** 使用您使用者名稱的 UPN 格式。|
    |**密碼** (為標準 AD 使用者帳戶所需)|(僅限 AD 使用者帳戶) 輸入唯讀使用者的密碼。 例如：**Pencil1**。|
    |**群組受管理的服務帳戶** (為 gMSA 帳戶所需)|(僅限 gMSA 帳戶) 選取 [群組受管理的服務帳戶]。|
    |**網域** (必填)|輸入唯讀使用者的網域。 例如：**contoso.com**。 請務必輸入使用者所在網域的完整 FQDN。 例如，如果使用者的帳戶是在 corp.contoso.com 網域中，則需要輸入 `corp.contoso.com`，而非 contoso.com|

1. 在 [!INCLUDE [Product short](includes/product-short.md)] 入口網站中，按一下 [下載感應器安裝程式並安裝第一個感應器] 以繼續。

## <a name="next-steps"></a>後續步驟

> [!div class="step-by-step"]
> [« 步驟 1 - 建立 [!INCLUDE [Product short](includes/product-short.md)] 執行個體](install-step1.md)
> [步驟 3 - 下載感應器安裝程式 »](install-step3.md)

## <a name="join-the-community"></a>加入社群

有更多問題或想與其他人討論[!INCLUDE [Product short](includes/product-short.md)] 與相關的安全性？ 立即加入[[!INCLUDE [Product short](includes/product-short.md)] 社群](https://aka.ms/MDIcommunity) \(英文\)！
