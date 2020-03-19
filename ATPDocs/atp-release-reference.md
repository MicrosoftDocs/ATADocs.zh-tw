---
title: Azure 進階威脅防護 (Azure ATP) 舊版本參考
description: 此文章是 Azure 進階威脅防護 (Azure ATP) 舊版更新的參考。
keywords: ''
author: shsagir
ms.author: shsagir
manager: rkarlin
ms.date: 11/17/2019
ms.topic: reference
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: ort
ms.suite: ems
ms.openlocfilehash: efc6412bebeb839c577a3e65aac0d9386927a0a3
ms.sourcegitcommit: 11fff9d4ebf1c50b04f7789a22c80cdbc3e4416a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/15/2020
ms.locfileid: "79414177"
---
# <a name="release-reference-of-azure-advanced-threat-protection-azure-atp"></a>Azure 進階威脅防護 (Azure ATP) 的版本參考 

此文章是所有 Azure ATP 版本的參考，直到 (並包含) 2.55 版為止。 如需最新的 Azure ATP 版本更新 (2.56 與更新版本)，請參閱 [Azure ATP 新功能](atp-whats-new.md)。


## <a name="azure-atp-release-255"></a>Azure ATP 2.55 版
發行日期：2018 年 11 月 18 日

- **安全性警示：通過 DNS 的可疑通訊 - 一般可用性**<br>
Azure ATP [通過 DNS 的可疑通訊](suspicious-activity-guide.md) 安全性警訊現已正式推出。 <br> 通常，大多數組織中的 DNS 通訊協定不會受到監視，而且很少會因惡意活動而遭到封鎖。 這讓攻擊者有機會在遭入侵的電腦上濫用 DNS 通訊協定。 透過 DNS 的惡意通訊可用來竊取資料、命令和控制攻擊和/或規避公司網路限制。

- 此版本還包括內部感應器基礎結構的數項功能改進與 Bug 修正。

## <a name="azure-atp-release-254"></a>Azure ATP 2.54 版
發行日期：2018 年 11 月 11 日

- **功能增強：將預設網域排除項目新增至透過 DNS 的可疑通訊警示**<br>   將三個熱門網域新增至預設網域排除清單。 排除清單仍可完全自訂。 若要深入了解，請參閱[從偵測排除實體](excluding-entities-from-detections.md)。 

- **文件增強：SIEM 記錄檔更新、已知問題的指引**<br>    已將 externalId 對應和其他說明，新增至 SIEM 記錄檔描述。 若要深入了解，請參閱 [SIEM 記錄檔參考](cef-format-sa.md)。 <br>已額外新增目前尚未解決之已知問題指南的文章。 若要深入了解，請參閱 [Azure ATP 已知問題](known-issues.md)。  

- 此版本包括內部感應器基礎結構的數項功能改進與 Bug 修正。

## <a name="azure-atp-release-253"></a>Azure ATP 2.53 版
發行日期：2018 年 11 月 4 日

- **安全性警示增強功能：可疑的驗證失敗**<br>
Azure ATP 的[可疑的驗證失敗安全性警示](suspicious-activity-guide.md)現在包括針對密碼噴灑暴力密碼破解攻擊偵測的監視。
在典型的**密碼噴灑**攻擊中，攻擊者從網域控制站成功列舉有效使用者清單後，便會嘗試針對所有已知的使用者帳戶嘗試使用一個特製密碼 (一個密碼用於多個帳戶)。 當初始密碼噴灑失敗時，他們會利用其他的特製密碼再試一次，在嘗試之間通常會等候 30 分鐘。 等候時間可讓攻擊者避免觸發最常見以時間為基礎的帳戶鎖定閾值。 密碼噴灑已快速成為攻擊者和滲透測試者最愛的技術。 密碼噴灑攻擊已證明是取得組織內初始據點的有效方式，並可進行後續的橫向移動，嘗試提高權限。 

- **功能增強：傳送測試 Syslog 訊息**<br>   在 SIEM 設定程序期間可傳送測試 Syslog 訊息的新功能。 若要深入了解，請參閱[與 Syslog 整合](setting-syslog.md)。 

- 此版本還包括內部感應器基礎結構的數項功能改進與 Bug 修正。

## <a name="azure-atp-release-252"></a>Azure ATP 2.52 版
發行日期：2018 年 10 月 28 日


- **安全性警示增強功能：遠端程式碼執行嘗試**<br>
Azure ATP 的[遠端程式碼執行嘗試](suspicious-activity-guide.md)現在可以監視在網域控制站上執行遠端 PowerShell 程式碼的可疑嘗試。 遠端 PowerShell 是用於執行有效系統管理命令的常見方式，但常有人惡意用來嘗試在遠端端點上執行指令碼。 

