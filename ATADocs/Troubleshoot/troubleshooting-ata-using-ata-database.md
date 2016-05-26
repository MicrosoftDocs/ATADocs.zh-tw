---
# required metadata

title: 使用 ATA 資料庫疑難排解 ATA | Microsoft Advanced Threat Analytics
description: 描述如何使用 ATA 資料庫來協助疑難排解問題 
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: d89e7aff-a6ef-48a3-ae87-6ac2e39f3bdb

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# 使用 ATA 資料庫疑難排解 ATA
ATA 會使用 MongoDB 作為其資料庫。
您可以使用預設命令列或使用者介面工具來與資料庫互動，以執行進階工作和疑難排解。

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
|搜尋的進階屬性，例如帳戶的使用中日期。 |`db.UniqueEntityProfile.find({UniqueEntityId: "<Id of the account>")`|若要取得 &lt;帳戶的識別碼&gt;，您可以如此範例所示來查詢 UniqueEntity 集合。<br>顯示帳戶已啟用的日期屬性名稱為：「ActiveDates」。 <br>
比方說，您可能想要知道帳戶是否具有至少 21 天的活動，讓異常行為機器學習演算法能夠在其上執行。|
|進行進階組態變更。 在此範例中，我們可將全部 ATA 閘道的傳送佇列大小變更為 10,000。|`db.SystemProfile.update( {_t: "GatewaySystemProfile"} ,`<br>`{$set:{"Configuration.EntitySenderConfiguration.EntityBatchBlockMaxSize" : "10000"}})`|`|

下列範例提供使用上述語法的範例程式碼。 如果您正在調查 20/10/2015 發生的可疑活動 ，而且想要深入了解「John Doe」在那一天執行的 NTLM 活動︰<br /><br />首先，尋找「John Doe」的識別碼

`db.UniqueEntity.find({Name: "John Doe"})`<br>記下其識別碼 (由「`_id`」值指示) 在我們的範例中，我們假設識別碼是「`123bdd24-b269-h6e1-9c72-7737as875351`」<br>然後，搜尋正在尋找的日期前最接近的日期集合，在我們的範例為 20/10/2015。<br>然後，搜尋 John Doe 的帳戶 NTLM 活動︰ 

`db.Ntlms_<closest date>.find({SourceAccountId: "123bdd24-b269-h6e1-9c72-7737as875351"})`
## ATA 設定檔
ATA 組態會儲存在資料庫的「SystemProfile 」集合中。
ATA 中心服務每隔一小時會將這個集合備份到名為「SystemProfile.json」的檔案。 這位於名為「Backup」的子資料夾中。 在預設的 ATA 安裝位置中，它可以在這裡找到︰**C:\Program Files\Microsoft Advanced Threat Analytics\Center\Backup\SystemProfile.json**。 

**注意**：建議在針對 ATA 進行重大變更時，在某處備份此檔案。

可執行下列命令來還原所有設定︰

`mongoimport.exe --db ATA --collection SystemProfile --file "<SystemProfile.json backup file>" --upsert`

## 另請參閱
- [ATA 必要條件](/advanced-threat-analytics/plan-design/ata-prerequisites)
- [ATA 容量規劃](/advanced-threat-analytics/plan-design/ata-capacity-planning)
- [設定事件收集](/advanced-threat-analytics/deploy-use/configure-event-collection)
- [設定 Windows 事件轉送](/advanced-threat-analytics/deploy-use/configure-event-collection#configuring-windows-event-forwarding)
- [查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)


<!--HONumber=May16_HO3-->


