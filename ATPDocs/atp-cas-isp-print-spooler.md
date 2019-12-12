---
title: Azure 進階威脅防護列印多工緩衝處理器身分識別安全性狀態評估 | Microsoft Docs
description: 本文提供 Azure ATP 列印多工緩衝處理器身分識別安全性狀態評估報告的總覽。
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 07/08/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 1a7d9525-8923-4dae-af51-02a68aa61644
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 73f876a047ed48526e26cd9b3758077331dca05d
ms.sourcegitcommit: 6dd002b5a34f230aaada55a6f6178c2f9e1584d9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2019
ms.locfileid: "74206251"
---
# <a name="security-assessment-domain-controllers-with-print-spooler-service-available"></a>安全性評估：有可用列印多工緩衝處理器服務的網域控制站 

![停用列印多工緩衝處理器服務](media/atp-cas-isp-print-spooler-1.png)
 
## <a name="what-is-the-print-spooler-service"></a>什麼是**列印多工緩衝處理器**服務？ 

列印多工緩衝處理器是管理列印程序的軟體服務。 多工緩衝處理器會接受電腦的列印工作，並確定印表機資源可供使用。 多工緩衝處理器也會排定列印工作傳送到列印佇列以進行列印的順序。 在個人電腦的早期，使用者必須等到檔案列印完成，才能執行其他動作。 多虧出現了新式的列印多工緩衝處理器，列印現在不會再對使用者的整體生產力造成太大影響。

## <a name="what-risks-does-the-print-spooler-service-on-domain-controllers-introduce"></a>網域控制站上的**列印多工緩衝處理器**服務會帶來哪些風險？ 

所有已驗證的使用者都可以從遠端連線到網域控制站列印多工緩衝處理器服務，並要求更新新的列印工作，這乍看之下似乎沒有任何風險。 此外，使用者還能要求網域控制站對系統傳送具有[不受限制委派](atp-cas-isp-unconstrained-kerberos.md)的通知。 這些動作會測試連線並公開網域控制站電腦帳戶認證 (**列印多工緩衝處理器**由 SYSTEM 擁有)。 

因為有暴露的風險，所以網域控制站和 Active Directory 系統管理系統必須停用**列印多工緩衝處理器**服務。 建議的做法為使用群組原則物件 (GPO)。 

雖然此安全性評估著重於網域控制站，但任何伺服器都可能有這類攻擊的風險。

   > [!NOTE]
   > 停用此服務並防止主動列印工作流程之前，請務必先調查您的**列印多工緩衝處理器**設定、組態與相依性。

## <a name="how-do-i-use-this-security-assessment"></a>我該如何使用這項安全性評估？ 
1. 使用報告資料表來探索有哪些網域控制站已啟用**列印多工緩衝處理器**服務。   
    <br>![停用列印多工緩衝處理器服務安全性評估](media/atp-cas-isp-print-spooler-2.png)
1. 對具有風險的網域控制站採取適當的動作，並以手動方式、透過 GPO 或其他類型的遠端命令主動移除列印多工緩衝處理器服務。

## <a name="remediation"></a>修復

透過在不需要「列印多工緩衝處理器」的所有伺服器上將它停用以修正此特定問題。
  

## <a name="next-steps"></a>後續步驟
- [Cloud App Security 中的 Azure ATP 活動篩選](atp-activities-filtering-mcas.md)
- [查看 Azure ATP 論壇！](https://aka.ms/azureatpcommunity)