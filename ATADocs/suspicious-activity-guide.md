---
title: ATA 可疑活動指南
description: 本文提供 ATA 可能偵測到的可疑活動清單及修復步驟。
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 04/03/2019
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: 1fe5fd6f-1b79-4a25-8051-2f94ff6c71c1
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: eeccc1e5a5dd16b2d480bf82034a085159baff60
ms.sourcegitcommit: e844155ea57f73dfe2b47f4c5c1c7f5292ccbf1e
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/17/2020
ms.locfileid: "94690086"
---
# <a name="advanced-threat-analytics-suspicious-activity-guide"></a>Advanced Threat Analytics 可疑活動指南

[!INCLUDE [Banner for top of topics](includes/banner.md)]

在適當的調查之後，任何可疑活動可分類為：

- **真肯定**： ATA 偵測到惡意的動作。

- **良性真肯定**： ATA 偵測到真正但不是惡意的動作，例如滲透測試。
- **錯誤正面**：假的警示，表示活動並未發生。

如需如何使用 ATA 警示的詳細資訊，請參閱[處理可疑活動](working-with-suspicious-activities.md)。

如有任何問題或意見反應，請洽詢 ATA 小組 [ATAEval@microsoft.com](mailto:ATAEval@microsoft.com) 。

## <a name="abnormal-modification-of-sensitive-groups"></a>敏感性群組的異常修改

**描述**

攻擊者將使用者新增至具有高權限的群組。 他們這樣做以取得更多資源的存取權並取得持續入侵管道。 此偵測需要分析使用者群組修改活動，並在敏感性群組中出現異常新增時發出警示。 ATA 會持續執行分析。 可觸發警示的最短期限是每個網域控制站一個月。

