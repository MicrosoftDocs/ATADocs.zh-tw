---
title: Microsoft Defender 身分識別的身分識別安全性狀態評估
description: 本文概述 Microsoft Defender 身分識別的身分識別安全性狀態評量報告。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 10/26/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 58e079764c2e59623b94b78f29f0ad00d6219dcc
ms.sourcegitcommit: e2227c0b0e5aaa5163dc56d4131ca82f8dca8fb0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2020
ms.locfileid: "94847423"
---
# <a name="product-longs-identity-security-posture-assessments"></a>[!INCLUDE [Product long](includes/product-long.md)]的身分識別安全性狀態評估

一般來說，各種大小的組織對於其內部部署應用程式和服務是否會對其組織造成安全性弱點的瞭解有限。 只有在使用不支援或過期的元件時，才會發生有限可見度的問題。

雖然您的公司可能會投入大量時間和努力來強化身分識別和身分識別基礎結構 (例如 Active Directory、Active Directory Connect) 作為持續進行的專案，但很容易沒注意到常見的錯誤配置和使用舊版代表貴組織最大威脅風險之一的元件。 根據 Microsoft 安全性研究，大部分的身分識別攻擊都會利用 Active Directory 的常見錯誤，和舊版元件 (例如 NTLMv1 通訊協定) 的繼續使用來危害身分識別並成功入侵您的組織。 為了有效對抗這一點， [!INCLUDE [Product long](includes/product-long.md)] 現在提供主動式身分識別安全性狀態評估，以偵測並建議您內部部署 Active Directory 設定之間的改進動作。

## <a name="what-do-product-short-identity-security-posture-assessments-provide"></a>身分 [!INCLUDE [Product short](includes/product-short.md)] 識別安全性狀態評量提供哪些功能？

- 已知可攻擊元件和錯誤錯誤的偵測和內容資料，以及補救的相關路徑。
- [!INCLUDE [Product short](includes/product-short.md)] 不僅偵測到可疑的活動，還會主動監視您的內部部署身分識別，以及使用現有感應器的安全點身分識別基礎結構 [!INCLUDE [Product short](includes/product-short.md)] 。
- 精確地評估您目前組織安全性狀態的報告，在連續迴圈中啟用快速回應和效果監視。

## <a name="how-do-i-get-started"></a>如何開始？

### <a name="access"></a>存取

[!INCLUDE [Product short](includes/product-short.md)] 開啟整合之後，可以使用 Microsoft Cloud App Security 入口網站取得安全性評定 [!INCLUDE [Product short](includes/product-short.md)] 。 若要瞭解如何整合 [!INCLUDE [Product short](includes/product-short.md)] 至 Cloud App Security，請參閱[ [!INCLUDE [Product short](includes/product-short.md)] 整合](/cloud-app-security/aatp-integration)。

### <a name="licensing"></a>授權

存取 [!INCLUDE [Product short](includes/product-short.md)] Cloud App Security 中的安全性評定報告不需要 Cloud App Security 授權，僅 [!INCLUDE [Product short](includes/product-short.md)] 需要授權。

## <a name="access-product-short-using-cloud-app-security"></a>[!INCLUDE [Product short](includes/product-short.md)]使用 Cloud App Security 存取

請參閱 [Cloud App Security 快速入門](/cloud-app-security/getting-started-with-cloud-app-security)以熟悉使用 Cloud App Security 入口網站的基本概念。

**身分識別安全性狀態評估**

[!INCLUDE [Product short](includes/product-short.md)] 提供下列身分識別安全性狀態評估。 每個評估都是可下載的報告，其中包含用來建立要補救或解決之動作計劃的指示和工具。

**評估報告**

- [有可用列印多工緩衝處理器服務的網域控制站](cas-isp-print-spooler.md)
- [從敏感性群組中移除休眠實體](cas-isp-dormant-entities.md)
- [實體以純文字公開認證](cas-isp-clear-text.md)
- [Microsoft LAPS 使用情況](cas-isp-laps.md)
- [使用舊版通訊協定](cas-isp-legacy-protocols.md)
- [風險最高的橫向移動路徑 (LMP)](cas-isp-riskiest-lmp.md)
- [未受監視的網域控制站](cas-isp-unmonitored-domain-controller.md)
- [不安全的帳戶屬性](cas-isp-unsecure-account-attributes.md)
- [不安全的 Kerberos 委派](cas-isp-unconstrained-kerberos.md)
- [不安全的 SID History 屬性](cas-isp-unsecure-sid-history-attribute.md)
- [弱式加密使用方式](cas-isp-weak-cipher.md)

若要存取身分識別安全性狀態評估：

1. **開啟 Microsoft Cloud App Security** 入口網站。
    ![存取 [！包含 [產品簡短] (包含/產品簡短的 md) ] Cloud App Security 中的身分識別安全性狀態報表](media/cas-isp-report-1.png)
1. 從左側功能表中選取 [調查]，然後從下拉式功能表中按一下 [身分識別安全性狀態]。
1. 從開啟的 **安全性評估報告** 清單中，按一下您想要檢查的身分識別安全性狀態評估。

## <a name="next-steps"></a>後續步驟

- [深入瞭解如何搭配使用 Cloud App Security [!INCLUDE [Product short](includes/product-short.md)]](activities-filtering-mcas.md)
- [查看[!INCLUDE [Product short](includes/product-short.md)] 論壇！](https://aka.ms/MDIcommunity)\(英文\)
