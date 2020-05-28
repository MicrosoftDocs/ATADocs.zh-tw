---
title: 了解 Azure ATP Azure 健康情況警示
description: 描述如何使用 Azure ATP 記錄檔對問題進行疑難排解
keywords: ''
author: shsagir
ms.author: shsagir
manager: rkarlin
ms.date: 05/17/2020
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: d0551e91-3b21-47d5-ad9d-3362df6d47c0
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: b756b62a96a4d72fc00a405c174c734aed3861fa
ms.sourcegitcommit: 536d7595270732b99096e4044dd7b10085940ea0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/17/2020
ms.locfileid: "83443510"
---
# <a name="understanding-azure-atp-sensor-health-alerts"></a>了解 Azure ATP 感應器健康情況警示

當您的 Azure ATP 執行個體發生問題時，Azure ATP 健康情況中心會透過發出健康情況警示來讓您知道。 此文章描述每個元件的所有健康情況警示，並列出原因與解決問題所需的步驟。

## <a name="all-domain-controllers-are-unreachable-by-a-sensor"></a>感應器無法連線到所有網域控制站

|警示|說明|解決方案|嚴重性|
|----|----|----|----|
|由於所有已設定之網域控制站的連線問題，Azure ATP 感應器目前離線。|這會影響 Azure ATP 偵測由此 Azure ATP 感應器所監視之網域控制站相關可疑活動的能力。| 請確定網域控制站已啟動且正在執行，而且此 Azure ATP 感應器可以針對對它們開啟 LDAP 連線。 此外，請務必在 [設定] 中針對每個部署的樹系設定目錄服務帳戶。|中型|

## <a name="allsome-of-the-capture-network-adapters-on-a-sensor-are-not-available"></a>感應器上的所有/部分擷取網路介面卡無法使用

|警示|說明|解決方案|嚴重性|
|----|----|----|----|
|Azure ATP 感應器上所有/部分的擷取網路介面卡已停用或中斷連線。|Azure ATP 感應器不會再擷取部分/所有網域控制站的網路流量。 這會影響偵測與這些網域控制站相關之可疑活動的能力。|請確定 Azure ATP 感應器上這些選取的擷取網路介面卡已啟用並連線。|中型|

## <a name="directory-services-user-credentials-are-incorrect"></a>目錄服務使用者認證不正確

