---
title: 在 Azure 進階威脅防護中設定 Syslog 設定
description: 說明當 Azure ATP 偵測到可疑的活動時，如何通知您 (透過電子郵件或 Azure ATP 事件轉寄)
keywords: ''
author: shsagir
ms.author: shsagir
manager: shsagir
ms.date: 09/16/2019
ms.topic: conceptual
ms.collection: M365-security-compliance
ms.service: azure-advanced-threat-protection
ms.assetid: a2d29c9c-7ecb-4804-b74b-fde899b28648
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 5a7d5fbaf2313b6876c2fbdcc6bde84aaa89cbd5
ms.sourcegitcommit: fbb0768c392f9bccdd7e4adf0e9a0303c8d1922c
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/15/2020
ms.locfileid: "84775874"
---
# <a name="integrate-with-syslog"></a>與 Syslog 整合

> [!NOTE]
> 此頁面所述的 Azure ATP 功能也可使用新的[入口網站](https://portal.cloudappsecurity.com)來存取。

Azure ATP 可以在偵測到可疑活動時，透過指定的感應器將安全性和健康狀態警示傳送到 Syslog 伺服器。

當您啟用 Syslog 通知後，即可進行下列設定：

   |欄位|說明|
   |---------|---------------|
   |感應器|選取負責彙總所有 Syslog 事件，並將它們轉寄給您的 SIEM 伺服器的指定感應器。|
   |服務端點|Syslog 伺服器的 FQDN，選擇性地變更連接埠號碼 (預設值 514)|
   |傳輸|可以是 UDP、TCP 或 TLS (安全 Syslog)|
   |格式|這是 Azure ATP 用來將事件傳送至 SIEM 伺服器 - RFC 5424 或 RFC 3164 的格式。|

1. 設定 Syslog 通知前，請先洽詢您的 SIEM 系統管理員以了解下列資訊︰

    - SIEM 伺服器的 FQDN 或 IP 位址
    - SIEM 伺服器正在接聽的連接埠
    - 應使用的傳輸：UDP、TCP 或 TLS (安全 Syslog)
    - 要用來傳送資料 RFC 3164 或 5424 的格式

1. 開啟 Azure ATP 入口網站。
1. 按一下 [設定]。
1. 從 [通知和報告] 子功能表中，選取 [通知]。
1. 從 [Syslog 服務] 選項，按一下 [設定]。
1. 選取 [感應器]。
1. 輸入 [服務端點] URL。
1. 選取 [傳輸] 通訊協定 (TCP 或 UDP)。
1. 選取格式 (RFC 3164 或 RFC 5424)。
1. 選取 [傳送文字 Syslog 訊息]，然後確認您的 Syslog 基礎結構解決方案中有收到訊息。
1. 按一下 **[儲存]** 。

檢查或修改 Syslog 設定。

1. 按一下 [通知]，然後按一下 [Syslog 通知] 下的 [組態]，並輸入下列資訊：

   ![Azure ATP Syslog 伺服器設定影像](media/atp-syslog.png)

1. 您可以選取要傳送至 Syslog 伺服器的事件。 在 [Syslog 通知] 下，指定要傳送到 Syslog 伺服器的通知 (新的安全性警示、更新的安全性警示，以及新的健康狀態問題)。

> [!NOTE]
> 若您計劃為 Azure ATP SIEM 記錄檔建立自動化或指令碼，建議您使用 **externalId** 欄位來識別警示類型，而非使用警示名稱。 警示名稱有時候可能會遭到修改，但每個警示的 **externalId** 永遠不會變。 如需詳細資訊，請參閱 [Azure ATP SIEM 記錄檔參考](cef-format-sa.md)。

## <a name="see-also"></a>另請參閱

- [使用機密帳戶](sensitive-accounts.md)
- [查看 Azure ATP 論壇！](https://aka.ms/azureatpcommunity)
