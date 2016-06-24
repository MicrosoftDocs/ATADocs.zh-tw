---
# required metadata

title: ATA 1.6 版的新功能 | Microsoft Advanced Threat Analytics
description: 列出 ATA 1.6 版的新功能以及已知問題
keywords:
author: rkarlin
manager: stevenpo
ms.date: 04/28/2016
ms.topic: article
ms.prod: identity-ata
ms.service: advanced-threat-analytics
ms.technology: security
ms.assetid: a0d64aff-ca9e-4300-b3f8-eb3c8b8ae045

# optional metadata

#ROBOTS:
#audience:
#ms.devlang:
ms.reviewer: bennyl
ms.suite: ems
#ms.tgt_pltfrm:
#ms.custom:

---

# ATA 1.6 版的新功能
這些版本資訊提供此版 Advanced Threat Analytics 中已知問題的相關資訊。

## ATA 1.6 更新有什麼新功能？
ATA 1.6 的更新提供下列各方面的改良︰

-   新增偵測

-   改進現有偵測

-   ATA 輕量型閘道

-   自動更新

-   提升的 ATA 中心效能

-   降低儲存體需求

-   支援 IBM QRadar

### 新增偵測


- **惡意的資料保護私人資訊要求**：資料保護 API (DPAPI) 是使用密碼的資料保護服務。 有多種應用程式都使用此保護服務來儲存使用者的密碼，例如網站密碼和檔案共用認證。 為了在密碼遺失的情況下提供支援，使用者可以使用與密碼無關的修復金鑰，來解密受保護的資料。 在網域環境中，攻擊者可以從遠端竊取修復金鑰，並用來解密所有加入網域之電腦上受保護的資料。


- **Net Session 列舉**：探查是進階攻擊鏈中的重要階段。 網域控制站 (DC) 可作為檔案伺服器，透過伺服器訊息區 (SMB) 通訊協定，來達成散發群組原則物件的目的。 在探查階段階段中，攻擊者可以查詢伺服器上所有使用中 SMB 工作階段的 DC，進而取得與這些 SMB 工作階段相關聯的所有使用者和 IP 位址。 攻擊者可以使用 SMB 工作階段列舉來鎖定敏感性帳戶，此舉有助於他們在網路間橫向移動。


- **惡意的複寫要求**：在 Active Directory 環境中，網域控制站之間會定期發生複寫。 攻擊者可以假冒 Active Directory 複寫要求 (有時假冒網域控制站)，藉此擷取儲存在 Active Directory 中的資料 (包括密碼雜湊)，而不需要使用磁碟區陰影複製等較具侵入性的技術。


- **MS11-013 弱點偵測**：Kerberos 中因權限提高而出現弱點，讓 Kerberos 服務票證的特定部分可被偽造。 成功惡意探索此弱點的惡意使用者或攻擊者，可以取得網域控制站上權限提高的權杖。


- **不尋常的通訊協定實作**：驗證要求 (Kerberos 或 NTLM) 通常使用一組標準的方法和通訊協定來執行。 不過，為了成功進行驗證，要求只能符合一組特定的需求。 攻擊者可能會在環境中，以稍微偏離標準實作的方式來實作這些通訊協定。 這些偏差可能表示攻擊者嘗試執行 Pass-The-Hash、暴力密碼破解等攻擊。


### 改進現有偵測
ATA 1.6 包含改良的偵測邏輯，可減少 Golden Ticket、Honey Token、暴力密碼破解和遠端執行等現有偵測的誤判和誤否定情況。

