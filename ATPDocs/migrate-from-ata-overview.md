---
title: 對 Microsoft Defender 進行身分識別移動的先進威脅分析
description: 瞭解如何將現有的 Advanced 威脅分析安裝移至 Microsoft Defender 以進行身分識別。
ms.date: 10/26/2020
ms.topic: how-to
ms.openlocfilehash: 45b9004bc439a28e144686e3147b94b6019a7a0f
ms.sourcegitcommit: a892419a5cb95412e4643c35a9a72092421628ec
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/16/2021
ms.locfileid: "100533795"
---
# <a name="advanced-threat-analytics-ata-to-microsoft-defender-for-identity"></a>適用于身分識別的 Advanced 威脅分析 (ATA) 至 Microsoft Defender

> [!NOTE]
> ATA 的最終發行版本已 [正式推出](https://support.microsoft.com/help/4568997/update-3-for-microsoft-advanced-threat-analytics-1-9)。 ATA 將于2021年1月12日結束主流支援。 延伸支援將繼續進行，直到2026年1月為止。 如需詳細資訊，請閱讀 [我們的 blog](https://techcommunity.microsoft.com/t5/microsoft-security-and/end-of-mainstream-support-for-advanced-threat-analytics-january/ba-p/1539181)。

您可以使用本指南，從現有的 ATA 安裝移至 ([!INCLUDE [Product long](includes/product-long.md)]) 服務。 本指南說明 [!INCLUDE [Product short](includes/product-short.md)] 必要條件和需求，並詳細說明如何規劃和完成您的移動。 [!INCLUDE [Product short](includes/product-short.md)]此外也包含在安裝之後，利用最新威脅防護和安全性解決方案的驗證步驟和秘訣。

若要深入瞭解 ATA 與之間的差異 [!INCLUDE [Product short](includes/product-short.md)] ，請參閱[ [!INCLUDE [Product short](includes/product-short.md)] 常見問題](technical-faq.yml)。

在本指南中，您將會：

> [!div class="checklist"]
>
> - 檢查並確認 [!INCLUDE [Product short](includes/product-short.md)] 服務必要條件
> - 記錄現有的 ATA 設定
> - 規劃移動
> - 安裝和設定您的 [!INCLUDE [Product short](includes/product-short.md)]  服務
> - 執行移動後檢查和驗證
> - 在完成移動後解除 ATA

> [!NOTE]
> 從 ATA 移至 [!INCLUDE [Product short](includes/product-short.md)] 時，可以從任何 ata 版本移至。 不過，因為資料無法從 ATA 移至 [!INCLUDE [Product short](includes/product-short.md)] ，建議您保留您的 Ata 中心資料和持續調查所需的警示，直到所有 ATA 警示都已關閉或補救為止。

## <a name="prerequisites"></a>必要條件

- 需要至少有一個全域/安全性系統管理員的 Azure Active Directory 租使用者，才能建立 [!INCLUDE [Product short](includes/product-short.md)] 實例。 每個 [!INCLUDE [Product short](includes/product-short.md)] 執行個體都支援多 Active Directory 樹系邊界，以及 Windows 2003 和更新版本的樹系功能等級 (FFL)。

- [!INCLUDE [Product short](includes/product-short.md)] 需要 .Net Framework 4.7 或更新版本，如果您目前的 .Net Framework 版本不是4.7 或更新版本，則可能需要網域控制站 (重新開機) 。

- 確定您的網域控制站符合所有[ [!INCLUDE [Product short](includes/product-short.md)] 感應器需求](prerequisites.md#azure-atp-sensor-requirements)，而且您的環境符合所有[ [!INCLUDE [Product short](includes/product-short.md)] 需求](prerequisites.md)。

- 驗證您打算使用的所有網域控制站都有足夠的網際網路存取 [!INCLUDE [Product short](includes/product-short.md)] 服務。 檢查並確認您的網域控制站符合[ [!INCLUDE [Product short](includes/product-short.md)] proxy 設定需求](configure-proxy.md)。

> [!NOTE]
> 這項遷移指南僅適用于 [!INCLUDE [Product short](includes/product-short.md)] 感應器。

## <a name="plan"></a>方案

在開始移動之前，請務必先收集下列資訊：

1. [目錄服務](install-step2.md)帳戶的帳戶詳細資料。
1. Syslog 通知[設定](setting-syslog.md)。
1. 電子郵件[通知詳細資料](notifications.md)。
1. ATA 角色群組成員資格
1. VPN 整合
1. 警示排除項目
    - 排除專案不能從 ATA 轉移到 [!INCLUDE [Product short](includes/product-short.md)] ，因此需要每個排除的詳細資料，才能複寫[ [!INCLUDE [Product short](includes/product-short.md)] 中的排除](excluding-entities-from-detections.md)專案。
1. HoneyToken 帳戶的帳戶詳細資料。
    - 如果您還沒有專屬的 HoneyToken 帳戶，請深入瞭解如何[在 [!INCLUDE [Product short](includes/product-short.md)] 中 honeytoken](install-step7.md) ，並建立要用於此用途的新帳戶。
1. 您想要手動標記為敏感性實體的所有實體 (電腦、群組、使用者) 完整清單。
    - 深入瞭解中 [敏感性實體](sensitive-accounts.md) 的重要性 [!INCLUDE [Product short](includes/product-short.md)] 。
1. 報表排程[詳細資料](reports.md) (報表和排程時間的清單)。

> [!NOTE]
> 在移除所有 ATA 閘道之前，請不要解除安裝 ATA 中心。 在 ATA 閘道仍在執行中時解除安裝 ATA 中心，會使您的組織暴露在沒有任何威脅防護的情況下。

## <a name="move"></a>移動

您可以 [!INCLUDE [Product short](includes/product-short.md)] 用兩個簡單的步驟完成移至：

### <a name="step-1-create-and-install-defender-for-identity-instance-and-sensors"></a>步驟1：針對身分識別實例和感應器建立和安裝 Defender

1. [建立新的 [!INCLUDE [Product short](includes/product-short.md)] 實例](install-step1.md)

1. 在所有網域控制站上解除安裝 ATA 輕量型閘道。

1. [!INCLUDE [Product short](includes/product-short.md)]在所有網域控制站上安裝感應器：
    - [下載 [!INCLUDE [Product short](includes/product-short.md)] 感應器](install-step3.md)檔案。
    - [取得您的 [!INCLUDE [Product short](includes/product-short.md)] 存取金鑰](install-step3.md#download-the-setup-package)。
    - [ [!INCLUDE [Product short](includes/product-short.md)] 在您的網域控制站上安裝感應器](install-step4.md)。

### <a name="step-2-configure-and-validate-defender-for-identity-instance"></a>步驟2：設定及驗證身分識別實例的 Defender

- [設定感應器](install-step5.md)

> [!NOTE]
> 在安裝 [!INCLUDE [Product short](includes/product-short.md)] 感應器然後完成初始同步處理（例如選取實體以進行手動 **敏感性** 標記）之前，無法完成下列清單中的特定工作。 最多允許 2 小時來完成初始同步處理。

#### <a name="configuration"></a>設定

登入 [!INCLUDE [Product short](includes/product-short.md)] 入口網站並完成下列設定工作。

| 步驟    | 動作 | 狀態 |
|--------------|------------|------------------|
| 1  | 設定[選定網域控制站的延遲更新](sensor-update.md) | - [ ] |
| 2  | [目錄服務](install-step2.md)帳戶詳細資料| - [ ] |
| 3  | 設定 [Syslog 通知](setting-syslog.md) | - [ ] |
| 4  | [整合 VPN](install-step6-vpn.md) 資訊| - [ ] |
| 5  | 設定 [WDATP 整合](integrate-mde.md)| - [ ] |
| 6  | 設定 [HoneyToken](install-step7.md) 帳戶| - [ ] |
| 7  | 標記[敏感性實體](sensitive-accounts.md)| - [ ] |
| 8  | 建立[安全性警示排除項目](excluding-entities-from-detections.md)| - [ ] |
| 9 | [電子郵件通知切換](notifications.md) | - [ ] |
| 10  | [排程報表設定](reports.md) (報表和排程時間的清單)| - [ ] |
| 11  | 設定[角色型權限](role-groups.md) | - [ ] |
| 12  | [SIEM 通知設定 (IP 位址)](configure-event-collection.md#siemsyslog)| - [ ] |

#### <a name="validation"></a>驗證

在 [!INCLUDE [Product short](includes/product-short.md)] 入口網站中：

- 檢閱任何[健全狀況警示](health-center.md)，以了解服務問題的徵兆。
- 檢查 [!INCLUDE [Product short](includes/product-short.md)] [感應器錯誤記錄](troubleshooting-using-logs.md) 檔中是否有任何異常錯誤。

## <a name="after-the-move"></a>移動之後

本指南的這一節會說明可以在完成移動後執行的動作。

> [!NOTE]
> 不支援將現有的安全性警示從 ATA 匯入至 [!INCLUDE [Product short](includes/product-short.md)] 。 請務必在解除 ATA 中心之前先記錄或補救所有現有的 ATA 警示。

- **解除 ATA 中心**  
  - 為了在移動後參考 ATA 中心資料，建議您將中心資料保留在線上一段時間。 解除 ATA 中心之後，資源數目通常會縮減，特別是資源為虛擬機器時。

- **備份 Mongo DB**  
  - 如果您想要無限期保留 ATA 資料，請[備份 Mongo DB](/advanced-threat-analytics/ata-database-management#backing-up-the-ata-database)。

## <a name="mission-accomplished"></a>任務完成

恭喜！ 您從 ATA 移至 [!INCLUDE [Product short](includes/product-short.md)] 的工作已完成。

## <a name="next-steps"></a>下一步

深入瞭解 [[!INCLUDE [Product short](includes/product-short.md)]](what-is.md) 功能、功能和 [安全性警示](understanding-security-alerts.md)。

## <a name="join-the-community"></a>加入社群

是否有更多問題或想與其他人討論[!INCLUDE [Product short](includes/product-short.md)] 與相關的安全性？ 立即加入[[!INCLUDE [Product short](includes/product-short.md)] 社群](https://techcommunity.microsoft.com/t5/Azure-Advanced-Threat-Protection/bd-p/AzureAdvancedThreatProtection) \(英文\)！
