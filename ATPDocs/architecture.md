---
title: 適用於身分識別的 Microsoft Defender 架構
description: 描述適用於身分識別的 Microsoft Defender 的架構
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 10/26/2020
ms.topic: overview
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: e6baa54d7e8738d6132bf33d9ce8f4e829e6243f
ms.sourcegitcommit: f434dbff577d9944df18ca7533d026acdab0bb42
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/03/2020
ms.locfileid: "93276752"
---
# <a name="microsoft-defender-for-identity-architecture"></a>適用於身分識別的 Microsoft Defender 架構

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

[!INCLUDE [Product long](includes/product-long.md)] 可直接從您的網域控制站擷取及剖析網路流量並運用 Windows 事件，以監視您的網域控制站，然後分析攻擊和威脅資料。 [!INCLUDE [Product short](includes/product-short.md)] 會利用分析、確定性偵測、機器學習與行為演算法，來了解您的網路、啟用異常偵測並在發現可疑活動時警告您。

[!INCLUDE [Product short](includes/product-short.md)] 架構：

![[!INCLUDE [Product short](includes/product-short.md)] 架構拓撲圖表](media/architecture-topology.png)

此節描述[!INCLUDE [Product short](includes/product-short.md)] 的網路與事件擷取流程運作方式，並進一步詳細描述下列主要元件的功能：[!INCLUDE [Product short](includes/product-short.md)] 入口網站、[!INCLUDE [Product short](includes/product-short.md)] 感應器與[!INCLUDE [Product short](includes/product-short.md)] 雲端服務。

如果[!INCLUDE [Product short](includes/product-short.md)] 感應器直接安裝在網域控制站上，即會直接從網域控制站存取所需的事件記錄檔。 在感應器剖析記錄檔和網路流量之後，[!INCLUDE [Product short](includes/product-short.md)] 只會將經剖析的資訊傳送到[!INCLUDE [Product short](includes/product-short.md)] 雲端服務 (僅傳送某個百分比的記錄檔)。

## <a name="product-short-components"></a>[!INCLUDE [Product short](includes/product-short.md)] 元件

[!INCLUDE [Product short](includes/product-short.md)] 包含下列元件：

- **[!INCLUDE [Product short](includes/product-short.md)] 入口網站**  
[!INCLUDE [Product short](includes/product-short.md)] 入口網站可讓您建立[!INCLUDE [Product short](includes/product-short.md)] 執行個體、顯示從[!INCLUDE [Product short](includes/product-short.md)] 感應器接收的資料，並可讓您監視、管理及調查網路環境中的威脅。

- **[!INCLUDE [Product short](includes/product-short.md)] 感應器**  
[!INCLUDE [Product short](includes/product-short.md)] 感應器是直接安裝在您的網域控制站上。 感應器可直接監視網域控制站的流量，而不需要專用的伺服器或連接埠鏡像設定。
- **[!INCLUDE [Product short](includes/product-short.md)] 雲端服務**  
[!INCLUDE [Product short](includes/product-short.md)] 雲端服務目前部署於美國、歐洲和亞洲，並會在 Azure 基礎結構上執行。 [!INCLUDE [Product short](includes/product-short.md)] 雲端服務會與 Microsoft Intelligent Security Graph 連線。

## <a name="product-short-portal"></a>[!INCLUDE [Product short](includes/product-short.md)] 入口網站

使用[!INCLUDE [Product short](includes/product-short.md)] 入口網站來：

- 建立您的[!INCLUDE [Product short](includes/product-short.md)] 執行個體
- 與其他 Microsoft 安全性服務整合
- 管理[!INCLUDE [Product short](includes/product-short.md)] 感應器組態設定
- 檢視從[!INCLUDE [Product short](includes/product-short.md)] 感應器接收的資料
- 監視偵測到的可疑活動和以攻擊狙殺鏈模式為基礎的可疑攻擊
- **選擇性** ：您也可以將入口網站設定為在偵測到安全性警訊或健康狀態問題時傳送電子郵件和事件

> [!NOTE]
> 若[!INCLUDE [Product short](includes/product-short.md)] 執行個體在 60 天內未安裝感應器，系統可能會刪除執行個體且您必須重新建立。

