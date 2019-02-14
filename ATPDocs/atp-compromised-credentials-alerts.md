---
title: Azure ATP 遭入侵的認證階段安全性警示 | Microsoft Docs
d|Description: This article explains the Azure ATP alerts issued when attacks typical of the compromised credentials phase are detected against your organization.
keywords: ''
author: mlottner
ms.author: mlottner
manager: barbkess
ms.date: 1/15/2019
ms.topic: tutorial
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: e9cf68d2-36bd-4b0d-b36e-7cf7ded2618e
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 3696bf0d19957e95ab66bdc8d7de91184f437f80
ms.sourcegitcommit: 78748bfd75ae68230d72ad11010ead37d96b0c58
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/12/2019
ms.locfileid: "56077876"
---
# <a name="tutorial-compromised-credential-alerts"></a>教學課程：認證遭入侵警訊  

網路攻擊通常會針對任何可存取的實體進行，例如低權限的使用者，然後快速橫向移動，直到攻擊者得以存取有價值的資產，例如敏感性帳戶、網域系統管理員和高敏感性資料。 Azure ATP 會從整個攻擊狙殺鏈來源識別進階威脅，並予以分類為下列階段：

1. [偵察](atp-reconnaissance-alerts.md)
2. **遭入侵的認證**
3. [橫向移動](atp-lateral-movement-alerts.md)
4. [網域支配](atp-domain-dominance-alerts.md)
5. [Exfiltration](atp-exfiltration-alerts.md) 

若要深入了解如何了解所有 Azure ATP 安全性警示的結構和通用元件，請參閱[了解安全性警示](understanding-security-alerts.md)。

下列安全性警示有助於您找出並修復 Azure ATP 在網路中偵測到之**遭入侵的認證**階段可疑活動。 在本教學課程中，您將了解如何了解、分類、修復和避免下列各類攻擊：

> [!div class="checklist"]
> * Honeytoken 活動 (外部識別碼 2014)
> * 可疑的暴力密碼破解攻擊 (Kerberos、NTLM) (外部識別碼 2023)
> * 可疑的暴力密碼破解攻擊 (LDAP) (外部識別碼 2004)
> * 可疑的暴力密碼破解攻擊 (SMB) (外部識別碼 2033)
> * 可疑的 WannaCry 勒索軟體攻擊 (外部識別碼 2035)
> * 可疑的 Metasploit 入侵架構使用 (外部識別碼 2034)
> * 可疑的 VPN 連線 (外部識別碼 2025)

## <a name="honeytoken-activity-external-id-2014"></a>Honeytoken 活動 (外部識別碼 2014) 

先前的名稱：Honeytoken 活動

**描述**

Honeytoken 帳戶是假帳戶，可設定來識別和追蹤與這些帳戶相關的惡意活動。 Honeytoken 帳戶應保留未使用，同時擁有具吸引力的名稱來引誘攻擊者 (例如 SQL-Admin)。 任何來自這些帳戶的活動可能表示惡意行為。

如需 Honeytoken 帳戶的詳細資訊，請參閱[設定偵測排除範圍和 Honeytoken 帳戶](install-atp-step7.md)。

**TP、B-TP 或 FP**

1. 檢查來源電腦的擁有者是否使用 Honeytoken 帳戶，並搭配可疑活動頁面中所述的方法 (例如 Kerberos、LDAP、NTLM) 進行驗證。

    如果來源電腦的擁有者使用 Honeytoken 帳戶，並搭配警示中所述的相同方法進行驗證，請「關閉」有關 **B-TP** 活動的安全性警示。

**了解漏洞的範圍**

1. 調查[來源使用者](investigate-a-user.md)。
2. 調查[來源電腦](investigate-a-computer.md)。

**建議的補救和預防步驟**

1. 包含來源電腦。
    - 尋找執行攻擊的工具，並將它移除。
    - 尋找在活動發生期間登入的使用者，因為這些使用者可能也遭到入侵。 重設他們的密碼，並啟用 MFA。

