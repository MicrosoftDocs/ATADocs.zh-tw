---
title: Azure 進階威脅防護多重樹系支援 | Microsoft Docs
description: 如何在 Azure ATP 中設定多個 Active Directory 樹系的支援。
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 8/20/2018
ms.topic: get-started-article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: effca0f2-fcae-4fca-92c1-c37306decf84
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 2a3460c39d6428831cc34231321fff745dbe0701
ms.sourcegitcommit: 121c49d559e71741136db1626455b065e8624ff9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/20/2018
ms.locfileid: "41734521"
---
適用於：Azure 進階威脅防護

# <a name="install-azure-atp---step-9"></a>安裝 Azure ATP - 步驟 9

>[!div class="step-by-step"]
[« 步驟 8](install-atp-step8-samr.md)

## <a name="step-9--set-up-azure-advanced-threat-protection-multi-forest-support"></a>步驟 9：  設定 Azure 進階威脅防護多重樹系支援

Azure ATP 可支援擁有多個樹系的組織，讓您能輕鬆地從單一管理點跨樹系監視活動和分析使用者。 

企業組織通常有數個 Active Directory 樹系，通常用於不同用途，包括來自公司合併和收購、地理分佈和安全性界限的舊版基礎結構 (紅色樹系)。 您可以使用 Azure ATP 保護多個樹系，以便可以透過單一管理點來進行監視和調查。

支援多個 Active Directory 樹系的功能可提供以下功能：
-   透過單一管理點來檢視和調查多個樹系中使用者執行的活動。 
-   提供了進階 Active Directory 整合和帳戶解析，以改進偵測及減少誤判。 
-   更好的控制和更簡單的部署方式。 當您的網域控制站全都是從單一 Azure ATP 主控台來監視時，可獲得跨組織涵蓋範圍的改良監視警示與回報功能。


## <a name="how-azure-atp-detects-activities-across-multiple-forests"></a>Azure ATP 如何跨多個樹系偵測活動 

為了偵測跨樹系活動，Azure ATP 感應器會查詢遠端樹系中的網域控制站，以建立所有相關實體的設定檔，包括來自遠端樹系的使用者和電腦。 

> [!NOTE]
> - Azure ATP 感應器可以安裝在所有樹系上 (如果存在最小的單向信任)。
> - 您在 Azure ATP 主控台中的 [目錄服務] 下設定的使用者，必須在所有其他樹系中都受到信任。


如果您有未安裝 Azure ATP 感應器的樹系，Azure ATP 仍然可以檢視和監視源自於這些樹系的活動。 安裝的 ATP 感應器可以查詢所有已連線的遠端樹系網域控制站，以解析使用者和電腦，並分別為其建立設定檔。 

## <a name="installation-requirements"></a>安裝需求 

-   如果 Azure ATP 獨立感應器是安裝在獨立電腦上，而不是直接安裝在網域控制站上，請確認已允許電腦使用 LDAP 與所有遠端樹系網域控制站通訊。 
- 您在 Azure ATP 主控台中的 [目錄服務] 下設定的使用者，必須受所有其他樹系信任，且必須至少有對網域控制站執行 LDAP 查詢的唯讀權限。

- 為了讓 Azure ATP 能夠與 ATP 感應器和 ATP 獨立感應器通訊，請在安裝 ATP 感應器的每部電腦上開啟以下連接埠：

 
  |通訊協定|傳輸|Port|去/從|方向|
  |----|----|----|----|----|
  |**內部連接埠**||||
  |SSL (*.atp.azure.com)|TCP|443|Azure ATP 雲端服務|輸出|
  |**內部連接埠**||||           
  |LDAP|TCP 和 UDP|389|網域控制站|輸出|
  |安全的 LDAP (LDAPS)|TCP|636|網域控制站|輸出|
  |LDAP 至通用類別|TCP|3268|網域控制站|輸出|
  |LDAPS 至通用類別|TCP|3269|網域控制站|輸出|


## <a name="multi-forest-support-network-traffic-impact"></a>多樹系支援的網路流量影響 

當 Azure ATP 對應您的樹系時，所使用的程序會有以下影響：

-   當 Azure ATP 感應器開始執行之後，會查詢遠端 Active Directory 樹系，並擷取使用者清單和電腦資料以建立設定檔。
-   每個 Azure ATP 感應器每隔 5 分鐘會查詢來自每個樹系中每個網域的其中一個網域控制站，以對應網路中的所有樹系。
-   每個 Azure ATP 感應器會藉由登入並檢查信任類型，使用 Active Directory 中的 "trustedDomain" 物件來對應樹系。
-   當 ATP 感應器偵測跨樹系活動時，您可能也會看到臨機操作流量。 當此情況發生時，ATP 感應器會傳送 LDAP 查詢到相關的網域控制站，以擷取實體資訊。 

## <a name="known-limitations"></a>已知限制
-   使用者在某樹系中為了存取其他樹系中的資源而執行的互動式登入，不會顯示在 Azure ATP 儀表板。


>[!div class="step-by-step"]
[« 步驟 8](install-atp-step8-samr.md)


## <a name="see-also"></a>另請參閱
- [ATP 調整大小工具](http://aka.ms/aatpsizingtool)
- [ATP 架構](atp-architecture.md)
- [安裝 ATP](install-atp-step1.md)
- [查看 ATP 論壇！](https://aka.ms/azureatpcommunity)\(英文\)

