---
title: 適用於身分識別的 Microsoft Defender：橫向移動安全性警訊
description: 本文說明偵測到組織受攻擊時 (通常在橫向移動階段)，適用於身分識別的 Microsoft Defender 所發出的警訊。
ms.date: 10/26/2020
ms.topic: tutorial
ms.openlocfilehash: 9176429ee16a905d0ef9d8afb34bcd7d55214c4e
ms.sourcegitcommit: cdb7ae4580851e25aae24d07e7d66a750aa54405
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2020
ms.locfileid: "96542709"
---
# <a name="tutorial-lateral-movement-alerts"></a>教學課程：橫向移動警訊

網路攻擊通常會針對低權限使用者等所有可存取的實體啟動，然後快速橫向移動，直到攻擊者得以存取有價值的資產。 敏感性帳戶、網域系統管理員或高度敏感性資料均為重要資產。 [!INCLUDE [Product long](includes/product-long.md)] 會從整個攻擊狙殺鏈來源識別進階威脅，並將其分成下列幾個階段：

1. [偵察](reconnaissance-alerts.md)
1. [遭入侵的認證](compromised-credentials-alerts.md)
1. **橫向移動**
1. [網域支配](domain-dominance-alerts.md)
1. [Exfiltration](exfiltration-alerts.md)

