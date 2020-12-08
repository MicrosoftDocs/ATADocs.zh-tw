---
title: 適用於身分識別的 Defender：新功能
description: 本文會經常更新，讓您知道適用於身分識別的 Defender 最新版功能。
ms.date: 10/27/2020
ms.topic: overview
ms.reviewer: ort
ms.suite: ems
ms.openlocfilehash: dc5e1aa2c4162795f376e1061aa9f963b9ce0c48
ms.sourcegitcommit: cdb7ae4580851e25aae24d07e7d66a750aa54405
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2020
ms.locfileid: "96544516"
---
# <a name="whats-new-in-product-long"></a>[!INCLUDE [Product long](includes/product-long.md)] 的新功能

本文會經常更新，讓您知道最新版本 [!INCLUDE [Product long](includes/product-long.md)] (先前稱為 Azure 進階威脅防護，即 Azure ATP) 的新功能。

如需舊版 [!INCLUDE [Product short](includes/product-short.md)] 直到 (含) 2.55 版的詳細資料，請參閱 [[!INCLUDE [Product short](includes/product-short.md)] 版本參考](release-reference.md)。

RSS 摘要：將下列 URL 複製並貼上至您的摘要讀取器中，以在本頁更新時收到通知：`https://docs.microsoft.com/api/search/rss?search=%22This+article+is+updated+frequently+to+let+you+know+what%27s+new+in+the+latest+release+of+Azure+ATP%22&locale=en-us`

