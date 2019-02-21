---
title: Azure ATP 偵察階段安全性警示 | Microsoft Docs
d|Description: This article explains the Azure ATP alerts issued when attacks typically part of reconnaissance phase efforts are detected against your organization.
keywords: ''
author: mlottner
ms.author: mlottner
manager: barbkess
ms.date: 02/04/2019
ms.topic: tutorial
ms.collection: M365-security-compliance
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: e9cf68d2-36bd-4b0d-b36e-7cf7ded2618e
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 09649f57041ca53ae7cdd183e60584ff37be9c9f
ms.sourcegitcommit: c48db18274edb2284e281960c6262d97f96e01d2
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/14/2019
ms.locfileid: "56264027"
---
# <a name="tutorial-reconnaissance-alerts"></a>教學課程：偵察警訊  

網路攻擊通常會針對任何可存取的實體進行，例如低權限的使用者，然後快速橫向移動，直到攻擊者得以存取有價值的資產。 敏感性帳戶、網域系統管理員或高度敏感性資料均為重要資產。 Azure ATP 會從整個攻擊狙殺鏈來源識別進階威脅，並將其分成下列幾個階段：

1. **偵察**
2. [遭入侵的認證](atp-compromised-credentials-alerts.md)
3. [橫向移動](atp-lateral-movement-alerts.md)
4. [網域支配](atp-domain-dominance-alerts.md)
5. [Exfiltration](atp-exfiltration-alerts.md) 

若要深入了解如何了解所有 Azure ATP 安全性警示的結構和通用元件，請參閱[了解安全性警示](understanding-security-alerts.md)。

下列安全性警示有助於您找出並修復 Azure ATP 在網路中偵測到的**偵察**階段可疑活動。

在本教學課程中，您將了解如何了解、分類、修復和避免下列各類攻擊：

> [!div class="checklist"]
> * 帳戶列舉偵察 (外部識別碼 2003)
> * 網路對應偵察 (DNS) (外部識別碼 2007)
> * 使用者和 IP 位址偵察 (SMB) (外部識別碼 2012)
> * 使用者和群組成員資格偵察 (SAMR) (外部識別碼 2021)

## <a name="account-enumeration-reconnaissance-external-id-2003"></a>帳戶列舉偵察 (外部識別碼 2003) 


先前的名稱：使用帳戶列舉偵查

**描述**

在帳戶列舉偵察中，攻擊者會使用含有上千筆使用者名稱的目錄或 KrbGuess 這類工具，嘗試猜測網域中的使用者名稱。

**Kerberos**：攻擊者利用這些名稱提出 Kerberos 要求，試著在網域中找到有效的使用者名稱。 如果成功猜到使用者名稱，攻擊者會收到「需要預先驗證」，而不是「未知的安全性主體」Kerberos 錯誤。

**NTLM**：攻擊者利用名稱字典來提出 NTLM 驗證要求，試著在網域中找到有效的使用者名稱。 如果成功猜到使用者名稱，攻擊者會收到 **WrongPassword (0xc000006a)** 而不是 **NoSuchUser (0xc0000064)** NTLM 錯誤。

在此警示偵測中，Azure ATP 會偵測帳戶列舉攻擊來源、猜測嘗試總次數及嘗試相符次數。 如果有太多未知的使用者，Azure ATP 會將其偵測為可疑的活動。

**TP、B-TP 或 FP**

某些伺服器和應用程式會查詢網域控制站，以判斷帳戶是否存在於合法使用情節中。

若要判斷此查詢是 **TP**、**BTP** 或 **FP**，請按一下警示以移至其詳細資料頁面：

1. 檢查來源電腦是否應該執行此類型的查詢。 在此情況下的 **B-TP** 範例可能是 Microsoft Exchange Server 或人力資源系統。

2. 檢查帳戶網域。
   - 您是否看到屬於不同網域的其他使用者？ 
     <br>伺服器設定不正確 (例如 Exchange/Skype 或 ADSF) 可能會導致出現屬於不同網域的其他使用者。
   - 請查看問題服務的設定，以修正設定不正確的問題。

     如果以上問題的答案為**是**，則為 **B-TP** 活動。 請「關閉」安全性警示。<br>

在下一個步驟中，查看來源電腦： 

1. 在可能產生這個行為的來源電腦上，有指令碼或應用程式在執行嗎？  
   - 指令碼或舊指令碼是否搭配舊的認證執行？ <br>如果是，請停止並編輯或刪除指令碼。 
   - 應用程式是否為應該在環境中執行的系統管理或安全性指令碼/應用程式？
 
     如果以上問題的答案為**是**，請「關閉」安全性警示並排除該電腦。 這可能是 **B-TP** 活動。

