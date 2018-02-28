---
title: "在 Azure 進階威脅防護中設定電子郵件通知設定 | Microsoft Docs"
description: "說明當 Azure ATP 偵測到可疑的活動時，如何通知您 (透過電子郵件或 Azure ATP 事件轉寄)"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 2/21/2018
ms.topic: article
ms.prod: 
ms.service: azure-advanced-threat-protection
ms.technology: 
ms.assetid: a2d29c9c-7ecb-4804-b74b-fde899b28648
ms.reviewer: itargoet
ms.suite: ems
ms.openlocfilehash: 74fe9976df769ae01c58a5d66ca491c3fa8958d9
ms.sourcegitcommit: 03e959b7ce4b6df421297e1872e028793c967302
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/21/2018
---
適用於：Azure 進階威脅防護



# <a name="integrate-with-syslog"></a>與 Syslog 整合

當 Azure ATP 偵測到可疑的活動與健康狀態警示時，就會將通知傳送至 Syslog 伺服器來通知您。 如果您啟用 Syslog 通知，就可以為其進行下列設定。

1.  設定 Syslog 通知前，請先洽詢您的 SIEM 系統管理員以了解下列資訊︰

    -   SIEM 伺服器的 FQDN 或 IP 位址

    -   SIEM 伺服器正在接聽的連接埠

    -   要使用的傳輸：UDP、TCP 或 TLS (安全 Syslog)

    -   要用來傳送資料 RFC 3164 或 5424 的格式

2.  輸入工作區入口網站 URL。

3.  輸入您的 Azure Active Directory 使用者名稱和密碼，然後按一下 [登入]。

4.  選取工具列上的 [設定] 選項並選取 [組態]。

    ![Azure ATP 組態設定圖示](media/ATP-config-menu.png)

5.  按一下 [通知]，然後按一下 [Syslog 通知] 下的 [組態]，並輸入下列資訊：

    |欄位|說明|
    |---------|---------------|
    |感應器|選取負責彙總所有 Syslog 事件，並將它們轉寄給您的 SIEM 伺服器的指定感應器。|
    |服務端點|Syslog 伺服器的 FQDN，選擇性地變更連接埠號碼 (預設值 514)|
    |傳輸|可以是 UDP、TCP 或 TLS (安全 Syslog)|
    |格式|這是 Azure ATP 用來將事件傳送至 SIEM 伺服器 - RFC 5424 或 RFC 3164 的格式。|

 ![Azure ATP Syslog 伺服器設定影像](media/atp-syslog.png)

6. 您可以選取要傳送至 Syslog 伺服器的事件。 在 [Syslog 通知] 下，指定要傳送到 Syslog 伺服器的通知 (新的安全性警示、更新的安全性警示，以及新的健康狀態問題)。


## <a name="see-also"></a>另請參閱

- [使用機密帳戶](sensitive-accounts.md)
- [查看 ATP 論壇！](https://aka.ms/azureatpcommunity)\(英文\)