### ATA 輕量型閘道
此版 ATA 引進新的 ATA 閘道部署選項，以便直接在網域控制站上安裝 ATA 閘道。 此部署選項移除了 ATA 閘道的非必要性功能，並引進以 DC 上可用資源為基礎的動態資源管理，以確保 DC 的現有作業不受影響。 ATA 輕量型閘道可降低 ATA 部署的成本。 同時可讓您更輕鬆地在分支網站中進行部署，這些分支網站中的硬體資源容量有限，或是無法設定連接埠鏡像支援。
如需 ATA 輕量型閘道的詳細資訊，請參閱 [ATA 架構](/advanced-threat-analytics/plan-design/ata-architecture#ata-gateway-and-ata-lightweight-gateway)

如需部署考量的詳細資訊，以選擇適合您的閘道類型，請參閱 [ATA 容量規劃](/advanced-threat-analytics/plan-design/ata-capacity-planning#choosing-the-right-gateway-type-for-your-deployment)


### 自動更新
從 1.6 版開始，您可以使用 Microsoft Update 更新 ATA 中心。 此外，ATA 閘道現在可以使用自己與 ATA 中心的標準通訊通道來自動更新。
### 提升的 ATA 中心效能
在此版本中，執行所有偵測的資料庫負載更少且執行方式的效率更高，因此單一 ATA 中心可以監視的網域控制站更多。

### 降低儲存體需求
ATA 1.6 執行 ATA 資料庫所需的儲存空間大幅減少，現在只需要舊版所用儲存空間的 20%。

### 支援 IBM QRadar
除了先前支援的 SIEM 解決方案之外，ATA 現在也可以從 IBM 的 QRadar SIEM 解決方案接收事件。

## 已知問題
下列已知問題存在於此版本中。

### 無法在手動移動的資料庫辨識新路徑

在手動移動資料庫路徑的部署中，ATA 部署不會使用新的資料庫路徑進行更新。 這可能會導致下列問題︰


- ATA 可能會使用 ATA 中心的系統磁碟機中所有可用空間，而不會循環刪除舊的網路活動。


- 將 ATA 更新至 1.6 版時，更新前的整備檢查可能會失敗，如下圖所示。
    ![整備檢查失敗](media/ata_failed_readinesschecks.png)
    >[!Important]
將 ATA 更新至 1.6 版之前，請使用正確的資料庫路徑更新下列登錄機碼︰  `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Microsoft Advanced Threat Analytics\Center\DatabaseDataPath`

### 從 ATA 1.5 更新時的移轉失敗
更新至 ATA 1.6 時，更新程序可能會失敗，並出現下列錯誤碼：

![將 ATA 更新至 1.6 錯誤](http://i.imgur.com/QrLSApr.png) 如果您看到此錯誤，請檢閱 **C:\Users\<使用者>\AppData\Local\Temp** 中的部署記錄，並尋找下列例外狀況︰

    System.Reflection.TargetInvocationException: Exception has been thrown by the target of an invocation. ---> MongoDB.Driver.MongoWriteException: A write operation resulted in an error. E11000 duplicate key error index: ATA.UniqueEntityProfile.$_id_ dup key: { : "<guid>" } ---> MongoDB.Driver.MongoBulkWriteException`1: A bulk write operation resulted in one or more errors.  E11000 duplicate key error index: ATA.UniqueEntityProfile.$_id_ dup key: { : " <guid> " }

您也可能會看到此錯誤︰System.ArgumentNullException: 不能是 Null。
    
如果您看到上述任一錯誤，請執行下列因應措施。

**因應措施**： 

1.  將 "data_old" 資料夾移至暫存資料夾 (通常位於 %ProgramFiles%\Microsoft Advanced Threat Analytics\Center\MongoDB\bin)。
2.  解除安裝 ATA 中心 v1.5，並刪除所有資料庫資料。
![解除安裝 ATA 1.5](http://i.imgur.com/x4nJycx.png)
3.  重新安裝 ATA 中心 v1.5。 請務必使用與先前 ATA 1.5 安裝相同的設定 (憑證、IP 位址、DB 路徑等)。
4.  依下列順序停止這些服務：
    1.  Microsoft Advanced Threat Analytics 中心
    2.  MongoDB
5.  以 “data_old” 資料夾中的檔案取代 MongoDB 資料庫檔案。
6.  依下列順序啟動這些服務：
    1.  MongoDB
    2.  Microsoft Advanced Threat Analytics 中心
7.  檢閱記錄以驗證產品正在執行，而且未發生錯誤。
8.  [下載](http://aka.ms/ataremoveduplicateprofiles "下載") "RemoveDuplicateProfiles.exe" 工具，然後將其複製到主要安裝路徑 (%ProgramFiles%\Microsoft Advanced Threat Analytics\Center)
9.  從提升權限的命令提示字元執行 “RemoveDuplicateProfiles.exe”，並等候其成功完成。
10. 從這裡：…\Microsoft Advanced Threat Analytics\Center\MongoDB\bin 目錄：**Mongo ATA**，輸入下列命令：

    db.SuspiciousActivities.remove({ "_t" : "RemoteExecutionSuspiciousActivity", "DetailsRecords" : { "$elemMatch" : { "ReturnCode" : null } } }, { "_id" : 1 });

![更新因應措施](http://i.imgur.com/Nj99X2f.png)

這應該會傳回 WriteResult({ "nRemoved" : XX })，其中 “XX” 是已刪除的可疑活動數目。 如果數目大於 0，請結束命令提示字元，並繼續進行更新程序。


### .Net Framework 4.6.1 需要重新啟動伺服器

在某些情況下，安裝 .Net Framework 4.6.1 可能需要您重新啟動伺服器。 請注意，在 [Microsoft Advanced Threat Analytics 中心安裝程式] 對話方塊中按一下 [確定] 將會自動重新啟動伺服器。 當您在網域控制站上安裝 ATA 輕量型閘道時，這一點特別重要，因為您可能需要在安裝前規劃維護期間。
    ![.NET Framework 重新啟動](media/ata-net-framework-restart.png)

### 不再移轉歷史網路活動
此版 ATA 提供改良的偵測引擎，因此可提供更精確的偵測，並減少許多誤判的情況，特別是針對 Pass-the-Hash。
改良後的新偵測引擎利用內嵌偵測技術，不需要存取歷史網路活動就能進行偵測，因此大幅提升 ATA 中心的效能。 這也表示不需要在更新程序期間移轉歷史網路活動。
ATA 更新程序會將資料匯出至 `<Center Installation Path>\Migration` 成為 JSON 檔案，以供您未來進行調查使用。

## 另請參閱
[查看 ATA 論壇！](https://social.technet.microsoft.com/Forums/security/en-US/home?forum=mata)

[將 ATA 更新至 1.6 版 - 移轉指南](ata-update-1.6-migration-guide.md)

<!--HONumber=May16_HO4-->