現在，查看帳戶：<br>
<br>攻擊者已知會使用隨機帳戶名稱字典來尋找組織中的現有帳戶名稱。

1. 不存在的帳戶看起來很眼熟嗎？  
   - 如果不存在的帳戶看起來很眼熟，有可能是已停用的帳戶，或屬於已離職的員工。
   - 檢查應用程式或指令碼，以判斷哪些帳戶仍然存在於 Active Directory 中。

     如果以上其中一個問題的答案為**是**，請「關閉」安全性警示，這可能是 **B-TP** 活動。

2. 若任何猜測意圖符合現有的帳戶名稱，攻擊者即可得知帳戶存在於您的環境中，而且可以嘗試使用暴力密碼破解，使用探索到的使用者名稱存取您的網域。 
    - 請檢查猜到的帳戶名稱，了解是否有其他可疑活動。 
    - 請檢查是否有任何相符的帳戶為敏感性帳戶。

### <a name="understand-the-scope-of-the-breach"></a>了解缺口的範圍

1. 調查來源電腦
2. 若任何猜測意圖符合現有的帳戶名稱，攻擊者即可得知帳戶存在於您的環境中，且可以使用暴力密碼破解，嘗試使用所探索使用者名稱來存取您的網域。 使用[使用者調查指南](investigate-a-user.md)調查現有的帳戶。 

### <a name="suggested-remediation-and-steps-for-prevention"></a>建議的補救和預防步驟

1. 包含來源[電腦](investigate-a-computer.md)。 
    1. 尋找執行攻擊的工具，並將它移除。
    2. 尋找在活動發生期間登入的使用者，因為這些使用者可能也遭到入侵。 
    3. 重設他們的密碼，並啟用 MFA。
