---
title: 設定 SAM-R 以在 Advanced Threat Analytics 中啟用橫向移動路徑偵測 | Microsoft Docs
description: 描述如何設定 SAM-R 以在 Advanced Threat Analytics (ATA) 中啟用橫向移動路徑偵測
keywords: ''
author: shsagir
ms.author: shsagir
manager: rkarlin
ms.date: 09/08/2019
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 7597ed25-87f5-472c-a496-d5f205c9c391
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 1b8e8924fe0cd00985252c04edfb92ec51759b48
ms.sourcegitcommit: 9673eb49729a06d3a25d52c0f43c76ac61b9cf89
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/12/2020
ms.locfileid: "75907975"
---
# <a name="install-ata---step-9"></a>安裝 ATA - 步驟 9

*適用於：Advanced Threat Analytics 1.9 版*

> [!div class="step-by-step"]
> [« 步驟 8](install-ata-step7.md)

> [!NOTE]
> 強制執行任何新原則之前，請務必先確定您的環境是安全的，而不會影響應用程式相容性，方法是先啟用並確認您在 audit 模式中的建議變更。 

## <a name="step-9-configure-sam-r-required-permissions"></a>步驟 9： 設定 SAM-R 所需的權限

[橫向移動路徑](use-case-lateral-movement-path.md)偵測有賴於識別特定電腦上本機系統管理員的查詢。 這些查詢是透過在步驟2中建立的 ATA 服務帳戶，使用 SAM-R 通訊協定來執行[。連接到 AD](install-ata-step2.md)。
 
若要確保 Windows 用戶端和伺服器允許 ATA 服務帳戶執行這項 SAM R 作業，您必須修改 [群組原則]，在 [網路存取] 原則列出的已設定帳戶之外新增 ATA 服務帳戶。 此群組原則應套用至您組織中的每個裝置。 

1. 找出原則：

   - 原則名稱：網路存取 - 限制允許對 SAM 發出遠端呼叫的用戶端
   - 位置：電腦設定、Windows 設定、安全性設定、本機原則、安全性選項
  
   ![找出原則](./media/samr-policy-location.png)

2. 將 ATA 服務新增至能夠在新式 Windows 系統上執行此動作的核准帳戶清單。
 
   ![新增服務](./media/samr-add-service.png)

3. **ATA 服務** (在安裝期間建立的 ATA 服務) 現在具備在環境中執行 SAM-R 的適當權限。

 如需有關 SAM-R 與群組原則的詳細資訊，請參閱[網路存取：限制允許對 SAM 發出遠端呼叫的用戶端](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/network-access-restrict-clients-allowed-to-make-remote-sam-calls) \(機器翻譯\)。


> [!div class="step-by-step"]
> [« 步驟 8](install-ata-step7.md)

## <a name="see-also"></a>另請參閱
- [ATA POC 部署指南](https://aka.ms/atapoc)
- [ATA 調整大小工具](https://aka.ms/atasizingtool)
- [查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [設定事件收集](configure-event-collection.md)
- [ATA 必要條件](ata-prerequisites.md)