|警示|說明|解決方案|嚴重性|
|----|----|----|----|
|目錄服務使用者帳戶的認證不正確。|這會影響感應器使用 LDAP 查詢對網域控制站偵測活動的能力。|- 針對**標準** AD 帳戶：確認 [目錄服務] 設定頁面中的使用者名稱、密碼與網域是正確的。<br>- 針對**群組受管理的服務帳戶**：確認 [目錄服務] 設定頁面中的使用者名稱與網域是正確的。 此外，請檢查[連線到您的 Active Directory 樹系](install-atp-step2.md#prerequisites)頁面上所述的所有其他 **gMSA 帳戶**先決條件。|中型|

## <a name="low-success-rate-of-active-name-resolution"></a>低成功率的主動名稱解析

|警示|說明|解決方案|嚴重性|
|----|----|----|----|
|列出的 Azure ATP 感應器在使用下列方法時有超過 90% 的時間無法將 IP 位址解析為裝置名稱：<br />- 透過 RPC 的 NTLM<br />- NetBios<br />- 反向 DNS|這會影響 Azure ATP 的偵測功能，而且可能會增加誤判為真的警示數量。|- 針對透過 RPC 的 NTLM：檢查是否已在環境中的所有電腦上針對來自 Azure ATP 感應器的連入通訊開放連接埠 135。<br />- 針對反向 DNS：檢查感應器是否可以連線到 DNS 伺服器，以及是否已啟用反向對應區域。<br />- 針對 NetBIOS：檢查是否已在環境中的所有電腦上針對來自 Azure ATP 感應器的連入通訊開放連接埠 137。<br />此外，請確定網路設定 (例如防火牆) 並未阻止與相關連接埠的通訊。|低|

## <a name="no-traffic-received-from-domain-controller"></a>未從網域控制站收到任何流量

|警示|說明|解決方案|嚴重性|
|----|----|----|----|
|未從網域控制站收到任何經由此 Azure ATP 感應器的流量。|這可能表示從網域控制站到 Azure ATP 感應器的連接埠鏡像尚未設定或無法運作。|確認[您網路裝置上的連接埠鏡像已正確設定](configure-port-mirroring.md)。<br></br>在 Azure ATP 感應器擷取 NIC 上，停用 [進階設定] 中的這些功能：<br></br>接收區段聯合 (IPv4)<br></br>接收區段聯合 (IPv6)|中型|

## <a name="read-only-user-password-to-expire-shortly"></a>唯讀使用者密碼即將過期

|警示|說明|解決方案|嚴重性|
|----|----|----|----|
|用來對 Active Directory 執行實體解析的唯讀使用者密碼即將在不到 30 天內過期。|如果此使用者的密碼過期，所有 Azure ATP 感應器將停止執行，且不會收集任何新資料。|[變更網域連線密碼](modifying-atp-config-dcpassword.md)，然後在 Azure ATP 入口網站中更新密碼。|中型|

## <a name="read-only-user-password-expired"></a>唯讀使用者密碼已過期

|警示|說明|解決方案|嚴重性|
|----|----|----|----|
|用來取得目錄資料的唯讀使用者密碼已過期。|所有 Azure ATP 感應器都會停止執行 (或即將停止執行)，而且不會收集任何新資料。|[變更網域連線密碼](modifying-atp-config-dcpassword.md)，然後在 Azure ATP 入口網站中更新密碼。|高|

## <a name="sensor-outdated"></a>感應器過期

|警示|說明|解決方案|嚴重性|
|----|----|----|----|
|Azure ATP 感應器已過期。|Azure ATP 感應器正在執行無法與 Azure ATP 雲端基礎結構通訊的版本。|手動更新並檢查感應器，以查看感應器無法自動更新的原因。 如果仍然失敗，請下載最新的感應器安裝套件，然後解除安裝感應器再重新安裝。 如需詳細資訊，請參閱[安裝 Azure ATP 感應器](install-atp-step4.md)。|中型|

## <a name="sensor-reached-a-memory-resource-limit"></a>感應器已達到記憶體資源限制

|警示|說明|解決方案|嚴重性|
|----|----|----|----|
|Azure ATP 感應器將自己停止並自動重新啟動，以防止網域控制站發生低記憶體的狀況。|Azure ATP 感應器對自己強制執行記憶體限制，以防止網域控制站遇到資源限制。 當網域控制站上的記憶體使用量偏高時，就會發生此情況。 來自此網域控制站的資料只會受到部分監視。|增加網域控制站上的記憶體數量 (RAM)，或在此網站上新增更多網域控制站，以更佳分散此網域控制站的負載。|中型|

## <a name="sensor-service-failed-to-start"></a>感應器服務無法啟動

|警示|說明|解決方案|嚴重性|
|----|----|----|----|
|Azure ATP 感應器服務至少 30 分鐘無法啟動。|這可能會影響偵測來自由此 Azure ATP 感應器所監視之網域控制站可疑活動的能力。|監視 Azure ATP 感應器記錄檔，以了解 Azure ATP 感應器服務失敗的根本原因。|高|

## <a name="sensor-stopped-communicating"></a>感應器已停止通訊

|警示|說明|解決方案|嚴重性|
|----|----|----|----|
|沒有來自 Azure ATP 感應器的通訊。 此警示的預設時間範圍為 5 分鐘。|Azure ATP 感應器上的網路介面卡已不再擷取網路流量。 由於網路流量無法到達 Azure ATP 雲端服務，因此這會影響 ATA 偵測可疑活動的能力。|請檢查 Azure ATP 感應器和 Azure ATP 雲端服務之間用來通訊的連接埠沒有被任何路由器或防火牆封鎖。|中型|

## <a name="some-domain-controllers-are-unreachable-by-a-sensor"></a>感應器無法連線到部分網域控制站

|警示|說明|解決方案|嚴重性|
|----|----|----|----|
|由於部分已設定之網域控制站的連線問題，Azure ATP 感應器的功能受到限制。|當 Azure ATP 感應器無法查詢部分網域控制站時，傳遞雜湊偵測可能較不正確。|請確定網域控制站已啟動且正在執行，而且此 Azure ATP 感應器可以針對對它們開啟 LDAP 連線。|中型|

## <a name="some-forwarded-events-could-not-be-analyzed"></a>無法分析某些轉送的事件

|警示|說明|解決方案|嚴重性|
|----|----|----|----|
|Azure ATP 感應器所接收到的事件比它能處理的還要多。|無法分析某些轉送的事件，這可能會影響偵測可疑活動的能力，這些活動源自於此 Azure ATP 感應器所監視的網域控制站上。|請確認只有必要的事件會被轉寄到 Azure ATP 感應器，或嘗試將某些事件轉寄到其他 Azure ATP 感應器。|中型|

## <a name="some-network-traffic-could-not-be-analyzed"></a>無法分析某些網路流量

|警示|說明|解決方案|嚴重性|
|----|----|----|----|
|Azure ATP 感應器所接收到的網路流量比它能處理的還要多。|無法分析某些網路流量，這可能會影響偵測可疑活動的能力，這些活動源自於此 Azure ATP 感應器所監視的網域控制站上。|視需要考慮[新增額外的處理器和記憶體](atp-capacity-planning.md)。 如果這是獨立 Azure ATP 感應器，請減少被監視的網域控制站數目。<br></br>如果在 VMware 虛擬機器上使用網域控制站，可能也會發生此情況。 若要避免這些警示，可檢查是否已將虛擬機器中的下列設定設為 [0] 或 [已停用]：<br></br>- TsoEnable<br></br>- LargeSendOffload(IPv4)<br></br>- IPv4 TSO Offload<br></br>此外也請考慮停用 [IPv4 Giant TSO Offload]。 如需詳細資訊，請參閱 VMware 文件。|中型|

## <a name="some-windows-events-could-not-be-analyzed"></a>無法分析某些 Windows 事件

|警示|說明|解決方案|嚴重性|
|----|----|----|----|
|Azure ATP 感應器目前接收到的 Windows 事件追蹤 (ETW) 事件已超過其能處理的量。|無法分析某些 Windows 事件追蹤 (ETW) 事件，這可能會影響偵測可疑活動的能力，這些活動源自於此 Azure ATP 感應器所監視的網域控制站上。|請確認只有必要的事件會被轉寄到 Azure ATP 感應器，或嘗試將某些事件轉寄到其他 Azure ATP 感應器。|中型|

## <a name="windows-events-missing-from-domain-controller-audit-policy"></a>網域控制站稽核原則中缺少 Windows 事件

|警示|說明|解決方案|嚴重性|
|----|----|----|----|
| 網域控制站稽核原則中缺少 Windows 事件|若要正確稽核事件並將其包含在 Windows 事件記錄檔中，則網域控制站需要正確的進階稽核原則設定。 不正確的進階稽核原則設定會讓記錄檔遺漏重要事件，並導致 Azure ATP 涵蓋範圍不完整。|檢閱您的[進階稽核原則](atp-advanced-audit-policy.md)，並視需要修改。 | 中型|

## <a name="see-also"></a>另請參閱

- [Azure ATP 必要條件](atp-prerequisites.md)
- [Azure ATP 容量規劃](atp-capacity-planning.md)
- [設定事件收集](configure-event-collection.md)
- [設定 Windows 事件轉送](configure-event-forwarding.md)
- [查看 Azure ATP 論壇！](https://aka.ms/azureatpcommunity)
