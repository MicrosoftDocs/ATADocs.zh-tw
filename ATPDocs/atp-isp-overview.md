---
title: Azure 進階威脅防護身分識別安全性狀態評估 | Microsoft Docs
description: 本文提供 Azure ATP 的身分識別安全性狀態評估報告的總覽。
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 09/16/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 71b15bd9-3183-4e24-b18a-705023ccc313
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: cb562e8d9dc21d8fa5fcce70ea2020be22796621
ms.sourcegitcommit: 475df3e87d8476ff13e48ebc7a722f46f29dab70
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/16/2019
ms.locfileid: "71007524"
---
# <a name="azure-atps-identity-security-posture-assessments"></a>Azure ATP 身分識別安全性狀態評估
 
一般來說，各種大小的組織對於其內部部署應用程式和服務是否會對其組織造成安全性弱點的瞭解有限。 只有在使用不支援或過期的元件時，才會發生有限可見度的問題。 

雖然您的公司可能會投入大量時間和努力來強化身分識別和身分識別基礎結構 (例如 Active Directory、Active Directory Connect) 作為持續進行的專案，但很容易沒注意到常見的錯誤配置和使用舊版代表貴組織最大威脅風險之一的元件。 根據 Microsoft 安全性研究，大部分的身分識別攻擊都會利用 Active Directory 的常見錯誤，和舊版元件 (例如 NTLMv1 通訊協定) 的繼續使用來危害身分識別並成功入侵您的組織。 為了有效對抗這一點, Azure ATP 現在提供主動式身分識別安全性狀態評估，以偵測並建議內部部署 Active Directory 設定的改進動作。 

## <a name="what-do-azure-atp-identity-security-posture-assessments-provide"></a>Azure ATP 身分識別安全性狀態評估提供什麼？  
- 已知可攻擊元件和錯誤錯誤的偵測和內容資料，以及補救的相關路徑。
- Azure ATP 不只會偵測到可疑的活動, 也會主動監視您的內部部署身分識別，以及使用現有 Azure ATP 感應器的安全點身分識別基礎結構。 
- 精確地評估您目前組織安全性狀態的報告，在連續迴圈中啟用快速回應和效果監視。 

## <a name="how-do-i-get-started"></a>如何開始？ 

### <a name="access"></a>存取

開啟 Azure ATP 整合之後，可以使用 Microsoft Cloud App Security 入口網站來利用 Azure ATP 安全性評估。 若要了解如何將 Azure ATP 整合至 Cloud App Security，請參閱 [Azure ATP 整合](https://docs.microsoft.com/cloud-app-security/aatp-integration)。 

### <a name="licensing"></a>授權

存取 Cloud App Security 中的 Azure ATP 安全性評估報告不需要 Cloud App Security 授權，只需要 Azure ATP 授權。 

## <a name="access-azure-atp-using-cloud-app-security"></a>使用 Cloud App Security 存取 Azure ATP 

請參閱 [Cloud App Security 快速入門](https://docs.microsoft.com/cloud-app-security/getting-started-with-cloud-app-security)以熟悉使用 Cloud App Security 入口網站的基本概念。 

**身分識別安全性狀態評估**

Azure ATP 提供下列身分識別安全性狀態評估。 每個評估都是可下載的報告，其中包含用來建立要補救或解決之動作計劃的指示和工具。 

**評估報告**
- 防止[實體以純文字公開認證](atp-cas-isp-clear-text.md)
- 防止[使用舊版通訊協定](atp-cas-isp-legacy-protocols.md)
- 防止[弱式加密使用](atp-cas-isp-weak-cipher.md)
- 防止[不安全的 Kerberos 委派](atp-cas-isp-unconstrained-kerberos.md)
- 停用網域控制站上的[列印多工緩衝處理器服務](atp-cas-isp-print-spooler.md)
- [從敏感性群組中移除休眠實體](atp-cas-isp-dormant-entities.md)

若要存取身分識別安全性狀態評估：
1. **開啟 Microsoft Cloud App Security** 入口網站。 
    ![存取 Cloud App Security 中的 Azure ATP 身分識別安全性狀態報告](media/atp-cas-isp-report-1.png)
1. 從左側功能表中選取 [調查]  ，然後從下拉式功能表中按一下 [身分識別安全性狀態]  。 
1. 從開啟的**安全性評估報告**清單中，按一下您想要檢查的身分識別安全性狀態評估。  


## <a name="next-steps"></a>後續步驟
- [深入了解如何搭配使用 Cloud App Security 與 Azure ATP](atp-activities-filtering-mcas.md)
- [查看 Azure ATP 論壇！](https://aka.ms/azureatpcommunity)