## <a name="suspected-brute-force-attack-kerberos-ntlm-external-id-2023"></a>可疑的暴力密碼破解攻擊 (Kerberos、NTLM) (外部識別碼 2023)

先前的名稱：可疑的驗證失敗

**描述**

在暴力密碼破解攻擊中，攻擊者會嘗試對不同帳戶使用多個密碼驗證，直到找到正確的密碼為止，或在大規模密碼噴濺中使用同一個密碼，直到至少可用於一個帳戶為止。 找到驗證之後，攻擊者就可使用已驗證的帳戶登入。

在此偵測中，當使用 Kerberos、NTLM 發生多次驗證失敗，或偵測到使用密碼噴灑，就會觸發警示。 使用 Kerberos 或 NTLM 時，此類型的攻擊通常是以下列方式執行：在許多使用者之間「水平」使用少量密碼、只對一些使用者「垂直」使用大量密碼，或這兩者的任意組合。

在密碼噴灑中，攻擊者從網域控制站成功列舉有效使用者清單後，便會嘗試針對所有已知的使用者帳戶嘗試使用一個特製密碼 (一個密碼用於多個帳戶)。 如果初始密碼噴灑失敗，他們會利用其他的特製密碼再試一次，在嘗試之間通常會等候 30 分鐘。 等候時間可讓攻擊者避免觸發最常見以時間為基礎的帳戶鎖定閾值。 密碼噴灑已快速成為攻擊者和滲透測試者最愛的技術。 密碼噴灑攻擊已證明是取得組織內初始據點的有效方式，並可進行後續的橫向移動，嘗試提高權限。 可觸發警示的最低期限為一週。

**學習期間**
 <br>1 週

**TP、B-TP 或 FP**

請務必檢查是否有任何登入嘗試已結束且成功驗證。

1. 如果有任何登入嘗試已成功結束，請檢查平常是否從該來源電腦使用任何 **猜對的帳戶** 。
   - 這些帳戶失敗是否有可能是因為使用了錯誤的密碼？  
   - 與使用者確認他們是否已產生活動 (無法登入幾次後成功)。 

     如果以上問題的答案為**是**，請**關閉**有關 B-TP 活動的安全性警示。

2. 如果沒有**猜對的帳戶**，請檢查平常是否從來源電腦使用任何**受攻擊的帳戶**。
    - 檢查來源電腦上是否有搭配錯誤/舊認證執行的指令碼？
    - 如果以上問題的答案為**是**，請停止並編輯或刪除指令碼。 請**關閉**有關 B-TP 活動的安全性警示。

**了解漏洞的範圍**

1. 調查來源電腦。  
2. 在警示頁面上，檢查是否已成功猜對任何使用者。
    - 針對成功猜對的每位使用者，請[檢查其設定檔](investigate-a-user.md)來進一步調查。
3. 如果警示出現多次，且使用 NTLM 執行驗證，有時來源電腦嘗試存取的伺服器相關資訊會不足。
    1. 若要取得這項資訊，請務必對涉及的網域控制站啟用 NTLM 稽核。  
    2. 若要啟用 NTLM 稽核，請開啟事件 8004 (這是 NTLM 驗證事件，其中包含來源電腦及其嘗試存取的使用者帳戶和伺服器相關資訊)。
    3. 當您了解驗證確認是由哪一部伺服器傳送時，您可以透過檢查事件 (例如事件 4624) 對伺服器進行調查，以進一步了解驗證程序。

**建議的補救和預防步驟**

1. 重設猜對的使用者密碼，並啟用 MFA。
2. 包含來源電腦。
    - 尋找執行攻擊的工具，並將它移除。
    - 尋找在活動發生期間登入的使用者，因為這些使用者可能也遭到入侵。 重設他們的密碼，並啟用 MFA。
