---
title: 瞭解 ATA 健康情況警示
description: 描述每個元件的所有健康情況警示，並列出原因和解決問題所需的步驟
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 02/20/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.prod: advanced-threat-analytics
ms.technology: ''
ms.assetid: b04fb8a4-b366-4b55-9d4c-6f054fa58a90
ms.reviewer: elofek
ms.suite: ems
ms.openlocfilehash: 456538f0b68f1eec0474f4579908a1dc2c42ee67
ms.sourcegitcommit: c7c0a4c9f7507f3e8e0f219798ed7d347c03e792
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/22/2020
ms.locfileid: "90912006"
---
# <a name="understanding-ata-health-alerts"></a>瞭解 ATA 健康情況警示

[!INCLUDE [Banner for top of topics](includes/banner.md)]

[!INCLUDE [Rebranding notice](includes/rebranding.md)]

ATA 健康狀態中心會發出健康情況警示，讓您知道 ATA 部署發生問題的時間。
此文章描述每個元件的所有健康情況警示，並列出原因與解決問題所需的步驟。
## <a name="ata-center-issues"></a>ATA 中心問題
### <a name="center-running-out-of-disk-space"></a>中心磁碟空間用盡
|警示|說明|解決方案|嚴重性|
|----|----|----|----|
|ATA 中心電腦磁碟機上用來儲存 ATA 資料庫的可用空間不足。|這表示硬碟的可用空間小於 200 GB 或不到 20% (以較小者為準)。 當 ATA 認為磁碟機空間不足時，就會開始從資料庫刪除舊資料。 如果舊資料因偵測引擎仍需要而無法刪除，您會收到此警示。 當您收到此警示時，ATA 會停止追蹤新活動。|增加磁碟機大小或釋出該磁碟機的空間。|高|
### <a name="failure-sending-mail"></a>傳送郵件失敗
|警示|說明|解決方案|嚴重性|
|----|----|----|----|
|ATA 無法將電子郵件通知傳送到指定的郵件伺服器。|不會從 ATA 傳送任何電子郵件訊息。|驗證 SMTP 伺服器設定。|低度|

### <a name="center-overloaded"></a>中心超載
|警示|說明|解決方案|嚴重性|
|----|----|----|----|
|ATA 中心無法處理從 ATA 閘道傳輸的資料量。 |ATA 中心停止分析新的網路流量和事件。 這表示在此健康情況警示為作用中時，偵測和設定檔的精確度會降低。|確定您為 ATA 中心提供足夠的資源。 如需如何適當地規劃 ATA 中心容量的詳細資訊，請參閱 [ATA 容量規劃](ata-capacity-planning.md)。 [使用效能計數器疑難排解 ATA](troubleshooting-ata-using-perf-counters.md) 來調查 ATA 中心的效能。|高|

### <a name="failure-connecting-to-the-siem-server-using-syslog"></a>無法連線到使用 Syslog 的 SIEM 伺服器
|警示|說明|解決方案|嚴重性|
|----|----|----|----|
|ATA 無法將事件傳送到指定的 SIEM。|這表示 ATA 中心無法傳送可疑的活動和健康情況警示給您的 SIEM。|確定您的 [Syslog 伺服器設定已正確設定](setting-syslog-email-server-settings.md)。|低度|
### <a name="center-certificate-is-about-to-expire"></a>中心憑證即將過期
|警示|說明|解決方案|嚴重性|
|----|----|----|----|
|ATA 中心憑證將會在不到 3 週內過期。|憑證過期後：從 ATA 閘道連線到 ATA 中心將會失敗。 ATA 中心處理序將會損毀，而且所有 ATA 功能將會停止。|[更換 ATA 中心憑證](modifying-ata-center-configuration.md)|中|
### <a name="ata-center-certificate-expired"></a>ATA 中心憑證已過期
|警示|說明|解決方案|嚴重性|
|----|----|----|----|
|ATA 中心憑證已過期。|憑證過期後：從 ATA 閘道連線到 ATA 中心會失敗。 ATA 中心處理序會損毀，而且所有 ATA 功能停止。|[重新部署 ATA 中心](install-ata-step1.md)|高|
## <a name="ata-gateway-issues"></a>ATA 閘道問題
### <a name="read-only-user-password-to-expire-shortly"></a>唯讀使用者密碼即將過期
|警示|說明|解決方案|嚴重性|
|----|----|----|----|
|用來對 Active Directory 執行實體解析的唯讀使用者密碼即將在不到 30 天內過期。|如果此使用者的密碼過期，所有 ATA 閘道停止執行，而且不會收集任何新資料。|[變更網域連線密碼](modifying-ata-config-dcpassword.md)，然後更新 ATA 主控台中的密碼。|中型|
### <a name="read-only-user-password-expired"></a>唯讀使用者密碼已過期
|警示|說明|解決方案|嚴重性|
|----|----|----|----|
|用來取得目錄資料的唯讀使用者密碼已過期。|所有 ATA 閘道停止執行 (或即將停止執行)，而且不會收集任何新資料。|[變更網域連線密碼](modifying-ata-config-dcpassword.md)，然後更新 ATA 主控台中的密碼。|高|
### <a name="gateway-certificate-about-to-expire"></a>閘道憑證即將過期
|警示|說明|解決方案|嚴重性|
|----|----|----|----|
|ATA 閘道憑證將會在不到 3 週內過期。|從特定 ATA 閘道連線到 ATA 中心會失敗。 不會從該 ATA 閘道傳送任何資料。|ATA 閘道憑證應該會自動更新。 閱讀 ATA 閘道和 ATA 中心記錄檔，以了解為何該憑證未自動更新。|中|

