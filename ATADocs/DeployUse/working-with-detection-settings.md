---
title: "使用 ATA 偵測設定 | Microsoft Docs"
description: "描述如何為具備異常情況且應該在網路上利用與其他實體不同方式處理的 IP 位址和子網路設定清單"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 08/24/2016
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: f4f2ae30-4849-4a4f-8f6d-bfe99a32c746
ms.reviewer: bennyl
ms.suite: ems
translationtype: Human Translation
ms.sourcegitcommit: 85e285c5d88e5916e0bf0eb7dd327cb4cb45b4cb
ms.openlocfilehash: 93f2a72c9623674c73b3ee83ecf12be8e0766365


---

適用於︰Advanced Threat Analytics 1.7 版



# <a name="working-with-ata-detection-settings"></a>使用 ATA 偵測設定
[偵測] 組態頁面可讓您為具備異常情況且應該在網路上利用與其他實體不同方式處理的 IP 位址和子網路設定清單。

## <a name="setting-up-detection"></a>設定偵測
在 [偵測] 區段中，您可以定義下列項目︰

-   **Honeytoken 帳戶 SID** – 這是應該沒有任何網路活動的使用者帳戶。 此帳戶將會設定為 ATA Honeytoken 使用者。 如果有人嘗試使用此使用者帳戶，ATA 會建立可疑活動，而且是惡意活動的指示。 若要設定 Honeytoken 使用者，您需要使用者帳戶的 SID，而不是使用者名稱。

>[!NOTE]
> 您可以在 ATA 主控台中使用者設定檔的 [帳戶資訊] 索引標籤上找到使用者的 SID。


![ATA 偵測設定 honeytoken](media/ata-detection-settings-honeytoken-1.7.png)


**偵測排除項目** - 您可以從下列偵測排除 IP 位址。 如果您在其中一個清單中輸入 IP 位址，ATA 會從此特定類型的偵測活動排除該 IP 位址。

-   DNS 探查 IP 位址排除項目

-   傳遞票證 IP 位址排除項目

![ATA 偵測設定排除項目](media/ata-detection-settings-exclusions-1.7.png)


## <a name="see-also"></a>另請參閱
- [處理可疑活動](working-with-suspicious-activities.md)
- [修改 ATA 組態](modifying-ata-configuration.md)
- [查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/home?forum=mata)



<!--HONumber=Jan17_HO1-->


