---
# required metadata

title: ATA 架構 | Microsoft Advanced Threat Analytics
description: 描述 Microsoft Advanced Threat Analytics 的架構 (ATA)
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 892b16d2-58a6-49f9-8693-1e5f69d8299c

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# ATA 架構
此圖表中詳細說明 Advanced Threat Analytics 架構︰

![ATA 架構拓撲圖表](media/ATA-architecture-topology.jpg)

ATA 有兩個主要元件 - ATA 閘道和 ATA 中心。

藉由鏡像網域控制站之間往來的網路流量，並藉由查看 Windows 事件 (直接從網域控制站或從 SIEM 伺服器轉送) 與分析攻擊和威脅的資料，這些元件可連接到您現有的網路。

本章節描述網路流量和事件擷取，並向下切入 ATA 閘道和 ATA 中心的主要元件與其功能。

![ATA 流量圖表](media/ATA-traffic-flow.jpg)

## ATA 元件
ATA 包含下列項目：

-   一或多個 ATA 閘道

-   一個 ATA 中心

## ATA 閘道
**ATA 閘道**會執行下列功能：

-   透過連接埠鏡像擷取並檢查網域控制站的網路流量

-   從 SIEM 或 Syslog 伺服器，或從使用 Windows 事件轉送的網域控制站接收 Windows 事件

-   從 Active Directory 網域擷取使用者和電腦的相關資料

-   執行網路實體解析 (使用者、群組及電腦)

-   傳輸相關資料至 ATA 中心

-   從單一 ATA 閘道監視多個網域控制站

ATA 閘道會從您的網路接收鏡像的網路流量和 Windows 事件，並在下列主要元件中加以處理︰

|||
|-|-|
|網路接聽程式|網路接聽程式負責擷取網路流量和剖析流量。 這是大量使用 CPU 的工作，因此請務必在規劃 ATA 閘道時檢查 [ATA 必要條件](/advanced-threat-analytics/PlanDesign/ata-prerequisites)。|
|事件接聽程式|事件接聽程式負責擷取及剖析從網路上 SIEM 伺服器轉送的 Windows 事件。|
|Windows 事件記錄讀取器|Windows 事件記錄讀取器負責讀取及剖析從網域控制站轉送至 ATA 閘道之 Windows 事件記錄的 Windows 事件。|
|網路活動轉譯程式 | 將剖析的流量轉譯為流量的t ATA 邏輯表示法 (NetworkActivity)。
|實體解析程式|實體解析程式會接受剖析的資料 (網路流量和事件)，並利用 Active Directory 解析資料以找出帳戶與身分識別資訊，並使其符合剖析資料中找到的 IP 位址。  此外，實體解析程式會有效率地檢查封包標頭，啟用機器名稱、屬性和身分識別的驗證封包剖析，並將它與實際封包中的資料結合。|
|實體傳送者|實體傳送者負責將剖析和相符的資料傳送到 ATA 中心。|
決定要在網路上部署多少 ATA 閘道時，請考慮下列項目︰

-   Active Directory 樹系和網域

    ATA 閘道可以監視來自單一 Active Directory 樹系之多個網域的流量。   監視多個 Active Directory 樹系需要個別 ATA 部署。 ATA 閘道不應該設定為監視來自不同樹系之網域控制站的網路流量。

-   連接埠鏡像

    連接埠鏡像考量可能需要您在每個資料中心 / 地理區域部署至少一個 ATA 閘道。

-   容量

    每個 ATA 閘道每秒可以剖析和傳送某個流量。 如果您要監視的網域控制站正在傳送及接收的流量多於 ATA 閘道所能處理的流量，您必須根據流量新增其他 ATA 閘道。 如需詳細資訊，請參閱 [ATA 容量規劃](/advanced-threat-analytics/PlanDesign/ata-capacity-planning)。

## ATA 中心
**ATA 中心**會執行下列功能：

-   管理 ATA 閘道組態設定

-   從 ATA 閘道接收資料

-   偵測可疑活動

-   執行各種行為機器學習引擎

-   執行 ATA 主控台。

-   選擇性︰ATA 中心可以設定為偵測到可疑活動時傳送電子郵件和事件。

ATA 中心會從 ATA 閘道接收剖析的流量、執行分析、執行決定性偵測並執行機器學習和行為演算法，以了解您的網路來啟用異常偵測，並警告您可疑的活動。

