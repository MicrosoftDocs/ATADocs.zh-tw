---
title: "Advanced Threat Analytics 架構 | Microsoft Docs"
description: "描述 Microsoft Advanced Threat Analytics 的架構 (ATA)"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 11/7/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 892b16d2-58a6-49f9-8693-1e5f69d8299c
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 66f5678285c203476aee3daafae22ac7b34d0ae2
ms.sourcegitcommit: 4d2ac5b02c682840703edb0661be09055d57d728
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/07/2017
---
*適用於︰Advanced Threat Analytics 1.8 版*




# <a name="ata-architecture"></a>ATA 架構
此圖表中詳細說明 Advanced Threat Analytics 架構︰

![ATA 架構拓撲圖表](media/ATA-architecture-topology.jpg)

ATA 會運用使用實體或虛擬交換器的 ATA 閘道連接埠鏡像，監視網域控制站的網路流量。 如果您直接在網域控制站上部署 ATA 輕量型閘道，它會移除連接埠鏡像的需求。 此外，ATA 可以運用 Windows 事件 (直接從網域控制站或 SIEM 伺服器轉寄)，分析用於攻擊和威脅的資料。
本節說明網路與事件擷取的流程，並深入描述 ATA 主要元件的功能︰ATA 閘道、ATA 輕量型閘道 (核心功能與 ATA 閘道相同) 和 ATA 中心。


![ATA 流量圖表](media/ATA-traffic-flow.jpg)

## <a name="ata-components"></a>ATA 元件
ATA 包含下列元件：

-   **ATA 中心** <br>
ATA 中心會接收您部署之所有 ATA 閘道和/或 ATA 輕量型閘道的資料。
-   **ATA 閘道**<br>
ATA 閘道安裝在監視網域控制站流量的專用伺服器上，這個控制站使用連接埠鏡像或網路 TAP。
-   **ATA 輕量型閘道**<br>
ATA 輕量型閘道直接安裝在網域控制站上，直接監視其流量，不需要專用伺服器或連接埠鏡像設定。 它可以替代 ATA 閘道。

ATA 部署的組成可以是連接至所有 ATA 閘道的單一 ATA 中心、所有 ATA 輕量型閘道，或 ATA 閘道和 ATA 輕量型閘道的組合。


## <a name="deployment-options"></a>部署選項
您可以使用下列閘道組合部署 ATA︰

-   **只使用 ATA 閘道** <br>
ATA 部署可以只包含 ATA 閘道，不含任何 ATA 輕量型閘道：所有網域控制站必須設定為啟用 ATA 閘道的連接埠鏡像，或者必須先準備好網路 TAP。
-   **只使用 ATA 輕量型閘道**<br>
ATA 部署可以只包含 ATA 輕量型閘道：ATA 輕量型閘道部署在每個網域控制站，不需要設定任何其他伺服器或連接埠鏡像。
-   **同時使用 ATA 閘道和 ATA 輕量型閘道**<br>
ATA 部署包括 ATA 閘道和 ATA 輕量型閘道。 ATA 輕量型閘道是安裝在一些網域控制站上 (例如，分支網站的所有網域控制站)。 同時，其他網域控制站是由 ATA 閘道監視 (例如，主要資料中心的較大網域控制站)。

在所有這些案例中，所有的閘道都會將資料傳送至 ATA 中心。




## <a name="ata-center"></a>ATA 中心
**ATA 中心**會執行下列功能：

-   管理 ATA 閘道和 ATA 輕量型閘道組態設定

-   接收來自 ATA 閘道和 ATA 輕量型閘道的資料 

-   偵測可疑活動

-   執行 ATA 行為機器學習演算法，以偵測異常行為。

-   執行各種具決定性的演算法，根據攻擊鏈偵測進階的攻擊。

-   執行 ATA 主控台。

-   選擇性︰ATA 中心可以設定為偵測到可疑活動時傳送電子郵件和事件。

ATA 中心會從 ATA 閘道和 ATA 輕量型閘道接收剖析過的流量。 然後執行分析、執行決定性偵測，並執行機器學習和行為演算法，以了解您的網路，啟用異常偵測並警告您可疑的活動。