## <a name="product-short-sensor"></a>[!INCLUDE [Product short](includes/product-short.md)] 感應器

[!INCLUDE [Product short](includes/product-short.md)] 感應器具有下列核心功能：

- 擷取並檢查網域控制站網路流量 (網域控制站的本機流量)
- 直接從網域控制站接收 Windows 事件
- 從您的 VPN 提供者接收 RADIUS 帳戶處理資訊
- 從 Active Directory 網域擷取使用者和電腦的相關資料
- 執行網路實體 (使用者、群組及電腦) 解析
- 將相關資料傳輸至[!INCLUDE [Product short](includes/product-short.md)] 雲端服務

## <a name="product-short-sensor-features"></a>[!INCLUDE [Product short](includes/product-short.md)] 感應器功能

[!INCLUDE [Product short](includes/product-short.md)] 感應器可讀取本機事件，而不需要購買及維護額外的硬體或設定。 [!INCLUDE [Product short](includes/product-short.md)] 感應器也支援 Windows 事件追蹤 (ETW)，以提供多個偵測的記錄資訊。 ETW 式偵測包含使用網域控制站複寫要求和網域控制站升階嘗試進行的可疑 DCShadow 攻擊。

### <a name="domain-synchronizer-process"></a>自動網域同步器流程

網域同步器流程負責主動同步處理特定 Active Directory 網域中的所有實體 (類似網域控制站自行複寫時所使用的機制)。 系統會自動從您所有合格的感應器當中隨機選擇一個感應器，當作網域同步器。

如果網域同步器離線超過 30 分鐘，則會自動選擇另一個感應器。

### <a name="resource-limitations"></a>資源限制

[!INCLUDE [Product short](includes/product-short.md)] 感應器包含的監視元件，會評估其執行所在網域控制站上的可用運算和記憶體容量。 監視處理序每 10 秒會執行一次，而且會動態更新[!INCLUDE [Product short](includes/product-short.md)] 感應器程序的 CPU 和記憶體使用量配額。 監視處理序可確保網域控制站一定會有至少 15% 的可用運算和記憶體資源。

無論網域控制站發生什麼事，監視處理序會持續釋出資源以確保網域控制站的核心功能絕不受影響。

如果監視處理序導致[!INCLUDE [Product short](includes/product-short.md)] 感應器用盡資源，則系統只會監視部分流量，而且會在[!INCLUDE [Product short](includes/product-short.md)] 入口網站的 [健康情況] 頁面中顯示健康情況警示：「已捨棄連接埠鏡像網路流量」。

### <a name="windows-events"></a>Windows 事件

為了加強與 NTLM 驗證、敏感性群組修改與可疑服務建立相關的[!INCLUDE [Product short](includes/product-short.md)] 偵測涵蓋範圍，[!INCLUDE [Product short](includes/product-short.md)] 必須分析下列 Windows 事件的記錄檔：4776、4732、4733、4728、4729、4756、4757、7045 與 8004。 具備正確[進階稽核原則設定](configure-windows-event-collection.md)的[!INCLUDE [Product short](includes/product-short.md)] 感應器會自動讀取這些事件。 若要確定已依服務所需[稽核 Windows 事件 8004](configure-windows-event-collection.md#ntlm-authentication-using-windows-event-8004)，請檢閱您的 [NTLM 稽核設定](/archive/blogs/askds/ntlm-blocking-and-you-application-analysis-and-auditing-methodologies-in-windows-7) \(英文\)。

## <a name="next-steps"></a>後續步驟

- [[!INCLUDE [Product short](includes/product-short.md)] 先決條件](prerequisites.md)
- [[!INCLUDE [Product short](includes/product-short.md)] 大小調整工具](https://aka.ms/trisizingtool) \(英文\)
- [[!INCLUDE [Product short](includes/product-short.md)] 容量規畫](capacity-planning.md)
- [設定事件轉寄](configure-event-forwarding.md)
- [設定 Windows 事件轉送](configure-event-forwarding.md)
- [查看[!INCLUDE [Product short](includes/product-short.md)] 論壇！](https://aka.ms/MDIcommunity)\(英文\)
