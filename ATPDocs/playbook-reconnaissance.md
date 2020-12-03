---
title: 適用於身分識別的 Microsoft Defender 偵察劇本教學課程
description: 適用於身分識別的 Microsoft Defender 偵察劇本教學課程描述如何模擬適用於身分識別的 Defender 所偵測到的偵察移動威脅。
ms.date: 10/26/2020
ms.topic: tutorial
ms.openlocfilehash: dcaac8ed69bb4c3b9ccd262af929652dbc12126a
ms.sourcegitcommit: cdb7ae4580851e25aae24d07e7d66a750aa54405
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2020
ms.locfileid: "96544482"
---
# <a name="tutorial-reconnaissance-playbook"></a>教學課程：偵察劇本

這個[!INCLUDE [Product long](includes/product-long.md)] 安全性警示四部分系列中的第二個教學課程是一個偵察劇本。 [!INCLUDE [Product short](includes/product-short.md)] 安全性警示實驗室的目的是要說明 **[!INCLUDE [Product short](includes/product-short.md)]** 對網路可疑活動與潛在攻擊的識別及偵測功能。 此劇本說明如何針對[!INCLUDE [Product short](includes/product-short.md)] 的一些「離散」偵測進行測試，並將焦點放在[!INCLUDE [Product short](includes/product-short.md)] 的「特徵」型功能上。 此劇本並不包括以進階機器學習為基礎的警示或偵測，或是使用者/實體型的行為偵測，因為它們需要一個最多有 30 天真實網路流量的學習期間。 如需有關此系列每個教學課程的詳細資訊，請參閱[[!INCLUDE [Product short](includes/product-short.md)] 安全性警示實驗室概觀](playbook-lab-overview.md)。

此劇本會說明針對來自常見、真實世界、可公開取得之入侵和攻擊工具的模擬威脅，[!INCLUDE [Product short](includes/product-short.md)] 可提供的威脅偵測與安全性警示服務。

在此教學課程中，您將：

> [!div class="checklist"]
>
> - 模擬網路對應偵察
> - 模擬目錄服務偵察
> - 模擬使用者和 IP 位址 (SMB) 偵察
> - 在[!INCLUDE [Product short](includes/product-short.md)] 中檢閱來自模擬偵察的安全性警示

## <a name="prerequisites"></a>先決條件

[已完成的[!INCLUDE [Product short](includes/product-short.md)] 安全性警示實驗室](playbook-setup-lab.md)

- 建議您儘可能完全依照實驗室設定指示進行操作。 您的實驗室與建議的實驗室設定越相似，就越容易依照[!INCLUDE [Product short](includes/product-short.md)] 測試程序進行操作。

## <a name="simulate-a-reconnaissance-attack"></a>模擬偵察攻擊

一旦攻擊者出現在您的環境中，他們的偵察活動便會開始。 在此階段，攻擊者通常會花時間進行研究。 他們會嘗試探索感興趣的電腦、列舉使用者和群組、收集重要的 IP，並對應您組織的資產和弱點。 偵察活動可讓攻擊者取得對您環境的徹底了解和完整對應，以供稍後使用。

偵察攻擊測試方法：

- 網路對應偵察
- 目錄服務偵察
- 使用者和 IP 位址 (SMB) 偵察

## <a name="network-mapping-reconnaissance-dns"></a>網路對應偵察 (DNS)

攻擊者會優先嘗試的動作之一，就是嘗試取得所有 DNS 資訊的複本。 當成功時，攻擊者會取得有關您環境的大量資訊，其中可能包括有關您其他環境或網路的類似資訊。

[!INCLUDE [Product short](includes/product-short.md)] 會抑制來自您 **可疑活動時間表** 的網路對應偵察活動，直到完成八天的學習期間。 在學習期間，[!INCLUDE [Product short](includes/product-short.md)] 會學習對您的網路來說，何謂正常及何謂異常。 在八天的學習期間過後，異常網路對應偵察事件會叫用相關安全性警示。

### <a name="run-nslookup-from-victimpc"></a>從 VictimPC 執行 nslookup

