---
title: Azure ATP 的新功能 | Microsoft Docs
description: 描述 Azure ATP 最新版本並提供各版本新功能的詳細資訊。
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 7/15/2018
ms.topic: article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 7d0f33db-2513-4146-a395-290e001f4199
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 9e28c18f118f7a2dc9d516cf62a113245a7be1fa
ms.sourcegitcommit: a9b8bc26d3cb5645f21a68dc192b4acef8f54895
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 07/16/2018
ms.locfileid: "39064078"
---
適用於：Azure 進階威脅防護


# <a name="whats-new-in-azure-atp"></a>Azure ATP 的新功能 

## <a name="azure-atp-release-240"></a>Azure ATP 2.40 版

發行日期：2018 年 7 月 15 日

- 傳遞票證偵測現在會在 [警示詳細資料] 頁面中包含辨識項區段。 如此可提供額外的資訊以調查警示。

- 使用者存取控制旗標 (位在使用者設定檔中的 [目錄] 資料下) 現已包含圖例，讓您可以更清楚了解開啟和關閉的屬性有哪些。  

## <a name="azure-atp-release-239"></a>Azure ATP 2.39 版

發行日期：2018 年 7 月 5 日
-   **加入新的偵測：Kerberos 黃金票證 - 不存在的帳戶** (預覽)<br>這個新偵測所能防禦針對網域中不存在帳戶所建立黃金票證的攻擊，因此得以協助保護您的組織。 如需詳細資訊，請參閱 [Azure 進階威脅防護可疑活動指南](suspicious-activity-guide.md#golden-ticket)

- 此版本包含針對多個問題的修正和改善。 


## <a name="azure-atp-release-238"></a>Azure ATP 2.38 版

發行日期：2018 年 7 月 1 日

- 此版本包含多個問題的修正與改善，並且加強了 Azure ATP 入口網站。 

## <a name="azure-atp-release-237"></a>Azure ATP 2.37 版

發行日期：2018 年 6 月 24 日

- 此版本包含針對多個問題的修正和改善。 

## <a name="azure-atp-release-236"></a>Azure ATP 2.36 版

發行日期：2018 年 6 月 17 日

- 此版本包含針對多個問題的修正和改善。 


## <a name="azure-atp-release-235"></a>Azure ATP 2.35 版

發行日期：2018 年 6 月 10 日
 
- **新預覽偵測**<br></br>從現在起，Azure ATP 將利用它是雲端服務的事實 (即以更快的週期提供新功能)，並盡快提供新偵測。 這些新偵測在第一次發行時會標示為「預覽」。 新偵測通常會在數週內從預覽移至正式運作。 您預設會看到預覽偵測。 如需退出的資訊，請參閱[預覽偵測](working-with-suspicious-activities.md#preview-detections)。
 
- **可疑 VPN 偵測**<br></br>此版本介紹可疑 VPN 偵測的預覽版本。 Azure ATP 會學習使用者 VPN 行為 (包括使用者登入的電腦以及使用者從中連線的位置)，並在與預期行為有所偏差時對您發出警示。 如需詳細資訊，請參閱[可疑 VPN 偵測](suspicious-activity-guide.md#suspicious-vpn-detection)。

- [Delayed update] \(延遲更新\)<br></br>每次 Azure ATP 更新時，您現在都可以選擇設定 Azure ATP 感應器稍後更新。 您現在可以將每個 Azure ATP 感應器設定為 [Delayed update] \(延遲更新\)，以在 Azure ATP 雲端服務更新後的 24 小時更新。 此功能可讓您在特定測試感應器上測試更新，而且只有在稍後才會更新生產感應器。 如果您在第一個更新週期期間發現問題，請開啟支援票證。 如需詳細資訊，請參閱[更新 Azure ATP 感應器](sensor-update.md)。

- **更新異常通訊協定實作偵測**<br></br>異常通訊協定實作偵測現在會提供相關資訊。 您現在可以看到 Azure ATP 懷疑哪個潛在攻擊工具在您的網路上工作。 如需詳細資訊，請參閱[可疑活動指南](suspicious-activity-guide.md)。
 
- **過期感應器警示**<br></br>Azure ATP 包括新監視警示，讓您知道感應器是否過期超過三個版本。 如果您看到此警示，則應該更新感應器，或調查為什麼未自動更新感應器。 如果警示再次發生，則請解除安裝並重新安裝感應器。

- 此版本包含針對多個問題的修正和改善。 

## <a name="azure-atp-release-234"></a>Azure ATP 2.34 版

發行日期：2018 年 6 月 3 日
 
- 此版本包含針對多個問題的修正和改善。 

 
## <a name="azure-atp-release-233"></a>Azure ATP 2.33 版

發行日期：2018 年 5 月 27 日

- 預覽功能：Azure ATP 現在支援新語言以及 13 個新地區設定：
    - 捷克文
    - 匈牙利文
    - 義大利文
    - 韓文
    - 荷蘭文
    - 波蘭文
    - 葡萄牙文 (巴西)
    - 葡萄牙文 (葡萄牙)
    - 俄羅斯
    - 瑞典文
    - 土耳其文
    - 簡體中文
    - 中文 (台灣)



## <a name="azure-atp-release-232"></a>Azure ATP 2.32 版

發行日期：2018 年 5 月 13 日
 
- 此版本包含針對多個問題的修正和改善。 

## <a name="azure-atp-release-231"></a>Azure ATP 2.31 版

2018 年 5 月 6 日發行
 
- 已對名稱解析進行改善。 在這項作業中，除了 RPC 與 NetBIOS 動態解析外，感應器可能會發出 TLS Client Hello 封包至端點 RDP 連接埠 (3389)。 
- 此版本包含針對多個問題的修正和改善。 

## <a name="azure-atp-release-230"></a>Azure ATP 2.30 版

發行日期：2018 年 4 月 29 日
 
- 加密降級可疑活動現在包含描述 Azure ATP 所偵測到之徵兆的辨識項區段，導致其懷疑發生加密降級活動。 
-   Azure ATP 現在會針對從 Azure ATP 傳送的所有電子郵件使用 Azure Email Orchestrator，包括可疑活動、監視警示和報表。 您會看到這些電子郵件通知現在遵循一致的格式使其容易使用，而從電子郵件連結到的 Excel 檔案將會從主控台中下載。
 
 

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