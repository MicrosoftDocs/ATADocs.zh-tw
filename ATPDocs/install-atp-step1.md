---
title: 安裝 Azure 進階威脅防護 | Microsoft Docs
description: 安裝 Azure ATP 的第一個步驟包含建立 Azure ATP 部署的執行個體。
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 12/02/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 15ee7d0b-9a0c-46b9-bc71-98d0b4619ed0
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 3fb857308d945fcae04e7dc3d501404a2334382e
ms.sourcegitcommit: f4f2a1b2c674c4dba7a46ece0624f5ea10c4865e
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/02/2018
ms.locfileid: "52744688"
---
適用於：Azure 進階威脅防護


# <a name="creating-your-azure-atp-instance-in-the-azure-atp-portal---step-1"></a>在 Azure ATP 入口網站中建立您的 Azure ATP 執行個體 - 步驟 1

> [!div class="step-by-step"]
> [步驟 2 »](install-atp-step2.md)

此安裝程序提供建立及管理 Azure ATP 執行個體 (先前稱為工作區) 的指示。 如需 Azure ATP 架構的詳細資訊，請參閱 [Azure ATP 架構](atp-architecture.md)。

在 Azure ATP 中，您將擁有單一執行個體，可讓您透過單一窗口來管理多個樹系。 

> [!NOTE]
> 目前，Azure ATP 資料中心部署在歐洲、北美地區/美國中部/加勒比海和亞洲。 您的執行個體會自動在與您 AAD 地理位置最接近的資料中心內建立。 一旦建立後，Azure ATP 執行個體便無法移動。 

## <a name="step-1-enter-the-azure-atp-portal"></a>步驟 1： 進入 Azure ATP 入口網站

確認您的網路符合感應器的需求後，請繼續建立您的 Azure ATP 執行個體。

> [!NOTE]
>若要存取 Azure ATP 入口網站，您必須是該租用戶上的全域系統管理員或安全性系統管理員。


1.  進入 [Azure ATP 入口網站](https://portal.atp.azure.com)。

2.  使用您的 Azure Active Directory 使用者帳戶登入。

## <a name="step-2-create-your-instance"></a>步驟 2： 建立您的執行個體

1. 按一下 [建立執行個體]。 

    ![建立 Azure ATP 執行個體](media/create-instance.png)

2. 您的 Azure ATP 執行個體會自動以 AAD 初始網域名稱命名，並會配置到與您 AAD 位置最接近的資料中心建立。 

    ![已建立 Azure 執行個體](media/instance-created.png)

> [!NOTE]
 > 若要登入 Azure ATP，您必須使用已指派具 Azure ATP 入口網站存取權限的 Azure ATP 角色使用者來登入。 如需 Azure ATP 中有關角色型存取控制 (RBAC) 的詳細資訊，請參閱[使用 Azure ATP 角色群組](atp-role-groups.md)。
 
3. 按一下 [設定]、[管理角色群組]，然後使用 [Azure AD 系統管理中心](https://docs.microsoft.com/azure/active-directory/active-directory-assign-admin-roles-azure-portal)連結來管理您的角色群組。 。

    ![管理角色群組](media/creation-manage-role-groups.png)

- 資料保留 – 之前刪除的 Azure ATP 執行個體不會在 UI 中顯示。 如需 Azure ATP 資料保留的詳細資訊，請參閱 [Aure ATP 資料安全性與隱私權](atp-privacy-compliance.md)。


>[!div class="step-by-step"]
[«前置安裝](atp-prerequisites.md)
[步驟 2»](install-atp-step2.md)



## <a name="see-also"></a>另請參閱
- [Azure ATP 調整大小工具](http://aka.ms/aatpsizingtool) \(英文\)
- [設定事件收集](configure-event-collection.md)
- [Azure ATP 必要條件](atp-prerequisites.md)
- [查看 Azure ATP 論壇！](https://aka.ms/azureatpcommunity)
