---
# required metadata

title: 設定 ATA 警示 | Microsoft Advanced Threat Analytics
description: 說明當 ATA 偵測到可疑的活動時，如何警示您 (透過電子郵件或 ATA 事件轉送) 
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: 14cb7513-5dc8-49cb-b3e0-94f469c443dd

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 設定 ATA 警示
ATA 可在偵測到可疑的活動時警示您，方法是透過電子郵件或使用 ATA 事件轉送，並將事件轉送至您的 SIEM/syslog 伺服器。 如果您啟用一個或兩類警示，您可以為其進行下列設定。

> [!NOTE]
> -   包含連結的電子郵件通知，將使用者直接帶到偵測到的可疑活動。 連結的主機名稱部分是來自 [ATA 中心] 頁面的 [ATA 主控台 URL] 的設定。 根據預設，ATA 主控台 URL 是安裝 ATA 中心期間所選取的 IP 位址。  如果要設定電子郵件警示，建議您使用 FQDN 做為 ATA 主控台 URL。
> -   「系統健全狀況警示」警示只會透過電子郵件傳送。
> -   會從 ATA 中心將警示傳至 SMTP 伺服器和 Syslog 伺服器。
> -   只有在建立可疑活動時，才會傳送可疑活動的電子郵件警示。

## 設定語言和頻率
[語言]**** 設定適用於電子郵件傳送的通知，和傳送至 Syslog 伺服器的通知。

[頻率]**** 設定僅適用於傳送至 Syslog 伺服器的通知。

1.  開啟 ATA 主控台。

2.  選取工具列上的 [設定] 選項並選取 [組態]****。

    ![ATA 組態設定圖示](media/ATA-config-icon.JPG)

3.  選取 [警示]****。

4.  在 [語言]**** 下，選取您所選擇的語言。

5.  在 [頻率]**** 下，選取 [低頻]**** (如果只想在新警示產生時才收到簡短的通知)。 如果想要在產生新警示以及修改現有的警示時收到詳細通知，請選取 [高頻率]**** 。

    ![設定警示的詳細資訊影像](media/ATA-alerts-verbosity-language.png)

6.  按一下 [儲存] ****。

## 設定電子郵件警示
ATA 會警示您它偵測到可疑的活動。 如果您啟用電子郵件警示，您可以為其進行下列設定。

1.  在 ATA 中央伺服器上，按一下桌面上的 [Microsoft Advanced Threat Analytics Management]**** 圖示。

2.  輸入您的使用者名稱和密碼，然後按一下 [登入]****。

3.  選取工具列上的 [設定] 選項並選取 [組態]****。

    ![ATA 組態設定圖示](media/ATA-config-icon.JPG)

4.  選取 [警示]****。

5.  開啟 [郵件]**** 啟用電子郵件警示，並輸入下列資訊 ︰

    |欄位|說明|值|
    |---------|---------------|---------|
    |SMTP 伺服器的端點 (必要)|輸入 SMTP 伺服器的 FQDN。|例如：<br />smtp.contoso.com|
    |SSL|如果 SMTP 伺服器需要 SSL，請切換 SSL。 **注意︰**如果啟用 SSL，您也需要變更連接埠號碼。|預設會停用|
    |驗證|如果您的 SMTP 伺服器需要驗證，請啟用。 **注意︰**如果您啟用驗證，您必須提供有權連接到 SMTP 伺服器的電子郵件帳戶的使用者名稱和密碼。|預設會停用|
    |傳送來源 (必要)|輸入電子郵件傳送者的電子郵件地址。|例如：<br />ATA@contoso.com|
    |傳送至 (必要)|輸入當 ATA 偵測到可疑的活動時，必須取得電子郵件的使用者或電子郵件群組的電子郵件地址。 **注意 ︰**一次輸入一個電子郵件地址，然後按一下加號將它加入。|例如：<br />securityteam@contoso.com|

## 設定轉寄至 SIEM 的 ATA 事件
當 ATA 偵測到可疑的活動時，它會將警示傳送至 Syslog 伺服器來警示您。 如果您啟用 Syslog 警示，您可以為其進行下列設定。

1.  設定 Syslog 警示時，使用您的 SIEM 系統管理員以瞭解下列資訊︰

    -   SIEM 伺服器的 FQDN 或 IP 位址

    -   SIEM 伺服器正在接聽的連接埠

    -   要使用 UDP 或 TCP 或安全 TCP 的傳輸

    -   要用來傳送資料 RFC 3164 或 5424 的格式

2.  在 ATA 中央伺服器上，按一下桌面上的 [Microsoft Advanced Threat Analytics Management]**** 圖示。

3.  輸入您的使用者名稱和密碼，然後按一下 [登入]****。

4.  選取工具列上的 [設定] 選項並選取 [組態]****。

    ![ATA 組態設定圖示](media/ATA-config-icon.JPG)

5.  選取 [警示]****。

6.  開啟 [Syslog]**** 來啟用將可疑活動的相關警示傳至 Syslog 伺服器，並輸入下列資訊 ︰

    |欄位|說明|
    |---------|---------------|
    |Syslog 伺服器端點|Syslog 伺服器的 FQDN|
    |傳輸|可以是 UDC、TCP 或安全 TCP|
    |格式|這是 ATA 用來將事件傳送至 SIEM 伺服器 - RFC 5424 或 RFC 3164 的格式。|

## 另請參閱
[如需支援，請查看我們的論壇！](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=Apr16_HO2-->


