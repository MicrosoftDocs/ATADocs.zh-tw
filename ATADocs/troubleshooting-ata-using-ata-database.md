---
title: 使用資料庫針對 Advanced Threat Analytics 進行疑難排解 | Microsoft Docs
description: 描述如何使用 ATA 資料庫來協助疑難排解問題
keywords: ''
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 3/21/2018
ms.topic: conceptual
ms.prod: advanced-threat-analytics
ms.service: ''
ms.technology: ''
ms.assetid: 377a3c81-5c1d-486f-8942-85249aacf560
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: b3fb06733a2ba1c38aeb682cd6f8cc57a2ba1a3b
ms.sourcegitcommit: 65885bab8e31dd862a4f2ae9028fb31b288d7229
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/20/2018
ms.locfileid: "52157517"
---
*適用於：Advanced Threat Analytics 1.9 版*



# <a name="troubleshooting-ata-using-the-ata-database"></a>使用 ATA 資料庫疑難排解 ATA
ATA 會使用 MongoDB 作為其資料庫。
您可以使用預設命令列或使用者介面工具來與資料庫互動，以執行進階工作和疑難排解。

## <a name="interacting-with-the-database"></a>與資料庫互動
查詢資料庫的預設和最基本的方式是使用 Mongo 殼層︰

1.  開啟命令列視窗，並將路徑變更為 MongoDB 的 bin 資料夾。 預設路徑為︰**C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin**。

2.  執行：`mongo.exe ATA`。 請確定輸入全部大寫字母的 ATA。

> [!div class="mx-tableFixed"]
|作法|語法|附註|
|-------------|----------|---------|
|檢查資料庫中的集合。|`show collections`|可讓端對端測試有效查看正在寫入到資料庫的流量，及 ATA 正在接收的事件 4776。|
|取得使用者/電腦/群組 (UniqueEntity) 的詳細資料，例如使用者識別碼。|`db.UniqueEntity.find({CompleteSearchNames: "<name of entity in lower case>"})`||
|尋找來自特定日期的特定電腦中的 Kerberos 驗證流量。|`db.KerberosAs_<datetime>.find({SourceComputerId: "<Id of the source computer>"})`|若要取得 &lt;來源電腦的識別碼&gt;，您可以如此範例所示來查詢 UniqueEntity 集合。<br /><br />每個網路活動類型 (例如 Kerberos 驗證) 都有它自己的集合 (每個 UTC 日期)。|
|進行進階組態變更。 在此範例中，請將所有 ATA 閘道的傳送佇列大小變更為 10,000。|`db.SystemProfile.update( {_t: "GatewaySystemProfile"} ,`<br>`{$set:{"Configuration.EntitySenderConfiguration.EntityBatchBlockMaxSize" : "10000"}})`|`|

下列範例會提供使用先前所提供之語法的範例程式碼。 如果您正在調查 20/10/2015 發生的可疑活動 ，而且想要深入了解「John Doe」在那一天執行的 NTLM 活動︰<br /><br />首先，尋找「John Doe」的識別碼

`db.UniqueEntity.find({Name: "John Doe"})`<br>記下由 `_id` 的值所指出的識別碼。例如，假設識別碼為 `123bdd24-b269-h6e1-9c72-7737as875351`<br>然後，根據您正在尋找的日期 (在範例中為 20/10/2015)，搜尋日期與它最為接近的集合。<br>然後，搜尋 John Doe 的帳戶 NTLM 活動︰ 

`db.Ntlms_<closest date>.find({SourceAccountId: "123bdd24-b269-h6e1-9c72-7737as875351"})`

## <a name="see-also"></a>另請參閱
- [ATA 必要條件](ata-prerequisites.md)
- [ATA 容量規劃](ata-capacity-planning.md)
- [設定事件收集](configure-event-collection.md)
- [設定 Windows 事件轉送](configure-event-collection.md#configuring-windows-event-forwarding)
- [查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/home?forum=mata)
