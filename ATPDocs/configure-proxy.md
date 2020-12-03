---
title: 設定您的 Proxy 或防火牆，以啟用適用於身分識別的 Microsoft Defender 與感應器的通訊 | Microsoft Docs
description: 描述如何設定您的防火牆或 Proxy，以允許適用於身分識別的 Microsoft Defender 雲端服務與適用於身分識別的 Microsoft Defender 感應器之間的通訊
ms.date: 10/26/2020
ms.topic: how-to
ms.openlocfilehash: 4606ab39457cbf1210974cb9f150d7410051c361
ms.sourcegitcommit: cdb7ae4580851e25aae24d07e7d66a750aa54405
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 12/03/2020
ms.locfileid: "96543428"
---
# <a name="configure-endpoint-proxy-and-internet-connectivity-settings-for-your-product-long-sensor"></a>為[!INCLUDE [Product long](includes/product-long.md)] 感應器設定端點 Proxy 與網際網路連線設定

每個[!INCLUDE [Product long](includes/product-long.md)] 感應器都需要連到 [!INCLUDE [Product short](includes/product-short.md)] 雲端服務的網際網路連線，才能報告感應器資料並成功運作。 在某些組織中，網域控制站不會直接連線到網際網路，而是透過 Web Proxy 連線來連線。

建議您使用命令列來設定 Proxy 伺服器，因為這麼做可確保只有[!INCLUDE [Product short](includes/product-short.md)] 感應器服務會透過 Proxy 進行通訊。

## <a name="configure-proxy-server-using-the-command-line"></a>使用命令列設定 Proxy 伺服器

您可以使用下列命令列參數，在感應器安裝期間設定 Proxy 伺服器。

### <a name="syntax"></a>語法

"Azure ATP sensor Setup.exe" [/quiet] [/Help] [ProxyUrl="http://proxy.internal.com"] [ProxyUserName="domain\proxyuser"] [ProxyUserPassword="ProxyPassword"]

### <a name="switch-descriptions"></a>參數描述

> [!div class="mx-tableFixed"]
>
> |Name|語法|對無訊息安裝而言是否為必要？|說明|
> |-------------|----------|---------|---------|
> |ProxyUrl|ProxyUrl="https\://proxy.contoso.com:8080"|否|為[!INCLUDE [Product short](includes/product-short.md)] 感應器指定 ProxyUrl 與連接埠號碼。|
> |ProxyUserName|ProxyUserName="Contoso\ProxyUser"|否|如果您的 Proxy 服務需要驗證，請以 DOMAIN\user 格式提供使用者名稱。|
> |ProxyUserPassword|ProxyUserPassword="P@ssw0rd"|否|指定 Proxy 使用者名稱的密碼。 \* 認證會經過加密，並由[!INCLUDE [Product short](includes/product-short.md)] 感應器儲存在本機。|

## <a name="alternative-methods-to-configure-your-proxy-server"></a>設定 Proxy 伺服器的替代方法

您可以使用下列其中一種替代方法來設定 Proxy 伺服器。 使用這些方法進行 Proxy 設定時，在內容中作為本機系統或本機服務執行的其他服務，也會透過 Proxy 引導流量。

