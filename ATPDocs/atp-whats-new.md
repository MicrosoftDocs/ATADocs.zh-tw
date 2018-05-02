---
title: Azure ATP 的新功能 | Microsoft Docs
description: 描述 Azure ATP 最新版本並提供各版本新功能的詳細資訊。
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 4/22/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 7d0f33db-2513-4146-a395-290e001f4199
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: edf9222f7ccaca33317120a7cdaacf04873a67a4
ms.sourcegitcommit: d2d2750bfb0198c8488d538f1773fda6eda5e6f9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/23/2018
---
適用於：Azure 進階威脅防護


# <a name="whats-new-in-azure-atp"></a>Azure ATP 的新功能 



## <a name="azure-atp-release-229"></a>Azure ATP 2.29 版

發行日期：2018 年 4 月 22 日
 
- 此版本包含針對多個問題的修正和改善。 
 
 
## <a name="azure-atp-release-228"></a>Azure ATP 2.28 版

發行日期：2018 年 4 月 15 日
 
-   使用者若是角色群組 Azure ATP 使用者和 Azure ATP 檢視者的成員，現在就有權限可查看監視警示。
- 此版本包含針對多個問題的修正和改善。 


## <a name="azure-atp-release-227"></a>Azure ATP 2.27 版

發行日期：2018 年 4 月 8 日

- 您現在可以從上方導覽列提供使用者意見反應。 按一下功能表列中的笑臉，可讓您透過電子郵件，向 Azure Advanced Threat Protection 小組傳送您的意見反應。

- 此版本包含針對多個問題的修正和改善。 
 

## <a name="azure-atp-release-226"></a>Azure ATP 2.26 版

發行日期：2018 年 3 月 25 日

- 當 Azure ATP 因為偵測到可疑活動向您提供警示，但您將它視為良性積極 (非屬可疑活動的合法動作) 時，您可以選擇將該電腦與 IP 位址排除而不再予以偵測，包括：加密降級、LDAP 暴力密碼破解攻擊、偽造的 PAC、暴力密碼破解攻擊與傳遞雜湊 (Pass-the-hash)。
-   Azure ATP 感應器效能已改進。
-   已針對工作區部署新增一個區域，您現在可以在亞洲部署工作區。 


## <a name="azure-atp-release-225"></a>Azure ATP 2.25 版

發行日期：2018 年 3 月 18 日

- Azure ATP 現已支援多重要素驗證 (MFA)。 使用 MFA 的租用戶現在能夠進入 Azure ATP 入口網站。
- Azure ATP 現在具有[**系統狀態**](https://health.atp.azure.com/)頁面，可讓您了解工作區管理入口網站是否正常運作、是否偵測到任何問題、感應器是否可將流量傳送至雲端。 您可從 Azure ATP 的功能表列存取 [系統狀態]。


## <a name="azure-atp-release-224"></a>Azure ATP 2.24 版

發行日期：2018 年 3 月 11 日

**新的和更新的偵測項目**
  - 可疑服務的建立作業 – 攻擊者嘗試在您的網路上執行可疑的服務。 Azure ATP 發現特定電腦上有人正在執行可疑的新服務時，會產生警示。 這項偵測是以事件為基礎 (不是網路流量)，偵測位置是您網路中將事件 7045 轉寄至 Azure ATP 的任何網域控制站。 如需詳細資訊，請參閱[可疑活動指南](suspicious-activity-guide.md)。

**改良的調查**
  - Azure ATP 包含豐富的[實體設定檔](entity-profiles.md)。 實體設定檔為您提供專為深入調查使用者活動所設計的平台。這包括他們存取的資源、登入的電腦及其他更多。 實體設定檔也提供目錄資料，讓您識別往來實體的潛在橫向移動路徑，讓您深入了解您組織中的潛在漏洞。

  - ATP 可讓您將實體手動標記為*機密*，以加強偵測和監視。 這項標記會影響很多 Azure ATP 偵測，例如機密群組修改偵測和[橫向移動路徑](use-case-lateral-movement-path.md)，這些都仰賴於視為機密的實體。

**可協助您調查的新報表**
  - [在純文字格式報表中公開的密碼](reports.md)可讓您偵測服務傳送的帳戶認證何時會以純文字傳送。 這可讓您調查服務，並改善您的網路安全性層級。 此報表會取代純文字的可疑活動警示。
  - [機密帳戶報表的橫向移動路徑](reports.md)會列出透過橫向移動路徑公開的機密帳戶。 這可讓您減輕這些路徑的危險並強化您的網路，將攻擊面的風險降至最低。 這可讓您防止橫向移動，讓攻擊者無法在您的網路中於使用者和電腦之間移動，尋找虛擬安全性大獎：您的機密管理員帳戶認證。

- 您現在可以從可疑活動警示所提供的連結內輕鬆存取文件，以檢視[您可採取的調查步驟](suspicious-activity-guide.md)。 

**效能改善**
 -  Azure ATP 感應器基礎結構已改進效能：流量的彙總檢視可最佳化 CPU 和封包管線，並重複使用網域控制站的通訊端，將 SSL 工作階段減少至 DC。

## <a name="see-also"></a>另請參閱
- [Azure ATP 必要條件](atp-prerequisites.md)
- [Azure ATP 容量規劃](atp-capacity-planning.md)
- [設定事件收集](configure-event-collection.md)
- [設定 Windows 事件轉送](configure-event-forwarding.md#configuring-windows-event-forwarding)
- [查看 ATP 論壇！](https://aka.ms/azureatpcommunity)\(英文\)