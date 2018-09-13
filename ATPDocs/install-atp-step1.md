---
title: 安裝 Azure 進階威脅防護 - 步驟 1 | Microsoft Docs
description: 安裝 Azure ATP 的第一個步驟包含建立 Azure ATP 部署的執行個體。
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 9/04/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 15ee7d0b-9a0c-46b9-bc71-98d0b4619ed0
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 6f44bbf50cff2e983a7ddb1ef1cf54ebaf928741
ms.sourcegitcommit: 7f3ded32af35a433d4b407009f87cfa6099f8edf
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/07/2018
ms.locfileid: "44126224"
---
適用於：Azure 進階威脅防護


# <a name="creating-a-workspace-in-the-azure-atp-workspace-management-portal---step-1"></a>在 Azure ATP 工作區管理入口網站中建立工作區 - 步驟 1

>[!div class="step-by-step"]
[步驟 2 »](install-atp-step2.md)

這個安裝程序提供建立及管理 Azure ATP 執行個體的指示。 如需 Azure ATP 架構的詳細資訊，請參閱 [Azure ATP 架構](atp-architecture.md)。

在 Azure ATP 中，您將有單一工作區或執行個體，可讓您統一管理多個樹系。 

> [!NOTE]
> 目前，Azure ATP 資料中心部署在歐洲、北美地區/美國中部/加勒比海和亞洲。

## <a name="step-1-enter-the-management-portal"></a>步驟 1： 進入管理入口網站

驗證您的網路符合感應器的需求之後，您接著可以建立 Azure ATP 工作區。

> [!NOTE]
>若要存取管理入口網站，您必須是該租用戶上的全域系統管理員或安全性系統管理員。


1.  進入 [Azure ATP 入口網站](https://portal.atp.azure.com)。

2.  使用您的 Azure Active Directory 使用者帳戶登入。

## <a name="step-2-create-your-workspace"></a>步驟 2： 建立工作區

1. 按一下 [建立工作區]。

2. 在 [建立新工作區] 對話方塊中，為工作區命名，並為資料中心選取 [地理位置]。 只有一個工作區可以設定為主要工作區。 將工作區設定為主要工作區會影響整合，您只能針對主要工作區將 Azure ATP 與 Windows Defender ATP 整合。 您稍後可以變更要作為主要工作區的工作區，但若要這麼做，您必須移除已針對目前主要工作區設定的所有整合。
 > [!NOTE]
 > 選取地理位置之後，就無法再加以修改。
    ![Azure ATP 工作區](media/create-workspace.png)

3. 您可以按一下 [管理 Azure ATP 使用者角色] 連結，以直接存取 [Azure Active Directory 管理中心](https://docs.microsoft.com/azure/active-directory/active-directory-assign-admin-roles-azure-portal)並管理您的角色群組。

 > [!NOTE]
 > 若要成功登入 Azure ATP，您必須使用已指派適當 Azure ATP 角色的使用者來登入，才能存取 Azure ATP 工作區入口網站。 如需 Azure ATP 中有關角色型存取控制 (RBAC) 的詳細資訊，請參閱[使用 Azure ATP 角色群組](atp-role-groups.md)。

4. 按一下新工作區的名稱，以存取該工作區的 Azure ATP 工作區入口網站。

    ![Azure ATP 工作區](media/atp-workspaces.png)

- 只能編輯主要工作區。 若要變更其他工作區，您可以將它們刪除並再次新增。 如果您想要刪除主要工作區，則必須先關閉整合，並將該工作區設定為非**主要**，之後才能刪除。
- 若要編輯主要工作區，您必須先關閉工作區中現有的整合。

- 資料保留 - 刪除的工作區不會在 UI 中顯示。 如需 Azure ATP 資料保留的詳細資訊，請參閱 [Aure ATP 資料安全性與隱私權](atp-privacy-compliance.md)。


>[!div class="step-by-step"]
[«前置安裝](configure-port-mirroring.md)
[步驟 2»](install-atp-step2.md)


## <a name="see-also"></a>另請參閱
- [Azure ATP 調整大小工具](http://aka.ms/aatpsizingtool) \(英文\)
- [設定事件收集](configure-event-collection.md)
- [Azure ATP 必要條件](atp-prerequisites.md)
- [查看 ATP 論壇！](https://aka.ms/azureatpcommunity)\(英文\)
