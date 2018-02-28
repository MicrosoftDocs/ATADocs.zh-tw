---
title: "設定 SAM-R 以在 Azure ATP 中啟用橫向移動路徑偵測 | Microsoft Docs"
description: "描述如何設定 SAM-R 以在 Azure ATP 中啟用橫向移動路徑偵測"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2018
ms.topic: get-started-article
ms.prod: 
ms.service: azure-advanced-threat-protection
ms.technology: 
ms.assetid: b09adce3-0fbc-40e3-a53f-31f57fe79ca3
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 0e2ac4fb68fb1429610a0416582c871c9ae704df
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/21/2018
---
適用於：Azure 進階威脅防護

# <a name="install-azure-atp---step-8"></a>安裝 Azure ATP - 步驟 8

>[!div class="step-by-step"]
[« 步驟 7](install-atp-step7.md)

## <a name="step-8-configure-sam-r-required-permissions"></a>步驟 8： 設定 SAM-R 所需的權限

[橫向移動路徑](use-case-lateral-movement-path.md)偵測有賴於識別特定電腦上本機系統管理員的查詢。 這些查詢是透過[步驟 2.連線到 AD](install-atp-step2.md) 中建立的 Azure ATP 服務帳戶，使用 SAM-R 通訊協定來執行。
 
若要確保 Windows 用戶端和伺服器允許 Azure ATP 服務帳戶執行這項 SAM-R 作業，必須對群組原則進行修改。

1. 找出原則：

 - 原則名稱：網路存取 - 限制允許對 SAM 發出遠端呼叫的用戶端
 - 位置：電腦設定、Windows 設定、安全性設定、本機原則、安全性選項
  
  ![找出原則](./media/samr-policy-location.png)

2. 將 Azure ATP 服務新增至能夠在新式 Windows 系統上執行此動作的核准帳戶清單。
 
  ![新增服務](./media/samr-add-service.png)

3. **AATP 服務** (在安裝期間建立的 Azure ATP 服務) 現在具備在環境中執行 SAMR 的適當權限。

如需有關 SAM-R 以及此群組原則的詳細資訊，請參閱[網路存取：限制允許對 SAM 發出遠端呼叫的用戶端](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/network-access-restrict-clients-allowed-to-make-remote-sam-calls) \(英文\)。


>[!div class="step-by-step"]
[« 步驟 7](install-atp-step7.md)



## <a name="see-also"></a>另請參閱
- [使用 Azure ATP 調查橫向移動路徑攻擊](use-case-lateral-movement-path.md)
- [查看 ATP 論壇！](https://aka.ms/azureatpcommunity)\(英文\)