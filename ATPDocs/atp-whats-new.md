---
title: Azure 進階威脅防護中的新功能 (Azure ATP) | Microsoft Docs
description: 本文會經常更新，讓您知道最新版 Azure 進階威脅防護 (Azure ATP) 的新功能。
keywords: ''
author: mlottner
ms.author: mlottner
manager: rkarlin
ms.date: 09/08/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 7d0f33db-2513-4146-a395-290e001f4199
ms.reviewer: ort
ms.suite: ems
ms.openlocfilehash: 946cfdeafd6f2ef0cba5c16d290ac922ccf68f4b
ms.sourcegitcommit: e4f108aec3cbfd88562217e36195b5d1250a1bbd
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/08/2019
ms.locfileid: "70803153"
---
# <a name="whats-new-in-azure-advanced-threat-protection-azure-atp"></a>Azure 進階威脅防護中的新功能 (Azure ATP)

本文會經常更新，讓您知道最新版 Azure ATP 的新功能。

RSS 摘要：複製以下 URL 並在您的摘要讀取程式中貼上，以在此頁面更新時接收通知：`https://docs.microsoft.com/api/search/rss?search=%22This+article+is+updated+frequently+to+let+you+know+what%27s+new+in+the+latest+release+of+Azure+ATP%22&locale=en-us`

發行日期：2019 年 9 月 8 日

# <a name="azure-atp-release-294"></a>Azure ATP 2.94 版

- 版本包括內部感應器基礎結構的數個功能改進與錯誤 (Bug) 修正。


發行日期：2019 年 9 月 1 日

## <a name="azure-atp-release-293"></a>Azure ATP 2.93 版

- 版本包括內部感應器基礎結構的數個功能改進與錯誤 (Bug) 修正。

發行日期：2019 年 8 月 25 日

## <a name="azure-atp-release-292"></a>Azure ATP 2.92 版

- 版本包括內部感應器基礎結構的數個功能改進與錯誤 (Bug) 修正。

發行日期：2019 年 8 月 18 日

## <a name="azure-atp-release-291"></a>Azure ATP 2.91 版

- 版本包括內部感應器基礎結構的數個功能改進與錯誤 (Bug) 修正。

發行日期：2019 年 8 月 11 日

## <a name="azure-atp-release-290"></a>Azure ATP 2.90 版

- 版本包括內部感應器基礎結構的數個功能改進與錯誤 (Bug) 修正。

發行日期：2019 年 8 月 4 日

## <a name="azure-atp-release-289"></a>Azure ATP 2.89 版

- **感應器方法改善**<br>為了避免在建立精確的橫向移動路徑 (LMP) 評定時產生過多 NTLM 流量，而改善了 Azure ATP 感應器方法，以降低依賴使用 NTLM 的程度，並提升 Kerberos 的使用率。  

