---
title: "設定 ATA 通知 | Microsoft ATA"
description: "說明當 ATA 偵測到可疑的活動時，如何通知您 (透過電子郵件或 ATA 事件轉寄)"
keywords: 
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 14cb7513-5dc8-49cb-b3e0-94f469c443dd
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: a5c7163bc7b1989672e587bfb4fa6a65cd4e3751
ms.openlocfilehash: 5864070fe3ad5aedf1ff79d8386caba4b6a79adc


---

## 使用電子郵件伺服器設定提供 ATA
當 ATA 偵測到可疑的活動時，就會通知您。 若要讓 ATA 能夠傳送電子郵件通知，您必須先進行**電子郵件伺服器設定**。

1.  在 ATA 中央伺服器上，按一下桌面上的 [Microsoft Advanced Threat Analytics Management] 圖示。

2.  輸入您的使用者名稱和密碼，然後按一下 [登入]。

3.  選取工具列上的 [設定] 選項並選取 [組態]。

    ![ATA 組態設定圖示](media/ATA-config-icon.JPG)

4.  在 [一般] 索引標籤的 [電子郵件伺服器] 下，輸入下列資訊：

    |欄位|說明|值|
    |---------|---------------|---------|
    |SMTP 伺服器的端點 (必要)|輸入 SMTP 伺服器的 FQDN。|例如：<br />smtp.contoso.com|
    |SSL|如果 SMTP 伺服器需要 SSL，請切換 SSL。 **注意︰**如果啟用 SSL，您也需要變更連接埠號碼。|預設會停用|
    |驗證|如果您的 SMTP 伺服器需要驗證，請啟用。 **注意︰**如果您啟用驗證，您必須提供有權連接到 SMTP 伺服器的電子郵件帳戶的使用者名稱和密碼。|預設會停用|
    |傳送來源 (必要)|輸入電子郵件傳送者的電子郵件地址。|例如：<br />ATA@contoso.com|
    ![ATA 電子郵件伺服器設定影像](media/ATA-email-server.png)

## 使用 Syslog 伺服器設定提供 ATA
當 ATA 偵測到可疑的活動時，就會將通知傳送至 Syslog 伺服器來通知您。 如果您啟用 Syslog 通知，就可以為其進行下列設定。

1.  設定 Syslog 通知前，請先洽詢您的 SIEM 系統管理員以了解下列資訊︰

    -   SIEM 伺服器的 FQDN 或 IP 位址

    -   SIEM 伺服器正在接聽的連接埠

    -   要使用的傳輸：UDP、TCP 或 TLS (安全 Syslog)

    -   要用來傳送資料 RFC 3164 或 5424 的格式

2.  在 ATA 中央伺服器上，按一下桌面上的 [Microsoft Advanced Threat Analytics Management] 圖示。

3.  輸入您的使用者名稱和密碼，然後按一下 [登入]。

4.  選取工具列上的 [設定] 選項並選取 [組態]。

    ![ATA 組態設定圖示](media/ATA-config-icon.JPG)

5.  選取 [Syslog 伺服器]，然後輸入下列資訊：

    |欄位|說明|
    |---------|---------------|
    |Syslog 伺服器端點|Syslog 伺服器的 FQDN|
    |傳輸|可以是 UDC、TCP 或 TLS (安全 Syslog)|
    |格式|這是 ATA 用來將事件傳送至 SIEM 伺服器 - RFC 5424 或 RFC 3164 的格式。|





## 另請參閱
[查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Jul16_HO3-->