### <a name="gateway-certificate-expired"></a>閘道憑證已過期
|警示|說明|解決方案|嚴重性|
|----|----|----|----|
|ATA 閘道憑證已過期。|未從此 ATA 閘道連線到 ATA 中心。 不會從該 ATA 閘道傳送任何資料。|[解除安裝再重新安裝 ATA 閘道](install-ata-step3.md)。|高|
### <a name="domain-synchronizer-not-assigned"></a>未指派網域同步器
|警示|說明|解決方案|嚴重性|
|----|----|----|----|
|未將網域同步器指派給任何 ATA 閘道。 如果沒有設定為網域同步器候選的 ATA 閘道，就可能會發生此情況。|當網域未同步處理時，實體的變更可能會造成 ATA 中的實體資訊變成過期或遺失，但不影響任何偵測。|確定至少將一個 ATA 閘道設定為[網域同步器](install-ata-step5.md)。|低度|
### <a name="allsome-of-the-capture-network-adapters-on-a-gateway-are-not-available"></a>閘道上的所有/部分擷取網路介面卡無法使用
|警示|說明|解決方案|嚴重性|
|----|----|----|----|
|ATA 閘道上所有/部分選取的擷取網路介面卡已停用或中斷連線。|ATA 閘道不會再擷取部分/所有網域控制站的網路流量。 這會影響偵測與這些網域控制站相關之可疑活動的能力。|確定啟用並連線到 ATA 閘道上選取的擷取網路介面卡。|中|
### <a name="some-domain-controllers-are-unreachable-by-a-gateway"></a>閘道無法連線到部分網域控制站
|警示|說明|解決方案|嚴重性|
|----|----|----|----|
|由於設定之部分網域控制站的連線問題，ATA 閘道的功能有限。|當 ATA 閘道無法查詢部分網域控制站時，傳遞雜湊偵測可能較不正確。|確定網域控制站啟動並執行，而且此 ATA 閘道可以開啟其 LDAP 連線。|中|
### <a name="all-domain-controllers-are-unreachable-by-a-gateway"></a>閘道無法連線到任何網域控制站
|警示|說明|解決方案|嚴重性|
|----|----|----|----|
|由於設定之所有網域控制站的連線問題，ATA 閘道目前離線。|這會影響 ATA 偵測與此 ATA 閘道所監視的網域控制站相關之可疑活動的能力。| 確定網域控制站啟動並執行，而且此 ATA 閘道可以開啟其 LDAP 連線。|中|
### <a name="gateway-stopped-communicating"></a>閘道已停止通訊
|警示|說明|解決方案|嚴重性|
|----|----|----|----|
|沒有來自 ATA 閘道的通訊。 此警示的預設時間範圍為 5 分鐘。|ATA 閘道上的網路介面卡不會再擷取網路流量。 這會影響 ATA 偵測可疑活動的能力，因為網路流量無法到達 ATA 中心。|檢查用於 ATA 閘道與 ATA 中心服務間通訊的連接埠未遭到任何路由器或防火牆封鎖。|中|
### <a name="no-traffic-received-from-domain-controller"></a>未從網域控制站收到任何流量
|警示|說明|解決方案|嚴重性|
|----|----|----|----|
|未從網域控制站收到任何經由此 ATA 閘道的流量。|這可能表示從網域控制站到 ATA 閘道的連接埠鏡像尚未設定或無法運作。|確認[您網路裝置上的連接埠鏡像已正確設定](configure-port-mirroring.md)。<br></br>在 ATA 閘道擷取 NIC 上，停用 [進階設定] 中的這些功能：<br></br>接收區段聯合 (IPv4)<br></br>接收區段聯合 (IPv6)|中型|
### <a name="some-forwarded-events-are-not-being-analyzed"></a>某些轉送的事件不會被分析
|警示|說明|解決方案|嚴重性|
|----|----|----|----|
|ATA 閘道正在接收的事件超出其處理能力。|某些轉送的事件不會被分析，這可能會影響偵測來自此 ATA 閘道所監視的網域控制站之可疑活動的能力。|確認只將必要的事件轉送到 ATA 閘道，或嘗試將某些事件轉送到另一個 ATA 閘道。|中|
### <a name="some-network-traffic-is-not-being-analyzed"></a>某些網路流量不會被分析
|警示|說明|解決方案|嚴重性|
|----|----|----|----|
|ATA 閘道正在接收的網路流量超出其處理能力。|某些網路流量不會被分析，這可能會影響偵測來自此 ATA 閘道所監視的網域控制站之可疑活動的能力。|視需要考慮[新增額外的處理器和記憶體](ata-capacity-planning.md)。 如果這是獨立 ATA 閘道，請減少受監視的網域控制站數目。<br></br>如果在 VMware 虛擬機器上使用網域控制站，可能也會發生此情況。 若要避免這些警示，可檢查是否已將虛擬機器中的下列設定設為 [0] 或 [已停用]：<br></br>- TsoEnable<br></br>- LargeSendOffload(IPv4)<br></br>- IPv4 TSO Offload<br></br>此外也請考慮停用 [IPv4 Giant TSO Offload]。 如需詳細資訊，請參閱 VMware 文件。|中|