|||
|-|-|
|實體接收者|從所有 ATA 閘道接收實體批次。|
|網路活動處理器|處理每個批次中收到的所有網路活動。 例如，比對可能從不同電腦執行的各種 Kerberos 步驟|
|實體程分析工具|根據流量與事件設定所有唯一實體。 比方說，這是 ATA 更新每個使用者設定檔之登入電腦清單的位置。|
|ATA 中心資料庫用戶端 |管理網路活動和事件寫入資料庫的程序。 |
|資料庫|ATA 使用 MongoDB，其目的為在系統中儲存所有資料︰<br /><br />-   網路活動<br />-   事件<br />-   唯一實體<br />-   可疑活動<br />-   ATA 設定|
|偵測引擎|偵測引擎使用機器學習演算法和決定性規則，在您的網路中尋找可疑活動和異常使用者行為。|
|ATA 主控台|ATA 主控台可用來設定 ATA 及監視 ATA 在網路上偵測到的可疑活動。 ATA 主控台並未依存於 ATA 中心服務，即使在服務停止時，只要它可以和資料庫通訊，就會持續執行。|
決定要在網路上部署多少 ATA 中心時，請考慮下列項目︰

-   一個 ATA 中心可以監視單一 Active Directory 樹系。 如果您有多個 Active Directory 樹系，每個 Active Directory 樹系需要至少一個 ATA 中心。

    在大型的 Active Directory 部署中，單一 ATA 中心可能無法處理所有網域控制站的所有流量。 在此情況下，需要多個 ATA 中心，而且 ATA 偵測比較沒有效率。 ATA 中心的數目應該取決於 [ATA 容量規劃](/advanced-threat-analytics/PlanDesign/ata-capacity-planning)。

## 您的網路元件
為了使用 ATA，您必須盡少變更現有網路，但是您必須確定下列項目。

### 連接埠鏡像
若要讓 ATA 運作，您必須在受監視的 Active Directory 樹系中啟用所有網域控制站的連接埠鏡像。 如果部分 (而非全部) 的網域控制站都有對 ATA 啟用的連接埠鏡像，ATA 就會運作，但是偵測將會比較沒有效率。

從網域控制站將連接埠鏡像設定至 ATA 閘道。 雖然所有網域控制站的網路流量都會鏡像處理到 ATA 閘道，但是只有少部分的流量會傳送與壓縮至 ATA 中心進行分析。

您的網域控制站和 ATA 閘道可以是實體或虛擬的，如需詳細資訊，請參閱[設定連接埠鏡像](/advanced-threat-analytics/PlanDesign/configure-port-mirroring)。

### 事件
若要增強 ATA 對傳遞雜湊攻擊的偵測，ATA 需要識別碼為 4776 的 Windows 事件記錄檔。 可透過下列兩種方式的其中一種轉送到 ATA 閘道，將 ATA 閘道設定為接聽 SIEM 事件，或使用 Windows 事件轉送。

-   將 ATA 閘道設定為接聽 SIEM 事件

    將您的 SIEM 設定為轉送特定 Windows 事件至 ATA。 ATA 支援許多 SIEM 廠商。 如需詳細資訊，請參閱[設定事件收集](/advanced-threat-analytics/PlanDesign/configure-event-collection)。

-   設定 Windows 事件轉送

    ATA 可以取得事件的另一個方法是將網域控制站設定為將 Windows 事件 4776 轉送至 ATA 閘道。 如果您沒有 SIEM，或者 ATA 目前不支援您的 SIEM，這個方法特別有用。 如需 ATA 中 Windows 事件轉送的詳細資訊，請參閱[設定 Windows 事件轉送](/advanced-threat-analytics/PlanDesign/configure-event-collection#ATA_event_WEF)。

## 另請參閱
- [ATA 必要條件](/advanced-threat-analytics/PlanDesign/ata-prerequisites)
- [ATA 容量規劃](/advanced-threat-analytics/PlanDesign/ata-capacity-planning)
- [設定事件收集](/advanced-threat-analytics/PlanDesign/configure-event-collection)
- [設定 Windows 事件轉送](/advanced-threat-analytics/PlanDesign/configure-event-collection#ATA_event_WEF)
- [如需支援，請查看我們的論壇！](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=Apr16_HO2-->


