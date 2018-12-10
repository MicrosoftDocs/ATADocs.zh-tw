---
title: 設定 SAM-R 以在 Azure ATP 中啟用橫向移動路徑偵測 | Microsoft Docs
description: 說明如何設定 Azure ATP 對 SAM 發出遠端呼叫
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 12/02/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: b09adce3-0fbc-40e3-a53f-31f57fe79ca3
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 020517e576f93b79e00158bbb7c6553d722a73b1
ms.sourcegitcommit: f4f2a1b2c674c4dba7a46ece0624f5ea10c4865e
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/02/2018
ms.locfileid: "52744382"
---
適用於：Azure 進階威脅防護

# <a name="configure-azure-atp-to-make-remote-calls-to-sam"></a>設定 Azure ATP 對 SAM 發出遠端呼叫
Azure ATP [橫向移動路徑](use-case-lateral-movement-path.md)偵測有賴於識別特定電腦上本機系統管理員的查詢。 這些查詢是在 Azure ATP 安裝期間透過[步驟 2.連線到 AD](install-atp-step2.md) 中建立的 Azure ATP 服務帳戶，使用 SAM-R 通訊協定來執行。

## <a name="configure-sam-r-required-permissions"></a>設定 SAM-R 所需的權限
若要確保 Windows 用戶端和伺服器允許 Azure ATP 帳戶執行 SAM-R，您必須修改 [群組原則]，在 [網路存取] 原則列出的已設定帳戶之外新增 Azure ATP 服務帳戶。

1. 找出原則：

 - 原則名稱：網路存取 - 限制允許對 SAM 發出遠端呼叫的用戶端
 - 位置：電腦設定、Windows 設定、安全性設定、本機原則、安全性選項
  
  ![找出原則](./media/samr-policy-location.png)

2. 將 Azure ATP 服務新增至能夠在新式 Windows 系統上執行此動作的核准帳戶清單。
 
  ![新增服務](./media/samr-add-service.png)

3. **AATP 服務** (在安裝期間建立的 Azure ATP 服務) 現在具備在環境中執行 SAM-R 的適當權限。

> [!NOTE]
> 強制執行新原則之前，請確定您的環境仍然是安全的，不要透過在稽核模式中啟用及驗證您建議的變更而影響應用程式相容性。

如需有關 SAM-R 與此群組原則的詳細資訊，請參閱[網路存取：限制允許對 SAM 發出遠端呼叫的用戶端](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/network-access-restrict-clients-allowed-to-make-remote-sam-calls) \(機器翻譯\)。



## <a name="see-also"></a>另請參閱
- [使用 Azure ATP 調查橫向移動路徑攻擊](use-case-lateral-movement-path.md)
- [查看 Azure ATP 論壇！](https://aka.ms/azureatpcommunity)