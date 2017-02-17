---
title: "於部署 Advanced Threat Analytics 時設定連接埠鏡像 | Microsoft Docs"
description: "描述連接埠鏡像選項以及如何設定它們以進行 ATA"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 1/23/2017
ms.topic: get-started-article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: cdaddca3-e26e-4137-b553-8ed3f389c460
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: b28cb3a0da844b7c460c03726222bc775a9e47da
ms.openlocfilehash: 8e18bcefc023f1c37b2255000c244bc54bca4fe7


---

適用於︰Advanced Threat Analytics 1.7 版



# <a name="configure-port-mirroring"></a>設定連接埠鏡像
> [!NOTE] 
> 本文只有在部署 ATA 閘道 (而非 ATA 輕量型閘道) 時才適用。 若要判斷是否需要使用 ATA 閘道，請參閱[為您的部署選擇正確閘道](/advanced-threat-analytics/plan-design/ata-capacity-planning#choosing-the-right-gateway-type-for-your-deployment)。
 
ATA 使用的主要資料來源是對進出網域控制站的網路流量的深度封包檢查。 為了讓 ATA 看到網路流量，您必須設定連接埠鏡像或使用網路 TAP。

若是連接埠鏡像，請為每個要監視的網域控制站設定**連接埠鏡像**，做為網路流量的**來源**。 一般而言，設定連接埠鏡像必須與網路或虛擬化團隊合作。
如需詳細資訊，請參閱廠商的文件。

您的網域控制站和 ATA 閘道可以是實體或虛擬。 以下是連接埠鏡像的常用方法和一些考量。 如需詳細資訊，請檢閱交換器或虛擬伺服器的產品文件。 您的交換器製造商有可能使用不同的術語。

**交換器連接埠分析器 (SPAN)** – 會將一或多個交換器連接埠的網路流量複製到相同交換器上的另一個交換器連接埠。 ATA 閘道和網域控制站皆必須連接到相同的實體交換器。

**遠端交換器連接埠分析器 (RSPAN)**  – 可讓您監視分佈在多部實體交換器連接埠上的來源連接埠的網路流量。 RSPAN 會將來源流量複製到特殊的 RSPAN 設定 VLAN。 此 VLAN 需要是其他相關交換器的主幹。 RSPAN 是在第 2 層運作。

**封裝遠端交換器連接埠分析器 (ERSPAN)** – 是 Cisco 的專利技術，在第 3 層運作。 ERSPAN 可讓您監視多部交換器的流量，而不需要 VLAN 主幹。 ERSPAN 使用一般路由封裝 (GRE) 複製受監視的網路流量。 目前 ATA 無法直接接收 ERSPAN 流量。 若要讓 ATA 使用 ERSPAN 流量，必須將可解除封裝的交換器或路由器設定為 ERSPAN 的目的地，它可以將流量解除封裝。 然後必須將交換器或路由器設定為使用 SPAN 或 RSPAN 轉送流量寄至 ATA 閘道。

> [!NOTE]
> 如果被連接埠鏡像的網域控制站是透過 WAN 連結進行連線，請確定 WAN 連結可以處理 ERSPAN 流量的額外負載。

## <a name="supported-port-mirroring-options"></a>支援的連接埠鏡像選項

|ATA 閘道|網域控制站|考量|
|---------------|---------------------|------------------|
|網路|相同主機上的虛擬|虛擬交換器需要支援連接埠鏡像。<br /><br />將其中一部虛擬機器本身單獨移至另一個主機，可能會中斷連接埠鏡像。|
|網路|不同主機上的虛擬|請確定您的虛擬交換器支援這種案例。|
|網路|實體|需要專用的網路介面卡，否則 ATA 會看到所有進出主機的流量，甚至是它傳送至 ATA 中心的流量。|
|實體|網路|請確定您的虛擬交換器支援這種案例 - 且實體交換器上的連接埠鏡像設定是根據此案例︰<br /><br />如果虛擬主機位於相同實體交換器上，您必須設定交換器層級的 SPAN。<br /><br />如果虛擬主機位於不同交換器上，您必須設定 RSPAN 或 ERSPAN&#42;。|
|實體|相同交換器上的實體|實體交換器必須支援 SPAN/連接埠鏡像。|
|實體|不同交換器上的實體|實體交換器需要支援 RSPAN 或 ERSPAN &#42;。|
&#42; 在 ATA 流量分析之前先解除除封裝的前提下，才支援 ERSPAN。

> [!NOTE]
> 請確定它們連線的網域控制站和 ATA 閘道彼此的時間同步相差不到 5 分鐘。

**如果您正在使用虛擬化叢集︰**

-   在具有 ATA 閘道之虛擬機器中的虛擬化叢集上執行的每個網域控制站，設定網域控制站與 ATA 閘道之間的親和性。 如此一來，當網域控制站移至集中的另一部主機，ATA 閘道叢將會跟隨它。 只有幾個網域控制站時，這可以運作的很好。
> [!NOTE]
> 如果您的環境支援在不同主機上進行虛擬對虛擬 (RSPAN)，就不需要擔心親和性。
> 
-   為了確保 ATA 閘道具有適當大小可以自己處理所有 DC 的監視，請嘗試此選項︰在每個虛擬化主機上安裝虛擬機器，並在每個主機上安裝 ATA 閘道。 將每個 ATA 閘道設定為監視叢集上執行的所有網域控制站。 如此一來，網域控制站執行的任何主機都會被監視。

設定連接埠鏡像之後，先驗證連接埠鏡像運作正常，再安裝 ATA 閘道。

## <a name="see-also"></a>另請參閱
- [驗證連接埠鏡像](validate-port-mirroring.md)
- [查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Feb17_HO1-->