> [!IMPORTANT]
>
> Microsoft 的威脅防護產品名稱即將變更。 如需有關此變更的詳細資訊與其他更新，請參閱[這裡](https://www.microsoft.com/security/blog/?p=91813)。 從 2.129 版開始，我們將使用新的名稱。

## <a name="product-short-release-2132"></a>[!INCLUDE [Product short](includes/product-short.md)] 2.132 版

發行日期：2020 年 11 月 17 日

- 版本包括內部感應器基礎結構的數個功能改進與錯誤 (Bug) 修正。

## <a name="product-short-release-2131"></a>[!INCLUDE [Product short](includes/product-short.md)] 2.131 版

發行日期：2020 年 11 月 8 日

- **新的安全性警訊： 可疑的 Kerberos SPN 公開 (外部識別碼 2410)**  
[!INCLUDE [Product short](includes/product-short.md)]*可疑的 Kerberos SPN 公開 (外部識別碼2410)* 安全性警訊現已推出。 在此類偵測中，當攻擊者列舉服務帳戶及其各自的 SPN，並要求服務的 Kerberos TGS 票證時，即會觸發 [!INCLUDE [Product short](includes/product-short.md)] 安全性警訊。 攻擊者的意圖可能是從票證中擷取雜湊並加以儲存，以供往後用於離線暴力密碼破解攻擊。 如需詳細資訊，請參閱 [Kerberos SPN 公開](compromised-credentials-alerts.md#suspected-kerberos-spn-exposure-external-id-2410)。
- 版本包括內部感應器基礎結構的數個功能改進與錯誤 (Bug) 修正。

## <a name="product-short-release-2130"></a>[!INCLUDE [Product short](includes/product-short.md)] 2.130 版

發行日期：2020 年 10 月 25 日

- 版本包括內部感應器基礎結構的數個功能改進與錯誤 (Bug) 修正。

## <a name="azure-atp-release-2129"></a>Azure ATP 2.129 版

發行日期：2020 年 10 月 18 日

- 版本包括內部感應器基礎結構的數個功能改進與錯誤 (Bug) 修正。

## <a name="azure-atp-release-2128"></a>Azure ATP 2.128 版

發行日期：2020 年 9 月 27 日

- **修改過的電子郵件通知設定**  
我們正在移除用於開啟電子郵件通知的 [郵件通知] 切換開關。 若要接收電子郵件通知，只要新增地址即可。 如需詳細資訊，請參閱[設定通知](notifications.md)。
- 版本包括內部感應器基礎結構的數個功能改進與錯誤 (Bug) 修正。

## <a name="azure-atp-release-2127"></a>Azure ATP 2.127 版

發行日期：2020 年 9 月 20 日

- **新的安全性警訊：可疑的 Netlogon 權限提升嘗試 (外部識別碼 2411)**  
Azure ATP 的「可疑的 Netlogon 權限提升嘗試 (CVE-2020-1472 惡意探索) (外部識別碼 2411)」安全性警示現已可供使用。 在此偵測中，Azure ATP 安全性警示會在攻擊者使用也稱為「Netlogon 權限提高弱點」的 Netlogon 遠端通訊協定 ([MS-NRPC](/openspecs/windows_protocols/ms-nrpc/ff8f970f-3e37-40f7-bd4b-af7336e4792f))，針對網域控制站建立易受攻擊的 Netlogon 安全通道連線時觸發。 如需詳細資訊，請參閱[可疑的 Netlogon 權限提升嘗試](compromised-credentials-alerts.md#suspected-netlogon-priv-elev-2411)。
- 版本包括內部感應器基礎結構的數個功能改進與錯誤 (Bug) 修正。

## <a name="azure-atp-release-2126"></a>Azure ATP 版本 2.126

發行日期：2020 年 9 月 13 日

- 版本包括內部感應器基礎結構的數個功能改進與錯誤 (Bug) 修正。

## <a name="azure-atp-release-2125"></a>Azure ATP 2.125 版

發行日期：2020 年 9 月 6 日

- 版本包括內部感應器基礎結構的數個功能改進與錯誤 (Bug) 修正。

## <a name="azure-atp-release-2124"></a>Azure ATP 2.124 版

發行日期：2020 年 8 月 30 日

- **新的安全性警示**  
Azure ATP 安全性警示現在包含下列新的偵測：
  - **Active Directory 屬性偵察 (LDAP) (外部識別碼 2210)**  
在此偵測中，當懷疑攻擊者正成功取得可用於攻擊狙殺鏈的網域重要資訊時，就會觸發 Azure ATP 安全性警示。 如需詳細資訊，請參閱 [Active Directory 屬性偵察](reconnaissance-alerts.md#active-directory-attributes-reconnaissance-ldap-external-id-2210)。
  - **可疑的 Rogue Kerberos 憑證使用方式 (外部識別碼 2047)**  
在此偵測中，當攻擊者藉由洩露憑證授權單位伺服器而取得了組織的控制權，且可能正在產生憑證，以在日後的攻擊 (例如在網路中橫向移動) 中當作後門程式帳戶使用，就會觸發 Azure ATP 安全性警示。 如需詳細資訊，請參閱[可疑的 Rogue Kerberos 憑證使用方式](lateral-movement-alerts.md#suspected-rogue-kerberos-certificate-usage-external-id-2047)。
  - **可疑的黃金票證使用方式 (使用 RBCD 的票證異常) (外部識別碼 2040)**  
具有網域系統管理員權限的攻擊者可能會危害 KRBTGT 帳戶。 他們可使用 KRBTGT 帳戶，建立可提供任何資源授權的 Kerberos 票證授權票證 (TGT)。  
因為這種偽造的 TGT 可以讓攻擊者使用按資源限制委派 (RBCD) 獲得持久的網路持續性，所以稱為「黃金票證」。 此全新偵測設計用來識別這類偽造黃金票證擁有的唯一特性。
如需詳細資訊，請參閱 [可疑的黃金票證使用方式 (使用 RBCD 的票證異常)](domain-dominance-alerts.md#suspected-golden-ticket-usage-ticket-anomaly-using-rbcd-external-id-2040)。
- 版本包括內部感應器基礎結構的數個功能改進與錯誤 (Bug) 修正。

## <a name="azure-atp-release-2123"></a>Azure ATP 2.123 版

發行日期：2020 年 8 月 23 日

- 版本包括內部感應器基礎結構的數個功能改進與錯誤 (Bug) 修正。

## <a name="azure-atp-release-2122"></a>Azure ATP 2.122 版

發行日期：2020 年 8 月 16 日

- 版本包括內部感應器基礎結構的數個功能改進與錯誤 (Bug) 修正。

## <a name="azure-atp-release-2121"></a>Azure ATP 2.121 版

發行日期：2020 年 8 月 2 日

- 版本包括內部感應器基礎結構的數個功能改進與錯誤 (Bug) 修正。

## <a name="azure-atp-release-2120"></a>Azure ATP 2.120 版

2020 年 7 月26 日發行

- 版本包括內部感應器基礎結構的數個功能改進與錯誤 (Bug) 修正。

## <a name="azure-atp-release-2119"></a>Azure ATP 2.119 版

2020 年 7 月 5 日發行

- **功能增強：Excel 報表中新的 [排除的網域控制站]** 索引標籤  
為了改善網域控制站涵蓋範圍計算的正確性，我們將會從計算中排除具有外部信任的網域控制站，以達到 100% 的涵蓋範圍。 排除的網域控制站會在網域涵蓋範圍 Excel 報表下載中，顯示在新的 [排除的網域控制站] 索引標籤。 如需下載報告的相關資訊，請參閱[網域控制站狀態](sensor-monitoring.md#domain-controller-status)。
- 版本包括內部感應器基礎結構的數個功能改進與錯誤 (Bug) 修正。

## <a name="azure-atp-release-2118"></a>Azure ATP 2.118 版

2020 年 6 月 28 日發行

- **新的安全性評估**  
Azure ATP 安全性評估現在包含下列新的評估：
  - **風險最高的橫向移動路徑**  
    此評定會持續監視您的環境，辨識橫向移動路徑風險最高而造成安全性風險的 **敏感性** 帳戶，並針對這些帳戶提出報告，以協助您管理環境。 若路徑有三個以上的非敏感性帳戶，可能讓惡意行動者對敏感性帳戶進行認證竊取，該路徑即視為有風險的路徑。 如需詳細資訊，請參閱[安全性評估：風險最高的橫向移動路徑 (LMP)](cas-isp-riskiest-lmp.md)。
  - **不安全的帳戶屬性**  
    此評定 Azure ATP 會持續監視您的環境，辨識屬性值會造成安全性風險的帳戶，並針對這些帳戶提出報告，以協助您保護環境。 如需詳細資訊，請參閱[安全性評估：不安全的帳戶屬性](cas-isp-unsecure-account-attributes.md)。

- **更新的敏感性定義**  
我們擴充了內部部署帳戶的敏感性定義，以納入允許使用 Active Directory 複寫的實體。

## <a name="azure-atp-release-2117"></a>Azure ATP 2.117 版

2020 年 6 月 14 日發行

- **功能增強：現已在整合 SecOps 體驗中提供其他活動的詳細資料**  
我們已擴充傳送給 Cloud App Security 的裝置資訊，包括裝置名稱、IP 位址、帳戶 UPN 和使用的連接埠。 如需與 Cloud App Security 整合的詳細資訊，請參閱[搭配 Cloud App Security 使用 Azure ATP](mcas-integration.md)。

- 版本包括內部感應器基礎結構的數個功能改進與錯誤 (Bug) 修正。

## <a name="azure-atp-release-2116"></a>Azure ATP 2.116 版

2020 年 6 月 7 日發行

- 版本包括內部感應器基礎結構的數個功能改進與錯誤 (Bug) 修正。

## <a name="azure-atp-release-2115"></a>Azure ATP 2.115 版

2020 年 5 月 31 日發行

- **新的安全性評估**  
Azure ATP 安全性評估現在包含下列新的評估：
  - **不安全的 SID History 屬性**  
    此評估會指出可讓惡意攻擊者用來存取環境的 SID History 屬性。 如需詳細資訊，請參閱[安全性評估：不安全的 SID History 屬性](cas-isp-unsecure-sid-history-attribute.md)。
  - **Microsoft LAPS 使用情況**  
    此評估會指出未使用 Microsoft「區域系統管理員密碼解決方案」(LAPS) 來保護其密碼的本機系統管理員帳戶。 使用 LAPS 可簡化密碼管理，並有助於防範網路攻擊。 如需詳細資訊，請參閱[安全性評估：Microsoft LAPS 使用情況](cas-isp-laps.md)。

- 版本包括內部感應器基礎結構的數個功能改進與錯誤 (Bug) 修正。

## <a name="azure-atp-release-2114"></a>Azure ATP 2.114 版

2020 年 5 月 17 日發行

- 版本包括內部感應器基礎結構的數個功能改進與錯誤 (Bug) 修正。

## <a name="azure-atp-release-2113"></a>Azure ATP 版本 2.113

2020 年 5 月 5 日發行

- **功能增強：豐富的 NTLMv1 資源存取活動**  
Azure ATP 從此版本開始，已提供資源存取活動的資訊，顯示該資源是否使用 NTLMv1 驗證。 這種資源設定並不安全，而且會造成惡意執行者強制應用程式執行惡意動作。 如需有關風險的詳細資訊，請參閱[使用舊版通訊協定](cas-isp-legacy-protocols.md)。

- **功能增強：可疑的暴力密碼破解攻擊 (Kerberos、NTLM) 警示**  
暴力密碼破解攻擊能讓攻擊者用來佔據您的組織，而且是在 Azure ATP 中進行威脅及風險探索的主要方法。 為協助您聚焦於使用者的重大風險，此更新可藉由限制及排序警示量，更輕鬆且快速地分析及補救風險。

## <a name="azure-atp-release-2112"></a>Azure ATP 2.112 版

發行日期：2020 年 3 月 15 日

- **新的 Azure ATP 執行個體會自動與 Microsoft Cloud App Security 整合**  
建立 Azure ATP 執行個體 (先前稱為工作區) 時，預設會啟用與 Microsoft Cloud App Security 的整合。 如需有關整合的詳細資訊，請參閱[搭配 Microsoft Cloud App Security 使用 Azure ATP](mcas-integration.md)。

- **新的受監視活動**  
現在可以使用下列活動監視器：
  - 使用憑證的互動式登入
  - 使用憑證的失敗登入
  - 委派資源存取

    深入了解 [Azure ATP 監視器](monitored-activities.md)會監視哪些活動，以及如何在入口網站中[篩選和搜尋受監視的活動](activities-search.md)。

- **功能增強：豐富的資源存取活動**  
從這個版本開始，Azure ATP 現在會提供資源存取活動的資訊，顯示是否信任該資源以進行不受限制的委派。 這種資源設定並不安全，而且會造成惡意執行者強制應用程式執行惡意動作。 如需有關風險的詳細資訊，請參閱[安全性評估：不安全的 Kerberos 委派](cas-isp-unconstrained-kerberos.md)。

- **可疑的 SMB 封包操作 (CVE-2020-0796 惡意探索) - (預覽)**  
Azure ATP [可疑的 SMB 封包操作](lateral-movement-alerts.md#suspected-smb-packet-manipulation-cve-2020-0796-exploitation-external-id-2406)安全性警示現已公開預覽。 在此偵測中，若懷疑 SMBv3 封包會對網路中的網域控制站惡意探索 [CVE-2020-0796](https://portal.msrc.microsoft.com/en-US/security-guidance/advisory/CVE-2020-0796) 安全性弱點時，即會觸發 Azure ATP 安全性警示。

## <a name="azure-atp-release-2111"></a>Azure ATP 2.111 版

發行日期：2020 年 3 月 1 日

- 版本包括內部感應器基礎結構的數個功能改進與錯誤 (Bug) 修正。

## <a name="azure-atp-release-2110"></a>Azure ATP 2.110 版

發行日期：2020 年 2 月 23 日

- **新增安全性評量：未受監視的網域控制站**  
Azure ATP 安全性評量現在包括未受監視的網域控制站 (不含感應器的伺服器) 報告，可協助您管理環境的各層面。 如需詳細資訊，請參閱[未受監視的網域控制站](cas-isp-unmonitored-domain-controller.md)。

## <a name="azure-atp-release-2109"></a>Azure ATP 2.109 版

發行日期：2020 年 2 月 16 日

- **功能增強：機密實體**  
從此版本 (2.109) 開始，由 Azure ATP 識別為憑證授權單位、DHCP 或 DNS 伺服器的機器現在會自動標記為 **機密**。

## <a name="azure-atp-release-2108"></a>Azure ATP 2.108 版

發行日期：2020 年 2 月 9 日

- **新功能：支援群組受管理的服務帳戶**  
Azure ATP 現在支援使用群組受管理的服務帳戶 (gMSA)，以在將 Azure ATP 感應器連線到您的 Azure Active Directory (AD) 樹系時獲得更好的安全性。 如需有關搭配 Azure ATP 感應器使用 gMSA 的詳細資訊，請參閱[連線到您的 Active Directory 樹系](install-step2.md#prerequisites)。

- **功能增強：具有太多資料的已排程報表**  
當已排程的報表具有太多資料時，電子郵件現在會透過顯示下列文字來通知您事實：指定期間內的資料太多，無法產生報告。 這會取代先前在電子郵件中按一下 [報告] 連結之後才探索事實的行為。

- **功能增強：已更新的網域控制站涵蓋範圍邏輯**  
我們將網域控制站涵蓋範圍報告邏輯更新成包含來自 Azure AD 的其他資訊，提升網域控制站檢視的精確度，而且去除了感應器。 這個新邏輯對對應的 Microsoft 安全分數也應該有正面的影響。

## <a name="azure-atp-release-2107"></a>Azure ATP 2.107 版

發行日期：2020 年 2 月 3 日

- **新的受監視的活動：SID 歷程記錄變更**  
SID 歷程記錄變更現在是受監視且可篩選的活動。 深入了解 [Azure ATP 監視器](monitored-activities.md)會監視哪些活動，以及如何在入口網站中[篩選和搜尋受監視的活動](activities-search.md)。

- **功能增強：不再重新開啟已關閉或隱藏的警示**  
在 Azure ATP 入口網站中關閉或隱藏警示後，如果在短時間內再次偵測到相同的活動，就會開啟新的警示。 而先前在相同的情況下，則是會重新開啟該警示。

- **入口網站存取與感應器需要 TLS 1.2**  
現在需要 TLS 1.2，才能使用 Azure ATP 感應器與雲端服務。 使用不支援 TLS 1.2 的瀏覽器標將無法再存取 Azure ATP 入口網站。

## <a name="azure-atp-release-2106"></a>Azure ATP 2.106 版

發行日期：2020 年 1 月 19 日

- 版本包括內部感應器基礎結構的數個功能改進與錯誤 (Bug) 修正。

## <a name="azure-atp-release-2105"></a>Azure ATP 2.105 版

發行日期：2020 年 1 月 12 日

- 版本包括內部感應器基礎結構的數個功能改進與錯誤 (Bug) 修正。

## <a name="azure-atp-release-2104"></a>Azure ATP 2.104 版

發行日期：2019 年 12 月 23 日

- **已消除感應器版本到期**  
Azure ATP 感應器部署及感應器安裝套件在數個版本之後已不再會到期，且現在只會自行更新一次。 此功能的結果是已可安裝先前所下載的感應器安裝套件，即使它們的版本號碼比已過期版本的最大號碼還舊。

- **確認入侵**  
您現在可以確認特定 Microsoft 365 使用者的入侵，並將他們的風險層級設定為 [高]。 此工作流程可為您的安全性作業小組提供另一個回應功能，以降低其安全性事件解決時間閾值。 深入了解如何使用 Azure ATP 和 Cloud App Security 來[確認入侵](/cloud-app-security/tutorial-ueba?branch=pr-en-us-1204#phase-4-protect-your-organization)。

- **新體驗橫幅**  
在於 Cloud App Security 入口網站中有新體驗可供使用的 Azure ATP 入口網站頁面上，會顯示描述可用內容及存取連結的新橫幅。

- 此版本還包括內部感應器基礎結構的數項功能改進與 Bug 修正。

## <a name="azure-atp-release-2103"></a>Azure ATP 2.103 版

發行日期：2019 年 12 月 15 日

- 版本包括內部感應器基礎結構的數個功能改進與錯誤 (Bug) 修正。

## <a name="azure-atp-release-2102"></a>Azure ATP 2.102 版

發行日期：2019 年 12 月 8 日

- 版本包括內部感應器基礎結構的數個功能改進與錯誤 (Bug) 修正。

## <a name="azure-atp-release-2101"></a>Azure ATP 2.101 版

發行日期：2019 年 11 月 24 日

- 版本包括內部感應器基礎結構的數個功能改進與錯誤 (Bug) 修正。

## <a name="azure-atp-release-2100"></a>Azure ATP 2.100 版

2019 年 11 月 17 日發佈

- 版本包括內部感應器基礎結構的數個功能改進與錯誤 (Bug) 修正。

## <a name="azure-atp-release-299"></a>Azure ATP 2.99 版

發行日期：2019 年 11 月 3 日

- **功能增強：為 Azure ATP 入口網站** 新增 Cloud App Security 入口網站可用性的使用者介面通知  
確保所有使用 Cloud App Security 入口網站的使用者，都能得知增強功能的發行。為入口網站新增的通知，會以現有的 Azure ATP 警示時間軸為準。

- 版本包括內部感應器基礎結構的數個功能改進與錯誤 (Bug) 修正。

## <a name="azure-atp-release-298"></a>Azure ATP 2.98 版

發行日期：2019 年 10 月 27 日

- **功能增強：可疑的暴力密碼破解攻擊警示**  
使用其他分析，改善 [可疑的暴力密碼破解攻擊 (SMB)](compromised-credentials-alerts.md#suspected-brute-force-attack-smb-external-id-2033) 警示，並且改善偵測邏輯，減少 **良性確判 (B-TP)** 與 **誤判 (FP)** 警示結果。

- 版本包括內部感應器基礎結構的數個功能改進與錯誤 (Bug) 修正。

## <a name="azure-atp-release-297"></a>Azure ATP 2.97 版

發行日期：2019 年 10 月 6 日

- 版本包括內部感應器基礎結構的數個功能改進與錯誤 (Bug) 修正。

## <a name="azure-atp-release-296"></a>Azure ATP 2.96 版

發行日期：2019 年 9 月 22 日

- **使用 Windows 事件 8004 加強的 NTLM 驗證**  
當啟用 NTLM 稽核並開啟 Windows 事件 8004 之後，Azure ATP 感應器現在可以使用您存取的伺服器資料自動讀取及加強 NTLM 驗證活動。 Azure ATP 會依序針對 NTLM 驗證剖析 Windows 事件 8004，以加強用於 Azure ATP 威脅分析與警示的 NTLM 驗證資料。 這個加強的功能提供 NTLM 資料的資源存取活動，以及加強的失敗登入活動，包括使用者嘗試存取但失敗的目的地電腦。

    [使用 Windows 事件 8004](configure-windows-event-collection.md#ntlm-authentication-using-windows-event-8004)深入了解 NTLM 驗證活動。

- 版本也包括內部感應器基礎結構的數個功能改進與錯誤 (Bug) 修正。

## <a name="azure-atp-release-295"></a>Azure ATP 2.95 版

發行日期：2019 年 9 月 15 日

- 版本包括內部感應器基礎結構的數個功能改進與錯誤 (Bug) 修正。

## <a name="azure-atp-release-294"></a>Azure ATP 2.94 版

發行日期：2019 年 9 月 8 日

- 版本包括內部感應器基礎結構的數個功能改進與錯誤 (Bug) 修正。

## <a name="azure-atp-release-293"></a>Azure ATP 2.93 版

發行日期：2019 年 9 月 1 日

- 版本包含內部感應器基礎結構的功能改進及 Bug 修正。

## <a name="azure-atp-release-292"></a>Azure ATP 2.92 版

發行日期：2019 年 8 月 25 日

- 版本包含內部感應器基礎結構的功能改進及 Bug 修正。

## <a name="azure-atp-release-291"></a>Azure ATP 2.91 版

發行日期：2019 年 8 月 18 日

- 版本包括內部感應器基礎結構的數個功能改進與錯誤 (Bug) 修正。

## <a name="azure-atp-release-290"></a>Azure ATP 2.90 版

發行日期：2019 年 8 月 11 日

- 版本包括內部感應器基礎結構的數個功能改進與錯誤 (Bug) 修正。

## <a name="azure-atp-release-289"></a>Azure ATP 2.89 版

發行日期：2019 年 8 月 4 日

- **感應器方法改善**  
為了避免在建立精確的橫向移動路徑 (LMP) 評定時產生過多 NTLM 流量，而改善了 Azure ATP 感應器方法，以降低依賴使用 NTLM 的程度，並提升 Kerberos 的使用率。

- **警示增強：可疑的黃金票證使用 (不存在的帳戶)**  
SAM 名稱變更已新增至此類型警示中所列的支援辨識項類型。 若要深入了解警示，包括如何預防此類型的活動與補救措施，請參閱[可疑的黃金票證使用 (不存在的帳戶)](domain-dominance-alerts.md#suspected-golden-ticket-usage-nonexistent-account-external-id-2027)。

- **正式運作：可疑的 NTLM 驗證竄改**  
[可疑的 NTLM 驗證竄改](lateral-movement-alerts.md#suspected-ntlm-authentication-tampering-external-id-2039)警示已不再處於預覽模式，現在已公開推出。

- 版本包括內部感應器基礎結構的數個功能改進與錯誤 (Bug) 修正。

## <a name="azure-atp-release-288"></a>Azure ATP 2.88 版

2019 年 7 月 28 日發佈

- 此版本包括內部感應器基礎結構的數項功能改進與 Bug 修正。

## <a name="azure-atp-release-287"></a>Azure ATP 2.87 版

2019 年 7 月 21 日發佈

- **功能增強：Azure ATP 獨立感應器的自動化 Syslog 事件收集**  
Azure ATP 獨立感應器的連入 Syslog 連線現在已完全自動化，同時從設定畫面中移除切換選項。 這些變更不會影響連出 Syslog 連線。

- 此版本包括內部感應器基礎結構的數項功能改進與 Bug 修正。

## <a name="azure-atp-release-286"></a>Azure ATP 2.86 版

2019 年 7 月 14 日發行

- **新的安全性警訊：可疑的 NTLM 驗證竄改 (外部識別碼 2039)**  
Azure ATP 新增[可疑的 NTLM 驗證竄改](lateral-movement-alerts.md#suspected-ntlm-authentication-tampering-external-id-2039)安全性警示，現已進入公開預覽階段。    在此偵測中，當系統懷疑有人使用「中間人」攻擊成功繞過 NTLM 訊息完整性檢查 (MIC) (Microsoft [CVE-2019-040](https://portal.msrc.microsoft.com/en-US/security-guidance/advisory/CVE-2019-1040) 中詳述的安全性弱點) 時，會觸發 Azure ATP 安全性警訊。 這些類型的攻擊會嘗試使 NTLM 安全性功能降級並成功驗證，最終目標是要進行成功的橫向移動。

- **功能增強：擴充的裝置作業系統身分識別**  
到目前為止，Azure ATP 根據 Active Directory 中的可用屬性來提供實體裝置作業系統資訊。 先前，如果 Active Directory 未提供作業系統資訊，Azure ATP 實體頁面就也無法使用該資訊。 從這個版本開始，若遇到 Active Directory 沒有資訊的裝置，或未在 Active Directory 中註冊的裝置，Azure ATP 會使用擴充的裝置作業系統身分識別方法 TCP 指紋提供此資訊。

    新增擴充裝置作業系統身分識別資料有助於識別未註冊和非 Windows 的裝置，同時在您的調查程序中提供協助。 若要深入了解 Azure ATP 中的網路名稱解析，請參閱[了解網路名稱解析 (NNR)](nnr-policy.md)。  

- **新功能：已驗證的 Proxy - 預覽**  
Azure ATP 現在支援已驗證的 Proxy。 請使用感應器命令列指定 Proxy URL，並指定使用者名稱/密碼，以使用需要驗證的 Proxy。 如需如何使用已驗證 Proxy 的詳細資訊，請參閱[設定 Proxy](configure-proxy.md)。

- **功能增強：自動網域同步器流程**  
在安裝期間將網域控制站指定及標記為候選網域同步器的流程，現在已完全自動化。 手動將網域控制站選取為候選網域同步器的切換選項已經移除。

- 此版本還包括內部感應器基礎結構的數項功能改進與 Bug 修正。

## <a name="azure-atp-release-285"></a>Azure ATP 2.85 版

發行日期：2019 年 7 月 7 日

- 此版本包括內部感應器基礎結構的數項功能改進與 Bug 修正。

## <a name="azure-atp-release-284"></a>Azure ATP 2.84 版

發行日期：2019 年 7 月 1 日

- **新增位置支援：Azure 英國資料中心**  
Azure 英國資料中心現在支援 Azure ATP 執行個體。 若要了解如何建立 Azure ATP 執行個體和其對應的資料中心位置，請參閱 [Azure ATP 安裝的步驟 1](install-step1.md)。

- **功能增強：敏感性群組的可疑新增項目警示 (外部識別碼 2024) 新名稱和功能**  
**敏感性群組的可疑新增項目** 警示先前命名為 **敏感性群的可疑修改** 警示。 警示 (識別碼 2024) 的外部識別碼保持不變。 描述性名稱變更可更精確地反映針對 **敏感性** 群組新增項目發出警示的目的。 增強型警示也強調新辨識項和改善的描述。 如需詳細資訊，請參閱[敏感性群組的可疑新增項目](domain-dominance-alerts.md#suspicious-additions-to-sensitive-groups-external-id-2024)。  

- **新文件功能：從 Advanced Threat Analytics 移至 Azure ATP 的指南**  
這篇新文章包含必要條件、規劃指引，以及從 ATA 移至 Azure ATP 服務的設定和驗證步驟。 如需詳細資訊，請參閱[從 ATA 移至 Azure ATP](migrate-from-ata-overview.md)。

- 此版本還包括內部感應器基礎結構的數項功能改進與 Bug 修正。

## <a name="azure-atp-release-283"></a>Azure ATP 2.83 版

2019 年 6 月 23 日發行

- **功能增強：可疑的服務建立警示 (外部識別碼 2026)**  
此警示現在會強調改善的警示頁面，其中含有額外的辨識項和新說明。 如需詳細資訊，請參閱[可疑的服務建立安全性警示](domain-dominance-alerts.md#suspicious-service-creation-external-id-2026)。

- **執行個體命名支援：新增支援僅限數字的網域前置詞**  
新增支援使用只包含數字的初始網域前置詞來建立 Azure ATP 執行個體。 例如，現在支援使用 123456.contoso.com 等僅限數字的初始網域前置詞。

- 此版本還包括內部感應器基礎結構的數項功能改進與 Bug 修正。

## <a name="azure-atp-release-282"></a>Azure ATP 2.82 版

發行日期：2019 年 6 月 18 日

- **新的公開預覽**  
Azure ATP 的身分識別威脅調查體驗目前處於 **公開預覽** 狀態，適用於所有受保護的 Azure ATP 租用戶。 如需深入了解，請參閱 [Azure ATP Microsoft Cloud App Security 調查體驗](mcas-integration.md)。

- **正式版本**  
Azure ATP 現已在正式版本中支援未受信任的樹系。 如果要深入了解，請參閱 [Azure ATP 多重樹系](multi-forest.md)。

- 此版本包括內部感應器基礎結構的數項功能改進與 Bug 修正。

## <a name="azure-atp-release-281"></a>Azure ATP 2.81 版

發行日期：2019 年 6 月 10 日

- 此版本包括內部感應器基礎結構的數項功能改進與 Bug 修正。

## <a name="azure-atp-release-280"></a>Azure ATP 2.80 版

發行日期：2019 年 6 月 2 日

- **功能增強：可疑 VPN 連線警示**  
此警示現在包含增強的辨識項和文字，以提供更好的使用性。 如需該警示功能，以及建議的補救步驟和預防措施的詳細資訊，請參閱[可疑 VPN 連線警示描述](compromised-credentials-alerts.md#suspicious-vpn-connection-external-id-2025)。

- 此版本還包括內部感應器基礎結構的數項功能改進與 Bug 修正。

## <a name="azure-atp-release-279"></a>Azure ATP 2.79 版

發行日期：2019 年 5 月 26 日

- **正式運作：安全性主體偵察 (LDAP) (外部識別碼 2038)**

    此警示現在已 GA (正式運作)。 如需該警示及其功能，以及建議的補救和預防措施的詳細資訊，請參閱[安全性主體偵查 (LDAP) 警示描述](reconnaissance-alerts.md#security-principal-reconnaissance-ldap-external-id-2038)

- 此版本還包括內部感應器基礎結構的數項功能改進與 Bug 修正。

## <a name="azure-atp-release-278"></a>Azure ATP 2.78 版

發行日期：2019 年 5 月 19 日

- **功能增強：機密實體**  
Exchange 伺服器的手動機密標記

    您現在可以在設定期間手動將實體標記為 Exchange Server伺服器。

    若要手動將實體標記為 Exchange 伺服器：

    1. 在 Azure ATP 入口網站中，選取 [設定]。
    2. 在 [偵測] 下，選取 [實體標記]，然後選取 [機密]。
    3. 選取 [Exchange 伺服器]，然後新增您要標記的實體。

    將某部電腦標記為 Exchange 伺服器之後，系統會將它標記為機密，並顯示它已被標記為 Exchange 伺服器。  「機密」標籤會出現在該電腦的實體設定檔中，而且所有在機密帳戶及橫向移動路徑上執行的偵測，都會仔細檢查該部電腦。

- 此版本還包括內部感應器基礎結構的數項功能改進與 Bug 修正。

## <a name="azure-atp-release-277"></a>Azure ATP 2.77 版

發行日期：2019 年 5 月 12 日

- 此版本包括內部感應器基礎結構的數項功能改進與 Bug 修正。

## <a name="azure-atp-release-276"></a>Azure ATP 2.76 版

發行日期：2019 年 5 月 6 日

- 此版本包括內部感應器基礎結構的數項功能改進與 Bug 修正。

## <a name="azure-atp-release-275"></a>Azure ATP 2.75 版

發行日期：2019 年 4 月 28 日

- **功能增強：機密實體**  
從此版本 (2.75) 開始，由 Azure ATP 識別為 Exchange Server 的機器現在會被自動標示為 **機密**。  

    因為運作方式如 Exchange Server 的清單而被自動標示為 **機密** 的實體原會列出此分類作為其被標示的原因。

- 此版本包括內部感應器基礎結構的數項功能改進與 Bug 修正。

## <a name="azure-atp-release-274"></a>Azure ATP 2.74 版

將於 2019 年 4 月 14 日發佈

- 此版本包括內部感應器基礎結構的數項功能改進與 Bug 修正。

## <a name="azure-atp-release-273"></a>Azure ATP 2.73 版

發行日期：2019 年 4 月 10 日

- 此版本包括內部感應器基礎結構的數項功能改進與 Bug 修正。

## <a name="azure-atp-release-272"></a>Azure ATP 2.72 版

發行日期：2019 年 3 月 31 日

- **功能增強：橫向移動路徑 (LMP) 限域深度**  
橫向移動路徑 (LMP) 為 Azure ATP 探索威脅和風險的重要方法。 為了讓您可以專注在針對您最敏感使用者的重大風險上，此更新能限制所顯示之每個圖表的範圍和深度，使您能以更輕鬆且快速的方式分析並補救每個 LMP 上之敏感性使用者的風險。

    請參閱[橫向移動路徑](use-case-lateral-movement-path.md)以深入了解 Azure ATP 如何使用 LMP 來呈現針對您環境中每個實體的存取風險。

- 此版本還包括內部感應器基礎結構的數項功能改進與 Bug 修正。

## <a name="azure-atp-release-271"></a>Azure ATP 2.71 版

發行日期：2019 年 3 月 24 日

- **功能增強：網路名稱解析 (NNR) 健康情況警示**  
已根據 NNR 針對與 Azure ATP 安全性警訊關聯的信賴等級新增健康情況警示。 每個健康情況警示都包括可採取的動作與詳細建議，可協助解決低 NNR 成功率問題。

    請參閱[什麼是網路名稱解析](nnr-policy.md)以深入了解 Azure ATP 如何使用 NNR 以及它對警示精確度而言為何很重要。

- **Server 支援：我們透過 KB4487044 新對 Server 2019 的支援**  
我們透過 KB4487044 的修補層級新增對使用 Windows Server 2019 的支援。 不支援在不安裝該補充程式的情況下使用 Server 2019，而且也無法安裝此更新。

- **功能增強：以使用者為基礎的警示排除**  
延伸警示排除選項現在允許將特定使用者從特定警示排除。 排除有助於避免使用或設定特定內部軟體類型重複觸發良性安全性警訊的情況。

- 此版本還包括內部感應器基礎結構的數項功能改進與 Bug 修正。

## <a name="azure-atp-release-270"></a>Azure ATP 2.70 版

發行日期：2019 年 3 月 17 日

- **功能增強：網路名稱解析 (NNR) 信賴等級已新增至多重警示**  網路名稱解析 (或稱 NNR) 可用來協助主動識別可疑攻擊的來源實體身分識別。 您現在只要將 NNR 信賴等級新增至 Azure ATP 警示辨識項清單，就能立即針對已識別之可能來源的相關 NNR 信賴等級進行評估與了解，並適當地進行補救。

    已將 NNR 信賴等級辨識項新增至下列警示：
  - [網路對應偵察 (DNS)](reconnaissance-alerts.md#network-mapping-reconnaissance-dns-external-id-2007)
  - [可疑的身分識別竊取 (票證傳遞)](lateral-movement-alerts.md#suspected-identity-theft-pass-the-ticket-external-id-2018)
  - [可疑的 NTLM 轉送攻擊 (Exchange 帳戶) - 預覽](lateral-movement-alerts.md#suspected-ntlm-relay-attack-exchange-account-external-id-2037)
  - [可疑的 DCSync 攻擊 (目錄服務的複寫)](domain-dominance-alerts.md#suspected-dcsync-attack-replication-of-directory-services-external-id-2006)

- **其他健全狀況警示案例：Azure ATP 感應器服務無法啟動**  
目前假如因為網路擷取驅動程式發生問題，導致 Azure ATP 感應器無法啟動，便會觸發感應器健全狀況警示。 如需關於 Azure ATP 記錄及如何使用的詳細資訊，請參閱[使用 Azure ATP 記錄針對 Azure ATP 進行疑難排解](troubleshooting-using-logs.md)。

- 此版本還包括內部感應器基礎結構的數項功能改進與 Bug 修正。

## <a name="azure-atp-release-269"></a>Azure ATP 2.69 版

發行日期：2019 年 3 月 10 日

- **功能增強：可疑身分盜用 (票證傳遞) 警示**   此警示現可提供新的辨識項，來顯示使用遠端桌面通訊協定 (RDP) 所進行之連線的詳細資料。 新增的辨識項可供您輕鬆補救因透過 RDP 連線使用 Remote Credential Guard 而造成的已知良性確判 (B-TP) 警訊問題。

- **功能增強：透過 DNS 執行遠端程式碼警訊**  
此警訊現可提供新的辨識項，來顯示您網域控制站安全性更新的狀態，及通知您何時需要更新。

- **新文件功能：Azure ATP 安全性警示 MITRE ATT&CK Matrix&trade;**  
為了說明及讓您更輕鬆地對應 Azure ATP 安全性警訊及所熟悉 MITRE ATT&CK Matrix 之間的關聯性，我們將相關的 MITRE 技術新增到了 Azure ATP 安全性警訊清單。 這項新增的參考可供您更輕鬆地了解觸發 Azure ATP 安全性警訊時，可能使用的可疑攻擊技術。 深入了解 [Azure ATP 安全性警訊指南](suspicious-activity-guide.md)。  

- 此版本還包括內部感應器基礎結構的數項功能改進與 Bug 修正。

## <a name="azure-atp-release-268"></a>Azure ATP 2.68 版

發行日期：2019 年 3 月 3 日

- **功能增強：可疑的暴力密碼破解攻擊 (LDAP) 警示**  
針對此安全性警示，已進行大幅的可用性改進，包括已修訂的描述、額外來源資訊的佈建，以及可加速進行補救的猜測嘗試詳細資料。  
深入了解[可疑的暴力密碼破解攻擊 (LDAP)](compromised-credentials-alerts.md#suspected-brute-force-attack-ldap-external-id-2004) 安全性警示。

- **新文件功能：安全性警示實驗室**  
為了說明 Azure ATP 對您工作環境之真實威脅的強大偵測能力，我們已為此文件新增了新的 **安全性警示實驗室**。 **安全性警示實驗室** 可協助您快速設定實驗室或測試環境，並說明可抵禦常見、真實世界威脅和攻擊的最佳防禦姿態。  

    [逐步執行實驗室](playbook-lab-overview.md)的設計目的是要確保您花費最少的時間進行建置，而將較多時間用在了解您的威脅局勢，以及可用的 Azure ATP 警示和防護。 我們很樂意收到您的意見反應。

- 此版本還包括內部感應器基礎結構的數項功能改進與 Bug 修正。

## <a name="azure-atp-release-267"></a>Azure ATP 2.67 版

發行日期：2019 年 2 月 24 日

- **新的安全性警訊：安全性主體偵察 (LDAP) - (預覽)**  
Azure ATP 之 [安全性主體偵察 (LDAP) - 預覽](reconnaissance-alerts.md#security-principal-reconnaissance-ldap-external-id-2038)安全性警示現已進入公開預覽階段。    在此偵測中，當攻擊者使用安全性主體偵察來取得有關網域環境的重要資訊時，會觸發 Azure ATP 安全性警示。 此資訊可協助攻擊者對應網域結構以及識別具特殊權限帳戶以便在其攻擊擊殺鏈中的後續步驟中使用。

    輕量型目錄存取通訊協定 (LDAP) 是同時用於合法與惡意目的來查詢 Active Directory 的最熱門的方法之一。 專注在 LDAP 的安全性主體偵察通常用於 Kerberoasting 攻擊的第一個階段。 Kerberoasting 攻擊是用於取得目標安全性主體名稱 (SPN) 清單，接著攻擊者會嘗試為其取得票證授權伺服器 (TGS) 憑證。

- **功能增強：帳戶列舉偵察 (NTLM) 警示**  
改進的 **帳戶列舉偵察 (NTLM)** 警示 (使用額外分析)，以及改進的偵測邏輯以減少 **B-TP** 與 **FP** 警示結果。

- **功能增強：網路對應偵察 (DNS) 警示**  
新的偵測類型已新增到網路對應偵察 (DNS) 警示。 除了偵測可疑的 AXFR 要求之外，Azure ATP 現在也會偵測源自非 DNS 伺服器且使用過量要求的可疑要求類型。

- 此版本還包括內部感應器基礎結構的數項功能改進與 Bug 修正。

## <a name="azure-atp-release-266"></a>Azure ATP 2.66 版

發行日期：2019 年 2 月 17 日

- **功能增強：可疑的 DCSync 攻擊 (目錄服務的複寫) 警示**  
已針對此安全性警示進行使用方面性的改進，包括已修正的描述、佈建額外的來源資訊、新資訊圖表與更多辨識項。
深入了解[可疑 DCSync 攻擊 (目錄服務的複寫)](domain-dominance-alerts.md#suspected-dcsync-attack-replication-of-directory-services-external-id-2006) 安全性警示。

- 此版本還包括內部感應器基礎結構的數項功能改進與 Bug 修正。

## <a name="azure-atp-release-265"></a>Azure ATP 2.65 版

發行日期：2019 年 2 月 10 日

- **新的安全性警訊：可疑的 NTLM 轉送攻擊 (Exchange 帳戶) – (預覽)**  
Azure ATP 之[可疑的 NTLM 轉送攻擊 (Exchange 帳戶) - 預覽](lateral-movement-alerts.md#suspected-ntlm-relay-attack-exchange-account-external-id-2037)安全性警示現已進入公開預覽階段。    在此偵測中，當識別到可疑來源使用 Exchange 帳戶認證時，便會觸發 Azure ATP 安全性警訊。 這些攻擊類型會嘗試利用 NTLM 轉送技術來取得網域控制站交換權限，又稱為 **ExchangePriv**。 若要深入了解 **ExchangePriv** 技術，請參閱最早於 2019 年 1 月 31 日發佈的 [ADV190007 公告](https://portal.msrc.microsoft.com/en-US/security-guidance/advisory/ADV190007)，以及 [Azure ATP 警示回應](https://techcommunity.microsoft.com/t5/Enterprise-Mobility-Security/How-to-win-the-latest-security-race-over-NTLM-relay/ba-p/334511) \(英文\)。  

- **正式運作：透過 DNS 執行遠端程式碼**  
此警示現在已 GA (正式運作)。 如需詳細資訊與警示功能，請參閱[透過 DNS 執行遠端程式碼警示描述頁面](lateral-movement-alerts.md#remote-code-execution-over-dns-external-id-2036)。

- **正式運作：SMB 上的資料外流**  
此警示現在已 GA (正式運作)。 如需詳細資訊與警示功能，請參閱[透過 SMB 的資料外流警示頁面](exfiltration-alerts.md#data-exfiltration-over-smb-external-id-2030)。

- 此版本還包括內部感應器基礎結構的數項功能改進與 Bug 修正。

## <a name="azure-atp-release-264"></a>Azure ATP 2.64 版

2019 年 2 月 4 日發行

- **正式運作：可疑的黃金票證使用 (票證異常)**  
此警示現在已 GA (正式運作)。 如需詳細資訊與警示功能，請參閱[可疑的黃金票證使用 (票證異常) 警示描述頁面](domain-dominance-alerts.md#suspected-golden-ticket-usage-ticket-anomaly-external-id-2032)。

- **功能增強：網路對應偵察 (DNS)**  
改善針對此警示部署的警示偵測邏輯，將誤判和警示干擾降至最低。 此警示在第一次可能觸發之前，有 8 天的學習期間。 如需此警示的詳細資訊，請參閱[網路對應偵察 (DNS) 警示描述頁面](reconnaissance-alerts.md#network-mapping-reconnaissance-dns-external-id-2007)。

    **由於此警示的增強功能，所以 nslookup 方法不應再用來於初始設定期間測試 Azure ATP 連線。**

- **功能增強：**  
此版本包含重新設計的警示頁面以及新的辨識項，提供更佳的警示調查。
  - [可疑的暴力密碼破解攻擊 (SMB)](compromised-credentials-alerts.md#suspected-brute-force-attack-smb-external-id-2033)
  - [可疑的黃金票證使用 (時間異常) 警示描述頁面](domain-dominance-alerts.md#suspected-golden-ticket-usage-time-anomaly-external-id-2022)
  - [可疑的 Overpass-the-Hash 攻擊 (Kerberos)](lateral-movement-alerts.md#suspected-overpass-the-hash-attack-kerberos-external-id-2002)
  - [可疑的 Metasploit 入侵架構使用](compromised-credentials-alerts.md#suspected-use-of-metasploit-hacking-framework-external-id-2034)
  - [可疑的 WannaCry 勒索軟體攻擊](compromised-credentials-alerts.md#suspected-wannacry-ransomware-attack-external-id-2035)

- 此版本還包括內部感應器基礎結構的數項功能改進與 Bug 修正。

## <a name="azure-atp-release-263"></a>Azure ATP 2.63 版

發行日期：2019 年 1 月 27 日

- **新功能：不信任的樹系支援 - (預覽)**  
Azure ATP 支援不信任樹系中的感應器功能現已進入公開預覽階段。
從 Azure ATP 入口網站 [目錄服務] 頁面設定額外一組認證，讓 Azure ATP 感應器能連線至不同 Active Directory 樹系，以及回報給 Azure ATP 服務。 如果要深入了解，請參閱 [Azure ATP 多重樹系](multi-forest.md)。

- **新功能：網域控制站涵蓋範圍**  
Azure ATP 現在會提供 Azure ATP 監視網域控制站的涵蓋範圍資訊。  
從 Azure ATP 入口網站 [感應器] 頁面，檢視 Azure ATP 在您環境中偵測到的受監視與未受監視網域控制站數。 下載受監視網域控制站清單以利進一步分析，以及建置行動計劃。 如果要深入了解，請參閱[網域控制站監視](sensor-monitoring.md)操作指南。

- **功能增強：帳戶列舉偵察**  
Azure ATP 帳戶列舉偵察偵測現在會偵測使用 Kerberos 和 NTLM 的列舉嘗試，並據此發出警示。 偵測在之前僅適用於使用 Kerberos 的嘗試。 如果要深入了解，請參閱 [Azure ATP 偵查警示](reconnaissance-alerts.md#account-enumeration-reconnaissance-external-id-2003)。

- **功能增強：遠端程式碼執行嘗試警示**
  - 服務建立、WMI 執行和新的 **PowerShell** 執行等所有遠端執行活動，均已新增至目的地電腦的設定檔時間軸。 目的地電腦是命令執行所在的網域控制站。
  - **PowerShell** 執行已新增至遠端程式碼執行活動的清單中，該清單列在實體設定檔警示時間軸內。
  - 如果要深入了解，請參閱[修復遠端程式碼執行嘗試](domain-dominance-alerts.md#remote-code-execution-attempt-external-id-2019)。  

- **Windows Server 2019 LSASS 問題和 Azure ATP**  
為了回應客戶對於搭配執行 Windows Server 2019 之網域控制站使用 Azure ATP 所提出的意見反應，此更新包含了額外的邏輯，可避免在 Windows Server 2019 電腦上觸發回報的行為。 雖然我們規劃在之後的 Azure ATP 更新中為 Windows Server 2019 推出完整的 Azure ATP 感應器支援，但目前並 **不** 支援在 Windows Servers 2019 上安裝和執行 Azure ATP。 如果要深入了解，請參閱 [Azure ATP 感應器需求](prerequisites.md#azure-atp-sensor-requirements)。

- 此版本還包括內部感應器基礎結構的數項功能改進與 Bug 修正。

## <a name="azure-atp-release-262"></a>Azure ATP 2.62 版

發行日期：2019 年 1 月 20 日

- **新的安全性警訊：透過 DNS 執行遠端程式碼 - (預覽)**  
Azure ATP 之[透過 DNS 執行遠端程式碼](lateral-movement-alerts.md#remote-code-execution-over-dns-external-id-2036)安全性警示現已進入公開預覽階段。    在此偵測中，當 DNS 查詢可能利用安全性弱點 [CVE-2018-8626](https://portal.msrc.microsoft.com/en-US/security-guidance/advisory/CVE-2018-8626) 對網路中的網域控制站發動攻擊時，會觸發 Azure ATP 安全性警示。

- **功能增強：感應器更新延遲 72 小時**  
變更選項使所選感應器的感應器更新，於每次 Azure ATP 更新推出之後延遲 72 小時 (而不是先前延遲 24 小時)。 如需設定指示，請參閱 [Azure ATP 感應器更新](sensor-update.md)。

- 此版本還包括內部感應器基礎結構的數項功能改進與 Bug 修正。

## <a name="azure-atp-release-261"></a>Azure ATP 2.61 版

發行日期：2019 年 1 月 13 日

- **新的安全性警示：SMB 上的資料外洩 - (預覽)**  
Azure ATP 之[透過 SMB 資料外流](exfiltration-alerts.md)安全性警示現為公開預覽狀態。 具有網域系統管理員權限的攻擊者可能會危害 KRBTGT 帳戶。 攻擊者可使用 KRBTGT 帳戶，建立可提供任何資源授權的 Kerberos 票證授權票證 (TGT)。

- **功能增強：遠端程式碼執行嘗試** 安全性警訊  
新增警訊描述及其他辨識項，讓您能更容易了解警訊，且提供了更好的調查工作流程。

- **功能增強：DNS 查詢邏輯活動**  
將其他查詢類型新增到 [Azure ATP 受監視的活動](monitored-activities.md)，其中包含：**TXT**、**MX**、**NS**、**SRV**、**ANY**、**DNSKEY**。

- **功能增強：可疑的黃金票證使用方式 (票證異常) 及可疑的黃金票證使用方式 (不存在的帳戶)**  
改善的偵測邏輯皆已套用到兩個警訊中，以降低 FP 警訊的數目，進而傳遞更準確的結果。

- **功能增強：Azure ATP 安全性警訊文件**  
Azure ATP 安全性警訊文件已增強並擴充，現在其中包含更優異的警訊描述、更準確的警訊分級，以及辨識項、修復和防護的解說。 使用以下連結熟悉全新安全性警訊文件的設計：
  - [Azure ATP 安全性警訊](suspicious-activity-guide.md)
  - [了解安全性警訊](understanding-security-alerts.md)
    - [偵察階段警訊](reconnaissance-alerts.md)
    - [遭入侵的認證階段警示](compromised-credentials-alerts.md)
    - [橫向移動階段警示](lateral-movement-alerts.md)
    - [網域支配階段警示](domain-dominance-alerts.md)
    - [外洩階段警訊](exfiltration-alerts.md)
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

- **安全性警示增強功能：不尋常的通訊協定實作警示分割**  
「不尋常通訊協定實作」安全性警訊的 Azure ATP 系列先前共用 1 個 externalId (2002)，現在則分割為四個不同的警訊，且每個都含有對應的唯一外部識別碼。

### <a name="new-alert-externalids"></a>新的警示 externalId

> [!div class="mx-tableFixed"]
> |新安全性警訊名稱|舊安全性警訊名稱|唯一外部識別碼|
> |---------|----------|---------|
> |可疑的暴力密碼破解攻擊 (SMB)|不尋常的通訊協定實作 (可能使用 Hydra 等惡意工具)|2033
> |可疑的 Overpass-the-Hash 攻擊 (Kerberos)|不尋常的 Kerberos 通訊協定實作 (可能為 Overpass-the-Hash 攻擊)|2002|
> |可疑的 Metasploit 入侵架構使用|不尋常的通訊協定實作 (可能使用 Metasploit 入侵工具)|2034
> |可疑的 WannaCry 勒索軟體攻擊|不尋常的通訊協定實作 (可能為 WannaCry 勒索軟體攻擊)|2035
> |

- **新的受監視的活動：透過 SMB 的檔案複製**  
使用 SMB 複製檔案現在是受監視且可篩選的活動。 深入了解 [Azure ATP 監視器](monitored-activities.md)會監視哪些活動，以及如何在入口網站中[篩選和搜尋受監視的活動](activities-search.md)。

- **大型橫向移動路徑映像增強功能**  
在檢視大型橫向移動路徑時，Azure ATP 現在只會將連線到選取之實體的節點醒目提示，而不會將其他節點模糊處理。 這項變更可大幅提升大型 LMP 轉譯的速度。

- 此版本包括內部感應器基礎結構的數項功能改進與 Bug 修正。

## <a name="azure-atp-release-257"></a>Azure ATP 2.57 版

發行日期：2018 年 12 月 2 日

- **新的安全性警示：可疑的黃金票證使用 - 票證異常 (預覽)**  
Azure ATP 之[可疑的 Golden Ticket 使用 - 票證異常](suspicious-activity-guide.md)安全性警示現已進入公開預覽階段。    具有網域系統管理員權限的攻擊者可能會危害 KRBTGT 帳戶。 攻擊者可使用 KRBTGT 帳戶，建立可提供任何資源授權的 Kerberos 票證授權票證 (TGT)。

    因為這種偽造的 TGT 可以讓攻擊者獲得持久的網路持續性，所以稱為「黃金票證」。 此全新偵測設計用來識別這類偽造黃金票證擁有的唯一特性。

- **功能增強：自動化建立 Azure ATP 執行個體 (工作區)**  
即日起，Azure ATP「工作區」已重新命名為 Azure ATP「執行個體」。 Azure ATP 現在支援每個 Azure ATP 帳戶一個 Azure ATP 執行個體。 新客戶的執行個體會使用 [Azure ATP 入口網站](https://portal.atp.azure.com)中的執行個體建立精靈來建立。 現有的 Azure ATP 工作區會自動轉換成具備更新的 Azure ATP 執行個體。  

  - 使用[建立您的 Azure ATP 執行個體](install-step1.md)來簡化執行個體建立，以進行更快速的部署和保護。
  - 所有[資料隱私權與合規性](privacy-compliance.md)皆維持不變。

  若要深入了解 Azure ATP 執行個體，請參閱[建立您的 Azure ATP 執行個體](install-step1.md)。

- 此版本包括內部感應器基礎結構的數項功能改進與 Bug 修正。

## <a name="azure-atp-release-256"></a>Azure ATP 2.56 版

發行日期：2018 年 11 月 25 日

- **功能增強：橫向移動路徑 (LMP)**  
已新增兩個其他功能來加強 Azure ATP 橫向移動路徑 (LMP) 功能：

  - 使用 LMP 報表時，現在可以根據每個實體儲存及探索 LMP 歷程記錄。
  - 透過活動時間表追蹤 LMP 中的實體，並使用提供的額外辨識項來探索潛在的攻擊路徑。

  請參閱 [Azure ATP 橫向移動路徑](use-case-lateral-movement-path.md)以深入了解使用及利用增強 LMP 進行調查的方式。

- **文件增強：橫向移動路徑、安全性警示名稱**  
已對 Azure ATP 文章進行新增與更新，其包括橫向移動路徑的描述及功能說明，並且已為所有舊安全性警訊名稱新增新名稱和 externalId 的名稱對應。
  - 請參閱 [Azure ATP 橫向移動路徑](use-case-lateral-movement-path.md)、[調查橫向移動路徑](investigate-lateral-movement-path.md)，以及[安全性警訊指南](suspicious-activity-guide.md)以深入了解。

- 此版本包括內部感應器基礎結構的數項功能改進與 Bug 修正。

如需 2.55 版 (包含 2.55 版) 之前每個 [!INCLUDE [Product short](includes/product-short.md)] 版本的詳細資料，請參閱 [[!INCLUDE [Product short](includes/product-short.md)] 版本參考](release-reference.md)。

## <a name="see-also"></a>另請參閱

- [什麼是 [!INCLUDE [Product long](includes/product-long.md)]？](what-is.md)
- [常見問題集](technical-faq.md)
- [[!INCLUDE [Product short](includes/product-short.md)] 先決條件](prerequisites.md)
- [[!INCLUDE [Product short](includes/product-short.md)] 容量規畫](capacity-planning.md)
- [查看[!INCLUDE [Product short](includes/product-short.md)] 論壇！](https://aka.ms/MDIcommunity)\(英文\)
