---
title: "設定 ATA 通知 | Microsoft Docs"
description: "描述如何設定 ATA 警示，所以偵測到可疑的活動時，您會收到通知。"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 11/29/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 14cb7513-5dc8-49cb-b3e0-94f469c443dd
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 7dc860fe31da1374a4466f8e56e55e6520bc10dc
ms.openlocfilehash: f069f910e99c537e08b34b9a0b65aab7dcd08452


---

*適用於︰Advanced Threat Analytics 1.7 版*



# <a name="set-ata-notifications"></a>設定 ATA 通知
ATA 可在偵測到可疑的活動時通知您，方法是透過電子郵件或使用 ATA 事件轉寄，並將事件轉寄到您的 SIEM/syslog 伺服器。 您必須先[設定電子郵件伺服器和 Syslog 伺服器](setting-syslog-email-server-settings.md)，才能選取要接收的通知。

> [!NOTE]
> -   包含連結的電子郵件通知，將使用者直接帶到偵測到的可疑活動。 連結的主機名稱部分是來自 [ATA 中心] 頁面的 [ATA 主控台 URL] 的設定。 根據預設，ATA 主控台 URL 是安裝 ATA 中心期間所選取的 IP 位址。  如果要設定電子郵件通知，建議您使用 FQDN 作為 ATA 主控台 URL。
> -   通知會從 ATA 中心傳送到 SMTP 伺服器和 Syslog 伺服器。

## <a name="mail-notifications"></a>郵件通知
若要接收郵件通知，請設定下列項目：


1. 在 ATA 主控台中，選取工具列上的 [設定] 選項，然後選取 [設定]。
![ATA 組態設定圖示](media/ATA-config-icon.JPG)

2. 在 [通知] 區段下，選取 [設定]。
3. 在 [郵件收件者]下，指定將透過電子郵件接收通知的收件者。
>   [!NOTE]
>   只有在建立可疑活動時，才會傳送可疑活動的電子郵件警示。

4. 在 [通知時機:] 下，使用切換鍵來選取應該傳送的通知︰
  - 偵測到新的可疑活動
  - 偵測到新的健康情況問題
  - 有新的軟體更新可用

5. 按一下 [儲存]。

![ATA 郵件通知設定影像](media/ATA-mail-notification-settings-1.7.png)


## <a name="syslog-notification"></a>Syslog 通知

若要接收 Syslog 通知，請設定下列項目：


1. 在 ATA 主控台中，選取工具列上的 [設定] 選項，然後選取 [設定]。
![ATA 組態設定圖示](media/ATA-config-icon.JPG)

2. 在 [通知] 區段下，選取 [設定]。
3. 在 **[Syslog notifications (Syslog 通知)]** 下，使用切換鍵來選取應該傳送的通知︰


    - 偵測到新的可疑活動
    - 現有的可疑活動已更新
    - 偵測到新的健康情況問題
5. 按一下 **[儲存]**。

![ATA 通知設定影像](media/ATA-syslog-notification-settings-1.7.png)




## <a name="see-also"></a>另請參閱
[查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Nov16_HO5-->


