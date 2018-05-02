---
title: Azure 進階威脅防護架構 | Microsoft Docs
description: 描述 Azure 進階威脅防護 (ATP) 的架構
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/27/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 90f68f2c-d421-4339-8e49-1888b84416e6
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 435e5141c8abda338c1115004d1876ff5b7736a4
ms.sourcegitcommit: e0209c6db649a1ced8303bb1692596b9a19db60d
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/16/2018
---
適用於：Azure 進階威脅防護


# <a name="azure-atp-architecture"></a>Azure ATP 架構
此圖表能詳細說明 Azure 進階威脅防護的架構：

![Azure ATP 架構拓撲圖表](media/atp-architecture-topology.png)

Azure ATP 會運用使用實體或虛擬交換器針對 Azure ATP 獨立感應器的連接埠鏡像，監視網域控制站的網路流量。 如果您直接在網域控制站上部署 Azure ATP 感應器，則可免除連接埠鏡像的需求。 此外，Azure ATP 可以利用 Windows 事件 (直接從網域控制站或 SIEM 伺服器轉寄)，分析攻擊和威脅的資料。 Azure ATP 會從 Azure ATP 獨立感應器和 Azure ATP 感應器接收已剖析的流量。 然後執行分析、執行決定性偵測，並執行機器學習和行為演算法，以了解您的網路，啟用異常偵測並警告您可疑的活動。

本節說明網路與事件擷取的流程，並深入描述下列 ATP 主要元件的功能︰Azure ATP 獨立感應器、Azure ATP 感應器 (核心功能與 Azure ATP 獨立感應器相同) 和 Azure ATP 雲端服務。 

## <a name="azure-atp-components"></a>Azure ATP 元件
Azure ATP 包含下列元件：

-   **Azure ATP 工作區管理入口網站** <br>
Azure ATP 工作區管理入口網站可讓您建立工作區，並整合其他 Microsoft 服務。

> [!NOTE]
> 只有來自單一 Active Directory 樹系的感應器才能連線至單一工作區。

-   **Azure ATP 工作區入口網站** <br>
Azure ATP 工作區入口網站會接收來自 ATP 感應器和獨立感應器的資料。 它會監視、管理，並調查您環境中的威脅。

-   **Azure ATP 感應器**<br>
Azure ATP 感應器直接安裝在網域控制站上並直接監視其流量，不需要專用伺服器或設定連接埠鏡像。 

-   **Azure ATP 獨立感應器**<br>
Azure ATP 獨立感應器是安裝在使用連接埠鏡像或網路 TAP 來監視網域控制站流量的專用伺服器上。 它可以替代 Azure ATP 感應器。

## <a name="deployment-options"></a>部署選項
您可以使用下列感應器組合部署 Azure ATP︰

-   **只使用 Azure ATP 感應器**<br>
Azure ATP 部署可以只包含 Azure ATP 感應器：Azure ATP 感應器是部署在每個網域控制站上，不需要設定任何其他伺服器或連接埠鏡像。

-   **只使用 Azure ATP 獨立感應器** <br>
您的 Azure ATP 部署可以只包含 Azure ATP 獨立感應器，不需要任何 Azure ATP 感應器：所有網域控制站都必須設定以啟用針對 Azure ATP 獨立感應器的連接埠鏡像，否則便必須具備網路 TAP。

-   **同時使用 Azure ATP 獨立感應器和 Azure ATP 感應器**<br>
您的 Azure ATP 部署同時包含 Azure ATP 獨立感應器和 Azure ATP 感應器。 Azure ATP 感應器會安裝在您部分的網域控制站上 (例如您分支網站中的所有網域控制站)。 同時，其他網域控制站則是由 Azure ATP 獨立感應器監視 (例如您主要資料中心中的大型網域控制站)。


### <a name="azure-atp-workspace-management-portal"></a>Azure ATP 工作區管理入口網站

Azure ATP 工作區管理入口網站可讓您：

-   建立及管理 Azure ATP 工作區

-   與其他 Microsoft 安全性服務整合

將您的主要工作區設定為 [主要]。 只有一個工作區可以設定為主要工作區。 將工作區設定為主要工作區會影響整合，您只能針對主要工作區將 Azure ATP 與 Windows Defender ATP 整合。 您稍後可以變更要作為主要工作區的工作區，但若要這麼做，您必須移除已針對目前主要工作區設定的所有整合。

> [!NOTE]
> Azure ATP 目前支援建立兩個工作區。 建議您為生產環境建立主要工作區，而其他工作區作為預備環境。
> 刪除工作區之後，您可以連絡支援人員重新啟動它。 您最多可有三個刪除的工作區。 若要增加儲存的刪除工作區數量，請連絡 Azure ATP 支援。


### <a name="azure-atp-workspace-portal"></a>Azure ATP 工作區入口網站

Azure ATP 工作區入口網站可讓您管理下列 Azure ATP 功能：

-   管理 Azure ATP 感應器和獨立感應器組態設定

-   檢視從 Azure ATP 獨立感應器和 Azure ATP 感應器接收的資料 

