---
title: 安裝 Azure 進階威脅防護 | Microsoft Docs
description: 安裝 Azure ATP 的第一個步驟包含建立 Azure ATP 部署的執行個體。
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 10/4/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 15ee7d0b-9a0c-46b9-bc71-98d0b4619ed0
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 97cce3de3a1cbe049523c54901ecbc9228aaee53
ms.sourcegitcommit: 27cf312b8ebb04995e4d06d3a63bc75d8ad7dacb
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/04/2018
ms.locfileid: "48783004"
---
適用於：Azure 進階威脅防護


# <a name="creating-your-azure-atp-instance-in-the-portal---step-1"></a>在入口網站中建立您的 Azure ATP 執行個體 - 步驟 1

> [!div class="step-by-step"]
> [步驟 2 »](install-atp-step2.md)

這個安裝程序提供建立及管理 Azure ATP 執行個體或工作區的指示。 如需 Azure ATP 架構的詳細資訊，請參閱 [Azure ATP 架構](atp-architecture.md)。

在 Azure ATP 中，您將有單一執行個體或工作區，以透過單一管理點來管理多個樹系。 

> [!NOTE]
> 目前，Azure ATP 資料中心部署在歐洲、北美地區/美國中部/加勒比海和亞洲。

## <a name="step-1-enter-the-azure-atp-portal"></a>步驟 1： 進入 Azure ATP 入口網站

驗證您的網路符合感應器的需求之後，您接著可以建立 Azure ATP 工作區。

> [!NOTE]
>若要存取管理入口網站，您必須是該租用戶上的全域系統管理員或安全性系統管理員。


1.  進入 [Azure ATP 入口網站](https://portal.atp.azure.com)。

2.  使用您的 Azure Active Directory 使用者帳戶登入。

## <a name="step-2-create-your-workspace"></a>步驟 2： 建立工作區

1. 按一下 [建立工作區]。

2. 在 [建立新工作區] 對話方塊中，為工作區命名，並為資料中心選取 [地理位置]。 您的工作區預設為**主要**。 
 > [!NOTE]
 > 選取地理位置之後，就無法再加以修改。
    ![Azure ATP 工作區](media/create-workspace.png)

3. 您可以按一下 [管理 Azure ATP 使用者角色] 連結，以直接存取 [Azure Active Directory 管理中心](https://docs.microsoft.com/azure/active-directory/active-directory-assign-admin-roles-azure-portal)並管理您的角色群組。

 > [!NOTE]
 > 若要成功登入 Azure ATP，您必須使用已指派適當 Azure ATP 角色的使用者來登入，才能存取 Azure ATP 入口網站。 如需 Azure ATP 中有關角色型存取控制 (RBAC) 的詳細資訊，請參閱[使用 Azure ATP 角色群組](atp-role-groups.md)。

4. 按一下您的工作區名稱，以存取 Azure ATP 入口網站。

    ![Azure ATP 工作區](media/atp-workspaces.png)

- 只能編輯主要工作區。 如果您想要刪除主要工作區，則必須先關閉整合，之後才能刪除。

- 資料保留 – 之前刪除的工作區不會在 UI 中顯示。 如需 Azure ATP 資料保留的詳細資訊，請參閱 [Aure ATP 資料安全性與隱私權](atp-privacy-compliance.md)。


>[!div class="step-by-step"]
[«前置安裝](atp-prerequisites.md)
[步驟 2»](install-atp-step2.md)



## <a name="see-also"></a>另請參閱
- [Azure ATP 調整大小工具](http://aka.ms/aatpsizingtool) \(英文\)
- [設定事件收集](configure-event-collection.md)
- [Azure ATP 必要條件](atp-prerequisites.md)
- [查看 Azure ATP 論壇！](https://aka.ms/azureatpcommunity)
