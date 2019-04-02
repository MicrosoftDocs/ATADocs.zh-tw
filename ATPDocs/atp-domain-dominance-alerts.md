---
title: Azure ATP 網域支配安全性警示 | Microsoft Docs
d|Description: This article explains the Azure ATP alerts issued when attacks typically part of domain dominance phase efforts are detected against your organization.
keywords: ''
author: mlottner
ms.author: mlottner
manager: barbkess
ms.date: 02/03/2019
ms.topic: tutorial
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 0b3a1db5-0d43-49af-b356-7094cc85f0a5
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 40d74431d4175512bce15dcfdec8bb3b80973e30
ms.sourcegitcommit: b468d9060eb784c16b64a9cc46dbe2d246046cdd
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/30/2019
ms.locfileid: "58675280"
---
# <a name="tutorial-domain-dominance-alerts"></a>教學課程：控制網域警訊  

網路攻擊通常會針對任何可存取的實體進行，例如低權限的使用者，然後快速橫向移動，直到攻擊者得以存取有價值的資產。 敏感性帳戶、網域系統管理員或高度敏感性資料均為重要資產。 Azure ATP 會從整個攻擊狙殺鏈來源識別進階威脅，並將其分成下列幾個階段：

1. [偵察](atp-reconnaissance-alerts.md)
2. [遭入侵的認證](atp-compromised-credentials-alerts.md)
3. [橫向移動](atp-lateral-movement-alerts.md)
4. **網域支配**
5. [Exfiltration](atp-exfiltration-alerts.md)

若要深入了解如何了解所有 Azure ATP 安全性警示的結構和通用元件，請參閱[了解安全性警示](understanding-security-alerts.md)。

下列安全性警示有助於您找出並修復 Azure ATP 在網路中偵測到的**網域支配**階段可疑活動。 在本教學課程中，您將了解如何了解、分類、避免和修復下列攻擊：

> [!div class="checklist"]
> * 資料保護 API 主要金鑰的惡意要求 (外部識別碼 2020)
> * 遠端程式碼執行嘗試 (外部識別碼 2019)
> * 可疑的 DCShadow 攻擊 (網域控制站升階) (外部識別碼 2028)
> * 可疑的 DCShadow 攻擊 (網域控制站複寫要求) (外部識別碼 2029)
> * 可疑的 DCSync 攻擊 (目錄服務的複寫) (外部識別碼 2006)
> * 可疑的黃金票證使用 (加密降級) (外部識別碼 2009)
> * 可疑的黃金票證使用 (偽造的授權資料) (外部識別碼 2013)
> * 可疑的黃金票證使用 (不存在的帳戶) (外部識別碼 2027)
> * 可疑的黃金票證使用 (票證異常) (外部識別碼 2032)
> * 可疑的黃金票證使用 (時間異常) (外部識別碼 2022)
> * 可疑的萬能金鑰攻擊 (加密降級) (外部識別碼 2010)
> * 敏感性群組的可疑修改 (外部識別碼 2024)
> * 可疑的服務建立 (外部識別碼 2026)

## <a name="malicious-request-of-data-protection-api-master-key-external-id-2020"></a>資料保護 API 主要金鑰的惡意要求 (外部識別碼 2020) 

先前的名稱：惡意的資料保護私人資訊要求

**描述**

Windows 使用資料保護 API (DPAPI) 來安全地保護瀏覽器所儲存的密碼、加密檔案和其他敏感性資料。 網域控制站會保留備份的主要金鑰，該金鑰可用來解密已加入網域的 Windows 電腦上使用 DPAPI 加密的所有密碼。 攻擊者可以使用主要金鑰，來解密所有已加入網域之電腦上由 DPAPI 保護的任何祕密。
在此偵測中，當使用 DPAPI 來擷取備份的主要金鑰時，就會觸發 Azure ATP 警示。

**TP、B-TP 或FP？**

進階安全性掃描程式可能會對 Active Directory 合法產生此類型的活動。

1. 檢查來源電腦是否正在對 Active Directory 執行組織核准的進階安全性掃描程式？

    - 如果答案為**是**，且不應該執行，請修正應用程式設定。 此警示為 **B-TP** 且可能**已關閉**。
    - 如果答案為**是**，且一律應該執行此作業，請**關閉**警示並排除該電腦，這可能是 **B-TP** 活動。

**了解漏洞的範圍**

1. 調查[來源電腦](investigate-a-computer.md)。
2. 若[來源使用者](investigate-a-user.md)存在，請進行調查。

**建議的補救和預防步驟**

1. 重設來源使用者的密碼，並啟用 MFA。
2. 包含來源電腦。 
    - 尋找執行攻擊的工具，並將它移除。
    - 尋找在活動發生期間登入的使用者，因為這些使用者可能也遭到入侵。 重設他們的密碼，並啟用 MFA。
3. 遭竊的私密金鑰永不變更。 這表示動作項目一律可以使用遭竊的金鑰來解密目標網域中受保護資料。 變更此私密金鑰的方法並不存在。 
    - 若要建立金鑰，請使用目前的私密金鑰、建立金鑰，然後使用新私密金鑰來重新加密每個網域的主要金鑰。