|||
|-|-|
|實體接收者|從所有 ATA 閘道和 ATA 輕量型閘道接收實體批次。|
|網路活動處理器|處理每個批次中收到的所有網路活動。 例如，比對可能從不同電腦執行的各種 Kerberos 步驟|
|實體程分析工具|根據流量與事件設定所有唯一實體。 例如，ATA 會更新每個使用者設定檔之登入電腦清單的位置。|
|中心資料庫|管理網路活動和事件寫入資料庫的程序。 |
|資料庫|ATA 使用 MongoDB，其目的為在系統中儲存所有資料︰<br /><br />-   網路活動<br />-   事件活動<br />-   唯一實體<br />-   可疑活動<br />-   ATA 設定|
|偵測器|偵測器使用機器學習演算法和決定性規則，在您的網路中尋找可疑活動和異常使用者行為。|
|ATA 主控台|ATA 主控台可用來設定 ATA 及監視 ATA 在網路上偵測到的可疑活動。 ATA 主控台並未依存於 ATA 中心服務，即使在服務停止時，只要它可以和資料庫通訊，就會持續執行。|
決定要在網路上部署多少 ATA 中心時，請考慮下列準則︰

-   一個 ATA 中心可以監視單一 Active Directory 樹系。 如果您有多個 Active Directory 樹系，每個 Active Directory 樹系需要至少一個 ATA 中心。

-    在大型的 Active Directory 部署中，單一 ATA 中心可能無法處理所有網域控制站的所有流量。 這種情況需要有多個 ATA 中心。 ATA 中心的數目應該取決於 [ATA 容量規劃](ata-capacity-planning.md)。

## <a name="ata-gateway-and-ata-lightweight-gateway"></a>ATA 閘道和 ATA 輕量型閘道

### <a name="gateway-core-functionality"></a>閘道核心功能
**ATA 閘道** 和 **ATA 輕量型閘道** 兩者都有相同的核心功能︰

-   擷取並檢查網域控制站的網路流量。 這是 ATA 閘道的連接埠鏡像流量，和 ATA 輕量型閘道中網域控制站的本機流量。 

-   從 SIEM 或 Syslog 伺服器或者從使用 Windows 事件轉送的網域控制站接收 Windows 事件

-   從 Active Directory 網域擷取使用者和電腦的相關資料

-   執行網路實體 (使用者、群組及電腦) 解析

-   將相關資料傳輸至 ATA 中心

-   監視單一 ATA 閘道的多個網域控制站，或監視 ATA 輕量型閘道的單一網域控制站。

ATA 閘道會從您的網路接收網路流量和 Windows 事件，並在下列主要元件中加以處理︰

|||
|-|-|
|網路接聽程式|網路接聽程式會擷取網路流量和剖析流量。 這項工作會使用大量的 CPU，因此請務必在規劃 ATA 閘道或 ATA 輕量型閘道時檢查 [ATA Prerequisites](ata-prerequisites.md) (ATA 必要條件)。|
|事件接聽程式|事件接聽程式會擷取及剖析從網路上 SIEM 伺服器轉送的 Windows 事件。|
|Windows 事件記錄讀取器|Windows 事件記錄讀取器會讀取及剖析從網域控制站轉送至 ATA 閘道之 Windows 事件記錄的 Windows 事件。|
|網路活動轉譯程式 | 將剖析的流量轉譯為 ATA 所用的流量邏輯表示法 (NetworkActivity)。
|實體解析程式|實體解析程式會接受剖析的資料 (網路流量和事件)，並利用 Active Directory 解析資料以找出帳戶與身分識別資訊。 然後在剖析的資料中找出符合的 IP 位址。 實體解析程式會有效率地檢查封包標頭，啟用機器名稱、屬性和身分識別的驗證封包剖析。 實體解析程式會結合已剖析驗證封包與實際封包中的資料。|
|實體傳送者|實體傳送者會將剖析和相符的資料傳送到 ATA 中心。|

## <a name="ata-lightweight-gateway-features"></a>ATA 輕量型閘道功能

下列功能的運作方式不同，視您執行的是 ATA 閘道或 ATA 輕量型閘道而定。

-   ATA 輕量型閘道可以在本機讀取事件，而不需要設定事件轉送。

-   **網域同步器候選**<br>
網域同步器閘道負責主動同步處理特定 Active Directory 網域中的所有實體 (類似網域控制站自行複寫時所使用的機制)。 從候選清單中隨機選擇一個閘道，當成網域同步器。 <br><br>
如果同步器離線超過 30 分鐘，就會選擇其他的候選。 如果特定的網域沒有任何網域同步器可用，ATA 就會主動同步處理實體和其變更。不過，當受監視的流量中偵測到新的實體時，ATA 會被動地擷取新的實體。 
<br>如無任何網域同步器可用，而您搜尋的實體又沒有任何相關流量，就不會顯示任何搜尋結果。<br><br>
根據預設，所有的 ATA 閘道都是同步器候選。<br><br>
因為所有的 ATA 輕量型閘道皆較可能部署在分公司站台和小型的網域控制站上，所以它們預設不是同步器候選。