### <a name="gateway-version-outdated"></a>閘道版本已過期
|警示|說明|解決方案|嚴重性|
|----|----|----|----|
|ATA 中心比 ATA 閘道上安裝的版本還新。 這導致 ATA 閘道無法如預期般運作。|這可能會影響偵測來自此 ATA 閘道所監視的網域控制站之可疑活動的能力。|在 ATA 主控台中啟用[自動更新](install-ata-step1.md)，自動將 ATA 閘道更新為最新版本，或下載 ATA 主控台中可用的最新 ATA 閘道套件。|高|
### <a name="gateway-service-failed-to-start"></a>閘道服務無法啟動
|警示|說明|解決方案|嚴重性|
|----|----|----|----|
|ATA 閘道服務無法啟動至少 30 分鐘。|這可能會影響偵測來自此 ATA 閘道所監視的網域控制站之可疑活動的能力。|監視 ATA 閘道記錄檔，以[了解 ATA 閘道服務失敗的根本原因](troubleshooting-ata-using-logs.md)。|高|
## <a name="lightweight-gateway"></a>輕量型閘道
### <a name="lightweight--gateway-reached-a-memory-resource-limit"></a>輕量型閘道已達到記憶體資源限制
|警示|說明|解決方案|嚴重性|
|----|----|----|----|
|ATA 輕量型閘道已自行停止並將自動重新啟動，以在記憶體不足的情況下保護網域控制站。|ATA 輕量型閘道會對其本身強制執行記憶體限制，以防止網域控制站遇到資源限制。 當網域控制站上的記憶體使用量偏高時，就會發生此情況。 來自此網域控制站的資料只會受到部分監視。|增加網域控制站上的記憶體數量 (RAM)，或在此網站上新增更多網域控制站，以更佳分散此網域控制站的負載。|中型|


## <a name="see-also"></a>另請參閱
- [ATA 必要條件](ata-prerequisites.md)
- [ATA 容量規劃](ata-capacity-planning.md)
- [設定事件收集](configure-event-collection.md)
- [設定 Windows 事件轉送](configure-event-collection.md)
- [查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
