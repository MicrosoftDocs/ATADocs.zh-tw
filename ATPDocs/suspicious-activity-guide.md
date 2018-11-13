---
title: Azure ATP 安全性警訊指南 | Microsoft Docs
d|Description: This article provides a list of the security alerts issued by Azure ATP and steps for remediation.
keywords: ''
author: mlottner
ms.author: mlottner
manager: mbaldwin
ms.date: 10/28/2018
ms.topic: conceptual
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: ca5d1c7b-11a9-4df3-84a5-f53feaf6e561
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: daeb998f6e97bc4ebdf290d4430fec8fcef40313
ms.sourcegitcommit: 03b1949beaf2f78a3cdf9396356a96488ea2e127
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/05/2018
ms.locfileid: "50983152"
---
適用於：Azure 進階威脅防護


# <a name="azure-advanced-threat-protection-security-alert-guide"></a>Azure 進階威脅防護安全性警訊指南

在適當的調查之後，所有 Azure ATP 安全性警訊可分類為：

-   **真肯定**︰由 Azure ATP 所偵測到的惡意動作。

-   **良性真肯定**︰由 Azure ATP 所偵測到的真實且非惡意動作，例如滲透測試。

-   **誤判**：假警示，表示活動並未發生。

如需如何使用 Azure ATP 安全性警訊的詳細資訊，請參閱[使用安全性警訊](working-with-suspicious-activities.md)。




## <a name="brute-force-attack-using-ldap-simple-bind"></a>使用 LDAP 簡單繫結的暴力密碼破解攻擊

**描述**

>[!NOTE]
> **可疑的驗證失敗**與此偵測的主要差異，是 Azure ATP 在此偵測中可判斷不同的密碼是否已在使用中。

在暴力密碼破解攻擊中，攻擊者會嘗試使用許多不同的密碼對不同的帳戶進行驗證，直到找到至少一個帳戶的正確密碼。 找到後，攻擊者就可以使用該帳戶登入。

在此偵測中，當 Azure ATP 偵測到大量的簡單繫結驗證時，便會觸發警示。 這可能是在許多使用者之間「水平」使用少量密碼、只對一些使用者「垂直」使用大量密碼，或這兩個選項的任意組合。

**調查**

1. 如果有許多相關帳戶，請按一下 [下載詳細資料] 以檢視 Excel 試算表中的清單。

2. 按一下警示以移至其專用頁面。 檢查是否有任何登入嘗試已結束且成功驗證。 這些嘗試會顯示為資訊圖表右邊的**猜對的帳戶**。 如果是，平常是否從來源電腦使用任何**猜對的帳戶**？ 如果是，請**隱藏**可疑活動。

3. 如果沒有**猜對的帳戶**，平常是否從來源電腦使用任何**受攻擊的帳戶**？ 如果是，請**隱藏**可疑活動。

**補救**

