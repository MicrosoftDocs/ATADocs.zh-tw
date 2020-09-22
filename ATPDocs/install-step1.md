---
title: 建立您自己的 Azure ATP 執行個體快速入門
description: 建立您 Azure ATP 部署執行個體的快速入門，這是安裝 Azure ATP 的第一步。
keywords: ''
author: shsagir
ms.author: shsagir
ms.date: 10/31/2019
ms.topic: quickstart
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 0fd44a4ea1b2bae549c71c957551482ba651d58f
ms.sourcegitcommit: 0c356b0860ae8663254e0cf6f04001bcc91ce207
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/21/2020
ms.locfileid: "90826782"
---
# <a name="quickstart-create-your-azure-atp-instance"></a>快速入門：建立您的 Azure ATP 執行個體

在此快速入門中，您會在 Azure ATP 入口網站中建立 Azure ATP 執行個體。 在 Azure ATP 中，您將會擁有單一執行個體 (先前稱為工作區)。 單一執行個體可讓您透過單一窗口來管理多個樹系。

> [!IMPORTANT]
> 目前，Azure ATP 資料中心部署在歐洲、英國、北美洲/中美洲/加勒比海及亞洲。 您的執行個體會自動建立在與您 Azure Active Directory (Azure AD) 地理位置最接近的資料中心內。 建立後，Azure ATP 執行個體即無法移動。

## <a name="prerequisites"></a>先決條件

- [Azure ATP 授權](technical-faq.md#licensing-and-privacy)。
- 您必須是[租用戶上的全域管理員或安全性系統管理員](/azure/active-directory/users-groups-roles/directory-assign-admin-roles#available-roles)，才能存取 Azure ATP 入口網站。
- 檢閱 [Azure ATP 架構](architecture.md)文章。
- 檢閱 [Azure ATP 必要條件](prerequisites.md)文章。

## <a name="sign-in-to-the-azure-atp-portal"></a>登入 Azure ATP 入口網站

確認您的網路符合感應器的需求後，請開始建立您的 Azure ATP 執行個體。

1. 前往 [Azure ATP 入口網站](https://portal.atp.azure.com)*。

1. 使用您的 Azure Active Directory 使用者帳戶登入。

\*GCC High 客戶必須使用 [Azure ATP GCC High](http://portal.atp.azure.us) 入口網站。

## <a name="create-your-instance"></a>建立您的執行個體

1. 按一下 [建立執行個體]  。

    ![建立 Azure ATP 執行個體](media/create-instance.png)

1. 您的 Azure ATP 執行個體會自動以 Azure AD 初始網域名稱命名，並會建立在與您 Azure AD 位置最接近的資料中心內。

    ![已建立 Azure 執行個體](media/instance-created.png)

    > [!NOTE]
    > 若要登入 Azure ATP，您必須使用已獲得 Azure ATP 角色指派，有權存取 Azure ATP 入口網站的使用者來登入。 如需 Azure ATP 中有關角色型存取控制 (RBAC) 的詳細資訊，請參閱[使用 Azure ATP 角色群組](role-groups.md)。

1. 按一下 [設定]  、[管理角色群組]  ，然後使用 [Azure AD 系統管理中心](/azure/active-directory/active-directory-assign-admin-roles-azure-portal)連結來管理您的角色群組。

    ![管理角色群組](media/creation-manage-role-groups.png)

- 資料保留 – 之前刪除的 Azure ATP 執行個體不會顯示在 UI 中。 如需 Azure ATP 資料保留的詳細資訊，請參閱 [Aure ATP 資料安全性與隱私權](privacy-compliance.md)。

## <a name="next-steps"></a>後續步驟

> [!div class="step-by-step"]
> [« 必要條件](prerequisites.md)
> [步驟 2 - 連線到 Active Directory »](install-step2.md)

## <a name="join-the-community"></a>加入社群

有更多問題嗎，或是想與其他人討論 Azure ATP 與相關的安全性？ 現在就加入 [Azure ATP 社群](https://aka.ms/azureatpcommunity)！