如需 ATA 中敏感性群組的定義，請參閱[使用 ATA 主控台](working-with-ata-console.md#sensitive-groups)。

偵測會依賴 [網域控制站上所審核的事件](configure-event-collection.md)。
若要確保您的網域控制站稽核所需的事件，請使用 [ATA 稽核 (AuditPol、進階稽核設定強制、輕量型閘道服務探索)](https://aka.ms/ataauditingblog) \(英文\) 中參考的工具。

**調查**

1. 群組修改是否合法？ </br>若合法的群組修改很少發生，且未被視為「正常」，則可能會導致警示，這會被視為良性真肯定。

1. 如果新增的物件是使用者帳戶，請檢查使用者帳戶在新增至系統管理員群組之後採取了哪些動作。 移至 ATA 中的使用者頁面，以取得更多內容。 新增前後是否有與帳戶建立關聯的任何其他可疑活動？ 下載 **敏感性群組修改** 報表，以查看同一時段內有誰做了哪些其他修改。

**補救**

減少授權修改敏感性群組的使用者數目。

設定 [Active Directory 的 Privileged Access Management （](/microsoft-identity-manager/pam/privileged-identity-management-for-active-directory-domain-services) 如果適用）。

## <a name="broken-trust-between-computers-and-domain"></a>電腦與網域之間的信任中斷

> [!NOTE]
> 電腦與網域之間的信任中斷警示已過時，而且只會出現在 ATA 1.9 版之前。

**描述**

信任中斷表示 Active Directory 安全性需求對那些有問題的電腦可能無效。 這會被視為基準安全性與合規性失敗，而且是攻擊者容易攻擊的目標。 在此偵測中，如果在 24 小時內從電腦帳戶看到超過五次 Kerberos 驗證失敗，就會觸發警示。

**調查**

正在調查的電腦是否允許網域使用者登入？
- 如果是，您可以在補救步驟中忽略此電腦。

**補救**

視需要將電腦重新加回網域，或重設電腦的密碼。

## <a name="brute-force-attack-using-ldap-simple-bind"></a>使用 LDAP 簡單繫結的暴力密碼破解攻擊

**描述**

>[!NOTE]
> **可疑的驗證失敗** 與此偵測的主要差異，是在此偵測中，ATA 可判斷不同的密碼是否已在使用中。

在暴力密碼破解攻擊中，攻擊者會嘗試使用許多不同的密碼對不同的帳戶進行驗證，直到找到至少一個帳戶的正確密碼。 找到後，攻擊者就可以使用該帳戶登入。

在此偵測中，當 ATA 偵測到大量的簡單繫結驗證時，便會觸發警示。 這可能是在許多使用者之間以一組較小的密碼 *水準水準* ;或 *垂直* 「在少數幾個使用者上有一組大量的密碼;或這兩個選項的任何組合。

**調查**

1. 如果有許多相關帳戶，請按一下 [下載詳細資料] 以檢視 Excel 試算表中的清單。

1. 按一下警示以移至其專用頁面。 檢查是否有任何登入嘗試已結束且成功驗證。 這些嘗試會顯示為資訊圖表右邊的 **猜對的帳戶**。 如果是，平常是否從來源電腦使用任何 **猜對的帳戶**？ 如果是，請 **隱藏** 可疑活動。

1. 如果沒有 **猜對的帳戶**，平常是否從來源電腦使用任何 **受攻擊的帳戶**？ 如果是，請 **隱藏** 可疑活動。

**補救**

[複雜和長密碼](/windows/device-security/security-policy-settings/password-policy) 提供必要的第一層安全性，以防範暴力密碼破解攻擊。

## <a name="encryption-downgrade-activity"></a>加密降級活動

**描述**

加密降級是一種減弱 Kerberos 的方法，它會針對通訊協定一般會以最高加密層級進行加密的不同欄位，對其加密層級做出降級。 攻擊者將能較為輕鬆地對減弱的加密欄位進行離線暴力密碼破解。 利用弱式 Kerberos 加密 Cypher 的各種攻擊方法。 在此偵測中，ATA 會了解電腦和使用者所使用的 Kerberos 加密類型，並在使用下列較弱的 Cypher 時向您發出警示：(1) 對來源電腦及/或使用者而言不尋常，以及 (2) 符合已知的攻擊手法。

有三種偵測類型：

1. 基本架構金鑰 - 這是在網域控制站上執行的惡意程式碼，允許在不知道帳戶密碼的情況下，使用任何帳戶向網域進行驗證。 此惡意程式碼通常會使用較弱的加密演算法，來推測出網域控制站上的使用者密碼。 在此偵測中，來自要求票證帳戶之網域控制站的 KRB_ERR 訊息加密方法相較於先前學到的行為已降級。

1. 黃金票證 - 在[黃金票證](#golden-ticket)警示中，相較於先前學到的行為，來自來源電腦的 TGS_REQ (服務要求) 訊息的 TGT 欄位加密方法已降級。 這不是依據時間異常偵測 (如同其他黃金票證偵測)。 此外，ATA 未偵測到與先前服務要求建立關聯的任何 Kerberos 驗證要求。

1. 越過雜湊 - 攻擊者可以透過 Kerberos AS 要求，使用竊取的弱式雜湊建立強式票證。 在此偵測中，來自來源電腦的 AS_REQ 訊息加密類型相較於先前學到的行為 (亦即電腦使用 AES) 已降級。

**調查**

請先檢查警示的描述，以查看您處理的是上述三種偵測類型的哪一種。 如需詳細資訊，請下載 Excel 試算表。

1. 基本架構金鑰 - 您可以使用 [ATA 小組所撰寫的掃描程式](https://gallery.technet.microsoft.com/Aorato-Skeleton-Key-24e46b73) \(英文\)，以檢查基本架構金鑰是否影響您的網域控制站。 如果掃描程式在一或多個網域控制站上找到惡意程式碼，則為真肯定。
1. 黃金票證-在 Excel 試算表中，移至 [ **網路活動** ] 索引標籤。您會看到相關的降級欄位為 [ **要求票證加密類型**]，而 [ **來源電腦支援的加密類型** ] 會列出更強的加密方法。
    1. 檢查來源電腦和帳戶，或者如果有多個來源電腦和帳戶，檢查它們是否有常見 (的內容，所有行銷人員都使用可能導致警示觸發) 的特定應用程式。 在某些情況下，可能會有很少使用的自訂應用程式，正在使用較低的加密編碼器進行驗證。 檢查來源電腦上是否有任何這類自訂應用程式。 如果是，則可能是良性真肯定，您可以 **隱藏** 它。
    1. 檢查這些票證所存取的資源，如果有一個資源正在存取，請加以驗證，確定它是其應存取的有效資源。 此外，請驗證目標資源是否支援強式加密方法。 您可以透過在 Active Directory 中檢查資源服務帳戶的 `msDS-SupportedEncryptionTypes` 屬性來檢查這點。
1. 越過-雜湊-在 Excel 試算表中，移至 [ **網路活動** ] 索引標籤。您會看到相關的降級欄位為 [ **加密時間戳記加密類型]** 和 [ **來源電腦支援的加密類型** ] 包含更強的加密方法。
    1. 如果最近有變更智慧卡設定，則當使用者使用智慧卡登入時，可能會觸發此警示。 檢查相關帳戶是否有類似的變更。 如果是，這可能是良性真肯定，您可以 **隱藏** 它。
    1. 檢查這些票證所存取的資源，如果有一個資源正在存取，請加以驗證，確定它是其應存取的有效資源。 此外，請驗證目標資源是否支援強式加密方法。 您可以透過在 Active Directory 中檢查資源服務帳戶的 `msDS-SupportedEncryptionTypes` 屬性來檢查這點。

**補救**

1. 基本架構金鑰 - 移除惡意程式碼。 如需詳細資訊，請參閱[基本架構金鑰惡意程式碼分析](https://www.virusbulletin.com/virusbulletin/2016/01/paper-digital-bian-lian-face-changing-skeleton-key-malware) \(英文\)。

1. 黃金票證 - 遵循[黃金票證](#golden-ticket)可疑活動的指示。
    此外，由於建立黃金票證需要網域系統管理員許可權，因此請執行 [傳遞雜湊建議](https://www.microsoft.com/download/details.aspx?id=36036)。

1. 越過雜湊 - 如果相關帳戶不是敏感性帳戶，請重設該帳戶的密碼。 這可防止攻擊者從密碼雜湊建立新的 Kerberos 票證，但現有票證在過期前仍可使用。 如果是敏感性帳戶，您應該考慮重設 KRBTGT 帳戶兩次，就像在黃金票證可疑活動中一樣。 重設 KRBTGT 兩次會使此網域中的所有 Kerberos 票證失效，因此請事先規劃再這麼做。 請參閱 [KRBTGT Account Password Reset Scripts now available for customers](https://blogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/) (客戶現在可以使用 KRBTGT 帳戶密碼重設指令碼) 中的指引。 另請參閱使用 [重設 KRBTGT 帳戶密碼/金鑰]

    工具] (https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51) 。 由於這是橫向移動攻擊手法，因此請遵循[傳遞雜湊建議](https://www.microsoft.com/download/details.aspx?id=36036)的最佳做法。

## <a name="honeytoken-activity"></a>Honeytoken 活動

**描述**

Honeytoken 帳戶是假帳戶，可設定來識別和追蹤與這些帳戶相關的惡意活動。 Honeytoken 帳戶應保留未使用，同時擁有具吸引力的名稱來引誘攻擊者 (例如 SQL-Admin)。 任何來自這些帳戶的活動可能表示惡意行為。

如需 honey token 帳戶的詳細資訊，請參閱[安裝 ATA - 步驟 7](install-ata-step7.md)。

**調查**

1. 使用可疑活動頁面中所述的方法 (例如 Kerberos、LDAP、NTLM)，檢查來源電腦的擁有者是否使用 Honeytoken 帳戶進行驗證。

1. 瀏覽至來源電腦設定檔頁面，並檢查其中已驗證哪些其他帳戶。 與這些帳戶的擁有者確認他們是否使用 Honeytoken 帳戶。

1. 這可能是非互動式登入，因此請務必檢查來源電腦上是否有應用程式或指令碼正在執行。

如果在執行步驟1到3之後，如果沒有良性使用的證據，請假設這是惡意的。

**補救**

請確定 Honeytoken 帳戶只會用於其預期用途，否則可能會產生許多警示。

## <a name="identity-theft-using-pass-the-hash-attack"></a>使用傳遞雜湊攻擊竊取身分

**描述**

傳遞票證是一種橫向移動攻擊手法，在此攻擊中，攻擊者從一部電腦竊取使用者的 NTLM 雜湊，然後加以使用以存取另一部電腦。

**調查**

所使用的雜湊是來自目標使用者所擁有還是定期使用的電腦？ 如果是，則警示為誤判；否則，可能是真的有問題。

**補救**

1. 如果相關帳戶不是敏感性帳戶，請重設該帳戶的密碼。 重設密碼可防止攻擊者從密碼雜湊建立新的 Kerberos 票證。 現有的票證在到期之前仍可使用。

1. 如果涉及的帳戶是敏感性帳戶，請考慮重設 KRBTGT 帳戶兩次，如在黃金票證可疑活動中一樣。 重設 KRBTGT 兩次可使所有網域 Kerberos 票證失效，因此在這樣做之前請務必先做好規劃。 請參閱[客戶現在可以使用 KRBTGT 帳戶密碼重設指令碼](https://blogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/) \(英文\) 中的指導方針，另請參閱並使用[重設 KRBTGT 帳戶密碼/金鑰工具](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51) \(英文\)。 由於這通常是橫向移動攻擊手法，因此請遵循[傳遞雜湊建議](https://www.microsoft.com/download/details.aspx?id=36036)的最佳做法。

## <a name="identity-theft-using-pass-the-ticket-attack"></a>使用傳遞票證攻擊竊取身分

**描述**

傳遞票證是一種橫向移動攻擊手法，在此攻擊中，攻擊者從一部電腦竊取 Kerberos 票證，並重複使用竊取的票證來存取另一部電腦。 在此偵測中，會看到 Kerberos 票證用於兩部 (或多部) 不同的電腦。

**調查**

1. 按一下 [下載詳細資料] 按鈕，以檢視相關 IP 位址的完整清單。 一或兩部電腦的 IP 位址是否屬於從過小 DHCP 集區配置的子網路，例如 VPN 或 WiFi？ 是否共用 IP 位址？ 例如，透過 NAT 裝置？ 如果上述任何問題的答案為是，則警示為誤判。

1. 是否有自訂應用程式代表使用者轉送票證？ 如果是，則為良性真肯定。

**補救**

1. 如果相關帳戶不是敏感性帳戶，請重設該帳戶的密碼。 密碼重設可防止攻擊者從密碼雜湊建立新的 Kerberos 票證。 任何現有的票證在到期之前仍可用。

1. 如果是敏感性帳戶，您應該考慮重設 KRBTGT 帳戶兩次，就像在黃金票證可疑活動中一樣。 重設 KRBTGT 兩次會使此網域中的所有 Kerberos 票證失效，因此請事先規劃再這麼做。 請參閱 [KRBTGT Account Password Reset Scripts now available for customers](https://blogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/) (客戶現在可以使用 KRBTGT 帳戶密碼重設指令碼) 中的指引，另請參閱並使用 [Reset the KRBTGT account password/keys tool](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51) (重設 KRBTGT 帳戶密碼/金鑰工具)。  由於這是橫向移動攻擊手法，因此請遵循[傳遞雜湊建議](https://www.microsoft.com/download/details.aspx?id=36036)中的最佳做法。

## <a name="kerberos-golden-ticket-activity"></a>Kerberos 黃金票證活動<a name="golden-ticket"></a>

**描述**

具有網域系統管理員權限的攻擊者可能會危害您的 [KRBTGT 帳戶](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/dn745899(v=ws.11)#Sec_KRBTGT)。 攻擊者可以使用 KRBTGT 帳戶來建立 Kerberos 票證授權票證 (TGT) ，提供對您任何資源的授權。 票證到期日可設定為任意時間。 這個假 TGT 稱為「黃金票證」，可讓攻擊者在您的網路中取得並維持永續性。

在此偵測中，當 Kerberos 票證授權票證 (TGT) 使用超過[使用者票證最長存留期](/previous-versions/windows/it-pro/windows-server-2012-R2-and-2012/jj852169(v=ws.11)) \(英文\) 安全性原則中所指定的允許時間時，就會觸發警示。

**調查**

1. 群組原則中的 [使用者票證最長存留期] 設定最近 (過去幾小時內) 是否有任何變更？ 如果是，請 **關閉** 警示 (這是誤判)。

1. 此警示中的相關 ATA 閘道是否為虛擬機器？ 如果是，它最近是否從儲存狀態繼續？ 如果是，請 **關閉** 此警示。

1. 如果上述問題的答案為否，則假設這是惡意的。

**補救**

根據 [KRBTGT Account Password Reset Scripts now available for customers](https://blogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/) (客戶現在可以使用 KRBTGT 帳戶密碼重設指令碼) 中的指引，使用 [Reset the KRBTGT account password/keys tool](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51) (重設 KRBTGT 帳戶密碼/金鑰工具)，變更 Kerberos 票證授權票證 (KRBTGT) 密碼兩次。 重設 KRBTGT 兩次會使此網域中的所有 Kerberos 票證失效，因此請事先規劃再這麼做。
此外，由於建立黃金票證需要網域系統管理員許可權，因此請執行 [傳遞雜湊建議](https://www.microsoft.com/download/details.aspx?id=36036)。

## <a name="malicious-data-protection-private-information-request"></a>惡意的資料保護私人資訊要求

**描述**

Windows 使用資料保護 API (DPAPI) 來安全地保護瀏覽器所儲存的密碼、加密檔案和其他敏感性資料。 網域控制站會保留備份的主要金鑰，該金鑰可用來解密已加入網域的 Windows 電腦上使用 DPAPI 加密的所有密碼。 攻擊者可以使用主要金鑰，來解密所有已加入網域之電腦上由 DPAPI 保護的所有密碼。
在此偵測中，當使用 DPAPI 來擷取備份的主要金鑰時，就會觸發警示。

**調查**

1. 來源電腦是否正在對 Active Directory 執行組織核准的進階安全性掃描程式？

1. 如果是且一律應該這麼做，請 **關閉並排除** 可疑活動。

1. 如果是且不應該這麼做，請**關閉可疑活動。

**補救**

若要使用 DPAPI，攻擊者需要網域系統管理員權限。 實作[傳遞雜湊建議](https://www.microsoft.com/download/details.aspx?id=36036)。

## <a name="malicious-replication-of-directory-services"></a>惡意的目錄服務複寫

**描述**

在 Active Directory 複寫程序中，某個網域控制站上所做的變更，會與所有其他網域控制站同步處理。 若具有必要權限，攻擊者就可以起始複寫要求，讓他們擷取儲存在 Active Directory 中的資料，包括密碼雜湊。

在此偵測中，當複寫要求從非網域控制站的電腦起始時，就會觸發警示。

**調查**

1. 有問題的電腦是否為網域控制站？ 例如，有複寫問題之新升級的網域控制站。 如果是，請 **關閉** 可疑活動。
1. 有問題的電腦是否預期會從 Active Directory 複寫資料？ 例如，Azure AD Connect。 如果是，請 **關閉並排除** 可疑活動。
1. 按一下來源電腦或帳戶以移至其設定檔頁面。 檢查複寫期間所發生的事件，並搜尋不尋常的活動，例如當時登入的使用者，以及被存取的資源有哪些。

**補救**

驗證下列權限：

- 複寫目錄變更

- 全部複寫目錄變更

如需詳細資訊，請參閱[在 SharePoint Server 2013 中授與 Active Directory 網域服務權限，以進行設定檔同步處理](/SharePoint/administration/user-profile-service-administration)。
您可以利用 [AD ACL 掃描程式](/archive/blogs/pfesweplat/take-control-over-ad-permissions-and-the-ad-acl-scanner-tool)或建立 Windows PowerShell 指令碼，以判斷誰在網域中具有這些權限。

## <a name="massive-object-deletion"></a>大量物件刪除

**描述**

在某些情況下，攻擊者會執行阻斷服務攻擊 (DoS)，而不是只竊取資訊。 刪除大量帳戶是一種嘗試進行 DoS 攻擊的手法。

在此偵測中，當刪除的帳戶超過所有帳戶的 5% 時，就會觸發警示。 此偵測需要已刪除物件容器的讀取權限。
如需設定已刪除物件容器之唯讀權限的資訊，請參閱 [View or Set Permissions on a Directory Object](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc816824(v=ws.10)) (檢視或設定目錄物件的權限) 中的 **Changing permissions on a deleted object container** (變更已刪除物件容器的權限)。

**調查**

檢閱已刪除的帳戶清單，並判斷是否有可能造成此大量刪除的模式或業務理由。

**補救**

移除可刪除 Active Directory 中帳戶之使用者的權限。 如需詳細資訊，請參閱 [View or Set Permissions on a Directory Object](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc816824(v=ws.10)) (檢視或設定目錄物件的權限)。

## <a name="privilege-escalation-using-forged-authorization-data"></a>使用偽造授權資料提升權限

**描述**

舊版 Windows Server 中的已知弱點可能會被攻擊者用來操縱 Privileged Attribute Certificate (PAC)。 PAC 是 Kerberos 票證中的一個領域，它具有使用者授權資料 (在 Active Directory 中，這是群組成員資格) 而且會將額外權限授與攻擊者。

**調查**

1. 按一下警示以存取其詳細資料頁面。

1. 目的地電腦 (在 [已存取] 欄下) 是否已透過 MS14-068 (網域控制站) 或 MS11-013 (伺服器) 修補？ 如果是，請 **關閉** 可疑活動 (這是誤判)。

1. 若目的地電腦未修補，來源電腦 (在 [來源] 欄下) 是否為已知要修改 PAC 的 OS/應用程式？ 如果是，請 **隱藏** 可疑活動 (這是良性真肯定)。

1. 若前兩個問題的答案為否，則假設此活動為惡意。

**補救**

請確定所有具有 Windows Server 2012 R2 作業系統的網域控制站都已與 [>kb3011780](https://support.microsoft.com/help/2496930/ms11-013-vulnerabilities-in-kerberos-could-allow-elevation-of-privilege) 一起安裝，而且所有成員伺服器和最高 2012 R2 的網域控制站都是最新的 KB2496930。 如需詳細資訊，請參閱 [Silver PAC](/security-updates/SecurityBulletins/2011/ms11-013) 和[偽造 PAC](/security-updates/SecurityBulletins/2014/ms14-068)。

## <a name="reconnaissance-using-account-enumeration"></a>使用帳戶列舉偵查

**描述**

在帳戶列舉探查中，攻擊者會使用含有上千筆使用者名稱的目錄或 KrbGuess 這類工具，嘗試猜測網域中的使用者名稱。 攻擊者利用這些名字提出 Kerberos 要求，試著在您的網域中找到有效的使用者名稱。 如果成功猜到使用者名稱，攻擊者將會收到 Kerberos 錯誤 **需要預先驗證**，而不是 **未知的安全性主體**。

在這項偵測中，ATA 可以偵測到攻擊來源、猜測嘗試總次數及相符次數。 如果有太多未知的使用者，ATA 會將其偵測為可疑的活動。

**調查**

1. 按一下警示以移至其詳細資料頁面。

    1. 關於帳戶是否存在，主機電腦該對網域控制站進行查詢嗎 (例如 Exchange 伺服器)？

1. 在可能產生這個行為的主機上，有指令碼或應用程式在執行嗎？

    如果以上其中一個問題的答案是肯定的，請 **關閉** 可疑活動 (其為良性確判)，並將主機從可疑活動中排除。

1. 下載警示詳細資料的 Excel 試算表，以便查看分成現有及非現有帳戶的帳戶嘗試清單。 如果您在查看試算表中的非現有帳戶工作表時，發現帳戶很眼熟，帳戶有可能是已停用的帳戶，或已離開公司的員工。 在這種情況下，嘗試就不太可能來自字典。 最有可能的情況是，應用程式或指令碼正在檢查哪個帳戶仍然存在於 Active Directory 中，表示其為良性確判。

1. 如果大部分都是不熟悉的名稱，有任何猜測嘗試與 Active Directory 中的現有帳戶名稱相符嗎？ 如果沒有相符的名稱，嘗試即無效，但您應該要注意警示，看看是否有隨著時間而更新。

1. 若任何猜測意圖符合現有的帳戶名稱，攻擊者即可得知帳戶存在於您的環境中，而且可以嘗試使用暴力密碼破解，使用探索到的使用者名稱存取您的網域。 請檢查猜到的帳戶名稱，了解是否有其他可疑活動。 請檢查是否有任何相符的帳戶為敏感性帳戶。

**補救**

[複雜和長密碼](/windows/device-security/security-policy-settings/password-policy) 提供必要的第一層安全性，以防範暴力密碼破解攻擊。

## <a name="reconnaissance-using-directory-services-queries"></a>使用目錄服務查詢的偵察

**描述**

攻擊者可利用目錄服務探查來對應目錄結構，並鎖定特殊權限帳戶以在稍後用於攻擊步驟。 安全性帳戶管理員遠端 (SAM-R) 通訊協定是用來查詢目錄以執行這類對應的其中一種方法。

在此偵測中，在部署 ATA 之後的第一個月內不會觸發任何警示。 在學習期間，ATA 會分析哪個 SAM-R 查詢是從哪部電腦發出，包括敏感性帳戶的列舉和個別查詢。

**調查**

1. 按一下警示以移至其詳細資料頁面。 確認已執行哪些查詢 (例如 Enterprise Admins 或 Administrator)，以及查詢是否成功。

1. 這類查詢是否預期會從有問題的來源電腦發出？

1. 如果是且警示已更新，請 **隱藏** 可疑活動。

1. 如果是且不應該再這麼做，請 **關閉** 可疑活動。

1. 如果有相關帳戶的資訊：這類查詢是否預期會由該帳戶發出，或該帳戶是否通常會登入來源電腦？

   - 如果是且警示已更新，請 **隱藏** 可疑活動。

   - 如果是且不應該再這麼做，請 **關閉** 可疑活動。

   - 如果上述所有問題的答案均為否，則假設這是惡意的。

1. 如果沒有涉及之帳戶的相關資訊，您可以移至端點並檢查於警示期間登入的帳戶。

**補救**

使用 [SAMRi10 工具](https://gallery.technet.microsoft.com/SAMRi10-Hardening-Remote-48d94b5b)來強化您的環境，以防止此攻擊手法。
若此工具不適用您的網域控制站：
1. 電腦是否在執行弱點掃描工具？
1. 調查在攻擊中被查詢的特定使用者及群組是否為具有特殊權限或高價值的帳戶 (例如執行長、財務長、IT 管理等)。  若是如此，也請查看端點上的其他活動，並監視已查詢帳戶登入的電腦，因為這些可能是橫向移動的目標。

## <a name="reconnaissance-using-dns"></a>使用 DNS 探查

**描述**

您的 DNS 伺服器包含您網路中所有電腦、IP 位址和服務的對應。 攻擊者會使用這項資訊來對應您的網路結構，並鎖定感興趣的電腦以在稍後用於攻擊步驟。

DNS 通訊協定中有數種查詢類型。 ATA 會偵測源自於非 DNS 伺服器的 AXFR (傳輸) 要求。

**調查**

1. 來源電腦 (**源自於...**) 是否為 DNS 伺服器？ 如果是，則可能是誤判。 若要驗證，請按一下警示以移至其詳細資料頁面。 在表格的 [查詢] 下，確認已查詢哪些網域。 這是現有的網域嗎？ 如果是，請 **關閉** 可疑活動 (這是誤判)。 此外，請確定 ATA 閘道與來源電腦之間的 UDP 連接埠 53 已開啟，以防止未來發生誤判。
1. 來源電腦是否正在執行安全性掃描程式？ 如果是，請在 ATA 中，直接透過 **關閉並排除** 或透過 [排除] 頁面 (在 [設定] 下 - 僅適用於 ATA 系統管理員)，來 **排除** 實體。
1. 如果上述所有問題的答案都是否定的，請繼續針對來源電腦進行調查。 按一下來源電腦以移至其設定檔頁面。 檢查要求期間所發生的事件，並搜尋不尋常的活動，例如當時登入的使用者，以及被存取的資源有哪些。

**補救**

您可以停用區域傳輸，或將區域傳輸僅限於指定的 IP 位址，來保護內部 DNS 伺服器，以防止發生使用 DNS 探查。 如需限制區域傳輸的詳細資訊，請參閱 [限制區域傳輸](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ee649273(v=ws.10))。
「修改區域傳輸」是檢查清單中的一項工作，應該加以解決才能[保護 DNS 伺服器免受內部和外部攻擊](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc770432(v=ws.11))。

## <a name="reconnaissance-using-smb-session-enumeration"></a>使用 SMB 工作階段列舉的偵察

**描述**

伺服器訊息區 (SMB) 列舉可讓攻擊者取得使用者最近登入位置的相關資訊。 一旦攻擊者擁有這項資訊，他們就可以在網路中橫向移動來到達特定敏感性帳戶。

在此偵測中，對網域控制站執行 SMB 工作階段列舉時，就會觸發警示。

**調查**

1. 按一下警示以移至其詳細資料頁面。 確認哪些帳戶已執行此作業，以及已公開哪些帳戶 (如果有的話)。

   - 來源電腦上是否正在執行某種安全性掃描程式？ 如果是，請 **關閉並排除** 可疑活動。

1. 確認哪些相關使用者已執行此作業。 這些使用者是否通常會登入來源電腦，或者是否會管理應執行這類動作的人員？

1. 如果是且警示已更新，請 **隱藏** 可疑活動。

1. 如果是且不應該更新，請 **關閉** 可疑活動。

1. 如果上述所有問題的答案均為否，則假設該活動為惡意。

**補救**

使用 [Net Cease 工具](https://gallery.technet.microsoft.com/Net-Cease-Blocking-Net-1e8dcb5b)來強化您的環境，以防止此類型的攻擊。

## <a name="remote-execution-attempt-detected"></a>偵測到遠端執行嘗試

**描述**

盜用系統管理認證或使用零時差惡意探索的攻擊者可能會在您的網域控制站上執行遠端命令。 這可用於取得持續性、收集資訊、發動拒絕服務 (DOS) 的攻擊或任何其他原因。 ATA 會偵測 PSexec 和遠端 WMI 連線。

**調查**

1. 對網域控制站執行系統管理工作的系統管理工作站以及 IT 小組成員和服務帳戶經常會發生這種情況。 如果是這種情況，而且由於相同的系統管理員或電腦執行工作而更新警示，請 **隱藏** 警示。
1. 有問題的電腦是否可以對您的網域控制站執行此遠端執行？
   - 有問題的帳戶是否可以對您的網域控制站執行此遠端執行？
   - 如果這兩個問題的答案均為「是」，請 [關閉] 警示。
1. 如果針對這兩個問題的答案皆為否，則應將此活動視為真的有問題。 試著透過檢查電腦和帳戶設定檔，來找出嘗試的來源。 按一下來源電腦或帳戶以移至其設定檔頁面。 檢查這些嘗試的期間所發生的事件，並搜尋不尋常的活動，例如當時登入的使用者，以及被存取的資源有哪些。

**補救**

1. 限制從非 0 層電腦遠端存取網域控制站。

1. 實作[特殊權限存取](/windows-server/identity/securing-privileged-access/securing-privileged-access)只允許強化的電腦連線到系統管理員的網域控制站。

## <a name="sensitive-account-credentials-exposed--services-exposing-account-credentials"></a>已公開的敏感性帳戶認證與要公開帳戶認證的服務

> [!NOTE]
> 這項可疑的活動已淘汰，只會顯示在 1.9 版以前的 ATA。 若為 ATA 1.9 或更新版本，請參閱[報表](reports.md)。

**描述**

某些服務會以純文字傳送帳戶認證。 即使是敏感性帳戶也可能會發生此情況。 監視網路流量的攻擊者可能會惡意攔截並重複使用這些認證。 敏感性帳戶的任何純文字密碼都會觸發警示。若為非敏感性帳戶，如果有五個以上不同的帳戶從相同的來源電腦傳送純文字密碼，則會觸發警示。

**調查**

按一下警示以移至其詳細資料頁面。 查看已公開哪些帳戶。 如果有許多這類帳戶，請按一下 [下載詳細資料] 以檢視 Excel 試算表中的清單。

通常會在來源電腦上使用 LDAP 簡單系結的腳本或繼承應用程式。

**補救**

確認來源電腦上的設定，並確定未使用 LDAP 簡單繫結。 您可以改用 LDAP SAL 或 LDAPS，而不要使用 LDAP 簡單繫結。

## <a name="suspicious-authentication-failures"></a>可疑的驗證失敗

**描述**

在暴力密碼破解攻擊中，攻擊者會嘗試使用許多不同的密碼對不同的帳戶進行驗證，直到找到至少一個帳戶的正確密碼。 找到後，攻擊者就可以使用該帳戶登入。

在此偵測中，當發生許多使用 Kerberos 或 NTLM 的驗證失敗時就會觸發警示。這可能是在許多使用者之間使用一小組密碼 (水平分佈)，或是只有少數使用者但使用一大組密碼 (垂直分佈)，或者是這兩個選項的任意組合。 可觸發警示的最低期限為一週。

**調查**

1. 按一下 [下載詳細資料] 以在 Excel 試算表中檢視完整資訊。 您可以取得下列資訊：
   - 被攻擊帳戶的清單
   - 登入嘗試成功進行驗證之被猜測帳戶的清單
   - 如果驗證嘗試是使用 NTLM 來執行，您將會看到相關的事件活動
   - 如果驗證嘗試是使用 Kerberos 來執行，您將會看到相關的網路活動
1. 按一下來源電腦以移至其設定檔頁面。 檢查這些嘗試的期間所發生的事件，並搜尋不尋常的活動，例如當時登入的使用者，以及被存取的資源有哪些。
1. 如果驗證是使用 NTLM 來執行，且您多次看到該警示，且沒有來源電腦嘗試存取之伺服器的足夠相關資訊，則您應該對涉及的網域控制站啟用 **NTLM 稽核**。 若要這樣做，請開啟事件 8004。 這是 NTLM 驗證事件，其中包含來源電腦嘗試存取的來源電腦、使用者帳戶及 **伺服器** 的相關資訊。 知道驗證確認是由哪一部伺服器所傳送的之後，您應該透過檢查其事件 (例如 4624) 來調查它，以進一步了解驗證程序。

**補救**

[複雜和長密碼](/windows/device-security/security-policy-settings/password-policy) 提供必要的第一層安全性，以防範暴力密碼破解攻擊。

## <a name="suspicious-service-creation"></a>可疑的服務建立 <a name="suspicious-service-creation"></a>

**描述**

攻擊者嘗試在您的網路上執行可疑的服務。 當看似可疑的新服務在網域控制站上建立時，ATA 會發出警示。 這項警示依賴事件 7045，並且會受 ATA 閘道或輕量型閘道所涵蓋的每個網域控制站偵測。

**調查**

1. 若有問題的電腦為系統管理工作站，或是 IT 團隊成員及服務帳戶會在上方執行系統管理工作的電腦，此警示可能會是誤判，您可能需要 **隱藏** 警示，並視需要將它新增至排除清單。

1. 該服務是否為您在此電腦上知道的服務？

   - 有問題的 **帳戶** 是否可以安裝此服務？

   - 如果這兩個問題的答案均為「是」，請 **關閉** 警示或將它新增至排除清單。

1. 如果其中一個問題的答案為「 *否*」，則應該將此視為真肯定。

**補救**

- 在網域電腦上實作具有較低權限的存取，以僅允許特定使用者建立新的服務。

## <a name="suspicion-of-identity-theft-based-on-abnormal-behavior"></a>基於異常行為懷疑身分遭竊

**描述**

ATA 會持續三週學習使用者、電腦和資源的實體行為。 此行為模型是以下列活動為依據：實體已登入的電腦、實體已要求存取的資源，以及這些作業發生的時間。 當實體的行為是以機器學習演算法為基礎時，ATA 就會傳送警示。

**調查**

1. 有問題的使用者是否預期會執行這些作業？

1. 請將下列情況視為可能的誤判：使用者剛從假期返回工作、IT 人員執行超過其職責的存取 (例如技術支援服務在指定日期或週突然增加)、遠端桌面應用程式。此外，如果您 **關閉並排除** 警示，則不會再偵測使用者。

**補救**

 應該根據造成此異常行為發生的原因採取不同的動作。 例如，若已掃描網路，來源電腦應該會被封鎖在網路之外 (除非已獲核准)。

## <a name="unusual-protocol-implementation"></a>不尋常的通訊協定實作

**描述**

攻擊者會使用以非標準方式實作各種通訊協定 (SMB、Kerberos、NTLM) 的工具。 雖然 Windows 會接受這種類型的網路流量而不發出警告，但 ATA 能夠辨識可能的惡意用途。 此行為表示越過雜湊，以及進階勒索軟體所使用的惡意探索等技術，例如 WannaCry。

**調查**

從可疑活動時間軸找出不尋常的通訊協定，按一下可疑活動以存取其詳細資料頁面；下列通訊協定會出現在箭號上方：Kerberos 或 NTLM。

- **Kerberos**：如果已使用 Mimikatz 等駭客工具潛在使用越過雜湊攻擊，通常會觸發此警示。 檢查來源電腦所執行的應用程式是否實作自己的 Kerberos 堆疊，但該堆疊不符合 Kerberos RFC 規範。 如果是這種情況，則真的有問題，而且您可以 **關閉** 警示。 如果持續觸發警示，而且仍是這種情況，您可以 **隱藏** 警示。

- **NTLM**：可能是 WannaCry，或是 Metasploit、Medusa 和 Hydra 等工具。

若要判斷活動是否為 WannaCry 攻擊，請執行下列步驟：

1. 檢查來源電腦是否執行 Metasploit、Medusa 或 Hydra 等攻擊工具。

1. 如果找不到任何攻擊工具，請檢查來源電腦所執行的應用程式是否實作自己的 NTLM 或 SMB 堆疊。

1. 若否，請對可疑活動中的相關來源電腦執行 WannaCry 掃描程式指令碼 (例如[此掃描程式](https://github.com/apkjet/TrustlookWannaCryToolkit/tree/master/scanner))，來確認這是否由 WannaCry 所造成。 如果掃描程式判定此電腦受到感染或易受攻擊，請著手修補電腦並從網路移除及封鎖惡意程式碼。

1. 如果該指令碼判定此電腦未受到感染且不容易受攻擊，它可能仍受到感染，但已停用 SMBv1 或已修補電腦，這會影響掃描工具。

**補救**

將最新的補充程式套用到您的所有電腦，然後檢查是否已套用所有安全性更新。

1. [停用 SMBv1](https://blogs.technet.microsoft.com/filecab/2016/09/16/stop-using-smb1/)

1. [移除 WannaCry](https://support.microsoft.com/help/890830/remove-specific-prevalent-malware-with-windows-malicious-software-remo)

1. 由某些勒索軟體所控制的資料有時候可被解密。 只有當使用者尚未重新啟動或關閉電腦時，才能進行解密。 如需詳細資訊，請參閱 [Wanna Cry Ransomware](https://answers.microsoft.com/en-us/windows/forum/windows_10-security/wanna-cry-ransomware/5afdb045-8f36-4f55-a992-53398d21ed07?auth=1) (Wanna Cry 勒索軟體)

>[!NOTE]
> 若要停用可疑活動警示，請連絡支援人員。

## <a name="related-videos"></a>相關影片

- [加入安全性社群](https://channel9.msdn.com/Shows/Microsoft-Security/Join-the-Security-Community)

## <a name="see-also"></a>另請參閱

- [ATA 可疑活動腳本](https://aka.ms/ataplaybook)
- [查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
- [處理可疑活動](working-with-suspicious-activities.md)