若要深入了解如何了解結構和所有 [!INCLUDE [Product short](includes/product-short.md)] 安全性警訊的一般元件，請參閱[了解安全性警訊](understanding-security-alerts.md)。 如需 **確判 (TP)** 、**良性確判 (B-TP)** 及 **誤判 (FP)** 的詳細資訊，請參閱 [安全性警訊分類](understanding-security-alerts.md#security-alert-classifications)。

下列安全性警訊可協助您找出並補救 [!INCLUDE [Product short](includes/product-short.md)] 在網路中偵測到的 **橫向移動** 階段可疑活動。 在本教學課程中，您將了解如何了解、分類、補救和防範以下各類攻擊：

> [!div class="checklist"]
>
> - 透過 DNS 執行遠端程式碼 (外部識別碼 2036)
> - 可疑的身分識別竊取 (雜湊傳遞) (外部識別碼 2017)
> - 可疑的身分識別竊取 (票證傳遞) (外部識別碼 2018)
> - 可疑的 NTLM 驗證竄改 (外部識別碼 2039)
> - 可疑的 NTLM 轉送攻擊 (Exchange 帳戶) (外部識別碼 2037)
> - 可疑的 Overpass-the-Hash 攻擊 (Kerberos) (外部識別碼 2002)
> - 可疑的 Rogue Kerberos 憑證使用方式 (外部識別碼 2047)
> - 可疑的 SMB 封包操作 (CVE-2020-0796 惡意探索)-(預覽) (外部識別碼 2406)

<!-- * Suspected overpass-the-hash attack (encryption downgrade) (external ID 2008)-->

## <a name="remote-code-execution-over-dns-external-id-2036"></a>透過 DNS 執行遠端程式碼 (外部識別碼 2036)

**描述**

2018/12/11 Microsoft 發佈了 [CVE-2018-8626](https://portal.msrc.microsoft.com/en-US/security-guidance/advisory/CVE-2018-8626)，宣布新發現在 Windows 網域名稱系統 (DNS) 伺服器中存在遠端程式碼執行弱點。 在這個弱點中，伺服器無法適當地處理要求。 成功攻擊該弱點的攻擊者，可在本機系統帳戶的環境中執行任意程式碼。 目前設定為 DNS 伺服器的 Windows 伺服器具有此弱點的風險。

在此偵測中，當懷疑針對網路中的網域控制站利用 CVE-2018-8626 安全性弱點的 DNS 查詢時，即會觸發 [!INCLUDE [Product short](includes/product-short.md)] 安全性警訊。

**學習期間**

不適用

**TP、B-TP 或 FP**

1. 目的電腦是否為最新，且已針對 CVE-2018-8626 進行修補？
    - 如果電腦為最新且已修補，請視為 **FP** 並 **關閉** 安全性警示。
1. 在攻擊發生前是否建立了服務或執行了不熟悉的程序
    - 如果沒有發現任何新的服務或不熟悉的服務，請視為 **FP** 並 **關閉** 安全性警示。
1. 此攻擊類型可能使 DNS 服務當機，然後成功地執行程式碼。
    - 檢查 DNS 服務在攻擊發生前是否曾重新啟動過幾次。
    - 如果 DNS 已重新啟動，則有可能是嘗試惡意探索 CVE-2018-8626。 請將此警告視為 **TP**，並遵循 **了解缺口的範圍** 中的指示。

**了解漏洞的範圍**

- 調查[來源和目的電腦](investigate-a-computer.md)。

**建議的補救和預防步驟**

**補救**

1. 包含網域控制站。
    1. 修復遠端程式碼執行嘗試。
    1. 另外請尋找在可疑活動期間登入的使用者，因為他們可能也遭到入侵。 重設其密碼並啟用 MFA，或者，如果您已在 Azure Active Directory Identity Protection 中設定相關的高風險使用者原則，您可以在 Cloud App Security 入口網站中使用 [**確認使用者遭入侵**](/cloud-app-security/accounts#governance-actions)動作。
1. 包含來源電腦。
    1. 尋找執行攻擊的工具，並將它移除。
    1. 另外請尋找在可疑活動期間登入的使用者，因為他們可能也遭到入侵。 重設其密碼並啟用 MFA，或者，如果您已在 Azure Active Directory Identity Protection 中設定相關的高風險使用者原則，您可以在 Cloud App Security 入口網站中使用 [**確認使用者遭入侵**](/cloud-app-security/accounts#governance-actions)動作。

**防範**

- 確定環境中的所有 DNS 伺服器都是最新狀態，並已針對 [CVE-2018-8626](https://portal.msrc.microsoft.com/en-US/security-guidance/advisory/CVE-2018-8626) 進行修補。

## <a name="suspected-identity-theft-pass-the-hash-external-id-2017"></a>可疑的身分識別竊取 (雜湊傳遞) (外部識別碼 2017)

先前的名稱：使用傳遞雜湊攻擊竊取身分

**描述**

傳遞票證是一種橫向移動攻擊手法，在此攻擊中，攻擊者從一部電腦竊取使用者的 NTLM 雜湊，然後加以使用以存取另一部電腦。

**學習期間**

不適用

**TP、B-TP、或 FP？**
1. 判斷是否為使用者固定使用的電腦在使用該雜湊？
    - 如果是使用者固定使用的電腦在使用該雜湊，則為 **FP**，並請 **關閉** 該警訊。

**了解漏洞的範圍**

1. 進一步調查[來源和目的電腦](investigate-a-computer.md)。
1. 調查[遭入侵的使用者](investigate-a-computer.md)。

**建議的補救和預防步驟**

1. 重設來源使用者的密碼並啟用 MFA，或者，如果您已在 Azure Active Directory Identity Protection 中設定相關的高風險使用者原則，您可以在 Cloud App Security 入口網站中使用 [**確認使用者遭入侵**](/cloud-app-security/accounts#governance-actions)動作。
1. 包含來源和目的電腦。
1. 尋找執行攻擊的工具，並將它移除。
1. 尋找在活動期間登入的使用者，因為他們可能也遭到入侵。 重設其密碼並啟用 MFA，或者，如果您已在 Azure Active Directory Identity Protection 中設定相關的高風險使用者原則，您可以在 Cloud App Security 入口網站中使用 [**確認使用者遭入侵**](/cloud-app-security/accounts#governance-actions)動作。

## <a name="suspected-identity-theft-pass-the-ticket-external-id-2018"></a>可疑的身分識別竊取 (票證傳遞) (外部識別碼 2018)

先前的名稱：使用傳遞票證攻擊竊取身分

**描述**

傳遞票證是一種橫向移動攻擊手法，在此攻擊中，攻擊者從一部電腦竊取 Kerberos 票證，並重複使用竊取的票證來存取另一部電腦。 在此偵測中，會看到 Kerberos 票證用於兩部 (或多部) 不同的電腦。

**學習期間**

不適用

**TP、B-TP、或 FP？**

識別每部電腦上票證傳遞攻擊的關鍵在於成功將 IP 解析至組織中的電腦。

1. 檢查一或兩部電腦的 IP 位址是否屬於從過小 DHCP 集區配置的子網路，例如 VPN、VDI 或 WiFi？
1. IP 位址是否共用 (例如透過 NAT 裝置)？
1. 感應器未解析一或多個目的地 IP 位址嗎？ 如果未解析目的地 IP 位址，可能表示感應器與裝置之間的正確連接埠未正確開啟。

    如果任何上述問題的答案為 **是**，請檢查來源和目的電腦是否相同。 如果相同，則為 **FP**，而且沒有任何實際的 **票證傳遞** 嘗試。

當透過 Windows Server 2016 及更新版本上的 Windows 10 使用 RDP 連線的 [Remote Credential Guard](/windows/security/identity-protection/remote-credential-guard) 功能時，就會出現 **B-TP** 警示。
使用警示辨識項，檢查使用者是否使用了遠端桌面連線，從來源電腦連線至目的地電腦。

1. 檢查相互關聯的辨識項。
1. 若發現相互關聯的辨識項，請檢查是否使用 Remote Credential Guard 進行 RDP 連線。
1. 如果答案為是，則為 **T-BP** 活動，並請 **關閉** 安全性警訊。

有些自訂應用程式可代表使用者轉送票證。 這些應用程式具有使用者票證的委派權限。

1. 類似上述說明的自訂應用程式類型目前在目的電腦上嗎？ 應用程式正在執行哪些服務？ 這些服務都代表使用者執行動作嗎？例如存取資料庫。
    - 如果答案為是，則為 **T-BP** 活動，並請 **關閉** 安全性警訊。
1. 目的電腦為委派伺服器嗎？
    - 如果答案為是，請 **關閉** 安全性警訊，將該電腦視為 **T-BP** 活動並予以排除。

**了解漏洞的範圍**

1. 調查[來源和目的電腦](investigate-a-computer.md)。
1. 調查[遭入侵的使用者](investigate-a-computer.md)。

**建議的補救和預防步驟**

1. 重設來源使用者的密碼並啟用 MFA，或者，如果您已在 Azure Active Directory Identity Protection 中設定相關的高風險使用者原則，您可以在 Cloud App Security 入口網站中使用 [**確認使用者遭入侵**](/cloud-app-security/accounts#governance-actions)動作。
1. 包含來源和目的電腦。
1. 尋找執行攻擊的工具，並將它移除。
1. 因為使用者可能也遭到入侵，所以請搜尋在活動期間登入的使用者。 重設其密碼並啟用 MFA，或者，如果您已在 Azure Active Directory Identity Protection 中設定相關的高風險使用者原則，您可以在 Cloud App Security 入口網站中使用 [**確認使用者遭入侵**](/cloud-app-security/accounts#governance-actions)動作。
1. 如果已安裝適用於端點的 Microsoft Defender – 請使用 **klist.exe 清除** 以刪除指定登入工作階段的所有票證，並防止日後再使用該票證。

## <a name="suspected-ntlm-authentication-tampering-external-id-2039"></a>可疑的 NTLM 驗證竄改 (外部識別碼 2039)

2019 年 6 月，Microsoft 發佈了[資訊安全漏洞 CVE-2019-1040](https://portal.msrc.microsoft.com/en-US/security-guidance/advisory/CVE-2019-1040)，宣佈在 Microsoft Windows 中探索到新的竄改漏洞，會在「中間人」攻擊能夠成功略過 NTLM MIC (訊息完整性檢查) 保護時出現。

成功惡意探索這個漏洞的惡意執行者，能夠使 NTLM 安全性功能降級，並可能成功代表其他帳戶建立已驗證的工作階段。 未修補的 Windows 伺服器有可能遇到這個漏洞。

在此偵測中，當有人對網路中網域控制站提出 [CVE-2019-1040](https://portal.msrc.microsoft.com/en-US/security-guidance/advisory/CVE-2019-1040) 中認為可能惡意探索資訊安全弱點的 NTLM 驗證要求時，即會觸發 [!INCLUDE [Product short](includes/product-short.md)] 安全性警訊。

**學習期間**

不適用

**TP、B-TP、或 FP？**

1. 包括網域控制站等相關電腦，已針對 [CVE-2019-1040](https://portal.msrc.microsoft.com/en-US/security-guidance/advisory/CVE-2019-1040) 更新為最新狀態且進行過修補嗎？
    - 若電腦已為最新版且已進行過修補，則驗證預計會失敗。 如果驗證失敗了，安全性警訊即代表失敗的嘗試，您可予以 [關閉]。

**了解漏洞的範圍**

1. 調查[來源電腦](investigate-a-computer.md)。
1. 調查[來源帳戶](investigate-a-user.md)。

**建議的補救和預防步驟**

**補救**

1. 包含來源電腦
1. 尋找執行攻擊的工具，並將它移除。
1. 因為使用者可能也遭入侵，所以請搜尋在活動發生期間登入的使用者。 重設其密碼並啟用 MFA，或者，如果您已在 Azure Active Directory Identity Protection 中設定相關的高風險使用者原則，您可以在 Cloud App Security 入口網站中使用 [**確認使用者遭入侵**](/cloud-app-security/accounts#governance-actions)動作。
1. 在網域中強制使用密封 NTLMv2，並使用 **網路安全性：LAN Manager 驗證層級** 群組原則。 如需詳細資訊，請參閱 [LAN Manager 驗證層級指示](/windows/security/threat-protection/security-policy-settings/network-security-lan-manager-authentication-level)，以設定網域控制站的群組原則。

**防範**

- 確定環境中的所有裝置都處於最新狀態，並已針對 [CVE-2019-1040](https://portal.msrc.microsoft.com/en-US/security-guidance/advisory/CVE-2019-1040) 進行修補。

## <a name="suspected-ntlm-relay-attack-exchange-account-external-id-2037"></a>可疑的 NTLM 轉送攻擊 (Exchange 帳戶) (外部識別碼 2037)

**描述**

Exchange Server 可設為使用 Exchange Server 帳戶向攻擊者所執行的遠端 HTTP 伺服器觸發 NTLM 驗證。 伺服器會等候 Exchange Server 通訊將其自身的敏感性驗證轉送到任何其他伺服器，或是以更有趣的方式透過 LDAP 轉送到 Active Directory，然後捕捉驗證資訊。

轉送伺服器接收到 NTLM 驗證後，即會提供原先由目標伺服器建立的挑戰。 用戶端會回應挑戰，防止攻擊者接收回應，並使用它來繼續與目標網域控制站進行 NTLM 交涉。

在此偵測中，當 [!INCLUDE [Product short](includes/product-short.md)] 識別到可疑來源使用 Exchange 帳戶認證時，即會觸發警訊。

**學習期間**

不適用

**TP、B-TP、或 FP？**

1. 請檢查 IP 位址後方的來源電腦。
    1. 若來源電腦是 Exchange Server，請將其視為 **FP** 活動並 **關閉** 安全性警訊。
    1. 判斷來源帳戶是否應從這些電腦使用 NTLM 進行驗證？ 若它們應進行驗證，請 **關閉** 安全性警訊，並將這些電腦視為 **B-TP** 活動而予以排除。

**了解漏洞的範圍**

1. 繼續[調查所涉及 IP 位址後方的來源電腦](investigate-a-computer.md)。
1. 調查[來源帳戶](investigate-a-user.md)。

**建議的補救和預防步驟**

1. 包含來源電腦
    1. 尋找執行攻擊的工具，並將它移除。
    1. 因為使用者可能也遭入侵，所以請搜尋在活動發生期間登入的使用者。 重設其密碼並啟用 MFA，或者，如果您已在 Azure Active Directory Identity Protection 中設定相關的高風險使用者原則，您可以在 Cloud App Security 入口網站中使用 [**確認使用者遭入侵**](/cloud-app-security/accounts#governance-actions)動作。
1. 在網域中強制使用密封 NTLMv2，並使用 **網路安全性：LAN Manager 驗證層級** 群組原則。 如需詳細資訊，請參閱 [LAN Manager 驗證層級指示](/windows/security/threat-protection/security-policy-settings/network-security-lan-manager-authentication-level)，以設定網域控制站的群組原則。

<!--
## Suspected overpass-the-hash attack (encryption downgrade) (external ID 2008)

*Previous name:* Encryption downgrade activity

**Description**

Encryption downgrade is a method of weakening Kerberos using encryption downgrade of different fields of the protocol, normally encrypted using the highest levels of encryption. A weakened encrypted field can be an easier target to offline brute force attempts. Various attack methods utilize weak Kerberos encryption cyphers. In this detection, [!INCLUDE [Product short](includes/product-short.md)] learns the Kerberos encryption types used by computers and users, and alerts you when a weaker cypher is used that is unusual for the source computer, and/or user, and matches known attack techniques.

In an over-pass-the-hash attack, an attacker can use a weak stolen hash to create a strong ticket, with a Kerberos AS request. In this detection,  instances are detected where the AS_REQ message encryption type from the source computer is downgraded, when compared to the previously learned behavior (the computer used AES).

**Learning period**

Not applicable

**TP, B-TP, or FP?**

1. Determine if the smartcard configuration recently changed.
    - Did the accounts involved recently have smartcard configurations changes?

      If the answer is yes, **Close** the security alert as a **T-BP** activity.

Some legitimate resources don't support strong encryption ciphers and may trigger this alert.

1. Do all source users share something?
    1. For example, are all of your marketing personnel accessing a specific resource that could cause the alert to be triggered?
    1. Check the resources accessed by those tickets.
       - Check this in Active Directory by checking the attribute *msDS-SupportedEncryptionTypes*, of the resource service account.
    1. If there is only one accessed resource, check if it is a valid resource for these users to access.

      If the answer to one of the previous questions is **yes**, it is likely to be a **T-BP** activity. Check if the resource can support a strong encryption cipher, implement a stronger encryption cipher where possible, and **Close** the security alert.

**Understand the scope of the breach**

1. Investigate the [source computer](investigate-a-computer.md).
1. Investigate the [compromised user](investigate-a-computer.md).

**Suggested remediation and steps for prevention**

**Remediation**

1. Reset the password of the source user and enable MFA or, if you have configured the relevant high-risk user policies in Azure Active Directory Identity Protection, you can use the [**Confirm user compromised**](/cloud-app-security/accounts#governance-actions) action in the Cloud App Security portal.
1. Contain the source computer.
1. Find the tool that performed the attack and remove it.
1. Look for users logged on around the time of the activity, as they may also be compromised. Reset their passwords and enable MFA or, if you have configured the relevant high-risk user policies in Azure Active Directory Identity Protection, you can use the [**Confirm user compromised**](/cloud-app-security/accounts#governance-actions) action in the Cloud App Security portal.

**Prevention**

1. Configure your domain to support strong encryption cyphers, and remove *Use Kerberos DES encryption types*. Learn more about [encryption types and Kerberos](/archive/blogs/openspecification/windows-configurations-for-kerberos-supported-encryption-type).
1. Make sure the domain functional level is set to support strong encryption cyphers.
1. Give preference to using applications that support strong encryption cyphers.
-->

## <a name="suspected-overpass-the-hash-attack-kerberos-external-id-2002"></a>可疑的 Overpass-the-Hash 攻擊 (Kerberos) (外部識別碼 2002)

先前的名稱：不尋常的 Kerberos 通訊協定實作 (可能為 Overpass-the-Hash 攻擊)

**描述**

攻擊者會使用以非標準方式實作各種通訊協定 (例如 Kerberos 和 SMB) 的工具。 儘管 Microsoft Windows 接受這類網路流量而不會發出任何警告，但 [!INCLUDE [Product short](includes/product-short.md)] 仍可辨識潛在的惡意意圖。 此行為表示使用了多項手法，像是 Overpass-the-Hash、暴力密碼破解及進階勒索軟體惡意探索 (如 WannaCry)。

**學習期間**

不適用

**TP、B-TP、或 FP？**

有時候應用程式會實作自己的 Kerberos 堆疊，而不是根據 Kerberos RFC。

1. 檢查來源電腦執行的應用程式是否有其專屬的 Kerberos 堆疊，而不是以 Kerberos RFC 為依據。
1. 如果來源電腦正在但卻 **不** 應執行這類應用程式，請修正應用程式設定。 請視為 **T-BP** 活動，並 **關閉** 安全性警訊。
1. 如果來源電腦正在並應繼續執行這類應用程式，請視為 **T-BP** 活動，並 **關閉** 安全性警訊，然後排除該電腦。

**了解漏洞的範圍**

1. 調查[來源電腦](investigate-a-computer.md)。
1. 如有[來源使用者](investigate-a-user.md)，也請予以調查。

**建議的補救和預防步驟**

1. 重設遭入侵之使用者的密碼並啟用 MFA，或者，如果您已在 Azure Active Directory Identity Protection 中設定相關的高風險使用者原則，您可以在 Cloud App Security 入口網站中使用 [**確認使用者遭入侵**](/cloud-app-security/accounts#governance-actions)動作。
1. 包含來源電腦。
1. 尋找執行攻擊的工具，並將它移除。
1. 尋找在可疑活動期間登入的使用者，因為他們可能也遭到入侵。 重設其密碼並啟用 MFA，或者，如果您已在 Azure Active Directory Identity Protection 中設定相關的高風險使用者原則，您可以在 Cloud App Security 入口網站中使用 [**確認使用者遭入侵**](/cloud-app-security/accounts#governance-actions)動作。
1. 重設來源使用者的密碼並啟用 MFA，或者，如果您已在 Azure Active Directory Identity Protection 中設定相關的高風險使用者原則，您可以在 Cloud App Security 入口網站中使用 [**確認使用者遭入侵**](/cloud-app-security/accounts#governance-actions)動作。

<!-- REMOVE BOOKMARK FROM TITLE WHEN PREVIEW REMOVED -->

<a name="suspected-smb-packet-manipulation-cve-2020-0796-exploitation-external-id-2406"></a>

## <a name="suspected-rogue-kerberos-certificate-usage-external-id-2047"></a>可疑的 Rogue Kerberos 憑證使用方式 (外部識別碼 2047)

**描述**

Rogue 憑證攻擊為攻擊者取得組織控制權後，所使用的一種持續性技術。 攻擊者會入侵憑證授權單位 (CA) 伺服器，並產生可在未來攻擊中用作後門程式帳戶的憑證。

**學習期間**

不適用

**TP、B-TP 或 FP**

- 判斷帳戶是否定期登入電腦？
  - 如果電腦定期使用該憑證，請將該警訊 **關閉** 為 **FP**。

**了解漏洞的範圍**

1. 調查[來源電腦](investigate-a-computer.md)。
2. 調查[來源使用者](investigate-a-user.md)。
3. 檢查已成功存取哪些資源，並進行[調查](investigate-a-computer.md)。

**建議的補救和預防步驟**

1. 重設來源使用者的密碼並啟用 MFA，或者，如果您已在 Azure Active Directory Identity Protection 中設定相關的高風險使用者原則，您可以在 Cloud App Security 入口網站中使用 [**確認使用者遭入侵**](/cloud-app-security/accounts#governance-actions)動作。
1. 包含來源電腦
    - 尋找執行攻擊的工具，並將它移除。
    - 因為使用者可能也遭到入侵，所以請搜尋在活動期間登入的使用者。 重設其密碼並啟用 MFA，或者，如果您已在 Azure Active Directory Identity Protection 中設定相關的高風險使用者原則，您可以在 Cloud App Security 入口網站中使用 [**確認使用者遭入侵**](/cloud-app-security/accounts#governance-actions)動作。
1. 尋找 CA 伺服器中使用的憑證，並在其排定的到期日前使 TLS/SSL 失效，藉以撤銷憑證。

## <a name="suspected-smb-packet-manipulation-cve-2020-0796-exploitation---preview-external-id-2406"></a>可疑的 SMB 封包操作 (CVE-2020-0796 惡意探索)-(預覽) (外部識別碼 2406)

**描述**

2020 年 3月 12 日 Microsoft 發佈了 [CVE-2020-0796](https://portal.msrc.microsoft.com/en-US/security-guidance/advisory/CVE-2020-0796)，並宣佈在 Microsoft 伺服器訊息區 3.1.1 (SMBv3) 通訊協定處理特定要求的方式中，近期出現遠端程式碼的執行弱點。 成功惡意探索到此漏洞的攻擊者，即可在目標伺服器或用戶端上執行程式碼。 未經修補的 Windows 伺服器即有暴露在此弱點下的風險。

在此偵測中，若懷疑 SMBv3 封包會對網路中的網域控制站惡意探索 CVE-2020-0796 安全性弱點時，即會觸發 [!INCLUDE [Product short](includes/product-short.md)] 安全性警訊。

**學習期間**

不適用

**TP、B-TP、或 FP？**

1. 相關的網域控制站已更新到最新，並針對 CVE-2020-0796 進行修補嗎？
    - 若電腦已為最新狀態並已進行過修補，則攻擊應會失敗，請 **終止** 此安全性警示，標為嘗試失敗。

**了解漏洞的範圍**

1. 調查[來源電腦](investigate-a-computer.md)。
1. 調查目的網域控制站。

**建議的補救和預防步驟**

**補救**

1. 包含來源電腦。
1. 尋找執行攻擊的工具，並將它移除。
1. 尋找在可疑活動期間登入的使用者，因為他們可能也遭到入侵。 重設其密碼並啟用 MFA，或者，如果您已在 Azure Active Directory Identity Protection 中設定相關的高風險使用者原則，您可以在 Cloud App Security 入口網站中使用 [**確認使用者遭入侵**](/cloud-app-security/accounts#governance-actions)動作。
1. 如果您電腦的作業系統不支援 [KB4551762](https://www.catalog.update.microsoft.com/Search.aspx?q=KB4551762)，建議您在環境中停用 SMBv3 壓縮功能，如[因應措施](https://portal.msrc.microsoft.com/en-US/security-guidance/advisory/CVE-2020-0796)一節中所述。

**防範**

1. 確定環境中的所有裝置都針對 [CVE-2020-0796](https://portal.msrc.microsoft.com/en-US/security-guidance/advisory/CVE-2020-0796) 更新為最新狀態且已進行過修補。

> [!div class="nextstepaction"]
> [網域支配警訊教學課程](domain-dominance-alerts.md)

## <a name="see-also"></a>另請參閱

- [調查電腦](investigate-a-computer.md)
- [使用安全性警訊](working-with-suspicious-activities.md)
- [使用橫向移動路徑](use-case-lateral-movement-path.md)
- [偵察警訊](reconnaissance-alerts.md)
- [遭入侵的認證警訊](compromised-credentials-alerts.md)
- [網域支配警訊](domain-dominance-alerts.md)
- [外流警訊](exfiltration-alerts.md)
- [查看[!INCLUDE [Product short](includes/product-short.md)] 論壇！](https://aka.ms/MDIcommunity)\(英文\)
