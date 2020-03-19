---
title: 設定您的 Proxy 或防火牆，以啟用與感應器的 Azure ATP 通訊
description: 描述如何設定防火牆或 Proxy，以允許 Azure ATP 雲端服務和 Azure ATP 感應器之間的通訊
keywords: ''
author: shsagir
ms.author: shsagir
manager: rkarlin
ms.date: 09/23/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: 9c173d28-a944-491a-92c1-9690eb06b151
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: a1e8065f5a1898301439c160c2a877cabe750928
ms.sourcegitcommit: 11fff9d4ebf1c50b04f7789a22c80cdbc3e4416a
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/15/2020
ms.locfileid: "79413820"
---
# <a name="configure-endpoint-proxy-and-internet-connectivity-settings-for-your-azure-atp-sensor"></a>設定 Azure ATP 感應器的端點 Proxy 和網際網路連線設定

每個 Azure 進階威脅防護 (ATP) 感應器都需要 Azure ATP 雲端服務的網際網路連線，才能成功運作。 在某些組織中，網域控制站不會直接連線到網際網路，而是透過 Web Proxy 連線來連線。 每個 Azure ATP 感應器都要求您使用 Microsoft Windows Internet (WinINET) Proxy 設定來回報感應器資料，並與 Azure ATP 服務進行通訊。 如果您使用 WinHTTP 進行 Proxy 設定，則仍需要為感應器和 ATP Azure 雲端服務之間的通訊設定 Windows Internet (WinINet) 瀏覽器 Proxy 設定。

設定 Proxy 時，請記住內嵌 Azure ATP 感應器服務是使用 **LocalService** 帳戶在系統內容中執行，而 Azure ATP 感應器更新程式服務則是使用 **LocalSystem** 帳戶在系統內容中執行。

> [!NOTE]
> 如果您在網路拓撲中使用 Transparent Proxy 或 WPAD，則不需要針對您的 Proxy 設定 WinINET。

## <a name="configure-the-proxy"></a>設定 Proxy

您可以使用[無訊息安裝，Proxy 驗證設定](https://docs.microsoft.com/azure-advanced-threat-protection/atp-silent-installation#proxy-authentication)，在感應器安裝期間設定您的 Proxy 設定。

### <a name="proxy-authentication"></a>Proxy 驗證

請使用下列命令來完成 Proxy 驗證：

**語法**：

> [!div class="mx-tableFixed"]
>
> |Name|語法|對無訊息安裝而言是否為必要？|說明|
> |-------------|----------|---------|---------|
> |ProxyUrl|ProxyUrl="https\://proxy.contoso.com:8080"|否|指定 Azure ATP 感應器的 ProxyUrl 和連接埠號碼。|
> |ProxyUserName|ProxyUserName="Contoso\ProxyUser"|否|如果您的 Proxy 服務需要驗證，請以 DOMAIN\user 格式提供使用者名稱。|
> |ProxyUserPassword|ProxyUserPassword="P@ssw0rd"|否|指定 Proxy 使用者名稱的密碼。 \* 認證會經過加密，並由 Azure ATP 感應器儲存在本機。|

您也可以使用以登錄為基礎的靜態 Proxy 手動設定您的 Proxy 伺服器，讓 Azure ATP 感應器在不允許電腦連線到網際網路時回報診斷資料，並與 Azure ATP 雲端服務進行通訊。

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

## <a name="enable-access-to-azure-atp-service-urls-in-the-proxy-server"></a>啟用 Proxy 伺服器中的 Azure ATP 服務 URL 存取

若要允許存取 Azure ATP，請允許下列 URL 的流量：

- \<your-instance-name>.atp.azure.com – 針對主控台連線能力。 例如 "Contoso-corp.atp.azure.com"

- \<your-instance-name>sensorapi.atp.azure.com – 針對感應器連線能力。 例如 "contoso-corpsensorapi.atp.azure.com"

上述 URL 會自動對應至 Azure ATP 執行個體的正確服務位置。 若您需要更細微的控制，可考慮允許下表相關端點的流量：

|服務位置|*.atp.azure.com DNS 記錄|
|----|----|
|美國 |triprd1wcusw1sensorapi.atp.azure.com<br>triprd1wcuswb1sensorapi.atp.azure.com<br>triprd1wcuse1sensorapi.atp.azure.com|
|歐洲|triprd1wceun1sensorapi.atp.azure.com<br>triprd1wceuw1sensorapi.atp.azure.com|
|亞洲|triprd1wcasse1sensorapi.atp.azure.com|

> [!NOTE]
>
> - 為確保最大的安全性與資料隱私權，Azure ATP 會在每個 Azure ATP 感應器與 Azure ATP 雲端後端之間使用以憑證為基礎的相互驗證。 如果您的環境中使用 SSL 檢查，請確定已針對相互驗證設定檢查，使其不會干擾驗證程序。
> - 您也可以使用 Azure 服務標籤 (**AzureAdvancedThreatProtection**) 來啟用對 Azure ATP 的存取權。 如需服務標籤的詳細資訊，請參閱[虛擬網路服務標籤](https://docs.microsoft.com/azure/virtual-network/service-tags-overview)或[下載服務標籤](https://www.microsoft.com/download/details.aspx?id=56519)檔案。

## <a name="see-also"></a>另請參閱

- [設定事件轉寄](configure-event-forwarding.md)
- [查看 Azure ATP 論壇！](https://aka.ms/azureatpcommunity)
