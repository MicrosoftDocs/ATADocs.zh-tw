---
title: Azure 進階威脅防護不受限制的 Kerberos 身分識別安全性狀態評量
description: 本文提供 Azure ATP 不受限制的 Kerberos 身分識別安全性狀態評估報告總覽。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 08/25/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 7eea354b-7a50-40d9-bfa7-dcccaef23179
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: a4676837537869f6984ffe27f20b5cbeae971bde
ms.sourcegitcommit: c7c0a4c9f7507f3e8e0f219798ed7d347c03e792
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/22/2020
ms.locfileid: "90912791"
---
# <a name="security-assessment-unsecure-kerberos-delegation"></a>安全性評估：不安全的 Kerberos 委派

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

## <a name="what-is-kerberos-delegation"></a>什麼是 Kerberos 委派？

Kerberos 委派是一種委派設定，可讓應用程式要求使用者存取認證，以代表原始使用者存取資源。

## <a name="what-risk-does-unsecure-kerberos-delegation-pose-to-an-organization"></a>不安全的 Kerberos 委派會對組織造成什麼風險？

不安全的 Kerberos 委派能讓實體向任何其他所選服務模擬您。 假設您有一個 IIS 網站，而應用程式集區帳戶是以不受限制的委派來設定。 IIS 網站網站也已啟用 Windows 驗證，允許原生 Kerberos 驗證，而且該網站使用後端 SQL Server 來取得商務資料。 使用您的網域系統管理員帳戶劉覽至 IIS 網站並對其進行驗證。 使用不受限制委派的網站可以代您從網域控制站取得交給 SQL 服務的服務票證。

Kerberos 委派的主要問題在於，您必須信任應用程式永遠會執行正確的動作。 惡意執行者可以改為強制應用程式執行錯誤的動作。 如果您是以**網域系統管理員**的身分登入，則網站可以建立任何其他服務的票證，如同您的**網域系統管理員**。例如，網站可以選擇網域控制站，並對**企業系統管理員**群組進行變更。 同樣地，網站可以取得 KRBTGT 帳戶的雜湊，或從人力資源部門下載有趣的檔案。 這項風險很明確，但不安全的委派卻幾乎有無限多種可能的風險。

以下是對不同委派類型所造成風險的描述：

- **無限制委派**：如果其中一個委派項目是敏感性項目，則任何服務都可能遭到濫用。
- **限制委派**：如果其中一個委派項目是敏感性項目，則限制實體可能遭到濫用。
- **按資源限制委派 (RBCD)** ：如果實體本身是敏感性項目，則按資源限制實體可能遭到濫用。

## <a name="how-do-i-use-this-security-assessment"></a>我該如何使用這項安全性評估？

1. 使用報表資料表來探索哪些非網域控制站實體已設定為**不安全的 Kerberos 委派**。

    ![不安全的 Kerberos 委派安全性評定](media/atp-cas-isp-kerberos-delegation-2.png)
1. 對那些具有風險的使用者採取適當的行動，例如移除其不受限制的屬性，或將其變更為更安全的限制委派。

> [!NOTE]
> 此評定會每隔 24 小時更新一次。

## <a name="remediation"></a>修復

使用適用於委派類型的補救。

### <a name="unconstrained-delegation"></a>無限制委派

停用委派，或使用下列其中一個 Kerberos 限制委派 (KCD) 類型：

- **限制委派：** 限制此帳戶可以模擬的服務。

    1. 選取 [信任這台電腦，但只委派指定的服務]。

        ![不受限制的 Kerberos 委派補救](media/atp-cas-isp-unconstrained-kerberos-1.png)

    2. 指定 [這個帳戶可以呈送委派認證的服務]。

- **按資源限制委派：** 限制可以模擬此帳戶的實體。  
按資源 KCD 使用 PowerShell 來設定。 視模擬帳戶是電腦帳戶或使用者帳戶/服務帳戶而定，您可以使用 [Set-ADComputer](/powershell/module/addsadministration/set-adcomputer?view=win10-ps&preserve-view=true) 或 [Set-ADUser](/powershell/module/addsadministration/set-aduser?view=win10-ps&preserve-view=true) Cmdlet。

### <a name="constrained-delegation"></a>限制委派

檢查建議中列出的敏感性使用者，並將其從受影響帳戶可以呈送委派認證的服務中移除。

![受限制的 Kerberos 委派補救](media/atp-cas-isp-unconstrained-kerberos-2.png)

### <a name="resource-based-constrained-delegation-rbcd"></a>按資源限制委派 (RBCD)

檢查建議中列出的敏感性使用者，並將其從資源中移除。 如需設定 RBCD 的詳細資訊，請參閱[在 Azure Active Directory Domain Services 中設定 Kerberos 限制委派 (KCD)](/azure/active-directory-domain-services/deploy-kcd)。

## <a name="next-steps"></a>後續步驟

- [Cloud App Security 中的 Azure ATP 活動篩選](activities-filtering-mcas.md)
- [查看 Azure ATP 論壇！](https://aka.ms/azureatpcommunity)
