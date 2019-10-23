---
title: 從 Advanced Threat Analytics 移至 Azure 進階威脅防護 | Microsoft Docs
description: 了解如何將現有的 Advanced Threat Analytics 安裝移至 Azure ATP。
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 10/16/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: e734e382-c4b1-43ca-9a8d-96c91daf2578
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: f54c60f97c9489934f0ac0a40b3b27780e6a60d9
ms.sourcegitcommit: dd8db49bc54acc5483a3fa889379230d144b0623
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 10/21/2019
ms.locfileid: "72690241"
---
# <a name="advanced-threat-analytics-ata-to-azure-advanced-threat-protection-azure-atp"></a>Advanced Threat Analytics (ATA) 移至 Azure 進階威脅防護 (Azure ATP) 


您可以使用本指南將現有的 ATA 安裝移至 Azure 進階威脅防護 (Azure ATP) 服務。 本指南會說明 Azure ATP 必要條件和需求，並詳細說明如何規劃和完成移動。 其中還包含一些驗證步驟和祕訣，可在安裝後利用運用 Azure ATP 的最新威脅保護與安全性解決方案。 

若要深入了解 ATA 與 Azure ATP 之間的差異，請參閱 [Azure ATP 常見問題集] (https://docs.microsoft.com/en-us/azure-advanced-threat-protection/atp-technical-faq#what-is-azure-atp) 。

在本指南中，您將會： 

> [!div class="checklist"]
> * 檢閱並確認 Azure ATP 服務必要條件
> * 記錄現有的 ATA 設定
> * 規劃移動
> * 安裝並設定 Azure ATP 服務
> * 執行移動後檢查和驗證
> * 在完成移動後解除 ATA 

>[!NOTE]
> 任何 ATA 版本都可以從 ATA 移至 Azure ATP。 不過，由於資料無法從 ATA 移至 Azure ATP，因此建議您要保留進行中調查所需的 ATA 中心資料與警示，直到所有的 ATA 警示皆已關閉或已補救為止。 

## <a name="prerequisites"></a>必要條件

- 至少需要含有一個全域管理員/安全性系統管理員的 Azure Active Directory 租用戶，才能建立 Azure ATP 執行個體。 每個 Azure ATP 執行個體都支援多 Active Directory 樹系邊界，以及 Windows 2003 和更新版本的樹系功能等級 (FFL)。

- Azure ATP 需要 .Net Framework 4.7，如果您目前的 .Net Framework 版本不是 4.7，則可能需要網域控制站 (重新啟動)。

- 請確定您的網域控制站符合所有 [Azure ATP 感應器需求](https://docs.microsoft.com/azure-advanced-threat-protection/atp-prerequisites#azure-atp-sensor-requirements)，且您的環境符合所有 [Azure ATP 需求](https://docs.microsoft.com/azure-advanced-threat-protection/atp-prerequisites)。

- 驗證您打算使用的所有網域控制站對 Azure ATP 服務都有足夠網際網路存取權。 請檢查並確認您的網域控制站符合 [Azure ATP Proxy 設定需求](https://docs.microsoft.com/azure-advanced-threat-protection/configure-proxy)。

>[!NOTE]
> 本移轉指南專為 Azure ATP 感應器而設計。 如需詳細資訊，請參閱[為您的部署選擇正確的感應器](https://docs.microsoft.com/azure-advanced-threat-protection/atp-capacity-planning#choosing-the-right-sensor-type-for-your-deployment)。 

## <a name="plan"></a>方案 

在開始移動之前，請務必先收集下列資訊： 
1. [目錄服務](https://docs.microsoft.com/azure-advanced-threat-protection/install-atp-step2)帳戶的帳戶詳細資料。
1. Syslog 通知[設定](https://docs.microsoft.com/azure-advanced-threat-protection/setting-syslog)。
1. 電子郵件[通知詳細資料](https://docs.microsoft.com/azure-advanced-threat-protection/notifications)。
1. ATA 角色群組成員資格
1. VPN 整合
1. 警示排除項目 
    - 排除項目不能從 ATA 轉移到 Azure ATP，因此需要有每一個排除項目的詳細資料，才能[複寫 Azure ATP 中的排除項目](https://docs.microsoft.com/azure-advanced-threat-protection/excluding-entities-from-detections)。
1. HoneyToken 帳戶的帳戶詳細資料。 
    - 如果您還沒有專用的 HoneyToken 帳戶，請深入了解 [Azure ATP 中的 HoneyToken](https://docs.microsoft.com/azure-advanced-threat-protection/install-atp-step7)，並建立用於此用途的新帳戶。
1. 您想要手動標記為敏感性實體的所有實體 (電腦、群組、使用者) 完整清單。 
    - 深入了解 Azure ATP 中[敏感性實體](https://docs.microsoft.com/azure-advanced-threat-protection/sensitive-accounts) 的重要性。
1. 報表排程[詳細資料](https://docs.microsoft.com/azure-advanced-threat-protection/reports) (報表和排程時間的清單)。 
1. 每個 ATA 輕量型閘道 (其為 Azure ATP 網域同步器候選項目) 的識別與詳細資料。 
   - 深入了解 Azure ATP 中[網域同步器候選項目](https://docs.microsoft.com/azure-advanced-threat-protection/install-atp-step5#configure-sensor-settings)的重要性。

> [!NOTE]
> 在移除所有 ATA 閘道之前，請不要解除安裝 ATA 中心。 在 ATA 閘道仍在執行中時解除安裝 ATA 中心，會使您的組織暴露在沒有任何威脅防護的情況下。

## <a name="move"></a>移動 

以兩個簡單步驟完成移至 Azure ATP 的作業：

### <a name="step-1-create-and-install-azure-atp-instance-and-sensors"></a>步驟 1：建立並安裝 Azure ATP 執行個體和感應器

1. [建立您的 Azure ATP 執行個體](https://docs.microsoft.com/azure-advanced-threat-protection/install-atp-step1)

2. 在所有網域控制站上解除安裝 ATA 輕量型閘道。  

3. 在所有網域控制站上安裝 Azure ATP 感應器：
     - [下載 Azure ATP 感應器檔案](https://docs.microsoft.com/azure-advanced-threat-protection/install-atp-step3)。
     - [擷取您的 Azure ATP 存取金鑰](https://docs.microsoft.com/azure-advanced-threat-protection/install-atp-step3#download-the-setup-package)。
     - [在您的網域控制站上安裝 Azure ATP 感應器](https://docs.microsoft.com/azure-advanced-threat-protection/install-atp-step4)。 

### <a name="step-2-configure-and-validate-azure-atp-instance"></a>步驟 2：設定並驗證 Azure ATP 執行個體  

- [設定感應器](https://docs.microsoft.com/azure-advanced-threat-protection/install-atp-step5)

>[!NOTE]
> 在安裝 Azure ATP 感應器然後完成初始同步處理之前，無法完成下列清單中的特定工作，例如選取實體以進行手動**敏感性**標記。 最多允許 2 小時來完成初始同步處理。 

#### <a name="configuration"></a>設定

登入 Azure ATP 入口網站並完成下列設定工作。

| 步驟    | 動作 | 狀態 |
|--------------|------------|------------------|
| 1  | 設定[選定網域控制站的延遲更新](https://docs.microsoft.com/azure-advanced-threat-protection/sensor-update) | - [ ] |
| 2  | [目錄服務](https://docs.microsoft.com/azure-advanced-threat-protection/install-atp-step2)帳戶詳細資料| - [ ] |
| 3  | 設定[網域同步器候選項目](https://docs.microsoft.com/azure-advanced-threat-protection/install-atp-step5#configure-sensor-settings) | - [ ] |
| 4  | 設定 [Syslog 通知](https://docs.microsoft.com/azure-advanced-threat-protection/setting-syslog) | - [ ] |
| 5  | [整合 VPN](https://docs.microsoft.com/azure-advanced-threat-protection/install-atp-step6-vpn) 資訊| - [ ] |
| 6  | 設定 [WDATP 整合](https://docs.microsoft.com/azure-advanced-threat-protection/integrate-wd-atp)| - [ ] |
| 7  | 設定 [HoneyToken](https://docs.microsoft.com/azure-advanced-threat-protection/install-atp-step7) 帳戶| - [ ] |
| 8  | 標記[敏感性實體](https://docs.microsoft.com/azure-advanced-threat-protection/sensitive-accounts)| - [ ] |
| 9  | 建立[安全性警示排除項目](https://docs.microsoft.com/azure-advanced-threat-protection/excluding-entities-from-detections)| - [ ] |
| 10 | [電子郵件通知切換](https://docs.microsoft.com/azure-advanced-threat-protection/notifications) | - [ ] |
| 11  | [排程報表設定](https://docs.microsoft.com/azure-advanced-threat-protection/reports) (報表和排程時間的清單)| - [ ] |
| 12  | 設定[角色型權限](https://docs.microsoft.com/azure-advanced-threat-protection/atp-role-groups) | - [ ] |
| 12  | [SIEM 通知設定 (IP 位址)](https://docs.microsoft.com/azure-advanced-threat-protection/configure-event-collection#siemsyslog)| - [ ] | 

#### <a name="validation"></a>驗證

在 Azure ATP 入口網站內：
- 檢閱任何[健全狀況警示](https://docs.microsoft.com/azure-advanced-threat-protection/atp-health-center)，以了解服務問題的徵兆。 
- 檢閱 Azure ATP [感應器錯誤記錄檔](https://docs.microsoft.com/azure-advanced-threat-protection/troubleshooting-atp-using-logs)是否有任何不尋常的錯誤。

## <a name="after-the-move"></a>移動之後

本指南的這一節會說明可以在完成移動後執行的動作。 

>[!NOTE]
> 不支援從 ATA 將現有的安全性警示匯入至 ATP。 請務必在解除 ATA 中心之前先記錄或補救所有現有的 ATA 警示。  

- **解除 ATA 中心** 
    - 為了在移動後參考 ATA 中心資料，建議您將中心資料保留在線上一段時間。 解除 ATA 中心之後，資源數目通常會縮減，特別是資源為虛擬機器時。  

- **備份 Mongo DB** 
    - 如果您想要無限期保留 ATA 資料，請[備份 Mongo DB](https://docs.microsoft.com/advanced-threat-analytics/ata-database-management#backing-up-the-ata-database)。  

## <a name="mission-accomplished"></a>任務完成

恭喜！ 您已完成從 ATA 移至 Azure ATP。 

## <a name="next-steps"></a>後續步驟

深入了解 [Azure ATP](https://docs.microsoft.com/azure-advanced-threat-protection/what-is-atp) 特色、功能及[安全性警示](https://docs.microsoft.com/azure-advanced-threat-protection/understanding-security-alerts)。  
## <a name="join-the-community"></a>加入社群

是否有更多問題，或是想與其他人討論 Azure ATP 及相關的安全性？ 現在就加入 [Azure ATP 社群](https://techcommunity.microsoft.com/t5/Azure-Advanced-Threat-Protection/bd-p/AzureAdvancedThreatProtection)！




