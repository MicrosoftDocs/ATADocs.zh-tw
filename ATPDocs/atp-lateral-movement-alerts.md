---
title: Azure ATP 橫向移動的安全性警訊 |Microsoft Docs
d|Description: This article explains the Azure ATP alerts issued when attacks typically part of lateral movement phase efforts are detected against your organization.
keywords: ''
author: mlottner
ms.author: mlottner
manager: barbkess
ms.date: 03/18/2019
ms.topic: tutorial
ms.collection: M365-security-compliance
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 2257eb00-8614-4577-b6a1-5c65085371f2
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 3e2dffff3d9c2c784709c323877ec74601781a05
ms.sourcegitcommit: 9252c74620abb99d8fa2b8d2cc2169018078bec9
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/19/2019
ms.locfileid: "58136855"
---
# <a name="tutorial-lateral-movement-alerts"></a>教學課程：橫向移動警訊  

一般來說，攻擊者會針對任何可存取的實體 (例如低權限使用者) 發動攻擊，再快速橫向移動，直到獲得重要資產的存取權為止。 敏感性帳戶、網域系統管理員或高度敏感性資料均為重要資產。 Azure ATP 會從整個攻擊狙殺鏈來源識別進階威脅，並將其分成下列幾個階段：

1. [偵察](atp-reconnaissance-alerts.md)
2. [遭入侵的認證](atp-compromised-credentials-alerts.md)
3. **橫向移動**
4. [網域支配](atp-domain-dominance-alerts.md)
5. [Exfiltration](atp-exfiltration-alerts.md)

若要深入了解如何了解結構和所有 Azure ATP 安全性警訊的一般元件，請參閱 [Understanding security alerts](understanding-security-alerts.md) (了解安全性警訊)。

下列安全性警訊可協助您找出並補救 Azure ATP 在您網路中偵測到的**橫向移動**階段可疑活動。 在本教學課程中，您將了解如何了解、分類、補救和防範以下各類攻擊：

> [!div class="checklist"]
> * 透過 DNS 執行遠端程式碼 (外部識別碼 2036)
> * 可疑的身分識別竊取 (雜湊傳遞) (外部識別碼 2017)
> * 可疑的身分識別竊取 (票證傳遞) (外部識別碼 2018)
> * 可疑的 NTLM 轉送攻擊 (Exchange 帳戶) (外部識別碼 2037) - 預覽
> * 可疑的 Overpass-the-Hash 攻擊 (加密降級) (外部識別碼 2008)
> * 可疑的 Overpass-the-Hash 攻擊 (Kerberos) (外部識別碼 2002)

## <a name="remote-code-execution-over-dns-external-id-2036"></a>透過 DNS 執行遠端程式碼 (外部識別碼 2036)

**描述**

