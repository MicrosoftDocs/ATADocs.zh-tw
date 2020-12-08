---
title: 快速入門：為適用於身分識別的 Microsoft Defender 建立執行個體
description: 快速入門：為適用於身分識別的 Microsoft Defender 建立執行個體，以開始安裝適用於身分識別的 Defender。
ms.date: 10/26/2020
ms.topic: quickstart
ms.openlocfilehash: 299edc14a51f92efa94969a3f442b2e1ca5d8e2b
ms.sourcegitcommit: cdb7ae4580851e25aae24d07e7d66a750aa54405
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2020
ms.locfileid: "96543207"
---
# <a name="quickstart-create-your-product-long-instance"></a>快速入門：建立 [!INCLUDE [Product long](includes/product-long.md)] 執行個體

在此快速入門中，您將在 [!INCLUDE [Product short](includes/product-short.md)] 入口網站中建立 [!INCLUDE [Product long](includes/product-long.md)] 執行個體。 在 [!INCLUDE [Product short](includes/product-short.md)] 中，您將會擁有單一執行個體 (先前稱為工作區)。 單一執行個體可讓您透過單一窗口來管理多個樹系。

> [!IMPORTANT]
> 目前，[!INCLUDE [Product short](includes/product-short.md)] 資料中心部署在歐洲、英國、北美洲/中美洲/加勒比海及亞洲。 您的執行個體會自動建立在與您 Azure Active Directory (Azure AD) 地理位置最接近的資料中心內。 建立後，[!INCLUDE [Product short](includes/product-short.md)] 執行個體即無法移動。

## <a name="prerequisites"></a>先決條件

- [[!INCLUDE [Product long](includes/product-long.md)] 授權](technical-faq.md#licensing-and-privacy)。
- 您必須是[租用戶上的全域管理員或安全性系統管理員](/azure/active-directory/users-groups-roles/directory-assign-admin-roles#available-roles)，才能存取 [!INCLUDE [Product short](includes/product-short.md)] 入口網站。
- 檢閱 [[!INCLUDE [Product short](includes/product-short.md)] 架構](architecture.md)一文。
- 請檢閱 [[!INCLUDE [Product short](includes/product-short.md)] 先決條件](prerequisites.md)一文。

## <a name="sign-in-to-the-product-short-portal"></a>登入 [!INCLUDE [Product short](includes/product-short.md)] 入口網站

確認網路符合感應器的需求後，請開始建立 [!INCLUDE [Product short](includes/product-short.md)] 執行個體。

1. 前往 [[!INCLUDE [Product short](includes/product-short.md)] 入口網站](https://portal.atp.azure.com)*。

1. 使用您的 Azure Active Directory 使用者帳戶登入。

\*GCC High 客戶必須使用 [[!INCLUDE [Product short](includes/product-short.md)] GCC High](http://portal.atp.azure.us) 入口網站。

## <a name="create-your-instance"></a>建立您的執行個體

1. 按一下 [建立執行個體]  。

    ![建立 [!INCLUDE [Product short](includes/product-short.md)] 執行個體](media/create-instance.png)

1. [!INCLUDE [Product short](includes/product-short.md)] 執行個體會自動以 Azure AD 初始網域名稱命名，並會建立在與您 Azure AD 位置最接近的資料中心內。

    ![已建立 Azure 執行個體](media/instance-created.png)

    > [!NOTE]
    > 若要登入 [!INCLUDE [Product short](includes/product-short.md)]，則必須使用已獲得 [!INCLUDE [Product short](includes/product-short.md)] 角色指派，且有權存取 [!INCLUDE [Product short](includes/product-short.md)] 入口網站的使用者來登入。 如需[!INCLUDE [Product short](includes/product-short.md)] 中有關角色型存取控制 (RBAC) 的詳細資訊，請參閱[使用[!INCLUDE [Product short](includes/product-short.md)] 角色群組](role-groups.md)。

1. 選取 [設定]、[管理角色群組]，然後使用 [Azure AD 系統管理中心](/azure/active-directory/active-directory-assign-admin-roles-azure-portal)連結來管理角色群組。

    ![管理角色群組](media/creation-manage-role-groups.png)

- 資料保留 – 先前刪除的 [!INCLUDE [Product short](includes/product-short.md)] 執行個體不會顯示在 UI 中。 如需 [!INCLUDE [Product short](includes/product-short.md)] 資料保留的詳細資訊，請參閱 [[!INCLUDE [Product short](includes/product-short.md)] 資料安全性與隱私權](privacy-compliance.md)。

## <a name="next-steps"></a>後續步驟

> [!div class="step-by-step"]
> [« 必要條件](prerequisites.md)
> [步驟 2 - 連線到 Active Directory »](install-step2.md)

## <a name="join-the-community"></a>加入社群

有更多問題或想與其他人討論[!INCLUDE [Product short](includes/product-short.md)] 與相關的安全性？ 立即加入[[!INCLUDE [Product short](includes/product-short.md)] 社群](https://aka.ms/MDIcommunity) \(英文\)！