## <a name="remote-code-execution-attempt-external-id-2019"></a>遠端程式碼執行嘗試 (外部識別碼 2019) 

先前的名稱：遠端程式碼執行嘗試

**描述**

盜用系統管理認證或使用零時差惡意探索的攻擊者可能會在您的網域控制站上執行遠端命令。 這可用於取得持續性、收集資訊、發動拒絕服務 (DOS) 的攻擊或任何其他原因。 Azure ATP 會偵測 PSexec、遠端 WMI 和 PowerShell 連線。

**TP、B-TP 或 FP**

系統管理工作站、IT 小組成員和服務帳戶都可能會對網域控制站執行合法的系統管理工作。

1. 檢查來源電腦或使用者是否應該在您的網域控制站上執行這些命令類型？  
    - 如果來源電腦或使用者應該執行這些命令類型，請**關閉**有關 **B-TP** 活動的安全性警示。  
    - 如果來源電腦或使用者應該在您的網域控制站上執行這些命令，並將繼續這麼做，則為 **B-TP** 活動。 請**關閉**安全性警示並排除電腦。


**了解漏洞的範圍**

1. 調查[來源電腦](investigate-a-computer.md)和[使用者](investigate-a-user.md)。
2. 調查[網域控制站](investigate-a-computer.md)

**建議的補救和預防步驟：**

**補救**

1. 重設來源使用者的密碼，並啟用 MFA。
2. 利用下列方式來包含網域控制站：
    - 修復遠端程式碼執行嘗試。
    - 尋找在可疑活動期間登入的使用者，因為他們可能也遭到入侵。 重設他們的密碼，並啟用 MFA。  
3. 包含來源電腦。
    - 尋找執行攻擊的工具，並將它移除。
    - 尋找在可疑活動期間登入的使用者，因為他們可能也遭到入侵。 重設他們的密碼，並啟用 MFA。

**預防**

