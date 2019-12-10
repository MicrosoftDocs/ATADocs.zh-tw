---
title: 將 Azure ATP 連線到 Active Directory 快速入門 | Microsoft Docs
description: 安裝 Azure ATP 的步驟 2 可協助您設定 Azure ATP 雲端服務上的網域連線設定
author: mlottner
ms.author: mlottner
ms.date: 02/05/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.openlocfilehash: 3e39bcdd5b3ffbe7a1d39064d28851fba7058d94
ms.sourcegitcommit: 6dd002b5a34f230aaada55a6f6178c2f9e1584d9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2019
ms.locfileid: "56263944"
---
# <a name="quickstart-connect-to-your-active-directory-forest"></a>快速入門：連線到您的 Active Directory 樹系

在此快速入門中，您會將 Azure ATP 連線到 Active Directory (AD)，來擷取使用者和電腦的相關資料。 若您要連線多個樹系，請參閱[多樹系支援](atp-multi-forest.md)一文。

## <a name="prerequisites"></a>必要條件

- [Azure ATP 執行個體](install-atp-step1.md)。
- 檢閱 [Azure ATP 必要條件](atp-prerequisites.md)文章。
- 針對監視網域中的所有物件具有讀取存取權的**內部部署** AD 使用者帳戶和密碼。

## <a name="provide-a-username-and-password-to-connect-to-your-active-directory-forest"></a>提供使用者名稱和密碼來連線到您的 Active Directory 樹系

當您第一次開啟 Azure ATP 入口網站時，會出現下列畫面：

![Azure ATP 歡迎使用階段 1](media/directory-services.png)


1. 輸入下列資訊，然後按一下 [儲存]  ：

    |欄位|註解|
    |---------|------------|
    |**使用者名稱** (必填)|輸入唯讀 Active Directory 使用者名稱。 例如：**ATPuser**。  您必須使用**內部部署** AD 使用者帳戶。 **請勿**使用您使用者名稱的 UPN 格式。|
    |**密碼** (必填)|輸入唯讀使用者的密碼。 例如：**Pencil1**。|
    |**網域** (必填)|輸入唯讀使用者的網域。 例如：**contoso.com**。 請務必輸入使用者所在網域的完整 FQDN。 例如，如果使用者的帳戶是在 corp.contoso.com 網域中，您需要輸入 `corp.contoso.com`，而非 contoso.com|

2. 在 Azure ATP 入口網站中，按一下 [下載感應器安裝程式並安裝第一個感應器]  以繼續。


## <a name="next-steps"></a>後續步驟

> [!div class="step-by-step"]
> [« 步驟 1 - 建立 Azure ATP 執行個體](install-atp-step1.md)
> [步驟 3 - 下載感應器安裝程式 »](install-atp-step3.md)

## <a name="join-the-community"></a>加入社群

有更多問題嗎，或是想與其他人討論 Azure ATP 與相關的安全性？ 現在就加入 [Azure ATP 社群](https://aka.ms/azureatpcommunity)！
