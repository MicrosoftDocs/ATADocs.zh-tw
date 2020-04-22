---
title: 設定 SAM-R 以在 Azure ATP 中啟用橫向移動路徑偵測
description: 說明如何設定 Azure ATP 對 SAM 發出遠端呼叫
keywords: ''
author: shsagir
ms.author: shsagir
manager: rkarlin
ms.date: 05/16/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: b09adce3-0fbc-40e3-a53f-31f57fe79ca3
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: ddfc7b738ddf31be12ae1357b2024df1bc468251
ms.sourcegitcommit: 63be53de5b84eabdeb8c006438dab45bd35a4ab7
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/21/2020
ms.locfileid: "79413633"
---
# <a name="configure-azure-atp-to-make-remote-calls-to-sam"></a>設定 Azure ATP 對 SAM 發出遠端呼叫
Azure ATP [橫向移動路徑](use-case-lateral-movement-path.md)偵測有賴於識別特定電腦上本機系統管理員的查詢。 這些查詢是在 Azure ATP 安裝期間透過[步驟 2.連線到 AD](install-atp-step2.md) 中建立的 Azure ATP 服務帳戶，使用 SAM-R 通訊協定來執行。

## <a name="configure-sam-r-required-permissions"></a>設定 SAM-R 所需的權限
若要確保 Windows 用戶端和伺服器允許 Azure ATP 帳戶執行 SAM-R，您必須修改 [群組原則]  ，在 [網路存取]  原則列出的已設定帳戶之外新增 Azure ATP 服務帳戶。 務必將群組原則套用到所有電腦。 

> [!Note]
> 在施行此類新原則之前，請務必確認您環境的安全，以及任何變更都不會影響應用程式的相容性。 如果要這麼做，請先予以啟用，然後以稽核模式驗證所提出變更的相容性，再對您的生產環境進行變更。

1. 找出原則：

   - 原則名稱：網路存取 - 限制允許對 SAM 發出遠端呼叫的用戶端
   - 位置：電腦設定、Windows 設定、安全性設定、本機原則、安全性選項
  
   ![找出原則](./media/samr-policy-location.png)

2. 將 Azure ATP 服務新增至能夠在新式 Windows 系統上執行此動作的核准帳戶清單。
 
   ![新增服務](./media/samr-add-service.png)

3. **AATP 服務** (在安裝期間建立的 Azure ATP 服務) 現在具備在環境中執行 SAM-R 的適當權限。



如需 SAM-R 和此群組原則的詳細資訊，請參閱[網路存取：限制允許對 SAM 發出遠端呼叫的用戶端](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/network-access-restrict-clients-allowed-to-make-remote-sam-calls) \(部分為機器翻譯\)。



## <a name="see-also"></a>另請參閱
- [使用 Azure ATP 調查橫向移動路徑攻擊](use-case-lateral-movement-path.md)
- [查看 Azure ATP 論壇！](https://aka.ms/azureatpcommunity)
