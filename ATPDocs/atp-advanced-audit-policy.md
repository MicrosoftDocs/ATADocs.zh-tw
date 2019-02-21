---
title: Azure 進階威脅防護進階稽核原則檢查 | Microsoft Docs
description: 本文提供 Azure ATP 進階稽核原則檢查的概觀。
keywords: ''
author: mlottner
ms.author: mlottner
manager: barbkess
ms.date: 1/24/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: ab1e8dd9-a6c2-4c68-89d5-343b8ec56142
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 7e296690485cfec05db560019496fe09b3a685a6
ms.sourcegitcommit: c48db18274edb2284e281960c6262d97f96e01d2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/14/2019
ms.locfileid: "56263743"
---
# <a name="azure-atp-advanced-audit-policy-check"></a>Azure ATP 進階稽核原則檢查

Azure ATP 偵測憑藉特定 Windows 事件記錄檔來取得特定案例的可見度，例如 NTLM 登入、安全性群組修改及類似事件。 若要正確稽核事件並將其包含在 Windows 事件記錄檔中，則網域控制站需要正確的進階稽核原則設定。 不正確的進階稽核原則設定會讓記錄檔遺漏重要事件，並導致 Azure ATP 涵蓋範圍不完整。

為讓您更輕鬆地確認每個網域控制站進階稽核原則目前的狀態，Azure ATP 會自動檢查現有的進階稽核原則，並針對需要修改的原則設定發出健全狀況警示。 每個健全狀況警示各會提供網域控制站、問題原則及補救建議的具體詳細資料。

![進階稽核原則健全狀況警示](media/atp-health-alert-audit-policy.png)


您可透過 [預設網域控制站原則] GPO 來啟用進階安全性稽核原則。 這些稽核事件會記錄在網域控制站的 Windows 事件上。 

## <a name="modify-audit-policies"></a>修改稽核原則 

請使用下列指示修改網域控制站的進階稽核原則：

1. 以 [網域系統管理員] 身分登入伺服器。
2. 從 [伺服器管理員] > [工具] > [群組原則管理] 載入 [群組原則管理編輯器]。 
3. 展開 [網域控制站組織單位]，以滑鼠右鍵按一下 [預設網域控制站原則]，然後選取 [編輯]。 

    ![編輯網域控制站原則](media/atp-advanced-audit-policy-check-step-1.png)

4. 從開啟的視窗前往 [電腦設定] > [原則] > [Windows 設定] > [安全性設定] > [進階稽核原則設定]。

    ![進階稽核原則設定](media/atp-advanced-audit-policy-check-step-2.png)

5. 前往 [帳戶登入]，按兩下 [稽核認證驗證]，然後為 [設定下列稽核事件] 同時選取成功和失敗事件。 

    ![認證驗證](media/atp-advanced-audit-policy-check-step-3.png)

6. 前往 [帳戶管理]，按兩下 [稽核安全性群組管理]，然後針對成功和失敗事件均選取 [設定下列稽核事件]。

    ![稽核安全性群組管理](media/atp-advanced-audit-policy-check-step-4.png)

    > [!NOTE]
    > 如果您選擇使用本機原則，請務必在本機原則中新增 [帳戶登入] 與 [帳戶管理] 稽核記錄。 如果您要設定進階稽核原則，請務必強制執行[稽核原則子類別](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/audit-force-audit-policy-subcategory-settings-to-override)。

7. 在套用 GPO 後，新的事件會顯示在您的 **Windows 事件記錄檔**下。

## <a name="see-also"></a>另請參閱
- [Azure ATP 必要條件](atp-prerequisites.md)
- [設定事件收集](configure-event-collection.md)
- [設定 Windows 事件轉送](configure-event-forwarding.md)
- [查看 Azure ATP 論壇！](https://aka.ms/azureatpcommunity)