-   監視偵測到的可疑活動，根據行為機器學習演算法來偵測異常行為，並根據決定性演算法來偵測以攻擊狙殺鏈為基礎的進階攻擊

-   選擇性：工作區管理入口網站可設定為在偵測到可疑活動或健康情況事件時傳送電子郵件和事件。


|||
|-|-|
|實體接收者|接收來自所有 Azure ATP 感應器和 Azure ATP 獨立感應器的實體批次。|
|網路活動處理器|處理每個批次中收到的所有網路活動。 例如，比對可能從不同電腦執行的各種 Kerberos 步驟|
|實體程分析工具|根據流量與事件設定所有唯一實體。 例如，Azure ATP 會針對每個使用者設定檔更新登入電腦清單。|
|Azure ATP 工作區管理入口網站|管理您的 Azure ATP 工作區。|
|Azure ATP 工作區入口網站|Azure ATP 工作區用來設定 Azure ATP，以及監視 Azure ATP 在您網路上所偵測到的可疑活動。 Azure ATP 工作區不需仰賴 Azure ATP 感應器，甚至在 Azure ATP 感應器服務停止時仍可執行。 |
|偵測器|偵測器使用機器學習演算法和決定性規則，在您的網路中尋找可疑活動和異常使用者行為。|

決定要在網路上部署多少 Azure ATP 工作區時，請考慮下列準則︰

-   一個 Azure ATP 工作區可以監視單一 Active Directory 樹系。 如果您有多個 Active Directory 樹系，每個 Active Directory 樹系需要至少一個 Azure ATP 雲端服務。


## <a name="azure-atp-sensor-and-azure-atp-standalone-sensor"></a>Azure ATP 感應器和 Azure ATP 獨立感應器

**Azure ATP 感應器**和 **Azure ATP 獨立感應器**兩者都有相同的核心功能：

-   擷取並檢查網域控制站的網路流量。 這是 Azure ATP 獨立感應器的連接埠鏡像流量，和 Azure ATP 感應器中網域控制站的本機流量。 

-   直接從網域控制站 (針對 ATP 感應器) 或從 SIEM 或 Syslog 伺服器 (針對 ATP 獨立感應器) 接收 Windows 事件

-  從您的 VPN 提供者接收 RADIUS 帳戶處理資訊

-   從 Active Directory 網域擷取使用者和電腦的相關資料

-   執行網路實體 (使用者、群組及電腦) 解析

-   將相關資料傳輸至 Azure ATP 雲端服務

-   從單一 Azure ATP 獨立感應器監視多個網域控制站，或使用單一 Azure ATP 感應器監視單一網域控制站。

根據預設值，Azure ATP 最多支援 100 個感應器。 如果您想要安裝更多，請連絡 Azure ATP 支援。

Azure ATP 獨立感應器會從您的網路接收網路流量和 Windows 事件，並在下列主要元件中加以處理︰

|||
|-|-|
|網路接聽程式|網路接聽程式會擷取網路流量並剖析流量。 這項工作會使用大量的 CPU，因此在規劃 Azure ATP 感應器或 Azure ATP 獨立感應器時，請務必檢查 [Azure ATP 必要條件](atp-prerequisites.md)。|
|事件接聽程式|事件接聽程式會擷取並剖析從網路上 SIEM 伺服器轉寄的 Windows 事件。|
|Windows 事件記錄讀取器|Windows 事件記錄讀取器會讀取及剖析從網域控制站轉寄至 Azure ATP 獨立感應器之 Windows 事件記錄的 Windows 事件。|
|網路活動轉譯程式 | 將剖析的流量轉譯為 Azure ATP 所使用的流量邏輯表示法 (NetworkActivity)。
|實體解析程式|實體解析程式會接受剖析的資料 (網路流量和事件)，並利用 Active Directory 解析資料以找出帳戶與身分識別資訊。 然後在剖析的資料中找出符合的 IP 位址。 實體解析程式會有效率地檢查封包標頭，啟用機器名稱、屬性和身分識別的驗證封包剖析。 實體解析程式會結合已剖析驗證封包與實際封包中的資料。|
|實體傳送者|實體傳送者會將已剖析和符合的資料傳送到 Azure ATP 雲端服務。|

## <a name="azure-atp-sensor-features"></a>Azure ATP 感應器功能

下列功能的運作方式，視您執行的是 Azure ATP 獨立感應器或 Azure ATP 感應器而有所不同。

-   Azure ATP 感應器可在本機讀取事件，而不需要設定事件轉寄。

-   **網域同步器候選**<br>
網域同步器候選負責主動同步處理特定 Active Directory 網域中的所有實體 (類似網域控制站進行複寫時所使用的機制)。 系統會從候選清單中隨機選擇一個感應器作為網域同步器。 <br><br>
如果同步器離線超過 30 分鐘，就會選擇其他的候選。 如果特定的網域沒有任何網域同步器可供使用，Azure ATP 就會主動同步處理實體和其變更。不過，當在受監視的流量中偵測到新的實體時，Azure ATP 就會擷取新的實體。 
<br>如無任何網域同步器可用，而您搜尋的實體又沒有任何相關流量，就不會顯示任何搜尋結果。<br><br>
根據預設，所有的 Azure ATP 獨立感應器都是同步器候選。<br><br>
Azure ATP 感應器預設並非同步器候選。


