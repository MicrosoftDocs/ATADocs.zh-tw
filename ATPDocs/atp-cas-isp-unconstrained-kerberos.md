---
title: Azure 進階威脅防護不受限制的 Kerberos 身分識別安全性狀態評估 | Microsoft Docs
description: 本文提供 Azure ATP 不受限制的 Kerberos 身分識別安全性狀態評估報告總覽。
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 09/15/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 7eea354b-7a50-40d9-bfa7-dcccaef23179
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 949f99c2ab19a5765a69c21121a274257c20efb6
ms.sourcegitcommit: be4525a93601d9356a4e487398262a2ffaf8c202
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2019
ms.locfileid: "74206322"
---
# <a name="security-assessment-unsecure-kerberos-delegation"></a>安全性評估：不安全的 Kerberos 委派


## <a name="what-is-kerberos-delegation"></a>什麼是 Kerberos 委派？ 

Kerberos 委派是一種委派設定，可讓應用程式要求使用者存取認證，以代表原始使用者存取資源。  

## <a name="what-risk-does-unsecure-kerberos-delegation-pose-to-an-organization"></a>不安全的 Kerberos 委派會對組織造成什麼風險？ 

不安全的 Kerberos 委派能讓實體向任何其他所選服務模擬您。 假設您有一個 IIS 網站，而應用程式集區帳戶是以不受限制的委派來設定。 IIS 網站網站也已啟用 Windows 驗證，允許原生 Kerberos 驗證，而且該網站使用後端 SQL Server 來取得商務資料。 使用您的網域系統管理員帳戶劉覽至 IIS 網站並對其進行驗證。 使用不受限制委派的網站可以代您從網域控制站取得交給 SQL 服務的服務票證。

Kerberos 委派的主要問題在於，您必須信任應用程式永遠會執行正確的動作。 惡意執行者可以改為強制應用程式執行錯誤的動作。 如果您是以**網域系統管理員**的身分登入，則網站可以建立任何其他服務的票證，如同您的**網域系統管理員**。例如，網站可以選擇網域控制站，並對**企業系統管理員**群組進行變更。 同樣地，網站可以取得 KRBTGT 帳戶的雜湊，或從人力資源部門下載有趣的檔案。 這項風險很明確，但不安全的委派卻幾乎有無限多種可能的風險。 

 
## <a name="how-do-i-use-this-security-assessment"></a>我該如何使用這項安全性評估？

1. 使用報表資料表來探索哪些非網域控制站實體已設定為**不安全的 Kerberos 委派**。    
    <br>![不安全的 Kerberos 委派安全性評定](media/atp-cas-isp-kerberos-delegation-2.png)
1. 對那些具有風險的使用者採取適當的行動，例如移除其不受限制的屬性，或將其變更為更安全的限制委派。

## <a name="remediation"></a>修復

若要深入了解如何補救這些帳戶類型，請參閱 [Removing accounts that use unconstrained Kerberos delegation (移除使用不受限制的 Kerberos 委派的帳戶)](https://blogs.technet.microsoft.com/389thoughts/2017/04/18/get-rid-of-accounts-that-use-kerberos-unconstrained-delegation/)。

## <a name="next-steps"></a>後續步驟
- [Cloud App Security 中的 Azure ATP 活動篩選](atp-activities-filtering-mcas.md)
- [查看 Azure ATP 論壇！](https://aka.ms/azureatpcommunity)
