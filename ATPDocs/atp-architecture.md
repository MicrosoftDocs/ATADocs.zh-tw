---
title: Azure 進階威脅防護架構 | Microsoft Docs
description: 描述 Azure 進階威脅防護 (ATP) 的架構
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 1/27/2019
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 90f68f2c-d421-4339-8e49-1888b84416e6
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 6988b41b64dc3d8afef5f7af614f78b41501e2af
ms.sourcegitcommit: 19ff0ed88e450506b5725bbcbb0d0bd2f0c5e4bb
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/27/2019
ms.locfileid: "55085311"
---
# <a name="azure-atp-architecture"></a>Azure ATP 架構

Azure ATP 可直接從您的網域控制站擷取和剖析網路流量並運用 Windows 事件，以監視您的網域控制站，然後分析攻擊和威脅資料。 Azure ATP 會利用分析、確定性偵測、機器學習和行為演算法，來了解您的網路、啟用異常偵測並警告您可疑的活動。

Azure 進階威脅防護架構：

![Azure ATP 架構拓撲圖表](media/atp-architecture-topology.png)

本節描述 Azure ATP 的網路與事件擷取流程運作方式，並進一步詳細描述下列主要元件的功能：Azure ATP 入口網站、Azure ATP 感應器和 Azure ATP 雲端服務。 

如果 Azure ATP 感應器直接安裝在網域控制站上，即會直接從網域控制站存取所需的事件記錄檔。 在感應器剖析記錄檔和網路流量之後，Azure ATP 只會將經剖析的資訊傳送給 Azure ATP 雲端服務 (僅傳送某個百分比的記錄檔)。 

## <a name="azure-atp-components"></a>Azure ATP 元件
Azure ATP 包含下列元件：

-   **Azure ATP 入口網站** <br>
Azure ATP 入口網站可讓您建立 Azure ATP 執行個體、顯示從 Azure ATP 感應器接收的資料，並可讓您監視、管理及調查網路環境中的威脅。  
-   **Azure ATP 感應器**<br>
Azure ATP 感應器是直接安裝在您的網域控制站上。 感應器可直接監視網域控制站的流量，而不需要專用的伺服器或連接埠鏡像設定。

-   **Azure ATP 雲端服務**<br>
Azure ATP 雲端服務目前部署於美國、歐洲和亞洲，並會在 Azure 基礎結構上執行。 Azure ATP 雲端服務會與 Microsoft Intelligent Security Graph 連線。 

## <a name="azure-atp-portal"></a>Azure ATP 入口網站 
使用 Azure ATP 入口網站進行下列作業：
- 建立您的 Azure ATP 執行個體
- 與其他 Microsoft 安全性服務整合 
- 管理 Azure ATP 感應器的組態設定 
- 檢視 Azure ATP 感應器接收的資料
- 監視偵測到的可疑活動和以攻擊狙殺鏈模式為基礎的可疑攻擊
- **選擇性**：您也可以將入口網站設定為在偵測到安全性警訊或健康狀態問題時傳送電子郵件和事件

> [!NOTE]
> - 若 Azure ATP 執行個體在 60 天內未安裝感應器，系統可能會刪除執行個體且您必須重新建立。

## <a name="azure-atp-sensor"></a>Azure ATP 感應器
Azure ATP 感應器具有下列核心功能：
- 擷取並檢查網域控制站網路流量 (網域控制站的本機流量)
- 直接從網域控制站接收 Windows 事件 
- 從您的 VPN 提供者接收 RADIUS 帳戶處理資訊
- 從 Active Directory 網域擷取使用者和電腦的相關資料
- 執行網路實體 (使用者、群組及電腦) 解析
- 將相關資料傳輸至 Azure ATP 雲端服務

 
## <a name="azure-atp-sensor-features"></a>Azure ATP 感應器功能
Azure ATP 感應器可本機讀取事件，而不需要購買及維護額外的硬體或設定。 Azure ATP 感應器也支援 Windows 事件追蹤 (ETW)，以提供多個偵測的記錄資訊。 ETW 式偵測包含使用網域控制站複寫要求和網域控制站升階嘗試進行的可疑 DCShadow 攻擊。

### <a name="domain-synchronizer-candidate"></a>網域同步器候選

    The domain synchronizer candidate is responsible for synchronizing all entities from a specific Active Directory domain proactively (similar to the mechanism used by the domain controllers themselves for replication). One sensor is chosen randomly, from the list of candidates, to serve as the domain synchronizer. 

    If the synchronizer is offline for more than 30 minutes, another candidate is chosen instead. If there is no domain synchronizer available for a specific domain, Azure ATP proactively synchronizes entities and their changes, however Azure ATP retrieves new entities as they are detected in the monitored traffic. 
    
    If there is no domain synchronizer available, and you search for an entity that did not have any traffic related to it, no search results are displayed.

    By default, Azure ATP sensors are not synchronizer candidates. To manually set an Azure ATP sensor as a domain synchronizer candidate, follow the steps in the [Azure ATP installation workflow](install-atp-step5.md#configure-azure-atp-sensor-settings).

### <a name="resource-limitations"></a>資源限制

    The Azure ATP sensor includes a monitoring component that evaluates the available compute and memory capacity on the domain controller on which it is running. The monitoring process runs every 10 seconds and dynamically updates the CPU and memory utilization quota on the Azure ATP sensor process. The monitoring process makes sure the domain controller always has at least 15% of free compute and memory resources available.

    No matter what occurs on the domain controller, the monitoring process continually frees up resources to make sure the domain controller's core functionality is never affected.

    If the monitoring process causes the Azure ATP sensor to run out of resources, only partial traffic is monitored and the monitoring alert "Dropped port mirrored network traffic" appears in the Azure ATP portal Health page.

### <a name="windows-events"></a>Windows 事件

    To enhance Azure ATP detection coverage of suspected identity theft (pass-the-hash), suspicious authentication failures,modifications to sensitive groups, creation of suspicious services, and Honeytoken activity types of attack, Azure ATP needs to analyze the logs of the following Windows events: 4776,4732,4733,4728,4729,4756,4757, and 7045. These events are read automatically by Azure ATP sensors with correct [advanced audit policy settings](atp-advanced-audit-policy.md). 

## <a name="see-also"></a>另請參閱
- [Azure ATP 必要條件](atp-prerequisites.md)
- [Azure ATP 調整大小工具](http://aka.ms/trisizingtool) \(英文\)
- [Azure ATP 容量規劃](atp-capacity-planning.md)
- [設定事件轉寄](configure-event-forwarding.md)
- [設定 Windows 事件轉送](configure-event-forwarding.md)
- [查看 Azure ATP 論壇！](https://aka.ms/azureatpcommunity)
