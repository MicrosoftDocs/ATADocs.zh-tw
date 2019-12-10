---
title: 適用於存取管理的 Azure 進階威脅防護角色群組 | Microsoft Docs
description: 逐步引導您使用 Azure ATP 角色群組。
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 11/29/2018
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: effca0f2-fcae-4fca-92c1-c37306decf84
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: e2e3b35373bdfaaa0d13c1c175deea12bf24a34d
ms.sourcegitcommit: 6dd002b5a34f230aaada55a6f6178c2f9e1584d9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2019
ms.locfileid: "65195466"
---
# <a name="azure-atp-role-groups"></a>Azure ATP 角色群組

Azure ATP 提供角色型安全性，可根據組織的特定安全性和合規性需求來保護資料。 Azure ATP 支援三種不同的角色：系統管理員、使用者和檢視者。 

[!INCLUDE [Handle personal data](../includes/gdpr-intro-sentence.md)]

角色群組可針對 Azure ATP 啟用存取管理。 使用角色群組可以隔離安全性小組內的責任，並授與使用者執行工作所需的存取權。 本文說明存取管理與 Azure ATP 角色授權，並可協助您在 Azure ATP 中開始使用角色群組。

> [!NOTE]
> 租用戶 Azure Active Directory 上的任何全域管理員或安全性系統管理員，都會自動是 Azure ATP 系統管理員。

## <a name="accessing-the-azure-atp-portal"></a>存取 Azure ATP 入口網站

只有具備全域管理員或安全性系統管理員目錄角色的 Azure AD 使用者，才能存取 Azure ATP 入口網站 (portal.atp.azure.com)。 在使用必要角色進入入口網站後，您便可以建立 Azure ATP 執行個體。 Azure ATP 服務會在 Azure Active Directory 租用戶中建立三個安全性群組：Administrators、Users、Viewers。 

> [!NOTE]
> Azure ATP 入口網站的存取權只會授與 Azure Active Directory 中 Azure ATP 安全性群組內的使用者，以及租用戶的全域系統管理員及安全性系統管理員。


## <a name="types-of-azure-atp-security-groups"></a>Azure ATP 安全性群組的類型 

Azure ATP 提供三種類型的安全性群組：Azure ATP (「執行個體名稱」)  系統管理員、Azure ATP (「執行個體名稱」)  使用者和 Azure ATP (「執行個體名稱」)  檢視者。 下表描述每個角色在 Azure ATP 入口網站中可用的存取類型。 根據您所指派的角色而定，這些使用者將會無法使用 Azure ATP 入口網站中的各種畫面與功能表選項，如下所示：

|活動 |Azure ATP (「執行個體名稱」)  系統管理員|Azure ATP (「執行個體名稱」)  使用者|Azure ATP (「執行個體名稱」)  檢視者|
|----|----|----|----|
|登入|可用|可用|可用|
|變更安全性警訊的狀態 (重新開啟、關閉、排除、隱藏)|可用|可用|無法使用|
|共用/匯出安全性警訊 (透過電子郵件、取得連結、下載詳細資料)|可用|可用|可用|
|下載報表|可用|可用|可用|
|變更監視警示的狀態|可用|無法使用|無法使用|
|更新 Azure ATP 設定 - 感應器 (下載、重新產生金鑰、設定、刪除)|可用|無法使用|無法使用|
|更新 Azure ATP 設定 - 資料來源 (目錄服務、SIEM、VPN WD-ATP)|可用|無法使用|無法使用|
|更新 ATP 設定 - 更新|可用|無法使用|無法使用|
|更新 ATP 設定 - 排程報告|可用|可用|無法使用|
|更新 ATP 設定 - 實體標記 (敏感性和 honeytoken)|可用|可用|無法使用|
|更新 ATP 設定 - 排除|可用|可用|無法使用|
|更新 ATP 設定 - 語言|可用|可用|無法使用|
|更新 ATP 設定 - 通知 (電子郵件和 syslog)|可用|可用|無法使用|
|更新 ATP 設定 - 預覽偵測|可用|可用|無法使用|
|檢視實體設定檔和安全性警訊|可用|可用|可用|


當使用者嘗試存取不適用於其角色群組的頁面時，便會被重新導向至 Azure ATP 未授權頁面。 

## <a name="add-and-remove-users"></a>新增及移除使用者 


Azure ATP 使用 Azure AD 安全性群組作為角色群組的基礎。 您可以從 [https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/GroupsManagementMenuBlade/All%20groups](https://aad.portal.azure.com/#blade/Microsoft_AAD_IAM/GroupsManagementMenuBlade/All%20groups) 管理角色群組。 只可以將 Azure AD 使用者加入或移除自安全性群組。 

## <a name="see-also"></a>另請參閱
- [ATP 調整大小工具](http://aka.ms/aatpsizingtool)
- [ATP 架構](atp-architecture.md)
- [安裝 Azure ATP](install-atp-step1.md)
- [查看 Azure ATP 論壇！](https://aka.ms/azureatpcommunity)

