---
title: Azure 進階威脅防護多重樹系支援 | Microsoft Docs
description: 對 Azure ATP 中多個 Active Directory 樹系的支援。
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 1/24/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: effca0f2-fcae-4fca-92c1-c37306decf84
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 00718998299590f658f8cdd6c7e2fc21c553210c
ms.sourcegitcommit: 6dd002b5a34f230aaada55a6f6178c2f9e1584d9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/05/2019
ms.locfileid: "65195574"
---
# <a name="azure-advanced-threat-protection-multi-forest-support"></a>Azure 進階威脅防護多重樹系支援


## <a name="multi-forest-support-set-up"></a>設定多重樹系支援 

Azure ATP 支援擁有多個樹系的組織，讓您可以輕鬆地監視活動和分析使用者。 

企業組織通常有數個 Active Directory 樹系，通常用於不同用途，包括來自公司合併和收購、地理分佈和安全性界限的舊版基礎結構 (紅色樹系)。 您可以使用 Azure ATP 保護多個樹系，以便可以透過單一管理點來進行整個網路的監視和調查。

支援多個 Active Directory 樹系的功能可提供以下功能：
-   透過單一管理點來檢視和調查多個樹系中使用者執行的活動。 
-   提供了進階 Active Directory 整合和帳戶解析，以改進偵測及減少誤判。 
-   更好的控制和更簡單的部署方式。 當您的網域控制站全都是從單一 Azure ATP 主控台來監視時，可獲得跨組織涵蓋範圍的改良監視警示與回報功能。


## <a name="azure-atp-detection-activity-across-multiple-forests"></a>跨多個樹系的 Azure ATP 偵測活動 

為了偵測跨樹系活動，Azure ATP 感應器會查詢遠端樹系中的網域控制站，以建立所有相關實體的設定檔 (包括來自遠端樹系的使用者和電腦)。 

- Azure ATP 感應器可以安裝在所有樹系上，即使樹系沒有信任也是如此。
- 在目錄服務頁面上為您環境中的所有樹系新增認證。 
    - 每個使用雙向信任的樹系都需要一個認證。 
    - 每個具有非 Kerberos 信任或不具信任的樹系，都需要其他認證。 
    - 每個 Azure ATP 執行個體都有 10 個樹系的限制。 若您的組織的樹系數目超過 10 個，請連絡客戶支援。 

![Azure ATP 歡迎使用階段 1](media/directory-services-add-no-trust-forests.png)

### <a name="requirements"></a>需求 

- 您在 Azure ATP 主控台中的 [目錄服務]  下設定的使用者，必須受所有其他樹系信任，且必須至少有對網域控制站執行 LDAP 查詢的唯讀權限。
- 如果 Azure ATP 獨立感應器是安裝在獨立電腦上，而不是直接安裝在網域控制站上，請確認已允許電腦使用 LDAP 與所有遠端樹系網域控制站通訊。 

- 為了讓 Azure ATP 能夠與 Azure ATP 感應器和 Azure ATP 獨立感應器通訊，請在安裝 Azure ATP 感應器的每部電腦上開啟以下連接埠：
 
  |通訊協定|傳輸|Port|去/從|方向|
  |----|----|----|----|----|
  |**內部連接埠**||||
  |SSL (*.atp.azure.com)|TCP|443|Azure ATP 雲端服務|輸出|
  |**內部連接埠**||||           
  |LDAP|TCP 和 UDP|389|網域控制站|輸出|
  |安全的 LDAP (LDAPS)|TCP|636|網域控制站|輸出|
  |LDAP 至通用類別|TCP|3268|網域控制站|輸出|
  |LDAPS 至通用類別|TCP|3269|網域控制站|輸出|


## <a name="multi-forest-support-network-traffic-impact"></a>多重樹系支援的網路流量影響 

當 Azure ATP 對應您的樹系時，所使用的程序會有以下影響：

-   當 Azure ATP 感應器開始執行之後，會查詢遠端 Active Directory 樹系，並擷取使用者清單和電腦資料以建立設定檔。
-   每個 Azure ATP 感應器每隔 5 分鐘會查詢來自每個樹系中每個網域的其中一個網域控制站，以對應網路中的所有樹系。
-   每個 Azure ATP 感應器會藉由登入並檢查信任類型，使用 Active Directory 中的 "trustedDomain" 物件來對應樹系。
-   當 Azure ATP 感應器偵測到跨樹系活動時，您可能也會看到臨機操作流量。 當此情況發生時，Azure ATP 感應器會傳送 LDAP 查詢到相關的網域控制站，以擷取實體資訊。 

## <a name="known-limitations"></a>已知限制
-   使用者在某樹系中為了存取其他樹系中的資源而執行的互動式登入，不會顯示在 Azure ATP 儀表板。



## <a name="see-also"></a>另請參閱
- [Azure ATP 調整大小工具](http://aka.ms/aatpsizingtool) \(英文\)
- [Azure ATP 架構](atp-architecture.md)
- [安裝 Azure ATP](install-atp-step1.md)
- [查看 Azure ATP 論壇！](https://aka.ms/azureatpcommunity)