2018/12/11 Microsoft 發佈了 [CVE-2018-8626](https://portal.msrc.microsoft.com/en-US/security-guidance/advisory/CVE-2018-8626)，宣布新發現在 Windows 網域名稱系統 (DNS) 伺服器中存在遠端程式碼執行弱點。 在這個弱點中，伺服器無法適當地處理要求。 成功攻擊該弱點的攻擊者，可在本機系統帳戶的環境中執行任意程式碼。 目前設定為 DNS 伺服器的 Windows 伺服器具有此弱點的風險。

在此偵測中，當懷疑針對網路中的網域控制站利用 CVE-2018-8626 安全性漏洞的 DNS 查詢時，便會觸發 Azure ATP 安全性警示。

**TP、B-TP 或 FP**

1. 目的電腦是否為最新，且已針對 CVE-2018-8626 進行修補？ 
    - 如果電腦為最新且已修補，請視為 **FP** 並**關閉**安全性警示。
2. 在攻擊發生前是否建立了服務或執行了不熟悉的程序
    - 如果沒有發現任何新的服務或不熟悉的服務，請視為 **FP** 並**關閉**安全性警示。 
3. 此攻擊類型可能使 DNS 服務當機，然後成功地執行程式碼。
    - 檢查 DNS 服務在攻擊發生前是否曾重新啟動過幾次。
    - 如果 DNS 已重新啟動，則有可能是嘗試惡意探索 CVE-2018-8626。 請將此警告視為 **TP**，並遵循**了解缺口的範圍**中的指示。 

**了解漏洞的範圍**

- 調查[來源和目的電腦](investigate-a-computer.md)。

**建議的補救和預防步驟**

**補救**

1. 包含網域控制站。 
    1. 修復遠端程式碼執行嘗試。
    2. 另外請尋找在可疑活動期間登入的使用者，因為他們可能也遭到入侵。 重設他們的密碼，並啟用 MFA。 
2. 包含來源電腦。
    1. 尋找執行攻擊的工具，並將它移除。
    2. 另外請尋找在可疑活動期間登入的使用者，因為他們可能也遭到入侵。 重設他們的密碼，並啟用 MFA。

**防範**

- 確定環境中的所有 DNS 伺服器都是最新狀態，並已針對 [CVE-2018-8626](https://portal.msrc.microsoft.com/en-US/security-guidance/advisory/CVE-2018-8626) 進行修補。 

## <a name="suspected-identity-theft-pass-the-hash-external-id-2017"></a>可疑的身分識別竊取 (雜湊傳遞) (外部識別碼 2017)

先前的名稱：使用傳遞雜湊攻擊竊取身分

**描述**

傳遞票證是一種橫向移動攻擊手法，在此攻擊中，攻擊者從一部電腦竊取使用者的 NTLM 雜湊，然後使用它來存取另一部電腦。

**TP、B-TP、或 FP？**
1. 判斷是否為使用者固定使用的電腦在使用該雜湊？ 
    - 如果是使用者固定使用的電腦在使用該雜湊，則為 **FP**，並請**關閉**該警訊。  
 
**了解漏洞的範圍**

1. 進一步調查[來源和目的電腦](investigate-a-computer.md)。  
2. 調查[遭入侵的使用者](investigate-a-computer.md)。
 
**建議的補救和預防步驟**

1. 重設來源使用者的密碼，並啟用 MFA。
2. 包含來源和目的電腦。
3. 尋找執行攻擊的工具，並將它移除。
4. 尋找在活動期間登入的使用者，因為他們可能也遭到入侵。 重設他們的密碼，並啟用 MFA。

## <a name="suspected-identity-theft-pass-the-ticket-external-id-2018"></a>可疑的身分識別竊取 (票證傳遞) (外部識別碼 2018)

先前的名稱：使用傳遞票證攻擊竊取身分

**描述**

傳遞票證是一種橫向移動攻擊手法，在此攻擊中，攻擊者從一部電腦竊取 Kerberos 票證，並重複使用竊取的票證來存取另一部電腦。 在此偵測中，會看到 Kerberos 票證用於兩部 (或多部) 不同的電腦。

**TP、B-TP、或 FP？**

識別每部電腦上票證傳遞攻擊的關鍵在於成功將 IP 解析至組織中的電腦。 

1. 檢查一或兩部電腦的 IP 位址是否屬於從過小 DHCP 集區配置的子網路，例如 VPN、VDI 或 WiFi？ 
2. IP 位址是否共用 (例如透過 NAT 裝置)？  
3. 感應器未解析一或多個目的地 IP 位址嗎？ 如果未解析目的地 IP 位址，可能表示感應器與裝置之間的正確連接埠未正確開啟。 

    如果任何上述問題的答案為**是**，請檢查來源和目的電腦是否相同。 如果相同，則為 **FP**，而且沒有任何實際的**票證傳遞**嘗試。 

當透過 Windows Server 2016 及更新版本上的 Windows 10 使用 RDP 連線的 [Remote Credential Guard](https://docs.microsoft.com/windows/security/identity-protection/remote-credential-guard) 功能時，就會出現 **B-TP** 警示。 使用警示辨識項，檢查使用者是否使用了遠端桌面連線，從來源電腦連線至目的地電腦。

1. 檢查相互關聯的辨識項。
2. 若發現相互關聯的辨識項，請檢查是否使用 Remote Credential Guard 進行 RDP 連線。 
3. 如果答案為是，則為 **T-BP** 活動，並請**關閉**安全性警訊。 

有些自訂應用程式可代表使用者轉送票證。 這些應用程式具有使用者票證的委派權限。

1. 類似上述說明的自訂應用程式類型目前在目的電腦上嗎？ 應用程式正在執行哪些服務？ 這些服務都代表使用者執行動作嗎？例如存取資料庫。
    - 如果答案為是，則為 **T-BP** 活動，並請**關閉**安全性警訊。
2. 目的電腦為委派伺服器嗎？
    - 如果答案為是，請**關閉**安全性警訊，將該電腦視為 **T-BP** 活動並予以排除。
 
**了解漏洞的範圍**

1. 調查[來源和目的電腦](investigate-a-computer.md)。  
2. 調查[遭入侵的使用者](investigate-a-computer.md)。 

**建議的補救和預防步驟**

1. 重設來源使用者的密碼，並啟用 MFA。
2. 包含來源和目的電腦。
3. 尋找執行攻擊的工具，並將它移除。
4. 因為使用者可能也遭到入侵，所以請搜尋在活動期間登入的使用者。 重設他們的密碼，並啟用 MFA。
5. 如果您已安裝 Windows Defender ATP – 請使用 **klist.exe 清除**刪除指定登入工作階段的所有票證，並防止日後再使用該票證。

## <a name="suspected-ntlm-relay-attack-exchange-account-external-id-2037---preview"></a>可疑的 NTLM 轉送攻擊 (Exchange 帳戶) (外部識別碼 2037) - 預覽

**描述**

Exchange Server 可設為使用 Exchange Server 帳戶向攻擊者所執行的遠端 HTTP 伺服器觸發 NTLM 驗證。 此伺服器會等候 Exchange Server 通訊將其自身的敏感性驗證轉送到任何其他的伺服器，或是以更有趣的方式透過 LDAP 轉送到 Active Directory，然後捕捉驗證資訊。

轉送伺服器接收到 NTLM 驗證後，即會提供原先由目標伺服器建立的挑戰。 用戶端會回應挑戰，防止攻擊者接收回應，並使用它來繼續與目標網域控制站進行 NTLM 交涉。 

在此偵測中，當 Azure ATP 識別到可疑來源使用 Exchange 帳戶認證時，便會觸發警訊。

**TP、B-TP、或 FP？**

1. 請檢查 IP 位址後方的來源電腦。 
    1. 若來源電腦是 Exchange Server，請將其視為 **FP** 活動並**關閉**安全性警訊。
    2. 判斷來源帳戶是否應從這些電腦使用 NTLM 進行驗證？ 若它們應進行驗證，請**關閉**安全性警訊，並將這些電腦視為 **B-TP** 活動而予以排除。

**了解漏洞的範圍**

1. 繼續[調查所涉及 IP 位址後方的來源電腦](investigate-a-computer.md)。  
2. 調查[來源帳戶](investigate-a-user.md)。

**建議的補救和預防步驟**

1. 包含來源電腦
    1. 尋找執行攻擊的工具，並將它移除。
    2. 因為使用者可能也遭入侵，所以請搜尋在活動發生期間登入的使用者。 重設他們的密碼，並啟用 MFA。
2. 在網域中強制使用密封 NTLMv2，並使用**網路安全性：LAN Manager 驗證層級**群組原則。 如需詳細資訊，請參閱 [LAN Manager 驗證層級指示](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/network-security-lan-manager-authentication-level)，以設定網域控制站的群組原則。 

## <a name="suspected-overpass-the-hash-attack-encryption-downgrade-external-id-2008"></a>可疑的 Overpass-the-Hash 攻擊 (加密降級) (外部識別碼 2008) 

先前的名稱：加密降級活動

**描述**

加密降級是一種減弱 Kerberos 的方法，它會針對通訊協定一般以最高加密層級加密的不同欄位，將其加密降級。 攻擊者將能較為輕鬆地對減弱的加密欄位進行離線暴力密碼破解。 利用弱式 Kerberos 加密 Cypher 的各種攻擊方法。 在此偵測中，Azure ATP 會了解電腦和使用者使用的 Kerberos 加密類型，並在使用較弱的加密且符合以下條件時向您發出警訊：對來源電腦及 (或) 使用者而言不尋常，而且符合已知的攻擊手法。 

在 Overpass-the-Hash 攻擊中，攻擊者可以透過 Kerberos AS 要求，使用遭竊的弱式雜湊建立強式票證。 在此偵測中，已偵測到執行個體。而相較於先前學到的行為 (亦即電腦使用 AES) ，來自來源電腦的 AS_REQ 訊息加密類型已降級。

**TP、B-TP、或 FP？**
1. 判斷智慧卡設定最近是否變更過。 
   - 有關帳戶的智慧卡設定最近是否變更過？  
    
     如果答案為是，則為 **T-BP** 活動，並請**關閉**安全性警訊。 

某些合法資源不支援強式加密，並可能觸發此警訊。 

2. 所有來源使用者都共用某些項目嗎？ 
   1. 比方說，您所有的行銷人員是否都能存取可能會觸發警訊的特定資源？
   2. 檢查透過那些票證所存取的資源。 
       - 透過檢查資源服務帳戶的 *msDS-SupportedEncryptionTypes* 屬性，以在 Active Directory 中檢查這點。
   3. 若只存取了一項資源，請檢查其是否為這些使用者可存取的有效資源。   

      若上述任一問題的答案為**是**，則很可能是 **T-BP** 活動。 檢查該資源是否可支援強式加密，並盡量實作強式加密，然後**關閉**安全性警訊。

**了解漏洞的範圍**

1. 調查[來源電腦](investigate-a-computer.md)。  
2. 調查[遭入侵的使用者](investigate-a-computer.md)。 

**建議的補救和預防步驟** 

**補救**
1. 重設來源使用者的密碼，並啟用 MFA。 
2. 包含來源電腦。 
3. 尋找執行攻擊的工具，並將它移除。 
4. 搜尋在活動期間登入的使用者，因為他們可能也遭到入侵。 將他們的密碼重設，並啟用 MFA  

**防範**
 
1. 將您的網域設定為支援強式加密，並移除「使用 Kerberos DES 加密類型」。 深入了解 [encryption types and Kerberos](https://blogs.msdn.microsoft.com/openspecification/2011/05/30/windows-configurations-for-kerberos-supported-encryption-type/) (加密類型和 Kerberos)。 
2. 請務必將網域功能層級設定為支援強式加密。  
3. 請優先使用支援強式加密的應用程式。

## <a name="suspected-overpass-the-hash-attack-kerberos-external-id-2002"></a>可疑的 Overpass-the-Hash 攻擊 (Kerberos) (外部識別碼 2002) 

先前的名稱：不尋常的 Kerberos 通訊協定實作 (可能為 Overpass-the-Hash 攻擊)

**描述**

攻擊者會使用以非標準方式實作各種通訊協定 (例如 Kerberos 和 SMB) 的工具。 儘管 Microsoft Windows 接受這類網路流量而不會發出任何警告，但 Azure ATP 仍可辨識潛在的惡意意圖。 此行為表示使用了多項手法，像是 Overpass-the-Hash、暴力密碼破解及進階勒索軟體惡意探索 (如 WannaCry)。

**TP、B-TP、或 FP？**

有時候應用程式會實作自己的 Kerberos 堆疊，而不是根據 Kerberos RFC。 

1. 檢查來源電腦執行的應用程式是否有其專屬的 Kerberos 堆疊，而不是以 Kerberos RFC 為依據。  
2. 如果來源電腦正在但卻**不**應執行這類應用程式，請修正應用程式設定。 請視為 **T-BP** 活動，並**關閉**安全性警訊。  
3. 如果來源電腦正在並應繼續執行這類應用程式，請視為 **T-BP** 活動，並**關閉**安全性警訊，然後排除該電腦。 

**了解漏洞的範圍**

1. 調查[來源電腦](investigate-a-computer.md)。  
2. 如有[來源使用者](investigate-a-user.md)，也請予以調查。 

**建議的補救和預防步驟** 

1. 重設遭入侵使用者的密碼，並啟用 MFA。
2. 包含來源電腦。
3. 尋找執行攻擊的工具，並將它移除。
4. 尋找在可疑活動期間登入的使用者，因為他們可能也遭到入侵。 重設他們的密碼，並啟用 MFA。  
5. 重設來源使用者的密碼，並啟用 MFA。

> [!div class="nextstepaction"]
> [網域支配警訊教學課程](atp-domain-dominance-alerts.md)

## <a name="see-also"></a>另請參閱

- [調查電腦](investigate-a-computer.md)
- [使用安全性警訊](working-with-suspicious-activities.md)
- [使用橫向移動路徑](use-case-lateral-movement-path.md)
- [偵察警訊](atp-reconnaissance-alerts.md)
- [遭入侵的認證警訊](atp-compromised-credentials-alerts.md)
- [網域支配警訊](atp-domain-dominance-alerts.md)
- [外流警訊](atp-exfiltration-alerts.md)
- [查看 Azure ATP 論壇！](https://aka.ms/azureatpcommunity)
