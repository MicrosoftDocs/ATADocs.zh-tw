---
title: 在適用於身分識別的 Microsoft Defender 中設定 Syslog 設定
description: 說明如何讓適用於身分識別的 Microsoft Defender 在偵測到可疑活動時通知您 (透過電子郵件或適用於身分識別的 Defender 事件轉送)
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 10/27/2020
ms.topic: how-to
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 833b836c28455a231fa4a30afe2e604ce7646a16
ms.sourcegitcommit: e2227c0b0e5aaa5163dc56d4131ca82f8dca8fb0
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/18/2020
ms.locfileid: "94848970"
---
# <a name="integrate-with-syslog"></a>與 Syslog 整合

> [!NOTE]
> 此頁面所述的[!INCLUDE [Product long](includes/product-long.md)] 功能也可使用新的[入口網站](https://portal.cloudappsecurity.com)來存取。

[!INCLUDE [Product long](includes/product-long.md)] 可以在偵測到可疑活動時，透過指定的感應器將安全性與健康情況警示傳送到您的 Syslog 伺服器。

當您啟用 Syslog 通知後，即可進行下列設定：

|欄位|說明|
|---------|---------------|
|感應器|選取負責彙總所有 Syslog 事件，並將它們轉寄給您的 SIEM 伺服器的指定感應器。|
|服務端點|Syslog 伺服器的 FQDN，選擇性地變更連接埠號碼 (預設值 514)|
|傳輸|可以是 UDP、TCP 或 TLS (安全 Syslog)|
|格式|這是[!INCLUDE [Product short](includes/product-short.md)] 用來將事件傳送至 SIEM 伺服器的格式，其可以是 RFC 5424 或 RFC 3164。|

1. 設定 Syslog 通知前，請先洽詢您的 SIEM 系統管理員以了解下列資訊︰

    - SIEM 伺服器的 FQDN 或 IP 位址
    - SIEM 伺服器正在接聽的連接埠
    - 應使用的傳輸：UDP、TCP 或 TLS (安全 Syslog)
    - 要用來傳送資料 RFC 3164 或 5424 的格式

1. 開啟[!INCLUDE [Product short](includes/product-short.md)] 入口網站。
1. 按一下 [設定]。
1. 從 [通知和報告] 子功能表中，選取 [通知]。
1. 從 [Syslog 服務] 選項，按一下 [設定]。
1. 選取 [感應器]。
1. 輸入 [服務端點] URL。
1. 選取 [傳輸] 通訊協定 (TCP 或 UDP)。
1. 選取格式 (RFC 3164 或 RFC 5424)。
1. 選取 [傳送測試 Syslog 訊息]，然後確認您的 Syslog 基礎結構解決方案中已收到訊息。
1. 按一下 **[儲存]** 。

檢查或修改 Syslog 設定。

1. 按一下 [通知]，然後按一下 [Syslog 通知] 下的 [組態]，並輸入下列資訊：

    ![[!INCLUDE [Product short](includes/product-short.md)] Syslog 伺服器設定影像](media/syslog.png)

1. 您可以選取要傳送至 Syslog 伺服器的事件。 在 [Syslog 通知] 下，指定要傳送到 Syslog 伺服器的通知 (新的安全性警示、更新的安全性警示，以及新的健康狀態問題)。

> [!NOTE]
> 若您計劃為[!INCLUDE [Product short](includes/product-short.md)] SIEM 記錄建立自動化或指令碼，建議您使用 **externalId** 欄位來識別警示類型，而非使用警示名稱。 警示名稱有時候可能會遭到修改，但每個警示的 **externalId** 永遠不會變。 如需詳細資訊，請參閱[[!INCLUDE [Product short](includes/product-short.md)] SIEM 記錄參考](cef-format-sa.md)。

## <a name="see-also"></a>另請參閱

- [使用機密帳戶](sensitive-accounts.md)
- [查看[!INCLUDE [Product short](includes/product-short.md)] 論壇！](https://aka.ms/MDIcommunity)\(英文\)