[複雜且很長的密碼](https://docs.microsoft.com/windows/device-security/security-policy-settings/password-policy)提供必要的第一層安全性，以防止暴力密碼破解攻擊。

## <a name="encryption-downgrade-activity"></a>加密降級活動

**描述**

加密降級是一種減弱 Kerberos 的方法，它會針對通訊協定通常會以最高加密層級進行加密的不同欄位，對其加密層級做出降級。 攻擊者將能較為輕鬆地對減弱的加密欄位進行離線暴力密碼破解。 利用弱式 Kerberos 加密 Cypher 的各種攻擊方法。 在此偵測中，Azure ATP 會了解電腦和使用者所使用的 Kerberos 加密類型，並在使用下列較弱的 Cypher 時向您發出警示：(1) 對來源電腦及/或使用者而言不尋常，以及 (2) 符合已知的攻擊手法。

有三種偵測類型：

1.  基本架構金鑰 - 這是在網域控制站上執行的惡意程式碼，允許在不知道帳戶密碼的情況下，使用任何帳戶向網域進行驗證。 此惡意程式碼通常會使用較弱的加密演算法，來推測出網域控制站上的使用者密碼。 在此偵測中，相較於先前學到的行為，從網域控制站向帳戶要求票證的 KRB_ERR 訊息加密方法已降級。

2.  黃金票證 - 在[黃金票證](#golden-ticket)警示中，相較於先前學到的行為，來自來源電腦的 TGS_REQ (服務要求) 訊息的 TGT 欄位加密方法已降級。 這不是依據時間異常偵測 (如同其他黃金票證偵測)。 此外，沒有 Kerberos 驗證要求與先前由 ATP 偵測到的服務要求相關聯。

3.  Overpass-the-Hash - 攻擊者可以透過 Kerberos AS 要求，使用竊取的弱式雜湊建立強式票證。 在此偵測中，相較於先前學到的行為 (亦即電腦使用 AES)，來自來源電腦的 AS_REQ 訊息加密類型已降級。

**調查**

先查看警示的描述，以了解您處理的是上述三種偵測類型的哪一種。 如需詳細資訊，請下載 Excel 試算表。

1.  基本架構金鑰 - 您可以使用 [Azure ATP 小組所撰寫的掃描程式](https://gallery.technet.microsoft.com/Aorato-Skeleton-Key-24e46b73) \(英文\)，來檢查基本架構金鑰是否已影響到您的網域控制站。 如果掃描程式在一或多個網域控制站上找到惡意程式碼，則為真肯定。

2.  黃金票證 - 在 Excel 試算表中，移至 [網路活動] 索引標籤。相關的降級欄位為 [要求票證加密類型]，且 [來源電腦支援的加密類型] 有更強的加密方法。

  1. 檢查那些票證所存取的資源，如果有所有票證都會存取的資源，請驗證該資源以確定它是票證應存取的有效資源。 此外，請驗證目標資源是否支援強式加密方法。 您可以透過在 Active Directory 中檢查資源服務帳戶的 msDS-SupportedEncryptionTypes 屬性來檢查這點。
  
  2. 請檢查來源電腦和帳戶，或如果有多個來源電腦和帳戶，檢查它們是否有共通的某些項目。 例如，您所有的行銷人員是否使用可能觸發警示的特定應用程式。 在某些情況下，可能會有很少使用的自訂應用程式，正在使用較低的加密編碼器進行驗證。 檢查來源電腦上是否有任何這類自訂應用程式。 如果是，則可能是良性真肯定，因此可予以隱藏。
  


3.  Overpass-the-Hash - 在 Excel 試算表中，移至 [網路活動] 索引標籤。您會看到相關的降級欄位為 [加密時間戳記加密類型]，且 [來源電腦支援的加密類型] 包含更強的加密方法。

  1. 如果最近有變更智慧卡設定，則使用者在使用智慧卡登入時可能會觸發此警示。 檢查相關帳戶是否有類似的變更。 如果是，這可能是良性真肯定，因此可予以隱藏。
  2. 檢查那些票證所存取的資源，如果有所有票證都會存取的資源，請驗證該資源以確定它是票證應存取的有效資源。 此外，請驗證目標資源是否支援強式加密方法。 您可以透過在 Active Directory 中檢查資源服務帳戶的 msDS-SupportedEncryptionTypes 屬性來檢查這點。

**補救**

1.  基本架構金鑰 - 移除惡意程式碼。 如需詳細資訊，請參閱[基本架構金鑰惡意程式碼分析](https://www.virusbulletin.com/virusbulletin/2016/01/paper-digital-bian-lian-face-changing-skeleton-key-malware) \(英文\)。

2.  黃金票證 - 遵循[黃金票證](#golden-ticket)可疑活動的指示。   
    此外，由於建立黃金票證需要網域管理員權限，因此請實作 [雜湊傳遞建議](https://www.microsoft.com/download/details.aspx?id=36036)。

3.  越過雜湊 - 如果相關帳戶不是敏感性帳戶，請重設該帳戶的密碼。 這可防止攻擊者從密碼雜湊建立新的 Kerberos 票證，但現有票證在過期前仍可使用。 如果是敏感性帳戶，您應該考慮重設 KRBTGT 帳戶兩次，如黃金票證可疑活動中所示。 重設 KRBTGT 兩次會使此網域中的所有 Kerberos 票證失效，因此請事先規劃再這麼做。 請參閱 [KRBTGT Account Password Reset Scripts now available for customers](https://blogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/) (客戶現在可以使用 KRBTGT 帳戶密碼重設指令碼) 中的指導方針。 另請參閱並使用  [Reset the KRBTGT account password/keys tool](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51) (重設 KRBTGT 帳戶密碼/金鑰工具)。 由於這是橫向移動攻擊手法，因此請遵循[傳遞雜湊建議](https://www.microsoft.com/download/details.aspx?id=36036)的最佳做法。

## <a name="honeytoken-activity"></a>Honeytoken 活動


**描述**

Honeytoken 帳戶是假帳戶，可設定來識別和追蹤與這些帳戶相關的惡意活動。 Honeytoken 帳戶應保留未使用，同時擁有具吸引力的名稱來引誘攻擊者 (例如 SQL-Admin)。 任何來自這些帳戶的活動可能表示惡意行為。

如需 Honeytoken 帳戶的詳細資訊，請參閱[安裝 Azure ATP - 步驟 7](install-atp-step7.md)。

**調查**

1.  使用可疑活動頁面中所述的方法 (例如 Kerberos、LDAP、NTLM)，檢查來源電腦的擁有者是否使用 Honeytoken 帳戶進行驗證。

2.  瀏覽至來源電腦設定檔頁面，並檢查其中已驗證哪些其他帳戶。 與這些帳戶的擁有者確認他們是否使用 Honeytoken 帳戶。

3.  這可能是非互動式登入，因此請務必檢查來源電腦上是否有應用程式或指令碼正在執行。

如果在執行步驟 1 到 3 之後，沒有證據指出這是良性用途，則假設這是惡意的。

**補救**

請確定 Honeytoken 帳戶只會用於其預期用途，否則可能會產生許多警示。

## <a name="identity-theft-using-pass-the-hash-attack"></a>使用傳遞雜湊攻擊竊取身分

**描述**

傳遞票證是一種橫向移動攻擊手法，在此攻擊中，攻擊者從一部電腦竊取使用者的 NTLM 雜湊，然後使用它來存取另一部電腦。 

**調查**

調查雜湊是否來自目標使用者所擁有或定期使用的電腦？ 如果是，則為誤判；否則，可能是真的有問題。

**補救**

1. 如果相關帳戶不是敏感性帳戶，請重設該帳戶的密碼。 這可防止攻擊者從密碼雜湊建立新的 Kerberos 票證，但現有票證在過期前仍可使用。 

2. 如果是敏感性帳戶，您應該考慮重設 KRBTGT 帳戶兩次，如黃金票證可疑活動中所示。 重設 KRBTGT 兩次會使此網域中的所有 Kerberos 票證失效，因此請事先規劃再這麼做。 請參閱 [KRBTGT Account Password Reset Scripts now available for customers](https://blogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/) (客戶現在可以使用 KRBTGT 帳戶密碼重設指令碼) 中的指導方針，另請參閱如何使用  [Reset the KRBTGT account password/keys tool](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51) (重設 KRBTGT 帳戶密碼/金鑰工具)。 由於這是橫向移動攻擊手法，因此請遵循[傳遞雜湊建議](https://www.microsoft.com/download/details.aspx?id=36036)的最佳做法。

## <a name="identity-theft-using-pass-the-ticket-attack"></a>使用傳遞票證攻擊竊取身分

**描述**

傳遞票證是一種橫向移動攻擊手法，在此攻擊中，攻擊者從一部電腦竊取 Kerberos 票證，並重複使用竊取的票證來存取另一部電腦。 在此偵測中，會看到 Kerberos 票證用於兩部 (或多部) 不同的電腦。

**調查**

1. 按一下 [下載詳細資料] 按鈕，以檢視相關 IP 位址的完整清單。 一或兩部電腦的 IP 位址是否屬於從過小 DHCP 集區配置的子網路，例如 VPN 或 WiFi？ 是否共用 IP 位址？ 例如，透過 NAT 裝置？ 是否有一或多個來源 IP 位址沒有由感應器解析？ (這可能代表感應器針對裝置應開啟的連接埠未正確開啟)。如果上述任何問題的答案為是，則為誤判。

2. 是否有自訂應用程式代表使用者轉送票證？ 如果是，則為良性真肯定。

**補救**

1. 如果相關帳戶不是敏感性帳戶，請重設該帳戶的密碼。 這可防止攻擊者從密碼雜湊建立新的 Kerberos 票證，但現有票證在過期前仍可使用。  

2. 如果是敏感性帳戶，您應該考慮重設 KRBTGT 帳戶兩次，如黃金票證可疑活動中所示。 重設 KRBTGT 兩次會使此網域中的所有 Kerberos 票證失效，因此請事先規劃再這麼做。 請參閱 [KRBTGT Account Password Reset Scripts now available for customers](https://blogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/) (客戶現在可以使用 KRBTGT 帳戶密碼重設指令碼) 中的指導方針，另請參閱如何使用  [Reset the KRBTGT account password/keys tool](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51) (重設 KRBTGT 帳戶密碼/金鑰工具)。  由於這是橫向移動攻擊手法，因此請遵循[傳遞雜湊建議](https://www.microsoft.com/download/details.aspx?id=36036)中的最佳做法。

## Kerberos 黃金票證 (Golden Ticket)<a name="golden-ticket"></a>

**描述**

具有網域系統管理員權限的攻擊者可能會危害 [KRBTGT 帳戶](https://technet.microsoft.com/library/dn745899(v=ws.11).aspx#Sec_KRBTGT)。 他們可以利用 KRBTGT 帳戶建立 Kerberos 票證授權票證 (TGT)，以提供任何資源的授權，並將票證到期日設定為任何時間。 這個假 TGT 稱為「黃金票證」，可讓攻擊者在網路上持續存在。

在此偵測中，當 Kerberos 票證授與的票證使用超過[使用者票證最長存留期](https://technet.microsoft.com/library/jj852169(v=ws.11).aspx)中指定的允許時間時，就會觸發警示。這是**時間異常**黃金票證攻擊，若是透過不存在的帳戶，則是**不存在的帳戶**黃金票證攻擊。


**調查**

- **時間異常**
   1.   群組原則中的 [使用者票證最長存留期] 設定最近 (過去幾小時內) 是否有任何變更？ 檢查該特定值是否低於票證的使用時間。 如果是，請關閉警示 (這是誤判)。
   2.   涉及此警示的 Azure ATP 感應器是否為虛擬機器？ 如果是，它最近是否從儲存狀態繼續？ 如果是，請關閉此警示。
   3.   如果上述問題的答案為否，則假設這是惡意的。

- **不存在的帳戶 - 新增** 
   1.   詢問以下問題：
         - 使用者是否為已知且有效的網域使用者？ 如果是，請關閉警示 (這是誤判)。
         - 該使用者是否為最近新增？ 如果是，請關閉警示，變更可能尚未同步處理。
         - 該使用者是否最近從 AD 刪除？ 如果是，請關閉警示。
   2.   如果上述問題的答案為否，則假設這是惡意的。

1. 對於這兩種類型的黃金票證攻擊，請按一下來源電腦以移至其 [設定檔] 頁面。 檢查活動發生的前後期間發生什麼事，並尋找異常活動，包括當時登入的使用者以及被存取的資源。 

2.  登入電腦的所有使用者是否都可登入？ 他們的權限為何？ 

3.  已登入的使用者是否可以存取這些資源？<br>
如果您已啟用 Windows Defender ATP 整合，請按一下 Windows Defender ATP 徽章。
 
 4. 若要進一步調查電腦，請檢查 Windows Defender ATP 中警示出現的前後期間，有哪些處理程序與警示出現。

**補救**


根據 [KRBTGT Account Password Reset Scripts now available for customers](https://blogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/) (客戶現在可以使用 KRBTGT 帳戶密碼重設指令碼) 中的指導方針，使用 [Reset the KRBTGT account password/keys tool](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51) (重設 KRBTGT 帳戶密碼/金鑰工具)，變更 Kerberos 票證授權票證 (KRBTGT) 密碼兩次。 重設 KRBTGT 兩次會使此網域中的所有 Kerberos 票證失效，因此請事先規劃再這麼做。 此外，由於建立黃金票證需要網域系統管理員權限，因此請實作[傳遞雜湊建議](https://www.microsoft.com/download/details.aspx?id=36036)。




## <a name="malicious-data-protection-private-information-request"></a>惡意的資料保護私人資訊要求

**描述**

Windows 使用資料保護 API (DPAPI) 來安全地保護瀏覽器所儲存的密碼、加密檔案和其他敏感性資料。 網域控制站會保留備份的主要金鑰，該金鑰可用來解密已加入網域的 Windows 電腦上使用 DPAPI 加密的所有密碼。 攻擊者可以使用主要金鑰，來解密所有已加入網域之電腦上由 DPAPI 保護的所有密碼。
在此偵測中，當使用 DPAPI 來擷取備份的主要金鑰時，就會觸發警示。

**調查**

1. 來源電腦是否正在對 Active Directory 執行組織核准的進階安全性掃描程式？

2. 如果是且一律應該這麼做，請**關閉並排除**可疑活動。

3. 如果是且不應該這麼做，請**關閉**可疑活動。

**補救**

若要使用 DPAPI，攻擊者需要網域系統管理員權限。 實作 [雜湊傳遞建議](https://www.microsoft.com/download/details.aspx?id=36036)。

## <a name="malicious-replication-of-directory-services"></a>惡意的目錄服務複寫


**描述**

在 Active Directory 複寫程序中，某個網域控制站上所做的變更，會與所有其他網域控制站同步處理。 若具有必要權限，攻擊者就可以起始複寫要求，讓他們擷取儲存在 Active Directory 中的資料，包括密碼雜湊。

在此偵測中，當複寫要求從非網域控制站的電腦起始時，就會觸發警示。

**調查**

> [!NOTE]
> 如果有未安裝 Azure ATP 感應器的網域控制站，則 Azure ATP 不會涵蓋這些網域控制站。 在此情況下，如果您在未註冊或未受保護的網域控制站上部署新的網域控制站，則 Azure ATP 一開始可能不會將之識別為網域控制站。 強烈建議您在每個網域控制站上都安裝 Azure ATP 感應器，以便能完整涵蓋。

1. 有問題的電腦是否為網域控制站？ 例如，有複寫問題之新升級的網域控制站。 如果是，請**關閉**可疑活動。 
2.  有問題的電腦是否預期會從 Active Directory 複寫資料？ 例如，Azure AD Connect 或網路效能監視裝置。 如果是，請**關閉並排除**可疑活動。
3. 複寫要求是否傳送自 NAT 或 Proxy 的 IP 位址？ 如果是，請檢查裝置後方是否有新的網域控制站，或者裝置是否產生可疑活動。 

4. 按一下來源電腦或帳戶以移至其設定檔頁面。 檢查複寫期間所發生的事件，並搜尋不尋常的活動，例如當時登入的使用者，以及被存取的資源有哪些。 如果您已啟用 Windows Defender ATP 整合，請按一下 [Windows Defender ATP] 徽章 ![[Windows Defender ATP] 徽章](./media/wd-badge.png) 以進一步調查電腦。 在 Windows Defender ATP 中，您可以查看在警示期間所發生的處理程序與警示。 


**補救**

驗證下列權限： 

- 複寫目錄變更   

- 全部複寫目錄變更  

如需詳細資訊，請參閱  [Grant Active Directory Domain Services permissions for profile synchronization in SharePoint Server 2013](https://technet.microsoft.com/library/hh296982.aspx) (在 SharePoint Server 2013 中授與 Active Directory Domain Services 權限，以進行設定檔同步處理)。
您可以利用  [AD ACL 掃描程式](https://blogs.technet.microsoft.com/pfesweplat/2013/05/13/take-control-over-ad-permissions-and-the-ad-acl-scanner-tool/)或建立 Windows PowerShell 指令碼，以判斷誰在網域中具有這些權限。


## <a name="privilege-escalation-using-forged-authorization-data"></a>使用偽造授權資料提升權限

**描述**

舊版 Windows Server 中的已知弱點可能會被攻擊者用來操縱 Privileged Attribute Certificate (PAC)。 PAC 是 Kerberos 票證中的一個欄位，它包含使用者授權資料 (在 Active Directory 中，這是群組成員資格) 而且會將額外權限授與攻擊者。

**調查**

1. 按一下警示以移至其詳細資料頁面。

2. 目的地電腦 (在 [已存取] 欄下) 是否已透過 MS14-068 (網域控制站) 或 MS11-013 (伺服器) 修補？ 如果是，請**關閉**可疑活動 (這是誤判)。

3. 如果否，來源電腦, 執行 (在 [來源] 欄下) 是否為已知要修改 PAC 的 OS/應用程式？ 如果是，請**隱藏**可疑活動 (這是良性真肯定)。

4. 如果上述兩個問題的答案均為否，則假設這是惡意的。

**補救**

確定作業系統早於 Windows Server 2012 R2 的所有網域控制站均已安裝  [KB3011780](https://support.microsoft.com/help/2496930/ms11-013-vulnerabilities-in-kerberos-could-allow-elevation-of-privilege)，而且早於 2012 R2 的所有成員伺服器和網域控制站均有 KB2496930，為最新狀態。 如需詳細資訊，請參閱  [Silver PAC](https://technet.microsoft.com/library/security/ms11-013.aspx)  和  [Forged PAC](https://technet.microsoft.com/library/security/ms14-068.aspx)。

## <a name="reconnaissance-using-account-enumeration"></a>使用帳戶列舉偵查

**描述**

在帳戶列舉探查中，攻擊者會使用含有上千筆使用者名稱的目錄或 KrbGuess 這類工具，嘗試猜測網域中的使用者名稱。 攻擊者利用這些名字提出 Kerberos 要求，試著在您的網域中找到有效的使用者名稱。 如果成功猜到使用者名稱，攻擊者會收到 Kerberos 錯誤「需要預先驗證」，而不是「未知的安全性主體」。 

在此偵測中，Azure ATP 可以偵測到攻擊來源、猜測嘗試總次數及相符次數。 如果有太多未知的使用者，Azure ATP 會將其偵測為可疑的活動。 

**調查**

1. 按一下警示以移至其詳細資料頁面。 

2. 關於帳戶是否存在，主機電腦該對網域控制站進行查詢嗎 (例如 Exchange 伺服器)？ <br></br>
在可能產生這個行為的主機上，有指令碼或應用程式在執行嗎？ <br></br>
如果以上其中一個問題的答案是肯定的，請**關閉**可疑活動 (其為良性確判)，並將主機從可疑活動中排除。

3. 下載警示詳細資料的 Excel 試算表，以便查看分成現有及非現有帳戶的帳戶嘗試清單。 如果您在查看試算表中的非現有帳戶工作表時，發現帳戶很眼熟，帳戶有可能是已停用的帳戶，或已離開公司的員工。 在這種情況下，嘗試就不太可能來自字典。 最有可能的情況是，應用程式或指令碼正在檢查哪個帳戶仍然存在於 Active Directory 中，表示其為良性確判。

3. 如果大部分都是不熟悉的名稱，有任何猜測嘗試與 Active Directory 中的現有帳戶名稱相符嗎？ 如果沒有相符的名稱，嘗試即無效，但您應該要注意警示，看看是否有隨著時間而更新。

4. 若任何猜測意圖符合現有的帳戶名稱，攻擊者即可得知帳戶存在於您的環境中，而且可以嘗試使用暴力密碼破解，使用探索到的使用者名稱存取您的網域。 請檢查猜到的帳戶名稱，了解是否有其他可疑活動。 請檢查是否有任何相符的帳戶為敏感性帳戶。


**補救**

[複雜且很長的密碼](https://docs.microsoft.com/windows/device-security/security-policy-settings/password-policy)提供必要的第一層安全性，以防止暴力密碼破解攻擊。


## <a name="reconnaissance-using-directory-services-queries"></a>使用目錄服務查詢探查

**描述**

攻擊者可利用目錄服務探查來對應目錄結構，並鎖定特殊權限帳戶以在稍後用於攻擊步驟。 安全性帳戶管理員遠端 (SAM-R) 通訊協定是用來查詢目錄以執行這類對應的其中一種方法。

在此偵測中，在部署 Azure ATP 之後的第一個月內不會觸發任何警示。 在學習期間，Azure ATP 會分析有哪個 SAM-R 查詢是從哪部電腦發出，同時包括敏感性帳戶的列舉和個別查詢。

**調查**

1. 按一下警示以移至其詳細資料頁面。 確認已執行哪些查詢 (例如 Enterprise Admins 或 Administrator)，以及查詢是否成功。

2. 這類查詢是否預期會從有問題的來源電腦發出？

3. 如果是且警示已更新，請**隱藏**可疑活動。

4. 如果是且不應該再這麼做，請**關閉**可疑活動。

5. 如果有相關帳戶的資訊：這類查詢是否預期會由該帳戶發出，或該帳戶是否通常會登入來源電腦？

 - 如果是且警示已更新，請**隱藏**可疑活動。

 - 如果是且不應該再這麼做，請**關閉**可疑活動。

 - 如果上述所有問題的答案均為否，則假設這是惡意的。

6. 如果沒有涉及之帳戶的相關資訊，您可以移至端點並檢查於警示期間登入的帳戶。

**補救**

使用下列程序來強化您的環境，以防止此攻擊手法：
1. 電腦是否在執行弱點掃描工具？  
2. 調查在攻擊中被查詢的特定使用者及群組是否為具有特殊權限或高價值的帳戶 (例如執行長、財務長、IT 管理等)。  若是如此，也請查看端點上的其他活動，並監視已查詢帳戶登入的電腦，因為這些可能是橫向移動的目標。

## <a name="reconnaissance-using-dns"></a>使用 DNS 探查

**描述**

您的 DNS 伺服器包含您網路中所有電腦、IP 位址和服務的對應。 攻擊者會使用這項資訊來對應您的網路結構，並鎖定感興趣的電腦以在稍後用於攻擊步驟。

DNS 通訊協定中有數種查詢類型。 Azure ATP 會偵測源自於非 DNS 伺服器的 AXFR (傳輸) 要求。

**調查**

1. 來源電腦 (**源自於...**) 是否為 DNS 伺服器？ 如果是，則可能是誤判。 若要驗證，請按一下警示以移至其詳細資料頁面。 在表格的 [查詢] 下，確認已查詢哪些網域。 這是現有的網域嗎？ 如果是，請**關閉**可疑活動 (這是誤判)。 此外，請確定 Azure ATP 獨立感應器與來源電腦之間的 UDP 連接埠 53 已開啟，以防止未來發生誤判。

2. 來源電腦是否正在執行安全性掃描程式？ 如果是，請在 ATP 中直接透過 [關閉並排除]，或透過 [排除] 頁面 (位於 [設定] 下，且僅適用於 Azure ATP 系統管理員)，來**排除實體**。

3. 如果上述所有問題的答案都是否定的，請繼續針對來源電腦進行調查。 按一下來源電腦以移至其設定檔頁面。 檢查要求期間所發生的事件，並搜尋不尋常的活動，例如當時登入的使用者，以及被存取的資源有哪些。 如果您已啟用 Windows Defender ATP 整合，請按一下 [Windows Defender ATP] 徽章 ![[Windows Defender ATP] 徽章](./media/wd-badge.png) 以進一步調查電腦。 在 Windows Defender ATP 中，您可以查看在警示期間所發生的處理程序與警示。 

**補救**

您可以停用區域傳輸，或將區域傳輸僅限於指定的 IP 位址，來保護內部 DNS 伺服器，以防止發生使用 DNS 探查。 如需限制區域傳輸的詳細資訊，請參閱 [Restrict Zone Transfers](https://technet.microsoft.com/library/ee649273(v=ws.10).aspx) (限制區域傳輸)。
修改區域傳輸是檢查清單中的一項工作，應該加以解決才能 [保護 DNS 伺服器免受內部和外部攻擊](https://technet.microsoft.com/library/cc770432(v=ws.11).aspx)。

## <a name="reconnaissance-using-smb-session-enumeration"></a>使用 SMB 工作階段列舉探查


**描述**

伺服器訊息區 (SMB) 列舉可讓攻擊者取得使用者最近登入位置的相關資訊。 一旦攻擊者擁有這項資訊，他們就可以在網路中橫向移動來到達特定敏感性帳戶。

在此偵測中，對網域控制站執行 SMB 工作階段列舉時，就會觸發警示，因為這不應該發生。

**調查**

1. 按一下警示以移至其詳細資料頁面。 確認哪些帳戶已執行此作業，以及已公開哪些帳戶 (如果有的話)。

 - 來源電腦上是否正在執行某種安全性掃描程式？ 如果是，請**關閉並排除**可疑活動。

2. 確認哪些相關使用者已執行此作業。 這些使用者是否通常會登入來源電腦，或者是否會管理應執行這類動作的人員？  

3. 如果是且警示已更新，請**隱藏**可疑活動。  

4. 如果是且不應該再這麼做，請**關閉**可疑活動。

5. 如果上述所有問題的答案均為否，則假設這是惡意的。

**補救**

使用 [Net Cease 工具](https://gallery.technet.microsoft.com/Net-Cease-Blocking-Net-1e8dcb5b)來強化您的環境，以防止此攻擊。

## <a name="remote-code-execution-attempt---enhanced"></a>遠端程式碼執行嘗試 - 增強

**描述**

盜用系統管理認證或使用零時差惡意探索的攻擊者可能會在您的網域控制站上執行遠端命令。 這可用於取得持續性、收集資訊、發動拒絕服務 (DOS) 的攻擊或任何其他原因。 Azure ATP 會偵測 PSexec、遠端 WMI 和 PowerShell 連線。

**調查**

1. 對網域控制站執行系統管理工作的系統管理工作站以及 IT 小組成員和服務帳戶經常會發生這種情況。 如果是這種情況，而且由於相同的系統管理員及/或電腦執行工作而更新警示，請**隱藏**警示。

2. 有問題的**電腦**是否可以對您的網域控制站執行此遠端執行？

 - 有問題的**帳戶**是否可以對您的網域控制站執行此遠端執行？

 - 如果這兩個問題的答案均為「是」，請**關閉**警示。

3. 如果針對這兩個問題的答案都是否定的，則應將此事件視為真肯定。 試著透過檢查電腦和帳戶設定檔，來找出嘗試的來源。 按一下來源電腦或帳戶以移至其設定檔頁面。 檢查這些嘗試的期間所發生的事件，並搜尋不尋常的活動，例如當時登入的使用者，以及被存取的資源有哪些。 如果您已啟用 Windows Defender ATP 整合，請按一下 [Windows Defender ATP] 徽章 ![[Windows Defender ATP] 徽章](./media/wd-badge.png) 以進一步調查電腦。 在 Windows Defender ATP 中，您可以查看在警示期間所發生的處理程序和警示。 

**補救**

1. 限制從非 0 層電腦遠端存取網域控制站。

2. 實作 [特殊權限存取](https://technet.microsoft.com/windows-server-docs/security/securing-privileged-access/securing-privileged-access) 只允許強化的電腦連線到網域控制站來進行管理。

> [!NOTE]
> 只有 ATP 感應器才支援遠端程式碼執行嘗試的警示。 

## <a name="suspicious-authentication-failures--enhanced"></a>可疑的驗證失敗 - 增強

**描述**

在暴力密碼破解攻擊中，攻擊者嘗試使用不同帳戶搭配多個密碼來驗證，直到找到正確的密碼為止，或使用單一密碼進行大規模密碼噴灑，直到至少可使用一個帳戶為止。 找到驗證之後，攻擊者就可使用已驗證的帳戶登入。

在此偵測中，當使用 Kerberos 或 NTLM 發生多次驗證失敗，或偵測到使用密碼噴灑，就會觸發警示。 使用 Kerberos 或 NTLM，這種攻擊通常是在許多使用者之間水平使用少量密碼，或只對一些使用者垂直使用大量密碼，或這兩者的任意組合。 在密碼噴灑中，攻擊者從網域控制站成功列舉有效使用者清單後，便會嘗試針對所有已知的使用者帳戶嘗試使用一個特製密碼 (一個密碼用於多個帳戶)。 如果初始密碼噴灑失敗，他們會利用其他的特製密碼再試一次，在嘗試之間通常會等候 30 分鐘。 等候時間可讓攻擊者避免觸發最常見以時間為基礎的帳戶鎖定閾值。 密碼噴灑已快速成為攻擊者和滲透測試者最愛的技術。 密碼噴灑攻擊已證明是取得組織內初始據點的有效方式，並可進行後續的橫向移動，嘗試提高權限。 

**學習期間** 可觸發這類型警示的最短期間為一週。

**調查**

1.  按一下 [下載詳細資料] 以在 Excel 試算表中檢視完整資訊。 以下是可提供的資訊： 
   -    被攻擊帳戶的清單
   -    登入嘗試成功進行驗證之被猜測帳戶的清單
   -    如果驗證嘗試是使用 NTLM 來執行，您會看到相關的事件活動 
   -    如果驗證嘗試是使用 Kerberos 來執行，您會看到相關的網路活動
   -  如果驗證嘗試是使用密碼噴灑，您會看到相關的網路活動

2.  按一下來源電腦以移至其設定檔頁面。 檢查這些嘗試的期間所發生的事件，並搜尋不尋常的活動，例如當時登入的使用者，以及被存取的資源有哪些。 如果您已啟用 Windows Defender ATP 整合，請按一下 [Windows Defender ATP] 徽章 ![[Windows Defender ATP] 徽章](./media/wd-badge.png) 以進一步調查電腦。 在 Windows Defender ATP 中，您可以查看在警示期間所發生的處理程序與警示。 

3.  如果驗證是使用 NTLM 來執行，而您多次看到該警示，且沒有來源電腦嘗試存取之伺服器的足夠相關資訊，請針對涉及的網域控制站啟用 **NTLM 稽核**。 若要這樣做，請開啟事件 8004。 這是 NTLM 驗證事件，其中包含來源電腦嘗試存取的來源電腦、使用者帳戶及**伺服器**的相關資訊。 知道驗證確認是由哪一部伺服器所傳送之後，您可以透過檢查其事件 (例如 4624) 來調查它，以進一步了解驗證程序。 

**補救**

[複雜且很長的密碼](https://docs.microsoft.com/windows/device-security/security-policy-settings/password-policy)提供必要的第一層安全性，以防止暴力密碼破解攻擊。

## <a name="suspicious-communication-over-dns---preview"></a>透過 DNS 的可疑通訊 - 預覽

**描述**

大多數組織中的 DNS 通訊協定通常不會受到監視，而且很少會因惡意活動遭到封鎖。 這讓攻擊者有機會在遭入侵的電腦上濫用 DNS 通訊協定。 透過 DNS 的惡意通訊可用來竊取資料、命令和控制攻擊和/或規避公司網路限制。

**調查**
> [!NOTE]
> 「透過 DNS 的可疑通訊」安全性警訊會列出可疑網域。 新的網域，或是 Azure ATP 未知或無法辨識但您組織已知或屬於其一部分的最近新增網域，都可能被關閉。 


1.  某些合法公司會使用 DNS 進行定期通訊。 請檢查已註冊查詢網域是否屬於信任的來源，例如您的防毒提供者。 如果網域已知並受信任，而且允許 DNS 查詢，則可以關閉警示，並在未來警示中[排除](excluding-entities-from-detections.md)該網域。 
2.   如果已註冊的查詢網域未受信任，請指出在來源電腦上建立要求的程序。 使用 [Process Monitor](https://docs.microsoft.com/en-us/sysinternals/downloads/procmon) 可協助進行這項工作。
3.  判斷可疑活動何時開始？ 是否已在組織中部署或安裝任何新程式 (AV)？ 同一時間是否有其他警示？
4.  按一下來源電腦以存取其設定檔頁面。 檢查 DNS 查詢出現前後期間的事件，並搜尋異常活動，例如當時登入的使用者，以及所使用的資源。 如果您已啟用 Windows Defender ATP 整合，請按一下 Windows Defender ATP 徽章 ![[Windows Defender ATP] 徽章](./media/wd-badge.png) 以進一步調查電腦。 使用 Windows Defender ATP，您可以查看在警示期間所發生的處理程序和警示。

**補救**：如果在調查後發現已註冊的查詢網域不受信任，建議封鎖目的地網域以避免未來的所有通訊。 

## <a name="suspicious-domain-controller-promotion-potential-dcshadow-attack"></a>可疑的網域控制站升級 (潛在的 DCShadow 攻擊)

**描述**

網域控制站陰影 (DCShadow) 攻擊是藉由惡意複寫來變更目錄物件。 透過使用複寫流程來建立惡意的網域控制站，便可以從任何電腦進行此攻擊。
 
DCShadow 使用 RPC 和 LDAP 進行：
1. 將電腦帳戶註冊為網域控制站 (使用網域管理員權限)，以及
2. 對 DRSUAPI 執行複寫 (使用授與的複寫權限)，並將變更傳送到目錄物件。
 
在此偵測中，當網路中的電腦嘗試註冊為惡意網域控制站時，就會觸發警示。 

**調查**
 
1. 有問題的電腦是否為網域控制站？ 例如，有複寫問題之新升級的網域控制站。 如果是，請**關閉**可疑活動。
2. 有問題的電腦是否預期會從 Active Directory 複寫資料？ 例如，Azure AD Connect。 如果是，請**關閉並排除**可疑活動。
3. 按一下來源電腦或帳戶以移至其設定檔頁面。 檢查複寫前後期間的事件，並搜尋異常活動，例如當時登入的使用者及其存取的資源，以及電腦的作業系統為何？
   1. 所有登入電腦的使用者，是否都可在該電腦登入？ 他們的權限為何？ 使用者是否有權限將伺服器升級成網域控制站？ (是否為網域管理員？)
   2. 使用者是否可存取這些資源？
   3. 電腦是否為執行 Windows Server OS (或是 Windows/Linux)？ 非伺服器電腦不應複寫資料。
如果您啟用了 Windows Defender ATP 整合，請按一下 Windows Defender ATP 徽章 ![Windows Defender ATP 徽章](./media/wd-badge.png) 來進一步調查電腦。 在 Windows Defender ATP 中，您可以查看在警示期間所發生的處理程序與警示。

4. 查看 [事件檢視器]，以了解其[目錄服務記錄檔中記錄的 Active Directory 事件](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-2000-server/cc961809(v=technet.10)/) \(英文\)。 您可以使用記錄來監視 Active Directory 中的變更。 根據預設，Active Directory 只記錄重大錯誤事件，但如果此警示重複出現，請在相關的網域控制站上啟用此稽核，以供後續調查。

**補救**

檢查組織中具有以下權限的人員： 
- 複寫目錄變更 
- 全部複寫目錄變更 
 
 
如需詳細資訊，請參閱[在 SharePoint Server 2013 中授與 Active Directory 網域服務權限，以進行設定檔同步處理](https://technet.microsoft.com/library/hh296982.aspx)。 

您可以利用 [AD ACL 掃描程式](https://blogs.technet.microsoft.com/pfesweplat/2013/05/13/take-control-over-ad-permissions-and-the-ad-acl-scanner-tool/)或建立 Windows PowerShell 指令碼，以判斷誰在網域中具有這些權限。
 
> [!NOTE]
> 只有 ATP 感應器才支援可疑網域控制站升階 (潛在 DCShadow 攻擊) 的警示。 

## <a name="suspicious-modification-of-sensitive-groups"></a>敏感性群組的可疑修改

**描述**

攻擊者將使用者新增至具有高權限的群組。 如此一來就能存取更多資源並取得永續性。 此偵測需要分析使用者的群組修改活動，並在敏感性群組中出現異常新增時發出警示。 Azure ATP 會持續執行分析。 可觸發警示的最低期限是每個網域控制站一個月。

如需 Azure ATP 中敏感性群組的定義，請參閱[處理敏感性帳戶](sensitive-accounts.md)。


此偵測需要[網域控制站上稽核的事件](configure-event-collection.md)。
以確保您的網域控制站會稽核所需的事件。

**調查**

1. 群組修改是否合法？ </br>合法的群組修改很少發生且經判定並不「正常」，這可能會造成警示，因此會視為良性真肯定。

2. 如果新增的物件是使用者帳戶，請檢查使用者帳戶在新增至系統管理員群組之後採取了哪些動作。 移至 Azure ATP 中的使用者頁面以取得更多內容。 新增前後是否有與帳戶建立關聯的任何其他可疑活動？ 下載**敏感性群組修改**報表，以查看同一時段內有誰做了哪些其他修改。

**補救**

減少授權修改敏感性群組的使用者數目。

如果適用，請設定 [Privileged Access Management for Active Directory](https://docs.microsoft.com/microsoft-identity-manager/pam/privileged-identity-management-for-active-directory-domain-services)。



## <a name="suspicious-replication-request-potential-dcshadow-attack"></a>可疑的複寫要求 (潛在的 DCShadow 攻擊) 

**描述** 

在 Active Directory 複寫程序中，某個網域控制站上所做的變更，會與所有網域控制站同步處理。 若有足夠的權限，攻擊者就可授與其電腦帳戶權限，以便能夠模擬網域控制站。 攻擊者會力圖起始惡意的複寫要求，以便能夠變更真正網域控制站上的 Active Directory 物件，攻擊者就能持續存在網域中。
在此偵測中，針對受到 Azure ATP 保護的真正網域控制站，當產生了可疑的複寫要求時，就會觸發警示。 此行為表示可能是網域控制站陰影攻擊所使用的技術。

**調查** 
 
1. 有問題的電腦是否為網域控制站？ 例如，有複寫問題之新升級的網域控制站。 如果是，請**關閉**可疑活動。
2. 有問題的電腦是否預期會從 Active Directory 複寫資料？ 例如，Azure AD Connect。 如果是，請**關閉並排除**可疑活動。
3. 按一下來源電腦以移至其設定檔頁面。 檢查複寫**前後期間**的事件，並搜尋異常活動，例如當時登入的使用者、被使用的資源，以及電腦的作業系統為何？

   1.  所有登入電腦的使用者，是否都可在該電腦登入？ 他們的權限為何？ 使用者是否有權限執行複寫 (是否為網域管理員)？
   2.  使用者是否可存取這些資源？
   3. 電腦是否為執行 Windows Server OS (或是 Windows/Linux)？ 非伺服器電腦不應複寫資料。
如果您啟用了 Windows Defender ATP 整合，請按一下 Windows Defender ATP 徽章 ![Windows Defender ATP 徽章](./media/wd-badge.png) 來進一步調查電腦。 在 Windows Defender ATP 中，您可以查看在警示期間所發生的處理程序與警示。
1. 查看 [事件檢視器]，以了解其[目錄服務記錄檔中記錄的 Active Directory 事件](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-2000-server/cc961809(v=technet.10)/) \(英文\)。 您可以使用記錄來監視 Active Directory 中的變更。 根據預設，Active Directory 只記錄重大錯誤事件，但如果此警示重複出現，請在相關的網域控制站上啟用此稽核，以供後續調查。

**補救**

檢查組織中具有以下權限的人員： 
- 複寫目錄變更 
- 全部複寫目錄變更 

若要這麼做，您可以利用 [AD ACL 掃描程式](https://blogs.technet.microsoft.com/pfesweplat/2013/05/13/take-control-over-ad-permissions-and-the-ad-acl-scanner-tool/) \(英文\) 或建立 Windows PowerShell 指令碼，以判斷網域中具有這些權限的人員。

> [!NOTE]
> 只有 ATP 感應器才支援可疑複寫要求 (潛在 DCShadow 攻擊) 的警示。 


## <a name="suspicious-service-creation"></a>可疑的服務建立

**描述**

可疑的服務已在您組織中的網域控制站上建立。 此警示會依賴事件 7045，以識別此可疑活動。 

**調查**

1. 若有問題的電腦為系統管理工作站，或是 IT 團隊成員及服務帳戶會在上方執行系統管理工作的電腦，此警示可能會是誤判，您可能需要**隱藏**警示，並視需要將它新增至排除清單。

2. 該服務是否為您在此電腦上知道的服務？

 - 有問題的**帳戶**是否可以安裝此服務？

 - 如果這兩個問題的答案均為「是」，請**關閉**警示或將它新增至排除清單。

3. 如果其中一個問題的答案為「否」，則應視為真肯定。

**補救**

- 在網域電腦上實作具有較低權限的存取，以僅允許特定使用者建立新的服務。


## 可疑 VPN 連線 <a name="suspicious-vpn-detection"></a>

**描述**

Azure ATP 會連續一個月學習使用者 VPN 連線的實體行為。 

VPN 行為模型以下列活動為基礎：使用者登入的機器以及使用者連線的來源位置。 

當經機器學習演算法計算，發現與使用者的行為產生偏差時，就會開啟警示。

**調查**

1.  有問題的使用者是否預期會執行這些作業？
2.  請將下列情況視為可能的誤判：變更位置的使用者，以及正在移動並從新裝置連線的使用者。

**補救**

1.  請考慮重設該使用者的密碼。 這可防止攻擊者使用舊的認證建立新的 VPN 連線。
2.  請考慮禁止此使用者透過 VPN 連線。

## <a name="unusual-protocol-implementation"></a>不尋常的通訊協定實作


**描述**

攻擊者會使用以非標準方式實作各種通訊協定 (SMB、Kerberos、NTLM) 的工具。 雖然 Windows 會接受這種類型的網路流量而不發出警告，但 Azure ATP 能夠辨識可能的惡意用途。 此行為可能會以越過雜湊和暴力密碼破解，以及透過進階勒索軟體的惡意探索等攻擊手法來表示。

**調查**

從可疑活動時間軸找出不尋常的通訊協定，按一下可疑活動以移至其詳細資料頁面；下列通訊協定會出現在箭號上方：Kerberos 或 NTLM。

- **Kerberos**：如果已使用 Mimikatz 等駭客工具 (可能是執行越過雜湊攻擊)，通常會觸發此警示。 檢查來源電腦所執行的應用程式是否實作自己的 Kerberos 堆疊，而不是根據 Kerberos RFC。 如果是這種情況，則為良性真肯定；而且您可以**關閉**警示。 如果持續觸發警示，而且仍是這種情況，您可以**隱藏**警示。

- **NTLM**：可能是 WannaCry，或是 Metasploit、Medusa 和 Hydra 等工具。  

若要判斷這是否為 WannaCry 攻擊，請執行下列步驟：

1. 檢查來源電腦是否執行 Metasploit、Medusa 或 Hydra 等攻擊工具。

2. 如果找不到任何攻擊工具，請檢查來源電腦所執行的應用程式是否實作自己的 NTLM 或 SMB 堆疊。

3. 按一下來源電腦以移至其設定檔頁面。 檢查警示出現前後期間的事件，並搜尋異常活動，例如當時登入的使用者，以及被存取的資源。 如果您已啟用 Windows Defender ATP 整合，請按一下 [Windows Defender ATP] 徽章 ![wd 徽章](./media/wd-badge.png) 以進一步調查電腦。 在 Windows Defender ATP 中，您可以查看在警示期間所發生的處理程序與警示。



**補救**

修補您所有的電腦，特別是套用安全性更新。

1. [停用 SMBv1](https://blogs.technet.microsoft.com/filecab/2016/09/16/stop-using-smb1/)

2. [移除 WannaCry](https://support.microsoft.com/help/890830/remove-specific-prevalent-malware-with-windows-malicious-software-remo)

3. WanaKiwi 可以解密受到某種勒索軟體支配的資料，但只適用於使用者尚未重新啟動或關閉電腦的情況。 如需詳細資訊，請參閱 [Wanna Cry Ransomware](https://answers.microsoft.com/en-us/windows/forum/windows_10-security/wanna-cry-ransomware/5afdb045-8f36-4f55-a992-53398d21ed07?auth=1) (Wanna Cry 勒索軟體)


> [!NOTE]
> 若要停用安全性警訊，請連絡支援人員。


## <a name="see-also"></a>另請參閱
- [處理可疑活動](working-with-suspicious-activities.md)
- [查看 Azure ATP 論壇！](https://aka.ms/azureatpcommunity)
