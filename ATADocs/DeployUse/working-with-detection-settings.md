---
# required metadata

title: 使用 ATA 偵測設定 | Microsoft Advanced Threat Analytics
description: 描述如何為具備異常情況且應該在網路上利用與其他實體不同方式處理的 IP 位址和子網路設定清單
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: f4f2ae30-4849-4a4f-8f6d-bfe99a32c746

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 使用 ATA 偵測設定
[偵測] 組態頁面可讓您為具備異常情況且應該在網路上利用與其他實體不同方式處理的 IP 位址和子網路設定清單。

## 設定偵測
在 [偵測] 頁面中，您可以定義下列項目︰

-   **短期租用子網路** - 如果您的組織有任何子網路的 IP 位址非常短期，例如 VPN IP 位址子網路或 Wi-Fi 子網路，請務必將這些 IP 位址和子網路輸入 ATA，以便 ATA 了解從這些範圍儲存電腦和 IP 位址之間的關聯，儲存時間比其他 IP 位址還短。

-   **Honeytoken 帳戶 SID** – 這是應該沒有任何網路活動的使用者帳戶。 此帳戶將會設定為 ATA Honeytoken 使用者。 如果有人嘗試使用此使用者帳戶，ATA 會建立可疑活動，而且是惡意活動的指示。 若要設定 Honeytoken 使用者，您需要使用者帳戶的 SID，而不是使用者名稱。

您可以從下列偵測排除 IP 位址。 如果您在其中一個清單中輸入 IP 位址，ATA 會從此特定類型的偵測活動排除該 IP 位址。

-   DNS 探察 IP 位址排除項目

-   傳遞票證 IP 位址排除項目

## 另請參閱
- [處理可疑活動](working-with-suspicious-activities.md)
- [修改 ATA 組態](modifying-ata-configuration.md)
- [查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO1-->


