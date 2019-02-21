---
title: Azure 進階威脅防護架構 | Microsoft Docs
description: 描述 Azure 進階威脅防護 (ATP) 的架構
keywords: ''
author: mlottner
ms.author: mlottner
manager: barbkess
ms.date: 1/27/2019
ms.topic: article
ms.collection: M365-security-compliance
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 90f68f2c-d421-4339-8e49-1888b84416e6
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: ac10508d7120f6c643c4f8cd0ad59b32ed09bcb0
ms.sourcegitcommit: c48db18274edb2284e281960c6262d97f96e01d2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/14/2019
ms.locfileid: "56264214"
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

網域同步器候選負責主動同步處理特定 Active Directory 網域中的所有實體 (類似網域控制站進行複寫時所使用的機制)。 系統會從候選清單中隨機選擇一個感應器作為網域同步器。 

如果同步器離線超過 30 分鐘，就會選擇其他的候選。 如果特定的網域沒有任何網域同步器可供使用，則 Azure ATP 會主動同步實體和其變更；不過，當在受監視的流量中偵測到新的實體時，Azure ATP 就會擷取新的實體。
    
如無任何網域同步器可供使用，而您搜尋的實體又沒有任何相關流量，就不會顯示任何搜尋結果。

根據預設，Azure ATP 感應器並非同步器的候選。 若要將 Azure ATP 感應器手動設定為網域同步器候選，請遵循 [Azure ATP 安裝工作流程](install-atp-step5.md)中的步驟。

### <a name="resource-limitations"></a>資源限制

Azure ATP 感應器包含的監視元件，會評估其執行所在網域控制站上的可用運算和記憶體容量。 監視處理序每 10 秒會執行一次，且會動態更新 Azure ATP 感應器程序的 CPU 和記憶體使用量配額。 監視處理序可確保網域控制站一定會有至少 15% 的可用運算和記憶體資源。

無論網域控制站發生什麼事，監視處理序會持續釋出資源以確保網域控制站的核心功能絕不受影響。

如果監視處理序導致 Azure ATP 感應器用盡資源，則系統只會監視部分流量，並在 Azure ATP 入口網站的 [健康狀態] 頁面中顯示監視警示：「已捨棄連接埠鏡像網路流量」。

### <a name="windows-events"></a>Windows 事件

為了增強 Azure ATP 針對可疑身分識別竊取 (雜湊傳遞)、可疑驗證失敗、敏感性群組修改、可疑服務建立，以及 Honeytoken 活動等攻擊類型的偵測範圍，Azure ATP 需要分析下列 Windows 事件的記錄：4776、4732、4733、4728、4729、4756、4757 與 7045。 具備適當[進階稽核原則設定](atp-advanced-audit-policy.md)的 Azure ATP 感應器會自動讀取這些事件。 

## <a name="next-steps"></a>後續步驟

- [Azure ATP 必要條件](atp-prerequisites.md)
- [Azure ATP 調整大小工具](http://aka.ms/trisizingtool) \(英文\)
- [Azure ATP 容量規劃](atp-capacity-planning.md)
- [設定事件轉寄](configure-event-forwarding.md)
- [設定 Windows 事件轉送](configure-event-forwarding.md)
- [查看 Azure ATP 論壇！](https://aka.ms/azureatpcommunity)
