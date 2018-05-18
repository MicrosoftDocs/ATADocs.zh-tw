---
title: 設定您的 Proxy 或防火牆，以啟用與感應器的 Azure ATP 通訊 | Microsoft Docs
description: 描述如何設定防火牆或 Proxy，以允許 Azure ATP 雲端服務和 Azure ATP 感應器之間的通訊
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 5/16/2018
ms.topic: get-started-article
ms.prod: ''
ms.service: azure-advanced-threat-protection
ms.technology: ''
ms.assetid: 9c173d28-a944-491a-92c1-9690eb06b151
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 5a1fd5631a568419c600f35d44f09c9c61f17129
ms.sourcegitcommit: 714a01edc9006b38d1163d03852dafc2a5fddb5f
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/16/2018
---
適用於：Azure 進階威脅防護



# <a name="configure-endpoint-proxy-and-internet-connectivity-settings-for-your-azure-atp-sensor"></a>設定 Azure ATP 感應器的端點 Proxy 和網際網路連線設定

每個 Azure 進階威脅防護 (ATP) 感應器都需要 Azure ATP 雲端服務的網際網路連線，才能成功運作。 在某些組織中，網域控制站不會直接連線到網際網路，而是透過 Web Proxy 連線來連線。 每個 Azure ATP 感應器都要求您使用 Microsoft Windows Internet (WinINET) Proxy 設定來回報感應器資料，並與 Azure ATP 服務進行通訊。 如果您使用 WinHTTP 進行 Proxy 設定，則仍需要為感應器和 ATP Azure 雲端服務之間的通訊設定 Windows Internet (WinINet) 瀏覽器 Proxy 設定。


設定 Proxy 時，您需要知道內嵌 Azure ATP 感應器服務使用 **LocalService** 帳戶在系統內容中執行，而 Azure ATP Sensor Updater 服務使用 **LocalSystem** 帳戶在系統內容中執行。 

> [!NOTE]
> 如果您在網路拓撲中使用 Transparent Proxy 或 WPAD，則不需要針對您的 Proxy 設定 WinINET。

## <a name="configure-the-proxy"></a>設定 Proxy 

使用以登錄為基礎的靜態 Proxy 手動設定您的 Proxy 伺服器，讓 Azure ATP 感應器在不允許電腦連線到網際網路時回報診斷資料，並與 Azure ATP 雲端服務進行通訊。

> [!NOTE]
> 登錄變更應僅套用至 LocalService 和 LocalSystem。

靜態 Proxy 可透過登錄進行設定。 您必須將您在使用者內容中使用的 Proxy 設定複製到 localsystem 和 localservice。 複製您的使用者內容 Proxy 設定：

1.   在修改登錄機碼之前，請務必先進行備份。

2. 在登錄中，在登錄機碼 `HKCU\Software\Microsoft\Windows\CurrentVersion\InternetSetting\Connections\DefaultConnectionSetting` 下搜尋值為 `DefaultConnectionSetting` 的 REG_BINARY 並複製它。
 
2.  如果 LocalSystem 沒有正確的 Proxy 設定 (未設定或是與 Current_User 不同)，則您可能需要從 Current_User 將 Proxy 設定複製到 LocalSystem。 在登錄機碼 `HKU\S-1-5-18\Software\Microsoft\Windows\CurrentVersion\InternetSetting\Connections\DefaultConnectionSetting` 下。

3.  將 Current_user `DefaultConnectionSetting` 中的值貼為 REG_BINARY。

4.  如果 LocalService 沒有正確的 Proxy 設定，則將 Current_User 中的 Proxy 設定複製到 LocalService。 在登錄機碼 `HKU\S-1-5-19\Software\Microsoft\Windows\CurrentVersion\InternetSetting\Connections\DefaultConnectionSetting` 下。

5.  將 Current_User `DefaultConnectionSetting` 中的值貼為 REG_BINARY。

> [!NOTE]
> 這將影響所有應用程式，包括使用 WinINET 搭配 LocalService、LocalSytem 內容的 Windows 服務。


## <a name="enable-access-to-azure-atp-service-urls-in-the-proxy-server"></a>啟用 Proxy 伺服器中的 Azure ATP 服務 URL 存取

如果 Proxy 或防火牆根據預設封鎖了所有流量，並且只允許特定網域通過，或者啟用了 HTTPS 掃描 (SSL 檢查)，請確定下列 URL 已列入白名單，以允許與連接埠 443 中的 Azure ATP 服務進行通訊：

|服務位置|.Atp.Azure.com DNS 記錄|
|----|----|
|美國 |triprd1wcusw1sensorapi.atp.azure.com<br>triprd1wcuswb1sensorapi.atp.azure.com<br>triprd1wcuse1sensorapi.atp.azure.com|
|歐洲|triprd1wceun1sensorapi.atp.azure.com<br>triprd1wceuw1sensorapi.atp.azure.com|
|亞洲|triprd1wcasse1sensorapi.atp.azure.com|


您也可以自己建立的特定工作區強化防火牆與 Proxy 規則，方法是為下列 DNS 記錄建立規則：
- <Workspace-Name>.atp.azure.com - 針對主控台連線
- <Workspace-Name>sensorapi.atp.azure.com - 針對感應器連線
 
> [!NOTE]
> 針對 Azure ATP 網路流量 (感應器和 Azure ATP 服務之間) 執行 SSL 檢查時，SSL 檢查必須支援相互檢查。


## <a name="see-also"></a>另請參閱
- [設定事件轉寄](configure-event-forwarding.md)
- [查看 ATP 論壇！](https://aka.ms/azureatpcommunity)\(英文\)