-   **資源限制**<br>
Azure ATP 感應器包含的監視元件，會評估其執行所在網域控制站上的可用運算和記憶體容量。 監視程序每 10 秒會執行一次，且會動態更新 Azure ATP 感應器程序的 CPU 和記憶體使用量配額，以確定在任何指定的時間點，網域控制站都至少會有 15% 的可用運算和記憶體資源。<br><br>
無論網域控制站發生什麼事，這項處理程序一律會釋出資源以確定網域控制站的核心功能不受影響。<br><br>
如果這導致 Azure ATP 感應器用盡資源，則系統只會監視部分流量，且 [健康情況] 頁面中會顯示監視警示：「已捨棄連接埠鏡像網路流量」。

下表提供的網域控制站範例，其運算資源足可供應比目前所需更大的配額，所以全部的流量都受到監視︰

> [!div class="mx-tableFixed"]
||||||
|-|-|-|-|-|
|Active Directory (Lsass.exe)|Azure ATP 感應器 (Microsoft.Tri.sensor.exe)|其他 (其他處理程序) |Azure ATP 感應器配額|感應器是否正在捨棄流量？|
|30%|20%|10%|45%|否|

如果 Active Directory 需要更多運算能力，就會減少 Azure ATP 感應器需要的配額。 下列範例中，Azure ATP 感應器需要比已配置配額還要多的配額，所以捨棄了部分流量 (僅監視部分流量)：

> [!div class="mx-tableFixed"]
||||||
|-|-|-|-|-|
|Active Directory (Lsass.exe)|Azure ATP 感應器 (Microsoft.Tri.sensor.exe)|其他 (其他處理程序) |Azure ATP 感應器配額|感應器是否正在捨棄流量？|
|60%|15%|10%|15%|是|


## <a name="your-network-components"></a>您的網路元件
若要使用 Azure ATP，請務必檢查是否已設定好下列元件。

### <a name="port-mirroring"></a>連接埠鏡像
如果使用 Azure ATP 獨立感應器，就必須為要監視的網域控制站設定連接埠鏡像，並使用實體或虛擬交換器將 Azure ATP 獨立感應器設定為目的地。 另一個選項是使用網路 TAP。 如果只有部分 (而非全部) 的網域控制站受到監視，Azure ATP 仍可運作，但是偵測比較沒有效率。

雖然連接埠鏡像會將所有網域控制站的網路流量都鏡像處理到 Azure ATP 獨立感應器，但是有少部分的流量會傳送並壓縮至 Azure ATP 雲端服務進行分析。

您的網域控制站和 Azure ATP 獨立感應器可以是實體或虛擬的。 如需詳細資訊，請參閱[設定連接埠鏡像](configure-port-mirroring.md)。


### <a name="events"></a>事件
若要增強 Azure ATP 偵測傳遞雜湊、暴力密碼破解、修改敏感性群組、建立可疑服務，以及修改 Honey Token 的能力，Azure ATP 需要下列 Windows 事件：4776、4732、4733、4728、4729、4756、4757 和 7045。 Azure ATP 感應器可以直接讀取這些事件。如果沒有部署 Azure ATP 感應器，則有兩種方法可以將之轉寄到 Azure ATP 獨立感應器：一種是將 Azure ATP 獨立感應器設定為接聽 SIEM 事件，另一種是[設定 Windows 事件轉寄](configure-event-forwarding.md)。

-   設定 Azure ATP 獨立感應器接聽 SIEM 事件 <br>將您的 SIEM 設定為將特定 Windows 事件轉寄至 ATP。 Azure ATP 能支援數個 SIEM 廠商。 如需詳細資訊，請參閱[設定事件轉寄](configure-event-forwarding.md)。

-   設定 Windows 事件轉送<br>讓 Azure ATP 取得事件的另一個方法，是將網域控制站設定為將 Windows 事件 4776、4732、4733、4728、4729、4756、4757 和 7045 轉寄至 Azure ATP 獨立感應器。 如果您沒有 SIEM，或是 ATP 目前不支援您的 SIEM，這個方法特別有用。 如需 ATP 中 Windows 事件轉寄的詳細資訊，請參閱[設定 Windows 事件轉寄](configure-event-forwarding.md)。 這只適用於實體 Azure ATP 獨立感應器，不適用 Azure ATP 感應器。


## <a name="see-also"></a>另請參閱
- [Azure ATP 必要條件](atp-prerequisites.md)
- [Azure ATP 調整大小工具](http://aka.ms/trisizingtool) \(英文\)
- [Azure ATP 容量規劃](atp-capacity-planning.md)
- [設定事件轉寄](configure-event-forwarding.md)
- [設定 Windows 事件轉送](configure-event-forwarding.md)

- - [查看 ATP 論壇！](https://aka.ms/azureatpcommunity)\(英文\)
