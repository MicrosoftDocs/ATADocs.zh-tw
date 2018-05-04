---
title: 設定 SAM-R 以在 Advanced Threat Analytics 中啟用橫向移動路徑偵測 | Microsoft Docs
description: 描述如何設定 SAM-R 以在 Advanced Threat Analytics (ATA) 中啟用橫向移動路徑偵測
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 4/25/2018
ms.topic: get-started-article
ms.prod: ''
ms.service: advanced-threat-analytics
ms.technology: ''
ms.assetid: 7597ed25-87f5-472c-a496-d5f205c9c391
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 6e32f3ce59b049d0ced68a1330eefca7315bf49d
ms.sourcegitcommit: 5c0f914b44bfb8e03485f12658bfa9a7cd3d8bbc
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/30/2018
---
*適用於：Advanced Threat Analytics 1.9 版*

# <a name="install-ata---step-9"></a>安裝 ATA - 步驟 9

>[!div class="step-by-step"]
[« 步驟 8](install-ata-step7.md)

## <a name="step-9-configure-sam-r-required-permissions"></a>步驟 9： 設定 SAM-R 所需的權限

[橫向移動路徑](use-case-lateral-movement-path.md)偵測有賴於識別特定電腦上本機系統管理員的查詢。 這些查詢會透過[步驟 2.連線到 AD](install-ata-step2.md) 中建立的 Azure ATP 服務帳戶，使用 SAM-R 通訊協定來執行。
 
若要確保 Windows 用戶端和伺服器允許 ATA 服務帳戶執行這項 SAM R 作業，您必須修改 [群組原則]，在 [網路存取] 原則列出的已設定帳戶之外新增 ATA 服務帳戶。

1. 找出原則：

 - 原則名稱：網路存取 - 限制允許對 SAM 發出遠端呼叫的用戶端
 - 位置：電腦設定、Windows 設定、安全性設定、本機原則、安全性選項
  
  ![找出原則](./media/samr-policy-location.png)

2. 將 ATA 服務新增至能夠在新式 Windows 系統上執行此動作的核准帳戶清單。
 
  ![新增服務](./media/samr-add-service.png)

3. **ATA 服務** (在安裝期間建立的 ATA 服務) 現在具備在環境中執行 SAMR 的適當權限。

如需有關 SAM-R 以及此群組原則的詳細資訊，請參閱[網路存取：限制允許對 SAM 發出遠端呼叫的用戶端](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/network-access-restrict-clients-allowed-to-make-remote-sam-calls) \(英文\)。


>[!div class="step-by-step"]
[« 步驟 8](install-ata-step7.md)

## <a name="see-also"></a>另請參閱
- [ATA POC 部署指南](http://aka.ms/atapoc)
- [ATA 調整大小工具](http://aka.ms/atasizingtool)
- [查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [設定事件收集](configure-event-collection.md)
- [ATA 必要條件](ata-prerequisites.md)
