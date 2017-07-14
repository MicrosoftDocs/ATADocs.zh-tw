---
title: "使用資料庫針對 Advanced Threat Analytics 進行疑難排解 | Microsoft Docs"
description: "描述如何使用 ATA 資料庫來協助疑難排解問題"
keywords: 
author: rkarlin
ms.author: rkarlin
manager: mbaldwin
ms.date: 6/23/2017
ms.topic: article
ms.prod: 
ms.service: advanced-threat-analytics
ms.technology: 
ms.assetid: 377a3c81-5c1d-486f-8942-85249aacf560
ms.reviewer: bennyl
ms.suite: ems
ms.openlocfilehash: 112ee57f79b20b4e42b15c6fdc4566bbdcebe29f
ms.sourcegitcommit: 470675730967e0c36ebc90fc399baa64e7901f6b
ms.translationtype: HT
ms.contentlocale: zh-TW
ms.lasthandoff: 06/30/2017
---
適用於︰Advanced Threat Analytics 1.8 版



<a id="troubleshooting-ata-using-the-ata-database" class="xliff"></a>

# 使用 ATA 資料庫疑難排解 ATA
ATA 會使用 MongoDB 作為其資料庫。
您可以使用預設命令列或使用者介面工具來與資料庫互動，以執行進階工作和疑難排解。

<a id="interacting-with-the-database" class="xliff"></a>

## 與資料庫互動
查詢資料庫的預設和最基本的方式是使用 Mongo 殼層︰

1.  開啟命令列視窗，並將路徑變更為 MongoDB bin 資料夾。 預設路徑為︰**C:\Program Files\Microsoft Advanced Threat Analytics\Center\MongoDB\bin**。

2.  執行：`mongo.exe ATA`。 請確定輸入全部大寫字母的 ATA。

|作法|語法|附註|
|-------------|----------|---------|
|檢查資料庫中的集合。|`show collections`|可讓端對端測試有效查看正在寫入到資料庫的流量，及 ATA 正在接收的事件 4776。|
|取得使用者/電腦/群組 (UniqueEntity) 的詳細資料，例如使用者識別碼。|`db.UniqueEntity.find({SearchNames: "<name of entity in lower case>"})`||
|尋找來自特定日期的特定電腦中的 Kerberos 驗證流量。|`db.KerberosAs_<datetime>.find({SourceComputerId: "<Id of the source computer>"})`|若要取得 &lt;來源電腦的識別碼&gt;，您可以如此範例所示來查詢 UniqueEntity 集合。<br /><br />每個網路活動類型 (例如 Kerberos 驗證) 都有它自己的集合 (每個 UTC 日期)。|
|尋找源自於特定日期上特定帳戶所相關的特定電腦的 NTLM 流量。|`db.Ntlm_<datetime>.find({SourceComputerId: "<Id of the source computer>", SourceAccountId: "<Id of the account>"})`|若要取得 &lt;來源電腦的識別碼&gt; 和 &lt;帳戶的識別碼&gt;，您可以如此範例所示來查詢 UniqueEntity 集合。<br /><br />每個網路活動類型 (例如 NTLM 驗證) 都有它自己的集合 (每個 UTC 日期)。|
|搜尋的進階屬性，例如帳戶的使用中日期。 |`db.UniqueEntityProfile.find({UniqueEntityId: "<Id of the account>")`|若要取得 &lt;帳戶的識別碼&gt;，您可以如此範例所示來查詢 UniqueEntity 集合。<br>顯示帳戶已啟用的日期屬性名稱為：「ActiveDates」。 比方說，您可能想要知道帳戶是否具有至少 21 天的活動，讓異常行為機器學習演算法能夠在其上執行。|
|進行進階組態變更。 在此範例中，我們可將全部 ATA 閘道的傳送佇列大小變更為 10,000。|`db.SystemProfile.update( {_t: "GatewaySystemProfile"} ,`<br>`{$set:{"Configuration.EntitySenderConfiguration.EntityBatchBlockMaxSize" : "10000"}})`|`|

下列範例提供使用上述語法的範例程式碼。 如果您正在調查 20/10/2015 發生的可疑活動 ，而且想要深入了解「John Doe」在那一天執行的 NTLM 活動︰<br /><br />首先，尋找「John Doe」的識別碼

`db.UniqueEntity.find({Name: "John Doe"})`<br>記下 `_id` 的值所代表的識別碼。在我們的範例中，假設該識別碼為 `123bdd24-b269-h6e1-9c72-7737as875351`<br>然後，搜尋正在尋找的日期前最接近的日期集合，在我們的範例為 20/10/2015。<br>然後，搜尋 John Doe 的帳戶 NTLM 活動︰ 

`db.Ntlms_<closest date>.find({SourceAccountId: "123bdd24-b269-h6e1-9c72-7737as875351"})`

<a id="see-also" class="xliff"></a>

## 另請參閱
- [ATA 必要條件](ata-prerequisites.md)
- [ATA 容量規劃](ata-capacity-planning.md)
- [設定事件收集](configure-event-collection.md)
- [設定 Windows 事件轉送](configure-event-collection.md#configuring-windows-event-forwarding)
- [查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/home?forum=mata)