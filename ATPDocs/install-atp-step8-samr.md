---
title: 設定 SAM-R 以在 Azure ATP 中啟用橫向移動路徑偵測
description: 說明如何設定 Azure ATP 對 SAM 發出遠端呼叫
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 05/16/2019
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: b09adce3-0fbc-40e3-a53f-31f57fe79ca3
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 8f9bd3877286e4b7230e9bb35d6f382fe3092e13
ms.sourcegitcommit: 2be59f0bd4c9fd0d3827e9312ba20aa8eb43c6b5
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/27/2020
ms.locfileid: "88956494"
---
# <a name="configure-azure-atp-to-make-remote-calls-to-sam"></a>設定 Azure ATP 對 SAM 發出遠端呼叫

Azure ATP [橫向移動路徑](use-case-lateral-movement-path.md)偵測有賴於識別特定電腦上本機系統管理員的查詢。 這些查詢是在 Azure ATP 安裝期間透過[步驟 2.連線到 AD](install-atp-step2.md) 中建立的 Azure ATP 服務帳戶，使用 SAM-R 通訊協定來執行。

## <a name="configure-sam-r-required-permissions"></a>設定 SAM-R 所需的權限

若要確保 Windows 用戶端和伺服器允許 Azure ATP 帳戶執行 SAM-R，您必須修改 [群組原則]，在 [網路存取] 原則列出的已設定帳戶之外新增 Azure ATP 服務帳戶。 請務必將群組原則套用至網域控制站以外的所有電腦。

> [!Note]
> 在施行此類新原則之前，請務必確認您環境的安全，以及任何變更都不會影響應用程式的相容性。 若要這麼做，請先予以啟用，然後以稽核模式驗證建議變更的相容性，再對您的實際執行環境做出變更。

1. 找出原則：

   - 原則名稱：網路存取 - 限制允許對 SAM 發出遠端呼叫的用戶端
   - 位置：電腦設定、Windows 設定、安全性設定、本機原則、安全性選項

    ![找出原則](media/samr-policy-location.png)

1. 將 Azure ATP 服務新增至能夠在新式 Windows 系統上執行此動作的核准帳戶清單。

    ![新增服務](media/samr-add-service.png)

3. **AATP 服務** (在安裝期間建立的 Azure ATP 服務) 現在具備在環境中執行 SAM-R 的適當權限。

如需 SAM-R 和此群組原則的詳細資訊，請參閱[網路存取：限制允許對 SAM 發出遠端呼叫的用戶端](/windows/security/threat-protection/security-policy-settings/network-access-restrict-clients-allowed-to-make-remote-sam-calls) \(部分為機器翻譯\)。

## <a name="see-also"></a>另請參閱

- [使用 Azure ATP 調查橫向移動路徑攻擊](use-case-lateral-movement-path.md)
- [查看 Azure ATP 論壇！](https://aka.ms/azureatpcommunity)