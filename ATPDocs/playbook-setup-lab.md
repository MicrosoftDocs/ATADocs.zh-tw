---
title: Azure ATP 安全性警示實驗室設定教學課程
description: 在此教學課程中，您會設定 Azure ATP 測試實驗室來模擬威脅以供 Azure ATP 偵測。
ms.service: azure-advanced-threat-protection
ms.topic: how-to
author: shsagir
ms.author: shsagir
ms.date: 02/28/2019
ms.reviewer: itargoet
ms.openlocfilehash: 5b7bc09b0327260504900c6a0b075b243c02f70e
ms.sourcegitcommit: 0c356b0860ae8663254e0cf6f04001bcc91ce207
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/21/2020
ms.locfileid: "90828177"
---
# <a name="tutorial-setup-an-atp-security-alert-lab"></a>教學課程：設定 ATP 安全性警示實驗室 

 Azure ATP 安全性警示實驗室的目的是要說明 **Azure ATP**的功能，以找出並偵測可疑活動以及對網路的潛在攻擊。 這個四部分系列中的第一個教學課程會逐步引導您建立一個實驗室環境，以針對 Azure ATP 的「離散」** 偵測進行測試。 安全性警示實驗室的焦點是放在 Azure ATP 的「簽章型」** 功能上。 此實驗室並不包括進階機器學習、使用者或實體型的行為偵測，因為這些偵測需要一個最多有 30 天真實網路流量的學習期間。 如需有關本系列每個教學課程的詳細資訊，請參閱 [ATP 安全性警示實驗室概觀](playbook-lab-overview.md)。 


在本教學課程中，您將： 

> [!div class="checklist"]
> * 設定您的實驗室伺服器和電腦
> * 為 Active Directory 設定使用者和群組
> * 安裝及設定 Azure ATP
> * 為您的伺服器和電腦設定本機原則
> * 使用排定的工作來模擬服務台管理案例

## <a name="prerequisites"></a>Prerequisites

