---
title: "設定 Advanced Threat Analytics 通知 | Microsoft Docs"
description: "描述如何設定 ATA 警示，所以偵測到可疑的活動時，您會收到通知。"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 6/12/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 14cb7513-5dc8-49cb-b3e0-94f469c443dd
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: cc7f5d2e75076b1f684ad76daca9ceb35e0d30e3
ms.sourcegitcommit: 470675730967e0c36ebc90fc399baa64e7901f6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/30/2017
---
適用於︰Advanced Threat Analytics 1.8 版



<a id="set-ata-notifications" class="xliff"></a>

# 設定 ATA 通知
ATA 可在偵測到可疑的活動時通知您，方法是透過電子郵件或使用 ATA 事件轉寄，並將事件轉寄到您的 SIEM/syslog 伺服器。 您必須先[設定電子郵件伺服器和 Syslog 伺服器](setting-syslog-email-server-settings.md)，才能選取要接收的通知。

> [!NOTE]
> -   包含連結的電子郵件通知，將使用者直接帶到偵測到的可疑活動。 連結的主機名稱部分是來自 [ATA 中心] 頁面的 [ATA 主控台 URL] 的設定。 根據預設，ATA 主控台 URL 是安裝 ATA 中心期間所選取的 IP 位址。  如果要設定電子郵件通知，建議您使用 FQDN 作為 ATA 主控台 URL。
> -   通知會從 ATA 中心傳送到 SMTP 伺服器和 Syslog 伺服器。


若要接收通知，請設定下列項目：


1. 在 ATA 主控台中，選取工具列上的 [設定] 選項，然後選取 [設定]。

![ATA 組態設定圖示](media/ATA-config-icon.png)

2. 在 [Notifications & Reports (通知與報表)] 區段中，選取 [通知]。
3. 在 [郵件通知] 下，指定要透過電子郵件傳送的通知 - 新的可疑活動和新的健康狀態問題。 您可以為所要傳送的可疑活動和健康狀態警示設定個別電子郵件地址，例如，您可以將可疑活動通知傳送給安全性分析師，並將健康狀態警示通知傳送給 IT 系統管理員。
>   [!NOTE]
>   只有在建立可疑活動時，才會傳送可疑活動的電子郵件警示。
3. 在 [Syslog notifications (Syslog 通知)] 下，指定要傳送到 Syslog 伺服器的通知 - 新的可疑活動、更新的可疑活動和新的健康狀態問題。
5. 按一下 [儲存]。

![ATA 郵件通知設定影像](media/ata-mail-notification-settings.png)




<a id="see-also" class="xliff"></a>

## 另請參閱
[查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