為了測試 DNS 偵察，我們將使用原生命令列工具 *nslookup* 來起始 DNS 區域傳輸。 具有正確設定的 DNS 伺服器會拒絕這類查詢，而不會允許嘗試區域傳輸。

使用已遭盜用的 JeffL 認證來登入 **VictimPC**。 執行下列命令：

```dos
nslookup
```

輸入 **server**，然後輸入已安裝[!INCLUDE [Product short](includes/product-short.md)] 感應器之 DC 的 FQDN 或 IP 位址。

```nslookup
server contosodc.contoso.azure
```

讓我們嘗試傳輸網域。

```nslookup
ls -d contoso.azure
```

- 將 contosodc.contoso.azure 與 contoso.azure 分別取代成您[!INCLUDE [Product short](includes/product-short.md)] 感應器的 FQDN 與網域。

 ![nslookup 命令嘗試複製 DNS 伺服器 - 失敗](media/playbook-recon-nslookup.png)

如果 **ContsoDC** 是第一個部署的感應器，請等候 15 分鐘，以允許資料庫後端完成必要微服務的部署。

### <a name="network-mapping-reconnaissance-dns-detected-in-product-short"></a>[!INCLUDE [Product short](includes/product-short.md)] 中偵測到的網路對應偵察 (DNS)

能夠檢視這類嘗試 (失敗或成功) 對網域威脅防護來說至關重要。 在最近安裝環境之後，您將必須移至 [邏輯活動]  時間表以查看偵測到的活動。

在[!INCLUDE [Product short](includes/product-short.md)] 的 [搜尋] 中，輸入 **VictimPC**，然後在其上按一下來檢視時間表。

![由[!INCLUDE [Product short](includes/product-short.md)] 偵測到的 DNS 偵察，概略檢視](media/playbook-recon-nslookupdetection1.png)

尋找 [AXFR 查詢] 活動。 [!INCLUDE [Product short](includes/product-short.md)] 會偵測對您 DNS 進行的這類偵察活動。

- 如果您有大量活動，請按一下 [篩選依據]  ，然後取消選取 [DNS 查詢]  以外的所有類型。

![[!INCLUDE [Product short](includes/product-short.md)] 中 DNS 偵察偵測的詳細檢視](media/playbook-recon-nslookupdetection2.png)

如果您的安全性分析師判斷此活動源自安全性掃描程式，則可以將特定裝置從進一步的偵測警示中排除。 在警示的右上方區域中，按一下三個點。 接著，選取 [Close and exclude MySecurityScanner] \(關閉並排除 MySecurityScanner\)  。 確保從 "MySecurityScanner" 偵測到時，不會再顯示此警示。

偵測失敗與偵測對環境進行的成功攻擊一樣可提供深入解析。 [!INCLUDE [Product short](includes/product-short.md)] 入口網站可讓我們查看可能的攻擊者所執行動作的確切結果。 在我們的模擬 DNS 偵察攻擊案例中，我們扮演的攻擊者角色被阻止傾印網域的 DNS 記錄。 您的 SecOps 小組從[!INCLUDE [Product short](includes/product-short.md)] 安全性警示中開始察覺了我們的攻擊嘗試，以及我們在嘗試中所使用的機器。

## <a name="directory-service-reconnaissance"></a>目錄服務偵察

作為一個攻擊者，下一個偵察目標就是嘗試列舉「樹系」中的所有使用者和群組。 [!INCLUDE [Product short](includes/product-short.md)] 會抑制「目錄服務」列舉活動出現在您的「可疑活動」時間表中，直到 30 天學習期間完成為止。 在學習期間，[!INCLUDE [Product short](includes/product-short.md)] 會學習對您的網路來說，何謂正常及何謂異常。 在 30 天學習期間之後，異常的「目錄服務」列舉事件會叫用安全性警示。 在 30 天的學習期間，您可以使用您網路中實體的活動時間表，來查看[!INCLUDE [Product short](includes/product-short.md)] 對這些活動的偵測。 此實驗室會顯示[!INCLUDE [Product short](includes/product-short.md)] 對這些活動的偵測。