2. 在組織中強制執行[複雜的長密碼](https://docs.microsoft.com/windows/device-security/security-policy-settings/password-policy)。 複雜之長密碼提供必要的第一層安全性，以防範暴力密碼破解攻擊。 暴力密碼破解攻擊通常是網路攻擊狙殺鏈中列舉後的下一個步驟。 

## <a name="network-mapping-reconnaissance-dns-external-id-2007"></a>網路對應偵察 (DNS) (外部識別碼 2007) 


先前的名稱：使用 DNS 探查

**描述**

您的 DNS 伺服器包含您網路中所有電腦、IP 位址和服務的對應。 攻擊者會使用這項資訊來對應您的網路結構，並鎖定感興趣的電腦以在稍後用於攻擊步驟。 
 
DNS 通訊協定中有數種查詢類型。 此 Azure ATP 安全性警示會偵測源自於非 DNS 伺服器的可疑 AXFR (傳輸) 要求。

**學習期間**

此警示從網域控制站監視開始有 8 天的學習期間。 

**TP、B-TP 或 FP**

1. 檢查來源電腦是否為 DNS 伺服器。

    - 如果來源電腦**是** DNS 伺服器，請關閉 **FP** 的安全性警示。 
    - 若要防止未來發生 **FP**，請確認 Azure ATP 感應器與來源電腦之間的 UDP 連接埠 53 已**開啟**。

安全性掃描程式與合法應用程式都可能會產生 DNS 查詢。 

1. 檢查此來源電腦是否應該產生此類型的活動？

    - 如果此來源電腦應該產生此類型的活動，請**關閉**有關 **B-TP** 活動的安全性警示並排除電腦。

**了解漏洞的範圍**

1. 調查[來源電腦](investigate-a-computer.md)。 

**建議的補救和預防步驟**

**補救：**
1. 包含來源電腦。 
    - 尋找執行攻擊的工具，並將它移除。
    - 尋找在活動發生期間登入的使用者，因為這些使用者可能也遭到入侵。 重設他們的密碼，並啟用 MFA。

**預防：** 請務必保護您的內部 DNS 伺服器，以防止發生使用 AXFR 查詢的未來攻擊。

1. 您可以停用區域傳輸，或[限制區域傳輸](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ee649273(v=ws.10))僅針對指定的 IP 位址，來保護您的內部 DNS 伺服器，以防止發生使用 DNS 的偵察。 「修改區域傳輸」是檢查清單中的一項工作，應該加以解決才能[保護 DNS 伺服器免受內部和外部攻擊](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/ee649273(v=ws.10))。

## <a name="user-and-ip-address-reconnaissance-smb-external-id-2012"></a>使用者和 IP 位址偵察 (SMB) (外部識別碼 2012) 


先前的名稱：使用 SMB 工作階段列舉探查

### <a name="description"></a>說明

攻擊者可以使用伺服器訊息區 (SMB) 通訊協定進行列舉，來取得使用者最近登入位置的相關資訊。 一旦攻擊者擁有這項資訊，他們就可以在網路中橫向移動來到達特定敏感性帳戶。

在此偵測中，對網域控制站執行 SMB 工作階段列舉時，就會觸發警示。 

**TP、B-TP 或 FP**

安全性掃描程式和應用程式可能會合法查詢網域控制站中是否有已開啟的 SMB 工作階段。

1. 此來源電腦是否應該產生此類型的活動？
2. 來源電腦上是否正在執行某種安全性掃描程式？  
    如果答案為是，則可能為 B-TP 活動。 請「關閉」安全性警示並排除該電腦。
3. 檢查執行該作業的使用者。
   這些使用者是否應該執行這些動作？  
    如果答案為是，請「關閉」有關 B-TP 活動的安全性警示。

**了解漏洞的範圍**

1. 調查來源電腦。  
2. 在警示頁面上，檢查是否有任何暴露的使用者。 若要進一步調查每位暴露的使用者，請檢查其設定檔。 建議您從敏感性和高調查優先順序的使用者開始調查。

**建議的補救和預防步驟**

使用 [Net Cease 工具](https://gallery.technet.microsoft.com/Net-Cease-Blocking-Net-1e8dcb5b)來強化您的環境，以防止此攻擊。

## <a name="user-and-group-membership-reconnaissance-samr-external-id-2021"></a>使用者和群組成員資格偵察 (SAMR) (外部識別碼 2021) 


先前的名稱：使用目錄服務查詢探查 

**描述**：攻擊者會使用使用者及群組成員資格偵察來對應目錄結構，並以權限帳戶為目標，為其往後的攻擊鋪路。 安全性帳戶管理員遠端 (SAM-R) 通訊協定是用來查詢目錄，以執行這類對應的其中一種方法。  
在此偵測中，在部署 Azure ATP 之後的第一個月內不會觸發任何警示 (學習期間)。 在學習期間，Azure ATP 會分析有哪個 SAM-R 查詢是從哪部電腦發出，同時包括敏感性帳戶的列舉和個別查詢。 

**學習期間**

每個網域控制站從對特定 DC 的第一個 SAMR 網路活動起四週。

**TP、B-TP 或 FP** 

1. 按一下來源電腦以移至其設定檔頁面。        
   - 來源電腦是否應該產生此類型的活動？
     - 如果是，請「關閉」有關 **B-TP** 活動的安全性警示並排除該電腦。 
   - 檢查執行該作業的使用者。
     - 這些使用者是否正常登入該來源電腦，或是否為應執行這些特定動作的系統管理員？   
     - 檢查使用者設定檔，以及與他們相關的使用者活動。 使用[使用者調查指南](investigate-a-user.md)，以了解他們的一般使用者行為和搜尋其他可疑活動。 
    
     如果對以上問題的答案為**是**，請「關閉」有關 **B-TP** 活動的警示。 
  
**了解漏洞的範圍**

1. 檢查已執行的查詢 (例如 Enterprise Admins 或 Administrator)，並判斷查詢是否成功。
2. 使用使用者調查指南調查各暴露的使用者。
3. 調查來源電腦。  
  
**建議的補救和預防步驟**

1. 包含來源電腦。
2. 尋找並移除執行攻擊的工具。
3. 因為使用者可能也遭到入侵，所以請搜尋在活動期間登入的使用者。 重設他們的密碼，並啟用 MFA。
4. 重設來源使用者的密碼，並啟用 MFA。
5. 套用網路存取，並限制允許對 SAM 群組原則發出遠端呼叫的用戶端。

> [!NOTE]
> 若要停用任何 Azure ATP 安全性警示，請連絡支援人員。

> [!div class="nextstepaction"]
> [遭入侵的認證警示教學課程](atp-compromised-credentials-alerts.md)

## <a name="see-also"></a>另請參閱

- [調查電腦](investigate-a-computer.md)
- [調查使用者](investigate-a-user.md)
- [使用安全性警訊](working-with-suspicious-activities.md)
- [遭入侵的認證警訊](atp-compromised-credentials-alerts.md)
- [橫向移動警訊](atp-lateral-movement-alerts.md)
- [網域支配警訊](atp-domain-dominance-alerts.md)
- [外流警訊](atp-exfiltration-alerts.md)
- [Azure ATP SIEM 記錄檔參考](cef-format-sa.md)
- [使用橫向移動路徑](use-case-lateral-movement-path.md)
- [查看 Azure ATP 論壇！](https://aka.ms/azureatpcommunity)