- **警示增強：可疑的黃金票證使用 (不存在的帳戶)**<br>SAM 名稱變更已新增至此類型警示中所列的支援辨識項類型。 若要深入了解警示，包括如何預防此類型的活動與補救措施，請參閱[可疑的黃金票證使用 (不存在的帳戶)](atp-domain-dominance-alerts.md#suspected-golden-ticket-usage-nonexistent-account-external-id-2027)。

- **正式運作：可疑的 NTLM 驗證竄改**<br> [可疑的 NTLM 驗證竄改](atp-lateral-movement-alerts.md#suspected-ntlm-authentication-tampering-external-id-2039)警示已不再處於預覽模式，現在已公開推出。 

- 版本包括內部感應器基礎結構的數個功能改進與錯誤 (Bug) 修正。


2019 年 7 月 28 日發佈

## <a name="azure-atp-release-288"></a>Azure ATP 2.88 版 

- 此版本包括內部感應器基礎結構的數項功能改進與 Bug 修正。

2019 年 7 月 21 日發佈

## <a name="azure-atp-release-287"></a>Azure ATP 2.87 版 

- **功能增強：Azure ATP 獨立感應器的自動化 Syslog 事件收集**<br> Azure ATP 獨立感應器的連入 Syslog 連線現在已完全自動化，同時從設定畫面中移除切換選項。 這些變更不會影響連出 Syslog 連線。 

- 此版本包括內部感應器基礎結構的數項功能改進與 Bug 修正。

## <a name="azure-atp-release-286"></a>Azure ATP 2.86 版 

2019 年 7 月 14 日發行

- **新的安全性警訊：可疑的 NTLM 驗證竄改 (外部識別碼 2039)**<br>
Azure ATP [可疑的 NTLM 驗證竄改](atp-lateral-movement-alerts.md#suspected-ntlm-authentication-tampering-external-id-2039)新安全性警示目前處於公開預覽狀態。 <br> 在此偵測中，當系統懷疑有人使用「中間人」攻擊成功繞過 NTLM 訊息完整性檢查 (MIC) (Microsoft [CVE-2019-040](https://portal.msrc.microsoft.com/en-US/security-guidance/advisory/CVE-2019-1040) 中詳述的安全性弱點) 時，會觸發 Azure ATP 安全性警訊。 這些類型的攻擊會嘗試使 NTLM 安全性功能降級並成功驗證，最終目標是要進行成功的橫向移動。 

- **功能增強：擴充的裝置作業系統身分識別**<br> 到目前為止，Azure ATP 根據 Active Directory 中的可用屬性來提供實體裝置作業系統資訊。 先前，如果 Active Directory 未提供作業系統資訊，Azure ATP 實體頁面就也無法使用該資訊。 從這個版本開始，若遇到 Active Directory 沒有資訊的裝置，或未在 Active Directory 中註冊的裝置，Azure ATP 會使用擴充的裝置作業系統身分識別方法 TCP 指紋提供此資訊。 
 
    新增擴充裝置作業系統身分識別資料有助於識別未註冊和非 Windows 的裝置，同時在您的調查程序中提供協助。 若要深入了解 Azure ATP 中的網路名稱解析，請參閱[了解網路名稱解析 (NNR)](atp-nnr-policy.md)。  

- **新功能：已驗證的 Proxy - 預覽**<br> Azure ATP 現在支援已驗證的 Proxy。 請使用感應器命令列指定 Proxy URL，並指定使用者名稱/密碼，以使用需要驗證的 Proxy。 如需如何使用已驗證 Proxy 的詳細資訊，請參閱[設定 Proxy](https://docs.microsoft.com/azure-advanced-threat-protection/configure-proxy#configure-the-proxy)。

- **功能增強：自動網域同步器流程**<br> 在安裝期間將網域控制站指定及標記為候選網域同步器的流程，現在已完全自動化。 手動將網域控制站選取為候選網域同步器的切換選項已經移除。 

- 此版本還包括內部感應器基礎結構的數項功能改進與 Bug 修正。

## <a name="azure-atp-release-285"></a>Azure ATP 2.85 版

發行日期：2019 年 7 月 7 日

- 此版本包括內部感應器基礎結構的數項功能改進與 Bug 修正。

## <a name="azure-atp-release-284"></a>Azure ATP 2.84 版

發行日期：2019 年 7 月 1 日

- **新增位置支援：Azure 英國資料中心**<br>
    Azure 英國資料中心現在支援 Azure ATP 執行個體。 若要了解如何建立 Azure ATP 執行個體和其對應的資料中心位置，請參閱 [Azure ATP 安裝的步驟 1](https://docs.microsoft.com/azure-advanced-threat-protection/install-atp-step10)。

- **功能增強：敏感性群組的可疑新增項目警示 (外部識別碼 2024) 新名稱和功能**<br> 
    **敏感性群組的可疑新增項目**警示先前命名為**敏感性群的可疑修改**警示。 警示 (識別碼 2024) 的外部識別碼保持不變。 描述性名稱變更可更精確地反映針對**敏感性**群組新增項目發出警示的目的。 增強型警示也強調新辨識項和改善的描述。 如需詳細資訊，請參閱[敏感性群組的可疑新增項目](https://docs.microsoft.com/azure-advanced-threat-protection/atp-domain-dominance-alerts#suspicious-additions-to-sensitive-groups-external-id-2024)。  

- **新文件功能：從 Advanced Threat Analytics 移至 Azure ATP 的指南**<br>
    這篇新文章包含必要條件、規劃指引，以及從 ATA 移至 Azure ATP 服務的設定和驗證步驟。 如需詳細資訊，請參閱[從 ATA 移至 Azure ATP](https://docs.microsoft.com/azure-advanced-threat-protection/ata-atp-move-overview)。   

- 此版本還包括內部感應器基礎結構的數項功能改進與 Bug 修正。

## <a name="azure-atp-release-283"></a>Azure ATP 2.83 版

2019 年 6 月 23 日發行

- **功能增強：可疑的服務建立警示 (外部識別碼 2026)**<br> 
    此警示現在會強調改善的警示頁面，其中含有額外的辨識項和新說明。 如需詳細資訊，請參閱[可疑的服務建立安全性警示](https://docs.microsoft.com/azure-advanced-threat-protection/atp-domain-dominance-alerts#suspicious-service-creation-external-id-2026)。

-  **執行個體命名支援：新增支援僅限數字的網域前置詞**<br>
    新增支援使用只包含數字的初始網域前置詞來建立 Azure ATP 執行個體。 例如，現在支援使用 123456.contoso.com 等僅限數字的初始網域前置詞。 

- 此版本還包括內部感應器基礎結構的數項功能改進與 Bug 修正。


## <a name="azure-atp-release-282"></a>Azure ATP 2.82 版

發行日期：2019 年 6 月 18 日

- **新的公開預覽**<br>
Azure ATP 的身分識別威脅調查體驗目前處於**公開預覽**狀態，適用於所有受保護的 Azure ATP 租用戶。 如需深入了解，請參閱 [Azure ATP Microsoft Cloud App Security 調查體驗](atp-mcas-integration.md)。 

- **正式版本**<br>
Azure ATP 現已在正式版本中支援未受信任的樹系。 如果要深入了解，請參閱 [Azure ATP 多重樹系](atp-multi-forest.md)。 

- 此版本包括內部感應器基礎結構的數項功能改進與 Bug 修正。

## <a name="azure-atp-release-281"></a>Azure ATP 2.81 版

發行日期：2019 年 6 月 10 日

- 此版本包括內部感應器基礎結構的數項功能改進與 Bug 修正。

## <a name="azure-atp-release-280"></a>Azure ATP 2.80 版

發行日期：2019 年 6 月 2 日

- **功能增強：可疑 VPN 連線警示**<br>
   此警示現在包含增強的辨識項和文字，以提供更好的使用性。 如需該警示功能，以及建議的補救步驟和預防措施的詳細資訊，請參閱[可疑 VPN 連線警示描述](atp-compromised-credentials-alerts.md#suspicious-vpn-connection-external-id-2025)。

- 此版本還包括內部感應器基礎結構的數項功能改進與 Bug 修正。

## <a name="azure-atp-release-279"></a>Azure ATP 2.79 版
發行日期：2019 年 5 月 26 日

- **正式運作：安全性主體偵察 (LDAP) (外部識別碼 2038)**

    此警示現在已 GA (正式運作)。 如需該警示及其功能，以及建議的補救和預防措施的詳細資訊，請參閱[安全性主體偵查 (LDAP) 警示描述](atp-reconnaissance-alerts.md#security-principal-reconnaissance-ldap-external-id-2038)

- 此版本還包括內部感應器基礎結構的數項功能改進與 Bug 修正。

## <a name="azure-atp-release-278"></a>Azure ATP 2.78 版

發行日期：2019 年 5 月 19 日

- **功能增強：機密實體**<br> Exchange 伺服器的手動機密標記

    您現在可以在設定期間手動將實體標記為 Exchange Server伺服器。

    若要手動將實體標記為 Exchange 伺服器：
    1. 在 Azure ATP 入口網站中，存取 [設定]  功能表。
    2. 在 [偵測]  下，選取 [實體標記]  ，然後選取 [機密]  。
    3. 選取 [Exchange 伺服器]  ，然後新增您要標記的實體。

    將某部電腦標記為 Exchange 伺服器之後，系統會將它標記為機密，並顯示它已被標記為 Exchange 伺服器。  「機密」標記將會出現在該電腦的實體設定檔中，而且該電腦在所有偵測中都會被視為以「機密」帳戶與「橫向移動路徑」為基礎。

- 此版本還包括內部感應器基礎結構的數項功能改進與 Bug 修正。

## <a name="azure-atp-release-277"></a>Azure ATP 2.77 版

發行日期：2019 年 5 月 12 日

- 此版本包括內部感應器基礎結構的數項功能改進與 Bug 修正。

## <a name="azure-atp-release-276"></a>Azure ATP 2.76 版

發行日期：2019 年 5 月 6 日

- 此版本包括內部感應器基礎結構的數項功能改進與 Bug 修正。

## <a name="azure-atp-release-275"></a>Azure ATP 2.75 版

發行日期：2019 年 4 月 28 日

- **功能增強：機密實體**<br> 從此版本 (2.75) 開始，由 Azure ATP 識別為 Exchange Server 的機器現在會被自動標示為**機密**。  

    因為運作方式如 Exchange Server 的清單而被自動標示為**機密**的實體原會列出此分類作為其被標示的原因。 

- 此版本包括內部感應器基礎結構的數項功能改進與 Bug 修正。

## <a name="azure-atp-release-274"></a>Azure ATP 2.74 版

將於 2019 年 4 月 14 日發佈

- 此版本包括內部感應器基礎結構的數項功能改進與 Bug 修正。

## <a name="azure-atp-release-273"></a>Azure ATP 2.73 版

將於 2019 年 4 月 10 日發佈

- 此版本包括內部感應器基礎結構的數項功能改進與 Bug 修正。

## <a name="azure-atp-release-272"></a>Azure ATP 2.72 版

發行日期：2019 年 3 月 31 日

- **功能增強：橫向移動路徑 (LMP) 限域深度**<br>
橫向移動路徑 (LMP) 為 Azure ATP 探索威脅和風險的重要方法。 為了讓您可以專注在針對您最敏感使用者的重大風險上，此更新能限制所顯示之每個圖表的範圍和深度，使您能以更輕鬆且快速的方式分析並補救每個 LMP 上之敏感性使用者的風險。   

    請參閱[橫向移動路徑](use-case-lateral-movement-path.md)以深入了解 Azure ATP 如何使用 LMP 來呈現針對您環境中每個實體的存取風險。   

- 此版本還包括內部感應器基礎結構的數項功能改進與 Bug 修正。

## <a name="azure-atp-release-271"></a>Azure ATP 2.71 版

發行日期：2019 年 3 月 24 日

- **功能增強：網路名稱解析 (NNR) 監視警示**<br>
已根據 NNR 針對與 Azure ATP 安全性警訊關聯的信賴等級新增監視警示。 每個監視警示都包括可採取的動作與詳細建議，可協助解決低 NNR 成功率問題。 

    請參閱[什麼是網路名稱解析](atp-nnr-policy.md)以深入了解 Azure ATP 如何使用 NNR 以及它對警示精確度而言為何很重要。 

- **Server 支援：我們透過 KB4487044 新對 Server 2019 的支援**<br>
我們透過 KB4487044 的修補層級新增對使用 Windows Server 2019 的支援。 不支援在不安裝該補充程式的情況下使用 Server 2019，而且也無法安裝此更新。 

- **功能增強：以使用者為基礎的警示排除**<br>
延伸警示排除選項現在允許將特定使用者從特定警示排除。 排除有助於避免使用或設定特定內部軟體類型重複觸發良性安全性警訊的情況。

- 此版本還包括內部感應器基礎結構的數項功能改進與 Bug 修正。

## <a name="azure-atp-release-270"></a>Azure ATP 2.70 版
發行日期：2019 年 3 月 17 日

- **功能增強：已將網路名稱解析 (NNR) 信賴等級新增至多個警示**<br> 網路名稱解析 (或稱 NNR)，可用來協助主動識別可疑攻擊的來源實體身分識別。 您現在只要將 NNR 信賴等級新增至 Azure ATP 警示辨識項清單，就能立即針對已識別之可能來源的相關 NNR 信賴等級進行評估與了解，並適當地進行補救。 

    已將 NNR 信賴等級辨識項新增至下列警示：
  - [網路對應偵察 (DNS)](atp-reconnaissance-alerts.md#network-mapping-reconnaissance-dns-external-id-2007)
  - [可疑的身分識別竊取 (票證傳遞)](atp-lateral-movement-alerts.md#suspected-identity-theft-pass-the-ticket-external-id-2018) 
  - [可疑的 NTLM 轉送攻擊 (Exchange 帳戶) - 預覽](atp-lateral-movement-alerts.md#suspected-ntlm-relay-attack-exchange-account-external-id-2037)
  - [可疑的 DCSync 攻擊 (目錄服務的複寫)](atp-domain-dominance-alerts.md#suspected-dcsync-attack-replication-of-directory-services-external-id-2006)

- **其他健全狀況警示案例：Azure ATP 感應器服務無法啟動**<br>目前假如因為網路擷取驅動程式發生問題，導致 Azure ATP 感應器無法啟動，便會觸發感應器健全狀況警示。 如需關於 Azure ATP 記錄及如何使用的詳細資訊，請參閱[使用 Azure ATP 記錄針對 Azure ATP 進行疑難排解](troubleshooting-atp-using-logs.md)。 
  
- 此版本還包括內部感應器基礎結構的數項功能改進與 Bug 修正。

## <a name="azure-atp-release-269"></a>Azure ATP 2.69 版
發行日期：2019 年 3 月 10 日

- **功能增強：可疑的身分識別竊取 (票證傳遞) 警訊**<br> 此警訊現可提供新的辨識項，來顯示使用遠端桌面通訊協定 (RDP) 所進行之連線的詳細資料。 新增的辨識項可供您輕鬆補救因透過 RDP 連線使用 Remote Credential Guard 而造成的已知良性確判 (B-TP) 警訊問題。 

- **功能增強：透過 DNS 執行遠端程式碼警訊**<br> 此警訊現可提供新的辨識項，來顯示您網域控制站安全性更新的狀態，及通知您何時需要更新。   

- **新文件功能：Azure ATP 安全性警訊 MITRE ATT&CK Matrix™**<br>

    為了說明及讓您更輕鬆地對應 Azure ATP 安全性警訊及所熟悉 MITRE ATT&CK Matrix 之間的關聯性，我們將相關的 MITRE 技術新增到了 Azure ATP 安全性警訊清單。 這項新增的參考可供您更輕鬆地了解觸發 Azure ATP 安全性警訊時，可能使用的可疑攻擊技術。 深入了解 [Azure ATP 安全性警訊指南](suspicious-activity-guide.md)。  

- 此版本還包括內部感應器基礎結構的數項功能改進與 Bug 修正。

## <a name="azure-atp-release-268"></a>Azure ATP 2.68 版
發行日期：2019 年 3 月 3 日

- **功能增強：可疑的暴力密碼破解攻擊 (LDAP) 警示**<br>
針對此安全性警示，已進行大幅的可用性改進，包括已修訂的描述、額外來源資訊的佈建，以及可加速進行補救的猜測嘗試詳細資料。 深入了解[可疑的暴力密碼破解攻擊 (LDAP)](atp-compromised-credentials-alerts.md#suspected-brute-force-attack-ldap-external-id-2004) 安全性警示。 

- **新文件功能：安全性警示實驗室**<br>

    為了說明 Azure ATP 對您工作環境之真實威脅的強大偵測能力，我們已為此文件新增了新的**安全性警示實驗室**。 **安全性警示實驗室**可協助您快速設定實驗室或測試環境，並說明可抵禦常見、真實世界威脅和攻擊的最佳防禦姿態。  

    [逐步執行實驗室](atp-playbook-lab-overview.md)的設計目的是要確保您花費最少的時間進行建置，而將較多時間用在了解您的威脅局勢，以及可用的 Azure ATP 警示和防護。 我們很樂意收到您的意見反應。

- 此版本還包括內部感應器基礎結構的數項功能改進與 Bug 修正。

## <a name="azure-atp-release-267"></a>Azure ATP 2.67 版
發行日期：2019 年 2 月 24 日

- **新的安全性警訊：安全性主體偵察 (LDAP) - (預覽)**<br>

    Azure ATP 的[安全性主體偵察 (LDAP) - 預覽](atp-reconnaissance-alerts.md#security-principal-reconnaissance-ldap-external-id-2038)安全性警示現在處於公開預覽階段。 <br> 在此偵測中，當攻擊者使用安全性主體偵察來取得有關網域環境的重要資訊時，會觸發 Azure ATP 安全性警示。 此資訊可協助攻擊者對應網域結構以及識別具特殊權限帳戶以便在其攻擊擊殺鏈中的後續步驟中使用。 

    輕量型目錄存取通訊協定 (LDAP) 是同時用於合法與惡意目的來查詢 Active Directory 的最熱門的方法之一。 專注在 LDAP 的安全性主體偵察通常用於 Kerberoasting 攻擊的第一個階段。 Kerberoasting 攻擊是用於取得目標安全性主體名稱 (SPN) 清單，接著攻擊者會嘗試為其取得票證授權伺服器 (TGS) 憑證。

- **功能增強：帳戶列舉偵察 (NTLM) 警示** <br> 
    改進的**帳戶列舉偵察 (NTLM)** 警示 (使用額外分析)，以及改進的偵測邏輯以減少 **B-TP** 與 **FP** 警示結果。 
 
- **功能增強：網路對應偵察 (DNS) 警示** <br>
    新的偵測類型已新增到網路對應偵察 (DNS) 警示。 除了偵測可疑的 AXFR 要求之外，Azure ATP 現在也會偵測源自非 DNS 伺服器且使用過量要求的可疑要求類型。

 - 此版本還包括內部感應器基礎結構的數項功能改進與 Bug 修正。

## <a name="azure-atp-release-266"></a>Azure ATP 2.66 版
發行日期：2019 年 2 月 17 日

- **功能增強：可疑的 DCSync 攻擊 (目錄服務的複寫) 警示**<br>
已針對此安全性警示進行使用方面性的改進，包括已修正的描述、佈建額外的來源資訊、新資訊圖表與更多辨識項。 深入了解[可疑 DCSync 攻擊 (目錄服務的複寫)](atp-domain-dominance-alerts.md#suspected-dcsync-attack-replication-of-directory-services-external-id-2006) 安全性警示。 

- 此版本還包括內部感應器基礎結構的數項功能改進與 Bug 修正。

## <a name="azure-atp-release-265"></a>Azure ATP 2.65 版
發行日期：2019 年 2 月 10 日

- **新的安全性警訊：可疑的 NTLM 轉送攻擊 (Exchange 帳戶) – (預覽)**<br>
Azure ATP [可疑的 NTLM 轉送攻擊 (Exchange 帳戶) - 預覽](atp-lateral-movement-alerts.md#suspected-ntlm-relay-attack-exchange-account-external-id-2037)安全性警訊現已在公開預覽階段。 <br> 在此偵測中，當識別到可疑來源使用 Exchange 帳戶認證時，便會觸發 Azure ATP 安全性警訊。 這些攻擊類型會嘗試利用 NTLM 轉送技術來取得網域控制站交換權限，又稱為 **ExchangePriv**。 若要深入了解 **ExchangePriv** 技術，請參閱最早於 2019 年 1 月 31 日發佈的 [ADV190007 公告](https://portal.msrc.microsoft.com/en-US/security-guidance/advisory/ADV190007)，以及 [Azure ATP 警示回應](https://techcommunity.microsoft.com/t5/Enterprise-Mobility-Security/How-to-win-the-latest-security-race-over-NTLM-relay/ba-p/334511) \(英文\)。  

- **正式運作：透過 DNS 執行遠端程式碼**<br>
此警示現在已 GA (正式運作)。 如需詳細資訊與警示功能，請參閱[透過 DNS 執行遠端程式碼警示描述頁面](atp-lateral-movement-alerts.md#remote-code-execution-over-dns-external-id-2036)。 

- **正式運作：SMB 上的資料外流**<br>
此警示現在已 GA (正式運作)。 如需詳細資訊與警示功能，請參閱[透過 SMB 的資料外流警示頁面](atp-exfiltration-alerts.md#data-exfiltration-over-smb-external-id-2030)。


- 此版本還包括內部感應器基礎結構的數項功能改進與 Bug 修正。

## <a name="azure-atp-release-264"></a>Azure ATP 2.64 版
2019 年 2 月 4 日發行

- **正式運作：可疑的黃金票證使用 (票證異常)**<br>
此警示現在已 GA (正式運作)。 如需詳細資訊與警示功能，請參閱[可疑的黃金票證使用 (票證異常) 警示描述頁面](atp-domain-dominance-alerts.md#suspected-golden-ticket-usage-ticket-anomaly-external-id-2032)。 

- **功能增強：網路對應偵察 (DNS)**<br>
改善針對此警示部署的警示偵測邏輯，將誤判和警示干擾降至最低。 此警示在第一次可能觸發之前，有 8 天的學習期間。 如需此警示的詳細資訊，請參閱[網路對應偵察 (DNS) 警示描述頁面](atp-reconnaissance-alerts.md#network-mapping-reconnaissance-dns-external-id-2007)。 

    **由於此警示的增強功能，所以 nslookup 方法不應再用來於初始設定期間測試 Azure ATP 連線。** 

- **功能增強：**<br>
此版本包含重新設計的警示頁面以及新的辨識項，提供更佳的警示調查。 
    - [可疑的暴力密碼破解攻擊 (SMB)](atp-compromised-credentials-alerts.md#suspected-brute-force-attack-smb-external-id-2033)
    - [可疑的黃金票證使用 (時間異常) 警示描述頁面](atp-domain-dominance-alerts.md#suspected-golden-ticket-usage-time-anomaly-external-id-2022)
    - [可疑的 Overpass-the-Hash 攻擊 (Kerberos)](atp-lateral-movement-alerts.md#suspected-overpass-the-hash-attack-kerberos-external-id-2002)
    - [可疑的 Metasploit 入侵架構使用](atp-compromised-credentials-alerts.md#suspected-use-of-metasploit-hacking-framework-external-id-2034)
    - [可疑的 WannaCry 勒索軟體攻擊](atp-compromised-credentials-alerts.md#suspected-wannacry-ransomware-attack-external-id-2035)

- 此版本還包括內部感應器基礎結構的數項功能改進與 Bug 修正。


## <a name="azure-atp-release-263"></a>Azure ATP 2.63 版
發行日期：2019 年 1 月 27 日

- **新功能：不信任的樹系支援 - (預覽)**<br>
Azure ATP 對非信任樹系內的感應器支援現已開放預覽。 從 Azure ATP 入口網站 [目錄服務]  頁面設定額外一組認證，讓 Azure ATP 感應器能連線至不同 Active Directory 樹系，以及回報給 Azure ATP 服務。 如果要深入了解，請參閱 [Azure ATP 多重樹系](atp-multi-forest.md)。 

- **新功能：網域控制站涵蓋範圍**<br>
Azure ATP 現在會提供 Azure ATP 監視網域控制站的涵蓋範圍資訊。  
從 Azure ATP 入口網站 [感應器]  頁面，檢視 Azure ATP 在您環境中偵測到的受監視與未受監視網域控制站數。 下載受監視網域控制站清單以利進一步分析，以及建置行動計劃。 如果要深入了解，請參閱[網域控制站監視](atp-sensor-monitoring.md)操作指南。 

- **功能增強：帳戶列舉偵察**<br>
Azure ATP 帳戶列舉偵察偵測現在會偵測使用 Kerberos 和 NTLM 的列舉嘗試，並據此發出警示。 偵測在之前僅適用於使用 Kerberos 的嘗試。 如果要深入了解，請參閱 [Azure ATP 偵查警示](atp-reconnaissance-alerts.md#account-enumeration-reconnaissance-external-id-2003)。 

- **功能增強：遠端程式碼執行嘗試警示**<br>
    - 服務建立、WMI 執行和新的 **PowerShell** 執行等所有遠端執行活動，均已新增至目的地電腦的設定檔時間軸。 目的地電腦是命令執行所在的網域控制站。 
    - **PowerShell** 執行已新增至遠端程式碼執行活動的清單中，該清單列在實體設定檔警示時間軸內。
    - 如果要深入了解，請參閱[修復遠端程式碼執行嘗試](atp-domain-dominance-alerts.md#remote-code-execution-attempt-external-id-2019)。  

- **Windows Server 2019 LSASS 問題和 Azure ATP**<br>
為了回應客戶對於搭配執行 Windows Server 2019 之網域控制站使用 Azure ATP 所提出的意見反應，此更新包含了額外的邏輯，可避免在 Windows Server 2019 電腦上觸發回報的行為。 雖然我們規劃在之後的 Azure ATP 更新中為 Windows Server 2019 推出完整的 Azure ATP 感應器支援，但目前並**不**支援在 Windows Servers 2019 上安裝和執行 Azure ATP。 如果要深入了解，請參閱 [Azure ATP 感應器需求](atp-prerequisites.md#azure-atp-sensor-requirements)。 

- 此版本還包括內部感應器基礎結構的數項功能改進與 Bug 修正。


## <a name="azure-atp-release-262"></a>Azure ATP 2.62 版
發行日期：2019 年 1 月 20 日

- **新的安全性警訊：透過 DNS 執行遠端程式碼 - (預覽)**<br>
Azure ATP 的[透過 DNS 執行遠端程式碼](atp-lateral-movement-alerts.md#remote-code-execution-over-dns-external-id-2036)安全性警示目前處於公開預覽狀態。 <br> 在此偵測中，當 DNS 查詢可能利用安全性弱點 [CVE-2018-8626](https://portal.msrc.microsoft.com/en-US/security-guidance/advisory/CVE-2018-8626) 對網路中的網域控制站發動攻擊時，會觸發 Azure ATP 安全性警示。

- **功能增強：感應器更新延遲 72 小時** <br> 變更選項使所選感應器的感應器更新，於每次 Azure ATP 更新推出之後延遲 72 小時 (而不是先前延遲 24 小時)。 如需設定指示，請參閱 [Azure ATP 感應器更新](sensor-update.md)。 


- 此版本還包括內部感應器基礎結構的數項功能改進與 Bug 修正。

## <a name="azure-atp-release-261"></a>Azure ATP 2.61 版
發行日期：2019 年 1 月 13 日

- **新的安全性警示：SMB 上的資料外洩 - (預覽)**<br>
Azure ATP 的 [SMB 上的資料外流](atp-exfiltration-alerts.md)安全性警訊現為公開預覽狀態。 <br> 具有網域系統管理員權限的攻擊者可能會危害 KRBTGT 帳戶。 攻擊者可使用 KRBTGT 帳戶，建立可提供任何資源授權的 Kerberos 票證授權票證 (TGT)。 


- **功能增強：遠端程式碼執行嘗試**安全性警訊 <br> 新增警訊描述及其他辨識項，讓您能更容易了解警訊，且提供了更好的調查工作流程。 


- **功能增強：DNS 查詢邏輯活動** <br>將其他查詢類型新增到 [Azure ATP 受監視的活動](monitored-activities.md)，其中包含：**TXT**、**MX**、**NS**、**SRV**、**ANY**、**DNSKEY**。 

- **功能增強：可疑的黃金票證使用方式 (票證異常) 及可疑的黃金票證使用方式 (不存在的帳戶)** <br>
改善的偵測邏輯皆已套用到兩個警訊中，以降低 FP 警訊的數目，進而傳遞更準確的結果。

- **功能增強：Azure ATP 安全性警訊文件** <br>
Azure ATP 安全性警訊文件已增強並擴充，現在其中包含更優異的警訊描述、更準確的警訊分級，以及辨識項、修復和防護的解說。 使用以下連結熟悉全新安全性警訊文件的設計： 
    - [Azure ATP 安全性警訊](suspicious-activity-guide.md)
    - [了解安全性警訊](understanding-security-alerts.md)
        - [偵察階段警訊](atp-reconnaissance-alerts.md)
        - [遭入侵的認證階段警示](atp-compromised-credentials-alerts.md)
        - [橫向移動階段警示](atp-lateral-movement-alerts.md)
        - [網域支配階段警示](atp-domain-dominance-alerts.md)
        - [外洩階段警訊](atp-exfiltration-alerts.md)
    - [調查電腦](investigate-a-computer.md)
    - [調查使用者](investigate-a-user.md)

- 此版本還包括內部感應器基礎結構的數項功能改進與 Bug 修正。


## <a name="azure-atp-release-260"></a>Azure ATP 2.60 版
發行日期：2019 年 1 月 6 日

- 此版本包括內部感應器基礎結構的數項功能改進與 Bug 修正。

## <a name="azure-atp-release-259"></a>Azure ATP 2.59 版
發行日期：2018 年 12 月 16 日

- 此版本包括內部感應器基礎結構的數項功能改進與 Bug 修正。


## <a name="azure-atp-release-258"></a>Azure ATP 2.58 版

發行日期：2018 年 12 月 9 日

- **安全性警示增強功能：不尋常的通訊協定實作警示分割**<br>
「不尋常通訊協定實作」安全性警訊的 Azure ATP 系列先前共用 1 個 externalId (2002)，現在則分割為四個不同的警訊，且每個都含有對應的唯一外部識別碼。 

### <a name="new-alert-externalids"></a>新的警示 externalId

> [!div class="mx-tableFixed"] 

|新安全性警訊名稱|舊安全性警訊名稱|唯一外部識別碼|
|---------|----------|---------|
|可疑的暴力密碼破解攻擊 (SMB)|不尋常的通訊協定實作 (可能使用 Hydra 等惡意工具)|2033
|可疑的 Overpass-the-Hash 攻擊 (Kerberos)|不尋常的 Kerberos 通訊協定實作 (可能為 Overpass-the-Hash 攻擊)|2002|
|可疑的 Metasploit 入侵架構使用|不尋常的通訊協定實作 (可能使用 Metasploit 入侵工具)|2034
|可疑的 WannaCry 勒索軟體攻擊|不尋常的通訊協定實作 (可能為 WannaCry 勒索軟體攻擊)|2035
|

- **新的受監視的活動：透過 SMB 的檔案複製**<br>
使用 SMB 複製檔案現在是受監視且可篩選的活動。 深入了解 [Azure ATP 監視器](monitored-activities.md)會監視哪些活動，以及如何在入口網站中[篩選和搜尋受監視的活動](atp-activities-search.md)。 

- **大型橫向移動路徑映像增強功能**<br>
在檢視大型橫向移動路徑時，Azure ATP 現在只會將連線到選取之實體的節點醒目提示，而不會將其他節點模糊處理。 這項變更可大幅提升大型 LMP 轉譯的速度。 

- 此版本包括內部感應器基礎結構的數項功能改進與 Bug 修正。

## <a name="azure-atp-release-257"></a>Azure ATP 2.57 版
發行日期：2018 年 12 月 2 日

- **新的安全性警示：可疑的黃金票證使用 - 票證異常 (預覽)**<br>
Azure ATP 的[可疑黃金票證使用 - 票證異常](suspicious-activity-guide.md)安全性警示目前處於公開預覽狀態。 <br> 具有網域系統管理員權限的攻擊者可能會危害 KRBTGT 帳戶。 攻擊者可使用 KRBTGT 帳戶，建立可提供任何資源授權的 Kerberos 票證授權票證 (TGT)。 
<br>因為這種偽造的 TGT 可以讓攻擊者獲得持久的網路持續性，所以稱為「黃金票證」。 此全新偵測設計用來識別這類偽造黃金票證擁有的唯一特性。 


- **功能增強：自動化建立 Azure ATP 執行個體 (工作區)** <br>
即日起，Azure ATP「工作區」  已重新命名為 Azure ATP「執行個體」  。 Azure ATP 現在支援每個 Azure ATP 帳戶一個 Azure ATP 執行個體。 新客戶的執行個體會使用 [Azure ATP 入口網站](https://portal.atp.azure.com)中的執行個體建立精靈來建立。 現有的 Azure ATP 工作區會自動轉換成具備更新的 Azure ATP 執行個體。  

  - 使用[建立您的 Azure ATP 執行個體](install-atp-step1.md)來簡化執行個體建立，以進行更快速的部署和保護。 
  - 所有[資料隱私權與合規性](atp-privacy-compliance.md)皆維持不變。 

  若要深入了解 Azure ATP 執行個體，請參閱[建立您的 Azure ATP 執行個體](install-atp-step1.md)。 

- 此版本包括內部感應器基礎結構的數項功能改進與 Bug 修正。

## <a name="azure-atp-release-256"></a>Azure ATP 2.56 版
發行日期：2018 年 11 月 25 日


- **功能增強：橫向移動路徑 (LMP)** <br>
已新增兩個其他功能來加強 Azure ATP 橫向移動路徑 (LMP) 功能：

  - 使用 LMP 報表時，現在可以根據每個實體儲存及探索 LMP 歷程記錄。 
  - 透過活動時間表追蹤 LMP 中的實體，並使用提供的額外辨識項來探索潛在的攻擊路徑。 

  請參閱 [Azure ATP 橫向移動路徑](use-case-lateral-movement-path.md)以深入了解使用及利用增強 LMP 進行調查的方式。 

- **文件增強：橫向移動路徑、安全性警示名稱**<br> 已對 Azure ATP 文章進行新增與更新，其包括橫向移動路徑的描述及功能說明，並且已為所有舊安全性警訊名稱新增新名稱和 externalId 的名稱對應。 
  - 請參閱 [Azure ATP 橫向移動路徑](use-case-lateral-movement-path.md)、[調查橫向移動路徑](investigate-lateral-movement-path.md)，以及[安全性警訊指南](suspicious-activity-guide.md)以深入了解。   

- 此版本包括內部感應器基礎結構的數項功能改進與 Bug 修正。

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
