---
title: Azure ATP 外洩警訊教學課程 | Microsoft Docs
d|Description: This article explains the Azure ATP alerts issued when attacks typically part of exfiltration phase efforts are detected against your organization.
keywords: ''
author: mlottner
ms.author: mlottner
manager: barbkess
ms.date: 02/11/2019
ms.topic: tutorial
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 452d951c-5f49-4a21-ae10-9fb38c3de302
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 54e2e6df751dab47772c20d2c3cbe30665d4840b
ms.sourcegitcommit: b468d9060eb784c16b64a9cc46dbe2d246046cdd
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2019
ms.locfileid: "58674804"
---
# <a name="tutorial-exfiltration-alerts"></a>教學課程：外流警訊  

網路攻擊通常會針對低權限使用者等所有可存取的實體啟動，然後快速橫向移動，直到攻擊者得以存取有價值的資產。 敏感性帳戶、網域系統管理員或高度敏感性資料均為重要資產。 Azure ATP 會從整個攻擊狙殺鏈來源識別進階威脅，並將其分成下列幾個階段：

1. [偵察](atp-reconnaissance-alerts.md)
2. [遭入侵的認證](atp-compromised-credentials-alerts.md)
3. [橫向移動](atp-lateral-movement-alerts.md)
4. [網域支配](atp-domain-dominance-alerts.md)
5. **外洩**

若要深入了解如何理解結構和所有 Azure ATP 安全性警訊的一般元件，請參閱[理解安全性警訊](understanding-security-alerts.md)

以下安全性警訊有助於您找出並修復 Azure ATP 在網路中偵測到的**外洩**階段可疑活動。 在此教學課程中，學習如何理解、分類、防範及修復以下攻擊：

> [!div class="checklist"]
> * DNS 上的可疑通訊 (外部識別碼 2031)
> * SMB 上的資料外流 (外部識別碼 2030)

## <a name="suspicious-communication-over-dns-external-id-2031"></a>DNS 上的可疑通訊 (外部識別碼 2031) 

上一個名稱：透過 DNS 的可疑通訊

**描述**

大多數組織中的 DNS 通訊協定通常不會受到監視，而且很少會因惡意活動遭到封鎖。 這使攻擊者得以在遭入侵的電腦上濫用 DNS 通訊協定。 透過 DNS 的惡意通訊可用來竊取資料、命令和控制攻擊和/或規避公司網路限制。

**TP、B-TP 或FP？**
 
某些公司會合法地使用 DNS 進行定期通訊。 若要判斷安全性警訊的狀態：

1. 請檢查已註冊查詢網域是否屬於信任的來源，例如您的防毒提供者。  
    - 若該網域為已知且受信任的，且已允許 DNS 查詢，請將其視為 **B-TP** 活動。 關閉安全性警訊，然後將該網域從往後的警訊排除。  
    - 若已註冊的查詢網域未受信任，請指出在來源電腦上建立要求的程序。 使用 [Process Monitor](https://docs.microsoft.com/sysinternals/downloads/procmon) 可協助進行這項工作。

**了解漏洞的範圍**

1. 在應為 DNS 伺服器的目的地電腦上，檢查上述網域的記錄。
    - 與其相互關聯的 IP 為何？
    - 網域的擁有者是誰？
    - IP 的位置在哪？
1. 調查[來源和目的電腦](investigate-a-computer.md)。

**建議的補救和預防步驟**

1. 包含來源電腦。
    - 尋找執行攻擊的工具，並將它移除。
    - 因為使用者可能也遭到入侵，所以請搜尋在活動期間登入的使用者。 重設他們的密碼，並啟用 MFA。
2. 若經過調查後，發現註冊的查詢網域仍不受信任，建議封鎖目的地網域，以避免往後出現任何通訊。

> [!NOTE]
> 「透過 DNS 的可疑通訊」安全性警訊會列出可疑網域。 新的網域，或是 Azure ATP 未知或無法辨識但您組織已知或屬於其一部分的最近新增網域，都可能被關閉。

## <a name="data-exfiltration-over-smb-external-id-2030"></a>SMB 上的資料外流 (外部識別碼 2030)

**描述** 網域控制站會保留最敏感的組織資料。 以大部分的攻擊者來說，他們的優先要務之一是取得網域控制站的存取權，進而竊取您最敏感的資料。 例如，如果儲存在 DC 上的 Ntds.dit 檔案外洩，攻擊者就得以偽造 Kerberos 票證授權票證 (TGT)，進而取得所有資源的授權。 偽造的 Kerberos TGT 讓攻擊者得以任意設定票證的到期時間。 當從您受監視的網域控制站上發現可疑的資料傳輸時，就會觸發 Azure ATP **SMB 上的資料外洩**警訊。

**TP、B-TP 或 FP**
1. 這些使用者應將這些檔案複製到此電腦嗎？  
    - 若以上問題的答案為**是**，那麼請**關閉**安全性警訊，然後將該電腦視為 **B-TP** 活動排除。

**了解漏洞的範圍**
1. 調查[來源使用者](investigate-a-user.md)。  
2. 調查複本的[來源及目的地電腦](investigate-a-computer.md)。 

**建議的補救和預防步驟**
1. 重設來源使用者的密碼，並啟用 MFA。
2. 包含來源電腦。
    - 尋找執行攻擊的工具，並將它移除。
    - 尋找已複製的檔案，並予以移除。 
    <br>檢查這些檔案上是否有其他活動。 他們傳輸到的其他位置為何？ 檢查他們是否在組織網路以外傳輸？ 
    - 因為使用者可能也遭到入侵，所以請搜尋在活動期間登入的使用者。 重設他們的密碼，並啟用 MFA。
3. 若其中一個檔案是 **ntds.dit** 檔案：
    - 根據 [KRBTGT Account Password Reset Scripts now available for customers](https://cloudblogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/) (客戶現在可以使用 KRBTGT 帳戶密碼重設指令碼) 中的指引，使用 [Reset the KRBTGT account password/keys tool](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51) (重設 KRBTGT 帳戶密碼/金鑰工具)，變更 Kerberos 票證授權票證 (KRBTGT) 密碼兩次。 
    - 重設 KRBTGT 兩次會使此網域中的所有 Kerberos 票證失效。 使此網域中的所有 Kerberos 票證失效，代表**所有**服務將會中斷，且在這些票證更新之前都不會運作，或者在某些情況下重新啟動服務。

    - **請在對 KRBTGT 進行兩次重設之前，先做好謹慎規劃。對 KRBTGT 進行兩次重設會影響環境中所有的電腦、伺服器及使用者。**

   - 對網域控制站關閉所有現有的工作階段。 

## <a name="see-also"></a>另請參閱

- [調查電腦](investigate-a-computer.md)
- [使用安全性警訊](working-with-suspicious-activities.md)
- [使用橫向移動路徑](use-case-lateral-movement-path.md)
- [偵察警訊](atp-reconnaissance-alerts.md)
- [遭入侵的認證警訊](atp-compromised-credentials-alerts.md)
- [橫向移動警訊](atp-lateral-movement-alerts.md)
- [網域支配警訊](atp-domain-dominance-alerts.md)
- [查看 Azure ATP 論壇！](https://aka.ms/azureatpcommunity)