3. 重設來源使用者的密碼，並啟用 MFA。
4. 在組織中強制執行[複雜的長密碼](https://docs.microsoft.com/windows/device-security/security-policy-settings/password-policy)，這會提供必要的第一層安全性，以防止暴力密碼破解攻擊。

## <a name="suspected-brute-force-attack-ldap-external-id-2004"></a>可疑的暴力密碼破解攻擊 (LDAP) (外部識別碼 2004) 

先前的名稱：使用 LDAP 簡單繫結的暴力密碼破解攻擊

**描述**

在暴力密碼破解攻擊中，攻擊者會嘗試使用許多不同密碼對不同帳戶進行驗證，直到找到至少一個帳戶的正確密碼。 找到後，攻擊者就可以使用該帳戶登入。  
在此偵測中，當 Azure ATP 偵測到大量的簡單繫結驗證時，便會觸發警示。 此警示會偵測以下列方式執行的暴力密碼破解攻擊：在許多使用者之間「水平」使用少量密碼、只對一些使用者「垂直」使用大量密碼，或這兩個選項的任意組合。

**TP、B-TP 或 FP**

請務必檢查是否有任何登入嘗試已結束且成功驗證。

1. 如果有任何登入嘗試已成功結束，平常是否從該來源電腦使用任何 **猜對的帳戶** ？
   - 這些帳戶失敗是否有可能是因為使用了錯誤的密碼？  
   - 與使用者確認他們是否已產生活動 (無法登入幾次後成功)。

     如果以上問題的答案為**是**，請**關閉**有關 B-TP 活動的安全性警示。

2. 如果沒有**猜對的帳戶**，請檢查平常是否從來源電腦使用任何**受攻擊的帳戶**。
   - 檢查來源電腦上是否有搭配錯誤/舊認證執行的指令碼？

     如果以上問題的答案為**是**，請停止並編輯或刪除指令碼。 請**關閉**有關 B-TP 活動的安全性警示。

**了解漏洞的範圍**

1. 調查[來源電腦](investigate-a-computer.md)。  
2. 在警示頁面上，檢查已成功猜對哪些使用者 (如果有)。 針對成功猜對的每位使用者，請[檢查其設定檔](investigate-a-user.md)來進一步調查。

**建議的補救和預防步驟**

1. 重設猜對的使用者密碼，並啟用 MFA。
2. 包含來源電腦。
    - 尋找執行攻擊的工具，並將它移除。
    - 尋找在活動發生期間登入的使用者，因為這些使用者可能也遭到入侵。 重設他們的密碼，並啟用 MFA。
3. 重設來源使用者的密碼，並啟用 MFA。
4. 在組織中強制執行[複雜的長密碼](https://docs.microsoft.com/windows/device-security/security-policy-settings/password-policy)，這會提供必要的第一層安全性，以防止暴力密碼破解攻擊。
5. 防止未來在您的組織中使用 LDAP 純文字通訊協定。

## <a name="suspected-brute-force-attack-smb-external-id-2033"></a>可疑的暴力密碼破解攻擊 (SMB) (外部識別碼 2033) 

先前的名稱：不尋常的通訊協定實作 (可能使用 Hydra 等惡意工具)

**描述**

攻擊者會使用以非標準方式實作各種通訊協定 (例如 SMB、Kerberos 和 NTLM) 的工具。 雖然 Windows 會接受這種類型的網路流量而不發出警告，但 Azure ATP 能夠辨識可能的惡意用途。 此行為表示可能是暴力密碼破解技術。

**TP、B-TP 或 FP**

1. 檢查來源電腦是否執行如 Hydra 等攻擊工具。
   1. 如果來源電腦正在執行攻擊工具，則此警示為 **TP**。 請遵循[了解缺口的範圍](#understand-the-scope-of-the-breach)中的指示。

有時是應用程式實作自己的 NTLM 或 SMB 堆疊。

1. 檢查來源電腦是否對應用程式執行自己的 NTLM 或 SMB 堆疊類型。
    1. 如果發現執行該應用程式類型的來源電腦，且它不應該繼續執行，請視需要修正應用程式設定。 請**關閉**有關 **T-BP** 活動的安全性警示。
    2. 如果發現執行該應用程式類型的來源電腦，且它應該繼續這麼做，請**關閉**有關 **T-BP** 活動的安全性警示，並排除該電腦。

**了解漏洞的範圍**

1. 調查[來源電腦](investigate-a-computer.md)。
2. 調查[來源使用者](investigate-a-user.md) (如果有來源使用者)。

**建議的補救和預防步驟**

1. 重設被猜測之使用者的密碼，並啟用多重要素驗證。
2. 包含來源電腦
   1. 尋找執行攻擊的工具，並將它移除。
   2. 搜尋在活動期間登入的使用者，因為他們可能也遭到入侵。
   3. 重設其密碼，並啟用多重要素驗證。
3. 在組織中強制執行[複雜的長密碼](https://docs.microsoft.com/windows/security/threat-protection/security-policy-settings/password-policy)。 複雜且很長的密碼提供必要的第一層安全性，以防止暴力密碼破解攻擊。
4. [停用 SMBv1](https://blogs.technet.microsoft.com/filecab/2016/09/16/stop-using-smb1/)

## <a name="suspected-wannacry-ransomware-attack-external-id-2035"></a>可疑的 WannaCry 勒索軟體攻擊 (外部識別碼 2035)

先前的名稱：不尋常的通訊協定實作 (可能為 WannaCry 勒索軟體攻擊)

**描述**

攻擊者會使用以非標準方式實作各種通訊協定的工具。 雖然 Windows 會接受這種類型的網路流量而不發出警告，但 Azure ATP 能夠辨識可能的惡意用途。 此行為表示進階勒索軟體所使用的技術，例如 WannaCry。

**TP、B-TP 或 FP**

1. 請檢查來源電腦上是否正在執行 WannaCry。 

    - 如果正在執行 WannaCry，則此警示為 **TP**。 請遵循[了解缺口的範圍](#understand-the-scope-of-the-breach)中的指示。

有時是應用程式實作自己的 NTLM 或 SMB 堆疊。

1. 檢查來源電腦是否對應用程式執行自己的 NTLM 或 SMB 堆疊類型。 
    1. 如果發現執行該應用程式類型的來源電腦，且它不應該繼續執行，請視需要修正應用程式設定。 請**關閉**有關 **T-BP** 活動的安全性警示。
    2. 如果發現執行該應用程式類型的來源電腦，且它應該繼續這麼做，請**關閉**有關 **T-BP** 活動的安全性警示，並排除該電腦。

**了解漏洞的範圍**

1. 調查[來源電腦](investigate-a-computer.md)。
2. 調查[遭入侵的使用者](investigate-a-user.md)。

**建議的補救和預防步驟**

1. 包含來源電腦。
      - [移除 WannaCry](https://support.microsoft.com/help/890830/remove-specific-prevalent-malware-with-windows-malicious-software-remo)
      - WanaKiwi 可以解密受到某種勒索軟體支配的資料，但只適用於使用者尚未重新啟動或關閉電腦的情況。 如需詳細資訊，請參閱 [Wanna Cry Ransomware](https://answers.microsoft.com/en-us/windows/forum/windows_10-security/wanna-cry-ransomware/5afdb045-8f36-4f55-a992-53398d21ed07?auth=1) (WannaCry 勒索軟體)
      - 尋找在活動期間登入的使用者，因為他們可能也遭到入侵。 重設他們的密碼，並啟用 MFA。
2. 修補您所有的電腦，確定已套用安全性更新。 
      - [停用 SMBv1](https://blogs.technet.microsoft.com/filecab/2016/09/16/stop-using-smb1/)

## <a name="suspected-use-of-metasploit-hacking-framework-external-id-2034"></a>可疑的 Metasploit 入侵架構使用 (外部識別碼 2034)

先前的名稱：不尋常的通訊協定實作 (可能使用 Metasploit 入侵工具)

**描述**

攻擊者會使用以非標準方式實作各種通訊協定 (SMB、Kerberos、NTLM) 的工具。 雖然 Windows 會接受這種類型的網路流量而不發出警告，但 Azure ATP 能夠辨識可能的惡意用途。 此行為表示可能是使用如 Metasploit 入侵架構的技術。 

**TP、B-TP 或 FP**

1. 檢查來源電腦是否執行 Metasploit 或 Medusa 等攻擊工具。

2. 如果是，則為確判。 請遵循[了解缺口的範圍](#understand-the-scope-of-the-breach)中的指示。

有時是應用程式實作自己的 NTLM 或 SMB 堆疊。

 1. 檢查來源電腦是否對應用程式執行自己的 NTLM 或 SMB 堆疊類型。 
    1. 如果發現執行該應用程式類型的來源電腦，且它不應該繼續執行，請視需要修正應用程式設定。 請**關閉**有關 **T-BP** 活動的安全性警示。
    2. 如果發現執行該應用程式類型的來源電腦，且它應該繼續這麼做，請**關閉**有關 **T-BP** 活動的安全性警示，並排除該電腦。

**了解漏洞的範圍**

1. 調查[來源電腦](investigate-a-computer.md)。
2. 如果有來源使用者，請[調查使用者](investigate-a-user.md)。

**建議的補救和預防步驟**

1. 重設猜對的使用者密碼，並啟用 MFA。
2. 包含來源電腦。
   1. 尋找執行攻擊的工具，並將它移除。
   2. 搜尋在活動期間登入的使用者，因為他們可能也遭到入侵。 重設其密碼，並啟用多重要素驗證。
3. 重設來源使用者的密碼，並啟用 MFA。 
4. [停用 SMBv1](https://blogs.technet.microsoft.com/filecab/2016/09/16/stop-using-smb1/) 

## <a name="suspicious-vpn-connection-external-id-2025"></a>可疑的 VPN 連線 (外部識別碼 2025) 

先前的名稱：可疑 VPN 連線 

**描述**

Azure ATP 會連續一個月學習使用者 VPN 連線的實體行為。 

VPN 行為模型以使用者登入的電腦，以及使用者連線的來源位置為基礎。 

當經機器學習演算法計算，發現與使用者的行為產生偏差時，就會開啟警示。

**學習期間**

每位使用者第一次 VPN 連線起 30 天，且最近 30 天內至少 5 個 VPN 連線。

**TP、B-TP 或 FP**

1. 可疑的使用者是否應該執行這些作業？
    1. 使用者最近是否變更其位置？
    2. 使用者是否從新裝置周遊並連線？

如果以上問題的答案為是，請**關閉**有關 **B-TP** 活動的安全性警示。

**了解漏洞的範圍**

1. 調查[來源電腦](investigate-a-computer.md)。
2. 如果有來源使用者，請[調查使用者](investigate-a-user.md)。

**建議的補救和預防步驟**

1. 重設使用者的密碼，並啟用 MFA。
2. 考慮禁止此使用者使用 VPN 連線。
3. 考慮禁止此電腦使用 VPN 連線。
4. 檢查是否有其他使用者從這些位置透過 VPN 連線，並檢查這些使用者是否遭到入侵。

> [!div class="nextstepaction"]
> [橫向移動警示教學課程](atp-lateral-movement-alerts.md)

## <a name="see-also"></a>另請參閱

- [調查電腦](investigate-a-computer.md)
- [調查使用者](investigate-a-user.md)
- [使用安全性警訊](working-with-suspicious-activities.md)
- [使用橫向移動路徑](use-case-lateral-movement-path.md)
- [偵察警訊](atp-reconnaissance-alerts.md)
- [橫向移動警訊](atp-lateral-movement-alerts.md)
- [網域支配警訊](atp-domain-dominance-alerts.md)
- [外流警訊](atp-exfiltration-alerts.md)
- [查看 Azure ATP 論壇！](https://aka.ms/azureatpcommunity)
