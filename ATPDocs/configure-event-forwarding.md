---
title: 在適用於身分識別的 Microsoft Defender 中設定 Windows 事件轉送
description: 描述使用適用於身分識別的 Microsoft Defender 設定 Windows 事件轉送的選項
ms.date: 10/26/2020
ms.topic: how-to
ms.openlocfilehash: f3a11a3d39972b3bdb3df38669ef2fa4b10cc5fb
ms.sourcegitcommit: cdb7ae4580851e25aae24d07e7d66a750aa54405
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2020
ms.locfileid: "96543530"
---
# <a name="configuring-windows-event-forwarding"></a>設定 Windows 事件轉送

> [!NOTE]
> [!INCLUDE [Product long](includes/product-long.md)] 感應器會自動在本機讀取事件，而不需要設定事件轉送。

為增強偵測功能，[!INCLUDE [Product short](includes/product-short.md)] 需要列於[設定事件收集](configure-windows-event-collection.md#configure-event-collection)的 Windows 事件。 [!INCLUDE [Product short](includes/product-short.md)] 感應器可以自動讀取這些事件；如果沒有部署[!INCLUDE [Product short](includes/product-short.md)] 感應器，則有兩種方法可以將其轉送到[!INCLUDE [Product short](includes/product-short.md)] 獨立感應器：一種是將[!INCLUDE [Product short](includes/product-short.md)] 獨立感應器設定為接聽 SIEM 事件，另一種是設定 Windows 事件轉送。

> [!NOTE]
>
> - [!INCLUDE [Product short](includes/product-short.md)] 獨立感應器不支援可提供多種偵測的資料 Windows 事件追蹤 (ETW) 記錄項目。 若要完整涵蓋您的環境，建議您部署[!INCLUDE [Product short](includes/product-short.md)] 感應器。
> - 檢查網域控制站是否已正確設定來擷取必要事件。

## <a name="wef-configuration-for-product-short-standalone-sensors-with-port-mirroring"></a>適用於具有連接埠鏡像之[!INCLUDE [Product short](includes/product-short.md)] 獨立感應器的 WEF 設定

設定從網域控制站到[!INCLUDE [Product short](includes/product-short.md)] 獨立感應器之間的連接埠鏡像之後，請依照下列指示以使用來源起始設定來設定 Windows 事件轉送。 這是一個設定 Windows 事件轉送的方法。

**步驟 1：新增網路服務帳戶到網域 Event Log Readers 群組。**

在此案例中，假設[!INCLUDE [Product short](includes/product-short.md)] 獨立感應器是網域的成員。

1. 開啟 [Active Directory 使用者和電腦]，瀏覽至 **BuiltIn** 資料夾，然後按兩下 [Event Log Readers]。
1. 選取 [成員]。
1. 如果未列出 [Network Service]，請按一下 [新增]，在 [輸入要選取的物件名稱] 欄位中輸入 **Network Service**。 然後按一下 [檢查名稱]，再按兩次 [確定]。

在將 [網路服務] 新增到 [Event Log Readers] 群組後，請重新啟動網域控制站，變更才會生效。

**步驟 2：在網域控制站上建立原則以設定 [設定目標訂閱管理員] 設定。**

> [!Note]
> 您可以建立這些設定的群組原則，並將群組原則套用到[!INCLUDE [Product short](includes/product-short.md)] 獨立感應器監視的每個網域控制站。 下列步驟修改網域控制站的本機原則。

1. 在每個網域控制站上執行下列命令︰*winrm quickconfig*
1. 在命令提示字元中輸入 *gpedit.msc*
1. 展開 [電腦設定] > [系統管理範本] > [Windows 元件] > [事件轉送]

    ![本機原則群組編輯器影像](media/wef-1-local-group-policy-editor.png)

1. 按兩下 [設定目標訂閱管理員]。

    1. 選取 [啟用]。
    1. 在 [選項] 下，按一下 [顯示]。
    1. 在 [SubscriptionManagers] 下方，輸入下列值，然後按一下 [確定]：`Server=http\://\<fqdnMicrosoftDefenderForIdentitySensor>:5985/wsman/SubscriptionManager/WEC,Refresh=10` (例如：`Server=http\://atpsensor9.contoso.com:5985/wsman/SubscriptionManager/WEC,Refresh=10`)

    ![設定目標訂閱影像](media/wef-2-config-target-sub-manager.png)

1. 按一下 [確定]。
1. 在提升權限的命令提示字元中，輸入 *gpupdate /force*。

**步驟 3：在[!INCLUDE [Product short](includes/product-short.md)] 獨立感應器** 上執行下列步驟

1. 開啟提升權限的命令提示字元，輸入 *wecutil qc*
1. 開啟 [事件檢視器]。
1. 以滑鼠右鍵按一下 [訂閱]，然後選取 [建立訂閱]。

    1. 為訂閱輸入名稱和描述。
    1. 針對 [目的地記錄檔]，請確認已選取 [轉送的事件]。 若要讓[!INCLUDE [Product short](includes/product-short.md)] 讀取事件， 目的記錄檔必須是 [轉送的事件]。
    1. 選取 [來源電腦起始]，按一下 [選取電腦群組]。
        1. 按一下 [加入網域電腦]。
        1. 在 [輸入要選取的物件名稱] 欄位中輸入網域控制站的名稱。 然後按一下 [檢查名稱]，再按一下 [確定]。
        1. 按一下 [確定]。
        ![事件檢視器影像](media/wef-3-event-viewer.png)
    1. 按一下 [選取事件]。
        1. 按一下 [依記錄]，然後選取 [安全性]。
        1. 在 [Includes/Excludes Event ID (包含/排除事件識別碼)] 欄位中鍵入事件編號，然後按一下 [確定]。 例如，輸入 4776，如下列範例所示：<br/>
        ![查詢篩選影像](media/wef-4-query-filter.png)
    1. 以滑鼠右鍵按一下建立的訂閱，然後選取 [執行階段狀態]，以查看該狀態是否有任何問題。
    1. 幾分鐘後，請檢查您設定要轉送的事件是否出現在[!INCLUDE [Product short](includes/product-short.md)] 上的 [轉送的事件] 中。

如需詳細資訊，請參閱：[設定電腦以轉送和收集事件](/previous-versions/windows/it-pro/windows-server-2008-R2-and-2008/cc748890(v=ws.11)) \(英文\)

## <a name="see-also"></a>另請參閱

- [安裝[!INCLUDE [Product short](includes/product-short.md)]](install-step1.md)
- [查看[!INCLUDE [Product short](includes/product-short.md)] 論壇！](https://aka.ms/MDIcommunity)\(英文\)