為了示範常見的「目錄服務」偵察方法，我們將使用原生 Microsoft 二進位檔 *net*。 在我們的嘗試之後，檢查 JeffL (我們的遭盜用使用者) 的「活動」時間表將會顯示[!INCLUDE [Product short](includes/product-short.md)] 正在偵測此活動。

### <a name="directory-service-enumeration-via-net-from-victimpc"></a>從 VictimPC 透過 *net* 進行目錄服務列舉

任何已驗證的使用者或電腦都可能列舉網域中的其他使用者和群組。 大多數應用程式都必須要有此列舉能力才能正確運作。 我們的遭盜用使用者 JeffL 是一個無特殊權限的網域帳戶。 在這個模擬攻擊中，我們將確切了解即使是一個無特殊權限的網域帳戶，如何也仍然能夠提供寶貴的資料點給攻擊者。

1. 從 **VictimPC**，執行下列命令：

    ```dos
    net user /domain
    ```

    輸出會顯示 Contoso.Azure 網域中的所有使用者。

    ![列舉網域中的所有使用者](media/playbook-recon-dsenumeration-netusers.png)

1. 讓我們嘗試列舉網域中的所有群組。 請執行下列命令：

    ```dos
    net group /domain
    ```

    輸出會顯示 Contoso.Azure 網域中的所有群組。 請注意一個不是預設群組的「安全性群組」：**Helpdesk**。

    ![列舉網域中的所有群組](media/playbook-recon-dsenumeration-netgroups.png)

1. 現在，讓我們嘗試只列舉 Domain Admins 群組。 執行下列命令：

    ```dos
    net group "Domain Admins" /domain
    ```

    ![列舉 Domain Admins 群組的所有成員](media/playbook-recon-dsenumeration-netdomainadmins.png)

    作為一個攻擊者，我們已了解 Domain Admins 群組有兩個成員：**SamiraA** 和 **ContosoAdmin** (「網域控制站」的內建「系統管理員」)。 在知道我們的「網域」與「樹系」之間沒有任何安全性界限的情況下，我們的下一個躍進就是嘗試列舉 Enterprise Admins。

1. 若要嘗試列舉 Enterprise Admins，請執行下列命令：

    ```dos
    net group "Enterprise Admins" /domain
    ```

    我們已了解只有一個「企業系統管理員」，即 ContosoAdmin。 此資訊並不重要，因為我們已經知道我們的「網域」與「樹系」之間沒有安全性界限。

    ![網域中列舉的 Enterprise Admins](media/playbook-recon-dsenumeration-netenterpriseadmins.png)

有了我們偵察中所收集的資訊，我們現在知道了「Helpdesk 安全性群組」。 雖然該資訊 *尚未* 引起關注。 我們也知道了 **SamiraA** 是 Domain Admins 群組的成員。 如果我們可以搜集 SamiraA 的認證，我們就可以存取「網域控制站」本身。

### <a name="directory-service-enumeration-detected-in-product-short"></a>[!INCLUDE [Product short](includes/product-short.md)] 中偵測到的目錄服務列舉

如果我們的實驗室「在已安裝[!INCLUDE [Product short](includes/product-short.md)] 的情況下有 30 天真實的即時活動」，則我們剛才以 JeffL 身分執行的活動將可能被歸類為異常活動。 異常活動會顯示在「可疑的活動」時間軸中。 不過，由於我們剛安裝好環境，因此將必須前往「邏輯活動」時間軸來查看活動。

在[!INCLUDE [Product short](includes/product-short.md)] 的 [搜尋] 中，讓我們看看 JeffL 的「邏輯活動」時間表看起來像怎樣：

![搜尋特定實體的邏輯活動時間軸](media/playbook-recon-dsenumeration-searchlogicalactivity.png)

我們可以看到 JeffL 使用 Kerberos 通訊協定登入 VictimPC 的時間。 此外，我們還看到 JeffL 從 VictimPC 列舉網域中的所有使用者。

