---
title: ATA 1.9 版的新功能 | Microsoft Docs
description: 列出 ATA 1.9 版的新功能以及已知問題
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/25/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: 51de491c-49ba-4aff-aded-cc133a8ccf0b
ms.reviewer: ''
ms.suite: ems
ms.openlocfilehash: 423f79ffc29af84fcb45a7103a07b1ef0ee0c546
ms.sourcegitcommit: 959b1f7753b9a8ad94870d2014376d55296fbbd4
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/18/2018
ms.locfileid: "46133356"
---
# <a name="whats-new-in-ata-version-19"></a>ATA 1.9 版的新功能

[從下載中心下載](https://www.microsoft.com/download/details.aspx?id=56725) \(英文\) 最新的 ATA 更新版本，或者從[評估中心](http://www.microsoft.com/evalcenter/evaluate-microsoft-advanced-threat-analytics)下載完整版本。

這些版本資訊提供此版 Advanced Threat Analytics 中更新、新功能、Bug 修正和已知問題的相關資訊。

## <a name="new--updated-detections"></a>新的和更新的偵測項目

-  **可疑的服務建立**：攻擊者嘗試在您的網路上執行可疑的服務。 當 ATA 偵測到某人在網域控制站上執行看似可疑的新服務時，現在會發出警示。 此偵測會根據事件而定 (而非網路流量)，如需詳細資訊，請參閱[可疑活動指南](suspicious-activity-guide.md#suspicious-service-creation)。


## <a name="new-reports-to-help-you-investigate"></a>可協助您調查的新報表 

-   [**以純文字公開的密碼**](reports.md)可讓您偵測到敏感性與非敏感性帳戶以純文字傳送帳戶認證。 這可讓您調查並解決在環境中使用 LDAP 簡單繫結的狀況，並改善您的網路安全性等級。 此報表會取代服務與敏感性帳戶純文字可疑活動警示。

- [**敏感性帳戶的橫向移動路徑**](reports.md)會列出透過橫向移動路徑公開的敏感性帳戶。 這可讓您減輕這些路徑的危險並強化您的網路，將攻擊面的風險降至最低。 這可讓您防止橫向移動，讓攻擊者無法在您的網路中於使用者和電腦之間移動，尋找虛擬安全性大獎：您的機密管理員帳戶認證。

## <a name="improved-investigation"></a>改善的調查

-  ATA 1.9 包含新增且改善的[實體設定檔](entity-profiles.md)。 實體設定檔提供您專為完整深入調查使用者、其所存取的資源以及其歷程記錄所設計的儀表板。 實體設定檔也能讓您識別可透過橫向移動路徑加以存取的敏感性使用者。 

-   ATA 1.9 可讓您[手動標記群組](tag-sensitive-accounts.md)或帳戶為敏感性，以增強偵測。 進行標記會影響許多 ATA 偵測，例如敏感性群組修改偵測與橫向移動路徑，這將取決於那些群組與帳戶視為具敏感性而定。

## <a name="performance-improvements"></a>效能改善

- ATA 中心基礎結構已改進效能：流量的彙總檢視可將 CPU 和封包管線最佳化，並重複使用網域控制站的通訊端，進而減少 DC 的 SSL 工作階段。



## <a name="additional-changes"></a>其他變更

- 安裝新版本的 ATA 後，[**最新消息**](working-with-ata-console.md)視窗會出現在右上角，讓您知道最新版本中新增了哪些功能。 該視窗也會為您提供詳細版本變更記錄的連結。


## <a name="removed-and-deprecated-features"></a>已移除和已淘汰的功能

- 移除**信任中斷可疑活動**警示。
- 移除以純文字公開密碼可疑活動。 其已由[**以純文字公開密碼報表**](reports.md)取代。



## <a name="see-also"></a>另請參閱
[查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/home?forum=mata)

[將 ATA 更新至 1.9 版 - 移轉指南](ata-update-1.9-migration-guide.md)

