---
title: 在適用於身分識別的 Microsoft Defender 中設定 Windows 事件收集
description: 在安裝適用於身分識別的 Microsoft Defender 的這個步驟中，您要設定 Windows 事件收集。
ms.date: 03/11/2021
ms.topic: how-to
ms.openlocfilehash: 20bb551928c01ce95bbf9186c1567d6bb5f1d0de
ms.sourcegitcommit: 439e9ad383f54ef31ff8ef6dd1ae4e177c3c31f4
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/14/2021
ms.locfileid: "103465330"
---
# <a name="configure-windows-event-collection"></a>設定 Windows 事件集合

[!INCLUDE [Product long](includes/product-long.md)] 偵測仰賴特定的 Windows 事件記錄項目來增強某些偵測，並提供額外資訊，包括特定動作的執行者 (例如 NTLM 登入)、安全性群組的修改內容與類似事件。 若要正確稽核事件並將其包含在 Windows 事件記錄檔中，則網域控制站需要正確的進階稽核原則設定。 不正確的進階稽核原則設定可能會造成所需的事件未記錄於事件記錄檔中，並導致[!INCLUDE [Product short](includes/product-short.md)] 涵蓋範圍不完整。

為了增強威脅偵測功能，[!INCLUDE [Product short](includes/product-short.md)] 會要求[!INCLUDE [Product short](includes/product-short.md)] [設定](#configure-audit-policies)及[收集](#configure-event-collection)下列 Windows 事件：

**Active Directory Federation Services (AD FS) 事件**

- 1202 -「同盟服務」已驗證新的認證
- 1203 -「同盟服務」無法驗證新的認證
- 4624 - 帳戶成功登入
- 4625 - 帳戶無法登入

**針對其他事件**

- 4726 - 使用者帳戶已刪除
- 4728 - 成員已新增至全域安全性群組
- 4729 - 成員已自全域安全性群組移除
- 4730 - 全域安全性群組已刪除
- 4732 - 成員已新增至本機安全性群組
- 4733 - 成員已從本機安全性群組移除
- 4741-已新增電腦帳戶
- 4743 - 電腦帳戶已刪除
- 4753 - 全域通訊群組已刪除
- 4756 - 成員已新增至萬用安全性群組
- 4757 - 成員已自萬用安全性群組移除
- 4758 - 萬用安全性群組已刪除
- 4763 - 萬用通訊群組已刪除
- 4776 - 網域控制站嘗試驗證帳戶的認證 (NTLM)
- 7045 - 新服務已安裝
- 8004 - NTLM 驗證

## <a name="configure-audit-policies"></a>設定稽核原則

請使用下列指示修改網域控制站的進階稽核原則：

1. 以 [網域系統管理員] 身分登入伺服器。
1. 從 [伺服器管理員] > [工具] > [群組原則管理] 載入 [群組原則管理編輯器]。
1. 展開 [網域控制站組織單位]，以滑鼠右鍵按一下 [預設網域控制站原則]，然後選取 [編輯]。

    > [!NOTE]
    > 您可以使用預設網域控制站原則或專用的 GPO 來設定這些原則。

    ![編輯網域控制站原則](media/advanced-audit-policy-check-step-1.png)

1. 從開啟的視窗前往 [電腦設定] > [原則] > [Windows 設定] > [安全性設定]，然後根據您想要啟用的原則，執行下列動作：

    **針對進階稽核原則設定**

    1. 請前往 [進階稽核原則設定] > [稽核原則]。
        ![進階稽核原則組態](media/advanced-audit-policy-check-step-2.png)
    1. 在 [稽核原則] 下編輯下列每個原則，然後針對 [設定下列稽核事件] 選取 [成功] 與 [失敗] 事件。

        | 稽核原則 | 子類別 | 觸發事件識別碼 |
        | --- |---|---|
        | 帳戶登入 | 稽核認證驗證 | 4776 |
        | 帳戶管理 | 稽核電腦帳戶管理 | 4741、4743 |
        | 帳戶管理 | 稽核通訊群組管理 | 4753、4763 |
        | 帳戶管理 | 稽核安全性群組管理 | 4728、4729、4730、4732、4733、4756、4757、4758 |
        | 帳戶管理 | 稽核使用者帳戶管理 | 4726 |
        | 系統 | 稽核安全性系統延伸 | 7045 |

        例如，若要設定 [稽核安全性群組管理]，請在 [帳戶管理] 下，按兩下 [稽核安全性群組管理]，然後針對 [設定下列稽核事件] 選取 [成功] 與 [失敗] 事件。

        ![稽核安全性群組管理](media/advanced-audit-policy-check-step-4.png)

    <a name="ntlm-authentication-using-windows-event-8004"></a> **針對本機原則 (事件識別碼：8004)**

    > [!NOTE]
    >
    > - 要 收集 Windows 事件 8004 的網域群組原則應該 **只** 套用到網域控制站。
    > - 當 Windows 事件 8004 由[!INCLUDE [Product short](includes/product-short.md)] 感應器剖析時，會使用伺服器存取的資料加強[!INCLUDE [Product short](includes/product-short.md)] NTLM 驗證活動。

    1. 前往 [本機原則] > [安全性選項]。
    1. 在 [安全性選項] 下設定指定的安全性原則，如下所示

        | 安全性原則設定 | 值 |
        |---|---|
        | 網路安全性: 限制 NTLM: 送往遠端伺服器的連出 NTLM 流量 | 全部稽核 |
        | 網路安全性: 限制 NTLM: 稽核這個網域的 NTLM 驗證 | 全部啟用 |
        | 網路安全性:限制 NTLM:稽核連入 NTLM 流量 | 為所有帳戶啟用稽核 |

        例如，若要設定 [送往遠端伺服器的連出 NTLM 流量]，請在 [安全性選項] 下，按兩下 [網路安全性:限制 NTLM:送往遠端伺服器的連出 NTLM 流量]，然後選取 [全部稽核]。

        ![稽核送往遠端伺服器的連出 NTLM 流量](media/advanced-audit-policy-check-step-3.png)

    > [!NOTE]
    > 如果您選擇使用本機安全性原則，而不是使用群組原則，請務必在本機原則中新增 [帳戶登入]、[帳戶管理] 及 [安全性選項] 稽核記錄。 如果您要設定進階稽核原則，請務必強制執行[稽核原則子類別](/windows/security/threat-protection/security-policy-settings/audit-force-audit-policy-subcategory-settings-to-override)。

1. 在套用 GPO 後，新的事件會顯示在您的 **Windows 事件記錄檔** 下。

<!--
## Defender for Identity Advanced Audit Policy check

To make it easier to verify the current status of each of your domain controller's Advanced Audit Policies, [!INCLUDE [Product short](includes/product-short.md)] automatically checks your existing Advanced Audit Policies and issues health alerts for policy settings that require modification. Each health alert provides specific details of the domain controller, the problematic policy as well as remediation suggestions.

![Advanced Audit Policy Health Alert](media/health-alert-audit.png)

Advanced Security Audit Policy is enabled via **Default Domain Controllers Policy** GPO. These audit events are recorded on the domain controller's Windows Events.
-->

## <a name="configure-event-collection"></a>設定事件收集

這些事件可由[!INCLUDE [Product short](includes/product-short.md)] 感應器自動收集，如果未部署[!INCLUDE [Product short](includes/product-short.md)] 感應器，則可使用下列其中一種方式，將事件轉送至[!INCLUDE [Product short](includes/product-short.md)] 獨立感應器：

- [設定[!INCLUDE [Product short](includes/product-short.md)] 獨立感應器](configure-event-forwarding.md)以接聽 SIEM 事件
- [設定 Windows 事件轉寄](configure-event-forwarding.md)

> [!NOTE]
>
> - [!INCLUDE [Product short](includes/product-short.md)] 獨立感應器不支援可提供多種偵測的資料 Windows 事件追蹤 (ETW) 記錄項目。 若要完整涵蓋您的環境，建議您部署[!INCLUDE [Product short](includes/product-short.md)] 感應器。
> - 在設定事件收集之前，請務必檢閱並驗證您的[稽核原則]()，以確保網域控制站已正確設定為可記錄必要的事件。

## <a name="see-also"></a>另請參閱

- [[!INCLUDE [Product short](includes/product-short.md)] 大小調整工具](https://aka.ms/aatpsizingtool)
- [[!INCLUDE [Product short](includes/product-short.md)] 先決條件](prerequisites.md)
- [[!INCLUDE [Product short](includes/product-short.md)] SIEM 記錄參考](cef-format-sa.md)
- [設定 Windows 事件轉送](configure-event-forwarding.md)
- [查看[!INCLUDE [Product short](includes/product-short.md)] 論壇！](https://aka.ms/MDIcommunity)\(英文\)
