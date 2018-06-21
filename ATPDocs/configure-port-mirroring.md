---
title: 於部署 Azure 進階威脅防護時設定連接埠鏡像 | Microsoft Docs
description: 描述連接埠鏡像選項以及如何針對 Azure ATP 設定它們
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 5/22/2018
ms.topic: get-started-article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 9ec7eb4c-3cad-4543-bbf0-b951d8fc8ffe
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 1f59f02f73507fe29b41fd13c96a359dee2e88fc
ms.sourcegitcommit: 324dc941282f2948366afa5a919bda0b029bd59d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/22/2018
ms.locfileid: "34444583"
---
適用於：Azure 進階威脅防護



# <a name="configure-port-mirroring"></a>設定連接埠鏡像
> [!NOTE] 
> 本文僅適用於您部署 Azure ATP 獨立感應器 (而非 Azure ATP 感應器) 的情況。 若要判斷是否需要使用 Azure ATP 獨立感應器閘道，請參閱[為您的部署選擇正確感應器](atp-capacity-planning.md#choosing-the-right-sensor-type-for-your-deployment)。
 
Azure ATP 所使用的主要資料來源，是針對您網域控制站之雙向網路流量的深度封包檢查。 為了讓 Azure ATP 看到網路流量，您必須設定連接埠鏡像或使用網路 TAP。

若是連接埠鏡像，請為每個要監視的網域控制站設定**連接埠鏡像**，做為網路流量的**來源**。 一般而言，設定通訊埠鏡像必須與網路或虛擬化團隊合作。
如需詳細資訊，請參閱廠商的文件。

您的網域控制站和 Azure ATP 獨立感應器可以是實體或虛擬的。 以下是連接埠鏡像的常用方法和一些考量。 如需詳細資訊，請參閱交換器或虛擬伺服器的產品文件。 您的交換器製造商有可能使用不同的術語。

**交換器連接埠分析器 (SPAN)** – 會將一或多個交換器連接埠的網路流量複製到相同交換器上的另一個交換器連接埠。 Azure ATP 獨立感應器和網域控制站皆必須連接到相同的實體交換器。

**遠端交換器連接埠分析器 (RSPAN)**  – 可讓您監視分佈在多部實體交換器連接埠上的來源連接埠的網路流量。 RSPAN 會將來源流量複製到特殊的 RSPAN 設定 VLAN。 此 VLAN 需要是其他相關交換器的主幹。 RSPAN 是在第 2 層運作。

**封裝遠端交換器連接埠分析器 (ERSPAN)** – 是 Cisco 的專利技術，在第 3 層運作。 ERSPAN 可讓您監視多部交換器的流量，而不需要 VLAN 主幹。 ERSPAN 使用一般路由封裝 (GRE) 複製受監視的網路流量。 目前 Azure ATP 無法直接接收 ERSPAN 流量。 若要讓 Azure ATP 能搭配 ERSPAN 流量使用，必須將可解除流量封裝的交換器或路由器設定為 ERSPAN 的目的地，使流量可以在該位置解除封裝。 然後設定交換器或路由器，使它們能透過 SPAN 或 RSPAN 將已解除封裝的流量轉送至 Azure ATP 獨立感應器。

> [!NOTE]
> 如果被連接埠鏡像的網域控制站是透過 WAN 連結進行連線，請確定 WAN 連結可以處理 ERSPAN 流量的額外負載。
> Azure ATP 只在流量以相同方式抵達 NIC 及網域控制站時，才會支援流量監視。 當流量分散到不同的連接埠時，Azure ATP 便不會支援流量監視。

## <a name="supported-port-mirroring-options"></a>支援的連接埠鏡像選項

|Azure ATP 獨立感應器|網域控制站|考量|
|---------------|---------------------|------------------|
|網路|相同主機上的虛擬|虛擬交換器需要支援連接埠鏡像。<br /><br />將其中一部虛擬機器本身單獨移至另一個主機，可能會中斷連接埠鏡像。|
|網路|不同主機上的虛擬|請確定您的虛擬交換器支援這種案例。|
|網路|實體|需要專用的網路介面卡，否則 Azure ATP 會看到所有進出主機的流量，甚至是由它傳送至 Azure ATP 雲端服務的流量。|
|實體|網路|請確定您的虛擬交換器支援這種案例 - 且實體交換器上的連接埠鏡像設定是根據此案例︰<br /><br />如果虛擬主機位於相同的實體交換器上，您必須設定交換器層級的 SPAN。<br /><br />如果虛擬主機位於不同的交換器上，您必須設定 RSPAN 或 ERSPAN&#42;。|
|實體|相同交換器上的實體|實體交換器必須支援 SPAN/連接埠鏡像。|
|實體|不同交換器上的實體|實體交換器需要支援 RSPAN 或 ERSPAN &#42;。|
&#42; 只有在 ATP 分析流量之前先解除除封裝的前提下，才支援 ERSPAN。

> [!NOTE]
> 請確定它們連線的網域控制站和 Azure ATP 獨立感應器彼此的時間已同步至相差不到五分鐘的間隔。

**如果您正在使用虛擬化叢集︰**

-   針對在具有 Azure ATP 獨立感應器之虛擬機器中的虛擬化叢集上執行的每個網域控制站，設定網域控制站與 Azure ATP 獨立感應器之間的親和性。 如此一來，當網域控制站移至叢集中的另一部主機時，Azure ATP 獨立感應器便會跟隨它。 只有幾個網域控制站時，這可以運作的很好。

 > [!NOTE]
 > 如果您的環境支援在不同主機上進行虛擬對虛擬 (RSPAN)，就不需要擔心親和性。
 
-   為了確保 Azure ATP 獨立感應器具有適當大小可以自己處理所有 DC 的監視，請嘗試此選項︰在每個虛擬化主機上安裝虛擬機器，並在每個主機上安裝 Azure ATP 獨立感應器。 將每個 Azure ATP 獨立感應器設定為監視叢集上執行的所有網域控制站。 如此一來，執行網域控制站的任何主機都會被監視。

設定連接埠鏡像之後，請先驗證連接埠鏡像運作正常，再安裝 Azure ATP 獨立感應器。

## <a name="see-also"></a>另請參閱
- [設定事件轉寄](configure-event-forwarding.md)
- [查看 ATP 論壇！](https://aka.ms/azureatpcommunity)\(英文\)