1. [一個實驗室網域控制站和兩個實驗室工作站](#servers-and-computers)。
   - 繼續並[藉由使用者將 Active Directory (AD) 序列化](#bkmk_hydrate)。
1. 一個[已連線至 AD](install-step2.md) 的 [Azure ATP 執行個體](install-step1.md)。
1. 在您實驗室的網域控制站上[下載](install-step3.md)並[安裝最新版的 Azure ATP 感應器](install-step4.md)。
1. 熟悉[特殊權限存取工作站](/windows-server/identity/securing-privileged-access/privileged-access-workstations)和 [SAMR 原則](/windows/security/threat-protection/security-policy-settings/network-access-restrict-clients-allowed-to-make-remote-sam-calls)。

## <a name="recommendations"></a>建議

建議您儘可能完全依照實驗室設定指示進行操作。 您的實驗室與建議的實驗室設定越相似，就越容易依照 Azure ATP 測試程序進行操作。 在實驗室設定完成之後，您將可以使用建議的入侵研究工具來執行動作，然後檢閱 Azure ATP 對這些動作的偵測。

您的完整實驗室設定應該看起來儘可能與下圖類似：

![Azure ATP 測試實驗室設定](media/playbook-atp-setup-lab.png)

### <a name="servers-and-computers"></a>伺服器和電腦

下表詳細說明電腦及所需的設定。 提供的 IP 位址僅供參考，以便您輕鬆照著操作。

在這些教學課程的範例中，「樹系 NetBIOS」名稱為 **CONTOSO.AZURE**。

|  FQDN | OS | IP | 用途 |
|------|-------|---------|--------------|
| ContosoDC.contoso.azure | Windows Server 2012 R2 | 10.0.24.4 | 將 Azure ATP 感應器安裝在本機的網域控制站 |
| VictimPC.contoso.azure | Windows 10 | 10.0.24.5 |受害者的電腦 |
| AdminPC.contoso.azure | Windows 10  | 10.0.24.6 | 網域系統管理員的電腦 (有時稱為「安全系統管理員工作站」或「特殊權限系統管理員工作站」) |

### <a name="active-directory-users-and-groups"></a>Active Directory 使用者和群組

在本實驗室中，有三個主要使用者和一個服務帳戶。 服務帳戶是 Azure ATP 的服務帳戶，並同時用於 LDAP 同步處理目的和 SAMR。

有一個 "Helpdesk" 安全性群組 (SG)，其中 Ron HelpDesk 為其成員。 這個 SG 會模擬「服務台」。 此 SG 會與賦予我們 Helpdesk 成員個別電腦上「本機系統管理員」權限的「群組原則物件」配對。 此設定是用來模擬生產環境中的實際系統管理模型。

| 全名    | SAMAccount |用途|
|--------------|------------|--------------------------------------------------------------------------------------------------|
| Jeff Leatherman  | JeffL  | 即將成為令人印象深刻之有效網路釣魚攻擊的受害者  |
| Ron HelpDesk  | RonHD  |Ron 是 Contoso IT 團隊中的「問題解決者」。 RonHD 是 "Helpdesk" 安全性群組的成員。 |
| Samira Abbasi | SamiraA  | 在 Contoso，此使用者是我們的「網域系統管理員」。 |
| Azure ATP 服務 | AATPService | Azure ATP 的服務帳戶 |

## <a name="azure-atp-base-lab-environment"></a>Azure ATP 基礎實驗室環境

為了設定基礎實驗室，我們將為 Active Directory 新增使用者和群組、編輯 SAM 原則，以及在 Azure ATP 中新增敏感性群組。

### <a name="hydrate-active-directory-users-on-contosodc"></a><a name="bkmk_hydrate"></a> 將 ContosoDC 上的 Active Directory 使用者序列化

為了簡化此實驗室，我們已將在 Active Directory 中建立虛構使用者和群組的程序自動化。 此指令碼會作為此教學課程的先決條件來執行。 您可以使用或修改此指令碼，以將您實驗室的 Active Directory 環境序列化。 如果您偏好不使用指令碼，則可以手動執行。

以網域系統管理員身分，在 ContosoDC 上執行以下指令碼，以將 Active Directory 使用者序列化：

``` PowerShell

# Store the user passwords as variables
$SamiraASecurePass = ConvertTo-SecureString -String 'NinjaCat123' -AsPlainText -Force
$ronHdSecurePass = ConvertTo-SecureString -String 'FightingTiger$' -AsPlainText -Force
$jefflSecurePass = ConvertTo-SecureString -String 'Password$fun' -AsPlainText -Force
$AATPService = ConvertTo-SecureString -String 'Password123!@#' -AsPlainText -Force

# Create new AD user SamiraA and add her to the domain admins group
New-ADUser -Name SamiraA -DisplayName "Samira Abbasi" -PasswordNeverExpires $true -AccountPassword $samiraASecurePass -Enabled $true
Add-ADGroupMember -Identity "Domain Admins" -Members SamiraA

# Create new AD user RonHD, create new Helpdesk SG, add RonHD to the Helpdesk SG
New-ADUser -Name RonHD -DisplayName "Ron Helpdesk" -PasswordNeverExpires $true -AccountPassword $ronHdSecurePass -Enabled $true
New-ADGroup -Name Helpdesk -GroupScope Global -GroupCategory Security
Add-ADGroupMember -Identity "Helpdesk" -Members "RonHD"

# Create new AD user JeffL
New-ADUser -Name JeffL -DisplayName "Jeff Leatherman" -PasswordNeverExpires $true -AccountPassword $jefflSecurePass -Enabled $true

# Take note of the "AATPService" user below which will be our service account for Azure ATP.
# Create new AD user Azure ATP Service

New-ADUser -Name AatpService -DisplayName "Azure ATP/ATA Service" -PasswordNeverExpires $true -AccountPassword $AATPService -Enabled $true

```

### <a name="configure-sam-r-capabilities-from-contosodc"></a>從 ContosoDC 設定 SAM-R 功能

為了允許 Azure ATP 服務正確地執行 SAM-R 列舉並建置「橫向移動」路徑，您將必須編輯 SAM 原則。

1. 尋找您的 SAM 原則： **原則 \> Windows 設定 \> 安全性設定 \> 本機原則 \> 安全性選項 \> [網路存取：限制允許對 SAM 進行遠端呼叫的用戶端]**_

    ![修改「群組原則」以允許 Azure ATP 使用「橫向移動」路徑功能。](media/playbook-labsetup-localgrouppolicies3.png)

1. 將 Azure ATP 服務帳戶 (AATPService) 新增至能夠在新式 Windows 系統上執行此動作的核准帳戶清單。

    ![新增服務](media/samr-add-service.png)

### <a name="add-sensitive-group-to-azure-atp"></a>將敏感性群組新增至 Azure ATP

將 "Helpdesk" 安全性群組新增為**敏感性群組**將可讓您使用 Azure ATP 的「橫向移動圖表」功能。 標記不一定是「網域系統管理員」但確實具有眾多資源權限的高敏感性使用者和群組，是最佳做法。

1. 在 Azure ATP 入口網站中，按一下功能表列的 [設定]**** 齒輪。

1. 在 [ **偵測** ] 下，按一下 [ **實體標記**]。

    ![Azure ATP 實體標記](media/entity-tags.png)

1. 在 [敏感性]**** 區段中，針對 [敏感性群組]**** 輸入名稱 "Helpdesk"，然後按一下 [+]**** 符號來新增它們。

    ![將 "Helpdesk" 標記為 Azure ATP 敏感性群組，來為此特殊權限群組啟用「橫向移動圖表」和報告功能](media/playbook-labsetup-helpdesksensitivegroup.png)

1. 按一下 [儲存]。

### <a name="azure-atp-lab-base-setup-checklist"></a>Azure ATP 實驗室基礎設定檢查清單

此時，您應該已有一個基礎的 Azure ATP 實驗室。 Azure ATP 應該已經可供使用，並且使用者也已預備妥當。 請檢閱檢查清單以確定基礎實驗室已完成。  

| 步驟    | 動作 | 狀態 |
|--------------|------------|------------------|
| 1  | 已在 ContosoDC 上安裝 Azure ATP 感應器 (先決條件步驟)| - [ ] |
| 2  | 已在 Active Directory 中建立使用者和群組  | - [ ] |
| 3  | 已針對 SAMR 正確設定 Azure ATP 服務帳戶權限 | - [ ] |
| 4  | 已在 Azure ATP 中將 Helpdesk 安全性群組新增為**敏感性群組**| - [ ] |

## <a name="set-up-the-lab-workstations"></a>設定實驗室工作站

確認基礎 Azure ATP 實驗室設定完成之後，您可以開始設定工作站，來為本系列接下來的三個教學課程做準備。 我們會將 VictimPC 和 AdminPC 序列化，以讓此實驗室顯示為作用中。

### <a name="victimpc-local-policies"></a>VictimPC 本機原則

您實驗室的下一個步驟是完成本機原則設定。 **VictimPC** 同時包含了 JeffL 和 Helpdesk 安全性群組作為本機 Administrators 群組的成員。 與在許多組織中一樣，JeffL 在其自己的裝置 (**VictimPC**) 上是系統管理員。

以本機系統管理員身分，執行自動化 PowerShell 指令碼來設定本機原則：

``` PowerShell
# Add JeffL to local Administrators group on VictimPC
Add-LocalGroupMember -Group "Administrators" -Member "Contoso\JeffL"
# Add Helpdesk to local Administrators group on VictimPC
Add-LocalGroupMember -Group "Administrators" -Member "Contoso\Helpdesk"
```

檢查 **VictimPC** 上的 Administrators 群組，確定它的成員至少包含 Helpdesk 和 JeffL：

![Helpdesk 和 JeffL 應該在 VictimPC 的「本機系統管理員群組」中](media/playbook-labsetup-localgrouppolicies2.png)

### <a name="simulate-helpdesk-support-on-victimpc"></a><a name="helpdesk-simulation"></a> 在 VictimPC 上模擬服務台支援

為了模擬可運作且受控的網路，請在 **VictimPC** 機器上建立一個「排定的工作」來以 **RonHD** 身分執行 "cmd.exe" 程序。

1. 從 VictimPC 上**已提高權限的 PowerShell 主控台**中執行下列程式碼：

    ``` PowerShell
    $action = New-ScheduledTaskAction -Execute 'cmd.exe'
    $trigger = New-ScheduledTaskTrigger -AtLogOn
    $runAs = 'Contoso\RonHD'
    $ronHHDPass = 'FightingTiger$'
    Register-ScheduledTask -TaskName "RonHD Cmd.exe - AATP SA Playbook" -Trigger $trigger -User $runAs -Password $ronHHDPass -Action $action
    ```

1. 以 **JeffL** 身分登入機器。 Cmd.exe 程序會於登入後在 RonHD 的內容中啟動，模擬管理機器的「服務台」。

### <a name="turn-off-antivirus-on-victimpc"></a>關閉 VictimPC 上的防毒軟體

基於測試目的，請關閉在實驗室環境中執行的所有防毒解決方案。 這麼做可確保我們能夠在這些練習期間將焦點放在 Azure ATP 上，而不是放在防毒迴避技術上。

如果不先關閉防毒解決方案，您將無法在下一節中下載某些工具。 此外，如果在預備攻擊工具之後啟用防毒軟體，您將必須在重新停用防毒軟體之後，重新下載這些工具。

### <a name="stage-common-hacker-tools"></a>預備常見的駭客工具

> [!WARNING]
> 下列顯示的工具僅供研究之用。 Microsoft 並**未**擁有這些工具，且 Microsoft 既無法保證也不保證或擔保其行為。 這些工具應該**僅限**在測試實驗室環境中執行。

若要執行 Azure ATP 安全性警示劇本，需要有下列工具。

| 工具 | URL |
|----|-----|
| Mimikatz | [GitHub - Mimikatz](https://github.com/gentilkiwi/mimikatz) |
| PowerSploit | [GitHub - PowerSploit](https://github.com/PowerShellMafia/PowerSploit) |
| PsExec | [Microsoft Docs](/sysinternals/downloads/psexec) |
| NetSess | [JoeWare 工具](https://www.joeware.net/freetools) |

我們感謝這些研究工具的作者，讓社群能夠更深入了解網路風險和影響。

### <a name="adminpc-local-policies"></a>AdminPC 本機原則

**AdminPC** 需要 **Helpdesk** 被新增至本機 Administrators 群組。 接著，請從本機 Administrators 群組中移除 'Domain Admins'。 此步驟可確保 Samira (一個網域系統管理員) 不是 AdminPC 的系統管理員。 這是認證檢疫的最佳做法。 請手動或使用所提供的 PowerShell 指令碼來執行此步驟。

1. 透過執行下列 PowerShell 指令碼，將 **Helpdesk** 新增至 **AdminPC**，並將 'Domain Admins' 從「本機系統管理員群組」中「移除」**：

    ``` PowerShell
   # Add Helpdesk to local Administrators group
   Add-LocalGroupMember -Group "Administrators" -Member "Contoso\Helpdesk"
   # Remove Domain Admins from local Administrators group
   Remove-LocalGroupMember -Group "Administrators" -Member "Domain Admins"

   ```

1. 執行此指令碼之後，**Helpdesk** 就會位於 **AdminPC** 的本機 [Administrators]**** > [成員]**** 清單中。
![AdminPC 之「本機系統管理員群組」中的 Helpdesk](media/playbook-labsetup-localgrouppolicies1.png)

### <a name="simulate-domain-activities-from-adminpc"></a>模擬來自 AdminPC 的網域活動

必須要有來自 SamiraA 的模擬網域活動。 您可以手動或使用所提供的 PowerShell 指令碼來執行此步驟。 此 PowerShell 指令碼會每 5 分鐘存取一次網域控制站，並且會以 Samira 身分產生模擬的網路活動。

以 **SamiraA** 身分，在 AdminPC 的 PowerShell 命令提示字元中執行下列指令碼：

```PowerShell

while ($true)
{
    Invoke-Expression "dir \\ContosoDC\c$"
    Start-Sleep -Seconds 300
}

```

### <a name="workstation-setup-checklist"></a>工作站設定檢查清單

請檢閱檢查清單以確定工作站設定已完成。

| 步驟    | 動作 | 狀態 |
|--------------|------------|------------------|
| 1  | 將 JeffL 和 Helpdesk 新增為 VictimPC 上的本機系統管理員 | - [ ] |
| 2  | 建立以 RonHD 身分在 VictimPC 上執行的「排定的工作」 | - [ ] |
| 3  | 關閉 VictimPC 上的防毒解決方案 | - [ ] |
| 4  | 在 VictimPC 上預備入侵工具| - [ ] |
| 5  | 在 AdminPC 的本機系統管理員群組中新增 Helpdesk 並移除 Domain Admins| - [ ] |
| 6  | 以 Samira 身分執行 PowerShell 指令碼來模擬網域活動 | - [ ] |

## <a name="mission-accomplished"></a>任務完成！

您的 Azure ATP 實驗室現在已可供使用。 此設定中使用的方法是在已知資源必須受到管理 (由「某個東西」** 或「某個人」**) 且管理需要本機系統管理員權限的情況下所選擇的。 還有其他可在實驗室中模擬管理工作流程的方法，例如：

- 使用 RonHD 的帳戶來登入和登出 VictimPC
- 新增另一個版本的「排定的工作」
- RDP 工作階段
- 在命令列列中執行 ‘runas’

 為了獲得最佳結果及基於一致性考量，請選擇可在您實驗室中自動執行的模擬方法。


## <a name="next-steps"></a>後續步驟

使用 Azure ATP 安全性警示劇本，從偵察階段開始，針對網路攻擊狙殺鏈的每個階段，測試您的 Azure ATP 實驗室環境。  

> [!div class="nextstepaction"]
> [Azure ATP 偵察劇本](playbook-reconnaissance.md)


## <a name="join-the-community"></a>加入社群

是否有更多問題，或是想與其他人討論 Azure ATP 及相關的安全性？ 現在就加入 [Azure ATP 社群](https://techcommunity.microsoft.com/t5/Azure-Advanced-Threat-Protection/bd-p/AzureAdvancedThreatProtection)！