1. 限制從非 0 層電腦遠端存取網域控制站。
2. 實作[特殊權限存取](https://technet.microsoft.com/windows-server-docs/security/securing-privileged-access/securing-privileged-access)。 只允許強化的電腦連線到系統管理員的網域控制站。
3. 在網域電腦上實作具有較低權限的存取，以授權特定使用者建立服務。 

> [!NOTE]
> 只有 ATP 感應器才支援有關嘗試使用 PowerShell 命令的遠端程式碼執行嘗試警示。

## <a name="suspected-dcshadow-attack-domain-controller-promotion-external-id-2028"></a>可疑的 DCShadow 攻擊 (網域控制站升階) (外部識別碼 2028) 

先前的名稱：可疑的網域控制站升級 (潛在的 DCShadow 攻擊)

**描述**

網域控制站陰影 (DCShadow) 攻擊是藉由惡意複寫來變更目錄物件。 透過使用複寫流程來建立惡意的網域控制站，便可以從任何電腦進行此攻擊。

在 DCShadow 攻擊中，RPC 和 LDAP 可用來：

1. 將電腦帳戶註冊為網域控制站 (使用網域系統管理員權限)。
2. 對 DRSUAPI 執行複寫 (使用授與的複寫權限)，並將變更傳送到目錄物件。

在此 Azure ATP 偵測中，當網路中的電腦嘗試註冊為 Rogue 網域控制站時，就會觸發安全性警示。

**TP、B-TP 或 FP**

如果來源電腦是網域控制站，則失敗或低確定性的解決方案可能會防止 Azure ATP 確認身分識別。  

1. 檢查來源電腦是否為網域控制站？
    如果答案為**是**，請**關閉**有關 **B-TP** 活動的警示。

同步您 Active Directory 中的變更可能需要一段時間。

1. 來源電腦是否為新升級的網域控制站？ 如果答案為**是**，請**關閉**有關 **B-TP** 活動的警示。

伺服器和應用程式可能會從 Active Directory 複寫資料，例如 Azure AD Connect 或網路效能監視裝置。 

1. 檢查此來源電腦是否應該產生此類型的活動？

    - 如果答案為**是**，但來源電腦在未來不應該繼續產生此類型的活動，請修正伺服器/應用程式的設定。 請**關閉**有關 **B-TP** 活動的安全性警示。

    - 如果答案為**是**，且來源電腦在未來應該繼續產生此類型的活動，請**關閉**有關 **B-TP** 活動的安全性警示，並排除電腦以避免發生其他良性警示。

**了解漏洞的範圍**

1. 調查[來源電腦](investigate-a-computer.md)。
2. 查看 [事件檢視器]，以了解其[目錄服務記錄檔中記錄的 Active Directory 事件](https://docs.microsoft.com/previous-versions/windows/it-pro/windows-2000-server/cc961809(v=technet.10)/) \(英文\)。 您可以使用記錄來監視 Active Directory 中的變更。 根據預設，Active Directory 只記錄重大錯誤事件，但如果此警示重複出現，請在相關的網域控制站上啟用此稽核，以供後續調查。

**建議的補救和預防步驟：**

**補救：**

1. 包含來源電腦。
    - 尋找執行攻擊的工具，並將它移除。
    - 尋找在活動發生期間登入的使用者，因為這些使用者可能也遭到入侵。 <br>重設他們的密碼，並啟用 MFA。

**預防：**

驗證下列權限：

1. 複寫目錄變更。
2. 複寫所有目錄變更。
3. 如需詳細資訊，請參閱[在 SharePoint Server 2013 中授與 Active Directory 網域服務權限，以進行設定檔同步處理](https://technet.microsoft.com/library/hh296982.aspx)。 您可以使用 [AD ACL 掃描程式](https://blogs.technet.microsoft.com/pfesweplat/2013/05/13/take-control-over-ad-permissions-and-the-ad-acl-scanner-tool/)或建立 Windows PowerShell 指令碼，以判斷誰在網域中具有這些權限。

> [!NOTE]
> 只有 ATP 感應器才支援可疑網域控制站升階 (潛在 DCShadow 攻擊) 的警示。

## <a name="suspected-dcshadow-attack-domain-controller-replication-request-external-id-2029"></a>可疑的 DCShadow 攻擊 (網域控制站複寫要求) (外部識別碼 2029) 

先前的名稱：可疑的複寫要求 (潛在的 DCShadow 攻擊)

**描述**

在 Active Directory 複寫程序中，某個網域控制站上所做的變更，會與所有網域控制站同步處理。 若有足夠的權限，攻擊者就可授與其電腦帳戶權限，以便能夠模擬網域控制站。 攻擊者會力圖起始惡意的複寫要求，以便能夠變更真正網域控制站上的 Active Directory 物件，攻擊者就能持續存在於網域中。
在此偵測中，針對受到 Azure ATP 保護的真正網域控制站，當產生了可疑的複寫要求時，就會觸發警示。 此行為表示可能是網域控制站陰影攻擊所使用的技術。

**TP、B-TP 或 FP** 

如果來源電腦是網域控制站，則失敗或低確定性的解決方案可能會防止 Azure ATP 進行識別。 

1. 檢查來源電腦是否為網域控制站？
    如果答案為**是**，請**關閉**有關 **B-TP** 活動的警示。

同步您 Active Directory 中的變更可能需要一段時間。

1. 來源電腦是否為新升級的網域控制站？ 如果答案為**是**，請**關閉**有關 **B-TP** 活動的警示。

伺服器和應用程式可能會從 Active Directory 複寫資料，例如 Azure AD Connect 或網路效能監視裝置。

1. 此來源電腦是否應該產生此類型的活動？

    - 如果答案為**是**，但來源電腦在未來不應該繼續產生此類型的活動，請修正伺服器/應用程式的設定。 請**關閉**有關 **B-TP** 活動的安全性警示。

    - 如果答案為**是**，且來源電腦在未來應該繼續產生此類型的活動，請**關閉**有關 **B-TP** 活動的安全性警示，並排除電腦以避免發生其他 **B-TP** 警示。

**了解漏洞的範圍**

1. 調查來源[電腦](investigate-a-computer.md)。

**建議的補救和預防步驟**

**補救：**

1. 包含來源電腦。
    - 尋找執行攻擊的工具，並將它移除。
    - 尋找在活動發生期間登入的使用者，因為這些使用者可能也遭到入侵。 
    <br>重設他們的密碼，並啟用 MFA。
2. 修復在網域控制站上複寫的資料。

**預防：**

驗證下列權限：

1. 複寫目錄變更。
2. 複寫所有目錄變更。
3. 如需詳細資訊，請參閱[在 SharePoint Server 2013 中授與 Active Directory 網域服務權限，以進行設定檔同步處理](https://technet.microsoft.com/library/hh296982.aspx)。 您可以使用 [AD ACL 掃描程式](https://blogs.technet.microsoft.com/pfesweplat/2013/05/13/take-control-over-ad-permissions-and-the-ad-acl-scanner-tool/)或建立 Windows PowerShell 指令碼，以判斷誰在網域中具有這些權限。

> [!NOTE]
> 只有 ATP 感應器才支援可疑複寫要求 (潛在 DCShadow 攻擊) 的警示。 

## <a name="suspected-dcsync-attack-replication-of-directory-services-external-id-2006"></a>可疑的 DCSync 攻擊 (目錄服務的複寫) (外部識別碼 2006) 

先前的名稱：惡意的目錄服務複寫

**描述**

在 Active Directory 複寫程序中，某個網域控制站上所做的變更，會與所有其他網域控制站同步處理。 若具有必要權限，攻擊者就可以起始複寫要求，讓他們擷取儲存在 Active Directory 中的資料，包括密碼雜湊。

在此偵測中，當複寫要求從非網域控制站的電腦起始時，就會觸發警示。

> [!NOTE]
> 如果有未安裝 Azure ATP 感應器的網域控制站，則 Azure ATP 不會涵蓋這些網域控制站。 在未註冊或未受保護的網域控制站上部署新網域控制站時，Azure ATP 可能無法立即將它識別為網域控制站。 強烈建議您在每個網域控制站上都安裝 Azure ATP 感應器，以便能完整涵蓋。

**TP、B-TP 或 FP**

如果來源電腦是網域控制站，則失敗或低確定性的解決方案可能會防止 Azure ATP 進行識別。   

1. 檢查來源電腦是否為網域控制站？
    如果答案為**是**，請**關閉**有關 **B-TP** 活動的警示。

同步您 Active Directory 中的變更可能需要一段時間。

1. 來源電腦是否為新升級的網域控制站？ 如果答案為**是**，請**關閉**有關 **B-TP** 活動的警示。

伺服器和應用程式可能會從 Active Directory 複寫資料，例如 Azure AD Connect 或網路效能監視裝置。

1. 此來源電腦是否應該產生此類型的活動？

    - 如果答案為**是**，但來源電腦在未來不應該繼續產生此類型的活動，請修正伺服器/應用程式的設定。 請**關閉**有關 **B-TP** 活動的安全性警示。

    - 如果答案為**是**，且來源電腦在未來應該繼續產生此類型的活動，請**關閉**有關 **B-TP** 活動的安全性警示，並排除電腦以避免發生其他良性警示。

**了解漏洞的範圍**

1. 調查來源[電腦](investigate-a-computer.md)和[使用者](investigate-a-user.md)。 

**建議的補救和預防步驟：**

**補救：**

1. 重設來源使用者的密碼，並啟用 MFA。
2. 包含來源電腦。
    - 尋找執行攻擊的工具，並將它移除。
    - 尋找在活動發生期間登入的使用者，因為這些使用者可能也遭到入侵。 重設他們的密碼，並啟用 MFA。

**預防：**

驗證下列權限：

1. 複寫目錄變更。
2. 複寫所有目錄變更。
3. 如需詳細資訊，請參閱[在 SharePoint Server 2013 中授與 Active Directory 網域服務權限，以進行設定檔同步處理](https://technet.microsoft.com/library/hh296982.aspx)。 您可以使用 [AD ACL 掃描程式](https://blogs.technet.microsoft.com/pfesweplat/2013/05/13/take-control-over-ad-permissions-and-the-ad-acl-scanner-tool/)或建立 Windows PowerShell 指令碼，來判斷誰在網域中具有這些權限。

## <a name="suspected-golden-ticket-usage-encryption-downgrade-external-id-2009"></a>可疑的黃金票證使用 (加密降級) (外部識別碼 2009) 

先前的名稱：加密降級活動

**描述**：加密降級是一種減弱 Kerberos 的方法，它會針對通常有最高加密層級的不同通訊協定欄位，降級其加密層級。 攻擊者將能較為輕鬆地對減弱的加密欄位進行離線暴力密碼破解。 利用弱式 Kerberos 加密 Cypher 的各種攻擊方法。 在此偵測中，Azure ATP 會了解電腦和使用者使用的 Kerberos 加密類型，並在使用較弱的加密且符合以下條件時向您發出警示：(1) 對來源電腦及/或使用者而言不尋常，以及 (2) 符合已知的攻擊手法。  

在黃金票證警示中，相較於先前學到的行為，來自來源電腦 TGS_REQ (服務要求) 訊息的 TGT 欄位加密方法已偵測到降級。 這不是依據時間異常偵測 (如同其他黃金票證偵測)。 此外，若發生此警示，沒有 Kerberos 驗證要求與先前由 Azure ATP 偵測到的服務要求建立關聯。
 
**TP、B-TP 或 FP**
<br>某些合法資源不支援強式加密方法，並可能觸發此警示。 


1. 所有的來源使用者是否共用某些共通項目？ 
   1. 例如，您所有的行銷人員是否都能存取特定資源，並有可能觸發警示？
   2. 檢查透過那些票證所存取的資源。 
       - 透過檢查資源服務帳戶的 *msDS-SupportedEncryptionTypes* 屬性，以在 Active Directory 中檢查這點。
   3. 若只存取一項資源，請檢查其是否為這些使用者應該存取的有效資源。  

      如果以上其中一個問題的答案為**是**，則可能為 **T-BP** 活動。 檢查資源是否可以支援強式加密方法；如有可能，請實作更強的加密方法，並**關閉**安全性警示。

應用程式可能使用較低的加密方法進行驗證。 某些應用程式會代替使用者進行驗證，例如 IIS 伺服器和 SQL Server。 

1. 檢查來源使用者是否有某些共通項目。         
   - 例如，您所有的銷售人員是否使用可能觸發警示的特定應用程式？
   - 檢查來源電腦上是否有此類型的應用程式。 
   - 檢查電腦角色。 <br>它們是否針對該工作提供這些應用程式類型？ 

     如果以上其中一個問題的答案為**是**，則可能為 **T-BP** 活動。 檢查資源是否可以支援強式加密方法；如有可能，請實作更強的加密方法，並**關閉**安全性警示。


**了解漏洞的範圍**

1. 調查[來源電腦及存取的資源](investigate-a-computer.md)。  
2. 調查[使用者](investigate-a-computer.md)。 

**建議的補救和預防步驟** 

**補救**
1. 重設來源使用者的密碼，並啟用 MFA。 
2. 包含來源電腦。 
    - 尋找執行攻擊的工具，並將它移除。
    - 尋找在活動期間登入的使用者，因為他們可能也遭到入侵。 重設他們的密碼，並啟用 MFA。
    - 如果您已安裝 Windows Defender ATP - 請利用 **klist.exe 清除**來刪除與特定登入工作階段有關的所有票證，並防止相關票證在未來遭到誤用。
2. 包含此票證所存取的資源。 
3. 根據 [KRBTGT Account Password Reset Scripts now available for customers](https://cloudblogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/) (客戶現在可以使用 KRBTGT 帳戶密碼重設指令碼) 中的指引，使用 [Reset the KRBTGT account password/keys tool](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51) (重設 KRBTGT 帳戶密碼/金鑰工具)，變更 Kerberos 票證授權票證 (KRBTGT) 密碼兩次。 
    - 重設 KRBTGT 兩次會使此網域中的所有 Kerberos 票證失效。 使此網域中的所有 Kerberos 票證失效，代表**所有**服務將會中斷，且在這些票證更新之前都不會運作，或在某些情況下重新啟動服務。 
    - **請在對 KRBTGT 進行兩次重設之前，先做好謹慎規劃。對 KRBTGT 進行兩次重設會影響環境中所有的電腦、伺服器及使用者。**

4. 確定具有 Windows Server 2012 R2 以前作業系統的所有網域控制站與 [KB3011780](https://www.microsoft.com/download/details.aspx?id=44978) 一起安裝，且 2012 R2 以前的所有成員伺服器和網域控制站已更新 [KB2496930](https://support.microsoft.com/help/2496930/ms11-013-vulnerabilities-in-kerberos-could-allow-elevation-of-privileg)。 如需詳細資訊，請參閱  [Silver PAC](https://technet.microsoft.com/library/security/ms11-013.aspx)  和  [Forged PAC](https://technet.microsoft.com/library/security/ms14-068.aspx)。

## <a name="suspected-golden-ticket-usage-forged-authorization-data-external-id-2013"></a>可疑的黃金票證使用 (偽造的授權資料) (外部識別碼 2013)

先前的名稱：使用偽造授權資料提升權限

描述：舊版 Windows Server 中的已知弱點可讓攻擊者操作專用權屬性憑證 (PAC)，這是 Kerberos 票證中包含使用者授權資料 (在 Active Directory 中為群組成員資格) 的欄位，會授與攻擊者更多權限。 
 
**TP、B-TP 或 FP**
<br>針對已透過 MS14-068 (網域控制站) 或 MS11-013 (伺服器) 修補的電腦，嘗試的攻擊不會成功，並會產生 Kerberos 錯誤。 

1. 檢查在安全性警示辨識項清單中存取哪些資源，以及嘗試已成功或失敗。  
2. 檢查是否如上所述已修補所存取的電腦？ 
    - 如果已修補電腦，請**關閉**有關 **B-TP** 活動的安全性警示。 

某些作業系統或應用程式已知會修改授權資料。 例如，Linux 和 Unix 服務本身具有可能會觸發警示的授權機制。 

1. 來源電腦是否正在執行本身有授權機制的 OS 或應用程式？  
    - 如果來源電腦正在執行此類型的授權機制，請考慮升級 OS 或修正應用程式設定。 請**關閉**有關 **B-TP** 活動的警示。 
  
**了解漏洞的範圍**
1. 調查[來源電腦](investigate-a-computer.md)。 
2. 如果有[來源使用者](investigate-a-user.md)，請進行調查。 
3. 檢查已成功存取哪些資源，並進行[調查](investigate-a-computer.md)。   
 
**建議的補救和預防步驟** 
1. 重設來源使用者的密碼，並啟用 MFA。 
2. 包含來源電腦 
    - 尋找執行攻擊的工具，並將它移除。 
    - 因為使用者可能也遭到入侵，所以請搜尋在活動期間登入的使用者。 重設他們的密碼，並啟用 MFA。 
3. 根據 [KRBTGT Account Password Reset Scripts now available for customers](https://cloudblogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/) (客戶現在可以使用 KRBTGT 帳戶密碼重設指令碼) 中的指引，使用 [Reset the KRBTGT account password/keys tool](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51) (重設 KRBTGT 帳戶密碼/金鑰工具)，變更 Kerberos 票證授權票證 (KRBTGT) 密碼兩次。 
    - 重設 KRBTGT 兩次會使此網域中的所有 Kerberos 票證失效。 使此網域中的所有 Kerberos 票證失效，代表**所有**服務將會中斷，且在這些票證更新之前都不會運作，或在某些情況下重新啟動服務。 請在對 KRBTGT 進行兩次重設之前，先做好謹慎規劃，因為這會影響環境中所有的電腦、伺服器及使用者。
4. 確定具有 Windows Server 2012 R2 以前作業系統的所有網域控制站與 [KB3011780](https://www.microsoft.com/download/details.aspx?id=44978) 一起安裝，且 2012 R2 以前的所有成員伺服器和網域控制站已更新 [KB2496930](https://support.microsoft.com/help/2496930/ms11-013-vulnerabilities-in-kerberos-could-allow-elevation-of-privileg)。 如需詳細資訊，請參閱  [Silver PAC](https://technet.microsoft.com/library/security/ms11-013.aspx)  和  [Forged PAC](https://technet.microsoft.com/library/security/ms14-068.aspx)。

## <a name="suspected-golden-ticket-usage-nonexistent-account-external-id-2027"></a>可疑的黃金票證使用 (不存在的帳戶) (外部識別碼 2027) 

先前的名稱：Kerberos 黃金票證

**描述**
 
具有網域系統管理員權限的攻擊者可能會危害 KRBTGT 帳戶。 他們可以利用 KRBTGT 帳戶建立 Kerberos 票證授權票證 (TGT)，以提供任何資源的授權，並將票證到期日設定為任何時間。 這個假 TGT 稱為「黃金票證」，可讓攻擊者取得網路持續性。 在此偵測中，不存在的帳戶會觸發警示。 
 
**TP、B-TP 或 FP**
<br>同步 Active Directory 中的變更可能需要一段時間。
1. 使用者是否為已知且有效的網域使用者？  
2. 該使用者是否為最近新增？  
3. 該使用者是否最近從 Active Directory 刪除？  

如果以上任何問題的答案為**是**，請**關閉**有關 **B-TP** 活動的警示。
 
**了解漏洞的範圍**
1. 調查[來源電腦及存取的資源](investigate-a-computer.md)。 
 
**建議的補救和預防步驟** 
1. 包含來源電腦 
    - 尋找執行攻擊的工具，並將它移除。
    - 因為使用者可能也遭到入侵，所以請搜尋在活動期間登入的使用者。 重設他們的密碼，並啟用 MFA。
    - 如果您已安裝 Windows Defender ATP - 請利用 **klist.exe 清除**來刪除與特定登入工作階段有關的所有票證，並防止相關票證在未來遭到誤用。
2. 包含此票證所存取的資源。
3. 根據 [KRBTGT Account Password Reset Scripts now available for customers](https://cloudblogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/) (客戶現在可以使用 KRBTGT 帳戶密碼重設指令碼) 中的指引，使用 [Reset the KRBTGT account password/keys tool](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51) (重設 KRBTGT 帳戶密碼/金鑰工具)，變更 Kerberos 票證授權票證 (KRBTGT) 密碼兩次。 
    - 重設 KRBTGT 兩次會使此網域中的所有 Kerberos 票證失效。 使此網域中的所有 Kerberos 票證失效，代表**所有**服務將會中斷，且在這些票證更新之前都不會運作，或在某些情況下重新啟動服務。 請在對 KRBTGT 進行兩次重設之前，先做好謹慎規劃，因為這會影響環境中所有的電腦、伺服器及使用者。

 
## <a name="suspected-golden-ticket-usage-ticket-anomaly-external-id-2032"></a>可疑的黃金票證使用 (票證異常) (外部識別碼 2032) 

**描述**：具有網域系統管理員權限的攻擊者可能會危害 KRBTGT 帳戶。 他們可以利用 KRBTGT 帳戶建立 Kerberos 票證授權票證 (TGT)，以提供任何資源的授權，並將票證到期日設定為任何時間。 這個假 TGT 稱為「黃金票證」，可讓攻擊者取得網路持續性。 此偵測特別設計用來識別這類偽造黃金票證所擁有的唯一特性。  
 
**TP、B-TP 或 FP** 

同盟服務可能會產生觸發此警示的票證。 
1. 來源電腦是否裝載產生這些票證類型的同盟服務？  
    - 如果來源電腦裝載產生這些票證類型的服務，請關閉有關 **B-TP** 活動的安全性警示。  
 
**了解漏洞的範圍**
1. 調查[來源電腦及存取的資源](investigate-a-computer.md)。 
2. 調查[來源使用者](investigate-a-user.md)。 
 
**建議的補救和預防步驟**

1. 包含來源電腦 
    - 尋找執行攻擊的工具，並將它移除。
    - 因為使用者可能也遭到入侵，所以請搜尋在活動期間登入的使用者。 重設他們的密碼，並啟用 MFA。
    - 如果您已安裝 Windows Defender ATP - 請利用 **klist.exe 清除**來刪除與特定登入工作階段有關的所有票證，並防止相關票證在未來遭到誤用。
2. 包含此票證所存取的資源。
3. 根據 [KRBTGT Account Password Reset Scripts now available for customers](https://cloudblogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/) (客戶現在可以使用 KRBTGT 帳戶密碼重設指令碼) 中的指引，使用 [Reset the KRBTGT account password/keys tool](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51) (重設 KRBTGT 帳戶密碼/金鑰工具)，變更 Kerberos 票證授權票證 (KRBTGT) 密碼兩次。 
   - 重設 KRBTGT 兩次會使此網域中的所有 Kerberos 票證失效。 使此網域中的所有 Kerberos 票證失效，代表**所有**服務將會中斷，且在這些票證更新之前都不會運作，或在某些情況下重新啟動服務。 

     **請在對 KRBTGT 進行兩次重設之前，先做好謹慎規劃。重設會影響環境中所有的電腦、伺服器及使用者。**

## <a name="suspected-golden-ticket-usage-time-anomaly-external-id-2022"></a>可疑的黃金票證使用 (時間異常) (外部識別碼 2022) 

先前的名稱：Kerberos 黃金票證

**描述**：具有網域系統管理員權限的攻擊者可能會危害 KRBTGT 帳戶。 他們可以利用 KRBTGT 帳戶建立 Kerberos 票證授權票證 (TGT)，以提供任何資源的授權，並將票證到期日設定為任何時間。 這個假 TGT 稱為「黃金票證」，可讓攻擊者取得網路持續性。 當使用 Kerberos 票證授權票證超過 [使用者票證最長存留期] 中指定的允許時間時，就會觸發此警示。 
 
**TP、B-TP 或 FP**
1. 在過去幾小時內，群組原則中的 [使用者票證最長存留期] 設定是否有任何變更，而可能影響警示？  
2. 涉及此警示的 Azure ATP 獨立感應器是否為虛擬機器？ 
    - 如果涉及 Azure ATP 獨立感應器，它最近是否從儲存狀態繼續？  
3. 網路中是否有時間同步化問題，其中並未同步所有電腦？ 
    - 按一下 [下載詳細資料] 按鈕，以檢視安全性警示報告 Excel 檔案、檢視相關網路活動，並檢查 "StartTime" 與 "DomainControllerStartTime" 之間是否有差異。

如果以上問題的答案為**是**，請**關閉**有關 **B-TP** 活動的安全性警示。 
 
**了解漏洞的範圍**
1. 調查[來源電腦及存取的資源](investigate-a-computer.md)。 
2. 調查[遭入侵的使用者](investigate-a-user.md)。 
 
**建議的補救和預防步驟** 
1. 包含來源電腦。 
    - 尋找執行攻擊的工具，並將它移除。
    - 因為使用者可能也遭到入侵，所以請搜尋在活動期間登入的使用者。 重設他們的密碼，並啟用 MFA。
    - 如果您已安裝 Windows Defender ATP - 請利用 **klist.exe 清除**來刪除與特定登入工作階段有關的所有票證，並防止相關票證在未來遭到誤用。
2. 包含此票證所存取的資源。
3. 根據 [KRBTGT Account Password Reset Scripts now available for customers](https://cloudblogs.microsoft.com/microsoftsecure/2015/02/11/krbtgt-account-password-reset-scripts-now-available-for-customers/) (客戶現在可以使用 KRBTGT 帳戶密碼重設指令碼) 中的指引，使用 [Reset the KRBTGT account password/keys tool](https://gallery.technet.microsoft.com/Reset-the-krbtgt-account-581a9e51) (重設 KRBTGT 帳戶密碼/金鑰工具)，變更 Kerberos 票證授權票證 (KRBTGT) 密碼兩次。 
   - 重設 KRBTGT 兩次會使此網域中的所有 Kerberos 票證失效。 使此網域中的所有 Kerberos 票證失效，代表**所有**服務將會中斷，且在這些票證更新之前都不會運作，或在某些情況下重新啟動服務。 

     **請在對 KRBTGT 進行兩次重設之前，先做好謹慎規劃。重設會影響環境中所有的電腦、伺服器及使用者。**

## <a name="suspected-skeleton-key-attack-encryption-downgrade-external-id-2010"></a>可疑的萬能金鑰攻擊 (加密降級) (外部識別碼 2010) 

先前的名稱：加密降級活動

**描述**：加密降級是一種減弱 Kerberos 的方法，它會針對通常有最高加密層級的不同通訊協定欄位，使用降級的加密層級。 攻擊者將能較為輕鬆地對減弱的加密欄位進行離線暴力密碼破解。 利用弱式 Kerberos 加密 Cypher 的各種攻擊方法。 在此偵測中，Azure ATP 會了解電腦和使用者所使用的 Kerberos 加密類型。 當使用下列較弱的加密時會發出警示：(1) 對來源電腦及/或使用者而言不尋常，以及 (2) 符合已知的攻擊手法。  
 
萬能金鑰是在網域控制站上執行的惡意程式碼，並可以在不知道帳戶密碼的情況下，使用任何帳戶向網域進行驗證。 此惡意程式碼通常會使用較弱的加密演算法，來推測出網域控制站上的使用者密碼。 在此警示中，從網域控制站到要求票證帳戶之先前 KRB_ERR 訊息加密所學到的行為已降級。
 
**了解漏洞的範圍**
1. 調查[網域控制站](investigate-a-computer.md)。 
2. [使用 Azure ATP 小組撰寫的掃描程式](https://gallery.technet.microsoft.com/Aorato-Skeleton-Key-24e46b73)，檢查萬能金鑰是否已影響您的網域控制站。  
3. 調查涉及的[使用者](investigate-a-user.md)和[電腦](investigate-a-computer.md)。 
 
**建議的補救和預防步驟**

1. 重設遭入侵的使用者密碼，並啟用 MFA。 
2. 包含網域控制站。 
    - 移除惡意程式碼。 如需詳細資訊，請參閱[基本架構金鑰惡意程式碼分析](https://www.virusbulletin.com/virusbulletin/2016/01/paper-digital-bian-lian-face-changing-skeleton-key-malware) \(英文\)。
    - 尋找在發生活動期間登入的使用者，因為他們可能也遭到入侵。 重設他們的密碼，並啟用 MFA。

## <a name="suspicious-modification-of-sensitive-groups-external-id-2024"></a>敏感性群組的可疑修改 (外部識別碼 2024)

**描述**：攻擊者將使用者新增至具有高權限的群組。 新增使用者是為了取得更多資源的存取權，並取得持續入侵管道。 此偵測需要分析使用者的群組修改活動，並在敏感性群組中出現異常新增時發出警示。 Azure ATP 會持續執行分析。  
 
如需 Azure ATP 中敏感性群組的定義，請參閱＜處理敏感性帳戶＞。
 
此偵測需要網域控制站上稽核的事件。 確保您的網域控制站會稽核所需事件，以稽核所需的事件。
 
**學習期間**
<br>每個 DC 從對第一個事件起四週。
 
**TP、B-TP 或 FP**
<br>合法的群組修改很少發生且經系統判定為不「正常」，這可能會觸發警示。 這些警示會視為 **B-TP**。 
1. 群組修改是否合法？ 
    - 如果群組修改合法，請**關閉**有關 **B-TP** 活動的安全性警示。
 
**了解漏洞的範圍** 
1. 調查新增至群組的使用者。 
    - 將焦點放在使用者新增至敏感性群組之後的活動。 
2. 調查來源使用者。 
    - 下載**敏感性群組修改**報告，以查看同一時段內有誰做了哪些其他修改。 
3. 調查來源使用者在活動期間已登入的電腦。 
  
**建議的補救和預防步驟** 

**補救：**

1. 重設來源使用者的密碼，並啟用 MFA。 
    - 尋找來源使用者作用中的電腦。 
    - 檢查使用者在活動期間已登入的電腦。 檢查這些電腦是否遭到入侵。 
    - 如果使用者遭到入侵，請重設其密碼，並啟用 MFA。 

**預防：**

1. 若要協助防止未來發生攻擊，請減少授權修改敏感性群組的使用者數目。 
2. 如果適用，請設定 Privileged Access Management for Active Directory。
 
## <a name="suspicious-service-creation-external-id-2026"></a>可疑的服務建立 (外部識別碼 2026)

先前的名稱：可疑的服務建立

**描述**：可疑的服務已在您組織中網域控制站上建立。 此警示需要事件 7045 來識別此可疑活動。  
 
**TP、B-TP 或 FP**
<br>系統管理工作站、IT 小組成員和服務帳戶都會對網域控制站合法執行系統管理工作。 

1. 來源使用者/電腦是否應該在網域控制站上執行這些服務類型？  
    - 如果來源使用者或電腦應該執行這些服務類型，且不應該繼續這麼做，請**關閉**有關 **B-TP** 的警示。 
    - 如果來源使用者或電腦應該執行這些服務類型，且應該繼續這麼做，請**關閉**有關 **B-TP** 的安全性警示。 
 
**了解漏洞的範圍**
1. 調查[來源使用者](investigate-a-user.md)。 
2. 調查服務建立所在的[目的地電腦](investigate-a-computer.md)。 
  
**建議的補救和預防步驟** 

**補救**
1. 重設來源使用者的密碼，並啟用 MFA。 
2. 包含網域控制站。
    - 修復可疑的服務。
    - 尋找在活動期間登入的使用者，因為他們可能也遭到入侵。 重設他們的密碼，並啟用 MFA。
3. 尋找來源使用者作用中的電腦。         
    - 檢查使用者在活動期間已登入的電腦，並檢查這些電腦是否也遭到入侵。 

**預防：**
1. 限制從非 0 層電腦遠端存取網域控制站。 
2. 實作[特殊權限存取](https://docs.microsoft.com/windows-server/identity/securing-privileged-access/securing-privileged-access)只允許經強化電腦連線到系統管理員的網域控制站。
3. 在網域電腦上實作具有較低權限的存取，只授權特定使用者建立服務。

> [!div class="nextstepaction"]
> [外流警示教學課程](atp-exfiltration-alerts.md)
 
## <a name="see-also"></a>另請參閱

- [調查電腦](investigate-a-computer.md)
- [使用安全性警訊](working-with-suspicious-activities.md)
- [使用橫向移動路徑](use-case-lateral-movement-path.md)
- [偵察警訊](atp-reconnaissance-alerts.md)
- [遭入侵的認證警訊](atp-compromised-credentials-alerts.md)
- [橫向移動警訊](atp-lateral-movement-alerts.md)
- [外流警訊](atp-exfiltration-alerts.md)
- [查看 Azure ATP 論壇！](https://aka.ms/azureatpcommunity)