- [使用 WinINet 設定 Proxy 伺服器](#configure-proxy-server-using-wininet)
- [使用登錄設定 Proxy 伺服器](#configure-proxy-server-using-the-registry)

### <a name="configure-proxy-server-using-wininet"></a>使用 WinINet 設定 Proxy 伺服器

您可以使用 Microsoft Windows Internet (WinINet) Proxy 組態來設定 Proxy 伺服器，讓[!INCLUDE [Product short](includes/product-short.md)] 感應器在不允許電腦連線到網際網路時回報診斷資料並與[!INCLUDE [Product short](includes/product-short.md)] 雲端服務進行通訊。 如果您使用 WinHTTP 進行 Proxy 設定，則仍需要為感應器與[!INCLUDE [Product short](includes/product-short.md)] 雲端服務之間的通訊設定 Windows Internet (WinINet) 瀏覽器 Proxy 設定。

設定 Proxy 時，請記住內嵌[!INCLUDE [Product short](includes/product-short.md)] 感應器服務是使用 **LocalService** 帳戶在系統內容中執行，而[!INCLUDE [Product short](includes/product-short.md)] 感應器更新程式服務則是使用 **LocalSystem** 帳戶在系統內容中執行。

> [!NOTE]
> 如果您在網路拓撲中使用 Transparent Proxy 或 WPAD，則不需要針對您的 Proxy 設定 WinINet。

### <a name="configure-proxy-server-using-the-registry"></a>使用登錄設定 Proxy 伺服器

您也可以使用以登錄為基礎的靜態 Proxy 手動設定您的 Proxy 伺服器，讓[!INCLUDE [Product short](includes/product-short.md)] 感應器在不允許電腦連線到網際網路時回報診斷資料並與 [!INCLUDE [Product short](includes/product-short.md)] 雲端服務進行通訊。

> [!NOTE]
> 登錄變更應僅套用至 LocalService 和 LocalSystem。

靜態 Proxy 可透過登錄進行設定。 您必須將您在使用者內容中使用的 Proxy 設定複製到 localsystem 和 localservice。 複製您的使用者內容 Proxy 設定：

1. 在修改登錄機碼之前，請務必先進行備份。

1. 在登錄中，在登錄機碼 `HKCU\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections\DefaultConnectionSettings` 下搜尋值為 `DefaultConnectionSettings` 的 REG_BINARY 並複製它。

1. 如果 LocalSystem 沒有正確的 Proxy 設定 (未設定或是與 Current_User 不同)，則您可能需要從 Current_User 將 Proxy 設定複製到 LocalSystem。 在登錄機碼 `HKU\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections\DefaultConnectionSettings` 下。

1. 將 Current_user `DefaultConnectionSettings` 中的值貼為 REG_BINARY。

1. 如果 LocalService 沒有正確的 Proxy 設定，則將 Current_User 中的 Proxy 設定複製到 LocalService。 在登錄機碼 `HKU\S-1-5-19\Software\Microsoft\Windows\CurrentVersion\Internet Settings\Connections\DefaultConnectionSettings` 下。

1. 將 Current_User `DefaultConnectionSettings` 中的值貼為 REG_BINARY。

> [!NOTE]
> 這將影響所有應用程式，包括使用 WinINET 搭配 LocalService、LocalSytem 內容的 Windows 服務。

<a name="enable-access-to-azure-atp-service-urls-in-the-proxy-server"></a>

## <a name="enable-access-to-product-short-service-urls-in-the-proxy-server"></a>在 Proxy 伺服器中啟用對[!INCLUDE [Product short](includes/product-short.md)] 服務 URL 的存取

若要允許存取[!INCLUDE [Product short](includes/product-short.md)]，建議您允許連到下列 URL 的流量。 這些 URL 會自動對應到[!INCLUDE [Product short](includes/product-short.md)] 執行個體的正確服務位置。

- `<your-instance-name>.atp.azure.com` - 針對主控台連線能力。 例如， `contoso-corp.atp.azure.com`

- `<your-instance-name>sensorapi.atp.azure.com`- 針對感應器連線能力。 例如， `contoso-corpsensorapi.atp.azure.com`

您也可以使用 Azure 服務標籤 (**AzureAdvancedThreatProtection**) 中的 IP 位址範圍來啟用對[!INCLUDE [Product short](includes/product-short.md)] 的存取。 如需服務標籤的詳細資訊，請參閱[虛擬網路服務標籤](/azure/virtual-network/service-tags-overview)或[下載服務標籤](https://www.microsoft.com/download/details.aspx?id=56519)檔案。

或者，若您需要更細微的控制，可考慮允許下表相關端點的流量：

|服務位置|*.atp.azure.com DNS 記錄|
|----|----|
|美國 |`triprd1wcusw2sensorapi.atp.azure.com`<br>`triprd1wcuswb3sensorapi.atp.azure.com`<br>`triprd1wcuse3sensorapi.atp.azure.com`|
|美國 GCC High|`https://triff1wcva2sensorapi.atp.azure.us`|
|歐洲|`triprd1wceun2sensorapi.atp.azure.com`<br>`triprd1wceuw3sensorapi.atp.azure.com`|
|Asia|`triprd1wcasse2sensorapi.atp.azure.com`|
|英國|`triprd1wcuks2sensorapi.atp.azure.com`|

> [!NOTE]
>
> - 為確保最大的安全性與資料隱私權，[!INCLUDE [Product short](includes/product-short.md)] 會在每個[!INCLUDE [Product short](includes/product-short.md)] 感應器與[!INCLUDE [Product short](includes/product-short.md)] 雲端後端之間使用以憑證為基礎的相互驗證。 如果您的環境中使用 SSL 檢查，請確定已針對相互驗證設定檢查，使其不會干擾驗證程序。
> - 有時候，[!INCLUDE [Product short](includes/product-short.md)] 服務 IP 位址可能會變更。 因此，如果您手動設定 IP 位址，或者 Proxy 自動將 DNS 名稱解析為其 IP 位址並加以使用，您應該定期檢查設定的 IP 位址是否仍為最新狀態。

## <a name="see-also"></a>另請參閱

- [設定事件轉寄](configure-event-forwarding.md)
- [查看[!INCLUDE [Product short](includes/product-short.md)] 論壇！](https://aka.ms/MDIcommunity)\(英文\)