![JeffL 的邏輯活動時間軸](media/playbook-recon-dsenumeration-jeffvlogicalactivity.png)

許多活動都記錄在「邏輯活動」時間軸中，使得它成為可執行「數位鑑識調查與數位回應」(DFIR) 的主要功能。 甚至當初始偵測不是來自[!INCLUDE [Product short](includes/product-short.md)]，但卻是來自適用於端點的 Microsoft Defender 或 Microsoft 365 等時，您也可以看到活動。

藉由查看 **ContosoDC 的頁面**，我們還可以看到 JeffL 所登入的電腦。

![JeffL 所登入的電腦](media/playbook-recon-dsenumeration-jeffvloggedin.png)

我們也可以取得「目錄資料」，包括 JeffL 的「成員資格」與「存取控制」，全都可從[!INCLUDE [Product short](includes/product-short.md)] 內取得。

![[!INCLUDE [Product short](includes/product-short.md)] 中 JeffL 的目錄資料](media/playbook-recon-dsenumeration-jeffvdirectorydata.png)

現在，我們的注意力將切換到「SMB 工作階段列舉」。

## <a name="user-and-ip-address-reconnaissance-smb"></a>使用者和 IP 位址偵察 (SMB)

Active Directory 的 [sysvol] 資料夾如果不是環境中 *最* 重要的網路共用，也是其中之一。 每個電腦和使用者都必須能夠存取此特定網路共用，才能提取「群組原則」。 攻擊者可以從列舉與 [sysvol] 資料夾具有作用中工作階段的使用者取得資訊寶庫。

我們的下一步是對 ContosoDC 資源進行「SMB 工作階段列舉」。 我們想要了解有哪些其他人與 SMB 共用具有工作階段，以及是「來自哪個 IP」  。

### <a name="use-joewares-netsessexe-from-victimpc"></a>從 VictimPC 使用 JoeWare 的 NetSess.exe

在已驗證的使用者 (在此案例中為 ContosoDC) 內容中，針對 ContosoDC 執行 JoeWare 的 **NetSess** 工具：

```dos
NetSess.exe ContosoDC
```

![攻擊者使用 SMB 偵察來識別使用者及其 IP 位址](media/playbook-recon-smbrecon.png)

我們已經知道 SamiraA 是一個「網域系統管理員」。這個攻擊為我們提供了 SamiraA 的 IP 位址 10.0.24.6。 身為攻擊者，我們已確切了解要盜用的對象是誰。 我們也取得了登入該認證的網路位置。

### <a name="user-and-ip-address-reconnaissance-smb-detected-in-product-short"></a>[!INCLUDE [Product short](includes/product-short.md)] 中偵測到的使用者與 IP 位址偵察 (SMB)

現在，我們可以看看[!INCLUDE [Product short](includes/product-short.md)] 為我們偵測到哪些東西：

![[!INCLUDE [Product short](includes/product-short.md)] 正在偵測 SMB 偵察](media/playbook-recon-smbrecon-detection1.png)

我們不僅接獲此活動的警示，也接獲「在該時間點」  已暴露之帳戶及其個別 IP 位址的警示。 作為「安全性作業中心」(SOC)，我們不僅掌握該嘗試及其狀態，也掌握了傳回給攻擊者的資訊。 此資訊可輔助我們的調查。

## <a name="next-steps"></a>後續步驟

攻擊狙殺鏈中的下一個階段通常是橫向移動嘗試。

> [!div class="nextstepaction"]
> [[!INCLUDE [Product short](includes/product-short.md)] 橫向移動劇本](playbook-lateral-movement.md)

## <a name="join-the-community"></a>加入社群

有更多問題或想與其他人討論[!INCLUDE [Product short](includes/product-short.md)] 與相關的安全性？ 立即加入[[!INCLUDE [Product short](includes/product-short.md)] 社群](https://techcommunity.microsoft.com/t5/Azure-Advanced-Threat-Protection/bd-p/AzureAdvancedThreatProtection) \(英文\)！