- **功能增強：設定報表排程**
<br>您現在可以使用[報表](reports.md#)功能，設定某一小時，來為您的 Azure ATP 報表排程。 

- **新增設定：租用戶角色型存取控制 (RBAC)**
<br>您可從 Azure ATP 入口網站中新的 [管理] 連結，直接在 Azure Active Directory (AAD) 管理中心設定租用戶的安全性角色。 

- **修改文件結構與內容**
<br>Azure ATP 文件的近期內容變更包括提供 Azure ATP 所有受監視活動完整清單、活動篩選指示的新文章，並重新設計了文件網站結構，以提升可用性：
  - [Azure ATP 受監視的活動](monitored-activities.md) 
  - [Azure ATP 活動篩選](atp-activities-search.md) 
  - [Azure ATP 文件](https://docs.microsoft.com/azure-advanced-threat-protection/)  

- 此版本還包括內部感應器基礎結構的數項功能改進與 Bug 修正。

## <a name="azure-atp-release-251"></a>Azure ATP 2.51 版
發行日期：2018 年 10 月 21 日

- 您現在可以從 Azure ATP 入口網站[設定](integrate-wd-atp.md#how-to-integrate-azure-atp-with-windows-defender-atp)畫面啟用/停用 **WD-ATP 整合**。 (Azure ATP 使用者必須是 AAD 租用戶的全域或安全性系統管理員，才能使用這項功能)。

- 此版本還包括內部感應器基礎結構的數項功能改進與 Bug 修正。

## <a name="azure-atp-release-250"></a>Azure ATP 2.50 版
發行日期：2018 年 10 月 14 日
- 此版本包含針對多個問題的修正和改善。


## <a name="azure-atp-release-249"></a>Azure ATP 2.49 版
發行日期：2018 年 10 月 7 日
-   **新增偵測：可疑的 DNS 通訊** (預覽)<br>新增可協助防範可疑 DNS 通訊攻擊的偵測：

    -   這項偵測可協助偵測對 DNS 通訊協定的攻擊。 大多數組織中的 DNS 通訊協定，都不會受到監視，且很少會因惡意活動而遭到封鎖。 讓攻擊者有機會在遭入侵的電腦上濫用 DNS 通訊協定。 透過 DNS 的惡意通訊可用來竊取資料、命令和控制攻擊和/或規避公司網路限制。

- **新功能** <br>Azure ATP **使用者角色**已增強下列功能：
  - 變更安全性警訊的狀態 (重新開啟、關閉、排除、隱藏)
  - 設定已排程報表
  - 設定實體標記 (敏感性與 honey token)
  - 排除偵測
  - 變更語言
  - 設定透過電子郵件或 syslog 的通知


- 已找出並解決發生在 2018 年 9 月 16 日**使用目錄服務查詢探查**中暫時性增加情況的安全性警訊。 

- 此版本也包含針對多個問題的修正和改善。


## <a name="azure-atp-release-248"></a>Azure ATP 2.48 版
發行日期：2018 年 9 月 16 日
- **安全性警示：** 使用目錄服務查詢探查

  現在已改善此安全性警訊的資訊圖表和辨識項。 

- **從偵測中排除實體** 

  您現在可以選擇從下列偵測中排除實體以減少誤判： 
  - 可疑的 VPN 連線 (使用者排除)
  - 可疑的網域控制站升級 (潛在的 DcShadow 攻擊)
  - 可疑的複寫要求 (潛在的 DcShadow 攻擊)

- 此版本也包含針對多個問題的修正和改善。


## <a name="azure-atp-release-247"></a>Azure ATP 2.47 版
發行日期：2018 年 9 月 2 日

- **Azure ATP 進階稽核原則檢查**
 
Azure 進階威脅防護現在會檢查網域控制站的現有進階稽核原則，並建議原則變更，以為組織提供最大 Azure ATP 服務涵蓋範圍。 

**這個新的檢查可讓您：**
  -  找出 Windows 事件記錄檔中目前排除在 Azure ATP 涵蓋範圍外的遺漏事件。
  -  確認理想設定，並根據提供的健全狀況警示建議進行變更。
  -  將會為您所有網域控制站發出單一彙總健全狀況警示，並包括補救建議 (視需要)。

檢閱如何[設定進階稽核原則](atp-advanced-audit-policy.md)以確保系統設定正確。 
- 此版本也包含針對多個問題的修正和改善。

## <a name="azure-atp-release-246"></a>Azure ATP 2.46 版

發行日期：2018 年 8 月26 日

- 此版本包含針對多個問題的修正和改善。

## <a name="azure-atp-release-245"></a>Azure ATP 2.45 版

發行日期：2018 年 8 月19 日

- **Azure ATP 加入 Windows 事件追蹤 (ETW) 做為額外的資料來源**  <br> 除了現有的網路流量與 Windows 事件之外，加入 Windows 事件追蹤 (ETW) 做為額外的事件來源。 ETW 提供額外的可疑活動偵測，包括：可疑網域控制站升級與可疑網域控制站複寫要求 (兩者都是潛在的 DCShadow 攻擊)。 <br>
只有網域控制站上安裝的 ATP 感應器才支援 ETW 型偵測。 ATP 獨立感應器不支援 ETW 偵測。 <br>  

- **現在公開推出四種新的偵測方式** <br>
  - 可疑 VPN 連線
  - Kerberos 黃金票證 – 不存在的帳戶 
  - 可疑網域控制站升級 (潛在 DcShadow 攻擊) – ETW 型偵測，只有 ATP 感應器才支援 
  - 可疑網域控制站複寫要求 (潛在 DcShadow 攻擊) – ETW 型偵測，只有 ATP 感應器才支援

- 此版本也包含針對多個問題的修正和改善。


## <a name="azure-atp-release-244"></a>Azure ATP 2.44 版

發行日期：2018 年 8 月 12 日

- 此版本包含針對多個問題的修正和改善。
- 在感應器機器上建立的記錄檔已不再包含「例外狀況統計資料」記錄檔。


## <a name="azure-atp-release-243"></a>Azure ATP 2.43 版

發行日期：2018 年 8 月 5 日

- 此版本包含針對多個問題的修正和改善。



## <a name="azure-atp-release-242"></a>Azure ATP 2.42 版

發行日期：2018 年 7 月 29 日

- 此版本包含針對多個問題的修正和改善。 


## <a name="azure-atp-release-241"></a>Azure ATP 2.41 版

發行日期：2018 年 7 月 22 日

- **Azure ATP 多樹系支援正逐步推出 (預覽)** <br> Azure ATP 現在可支援擁有多個樹系的組織，讓您能跨樹系監視活動和分析使用者。 這項新功能可讓您：

  - 透過單一管理點來檢視和調查多個樹系中使用者執行的活動。
  - 提供了進階 Active Directory 整合和帳戶解析，以改進偵測及減少誤判。
  - 針對涵蓋範圍跨越組織的情況，有更佳的監視警示和報告。


-   **新增偵測：DCShadow**<br>新增了兩個警示，以協助抵擋網域控制站陰影 (DCShadow) 攻擊：

    -   可疑的網域控制站升級 (潛在的 DCShadow 攻擊) - 此偵測可協助偵測下列攻擊：電腦模擬網域控制站，然後嘗試以複寫來將變更散佈到網域中的其他網域控制站。

    -   可疑的複寫要求 (潛在的 DCShadow 攻擊) - 此偵測可協助防禦下列攻擊：嘗試對不是網域控制站的電腦執行 DC 升級，以進一步變更目錄物件。

-   **改進的加密降級資訊**<br>加密降級偵測現在為偵測到的特定攻擊類型提供更多相關資訊：Overpass-the-Hash、黃金票證和基本架構金鑰。 此外，這些警示已經過彙總，讓調查更容易進行。
- 此版本包含針對多個問題的修正和改善。 


## <a name="azure-atp-release-240"></a>Azure ATP 2.40 版

發行日期：2018 年 7 月 15 日

- 傳遞票證偵測現在會在 [警示詳細資料] 頁面中包含辨識項區段。 如此可提供額外的資訊以調查警示。

- 使用者存取控制旗標 (位在使用者設定檔中的 [目錄] 資料下) 現已包含圖例，讓您可以更清楚了解開啟和關閉的屬性有哪些。  

## <a name="azure-atp-release-239"></a>Azure ATP 2.39 版

發行日期：2018 年 7 月 5 日
-   **新增新的偵測：Kerberos 黃金票證 - 不存在的帳戶** (預覽)<br>這個新偵測所能防禦針對網域中不存在帳戶所建立黃金票證的攻擊，因此得以協助保護您的組織。 如需詳細資訊，請參閱 [Azure 進階威脅防護可疑活動指南](suspicious-activity-guide.md)

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
 
- **可疑 VPN 偵測**<br></br>此版本介紹可疑 VPN 偵測的預覽版本。 Azure ATP 會學習使用者 VPN 行為 (包括使用者登入的電腦以及使用者從中連線的位置)，並在與預期行為有所偏差時對您發出警示。 如需詳細資訊，請參閱[可疑 VPN 偵測](suspicious-activity-guide.md)。

- [Delayed update] \(延遲更新\) <br></br>每次 Azure ATP 更新時，您現在都可以選擇設定 Azure ATP 感應器稍後更新。 您現在可以將每個 Azure ATP 感應器設定為 [Delayed update] \(延遲更新\)  ，以在 Azure ATP 雲端服務更新後的 24 小時更新。 此功能可讓您在特定測試感應器上測試更新，而且只有在稍後才會更新生產感應器。 如果您在第一個更新週期期間發現問題，請開啟支援票證。 如需詳細資訊，請參閱[更新 Azure ATP 感應器](sensor-update.md)。

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
- Azure ATP 現在具有[**系統狀態**](https://health.atp.azure.com/)頁面，可讓您了解工作區管理入口網站是否正常運作、是否偵測到任何問題、感應器是否可將流量傳送至雲端。 您可從 Azure ATP 的功能表列存取 [系統狀態]  。


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
- [什麼是 Azure 進階威脅防護？](what-is-atp.md)
- [常見問題集](atp-technical-faq.md)
- [Azure ATP 必要條件](atp-prerequisites.md)
- [Azure ATP 容量規劃](atp-capacity-planning.md)
- [查看 Azure ATP 論壇！](https://aka.ms/azureatpcommunity)