-   **資源限制**<br>
ATA 輕量型閘道包含的監視元件，會評估其執行所在網域控制站上的可用運算和記憶體容量。 監視處理程序每 10 秒執行一次，會動態更新 ATA 輕量型閘道處理程序的 CPU 和記憶體使用量配額，以確定在任何指定的時點，網域控制站都至少有 15% 的可用運算和記憶體資源。<br><br>
無論網域控制站發生什麼事，這項處理程序一律會釋出資源以確定網域控制站的核心功能不受影響。<br><br>
如果這導致 ATA 輕量型閘道用盡資源，則只有部分的流量受到監視，且 [健康情況] 頁面就會顯示監視警示：「已卸除連接埠鏡像網路流量」。

下表提供的網域控制站範例，其運算資源足可供應比目前所需更大的配額，所以全部的流量都受到監視︰

> [!div class="mx-tableFixed"]
||||||
|-|-|-|-|-|
|Active Directory (Lsass.exe)|ATA 輕量型閘道 (Microsoft.Tri.Gateway.exe)|其他 (其他處理程序) |ATA 輕量型閘道配額|閘道卸除中|
|30%|20%|10%|45%|否|

如果 Active Directory 需要執行更多的運算，就會減少 ATA 輕量型閘道需要的配額。 下例中，ATA 輕量型閘道需要比配置更多的配額，所以卸除了部分流量 (只監視部分流量)︰

> [!div class="mx-tableFixed"]
||||||
|-|-|-|-|-|
|Active Directory (Lsass.exe)|ATA 輕量型閘道 (Microsoft.Tri.Gateway.exe)|其他 (其他處理程序) |ATA 輕量型閘道配額|為閘道卸除中|
|60%|15%|10%|15%|是|


## <a name="your-network-components"></a>您的網路元件
若要使用 ATA，請務必檢查是否已設定好下列元件。

### <a name="port-mirroring"></a>連接埠鏡像
如果使用 ATA 閘道，就必須為要受監視的網域控制站設定連接埠鏡像，並使用實體或虛擬交換器將 ATA 閘道設定為目的地。 另一個選項是使用網路 TAP。 如果部分 (而非全部) 的網域控制站受到監視，ATA 仍可運作，但是偵測比較沒有效率。

雖然連接埠鏡像會將所有網域控制站的網路流量都鏡像處理到 ATA 閘道，但是有少部分的流量會傳送與壓縮至 ATA 中心進行分析。

您的網域控制站和 ATA 閘道可以為實體或虛擬，如需詳細資訊，請參閱 [Configure port mirroring](configure-port-mirroring.md) (設定連接埠鏡像)。


### <a name="events"></a>事件
若要增強傳遞雜湊、暴力密碼破解、修改敏感性群組以及 Honey Token 的 ATA 偵測，ATA 需要下列 Windows 事件：4776、4732、4733、4728、4729、4756、4757。 這些事件可透過 ATA 輕量型閘道自動讀取；如果未部署 ATA 輕量型閘道，則可以透過下列兩個方式之一轉送至 ATA 閘道：藉由將 ATA 閘道設定為接聽 SIEM 事件，或藉由[設定 Windows 事件轉送](#configuring-windows-event-forwarding)。

-   將 ATA 閘道設定為接聽 SIEM 事件 <br>將您的 SIEM 設定為轉送特定 Windows 事件至 ATA。 ATA 支援許多 SIEM 廠商。 如需詳細資訊，請參閱[設定事件收集](configure-event-collection.md)。

-   設定 Windows 事件轉送<br>讓 ATA 取得事件的另一個方法，是將網域控制站設定為將 Windows 事件 4776、4732、4733、4728、4729、4756 和 4757 轉送至 ATA 閘道。 如果您沒有 SIEM，或者 ATA 目前不支援您的 SIEM，這個方法特別有用。 如需 ATA 中 Windows 事件轉送的詳細資訊，請參閱[設定 Windows 事件轉送](configure-event-collection.md#configuring-windows-event-forwarding)。 這只適用於實體的 ATA 閘道，ATA 輕量型閘道不適用。

## <a name="related-videos"></a>相關影片
- [選擇正確的 ATA 閘道類型](https://channel9.msdn.com/Shows/Microsoft-Security/ATA-Deployment-Choose-the-Right-Gateway-Type)


## <a name="see-also"></a>另請參閱
- [ATA 必要條件](ata-prerequisites.md)
- [ATA 調整大小工具](http://aka.ms/atasizingtool)
- [ATA 容量規劃](ata-capacity-planning.md)
- [設定事件收集](configure-event-collection.md)
- [設定 Windows 事件轉送](configure-event-collection.md#configuring-windows-event-forwarding)
- [查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

